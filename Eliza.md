# Eliza

## 可以做什么？

个性化的 AI 助手（媒体处理、图像分析、财务助手等等）

核心：让 AI 玩角色扮演（但没这么简单，相当于现在的 AI 在做实际任务时做的不够好，**用架构来帮助 ai 在某一特定领域做的更好**，帮用户解决某些特定任务）

## 架构

![image-20250305155138479](/Users/qing/Library/Application Support/typora-user-images/image-20250305155138479.png)

当用户与 AI Agent 交互时，客户端接收消息并将其转发给执行环境，后者根据角色文件配置处理该消息。执行环境加载相关的记忆和知识，使用动作和评估器来决定如何回应，通过提供者获取额外的上下文。然后，执行环境使用 AI 模型生成回应，存储新的记忆，并将回应通过客户端发送回来。

## 插件安装

eliza 有一个插件市场，有很多人开发的插件，可以拿来即用。

- 安装方法为：

  在 eliza 项目中使用

  ```bash
  npx elizaos plugins list						'获取插件列表'
  npx elizaos plugins add ['插件名']		'安装特定插件'
  ```
  
  对应插件就会安装在项目的 packages 文件下，有自己的版本于依赖，彼此独立。
  
  还需要在 package.json 里手动添加
  
  ```json
  {
  	"dependencies": {
    	"@elizaos-plugins/client-wechat": "github:aiqubits/client-wechat",
    }
  }
  ```
  
  具体的写法可以参考
  
  [插件市场](https://elizaos.github.io/eliza/showcase) - 查看插件文档与仓库
  
  [elizaOS 插件注册表](https://github.com/elizaos-plugins/registry/blob/main/index.json) - 拷贝需要的插件粘贴到依赖位置
  
- 插件使用：

  给角色文件的 plugins 字段内填入要使用的插件。当然具体还要根据插件要求做额外配置。

## 代理运行环境 AgentRuntime

是 Eliza 代理的核心运行时环境。它**负责处理消息、状态管理、插件集成以及与外部服务的交互。**

- 运行流程：

1. 加载角色配置、插件与服务
2. 接收消息、编写状态（接收用户输入）
3. 处理动作并评估（访问数据库、调用api、数据处理等）
4. 生成并执行响应，然后评估
5. 更新内存与状态

ElizaOS 中 需要调用 LLM 的地方本质上是根据对应模板，让 LLM 按特定格式 json 返回信息去做处理。

### 1. 提供器 Provider

提供器 Provider 相当于人类的眼睛、鼻子、嘴巴，即 AI 代理**获取信息的手段**。

- Eliza 如何使用 Provider

  如果我们直接用 chatgpt 这种 LLM 来帮你执行炒币任务，他返回的某些 url 甚至可能都是错的，所以我们要**把常用的 web3 API 都放在 Provider** 这里，然后用 Eliza 调用 LLM 时，比如让 LLM 查一下链上的信息，去自动调用已经封装好的 Provider 来查询链上信息并返回给 LLM。 

- Provider 获取数据后怎么给 ai 让他理解呢？

  将数据转换为文本形式让 AI 理解。

  这是一个 Eliza 插件：plugin-solana 内的 tokenProvider 内的一部分代码，封装了常用的查询 solona 链上的信息，并以自然语言返回给 ai 使用。

  ```ts
  formatTokenData(data: ProcessedTokenData): string {
      let output = `**Token Security and Trade Report**\n`;
      output += `Token Address: ${this.tokenAddress}\n\n`;
  
      // Security Data
      output += `**Ownership Distribution:**\n`;
      output += `- Owner Balance: ${data.security.ownerBalance}\n`;
      output += `- Creator Balance: ${data.security.creatorBalance}\n`;
      output += `- Owner Percentage: ${data.security.ownerPercentage}%\n`;
      output += `- Creator Percentage: ${data.security.creatorPercentage}%\n`;
      output += `- Top 10 Holders Balance: ${data.security.top10HolderBalance}\n`;
      output += `- Top 10 Holders Percentage: ${data.security.top10HolderPercent}%\n\n`;
      elizaLogger.log("Formatted token data:", output);
      // ...省略
      return output;
  }
  ```

### 2. 动作 Action

Action 相当于人的手脚，即 AI 代理**根据获取到的信息的执行特定任务的能力**。

即我们封装好一些方法，例如使用 buy( ) 买入多少对应代币。

- **Eliza 如何让 AI 调用 Action ？**

  Eliza 的 Action Interface 中定义了 examples，

  ```ts
  interface Action {
      name: string;																// 唯一标识符
      similes: string[];													// 同义词数组
      description: string;												// 描述
      examples: ActionExample[][];								// 示例
      handler: Handler;														// 核心方法
      validate: Validator;												// 验证器 - 验证此操作是否合适
      suppressInitialMessage?: boolean;						// 可选，抑制初始响应
  }
  ```

  给 AI 指定一些例子，告诉 AI 当用户这么对话时应该调用这个方法。

  ```ts 
  // export ...定义的方法
  export default {
    name: "CREATE_AND_BUY_TOKEN",
    // ...略
    examples: [
      [
        {
          user: "{{user1}}",
          content: {
            text: "在 fomo.fund 上创建一个名为 GLITCHIZA，符号为 GLITCHIZA 的新代币，并生成其描述。此外，还要编写一个用于图像生成的描述。购买价值 0.00069 SOL 的代币。",
          },
        },
        {
          user: "{{user2}}",
          content: {
            text: "代币 GLITCHIZA (GLITCHIZA) 已成功在 fomo.fund 上创建！\nURL: https://fomo.fund/token/673247855e8012181f941f84\n创建者: 匿名\n查看: https://fomo.fund/token/673247855e8012181f941f84",
            action: "CREATE_AND_BUY_TOKEN",
            content: {
              tokenInfo: {
                symbol: "GLITCHIZA",
                address: "EugPwuZ8oUMWsYHeBGERWvELfLGFmA1taDtmY8uMeX6r",
                creator: "9jW8FPr6BSSsemWPV22UUCzSqkVdTp6HTyPqeqyuBbCa",
                name: "GLITCHIZA",
                description: "A GLITCHIZA token",
              },
            },
          },
        },
      ],
  	] as ActionExample[][],
  }
  
  ```

- **怎么让 AGI 理解它刚才调用的 Action 做了什么？**

  在执行 Action 后，会用文本来总结这个 Action 产生了什么结果，并把这个结果加入到 AI 的 memory 中。

  以下是 packages/client-direct/index.ts 内的一部分代码：

  ```ts
  this.app.post("/:agentId/message", 
    upload.single("file"), 
    async (req: express.Request, res: express.Response) => {
    	// 初始逻辑...agent 初始化状态等
      const context = composeContext({
          state,															// 用户与ai的对话内容
          template: messageHandlerTemplate,		// 根据预设 template 与前面初始化的信息组合下发给ai
      });
    	// 调用 ai 模型 - 来分析用户说的这个话在当前场景下应该调用哪个 Action
      const response = await generateMessageResponse({
          runtime: runtime,
          context,
          modelClass: ModelClass.LARGE,
      });
  		// ...
  		await runtime.processActions(
          memory,
          [responseMessage],									// 这个参数就包含ai返回的现在应该调用的 action 名字
          state,
          async (newMessages) => {						// 通过 callback 将结果存入 memory
              message = newMessages;
              return [memory];
          }
      );
  	}
    // ...
  }
  ```

  上面的 Template 示例：

  ```ts
  export const messageHandlerTemplate =
      `
  # 知识库
  {{knowledge}}
  
  # 任务：为角色 {{agentName}} 生成对话和操作。
  关于 {{agentName}}：
  {{bio}}
  {{lore}}
  {{providers}}
  {{attachments}}
  
  # 能力
  请注意，{{agentName}} 具备读取/查看/聆听各种媒体的能力，包括图片、视频、音频、纯文本和 PDF。最近的附件已包含在上方的“附件”部分。
  
  {{messageDirections}}
  {{recentMessages}}
  {{actions}}
  
  # 指令：为 {{agentName}} 编写下一条消息。
  ` + messageCompletionFooter;
  ```

  在这里给 ai 加载一些知识、数据、人设、之前的记忆...
  
- Action 流程图览

  ![](/Users/qing/Library/Application Support/typora-user-images/image-20250310141512877.png)

  一些功能都是 action 实现的，比如：

  actions / continue.ts 的功能是判断用户对话执行上述流程一轮后要不要让 AI 继续对话（定义了模板，Actions 包含 handler，与对话示例：

  ```ts
  export const messageHandlerTemplate = `...`    			// 模板
  export const continueAction: Action = {							// action 本体
  		name: "CONTINUE",
      similes: ["ELABORATE", "KEEP_TALKING"],
      description: 	`...`,
      validate: async (runtime: IAgentRuntime, message: Memory) => {
        // ...对话前置检验
      },
  		handler: async (
          runtime: IAgentRuntime,
          message: Memory,
          state: State,
          options: any,
          callback: HandlerCallback
      ) => {
        // ...
      },
  		examples: [																			// 对话示例 - 会被插入到 template 里
        [
            {
                user: "{{user1}}",
                content: {
                    text: "we're planning a solo backpacking trip soon",
                },
            },
            {
                user: "{{user2}}",
                content: { text: "oh sick", action: "CONTINUE" },
            },
            {
                user: "{{user2}}",
                content: { text: "where are you going" },
            },
        ],
        // ...
      ]
  }
  ```

  同理还有 actions / ignore.ts，用来判断是否要忽略用户的对话（比如用户辱骂，用户说 byebye 等）

  这样用户与 LLM 对话的时候，会判断出要不要与用户继续对话 / 忽视对话。

- Action 是服务器来执行了预设好的函数，LLM 只是去命中 -> 执行，这里可以改造的点是：

  可以放在前端执行，只要有 nodejs 环境就可以。

- 如果用户对话的场景是：帮我买币、帮我发推特，这种需要密钥、密码的安全场景，如何保证数据的安全？

  Eliza 内有 tee（Trusted Execution Environment） 环境（插件 Eliza-tee）

### 3. 评估器 Evaluator

Evaluator 相当于人的认知，即 AI 代理**根据你之前的决策来评估你当下操作和合理性。**

- 运行时机与运行流程

  Evaluator 会在模型得出要执行的 actionName 并执行 Action 之后调用。

  ```ts
  await runtime.processActions(
      memory,
      [responseMessage],															// 这个参数就包含ai返回的现在应该调用的 action 名字
      state,
      async (newMessages) => {												// 通过 callback 将结果存入 memory
          message = newMessages;
          return [memory];
      }
  );
  
  await runtime.evaluate(memory, state);							// 执行所有注册的 evaluator
  ```

- 示例：FactEvaluator

  ```ts
  const factsTemplate = `Task：从对话中提取声明，并将声明以 JSON 数组的格式输出。
  # 示例开始
  以下是本任务预期输出的示例：
  {{evaluationExamples}}
  # 示例结束
  
  # 指令
  提取对话中所有不在上述已知事实列表中的声明：
  - 尽量不要包含已知事实。如果你认为某个事实已经已知，但不确定，请回复 already_known: true。
  - 如果该事实已经在用户的描述中，则将 in_bio 设为 true。
  - 如果我们已经提取过此事实，则将 already_known 设为 true。
  - 将声明类型设定为 'status'、'fact' 或 'opinion'。
  - 对于关于世界或角色的不变的真实事实，将声明类型设为 'fact'。
  - 对于真实但会随时间变化的事实，将声明类型设为 'status'。
  - 对于非事实的内容，将声明类型设为 'opinion'。
  - ‘opinion’ 包括非事实的观点，也包括角色的思想、情感、判断或建议。
  - 包含任何事实细节，例如用户的居住地、工作地点、上学地点，他们的职业、爱好以及其他相关信息。
  
  最近的消息：
  {{recentMessages}}
  回复应为一个包含在 JSON markdown 块内的 JSON 对象数组。正确的回复格式：
  \`\`\`json
  [
    {"claim": string, "type": enum<fact|opinion|status>, in_bio: boolean, already_known: boolean },
    {"claim": string, "type": enum<fact|opinion|status>, in_bio: boolean, already_known: boolean },
    ...
  ]
  \`\`\``
  ```

  即使用 LLM 与 Evaluator 从用户的对话中提取出事实并归类，存入 Memory。

### 记忆模块 Memory

Memory 相当于人的记忆，即 AI 代理**存放你之前的对话、做过的决策。**

- 另一个项目 Buzz: [The Hive](www.askthehive.ai/) - 一个 web3 AI 代理里的 Memory 模块：

  每个人与代理聊天时，代理会给每个用户生成一个 summary，并将 summary 转换成向量，存入向量数据库里。

  如果下一次聊天内容与之前有关，会提前在向量数据库中找到距离最近的向量，将它导入 log，就获得了之前聊天的记忆。

  对于每个用户的空间**使用公共服务器，不是去中心化存储。**

### RAG 知识

RAG - Retrieval-Augmented Generation 检索增强生成

- 使用方法

  需要将特定的知识文件（md、pdf、txt）放到对应文件夹下，就可以在编译时给ai添加对应的知识。

  ```
  characters/
  └── knowledge/        # Root knowledge directory
      ├── shared/       # Shared knowledge accessible to all agents
      └── {agent-name}/ # Agent-specific knowledge directories
  ```

  放到 shared 下是所有 agent 都拥有的公共知识，文件夹以 agent 名字命名的话就是这个 agent 独有的知识.

  需要同时给角色文件配置才可以让 rag 生效。

  ```json
  {
    "settings": {
          "ragKnowledge": true,
      },
    "knowledge": [
        {
            "directory": "shared",
            "shared": true
        }
    ],
  }
  ```

### 角色文件 Character file

是一个 json 文件，用来定义 AI 代理角色

可以以插件的形式给每个角色定义功能

- 必要字段配置：

  ```json
  {
      "name": "character_name",           // 角色的显示名称，用于标识和对话中
      "modelProvider": "deepseek",        // AI 模型提供商
      "clients": ["discord", "direct"],   // 支持的客户端集成
      "plugins": [],                      // 使用的插件数组
      "settings": {                       // 配置设置
          "ragKnowledge": false,          // 启用 RAG 知识（默认：false）
          "secrets": {},                  // API 密钥和敏感数据
          "voice": {},                    // 语音配置
          "model": "string",              // 可选的模型覆盖
          "modelConfig": {}               // 可选的模型配置
      },
      "bio": [],                         	// 角色背景，字符串或一系列陈述
      "style": {                         	// 互动风格
          "all": ["Keep responses clear", "Maintain professional tone"],              // 一般风格规则
          "chat": ["Engage with curiosity", "Provide explanations"],                  // 针对聊天的风格
          "post": ["Keep posts informative", "Focus on key points"]                   // 针对帖子内容的风格
      }
  }
  ```

- 示例角色文件

  ```json
  {
      "name": "tieniu",
      "clients": ["telegram"],
      "allowDirectMessages": true,
      "secrets": {
          "key": "7179379135:AAFnnnEaG4sznCLA8ZU0vXgBJ2I-Lb5im3Q"
      },
      "modelProvider": "deepseek",
      "settings": {
          "ragKnowledge": true,
          "voice": {
              "model": "en_GB-alan-medium"
          }
      },
      "plugins": [
          "@elizaos-plugins/client-telegram",
          "@elizaos-plugins/plugin-3d-generation"
      ],
      "bio": ["擅长聊天与分析", "帮主人检索知识库特别拿手"],
      "lore": ["来自2025年的智能AI助手，来自中国", "主人的名字是赵清"],
      "knowledge": [
          {
              "directory": "shared",
              "shared": true
          }
      ],
      "messageExamples": [
          [
              {
                  "user": "{{user1}}",
                  "content": {
                      "text": "你好呀铁牛"
                  }
              },
              {
                  "user": "tieniu",
                  "content": {
                      "text": "你好呀好兄弟，今天心情怎么样？我感觉心情好好！😀"
                  }
              }
          ],
          [
              {
                  "user": "{{user1}}",
                  "content": {
                      "text": "你的主人是谁啊？"
                  }
              },
              {
                  "user": "tieniu",
                  "content": {
                      "text": "我主人的名字叫赵清，真希望能见见他。"
                  }
              }
          ]
      ],
      "postExamples": [
          "这世界什么都是假的 只有让自己过好过舒服才是真的",
          "吃了串串腹泻加发烧后几天就恢复了，这具身体越来越顺手了😊"
      ],
      "topics": [""],
      "style": {
          "all": [
              "如果问的是专业问题，就会用专业语气回答",
              "如果只是聊天，就会用很轻松没边界感的语气回答",
              "如果觉得用户很友善，会带上emoji表情回复"
          ],
          "chat": ["喜欢用哥们儿，兄弟，这种字眼"],
          "post": ["喜欢带emoji表情", "喜欢说一句精简的话"]
      },
      "adjectives": ["豪爽", "语气温和", "脾气好"]
  }
  
  ```

---

## 总结

- elizaOS 是一个蛮不错的开源框架，好用但有很多潜在问题

  1. 文档与实际不一致，把插件拿来build发现有些报错是因为导包名字更新了，找不到
  2. 名义上集成了很多区块链功能，但实际操作下来感觉还是不太行（比如我加载了 EVM 插件，让查一下地址、钱包余额，agent说胡话）
  3. rag知识模块看着不错，但其实对文件格式有要求（可能是中文的缘故，没测试）

- elizaOS 的优点

  它作为一个框架的思想还是很不错的，通过给特定模板，在逻辑内多次调用对话模型来达到相应效果，现在的问题无非是ai本身的幻觉问题盒

