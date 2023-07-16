# HTML + CSS + Web进阶

 ## 谷歌调试工具

浏览器按F12

1. 排错
   - Elements面板下是**所有html标签。**Styles下是所有**CSS内容。**
   - 当选择html标签时，Styles下的CSS内容会显示当前点击html标签所用的效果。
   - 在问题处看到**删除线**，说明**CSS效果被层叠覆盖了。**
   - 在问题处遇到**黄色叹号警示**，说明**CSS语法有问题，注意如果前一行报错会导致下一行遭殃。**
   - **写好的效果没生效**，右键检查后发现Style下**没有写好的效果**，说明不是效果的问题，而**是选择器的问题**，区代码标签里找选择器的问题，
   - 写好的**宽高没生效**，是显示模式的问题，需要转换显示模式。
   - 代码里中英文标点点击一下看距离即可，英文标点与光标很近，中文标点有间距。

2. 调试
   - 当不确定尺码大小时，选中不确定的尺码，**使用上或下调整大小。**但只能调试，如修改需要在代码处手动修改。
   - 也可以增加CSS效果，在Styles内想增加的地方，**按Tab键**，回车确认。

---

## HTML 

HTML 即 超文本标记语言。

使用 **Alt + B** 直接进入浏览器。（下载vscode，安装open in browser插件）

---

### 入门

0. **Web标准**

- 即 HTML + CSS + JavaScript。

HTML 决定**结构**，即负责将文字、图片、音视频放入页面。

CSS 决定**表现**，即对网页元素的外观、位置、大小进行处理。

JavaScript 决定**行为**，即负责动态效果、交互效果。

1. **HTML骨架**

包含 整个网页 html、头部 head（内含标题 title）、主体 body。

```html
<html>
    <head>
        <title>网页的标题</title>
    </head>
    <body>
        网页的主体内容
    </body>
</html>
```

双标签：标签分开始标签与结束标签，中间包裹内容。

单标签：无需成对出现，无法包裹内容。如 \<br\>

2. **注释**

快捷键 Ctrl + /

```html
<!-- 这是注释 -->
```

---

### **排版标签 h1、p、br、hr**

技巧：选中重复的部分按住 **Ctrl + D** 就可以选择这一行所有相同的字符快捷处理。

- 标题标签 **h1** ：只有1~6级标题。**加粗字体，独占一行。**

```html
<body>
    <h1>一级标题</h1>
    <h2>二级标题</h2>
    <h3>三级标题</h3>
    <h4>四级标题</h4>
    <h5>五级标题</h5>
    <h6>六级标题</h6>
</body>
```

- 段落标签 **p**

```html
<body>
    <p>一段文字</p>
</body>
```

- 换行标签 **br** ：让文字强制换行显示。

```html
<body>
    <p>屋舍俨然，有良田、美池、桑竹之属。阡陌交通，鸡犬相闻。 <br> 其中往来种作，男女衣着，悉如外人。</p>
</body>
```

- 水平分割线标签 **hr** ：增加一条水平分割线。

```html
<body>
    <h1>标题</h1>
    <hr>
    <p>
        段落1
        <br>
        段落2
    </p>
</body>
```

### **文本格式化标签**

实现加粗、斜体、下划线与删除线均有两种方法，效果完全相同，但后者有强调语境的意义，便于开发者维护。

注意是**没有换行**的！

```html
<body>
    <b>加粗</b>
    <strong>加粗</strong>
    <u>下划线</u>
    <ins>下划线</ins>
    <i>倾斜</i>
    <em>倾斜</em>
    <s>删除线</s>
    <del>删除线</del>
    <!-- 均无换行 -->
</body>
```

### **媒体标签 img、audio、video**

1. 图片

```html
<body>
    <img src="./1.jpg" alt="这是一只猛犸象" title="悬停显示" width="200">
    <!-- src: 图片路径 -->
    <!-- alt: 替换文本，当图片不显示时显示文本 -->
    <!-- title: 提示文本，当鼠标悬停时显示文本 -->
    <!-- width: 调整图片宽度 -->
    <!-- height: 调整图片高度 width 与 height 如果只设置一个，会自动等比例缩放-->
</body>
```

2. 路径

绝对路径略（直接复制文件位置或网页位置），以下为**相对路径**（从当前文件出发）。

- 同级目录：

```html
<img src="目标图片.jpg">
<img src="./目标图片.jpg">
```

- 下级目录：

```html
<img src="./某文件夹/目标图片.jpg">
```

- 上级目录：

```html
<img src="../上级下的某文件夹/目标图片.jpg">
```

3. 音频

```html
<audio src="../素材/港口.mp3" controls autoplay loop></audio>
<!-- src: 音频路径 -->
<!-- controls: 显示播放控件 -->
<!-- autoplay: 自动播放音乐（一般不支持） -->
<!-- loop: 循环播放 -->
```

4. 视频

```html
<video src="../素材/鸡.mp4" controls autoplay muted loop></video>
<!-- src: 音频路径 -->
<!-- controls: 显示播放控件 -->
<!-- autoplay: 自动播放视频（谷歌浏览器需要 muted 实现静音播放） -->
<!-- loop: 循环播放 -->
```

### **链接标签 a**

```html
<body>
    <!-- href: 跳转地址 -->
    <!-- target属性: _self 默认值（覆盖原网页）_blank （不会覆盖会跳转） -->
    <a href="https://www.baidu.com" target="_blank">点击进入百度</a>
    <br>
    <a href="./某网页.html">点击进入某网页</a>
    <br>
    <a href="#">空链接</a>
    <br>
    
    <!-- 锚点链接：跳转到本页面的某个位置 -->
    <a href="#two">点击跳转</a>
    <!-- 在需要调转的位置添加id属性 -->
    <h3 id="two">跳转到此位置</a>
    
    <!-- 开发初期，不知道跳转链接输入 #(表示空链接) -->
</body>
```

### **列表标签 ul、ol、dl**

列表分为**无序列表**、**有序列表**、**自定义列表**三种。

1. 无序列表 **ul**

**ul** 标签内**只能包含 li 标签**，不能包含其他任何标签，但 **li 标签内可以包含任意标签。**

```html
<ul>
    <li>榴莲</li>
    <li>香蕉</li>
    <li>苹果</li>
    <li>橘子</li>
</ul>
```

2. 有序列表 **ol**

相当于把无序列表中的 **ul** 换成 **ol** ，规则完全相同。

3. 自定义列表

**dl** 标签表示自定义列表整体，**dt** 标签表示自定义列表的主题，**dd** 标签表示列表每一项内容。

**dd** 前会默认显示缩进效果。**dl** 标签内只允许有 **dt** 标签与 **dd** 标签，但 **dt** 、**dd** 标签可以包含任意标签。

```html
<dl>
    <dt>客户服务</dt>
    <dd>以旧换新</dd>
    <dd>价值评估</dd>
</dl>
```

### **表格标签 table、caption、th、tr、td**

- 基本标签：**table** 整体 > **tr** 行 > **td** 单元格

- 格结构搭建：在 **table** 标签内，写入 **border** 会出现网格结构，数字表示**边框宽度**。（写入 width 、height 标签表示宽高，但一般不再 html 中写，在 css 中处理）

- 标题与表头：**caption** 标题 ，**th** 表头单元格
- （了解）表格结构标签：即用 **thead** 表哥头部、**tbody** 表格主体、**tfoot ** 表格底部 包裹住 tr 标签。
- 合并单元格：**rowspan** 上下合并（保留最上），**colspan** 左右合并（保留最左）且不能跨表格结构合并。

```html
<table border="1">
    <caption><strong>学生成绩单</strong></caption>
    <tr>
        <th>姓名</th>
        <th>成绩</th>
        <th>评语</th>
    </tr>
    <tr>
        <td>张三</td>
        <td rowspan="2">100分</td>
        <td>第一名</td>
    </tr>
    <tr>
        <td>李四</td>
        <td>第二名</td>
    </tr>
    <tr>
        <td>总结</td>
        <td colspan="2">配对成功</td>
    </tr>
</table>
```

### **表单标签 input**

|   属性    |   属性值   |                  描述                   |
| :-------: | :--------: | :-------------------------------------: |
|   name    | 用户自定义 | 规定input元素的名称。（给后台人员使用） |
|   value   | 用户自定义 |  规定input元素的值。（给后台人员使用）  |
|  checked  |     --     |   规定此input元素首次加载时应当被选中   |
| maxlength |   正整数   |      规定输入字段中字符的最大长度       |

使用以下 **type** 属性实现各种功能。

1. **text** 输入单行文本

**placeholder** 为占位符，达到提示字的效果，显示在匡内部。

```html
用户名：<input type="text" placeholder="请输入用户名">
```

2. **password** 输入密码

```html
密码：<input type="password" placeholder="请输入密码">
```

3. **radio** 单选框（圆形）

为了达到多选一效果，需要加入 **name** 标签只选择一项，**checked** 标签表示默认选中。

```html
性别：<input type="radio" name="gender" checked>男  <input type="radio" name="gender">女
```

4. **checkbox** 多选框（方形）

```html
<input type="checkbox" checked>我同意此协议
```

5. **file** 文件选择

配合 **multiple** 标签实现多选文件

```html
<input type="file" multiple>
```

6. **submit** 提交按钮

默认值为提交，使用 **value** 修改值。要配合**表单域标签 form**（里面的 action 表示地址）

```html
<form action="">
	<input type="submit" value="免费注册">
</form>
```

7. **reset** 重置按钮

```html
<form action="">
    <input type="reset">
</form>
```

8. **button** 普通按钮

默认无文字无功能，使用 **value** 属性增加文字，之后通过 js 添加功能。

```html
<input type="button" value="普通按钮">
```

### **表单标签 button**

与上面的 6.7.8 功能相同，需要用 **type** 属性决定是那种标签，不用 **value** 增加文字了。

```html
<button>我是按钮</button>
<button type="submit">提交按钮</button>
<button type="reset">重置按钮</button>
<button type="button">普通按钮</button>
```

### **下拉菜单标签 select**

标签组成：**select** 下拉菜单整体，**option** 下拉菜单每一项。

常见属性：**selected** 下拉菜单默认选中。

```html
<select>
    <option>北京</option>
    <option>上海</option>
    <option>广州</option>
    <option selected>深圳</option>
</select>
```

### **文本域 textarea**

生成一个用户输入框。

cols 与 rows 可以设置宽度和高度，但基本不常用，可以再 css 中修改宽高，禁用右下角放大箭头。

```html
<textarea></textarea>
```

### **label 标签**

可实现点击文字时，也能和点击文字前的选项一样的效果。

第一种方法（难）：使用 **label** 标签 包裹文字，在前面增加 **id** 属性，使 **id** 与 **label** 中的 **for** 相同。

第二种方法（易）：使用 **label** 标签包裹全部内容。

```html
性别：<input type="radio" name="gender" id="nan"> <label for="nan">男</label> 
    <label><input type="radio" name="gender">女
```

### **语义化标签 div、span**

1. 无语义网页布局标签 div（独占一行）和 span（不独占一行）

```html
<div>这是div标签</div>
<span>这是span标签</span>
```

2. 有语义的布局标签（了解 手机端网页开发）

### **空格字符实体 &nbsp；**

网页不认识多个空格，只认识单个空格。

```html
这之间有&nbsp;&nbsp;空格
```

---

## CSS

CSS 即 层叠样式表，

**CSS书写顺序规范：**（浏览器执行效率更高）

1. 定位
2. 浮动 / display
3. 盒子模型：margin border padding w+h
4. 文字样式

---

### css - 基础

css写在style标签中，style标签一般写在head标签里面，title标签的下面。

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 使用 ctrl + / 快捷键出现注释 */
        /* css 规则：选择器 {css属性} */
        /* 选择器的作用为：查找标签 */
        p {
            /* 文字颜色变成红色 */
            color: red;
            /* 字变大 px指像素*/
            font-size: 30px;
            /* 背景颜色 */
            background-color: pink;
            /* width 与 height */
            width: 400px;
            height: 400px;
        }
    </style>
</head>
<body>
    <p>这是一个p标签</p>
</body>
</html>
~~~

---

### CSS引入方式 style

css能写在哪？

- 内嵌式：CSS 写在style标签中，\<style> 标签可以写在页面任何位置，但约定俗成写在 \<head> 标签中。
- 外联式：CSS 写在一个单独的 css 文件中，通过 \<link> 标签引入。
- 行内式：CSS 写在标签 style 属性中，配合 js 使用。

**例子**

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 关联写好的 css 文件，使用 link 标签 -->
    <link rel="stylesheet" href="./my.css">
</head>
<body>
    <p>这是一个p标签</p>
    <!-- 在 div 标签内加 style，写入 css 中原本的 {} 中的内容 -->
    <div style="color: green; font-size: 30px;">这是一个div标签</div>
</body>
</html>
~~~

**总结**

| 引入方式             | 书写位置                                      | 作用范围 | 使用场景     |
| -------------------- | --------------------------------------------- | -------- | ------------ |
| 内嵌式               | CSS 写在 style 标签中                         | 当前页面 | 小案例       |
| 外联式               | CSS 写在单独的 css 文件中，通过 link 标签引入 | 多个页面 | 项目中       |
| 行内式（低概率使用） | CSS 写在标签的 style 属性中                   | 当前标签 | 配合 js 使用 |

---

### 基础选择器 . # *

**选择器是用来找标签的。**

- 标签选择器

结构为

```html
选择器 {}
```

以前面的 p 标签为例，会使整篇网页后的所有 p 标签都更换样式，若**想单独设置样式，使用下面的类选择器。**

- 类选择器

定义类选择器：**.** + **类名** + { **css属性名、属性值** }

类名有命名规则，不可以以数字和下划线作为开头。

一个标签可以有多个类名，以空格隔开。

```html
<head>
    <title>Document</title>
    <style>
        .red {
            color: green;
        }
        .size {
            font-size: 60px;
        }
    </style>
</head>
<body>
    <!-- 类：定义且使用后才能生效  -->
    <p>111</p>
    <p class="red size">222</p>
</body>
```

- id选择器

效果与类选择器一样，但一个标签内只能用一个 id，且不用 id 选择器做美化，用于 js 增加动态效果。

定义id选择器：**#** + **类名** + { **css属性名、属性值** }

- 通配符选择器

会**选中通篇所有标签**，修改所有标签样式，一般使用场景为，修改间距，几乎不用。

定义通配符选择器：***** + **类名** + { **css属性名、属性值** }

---

### 进阶选择器

**以下内容中的选择器1，选择器2可以是任何选择器，如标签，通配符，id等。**

1. 后代选择器：空格

功能：嵌套关系，在父子标签环境下，**寻找父元素的后代标签。**

结构为：

```
选择器1 选择器2 {css}
```

有时候效果没生效，不是因为后代选择器写错了，而是因为没有父子标签。

```html
<head>
    <style>
        /* 找到div下的p标签设置文字颜色为红色 */
        div p {
            color: red;
        }
    </style>
</head>
<body>
    <p>这是一个p标签</p>
    <div>
        <!-- 这里的p的父标签是div -->
        <p>这是div的儿子p</p>
    </div>
</body>
```

2. 子代选择器：

**选中某一标签的子标签**

结构为：选择器1>选择器2 {css}

```html
<head>
    <title>Document</title>
    <style>
        /* 会使两个a标签变红
        div a {
            color: red;
        } */
        
        /* 只选中div下的子标签a */
        div > a {
            color: red;
        }
    </style>
</head>
<body>
    <div>
        父级
        <a href="#">这是div里面的a标签</a>
        <p>
            <a href="#">这是div里的p里的a标签</a>
        </p>
    </div>
</body>
```

3. 并集选择器

可以**选择多组标签**，设置一样的css格式。

结构为：选择器1 ， 选择器2 {css}（工作中习惯换行）

```html
<head>
    <title>Document</title>
    <style>
        p, 
        div, 
        span, 
        h1 {
            color: red;
        }
    </style>
</head>
<body>
    <p>p</p>
    <div>div</div>
    <span>span</span>
    <h1>h1</h1>
    <h2>h2</h2>
</body>
```

4. 交集选择器

**选中页面中同时满足多个选择器的标签。**

格式：选择器1选择器2 {css}

```html
<head>
    <title>Document</title>
    <style>
        p.box {
            color: red;
        }
    </style>
</head>
<body>
    <!-- 使带box类的p标签颜色变红 -->
    <p class="box">p1</p>
    <p>p2</p>
    <div class="box">div</div>
</body>
```

---

### 伪类选择器 :hover、:focus、:checked

1. hover 伪类选择器

**选中鼠标悬停时的状态。任何标签都可以添加伪类**

格式：选择器:hover {css}

```html
<head>
    <style>
        /* 鼠标悬停时，文字变红 */
        a:hover {
            color: red;
            background-color: blue;
        }
    </style>
</head>
<body>
    <a href="#">这是超链接</a>
</body>
```

2. foucs 伪类选择器

鼠标点击文本框时的状态（焦点事件）

格式：选择器:focus {css}

```html
<head>
    <style>
        input {
            width: 200px;
            /* 过渡 */
            transition: all .3s;
        }
        /* focus伪类选择器 获得焦点 */
        input:focus {
            width: 300px;
        }
    </style>
</head>
<body>
    <input type="text">
</body>
```

3. checked 伪类选择器

只会选择被勾选的复选框。

```html
<head>
    <style>
        /* 选择被勾选的复选框 */
        .ck:checked {
            width: 20px;
            height: 20px;
        }
    </style>
</head>
<body>
    <input type="checkbox" name="" id="" class="ck">
    <input type="checkbox" name="" id="" class="ck">
    <input type="checkbox" name="" id="" class="ck">
</body>
```

---

### 结构伪类选择器 child

作用：**根据元素的家族关系查找元素**，常用于查找某父级选择器的子元素。

|         选择器         |                   说明                   |
| :--------------------: | :--------------------------------------: |
|    E:first-child {}    |  匹配父元素的第一个子元素，并且是E元素   |
|    E:last-child {}     | 匹配父元素的最后一个子元素，并且是E元素  |
|   E:nth-child(n) {}    |   匹配父元素的第n个子元素，并且是E元素   |
| E:nth-last-child(n) {} | 匹配父元素的倒数第n个子元素，并且是E元素 |


```html
<head>
    <title>Document</title>
    <style>
        /* 选中第一个li */
        li:first-child {
            background-color: green ;
        }
        /* 选中第n个li */
        li:nth-child(5) {
            background-color: pink;
        }
    </style>
</head>
<body>
    <!-- ul>li{这是第$个li}*8 -->
    <ul>
        <li>这是第1个li</li>
        <li>这是第2个li</li>
        <li>这是第3个li</li>
        <li>这是第4个li</li>
        <li>这是第5个li</li>
    </ul>
</body>
```

**nth-child(n) {} 里的 n 可以是公式**

|       功能       |       公式       |
| :--------------: | :--------------: |
|       偶数       |     2n、even     |
|       奇数       | 2n+1、2n-1,、odd |
|    找到前五个    |       -n+5       |
| 找到从第五个往后 |       n+5        |

```html
<head>
    <title>Document</title>
    <style>
        /* 选中第一个li */
        li:nth-child(4n) {
            background-color: green ;
        }
    </style>
</head>
<body>
    <!-- ul>li{这是第$个li}*8 -->
    <ul>
        <li>这是第1个li</li>
        <li>这是第2个li</li>
        <li>这是第3个li</li>
        <li>这是第4个li</li>
        <li>这是第5个li</li>
        <li>这是第6个li</li>
        <li>这是第7个li</li>
        <li>这是第8个li</li>
    </ul>
</body>
```

---

### 属性选择器 []

使用 [单一属性] 可以根据属性选择对应的标签。

```html
<head>
    <style>
        input[value] {
            color: bluesky;
        }
	</style>
</head>
<body>
    <input type="text" value="123">
    <input type="password">
</body>
```

或者 [属性=属性值]

```html
<head>
    <style>
        input[type= text] {
            color: bluesky;
        }
	</style>
</head>
<body>
    <input type="text">
    <input type="password">
</body>
```

---

### 字体样式 font - size、weight、style、family

**复合属性 font**

1. 字体大小

属性名：**font-size**

取值：**数字** + **px** （ 谷歌浏览器默认字号为16px ）

```html
<head>
    <title>Document</title>
    <style>
        p {
            font-size: 30px;
        }
    </style>
</head>
<body>
    <p>段落文字字号为30px</p>
</body>
```

2. 字体粗细

属性名：**font-weight**

取值：字符（normal等）或**数字**，推荐使用数字。数字取值**400**用来**变细**，取值**700**用来**加粗**。

```html
<head>
    <title>Document</title>
    <style>
        div {
            font-weight: 700;
        }
    </style>
</head>
<body>
    <div>这是div</div>
</body>
```

3. 文字倾斜

属性名：**font-style**

取值：**normal** 表示正常效果，**italic** 表示倾斜效果。

```html
<head>
    <title>Document</title>
    <style>
        div {
            font-style: italic;
        }
        em {
            font-style: normal;
        }
    </style>
</head>
<body>
    <div>使用css后倾斜</div>
    <em>这里本来是倾斜文字，使用css后不倾斜</em>
</body>
```

4. 字体系列

属性名：**font-family**

取值：默认为微软雅黑，sans-serif 表示非衬线字体。

```html
<head>
    <title>Document</title>
    <style>
        div {
            /* 如果用户电脑没有安装以下前者字体，按下一个字体显示 */
            /* 如果这几中字体都没有，按一种非衬线字体系列显示 */
            font-family: 微软雅黑, 宋体, 黑体, sans-serif;
        }
    </style>
</head>
<body>
    <div>这是一个div标签</div>
</body>
```

5. **CSS层叠性与复合属性**

- 基于层叠性，后面的属性覆盖前面的属性。

```html
<head>
    <title>Document</title>
    <style>
        p {
            color: red;
            color: green;
        }
    </style>
</head>
<body>
    <p>我是一个p标签</p>
</body>
```

- **复合属性**，font 后接 style weight size**/**line-height family，使用空格隔开，size 和 line-height 用 / 隔开。

```html
<head>
    <title>Document</title>
    <style>
        p {
            /* font: style  weight  size  字体 */
            font: italic 700 66px 宋体;
            font: 100px 微软雅黑;
            /* 只写两个也会生效 */
        }
    </style>
</head>
<body>
    <p>我是一个p标签</p>
</body>
```

---

### 行高(文本上下居中) lh

属性名：**line-height**

取值：**数字** + **px** 或 **倍数**

**行高与盒子高度（即height）相同时，文字即为居中效果。**

行高指文本高度加上下间距的总和，若使用倍数，则是字号的倍数。行高也可以放在 font 字段复合。

```html
<head>
    <title>Document</title>
    <style>
        /* p {
            line-height: 1.5;
        } */
        /* 字号66px 宋体 倾斜 加粗 行高两倍 */
        p {
            font: italic 700 66px/2 宋体;
        }
    </style>
</head>
<body>
    <p>一段文字</p>
</body>
```

---

### 文本样式 text - indent、align、decoration

1. 文本缩进

属性名：**text-indent**

取值：**数字** + **px** 或 **数字** + **em**（1 em = 当前标签的 font-size 的大小）

```html
<head>
    <title>Document</title>
    <style>
        p {
            text-indent: 2em;
            /* 默认字号16px，所以可以写32px，但不推荐 */
        }
    </style>
</head>
<body>
    <p>HTML 决定结构，即负责将文字、图片、音视频放入页面，CSS 决定表现，即对网页元素的外观、位置、大小进行处理。JavaScript 决定行为，即负责动态效果、交互效果。</p>
</body>
```

2. 文本/内容水平对齐

属性名：**text-align** 

取值：

| 属性值 | 效果         |
| ------ | ------------ |
| left   | 左对齐       |
| center | 左右居中对齐 |
| right  | 右对齐       |

```html
<head>
    <title>Document</title>
    <style>
        h1 {
            /* text-align: right; */
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>新闻标题，默认左对齐</h1>
</body>
```

**text-align** 不仅可使文字居中，也可以使**图片**等内容居中。text-align 可应用于：文本、span标签、a标签、input标签、img标签。

图片在父级 <body> 标签内，所以要给 <body> 标签居中，而不是给 img 居中，切记。

```html
<head>
    <title>Document</title>
    <style>
        body {
            text-align: center;
        }
    </style>
</head>
<body>
    <img src="./僵尸.jpeg" alt="">
</body>
```

3. 文本修饰

属性名：**text-decoration**

取值：

| 属性值        | 取值               |
| ------------- | ------------------ |
| **underline** | 下划线（常用）     |
| line-through  | 删除线（不常用）   |
| overline      | 上划线（几乎不用） |
| **none**      | 无装饰线（常用）   |

```html
<head>
    <title>Document</title>
    <style>
        div {
            text-decoration: underline;
        }
        p {
            text-decoration: line-through;
        }
        a {
            text-decoration: none;
        }
    </style>
</head>
<body>
    <div>div标签</div>
    <p>p标签</p>
    <a href="#">超链接</a>
</body>
```

---

### 文字颜色 color

属性名：**color**

属性值：

|  颜色表现方式  |                表示含义                 |                   属性值                    |
| :------------: | :-------------------------------------: | :-----------------------------------------: |
|     关键词     |             预定义的颜色名              |         red、green、blue、yellow……          |
|   rgba表示法   | 红绿蓝三原色+a表示透明度，取值范围是0~1 |  rgba(255,255,255,0.5)、rgba(255,0,0,0.3)…  |
| 十六进制表示法 |     #开头，将数字转换成十六进制表示     | #000000、#ff0000、#e92322，简写：#000、#f00 |

---

### 背景 bg - c、 i、r、p

**复合属性 bg**

1. 背景颜色

属性名：**background-color**

属性值：

|  颜色表现方式  |                表示含义                 |                   属性值                    |
| :------------: | :-------------------------------------: | :-----------------------------------------: |
|     关键词     |             预定义的颜色名              |         red、green、blue、yellow……          |
|   rgba表示法   | 红绿蓝三原色+a表示透明度，取值范围是0~1 |  rgba(255,255,255,0.5)、rgba(255,0,0,0.3)…  |
| 十六进制表示法 |     #开头，将数字转换成十六进制表示     | #000000、#ff0000、#e92322，简写：#000、#f00 |

2. 背景图片

属性名：**background-image**

属性值：**url('图片的路径')**

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

3. 背景平铺

背景图按上面直接用，标签尺寸太大会**导致复制多份**，当**只想显示一张图**平铺方式时使用。

属性名：**background-repeat**

属性值：

|   取值    |              效果              |
| :-------: | :----------------------------: |
|  repeat   | （默认值）水平和垂直方向都平铺 |
| no-repeat |             不平铺             |
| repeat-x  |    沿着水平方向（x轴）平铺     |
| repeat-y  |    沿着垂直方向（y轴）平铺     |

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 400px;
            height: 400px;
            background-color: pink;
            background-image: url(./images/1.jpg);
            background-repeat: no-repeat;
        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

4. 背景位置

改写背景图的位置，背景只显示在盒子内

属性名：**background-position**

属性值：水平位置 垂直位置（用空格隔开）

- 方法一：单词

| 水平方向 | 垂直方向 |
| :------: | :------: |
|   left   |   top    |
|  center  |  center  |
|  right   |  bottom  |

- 方法二：数字+px（坐标）

原点（0,0）为左上角，图片左上角会根据坐标移动，x轴表示水平向右，y轴表示垂直向下。

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 700px;
            height: 700px;
            background-color: pink;
            background-image: url(./图片/2.jpg);
            background-repeat: no-repeat;
            /* background-position: center center; */
            background-position: 50px 50px;

        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

5. 复合属性

background（**bg**）

bg属性后可接color、image、repeat、position，**无所谓先后顺序，但注意bgp不可以颠倒顺序。**

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 700px;
            height: 700px;
            background: pink url(./images/1.jpg) no-repeat center bottom;
        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

6. 注意事项

**img与背景图的区别：**他们都可以让网页上显示一张图片，img标签可以让网页显示原图片尺寸，不用设置宽高，但div标签+背景图片的方法要设置宽高。

**原则：****img**用来实现网页中**重要的图片**，**bg标签**用来实现**装饰性图片**。

**bg标签一定要设置height，否则看不到背景也看不到盒子。**

---

### 元素显示模式 display

元素即使标签，**所有<>都是元素。**

1. 块级元素

如**div**、**p**、**h**等。特点是**独占一行**，宽度默认为父元素的宽度，高度默认由内容撑开，**可设置宽高**。

2. 行内元素

如**a**、**span**、b、u、i、s、strong、ins、em、del等，特点是**一行可以显示多个**，宽度高度默认由内容撑开，**不可设置宽高**。

3. 行内快元素

特点是**一行可以显示多个，可以设置宽高。**

如**img**、**input**、**textarea**、button、select等。

```html
<head>
    <title>Document</title>
    <style>
        img {
            width: 100px;
            height: 100px;
        }
    </style>
</head>
<body>
    <img src="./images/1.jpg" alt="">
    <img src="./images/2.jpg" alt="">
</body>
```

4. 元素显示模式转换

可以让显示模式互相切换。

语法：

|         属性          |       效果       | 使用频率 |
| :-------------------: | :--------------: | :------: |
|    display：block     |  转换成块级元素  |   较多   |
| display：inline-block | 转换成行内块元素 |   较多   |
|    display：inline    |  转换成行内元素  |   较少   |

```html
<head>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            /* 将div转换为行内快模式 */
            display: inline-block;
        }
    </style>
</head>
<body>
    <div>1111</div>
    <div>2222</div>
</body>
```

5. **HTML嵌套规范**

块级元素一般作为大容器，可以嵌套文本、块级元素、行内快元素等。**但h标签内不要套h和p元素，p标签内不要钱套div、p、h元素，a标签可以嵌套任何元素，但不能嵌套a标签。**

---

### CSS特性

1. 继承性

特性：子元素有默认继承父元素样式的特点，**文字属性都可以继承**，非文字属性一律不能继承。可以谷歌浏览器F12，点击元素查看继承。

```html
<head>
    <title>Document</title>
    <style>
        div {
            color: red;
            font-size: 30px;
            height: 300px;
        }
    </style>
</head>
<body>
    <div>
        这是div里面标签的文字
        <span>这是div里的span</span>
        <a href="#">这是一个超链接</a>
        <!-- 自己没有效果会继承，有效果则不会，超链接自带蓝色，所以不会变红 -->
    </div>
</body>
```

2. 层叠性

层叠即效果覆盖。

```html
<head>
    <title>Document</title>
    <style>
        div {
            color: red;
            color: green;
        }
        .box {
            font-size: 30px;
        }
    </style>
</head>
<body>
    <div class="box">文字</div>
</body>
```

3. 优先级

如果一个标签**用了多个选择器**，优先级高的选择器样式会覆盖优先级低的选择器样式。

优先级公式：继承 < 通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important

上面的不用记，只要知道**哪个标签作用的范围更广，那么他的优先级就更低。**比如通配符选择器可以作用通篇所有标签，所有优先级比标签选择器低，因为标签选择器只作用单个标签。

**!important不能提升继承的优先级**，因为如果标签自己有样式了就无法继承父级样式了（没有才会继承），**能让非继承的优先级提升至最高，只要是继承优先级最低。**企业间慎用!important

- 优先级对比示例：

```html
<head>
    <title>Document</title>
    <style>
        div {
            color: green;
        }
        body {
            color: red;
        }
    </style>
</head>
<body>
    <div>测试优先级</div>
</body>
```

此时div的范围比body范围更小，所以优先级更高，显示为绿色。

```html
<head>
    <title>Document</title>
    <style>
        #box {
            color: orange;
        }
        .box {
            color: blue;
        }
    </style>
</head>
<body>
    <di class="box" id="box">测试优先级</div>
</body>
```

id选择器优先级大于类选择器，显示为橙色。接下来添加行内CSS样式。

```html
<head>
    <title>Document</title>
    <style>
        #box {
            color: orange;
        }
        .box {
            color: blue;
        }
    </style>
</head>
<body>
    <di class="box" id="box" style="color: pink;">测试优先级</div>
</body>
```

因为行内式只在此行生效，范围更小，所以最终显示为粉色。最后对非继承类且优先级最低的div标签加上!important

```html
<head>
    <title>Document</title>
    <style>
        #box {
            color: orange;
        }
        .box {
            color: blue;
        }
        div{
            color: green !important;
        }
        body {
            color: red;
        }
    </style>
</head>
<body>
    <div class="box" id="box" style="color: pink;">测试优先级</div>
</body>
```

最终会显示为绿色。

上面优先级（权重）都是单个标签，当标签为复合标签时，需要通过权重叠加计算方法，判断那个选择器会最终生效。

即**看个数**，看复合选择器中行内样式的个数、id选择器的个数。类选择的个数、标签选择器的个数，进行比对即可。

```html
<head>
    <title>Document</title>
    <style>
        /* (行内，id，类，标签) */
        /* (0,1,0,1) */
        div #one {
            color: orange;
        }
        /* (0,0,2,0) */
        .father .son {
            color: skyblue;
        }
        /* (0,0,1,1) */
        .father p {
            color: purples;
        }
        /* (0,0,0,2) */
        div p{
            color: pink;
        }
    </style>
</head>
<body>
    <div class="father">
        <p class="son" id="one">这是一个标签</p>
    </div>
</body>
```

最终生效为橙色。更复杂的可以看视频P89

---

### 盒子模型 w+h、bsz、bd、pd、mg

0. 工具与原则

下载PxCook，用来精准量尺寸。点击创建项目，设计模式用来打开png，jpg图片，然后拖入图片，点击尺子图标量大小，点击吸管图标量色值。开发模式用来打开psd文件。

工作中，复刻网页需要满足：**从外向内，从上到下的原则，先把盒子写好，把盒子的宽高写好，最后再调节文字。**

1. **盒子内容 w+h+bgc等**

盒子的作用是布局。页面中任何标签都可以看做是一个盒子。浏览器渲染网页会将网页中的元素看作是一个个矩形区域，即盒子。

每个盒子包括：**内容区域(content)，内边距区域(padding)，边框区域(border)，外边框区域(margin)。**

以一个装电脑的盒子为例，电脑就是内容，边框线就是箱子，填充泡沫就是内边距，两个盒子间的距离为外边距。

在浏览器里检查时，点击标签可以看到盒子颜色，蓝色为内容，绿色为内边距，黄色为边框，棕色为外边距。

使用 **width + height 规定盒子内容**的区域大小。

2. **边框 bd**

- 使用 **border** 属性**规定边框**，border属性为复合属性，取值间可以用空格隔开。快捷键为 **bd+Tab **键。取值为（粗细，线段类型，颜色）**（不分先后顺序！）**

```html
<head>
    <title>Document</title>
    <style>
        div {
            /* w200+h200+bgc */
            width: 200px;
            height: 200px;
            background-color: pink;
            /* bd 按下Tab */

            /* solid为实线 */
            /* border: 5px solid #000; */

            /* dashed为虚线 */
            /* border: 5px dashed #000; */

            /* dotted为点线 */
            border: 5px dashed #000;
        }
    </style>
</head>
<body>
    <div>电脑</div>
</body>
```

这种border效果会使盒子四个方向的边框全部生效，如果**只想让某一个方向生效**，使用：**border-方位名词**（top、bottom、left、right），border，padding与margin都可以这么写使某一方向生效。

```html
<head>
    <title>Document</title>
    <style>
        div {
            /* w200+h200+bgc */
            width: 200px;
            height: 200px;
            background-color: pink;

            border-left: 5px dashed #000;
            border-right: 5px dashed #000;
        }
    </style>
</head>
<body>
    <div>电脑</div>
</body>
```

注意**盒子最终尺寸包含border**

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 400px;
            height: 400px;
            background-color: green;
            border: 10px solid #000;
        }
    </style>
</head>
<body>
    <div>div</div>
</body>
```

上面这段代码最终盒子是420\*420的大小，而不是400\*400，想缩小需要减少为width: 380px，height: 380px。

3. **内边距 padding**

padding 属性可以作为复合属性使用，表示**单独设置某个方向的内边距，最多接四个值，如果值是0，后面不用接px**

采用**顺时针**方向生效：即上右下左，**缺的方向的值默认等于它对面方向的值。**

- 接四个值：表示四个方向。
- 接三个值：会作用上、右、下（左边距与右边距相同。）
- 接两个值：会作用上、右（下边距与上边距相同，左边距与右边距相同。）

**注意**盒子尺寸是**内容宽高、加上边框、加上内边距的最终大小。**

在综合案例2.3中，不符合实际场景，一旦有的导航字变多，内容区域会撑爆，为了**不让内容比盒子还要大，需取消盒子内容的宽度，添加内边距，这样内容外会有内边距包裹。**

```html
<head>
    <title>Document</title>
    <style>
        .box {
            height: 40px;
            border-top: 3px solid #ff8500;
            border-bottom: 3px solid #edeef0;
            text-decoration: none;
        }
        .box a {
            /* width: 80px; */
            height: 40px;
            /* background-color: #edeef0; */
            display: inline-block;
            text-align: center;
            line-height: 40px;
            text-decoration: none;
            font-size: 12px;
            color: #4c4c4c;
            padding: 0 16px;;
        }
        .box a:hover {
            background-color: #edeef0;
            color: #ff8400;
        }
    </style>
</head>
<body>
    <div class="box">
        <a href="#">新浪</a>
        <a href="#">新浪导航新浪导航</a>
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
    </div>
</body>
```

4. **CSS3自动内减 box-sizing**

CSS3可以自动内减，不用再手动添加内边距边框撑大盒子后手动减去内容宽高了，**通常写在*内**。

添加：**box-sizing: border-box**

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            /* 使用CSS3盒子模型可以再添加border和padding后不需要手动做减法 */
            box-sizing: border-box;
        }
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px solid #000;
            padding: 20px;
        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

5. **外边距 margin**

- **外边距的写法与内边距相同。**

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            margin: 50px;
        }
    </style>
</head>
<body>
    <div>内容</div>
</body>
```

- **版心居中 margin: 0 auto**； 版心指网页的有效内容，**margin: 0 auto 可以让版心水平居中**。（0表示上下间距，auto表示左右间距，等于auto意思是居中）

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 300px;
            height: 300px;
            background-color: pink;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div>文字</div>
</body>
```

6. **几种问题**

- **垂直布局的块级元素，上下的margin会合并**，结果为两者距离的margin最大值、尽量避免这种情况。

以下例子最终两块间距为60，而不是100

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        .one {
            margin-bottom: 60px;
        }
        .two {
            margin-bottom: 50px;
        }
    </style>
</head>
<body>
    <div class="one">11</div>
    <div class="two">11</div>
</body>
```

- **外边距塌陷问题：**以下代码为一个粉块内左上角一个蓝块，为了让蓝块向下一些，对蓝块添加上边距，但导致了坑爹：他的父元素粉块一起向下移动了。解决办法：**给父元素添加overflow: hidden。**

```html
<head>
    <title>Document</title>
    <style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
        }
        .son {
            width: 100px;
            height: 100px;
            background-color: skyblue;
            margin-top: 50px;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">son</div>
    </div>
</body>
```

- **行内标签的（inline）的 margin-top/bottom 与 padding-top/bottom 不生效。水平位置可以正常修改，需要修改垂直位置时，使用行高 line-height**

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        span {
            margin: 100px;
			/* margin 只会生效左右 */
            line-height: 100px;
        }
    </style>
</head>
<body>
    <span>span</span>
    <span>span</span>
</body>
```

7. **清除默认的内外边距**

浏览器会给部分标签设置默认的margin和padding，可以使用下面的方法清除所有内外边距，**开发项目时要有此内容。**

```html
<head>
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
    </style>
</head>
<body>
    <p>pppp</p>
    <h1>h1</h1>
    <ul>
        <li>lili</li>
    </ul>
</body>
```

---

### CSS浮动 fl

1. **伪元素**

一般网页中非主体元素内容可以使用伪元素。**用CSS模拟出标签效果**，一般用来装饰图。

**::before** 可以再父元素内容的最前添加一个伪元素，**::after** 可以再父元素内容的最后添加一个伪元素，**但必须添加content，否则伪元素不生效，伪元素内可以加所有CSS内容。**

```html
<head>
    <title>Document</title>
    <style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
        }
        .father::before {
            content: "超级";
            color: green;
            width: 100px;
            height: 100px;
            background-color: blue;
            /* 默认为行内元素，宽高不生效 */
            display: block;
        }
        .father::after {
            content: "里奥";
        }
    </style>
</head>
<body>
    <div class="father">马</div>
</body>
```

2. **浮动**

- 背景

**标准流：**标准流即标签默认的排列方式，如div独占一行就是标准流

**浮动：**即让块标签完美的显示在一行，浮动用来**网页布局**。

**浏览器解析行内块 inline-block 或行内标签 inline 时，标签换行会产生一个空格的间距。**

```html
<head>
    <title>Document</title>
    <style>
        div {
            display: inline-block;
            width: 100px;
            height: 100px;
        }
        .one {
            background-color: pink;
        }
        .two {
            background-color: skyblue;
        }
    </style>
</head>
<body>
    <!-- 会发现两个div中没有默认 margin，但有空隙 -->
    <div class="one">one</div>
    <div class="two">two</div>
    <!-- 应改为：<div class="one">one</div><div class="two">two</div> -->
</body>
```

虽然放在一行可以解决问题，但随着内容增多会不适用，可读性差。

当对两块添加浮动效果，就可以让他们在一行排列。

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
        }
        .one {
            background-color: pink;
            float: left;
        }
        .two {
            background-color: skyblue;
            /* 两块间没有间距 */
            float: left;
        }
    </style>
</head>
<body>
    <div class="one">one</div>
    <div class="two">two</div>
</body>
```

- 浮动的特点

**浮动的标签会脱离标准流，在标准流中不占位置。**可以覆盖标签，但不能覆盖文字。**下一个浮动元素会在上一个浮动元素后面排列，浮动后的标签具备行内块的特点：宽高生效，在一行排列。**

**如果父级宽度不够，子级会自动换行。**

```html
<head>
    <title>Document</title>
    <style>
        /* 浮动的标签时 顶对齐 */
        /* 浮动后的标签具备行内快的特点 */
        .one {
            width: 100px;
            height: 100px;
            background-color: pink;
            float: left;
            margin-top: 50px;
        }
        .two {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            float: left;
        }
        .three {
            width: 300px;
            height: 300px;
            background-color: orange;
        }
    </style>
</head>
<body>
    <div class="one">one</div>
    <div class="two">two</div>
    <div class="three">three</div>
</body>
```

- 浮动布局

**需要做版心居中的结构时，如图所示，需要有三个标签，其中一个作为父标签margin 0 auto！**

![](./\图片\浮动.png)

```html
<head>
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .top {
            height: 40px;
            background-color: #333;
        }
        .header {
            width: 1226px;
            height: 100px;
            background-color: #ffc0cb;
            margin: 0 auto;
        }
        .content {
            width: 1226px;
            height: 460px;
            background-color: green;
            margin: 0 auto;
        }
        .left {
            float: left;
            width: 234px;
            height: 460px;
            background-color: orange;
        }
        .right {
            float: left;
            width: 992px;
            height: 460px;
            background-color: #87ceeb;
        }
    </style>
</head>
<body>
    <div class="top"></div>
    <div class="header">头部</div>
    <div class="content">
        <!-- .left+.right -->
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
</body>
```

- 清除浮动

含义：**清除浮动个别的标签带来的影响。**

问题描述：假如有上下两个div块，上面的块里面做了分块浮动，如果取消上块的高，那么在浮动效果还在的情况下，下面的块会直接到顶部（上面块的下面）

问题代码：

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .top {
            margin: 0 auto;
            width: 1000px;
            /* height: 300px; */
            background-color: pink;
        }
        .bottom {
            height: 100px;
            background-color: green;
        }
        .left {
            float: left;
            width: 200px;
            height: 300px;
            background-color: #ccc;
        }
        .right {
            float: right;
            width: 790px;
            height: 300px;
            background-color: skyblue;
        }
    </style>
</head>
<body>
    <div class="top">
        <div class="left"></div>
        <div class="right"></div>
    </div>
    <div class="bottom"></div>
</body>
```

所以要清除浮动带来的影响：

方法一：给父元素家高度（有时需求上不允许加）

方法二：额外标签法：（会添加额外标签，使HTML结构复杂）

在父元素内容的最后添加一个**块级元素**，给块级元素设置**clear:both**，标签通常起名为**clearfix**。

```html
<head>
    <style>
        .clearfix {
            /* 清除左右两侧浮动的影响 */
            clear:both;
        }
    </style>
</head>
<body>
    <div class="top">
        <div class="left"></div>
        <div class="right"></div>
        <!-- 额外标签 -->
        <div class="clearfix"></div>
    </div>
    <div class="bottom"></div>
</body>
```

方法三：单伪元素清除法（与方法二原理相同）

细节代码不用背，企业清除浮动会给，直接复制。与方法二类似，只是不用加额外标签了。把clearfix结合伪元素的内容处理。

```html
<head>
    <style>
        .clearfix::after {
            content: '';
            /* 伪元素添加的标签是行内，而与方法二相同要求为块 */
            display: block;
            clear: both;
        }
    </style>
</head>
<body>
    <!-- 调用 top 类同时调用 clearfix 类 -->
    <div class="top clearfix">
        <div class="left"></div>
        <div class="right"></div>
    </div>
    <div class="bottom"></div>
</body>
```

方法四：双伪元素清除法（看似最麻烦，但只要调用clearfix不光能解决浮动还能解决塌陷问题。）

```html
<head>
    <style>
        /* 解决外边距塌陷问题：父子标签，都是块级，子标签margin会影响父级的位置 */
        .clearfix::before,
        .clearfix::after {
            content: '';
            display: table;
        }
        .clearfix::after {
            clear: both;
        }
    </style>
</head>
<body>
    <!-- 调用 top 类同时调用 clearfix 类 -->
    <div class="top clearfix">
        <div class="left"></div>
        <div class="right"></div>
    </div>
    <div class="bottom"></div>
</body>
```

方法五：**overflow:hidden**（最方便的方法）

给父元素设置即可。

```html
<head>
    <style>
        .top {
            margin: 0 auto;
            width: 1000px;
            /* height: 300px; */
            background-color: pink;
            /* 添加一行解决 */
            overflow:hidden;
        }
    </style>
</head>
```

---

### 定位 por、pos、poa、pof、z-index

作用：**可以让元素自由摆放在网页的任何位置，一般用于盒子之间的堆叠情况。**

1. 使用方法：

第一步：设置定位方式

属性名：**position**

属性值：

|   定位方式   |    属性值    |
| :----------: | :----------: |
|   静态定位   |    static    |
| **相对定位** | **ralative** |
| **绝对定位** | **absolute** |
| **固定定位** |  **fixed**   |

第二步：设置偏移值，水平和垂直方向选一个使用即可，**就近选择**。

| 方向 | 属性名 | 属性值  |      含义      |
| :--: | :----: | :-----: | :------------: |
| 水平 |  left  | 数字+px | 距离左边的距离 |
| 水平 | right  | 数字+px | 距离右边的距离 |
| 垂直 |  top   | 数字+px | 距离上边的距离 |
| 垂直 | bottom | 数字+px | 距离下边的距离 |

2. **相对定位 por**

**相对于自己之前的位置进行移动。不会改变标签原有显示模式。**

**没有脱标（没脱离标准流的控制，原先的位置还占着）**

代码：**position:relative;**

```html
<style>
        /* 如果left和right都有, 以left为准; top和bottom都有以top 为准 */
        /* css书写: 1. 定位 / 浮动 / display ; 2. 盒子模型; 3. 文字属性 */
        .box {
            position: relative;
            left: 100px;
            top: 200px;
            /* right: 200px; */
            /* bottom: 400px; */

            /* 
                1. 占有原来的位置
                2. 仍然具体标签原有的显示模式特点
                3. 改变位置参照自己原来的位置
            */

            width: 200px;
            height: 200px;
            background-color: pink;
        }
</style>
```

3. **绝对定位 poa**

**父级有定位，参照父级进行定位，父级无定位，参照浏览器窗口进行定位。（这里的父级是广义的，祖辈级都算）**

**脱标，不占位，改变标签的显示模式特点: 具体行内块特点（在一行共存, 宽高生效）**

子绝父相（子级若用绝对定位，父级请用相对定位）

代码：**position:absolute;**

```html
<head>
    <style>
        .father {
            /* 工作中父级一般用 relative 相对定位 */
            position: relative;

            width: 400px;
            height: 400px;
            background-color: pink;
        }
        
        .son {
            width: 300px;
            height: 300px;
            background-color: skyblue;
        }

        .sun {
            position: absolute;
            right: 20px;
            bottom: 50px;

            width: 200px;
            height: 200px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="father">
        <div class="son">
            <div class="sun"></div>
        </div>
    </div>
</body>
```

- 如果盒子绝对定位过，又用margin: auto居中过，**居中无效。**使用以下方法居中。

方法一：（修改性差，一旦修改 width 或 width 为奇数就不行）

```html
<style>
    .box {
        position: absolute;
        /* margin: 0 auto; (无效) */

        /* left: 50%, 整个盒子移动到浏览器中间线右侧 */
        left: 50%;
        /* 盒子左移: 取值为半个盒子宽度 */
        margin-left: -150px;

        top: 50%;
        margin-top: -150px;

        width: 300px;
        height: 300px;
        background-color: pink;
    }
</style>
```

**方法二：**CSS3 位移属性 **transform: translate();**

```html
<style>
    .box {
        position: absolute;
        left: 50%;
        top: 50%;
        /* 左移并上移: 自己宽度高度的一半 */
        transform: translate(-50%, -50%);

        width: 400px;
        height: 300px;
        background-color: pink;
    }
</style>
```

4. **固定定位 pof**

**position: fixed;**

固定在浏览器窗口的固定位置。参考浏览器窗口位置进行定位移动。**投标，不占位置**。

与绝对定位相同，**具备行内快的特点**，需要设置尺寸，如果没有内容那么看不到盒子。

```html
<style>
    .box {
        position: fixed;
        left: 0;
        top: 0;

        width: 200px;
        height: 200px;
        background-color: pink;
    }
</style>
```

5. **元素层级关系 z-index**

不同布局元素间：标准流 < 浮动 < 定位

两个都是定位元素时：写在下面的元素层级更高，会覆盖掉上面的元素。

可使用 **z-index** 属性，为定位加层级，取值越高位置越高，默认值为0，**必须配合定位**。

```html
<head>
    <style>
        div {
            width: 200px;
            height: 200px;
        }
        .one {
            position: absolute;
            left: 20px;
            top: 50px;

            z-index: 1;            
            background-color: pink;
        }
        .two {
            position: absolute;
            left: 50px;
            top: 100px;
            background-color: skyblue;
        }
    </style>
</head>
<body>
    <!-- 谁在上取决于这里两个标签的顺序 后来居上 -->
    <!-- 或者用 z-index 属性，取值越大，现实越靠上，默认值为0 -->
    <div class="one">one</div>
    <div class="two">two</div>
</body>
```

---

### 装饰 va、cu、bd - rd、ovh、dp

1. **垂直对齐 va**

问题：当图片和文字在一行显示时，其实底部没有对齐。**浏览器遇到行内或行内块标签默认当做文字处理。**

**处理行内块和文字对齐，或行内块和行内块对齐，想要居中均使用vertical-align: middle;**

属性名：**vertical-align**

属性值：

|   属性值   |      效果      |
| :--------: | :------------: |
|  baseline  | 默认，基线对齐 |
|    top     |    顶部对齐    |
| **middle** |  **中部对齐**  |
|   button   |    底部对齐    |

```html
<!-- 场景一：搜索框默认的 padding 与 margin 撑大了盒子，导致尺寸不一不对齐 -->
<!-- 解决尺寸不一：*{} 取消默认值 或 box-sizing: border-box;（内减） -->
<!-- 解决不对齐：对一个input标签添加 vertical-align: middle; -->
<head>
    <style>
        input {
            height: 50px;
        }
    </style>
</head>
<body>
    <input type="text"><input type="button" value="搜索">
</body>

<!-- 场景二：父级盒子中的图片无法居中 -->
<!-- 解决垂直居中：为 img 标签添加 vertical-align: middle; -->
<!-- 解决水平居中：为父级 father 添加 text-align: center; （因为浏览器认为图片是个文字） -->
<head>
    <style>
        .father {
            width: 400px;
            height: 400px;
            background-color: pink;
            line-height: 400px;
        }
    </style>
</head>
<body>
    <div class="father">
    	<img src="./images/1.jpg" alt="">
    </div>
</body>
```

2. **光标类型 cu**

设置鼠标光标在元素上时的显示的样式。

属性名：**cursor**

属性值：默认为鼠标光标

| 属性值  |            效果            |
| :-----: | :------------------------: |
| pointer |  小手效果，提示用户可点击  |
|  text   | 工字型，提示用户可选择文字 |
|  move   | 十字光标。提示用户可以移动 |

```html
<head>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div>div</div>
</body>
```

3. **边框圆角 bd - rd**

让盒子四角变圆润，提升用户体验

属性名：**border-radius**

取值：数字+px（取值为圆角的半径）、百分比，（最多链接四个值，按左上角顺时针作用，单值会作用四个角）

```html
<head>
    <style>
        .box {
            margin: 50px auto;
            width: 50px;
            height: 50px;
            background-color: pink;

            border-radius: 10px;
        }
    </style>
</head>
<body>
    <div class="box"></div>
</body>
```

边框圆角的应用：

- **让盒子变圆形：**要求盒子必须是正方形，且 border-radius 取值为盒子宽高的一半。
- **胶囊按钮：**要求盒子是长方形，且 border-radius 取值为盒子高度的一半。

4. **溢出部分显示效果 ovh**

控制内容**溢出的部分**的显示效果。

属性名：**overflow**

属性值：

|   属性值   |                效果                |
| :--------: | :--------------------------------: |
|  visible   |       默认值，溢出部分不可见       |
| **hidden** |          **溢出部分隐藏**          |
|   scroll   |     无论是否溢出，都显示滚动条     |
|    auto    | 根据是否溢出，自动显示或隐藏滚动条 |

5. **元素本身隐藏 dp**

让元素本身在屏幕中不可见，如鼠标:hover之后元素隐藏。

常见属性：**占位隐藏** visibility: hidden;（不常用）与 **不占位隐藏** display: none;

```html
<head>
    <style>
        div {
            width: 100px;
            height: 100px;
        }
        .one {
            /* 消失了但没完全消失，原本的位置变成空白 */
            /* visibility: hidden; */
            
            /* 工作中常用，好像从来不存在 */
            display: none;
            background-color: pink;
        }
        .two {
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="one"></div>
    <div class="two"></div>
</body>
```

**不占位隐藏 display: none; 可搭配 :hover 实现隐藏后鼠标悬停显示隐藏内容，只需在 :hover 里写 display: block;（非none都可） 即可。**

6. （拓展）元素整体透明度

让元素整体（包括内容）一起变透明

属性名：opacity，属性值：0~1之间的数字（0表示完全透明）

**该属性通常搭配 js 使用。**

---

## 综合案例 1 - 内容

效果：

![](./图片\综合案例1.png)

代码实现：

```html
<head>
    <title>Document</title>
    <style>
        div {
            width: 600px;
            height: 600px;
            margin: 0 auto;
        }
        .center {
            text-align: center;
        }
        .color1 {
            color: #808080;
        }
        .color2 {
            color: #87ceeb;
            font-weight: 700;
            /* 取值700表示加粗 */
        }
        a {
            text-decoration: none;
        }
        .indent {
            text-indent: 2em;
        }
    </style>
</head>
<body>
    <div>
        <h1 class="center">马里奥是谁</h1>
        <p class="center">
            <span class="color1">2077年1月1日</span>
            <span class="cloor2">马嬲科技</span>
            <a href="#">收藏本文</a>
        </p>
        <hr>
        <p class="indent">马力欧（早年常译作马里奥）是游戏《马力欧系列》中的角色。在《超级马力欧兄弟》中，他靠吃蘑菇变成超级马力欧，特征是大鼻子、头戴帽子、身穿背带裤，还留着胡子。与他的双胞胎兄弟路易吉一起，长年担任任天堂的招牌角色。在任天堂官方网页的标签图片上就是FC时代的马力欧。</p>
    </div>
</body>
</html>
```

---

## 综合案例 2 - 表格

效果：

![](./\图片\综合案例2.png)

代码实现：

```html
<head>
    <style>
        h2 {
            text-align: center;
        }
        table {
            /* 合并相邻边框 */
            border-collapse: collapse;
            height: 80px;
            margin: 0 auto;
            text-align: center;
        }
        th {
            padding: 5px 30px;
        }
        table, th, td {
            border: 1px solid #000;
        }
    </style>
</head>
<body>
    <h2>订单确认</h2>
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
            <td>1999</td>
            <td>10</td>
            <td>19990</td>
            <td>香港</td>
        </tr>
    </table>
</body>
```

这里数据写死了，转到 js 篇

---

## 综合案例 3 - 导航

效果：

![](./图片\综合案例3.png)

代码实现：

```html
<head>
    <style>
        a {
            text-decoration: none;
            /* a标签是行内元素，宽高不生效，需要转显示模式 */
            width: 100px;
            height: 50px;
            background-color: blue;
            color: white;
            text-align: center;
            line-height: 50px;
            display: inline-block;
        }
        /* 鼠标悬停变橙色 */
        a:hover {
            background-color: orange;
        }
    </style>
</head>
<body>
    <!-- a{导航$}*5 -->
    <!-- 按住Alt键 或 Alt+shift 都可以选中多处 -->
    <a href="#">导航1</a>
    <a href="#">导航2</a>
    <a href="#">导航3</a>
    <a href="#">导航4</a>
    <a href="#">导航5</a>
</body>
```

效果2：

![](./图片\综合案例3-2.png)

代码实现：

```html
<head>
    <style>
        .bg1 {
            background-image: url(./images/bg1.png);
        }
        .bg2 {
            background-image: url(./images/bg2.png);
        }
        .bg3 {
            background-image: url(./images/bg3.png);
        }
        .bg4 {
            background-image: url(./images/bg4.png);
        }
        .bg1:hover {
            background-image: url(./images/bg5.png);
        }
        .bg2:hover {
            background-image: url(./images/bg6.png);
        }
        .bg3:hover {
            background-image: url(./images/bg7.png);
        }
        .bg4:hover {
            background-image: url(./images/bg8.png);
        }
        a {
            width: 120px;
            height: 58px;
            display: inline-block;
            line-height: 50px;
            text-align: center;
            color: white;
            text-decoration: none;
        }
    </style>
</head>
<body>
    <a class="bg1" href="#">五彩导航</a>
    <a class="bg2" href="#">五彩导航</a>
    <a class="bg3" href="#">五彩导航</a>
    <a class="bg4" href="#">五彩导航</a>
</body>
```

效果3：采用盒子模型，**从外向内，先宽高背景色，再调解内容位置颜色**，

![](./图片\综合案例3-3.png)

代码实现：

```html
<head>
    <title>Document</title>
    <style>
        .box {
            height: 40px;
            border-top: 3px solid #ff8500;
            border-bottom: 3px solid #edeef0;
            text-decoration: none;
        }
        .box a {
            width: 80px;
            height: 40px;
            /* background-color: #edeef0; */
            /* 这里建议先加上背景色，方便修改文字细节，最后再删去 */
            display: inline-block;
            text-align: center;
            line-height: 40px;
            text-decoration: none;
            font-size: 12px;
            color: #4c4c4c;
        }
        .box a:hover {
            background-color: #edeef0;
            color: #ff8400;
        }
    </style>
</head>
<body>
    <div class="box">
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
        <a href="#">新浪导航</a>
    </div>
</body>
```

效果4：网页的主导航（正式）

![](./图片\综合案例3-4.png)

代码实现：

```html
<head>
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .nav {
            margin: 50px auto;
            width: 640px;
            height: 50px;
            background-color: #ffc0cb;
        }
        ul {
            list-style: none;
        }
        .nav li {
            float: left;
        }
        .nav li a {
            display: block;
            /* 这里block没有独占一行，因为父级li浮动了 */
            width: 80px;
            height: 50px;

            text-align: center;
            line-height: 50px;

            color: white;
            text-decoration: none;
        }
        .nav li a:hover {
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="nav">
        <!-- 主导航的结构是li里面嵌套a -->
        <ul>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
            <li><a href="#">新闻</a></li>
        </ul>
    </div>
</body>
```

---

## 综合案例 4 - 新闻

效果：

![](./图片\综合案例4.png)

细节1：**list-style: none;** 取消列表前的符号

细节2：用列表ul嵌套li嵌套a链接作为习惯。

细节3：**line-height 取1**即为一倍，字号的大小。

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        .news {
            /* 规定盒子内容 */
            width: 500px;
            height: 400px;
            border: 1px solid #ccc;
            /* 发现内容不对，添加样式 */
            margin: 50px auto;
            padding: 42px 30px 0;
        }
        .news h2 {
            border-bottom: 1px solid #ccc;
            font-size: 30px;
            line-height: 1;
            padding-bottom: 9px;
        }
        /* 去掉列表前的符号 */
        ul {
            list-style: none;
        }
        .news li {
            /* 规定盒子内容 */
            height: 50px;
            border-bottom: 1px dashed #ccc;
            /* 调节文字细节 */
            padding-left: 28px;
            line-height: 50px;
        }
        .news a {
            text-decoration: none;
            color: #666;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="news">
        <h2>最新文章/New Articles</h2>
        <!-- ul>li>a -->
        <ul>
            <li><a href="#">新闻内容1</a></li>
            <li><a href="#">新闻内容2</a></li>
            <li><a href="#">新闻内容3</a></li>
            <li><a href="#">新闻内容4</a></li>
            <li><a href="#">新闻内容5</a></li>
        </ul>
    </div>
</body>
```

---

## 综合案例 5 - 左右结构

效果：

![](./图片\综合案例5.png)

代码实现：

```html
<head>
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .box {
            margin: 0 auto;
            width: 1226px;
            height: 614px;
            /* background-color: pink; */
        }
        .left {
            float: left;
            width: 234px;
            height: 614px;
            background-color: #800080;
        }
        .right {
            float: right;
            width: 978px;
            height: 614px;
            /* background-color: green; */
        }
        ul {
            /* 去除列表符号 */
            list-style: none;
        }
        .right li {
            float: left;
            margin-right: 14px;
            margin-bottom: 14px;
            width: 234px;
            height: 300px;
            background-color: #87ceeb;
        }
        /* 如果父级宽度不够，子级会自动换行 */
        .right li:nth-child(4n) {
            margin-right: 0;
        }
    </style>
</head>
<body>
    <div class="box">
        <div class="left"></div>
        <div class="right">
            <ul>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
            </ul>
        </div>
    </div>
</body>
```

---

## 综合案例 6 - banner 定位

效果：透明遮蔽效果。

![](./图片\综合案例6.png)

代码实现：

```html
<head>
    <style>
        .banner {
            position: relative;
            margin: 0 auto;
            width: 600px;
            height: 600px;
        }
        .mask {
            position: absolute;
            left: 0;
            bottom: 0;
            /* 如果子级和父级的宽度相同，可以把宽度写为 100%  */
            width: 100%;
            height: 150px;
            background-color: rgba(0,0,0, .5);
        }
    </style>
</head>
<body>
    <div class="banner">
        <img src="../images/2.jpg" alt="">
        <!-- 遮罩 -->
        <div class="mask"></div>
    </div>
</body>
```

---

## 综合案例 7 - 渲染柱形图

【目前不会，学完 flex 布局再来】

效果：

![](./\图片\综合案例7.png)

代码实现：

```html
<head>
	<style>
        * {
            margin: 0;
            padding: 0;
        }
        .box {
            display: flex;
            width: 700px;
            height: 300px;
            border-left: 1px solid pink;
            border-bottom: 1px solid pink;
            margin: 50px auto;
            justify-content: space-around;
            align-items: flex-end;
            text-align: center;
        }
        .box > div {
            display: flex;
            width: 50px;
            background-color: pink;
            flex-direction: column;
            justify-content: space-between;
        }
        .box div span {
            margin-top: -20px;
        }
        .box div h4 {
            margin-bottom: -35px;
            width: 70px;
            margin-left: -10px;
        }
	</style>
</head>
<body>
    <div class="box">
        <div style="height: 123px;">
            <span>123</span>
            <h4>第1季度</h4>
        </div>
        <div style="height: 156px;">
            <span>156</span>
            <h4>第2季度</h4>
        </div>
        <div style="height: 120px;">
            <span>120</span>
            <h4>第3季度</h4>
        </div>
        <div style="height: 210px;">
            <span>210</span>
            <h4>第4季度</h4>
        </div>
    </div>
</body>
```

