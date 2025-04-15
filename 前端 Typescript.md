# Typescript 学习

编程语言分为动态类型语言与静态类型语言

动态包括：Js，Ruby，Python（运行时做数据检查）

静态包括：C、C++，Java（编译阶段进行数据检查）

---

## 安装

1. 安装 typescript

   ```bash
   npm i -g typescript
   tsc -v					// 检查版本
   ```

2. 安装 ts-node：可以不用翻译 js 直接编译

   ```bash
   npm i -g ts-node
   ```

   运行 ts 代码使用 

   ```
   tsc test.ts				// 翻译成 js
   ts-node test.ts			// 直接运行
   ```

---

## 数据类型

原始类型：Boolean，Null，Undefined，Number，BigInt，String，Symbol （值不可改变）Object（值可变）

新类型：

1. any

   ```typescript
   let notSure: any = 4
   notSure = true      // 不报错
   ```

2. Array 数组

   ```typescript
   let arrNum: number[] = [1, 2, 3, 4]			// 只能一种类型
   ```

### 元祖

1. **元组：**可以将不同类型存入一个数组

   ```typescript
   let user: [string, number] = ['tieNiu', 12]
   user.push(11)								// 只能 push 定义好的类型中的种类
   ```

### interface 接口与函数

1. **interface：接口**

   interface 编译后不会被翻译成类型，所以只能做**静态检查**，可以用来描述对象的类型与函数的类型

   ```typescript
   interface Person {
       readonly id: number
       name: string
       age?: number		// ? 表示此参数可选可不选
   }
   // 必须和规定的相同，没有? 的话不能多不能少
   let tieNiu: Person = {
       id: 1,
       name: 'tieniu',
       age: 26
   }
   
   tieNiu.id = 22			// 只读属性只能读，会报错
   ```

2. **Function：函数**

   注意可选参数? 后，不能添加确定参数了。

   ```typescript
   function add(x: number, y: number, z?: number): number {
       // 约定输入与输出的类型
       if (typeof z === 'number') return x + y + z
       else return x + y
   }
   add(2, 3)
   ```

   function 作为一个类型，赋值时不能直接 function，而要把原函数的输入输出类型全定义好，注意箭头不是箭头函数，而是返回值类型

   ```typescript
   let add2: (x: number, y: number, z?: number) => number = add
   ```

   这样可能有点麻烦，可以用 interface

   ```typescript
   interface ISum {
       (x: number, y: number, z?: number): number
   }
   let add2: ISum = add
   ```

### union 联合类型

1. 类型推论：typescript 可以在没有给类型的情况下推断可能的类型

   ```typescript
   let str = 'str'
   str = 123       // 报错
   ```

2. **union：联合类型**：加入想要一个变量类型要么是string要么是number，就是用联合类型

   ```typescript
   let numberOrString: number | string
   numberOrString = 123
   numberOrString = 'tieniu'
   // 只能访问联合类型中属性点共有方法
   numberOrString.toString()
   ```

   **类型断言：**假如使用以上联合类型，又想使用非公共属性，比如 length，使用类型断言告诉编译器，把它看成什么类型使用此类型下的方法。

   ```typescript
   function getLength(input: string | number): number {
       // 类型断言只能断言联合类型中的一种
       const str = input as string
       if (str.length) {
           return str.length
       } else {
           const number = input as number
           return number.toString().length
       }
   }
   ```

   或者：使用 type guard

   ```typescript
   function getLength2(input: string | number): number {
       // typeof 会智能缩小范围
       if (typeof input === 'string') {
           return input.length
       } else {
           return input.toString().length
       }
   }
   ```

### enum 枚举

- **enum**：枚举

   ```typescript
   enum Direction {
       Up,
       Down,
       Left,
       Right
   }
   console.log(Direction.Up)       // 0
   console.log(Direction[1])       // Down - 可以把他直接看成数组
   ```

   如果给第一项赋值，后面每一项自动递增 + 1

   ```typescript
   enum Direction {
       Up = 10,
       Down,
       Left,
       Right
   }
   console.log(Direction.Down)       // 11
   ```

   用法，用来字符串比较

   ```typescript
   enum Direction {
       Up = 'UP',
       Down = 'DOWN',
       Left = 'LEFT',
       Right = 'RIGHT'
   }
   const value = 'UP'
   if (value === Direction.Up) console.log('go up!')       // go up
   ```

   可以在枚举 enum 前加上 const，这样编译后的 js 代码会非常简洁，不会把枚举当一个类型编译，提升效率。

### <> 泛型与 extends 约束泛型

- **泛型**

   指定义接口，函数或类时，不预先定义类型、不知道是什么类型时使用。

   **【深入理解1】**

   这是个类型 F，实际上是个 number 数组
   
   ```ts
   type F = number[]
   ```
   
   可以把 F 看成是函数名（实际是类型名），number[] 看成这个函数的返回值。
   
   他被看成函数的话，函数是有变量作为传参的，而函数传参一般用 () 包裹，这里都是类型，**用 <> 包裹传参**。
   
   ```ts
   type F<T> = T[]
   ```
   
   用 T 表示函数（类型）的参数，返回值跟 T 有关，这就是**泛型**。
   
   使用的时候只要传入对应参数（传入对应类型）就可以了
   
   ```ts
   type F<T> = T[]
   let arr: F<number>				// 实际上是 number[]
   let newArr: F<string>			// 实际上是 string[]
   ```
   
   **【深入理解2】**
   
   ```ts
   type common = {
   	code: string
   	data: ?
   	msg: string
     time: string
   }
   ```
   
   现在有一个类型，里面的 data 字段不知道什么类型，需要根据接口返回数据的类型来确定。所以用变量 T 表示，同时使用 “形参列表” \<T>
   
   ```ts
   type common<T> = {
   	code: string
   	data: T
   	msg: string
     time: string
   }
   ```
   
   现在某个接口类型有了
   
   ```ts
   type User = {
   	name: string
     age: number
   }
   ```

   就可以传入类型得到完整的结构了
   
   ```ts
   common<User>
   ```
   
   相当于直接定义了这样的结构：
   
   ```ts
   type common = {
   	code: string
   	data: {
   		name: string
     	age: number
   	}
   	msg: string
     time: string
   }
   ```
   
   既然泛型作为一个类型函数，也可以像函数一样给一个默认值。
   
   ```ts
   type common<T = string> = {
   	code: string
   	data: T
   	msg: string
     time: string
   }
   ```
   
   这个意思就是当我使用 `common` 这个类型但是没有使用 `<>` 时，使用默认类型代替。
   
   **【深入理解3 - extends】**
   
   extends 表示继承，
   
   ```ts
   type F<T> = 类型1 extends 类型2
   ```
   
   表示判断，判断类型1是否继承自类型2，会得到结果 true / false，所以经常结合三元运算符。
   
   ```ts
   type F<T> = 类型1 extends 类型2 ? RT1 : RT2
   ```
   
   即先判断是否类型1继承自类型2，如果成立使用类型 RT1，否则使用 RT2 类型。
   
   实际一点的例子：
   
   ```ts
   type F<T> = T extends 'a'|'b'|'c' ? 'X': 'Y'
   
   let a: F<'b'>					      // 实际上 a 的类型为 'X'
   let b: F<'a'|'b'|'d'>				// 实际上 b 的类型为 'X' | 'Y'
   ```
   
   对于上面的b的类型判断，是因为先用 'a' 判断是否继承自 'a' | 'b' | 'c'，得到 'X'
   
   再判断 'b' 是否继承自 'a' | 'b' | 'c'，得到 'X'，再判断 'd' 是否继承自 'a' | 'b' | 'c'，得到 'Y'，最后 ‘X' | 'X' | 'Y' 得到 'X' | 'Y'
   
   即：当传入泛型的类型为“联合类型时”，会把联合类型的每一项做运算最后联合，即运算后返回的也是联合类型，成为**分发**。
   
   那么如果我用的联合类型传入但不想让他分别运算，希望作为整体运算，使用元祖 [] 括起来（extends 前后都要，否则非法）
   
   ```ts
   type F<T> = [T] extends ['a'|'b'|'c'] ? 'X': 'Y'
   ```
   
   extends 也可以写在泛型里，作为类型的约束：
   
   ```ts
   type F<T extends 'a' | 'b' | 'c'> = T
   let a: F<'a'>								// a 的类型是 'a'
   let b: F<'d'>								// error
   ```

### type 类型别名

- **type** 类型别名：即使用 type 给类型起个别名

   ```typescript
   type PlusType = (x: number, y: number) => number
   let sum: PlusType
   const result2 = sum(2, 3)
   ```

   字符串字面量：这是一个特殊类型，只能是原始类型，可以把值定死。

   ```typescript
   // 对值进行一个约束
   const str: 'name' = 'name'
   const number: 1 = 1
   type Direction = 'Up' | 'Dowm' | 'Left' | 'Right'
   let toWhere: Direction = 'Left'
   ```

   交叉类型：使用 & 把几种类型合并起来

   ```typescript
   interface IName {
       name: string
   }
   type IPerson = IName & { age: number }
   let person: IPerson = { name: 'tieniu', age: 22 }
   ```

   **interface 与 type 的区别： type 作为类型别名非常宽泛，类似“快捷方式”，interface 是 type 的实现方式**

---

## 声明文件 d.ts

针对 js 模块想在 ts 中使用的情形。

声明文件的目的就是给业务代码提供类型逻辑，所以此文件内**只有类型声明，没有逻辑代码**

- declare 例子

  declare 的作用就是告诉 ts，这有个变量，别管它怎么来的。

  ```typescript
  // 举例：真实的 axios 不返回 string
  // declare function axios(url: string): string
  
  interface IAxios {
      get: (url: string) => string
      post: (url: string, data: any) => string
  }
  declare const axios: IAxios
  ```

  然后在项目里打开此文件的同时输入 axios，就能自动补全，还有类型提示了。

  typescript 官网提供所有库的安装命令，安装时可选只安装类型声明文件

- 例子2：实现一个 calculator 方法，

  ```typescript
  calculator('plus', [1, 2])			// 3
  calculator('minus', [3, 2])			// 2
  // 另一种方式
  calculator.plus([2, 1])
  calculator.minus([2, 1])
  ```

  实现方法，calculator.d.ts

  ```typescript
  type IOperator = 'plus' | 'minus'
  // type ICalculator = (operator: IOperator, numbers: number[]) => number\
  // 因为要在函数上童泰添加属性，需要使用接口
  interface ICalculator {
      (operator: IOperator, numbers: number[]): number
      plus: (numbers: number[]) => number
      minus: (numbers: number[]) => number
  }
  declare const calcultor: ICalculator
  
  export default calcultor
  ```

  为了让这个模块看起来像正经模块，要放到 node_nidules 下的 @types 文件夹下，因为 node_nidules 模块下会自动加载

  在文件内导入模块后使用

  ```typescript
  import calcultor from "calculator"
  calcultor('minus', [1, 2])
  calcultor.plus([1, 2])
  ```

  当然，因为没实现方法，所以直接编译为 js 会报错

---

## 高阶

- 直接从一份 ts 文件来理解：

  ```ts
  import { KeyMapEnum } from '@lobehub/ui/es/Hotkey';
  
  export const KeyEnum = {
    ...KeyMapEnum,
    Number: '1-9',
  } as const;
  
  export const HotkeyEnum = {
    AddUserMessage: 'addUserMessage',
    EditMessage: 'editMessage',
    OpenChatSettings: 'openChatSettings',
    OpenHotkeyHelper: 'openHotkeyHelper',
    RegenerateMessage: 'regenerateMessage',
    SaveTopic: 'saveTopic',
    Search: 'search',
    SwitchAgent: 'switchAgent',
    ToggleLeftPanel: 'toggleLeftPanel',
    ToggleRightPanel: 'toggleRightPanel',
    ToggleZenMode: 'toggleZenMode',
  } as const;
  
  export const HotkeyGroupEnum = {
    Conversation: 'conversation',
    Essential: 'essential',
  } as const;
  
  export const HotkeyScopeEnum = {
    Chat: 'chat',
    // 默认全局注册的快捷键 scope
    // https://react-hotkeys-hook.vercel.app/docs/documentation/hotkeys-provider
    Global: 'global',
  } as const;
  
  export type HotkeyId = (typeof HotkeyEnum)[keyof typeof HotkeyEnum];
  export type HotkeyGroupId = (typeof HotkeyGroupEnum)[keyof typeof HotkeyGroupEnum];
  export type HotkeyScopeId = (typeof HotkeyScopeEnum)[keyof typeof HotkeyScopeEnum];
  
  export interface HotkeyItem {
    // 快捷键分组用于展示
    group: HotkeyGroupId;
    id: HotkeyId;
    isDesktop?: boolean;
    // 是否是桌面端专用的快捷键
    keys: string;
    // 是否为不可编辑的快捷键
    nonEditable?: boolean;
    // 快捷键作用域
    scopes?: HotkeyScopeId[];
  }
  
  export type HotkeyRegistration = HotkeyItem[];
  
  export type HotkeyI18nTranslations = Record<
    HotkeyId,
    {
      desc?: string;
      title: string;
    }
  >;
  ```

### 常量断言 as const

【冻结对象，使对象里的属性类型为他的固定值，不可变】

首先 as 是类型断言，就是断言一个东西的类型。这里的 **as const 是断言为常量。使其变为不可变类型。**

- 例子

  ```ts
  const obj = {
    name: "Alice",
    age: 25,
  }
  ```

  这个对象 ts 会认为他的类型是这样的：

  ```ts
  {
    name: string;  // 类型是 string，而不是 "Alice"
    age: number;   // 类型是 number，而不是 25
  }
  ```

  这里的 name 类型是 string，任意的 string 都行，age 同理。

  ```ts
  const obj = {
    name: "Alice",
    age: 25,
  } as const
  ```

  使用了 as const 后：

  ```ts
  {
    readonly name: "Alice";  // 类型是字面量 "Alice"，不是 string
    readonly age: 25;        // 类型是字面量 25，不是 number
  }
  ```

  这里的 **readonly 用来标记对象里的属性只读。**

  那么既然 as const 是为了让他的类型固定为字面量，我直接；

  ```ts
  type obj = {
    name: "Alice",
    age: 25,
  }
  ```

  这样也可以生成固定的类型为 obj，里面的 name 和 age 类型就是 'Alice' 和 25

  **但是！**这么定义只有纯类型，而上面的 as const 是定义了个对象，是值然后赋予了不可变的类型，场景不一样。

---

### Record<K , T>

【快速定义一个对象的键值结构】

要求：键的类型只能为 string、number

- 例子

  ```ts
  type UserType = "miffy" | "boris" | "mordred";
   
  interface CatInfo {
    age: number;
    breed: string;
  }
   
  const cats: Record<CatName, CatInfo> = {
    miffy: { age: 10, breed: "Persian" },
    boris: { age: 5, breed: "Maine Coon" },
    mordred: { age: 16, breed: "British Shorthair" },
  };
  ```

---

### Partial\<T>

【使 T 内的属性变为可选】

---

### Omit\<T>

【从 T 中排除部分属性】

---

### **类型验证 satisfies**

【这个对象必须符合某种类型，但你别改我原来的类型推断！】

- satisfies 

  左侧接值，右侧接类型，用来做**一个值的类型比如符合某种类型，但不会改他本来的类型推断**，不符合 ts 会报错

  ```ts
  const colors = {
    red: "#FF0000",
    green: "#00FF00",
  }
  ```

  这个意思就是有个常量 colors，ts 默认类型推断为

  ```ts
  {
    red: string;
    green: string
  }
  ```

  如果使用 as ，直接断言类型为 Record<string, string>

  ```ts
  const colors = {
    red: "#FF0000",
    green: "#00FF00",
  } as Record<string, string>
  ```

  这会导致使用 colors.blue 时不会报错。因为满足 Record<string, string>

  ```ts
  const colors = {
    red: "#FF0000",
    green: "#00FF00",
  } satisfies Record<string, string>;
  ```

  使用 satisfies，用来验证 colors 这个值是否满足类型为 Record<string, string>，但他的类型实则还是 `{red: string; green: string}`，所以使用 colors.blue 会报错。

---

### 键联合 keyof 与类型 typeof

- typeof 用来获取类型，keyof 用来获取对象的所有键的联合类型。

  ```ts
  export const Person {
    name: 'tie-niu',
    age: 28,
    sex: 'boy'
  } as const
  ```

  对于这个对象，`typeof Person` 的值就是他的对象类型，不再赘述。

  那么 `keyof typeof Person` 的意思就是从他的类型里得到所有键的联合，即

  ```ts
  'name' | 'age' | 'sex'
  ```

  所以有了这种用法

  ```ts
  export type PersonItem = (typeof Person)[keyof typeof Person]
  ```

  意思是从他的类型里 使用类型里的键（键联合）来拿到 类型里的值（值联合）。得到；

  ```ts
  'tie-niu' | 28 | 'boy'
  ```

  
