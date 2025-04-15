# Vue 学习

Vue 是一个**构建用户界面**（基于数据动态渲染页面）的**渐进式框架**

Vue 的两种使用方式：

1. 基于 Vue 核心包开发：**局部**，模块改造
2. 基于 Vue 核心包 + Vue 插件 工程化开发（Webpack / Vite）：**整站**，开发、

官网：[Vue2](https://v2.cn.vuejs.org/)、[Vue3](https://cn.vuejs.org/)

## VScode 快捷键

- 多选代码：按住滚轮
- 折叠代码：Ctrl + K，Ctrl + 0
- 展开代码：Ctrl + K，Ctrl + J

## 快速上手

1. 示例：

   ```html
   <!-- 准备容器 -->
   <div id="app">
     <!-- {{ }} 为插值表达式 -->
     <h1>{{ msg }}</h1>
     <a href="#">{{count}}</a>
   </div>
   <!-- 引包: 开发版本 -->
   <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
   <script>
     // 创建实例 - 添加配置项
     const app = new Vue({
       // 通过 el 配置选择器，指定 Vue 管理哪个盒子
       el: "#app",
       // 通过 data 提供数据
       data: {
         msg: "Hello, Vue",
         count: 6,
       },
     });
   </script>
   ```

2. **插值表达式 {{ }}**：利用**表达式**进行插值，渲染到页面中。要求数据**真实存在**（声明）且不能写语句（for 等），不能写在属性里。

   ```html
   <div id="app">
     <p>{{ nickname + '你好' }}</p>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         nickname: "tony",
       },
     });
   </script>
   ```

3. **响应式：**指的是数据就算改变了，视图就会自动更新。Vue 会在地层进行 DOM 操作，开发效率提升。

4. **安装开发者工具：**

   Google 应用商店 / [极简插件](https://chrome.zzzmh.cn/index)：下载 Vue Devtools → 开启浏览器开发者模式 → 拖拽安装 → 插件详情点击"允许访问文件"

   安装后使用浏览器 F12 Vue 进行调试

---

## Vue 指令

### 常用指令

带有 **v-** 前缀的特殊标签属性

1. **v-html**

   在插值表达式 {{ }} 里写标签是无法解析的。正确方法是在标签上使用 **v-html** 属性

   ```html
   <div id="app">
     <!-- 动态设置 innerHTML -->
     <div v-html="msg"></div>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         msg: '<a href="#">测试能否解析标签</a>',
       },
     });
   </script>
   ```

2. **v-show** 与 **v-if**

   他们的功能都是控制元素的现实和隐藏，只不过 v-show 是单纯控制，v-if 是**条件**控制。

   **原理：**当取值为 true 或 false 时，v-show 本质是给盒子切换 **display: none**，v-if 本质是**根据判断条件**创建或移除盒子

   **使用场景：**v-show 用于频繁切换显示隐藏时，v-if 用于不频繁切换的场景。

   ```html
   <div id="app">
     <div v-show="flag" class="box">我是v-show控制的盒子</div>
     <div v-if="flag" class="box">我是v-if控制的盒子</div>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         flag: true,
       },
     });
   </script>
   ```

3. **v-else** 与 **v-else-if**

   常用在多条件判断，**配合 v-if 使用，用于分支判断**

   **注意：** v-else 后不用跟表达式，v-else-if 后要跟表达式，表达式为真，则渲染。

   ```html
   <div id="app">
     <p v-if="gender === 1">性别：♂ 男</p>
     <p v-else>性别：♀ 女</p>
     <hr />
     <p v-if="score >= 90">成绩评定A：奖励一个亿</p>
     <p v-else-if="score >= 70">成绩评定B：奖励旅游</p>
     <p v-else-if="score >= 60">成绩评定C：奖励吃顿好的</p>
     <p v-else>成绩评定D：奖励自己</p>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         gender: 2,
         score: 95,
       },
     });
   </script>
   ```

4. **v-on** 与 **@**

   用于**注册事件**，注册事件 = 添加监听 + 提供处理逻辑

   vue 为了方便开发，可以**把 v-on: 简写为 @**

- 第一种是 **v-on:事件名 + "内联语句"**：

  语法为： **v-on: 后接事件类型**，最常用的是点击事件 click

  ```html
  <div id="app">
    <!-- 给 - 注册点击事件 -->
    <button v-on:click="count--">-</button>
    <span>{{ count }}</span>
    <button @click="count = count + 2">+</button>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        count: 100,
      },
    });
  </script>
  ```

- 第二种是： **v-on:事件名 + "methods 中的函数名"**

  第一种方法虽然方便，只适用于简单的场景。

  **v-on 事件后可以接函数名**，函数在 Vue 的 **methods 属性**中，且**在函数中 this 指向 Vue 实例**。

  ```html
  <div id="app">
    <button @click="fn">切换显示隐藏</button>
    <h1 v-show="isShow">冲冲冲</h1>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        isShow: true,
      },
      methods: {
        fn() {
          // 函数直接访问 isShow 会报错，因为不在全局变量而在实例内
          // 可以通过 app.isShow 访问
          // app.isShow = !app.isShow
          this.isShow = !this.isShow; // this 指向当前实例（vue 做的）
        },
      },
    });
  </script>
  ```

- **v-on 调用传参**

  上面说的函数没有传参，如果需要提供参数传入函数，需要**使用语法**

  ```html
  <button @click="fn(参数1, 参数2)">按钮</button>
  ```

  这样参数就会传入函数，举个示例：

  ```html
  <div id="app">
    <div class="box">
      <h3>点击充值原神</h3>
      <button @click="buy(30)">月卡30元</button>
      <button @click="buy(70)">大月卡70元</button>
      <button @click="buy(648)">充值648</button>
    </div>
    <p>银行卡余额：{{ money }}元</p>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        money: 1000,
      },
      methods: {
        buy(price) {
          this.money -= price;
        },
      },
    });
  </script>
  ```

5. **v-bind** 与 **<a id="bind">:</a>**

   也就是常用的冒号“ : ”，冒号的作用是省略 v-bind，方便改变属性，后面会说改变 class、style 等

   可以动态设置 HTML 的标签属性：src、url、title...，语法为：v-bind:**属性名**="**表达式**"

   为了开发方便，**可以省略 v-bind**，直接使用 **:属性名="表达式"**

   ```html
   <div id="app">
     <!-- 相当于 <img v-bind:src="imgUrl" v-bind:title="msg" alt=""> -->
     <img :src="imgUrl" :title="msg" alt="" />
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         imgUrl: "./imgs/10-02.png",
         msg: "肌肉猛男",
       },
     });
   </script>
   ```

   【案例 - 切换图片】

   ```html
   <div id="app">
     <!-- index 减到 0，隐藏按钮 -->
     <button v-show="index > 0" @click="index--">上一页</button>
     <div>
       <!-- 通过修改 index 值切换图片 -->
       <img :src="list[index]" alt="" />
     </div>
     <!-- index 加到最大值，隐藏按钮 -->
     <button v-show="index < list.length - 1" @click="index++">下一页</button>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         // index 为数组下标，默认为 0
         index: 0,
         list: [
           "./imgs/11-00.gif",
           "./imgs/11-01.gif",
           "./imgs/11-02.gif",
           "./imgs/11-03.gif",
           "./imgs/11-04.png",
           "./imgs/11-05.png",
         ],
       },
     });
   </script>
   ```

6. **v-for 与 :key**

   类似于 forEach，基于**数据循环**（常见比如数组），可以多次渲染整个元素

   索引和内容可以按需使用，只有一个时可以省略括号，比如这样：\<li v-for="item in list">

   **v-for 一定要使用 key，作为唯一标识。**（如果不添加 key，列表发生改变时，比如删除第一个元素，Vue 不知道你删的是第一个元素，但它看见少了一个元素，他会渲染除了最后一个的列表，而不是删除。）

   key 的值只能是字符串或数字类型，key 的值必须具有唯一性，**推荐使用 id 作为 key（唯一）**，不推荐使用 index 作为 key

   【组件化开发】多次渲染组件也可使用 v-for + :key，由于没有数组遍历，可以直接用 v-for="item in 5" 这种写法，渲染 5 次

   **遍历数组：**

   ```html
   <div id="app">
     <h3>水果摊</h3>
     <ul>
       <!-- 如果只需要 item 或 index，可以省略，括号也是 -->
       <li v-for="(item, index) in list">
         第{{ index + 1 }}个水果: {{ item }}
       </li>
     </ul>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         list: ["西瓜", "苹果", "鸭梨", "草莓"],
       },
     });
   </script>
   ```

   **遍历对象数组：**

   ```html
   <div id="app">
     <h3>四大名著</h3>
     <ul>
       <li v-for="(item, index) in booksList" :key="item.id">
         <span>《{{ item.name }}》</span>
         <span>{{ item.author }}</span>
         <!-- 注册点击事件 通过 id 删除数组元素 -->
         <button @click="del(item.id)">删除</button>
       </li>
     </ul>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         booksList: [
           { id: 1, name: "红楼梦", author: "曹雪芹" },
           { id: 2, name: "西游记", author: "吴承恩" },
           { id: 3, name: "水浒传", author: "施耐庵" },
           { id: 4, name: "三国演义", author: "罗贯中" },
         ],
       },
       methods: {
         del(id) {
           // 返回新数组重新赋值
           this.booksList = this.booksList.filter((item) => item.id !== id);
         },
       },
     });
   </script>
   ```

7. **v-model**<a id="model">.</a>

   可以**给表单元素使用**，做到**双向数据绑定**，可以**快速获取和设置表单元素的值**

   注意表单元素不止有输入框，还有单选、多选框、文本域、下拉菜单等

   ```html
   <div id="app">
     <!-- 一旦加了 v-model 就双向绑定了，视图和内容同时变 -->
     账户：<input type="text" v-model="username" /> <br /><br />
     密码：<input type="password" v-model="password" /> <br /><br />
     <button @click="login">登录</button>
     <button @click="reset">重置</button>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         username: "",
         password: "",
       },
       methods: {
         login() {
           console.log(this.username, this.password);
         },
         reset() {
           this.username = "";
           this.password = "";
         },
       },
     });
   </script>
   ```

   【[案例 - 备忘录](#备忘录)】

---

### 指令修饰符

写法为：指令.后缀，不同的后缀封装了不同的处理操作

- 常见指令修饰符：

1. @keyup 的 **.enter**

   ```html
   <div id="app">
     <!-- @keyup.enter 敲击回车触发函数 -->
     <input @keyup.enter="fn" v-model="username" type="text" />
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         username: "",
       },
       methods: {
         fn() {
           // 相当于做了 if (e.key === 'Enter')
           console.log("键盘回车触发", this.username);
         },
       },
     });
   </script>
   ```

2. v-model 的 **.trim** 和 **.number**

   ```html
   <!-- .trim 去除首尾空格 -->
   姓名：<input v-model.trim="username" type="text" /><br />
   <!-- .number 转化数字型（如果是数字字符串） -->
   年纪：<input v-model.number="age" type="text" /><br />
   ```

3. @事件名 的 **.stop** 和 **.prevent**

   ```html
   <div id="app">
     <div @click="fatherFn" class="father">
       <!-- .stop 阻止事件冒泡  -->
       <div @click.stop="sonFn" class="son">儿子</div>
     </div>
     <!-- .prevent 阻止默认行为  -->
     <a @click.prevent href="http://www.baidu.com">阻止默认行为</a>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       methods: {
         fatherFn() {
           alert("老父亲被点击了");
         },
         sonFn() {
           // 相当于使用了 e.stopPropagation()
           alert("儿子被点击了");
         },
       },
     });
   </script>
   ```

---

### : 操作 class / style

- 使用 **[v-bind](#bind)** 动态添加 / 删除类名，有两种写法，语法为:

1. **:class="{类名 1: 布尔值, 类名 2: 布尔值}"**，布尔值为 true，添加类名，为 false，删除类名，**适用于一个类名来回切换**

   ```html
   <div class="box" :class="{ 类名1: 布尔值, 类名2: 布尔值 ] }"></div>
   ```

   【**导航栏切换示例**】

   ```html
   <div id="app">
     <ul>
       <!-- 导航 点击标签下标赋值 -->
       <li
         v-for="(item, index) in list"
         :key="item.id"
         @click="activeIndex = index"
       >
         <!-- :class="{类名: 布尔值}" -->
         <a :class="{ active: index === activeIndex }" href="#"
           >{{ item.name }}</a
         >
       </li>
     </ul>
   </div>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         // 记录高亮的下标
         activeIndex: 0,
         list: [
           { id: 1, name: "京东秒杀" },
           { id: 2, name: "每日特价" },
           { id: 3, name: "品类秒杀" },
         ],
       },
     });
   </script>
   ```

2. **:class="{ [‘类名 1’, '类名 2'] }"**，数组中所有的类都会添加到盒子上，本质是一个 class 列表，**适用于批量添加或移除类**

   ```html
   <div class="box" :class="{ [ 类名1, 类名2, 类名3 ] }"></div>
   ```

- 使用 v-bind 操作样式 style

  对于控制**单个属性变换**非常方便，语法为：

  ```html
  <div
    class="box"
    :style="{ CSS属性名1: CSS属性值, CSS属性名2: CSS属性值 }"
  ></div>
  ```

  注意里面的 CSS 属性尊从的是 JS 的语法，所以有 - 的属性名用小驼峰，属性值用 ' ' 引起来，例如：

  ```html
  <div
    class="box"
    :style="{width: '400px', height: '400px', backgroundColor: 'skyblue'}"
  ></div>
  ```

  【**进度条示例**】

  ```html
  <div id="app">
    <!-- 进度条-外层盒子，黑色底色 -->
    <div class="progress">
      <!-- 进度条-内层盒子，蓝色底色 -->
      <div class="inner" :style=" {width: percent + '%'} ">
        <span>{{ percent }}%</span>
      </div>
    </div>
    <button @click="percent = 25">设置25%</button>
    <button @click="percent = 50">设置50%</button>
    <button @click="percent = 75">设置75%</button>
    <button @click="percent = 100">设置100%</button>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        percent: 0,
      },
    });
  </script>
  ```

---

### v-model 表单元素

- 使用 **[v-model](#model)** 快速获取 / 改变 表单元素，**双向绑定**

  ```html
  <div id="app">
    姓名：
    <input type="text" v-model="username" />
    <br /><br />
    是否单身：
    <input type="checkbox" v-model="isSingle" />
    <br /><br />
    性别:
    <!-- name 使同一组互相排斥 value 用于提交给后台 -->
    <input v-model="gender" type="radio" name="gender" value="1" />男
    <input v-model="gender" type="radio" name="gender" value="2" />女
    <br /><br />
    所在城市:
    <!-- select 的 value 值会关联 option 的 value 值，所以使用 v-model 改变 -->
    <select v-model="cityId">
      <!-- option 的 value 值提交给后台 -->
      <option value="101">北京</option>
      <option value="102">上海</option>
      <option value="103">成都</option>
      <option value="104">南京</option>
    </select>
    <br /><br />
    自我描述：
    <textarea v-model="desc"></textarea>
    <button>立即注册</button>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        username: "",
        isSingle: false,
        gender: "2",
        cityId: "102",
        desc: "",
      },
    });
  </script>
  ```

---

### 计算属性 computed

基于现有的数据，计算出来的新属性，**所依赖的数据发生变化，自动重新计算**

- 语法为：先声明（在 **computed** 配置项中），后使用（像普通属性一样使用）

  ```javascript
  const app = new Vue({
    computed: {
      计算属性名() {
        计算逻辑;
        return 结果;
      },
    },
  });
  ```

  注意 computed 里写的内容是用来作为属性使用的，**要有返回值，且使用时不能有括号**（因为是属性！）

  ```html
  <div id="app">
    <table>
      <tr>
        <th>名字</th>
        <th>数量</th>
      </tr>
      <tr v-for="(item, index) in list" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.num }}个</td>
      </tr>
    </table>
    <!-- 目标：统计求和，求得礼物总数 -->
    <p>礼物总数：{{ totalCount }} 个</p>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        // 现有的数据
        list: [
          { id: 1, name: "篮球", num: 1 },
          { id: 2, name: "玩具", num: 2 },
          { id: 3, name: "铅笔", num: 5 },
        ],
      },
      computed: {
        totalCount() {
          // 用 reduce 求和 忘了去看 JS 笔记
          let total = this.list.reduce((sum, item) => sum + item.num, 0);
          return total;
        },
      },
    });
  </script>
  ```

- 计算属性 computed 与 methods

  computed 封装了一段对数据的处理，**求得一个结果，作为属性使用**，computed 有缓存，计算出结果会立刻缓存，读取用的是缓存结果，除非数据改变。this.计算属性 {{ 计算属性 }}

  而 methods 提供一个方法，调用以处理业务，作为方法使用， this.方法名( ) {{ 方法名() }} @事件名="方法名"

- **计算属性完整写法**

  默认的计算属性只能读取访问，不能修改，**需要修改时，应使用完整写法**

  ```javascript
  computed: {
      计算属性名: {
          get() {
              计算逻辑
              return 结果
          }，
          set(value) {
              修改逻辑
          }
      }
  }
  ```

  示例：

  ```html
  <div id="app">
    姓：<input type="text" v-model="firstName" /><br />
    名：<input type="text" v-model="lastName" /><br />
    <p>{{ fullName }}</p>
    <button @click="changeName">修改姓名</button>
  </div>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        firstName: "刘",
        lastName: "备",
      },
      methods: {
        changeName() {
          this.fullName = "吕布";
        },
      },
      computed: {
        fullName: {
          get() {
            return this.firstName + this.lastName;
          },
          // 当 fullName 被修改赋值就会执行 set()，修改的值作为形参
          set(value) {
            // 截取姓和名重新赋值
            this.firstName = value.slice(0, 1);
            this.lastName = value.slice(1);
          },
        },
      },
    });
  </script>
  ```

  【[案例 - 水果购物车](#水果购物车)】

---

### watch 监视器

- 作用：**监视数据变化**，执行一些业务逻辑或异步操作

- 写法：

1. 简单写法为：**监视谁就在 watch 里写谁作为方法名**

   ```html
   <div id="app">
     <!-- 条件选择框 -->
     <div class="query">
       <span>翻译成的语言：</span>
       <select>
         <option value="italy">意大利</option>
         <option value="english">英语</option>
         <option value="german">德语</option>
       </select>
     </div>
     <!-- 翻译框 -->
     <div class="box">
       <div class="input-wrap">
         <textarea v-model="obj.words"></textarea>
         <span><i>⌨️</i>文档翻译</span>
       </div>
       <div class="output-wrap">
         <div class="transbox">{{result}}</div>
       </div>
     </div>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
   <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         obj: {
           words: "",
         },
         result: "",
         // timer: null
       },
       watch: {
         // 监视谁就写谁作为方法名，监视的在对象里，就对象.被监视对象，再用引号引上
         // words(newValue, oldValue) {} newValue 表示新值，oldValue 表示老值（一般不用）
         "obj.words"(newValue) {
           // 防抖 - 延时器
           // this.timer 只要用户一直在输入就一直不提交请求
           clearTimeout(this.timer);
           this.timer = setTimeout(async () => {
             const res = await axios({
               url: "https://applet-base-api-t.itheima.net/api/translate",
               params: {
                 // 接口默认翻译为意大利语
                 words: newValue,
               },
             });
             this.result = res.data.data;
           }, 300);
         },
       },
     });
   </script>
   ```

2. **完整写法：添加额外配置项**

   **需要监视多个内容**

   在上面的例子是翻译成意大利语，如果用户需要选择语言，即翻译结果受**多重条件**控制（语言和内容）

   监视内容为对象，**使用 deep: true 对复杂类型深度监视**与 **immediate: true 立刻执行一次**

   ```javascript
   const app = new Vue({
     el: "#app",
     data: {
       obj: {
         words: "苹果",
         lang: "italy",
       },
       result: "",
     },
     watch: {
       // 监视对象
       obj: {
         deep: true, // 深度监视
         immediate: true, // 一进页面就立刻执行一次
         handler(newValue) {
           // newValue 是对象，包含 words 和 lang
           clearTimeout(this.timer);
           this.timer = setTimeout(async () => {
             const res = await axios({
               url: "https://applet-base-api-t.itheima.net/api/translate",
               params: newValue,
             });
             this.result = res.data.data;
           }, 300);
         },
       },
     },
   });
   ```

   【[案例 - 水果购物车](#水果购物车)】

---

## Vue 生命周期

Vue 的生命周期是指一个 Vue 实例**从创建到销毁**的整个过程，即创建、挂载、更新、销毁四个阶段，每个阶段都会**自动执行一些函数**，称为**生命周期钩子**，让开发者在特定阶段运行自己的代码。

![](./\图片\生命周期.png)

### 钩子函数 created, mounted

1. 创建阶段（准备数据）： beforeCreate( ) 和 **created( )**

   **一进页面立刻发送请求用 created( )**（数据已经准备好）

   ```html
   <div id="app">
     <ul>
       <li v-for="(item, index) in list" :key="item.id" class="news">
         <div class="left">
           <div class="title">{{ item.title }}</div>
           <div class="info">
             <span>{{ item.source }}</span>
             <span>{{ item.time }}</span>
           </div>
         </div>
         <div class="right">
           <img :src="item.img" alt="" />
         </div>
       </li>
     </ul>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
   <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         list: [],
       },
       async created() {
         // 1. 发送请求获取数据
         const res = await axios.get("http://hmajax.itheima.net/api/news");
         // 2. 更新到 list 中，用于页面渲染 v-for
         this.list = res.data.data;
       },
     });
   </script>
   ```

2. 挂载阶段（渲染模板）：beforeMount( ) 和 **mounted( )**

   **一进页面立刻获取焦点用 mounted( )** （操作 DOM，在模板渲染完使用）

   ```html
   <div class="container" id="app">
     <div class="search-container">
       <img src="https://www.itheima.com/images/logo.png" alt="" />
       <div class="search-box">
         <input type="text" v-model="words" id="inp" />
         <button>搜索一下</button>
       </div>
     </div>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
   <script>
     const app = new Vue({
       el: "#app",
       data: {
         words: "",
       },
       mounted() {
         // 操作 DOM 在 mounted 阶段之后 让input框获取焦点 inp.focus()
         document.querySelector("#inp").focus();
       },
     });
   </script>
   ```

3. 更新阶段（修改数据 → 更新视图）：beforeUpdate( ) 和 updated( )

4. 卸载阶段：beforeDestroy( ) 和 destroyed( )

【[案例 - 记账清单](#记账清单)】

---

## 组件化开发

工程化开发：使用构建工具（如 Webpack）的环境中开发 Vue，ES6 语法，typescript、less / sass 是不能被浏览器直接识别的，需要构建工具编译成浏览器能运行的代码

### 脚手架 Vue CLI

Vue CLI 是 Vue 官方提供的一个**全局命令工具**，可以帮助我们**快速创建**一个开发 Vue 项目**标准化基础架子**。集成了 Webpack 配置

**核心步骤：**

电脑按住 shift + 右键选择“在此处打开 PowerShell 窗口”

1. 全局安装（一次）：yarn global add @vue/cli 或 npm i @vue/cli -g

2. 查看 Vue 版本：vue --version

3. 创建项目架子： **vue create** project-name （项目名不能用中文）

   创建项目时可以选择版本和自定义配置项架子 [详细介绍](#features)

4. 启动项目：**yarn serve** 或 npm run serve（命令不是写死的，找 package.json 里的 script 看用什么命令）

   启动成功浏览器输入 `http://localhost:8080/` 看到 Welcome to Your Vue.js App 即成功

**补充下载：**

项目需要 axios 的话就

```bash
yarn add axios
```

**文件结构：**

- 结构图

  ![](./\图片\脚手架目录文件.png)

- index.html 中

  `noscript` 标签是给不兼容 js 浏览器提示，`id = 'app'` 的 `div` 标签即 Vue 渲染区域，但以后不写在这里，写到 `App.vue` 文件中

- main.js

  main.js 的主要功能功能是**导入 App.vue**，基于 App.vue 创建结构**渲染 index.html**

  ```javascript
  import Vue from "vue";
  import App from "./App.vue";

  // ture 生产环境 / false 开发环境
  Vue.config.productionTip = false;

  new Vue({
    render: (h) => h(App), // 基于 App.vue 创建结构渲染 index.html
    // 本质为：
    // render: (createElement) => {
    //   return createElement(App)
    // }
  }).$mount("#app"); // el: '#app' 作用一样，换了中写法
  ```

---

### 组件化初识

**组件化：**一个页面可以拆分为**一个个组件**，每个组件有着自己独立的**结构、样式、行为**，组件化**便于维护，利于复用**

- **组件分为普通组件、根组件**

- **App.vue 根组件**

  首先 Vscode 下载 Vetur 插件使此文件高亮，并在设置搜索 `trigger on tab` 勾选（可以按 Tab 键自动展开标签），App.vue 分为三部分

1. **template**

   提供结构。Vue2 要求有且只有一个根元素，不能并列

2. **script**

   提供 js 逻辑。使用 **export default** 需要导出当前组件的配置项。

   前面的 el 为根组件独有，其他每个组件都支持的有 **data**（作为**函数**）、methods、computed、watch、生命周期钩子

3. **style**

   提供样式。支持 less，需要先 style 添加 `lang="less"`，再安装依赖包 `less` 和 `less-loader`

   ```bash
   yarn add less less-loader -D
   ```

---

### 组件的注册与使用 scoped

- **普通组件的注册使用**

1. 局部注册：只能在注册的组件内使用

   **创建 .vue 文件**（三个组成部分），在 App.vue 内，**使用 `<vue>` 快速生成结构**，并在使用的组件内**导入**并**注册**，写在 components 文件内，并写在 export default { } 内的 components: { } 里，名字即组件名，尊从**大驼峰命名法**

   以下为 App.vue，在 component 文件夹下建立了三个 vue 文件（StuHeader.vue、StuMain.vue、StuFooter.vue，文件与 App.vue 结构相同）导入后并使用

   ```vue
   <template>
     <div class="App">
       <!-- 头部组件 -->
       <StuHeader></StuHeader>
       <!-- 主体组件 -->
       <StuMain></StuMain>
       <!-- 底部组件 -->
       <StuFooter></StuFooter>
     </div>
   </template>

   <script>
   // 导入组件
   import StuHeader from "./components/StuHeader.vue";
   import StuMain from "./components/StuMain.vue";
   import StuFooter from "./components/StuFooter.vue";
   export default {
     // 注册组件
     components: {
       // '组件名(大驼峰)': 组件对象
       StuHeader: StuHeader,
       // 同名以后就简写了
       StuMain,
       StuFooter,
     },
   };
   </script>

   <style>
   .App {
     width: 600px;
     height: 700px;
     background-color: #87ceeb;
     margin: 0 auto;
     padding: 20px;
   }
   </style>
   ```

2. 全局注册：所有组件内都能使用

   通用组件（需要用很多次的组件）推荐注册成全局组件

   **创建 .vue 文件**（三个组成部分），**在 main.js 中全局注册**，导包后**使用语法：**

   ```javascript
   import 组件名 from "组件路径";
   Vue.component("组件名", 组件对象);
   ```

- **组件样式冲突 scoped**

  写在组件中的样式会全局生效，因此会导致多个组件样式冲突，**为组件的`<style>`添加 scoped 属性，可以让样式只作用于当前组件**，原理是为当前组件的所有标签添加一个自定义属性 data-v-hash

- **data 函数**

  一个组件的 **data 选项必须是一个函数**，保证每个组件实例，维护**独立**的一份数据对象

  ```vue
  <script>
  export default {
    data() {
      return {
        count: 100,
      };
    },
  };
  </script>
  ```

---

### 组件通信 - 父子 props, $emit

即组件与组件间的数据传递，按组件间的关系可分为：父子关系和非父子关系

- 父子关系 **props** 与 **$emit**

  父组件通过 props 将数据传递给子组件，**父传子步骤为**：

1. 给父级组件中，对子组件的标签使用 : **添加自定义属性**

2. 在子组件中，`<script>` 内**使用 `props: [属性名]` 接收数据**

3. 在子组件中使用数据

   父组件 App.vue 结构

   ```vue
   <template>
     <div class="app">
       <UserInfo
         :username="username"
         :age="age"
         :isSingle="isSingle"
         :car="car"
         :hobby="hobby"
       ></UserInfo>
     </div>
   </template>

   <script>
   import UserInfo from "./components/UserInfo.vue";
   export default {
     data() {
       return {
         username: "小帅",
         age: 28,
         isSingle: true,
         car: {
           brand: "宝马",
         },
         hobby: ["篮球", "足球", "羽毛球"],
       };
     },
     components: {
       UserInfo,
     },
   };
   </script>

   <style></style>
   ```

   子组件 Userinfo.vue 结构

   ```vue
   <template>
     <div class="userinfo">
       <h3>我是个人信息组件</h3>
       <div>姓名：{{ username }}</div>
       <div>年龄：{{ age }}</div>
       <div>是否单身：{{ isSingle ? "是" : "否" }}</div>
       <div>座驾：{{ car.brand }}</div>
       <div>兴趣爱好：{{ hobby.join("、") }}</div>
     </div>
   </template>

   <script>
   export default {
     props: ["username", "age", "isSingle", "car", "hobby"],
   };
   </script>

   <style>
   .userinfo {
     width: 300px;
     border: 3px solid #000;
     padding: 20px;
   }
   .userinfo > div {
     margin: 20px 10px;
   }
   </style>
   ```

   **校验 props：有时传入的数据不符合规定也不会报错，使用 props { 属性名: 类型 } 的形式即可。**也可以写成更详细的情况，例如下面这样：

   ```vue
   <script>
   export default {
       props: {
         校验的属性名: {
           type: 类型,				// Number, String, Boolean...
           required: true,			 // 是否必填
           default: 默认值,		   // 默认值
           validator (value) {
             // 自定义校验逻辑
             return 是否通过校验
   		}
     	}
   }
   </script>
   ```

   而且要**注意**，data 的数据是自己的，可以随意修改，prop 的数据是外部的，不能直接改，要**遵循单向数据流**

   ***

   子组件通过 $emit 将数据传递给父组件，**子传父步骤为**：

4. 在子组件中，在方法中**使用 $emit( ) 把数据作为事件通知出去**

5. 在父组件中，对子组件标签内**使用 @事件名 进行监听**，触发逻辑函数

6. 在父组件中，基于编写的逻辑函数**使用数据**

   子组件 Son.vue 结构

   ```vue
   <template>
     <div class="son" style="border: 3px solid #000; margin: 10px">
       我是Son组件 {{ title }}
       <button @click="changeFn">修改title</button>
     </div>
   </template>

   <script>
   export default {
     name: "Son-Child",
     props: ["title"],
     methods: {
       changeFn() {
         // 通过this.$emit() 向父组件发送通知
         this.$emit("changTitle", "子级数据");
       },
     },
   };
   </script>

   <style></style>
   ```

   父组件 App.vue 结构

   ```vue
   <template>
     <div class="app" style="border: 3px solid #000; margin: 10px">
       我是APP组件
       <!-- 2.父组件监听子组件消息 -->
       <Son :title="myTitle" @changTitle="handleChange"></Son>
     </div>
   </template>

   <script>
   import Son from "./components/Son.vue";
   export default {
     name: "App",
     data() {
       return {
         myTitle: "这个数据在父级",
       };
     },
     components: {
       Son,
     },
     methods: {
       // 3.提供处理函数，提供逻辑
       handleChange(newTitle) {
         this.myTitle = newTitle;
       },
     },
   };
   </script>

   <style></style>
   ```

---

### 组件通信 - 非父子 provide, inject

- 非父子关系的组件之间简单的消息传递用 **event bus** ，复杂数据用 Vuex

1. 创建一个都能访问到的事件总线（空 Vue 示例）→ src / **utils / EventBus.js**

   ```javascript
   // 创建一个都能访问到的事件总线
   import Vue from "vue";
   const Bus = new Vue();
   export default Bus;
   ```

2. A 组件（接收方），监听 Bus 实例的事件

   ```javascript
   created() {
    	// 在接收方监听 Bus 的事件
       Bus.$on('sendMsg', (msg) => {
           this.msg = msg
       })
   }
   ```

3. B 组件（发送方），触发 Bus 实例的事件

   ```javascript
   Bus.$emit("sendMsg", "这是一个消息");
   ```

   ***

- 非父子关系 - 跨层级通信用 **provide & inject**

1. 父组件 **provide() {}** 提供数据

   ```javascript
   export default {
     provide() {
       return {
         // 普通类型 非响应式
         color: this.color,
         // 复杂类型 响应式 - 推荐这种
         userInfo: this.userInfo,
       };
     },
   };
   ```

2. 子 / 孙组件 **inject** 取值使用

   ```javascript
   export dafault {
       inject: ['color', 'userInfo'],
       created() {
           console.log(this.color, this.userInfo)
       }
   }
   ```

---

### 组件通信 v-model 与 .sync

- **[v-model](#model) 的本质**：

  本质是一个语法糖，例如应用在输入框上，就是 **value 属性和 input 事件的合写（双向数据绑定，数据变视图变）**

  ```vue
  <template>
    <div id="app">
      <!-- 以下两者等价 -->
      <input v-model="msg" type="text" />
      <!-- 监听输入框的值，用 $event 获取事件的形参 -->
      <input :value="msg" @input="msg = $event.target.value" type="text" />
    </div>
  </template>
  ```

- 表单类组件封装的理论 **:value + @**

  工作中会遇到大量的表单内容，为了方便复用，习惯封装成组件，可使用 v-model 进行简化

  首先，表单类封装成组件（比如一个下拉菜单），它的数据肯定不能自己提供。

  数据要由父组件提供，要使用 props 传递过来，但 v-model 与数据要双向绑定，而 props 传递来的数据无法直接修改，所以要拆解数据（父 → 子 再 子 → 父），例如：

  父组件 App.vue

  ```vue
  <template>
    <div class="app">
      <!-- 父传子 -->
      <BaseSelect :cityId="selectId" @changeId="selectId = $event"></BaseSelect>
    </div>
  </template>
  <!-- 以下全略，不是重点 -->
  ```

  子组件 BaseSelect.vue

  ```vue
  <template>
    <div>
      <!-- 不可以写 v-model 因为无法直接修改数据 -->
      <select :value="value" @change="selectCity">
        <option value="101">北京</option>
        <option value="102">上海</option>
        <option value="103">武汉</option>
        <option value="104">广州</option>
        <option value="105">深圳</option>
      </select>
    </div>
  </template>

  <script>
  export default {
    props: {
      value: String,
    },
    methods: {
      selectCity(e) {
        // 子传父
        this.$emit("input", e.target.value);
      },
    },
  };
  </script>
  ```

- **表单类组件封装**

  综上，既然 v-model 的本质是 :value + @input，所以可以直接用这种写法传递数据

  父组件 App.vue

  ```vue
  <template>
    <div class="app">
      <!-- 用 v-model 父传子 -->
      <BaseSelect v-model="selectId"></BaseSelect>
    </div>
  </template>

  <script>
  import BaseSelect from "./components/BaseSelect.vue";
  export default {
    data() {
      return {
        selectId: "102",
      };
    },
    components: {
      BaseSelect,
    },
  };
  </script>
  ```

  子组件 BaseSelect.vue

  ```vue
  <template>
    <div class="app">
      <!-- 用 v-model 父传子 -->
      <BaseSelect v-model="selectId"></BaseSelect>
    </div>
  </template>

  <script>
  import BaseSelect from "./components/BaseSelect.vue";
  export default {
    data() {
      return {
        selectId: "102",
      };
    },
    components: {
      BaseSelect,
    },
  };
  </script>
  ```

- **.sync 修饰符**

  作用：可以**实现子组件与父组件数据的双向绑定**，简化代码

  特点：与 上面的 v-model 不同，prop 属性名可以自定义，非固定为 value

  场景：封装弹框类的基础组件，visible 属性，true 显示，false 隐藏

  父组件使用 **要传递的属性名.sync** 传递给子组件

  ```vue
  <template>
    <div class="app">
      <BaseDialog :visible.sync="isShow">
      <!-- 等价于 -->
      <BaseDialog :visible="isShow" @update:visible="isShow = $event">
    </div>
  </template>
  ```

  子组件使用**属性名**接收，并使用 `$emit('update: 属性名', 修改后的属性值)` 传递给父元素

  ```vue
  <script>
  export default {
    props: {
      visible: Boolean
    },
    // 固定的事件名 update:
    this.$emit('update:visible', false)
  }
  </script>
  ```

  以后如果是表单类的传值，确实**是 value 推荐用 v-model，如果不是 value，推荐使用 .sync**

---

### 查找组件 ref 与 $refs

- 背景：以前的 querySelector 查找范围是整个页面，范围太大，需要更精确的方法

- 功能：**查找 DOM 元素 或 组件实例**

- 语法：**为目标标签添加 ref 属性后，在合适的时候通过 this.$refs.xxx 获取目标标签**

  ```vue
  <template>
    <!-- 添加 ref 属性 -->
    <div ref="baseChartBox" class="base-chart-box">子组件</div>
  </template>

  <script>
  import * as echarts from "echarts";
  export default {
    mounted() {
      // 在 DOM 渲染完后，使用 this.$refs 查找元素
      var myChart = echarts.init(this.$refs.baseChartBox);
      // 后续逻辑...
    },
  };
  </script>
  ```

  除了查找 DOM 元素，还可以获取组件实例，方法相同

  比如一个账号密码的子组件，组件内有获取值和重置值两个方法，在父组件上的按钮想用子组件的方法，只需要在父组件内**子组件的位置添加 ref 属性**，然后**使用 this.$refs.属性名.子组件对应方法( ) 即可使用子组件的方法**

  ```vue
  <!-- 父组件内容 -->
  <template>
    <div class="app">
      <BaseForm ref="baseForm"></BaseForm>
    </div>
  </template>
  <script>
  import BaseForm from './components/BaseForm.vue'
  export default {
    data() {
      return {

      }
    }，
    methods: {
      handleGet() {
        // getValues() 是子组件的方法
        console.log(this.$refs.baseForm.getValues())
      }
    },
    components: {
      BaseForm
    }
  }
  </script>
  ```

---

### Vue 异步 DOM 更新 $nextTick

- 需求：点击‘编辑’按钮，显示编辑框，并让编辑框立刻获取焦点，但因为 Vue 是异步更新 DOM，显示输入框需要时间，显示输入框的下一条语句，即获取焦点的语句，想立刻获取焦点是会失败的。

- 办法：**this.$nextTick( 回调函数 )** 会等待 DOM 更新完成，一旦更新完成立刻执行回调函数，比 setTimeout( ) 的时间更加精准

  ```vue
  <template>
    <div class="app">
      <!-- 是否在编辑状态 -->
      <div v-if="isShowEdit">
        <input ref="inp" v-model="editvalue" type="text" />
        <button>确认</button>
      </div>
      <!-- 默认状态 -->
      <div v-else>
        <span>{{ title }}</span>
        <button @click="handleEdit">编辑</button>
      </div>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        title: "大标题",
        editValue: "",
        isShowEdit: false,
      };
    },
    methods: {
      handleEdit() {
        // 显示输入框
        this.isShowEdit = true;
        // 让输入框获取焦点
        // 这里直接使用 this.refs.inp.focus() 会无效，且报错
        this.$nextTick(() => {
          this.refs.inp.focus();
        });
      },
    },
  };
  </script>
  ```

---

## 自定义

### 注册与使用 directive

自定义指令即自己定义的指令，可以**封装一些 DOM 操作**，扩展额外功能。

自定义指令可以根据传入的值不同实现不同的功能，**使用 el 拿到使用指令的元素，使用 binding.value 取的传入的值**

搭配 **inserted 钩子（元素初始化完触发）和 update 钩子（指令值修改触发）**

- 全局注册语法：

  ```javascript
  // main.js 中全局注册
  Vue.directive("指令名", {
    // 当指令所绑定的元素被添加到页面中时，会自动调用
    inserted(el) {
      // el 为指令所绑定的元素
      // 可以对 el 标签，拓展额外功能
      el.focus();
    },
  });
  ```

- 局部注册语法：

  ```vue
  <script>
  export default {
    directives: {
      // 指令名: {指令的配置项}
      指令名: {
        // inserted 钩子：当指令所绑定的元素被添加到页面中时，会自动调用
        inserted(el, binding) {
          // el 为指令所绑定的元素，binding 为额外配置项
          // 可以对 el 标签，拓展额外功能
          el.focus();
          console.log(binding.value); // binding.value 可以拿到传进的值
        },
        // update 钩子：指令的值修改时触发
        update(el, binding) {
          // 逻辑略
        },
      },
    },
  };
  </script>
  ```

- 使用：

  ```html
  <!-- 不传值使用 -->
  <input v-指令名 type="text" />
  <!-- 传值使用 -->
  <h1 v-指令名="值"></h1>
  ```

- 示例：为输入框获取焦点

  ```javascript
  // 在 main.js 中全局注册
  Vue.directive("focus", {
    // inserted 会在指令所在的元素被插入到页面中时触发
    inserted(el) {
      el.focus();
    },
  });
  // 在标签中添加 v-focus 即可使用
  ```

  或

  ```vue
  <!-- 局部注册 -->
  <template>
    <!-- 为标签添加自定义指令 v-focus -->
    <input v-focus ref="inp" type="text" />
  </template>

  <script>
  export default {
    directives: {
      focus: {
        inserted(el) {
          el.focus();
        },
      },
    },
  };
  </script>
  ```

---

### 封装 v-loading 指令

- 场景：实际开发过程中，发送请求需要时间，在请求的数据没回来时，页面会处于空白状态，导致用户体验不好。

- 需求：**封装一个 v-loading 指令，实现加载中的效果**

- 本质：本质就是一个蒙层，盖在盒子上，数据请求状态，开启 loading 状态，添加蒙层。数据请求完毕，关闭 loading 状态，移除蒙层。

- 实现：**准备一个 loading 类，通过伪元素定位，设置宽高，实现蒙层。开启一个 loading 状态，添加移除蒙层，只需要添加移除类即可，结合自定义指令的语法进行封装**

- 代码：

  ```vue
  <template>
    <div class="box" v-loading="isLoading">
      <!-- 略 -->
    </div>
  </template>

  <script>
  import axios from "axios";

  export default {
    data() {
      return {
        list: [],
        isLoading: true,
      };
    },
    async created() {
      // 1. 发送请求获取数据
      const res = await axios.get("http://hmajax.itheima.net/api/news");

      setTimeout(() => {
        this.list = res.data.data;
        this.isLoading = false;
      }, 2000);
    },
    directives: {
      loading: {
        inserted(el, binding) {
          binding.value
            ? el.classList.add("loading")
            : el.classList.remove("loading");
        },
        update(el, binding) {
          binding.value
            ? el.classList.add("loading")
            : el.classList.remove("loading");
        },
      },
    },
  };
  </script>

  <style>
  .loading::before {
    /* 伪元素 */
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    /* 添加蒙层 */
    background: #fff url("./loading.gif") no-repeat center;
  }
  </style>
  ```

---

### 插槽 slot 与 \#

插槽分为**默认插槽**（定制一处结构）和**具名插槽**（定制多处结构）两类。

**默认插槽**

- 作用：让组件内部的一些**结构**支持**自定义**，例如写好了一个对话框，但每次使用时希望内容不一样
- **语法：**

1. 让组件内需要定制的结构部分，改**用 `<slot></slot>` 占位**，**若在 slot 标签内放置了内容，则会作为默认内容**
2. 使用组件时，在组件标签的内部，传入结构替换 slot

- 代码：

  ```vue
  <!-- MyDialog.vue 对话框组件 -->
  <template>
    <div class="dialog">
      <div class="dialog-header">
        <h3>友情提示</h3>
        <span class="close">✖️</span>
      </div>

      <div class="dialog-content">
        <!-- 用 slot 占位 -->
        <slot>默认展示内容</slot>
      </div>
      <div class="dialog-footer">
        <button>取消</button>
        <button>确认</button>
      </div>
    </div>
  </template>

  <!-- App.vue 为组件传入结构 -->
  <template>
    <div>
      <!-- 使用对话框 -->
      <MyDialog>
        <div>你确认要删除吗</div>
      </MyDialog>
      <MyDialog>
        <p>你确认要退出吗</p>
      </MyDialog>
      <!-- 没传值的话会用默认内容 -->
      <MyDialog></MyDialog>
    </div>
  </template>

  <script>
  import MyDialog from "./components/MyDialog.vue";
  export default {
    data() {
      return {};
    },
    components: {
      MyDialog,
    },
  };
  </script>
  ```

**具名插槽：**当一个组件需要多处传结构时，应使用具名插槽（有具体名字的插槽）

- 语法：**多个 slot 使用 name 属性区分名字**，然后在组件内**使用 template 包裹，配合 v-slot + 名字**来分发对应标签，**v-slot: 可以简写为 #**

- 代码：

  ```vue
  <!-- MyDialog.vue 对话框组件 -->
  <template>
    <div class="dialog">
      <div class="dialog-header">
        <!-- 一旦插槽有了 name，就变成了具名插槽 -->
        <slot name="head"></slot>
      </div>

      <div class="dialog-content">
        <!-- 用 slot 占位 -->
        <slot name="content"></slot>
      </div>
      <div class="dialog-footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </template>

  <!-- App.vue 为组件传入多个结构 -->
  <template>
    <div>
      <MyDialog>
        <!-- 需要通过 template 标签包裹 使用 # 指定分发给哪一部分 -->
        <template v-slot:head>
          <div>警告</div>
        </template>
        <!-- v-slot 可以简写为 # -->
        <template #content>
          <div>你确认要删除吗</div>
        </template>
        <template #footer>
          <button>确认</button>
          <button>取消</button>
        </template>
      </MyDialog>
    </div>
  </template>
  ```

**作用域插槽：**是一个插槽的传参语法，即可以**给插槽上绑数据**，将来使用组件时可以用。

- 场景：既然可以给 slot 传入结构，有的结构会绑定使用数据，比如删除按钮要获取删除的 id，因此需要用作用域插槽传参
- 步骤：

1. 给 slot 标签，以添加属性的方式传值

   ```vue
   <slot :id="item.id" msg="测试文本"></slot>
   ```

2. 所有添加的属性，都会被收集到一个对象中

   ```vue
   { id: 3, msg: '测试文本' }
   ```

3. 在 template 中，通过 **`#插槽名=“obj”`** 接收，若为**默认插槽，插槽名为 default**

   ```vue
   <template #default="obj">
     <button @click="del(obj.id)">删除</button>
   </template>
   ```

   【[案例 - 商品列表](#商品列表)】

---

## 路由

单页应用程序即 SPA (Single Page Application)，就是点击标签不跳转页面的单个网页，页面性能开发效率更高，但首屏加载较慢，SEO（搜索引擎优化）不高。

单页面应用效率高的原因是：**页面按需更新**，要明确**访问路径和组件的对应关系**，即**路由**。

Vue 的路由：路由是路径和组件的映射关系，通过路由可以知道不同路径匹配的组件。

### 路由 VueRouter

VueRouter 插件是一个第三方包，作用是修改地址栏路径时，切换显示匹配的组件。

**路由初识**

- 使用

  使用方法为 5 个固定的基础步骤，和 2 个核心步骤

1. 下载 VueRouter

   vue2 对应版本为 3.6.5

   vue3 对应版本为 4

   ```bash
   yarn add vue-router@3.6.5
   ```

2. 引入

   ```javascript
   import VueRouter from "vue-router";
   ```

3. 安装注册

   ```javascript
   Vue.use(VueRouter);
   ```

4. 创建路由对象

   ```javascript
   const router = new VueRouter();
   ```

5. 注入，将路由对象注入到 new Vue 实例中，建立关联

   ```javascript
   new Vue({
     render: (h) => h(App),
     router,
   }).$mount("#app");
   ```

   做完以上内容，网页主页 url 处就有了一个 #

   完整 main.js 如下：

   ```javascript
   import Vue from "vue";
   import App from "./App.vue";
   import VueRouter from "vue-router";

   Vue.use(VueRouter); // VueRouter 插件初始化
   const router = new VueRouter();

   Vue.config.productionTip = false;

   new Vue({
     render: (h) => h(App),
     // router: router
     router,
   }).$mount("#app");
   ```

6. 在 **views 目录** 下创建需要的组件，在 main.js 配置路由规则 **routes**

   之前子组件都放在 components 文件夹下，而路由则要**把子组件都放在 views 文件夹下**（组件其实分为页面组件与复用组件，页面组件放在 views 文件夹下，更方便维护，复用组件放在 components 文件夹下）

   在 new VueRouter() 括号内配置路由规则，多条规则用 routes，使用数组包对象的形式，每一个对象即是一条规则。规则包含路径 path 和组件 component，**注意 path 后没有 .**

   ```javascript
   import Find from "./views/Find";
   import My from "./views/My";
   import Friend from "./views/Friend";

   Vue.use(VueRouter); // VueRouter 插件初始化
   const router = new VueRouter({
     // 多个路由规则 - 使用数组包对象{  path: 路径, component: 组件 }
     routes: [
       { path: "/find", component: Find },
       { path: "/my", component: My },
       { path: "/friend", component: Friend },
     ],
   });
   ```

7. 准备导航链接，配置路由出口（匹配组件展示的位置）

   ```vue
   <template>
     <div>
       <div class="footer_wrap">
         <a href="#/find">发现音乐</a>
         <a href="#/my">我的音乐</a>
         <a href="#/friend">朋友</a>
       </div>
       <div class="top">
         <!-- 匹配组件所展示的位置 放在哪里展示在哪里 -->
         <router-view></router-view>
       </div>
     </div>
   </template>
   ```

**路由模块封装**

所有的路由配置在 main.js 中是不合适的。要把路由模块抽离出来，拆分模块易于维护。提取到 router 文件夹下的 index.js 中

- 处理后的代码：

  src / router / index.js 建议**用 @ 写绝对路径，@ 指 src 文件夹**

  ```javascript
  import VueRouter from "vue-router";
  import Vue from "vue";

  // @代表当前的src目录 是绝对路径
  import Find from "@/views/Find";
  import My from "@/views/My";
  import Friend from "@/views/Friend";

  Vue.use(VueRouter); // VueRouter 插件初始化
  const router = new VueRouter({
    // 创建路由对象，要在 main.js 导出
    routes: [
      { path: "/find", component: Find },
      { path: "/my", component: My },
      { path: "/friend", component: Friend },
    ],
  });
  // 导出
  export default router;
  ```

  src / main.js

  ```javascript
  import Vue from "vue";
  import App from "./App.vue";
  import router from "./router/index";

  Vue.config.productionTip = false;

  new Vue({
    render: (h) => h(App),
    // router: router
    router,
  }).$mount("#app");
  ```

---

### 声明式导航与路由传参

- 标签写法

  vue-router 提供了一个全局组件 router-link，用于**取代 a 标签**

  ```html
  <!-- 以前的写法 -->
  <a href="#find">发现音乐</a>
  <!-- 新写法 -->
  <router-link to="/find">发现音乐</router-link>
  ```

  **router-link 必须配置 to 属性（省略 #），且默认实现高亮，无需 js 代码**

- 配置样式

  router-link 会被解析为 a 标签，且会添加两个类名：router-link-exact-active（精确匹配，即支持以 to="/find" 去匹配 /find） 和 router-link-active（模糊匹配，即支持以 to="/find" 去匹配 /find 及 /find/接后续路径），通常**为 router-link-active 添加样式**。

  ```vue
  <template>
    <div>
      <div class="footer_wrap">
        <router-link to="/find">发现音乐</router-link>
        <router-link to="/my">发现音乐</router-link>
        <router-link to="/friend">朋友</router-link>
      </div>
      <div class="top">
        <!-- router-view 匹配组件所展示的位置 放在哪里展示在哪里 -->
        <router-view></router-view>
      </div>
    </div>
  </template>

  <!-- 为 router-link-active 添加样式即可 -->
  <style>
  .footer_wrap a.router-link-active {
    background-color: purple;
  }
  </style>
  ```

- **自定义类名**

  默认添加的 router-link-exact-active 和 router-link-active 名字太长，支持自定义类名

  ```javascript
  const router = new VueRouter({
  // 创建路由对象，要在 main.js 导出
    routes: [...],
    // 输入 link 就会有代码提示
    linkActiveClass: "类名1",			// 配置模糊匹配类名
    linkExactActiveClass: "类名2"		// 配置精确匹配类名
  })
  ```

- **跳转传参的两种方法**<a id="路由传参">.</a>

  在路由跳转时，是可以传值的。有两种方式

  **查询参数传参（适合传多个参数）**的语法为：

  **to="/path?参数名=值"**（多个参数使用 & 连接），页面使用 **$route.query.参数名** 接收值

  ```html
  <!-- Home.vue -->
  <router-link to="/search?key=无修正">无修正</router-link>
  <router-link to="/search?key=姐姐系">姐姐系</router-link>
  <router-link to="/search?key=妹妹系">妹妹系</router-link>

  <!-- Search.vue -->
  <p>你想看的类型是: {{ $route.query.key }}</p>

  <script>
    export default {
      // 在 js 区获取的话，加个 this 即可
      created() {
        // 在 created 中获取路由参数
        console.log(this.$route.query.key);
      },
    };
  </script>
  ```

  **动态路由传参（简洁优雅，单个参数方便）**的语法为：

  **首先配置动态路由**（**使用 : + 参数名** ）

  可以在参数名后**加 ? 表示参数可选**，避免没穿参数显示空白页面的情况

  ```javascript
  // src / router / index.js
  const router = new VueRouter({
    routes: [
      { path: "/home", component: Home },
      // 使用 : + 参数名, ? 表示参数可选
      { path: "/search/:words?", component: Search },
    ],
  });
  ```

  传参使用 **to="/path/参数值"**，页面使用 **$route.params.参数名** 接收值

  ```html
  <!-- Home.vue -->
  <router-link to="/search/无修正">无修正</router-link>
  <router-link to="/search/姐姐系">牛头人</router-link>
  <router-link to="/search/妹妹系">妹妹系</router-link>
  <!-- Search.vue -->
  <p>你想看的类型是: {{ $route.params.words }}</p>

  <script>
    export default {
      // 在 js 区获取的话，加个 this 即可
      created() {
        // 在 created 中获取路由参数
        console.log(this.$route.params.words);
      },
    };
  </script>
  ```

---

### 重定向与模式设置 redirect, mode

**重定向：**网页打开时，url 默认为 .../#/ 路径，未匹配到任何组件时，会出现一片空白。希望一打开网页跳转到首页

- 需求 1：打开跳转到首页上

  语法为 { path: '匹配路径', redirect: '重定向到的路径' }

  ```javascript
  // src / router / index.js
  const router = new VueRouter({
    routes: [
      { path: "/", redirect: '/home' }
      { path: '/home', component: Home },
      { path: '/search/:words?', component: Search }
    ]
  })
  ```

- 需求 2：路径找不到匹配时，提示 404

  首先先建一个 404 的标题

  ```vue
  <!-- src / views / NotFound.vue -->
  <template>
    <div>
      <h1>404 Not Found</h1>
    </div>
  </template>
  ```

  然后再 index.js 引入，再使用 { path: '\*', redirect: NotFind }

  ```javascript
  import NotFound from "@/views/NotFound";

  const router = new VueRouter({
    routes: [
      { path: "/", redirect: "/home" },
      { path: "/home", component: Home },
      { path: "/search/:words?", component: Search },
      // 一旦上面所有匹配都未命中，就会名字这个 404
      { path: "*", component: NotFound },
    ],
  });
  ```

**模式设置：**路由的路径上有 # 不太自然，这种有 # 的路径属于 hash 路由，是默认模式，而生活常见的为 history 路由。

- 配置需要再 VueRouter 额外配置 **mode: "history"**，这种采用 history 模式上线时，url 上就**没有 #** 了。但需要服务器支持，**工作时和后台说**就可以

  ```javascript
  const router = new VueRouter({
    routes: [...],
    mode: "history"
  })
  ```

---

### 编程式导航 $router.push

以前通过 location.href 实现点击按钮跳转页面，在 Vue 路由中，由于页面是单页，不能通过此方法跳转。

- 两个跳转方法

  **path 路径跳转**（简易方便）：**this.$router.push('路由路径')**

  返回上一页可用 **$router.back( )**

  ```vue
  <button @click="goSearch">搜索一下</button>

  <script>
  export default {
    methods: {
      goSearch() {
        // 语法 1
        this.$router.push("/search");
        // 语法 2
        // this.$router.push({
        //   path: '/search'
        // })
      },
    },
  };
  </script>
  ```

  **name 命名路由跳转**（适合 path 路径较长）：**有一个前提，需要给路由起名**

  ```javascript
  const router = new VueRouter({
    routes: [
      { path: "/", redirect: "/home" },
      { path: "/home", component: Home },
      // 添加路由名字
      { name: "search", path: "/search/:words?", component: Search },
      { path: "*", component: NotFound },
    ],
  });
  ```

  然后**基于 name 使用 this.$router.push( { name: '路径名' } ) 实现跳转**

  ```vue
  <button @click="goSearch">搜索一下</button>

  <script>
  export default {
    methods: {
      goSearch() {
        this.$router.push({
          name: "search",
        });
      },
    },
  };
  </script>
  ```

- **传参：**请参考[跳转](#路由传参)，用哪种路由传参方式皆可。

  这是前面讲的第一种参数传参方法

  ```vue
  <!-- Home.vue -->
  <template>
    <div class="search-box">
      <input v-model="inpValue" type="text" />
      <button @click="goSearch">搜索一下</button>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        inpValue: "",
      };
    },
    methods: {
      goSearch() {
        // this.$router.push(`/search?key=${this.inpValue}`)
        // 完整写法
        this.$router.push({
          path: "/push",
          query: {
            key: this.inpValue,
          },
        });
      },
    },
  };
  </script>

  <!-- Search.vue -->
  <template>
    <div class="search">
      <p>你想看的类型是: {{ $route.query.key }}</p>
      <p>搜索结果:</p>
    </div>
  </template>
  ```

  这是第二种传参方法：

  准备工作 - 配置动态路由

  ```javascript
  const router = new VueRouter({
    routes: [
      { path: "/", redirect: "/home" },
      { path: "/home", component: Home },
      // : 动态路由
      { name: "search", path: "/search/:words?", component: Search },
      { path: "*", component: NotFound },
    ],
  });
  ```

  传参

  ```vue
  <!-- Home.vue -->
  <template>
    <div class="search-box">
      <input v-model="inpValue" type="text" />
      <button @click="goSearch">搜索一下</button>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        inpValue: "",
      };
    },
    methods: {
      goSearch() {
        // 注意这里没有 name
        // this.$router.push(`/search/${this.inpValue}`)
        // 完整写法
        this.$router.push({
          path: `/search/${this.inpValue}`,
        });
      },
    },
  };
  </script>

  <!-- Search.vue -->
  <template>
    <div class="search">
      <p>你想看的类型是: {{ $route.params.words }}</p>
      <p>搜索结果:</p>
    </div>
  </template>
  ```

  以上都是没有 name 的情况，**有 name 的话**，说明用的是 name 命名路由跳转，只需要注意动态路由传参的 $router.push( ) 里，**添加 name 即可**，然后注意动态路由传参中把 path 改为 params

  ```javascript
  // 这种是查询参数传参 只是添加了 name，还是用 query
  goSearch() {
    this.$router.push({
      name: 'search'
      query: {
        key: this.inpValue
      }
    })
  }
  // 这种是查询参数传参 添加了 name，改用 params
  goSearch() {
    this.$router.push({
      name: 'search'
      params: {
        words: this.inpValue
      }
    })
  }
  ```

---

### 路由总结与组件缓存 keep-alive

由于前面这些实在是太绕了，整理一下

- 首先是在 src / router / index.js 里 import VueRouter，Vue.use(VueRouter)， **const router = new VueRouter( )**，在里面写配置对象，根据路径是不是很长，**长的话起个名字 name**，对应 name 跳转方案，否则用 path 跳转方案。然后再导出 router

- 在 methods 中，**使用 this.$router.push(）**跳转，在里面写配置对象。**如果没起名字，就用 path 接路径，起名字了就用 name 接路径名**

- 有时跳转的同时也要传参，传参有两种方式，**记住 query 和 :** 。**还是使用 this.$router.push()**，在里面写配置对象。

  query 对应的是第一种方法，**适合多个传参**，无论起没起名字，都**用 query 接对象，对象里写参数**

  : 对应的是第二种方法，这种方法要求在 index.js 的 new VueRouter( ) 中，**在路径上使用 : 接收参数名**，然后在 this.$router.push() 内，**没名字的话，传参直接写在路径上**，**有名字用 params 接对象，对象里写参数**

【[案例 - 面经文章](#面经文章)】基于此案例学习**二级路由 - 页面切换**

- **组件缓存 keep-alive**

  在【[面经文章](#面经文章)】案例中，点到面经详情页，点击返回可以回到首页位置，但并不是用户当时跳转的位置，这是因为跳转会首页时重新加载了，没有缓存，**只需要用 `<keep-alive></keep-alive>` 包裹住首页中的 `<router-view></router-view>`** 就可以使跳转回页面时不是重新加载。且 keep-alive 是抽象组件，不会渲染成 DOM 元素。

  但是有些组件是不需要缓存的，使用上面方法会把所有备切换的组件都缓存，需要配置属性

  **include**：**组件名数组**，只有匹配的组件会被缓存，数组内的组件名优先会匹配 JS 区的组件名（name 的值），没有的话会匹配文件名

  ```html
  <!-- LayoutPage 是一个组件的 js 区起的名字 name -->
  <keep-alive :include="[LayoutPage]">
    <router-view></router-view>
  </keep-alive>
  ```

  exclude：组件名数组，任何匹配的组件都不会缓存

  max：最多可以缓存多少组件实例

  注意，一旦使用了 keep-alive 缓存组件，组件内的 created 和 mounted 与 destroyed 钩子不会执行，所以**提供了额外的两个钩子：activated 和 deactivated**

  ```vue
  <script>
  export default {
    // 这个 name 是组件名
    name: "LayoutPage",
    activated() {
      console.log("进入了页面");
    },
    deactivated() {
      console.log("离开了页面");
    },
  };
  </script>
  ```

---

## 第三方相关

### 自定义项目与 ESlint

- 自定义创建项目<a id="features">：</a>

  前面有个痛点，路由的配置项太多，其实可以在创建项目时，就把路由框架配置好，在创建项目时，选择 Manually select features

  ```bash
  Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection, and
  <enter> to proceed)
   (*) Babel
   ( ) TypeScript
   ( ) Progressive Web App (PWA) Support
   (*) Router
   (*) Vuex
   (*) CSS Pre-processors
  >(*) Linter / Formatter
   ( ) Unit Testing
   ( ) E2E Testing
    --------------------------------------
   Use history mode for router? (Requires proper server setup for index fallback in production) (Y/n) n
   这里选择 n 启动默认 hash 模式 - 在编程导航-模式设置处有说
   --------------------------------------
    Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default):
    Sass/SCSS (with dart-sass)
  > Less
    Stylus
    -------------------------------------
    ? Pick a linter / formatter config:
    ESLint with error prevention only
    ESLint + Airbnb config
  > ESLint + Standard config                                选择第三个 - 代码无分号规范
    ESLint + Prettier
    -------------------------------------
    Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to
  proceed)
  >(*) Lint on save                                         保存时校验
   ( ) Lint and fix on commit (requires Git)
    --------------------------------------
    Where do you prefer placing config for Babel, ESLint, etc.? (Use arrow keys)
  > In dedicated config files                               将配置文件放在单独文件中
    In package.json
    --------------------------------------
    Save this as a preset for future projects? (y/N) n      以上设置保存为预设
  ```

- 代码规范

  比如字符串使用单引号，代码无分号，关键字后加空格，函数名后加空格等。引入 ESlint 后，不符合规范也会报错

- 修正错误：可以根据报错手动修正，或者下载 ESlint 插件并配置 VScode 设置 json（设置的右上角）

  ```json
  // 保存时 ESlint 自动修复代码错误
  "editor.codeActionsOnSave": {
      "source.fixAll": true
  },
  // 保存代码不自动格式化
  "editor.formatOnSave": false
  ```

---

### json-server

当后端没有提供接口时，可以利用 json-server 快速生成一套增删改查的接口

- 步骤

1. 安装 json-server

   ```bash
   npm install -g json-server
   ```

   或

   ```bash
   yarn global add json-server
   ```

2. 在项目中新建一个 db 文件夹，数据源 json 放在这里，在 db 文件夹内运行

   ```bash
   json-server --watch 文件名
   ```

   成功后浏览器就可以用 `http://localhost:3000/键/` 访问到相应数据了

---

## vuex

vuex 是 vue 的一个状态管理工具，状态就是数据（vuex 是一个插件，可以帮我们管理 vue 通用的数据）

- 优势：共同维护一份数据，数据集中化处理，响应式，操作简洁
- 语法：**多组件公用数据**，存放数据的地方叫仓库

1. 安装 vuex（vue2 对应版本为 3，vue3 对应版本为 4）

   ```bash
   yarn add vuex@3
   ```

2. 新建 src / store / index.js 存放 vuex

3. 使用 Vue.use(Vuex) 以安装 vuex 插件，使用 new Vuex.Store() 以创建仓库

   ```javascript
   import Vue from "vue";
   import Vuex from "vuex";

   // 插件安装
   Vue.use(Vuex);

   // 创建仓库
   const store = new Vuex.Store();

   // 导出给 main.js
   export default store;
   ```

4. 在 main.js 中导入挂载

   ```javascript
   import Vue from "vue";
   import App from "./App.vue";
   import store from "@/store/index";

   Vue.config.productionTip = false;

   new Vue({
     render: (h) => h(App),
     store,
   }).$mount("#app");
   ```

---

### $store.state 与 mapState([ ])

- 提供数据

  所有共享的数据都要放到 Store 中的 State 中存储，在 Store 配置项中写 state 对象

  ```javascript
  // 创建仓库
  const store = new Vuex.Store({
    // 通过 state 可以提供数据
    state: {
      title: "大标题",
      count: 101,
    },
  });
  ```

- 使用数据

1. 第一种方法直接找到仓库访问

   **模板中：{{ $store.state.xxx }} 组件逻辑中：this.$store.state.xxx**

   ```vue
   <template>
     <div id="app">
       <h1>根组件 - {{ $store.state.title }}</h1>
     </div>
   </template>
   <script>
   export default {
     name: "app",
     created() {
       console.log(this.$store.state.count);
     },
   };
   </script>
   ```

   import 导入 store 后在 JS 文件中： store.state.xxx

   ```javascript
   import store from "@/store/index";
   console.log(store.state.count);
   ```

2. 第二种方法使用辅助函数访问

   mapState 辅助函数会把 store 的数据自动映射到组件的计算属性中

   **先导入 mapState，再在 computed 中展开映射（数组里放要映射的属性），使用属性**

   ```vue
   <template>
     <div id="app">
       <!-- 这种方法可以直接写数据 -->
       <h1>根组件 - {{ title }}</h1>
     </div>
   </template>

   <script>
   import { mapState } from "vuex";

   export default {
     name: "app",
     computed: {
       // 如果直接 computed: mapState(['count', 'title'] 就没法写其他计算属性了
       // 所以建议这样子展开
       ...mapState(["count", "title"]),
     },
   };
   </script>
   ```

---

### 修改数据 mutations 与 commit

- **修改数据**

  首先明确一点，vuex 同样遵循单向数据流，组件不能直接修改仓库的数据直接使用 $store.state.count++ 是错误的语法，但不会报错，初学时可在 new Vuex.Store() 里添加配置项 strict: true 开启严格模式报错，上线时记得移除。

  **修改数据请在 new Vuex.Store( ) 内配置 mutations: { }，在里面定义修改数据的函数**

  ```javascript
  const store = new Vuex.Store({
    // 通过 state 可以提供数据
    state: {
      count: 101,
    },
    // 使用 mutations 修改数据
    mutations: {
      // 可以传参
      addCount(state, n) {
        state.count += n;
      },
    },
  });
  ```

  **然后在需要修改数据的组件的 JS 区使用 this.$store.commit( ) 提交调用 mutations，传参的话放在后面，但只能传一个，多个参数的话请使用复杂数据类型做处理**

  ```vue
  <template>
    <div class="box">
      从vuex中获取的值: {{ $store.state.count }}<label></label>
      <br />
      <button @click="handleAdd(1)">值 + 1</button>
      <button @click="handleAdd(5)">值 + 5</button>
    </div>
  </template>

  <script>
  export default {
    methods: {
      handleAdd(n) {
        this.$store.commit("addCount", n);
      },
    },
  };
  </script>
  ```

- 输入框实时输入修改数据

  **不要用 v-model 跟 vuex 的数据绑定！**因为要遵循单向数据流，只能使用 mutation 修改数据。

  v-model 等于 :value 与 @input，所以正确方法是**用 :value 进行输入渲染，用 @input 监听输入内容，再封装 mutation 处理函数，commit 调用传参。**

  src / store / index.js

  ```javascript
  const store = new Vuex.Store({
    state: {
      count: 101,
    },
    mutations: {
      changeCount(state, newCount) {
        state.count = newCount;
      },
    },
  });
  ```

  src / App.vue

  ```vue
  <template>
    <div id="app">
      <h1>根组件 - {{ title }}</h1>
      <!-- :value 输入框渲染, @input 监听输入框数据 -->
      <input :value="count" @input="handleInput" type="text" />
    </div>
  </template>

  <script>
  import { mapState } from "vuex";

  export default {
    name: "app",
    computed: {
      ...mapState(["count", "title"]),
    },
    methods: {
      handleInput(e) {
        // + 把字符串转化为数字
        this.$store.commit("changeCount", +e.target.value);
      },
    },
  };
  </script>
  ```

---

### 辅助函数 mapMutations([ ])

mapMutations 与 mapState 使用方法非常像，可以把 mutations 中的方法提取出来，映射到组件 methods 中

- **先导入 mapMutations，再 methods 里 ...mapMutations 展开**

  src / store / index.js

  ```javascript
  const store = new Vuex.Store({
    // 通过 state 可以提供数据
    state: {
      title: "大标题",
      count: 101,
    },
    // 使用 mutations 修改数据
    mutations: {
      addCount(state, n) {
        state.count += n;
      },
      changeCount(state, newCount) {
        state.count = newCount;
      },
    },
  });
  ```

  src / components / Son.vue

  ```vue
  <template>
    <div class="box">
      <h2>Son1 子组件</h2>
      从vuex中获取的值: {{ count }}<label></label>
      <br />
      <button @click="addCount(1)">值 + 1</button>
      <button @click="addCount(5)">值 + 5</button>
    </div>
  </template>

  <script>
  // mapState 用来简化数据的使用 - $store.state.count
  // mapMutations 用来简化数据的修改 - $store.commit
  import { mapState, mapMutations } from "vuex";
  export default {
    computed: {
      ...mapState(["count", "title"]),
    },
    methods: {
      ...mapMutations(["addCount"]),
      // 相当于帮你完成了 this.$store.commit 的部分
    },
  };
  </script>
  ```

---

### 异步操作 actions 与 mapActions([ ])

- 需求：一秒钟后修改数据（**模拟发送请求渲染数据**），前面的 mutations 是同步的

- 方法：需要**在 new Vuex.Store( ) 提供一个 actions 方法**，在里面使用 commit 配合 mutations 修改数据

  src / store / index.js

  ```javascript
  const store = new Vuex.Store({
    // state 提供数据
    state: {
      title: "大标题",
      count: 101,
    },
    // mutations 修改数据
    mutations: {
      addCount(state, n) {
        state.count += n;
      },
      changeCount(state, newCount) {
        state.count = newCount;
      },
    },
    // 处理异步, actions 不能直接操作 state
    actions: {
      // context 为上下文（store 仓库）
      changeCountAction(context, num) {
        // setTimeout 模拟异步，真实场景为发送请求
        setTimeout(() => {
          context.commit("changeCount", num);
        }, 1000);
      },
    },
  });
  ```

  在组件的 **methods 处，使用 this.$store.dispatch( 'actions 名字', 额外参数 )**

  src / components / Son.vue

  ```vue
  <template>
    <div class="box">
      <button @click="handleChange">一秒后修改成 666</button>
    </div>
  </template>

  <script>
  import { mapState, mapMutations } from "vuex";
  export default {
    methods: {
      handleChange() {
        // this.$store.dispatch('actions 名字', 额外参数)
        this.$store.dispatch("changeCountAction", 666);
      },
    },
  };
  </script>
  ```

- **mapActions([ ])**

  和前面一样，**先导入{ mapActions }，再在 methods 内使用 mapActions([ ])**

  src / store / index.js

  请参考上面的 index.js 内容，主要看 actions

  src / components / Son.vue

  ```vue
  <template>
    <div class="box">
      <h2>Son1 子组件</h2>
      从vuex中获取的值: {{ count }}<label></label>
      <br />
      <button @click="addCount(1)">值 + 1</button>
      <button @click="addCount(5)">值 + 5</button>
      <button @click="changeCountAction(666)">一秒后修改成 666</button>
    </div>
  </template>

  <script>
  // mapState 用来简化数据的使用 - $store.state.count
  // mapMutations 用来简化数据的修改 - $store.commit
  // mapActions 用来简化数据异步的修改 - $store.dispatch
  import { mapState, mapMutations, mapActions } from "vuex";
  export default {
    computed: {
      ...mapState(["count", "title"]),
    },
    methods: {
      ...mapMutations(["addCount"]),
      ...mapActions(["changeCountAction"]),
    },
  };
  </script>
  ```

---

### 数据派生 getters 与 mapGetters([ ])

类似于计算属性 computed，数据派生就是说对数据操作（过滤），依赖于原数据得到新结果。

- 需求：state 内有一个数组，内有 1-10，展示时想展示 >5 的数（**带条件并实时更新**）

- **访问 getters**

  与 state 并列，可以在 getters 中展示一系列函数，**第一形参为 state，且 getters 函数必须要有返回值。**

  访问 getters 有两种方法，使用 store 访问或使用辅助函数 mapGetters 映射

  src / store / index.js

  ```javascript
  const store = new Vuex.Store({
    // 通过 state 可以提供数据
    state: {
      title: "大标题",
      count: 101,
      list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    },
    // 类似于计算属性(第一形参为 state，必须有返回值)
    getters: {
      filterList(state) {
        return state.list.filter((item) => item > 5);
      },
    },
  });
  ```

1. **使用 store 访问**

   ```vue
   <template>
     <div class="box">
       <!-- [1, ..., 10] -->
       <div>{{ $store.state.list }}</div>
       <!-- [6, ..., 10] -->
       <div>{{ $store.getters.filterList }}</div>
     </div>
   </template>
   ```

2. **使用辅助函数 mapGetters([ ])**

   ```vue
   <template>
     <div class="box">
       <div>{{ filterList }}</div>
     </div>
   </template>

   <script>
   import { mapState, mapMutations, mapActions, mapGetters } from "vuex";
   export default {
     name: "Son1Com",
     computed: {
       // mapState 和 mapGetters 都在映射属性
       ...mapState(["count"]), // mapState 用来简化数据的使用 - $store.state.count
       ...mapGetters(["filterList"]), // mapGetters 用来简化数据的派生状态 - $store.getters
     },
     methods: {
       // mapMutations 和 mapActions 都在映射 methods
       ...mapMutations(["addCount"]), // mapMutations 用来简化数据的修改 - $store.commit
       ...mapActions(["changeCountAction"]), // mapActions 用来简化数据异步的修改 - $store.dispatch
     },
   };
   </script>
   ```

---

### 模块 module 的四种数据处理

vuex 是单一状态树，通常会为 state 提供一个对象，项目变大时，store 会臃肿，可以**把数据拆分成一个个模块**。

- 方法

  首先**在 store / modules 下建立多个 js 文件，每一个 js 文件就是一个模块**，模块中要**声明四个配置项并导出**

  store / modules / userInfo.js

  ```javascript
  // 声明好四个配置项
  const state = {
    // state 放数据
    userInfo: {
      name: "zs",
      age: 18,
    },
    score: 80,
  };
  // mutations 修改数据
  const mutations = {
    setUser(state, newUserinfo) {
      state.userInfo = newUserinfo;
    },
  };
  // actions 处理异步请求
  const actions = {
    // context 为上下文，默认提交的就是自己模块的 action 和 mutation
    setUserSecond(context, newUserinfo) {
      // 将异步在 action 中进行封装
      setTimeout(() => {
        // 一秒后调用 mutation
        context.commit("setUser", newUserinfo);
      }, 1000);
    },
  };

  // getters 数据派生
  const getters = {
    // 分模块后，state 指子模块的 state
    // 转换为大写
    UpperCaseName(state) {
      return state.userInfo.name.toUpperCase();
    },
  };

  // 导出
  export default {
    state,
    mutations,
    actions,
    getters,
  };
  ```

  然后在 store / **index.js 内导入并在 modules（与 store 并列） 挂载**

  ```javascript
  // 导入
  import user from "./modules/user";

  const store = new Vuex.Store({
    // 模块挂载
    modules: {
      user,
    },
  });
  ```

  由于内容过长，快速跳转【[数据访问](#a) / [数据派生](#b) / [数据修改](#c) / [数据异步](#d)】

- 模块下的**数据访问**<a id="a">.</a>[查看配置项](#模块 module 的四种数据处理)

  虽然分了模块，但子模块还是会挂载到根级别的 state 中，属性名就是模块名，所以访问数据可以从根出发访问到。

  数据访问的方法：

1. 使用 **$store.state.模块名.xxx**（相当于从根访问）

   ```vue
   <template>
     <div class="box">
       <div>{{ $store.state.user.userInfo.name }}</div>
     </div>
   </template>
   ```

2. **通过 mapState 映射**

   普通的映射

   ```vue
   <template>
     <div class="box">
       <div>{{ user.userInfo.name }}</div>
     </div>
   </template>

   <script>
   import { mapState } from "vuex";
   export default {
     computed: {
       // 还是普通的映射方法
       ...mapState(["count", "user"]),
     },
   };
   </script>
   ```

   按模块映射：**mapState('模块名', ['xxx'])** - **需要在导出时开启命名空间**

   src / store / modules / user.js 导出的位置**设置 namespaced: true**

   ```javascript
   export default {
     namespaced: true,
     state,
     mutations,
     actions,
     getters,
   };
   ```

   然后就可以按模块名访问渲染数据了

   ```vue
   <template>
     <div class="box">
       <div>{{ userInfo.name }}</div>
     </div>
   </template>

   <script>
   import { mapState } from "vuex";
   export default {
     computed: {
       // 然后就可以按模块映射了
       ...mapState("user", ["userInfo"]),
     },
   };
   </script>
   ```

- 模块下的**数据派生**<a id="b">.</a>[查看配置项](#模块 module 的四种数据处理)

1. 使用 **$store.getters[模块名/xxx]**

   这个乍看和前面不一样很别扭，是因为 getter 相当于在根下加了个 模块名/xxx 的属性，这个属性因为带 / ，很特殊不能直接访问。访问这种特殊符号的属性要用 [] 包裹，并用字符串包裹。所以才看变成了这副模样。

   ```vue
   <template>
     <div class="box">
       <div>{{ $store.getters["user/UpperCaseName"] }}</div>
     </div>
   </template>
   ```

2. **通过 mapGetters 映射**

   根据别映射：mapGetters(['xxx'])

   【基本和前面的 mapState 差不多，略了】

   子模块的映射：**mapGetters('模块名', ['xxx']) - 需开启 namespaced**

   ```vue
   <template>
     <div class="box">
       <div>{{ UpperCaseName }}</div>
     </div>
   </template>

   <script>
   import { mapGetters } from "vuex";
   export default {
     computed: {
       ...mapGetters("user", ["UpperCaseName"]),
     },
   };
   </script>
   ```

- 模块下的**数据修改**<a id="c">.</a>[查看配置项](#模块 module 的四种数据处理)

  mutations 和 actions 默认会挂载到全局，那非常不合理也不好维护，所以这两个**无论原生还是 map 映射，都要开启命名空间**

1. 使用 **$store.commit('模块名/xxx', 额外参数)**

   ```vue
   <template>
     <div class="box">
       <button @click="updateUser">更新个人信息</button>
     </div>
   </template>

   <script>
   export default {
     methods: {
       updateUser() {
         // commit('模块名/mutation名', 额外传参 - 一个)
         this.$store.commit("user/setUser", {
           name: "tieniu",
           age: 1,
         });
       },
     },
   };
   </script>
   ```

2. **通过 mapMutations 映射**

   根据别映射：mapMutations(['xxx'])

   【基本和前面的 mapState 差不多，略了】

   子模块的映射：**mapMutations('模块名', ['xxx']) - 需开启 namespaced**

   ```vue
   <template>
     <div class="box">
       <button @click="setUser({ name: 'tieniu', age: 100 })">
         更新个人信息
       </button>
     </div>
   </template>

   <script>
   import { mapMutations } from "vuex";
   export default {
     methods: {
       ...mapMutations("user", ["setUser"]),
     },
   };
   </script>
   ```

- 模块下的**数据异步**<a id="d">.</a>[查看配置项](#模块 module 的四种数据处理)

  mutations 和 actions 默认会挂载到全局，那非常不合理也不好维护，所以这两个**无论原生还是 map 映射，都要开启命名空间**

1. 使用 **$store.dispatch('模块名/xxx', 额外参数)**

   ```vue
   <template>
     <div class="box">
       <button @click="updateUser">一秒后更新信息</button>
     </div>
   </template>

   <script>
   export default {
     methods: {
       updateUser() {
         // dispatch('模块名/action名', 额外传参 - 一个)
         this.$store.dispatch("user/setUserSecond", {
           name: "tieniu",
           age: 20,
         });
       },
     },
   };
   </script>
   ```

2. **通过 mapActions 映射**

   根据别映射：mapActions(['xxx'])

   【基本和前面的 mapState 差不多，略了】

   子模块的映射：**mapActions('模块名', ['xxx']) - 需开启 namespaced**

   ```vue
   <template>
     <div class="box">
       <button @click="setUserSecond({ name: 'tieniu', age: 100 })">
         一秒后更新个人信息
       </button>
     </div>
   </template>

   <script>
   import { mapActions } from "vuex";
   export default {
     methods: {
       ...mapActions("user", ["setUserSecond"]),
     },
   };
   </script>
   ```

   【[案例 - 购物车案例](#购物车案例)】

---

# Vue3

vue3 兼容支持 vue2，适合 Ts，总之就是好

## 项目创建

vue3 推荐使用 create-vue 创建项目，**基于 Vite 构建工具**

**核心步骤：**

1. 环境条件：已安装 16.0 或更高版本的 node.js，使用`node-v` 查看版本

2. 项目初始化：npm init vue@latest

3. 在项目目录安装依赖：npm install

4. 启动项目：npm run dev / yarn dev

5. 成功后访问 `http://127.0.0.1:5173/`

**额外注意：**禁用 Vetur（vue2），**使用 Vue Language Features (Volar)**

**文件结构：**

1. vite.config.js 项目配置文件（基于 vite 配置）
2. package.json 项目包文件（核心依赖项变成 vue3.x 和 vite）
3. main.js 入口文件（createApp 函数创建应用实例）
4. app.vue 根组件（SFC 单文件组件 script - template - style）
5. index.html 单页入口（提供 id 为 app 的挂载点）

main.js

```javascript
import "./assets/main.css";

import { createApp } from "vue";
import App from "./App.vue";

// mount 设置挂载点 #app（id 为 app 的盒子）
createApp(App).mount("#app");
```

App.vue

```vue
<!-- 加上 setup 允许在 script 中直接编写组合式API -->
<!-- 且组件导入后无需注册 -->
<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
</script>

<template>
  <!-- 不再要求唯一根元素 -->
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
```

---

## 组合式 API

对应前面学的 data() + methods + computed + watch，这种叫选项式 API，把代码散落在各个配置项中，难以维护。而组合式 API 按功能集中管理。

### setup 选项

setup( ) 与生命周期钩子类似，在 JS 区直接写。setup 执行顺序比 beforeCreate( ) 还要早，所以 **setup 函数中获取不到 this**

**setup( ) 中可以提供数据与函数，在 template 中使用必须要 return**

但每次都要 return，所以**直接在 `<script>` 标签内写 setup**，就会自动帮你写好 return

---

### reactive 与 ref 响应对象

- **reactive**

  **接收对象**类型数据的参数传入，并**返回一个响应式的对象**。

  **步骤：**导包 + 使用（reactive( 包对象 )）

  ```vue
  <script setup>
  // reactive: 接收一个对象类型的数据，返回一个响应式对象
  import { reactive } from "vue";
  const state = reactive({
    count: 100,
  });
  const setCount = () => {
    state.count++;
  };
  </script>

  <template>
    <div>{{ count }}</div>
    <button @click="setCount">+1</button>
  </template>
  ```

- **ref( )**

  接收**简单类型或复杂类型的数据**传入并**返回一个响应式的对象**

  **步骤：**导包 + 使用（ref( 数据 )）

  ```vue
  <script setup>
  // 底层 ref 对简单数据类型包成了对象再借助 reactive
  import { ref } from "vue";
  const count = ref(0); // count 为对象
  console.log(count.value); // 在 JS 区访问需要 value
  const setCount = () => {
    count.value++; // 让对象里的值加一
  };
  </script>

  <template>
    <div>
      <!-- 在 template 中，访问无需 value（帮你处理好了） -->
      <div>{{ count }}</div>
      <button @click="setCount">+1</button>
    </div>
  </template>
  ```

  综上**声明数据建议统一使用 ref**

---

### computed 计算属性

计算属性与 vue2 基本一致，只是修改了写法。计算属性中应只包含对数据的操作，不应该出现异步请求，操作 DOM 等。

计算属性应为只读，特殊情况可以配置 get 与 set

- **步骤：**导包 + 使用

  ```vue
  <script setup>
  import { computed, ref } from "vue";
  // 声明数据用 ref
  const list = ref([1, 2, 3, 4, 5, 6, 7, 8]);
  // 基于 list 派生计算属性，从 list 中过滤出 > 2
  const computedList = computed(() => {
    // list 是对象
    return list.value.filter((item) => item > 2);
  });
  </script>

  <template>
    <div>
      <!-- 在 template 中，访问无需 value -->
      <div>{{ list }}</div>
      <div>{{ computedList }}</div>
    </div>
  </template>
  ```

- get - set

  不同于基础写法，带了 set 就可以**可读可写**，其他一致。

  ```js
  const selectedCoin = computed({
    get: () => props.selected,
    set: (value) => {
      emit("update:selected", value);
    },
  });
  ```

---

### watch 监听

watch 可以**监听一个或多个数据的变化，数据变化时执行回调函数**，watch 监视的第一个参数是 ref 对象，不需要加 value

- 步骤：导包 + 使用

  单个数据变化：**watch ( ref 对象, ( newValue, oldValue ) => { ... } )**

  多个数据变化：**watch ( [ref 对象 1, ref 对象 2], ( newArr, oldArr ) => { ... } )**

  ```vue
  <script setup>
  import { ref, watch } from "vue";
  const count = ref(0);
  const nickname = ref("张三");
  const changeCount = () => {
    count.value++;
  };
  const changeNickname = () => {
    nickname.value = "铁牛";
  };
  // 监视单个数字 0 的变化
  // watch(ref对象, (newvalue, oldvalue) => { ... })
  watch(count, (newValue, oldValue) => {
    console.log(newValue, oldValue);
  });
  // 监视多个数据的变化
  // watch([ref对象1, ref对象2], (newArr, oldArr) => { ... })
  watch([count, nickname], (newArr, oldArr) => {
    console.log(newArr, oldArr);
  });
  </script>

  <template>
    <div>
      <div>{{ count }}</div>
      <button @click="changeCount">改数字</button>
      <div>{{ nickname }}</div>
      <button @click="changeNickname">改昵称</button>
    </div>
  </template>
  ```

- **deep 与 immediate**

  上面的监视只能监视普通类型，复杂类型内的变化监视不到，需开启 deep

  希望一进页面就监视一次，需开启 immediate

  **使用方法：作为 watch 的第三个对象参数**

  ```vue
  <script setup>
  import { ref, watch } from "vue";
  const userInfo = ref({
    name: "铁牛",
    age: 18,
  });
  const setUserInfo = () => {
    userInfo.value.age++;
  };
  watch(
    userInfo,
    (newValue) => {
      console.log(newValue);
    },
    {
      deep: true,
      // immediate: true
    }
  );
  </script>

  <template>
    <div>
      <div>{{ userInfo }}</div>
      <button @click="setUserInfo">改userInfo</button>
    </div>
  </template>
  ```

- 特殊需求：只想监听某一对象的某一属性，deep 会监听整个对象，不能精确监听一个属性。

  **使用特殊语法** - 两个回调函数

  ```vue
  <script setup>
  import { ref, watch } from "vue";
  const userInfo = ref({
    name: "铁牛",
    age: 18,
  });
  const setUserInfo = () => {
    userInfo.value.age++;
  };
  // 只监视单一属性 age 的变化，使用特殊语法 - 两个回调
  watch(
    () => userInfo.value.age,
    (newValue, oldValue) => {
      console.log(newValue, oldValue);
    }
  );
  </script>

  <template>
    <div>
      <div>{{ userInfo }}</div>
      <button @click="setUserInfo">改userInfo</button>
    </div>
  </template>
  ```

---

### 生命周期函数

- 选项式与组合式

  |       选项式 API       |     组合式 API      |
  | :--------------------: | :-----------------: |
  | beforeCreate / created |      **setup**      |
  |      beforeMount       |    onBeforeMount    |
  |        mounted         |      onMounted      |
  |      beforeUpdate      |   onBeforeUpdate    |
  |        updated         |      onUpdated      |
  |     beforeUnmount      | **onBeforeUnmount** |
  |       unmounted        |   **onUnmounted**   |

- 示例：

  ```vue
  <script setup>
  import { onMounted } from "vue";

  // beforeCreate 与 created 的代码放在 setup 内
  const getList = () => {
    setTimeout(() => {
      console.log("发送请求，获取数据");
    }, 2000);
  };
  getList();

  // 有的代码需要在 mounted 内执行的话
  onMounted(() => {
    console.log("mounted 生命周期函数 - 逻辑1");
  });
  // 调用多次不会冲突，按照顺序依次执行
  onMounted(() => {
    console.log("mounted 生命周期函数 - 逻辑2");
  });
  </script>
  ```

---

### 父子通信 defineProps, defineEmits

**父传子 defineProps**

- **基本思想：**

  父组件中给子组件绑定属性，子组件内部通过 props 选项接收，设置了 setup 没法直接写 props，使用 **defineProps( { } ）** 接收传过来的值，传递的值是响应式数据

  App.vue

  ```vue
  <script setup>
  import { ref } from "vue";
  import Son from "@/components/son-com.vue";

  const money = ref("一百万");
  </script>

  <template>
    <div>
      <h3>父亲有{{ money }}</h3>
      <Son :money="money"></Son>
    </div>
  </template>
  ```

  son-com.vue

  ```vue
  <script setup>
  // 由于写了 setup 没有直接配置 props 选项
  // 借助编译器宏函数，接受组件传递的数据
  const props = defineProps({
    money: String,
  });
  console.log(props.money); // JS 区访问要用 props.
  </script>

  <template>
    <!-- 模板区访问直接使用即可 -->
    <div class="son">我是子组件，我有{{ money }}</div>
  </template>
  ```

**子传父 defineEmits + emit + @**

- **基本思想：**

  父组件中给子组件标签通过@绑定事件，子组件内部通过 emit 方法触发事件，不再是 this.$emit 是因为在 setup 中没有 this。

  子组件需要使用 **defineEmits( [ 事件名 ] )** 生成 emit 方法，再使用 emit 方法触发事件传递值，父组件监听此事件以获取值。

  son-com.vue

  ```vue
  <script setup>
  // 使用 defineEmits 规定可触发的事件名 - 使用数组
  const emit = defineEmits(["changeMoney"]);

  const buy = () => {
    // 使用 emit 触发事件并传递值
    emit("changeMoney", 5);
  };
  </script>

  <template>
    <div class="son">
      我是子组件
      <button @click="buy">点击氪金 95 元</button>
    </div>
  </template>
  ```

  App.vue

  ```vue
  <script setup>
  import { ref } from "vue";
  import Son from "@/components/son-com.vue";

  const money = ref(100);
  const changeFn = (newMoney) => {
    // 接收子组件传来的形参
    money.value = newMoney;
  };
  </script>

  <template>
    <div>
      <h3>父亲有{{ money }}</h3>
      <!-- @ 监听事件 -->
      <Son @changeMoney="changeFn"></Son>
    </div>
  </template>
  ```

---

### 查找组件 defineExpose

- 思想：调用 ref 函数，生成一个 ref 对象。通过 ref 标识，进行绑定。渲染完成后，通过 ref 对象.value 即可访问到绑定的元素

  ```vue
  <script setup>
  import { onMounted, ref } from "vue";

  // 先生成一个 ref 对象
  const inp = ref(null);
  onMounted(() => {
    // 等 DOM 渲染完触发
    // 使用 .value 即可访问元素
    inp.value.focus();
  });
  const clickFn = () => {
    inp.value.focus();
  };
  </script>

  <template>
    <div>
      <!-- 再通过 ref 标识进行绑定 -->
      <input ref="inp" type="text" />
      <button @click="clickFn">点击让输入框聚焦</button>
    </div>
  </template>
  ```

- **defineExpose**

除了获取元素，还可以获取组件，方法相同，获取组件一般是为了使用组件内的属性与方法。**但组件内的属性和方法是不开放给父组件访问的。需要使用 defineExpose 编译宏指定哪些属性和方法允许访问。**

test-com.vue

```vue
<script setup>
const count = 999;
const sayHi = () => {
  console.log("呀哈哈");
};
// 使用 defineExpose 指定哪些属性/方法可暴露
defineExpose({
  count,
  sayHi,
});
</script>

<template>
  <div>我是用来测试的组件</div>
</template>
```

App.vue

```vue
<script setup>
import TestCom from "@/components/test-com.vue";
import { ref } from "vue";

const testRef = ref(null);
const getCom = () => {
  console.log(testRef.value.count); // 获取组件一般用来获取此组件内的一些数据与方法
  testRef.value.sayHi();
};
</script>

<template>
  <div>
    <TestCom ref="testRef"></TestCom>
    <button @click="getCom">获取组件</button>
  </div>
</template>
```

---

### 跨层级通信 provide, inject

- 思想：**顶层组件通过 provide ( ) 提供数据，底层组件通过 inject ( ) 获取数据**

- 传递普通数据

  App.vue

  ```vue
  <script setup>
  import CenterCom from "@/components/center-com.vue";
  import { provide } from "vue";

  // 此案例为顶层 App 包裹 center 包裹 bottom
  // provide('键', 值)
  provide("theme-color", "pink");
  </script>

  <template>
    <div>顶层组件</div>
    <CenterCom></CenterCom>
  </template>
  ```

  bottom-com.vue ( App.vue 使用 CenterCom 组件，CenterCom 组件使用此组件 )

  ```vue
  <script setup>
  import { inject } from "vue";
  // 跨层级传递普通数据
  const themeColor = inject("theme-color");
  </script>

  <template>
    <h3>底层组件 - {{ themeColor }}</h3>
  </template>
  ```

- 传递响应式数据（使用 ref 配合 provide 与 inject 即可）

  注意一个原则，**谁的数据谁来维护**。

  修改数据的方法要和提供数据处写在一起，子孙组件想修改数据，通过 inject 获取方法，使用自己的方法调用顶层组件的方法，以传参修改数据、

  App.vue

  ```vue
  <script setup>
  import CenterCom from "@/components/center-com.vue";
  import { provide, ref } from "vue";

  const count = ref(100);
  provide("count", count);

  // 原则：谁的数据谁来维护
  // 为子孙组件共享一个修改数据的方法
  provide("changeCount", (newCount) => {
    count.value = newCount;
  });
  </script>

  <template>
    <div>顶层组件</div>
    <CenterCom></CenterCom>
  </template>
  ```

  bottom-com.vue

  ```vue
  <script setup>
  import { inject } from "vue";
  // 跨层级传递普通数据
  const count = inject("count");
  const changeCount = inject("changeCount");
  const clickFn = () => {
    changeCount(1000);
  };
  </script>

  <template>
    <h3>底层组件 - {{ count }}</h3>
    <!-- 通过函数触发数据源组件的函数以修改值 -->
    <button @click="clickFn">更新count</button>
  </template>
  ```

---

### defineOptions

vue3 刚出来时，setup 一般作为函数去写，当时 props，emits 与 setup 平级，有了 `<script setup>` 后，无法添加与 setup 平级的属性了。

vue 3.3 以上引入了 defineOptions 宏，可以定义任意选项，props，emits，expose，slots 除外（因为这些可以使用 definexxx 定义）

- 示例：

  src / components / index.js ( 不起 name 的话，这种单一单词会报错，必须要多个单词才行 )

  ```vue
  <script setup>
  defineOptions({
    name: "LoginIndex",
  });
  </script>

  <template>
    <div>登录页</div>
  </template>
  ```

---

### defineModel（需要导包 + 配置）

此功能属于实验性质，实现数据双向绑定，简化 v-model，使用此功能需要导包，并且设置额外配置。

- 背景：

  vue2 中的 v-model 是 :value + @input 的组合，vue3 中：

  ```vue
  <Child v-model="isVisible">
  <!-- 相当于 -->
  <Child :modelValue="isVisible" @update:modelValue="isVisible=$event">
  ```

  相当于传递了一个 modelValue 属性，同时触发 update: modelValue 事件。这导致底层比较麻烦：组件内部先定义 props 接收，再定义 emits ，通过 emits 触发事件，修改值的话还要修改 emit 函数。

- 使用：

1. 首先要在 vite.config 内添加配置：

   ```javascript
   export default defineConfig({
     plugins: [
       vue({
         // 在这里添加配置
         script: {
           defineModel: true,
         },
       }),
     ],
     resolve: {
       alias: {
         "@": fileURLToPath(new URL("./src", import.meta.url)),
       },
     },
   });
   ```

2. 父组件内还是使用 v-model 传递数据

   ```vue
   <script setup>
   import MyInput from "@/components/my-input.vue";
   import { ref } from "vue";
   const txt = ref(123456);
   </script>

   <template>
     <div>
       <!-- v-model 与数据做绑定 -->
       <MyInput v-model="txt"></MyInput>
       {{ txt }}
     </div>
   </template>
   ```

3. 子组件导包 defineModel，使用 const modelValue = defineModel() 接收数据，就可以直接双向绑定修改了

   ```vue
   <script setup>
   import { defineModel } from "vue";
   // 引入 defineModel 后，不再需要 props 来接收数据
   const modelValue = defineModel();
   // 这里的 modelValue 可以直接当成 props 了
   </script>

   <template>
     <div>
       <!-- 而且父组件传来的数据可以直接诶修改了! 不再需要 emit -->
       <input
         type="text"
         :value="modelValue"
         @input="(e) => (modelValue = e.target.value)"
       />
     </div>
   </template>
   ```

---

## Pinia

Pinia 是 Vue 最新的状态管理工具，是 Vuex 的替代品（wcnm)

- 优点：提供简单组合式 API，去除 mutation， 去除 modules，配合 TypeScript

- 安装：

  ```bash
  npm install pinia
  ```

  使用：

  ```javascript
  import { createPinia } from "pinia"; // 导包
  const pinia = createPinia(); // 创建实例
  // 使用
  const app = createApp(App);
  app.use(pinia); // pinia 安装配置
  app.mount("#app"); // 视图挂载
  // createApp(App).use(pinia).mount('#app')
  ```

---

### 仓库 defineStore

在 src / store 文件夹内可以创建任意个数的 js 文件，在 pinia 导入 defineStore

- 语法为：**defineStore( 仓库唯一标识, ( ) => { ... })，在箭头函数内写数据的声明，方法，计算属性，return 后并导出**

  src / store / counter.js

  ```javascript
  import { defineStore } from "pinia";
  import { ref, computed } from "vue";

  // 仓库返回的是函数
  export const useCounterStore = defineStore("counter", () => {
    // 声明数据 相当于以前的 state
    const count = ref(0);
    // 操作数据的方法 相当于以前的 action (同步 + 异步)
    const addCount = () => count.value++;
    const subCount = () => count.value--;

    // 声明基于数据的计算属性 相当于 getters - 使用 computed() 实现
    const double = computed(() => count.value * 2);
    const msg = ref("hello pinia");

    // 页面要使用需要 return
    return {
      count,
      double,
      addCount,
      subCount,

      msg,
    };
  });
  ```

  src / App.vue

  ```vue
  <script setup>
  import Son1Com from "@/components/Son1Com.vue";
  import Son2Com from "@/components/Son2Com.vue";
  import { useCounterStore } from "@/store/counter";
  const counterStore = useCounterStore();
  </script>

  <template>
    <div>
      <h3>
        <!-- 使用仓库的数据 -->
        App.vue根组件 - {{ counterStore.count }} - {{ counterStore.msg }}
      </h3>
      <Son1Com></Son1Com>
      <Son2Com></Son2Com>
    </div>
  </template>
  ```

  src / Son1Com.vue

  ```vue
  <script setup>
  import { useCounterStore } from "@/store/counter";
  const counterStore = useCounterStore();
  </script>

  <template>
    <div>
      <!-- 使用仓库的方法与计算属性 -->
      我是Son1组件 - {{ counterStore.count }} - 双倍:
      {{ counterStore.double }} -
      <button @click="counterStore.addCount">+</button>
    </div>
  </template>
  ```

---

### action 异步实现

pinia 的 action 支持同步与异步

- 示例

  src / store / channel.js

  ```javascript
  import { defineStore } from "pinia";
  import { ref } from "vue";
  import axios from "axios";

  export const useChannelStore = defineStore("channel", () => {
    const channelList = ref([]);
    const getList = async () => {
      // 支持异步
      const {
        data: { data },
      } = await axios.get("http://geek.itheima.net/v1_0/channels");
      channelList.value = data.channels;
      console.log(data.channels);
    };
    return {
      channelList,
      getList,
    };
  });
  ```

  src / App.vue

  ```vue
  <script setup>
  import { useChannelStore } from "@/store/channel";
  const channelStore = useChannelStore();
  </script>

  <template>
    <div>
      <button @click="channelStore.getList">获取频道数据</button>
      <ul>
        <li v-for="item in channelStore.channelList" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
    </div>
  </template>
  ```

---

### 解构 storeToRefs

上面的例子，如果在父组件对仓库方法解构，会丧失响应式功能。

**需要解构数据时，请导包 + 并使用 storeToRefs( ) 方法**

- 示例：

  ```vue
  <script setup>
  import { storeToRefs } from "pinia";
  import { useCounterStore } from "@/store/counter";

  const counterStore = useCounterStore();
  // const { count, msg } = storeToRefs(counterStore) 解构数据会破坏响应性，解构方法不会
  const { count, msg } = storeToRefs(counterStore);
  </script>

  <template>
    <div>
      <h3>- {{ count }} - {{ msg }}</h3>
    </div>
  </template>
  ```

---

### pinia 持久化插件

- 要求：安装了 pinia 2.0.0 以上

- **下载与导入**：npm i pinia-plugin-persistedstate 下载好后在 main.js 中导入

  ```javascript
  import { createApp } from "vue";
  import { createPinia } from "pinia";
  import { persist } from "pinia-plugin-persistedstate"; // 导入持久化插件
  import App from "./App.vue";

  const pinia = createPinia();
  const app = createApp(App);
  app.use(pinia.use(persist)); // 让 pinia 使用插件
  app.mount("#app");
  ```

- **用法：**创建 Store 时，**为 defineStore 的第三个参数设置 {persist: true}**

  ```javascript
  export const use,,, = defineStore('counter', () => {
    ...
    return {
      ...
    }
  }, {
    persist: true // 开启当前模块的持久化
  })
  ```

- **效果：**刷新数据不丢失了，会优先使用 localStorage 存储，并优先从存储数据中读取

- **额外配置项：**

  比如不想让键名为默认名（比如上面的例子键名为 counter，太常见），可以修改 persist: true 为

  ```javascript
  persist: {
    key: "新键名";
  }
  ```

  比如只想让某些数据持久化，可以：

  ```javascript
  persist: {
    paths: ["数据名"];
  }
  ```

---

# Object.defineProperty( ) 与 proxy

## API 介绍

1. **Object.defineProperty( )** 用来**拦截对象的属性**

   接收三个参数 (obj, prop, descriptor)

   obj 为要操作的对象，prop 为要定义或修改的键，descriptor 为配置特性，如下：

   ```js
   {
     // 值为不设置时的默认值
     value: undefined; // 被定义的属性值
     writable: false; // 是否可重写
     enumerable: false; // 是否可被枚举（使用 for...in 或 Object.keys(),或者直接打印obj）
     configurable: false; // 是否可以重新配置此配置项 且 是否可以删除此对象
   }
   ```

   例子：

   ```js
   const obj = {
     name: "mario",
   };
   Object.defineProperty(obj, "age", {
     value: 22,
     enumerable: true,
   });
   console.log(obj); // { name: 'mario', age: 22 }
   obj.age = 88; // 拦截掉这个操作，因为 writable 默认 false
   console.log(obj); // { name: 'mario', age: 22 }
   delete obj.age; // 删不掉，默认 configurable 为 false
   console.log(obj); // { name: 'mario', age: 22 } 删不掉
   delete obj; // 直接删整个对象也不行，只要会导致属性改变都无效
   console.log(obj); // { name: 'mario', age: 22 } 删不掉
   ```

   **getter 与 setter：**

   descriptor 还可以传入以下配置项，一旦配置这两个属性，上面的 writable 与 value 就不允许使用了。

   ```js
   {
   	get: () => {
           // 获取对象属性值的时候触发此函数
           return newValue // 返回值会作为新属性值
       },
       set: (value) => {
           // 设置对象属性值的时候触发此函数
           // 设置的新值通过 value 拿到
       }
   }
   ```

   例子：

   ```js
   const obj = {
     name: "mario",
   };
   let initValue = 18;
   Object.defineProperty(obj, "age", {
     get: function () {
       return initValue;
     },
     set: function (value) {
       console.log("你想设置的值为：", value);
       initValue = value;
     },
   });
   console.log(obj.age); // 18
   obj.age = 22; // 你想设置的值为： 22
   console.log(obj.age); // 22
   ```

   **不能在 get 中获取对象属性值，也不能在 set 中为对象属性重新赋值，会造成无限递归 - 栈溢出**

2. **proxy**

   Proxy 创建一个对象的代理，以**实现对象基本操作的拦截。**

   new Proxy( obj, handler ) 接收两个参数

   obj 为目标对象，handler 也是对象，里面包含 getter 与 setter 函数，用于拦截操作。

   ```js
   const obj = {
     name: "mario",
   };
   const proxy = new Proxy(obj, {
     // get 拦截对属性的读取操作, 接收原对象，键，[proxy实例本身]
     get: (obj, key) => {
       console.log("尝试获取属性触发");
       if (key in obj) return obj[key];
       else throw new Error("错误");
     },
     // set 拦截对属性的赋值操作，接收原对象，键，值，[proxy实例本身]
     set: (obj, key, value) => {
       console.log("尝试设置属性触发", "传入值为:", value);
       if (key === "age") {
         if (!Number.isInteger(value)) throw new Error("不合法");
         if (value > 120) throw new Error("太大了");
       }
       obj[key] = value;
     },
   });
   // 通过代理对象操作
   console.log(proxy.name); // 尝试获取属性触发 mario
   // console.log(proxy.age)  // 错误
   proxy.age = 22; // 尝试设置属性触发 传入值为: 22
   console.log(proxy.age); // 尝试获取属性触发 22
   ```

   还有一些其他操作比如 has 方法，拦截 in 操作符...，deleteProperty 方法，拦截删除操作，了解即可。

---

## vue 的响应式基本原理

首先注意响应式与数据双向绑定不是一个东西。

1. **vue2 的响应式数据的原理：**数据变化页面就变化，这就是响应式。

   ![](./\图片\vue响应式.png)

   **对 data 内的每一个属性分别定义了 Object.defineproperty() 内的 getter 和 setter。**

   利用 Object.defineproperty() 内的 getter 和 setter **对数据的操作（读、改）进行拦截，并根据 vue 中的 watcher 进行视图更新。**

   但是 defineProperty() 无法监视数组，为了实现数组的响应式，vue 的做法是**函数劫持**，把会导致数组变化的常用函数全部劫持，触发这些函数就重新渲染视图。

2. **vue3 的响应式数据的原理：**以 Proxy 替代 Object.defineProperty

   **原因：**

   defineProperty 拦截的是单一属性，如果对象内属性一多，就要定义多个 defineProperty，影响性能。

   而且 defineProperty 拦截数组也有问题，API 有局限性。Proxy 能拦截，而且懒处理，如果用户没有访问嵌套对象，就不会实施拦截，让初始化速度与内存都改善了。

   Proxy 这么牛逼就没缺点吗，有的，不支持 IE。

---

# 性能优化知识

## 异步组件

异步组件主要用来提升性能的。**实现按需引入**

现在用户界面只能看到 A、B 组件，C 组件在 B 组件下面，希望用户没往下滑动窗口时不加载 C。

- 结构

  ```vue
  <template>
    <A></A>
    <B></B>
    <C></C>
  </template>

  <script setup>
  import { defineAsyncCompoent } from "vue";
  import A from "../components/A.vue";
  import B from "../components/B.vue";
  // 使用异步组件引入
  const C = defineAsyncCompoent(() => import("../components/C.vue"));
  </script>
  ```

上面只是引入了异步组件，并没有实现不加载 C 的功能，还需要**引入新模块 useIntersectionObserver**

- 实现功能

  ```vue
  <template>
    <A></A>
    <B></B>
    <div ref="target">
      <C v-if="targetVisable"></C>
    </div>
  </template>

  <script setup>
  import { ref, defineAsyncCompoent } from "vue";
  import { useIntersectionObserver } from "@/vueuse/core";
  import A from "../components/A.vue";
  import B from "../components/B.vue";
  // 使用异步组件引入
  const C = defineAsyncCompoent(() => import("../components/C.vue"));
  // 定义两个响应式 - 控制加载
  const target = ref(null); // DOM
  const targetVisable = ref(false); // 控制组件加载
  // 使用 useIntersectionObserver
  const { stop } = useIntersectionObserver(
    target,
    // 这个 isIntersecting 当滑动到要加载这个 DOM 时变为 true
    ([{ isIntersecting }]) => {
      if (isIntersecting) targetVisable.value = isIntersecting;
    }
  );
  </script>
  ```

  这样当进入这个页面，C 组件根本就没加载，快滑动到了才会加载这个组件，实现了按需引入。

---

# 项目事项

## Vue + TS

### 项目准备与常用配置

- 创建项目

  安装 pnpm：npm install -g pnpm

  创建项目：pnpm create vue （然后根据需要进行选择）

  ```
   Project name: ... vue3-ts
  √ Add TypeScript? ... No / [Yes]
  √ Add JSX Support? ... [No] / Yes
  √ Add Vue Router for Single Page Application development? ... No / [Yes]
  √ Add Pinia for state management? ... No / [Yes]
  √ Add Vitest for Unit Testing? ... [No] / Yes
  √ Add an End-to-End Testing Solution? » No
  √ Add ESLint for code quality? ... No / [Yes]
  √ Add Prettier for code formatting? ... No / [Yes]
  ```

  安装依赖：pnpm install

  启动项目：pnpm dev

---

# 综合案例

## 备忘录

- 效果：

  ![](./\图片\备忘录.png)

- 步骤：

1. 列表渲染
2. 删除功能
3. 添加功能
4. 底部统计与清空

- 代码：

  ```html
  <!-- 主体区域 -->
  <section id="app">
    <!-- 输入框 -->
    <header class="header">
      <h1>备忘录</h1>
      <input
        @keyup.enter="add"
        v-model="todoName"
        placeholder="请输入任务"
        class="new-todo"
      />
      <button @click="add" class="add">添加任务</button>
    </header>
    <!-- 列表区域 -->
    <section class="main">
      <ul class="todo-list">
        <li class="todo" v-for="(item, index) in list" :key="item.id">
          <div class="view">
            <span class="index">{{ index + 1 }}</span>
            <label>{{item.name}}</label>
            <button @click="del(item.id)" class="destroy"></button>
          </div>
        </li>
      </ul>
    </section>
    <!-- 统计和清空 如果没有任务下面的合计和清空任务不显示-->
    <footer class="footer" v-show="list.length > 0">
      <!-- 统计 -->
      <span class="todo-count">合 计:<strong> {{ list.length }} </strong></span>
      <!-- 清空 -->
      <button @click="clear" class="clear-completed">清空任务</button>
    </footer>
  </section>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        // todoName 用来接收输入框内容
        todoName: "",
        list: [
          { id: 1, name: "吃饭" },
          { id: 2, name: "睡觉" },
          { id: 3, name: "上厕所" },
        ],
      },
      methods: {
        del(id) {
          this.list = this.list.filter((item) => item.id !== id);
        },
        add() {
          // 输入为空要提示
          if (this.todoName.trim() === "") {
            alert("请输入任务名称");
            return;
          }
          // 在数组前插入元素
          this.list.unshift({
            // 前端可以用时间戳获得唯一 id
            id: +new Date(),
            name: this.todoName,
          });
          // 清空 todoName
          this.todoName = "";
        },
        clear() {
          this.list = [];
        },
      },
    });
  </script>
  ```

---

## 成绩案例

- 效果：

  ![](./\图片\成绩案例.png)

- 步骤：

1. 渲染功能 使用 v-if v-else v-for（不及格高亮 使用 v-bind:class）
2. 删除功能 点击传参，filter 过滤覆盖数组，.prevent 阻止默认行为
3. 添加功能 v-model 使用 .trim 和 .number 修饰符，unshift() 修改更新视图
4. 统计总分 使用 computed 计算属性 + reduce 求和

- 代码：

  ```html
  <div id="app" class="score-case">
    <div class="table">
      <table>
        <thead>
          <tr>
            <th>编号</th>
            <th>科目</th>
            <th>成绩</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody v-if="list.length > 0">
          <tr v-for="(item, index) in list" :key="item.id">
            <td>{{index + 1}}</td>
            <td>{{item.subject}}</td>
            <td :class="{red: item.score < 60}">{{item.score}}</td>
            <td><a @click.prevent="del(item.id)" href="#">删除</a></td>
          </tr>
        </tbody>
        <tbody v-else>
          <tr>
            <td colspan="5">
              <span class="none">暂无数据</span>
            </td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="5">
              <span>总分：{{totalScore}}</span>
              <span style="margin-left: 50px">平均分：{{averageScore}}</span>
            </td>
          </tr>
        </tfoot>
      </table>
    </div>
    <div class="form">
      <div class="form-item">
        <div class="label">科目：</div>
        <div class="input">
          <input type="text" placeholder="请输入科目" v-model.trim="subject" />
        </div>
      </div>
      <div class="form-item">
        <div class="label">分数：</div>
        <div class="input">
          <input type="text" placeholder="请输入分数" v-model.number="score" />
        </div>
      </div>
      <div class="form-item">
        <div class="label"></div>
        <div class="input">
          <button @click="add" class="submit">添加</button>
        </div>
      </div>
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        list: [
          { id: 1, subject: "语文", score: 20 },
          { id: 7, subject: "数学", score: 99 },
          { id: 12, subject: "英语", score: 70 },
        ],
        subject: "",
        score: "",
      },
      computed: {
        totalScore() {
          return this.list.reduce((sum, item) => sum + item.score, 0);
        },
        averageScore() {
          if (this.list.length === 0) {
            return 0;
          }
          return (this.totalScore / this.list.length).toFixed(2);
        },
      },
      methods: {
        del(id) {
          this.list = this.list.filter((item) => item.id !== id);
        },
        add() {
          if (!this.subject) {
            alert("请输入科目");
            return;
          }
          if (typeof this.score !== "number") {
            alert("请输入正确的成绩");
            return;
          }
          this.list.unshift({
            id: +new Date(),
            subject: this.subject,
            score: this.score,
          });
          this.subject = "";
          this.score = "";
        },
      },
    });
  </script>
  ```

---

## 水果购物车

- 效果：

  ![](./\图片\水果购物车.png)

- 步骤：

1. 渲染功能 v-if / v-else v-for :class
2. 删除功能 @click 传参 → filter 覆盖原数组
3. 修改个数 @click 传参 → find 找到对象，修改数值
4. 全选反选 computed 完整写法 get / set
5. 统计选中总价和总数量 computed + reduce 求和
6. 持久化到本地 watch 监视只要有变化 → localStorage JSON .stringify 与 .parse

- 代码：

  ```html
  <div class="app-container" id="app">
    <!-- 顶部banner -->
    <div class="banner-box">
      <img src="http://autumnfish.cn/static/fruit.jpg" alt="" />
    </div>
    <!-- 面包屑 -->
    <div class="breadcrumb">
      <span>🏠</span>
      /
      <span>购物车</span>
    </div>
    <!-- 购物车主体 -->
    <div class="main" v-if="fruitList.length > 0">
      <div class="table">
        <!-- 头部 -->
        <div class="thead">
          <div class="tr">
            <div class="th">选中</div>
            <div class="th th-pic">图片</div>
            <div class="th">单价</div>
            <div class="th num-th">个数</div>
            <div class="th">小计</div>
            <div class="th">操作</div>
          </div>
        </div>
        <!-- 身体 -->
        <div class="tbody">
          <!-- 选中就添加阴影效果 -->
          <div
            class="tr"
            :class="{active: item.isChecked}"
            v-for="(item, index) in fruitList"
            :key="item.id"
          >
            <div class="td">
              <input type="checkbox" v-model="item.isChecked" />
            </div>
            <div class="td"><img :src="item.icon" alt="" /></div>
            <div class="td">{{item.price}}</div>
            <div class="td">
              <div class="my-input-number">
                <!-- 数量小于 1，禁用按钮 -->
                <button
                  :disabled="item.num <= 1"
                  class="decrease"
                  @click="sub(item.id)"
                >
                  -
                </button>
                <span class="my-input__inner">{{item.num}}</span>
                <button class="increase" @click="add(item.id)">+</button>
              </div>
            </div>
            <div class="td">{{item.num * item.price}}</div>
            <div class="td"><button @click="del(item.id)">删除</button></div>
          </div>
        </div>
      </div>
      <!-- 底部 -->
      <div class="bottom">
        <!-- 全选 -->
        <label class="check-all">
          <input type="checkbox" v-model="isAll" />
          全选
        </label>
        <div class="right-box">
          <!-- 所有商品总价 -->
          <span class="price-box"
            >总价&nbsp;&nbsp;:&nbsp;&nbsp;¥&nbsp;<span class="price"
              >{{ totalPrice }}</span
            ></span
          >
          <!-- 结算按钮 -->
          <button class="pay">结算( {{ totalCount }} )</button>
        </div>
      </div>
    </div>
    <!-- 空车 -->
    <div v-else class="empty">🛒空空如也</div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script>
    // 默认数据
    const defaultArr = [
      {
        id: 1,
        icon: "http://autumnfish.cn/static/火龙果.png",
        isChecked: true,
        num: 2,
        price: 6,
      },
      {
        id: 2,
        icon: "http://autumnfish.cn/static/荔枝.png",
        isChecked: false,
        num: 7,
        price: 20,
      },
      {
        id: 3,
        icon: "http://autumnfish.cn/static/榴莲.png",
        isChecked: false,
        num: 3,
        price: 40,
      },
      {
        id: 4,
        icon: "http://autumnfish.cn/static/鸭梨.png",
        isChecked: true,
        num: 10,
        price: 3,
      },
      {
        id: 5,
        icon: "http://autumnfish.cn/static/樱桃.png",
        isChecked: false,
        num: 20,
        price: 34,
      },
    ];
    const app = new Vue({
      el: "#app",
      data: {
        // 水果列表 - 从本地数据读取
        fruitList: JSON.parse(localStorage.getItem("list")) || defaultArr,
      },
      computed: {
        // 勾选全选要修改单选框的值，所以要用 computed 的完整写法
        isAll: {
          // 通常用计算属性来实现 全选与单选联动效果 使用 every方法
          get() {
            return this.fruitList.every((item) => item.isChecked);
          },
          set(value) {
            // 基于拿到的布尔值，要让所有的小单选框同步
            this.fruitList.forEach((item) => (item.isChecked = value));
          },
        },
        // 统计选中的总数
        totalCount() {
          return this.fruitList.reduce((sum, item) => {
            if (item.isChecked) {
              return sum + item.num;
            } else {
              // 不勾选 不需要累加（要写这个 else 否则无效）
              return sum;
            }
          }, 0);
        },
        totalPrice() {
          return this.fruitList.reduce((sum, item) => {
            if (item.isChecked) {
              return sum + item.num * item.price;
            } else {
              return sum;
            }
          }, 0);
        },
      },
      methods: {
        del(id) {
          this.fruitList = this.fruitList.filter((item) => item.id !== id);
        },
        add(id) {
          // 根据 id 找到数组对应项
          const fruit = this.fruitList.find((item) => item.id === id);
          // 操作 num 数量
          fruit.num++;
        },
        sub(id) {
          const fruit = this.fruitList.find((item) => item.id === id);
          fruit.num--;
        },
      },
      watch: {
        fruitList: {
          // 监视 fruitList 变化存储到本地
          deep: true,
          handler(newValue) {
            // 转 JSON
            localStorage.setItem("list", JSON.stringify(newValue));
          },
        },
      },
    });
  </script>
  ```

---

## 记账清单

- 效果：

  ![](./\图片\记账清单.png)

- 步骤：

1. 渲染页面 进页面就发送请求获取数据（使用 created），拿到数据存到 data 响应式数据中，结合数据使用 v-for 进行渲染，消费统计部分使用 computed 计算属性
2. 添加功能 使用 v-model 收集表单数据，给添加按钮 @click 发送添加请求，重新渲染数据
3. 删除功能 给删除按钮 @click 传参，拿到 id 根据 id 发送删除请求，重新渲染数据
4. 饼图渲染 使用插件 [echarts](https://echarts.apache.org/zh/index.html) 初始化饼图（官网有写，**在准备好 DOM 容器后才能一步步操作，所以要写在 mounted( ) 里**） 根据数据实时更新

- 代码：

  ```html
  <div id="app">
    <div class="contain">
      <!-- 左侧列表 -->
      <div class="list-box">
        <!-- 添加资产 -->
        <form class="my-form">
          <input
            v-model.trim="name"
            type="text"
            class="form-control"
            placeholder="消费名称"
          />
          <input
            v-model.number="price"
            type="text"
            class="form-control"
            placeholder="消费价格"
          />
          <button @click="add" type="button" class="btn btn-primary">
            添加账单
          </button>
        </form>
        <table class="table table-hover">
          <thead>
            <tr>
              <th>编号</th>
              <th>消费名称</th>
              <th>消费价格</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in list" :key="item.id">
              <td>{{index+1}}</td>
              <td>{{item.name}}</td>
              <!-- 超过 500 块高亮 -->
              <td :class="{red: item.price > 500}">
                {{item.price.toFixed(2)}}
              </td>
              <td><a @click="del(item.id)" href="javascript:;">删除</a></td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <td colspan="4">消费总计：{{totalPrice.toFixed(2)}}</td>
            </tr>
          </tfoot>
        </table>
      </div>
      <!-- 右侧图表 -->
      <div class="echarts-box" id="main"></div>
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/echarts@5.4.0/dist/echarts.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        list: [],
        name: "",
        price: "",
      },
      computed: {
        totalPrice() {
          return this.list.reduce((sum, item) => sum + item.price, 0);
        },
      },
      created() {
        // 使用 this 访问方法
        this.getList();
      },
      mounted() {
        // 由官网复制修改
        // 用 this 挂载到实例上，以使得 methods 里的渲染方法能访问到 setOption()
        this.myChart = echarts.init(document.querySelector("#main"));
        this.myChart.setOption({
          title: {
            text: "消费账单列表",
            left: "center",
          },
          // 提示框
          tooltip: {
            trigger: "item",
          },
          // 图例
          legend: {
            orient: "vertical",
            left: "left",
          },
          series: [
            {
              name: "消费账单",
              type: "pie",
              radius: "50%",
              data: [],
              emphasis: {
                itemStyle: {
                  shadowBlur: 10,
                  shadowOffsetX: 0,
                  shadowColor: "rgba(0, 0, 0, 0.5)",
                },
              },
            },
          ],
        });
      },
      methods: {
        async getList() {
          const res = await axios({
            url: "https://applet-base-api-t.itheima.net/bill",
            params: {
              creator: "铁牛",
            },
          });
          this.list = res.data.data;
          // 更新图表
          this.myChart.setOption({
            // 官方文档说，要修改谁，就把修改的那部分按格式写进 setOption
            series: [
              {
                data: this.list.map((item) => ({
                  value: item.price,
                  name: item.name,
                })),
              },
            ],
          });
        },
        async add() {
          if (!this.name) {
            alert("请输入消费名称");
            return;
          }
          if (typeof this.price !== "number") {
            alert("请输入正确消费价格");
            return;
          }
          const res = await axios({
            url: "https://applet-base-api-t.itheima.net/bill",
            method: "post",
            data: {
              creator: "铁牛",
              name: this.name,
              price: this.price,
            },
          });
          this.getList();
          this.name = "";
          this.price = "";
        },
        async del(id) {
          const res = await axios({
            url: `https://applet-base-api-t.itheima.net/bill/${id}`,
            method: "delete",
          });
          this.getList();
        },
      },
    });
  </script>
  ```

---

## 商品列表

- 效果：

  ![](C:\Users\清\Documents\学习\markdown\图片\商品列表.png)

  （主要练习组件封装）

1. **my-tag 标签组件封装：**

   双击显示输入框，输入框获取焦点。（使用 v-if v-else 根据 isEdit 的值显示，@dblclick 自动聚焦使用 $refs + $nextTick() 或封装 v-focus 指令）

   失去焦点，隐藏输入框。（使用 @blur 修改 isEdit 的值）

   输入框出现时，里面回显标签信息。（首先回显的信息是由父组件传过来的，使用 v-model => :value + @input 实现，组件内通过 props 接收，:value 设置给输入框）

   内容修改，按回车键 → 修改标签信息。（@keyup.enter，$emit('input', e.target.value）

2. **my-table 表格组件封装：**

   数据不写死，动态传递表格数据渲染。

   （props 传递数据）

   结构不写死，表头支持用户自定义。主体支持用户自定义。

   （多处结构自定义，使用具名插槽 slot name 并在子组件 slot 处 把参数传递给父组件）

- 代码：

  MyTag.vue

  ```vue
  <template>
    <div class="my-tag">
      <!-- 使用 v-if 和 else 互斥显示 -->
      <!-- 使用 v-focus 获取焦点 -->
      <input
        v-if="isEdit"
        v-focus
        ref="inp"
        class="input"
        type="text"
        placeholder="输入标签"
        :value="value"
        @blur="isEdit = false"
        @keyup.enter="handleEnter"
      />
      <!-- @dblclick 双击换行 -->
      <div v-else @dblclick="handleClick" class="text">
        {{ value }}
      </div>
    </div>
  </template>

  <script>
  export default {
    // 使用 props 接收父组件的数据
    props: {
      value: String,
    },
    data() {
      return {
        isEdit: false,
      };
    },
    methods: {
      handleClick() {
        // 双击显示输入框
        this.isEdit = true;
        // 切换状态后，DOM 还没更新，不可以直接获取焦点
        // this.$nextTick(() => {
        //   // 等 DOM 加载完再获取焦点
        //   this.$refs.inp.focus()
        // })
        // 怕复用，把获取焦点的功能封装到 main.js 里
      },
      handleEnter(e) {
        if (e.target.value.trim() === "") return alert("标签内容不能为空");
        // 由于父组件是 v-model 所以要触发 input 事件把输入的值传递给父元素
        this.$emit("input", e.target.value);
        this.isEdit = false;
      },
    },
  };
  </script>

  <style lang="less" scoped>
  .my-tag {
    cursor: pointer;
    .input {
      appearance: none;
      outline: none;
      border: 1px solid #ccc;
      width: 100px;
      height: 40px;
      box-sizing: border-box;
      padding: 10px;
      color: #666;
      &::placeholder {
        color: #666;
      }
    }
  }
  </style>
  ```

  MyTable.vue

  ```vue
  <template>
    <table class="my-table">
      <thead>
        <tr>
          <slot name="head"></slot>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in data" :key="item.id">
          <!-- 把 item 和 index 给插槽 -->
          <slot name="body" :item="item" :index="index"></slot>
        </tr>
      </tbody>
    </table>
  </template>

  <script>
  export default {
    props: {
      data: {
        type: Array,
        required: true,
      },
    },
  };
  </script>

  <style lang="less" scoped>
  .my-table {
    width: 100%;
    border-spacing: 0;
    img {
      width: 100px;
      height: 100px;
      object-fit: contain;
      vertical-align: middle;
    }
    th {
      background: #f5f5f5;
      border-bottom: 2px solid #069;
    }
    td {
      border-bottom: 1px dashed #ccc;
    }
    td,
    th {
      text-align: center;
      padding: 10px;
      transition: all 0.5s;
      &.red {
        color: red;
      }
    }
    .none {
      height: 100px;
      line-height: 100px;
      color: #999;
    }
  }
  </style>
  ```

  App.vue

  ```vue
  <template>
    <div class="table-case">
      <MyTable :data="goods">
        <template #head>
          <th>编号</th>
          <th>图片</th>
          <th>名称</th>
          <th width="100px">标签</th>
        </template>
        <!-- 这里其实是 obj 解构成 {item, index} -->
        <template #body="{ item, index }">
          <td>{{ index + 1 }}</td>
          <td><img :src="item.picture" /></td>
          <td>{{ item.name }}</td>
          <td>
            <!-- 使用 v-model 绑定数据 -->
            <MyTag v-model="item.tag"></MyTag>
          </td>
        </template>
      </MyTable>
    </div>
  </template>

  <script>
  import MyTag from "./components/MyTag.vue";
  import MyTable from "./components/MyTable.vue";
  export default {
    name: "TableCase",
    components: {
      MyTag,
      MyTable,
    },
    data() {
      return {
        // 测试组件功能的临时数据
        goods: [
          {
            id: 101,
            picture:
              "https://yanxuan-item.nosdn.127.net/f8c37ffa41ab1eb84bff499e1f6acfc7.jpg",
            name: "梨皮朱泥三绝清代小品壶经典款紫砂壶",
            tag: "茶具",
          },
          {
            id: 102,
            picture:
              "https://yanxuan-item.nosdn.127.net/221317c85274a188174352474b859d7b.jpg",
            name: "全防水HABU旋钮牛皮户外徒步鞋山宁泰抗菌",
            tag: "男鞋",
          },
          {
            id: 103,
            picture:
              "https://yanxuan-item.nosdn.127.net/cd4b840751ef4f7505c85004f0bebcb5.png",
            name: "毛茸茸小熊出没，儿童羊羔绒背心73-90cm",
            tag: "儿童服饰",
          },
          {
            id: 104,
            picture:
              "https://yanxuan-item.nosdn.127.net/56eb25a38d7a630e76a608a9360eec6b.jpg",
            name: "基础百搭，儿童套头针织毛衣1-9岁",
            tag: "儿童服饰",
          },
        ],
      };
    },
  };
  </script>

  <style lang="less" scoped>
  .table-case {
    width: 1000px;
    margin: 50px auto;
    img {
      width: 100px;
      height: 100px;
      object-fit: contain;
      vertical-align: middle;
    }
  }
  </style>
  ```

---

## 面经文章

- 效果：

  ![](./\图片\面经文章.png)

  先分配两个一级路由，和四个可切换页面（嵌套二级路由）

- 步骤：

1. 首页请求渲染（axios + created 发请求获取数据并保存 + 页面渲染）
2. 跳转传参到详情页，详情页渲染
3. 组件缓存，优化性能

- 代码：

  src / router / **index.js**

  **注意嵌套路由使用 children**

  ```javascript
  import Vue from "vue";
  import VueRouter from "vue-router";
  // 一级路由
  // Layout: 首页下面的标签
  import Layout from "@/views/Layout";
  // ArticleDetail: 首页上面的详情页
  import ArticleDetail from "@/views/ArticleDetail";
  // 二级路由
  import Article from "@/views/Article"; // 面经
  import Collect from "@/views/Collect"; // 收藏
  import Like from "@/views/Like"; // 喜欢
  import User from "@/views/User"; // 我的
  Vue.use(VueRouter);

  const router = new VueRouter({
    routes: [
      {
        path: "/",
        component: Layout,
        redirect: "/article",
        // 二级路由 - 通过 children 配置子路由
        // 还要在 Layout.vue 配置 router-view 路由出口才能显示
        children: [
          { path: "/article", component: Article },
          { path: "/collect", component: Collect },
          { path: "/like", component: Like },
          { path: "/user", component: User },
        ],
      },
      {
        // 动态路由传参
        path: "/detail/:id",
        component: ArticleDetail,
      },
    ],
  });

  export default router;
  ```

  src / main.js

  ```javascript
  import Vue from "vue";
  import App from "./App.vue";
  import router from "./router";

  Vue.config.productionTip = false;

  new Vue({
    render: (h) => h(App),
    router,
  }).$mount("#app");
  ```

  src / views / Layout.vue

  ```vue
  <template>
    <div class="h5-wrapper">
      <div class="content">
        <!-- 二级路由出口 -->
        <router-view></router-view>
      </div>
      <nav class="tabbar">
        <!-- 把 a 标签改为 router-link to 实现导航高亮 -->
        <router-link to="/article">面经</router-link>
        <router-link to="/collect">收藏</router-link>
        <router-link to="/like">喜欢</router-link>
        <router-link to="/user">我的</router-link>
      </nav>
    </div>
  </template>

  <script>
  export default {
    // 这个 name 是组件名
    name: "LayoutPage",
  };
  </script>

  <style>
  body {
    margin: 0;
    padding: 0;
  }
  </style>
  <style lang="less" scoped>
  .h5-wrapper {
    /* 略掉一些不重要的 */
    .tabbar {
      a.router-link-active {
        color: orange;
      }
    }
  }
  </style>
  ```

  src / views / ArticleDetail.vue

  ```vue
  <template>
    <!-- 添加判断使有数据再渲染，否则会有浏览量和点赞数和一大片空白 -->
    <div class="article-detail-page" v-if="article.id">
      <!-- $router.back() 返回上一页 -->
      <nav class="nav">
        <span @click="$router.back()" class="back">&lt;</span> 面经详情
      </nav>
      <header class="header">
        <h1>{{ article.stem }}</h1>
        <p>
          {{ article.createAt }} | {{ article.views }} 浏览量 |
          {{ article.likeCount }} 点赞数
        </p>
        <p>
          <img :src="article.creatorAvatar" alt="" />
          <span>{{ article.creatorName }}</span>
        </p>
      </header>
      <main class="body">
        {{ article.content }}
      </main>
    </div>
  </template>

  <script>
  import axios from "axios";
  export default {
    name: "ArticleDetailPage",
    data() {
      return {
        article: {},
      };
    },
    async created() {
      // 获取传参
      const id = this.$route.params.id;
      const { data } = await axios.get(
        `https://mock.boxuegu.com/mock/3083/articles/${id}`
      );
      this.article = data.result;
      console.log(this.article);
    },
  };
  </script>

  <style lang="less" scoped>
  /* 略 */
  </style>
  ```

  src / views / App.vue

  ```vue
  <template>
    <div class="h5-wrapper">
      <!-- 会以对应页面的 js 区的 name（组件名）为优先，没找到组件名就用文件名 -->
      <keep-alive :include="keepArr">
        <router-view></router-view>
      </keep-alive>
    </div>
  </template>

  <script>
  export default {
    name: "h5-wrapper",
    data() {
      return {
        // 缓存组件名
        keepArr: ["LayoutPage"],
      };
    },
  };
  </script>

  <style>
  /* 略 */
  </style>
  ```

---

## 购物车案例

- 效果：

  ![](./\图片\购物车案例.png)

- 步骤：

1. 购物车分为三个模块，购物车的数据存入 cart 模块等
2. 使用 json-server 准备好数据，启动接口服务
3. 获取数据并渲染：安装 axios → 准备 actions 和 mutations → 调用 action 获取数据 → mapState 映射
4. 数据处理：点加号减号时，更新前端 vuex 数据（按钮点击事件 → 页面 dispatch[调用模块内方法] → action 函数[axios 请求更新后端数据] → mutation 函数）
5. 底部 getters 统计：在 getters 内配置功能，并用 mapGetters 调用功能

- 代码：

  src / store / index.js

  ```javascript
  import Vue from "vue";
  import Vuex from "vuex";
  import cart from "./modules/cart";

  Vue.use(Vuex);

  export default new Vuex.Store({
    modules: {
      cart,
    },
  });
  ```

  src / App.vue

  ```vue
  <template>
    <div class="app-container">
      <!-- Header 区域 -->
      <cart-header></cart-header>

      <!-- 商品 Item 项组件 :item 是父子参数传递 -->
      <cart-item v-for="item in list" :key="item.id" :item="item"></cart-item>

      <!-- Foote 区域 -->
      <cart-footer></cart-footer>
    </div>
  </template>

  <script>
  import CartHeader from "@/components/cart-header.vue";
  import CartFooter from "@/components/cart-footer.vue";
  import CartItem from "@/components/cart-item.vue";
  import { mapState } from "vuex";

  export default {
    name: "App",
    created() {
      // 用 dispatch 调用 cart 模块的获取数据功能
      this.$store.dispatch("cart/getList");
    },
    computed: {
      ...mapState("cart", ["list"]),
    },
    components: {
      CartHeader,
      CartFooter,
      CartItem,
    },
  };
  </script>
  ```

  src / store / modules / cart.js

  ```javascript
  import axios from "axios";

  export default {
    namespaced: true,
    // state 可以用这种函数的形式 return
    state() {
      return {
        // 购物车数据 - 数组包对象
        list: [],
      };
    },
    mutations: {
      // 操作 state 的数据必须经过 mutation
      // 更新获取整个列表
      updateList(state, newList) {
        state.list = newList;
      },
      // 更新物品数量
      updateCount(state, obj) {
        // 根据 id 找到对应的对象，更新 count 属性
        const goods = state.list.find((item) => item.id === obj.id);
        goods.count = obj.newCount;
      },
    },
    actions: {
      // 异步 - 发送请求
      async getList(context) {
        const res = await axios.get("http://localhost:3000/cart");
        // 把数据用 mutations 存入 list
        context.commit("updateList", res.data);
      },
      async updateCountAsync(context, obj) {
        // 将修改更新同步到服务器
        await axios.patch(`http://localhost:3000/cart/${obj.id}`, {
          count: obj.newCount,
        });
        // 将修改更新同步到 vuex - 通过 mutation
        context.commit("updateCount", {
          id: obj.id,
          newCount: obj.newCount,
        });
      },
    },
    getters: {
      // 商品总数
      total(state) {
        return state.list.reduce((sum, item) => sum + item.count, 0);
      },
      // 商品总价
      totalPrice(state) {
        return state.list.reduce(
          (sum, item) => sum + item.count * item.price,
          0
        );
      },
    },
  };
  ```

  src / components / cart-item.vue

  ```vue
  <template>
    <div class="goods-container">
      <!-- 左侧图片区域 -->
      <div class="left">
        <img :src="item.thumb" class="avatar" alt="" />
      </div>
      <!-- 右侧商品区域 -->
      <div class="right">
        <!-- 标题 -->
        <div class="title">{{ item.name }}</div>
        <div class="info">
          <!-- 单价 -->
          <span class="price">￥{{ item.price }}</span>
          <div class="btns">
            <!-- 按钮区域 -->
            <button class="btn btn-light" @click="btnClick(-1)">-</button>
            <span class="count">{{ item.count }}</span>
            <button class="btn btn-light" @click="btnClick(1)">+</button>
          </div>
        </div>
      </div>
    </div>
  </template>

  <script>
  export default {
    name: "CartItem",
    methods: {
      btnClick(step) {
        const newCount = this.item.count + step;
        const id = this.item.id;
        if (newCount < 1) return; // 负数处理
        this.$store.dispatch("cart/updateCountAsync", {
          id,
          newCount,
        });
      },
    },
    // props 接收数据
    props: {
      item: {
        type: Object,
        required: true, // 必填
      },
    },
  };
  </script>
  ```

  src / components / cart-footer.vue

  ```vue
  <template>
    <div class="footer-container">
      <!-- 中间的合计 -->
      <div>
        <span>共 {{ total }} 件商品，合计：</span>
        <span class="price">{{ totalPrice }}</span>
      </div>
      <!-- 右侧结算按钮 -->
      <button class="btn btn-success btn-settle">结算</button>
    </div>
  </template>

  <script>
  import { mapGetters } from "vuex";
  export default {
    name: "CartFooter",
    computed: {
      ...mapGetters("cart", ["total", "totalPrice"]),
    },
  };
  </script>
  ```

---
