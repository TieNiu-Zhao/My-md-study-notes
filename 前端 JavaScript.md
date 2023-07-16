# JavaScript 学习

Js 运行在客户端（浏览器），Js 分为 ECMAscript 与 WebAPIs，WebAPIs 又分为 DOM 和 BOM。

## ECMAscript

ECMAscript 规定了 js 基础语法。

### 断点调试方法

浏览器按 F12 点击 Sources，双击要运行的 html 文件，点击有问题的代码行前的数字，**刷新浏览器**，点击右边第二个图标（英文是：Step over next function call）即可下一步。

---

### 基础的基础

1. Js 引入方式

   与 CSS 相同，分为内部，外部，行内三种引入方式，

   **内部：**通过 `script` 标签包裹 JavaScript 代码。写在 \</body> 的上面。（意味着html内容全部加载完毕）

   ```html
   <!-- alert('警告的内容') -->
   <body>
   	<script>
       	// 内部：通过 script 标签包裹 JavaScript 代码
           alert('三天之内撒了你')
   	</script>
   </body>
   ```

   **外部：**一般将 JavaScript 代码写在独立的以 .js 结尾的文件中，然后通过 \<script> 标签的 `src` 属性引入。

   ```html
   <!-- 假设在同级目录下的js文件夹内有my.js文件 -->
   <body>
   	<script>
       	// 外部：通过 script 的 src 属性引入独立的 .js 文件
           <script src="./js/my.js.js">
           // 使用外部引入法，后面的语句全部无效
           alert('本句不会执行'); 
   	</script>
   </body>
   ```

   **内联：**代码写在标签内部，vue 框架会用这种形式。略。

2. 注释：**单行注释：**//	快捷键：ctrl + /		**多行注释：**/* */	快捷键：shift + alt + A

3. 结束符：js 里的语句后 ; 可写可不写，但要统一，看团队要求。

4. 输入与输出

   输出：

   ```html
   <!-- alert('警告的内容') -->
   <!-- document.write('输出的内容') -->
   <!-- console.log('控制台输出') -->
   <script>
        document.write('输出的内容可以是文字和标签')
        document.write('<h1>我是标题</h1>')
        console.log('会显示在浏览器f12的console里')
   </script>
   ```

   输入：

   ```html
   <!-- prompt('弹出输入框') -->
   <script>
       prompt('请输入你的年龄')
   </script>
   ```

5. 变量：即存储数据的**容器**。先声明后使用。变量名允许字母、数字、$、下划线，数字不能开头。**严格区分大小写**。

   ```html
   <script>
       // let 变量名 = 数值
       // 变量初始化：声明并赋值
       let num = 1999
       let uname = 'Mario'
       // let + 变量名
       num = 2020
       // 使用
       console.log(num, uname)
   </script>
   ```

   var 与 let 功能类似，但 bug 太多，此处略，用 let 即可。

6. 数组：下标从0开始。

   ```html
   <script>
       // let 数组名 = [数据1， 数据2, ... , 数据n]
   	let arr = ['mario', 'luigi']
       // 使用
       console.log(arr[1])
   </script>
   ```

7. 常量：声明时必须初始化

   ```html
   <script>
       // const 常量名 = 常量值
   	let PI = 3,14
       // 使用
       console.log(PI)
   </script>
   ```

8. 数据类型：js 是弱数据类型语言，let 后只有赋值了才确定变量的数据类型。

   - **基本数据类型：**number 数字、string 字符串（用 ' '）、boolean 布尔、undefined 未定义、null 空

   值得一提的是，null == undefined （因为当 0 看）但 null !== undefined

   ```html
   <script>
       // 数字运算
   	let r = prompt('请输入圆的半径')
       let re = 3.14 * r * r
       document.write(re)
       
       // 字符串中有引号
       console.log('小明非常"美丽"')
       
       // 布尔型
       let isCool = true
       console.log(isCool)
       
       // 声明了变量未赋值，那么类型默认为 undefened
       
       // 空类型，常用于未创建的对象
       let obj = null
       console.log(obj)
       
       // 检测数据类型，typeof x
       console.log(typeof isCool)
   </script>
   ```

   1. **NaN** 代表 not a number，会在**计算错误**时出现，NaN是粘性的，任何对 NaN 的操作都返回 NaN。

   2. **模板字符串：必须用反引号``，搭配 ${ 变量名 }** 

   ```html
   <script>
       // 好用 -- 模板字符串
       let age = 20
       document.write(`小明今年${age}岁了`)
       
       // 不好用 -- 使用 + 可以让数字相加，也可以让字符相连
       let age = 20
       document.write('小明今年' + age + '岁了')
   </script>
   ```

   3. **类型转换 - 隐式：**js 中 prompt( ) 与 单/复/多选框取得的值默认是**字符串**类型。 

   ```html
   <script>
       // 问题代码
   	let num = prompt('请输入数字:')
       console.log(typeof num)		// string
       
   	// 隐式转换：+ 的两侧只要有字符串，另一个就会看成字符串，
       // 非 + 运算符如 -*/ 会把数据转成数字类型
       console.log('mario' + 1)	// mario1
       console.log(2 + '2')		// 22
       console.log(2 - '2')		// 0
       
       // + 可作为正好解析，将数据转换为数字型
       console.log(+’2‘ + 2)		// 4
   </script>
   ```

   4. **类型转换 - 显式：**转换为数字型使用：Number()、parseInt() 与 parseFloat()

   ```html
   <script>
       let numb = Number(prompt('请输入年薪:'))
       console.log(typeof numb)			// number
       console.log(parseInt('12.1px'))		// 12（只取了前面的整数）
       console.log(parseFloat('12.1px'))	// 12.1
       console.log(parseFloat('a12.1px'))	// NaN（没那么智能，数字在中间没办法）
   </script>
   ```

   **案例：**请按住Ctrl跳转：[综合案例 1 - 表格](#综合案例 1 - 表格)

   - 引用数据类型：复杂数据类型**存储的不是值是地址**（对象存入堆中，地址存入栈）。通过 new 关键字创建的对象，如 Object，Array，Date 等。

   ```html
   <script>
   	let num1 = 10
       let num2 = num1					// 值幅值
       num2 = 20
       console.log(num1)				// 10
       
       let obj1 = {
           age: 18
       }
       let obj2 = obj1					// 地址赋值
       obj2.age = 20
       console.log(obj.age)			// 20
   </script>
   ```

9. 运算符：**开发中判断是否相等，推荐使用 ===，不同类型用运算符比较，会发生隐式转换为 number。**

   ```html
   <script>
       // 幅值运算
       let num = 1
       num += 2				// num = num + 2
       
       // 自增运算
       let i = 1
       console.log(i++ + 1)	// 2
       
       // 比较运算 
       // ===：表示左右两边是否类型和值都相等
       console.log(2 == '2')		// true（比较运算符有隐式转换，把‘2’转换成2了）
       console.log(2 === '2')		// false
       console.log(NaN == NaN)		// false（NaN六亲不认，它不等于任何值，包括它自身）
       
       // 逻辑与&&，或||，非!
       let num = propmt('请输入一个数字，判断能否整除4且不整除100')
       alert(num % 4 === 0 && num % 100 !== 0)
   </script>
   ```

   优先级注意：! > || > &&

10. 分支语句：

    ```html
    <script>
        // if 语句
        // 除了0，所有的数字都为真，除了''（空字符串），所有的字符串都为真
    	if (-1) {
            console.log('执行语句')
        }
        
        // if-else 语句
        let uname = prompt('请输入用户名')
        let pwd = prompt('请输入密码')
        if (uname === 'mario' && pwd === '123456') {
            alert('登录成功')
        } else {
            alert('用户名或密码错误')
        }
        
        // if - else if - else 略
        
        // 三元运算符：条件 ? 满足执行 : 不满足执行，一般用来取值
        let num1 = +prompt('请输入第一个数')
        let num2 = +prompt('请输入第二个数')
        num1 > num2 ? alert(`最大值是${num1}`) : alert(`最大值是${num2}`)
        
        // switch 语句: 会选择 === 的那个分支然后依次执行直到 break，没有符合执行 default
        switch (1) {
            case 1:
                console.log('存款')
                break
            case 2:
                console.log('取款')
                break
            case 3:
                console.log('贷款')
                break
            default:
                console.log('不符合条件')
        }
    </script>
    ```

    【小案例 - 数字补0】输入数字，如果是10以下的数，自动在前面补0，如输入9，返回09

    ```javascript
    	let num = prompt('请输入一个数字')
        num < 10 ? 0 + num : num
    ```

11. 循环语句：**break** 直接退出循环，**continue** 结束本次循环，直接下轮<a id='for'>。</a>

    ```html
    <script>
    	// while 语句
        let i = 1
        while (i <= 100) {
            document.write(`这是第${i}个数<br>`)
            if (i % 3 === 0) {
                break
            }
            i++
        }
        
        // for 循环
        let arr = ['马超', '赵云', '张飞', '关羽', '黄忠']
        for (let j = 0; j < arr.length; j++) {
            console.log(arr[j])
        }
    </script>
    ```

    【小案例 - 99乘法表】

    ```html
    <style>
        span {
            display: inline-block;
            width: 100px;
            padding: 5px 10px;
            border: 1px solid #000;
            margin: 2px;
            border-radius: 5px;
            box-shadow: 2px 2px 2px pink;
            text-align: center;
        }
    </style>
    <script>
        for (let i = 1; i <= 9; i++) {
            for (let j = 1; j <= i; j++) {
                document.write(`<span>${j} × ${i} = ${j*i}</span>`)
            }
            document.write('<br>')
        }
    </script>
    ```

---

### 数组

- 数组：下标从0开始，长度通过数组的 **length** 属性获得。

  常用方法：push( )、unshift( )、pop( )、shift( )、splice( )

  ​				   map( )、join( ) [跳转](#map 与 join 方法)
  
  ​			 	  forEach( )、filter( ) [跳转](#forEach 与 filter 方法)
  
  ​			 	  其他方法 [跳转](#arr)
  
  ```html
  <script>
  	// 声明方法1
      let arr1 = [1, 2, 'mario', true]
      // 声明方法2
      let arr2 = new Array(1, 2, 3, 4)
      
      let sum
      sum = sum + arr[0]
      console.log(sum)		// 结果为 NaN，sum 不会默认为 0，而是 undefined
      
      // 遍历
      for (let i = 0; i < arr2.length; i++) {
          sum += arr2[i]
      }
      console.log(`数组的平均值为:${sum / arr2.length}`)
      
      // 增
      // push() 在数组最后增加元素，返回数组的新长度
      // unshift() 在数组最前增加元素，返回数组的新长度
      let arr = ['b', 'c']
      console.log(arr.push('d'))		// 3
      console.log(arr.unshift('a'))	// 4
      
      // 删
      // pop() 删除数组最后一个元素，返回该元素值
      // shift() 删除数组第一个元素，返回该元素值
      console.log(arr.pop())			// d
      arr.shift()
      // splice(start, deleteCount) 删除指定元素，start;起始位置，deleteCount:移除元素个数，不写会删到底
      let array = ['1', '2', '3', '4']
      array.splice(1, 1)				// 会删除掉'2'
  </script>
  ```

**案例：**[综合案例 2 - 渲染柱形图](#综合案例 2 - 渲染柱形图)

---

### 函数

- 函数：先声明，后调用（虽然具名函数可以在声明前调用）

  ```javascript
  // 声明
  function getSum(x = 0, y = 0) {	// 形参
      return x + y
  }
  // 调用
  let sum = getSum(1, 50)			// 实参
  console.log(sum)
  getSum()						// 缺少实参执行默认参数
  
  function fn() {					// 函数没有返回值默认返回 undefined
      
  }
  let re = fn()
  console.log(re)					// undefined
  ```

- 作用域<a id='zyy'>：</a>全局变量与局部变量，一个变量使用时，**如果局部变量没找到就会去全局变量找**，采用**就近原则**查找变量最终值。

  ```html
  <script>
  	let num = 20
      function fn() {
          num = 10
      }
      console.log(fn())			// 10, 因为fn()里num前没加let，不是局部变量了
  </script>
  ```

- 匿名函数：必须先声明后调用。

  ```javascript
  let fn = function(x, y) {
      console.log(x + y)
  }
  fn(1, 2)
  ```

- **立即执行函数<a id='fh'>：</a>**写法技巧是写两个小括号()()，在第一个小括号内正常写函数，多个立即执行函数结尾**必须加分号；**可防止全局变量污染。

  ```html
  <script>
      // (function(){})()
  	(function(x, y){
          console.log(x + y)
      })(1, 2);
      // 还有一种写法 (function(){}())
  </script>
  ```

- 逻辑中断：等效于前面的给形参写上默认值。因为有传参，||右侧就不会执行了。

  ```html
  <script>
  	function fn(x, y) {
          x = x || 0					// || 左侧为真右侧就不执行
          y = y || 0
          console.log(x + y)
          
          let age = 18
          console.log(false && age++)	// age++ 不会执行
          console.log(age)			// 18
          console.log(11 && 22)		// 22（&&两侧都为真，返回最后的真值）
          console.log(11 || 22)		// 11（||两侧都为真，返回第一个真值）
      }
  </script>
  ```

- 转换为 Boolean 型：''、0、undefined、null、false、NaN 使用该方法均为 false，其余为 true

  ```html
  <script>
      let age
      if (age) {
          console.log(18)				// 18不会打印，因为 age 为 undefined	
      }
      console.log(Boolean(age))		// false
  </script>
  ```


---

### For

- for 的几种分散在笔记各处，功能各不相同：

  for 循环：普通遍历 [跳转](#for)

  for in：用于遍历对象 [跳转](#forin)

  forEach( )：是个方法，用于遍历数组对象，且没有返回值 [跳转](#forEach 与 filter 方法)

---

### 对象

1. 基本操作

   对象 Object 是一种数据类型，无序的数据集合。对象**由属性和方法组成。**属性名的 '' 可以省略

   **null 是一个空对象。**<a id='forin'>.</a>

   ```html
   <script>
       // 声明
       let obj = {
           'user-name': 'mario',		// 属性名和值用 :
           age: 56,					// 属性间用，
           gender: '男'
           big: function() {			// 方法，前面是名字，方法可以传参
               console.log('吃了蘑菇')
           }
       }
       
       // 增
       obj.power = '火花'
       
       // 删 (用的少)
       delete obj.gender
       
       // 改
       obj,age = 57
       
       // 查 : 对象.属性 或 对象['属性']
       console.log(obj.age)
       console.log(obj['user-name'])	// 查询的另一种方法（属性名有-只能这么查）
       
       // 调用对象方法
       obj.big()
       
       // 遍历对象 - 这种 for 里的 k 是字符串型，用于遍历对象。
       for (let k in obj) {			// k 为属性名
           console.log(obj[k])			// 对象[k] 为属性值
       }
   </script>
   ```

   跳转：[创建对象的三种方式](#构造函数)

2. 内置对象

   **Math：**

   Math 对象提供属性：Math.PI 表示圆周率

   Math 对象提供了一些方法：向上取整 ceil()、向下取整 floor()、四舍五入 round()、最大值 max()、最小值 min()、取绝对值 abs()、生成 [0, 1) 间随机小数 random()。使用 Math.方法名() 调用方法。

   - 注意 floor() 和前面的 parsrInt() 都能向下取整，区别在于前者参数只能是数字，后者可以传字符串。

   ```javascript
   Math.floor(Math.random() * (10 + 1))			// 生成 0~10 的随机数（取不到1，乘以10所以取不到10，再加1即可）
   Math.floor(Math.random() * (5 + 1)) + 5			// 生成 5~10 的随机数
   
   // 应用：随机选取数组元素
   let arr = ['red', 'green', 'blue']
   let random = Math.floor(Math.random() * arr.length)
   console.log(arr[random])
   
   // 生成 N~M 间的随机数
   function getRandom(N, M) {
       return Math.floor(Math.random() * (M - N + 1)) + N
   }
   ```

   【小案例 - 随机颜色】传参为 true 生成随机16进制颜色，传参为 false 生成随机rgb格式颜色

   ```javascript
   function getRandomColor(flag = true) {
       if (flag) {	// 返回 #ffffff 格式
           let arr = ['0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f']
           let str = '#'
           for (let i = 1; i <= 6; i++) {
               let random = Math.floor(Math.random() * arr.length)
               str += arr[random]
           }
           return str
       } else {				// 返回 rgb(255,255,255)
           let r = Math.floor(Math.random() * 256)
           let g = Math.floor(Math.random() * 256)
           let b = Math.floor(Math.random() * 256)
           return `rgb(${r},${g},${b})`
       }
   }
   console.log(getRandomColor(0))
   ```

---

### 用 const 声明

**优先用 const 变量**，如果后面发现要改再改为 let，数组和对象可以用 const 声明，**对于引用数据类型，const 存的是地址，不是值。**对数组追加，删除属性不会报错，但直接赋值，替换会报错。

```html
<script>
	const names = []		// 会报错
    names = [1, 2, 3]	
    
    const obj1 = {}			// 会报错
    obj1 = {
        uname: 'mario'
    }
    
    const obj2 = {			// 不会报错
        uname: 'mario',
        age: 56,
        gender: '男'
    }
    obj2.power = '火花'
</script>
```

**所以数组和对象优先用 const 声明。**

---

## DOM - 操作

WebAPIs 可以控制网页元素交互效果，即用 js 去操作 HTML 和浏览器。

DOM 即（Document Object Model）文档对象模型，用于操作网页内容。

**DOM 树：**将 HTML 文档结构用树状结构表现。

**DOM 对象：**浏览器根据 HTML 标签生成 js 对象，网页中所有内容都在 document 里面，document 是页面中最大的对象。 

---

### 获取 DOM 元素 doc.qs()

使用 CSS选择器 获取DOM元素。

1. 方法名：**document.querySelector**( )	[简写：doc.qs]

   参数为：一个或多个有效的 **CSS 选择器** 的 **字符串**（**选择器必须加引号' '表示字符串。**）

   返回值：CSS 选择器匹配的第一个元素，未匹配返回 null

   说明：获取来的元素可直接使用属性直接操作修改。

   ```html
   <body>
       <div class="box">123</div>
       <div class="box">abc</div>
       <p id="nav">导航栏</p>
       <ul>
           <li>测试1</li>
           <li>测试2</li>
           <li>测试3</li>
       </ul>
       <script>
           // 获取匹配的第一个元素
           const div = document.querySelector('div')
           console.log(div)				// 123
           const box = document.querySelector('.box')
           console.log(box)    			// 123
           const nav = document.querySelector('#nav')
           nav.style.color = 'red'
           const lis = document.querySelector('ul li:first-child')
           console.log(lis)				// 测试1
       </script>
   </body>
   ```

2. 方法名：**document.querySelectorAll**( )	[简写：qsa]

   参数为：一个或多个有效的 **CSS 选择器** 的 **字符串**

   返回值：CSS 选择器匹配的**伪数组**（NodeList 对象集合）

   说明：获取来的元素不能直接操作修改，需要遍历。

   ```html
   <body>
       <ul class=“nav”>
           <li>测试1</li>
           <li>测试2</li>
           <li>测试3</li>
       </ul>
       <script>
       	const lis = document.querySelectorAll('.nav li')
           // 遍历
           for(let i = 0; i < lis.length; i++) {
               console.log(lis[i])
           }
       </script>
   </body>
   ```

   几年前用 document.getElementById( ) 等方法获取元素，现在不常用了。

---

### 操作元素内容 innerHTML

DOM 对象是根据标签生成的，所以操作标签，本质上就是操作 DOM 对象。

1. 对象.**innerText** 属性

   说明：针对标签的文本内容，显示纯文本，**不解析标签**

   ```html
   <body>
       <div class="box">我是文字内容</div>
       <script>
           const box = document.querySelector('.box')
           console.log(box.innerText)         // 获取文字内容
           box.innerText = '我是一个盒子'       // 修改文字内容
       </script>
   </body>
   ```

2. 对象.**innerHTML** 属性

   说明：针对标签的文本内容，显示纯文本，**解析标签**

   ```html
   <body>
       <div class="box">我是文字内容</div>
       <script>
           const box = document.querySelector('.box')
           console.log(box.innerHTML)
           box.innerHTML = '<strong>变粗</strong>'
       </script>
   </body>
   ```

   【小案例 - 年会抽奖】

   ```html
   <body>
   	<div class="wrapper">
           <strong>年会抽奖</strong>
           <h1>一等奖：<span id="one">???</span></h1>
           <h3>二等奖：<span id="two">???</span></h3>
           <h5>三等奖：<span id="three">???</span></h5>
     	</div>
   	<script>
           const personArr = ['小李', '小赵', '小王', '小张', '小郑']
           const random1 = Math.floor(Math.random() * personArr.length)
           const one = document.querySelector('#one')
           one.innerHTML = personArr[random1]
           personArr.splice(random1, 1)
           const random2 = Math.floor(Math.random() * personArr.length)
           const two = document.querySelector('#two')
           two.innerHTML = personArr[random2]
           personArr.splice(random2, 1)
           const random3 = Math.floor(Math.random() * personArr.length)
           const three = document.querySelector('#three')
           three.innerHTML = personArr[random3]
   	</script>
   </body>
   ```

---

### 操作元素属性 classList

- **操作元素的属性**

  常见属性有：href、title、src 等

  ```html
  <body>
  	<img src="./images/1.jpg" alt="">
      <script>
      	const img = document.querySelector('img')
      	img.src = './images/2.jpg'
  	</script>
  </body>
  ```

  上面的例子替换了原本的 src 属性的值。

- **修改样式属性**

1. 通过 **style 属性** 操作 CSS

   ```html
   <body>
       <div class="box"></div>
       <script>
           const box = document.querySelector('.box')
           // 要加单位 px
           box.style.width = '300px'
           box.style.height = '300px'
           // 多组单词使用小驼峰
           box.style.backgroundColor = 'skyblue'
       </script>
   </body>
   ```

2. 通过**类名 (ClassName)** 操作 CSS

   如果样式修改过多，通过 style 属性修改比较繁琐。如果标签本身就有类名，新的类名会覆盖旧类名，如果要**新添加一个类，请保留以前的类名。**

   ```html
   <head>
       <style>
           .nav {
               width: 100px;
               height: 200px;
               background-color: pink;
           }
           .box {
               width: 300px;
               height: 300px;
               background-color: skyblue;
               margin: 100px auto;
               padding: 10px;
               border: 1px solid #000;
           }
       </style>
   </head>
   <body>
       <div class="nav"></div>
       <script>
           const div = document.querySelector('div')
           // 保留以前的类名
           div.className = 'nav box'
       </script>
   </body>
   ```

3. 通过 **classList** 操作 CSS （最常用）

   最优的方法。使用 对象.**classList**. 后接 **add**('类名')、**remove**('类名')、**toggle**('类名') ，**类名前没有.**

   classList 还有个 **contains**( ) 方法，可以看某标签**是否包含某个类**，有返回 true，没有返回 false
   
   ```html
   <style>
       .box {
           width: 100px;
           height: 200px;
           color: #333;
       }
       .active {
           color: red;
           background-color: pink;
       }
   </style>
   <script>
       const box = document.querySelector('.box')
       // classList.add() 追加类
       box.classList.add('active')
       // classList.remove() 删除类
       box.classList.remove('box')
       // classList.toggle() 切换类 有就会删掉，没有就会增加
       box.classList.toggle('active')
   </script>
   ```
   
   **案例：**[综合案例 3 - 轮播图：效果1](#综合案例 3 - 轮播图)

- **操作表单元素**

  比如实现点击眼睛显示密码，或者点击全选，所有的框都打勾。

1. text 文本框 与 password 密码框

   表单的元素不是通过 innerHTML 获取的。表单的内容需要通过 .value 取得。

   ```html
   <body>
       <input type="text" value="电脑">
       <script>
           // 获取元素
           const uname = document.querySelector('input')
           // 获取值
           console.log(uname.value)
           // 切换为密码
           uname.type = 'password'
       </script>
   </body>
   ```

2. checkbox 复选框勾选 与 button 按钮禁用

   勾选即为 true，未勾选即为 false。全选功能只需遍历每个 input 标签，改变 checked 值即可。

   ```html
   <body>
       <input type="checkbox" name="" id="">
       <button>点击</button>
       <script>
           // 获取复选框
           const ipt = document.querySelector('input')
           // 勾选
           ipt.checked = true
           
           // 获取按钮
           const button = document.querySelector('button')
           // 禁用
           button.disabled = true
       </script>
   </body>
   ```
   
   注意：虽然因为表单特殊，获取表单里的元素需要 value ，但 button 更特殊，它是双标签，所以**获取 button 按钮上的信息，需要使用 innerHTML**。

- **自定义属性**

  自定义属性需要遵循语法规则，以 data- 开头（H5规范），使用 **dataset**.起的名字 选中标签

  ```html
  <body>
      <!-- 自定义属性 -->
      <div data-id="1" data-what="什么">1</div>
      <div data-id="2">2</div>
      <div data-id="3">3</div>
      <div data-id="4">4</div>
      <div data-id="5">5</div>
      <script>
          const one = document.querySelector('div')
          console.log(one.dataset.id)     // 1
          console.log(one.dataset.what)   // 什么
      </script>
  </body>
  ```
  
  【小案例 - 全选表单】
  
  ```html
  <body>
      <table>
      	<tr>
      		<th class="allCheck">
      			<input type="checkbox" name="" id="checkAll"> <span class="all">全选</span>
      		</th>
          </tr>
          <tr>
          	<td>
          		<input type="checkbox" name="check" class="ck">
          	</td>
          </tr>
          <tr>
          	<td>
          		<input type="checkbox" name="check" class="ck">
              </td>
          </tr>
          <tr>
          	<td>
          		<input type="checkbox" name="check" class="ck">
          	</td>
          </tr>
      </table>
      <script>
          // 获取大复选框
          const checkAll = document.querySelector('#checkAll')
          // 获取所有的小复选框
          const cks = document.querySelectorAll('.ck')
          checkAll.addEventListener('click', function() {
              // 遍历所有小复选框，让其状态等于大复选框
              for (let i = 0; i < cks.length; i++) {
                  cks[i].checked = checkAll.checked
              }
          })
          
          // 小复选框控制大复选框
          // 给所有小复选框添加点击事件
          for (let i = 0; i < cks.length; i++) {
  			cks[i].addEventListener('click', function() {
                  // 判断选中的小复选框个数是否等于总数 伪类选择器:checked
                  // 当右侧等于总数，为 true，赋值给大复选框
                  checkAll.checked = document.querySelectorAll('.ck:checked').length === cks.length
  			})
  		}
      </script>
  </body>
  ```

---

### 定时器 setInterval

网页中经常需要每段时间自动执行一段代码，不需要手动触发，比如页面中得倒计时，需要用到定时器函数。

- 间歇函数：每隔一段时间 (ms)，调用间歇函数

  方法名：**setInterval**( 函数, 间隔时间 )
  
  返回值：数字（定时器的编号）
  
  ```html
  <script>
      setInterval(function(){
          console.log('一秒执行一次')
      }, 1000)
  </script>
  ```
  
  或者这么写，注意别加 ( )
  
  ```html
  <script>
      function fn() {
          console.log('一秒执行一次')
      }
      setInterval(fn, 1000)
  </script>
  ```
  
  拓展，其实函数后也可以加 ( )，但要用 ' ' 引上，用得不多。
  
  定时器会从打开网页后隔一个设定的间隔时间后一直执行，使用 clearInterval( ) 关闭定时器。
  
  ```html
  <script>
      function fn() {
          console.log('一秒执行一次')
      }
      let n = setInterval(fn, 1000)
      // 关闭定时器
      clearInterval(n)
      // 再次打开定时器
      n = setInterval(fn, 1000)
  </script>
  ```
  
  【小案例 - 阅读用户协议倒计时】按钮为灰色，倒计时后解锁。
  
  ```html
  <button class="btn" disabled>我已阅读用户协议(5)</button>
      <script>
          // 获取元素
          const btn = document.querySelector('.btn')
          // 倒计时
          let i = 5
          let n = setInterval(function(){
              i--
              btn.innerHTML = `我已阅读用户协议(${i})`
              if (i === 0) {
                  clearInterval(n)        // 关闭定时器
                  btn.disabled = false
                  btn.innerHTML = '同意'
              }
          }, 1000)
      </script>
  ```
  
  **案例：**[综合案例 3 - 轮播图：效果2](#综合案例 3 - 轮播图)

---

## DOM - 事件与事件流

### 事件监听 addEventListener

让程序检测是否有事件发生（用户单击了按钮，鼠标经过等），一旦有事件触发，立即调用一个函数作出响应，称为绑定事件或注册事件。

- 方法名：元素对象.**addEventListener**( '事件类型', 要执行的函数 )	[简写：add]

  **事件类型一定要加引号**，事件监听三要素：事件源，事件类型与事件调用的函数。

  ```html
  <body>
      <button>点击</button>
      <script>
          // 需求：点击按钮弹出对话框
          // 事件源 按钮
          const btn = document.querySelector('button')
          // 事件监听 - 事件类型 点击鼠标
          btn.addEventListener('click', function(){
               // 事件处理程序 弹出对话框
              alert('呀哈哈~')
          })
      </script>
  </body>
  ```

  补充：以上代码添加 **btn.click( )** 相当于直接触发点击事件的回调函数。

  【小案例 - 随机抽奖】
  
  ```html
  <body>
      <h2>随机抽奖</h2>
      <div class="box">
          <span>奖品为：</span>
          <div class="display">这里显示结果</div>
      </div>
      <div class="btns">
          <button class="start">开始</button>
          <button class="end">结束</button>
      </div>
      <script>
          // 数据数组
          const arr = ['100万', '20万', '50万', '1万', '1亿']
          // 显示名字
          const display = document.querySelector('.display')
          // 开始按钮
          const start = document.querySelector('.start')
          // 定时器全局变量
          let timerId = 0
          // 随机数全局变量
          let random = 0
          // 事件监听：点击开始按钮抽奖
          start.addEventListener('click', function(){
              // 定时器
              timerId = setInterval(function(){
                  // 随机轮播
                  random = parseInt(Math.random() * arr.length)
                  display.innerHTML = arr[random]
              }, 35)
              // 如果只剩一个奖品，不用再抽了，禁用两个按钮
              if (arr.length === 1) {
                  start.disabled = end.disabled = true
              }
          })
          // 结束按钮
          const end = document.querySelector('.end')
          end.addEventListener('click', function(){
              clearInterval(timerId)
              // 删除当前抽取的元素
              arr.splice(random, 1)
          })
      </script>
  </body>
  ```
  
  以前事件监听是用 事件源.on事件 = function( ){ } 这种写法，有事件覆盖问题，了解即可。

---

### 事件类型

1. 鼠标触发：click 鼠标点击、mouseenter 鼠标经过、mouseleave 鼠标离开

   （以前用 mouseover，mouseout，但会有冒泡效果，不推荐，冒泡概念在事件解绑）

   ```html
   <head>
       <style>
           div {
               width: 200px;
               height: 200px;
               background-color: pink;
           }
       </style>
   </head>
   <body>
       <div></div>
       <script>
           const div = document.querySelector('div')
           div.addEventListener('mouseenter', function() {
               console.log('进来')
           })
           div.addEventListener('mouseleave', function() {
               console.log('出去')
           })
       </script>
   </body>
   ```

   **案例：**[综合案例 3 - 轮播图：效果3](#综合案例 3 - 轮播图)

2. 表单获得光标：focus 获得焦点、blur 失去焦点

   可用于做搜索框效果

   ```html
   <head>
       <style>
           /* 其他 css 略 */
           /* 边框变颜色 */
           .mi .search {
               border: 1px solid #ff6700;
           }
       </style>
   </head>
   <body>
       <!-- 小米搜索框 -->
       <div class="mi">
           <input type="search" placeholder="小米笔记本">
           <ul class="result-list">
               <li><a href="#">全部商品</a></li>
               <li><a href="#">小米11</a></li>
               <li><a href="#">小米10S</a></li>
               <li><a href="#">小米笔记本</a></li>
               <li><a href="#">小米手机</a></li>
               <li><a href="#">黑鲨4</a></li>
               <li><a href="#">空调</a></li>
           </ul>
       </div>
       <script>
           // 这里的[type=search]是属性选择器
           const input = document.querySelector('[type=search]')
           const ul = document.querySelector('.result-list')
           // 监听事件 获得焦点 弹出下拉菜单
           input.addEventListener('focus', function() {
               ul.style.display = 'block'
               input.classList.add('search')
           })
           // 监听事件 失去焦点 隐藏下拉菜单
           input.addEventListener('blur', function() {
               ul.style.display = 'none'
               input.classList.remove('search')
           })
       </script>
   </body>
   ```

3. 键盘触发：keydown 键盘按下触发、**keyup 键盘抬起触发**

   可用于做用户输入框效果

   ```html
   <body>
       <input type="text">
       <script>
           const input = document.querySelector('input')
           // 键盘事件
           input.addEventListener('focus', function() {
               console.log('有焦点触发')
           })
           input.addEventListener('blur', function() {
               console.log('失去焦点触发')
           })
   	</script>
   </body>
   ```

4. 表单输入触发：input 用户输入事件

   ```html
   <body>
       <input type="text">
       <script>
           const input = document.querySelector('input')
           input.addEventListener('input', function() {
               // 实时检测用户输入
               console.log(input.value)
           })
   	</script>
   </body>
   ```

- 清空字符串左右空格：用户输入的字符串内容左右可能包含空格，使用 trim( ) 方法清除。

  ```html
  <script>
  	const str = '   我乃 万物 之主  '
      console.log(str.trim())		// 我乃 万物 之主
  </script>
  ```

还有一些事件散落在其他知识点。

- [submit 事件](#submit)

- [其他事件（load，scroll 等）](###其他事件)

- [移动端事件（touch系列）](##移动端)

- change 事件

  内容发生了变化（当鼠标离开了表单且表单值发生变化时触发）

  ```javascript
  const input = document.querySelector('input')
  input.addEventListener('change', function() {
      console.log(111)
  })
  ```
  
- [loadend 事件](./框架前置.md/)

---

### 事件对象 e

事件对象也是对象，这个对象里有事件触发时的相关信息，例如鼠标点击事件中，事件对象存了鼠标点在哪个位置等信息。

使用场景：判断用户按下了哪个键（比如回车键），用户鼠标点击了哪个元素等。

1. 获取方法：事件回调函数的**第一个参数**，通常取为 event，ev，e

   ```html
   <body>
       <button>点击</button>
       <script>
           const btn = document.querySelector('button')
           btn.addEventListener('click', function(e) {
           })
       </script>
   </body>
   ```

2. 常见事件对象属性

   type 获取当前事件类型

   clientX / clientY 获取光标相对于浏览器可见窗口左上角的位置

   offsetX / offsetY 获取光标相对于当前 DOM 元素左上角的位置

   **key 用户按下的键盘键的值**

   ```html
   <body>
       <input type="text">
       <script>
           const input = document.querySelector('input')
           input.addEventListener('keyup', function(e) {
               // 用户敲下了回车键
               if (e.key === 'Enter') {
                   console.log('我按下了回车键');
               }
           })
       </script>
   </body>
   ```

   【小案例 - 评论区】
   
   ```html
   <head>
       <style>
           /* 其他效果略 */
   		.wrapper .total {
               margin-right: 80px;
               color: #999;
               margin-top: 5px;
               /* 不透明度 */
               opacity: 0;
               transition: all 0.5s;
   		}
       </style>
   </head>
   <body>
       <!-- 输入框 -->
       <div class="wrapper">
           <i class="avatar"></i>
           <textarea id="tx" placeholder="发一条友善的评论" rows="2" maxlength="200"></textarea>
           <button>发布</button>
       </div>
       <!-- 输入框字数显示 -->
      	<div class="wrapper">
       		<span class="total">0/200字</span>
       </div>
       <!-- 评论区 -->
       <div class="list">
       	<div class="item" style="display: none;">
           	<i class="avatar"></i>
           	<div class="info">
                   <p class="name">清风徐来</p>
                   <p class="text">大家都辛苦啦，感谢各位大大的努力，能圆满完成真是太好了[笑哭][支持]</p>
                   <p class="time">2022-10-10 20:29:21</p>
           	</div>
       	</div>
       </div>
   	<script>
           // 获取文本域
           const tx = document.querySelector('#tx')
           // 获取字数显示
           const total = document.querySelector('.total')
           // 获取评论区的显示模式
           const item = document.querySelector('.item')
           // 获取评论区文本内容
           const text = document.querySelector('.text')
           // 当文本域获得焦点，就让 total 显示出来
           tx.addEventListener('focus', function() {
           	total.style.opacity = 1
           })
           // 当文本域失去焦点，就让 total 隐藏起来
           tx.addEventListener('blur', function() {
           	total.style.opacity = 0
           })
           // 检测用户输入
           tx.addEventListener('input', function() {
           // 检测用户输入字符长度 替换 total 的文字部分
           	total.innerHTML = `${tx.value.length}/200字`
           })
           // 弹起键盘获得值
           tx.addEventListener('keyup', function(e) {
               // 弹起键为回车
               if (e.key === 'Enter') {
                   // 用户输入只要不是纯空格
                   if (tx.value.trim()) {
                       // 评论区显示模式由 none 变为 block
                       item.style.display = 'block'
                       // 输入内容放到评论区
                       text.innerHTML = tx.value
               	}
                   // 清空文本域
                   tx.value = ''
                   // 文字计数复原
                   total.innerHTML = '0/200字'
               }
           })
   	</script>
   </body>
   ```

---

### 环境对象

1. 环境对象<a id='this'>.</a>

   环境对象指的是函数内部特殊的变量 this，它代表着当前函数运行所处的环境，粗略规则为：**this 指向当前函数调用者。**

   ```html
   <body>
       <button>点击</button>
       <script>
           const btn = document.querySelector('button')
           btn.addEventListener('click', function() {
               // 按钮点击后变蓝
               // btn.style.color = 'blue'
               this.style.color = 'blue'
           })
   	</script>
   </body>
   ```

2. 回调函数

   当函数 A 作为参数传给函数 B 时，称函数 A 为回调函数

   ```html
   <script>
   	function fn() {
           console.log('fn 就是回调函数')
       }
       // 不会立刻执行，1s后开始执行，并每隔1s执行一次
       setInterval(fn, 1000)
   </script>
   ```

   **案例：**[综合案例 4 - tab 切换](#综合案例 4 - tab 切换)

---

### 事件冒泡与事件解绑 e.sp

事件流指时间完整执行过程中的流动路径。

和现实一样，老外前往中国 > 重庆 > 火锅店，吃完原路返回。这就是事件流。

从大到小为捕获阶段（例如 document > html > body > div），从小到大为**冒泡阶段**。(例如 div > body > html > document)

- 事件捕获（很少用）

  事件监听方法 addEventListener( ) 内其实有第三个参数，默认为 false，设定为 true 将开启捕获。以下例子点击 son 的紫色区域会触发爷爷 > 爸爸 > 孙子。

  ```html
  <head>
      <style>
      	.father {
              width: 300px;
              height: 300px;
              background-color: pink;
          }
          .son {
              width: 50px;
              height: 50px;
              background-color: purple;
          }
      </style>
  </head>
  <body>
      <div class="father">
          <div class="son"></div>
      </div>
      <script>
          const father = document.querySelector('.father')
          const son = document.querySelector('.son')
          document.addEventListener('click', function() {
              alert('爷爷')
          }, true)
          father.addEventListener('click', function() {
              alert('爸爸')
          }, true)
          son.addEventListener('click', function() {
              alert('孙子')
          }, true)
  	</script>
  </body>
  ```

- **事件冒泡 阻止冒泡**

  当一个元素的事件被触发时，**同名的事件**将会在该元素**所有祖先元素依次被触发**，此过程称为事件冒泡。

  由于冒泡一定会发生，有时触发事件不想让父级事件触发，所以要**阻止冒泡。将事件限制在当前元素内。**

  方法名：**事件对象**.**stopPropagation**( )	[简写：e.sp]

  ```html
  <body>
      <div class="father">
          <div class="son"></div>
      </div>
      <script>
          const father = document.querySelector('.father')
          const son = document.querySelector('.son')
          document.addEventListener('click', function() {
              alert('爷爷')
          })
          father.addEventListener('click', function() {
              alert('爸爸')
          })
          son.addEventListener('click', function(e) {
              alert('孙子')
              // 阻止事件流动传播
              e.stopPropagation()
          })
  	</script>
  </body>
  ```

- **阻止元素默认行为**<a id=submit>.</a>

  与事件冒泡类似。但一个是阻止事件扩散，一个是阻止默认行为（阻止链接跳转）

  方法名：事件对象.**preventDefault**( )	[简写：e.pd]

  ```html
  <body>
      <!-- 提交按钮 点击后跳转页面 -->
      <form action="www.zhuce.com">
          <input type="submit" value="免费注册">
      </form>
      <script>
          const form = document.querySelector('form')
          // 事件类型为 submit
          form.addEventListener('submit', function(e) {
              // 阻止提交行为
              e.preventDefault()
          })
  	</script>
</body>
  ```

- 事件解绑

  **匿名函数无法被解绑**，必须给函数起名。

  方法名：**removeEventListener**( 事件类型, 事件处理函数, [获取捕获 / 冒泡阶段])    （[]表示可隐藏）[简写：reme]

  ```html
  <body>
      <button>点击</button>
      <script>
          const btn = document.querySelector('button')
          function fn() {
              alert('点击了')
          }
          btn.addEventListener('click', fn)
          // 事件解绑
          btn.removeEventListener('click', fn)
  	</script>
  </body>
  ```

  在旧版本 Level0 中使用 on 注册的事件，事件解绑很简单。

  ```html
  <body>
      <button>点击</button>
      <script>
          const btn = document.querySelector('button')
          btn.onclick = function() {
              alert('点击了')
              // 第二次点击就没用了
              btn.onclick = null
          }
  	</script>
  </body>
  ```

---

### 事件委托 e.target

- **事件委托**是利用事件流特征解决一些开发需求的技巧。可以**减少注册次数，提高程序性能**。

  比如：实现点击变色效果时，ul 里有5个 li，需要给每个 li 注册事件，使用for循环，可以利用事件会冒泡到父级的特性，给 ul 注册事件。

  使用 **e.target** 获得我们**点击的对象**
  
  使用 **e.target.tagName 筛选标签**
  
  ```html
  <body>
      <ul>
          <li>第1个孩子</li>
          <li>第2个孩子</li>
          <li>第3个孩子</li>
          <li>第4个孩子</li>
          <li>第5个孩子</li>
          <p>我不需要变色</p>
      </ul>
      <script>
          // 点击每个 li，当前 li 文字变红
          const ul = document.querySelector('ul')
          ul.addEventListener('click', function(e) {
              // target.tagName 存的值是大写标签
              if (e.target.tagName === 'LI') {
                  // 使用 事件对象.target 就能获得我们点击的对象
                  e.target.style.color = 'red'
              }
          })
  	</script>
  </body>
  ```
  
  **案例：**[综合案例 4 - Tab 栏切换](#综合案例 4 - Tab 栏切换)

---

### 其他事件

1. 页面加载事件（了解）

   事件名：load

   如果网页资源很多，需要等全局资源加载完毕才能生效的的代码，使用 window + 事件监听 + **load** 事件类型（window 其实不是必须的，等待图片加载完也可以换成 img）

   ```html
   <head>
       <script>
       	// 等待页面所有资源加载结束，就执行回调函数
           window.addEventListener('load', function() {
               const btn = document.querySelector('button')
               btn.addEventListener('click', function() {
                   alert('点击按钮成功')
               })
           })
       </script>
   </head>
   <body>
       <button>点击</button>
   </body>
   ```

   当初始的 HTML 文档完全加载后，DOMContentLoaded 事件被触发，而无需等待样式表，图像等完全加载。

   事件名：DOMContentLoaded 

   ```html
   <body>
       <button>点击</button>
       <script>
           document.addEventListener('DOMContentLoaded', function() {
               const btn = document.querySelector('button')
               btn.addEventListener('click', function() {
                   alert('点击按钮成功')
               })
           })
   	</script>
   </body>
   ```

2. **元素滚动事件**

   网页有时需要检测用户把页面滚动到某个区域后做一些处理，比如**固定导航栏**，**返回顶部**等。

   事件名：**scroll**

   ```html
   <style>
       body {
           height: 3000px;
       }
   </style>
   <script>
       window.addEventListener('scroll', function() {
           console.log('我滚了')
       })
   </script>
   ```

   有时需要获取用户滚动条滚到的位置，需要使用以下属性

   属性名：**scrollTop** 与 scrollLeft

   内容框里的滚动条向下，内容就会向上，向上的距离就是 scrollTop，滚动条向右，scrollLeft 同理。

   使用 **document.documentElement** 获取页面 HTML 元素，该属性**可读写**

   **使用 document.documentElement.scrollTop 获取整个页面的滚动距离**

   ```html
   <head>
       <style>
        	/* 页面有滚动条 */   
           body {
               height: 3000px;
           }
           div {
               display: none;
               width: 200px;
               height: 200px;
               background-color: pink;
           }
       </style>
   </head>
   <body>
       <div></div>
       <script>
           // 启动网页页面滚动条直接到 800 位置
           document.documentElement.scrollTop = 800
           window.addEventListener('scroll', function() {
               // 获取 HTML 元素 这句话必须写在里面
               // 页面一滑动就会取得最新距离值
               const n = document.documentElement.scrollTop
               // 数字不带单位
               if (n >= 100) {
                   document.querySelector('div').style.display = 'block'
               }
           })
       </script>
   </body>
   ```

   【小案例 - 电梯导航】

   ```html
   <head>
       <style>
       	/* 略，xtx-elevator 内有 opacity 与 transition 实现透明与变化效果 */
       </style>
   </head>
   <body>
       <!-- 电梯 -->
       <div class="xtx-elevator">
           <ul class="xtx-elevator-list">
               <li><a href="javascript:;" data-name="new">新鲜好物</a></li>
               <li><a href="javascript:;" data-name="popular">人气推荐</a></li>
               <li><a href="javascript:;" data-name="brand">热门品牌</a></li>
               <li><a href="javascript:;" data-name="topic">最新专题</a></li>
               <li><a href="javascript:;" id="backTop"><i class="sprites"></i>顶部</a></li>
           </ul>
       </div>
       <script>
       	const elevator = document.querySelector('.xtx-elevator')
       	// 当页面滚动大于 300 像素，现实电梯导航
       	window.addEventListener('scroll', function() {
               const n = document.documentElement.scrollTop
               // if (n >= 300) {
               //   elevator.style.opacity = 1
               // } else {
               //   elevator.style.opacity = 0
               // }
   			elevator.style.opacity = n >= 300 ? 1 : 0
           })
           const backTop = document.querySelector('#backTop')
           backTop.addEventListener('click', function() {
   			document.documentElement.scrollTop = 0
           })
       </script>
   </body>
   ```

   完整案例在[综合案例 5 - 电梯导航](#综合案例 5 - 电梯导航)

3. 页面尺寸事件（了解）

   事件名：resize

   可监听浏览器窗口是否发生改变

   属性名：clientWidth 与 clientHeight

   可自动检测盒子宽度、高度 = 内容 + padding（不含 border）

   ```html
   <head>
       <style>
           div {
               display: inline-block;
               height: 200px;
               background-color: pink;
               padding: 10px;
               border: 20px solid skyblue;
           }
       </style>
   </head>
   <body>
       <div>内容内容内容内容内容内容内容内容</div>
       <script>
           const div = document.querySelector('div')
           // 检测盒子宽度 包含padding 不包含 border
           console.log(div.clientWidth);
           window.addEventListener('resize', function() {
               // resize 事件类型可监听浏览器窗口是否发生改变
               console.log(1);
           })
       </script>
   </body>
   ```

4. 元素在页面中的位置（了解）

   滚动多少距离其实不用自己算，最好是页面滚动到某个元素，就可以做某些事情。所以要获取元素在页面中的位置。

- 属性名：offsetWidth 与 offsetHeight

  检测盒子自身宽高 = 内容 + padding + border

  如果盒子是隐藏的，获取结果为 0
  
- 属性名：**offsetLeft** 与 **offsetTop**

  获取自己定位父级元素的左、上距离。（看最近一级带定位的祖先元素）

  **常使用 盒子.offsetTop 获得盒子与页面顶部的距离**

  【小案例 - 顶部导航栏滑动显示、隐藏】

  ```html
  <head>
      <style>
       	/* 其他 css 略 */   
      	.header {
              position: fixed;
              /* 不是直接让顶部隐藏 而是让它划上去不见 所以改 top 值 */
              top: -80px;
              left: 0;
              width: 100%;
              height: 80px;
              background-color: purple;
              text-align: center;
              color: #fff;
              line-height: 80px;
              font-size: 30px;
              transition: all .3s;
          }
      </style>
  </head>
  <body>
      <div class="header">我是顶部导航栏</div>
      <div class="content">
          <div class="sk">秒杀模块</div>
      </div>
      <div class="backtop">
          <img src="./images/close2.png" alt="">
          <a href="javascript:;"></a>
      </div>
      <script>
          const sk = document.querySelector('.sk')
          const header = document.querySelector('.header')
          // 当页面滚动到秒杀模块就改变 top 值
          window.addEventListener('scroll', function() {
              // 获取页面滚动距离
              const n = document.documentElement.scrollTop
              // 滚动距离 === 盒子与网页顶部的距离
              header.style.top = n >= sk.offsetTop ? 0 : '-80px'
          })
      </script>
  </body>
  ```

5. 总结：

   |            属性             |                   作用                   |                             说明                             |
   | :-------------------------: | :--------------------------------------: | :----------------------------------------------------------: |
   |   scrollLeft 和 scrollTop   |            被卷去的头部和左侧            |                   配合页面滚动来用，可读写                   |
   | clientWidth 和 clientHeight |            获取元素宽度和高度            | 不包含 border，margin，滚动条 用于 js 获取元素大小，只读属性 |
   | offsetWidth 和 offsetHeight |            获取元素宽度和高度            |             包含 border，padding，滚动条等，只读             |
   |   offsetLeft 和 offsetTop   | 获取元素距离自己定位父级元素的左、上距离 |               获取元素位置的时候使用，只读属性               |

   **案例：**[综合案例 5 - 电梯导航](#综合案例 5 - 电梯导航)

---

### 日期对象 Date

1. 获得日期对象

   使用 **new** 关键字，实例化时间对象获取时间。

   ```javascript
   // 当前时间
   const date = new Date()
   // 指定时间
   const date1 = new Date('2023-6-15')
   ```

2. 使用 **日期对象.方法**

   |      方法      |    作用    |          说明           |
   | :------------: | :--------: | :---------------------: |
   | getFullYear( ) |  获得年份  |      获取四位年份       |
   |  getMonth( )   |  获得月份  |    取值为 **0 ~11**     |
   |   getDate( )   |   获得日   |    根据月份取值不同     |
   |   getDay( )    | 获得星期几 | 星期天为0,，取值为0 ~ 6 |
   |  getHours( )   |  获得小时  |      取值为 0 ~ 23      |
   | getMinutes( )  |  获得分钟  |      取值为 0 ~ 59      |
   | getSeconds( )  |   获得秒   |      取值为 0 ~ 59      |

   ```javascript
   const date = new Date()
   console.log(date.getMonth() + 1)	// 记得加1
   ```

   【小案例 - 格式化时间】显示当前时间，格式为 2023-06-15 20:50

   ```html
   <head>
       <style>
           div {
               width: 300px;
               height: 50px;
               background-color: pink;
           }
   	</style>
   </head>
   <body>
       <div></div>
       <script>
           const div = document.querySelector('div')
           function getMyDate() {
               const date = new Date()
               let h = date.getHours()
               h = h < 10 ? '0' + h : h
               let m = date.getMinutes()
               m = m < 10 ? '0' + m : m
               let s = date.getSeconds()
               s = s < 10 ? '0' + s : s
               return `${date.getFullYear()}年${date.getMonth() + 1}月${date.getDate()}日 ${h}:${m}:${s}`
           }
            // 获取第一次实时
           div.innerHTML = getMyDate()
           // 1s后每秒刷新一次
           setInterval(function() {
               div.innerHTML = getMyDate()
           }, 1000)
       </script>
   </body>
   ```

   以上内容图一乐，以下方法简单

   方法名：**toLocaleString**( ) ，得到以上**模板时间**

   ```javascript
   const div = document.querySelector('div')
   // 得到日期对象
   const date = new Date()
   div.innerHTML = date.toLocaleString()
   setInterval(function() {
       // new Date().toLocaleString()
       const date = new Date()
       div.innerHTML = date.toLocaleString()
   }, 1000)
   ```

3. 时间戳 **new Date().toLocaleString()**

   时间戳是从1970年1月1日0点到现在的**毫秒数**，用来计算倒计时

   倒计时毫秒数 = 将来的时间戳 - 现在的时间戳

   获取当前时间戳：使用 **+new Date()**

   ```javascript
   // 获取当前时间戳
   // 方法 1
   const date = new Date()
   console.log(date.getTime())
   // 方法 2 - 推荐
   console.log(+new Date())
   // 方法 3
   console.log(Date.now())
   
   // 获取某时间的时间戳
   console.log(+new Date('2023-6-15 21:31:00'))
   ```

   【小案例 - 返回星期几】

   ```javascript
   const arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
   console.log(arr[new Date().getDay()])
   ```
   
   【小案例 - 倒计时】
   
   ```html
   <body>
       <div class="countdown">
           <p class="next">今天是2222年2月22日</p>
           <p class="title">下班倒计时</p>
           <p class="clock">
               <span id="hour">00</span>
               <i>:</i>
               <span id="minutes">25</span>
               <i>:</i>
               <span id="scond">20</span>
           </p>
           <p class="tips">21:30:00下课</p>
       </div>
       <script>
       	// 获取倒计时
           function getCountTime() {
               const now = +new Date()
               const last = +new Date('2023-6-16 21:30:00')
               // 得到剩余时间戳 count，转化为秒数
               const count = (last - now) / 1000
               let h = parseInt(count / 60 / 60 % 24)
               h = h < 10 ? '0' + h : h
               let m = parseInt(count / 60 % 60)
               m = m < 10 ? '0' + m : m
               let s = parseInt(count % 60)
               s = s < 10 ? '0' + s : s
               document.querySelector('#hour').innerHTML = h
               document.querySelector('#minutes').innerHTML = m
               document.querySelector('#scond').innerHTML = s
           }
           getCountTime()
           // 开启定时器
           setInterval(getCountTime, 1000)
       </script>
   </body>
   ```

---

## DOM - 节点 （增删拷查）

DOM 树里每一个内容都称之为节点。节点类型分为：元素节点（div，body）、属性节点（href）、文本节点（所有的文本）等。

1. **查找节点**

   这里是通过关系来查找节点，而不是通过querySelector( ) 获取每一个元素，通过元素间的节点关系可以找到其他元素。

- 找父节点

  属性名：**parentNode**

  ```html
  <body>
      <div class="ye">
          <div class="class">
              <div class="baby"></div>
          </div>
      </div>
      <script>
          const baby = document.querySelector('.baby')
          console.log(baby.parentNode)
          console.log(baby.parentNode.parentNode)
      </script>
  </body>
  ```

- 找子节点

  属性名：**children**

  获得**所有**子元素节点，返回一个伪数组。

  ```html
  <body>
      <ul>
          <li>
              <p>第一个段落</p>
          </li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
      </ul>
      <script>
          const ul = document.querySelector('ul')
          console.log(ul.children)
      </script>
  </body>
  ```

- 找兄弟节点

  属性名：**previousElementSibling** 与 **nextElementSibling**

  ```html
  <body>
      <ul>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
      </ul>
      <script>
          const li2 = document.querySelector('ul li:ntj-child(2)')
          console.log(li2.previousElementSibling) // 上一个兄弟
          console.log(li2.nextElementSibling)     // 下一个兄弟
      </script>
  </body>
  ```

2. **新增节点**

   需要新增元素的场景可使用，比如发布按钮新增一条消息。

   创建方法名：**document.createElement**( )    [简写：doc.cee]

   说明：可以创建元素，创建完元素，还要将元素追加到某父元素内。

   追加方法名1：父元素.appendChild( 要插入的元素 )    [简写：apc]

   说明：该方法可以追加元素作为父元素的**最后子元素**

   追加方法名2：父元素.**insertBefore**( 要插入的元素，要插到的位置)    [简写：ib]

   说明：前插，会插入到指定位置之前

   ```html
   <body>
       <ul>
           <li>老二</li>
       </ul>
       <script>
           const ul = document.querySelector('ul')
           // 创建节点
           const li = document.createElement('li')
           // 追加节点 - 作为最后一个子元素
           li.innerHTML = '老大'
           // ul.appendChild(li)
           // 追加节点 - 将 li 作为第一个元素插入
           ul.insertBefore(li, ul.children[0])
       </script>
   </body>
   ```

3. **克隆节点与删除节点**

   克隆方法名：元素.**cloneNode**( 布尔值 )

   说明：取值为 true，则代表克隆时会包含后代一起克隆，取值为 false（默认），则代表克隆时不包含后代节点。

   删除方法名：父元素.**removeChild**( 要删除的子元素 )

   说明：必须找到要删除元素的父元素

   ```html
   <body>
       <ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
       </ul>
       <script>
           const ul = document.querySelector('ul')
           // 克隆 li1
           // const li1 = ul.children[0].cloneNode(true)
           // 追加 li1 到最后
           // ul.appendChild(li1)
           ul.appendChild(ul.children[0].cloneNode(true))
           ul.removeChild(ul.children[0])   
       </script>
   </body>
   ```

**案例：**[综合案例 6 - 学生信息表](##综合案例 6 - 学生信息表)

---

## 移动端

1. M端事件

   **移动端**触屏事件 **touch**，touch 对象代表一个触摸点，触摸事件可响应用户手指，对屏幕或者触控板操作。

   常见触屏事件如下：

   | 触屏 touch 事件 |              说明               |
   | :-------------: | :-----------------------------: |
   |   touchstart    |  手指触摸到一个 DOM 元素时触发  |
   |    touchmove    | 手指在一个 DOM 元素上滑动时触发 |
   |    touchend     |  手指从一个 DOM 元素移开时触发  |

   ```html
   <head>
       <style>
           div {
               width: 300px;
               height: 300px;
               background-color: pink;
           }
       </style>
   </head>
   <body>
       <div></div>
       <script>
           const div = document.querySelector('div')
           div.addEventListener('touchstart', function() {
               console.log('开始触摸')
           })
           div.addEventListener('touchend', function() {
               console.log('触摸离开')
           })
           div.addEventListener('touchmove', function() {
               console.log('在划动')
           })
       </script>
   </body>
   ```

2. **js 插件**

   [swiper](https://swiper.com.cn) 是一个开源插件，即别人写好，直接拿来。移动端的基本都是插件。找到需要的效果，下载好本地文件，通过文件引入并复制相应代码即可。

   ```html
   <head>
       <link rel="stylesheet" href="./css/swiper-bundle.min.css">
       <style>
           /* 粘贴原网页代码 */
       </style>
   </head>
   <body>
       <!-- 粘贴原网页代码 -->
       <script src="./js/swiper-bundle.min.js"></script>
   </body>
   </html>
   ```

   需要定制的话，在官网点击 API 文档，查询相关代码复制粘贴即可。

---

## BOM - window 对象

BOM (Browser Object Model) 是浏览器对象模型

- windows 对象是一个全局对象，也是 javascript 中的顶级对象
- 像 document，alert，console.log( )这些都是 window 的属性，基本的 BOM 的属性和方法都是 window 的
- 所有 var 定义在全局作用域的变量，函数都会变成 window 对象的属性和方法
- window 对象的属性和方法调用的时候可以省略 window

### 定时器 setTimeout

与之前的间歇函数类似。

- 延时函数：延迟一段时间执行的函数

  方法名：**setTimeout**( 函数, 等待的毫秒数 )

  返回值：数字（定时器的编号）

  ```html
  <script>
  	setTimeout(function () {
          console.log('时间到了')
      }, 2000)
  </script>
  ```

- 清除延时函数：通常延时函数只用一次，不需要清除，特殊情况下（递归）需要清除：

  方法名：clearTimeout( )

  ```html
  <script>
  	let timer = setTimeout()
      clearTimeout(timer)
  </script>
  ```

- js 执行顺序：同步任务栈内执行，异步任务入队列，轮到了再从队列压入栈执行

  ```javascript
  console.log(1)
  console.log(2)
  setTimeout(function () {
      console.log(3)
  }, 0)
  console.log(4)			// 执行结果：1243
  ```

  主线程不断获取任务，执行任务，再获取再执行，这种机制称为**事件循环**。

---

### location 对象

- location.href 经常用来做自动跳转页面

  ```html
  <body>
      <a href="#">支付成功<span>5</span>秒后跳转到页面</a>
      <script>
          const a = document.querySelector('a')
          let num = 5
          let timeId = setInterval(function() {
              num--
              a.innerHTML = `支付成功<span>${num}</span>秒后跳转到页面`
              if (num === 0) {
                  clearInterval(timeId)
                  location.href = 'http://www.baidu.com'
              }
          }, 1000)
      </script>
  </body>
  ```

- location.search 用来拿取网址？后的部分，即表单提交的信息，用户名密码等

  ```html
  <body>
      <!-- 输入后，网址会出现? 使用 location.search 可获取此部分 -->
      <form action="">
          <input type="text" name="username">
          <input type="password" name="pwd">
          <button>提交</button>
      </form>
  </body>
  ```

- location.hash 用来拿取网址 # 后的部分，即同一页面下的链接分支（不用刷新页面）

  ```html
  <!-- 点击链接不会刷新页面，但会加载新页面 -->
  <a href="#/my">我的</a>
  <a href="#/friend">关注</a>
  <a href="#/download">下载</a>
  ```

- location.reload( ) 刷新页面，传入参数为 true 为强制刷新

  ```html
  <body>
      <button class="reload">刷新</button>
      <script>
          const reload = document.querySelector('.reload')
          reload.addEventListener('click', function() {
              // 刷新页面
              location.reload()
              // 强制刷新 类似于 ctrl + F5 强制刷新
              location.reload(true)
          })
      </script>
  </body>
  ```

---

### navigator 对象

navigator 对象记录了浏览器自身相关信息，用的浏览器，语言，版本等。

- navigator.userAgent 用来获取用户浏览器数据，判断是否为 Android 或 ios 以自动跳转到移动端。

  ```html
  <script>
  	!(function () {
          // 以下代码可自动检测移动端并跳转
          const userAgent = navigator.userAgent
          // 验证是否为Android或iPhone
          const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
          const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
          // 如果是Android或iPhone，则跳转至移动站点
          if (android || iphone) {
  			location.href = 'http://m.baidu.com'
  		}
  	})();
  </script>
  ```

---

### history 对象

- history.go( ) ：其实就是；浏览器上的后退按钮和前进按钮，参数为-1就是后退，1就是前进。和 back 与 forword 等价，用得不多。

  ```html
  <body>
      <button>后退</button>
      <button>前进</button>
      <script>
          const back = document.querySelector('button:first-child')
          forword = back.nextElementSibling
          back.addEventListener('click', function() {
              // history.back()
              history.go(-1)
          })
          forword.addEventListener('click', function() {
              // history.forward()
              history.go(1)
          })
      </script>
  </body>
  ```

---

### 本地存储 LocalStorage 与 JSON

经常在本地存储大量数据，数据**存储在**用户**浏览器**中，刷新页面不会丢失数据。

- LocalStorage 刷新不消失 **键一定带引号！**

  可以将数据永久存储在本地，除非手动删除，否则关闭页面也会存在。

1. 增：LocalStorage.setltem (键，值)，存储的数据可在浏览器 F12 - 应用部分看到，本地存储**只能存字符串**

   ```html
   localStorage.setItem('赵铁牛', '1000岁')
   ```

2. 删：LocalStorage.removeItem (键)

   ```html
   localStorage.removeItem('赵铁牛')
   ```

3. 改：如果键本身就存在，那就是改，本身不存在，就和增是一样的

4. 查：LocalStorage.getItem (键)，**记得加引号**

   ```html
   localStorage.getItem('赵铁牛')
   ```

- sessionStorage 刷新消失，与上面的 LocalStorage 相同

- **存储复杂数据类型**

1.  **JSON.sringify** ( 复杂数据类型 )

    对象必须**转化为 JSON 字符串**才能存储在本地。JSON 对象的属性和值都有**双引号**

     ```javascript
   const obj = {
       uname: '赵铁牛',
       age: 100,
       gender: '男'
   }
   // 存储 对象转化为字符串
   localStorage.setItem('obj', JSON.stringify(obj))
    ```

2. **JSON.parse** ( json字符串 )

   该方法可将 json 字符串转化为复杂数据类型（**对象数组**）

   ```javascript
   // 使用 字符串转化为对象
   const str = localStorage.getItem('obj')
   console.log(JSON.parse(str))
   ```

案例：[综合案例 6 - 学生信息表 - 效果2](##综合案例 6 - 学生信息表)

---

### map 与 join 方法

这俩方法一个是数组方法，一个转化字符串方法，下面的综合案例用到这两个方法和本地存储的内容所以放在这里。

- **map 方法**：

  map 可以遍历数组**处理数据**，并**返回新的数组**，map 称为映射，指两个元素相互对应的关系，map 重点在于**有返回值**。

  **不要用 map 遍历数组**，违背初衷，它用来返回新数组。

  ```javascript
  const arr = ['red', 'blue', 'green']
  // 数组 map 方法 ele:元素 index:索引
  const newArr = arr.map(function (ele, index) {
      return ele + '颜色'
  })
  console.log(newArr)
  ```

- **join 方法**：

  join 方法可以**把数组中的所有元素转化为一个字符串**，传参是空字符串就会没有分隔。

  ```javascript
  // join 方法
  const arr = ['red', 'blue', 'green']
  // 默认用逗号分隔
  console.log(arr.join())         // red,blue,green
  console.log(arr.join(''))       // redbluegreen
  console.log(arr.join('|'))      // red|blue|green
  ```

案例：[综合案例 6 - 学生信息表 - 效果2](##综合案例 6 - 学生信息表)

---

## 正则表达式

正则表达式是用于匹配字符串中字符组合的模式，在 Javascript 中，正则表达式也是对象。通常用来表单验证（**匹配**），过滤敏感词（**替换**），字符串**提取**想要的部分。 

- **简单版本语法**

1. 定义正则表达式语法：/ / 表示正则表达式字面量，使用 **test( )** 验证是否匹配

   ```javascript
   // 要检测的字符串
   const str = '被检测的字符串'
   // 定义规则
   const 变量名 = /表达式/
   // test 判断是否有符合规则的字符串 返回 boolean
   规则变量名.test(str)
   // exec 检索符合规则的字符串，返回数组 或 null，数组里包含索引
   规则变量名.exec(str)
   ```

   举例：

   ```javascript
   const str = '你是真牛逼啊'
   const reg = /逼/
   console.log(reg.test(str))	// true
   ```

- **元字符**

  前面的只能匹配普通字符，元字符是具有特殊含义的字符，极大提高了灵活性和强大的匹配功能。例如匹配只能是26个英文字母的字符串使用 [a-z]，正则表达式里 | 符号是 或|| 的意思

  元字符分为三类：

1. 边界符：**提示字符所处的位置**

   | 边界符 |              说明               |
   | :----: | :-----------------------------: |
   |   ^    | 表示匹配行首的文本（以谁开始）  |
   |   $    | 表示匹配行尾的文本（以谁结束 ） |

2. 量词：**表示重复次数**（如密码规定6位）

   | 量词  |               说明               |
   | :---: | :------------------------------: |
   |   *   |         重复零次或更多次         |
   |   +   |         重复一次或更多次         |
   |   ?   |          重复零次或一次          |
   |  {n}  |            重复 n 次             |
   | {n,}  |        重复 n 次或更多次         |
   | {n,m} | （, 后不能空格！）重复 n 到 m 次 |

3. 字符类：

   | 字符类 |                     说明                     |
   | :----: | :------------------------------------------: |
   |   []   |     [abc] 表示出现abc任何一个字符就可以      |
   |  [^]   | [] 内出现^ 表示取反 \[^a-z] 表示除了小写字母 |
   |   .    |       表示除了换行符以外的任何单个字符       |

   字符类有一些预定义，指某些常见模式的简写方式

   | 预定类 |                            说明                             |
   | :----: | :---------------------------------------------------------: |
   |   \d   |             匹配 0~9 间的任一数字，等价于 [0-9]             |
   |   \D   |           匹配所有非 0~9 以外的字符，等价于 [0-9]           |
   |   \w   |       匹配任意字母，数字和下划线，等价于 [a-zA-Z0-9_]       |
   |   \W   |   匹配字母，数字和下划线以外的字符，等价于 \[^a-zA-Z0-9_]   |
   |   \s   | 匹配空格（包括换行符，制表符，空格符），等价于 [\t\r\n\v\f] |
   |   \S   |           匹配非空格的字符，等价于 \[^\t\r\n\v\f]           |

   例子：

   ```javascript
   console.log(/哈/.test('哈'))                // true
   console.log(/哈/.test('哈哈'))              // true
   console.log(/哈/.test('二哈'))              // true
   console.log('-------边界符--------')
   console.log(/^哈/.test('哈'))               // true
   console.log(/^哈/.test('哈哈'))             // true
   console.log(/^哈/.test('二哈'))             // false
   console.log(/^哈$/.test('哈'))              // true
   // 以哈开始，以哈结束，且精确匹配只能有一个哈
   console.log(/^哈$/.test('哈哈'))            // false 
   console.log('--------量词---------')
   // * 等价于 >= 0 次 精确匹配，允许哈出现0次到多次，但不允许任何其他字符
   console.log(/^哈*$/.test('哈哈'))           // true
   console.log(/^哈*$/.test(''))               // true
   console.log(/^哈*$/.test('二哈'))           // false
   console.log(/^哈*$/.test('哈屁哈'))         // false
   // + 等价于 >= 1 次
   console.log(/^哈+$/.test(''))               // false
   // ? 等价于 0 || 1 有1个或者没有
   console.log(/^哈?$/.test('哈'))             // true
   console.log('------常用量词-------')
   // {n} 等价于 = n 次  {n,} 等价于 >= n 次
   console.log(/^哈{4}$/.test('哈哈哈哈'))     // true
   console.log(/^哈{4}$/.test('哈哈哈哈哈'))   // false
   console.log(/^哈{4,}$/.test('哈哈哈哈哈'))  // true
   // {n,m} 不能有空格！ 等价于 >=n 且 <=m 次
   console.log(/^哈{4,6}$/.test('哈哈哈哈哈')) // true
   console.log('-------字符类--------')
   console.log(/^[abc]$/.test('b'))           // true
   // 精确匹配 前面的[abc]只会选择了一个
   console.log(/^[abc]$/.test('ab'))          // false
   console.log(/^[abc]{2}$/.test('ab'))       // true
   // [a-z] 表示 26 个英文字母即可 但只能有 1 个
   console.log(/^[A-Z]$/.test('p'))           // false
   console.log(/^[0-9]$/.test('7'))           // true
   // 大小写英文字母，0~9数字 但只能有 1 个
   console.log(/^[a-zA-Z0-9]$/.test('7'))     // true
   ```

   【小案例 - 用户名验证案例】

   要求用户名为英文字母，数字，下划线或者短横线组成，并且用户长度为 6-16位，使用正则表达式：/^[a-zA-Z0-9-_]{6,16}$/

   ```html
   <body>
       <input type="text">
       <span></span>
       <script>
           const reg = /^[a-zA-Z0-9-_]{6,16}$/
           const input = document.querySelector('input')
           const span = document.querySelector('span')
           input.addEventListener('blur', function() {
               // console.log(reg.test(this.value))
               if (reg.test(this.value)) {
                   // span 区域追加输入正确文字 添加类（包含了文字效果）
                   span.innerHTML = '输入正确'
                   span.className = 'right'
               } else {
                   span.innerHTML = '我超你妈'
                   span.className = 'error'
               }
           })
       </script>
   </body>
   ```

- 修饰符

  修饰符约束正则执行的某些细节行为，如是否区分大小写，是否支持多行匹配等

  ```javascript
  /表达式/修饰符
  ```

  | 修饰符 |                  说明                  |
  | :----: | :------------------------------------: |
  |   i    |    正则表达式匹配时字母不区分大小写    |
  |   g    | 全局查找，匹配所有满足正则表达式的结果 |

  替换 **replace**( ) ：会把匹配正则表达式的部分用后面的文本替换

  ```javascript
  字符串.replace(/正则表达式/, '替换的文本')
  ```

  举例：
  ```javascript
  const str = '老二打了老大一拳，老大的老二漏了出来'
  const re = str.replace(/老二/g,'**')
  console.log(re)								// **打了老大一拳，老大的**漏了出来
  ```

**案例：**[综合案例 7 - 用户注册页面](##综合案例 7 - 用户注册页面)

---

# JavaScript 进阶

## 作用域

### 作用域与作用域链

前面的笔记提过一嘴作用域：[跳转](#zyy)

作用域规定了变量能够访问的范围，离开了这个范围，变量便不能访问。

- **局部作用域**

  局部作用域分为**函数作用域**和**块作用域**

1. 函数作用域：

   在函数内部声明的变量只能在函数内被访问，外部无法直接访问。

   函数的形参也是函数内部的局部变量。

   不同函数内部声明的变量无法互相访问

   函数执行完毕后，函数内部的变量实际被清空了

2. **块作用域**

   js 中只要是被 {} 包裹的代码都是代码块，代码块内声明的变量外部通常无法直接访问（有些手段可以访问,，比如使用 var）

   ```javascript
   for (let i = 0; i <= 3; i++) {
       // 块作用域
       console.log(i)				// 可访问
   }
   console.log(i)					// 报错
   ```

   上面的代码如果把 let 改为 var，就不会报错了，因为  **var 不会产生块作用域**，let 声明的变量会产生快作用域，const 声明的常量也会产生快作用域。所以推荐使用 let 与 const

- **全局作用域**

  \<script> 标签 和 .js 文件的**最外层**就是所谓的全局作用域，在此声明的变量在函数内部也可以被访问。

  （注意为 window 对象动态添加的属性默认也是全局变量，不推荐使用）

  （函数中未使用任何关键字声明的变量也是全局变量，不推荐使用）

  **尽可能减少声明全局变量，防止全局变量污染**

- **作用域链**

  **作用域链本质是底层的变量查找机制**

  在函数被执行时，会**优先查找当前函数**作用域中的变量

  如果当前作用域查找不到则会**依次逐级查找父级作用域**直到全局作用域

  ```javascript
  // 全局作用域
  let a = 1
  let b = 2
  // 局部作用域
  function f() {
      let a = 1
      // 局部作用域
      function g() {
          a = 2
          console.log(a)			// 2
      }
      g()
  }
  f()
  ```

  以上代码不会报错，打印结果是 2

  以上代码的作用域链：		global  ——   f( )  ——  g( )

  总结：

1. 嵌套关系的作用域串联起来形成了作用域链
2. 相同作用域链中按着从小到大的规则查找变量
3. **子作用域能够访问父作用域，父作用域无法访问子级作用域**

---

### 垃圾回收机制

JS 中内存的分配和回收是自动完成的，内存在不使用的时候会被垃圾回收器自动回收

- 内存的生命周期

  **内存分配：**当声明变量、函数、对象的时候，系统会自动为他们分配内存

  **内存使用：**即读写内存，使用变量、函数等

  **内存回收：**使用完毕，由垃圾回收器自动回收不再使用的内存

  说明：全局变量一般不会回收（关闭页面回收），一般情况下局部变量的值，不用了就会被自动回收掉

  **内存泄漏：**程序中分配的内存由于某种原因程序**未释放或无法释放**叫做内存泄漏

- JS 垃圾回收机制

  堆栈空间分配区别：

1. 栈：由操作系统自动分配释放函数的参数值，局部变量等，基本数据类型存放在栈里

2. 堆：一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收，复杂数据类型存放在堆里

   回收算法：

1. 引用计数法：IE 采用此算法，定义为“**内存不再使用**”，就是看一个对象是否有指向它的引用，没有引用了就回收对象

   跟踪记录被引用的次数，如果被引用了一次，那么就记录次数1，多次引用会累加，弱减少一个引用就减1，如果引用次数是0，则释放内存。

   ```javascript
   const arr = [1, 2, 3, 4]		// [1,2,3,4] 存在堆里，地址存在栈里，被地址引用，引用数为 1
   arr = null						// arr 为空，地址消失，[1,2,3,4]不再被引用，被内存释放
   ```

   因此想释放内存一种常用方法，就是赋值为 null

   ```javascript
   let person = {					// 声明对象默认就有个地址在堆里，地址指向栈里的对象，所以此时对象被引用数为 1
       age: 18,
       name: '吕布'
   }
   let p = person					// person 的值是地址，地址赋值给了 p,现在 p 也指向对象，引用数为 2
   person = 1
   p = null						// 引用数为 0，内存释放
   ```

   这个方法有致命缺点，**嵌套引用**，所以现在已经不再使用：

   ```javascript
   function fn() {
       let o1 = {}					// 堆里开对象，栈里存地址，o1 被引用 1
       let o2 = {}					// 堆里开对象，栈里存地址，o2 被引用 1
       o1.a = o2					// o1 引用一次 o2，o2 被引用 2
       o2.a = o1					// o2 引用一次 o1，o1 被引用 2
       return '引用计数无法回收'
   }
   fn()							// 两个对象相互引用，函数执行后引用数也不为 0，无法回收，内存泄漏
   ```

2. 标记清除法：现在浏览器使用此方法，定义为“**无法达到的对象**”，就是从根部（JS 中是全局对象）出发定期扫描内存中的对象，凡是能从根部到达的对象，都是**还需要使用**的。无法从根部出发触及到的对象被标记为不再使用，稍后进行回收。

   这里上面嵌套引用的例子就因为在函数内部，根部无法直接进入函数，所以会自动回收掉。

---

### 闭包

闭包的概念：一个函数对周围状态的引用捆绑在一起，**内层函数中访问到其外层函数的作用域**

- 理解：闭包 = 内层**函数** + 外层函数的**变量**

  ```javascript
  function outer() {
      const a = 1
      function f() {
          console.log(a)				// 内层函数使用了外层的变量
      }
      f()
  }
  outer()
  ```

  因此如果一个函数内有个变量，想在外部使用函数内部这个变量，可以使用闭包的方法。

  ```javascript
  function outer() {
      let a = 10
      function fn() {
          console.log(a)
      }
      return fn
  }
  // outer() === fn() === function fn() {}
  const fun = outer()
  fun()								// 相当与调用了 outer() 里的 fn()
  ```

  调用 outer( ) 相当于 调用 fn( )，调用 fn( ) 又相当于调用 function fn() {}，使得**外部函数使用了内部函数的值**。

- 闭包的应用：实现**数据私有**

  比如统计调用函数的次数，如果定义全局变量初始为0，然后在函数内写变量++，调用一次输出变量的值，就可以达到目的。但是，定义了全局变量，很容易被修改。可使用闭包：

  ```javascript
  function fn() {
      let count = 0
      function fun() {
          count++
          console.log(`函数被调用${count}次`)
      }
      return fun
  }
  const result = fn()
  result()						// 只要调用一次，count就加一次
  count = 1000
  result()						// 函数被调用2次，就算 count 修改过，也不影响调用
  ```

  这么写了之后，只要调用 fun( )，就能查看调用了几次，就算期间修改了 i 的值，实现了数据的私有，使用完后，页面不关闭，内存不会被回收，发生**内存泄漏**。

---

## 函数进阶

### 变量提升与函数提升

- 变量提升：用 var 声明的变量会发生的特有现象。当代码执行之前，会**在当前作用域下**把用 var 声明的全局变量提升到当前作用域的最前。**只提升声明，不提升赋值**

  ```javascript
  // var num --- 相当于在这里声了明
  console.log(num + '件')				// undefined 件
  var num = 10
  ```

  所以推荐先用 let 和 const 声明再访问变量。

- 函数提升：和变量提升类似，声明前即可调用，**只提升函数声明，不提升函数调用。**

  ```javascript
  fn()
  function fn() {
      console.log('函数提升')
  }
  ```

  但是下面这种就会报错。

  ```javascript
  fun()
  var fun = function () {
      console.log('函数表达式')
  }
  ```

  因为相当于在前面 var fun，再给 fun 赋值函数，付之前的 fun( ) 会被认为不是函数无法调用报错。

---

### 函数剩余参数与展开运算符

动态参数与剩余参数可以让用户**传参的个数不固定**。

1. 动态参数

   每个函数内都有一个默认参数 **arguments**，arguments 本质是个伪数组，存的值就是传参，**只存在于函数内**

   ```javascript
   function getSum() {
       console.log(arguments)
       let sum = 0
       for (let i = 0; i < arguments.length; i++) {
           sum += arguments[i]
       }
   }
   getSum(2, 3)
   getSum(2, 3, 4, 5)
   ```

2. **剩余参数**

   传参使用省略号。... 为语法符号，**至于最末参数之前**，用于获取多余的实参，借助 ... 获取的剩余实参，是个**真数组**。推荐开发者使用剩余参数的方法。

   ```javascript
   function getSum(a, b, ...arr) {
       console.log(arr)
       let sum = 0
       sum = a + b
       for (let i = 0; i < arr.length; i++) {
           sum += arr[i]
       }
   }
   getSum(2, 3, 4)
   getSum(2, 3, 4, 5)
   ```

- 展开运算符<a id='zhan'>.</a>

  展开运算符与剩余参数看起来非常像。可以**将一个数组展开**，且不会修改原数组。

  常见使用场景是求数组最大值和合并数组

  ```javascript
  const arr1 = [1, 2, 3]
  // 展开运算符 可以展开数组
  console.log(...arr1)						// 1 2 3
  // 应用场景1：求数组的最大值 别纠结传参没逗号，其实有逗号
  console.log(Math.max(...arr1))				// 3
  // 应用场景2：合并数组
  const arr2 = [3, 4, 5]
  const arr = [...arr1, ...arr2]
  console.log(arr)							// [1,2,3,3,4,5]
  ```


---

### 箭头函数

引入箭头函数的目的是更简短的函数写法并且不绑定 this，箭头函数的语法比函数表达式更简洁。

箭头函数更适用于那些本来**需要匿名函数的地方**

- 基本语法

   ```javascript
   // 函数表达式
   const f = function () {
       console.log(123)
   }
   f()
   
   // 箭头函数 - 基础写法
   const fn = () => {
       console.log(123)
   }
   fn()                        // 123
   ```

- 箭头函数函数参数

  ```javascript
  // 传参只有一个，可省略小括号
  const fun = x => {
      console.log(x)
  }
  fun(11)                     // 11
  
  // 只有一行代码，可省略大括号
  const func = x => console.log(x)
  func(1234)                  // 1234
  
  // 只有一行返回值代码，可省略 大括号 和 return
  const func = x => x + x
  func(1)                  	// 2
  ```

  **箭头函数可以直接返回对象**

  ```javascript
  // const fn = function(uname) {
  //     return {
  //         uname: uname
  //     }
  // }
  // 因为返回的是对象，函数也是{}，所以把对象的{}用()包起来表示返回对象
  const fn = (uname) => ({uname: uname})
  console.log(fn('mario'))
  ```
  
  箭头函数应用实例：利用箭头函数求和

  ```javascript
  const getSum(...arr) => {
      let sum = 0
      for(let i = 0; i < arr.length; i++) {
          sum += arr[i]
      }
      return sum
  }
  const result = getSum(2, 3, 4)
  console.log(result)
  ```
  
- 普通函数 this

  以前提过一嘴 this [跳转](#this)，这里回顾一下

  ```javascript
  // 谁调用就指向谁
  console.log(this)				// window
  
  function fn() {
      console.log(this)			// window
  }
  fn()
  
  const obj = {
      name: 'mario',
      jump: function () {
          console.log(this)		// this 指向 obj，因为 obj.jump()
      }
  }
  obj.jump()
  ```

- **箭头函数 this**<a id='thi'>.</a>

  在箭头函数中，**箭头函数不会创建自己的 this**，它只会从自己的作用域链的**上一层**沿用 this

  ```javascript
  // 箭头函数内没有 this，会去找上一层，上一层是空的，是 window
  const fn = () => {
      console.log(this)			// window
  }
  fn()
  
  const obj = {
      name: 'mario',
      jump: () => {
          console.log(this)		// this 指向 window，因为 jump 中没有this，沿用上一级 obj 的 this
      }							// 而 window 调用 obj，所以 this 指向 window
  }
  obj.jump()						// window.obj.jump()
  
  const obj1 = {
      name: 'mario',
      jump: function() {
          let i = 10
          const count = () => {
              console.log(this)	// this 指向 obj，因为箭头函数作用域没有this，沿用上一层 jump 的 this，即 obj1
          }
          count()
      }	
  }
  obj1.jump()
  ```
  
  注意：在开发中，使用箭头函数需考虑函数中 this 的值，事件回调函数使用箭头函数时，this 为全局的 window
  
  因此 **DOM 事件回调函数为了简便，不推荐使用箭头函数**
  
  ```javascript
  const btn = document.querySelector('.btn')
  this.addEventListener('click', () => {
      console.log(this)			// this 指向 window
  })
  this.addEventListener('click', function() {
      console.log(this)			// this 指向 btn
  })
  ```

---

### 解构赋值

- **数组解构**

  数组解构是**将数组的单元值快速批量赋值给一系列变量**的简洁语法。

  以前的写法：

  ```javascript
  const arr = [100, 60, 80]
  const max = arr[0]
  const min = arr[1]
  const avg = arr[2]
  console.log(max)
  console.log(min)
  console.log(avg)
  ```

- **数组解构的写法：**

  ```javascript
  // const arr = [100, 60, 80]
  // const [max, min, avg] = arr
  const [max, min, avg] = [100, 60, 80]			// 别忘了 const
  console.log(max)
  console.log(min)
  console.log(avg)
  ```

1. 数组解构可用剩余参数

   ```javascript
   const [a, b, ...c] = [1, 2, 3, 4]
   console.log(a)									// 1
   console.log(b)									// 2
   console.log(c)									// [3, 4]
   ```

2. 数组解构也可用默认值

   ```javascript
   const [a = 1, b = 2] = [3]
   console.log(a)									// 3
   console.log(b)									// 2
   ```

3. 数组解构可以按需忽略赋值，该忽略的地方记得空着

   ```javascript
   const [a, b,  , d] = [1, 2, 3, 4]
   console.log(a)									// 1
   console.log(b)									// 2
   console.log(d)									// 4
   ```

4. 数组解构可以解构多维数组

   ```javascript
   const [a, b, [c, d]] = [1, 2, [3, 4]]
   console.log(a)									// 1
   console.log(b)									// 2
   console.log(c)									// 3
   console.log(d)									// 4
   ```
   
   【小案例 - 两数交换】

   ```javascript
   let a = 1
   let b = 2;										// 这里必须加分号！
   [b, a] = [a, b]
   ```
   
   数组作为语句开头时，前面有代码的话要在数组前一句末尾或数组前加 ;
   
   JS 中同样加 ; 的情形还有：[跳转](#fh)

- **对象解构**

  对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法

  写法：要求**结构的变量名必须和对象的属性名保持一致**

  ```javascript
  // const obj = {
  //     uname: 'mario',
  //     age: 22
  // }
  const {uname, age} = {uname: 'mario', age: 22}
  // const uname = obj.uname
  console.log(uname)								// 'mario'
  console.log(age)								// 22
  ```

  但如果变量名前面用过，又不能修改对象属性名，可以这么改 **旧变量名: 新变量名**

  ```javascript
  const uname = 'luigi'							// uname 已经被用了
  const {uname: username, age} = {uname: 'mario', age: 22}
  console.log(username)
  console.log(age)
  ```

  同理，**数组对象**也可以解构

  ```javascript
  const goods = [
      {
          goodsName: '小米',
          price: 1999
  	}
  ]
  const [{goodsName, price}] = goods
  ```

- 对象内有对象时，解构别忘了指定子对象名

  ```javascript
  const pig = {
      name: '佩奇',
      family: {
      	mother: '猪母',
      	father: '猪爹',
      	bro: '乔治'
  	},
  	age: 6
  }
  // 别忘了 family:
  const {name, family: {mother, father, sister}, age} = pig
  ```

  【小案例 - 解构 JSON 对象】

  ```javascript
  // 1. 这是后台传递过来的数据
  const msg = {
      "code": 200,
      "msg": "获取新闻列表成功",
      "data": [
  		{
              "id": 1,
              "title": "5G商用自己，三大运用商收入下降",
              "count": 58
  		},
          {
              "id": 2,
              "title": "国际媒体头条速览",
              "count": 56
          },
          {
              "id": 3,
              "title": "乌克兰和俄罗斯持续冲突",
              "count": 1669
          },
    	]
  }
  
  // 需求1：将 msg 对象采用对象解构的方式 只选出 data
  const {data} = msg
  
  // 需求2：需要把 data 选出当做参数传递给 函数
  function render1( {data} ) {
      // 传参时顺便解构了 相当于 const {data} = msg，再传入 data，现在传入的是 msg 对象
      // 内部处理
      console.log(data)
  }
  render1(msg)
  
  // 需求3，为防止 msg 里面的 data 名字混淆，要求渲染函数里面的数据名改为 myData
  function render2( {data:myData} ) {
      // 内部处理
      console.log(myData)
  }
  render2(msg)
  ```

---

### forEach 与 filter 方法

- forEach( ) 用于调用数组的每个元素，并将元素传递给回调函数，使用场景为**遍历数组对象中每个元素**

  **没有返回值！**index 不需要可省略

  ```javascript
  const arr = ['red', 'blue', 'green']
  // 数组 forEach 方法 item:元素 index:索引
  arr.forEach(function (item, index) {
      console.log(item)						// red blue green
      console.log(index)						// 0 1 2
  })
  ```

- filter( ) 创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，使用场景为**筛选数组符合条件的元素**

  **返回筛选之后的新数组**

  ```javascript
  const arr = [10, 20, 30]
  const newArr = arr.filter(function(item, index) {
      return item >= 20					// 筛选值大于等于20的元素
  })
  console.log(newArr)						// [20, 30]
  ```

  技巧：以上代码可以这么写：（看不懂请去看箭头函数）

  ```javascript
  const arr = [10, 20, 30]
  const newArr = arr.filter(item => item >= 20)
  console.log(newArr)

**案例：**[综合案例 9 - 渲染筛选商品列表](#综合案例 9 - 渲染筛选商品列表)

---

### 构造函数

构造函数是一种特殊的函数，主要用来初始化对象，**快速创建多个类似的对象**

构造函数有两个**约定**：**命名以大写字母开头，只能由 new 操作符执行。**

**构造函数内部无需写 return，返回值即为新创建的对象**

- 创建对象的三种方式

1. 利用字面量创建对象

   ```javascript
   const obj = {
       name: 'mario'
   }
   ```

2. 利用 new Object 创建对象（了解即可）

   ```javascript
   // const obj = new Object()
   // obj.name = 'mario'
   const obj = new Object({name: 'mario'})
   ```

3. 利用**构造函数**创建对象

   ```javascript
   // 创建一个构造函数
   function Pig(name, age) {
       this.name = name
       this.age = age
   }
   // 调用
   const pig1 = new Pig('佩奇', 6)
   const pig2 = new Pig('乔治', 3)
   ```

   实例化执行过程：new 的时候会创建空对象，构造函数中的 this 指向新对象，再指向构造函数中的代码，返回新对象。

- 实例成员与静态成员

  构造函数创建的对象为实例对象，实例对象中的属性和方法称为**实例成员**（实例属性和实例方法），实例对象彼此独立不受影响。

  构造函数的属性和方法成为**静态成员**（静态属性和静态方法），静态成员只能构造函数来访问，且静态方法中的 this 指向构造函数。比如 Date.now()、Math.PI、Math.random()

---

## 内置构造函数常见方法

基本类型：比如字符串、数值、布尔等基本类型有专门的构造函数，有 JS 底层自动完成，所以可以调用 str.length 这种功能，

因为在声明字符串 const str = 'mario' 时，底层执行了：const str = new String('mario')

### Object 类

- 虽然不太推荐使用 new Object 声明对象，但 Object 提供了很多有用的静态方法

   **Object.keys( )** 用来返回对象的所有键，返回值为数组

   **Object.values( )** 用来返回对象的所有值，返回值为数组

   Object.assign( ) 用来拷贝对象，原对象放在后面，使用场景为给对象添加属性（多个属性作为对象添加）

   这样就不用 for in 遍历那么麻烦了

   ```javascript
   const obj = {name: '佩奇', age: 6}
   console.log(Object.keys(obj)) 			// [name, age] 决不能用 o.keys！
   console.log(Object.values(obj)) 		// ['佩奇', 6] 决不能用 o.keys！
   const oo = {gender: '女'}
   Object.assign(oo, obj)
   console.log(oo)							// {gender: '女', name: '佩奇', age: 6}
   ```

---

### Array 类

Array：虽然不推荐这么创建数组，但还是要学的，

1. 以下都是常见数组方法。

   forEach( )：遍历数组，不返回数组

   【实例方法】

   filter( )：过滤数组，返回新数组（满足某种条件的） [跳转](#forEach 与 filter 方法)  【🐕🐶🐕🐕.filter(🐶) => 🐶】

   map( )：迭代数组，返回新数组（处理之后的）[跳转](#map 与 join 方法)  【🐕🐕🐕🐕.map(🐕=>🐶) => 🐶🐶🐶🐶】

   **reduce**( )<a id='arr'>：</a>累计器，包含一个回调函数和一个可选初始值，常用于求和，**如果数组是对象数组，初始值记得设为 0**

   ```javascript
   // arr.reduce(function(上一次值, 当前值) {}, 起始值)
   const arr = [1, 5, 8]
   const total1 = arr.reduce(function(prev, current) {
       // 回调函数，把 prev 看做以前的 sum 即可
       // [第一次循环] 上一次值：1 当前值：5 返回值：6
       // [第二次循环] 上一次值：6 当前值：8 返回值：14
       return prev + current
   })
   console.log(total1)						// 14
   
   const total2 = arr.reduce(function(prev, current) {
       // [第一次循环] 上一次值：10 当前值：1 返回值：11
       // [第二次循环] 上一次值：11 当前值：5 返回值：16
       // [第三次循环] 上一次值：16 当前值：8 返回值：24    
       return prev + current
   }, 10)
   console.log(total2)						// 24
   
   // 箭头函数写法
   const arr = [1, 5, 8]
   const total = arr.reduce((prev, current) => prev + current, 10)
   console.log(total)						// 24
   ```

2. 数组还有一些其他实例方法，了解即可。

   |    方法名    |              功能              |              返回值               |                图示                 |
   | :----------: | :----------------------------: | :-------------------------------: | :---------------------------------: |
   |   join( )    |        数组转化为字符串        |              字符串               |        🐕🐶.join('/') => '🐕/🐶'        |
   | **find( )**  | 查找第一个符合条件的数组元素值 |        元素值或 undefined         |          🐕🐶🐕🐕.find(🐶) => 🐶          |
   |   every( )   |  检测数组所有元素是否符合条件  |           true 或 false           |       🐕🐕🐶🐕.every(🐕) => false        |
   |   some( )    |   检测数组中元素是否符合条件   | 有满足的返回 true，否则返回 false |        🐕🐶🐶🐕.some(🐶) => true         |
   |  concat( )   |          合并两个数组          |              新数组               |                 --                  |
   |   sort( )    |       对原数组单元值排序       |                --                 |                 --                  |
   |  splice( )   |      删除或替换原数组单元      |                --                 |                 --                  |
   |  reverse( )  |            反转数组            |                --                 |                 --                  |
   | findIndex( ) |         查找元素索引值         |                --                 | 🐕🐶🐕🐕.findIndex(el => el === 🐶) => 2 |

   其中对于 find( )，这个方法非常有用，可以再众多对象中找到需要的对象

   ```javascript
   // 需求：提取内容40cm*40cm/黑色
   const spec = {size: '40cm*40cm', color: '黑色'}
   Object.values(spec).join('/')
   
   const arr1 = [
       {
           name: '小米',
           price: '1999'
       }
       {
           name: '华为',
           price: '2999'
       }
       // 找到小米这个对象
       const mi = arr1.find(item => item.name === '小米')
   ]
   const arr2 = [10, 20, 30]
   const flag = arr2.every(item => item >= 10)				// flag = true
   ```

3. **伪数组转化为真数组**

   Array.form( )

   ```html
   <body>
    	<ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
       </ul>
       <script>
           const lis = document.querySelector('ul li')
           // lis.pop()               // 报错，因为伪数组不存在此方法
           const liss = Array.from(lis)
           liss.pop()
       </script>
   </body>
   ```

   【小案例 - 月结薪资计算】

   ```javascript
   const arr = [{
       name: '张三',
       salary: 5000
   }, {
       name: '李四',
       salary: 10000
   }, {
       name: '王五',
       salary: 8000
   }
   ]
   // reduce 不写初始值会以数组第一个元素作为初始值
   // 但此时第一个元素是对象，所以初始值一定要设为 0
   const total = arr.reduce((prev, current) => prev + current.salary, 0)
   ```

---

### String 类

以下是 String 类常见实例属性和方法

[, 参数] 表示该参数为可选参数

- 实例属性 length 用来获取字符串串长

- toString( )：转化为字符串

  ```javascript
  const num = 10
  console.log(num.toString())			// '10'
  console.log(String(num))			// '10'
  ```

- **split**('分隔符')：**将字符串转化为成数组**

  ```javascript
  const str1 = 'mario, luigi'
  const arr1 = str1.split(',')
  console.log(arr1)					// [mario, luigi]
  const str2 = '2023-6-30'
  const arr2 = str2.split('-')
  console.log(arr2)                   // [2023, 6, 30]
  ```

- substring( 开始的索引号 [, 结束的索引号] )：**截取字符串（左闭右开）**，返回新字符串。

  ```javascript
  const str = '出门小点心哦'
  console.log(str.substring(3, 5))	// 点心
  ```

- startsWith( 检测字符串 [, 检测位置索引号] )：检测是否以某字符开头，返回 boolean

  ```javascript
  const str = 'To be, or not to be, that is a question'
  console.log(str.startsWith('To be'))				// true
  console.log(str.startsWith('not to be'))			// false
  console.log(str.startsWith('not to be', 10))		// true
  ```

  同理还有个判断是否已某字符结尾的：endsWith( )

- includes( 检测字符串 [, 检测位置索引号] )：检测是否包含子串，返回 boolean

  ```javascript
  const str = 'To be, or not to be, that is a question'
  console.log(str.includes('To be'))					// true
  ```

  【小案例 - 规格文字处理】

  ```html
  <div></div>
  <script>
      // 将以下字符串分开添加进 span 标签，且带上【赠品】两字
      const gift = '50g茶叶,清洗球'
      // 转化为数组。在遍历转换，再把数组转化为字符串，再替换文本
      document.querySelector('div').innerHTML =  = gift.split(',').map(item => `<span>【赠品】 ${item}</span> <br>`).join('')
  </script>
  ```

---

### Number 类

- Number( ) 直接使用转化为数字

- toFixed( ) 设置保留小数位的长度，会四舍五入

  ```javascript
  const num = 12.933
  console.log(num.toFixed())				// 13
  console.log(num.toFixed(2))				// 12.93
  ```

**案例：**[综合案例 9 - 渲染筛选商品列表 - 效果2](#g)

---

## 原型

两种编程思想：

- 面向过程

  面向过程是分析出解决问题所需的步骤，然后用函数把这些步骤一一实现，使用时再一一调用。

- 面向对象

  面向对象是把事务分解成一个个对象，然后由对象之间分工与合作。具有灵活，代码可复用，容易维护和开发的优点，更适合多人合作的大型软件项目。

  面向对象三特性：封装 + 继承 + 多态

  JS 通过**构造函数**实现封装，但前面提到的构造函数存在内存浪费问题，因为构造函数创造的对象相互独立，如果构造函数中有方法，两个对象虽然方法一样，但在堆内存里开辟了两份内存的空间。

  所以为了让不同对象共用相同方法，使用**原型**

原型核心：

![](./\图片\构造函数关系.png)

---

### 原型对象 prototype

构造函数通过原型分配的函数是所有对象所**共享的**

- JS 规定，每一个构造函数都有一个 **prototype 属性，指向另一个对象**，也称为**原型对象**

  **原型对象可以挂载函数**，这样对象实例化就不会多次创建函数，节约内存了

  可以把不变的方法直接定义在 prototype 对象上，这样所有对象的实例都可以共享此方法

  ```javascript
  function Player(uname, age) {
      // 公共属性写在构造函数内
      this.uname = uname
      this.age = age
      // this.jump = function() {
      //     console.log('跳跃')
      // }
  }
  // 公共方法写在原型对象内
  Player.prototype.jump = function() {
      console.log('跳跃')
  }
  const mario = new Player('mario', 40)
  const luigi = new Player('luigi', 38)
  mario.jump()
  luigi.jump()
  ```

  上面的写在原型里的公共方法内，如果有 this，那么 **this 也指向实例对象**。（谁调用指向谁，mario.jump，所以指向实例对象）

- 原型对象 prototype 内有一个 **constructor 属性**

  该属性**指向该原型对象的构造函数**。

  即 构造函数.prototype 指向原型对象
  
  ​	 原型对象.constructor 指向构造函数
  
  ```javascript
  function Player() {
  }
  console.log(Player.prototype.constructor === Player)		// true
  ```
  
  使用场景为：如果有多个对象的方法，可以给原型对象采取对象形式赋值
  
  ```javascript
  function Player(uname, age) {
      this.uname = uname
      this.age = age
  }
  // 公共方法写在原型对象内
  Player.prototype = {
      jump: function() {
          console.log('跳跃')
      },
      take: function() {
          console.log('拿')
      }
  }
  console.log(Player.prototype.constructor)			// 指向 Object
  ```
  
  但这样会覆盖掉构造函数原型对象原来的内容，这样 constructor 就不再指向当前构造函数了，也不知道谁创造了原型对象，可以**在修改后的原型对象中，添加一个 constructor 指向原来的构造函数**
  
  ```javascript
  function Player(uname, age) {
      this.uname = uname
      this.age = age
  }
  // 公共方法写在原型对象内
  Player.prototype = {
      // 因为这里是赋值，而不是追加
      // 记得重新指回创造这个原型对象的构造函数
      constructor: Player,
      jump: function() {
          console.log('跳跃')
      },
      take: function() {
          console.log('拿')
      }
  }
  console.log(Player.prototype.constructor)			// 指向 Player
  ```
  
  【小案例 - 封装数组求最大值与求和方法】
  
  ```javascript
  // 自己定义数组的扩展方法，求和和最大值
  Array.prototype.max = function() {
      // 展开运算符
      return Math.max(...this)    		// this 指向实例对象
  }
  console.log([1, 2, 3].max())			// 3
  console.log([2, 5, 9].max())			// 9
  Array.prototype.sum = function() {
  	return this.reduce((prev, item) => prev + item, 0)
  }
  console.log([2, 5, 9].sum())			// 16
  ```
  

---

### 对象原型 \_\_proto\_\_

实例化对象都有一个属性：**\_\_proto\_\_** 指向构造函数的 prototype 原型对象，因此可以访问原型中的方法。

- 注意：\_\_proto\_\_ 是JS非标准属性，在一些浏览器里显示为 [[peototype]]，该属性**只读**，用来表明实例对象指向哪个原型对象 prototype，\_\_proto\_\_ 里也有一个 constructor 属性，指向该实例对象的构造函数。

  ```javascript
  function Hero() {}
  const caocao = new Hero()
  console.log(caocao.__proto__ === Hero.prototype)	// true
  ```

  对象原型里有 constructor 指向构造函数。不理解的话去看图。

---

### 原型继承

js 中大多借助原型对象实现继承。简称**原型继承**。

- 之前说公共的方法放到原型内，公共的属性也可以放到原型内，再继承。

  **使用 prototype 继承原型，且继承后要用 constructor 指回构造函数本身**

  ```javascript
  function Person() {
      this.eyes = 2
      this.head = 1
  }
  function Woman() {}
  // 继承
  Woman.prototype = new Person()   // {eyes: 2, head: 1} 
  // 指回原来的构造函数
  Woman.prototype.constructor = Woman
  
  // 给女人添加一个方法
  Woman.prototype.baby = function () {
      console.log('生孩子')
  }
  const rose = new Woman()
  rose.baby()                     // 生孩子
  
  function Man() {}
  Man.prototype = new Person()
  Man.prototype.constructor = Man
  const david = new Man()
  console.log(david.eyes)         // 2
  ```

---

### 原型链 instanceof

- 原型链的定义：

  **原型链**其实就**是一个查找规则**，弱当前构造没有此方法，就去上一层即自身的原型对象内去找，若还没有，继续上一层，直到找到 Object 的原型对象的上一层 null 为止。这个线路即原型链。

- 原型链的宗旨是：

  只要是对象，就有原型，即 \_\_proto\_\_，指向原型对象

  而原型对象的 \_\_proto\_\_ 指向 Object 构造函数的原型对象，即 Object.prototype

  Object 的原型对象即 Object.prototype，它的 \_\_proto\_\_ 为 null

- 可使用 **instanceof 运算符** 用于检测实例对象 / 构造函数的 prototype 属性是否出现在某个实例对象的原型链上（即它属不属于另外一个构造函数）

  ```javascript
  function Player() {}
  const mario = new Player()
  console.log(mario instanceof Player)        // true
  console.log(mario instanceof Object)        // true
  console.log(mario instanceof Array)         // false
  ```

  【小案例 - **模态框封装**】

  点击删除按钮，弹框”你没有权限删除“，点击登录按钮，弹框“你还没有注册账号”，使用构造函数封装。

  ```html
  <head>
      <style>
  		/* css 略 */
      </style>
  </head>
  <body>
      <button id="delete">删除</button>
      <button id="login">登录</button>
      <script>
          function Model(title = '', message = '') {
              // 创建模态框盒子
              this.modelBox = document.createElement('div')
              this.modelBox.className = 'model'
              this.modelBox.innerHTML = `
                  <div class="header">${title} <i>X</i></div>
                  <div class="body">${message}</div>
              `
          }
          // 给构造函数原型对象挂载 open 方法
          Model.prototype.open = function() {
              // 先判断页面中是否有 Model 盒子，若有先移除
              const box = document.querySelector('.model')
              // 前面为真后面不执行 逻辑与中断
              box && box.remove()
              // 注意这个方法不用箭头函数，因为要用 this
              // 把刚才创建好的 modelBox 显示到 body 中
              // this 指向实例对象，绝对不能忘
              document.body.append(this.modelBox)
              // 等盒子显示出来就绑定点击事件
              this.modelBox.querySelector('i').addEventListener('click', () => {
                  // 箭头函数没有 this，指向上一层的 this，即 Model 构造函数的 this，即实例对象
                  this.close()
              })
          }
          Model.prototype.close = function() {
              this.modelBox.remove()
          }
          document.querySelector('#delete').addEventListener('click', () => {
              // 点击调用 Model 构造函数
              const del = new Model('温馨提示', '您没有权限删除操作')
              del.open()
          })
          document.querySelector('#login').addEventListener('click', () => {
              // 点击调用 Model 构造函数
              const login = new Model('友情提示', '您还没有登录')
              login.open()
          })
      </script>
  </body>
  ```

---

## 高阶技巧

### 拷贝

开发中经常需要**复制对象**，直接用 = 复制后得到新对象，对新对象操作会影响旧对象，因为是一个地址。

1. 浅拷贝

   **浅拷贝拷贝的是地址**

   拷贝对象用：Object.assgin( )	/	展开运算符 { ...obj }

   拷贝数组用：Array.prototype.concat( )	/	[ ...arr ]

   但一旦对象里有对象嵌套，就会出现问题，对里面的值修改会影响旧对象，也就是说，**浅拷贝只能适用于对象的最外层**。

   ```javascript
   const obj = {
       uname: 'mario',
       age: 55
   }
   // 浅拷贝 1
   const o = {...obj}
   o.age = 20
   console.log(o)      // {uname: 'mario', age: 20}
   console.log(obj)    // {uname: 'mario', age: 55}
   // 浅拷贝 2
   const ob = {}
   Object.assign(ob, obj)
   console.log(ob)     // {uname: 'mario', age: 55}
   ```

2. 深拷贝

- 方法一：递归

  用函数递归实现深拷贝的话，普通拷贝正常赋值，遇到数组递归调用，遇到对象递归调用，且先处理数组再处理对象。

  ```javascript
  const obj = {
              uname: 'mario',
              age: 55,
              power: ['jump', 'take', 'fire'],
              family: {
                  brother: 'luigi'
              }
          }
  const o = {}
  // 深拷贝函数
  function deepCopy(newObj, oldObj) {
      for (let k in oldObj) {
       	// Array 也属于 Object 所以要先写在前面  
          if (oldObj[k] instanceof Array) {
              // 处理数组情形
              newObj[k] = []
              deepCopy(newObj[k], oldObj[k])
          } else if (oldObj[k] instanceof Object) {
              // 处理对象情形
              newObj[k] = {}
              deepCopy(newObj[k], oldObj[k])
          } else {
              // k 是属性名 oldObj[k] 是属性值
              // newObj[k] 是属性名，是为newObj添加属性！
              newObj[k] = oldObj[k]
          }
      }
  }
  // 调用
  deepCopy(o, obj)
  o.power[2] = 'bigger'
  o.family.brother = 'bowser'
  // {uname: 'mario', age: 55, ['jump', 'take', 'bigger'], family: {'bowser'}}
  console.log(o)
  // {uname: 'mario', age: 55, ['jump', 'take', 'fire'], family: {'luigi'}}
  console.log(obj)
  ```

- 方法二：Lodash / cloneDeep

  浏览器环境引入 Lodash 库

  ```html
  <script src="lodash.js"></script>
  ```

  通过 npm 引入 Lodash 库以后再说

  使用 lodash 库实现深拷贝：

  ```html
  <script src="./lodash.min.js"></script>
  <script>
      const obj = {
          uname: 'mario',
          age: 55,
          power: ['jump', 'take', 'fire'],
          family: {
              brother: 'luigi'
          }
      }
      // 深拷贝 Lodash 函数的特点是前面有个_. 目的是避免函数重名
      const o = _.cloneDeep(obj)
      console.log(o)
  </script>
  ```

- 方法三：通过 JSON.stringify( ) 实现

  把对象转化为 JSON 字符串，再转化为对象，新对象和旧对象没有任何关系了

  ```javascript
  const obj = {
      uname: 'mario',
      age: 55,
      power: ['jump', 'take', 'fire'],
      family: {
          brother: 'luigi'
      }
  }
  // 深拷贝 Lodash 函数的特点是前面有个_. 目的是避免函数重名
  const o = _.cloneDeep(obj)
  console.log(o)
  ```

---

### 异常处理

异常处理是指预估代码执行过程中可能存在的错误，然后最大限度避免错误发生影响整个程序无法运行。

1. throw 抛异常

   throw 后会抛出异常信息，程序也会中止运行，可配合 Error 对象使用

   ```javascript
   function fn(x, y) {
       if (!x || !y) {
           throw new Error('用户无传参')
       }
       return x + y
   }
   console.log(fn())
   ```

2. try / catch / finally 捕获错误信息

   **try** 用来包住**可能会出错的代码**，然后**用 catch 捕获错误**，不加 return 不会中断程序后面的运行，**finally 用来包住一定会执行的代码**

   ```html
   <p>123</p>
   <script>
       function fn() {
           try {
               // 可能发生错误的代码写在 try 里
               const p = document.querySelector('.p')
               p.style.color = 'red'
           } catch(err) {
               // 拦截错误，提示浏览器提供的错误信息，不中断程序的执行
               console.log(err.message)       // Cannot read properties of null (reading 'style')
               // 除非加 return 才中断
               return
           }
           finally {
               // 不管程序对不对一定会执行的代码
               alert('弹出对话框')
           }
       }
       fn()
   </script>
   ```

3. debugger

   ```javascript
   // 插入在代码中间
   debugger
   ```

   用来断点调试，会在 debugger 的位置自动断点。

---

### this 总结 bind()

1. this 指向总结

- 普通函数的 this：普通函数**谁调用指向谁**，严格模式下指向 undefined（严格模式不展开说）

  ```html
  <button>点击</button>
  <script>
      document.querySelector('button').addEventListener('click', function() {
          console.log(this)       // <button>点击</button>
      })
      const obj = {
          sayHi: function() {
              console.log(this)   // obj
          }
      }
      obj.sayHi()
  </script>
  ```

- 箭头函数：箭头函数不找自己，而是去找外面（**最近的作用域**）的 this 值

  所以箭头函数尽量别用 this，原型对象的函数不推荐使用箭头函数。[跳转](#thi)

2. 改变 this 指向

- 方法一：call( ) ：了解即可，使用 call 方法调用函数，同时指定被调用函数的 this 值，改变的 this 值写在传参最前面。

  ```javascript
  const obj = {
      uname: 'egg'
  }
  function fn(x, y) {
      x + y
      console.log(this)       // 正常调用指向 window
  }
  // 调用函数并改变 this 指向
  fn.call(obj, 1, 2)          // obj
  ```

- 方法二：apply( )：和 call 非常像，调用函数，改变 this 指向，区别在于原本函数的**传参必须写成数组**

  ```javascript
  const obj = {
      uname: 'egg'
  }
  function fn(x, y) {
      console.log(x + y)
      console.log(this)					// 正常调用指向 window
  }
  // 调用函数并改变 this 指向
  fn.apply(obj, [1, 2])					// obj
  ```

  使用场景是求数组最大值，以前用[展开运算符](#zhan)做过，这是第二种方法

  ```javascript
  const max = Math.max.apply(null, [1, 2, 3])
  ```

- 方法三：**bind**( )：bind 不会调用函数，但可以改变 this 的指向

  ```javascript
  const obj = {
      age: 22
  }
  function fn() {
      console.log(this)
  }
  // 返回值是改变了 this 指向的函数
  const fun = fn.bind(obj)
  fun()                           // obj
  ```

  使用场景比如：一个按钮，点击后禁用，两秒后开启。

  ```html
  <body>
      <button>点击</button>
      <script>
      	const btn = document.querySelector('button')
          btn.addEventListener('click', function() {
              this.disabled = true
              setTimeout(function() {
                  // this.disabled = false 本句无效，因为 this 指向 window
                  // 改变 this 指向
                  this.disabled = false
              }.bind(this), 2000)
              // bind() 里的 this 指向事件监听里那个 this，即 btn
          })
      </script>
  </body>
  ```

---

### 防抖和节流

1. 防抖 debounce

   单位时间内，频繁触发事件，只触发最后一次。防抖 = 回城，没加载完打断取消回城重新蓄力。

   使用场景为输入检测，只需用户最后一次输入完再发送请求。

   可以使用 Lodash 库来做防抖处理

   ```html
   <body>
       <div class="box"></div>
       <script src="./js/lodash.min.js"></script>
       <script>
           const box = document.querySelector('.box')
           let i = 1
           function mouseMove() {
               box.innerHTML = i++
           }
           // 利用 Lodash 库实现防抖，之前计数太快了，改为 500 ms 计数再加一
           box.addEventListener('mousemove', _.debounce(mouseMove, 500))
       </script>
   </body>
   ```

   或者使用 setTimeout 来实现

   思路为：先声明一个定时器变量，当鼠标滑动（事件触发）先判断是否有定时器了，**有就清除以前的定时器，没有就开一个定时器**，记得存在变量内。

   ```javascript
   const box = document.querySelector('.box')
   let i = 1
   function mouseMove() {
       box.innerHTML = i++
   }
   function debounce(fn, t) {
       let timer
       // return 返回一个匿名函数
       return function() {
           if (timer) clearTimeout(timer)
           timer = setTimeout(function() {
               fn()
           }, t)
       }
   }
   box.addEventListener('mousemove', debounce(mouseMove, 500))
   ```

2. 节流 throttle

   单位时间内，频繁触发事件，只执行一次。节流 = 技能，冷却时间内无法释放技能。

   使用场景为：高频事件，如鼠标移动，页面尺寸缩放，滚动条滚动等。

   可以使用 Lodash 库来做节流处理

   ```html
   <body>
       <div class="box"></div>
       <script src="./js/lodash.min.js"></script>
       <script>
           const box = document.querySelector('.box')
           let i = 1
           function mouseMove() {
               box.innerHTML = i++
           }
           // 利用 Lodash 库实现节流，改为 500 ms 计数再加一
           box.addEventListener('mousemove', _.throttle(mouseMove, 500))
       </script>
   </body>
   ```

   或者使用 setTimeout 来实现

   思路为：先声明一个定时器变量，当鼠标滑动（事件触发）先判断是否有定时器了，如果**有定时器则不开启新定时器，如果没有定时器则开启定时器，**记得存在变量内。

   ```javascript
   const box = document.querySelector('.box')
   let i = 1
   function mouseMove() {
       box.innerHTML = i++
   }
   function throttle(fn, t) {
       let timer = null
       return function() {
           if (!timer) {
               timer = setTimeout(function() {
               	fn()
                   // 清空定时器 - 无法在 setTimeout 内使用 clearTimeout()
                   timer = null
           	}, t)
           }
       }
   }
   box.addEventListener('mousemove', throttle(mouseMove, 500))
   ```

**案例：**[综合案例 10 - 记录播放视频时间](#综合案例 10 - 记录播放视频时间)


---

# 综合案例

## 综合案例 1 - 表格

效果：

![](./\图片\综合案例2.png)

在 HTML+CSS 篇里，数据写死了，这里数据改为用户输入框输入。只展示 js 部分。

```html
<script>
    // 用户输入
    let price = +prompt('请输入商品价格')
    let num = +prompt('请输入商品数量')
    let address = prompt('请输入收货地址')
    // 计算
    let total = price * num
    // 页面渲染
    document.write(`
        <table>
            <!-- tr>th*5 -->
            <tr>
                <th>商品名称</th>
                <th>商品价格</th>
                <th>商品数量</th>
                <th>总价</th>
                <th>收货地址</th>
            </tr>
            <!-- tr>td*5 -->
            <tr>
                <td>小米手机</td>
                <td>${price}</td>
                <td>${num}</td>
                <td>${total}</td>
                <td>${address}</td>
            </tr>
        </table>
    `)
</script>
```

这里的方法非常low比，学了vue以后再改。

---

## 综合案例 2 - 渲染柱形图

![](./\图片\综合案例7.png)

在HC篇，数据写死，这里改为输入数据

```html
<script>
	// 把数据放入数组，再遍历数组，柱形图就是div盒子，宽度固定，高度为用户输入的数据
    let arr = []
    for (let i = 0; i < 4; i++) {
        // 用户输入 4 次
        arr.push(prompt(`请输入第${i + 1}季度的数据:`))
    }
    // 盒子头
    document.write(`<div class="box">`)

    // 盒子内容 - 循环
    for (let i = 0; i < arr.length; i++) {
        document.write(`
            <div style="height: ${arr[i]}px;">
                <span>${arr[i]}</span>
                <h4>第${i + 1}季度</h4>
            </div>
        `)
    }

    // 盒子尾
    document.write(`</div>`)
</script>
```

## 综合案例 3 - 轮播图

效果1：刷新页面会随机换图片文字与底色

![](./\图片\轮播图.png)

代码实现：

```html
<head>
    <style>
    	/* css 部分过长，略 */
        /* 这个 active 是下面的小按钮类效果 */
        .slider-indicator li.active {
        	width: 12px;
        	height: 12px;
        	opacity: 1;
        }
    </style>
</head>
<body>
	<div class="slider">
    	<div class="slider-wrapper">
      		<img src="./images/slider01.jpg" alt="" />
    	</div>
    	<div class="slider-footer">
      		<p>对人类来说会不会太超前了？</p>
            <ul class="slider-indicator">
                <li class="active"></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
            </ul>
			<div class="toggle">
        		<button class="prev">&lt;</button>
        		<button class="next">&gt;</button>
      		</div>
    	</div>
	</div>
	<script>
        // 初始数据
        const sliderData = [
            { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
            { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
            { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
            { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
            { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
            { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
            { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
            { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
        ]
        // 得到随机数
        const random = parseInt(Math.random() * sliderData.length)
        // 获取图片
        const img = document.querySelector('.slider-wrapper img')
        // 修改图片路径
        img.src = sliderData[random].url
        // 获取 p
        const p = document.querySelector('.slider-footer p')
        // 修改 p
        p.innerHTML = sliderData[random].title
        // 修改背景色
        const footer = document.querySelector('.slider-footer')
        footer.style.backgroundColor = sliderData[random].color
        // 小圆点: 选中 li
        const li = document.querySelector(`.slider-indicator li:nth-child(${random + 1})`)
        // 让当前 li 添加 active 类名
        li.classList.add('active')
	</script>
</body>
```

效果2：在效果1的基础上，每隔两秒换一个图片

```html
<script>
    // 初始数据
    const sliderData = [
        { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
        { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
        { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
        { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
        { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
        { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
        { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
        { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
    ]
    // 获取图片
    const img = document.querySelector('.slider-wrapper img')
    // 获取 p
    const p = document.querySelector('.slider-footer p')
    // 设定定时器
    let i = 0
    let n = setInterval(function(){
        i++
        // 无缝滚动一定要写在这里
        if (i >= sliderData.length) {
        	i = 0
        }
        // 更换图片路径
        img.src = sliderData[i].url
        // 把 title 写到 p 内
        p.innerHTML = sliderData[i].title
        // 获取以前的小圆点 li 并把它移除
        document.querySelector('.slider-indicator .active').classList.remove('active')
        // 获取当前小圆点 li 并添加类名
        document.querySelector(`.slider-indicator li:nth-child(${i + 1})`).classList.add('active')
    }, 2000)
</script>
```

效果3：最终版，和网页上一样，按钮下一张，放小圆点上跳转

代码实现：

```html
<script>
    // 初始数据
    const sliderData = [
        { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
        { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
        { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
        { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
        { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
        { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
        { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
        { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
    ]
    const img = document.querySelector('.slider-wrapper img')
    const p = document.querySelector('.slider-footer p')
    const footer = document.querySelector('.slider-footer')

    // 信号量，控制图片张数
    let i = 0

    // 右按钮
    const next = document.querySelector('.next')
    next.addEventListener('click', function() {
        i++
        i = i >= sliderData.length ? 0 : i
        toggle()
    })

    // 左按钮
    const prev = document.querySelector('.prev')
    prev.addEventListener('click', function() {
        i--
        // 位于第一个再次点击应跳转到最后一个，索引号即length - 1
        i = i < 0 ? sliderData.length - 1 : i
        toggle()
    })

    // 自动播放
    let timerId = setInterval(function() {
        // 要加小括号，相当于调用函数
        next.click()
    }, 1000)

    // 鼠标经过停止定时器
    // 事件源 大盒子
    const slider = document.querySelector('.slider')
    // 注册事件
    slider.addEventListener('mouseenter', function() {
		// 停止计时器
		clearInterval(timerId)
    })

    // 鼠标离开开启定时器
    slider.addEventListener('mouseleave', function() {
        // 停止计时器 - 先关再开好习惯
        clearInterval(timerId)
        // 开启计时器
        timerId = setInterval(function() {
        	// 要加小括号，相当于调用函数
        	next.click()
		}, 1000)
	})

    function toggle() {
      // 渲染对应数据
      img.src = sliderData[i].url
      p.innerHTML = sliderData[i].title
      footer.style.backgroundColor = sliderData[i].color
      // 选中小圆点 删除类 再添加类
      document.querySelector('.slider-indicator .active').classList.remove('active')
      document.querySelector(`.slider-indicator li:nth-child(${i+1})`).classList.add('active')
    }
</script>
```

---

## 综合案例 4 - Tab 栏切换

效果：

![](./图片\Tab栏切换.png)

代码实现：鼠标经过标签自动切换。

```html
<body>
    <div class="tab">
    	<div class="tab-nav">
            <h3>每日特价</h3>
            <ul>
                <li><a class="active" href="javascript:;">精选</a></li>
                <li><a href="javascript:;">美食</a></li>
                <li><a href="javascript:;">百货</a></li>
                <li><a href="javascript:;">个护</a></li>
                <li><a href="javascript:;">预告</a></li>
            </ul>
    	</div>
        <div class="tab-content">
            <div class="item active"><img src="./images/tab00.png" alt="" /></div>
            <div class="item"><img src="./images/tab01.png" alt="" /></div>
            <div class="item"><img src="./images/tab02.png" alt="" /></div>
            <div class="item"><img src="./images/tab03.png" alt="" /></div>
            <div class="item"><img src="./images/tab04.png" alt="" /></div>
    	</div>
    </div>
    <script>
        // 给5个链接绑定鼠标经过事件
        const as = document.querySelectorAll('.tab-nav a')
        for (let i = 0; i < as.length; i++) {
        	as[i].addEventListener('mouseenter', function() {
                // 添加高亮效果 先移除 后添加
                document.querySelector('.tab-nav .active').classList.remove('active')
                this.classList.add('active')
                // 下面的大盒子 先移除
                document.querySelector('.tab-content .active').classList.remove('active')
                // 再添加 这里不能用 this，因为鼠标经过的是上面
                document.querySelector(`.tab-content .item:nth-child(${i+1})`).classList.add('active')
        	})
        }
    </script>
</body>
```

优化代码：使用事件委托对代码优化，不在给 li 注册事件，而给父级 ul 注册，效果变为点击。

```html
<body>
	<div class="tab">
		<div class="tab-nav">
			<h3>每日特价</h3>
            <ul>
                <li><a class="active" href="javascript:;" data-id="0">精选</a></li>
                <li><a href="javascript:;" data-id="1">美食</a></li>
                <li><a href="javascript:;" data-id="2">百货</a></li>
                <li><a href="javascript:;" data-id="3">个护</a></li>
                <li><a href="javascript:;" data-id="4">预告</a></li>
            </ul>
		</div>
		<div class="tab-content">
            <div class="item active"><img src="./images/tab00.png" alt="" /></div>
            <div class="item"><img src="./images/tab01.png" alt="" /></div>
            <div class="item"><img src="./images/tab02.png" alt="" /></div>
            <div class="item"><img src="./images/tab03.png" alt="" /></div>
            <div class="item"><img src="./images/tab04.png" alt="" /></div>
		</div>
	</div>
	<script>
        const ul = document.querySelector('.tab-nav ul')
        ul.addEventListener('click', function(e) {
			if (e.target.tagName === 'A') {
                document.querySelector('.tab-nav .active').classList.remove('active')
                // this 指向 ul ，不能用 this
                e.target.classList.add('active')
                // 没有索引i，使用自定义属性 取来的是字符串，要转化
                const id = +e.target.dataset.id
                document.querySelector('.tab-content .active').classList.remove('active')
                document.querySelector(`.tab-content .item:nth-child(${id + 1})`).classList.add('active')
            }
        })
    </script>
</body>
```

---

## 综合案例 5 - 电梯导航

效果：

![](./\图片\电梯导航.png)

模块分析：

1. 页面滚动到对应位置，导航显示，否则隐藏模块（在其他事件 2【小案例 - 电梯导航】实现）
2. 点击导航栏对应的小模块，跳转到对应大模块位置
3. 页面滚动到对应位置，电梯导航对应模块自动发生变化

代码实现：

```html
<head>
    <style>
    	/* 让页面滑动效果变丝滑 */
        html {
          scroll-behavior: smooth;
        }
    </style>
</head>
<body>
	<!-- 分类及焦点图 -->
	<div class="xtx_entry">...</div>
    <!-- 新鲜好物 -->
	<div class="xtx_goods_new xtx_panel">...</div>
    <!-- 人气推荐 -->
	<div class="xtx_goods_popular xtx_panel">...</div>
    <!-- 热门品牌 -->
	<div class="xtx_goods_brand xtx_panel">...</div>
    <!-- 最新主题 -->
	<div class="xtx_goods_topic xtx_panel">...</div>
    <!-- 电梯 -->
    <div class="xtx-elevator">
        <ul class="xtx-elevator-list">
            <li><a href="javascript:;" data-name="new">新鲜好物</a></li>
            <li><a href="javascript:;" data-name="popular">人气推荐</a></li>
            <li><a href="javascript:;" data-name="brand">热门品牌</a></li>
            <li><a href="javascript:;" data-name="topic">最新专题</a></li>
            <li><a href="javascript:;" id="backTop"><i class="sprites"></i>顶部</a></li>
        </ul>
    </div>
    <script>
    	// 模块一 立即执行函数
        (function() {
            const elevator = document.querySelector('.xtx-elevator')
            const entry = document.querySelector('.xtx_entry')
            // 当页面滚动大于第一模块与页面顶部的距离，显示电梯导航
            window.addEventListener('scroll', function() {
                // n 是页面滑动的距离
                const n = document.documentElement.scrollTop
                elevator.style.opacity = n >= entry.offsetTop ? 1 : 0
            })
            const backTop = document.querySelector('#backTop')
            backTop.addEventListener('click', function() {
            	document.documentElement.scrollTop = 0
        	})
		})();
        // 模块二
        (function() {
        	const list = document.querySelector('.xtx-elevator-list')
            list.addEventListener('click', function(e) {
                // 点击的是电梯拦超链接 且 不是返回顶部(没有data-name)
                if (e.target.tagName === 'A' && e.target.dataset.name) {
                    // 第一次点击是没有 active 的，不能直接移除 active 类
                    // 先获取类名
                    const old = document.querySelector('.xtx-elevator-list .active')
                    // 如果本身有 active 就移除，没有就不操作
                	if (old) old.classList.remove('active')
                	e.target.classList.add('active')
                	// 获取点击目标的 data-name 值匹配到大盒子到页面顶部的距离
                	const top = document.querySelector(`.xtx_goods_${e.target.dataset.name}`).offsetTop
                	// 让页面滚动到固定位置
                	document.documentElement.scrollTop = top
            	}
        	})
		})();
        // 模块三
        (function() {
            window.addEventListener('scroll', function() {
                // 先移除已有的 active 类
                const old = document.querySelector('.xtx-elevator-list .active')
                if (old) old.classList.remove('active')
                // 获取全部4个大盒子
                const news = document.querySelector('.xtx_goods_new')
                const popular = document.querySelector('.xtx_goods_popular')
                const brand = document.querySelector('.xtx_goods_brand')
                const topic = document.querySelector('.xtx_goods_topic')
                // 获取页面滚动距离
                const n = document.documentElement.scrollTop
                if (n >= news.offsetTop && n < popular.offsetTop) {
                    // 属性选择器:根据 data-name 选择相应的小盒子
                    document.querySelector('[data-name=new]').classList.add('active')
                } else if (n >= popular.offsetTop && n < brand.offsetTop) {
                	document.querySelector('[data-name=popular]').classList.add('active')
                } else if (n >= brand.offsetTop && n < topic.offsetTop) {
                	document.querySelector('[data-name=brand]').classList.add('active')
                } else if (n >= topic.offsetTop) {
                	document.querySelector('[data-name=topic]').classList.add('active')
            	}
            })
        })()
    </script>
</body>
```

---

## 综合案例 6 - 学生信息表

效果1：

![](./\图片\学生信息表.png)

思路：声明空数组，点击录入生成对象，追加到数组内，根据数组渲染页面即表格的行，点击删除删除对应数组的数据，再次根据数组渲染页面。

代码实现：

```html
<body>
    <h1>新增员工</h1>
    <form class="info" autocomplete="off">
        姓名：<input type="text" class="uname" name="uname" />
        年龄：<input type="text" class="age" name="age" />
        性别:
        <select name="gender" class="gender">
            <option value="男">男</option>
            <option value="女">女</option>
        </select>
        薪资：<input type="text" class="salary" name="salary" />
        就业城市：<select name="city" class="city">
            <option value="北京">北京</option>
            <option value="上海">上海</option>
            <option value="广州">广州</option>
            <option value="深圳">深圳</option>
            <option value="曹县">曹县</option>
        </select>
        <button class="add">录入</button>
    </form>

    <h1>就业榜</h1>
    <table>
    	<thead>
            <tr>
                <th>学号</th>
                <th>姓名</th>
                <th>年龄</th>
                <th>性别</th>
                <th>薪资</th>
                <th>就业城市</th>
                <th>操作</th>
            </tr>
		</thead>
    	<tbody>
      		<!-- 
                <tr>
                    <td>1001</td>
                    <td>欧阳霸天</td>
                    <td>19</td>
                    <td>男</td>
                    <td>15000</td>
                    <td>上海</td>
                    <td>
						<a href="javascript:">删除</a>
					</td>
				</tr> 
            -->
    	</tbody>
    </table>
	<script>
        // 声明数组
        const arr = []
        // 获取对象的元素，用于拼接对象
        const uname = document.querySelector('.uname')
        const age = document.querySelector('.age')
        const gender = document.querySelector('.gender')
        const salary = document.querySelector('.salary')
        const city = document.querySelector('.city')
        const tbody = document.querySelector('tbody')

        // 1.点击录入模块
        // 表单提交事件
        const info = document.querySelector('.info')
        info.addEventListener('submit', function(e) {
            // form 表单的默认行为是当用户点击提交后，页面自动跳转 
            e.preventDefault()  // 阻止默认行为
            // 表单非空验证 获取所有 name 属性的标签
            const items = document.querySelectorAll('[name]')
            for (let i = 0; i < items.length; i++) {
                if (items[i].value === '') {
                    return alert('输入内容不能为空')
                }
            }
            // 创建新对象
            const obj = {
                stuId: arr.length + 1,
                // 用 value 取值
                uname: uname.value,
                age: age.value,
                gender: gender.value,
                salary: salary.value,
                city: city.value
            }
            // 把对象加入数组
            arr.push(obj)
            // 提交后清空表单的输入区(重置)
            this.reset()
            // 调用渲染函数
            render()
        })

        // 2.渲染函数模块
        function render() {
            // 先清空 tbody，否则数据会重复
            tbody.innerHTML = ''
            for (let i = 0; i < arr.length; i++) {
                // 生成 tr
                const tr = document.createElement('tr')
                tr.innerHTML = `
                    <td>${arr[i].stuId}</td>
                    <td>${arr[i].uname}</td>
                    <td>${arr[i].age}</td>
                    <td>${arr[i].gender}</td>
                    <td>${arr[i].salary}</td>
                    <td>${arr[i].city}</td>
                    <td>
                    <a href="javascript:" data-id=${i}>删除</a>
                    </td>
            	`
            	// 追加元素，父元素.appendChild(子元素)
            	tbody.appendChild(tr)
            }
        }

        // 3.删除模块
        // 事件委托给 tbody
        tbody.addEventListener('click', function(e) {
            if (e.target.tagName === 'A') {
                arr.splice(e.target.dataset.id, 1)
                render()
            }
        })
	</script>
</body>
```

效果2：录入数据后，刷新不丢失

思路：

1. 渲染模块：遍历数组，根据数据生成 tr，里面填充数据，最后追加给 tbody，渲染业务封装成 render 函数，使用 map 方法遍历数组，更换里面的数据，返回有数据的 tr 数组。通过 join 方法把 map 返回的数组转换为字符串。把字符串通过 innerHTML 赋值给 tbody。
2. 新增模块：给 form 注册提交事件，要**阻止默认提交事件**，非空判断 - 年龄、性别、薪资有一项为空，return 返回“输入不能为空”
3. 删除模块：采用事件委托给 tbody 注册点击事件，根据当前点击的索引号（索引号需要给 a 链接添加自定义属性）
4. 解决bug：当有删除操作存在，序号可能会重复，因为不能只用数组长度来作为序号，应该使用最后的 id 号+1

代码实现：

```javascript
// 模块 1
// 读取本地存储数据，有数据返回数组，没数据空数组
const arr = JSON.parse(localStorage.getItem('data')) || []
const tbody = document.querySelector('tbody')
render()
function render() {
    // 用 map 遍历数组，返回对应 tr 的数组
    const trArr = arr.map(function(ele, index) {
        return `
            <tr>
                <td>${ele.stuId}</td>
                <td>${ele.uname}</td>
                <td>${ele.age}</td>
                <td>${ele.gender}</td>
                <td>${ele.salary}</td>
                <td>${ele.city}</td>
                <td>
                    <a href="javascript:" data-id="${index}">删除</a>
                </td>
            </tr>
        `
    })
    // 数组 > 字符串才能追加给 tbody
    tbody.innerHTML = trArr.join('')
}

// 模块 2
const info = document.querySelector('.info')
const uname = document.querySelector('.uname')
const age = document.querySelector('.age')
const gender = document.querySelector('.gender')
const salary = document.querySelector('.salary')
const city = document.querySelector('.city')

info.addEventListener('submit', function(e) {
    // 阻止默认行为
    e.preventDefault()
    if (!uname.value || !age.value || !salary.value) {
        return alert('输入内容不能为空')
    }
    // 给 arr 数组追加对象
    arr.push({
        // 这里有 bug，id号可能重复，应该是最后一条id + 1
        stuId: arr.length ? arr[arr.length - 1].stuId + 1 : 1,
        uname: uname.value,
        age: age.value,
        gender: gender.value,
        salary: salary.value,
        city: city.value,
    })
    // 渲染 并 重置
    render()
    this.reset()
    // 转化成 JSON 字符串存入本地数据
    localStorage.setItem('data', JSON.stringify(arr))
})

// 模块 3
// 利用事件委托，给 tbody 注册点击事件
tbody.addEventListener('click', function(e) {
	if (e.target.tagName === 'A') {
        // 确认框 返回 boolean
        if (confirm('您确定删除此数据吗？')) {
            // 利用自定义属性，获得删除对应的索引号
            arr.splice(e.target.dataset.id, 1)
            render()
            localStorage.setItem('data', JSON.stringify(arr))
		}
	}
})
```

---

## 综合案例 7 - 用户注册页

效果：

![](./\图片\用户注册页.png)

实现：

```javascript
// 模块 1 - 验证码倒计时
const code = document.querySelector('.code')
// flag 避免倒计时期间反复重开
let flag = true
code.addEventListener('click', function() {
	if (flag) {
        flag = false
        let i = 5
        code.innerHTML = `0${i}秒后重新获取`
        let timeId = setInterval(function(){
			i--
			code.innerHTML = `0${i}秒后重新获取`
			if (i === 0) {
                clearInterval(timeId)
                flag = true
                code.innerHTML = '重新获取'
			}
		}, 1000)
	}
})

// 模块 2 - 验证用户名
const username = document.querySelector('[name=username]')
// 使用 change 事件 检测表单值发生变化
username.addEventListener('change', verifyName)
// 验证手机号
const phone = document.querySelector('[name=phone]')
phone.addEventListener('change', verifyPhoneName)
// 验证验证码
const codeInput = document.querySelector('[name=code]')
codeInput.addEventListener('change', verifyCode)
// 验证密码
const password = document.querySelector('[name=password]')
password.addEventListener('change', verifyPwd)
// 再次验证密码
const confirm = document.querySelector('[name=confirm]')
confirm.addEventListener('change', verifyConfirm)

function verifyName() {
    // 这里不能 qs-span 因为有好多个 span
    const span = username.nextElementSibling
    // 定义规则
    const reg = /^[a-zA-Z0-9-_]{6,10}$/
    if (!reg.test(username.value)) {
        span.innerHTML = '输入不合法，请输入6~10位'
        return false
	}
    span.innerHTML = ''
    return true
}

function verifyPhoneName() {
    const span = phone.nextElementSibling
    const reg = /^1(3\d|4[5-9]|5[0-35-9]|6[567]|7[0-8]|8\d|9[0-35-9])\d{8}$/
    if (!reg.test(phone.value)) {
        span.innerHTML = '请输入正确的手机号'
        return false
	}
    span.innerHTML = ''
    return true
}

function verifyCode() {
    const span = codeInput.nextElementSibling
    const reg = /^\d{6}$/
    if (!reg.test(codeInput.value)) {
        span.innerHTML = '输入不合法，请输入6位数字'
        return false
	}
    span.innerHTML = ''
    return true
}

function verifyPwd() {
    const span = password.nextElementSibling
    const reg = /^[a-zA-Z0-9-_]{6,20}$/
    if (!reg.test(password.value)) {
        span.innerHTML = '输入不合法，6-20位数字字母符号组成'
        return false
	}
    span.innerHTML = ''
    return true
}

function verifyConfirm() {
    const span = confirm.nextElementSibling
    const reg = /^[a-zA-Z0-9-_]{6,20}$/
    if (confirm.value !== password.value) {
        span.innerHTML = '两次密码输入不一致'
        return false
	}
    span.innerHTML = ''
    return true
}

// 模块 3 - 同意协议
// 添加 .icon-queren2 类是选中样式
const queren = document.querySelector('.icon-queren')
queren.addEventListener('click', function() {
	this.classList.toggle('icon-queren2')
})

// 模块 4 - 表单提交模块
const form = document.querySelector('form')
form.addEventListener('submit', function(e) {
    // 判断是否勾选了协议 - 有无 icon-queren2 类
    if (!queren.classList.contains('icon-queren2')) {
		alert('请勾选同意协议')
        // 这里不直接 return alert，否则还会提交表单，要使用事件对象阻止默认行为
        e.preventDefault()
	}
    // 依次判断文本框，只要有一个没通过就阻止
    if (!verifyName()) e.preventDefault()
    if (!verifyPhoneName()) e.preventDefault()
    if (!verifyCode()) e.preventDefault()
    if (!verifyPwd()) e.preventDefault()
    if (!verifyConfirm()) e.preventDefault()
})
```

---

## 综合案例 8 - 放大镜效果

P148待补

---

## 综合案例 9 - 渲染筛选商品列表

效果1：点击价格区间，即可切换符合的商品

![](./\图片\渲染筛选商品.png)

渲染模块思路：有多少条数据，就渲染多少模块，然后生成对应的 html 标签，赋值给 list 标签即可

1. 利用 forEach 遍历数组里面的数据
2. 拿到数据，利用字符串拼接生成结构添加到页面中
3. 传递参数时，可以使用对象解构

切换模块思路：

1. 点击采取事件委托方式 .filter
2. 利用过滤函数 filter 筛选出符合条件的数据，因为生成的是数组，传递给渲染函数即可
3. 筛选条件根据点击的 data-index 来判断
4. 可使用对象解构，把事件对象解构

代码实现：

```html
<head>
    <style>
        /* 前面省略 css */
    	/* Tab 栏切换 - 只要 css 这一点代码即可搞定 */
        .filter a:active,
        .filter a:focus {
            background: #05943c;
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="list">
        <!-- <div class="item">
            <img src="" alt="">
            <p class="name"></p>
            <p class="price"></p>
        </div> -->
	</div>
    <script>
    	const goodsList = [
            {
                id: '4001172',
                name: '称心如意手摇咖啡磨豆机咖啡豆研磨机',
                price: '289.00',
                picture: 'https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg',
            },
            {
                id: '4001594',
                name: '日式黑陶功夫茶组双侧把茶具礼盒装',
                price: '288.00',
                picture: 'https://yanxuan-item.nosdn.127.net/3346b7b92f9563c7a7e24c7ead883f18.jpg',
            },
            {
                id: '4001009',
                name: '竹制干泡茶盘正方形沥水茶台品茶盘',
                price: '109.00',
                picture: 'https://yanxuan-item.nosdn.127.net/2d942d6bc94f1e230763e1a5a3b379e1.png',
            },
            {
                id: '4001874',
                name: '古法温酒汝瓷酒具套装白酒杯莲花温酒器',
                price: '488.00',
                picture: 'https://yanxuan-item.nosdn.127.net/44e51622800e4fceb6bee8e616da85fd.png',
            },
            {
                id: '4001649',
                name: '大师监制龙泉青瓷茶叶罐',
                price: '139.00',
                picture: 'https://yanxuan-item.nosdn.127.net/4356c9fc150753775fe56b465314f1eb.png',
            },
            {
                id: '3997185',
                name: '与众不同的口感汝瓷白酒杯套组1壶4杯',
                price: '108.00',
                picture: 'https://yanxuan-item.nosdn.127.net/8e21c794dfd3a4e8573273ddae50bce2.jpg',
            },
            {
                id: '3997403',
                name: '手工吹制更厚实白酒杯壶套装6壶6杯',
                price: '99.00',
                picture: 'https://yanxuan-item.nosdn.127.net/af2371a65f60bce152a61fc22745ff3f.jpg',
            },
            {
                id: '3998274',
                name: '德国百年工艺高端水晶玻璃红酒杯2支装',
                price: '139.00',
                picture: 'https://yanxuan-item.nosdn.127.net/8896b897b3ec6639bbd1134d66b9715c.jpg',
            },
        ]
        
        // 模块1 - 渲染函数
        function render(arr) {
            // 声明一个空字符串变量
            let str = ''
            // 遍历数据
            arr.forEach(item => {
                // 对象解构
                const {name, price, picture} = item
                // forEach 遍历
                str += `<div class="item">
                    <img src=${picture} alt="">
                    <p class="name">${name}</p>
                    <p class="price">${price}</p>
                </div>
                `
            })
            // 将字符串赋值给 list
            document.querySelector('.list').innerHTML = str
        }
        // 页面一打开就渲染
        render(goodsList)

        // 模块2 - 过滤筛选
        document.querySelector('.filter').addEventListener('click', e => {
            // 要用到 e.target.dataset.index 和 e.target.tagName
            // 解构
            const {tagName, dataset} = e.target
            if (tagName === 'A') {
                // arr 是返回的新数组
                let arr = goodsList
                // 0-100 元区间
                if (dataset.index === '1') {
                    arr = goodsList.filter(item => item.price > 0 && item.price <= 100) 
                } else if (dataset.index === '2') { // 100-300 元区间
                    arr = goodsList.filter(item => item.price >= 100 && item.price <= 300) 
                } else if (dataset.index === '3') { // 300 元以上区间
                    arr = goodsList.filter(item => item.price >= 300) 
                }
                // 全部区间无需判断，直接渲染，因为 arr 默认就赋值了 goodsList
                // 渲染函数
                render(arr)
            }
        })
    </script>
</body>
```

效果2<a id='g'>：</a>渲染页面，单价和小计模块，总价模块

![](./\图片\商品结算.png)

渲染模块思路：

1. 使用 map 方法遍历的同时返回数组，用 join 转化为字符串，并追加给 .list 大盒子的 innerHTML
2. 赠品模块 用 split 方法将字符串拆分为数组，使用 map 方法处理返回数组，再用 join 将数组拼接成字符串追加到 innerHTML
3. 总价模块 使用 reduce 方法求和

代码实现：

```html
<body>
    <div class="list">
    <!-- <div class="item">
        <img src="https://yanxuan-item.nosdn.127.net/84a59ff9c58a77032564e61f716846d6.jpg" alt="">
        <p class="name">称心如意手摇咖啡磨豆机咖啡豆研磨机 <span class="tag">【赠品】10优惠券</span></p>
        <p class="spec">白色/10寸</p>
        <p class="price">289.90</p>
        <p class="count">x2</p>
        <p class="sub-total">579.80</p>
    </div> -->
    </div>
    <div class="total">
    	<div>合计：<span class="amount">1000.00</span></div>
    </div>
    <script>
    	const goodsList = [/*同上，此处略*/]
        // 渲染模块 + 处理赠品模块 + 价格模块
        // 读取处理数组 > 转化为字符串 > 替换文本
        document.querySelector('.list').innerHTML = goodsList.map(item => {
            // 对象解构
            const {name, price, picture, count, spec, gift} = item
            // 获取对象值 > 转化为数组 > 转化为字符串用/分隔
            const text = Object.values(spec).join('/')
            // 计算小计模块 单位 * 数量 保留两位小数
            // 注意小数精度问题，小数建议转化为整数再转回来
            const subTotal = ((price * 100 * count) / 100).toFixed(2)
            // 字符串拆成数组 > map 处理数组 > 转化为字符串
            // 因为有的对象没有 gift，所以用三元运算符
            const str = gift ? gift.split(',').map(item => `<span class="tag">【赠品】${item}</span>`).join('') : ''
            return `
                <div class="item">
                    <img src=${picture} alt="">
                    <p class="name">${name} ${str}</p>
                    <p class="spec">${text}</p>
                    <p class="price">${price.toFixed(2)}</p>
                    <p class="count">${count}</p>
                    <p class="sub-total">${subTotal}</p>
				</div>
            `
		}).join('')
      
        // 总价模块
        const total = goodsList.reduce((prev, item) => prev + (item.price * 100 * item.count) / 100, 0)
        document.querySelector('.amount').innerHTML = total.toFixed(2)
    </script>
</body>
```

---

## 综合案例 10 - 记录播放视频时间

P199
