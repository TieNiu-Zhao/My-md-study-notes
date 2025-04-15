# Flutter 学习

## 技巧

1. 使用 cursor 编辑器时，选中想要 Center( ) 的代码时没有小灯泡，需要按下 cmd + .
2. 新建 dart 文件时，快速生成结构可以输入 stl 并选择弹出菜单 Flutter Stateless Widget 生成无状态组件模板、输入 stf 生成状态组件模板。

## 逗号配置

flutter_lint 会强制写的逗号删掉，在结构上可读性很差，需要修改配置文件

- analysis_options.yaml

  ```dart
  include: package:flutter_lints/flutter.yaml
  
  linter:
    rules:
      prefer_const_constructors: false
      prefer_final_fields: false
      use_key_in_widget_constructors: false
      prefer_const_literals_to_create_immutables: false
      prefer_const_constructors_in_immutables: false
      avoid_print: false
  ```

- pubspec.yaml

  ```dart
  name: namer_app
  description: A new Flutter project.
  
  publish_to: "none" # Remove this line if you wish to publish to pub.dev
  
  version: 0.0.1+1
  
  environment:
    sdk: ">=2.19.4 <4.0.0"
  
  dependencies:
    flutter:
      sdk: flutter
  
    english_words: ^4.0.0
    provider: ^6.0.0
  
  dev_dependencies:
    flutter_test:
      sdk: flutter
  
    flutter_lints: ^2.0.0
  
  flutter:
    uses-material-design: true
  ```

  这样改完就可以添加逗号了。

## appBar 顶部栏

- 使用方法

  ```dart
  appBar: AppBar(
    backgroundColor: Colors.deepPurple[500],
    title: Text(
      '顶部标题',
      style: TextStyle(
        color: Colors.white,
      ),
    ),
    leading: Icon(											// 顶部左侧图标
      Icons.menu,
      color: Colors.white,
    ),
    actions: [													// 顶部右侧图标
      IconButton(
        onPressed: () {},
        icon: Icon(
          Icons.logout,
          color: Colors.white,
        ),
      ),
    ],
  ),
  ```

## Row / Column 行列对齐（flex）

- 对齐方式

  对应 flex 的 justify 与 align

  这里是列，主轴方向就是从上到下。后面的 spaceEvenly 和前端一样

  ```dart
  body: Column(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly, // 主轴对齐方式
    crossAxisAlignment: CrossAxisAlignment.center, // 横轴对齐方式
    children: [
      child: Container(
        width: 500,
        height: 200,
        color: Colors.blue[100],
      ),
      child: Container(
        width: 300,
        height: 200,
        color: Colors.blue[200],
      ),
      child: Container(
        width: 100,
        height: 200,
        color: Colors.blue[400],
      ),
    ],
  ),
  ```

- 铺满 **Expanded**

  对应 flex 的 flex: 1

  没设置宽高的话就是自动填充。

  ```dart
  body: Column(
    children: [
      Expanded(
        child: Container(
          color: Colors.blue[100],
        ),
      ),
      Expanded(
        flex: 2,
        child: Container(
          color: Colors.blue[200],
        ),
      ),
      Expanded(
        child: Container(
          color: Colors.blue[400],
        ),
      )
    ],
  ),
  ```


## LIstView 列表视图

类似于 web 里的 v-for 渲染 ul 列表，又像 overflow-scroll

- 超出宽度 => 滚动 ListView

  ```dart
  body: Column(
    children: [
      Container(
        height: 400,
        color: Colors.blue[100],
      ),
      Container(
        height: 400,
        color: Colors.blue[200],
      ),
      Container(
        height: 400,
        color: Colors.blue[400],
      ),
    ],
  ),
  ```

  列表内容器高度已经超过了屏幕高度，会导致最下面的盒子显示溢出，解决办法是开启滚动，将 Column 改为 **ListView**，默认滚动方向为垂直，可以手动改成水平。

  ```dart
  body: ListView(
    scrollDirection: Axis.horizontal,				// 水平滚动开关
    children: [
      Container(
        height: 400,
        color: Colors.blue[100],
      ),
      Container(
        height: 400,
        color: Colors.blue[200],
      ),
      Container(
        height: 400,
        color: Colors.blue[400],
      ),
    ],
  ),
  ```

- **ListView.builder( )**

  生成滚动列表

  ```dart
  body: ListView.builder(
    itemCount: 10,
    itemBuilder: (context, index) => ListTile(
      title: Text(index.toString()),
    ),
  ),
  ```

  当然也可以根据数组来生成有特定内容的列表

  ```dart
  class MyApp extends StatelessWidget {
    MyApp({super.key});
  
    List names = ['name1', 'name2', 'name3'];
  
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          body: ListView.builder(
            itemCount: names.length,
            itemBuilder: (context, index) => ListTile(
              title: Text(names[index]),
            ),
          ),
        ),
      );
    }
  }
  ```

## GridView 网格视图

类似于 web 里的 grid 布局

- 渲染 gird

  ```dart
  body: GridView.builder(
    itemCount: 64,																													// grid 元素总数
    gridDelegate:										
        SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 4),				// 每行有多少个
    itemBuilder: (context, index) => Container(
      color: Colors.deepPurple,
      margin: EdgeInsets.all(2),
    ),
  ),
  ```

## Stack 堆栈（position）

类似于绝对定位

- 绝对定位

  ```dart
  body: Stack(
    alignment: Alignment.bottomRight,						// 以右下角绝对定位
    children: [
      Container(																// 大容器
        width: 300,
        height: 300,
        color: Colors.deepPurple,
      ),
      Container(																// 中等容器
        width: 200,
        height: 200,
        color: Colors.deepPurple[400],
      ),
      Container(																// 小容器
        width: 100,
        height: 100,
        color: Colors.deepPurple[200],
      ),
    ],
  ),
  ```

## GestureDetector 手势检测

类似于 vue 里的 @click

- 使用方法

  ```dart
  body: Center(
    child: GestureDetector(
      onTap: () => {
        print('用户点击了屏幕'),
      },
      child: Container(
        width: 300,
        height: 300,
        color: Colors.deepPurple[300],
        child: Center(
          child: Text('Click me!'),
        ),
      ),
    ),
  ),
  ```

## Navigator 路由

- 单一路由跳转

  main.dart

  ```dart
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: FirstPage(),											// 进入首页
    );
  }
  ```

  pages / first_page.dart

  ```dart
  import 'package:flutter/material.dart';
  import 'package:namer_app/pages/second_page.dart';
  
  class FirstPage extends StatelessWidget {
    const FirstPage({super.key});
  
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.deepPurple,
          title: Text('app'),
        ),
        body: Center(
          child: ElevatedButton(
            child: Text('Go to Second Page'),
            onPressed: () {
              // 点击跳转到第二页
              Navigator.push(
                context,
                MaterialPageRoute(						// 从右向左滑入动画
                  builder: (context) => SecondPage(),
                  // fullscreenDialog: true,  // 以 ios 模态风格打开
                ),
              );
            },
          ),
        ),
      );
    }
  }
  ```

- 路由配置

  有多个路由时，使用 routes 配置

  main.dart

  ```dart
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: FirstPage(),
      routes: {
        '/firstpage': (context) => FirstPage(),
        '/secondpage': (context) => SecondPage()
      },
    );
  }
  ```

  first_page.dart

  ```dart
  return Scaffold(
    appBar: AppBar(
      backgroundColor: Colors.deepPurple,
      title: Text('app'),
    ),
    body: Center(
      child: ElevatedButton(
        child: Text('Go to Second Page'),
        onPressed: () {
          // 使用 pushNamed
          Navigator.pushNamed(context, '/secondpage');
        },
      ),
    ),
  );
  ```

- 带 Drawer 的路由跳转

  Drawer 跳转后，点击页面返回按钮返回时 Drawer 还是打开的，所以要 Navigator.pop( ) 一下。

  ```dart
  drawer: Drawer(
    backgroundColor: Colors.deepPurple[300],
    child: Column(
      children: [
        DrawerHeader(
          child: Icon(
            Icons.favorite,
            size: 48,
          ),
        ),
        ListTile(
          leading: Icon(Icons.home),
          title: Text('首页'),
          onTap: () {
            // 必须有pop，不然点击返回到firstpage时抽屉是打开的
            Navigator.pop(context);
            Navigator.pushNamed(context, '/home');
          },
        ),
        ListTile(
          leading: Icon(Icons.settings),
          title: Text('设置'),
          onTap: () {
            Navigator.pop(context);
            Navigator.pushNamed(context, '/settings');
          },
        ),
      ],
    ),
  ),
  ```

## bottomNavigationBar 底部栏

- 配置方法

  ```dart
  import 'package:namer_app/pages/home.dart';
  import 'package:namer_app/pages/profile.dart';
  import 'package:namer_app/pages/settings.dart';
  
  class FirstPage extends StatefulWidget {
    FirstPage({super.key});
  
    @override
    State<FirstPage> createState() => _FirstPageState();
  }
  class _FirstPageState extends State<FirstPage> {
    // 切换下标
    int _selectedIndex = 0;
  	// 切换方法，修改状态
    void _navigateBottomBar(int index) {
      setState(() {
        _selectedIndex = index;
      });
    }
  	// 页面数组
    final List _pages = [
      Home(),
      Profile(),
      Settings(),
    ];
  
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          backgroundColor: Colors.deepPurple,
          title: Text('app'),
        ),
        body: _pages[_selectedIndex],
        bottomNavigationBar: BottomNavigationBar(
          // 绑定下标、onTap 和 items
          currentIndex: _selectedIndex,
          onTap: _navigateBottomBar,
          items: [
            BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: 'Home',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.person),
              label: 'Profile',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.settings),
              label: 'Settings',
            ),
          ],
        ),
      );
    }
  }
  ```

## 状态组件

- 计数器示例

  ```dart
  import 'package:flutter/material.dart';
  
  class CounterPage extends StatefulWidget {
    const CounterPage({super.key});
  
    @override
    State<CounterPage> createState() => _CounterPageState();
  }
  
  class _CounterPageState extends State<CounterPage> {
    int _counter = 0;
  
    void _incrementCounter() {
      setState(() {
        _counter++;
      });
    }
  
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('你点击了按钮多少次：'),
              Text(
                _counter.toString(),
                style: TextStyle(fontSize: 40),
              ),
              ElevatedButton(
                onPressed: _incrementCounter,
                child: Text('+'),
              ),
            ],
          ),
        ),
      );
    }
  }
  ```

  