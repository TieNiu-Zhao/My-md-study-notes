# Vue 学习

Vue 是一个**构建用户界面**（基于数据动态渲染页面）的**渐进式框架**

Vue 的两种使用方式：

1. 基于 Vue 核心包开发：**局部**，模块改造
2. 基于 Vue 核心包 + Vue 插件 工程化开发（Webpack / Vite）：**整站**，开发、

官网：[Vue2](https://v2.cn.vuejs.org/)、[Vue3](https://cn.vuejs.org/)

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
           el: '#app',
           // 通过 data 提供数据
           data: {
               msg: 'Hello, Vue',
               count: 6
           }
       })
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
           el: '#app',
           data: {
               nickname: 'tony' 
           }
       })
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
           el: '#app',
           data: {
               msg: '<a href="#">测试能否解析标签</a>'
           }
       })
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
           el: '#app',
           data: {
               flag: true
           }
       })
   </script>
   ```

3. **v-else** 与 **v-else-if**

   常用在多条件判断，**配合 v-if 使用，用于分支判断**

   **注意：** v-else 后不用跟表达式，v-else-if 后要跟表达式，表达式为真，则渲染。

   ```html
   <div id="app">
       <p v-if="gender === 1">性别：♂ 男</p>
       <p v-else>性别：♀ 女</p>
       <hr>
       <p v-if="score >= 90">成绩评定A：奖励一个亿</p>
       <p v-else-if="score >= 70">成绩评定B：奖励旅游</p>
       <p v-else-if="score >= 60">成绩评定C：奖励吃顿好的</p>
       <p v-else>成绩评定D：奖励自己</p>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               gender: 2,
               score: 95
           }
       })
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
           el: '#app',
           data: {
               count: 100
           }
       })
   </script>
   ```
   
- 第二种是： **v-on:事件名 + "methods中的函数名"**

   第一种方法虽然方便，只适用于简单的场景。

   **v-on 事件后可以接函数名**，函数在 Vue 的 **methods 属性**中，且**在函数中 this 指向 Vue 实例**。

   ```html
   <div id="app">
       <button @click="fn">切换显示隐藏</button>
       <h1 v-show="isShow">冲冲冲</h1>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
           	isShow: true
   		},
           methods: {
               fn () {
                   // 函数直接访问 isShow 会报错，因为不在全局变量而在实例内
                   // 可以通过 app.isShow 访问
                   // app.isShow = !app.isShow
                   this.isShow = !this.isShow      // this 指向当前实例（vue 做的）
               }
           }
       })
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
           el: '#app',
           data: {
               money: 1000
           },
           methods: {
               buy (price) {
                   this.money -= price
               }
           }
       })
   </script>
   ```

5. **v-bind** 与 **<a id="bind">:</a>**

   也就是常用的冒号“ : ”，冒号的作用是省略 v-bind，方便改变属性，后面会说改变 class、style 等

   可以动态设置 HTML 的标签属性：src、url、title...，语法为：v-bind:**属性名**="**表达式**"

   为了开发方便，**可以省略 v-bind**，直接使用 **:属性名="表达式"**

   ```html
   <div id="app">
       <!-- 相当于 <img v-bind:src="imgUrl" v-bind:title="msg" alt=""> -->
       <img :src="imgUrl" :title="msg" alt="">
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               imgUrl: './imgs/10-02.png',
               msg: '肌肉猛男'
           }
       })
   </script>
   ```

   【案例 - 切换图片】

   ```html
   <div id="app">
       <!-- index 减到 0，隐藏按钮 -->
       <button v-show="index > 0" @click="index--">上一页</button>
       <div>
           <!-- 通过修改 index 值切换图片 -->
       	<img :src="list[index]" alt="">
       </div>
       <!-- index 加到最大值，隐藏按钮 -->
       <button v-show="index < list.length - 1" @click="index++">下一页</button>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               // index 为数组下标，默认为 0
               index: 0,
               list: [
                   './imgs/11-00.gif',
                   './imgs/11-01.gif',
                   './imgs/11-02.gif',
                   './imgs/11-03.gif',
                   './imgs/11-04.png',
                   './imgs/11-05.png',
               ]
           }
       })
   </script>
   ```

6. **v-for**

   类似于 forEach，基于**数据循环**（常见比如数组），可以多次渲染整个元素

   索引和内容可以按需使用，只有一个时可以省略括号，比如这样：\<li v-for="item in list">

   **v-for 一定要使用 key，作为唯一标识。**（如果不添加 key，列表发生改变时，比如删除第一个元素，Vue 不知道你删的是第一个元素，但它看见少了一个元素，他会渲染除了最后一个的列表，而不是删除。）

   key 的值只能是字符串或数字类型，key 的值必须具有唯一性，**推荐使用 id 作为 key（唯一）**，不推荐使用 index 作为 key

   **遍历数组：**

   ```html
   <div id="app">
       <h3>水果摊</h3>
       <ul>
           <!-- 如果只需要 item 或 index，可以省略，括号也是 -->
           <li v-for="(item, index) in list">第{{ index + 1 }}个水果: {{ item }}</li>
       </ul>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               list: ['西瓜', '苹果', '鸭梨', '草莓']
           }
       })
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
           el: '#app',
           data: {
               booksList: [
                   { id: 1, name: '红楼梦', author: '曹雪芹'},
                   { id: 2, name: '西游记', author: '吴承恩'},
                   { id: 3, name: '水浒传', author: '施耐庵'},
                   { id: 4, name: '三国演义', author: '罗贯中'}
               ]
           },
           methods: {
               del(id) {
                   // 返回新数组重新赋值
                   this.booksList = this.booksList.filter(item => item.id !== id)
               }
           }
       })
   </script>
   ```

7. **v-model**<a id="model">.</a>

   可以**给表单元素使用**，做到**双向数据绑定**，可以**快速获取和设置表单元素的值**

   注意表单元素不止有输入框，还有单选、多选框、文本域、下拉菜单等

   ```html
   <div id="app">
       <!-- 一旦加了 v-model 就双向绑定了，视图和内容同时变 -->
       账户：<input type="text" v-model="username"> <br><br>
       密码：<input type="password" v-model="password"> <br><br>
       <button @click="login">登录</button>
       <button @click="reset">重置</button>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               username: '',
               password: ''
           },
           methods: {
               login () {
                   console.log(this.username, this.password)
               },
               reset () {
                   this.username = ''
                   this.password = ''
               }
           }
       })
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
       <input @keyup.enter="fn" v-model="username" type="text">
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               username: ''
           },
           methods: {
               fn() {	// 相当于做了 if (e.key === 'Enter')
                   console.log('键盘回车触发', this.username)
               }
           }
       })
   </script>
   ```

2. v-model 的 **.trim** 和 **.number**

   ```html
   <!-- .trim 去除首尾空格 -->
   姓名：<input v-model.trim="username" type="text"><br>
   <!-- .number 转化数字型（如果是数字字符串） -->
   年纪：<input v-model.number="age" type="text"><br>
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
           el: '#app',
           methods: {
               fatherFn () {
                   alert('老父亲被点击了')
               },
               sonFn () {	// 相当于使用了 e.stopPropagation()
                   alert('儿子被点击了')
               }
           }
       })
   </script>
   ```


---

### : 操作 class / style

- 使用 **[v-bind](#bind)** 动态添加 / 删除类名，有两种写法，语法为:

1. **:class="{类名1: 布尔值, 类名2: 布尔值}"**，布尔值为 true，添加类名，为 false，删除类名，**适用于一个类名来回切换**

   ```html
   <div class="box" :class="{ 类名1: 布尔值, 类名2: 布尔值 ] }"></div>
   ```

   【**导航栏切换示例**】

   ```html
   <div id="app">
       <ul>
           <!-- 导航 点击标签下标赋值 -->
           <li v-for="(item, index) in list" :key="item.id" @click="activeIndex = index">
               <!-- :class="{类名: 布尔值}" -->
               <a :class="{ active: index === activeIndex }" href="#">{{ item.name }}</a>
           </li>
       </ul>
   </div>
   <script>
       const app = new Vue({
           el: '#app',
           data: {
               // 记录高亮的下标
               activeIndex: 0,
               list: [
                   { id: 1, name: '京东秒杀' },
                   { id: 2, name: '每日特价' },
                   { id: 3, name: '品类秒杀' }
               ]
           }
       })
   </script>
   ```

2. **:class="{ [‘类名1’, '类名2'] }"**，数组中所有的类都会添加到盒子上，本质是一个 class 列表，**适用于批量添加或移除类**

   ```html
   <div class="box" :class="{ [ 类名1, 类名2, 类名3 ] }"></div>
   ```

- 使用 v-bind 操作样式 style

  对于控制**单个属性变换**非常方便，语法为：

  ```html
  <div class="box" :style="{ CSS属性名1: CSS属性值, CSS属性名2: CSS属性值 }"></div>
  ```

  注意里面的 CSS属性尊从的是 JS 的语法，所以有 - 的属性名用小驼峰，属性值用 ' ' 引起来，例如：

  ```html
  <div class="box" :style="{width: '400px', height: '400px', backgroundColor: 'skyblue'}"></div>
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
          el: '#app',
          data: {
          	percent: 0
          }
      })
  </script>
  ```

---

### v-model 表单元素

- 使用 **[v-model](#model)** 快速获取 / 改变 表单元素，双向绑定

  ```html
  <div id="app">
  	姓名：
          <input type="text" v-model="username"> 
          <br><br>
      是否单身：
          <input type="checkbox" v-model="isSingle"> 
          <br><br>
      性别: 
          <!-- name 使同一组互相排斥 value 用于提交给后台 -->
          <input v-model="gender" type="radio" name="gender" value="1">男
          <input v-model="gender" type="radio" name="gender" value="2">女
          <br><br>
      所在城市:
          <!-- select 的 value 值会关联 option 的 value 值，所以使用 v-model 改变 -->
          <select v-model="cityId">
              <!-- option 的 value 值提交给后台 -->
              <option value="101">北京</option>
              <option value="102">上海</option>
              <option value="103">成都</option>
              <option value="104">南京</option>
        	</select>
        	<br><br>
      自我描述：
  		<textarea v-model="desc"></textarea> 
  	<button>立即注册</button>
  </div>
  <script>
      const app = new Vue({
          el: '#app',
          data: {
              username: '',
              isSingle: false,
              gender: '2',
              cityId: '102',
              desc: ''
          }
      })
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
              计算逻辑
              return 结果
          }
  	}
  })
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
          el: '#app',
          data: {
              // 现有的数据
              list: [
                  { id: 1, name: '篮球', num: 1 },
                  { id: 2, name: '玩具', num: 2 },
                  { id: 3, name: '铅笔', num: 5 },
              ]
          },
          computed: {
              totalCount() {
                  // 用 reduce 求和 忘了去看 JS 笔记 
                  let total = this.list.reduce((sum, item) => sum + item.num, 0)
                  return total
              }
          }
      })
  </script>
  ```

- 计算属性 computed 与 methods

  computed 封装了一段对数据的处理，**求得一个结果，作为属性使用**，computed 有缓存，计算出结果会立刻缓存，读取用的是缓存结果，除非数据改变。this.计算属性    {{ 计算属性 }}

  而 methods 提供一个方法，调用以处理业务，作为方法使用， this.方法名( )    {{ 方法名() }}    @事件名="方法名"
  
- **计算属性完整写法**

  默认的计算属性只能读取访问，不能修改，**需要修改时，应使用完整写法**

  ```javascript
  computed: {
      计算属性名: {
          get() {
              计算逻辑
              return 结果
          }，
          set() {
              修改逻辑
          }
      }
  }
  ```

  示例：

  ```html
  <div id="app">
      姓：<input type="text" v-model="firstName"><br>
      名：<input type="text" v-model="lastName"><br>
      <p>{{ fullName }}</p>
      <button @click="changeName">修改姓名</button>
  </div>
  <script>
      const app = new Vue({
          el: '#app',
          data: {
              firstName: '刘',
              lastName: '备'
          },
          methods: {
              changeName() {
                this.fullName = '吕布'
              }
          },
          computed: {
              fullName: {
                  get() {
                  	return this.firstName + this.lastName
                  },
                  // 当 fullName 被修改赋值就会执行 set()，修改的值作为形参
                  set(value) {
                      // 截取姓和名重新赋值
                      this.firstName = value.slice(0, 1)
                      this.lastName = value.slice(1)
  				}
              }
  		}
  	})
  </script>
  ```

---

### watch 监视器

- 作用：**监视数据变化**，执行一些业务逻辑或异步操作

- 写法：

  简单写法为：监视谁就在 watch 里写谁作为方法名

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
          el: '#app',
          data: {
              obj: {
              	words: ''
              },
              result: '',
              // timer: null
          },
          watch: {
              // 监视谁就写谁作为方法名，监视的在对象里，就对象.被监视对象，再用引号引上
              // words(newValue, oldValue) {} newValue 表示新值，oldValue 表示老值（一般不用）
              'obj.words' (newValue) {
                  // 防抖 - 延时器
                  // this.timer 只要用户一直在输入就一直不提交请求
                  clearTimeout(this.timer)
                  this.timer = setTimeout(async () => {
  					const res = await axios({
                          url: 'https://applet-base-api-t.itheima.net/api/translate',
                          params: {
                              // 接口默认翻译为意大利语
                          	words: newValue
                          }
            			})
                		this.result = res.data.data
  				}, 300)
  			}
          }
  	})
  </script>
  ```

  完整写法：添加额外配置项

  在上面的例子是翻译成意大利语，如果用户需要选择语言，即翻译结果受**多重条件**控制（语言和内容），**需要监视多个内容**

  **使用 deep: true 对复杂类型深度监视**

  与 immediate: true

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
          <input @keyup.enter="add" v-model="todoName" placeholder="请输入任务" class="new-todo" />
          <button @click="add" class="add">添加任务</button>
  	</header>
  	<!-- 列表区域 -->
  	<section class="main">
      	<ul class="todo-list">
  			<li class="todo" v-for="(item, index) in list" :key="item.id">
          		<div class="view">
                  	<span class="index">{{ index + 1 }}</span> <label>{{item.name}}</label>
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
      	<button @click="clear" class="clear-completed">
        		清空任务
      	</button>
    	</footer>
  </section>
  <script>
  	const app = new Vue({
          el: '#app',
          data: {
              // todoName 用来接收输入框内容
              todoName: '',
              list: [
                  {id: 1, name: '吃饭' },
                  {id: 2, name: '睡觉' },
                  {id: 3, name: '上厕所' }
              ]
          },
          methods: {
              del(id) {
              	this.list = this.list.filter(item => item.id !== id)
          	},
              add() {
                  // 输入为空要提示
                  if (this.todoName.trim() === '') {
                      alert('请输入任务名称')
                      return
                  }
                  // 在数组前插入元素
                  this.list.unshift({
                      // 前端可以用时间戳获得唯一 id
                      id: +new Date(),
                      name: this.todoName,
                  })
                  // 清空 todoName
                  this.todoName = ''
              },
              clear() {
                  this.list = []
              }
          }
      })
  </script>
  ```

---
