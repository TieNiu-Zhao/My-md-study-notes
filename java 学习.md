# javaSE 学习

---

## 基础知识

编译 → 运行

```java
public class Hello{
	public static void main(String[] args){		//输入psvm
        System.out.println("Hello World");		//输入sout
    }
}
```

**编译与解释**：

- 中文书翻译成英文书（编译型：要求速度、C/C++）

- 中文书 → 翻译官 → 英文书（解释型：不要求速度、预编译、如 JavaScript）

- java 是先编译后解释

**注释**

- 注释颜色等更改：Settings→Editor→Color Scheme→Java→Comments

- 除了单行多行注释还有文档注释，格式为：/\*\* \*/（可识别参数、了解）

---

### Java 数据类型

**Java 数据类型分为基本类型和引用类型**

- 基本类型：数值（整数、浮点、字符）、boolean

- 引用类型：类、接口、数组

```java
public static void main(String[] args) {
	//八大基本数据类型
    //整数
    int num = 10;
    byte num2 = 127;    //byte最大为127
    short num3 =30;
    long num4 = 30L;    //long在后面加数字L用于区分
    //小数
    float num5 = 50.1F;  //float后面加F用于区分
    double num6 = 5.315466457;
    //字符
    char name = 'a';
    //字符串不是关键字，是类
    String namea = "土拨";
    //布尔
    boolean flag = true;
}
```

**转义字符**

- \t 制表符

- \n 换行符

### 运算符

**自增自减**

```java
int a = 3;
int b = a++;    	//执行完这行代码前，先给b赋值，再自增
System.out.println(b);		//b = 3
a = 3;
int c = ++a;    	//执行这行代码前，先自增，再给b赋值
System.out.println(c);		//c = 4
```

**字符串连接符**

- 只要 + 左右有字符串，就把所有字符串后面的 + 转换成字符串连接

```java
int a = 10;
int b = 20;
System.out.println(""+a+b);		//输出为：3020
System.out.println(a+b+"");		//输出为：30
```

**三元运算符**

```java
x ? y : z;		//如果x==true，则结果为y，否则结果为z
```

---

## 流程控制

---

### Scanner 类

- Java 提供了一个工具类 Scanner，可以获取用户的输入

```Java
Scanner s = new Scanner(System.in);
```

- 通过 Scanner 类的 next() 与 nextLine() 方法获取输入的字符串，再读取前一般需要使用 hasNext() 与 hasNextLine() 判断是否还有输入的数据。

**（1）使用 next 方式接收（以空格为结束符）**

```Java
public static void main(String[] args) {
	//创建一个扫描器对象，接收键盘数据
    Scanner scanner =new Scanner(System.in);
    System.out.println("使用next方式接收：");
    //判断用户有没有输入字符串
    if(scanner.hasNext()){
        //使用next方式接收
        String str = scanner.next();
        System.out.println("输出的内容为："+str);
    }
    scanner.close();
    //所有IO流的类不及时关会一直占用资源，随用随关
    }
```

- **以上代码执行完输入 hello world 后输出结果只有 hello**

**（2）使用 nextLine 方式接收（以回车为结束符）（常用）**

```Java
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    System.out.println("请输入数据：");
    if(scanner.hasNextLine()){
        String str = scanner.nextLine();
        System.out.println("输出的内容为："+str);
    }
    scanner.close();
}
```

- **以上代码执行完输入 hello world 后输出结果为 hello world**

**（3）hasNextFloat：下一行是否为浮点数**

```Java
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    int i = 0;
    float f = 0.0f;
    System.out.println("请输入小数：");
    //是否还有下一个小数
    if(scanner.hasNextFloat()){
        f = scanner.nextFloat();
        System.out.println("小数数据：" + f);
    }else{
        System.out.println("输入的不是小数数据！");
    }
    scanner.close();
}
```

---

### If 选择结构

```java
public static void main(String[] args) {
	Scanner scanner = new Scanner(System.in);
	System.out.println("请输入内容：");
	String s = scanner.nextLine();
	//equals：判断字符串是否相等（字符串判断不要用==）
	if (s.equals("Hello")){
        System.out.println(s);
    }
    System.out.println("End");
    scanner.close();
}
```

if-else 略。

---

### switch 选择结构

- switch-case 多选择结构，可用来匹配一个值。
- Java SE 7 开始，switch 支持字符串（将字符串转为哈希值判断）

```java
public static void main(String[] args) {
    String name = "丁真";
    switch (name){
        case "蔡徐坤":
            System.out.println("蔡徐坤");
            break;
        case "丁真":
            System.out.println("丁真");
            break;
        case "马保国":
            System.out.println("马保国");
            break;
        default:
            System.out.println("是穿山甲吗？");
    }
}
```

---

## 循环结构

---

### while

```java
public static void main(String[] args) {
    //计算1加到100
    int i = 0;
    int sum = 0;
    while (i<=100){
        sum = sum + i;
        i++；
    }
    System.out.println(sum);
}
```

---

### do while

- 无论条件是否满足，语句至少执行一遍。

```java
public static void main(String[] args) {
    int i = 0;
    int sum = 0;
    do{
        sum = sum + i;
        i++;
    }while (i<=100);
    System.out.println(sum);
}
```

---

### for

- 初始化;条件判断;迭代（初始化步骤可为空）

- 输入**100.for**自动生成（i < 100 的循环）

- 或输入 **fori** 快速上生成 for 循环，再补全条件判断。

```java
public static void main(String[] args) {
    //0~100奇数和与偶数和
    int oddSum = 0;
    int evenSum = 0;
    for (int i = 0; i < 100; i++) {
        if(i%2!=0){
            oddSum+=i;
        }else{
            evenSum+=i;
        }
    }
    System.out.println("奇数的和："+oddSum);
    System.out.println("偶数的和："+evenSum);
}
```

```java
public static void main(String[] args) {
    //循环输出1~1000间被5整除的数，且每行输出三个
    for (int i = 1; i < 1000; i++) {
        if (i%5==0){
            System.out.print(i+"\t");   //print输出不会换行
        }
        if (i%15==0) {
            System.out.println();		//输出空行
        }
    }
}
```

```java
public static void main(String[] args) {
    //打印九九乘法表
    for (int j = 1; j <= 9; j++) {
        for (int i = 1; i <= j; i++) {
            System.out.print(i + "*" + j + "=" + (j * i)+"\t");
        }
        System.out.println();
    }
}
```

---

### 增强 for 循环

- 用于**数组**或**集合**的增强对象

```java
public static void test() {
    //遍历数组的元素
    int[] numbers = {10,20,30,40,50};
    /*
    for (int i = 0; i<5; i++) {
    	System.out.println(numbers[i]);
    }
    */
    for (int x:numbers){
        System.out.println(x);
    }//两组代码完全等价
}
```

---

### break-continue

- break 用于循环语句或 switch 语句，**用于跳出循环**。
- continue 用于终止**某次循环**过程。

```java
public static void test() {
    int i = 0;
    while(i<100){
        i++;
        if (i%10==0){
            System.out.println();
            continue;	//i是10的倍数时，会直接跳过，开始下一轮
        }
        System.out.print(i);
    }
}
```

- goto 仍为 Java 的一个关键字，但未得到正式使用，但 Java 有标签的用法：即在想跳回的语句前加上 outer，在 continue 后加上 outer 就会调试转到 outer 语句的位置。

---

## 方法

---

### 定义

- System 是一个类、out 是一个对象、println()是一个方法。

```java
System.out.println();
//调用系统类里面的标准输出对象out中的println()方法
```

Java 方法是语句的集合，他们在一起执行一个功能。

- 方法是解决一类问题的步骤的有序组合
- 方法包含于类或对象中
- 方法在程序中被创建，在其他地方被引用

方法设计原则：一个方法只完成一个功能，有利于后期拓展。（原子性）

```java
修饰符 返回值类型 方法名(参数类型 参数名){
    方法体
	return 返回值;
}
```

1. 修饰符：可选，告诉编译器如何调用该方法，定义了该方法的访问类型。
2. 返回值类型：方法可能会返回值，没有就为 void。
3. 方法名：需遵守命名规范开头字母小写，后续首字母大写。
4. 参数：可选，方法被调用时，传递值给参数，称为实参或变量，方法可以不含参数。**形参：**在方法被调用时接收外界输入的数据。**实参：**调用方法实际传给方法的数据。

```java
public static void main(String[] args) {
    int sum = add(1,2);					//add()中的1,2为实参
    System.out.println(sum);
}
public static int add(int a,int b){		//int a,int b为形参
    return a + b;
}
```

5. 若方法存在返回值，一定要通过 return 返回出去，void 则不用。return 还表示终止方法。

```java
public static int max(int num1,int num2){
    //求两数最大值
    int result = 0;
    if (num1==num2){
        System.out.println("num1==num2");
        return 0;		//终止方法
    }
    if (num1>num2){
        result = num1;
    }else {
        result = num2;
    }
    return result;
}
```

---

### 方法调用

调用方法：Java 有两种调用方法的方式，根据方法是否返回值来选择

```java
对象名.方法名(实参列表)
```

当方法返回一个值的时候，方法调用通常被当做一个值。

```java
int larger = max(30,40);
```

如果方法返回值是 void，方法调用一定是一条语句。

```java
System.out.println("Hello,World!");
```

---

### 方法重载

重载指在一个类中，有相同的函数名称，但形参不同的函数。

```java
public static int max(int a,int b){
	略;
}
public static double max(double a,double b){
    略;
}
```

上面两个代码除了返回值和形参不同，内部完全一致，方法名也一样，就是**方法重载**。

重载原则：

- 方法名必须相同，参数列表必须不同（个数不同、或类型不同、或参数排列按顺序不同）
- 返回值类型可相同可不同，仅仅返回值不同不足以成为方法的重载。

---

### 可变参数

不定项参数：不规定要传多少参数。

- 在方法声明中，在指定参数类型后加一个省略号(...)
- 一个方法只能有一个可变长参数，它必须是方法的最后一个参数，任何普通参数必须在他之前声明。

```java
public static void main(String[] args) {
    printMax(34,33,31,56.5,22);
    printMax(new double[]{1,2,3});
}
public static void printMax(double... numbers){
    //打印最大值（但不确定有多少传参）
    if (numbers.length == 0){
        System.out.println("No argument passed");
        return;
    }
    double result = numbers[0];
    //排序
    for (int i = 1; i < numbers.length; i++) {
        if (numbers[i] > result){
            result = numbers[i];
        }
    }
    System.out.println("The max valur is " + result);
}
```

---

### 递归

递归即方法自己调用自己。

- 递归头：必须有出口，如果没有将陷入死循环。
- 递归体：什么时候需要调用自身。

```java
public static void main(String[] args) {
    System.out.println(f(5));
}
public static int f(int n){
    //计算n!
    if(n==1) {
        return 1;
    }else {
        return n*f(n-1);
    }
}
```

---

## 数组

---

### 声明与创建

```java
int[] nums;     		//声明一个数组
nums = new int[10];      //创建数组，创建了空间，可存10个int类型数字
//nums[0] = 1;			给第0号元素赋值1
//array.length表示数组长度
int sum =0
for (int i = 0; i < nums.length; i++){
    sum = sum + nums[i];
}
System.out.println("总和为：" + sum);
```

1. **特点**

- 数组长度是确定的，一旦被创建，它的大小就不可改变。
- 它的元素必须是相同类型，不允许出现混合类型。
- 数组中的元素可以是任何数据类型，包括基本类型和引用类型。
- 数组变量属于引用类型，数组可以看成是对象，数组中每个元素相当于该对象的成员变量。（数组对象本身在堆中）

2. **内存分析**

```java
int nums；			   //在栈里压了一块空间。
nums = new int[10];		//new关键字在堆里，所以在堆里产生了一片十块的空间。
```

运行时出现错误：java.lang.ArrayIndexOutOfBoundsException 表示数组下标越界

3. **三种初始化**

```java
//静态初始化(大小不可改变)
int[] a = {1,2,3,4,5,6,7,8};
//动态初始化：包含默认初始化
int[] b = new int[10];
b[0] = 10;
```

数组是引用类型，它的元素相当于类的实例变量，因此数组一旦分配空间，其中每个元素也被按照实例变量同样的方式被**隐式初始化**（被赋默认值）。

---

### 数组使用

1. 增强 for 循环：适合打印输出，**没有数组下标**，jdk1.5 以上。

```java
int[] arrays = {1,2,3,4,5};
for (int array : arrays){
    System.out.println(array);
}
printArray(arrays);
```

2. 数组作为参数与数组作为返回值

```java
public static void main(String[] args) {
    int[] arrays = {1,2,3,4,5};
    int[] reverse = reverse(arrays);
    printArray(reverse);
}
//打印数组-数组作为方法入参
public static void printArray(int[] arrays){
    for (int i = 0; i < arrays.length; i++) {
        System.out.print(arrays[i]+" ");
    }
}
//反转数组-数组作为返回值
public static int[] reverse(int[] arrays){
    int[] result = new int[arrays.length];
    for (int i = 0,j = result.length-1; i < arrays.length; i++,j--) {
        result[j] = arrays[i];
    }
    return result;
}
```

---

### 多维数组

二维数组：数组的元素为数组，即数组的嵌套。

```java
//定义四行两列的数组
int[][] array = {{1,2},{2,3},{3,4},{4,5}};
//遍历二维数组元素
for (int i = 0; i < array.length; i++) {
    for (int j = 0; j < array[i].length; j++) {
        System.out.println(array[i][j]);
    }
}
```

---

### Arrays 类

- 数组的工具类 java.util.Arrays（了解即可）

```java
int[] a = {1,2,3,4,9999,312431,534,3,421,656,23};
//升序排序
Arrays.sort(a);
//打印数组元素
System.out.println(Arrays.toString(a));
//填充第2~4的数组元素
Arrays.fill(a,2,4,0);
System.out.println(Arrays.toString(a));
```

---

### 冒泡排序

- 简易版

```java
public static int[] BubbleSort(int[] array){
    int temp = 0;
    for (int i = 0; i < array.length-1; i++) {
        //若第一个数比第二个数大则两数交换
        for (int j = 0; j < array.length-1; j++) {
            if (array[j+1]<array[j]){
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
        }
    }
    return array;
}
```

- 优化版

```java
public static int[] BubbleSort(int[] array){
    int temp = 0;
    for (int i = 0; i < array.length-1; i++) {
        boolean flag = false;   	//通过标志位减少无意义的比较
        for (int j = 0; j < array.length-1; j++) {
            //每次比较交换后改变flag值
            if (array[j+1]<array[j]){
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                flag = true;
            }
        }
        //说明没有进行比较
        if (flag == false){
            break;
        }
    }
    return array;
}
```

---

## 面向对象编程

**面向对象编程**(Object-Oriented Programming,OOP)，其本质为**以类的方式组织代码，以对象的组织封装数据**。

**属性+方法**：将众多共同特性的方法提取出来加上属性就成为了一个类。

---

### 静态方法与非静态方法

- **静态方法：**若类 1 中存在的静态方法，就可以在类 2 中使用类 1 中的静态方法。

```java
public class X{
    public static void a{
        ...
    }
}
//可以在别的类中的main方法中使用X.a()来调用此方法
```

- **非静态方法：**若类 1 中的方法是非静态方法，可以使用 new 关键字将类实例化。

```java
public class X{
    public void a{
        ...
    }
}
//可以再别的类中使用 new X().a();	相当于创建了X类调用了a方法，但一般写为下面的形式
//对象类型 对象名 = 对象值；
//X x = new X1();
```

**[两种情形]**

两个非静态方法可以互相调用。

```java
public void a(){
    b();
}
public void b(){}
```

一个为静态方法时，静态方法中不能调用非静态方法。因为 **static 和类一起加载**，当类存在时，其中的静态方法就已经存在，而 b()与对象有关，当对象存在时方法才存在，所以**无法调用不存在的方法**，即**需要实例化**（需要 new）。

```java
public static void a(){
    b();	//此时无法调用b(),报错
}
public void b(){}
```

---

### 值传递与引用传递

java 为值传递，下面的例子 change() 方法内 a 为 10，回到主方法 a 仍是主方法中的值为 1 的 a

```java
public class Demo {
    public static void main(String[] args) {
        int a = 1;
        System.out.println(a);	//输出为1
        change(a);
        System.out.println(a);	//输出仍为1
    }
    public static int change(int a){
        a = 10;
        return a;
    }
}
```

引用传递：对象，但本质还是值传递

```java
public class Demo {
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.name);	//输出为null
        change(person);
        System.out.println(person.name);	//输出为土拨
    }
    public static void change(Person person){
//person是一个对象，它指向的是Person person = new Person();（一个具体的人，可以改变属性）
        person.name = "土拨";
    }
}
//定义了一个person类，有一个属性name
class Person{
    String name;    //默认值为null
}
```

---

### 类与对象的关系

类是一种抽象的数据类型，它是对某一类事物的整体描述/定义，但**不能够代表某一个具体事物**。

对象是抽象概念的具体实例，类：人，对象：张三

- **使用 new 关键字创建对象！**除了**分配内存空间**外，还会给创建好的对象进行**默认的初始化** 以及 **对类中构造器的调用**。

```java
public class Student {		//Student.java
    //属性：字段
    String name;
    int age;
    //方法
    public void study(){
        System.out.println(this.name+"在学习");
    }
}
public class Application {		//Application.java
    //一个项目应该只存在一个main方法
    public static void main(String[] args) {
        //类：抽象的,实例化后会产生返回结果
        //student对象就是Student类的具体实例
        Student xiaoming = new Student();
        Student gouzi = new Student();
        xiaoming.name = "小明";
        xiaoming.age = 3;
    }
}
```

---

### 构造器

一个类即便什么都不写，它也会存在一个方法，这个方法就是构造方法。（类中不写会自动在在同名文件的.class 中生成空方法）

1. 特点

- 必须**和类的名字相同**
- 必须**没有返回值**，也不能写 void

2. 作用

- 使用 new 关键字，**必须要有构造器**，**new 关键字本质是在调用构造器**。
- 构造器**一般用来初始化值**。
- 有参构造：一旦定义了有参构造，若想调用无参构造，原本的无参构造就必须显式定义（空定义），否则调用就报错。
- 快捷键 Alt + Insert 快速生成构造器。
- this.表示当前类

```java
public static void main(String[] args) {	//Application.java
    Person person = new Person();
    System.out.println(person.name);
}
public class Person {		//person.java
    String name;
    public Person() {
    }
    public Person(String name) {
        this.name = name;		//this。name指这个类中的name
    }
}
```

---

### 封装（private，get 与 set）

**private** 将数据中的属性隐藏起来，禁止直接访问一个对象中的数据的实际表示，而通过操作接口来访问。

封装可以提高程序安全性，保护数据，隐藏代码的实现细节，统一接口，提高系统可维护性。

- 使用快捷键 Alt + Insert 后选择 getter and setter 快速生成 get / set

```java
public class Student {
    private String name;//名字
    private int id;//学号
    private char sex;//性别

    //需要提供一些可以操作这些属性的方法
    //提供一些public的get、set方法
    public String getName(){
        return this.name;
    }
    public void setName(String name){
        this.name = name;
    }
}
public class Application {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.setName("土拨");
        System.out.println(s1.getName());
    }
}
```

---

### 继承（extends , super , 重写 与 多态）

1. **extends**

继承的本质是对某一批类的抽象，比如动物这个大类下有灵长类动物类。继承是类和类之间的一种关系，除此之外，类和类之间的关系还有依赖、组合、聚合等。

- **子类继承父类，就会拥有父类的全部方法。**
- 快捷键 Ctrl + H 打开继承树
- 在 Java 中，所有的类都默认继承 Object 类，且 Java 只有单继承，没有多继承。（一个爸爸可以有多个儿子，但一个儿子不能有多个爸爸）

```java
public class Person {//父类
    private int money = 10_0000_0000;
    public void say(){
        System.out.println("说了一句话");
    }
    public int getMoney() {
        return money;
    }
}
public class Student extends Person{}//子类，继承父类
public class Application {
    public static void main(String[] args) {
        Student student = new Student();
        student.say();//输出：说了一句话
        System.out.println(student.getMoney());//输出1000000000
    }
}
```

2. **super**

与**this.**对应，子类继承父类后，使用**super.**调用父类的方法，使用**this.**调用本类的属性，且**this.**没有继承也能使用而**super.**要有继承条件才能使用。

- **super() 调用父类的构造方法，必须在构造方法的第一行**
- super() 必须只能出现在子类的方法或者构造方法中
- **super() 和 this()不能同时调用构造方法！**

```java
public class Person {
    public Person() {//无参构造器
        System.out.println("Person无参构造执行了");
    }
    protected String name = "tubo_dad";
    public void print(){
        //若这里的public为private，则无法调用，私有无法被继承
        System.out.println("Person");
    }
}
public class Student extends Person{
    public Student() {
        //隐藏代码super：这里默认调用了父类的无参构造
        //调用父类的构造器必须要在子类的第一行
        System.out.println("Student无参构造执行了");
    }
    private String name = "tubo_son";
    public void print() {
        System.out.println("Student");
    }
    public void test1(){
        print();//Student
        this.print();//Student
        super.print();//Person
    }
    public void test2(String name){
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }
}
public class Application {
    public static void main(String[] args) {
        Student student = new Student();
        student.test1();
        student.test2("tubo");
    }
}
```

运行结果为：

```java
Person无参构造执行了//new Student()>调用了Student构造器>调用了父类Person构造器
Student无参构造执行了
Student//test1中的print()
Student//test1中的this.print()，以上两个语句是等价的
Person//super调用了父类的print()方法
tubo
tubo_son
tubo_dad
```

3. **方法重写**

**重写指重写非静态方法，需要有继承关系。**

**子类重写父类的方法，和属性无关，和静态方法无关。且方法名、参数列表必须相同。**

子类方法和父类方法必须一致，但里面的方法体不同。

为什么和方法重写和静态方法无关？因为静态方法一开始就加载出来了。

**重写时修饰符的范围可以扩大，但不可以缩小。**如 private 可以重写 public（修饰符范围大小关系：public > proteted > Default > private）

重写抛出的异常范围可以被缩小，但不能被扩大。如 ClassNotFoundException < Exception

```java
public class B {
    public static void test(){//静态方法
        System.out.println("B=>test()");
    }
}
public class A extends B{
    public static void test() {//静态方法
        System.out.println("A=>test()");
    }
}
public class Application {
    public static void main(String[] args) {
        //方法的调用只和左边定义的数据类型有关
        A a = new A();
        a.test();//调用A类的方法

        //父类的引用指向了子类
        B b = new A();
        b.test();//调用B类的方法
    }
}
```

删去 A 与 B 类的 static 关键字，将 A 类下原内容删除后使用 **Alt + insert** 出现**方法重写**，默认调用了父类的 test()，重写为 System.out.println("A=>test()")后运行程序结果发生了变化。

```java
public class B {
    public void test(){
        System.out.println("B=>test()");
    }
}
public class A extends B{
    //Override 重写
    @Override//注解：有功能的注释
    public void test() {
        System.out.println("A=>test()");
    }
}
public class Application {
    public static void main(String[] args) {
        A a = new A();
        a.test();//输出A=>test()
        //父类的引用指向了子类
        B b = new A();//子类重写了父类的方法
        b.test();//输出A=>test()
    }
}
```

结论：

- 若方法为 **static 静态方法**，使用 new 关键字时，它的**结果只和最左边的类有关。**
- 对象能执行那些方法，主要看左边的类型，和右侧关系不大。
- **只有非静态方法才能重写**
- 应用场景：父类的功能，子类不一定需要或不一定满足，需要重写。
- 不能重写的方法：static 方法（属于类，它不属于实例）、final 常量（被 final 修饰就无法被重写）、private 方法。

4. **多态**

多态即**同一方法可根据发送对象不同可以采取不同的行为方式**。多态是指**方法多态**，属性没有多态性。需要有继承关系。

**一个对象的实际类型是确定的**，如 new Student() 一定是 Student 类，但**可以指向的引用类型是不确定的**。

```java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person {
    @Override
    public void run() {
        System.out.println("son");
    }
}
public class Application {
    public static void main(String[] args) {
        Student s1 = new Student();
        Person s2 = new Student();//父类的引用指向子类的类型
        Object s3 = new Student();//祖宗类的引用指向子类的类型
        //若子类重写了父类的方法，那么执行子类的方法
        s2.run();//输出son
        s1.run();//输出son
    }
}
```

结论：

- 父类与子类间需有联系。两种无联系的类无法互相转化，比如 Student 类无法转为 String 类，会报类型转换异常 ClassCostException !
- **多态存在条件：**继承关系，方法需要重写，父类引用指向子类对象 即 **father f1 = new son();**

---

### instanceof 关键字 与 类型转换

1. **instanceof**

instanceof 用来判断两个类之间**是否存在继承关系（没有继承关系就编译报错）**

```Java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person{}
public class Teacher extends Person{}
public class Application {
    public static void main(String[] args) {
        public static void main(String[] args) {
        //Object > String
        //Object > Person > Student
        //Object > Person > Teacher
        Object object = new Student();
        System.out.println(object instanceof Student);//true
        System.out.println(object instanceof Person);//true
        System.out.println(object instanceof Object);//true
        System.out.println(object instanceof Teacher);//false
        System.out.println(object instanceof String); //false
        System.out.println("===================================");
        Person person = new Student();
        System.out.println(person instanceof Student);//true
        System.out.println(person instanceof Person);//true
        System.out.println(person instanceof Object);//true
        System.out.println(person instanceof Teacher);//false
        //System.out.println(person instanceof String); //编译报错
        System.out.println("===================================");
        Student student = new Student();
        System.out.println(student instanceof Student);//true
        System.out.println(student instanceof Person);//true
        System.out.println(student instanceof Object);//true
        //System.out.println(student instanceof Teacher);//编译报错
    }
    }
}
```

2. **类型转换**

基本类型转换满足：从低转高（如 32 位转 64 位），从高转低需要**强制类型转换**，继承关系同理。

```java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person {
    public void go() {
        System.out.println("go");
    }
}
public static void main(String[] args) {
    //Person 高 > Student 低
    Student aaa = new Student();
    aaa.go();
    Person bbb = aaa;//低转高 不需要强制类型转换
    //bbb.go();//子类转为父类可能丢失自己的方法

    Person xxx = new Student();
    //xxx.go();//报错
    //需要转换为Student类型才能使用Student类下的方法
    Student yyy = (Student) xxx;//强制转换成Student类
    yyy.go();
    //以上两句可以写成一句 ((Student) xxx).go();
}
```

**总结：**父类的引用 指向 子类的对象，子类转父类，不用强制转换担忧可能丢失方法，父类转子类，需要强制类型转换。使用类型转换可以方便方法的调用，减少重复的代码。

---

### static 关键字

- 静态方法与非静态方法（前文有说）

非静态方法可以调用所有的静态方法中的内容，因为静态方法一开始就加载出来了。

```java
public class Student {
    private static int age;//静态变量
    private double score;//非静态变量
    public void run(){}
    public static void go(){}
    public static void main(String[] args) {
        Student s1 = new Student();
        System.out.println(Student.age);//类变量
        //System.out.println(Student.score);//报错
        System.out.println(s1.age);
        System.out.println(s1.score);
        System.out.println("========================");
        //run();//报错，需要用对象来调用run方法
        new Student().run();
        Student.go();
        go();//以上两行等价
    }
}
```

- **匿名代码块与静态代码块**

**匿名代码块**，程序无法主动调用此模块，**创建对象时自动创建好此模块。**

**静态代码块**，类一加载直接执行，且永久**只执行一次。**

1. 结构：

```java
public class X {
    {
        //代码块（匿名代码块）
    }
    static {
        //静态代码块（方便初始化数据）
    }
}
```

2. 测试：

```java
public class Person {
    {
        System.out.println("匿名代码块");
    }
    static {
        System.out.println("静态代码块");
    }
    public Person() {
        System.out.println("构造方法");
    }
    public static void main(String[] args) {
        Person person1 = new Person();//静态代码块	匿名代码块	构造方法
        System.out.println();
        Person person2 = new Person();//匿名代码块	构造方法
    }
}
```

- 静态导入包

Math.random() 是 java . lang 包下的一个类，random() 用于生成随机数

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(Math.random());
    }
}
```

但是每次用要写 Math.很麻烦，可使用 import + static 导入包下的方法

```java
import static java.lang.Math.random;
public class Test {
    public static void main(String[] args) {
        System.out.println(random());
    }
}
```

---

### final 关键字

final 是**常量**的修饰符，通过 final 修饰的类就无法继承了（即没有子类）

```java
public final class Person{}
public class Student extends Person{}//报错，无法继承
```

---

### 抽象类（abstract）

通过 **abstract** 修饰符修饰的方法称为抽象方法，即只有方法的名字，没有实现方法。修饰的类称为抽象类。

特点：

- 不能 new 这个抽象类，只能靠子类去实现它。
- 抽象类中可以有正常的方法，也可以有抽象的方法。但一旦有抽象方法，这个类必须是抽象类。
- 抽象类如果要被继承，必须要**重写**其中的抽象方法。

```java
public abstract class Action {//抽象类
    public abstract void soSomething();//抽象方法，只有方法名字没有方法实现。
}
```

---

### 接口（interface）

1. **对比**

   普通类：只有具体实现

   抽象类：具体实现、规范（抽象方法）

   接口：只有规范，**自己无法写方法。**

**声明类的关键字是 class，声明接口的关键字是 interface**，接口的本质是契约，制定好之后需要遵守。

2. 特点

   接口拥有类似**多继承**的特性。

   使用**类 + implements 可以实现接口**，但需要**重写**接口中的方法，否则会报错，使用 **Alt + Insert** 可以快速添加接口方法重写。

   接口中的属性默认为常量，前面隐藏了 public static final（但**一般不在接口里定义常量**）

   接口中的方法默认为抽象方法，前面隐藏了 public abstract

   接口不能实例化，因为接口中没有构造方法。

```java
public interface UserService {
    int AGE = 99;//默认隐藏了 public static final
    void add(String name);//默认隐藏了 public abstract
    void delete(String name);
    void update(String name);
    void query(String name);
}
public interface TimeService {
    void timer();
}
public class ServiceImpl implements UserService,TimeService {//伪多继承
    @Override
    public void add(String name) {}
    @Override
    public void delete(String name) {}
    @Override
    public void update(String name) {}
    @Override
    public void query(String name) {}
    @Override
    public void timer() {}
}
```

**命名规范：**接口的实现类的命名一般在后面加 Impl 。

---

### 泛型

假如有需求：写一个排序方法，能够对整型数组、字符串数组甚至其他任何类型的数组进行排序，那么可以使用 **Java 泛型**。

- 定义泛型方法的规则：

1. 所有泛型方法声明都有一个类型参数声明部分 **< >**，该类型参数声明部分在方法返回类型之前。
2. 每一个类型参数声明部分包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。
3. 泛型方法体的声明和其他方法一样。注意类型参数只能代表引用型类型，不能是原始类型（像 int、double、char 等）。

---

### 内部类 \*

内部类是指在一个类里面写另一个类。里面的类就称为内部类。

```java
public class Outer {//外部类
    private int id = 10;
    public void out(){
        System.out.println("这是外部类的方法");
    }
    public class Inner{//内部类
        public void in(){
            System.out.println("这是内部类的方法");
        }
        public void getID(){//获得外部类的私有属性
            System.out.println(id);
        }
    }
}
public static void main(String[] args) {
    Outer outer = new Outer();
    //通过这个外部类来实例化内部类
    Outer.Inner inner = outer.new Inner();//outer.new Inner();
    inner.in();//输出这是内部类的方法
    inner.getID();//输出10
}
```

- 内部类前加上 static 就是**静态内部类**，内部类加了 static 关键字就无法获取非静态外部类的私有属性了。
- 另一种内部类（相当于在一个 Java 文件下写了两个类）

```java
public class Outer {}
class A {}//这个class A前不能加public
```

这个 class A{} 前不能加 public，因为一个 .java 文件里**只能有一个 public class**，但可以有多个 class（可以用来写 main 方法测试）。

- **局部内部类**

方法里写类称为局部内部类。

```java
public class Outer {
    public void method(){
        class Inner{//局部内部类
            public void in(){}
        }
    }
}
```

- **匿名内部类**，指不用名字去初始化类，不用把实例保留到变量中。

```java
public class Test {
    public static void main(String[] args) {
        Apple apple = new Apple();//正常的new方式，实例化对象并赋值
        new Apple().eat();//没有名字却调用了方法，匿名内部类
    }
}
class Apple{
    public void eat(){
        System.out.println("吃苹果");
    }
}
```

# javaSE 学习

---

## 基础知识

编译 → 运行

```java
public class Hello{
	public static void main(String[] args){		//输入psvm
        System.out.println("Hello World");		//输入sout
    }
}
```

**编译与解释**：

- 中文书翻译成英文书（编译型：要求速度、C/C++）

- 中文书 → 翻译官 → 英文书（解释型：不要求速度、预编译、如 JavaScript）

- java 是先编译后解释

**注释**

- 注释颜色等更改：Settings→Editor→Color Scheme→Java→Comments

- 除了单行多行注释还有文档注释，格式为：/\*\* \*/（可识别参数、了解）

---

### Java 数据类型

**Java 数据类型分为基本类型和引用类型**

- 基本类型：数值（整数、浮点、字符）、boolean

- 引用类型：类、接口、数组

```java
public static void main(String[] args) {
	//八大基本数据类型
    //整数
    int num = 10;
    byte num2 = 127;    //byte最大为127
    short num3 =30;
    long num4 = 30L;    //long在后面加数字L用于区分
    //小数
    float num5 = 50.1F;  //float后面加F用于区分
    double num6 = 5.315466457;
    //字符
    char name = 'a';
    //字符串不是关键字，是类
    String namea = "土拨";
    //布尔
    boolean flag = true;
}
```

**转义字符**

- \t 制表符

- \n 换行符

### 运算符

**自增自减**

```java
int a = 3;
int b = a++;    	//执行完这行代码前，先给b赋值，再自增
System.out.println(b);		//b = 3
a = 3;
int c = ++a;    	//执行这行代码前，先自增，再给b赋值
System.out.println(c);		//c = 4
```

**字符串连接符**

- 只要 + 左右有字符串，就把所有字符串后面的 + 转换成字符串连接

```java
int a = 10;
int b = 20;
System.out.println(""+a+b);		//输出为：3020
System.out.println(a+b+"");		//输出为：30
```

**三元运算符**

```java
x ? y : z;		//如果x==true，则结果为y，否则结果为z
```

---

## 流程控制

---

### Scanner 类

- Java 提供了一个工具类 Scanner，可以获取用户的输入

```Java
Scanner s = new Scanner(System.in);
```

- 通过 Scanner 类的 next() 与 nextLine() 方法获取输入的字符串，再读取前一般需要使用 hasNext() 与 hasNextLine() 判断是否还有输入的数据。

**（1）使用 next 方式接收（以空格为结束符）**

```Java
public static void main(String[] args) {
	//创建一个扫描器对象，接收键盘数据
    Scanner scanner =new Scanner(System.in);
    System.out.println("使用next方式接收：");
    //判断用户有没有输入字符串
    if(scanner.hasNext()){
        //使用next方式接收
        String str = scanner.next();
        System.out.println("输出的内容为："+str);
    }
    scanner.close();
    //所有IO流的类不及时关会一直占用资源，随用随关
    }
```

- **以上代码执行完输入 hello world 后输出结果只有 hello**

**（2）使用 nextLine 方式接收（以回车为结束符）（常用）**

```Java
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    System.out.println("请输入数据：");
    if(scanner.hasNextLine()){
        String str = scanner.nextLine();
        System.out.println("输出的内容为："+str);
    }
    scanner.close();
}
```

- **以上代码执行完输入 hello world 后输出结果为 hello world**

**（3）hasNextFloat：下一行是否为浮点数**

```Java
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    int i = 0;
    float f = 0.0f;
    System.out.println("请输入小数：");
    //是否还有下一个小数
    if(scanner.hasNextFloat()){
        f = scanner.nextFloat();
        System.out.println("小数数据：" + f);
    }else{
        System.out.println("输入的不是小数数据！");
    }
    scanner.close();
}
```

---

### If 选择结构

```java
public static void main(String[] args) {
	Scanner scanner = new Scanner(System.in);
	System.out.println("请输入内容：");
	String s = scanner.nextLine();
	//equals：判断字符串是否相等（字符串判断不要用==）
	if (s.equals("Hello")){
        System.out.println(s);
    }
    System.out.println("End");
    scanner.close();
}
```

if-else 略。

---

### switch 选择结构

- switch-case 多选择结构，可用来匹配一个值。
- Java SE 7 开始，switch 支持字符串（将字符串转为哈希值判断）

```java
public static void main(String[] args) {
    String name = "丁真";
    switch (name){
        case "蔡徐坤":
            System.out.println("蔡徐坤");
            break;
        case "丁真":
            System.out.println("丁真");
            break;
        case "马保国":
            System.out.println("马保国");
            break;
        default:
            System.out.println("是穿山甲吗？");
    }
}
```

---

## 循环结构

---

### while

```java
public static void main(String[] args) {
    //计算1加到100
    int i = 0;
    int sum = 0;
    while (i<=100){
        sum = sum + i;
        i++；
    }
    System.out.println(sum);
}
```

---

### do while

- 无论条件是否满足，语句至少执行一遍。

```java
public static void main(String[] args) {
    int i = 0;
    int sum = 0;
    do{
        sum = sum + i;
        i++;
    }while (i<=100);
    System.out.println(sum);
}
```

---

### for

- 初始化;条件判断;迭代（初始化步骤可为空）

- 输入**100.for**自动生成（i < 100 的循环）

- 或输入 **fori** 快速上生成 for 循环，再补全条件判断。

```java
public static void main(String[] args) {
    //0~100奇数和与偶数和
    int oddSum = 0;
    int evenSum = 0;
    for (int i = 0; i < 100; i++) {
        if(i%2!=0){
            oddSum+=i;
        }else{
            evenSum+=i;
        }
    }
    System.out.println("奇数的和："+oddSum);
    System.out.println("偶数的和："+evenSum);
}
```

```java
public static void main(String[] args) {
    //循环输出1~1000间被5整除的数，且每行输出三个
    for (int i = 1; i < 1000; i++) {
        if (i%5==0){
            System.out.print(i+"\t");   //print输出不会换行
        }
        if (i%15==0) {
            System.out.println();		//输出空行
        }
    }
}
```

```java
public static void main(String[] args) {
    //打印九九乘法表
    for (int j = 1; j <= 9; j++) {
        for (int i = 1; i <= j; i++) {
            System.out.print(i + "*" + j + "=" + (j * i)+"\t");
        }
        System.out.println();
    }
}
```

---

### 增强 for 循环

- 用于**数组**或**集合**的增强对象

```java
public static void test() {
    //遍历数组的元素
    int[] numbers = {10,20,30,40,50};
    /*
    for (int i = 0; i<5; i++) {
    	System.out.println(numbers[i]);
    }
    */
    for (int x:numbers){
        System.out.println(x);
    }//两组代码完全等价
}
```

---

### break-continue

- break 用于循环语句或 switch 语句，**用于跳出循环**。
- continue 用于终止**某次循环**过程。

```java
public static void test() {
    int i = 0;
    while(i<100){
        i++;
        if (i%10==0){
            System.out.println();
            continue;	//i是10的倍数时，会直接跳过，开始下一轮
        }
        System.out.print(i);
    }
}
```

- goto 仍为 Java 的一个关键字，但未得到正式使用，但 Java 有标签的用法：即在想跳回的语句前加上 outer，在 continue 后加上 outer 就会调试转到 outer 语句的位置。

---

## 方法

---

### 定义

- System 是一个类、out 是一个对象、println()是一个方法。

```java
System.out.println();
//调用系统类里面的标准输出对象out中的println()方法
```

Java 方法是语句的集合，他们在一起执行一个功能。

- 方法是解决一类问题的步骤的有序组合
- 方法包含于类或对象中
- 方法在程序中被创建，在其他地方被引用

方法设计原则：一个方法只完成一个功能，有利于后期拓展。（原子性）

```java
修饰符 返回值类型 方法名(参数类型 参数名){
    方法体
	return 返回值;
}
```

1. 修饰符：可选，告诉编译器如何调用该方法，定义了该方法的访问类型。
2. 返回值类型：方法可能会返回值，没有就为 void。
3. 方法名：需遵守命名规范开头字母小写，后续首字母大写。
4. 参数：可选，方法被调用时，传递值给参数，称为实参或变量，方法可以不含参数。**形参：**在方法被调用时接收外界输入的数据。**实参：**调用方法实际传给方法的数据。

```java
public static void main(String[] args) {
    int sum = add(1,2);					//add()中的1,2为实参
    System.out.println(sum);
}
public static int add(int a,int b){		//int a,int b为形参
    return a + b;
}
```

5. 若方法存在返回值，一定要通过 return 返回出去，void 则不用。return 还表示终止方法。

```java
public static int max(int num1,int num2){
    //求两数最大值
    int result = 0;
    if (num1==num2){
        System.out.println("num1==num2");
        return 0;		//终止方法
    }
    if (num1>num2){
        result = num1;
    }else {
        result = num2;
    }
    return result;
}
```

---

### 方法调用

调用方法：Java 有两种调用方法的方式，根据方法是否返回值来选择

```java
对象名.方法名(实参列表)
```

当方法返回一个值的时候，方法调用通常被当做一个值。

```java
int larger = max(30,40);
```

如果方法返回值是 void，方法调用一定是一条语句。

```java
System.out.println("Hello,World!");
```

---

### 方法重载

重载指在一个类中，有相同的函数名称，但形参不同的函数。

```java
public static int max(int a,int b){
	略;
}
public static double max(double a,double b){
    略;
}
```

上面两个代码除了返回值和形参不同，内部完全一致，方法名也一样，就是**方法重载**。

重载原则：

- 方法名必须相同，参数列表必须不同（个数不同、或类型不同、或参数排列按顺序不同）
- 返回值类型可相同可不同，仅仅返回值不同不足以成为方法的重载。

---

### 可变参数

不定项参数：不规定要传多少参数。

- 在方法声明中，在指定参数类型后加一个省略号(...)
- 一个方法只能有一个可变长参数，它必须是方法的最后一个参数，任何普通参数必须在他之前声明。

```java
public static void main(String[] args) {
    printMax(34,33,31,56.5,22);
    printMax(new double[]{1,2,3});
}
public static void printMax(double... numbers){
    //打印最大值（但不确定有多少传参）
    if (numbers.length == 0){
        System.out.println("No argument passed");
        return;
    }
    double result = numbers[0];
    //排序
    for (int i = 1; i < numbers.length; i++) {
        if (numbers[i] > result){
            result = numbers[i];
        }
    }
    System.out.println("The max valur is " + result);
}
```

---

### 递归

递归即方法自己调用自己。

- 递归头：必须有出口，如果没有将陷入死循环。
- 递归体：什么时候需要调用自身。

```java
public static void main(String[] args) {
    System.out.println(f(5));
}
public static int f(int n){
    //计算n!
    if(n==1) {
        return 1;
    }else {
        return n*f(n-1);
    }
}
```

---

## 数组

---

### 声明与创建

```java
int[] nums;     		//声明一个数组
nums = new int[10];      //创建数组，创建了空间，可存10个int类型数字
//nums[0] = 1;			给第0号元素赋值1
//array.length表示数组长度
int sum =0
for (int i = 0; i < nums.length; i++){
    sum = sum + nums[i];
}
System.out.println("总和为：" + sum);
```

1. **特点**

- 数组长度是确定的，一旦被创建，它的大小就不可改变。
- 它的元素必须是相同类型，不允许出现混合类型。
- 数组中的元素可以是任何数据类型，包括基本类型和引用类型。
- 数组变量属于引用类型，数组可以看成是对象，数组中每个元素相当于该对象的成员变量。（数组对象本身在堆中）

2. **内存分析**

```java
int nums；			   //在栈里压了一块空间。
nums = new int[10];		//new关键字在堆里，所以在堆里产生了一片十块的空间。
```

运行时出现错误：java.lang.ArrayIndexOutOfBoundsException 表示数组下标越界

3. **三种初始化**

```java
//静态初始化(大小不可改变)
int[] a = {1,2,3,4,5,6,7,8};
//动态初始化：包含默认初始化
int[] b = new int[10];
b[0] = 10;
```

数组是引用类型，它的元素相当于类的实例变量，因此数组一旦分配空间，其中每个元素也被按照实例变量同样的方式被**隐式初始化**（被赋默认值）。

---

### 数组使用

1. 增强 for 循环：适合打印输出，**没有数组下标**，jdk1.5 以上。

```java
int[] arrays = {1,2,3,4,5};
for (int array : arrays){
    System.out.println(array);
}
printArray(arrays);
```

2. 数组作为参数与数组作为返回值

```java
public static void main(String[] args) {
    int[] arrays = {1,2,3,4,5};
    int[] reverse = reverse(arrays);
    printArray(reverse);
}
//打印数组-数组作为方法入参
public static void printArray(int[] arrays){
    for (int i = 0; i < arrays.length; i++) {
        System.out.print(arrays[i]+" ");
    }
}
//反转数组-数组作为返回值
public static int[] reverse(int[] arrays){
    int[] result = new int[arrays.length];
    for (int i = 0,j = result.length-1; i < arrays.length; i++,j--) {
        result[j] = arrays[i];
    }
    return result;
}
```

---

### 多维数组

二维数组：数组的元素为数组，即数组的嵌套。

```java
//定义四行两列的数组
int[][] array = {{1,2},{2,3},{3,4},{4,5}};
//遍历二维数组元素
for (int i = 0; i < array.length; i++) {
    for (int j = 0; j < array[i].length; j++) {
        System.out.println(array[i][j]);
    }
}
```

---

### Arrays 类

- 数组的工具类 java.util.Arrays（了解即可）

```java
int[] a = {1,2,3,4,9999,312431,534,3,421,656,23};
//升序排序
Arrays.sort(a);
//打印数组元素
System.out.println(Arrays.toString(a));
//填充第2~4的数组元素
Arrays.fill(a,2,4,0);
System.out.println(Arrays.toString(a));
```

---

### 冒泡排序

- 简易版

```java
public static int[] BubbleSort(int[] array){
    int temp = 0;
    for (int i = 0; i < array.length-1; i++) {
        //若第一个数比第二个数大则两数交换
        for (int j = 0; j < array.length-1; j++) {
            if (array[j+1]<array[j]){
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
            }
        }
    }
    return array;
}
```

- 优化版

```java
public static int[] BubbleSort(int[] array){
    int temp = 0;
    for (int i = 0; i < array.length-1; i++) {
        boolean flag = false;   	//通过标志位减少无意义的比较
        for (int j = 0; j < array.length-1; j++) {
            //每次比较交换后改变flag值
            if (array[j+1]<array[j]){
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                flag = true;
            }
        }
        //说明没有进行比较
        if (flag == false){
            break;
        }
    }
    return array;
}
```

---

## 面向对象编程

**面向对象编程**(Object-Oriented Programming,OOP)，其本质为**以类的方式组织代码，以对象的组织封装数据**。

**属性+方法**：将众多共同特性的方法提取出来加上属性就成为了一个类。

---

### 静态方法与非静态方法

- **静态方法：**若类 1 中存在的静态方法，就可以在类 2 中使用类 1 中的静态方法。

```java
public class X{
    public static void a{
        ...
    }
}
//可以在别的类中的main方法中使用X.a()来调用此方法
```

- **非静态方法：**若类 1 中的方法是非静态方法，可以使用 new 关键字将类实例化。

```java
public class X{
    public void a{
        ...
    }
}
//可以再别的类中使用 new X().a();	相当于创建了X类调用了a方法，但一般写为下面的形式
//对象类型 对象名 = 对象值；
//X x = new X1();
```

**[两种情形]**

两个非静态方法可以互相调用。

```java
public void a(){
    b();
}
public void b(){}
```

一个为静态方法时，静态方法中不能调用非静态方法。因为 **static 和类一起加载**，当类存在时，其中的静态方法就已经存在，而 b()与对象有关，当对象存在时方法才存在，所以**无法调用不存在的方法**，即**需要实例化**（需要 new）。

```java
public static void a(){
    b();	//此时无法调用b(),报错
}
public void b(){}
```

---

### 值传递与引用传递

java 为值传递，下面的例子 change() 方法内 a 为 10，回到主方法 a 仍是主方法中的值为 1 的 a

```java
public class Demo {
    public static void main(String[] args) {
        int a = 1;
        System.out.println(a);	//输出为1
        change(a);
        System.out.println(a);	//输出仍为1
    }
    public static int change(int a){
        a = 10;
        return a;
    }
}
```

引用传递：对象，但本质还是值传递

```java
public class Demo {
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.name);	//输出为null
        change(person);
        System.out.println(person.name);	//输出为土拨
    }
    public static void change(Person person){
//person是一个对象，它指向的是Person person = new Person();（一个具体的人，可以改变属性）
        person.name = "土拨";
    }
}
//定义了一个person类，有一个属性name
class Person{
    String name;    //默认值为null
}
```

---

### 类与对象的关系

类是一种抽象的数据类型，它是对某一类事物的整体描述/定义，但**不能够代表某一个具体事物**。

对象是抽象概念的具体实例，类：人，对象：张三

- **使用 new 关键字创建对象！**除了**分配内存空间**外，还会给创建好的对象进行**默认的初始化** 以及 **对类中构造器的调用**。

```java
public class Student {		//Student.java
    //属性：字段
    String name;
    int age;
    //方法
    public void study(){
        System.out.println(this.name+"在学习");
    }
}
public class Application {		//Application.java
    //一个项目应该只存在一个main方法
    public static void main(String[] args) {
        //类：抽象的,实例化后会产生返回结果
        //student对象就是Student类的具体实例
        Student xiaoming = new Student();
        Student gouzi = new Student();
        xiaoming.name = "小明";
        xiaoming.age = 3;
    }
}
```

---

### 构造器

一个类即便什么都不写，它也会存在一个方法，这个方法就是构造方法。（类中不写会自动在在同名文件的.class 中生成空方法）

1. 特点

- 必须**和类的名字相同**
- 必须**没有返回值**，也不能写 void

2. 作用

- 使用 new 关键字，**必须要有构造器**，**new 关键字本质是在调用构造器**。
- 构造器**一般用来初始化值**。
- 有参构造：一旦定义了有参构造，若想调用无参构造，原本的无参构造就必须显式定义（空定义），否则调用就报错。
- 快捷键 Alt + Insert 快速生成构造器。
- this.表示当前类

```java
public static void main(String[] args) {	//Application.java
    Person person = new Person();
    System.out.println(person.name);
}
public class Person {		//person.java
    String name;
    public Person() {
    }
    public Person(String name) {
        this.name = name;		//this。name指这个类中的name
    }
}
```

---

### 封装（private，get 与 set）

**private** 将数据中的属性隐藏起来，禁止直接访问一个对象中的数据的实际表示，而通过操作接口来访问。

封装可以提高程序安全性，保护数据，隐藏代码的实现细节，统一接口，提高系统可维护性。

- 使用快捷键 Alt + Insert 后选择 getter and setter 快速生成 get / set

```java
public class Student {
    private String name;//名字
    private int id;//学号
    private char sex;//性别

    //需要提供一些可以操作这些属性的方法
    //提供一些public的get、set方法
    public String getName(){
        return this.name;
    }
    public void setName(String name){
        this.name = name;
    }
}
public class Application {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.setName("土拨");
        System.out.println(s1.getName());
    }
}
```

---

### 继承（extends , super , 重写 与 多态）

1. **extends**

继承的本质是对某一批类的抽象，比如动物这个大类下有灵长类动物类。继承是类和类之间的一种关系，除此之外，类和类之间的关系还有依赖、组合、聚合等。

- **子类继承父类，就会拥有父类的全部方法。**
- 快捷键 Ctrl + H 打开继承树
- 在 Java 中，所有的类都默认继承 Object 类，且 Java 只有单继承，没有多继承。（一个爸爸可以有多个儿子，但一个儿子不能有多个爸爸）

```java
public class Person {//父类
    private int money = 10_0000_0000;
    public void say(){
        System.out.println("说了一句话");
    }
    public int getMoney() {
        return money;
    }
}
public class Student extends Person{}//子类，继承父类
public class Application {
    public static void main(String[] args) {
        Student student = new Student();
        student.say();//输出：说了一句话
        System.out.println(student.getMoney());//输出1000000000
    }
}
```

2. **super**

与**this.**对应，子类继承父类后，使用**super.**调用父类的方法，使用**this.**调用本类的属性，且**this.**没有继承也能使用而**super.**要有继承条件才能使用。

- **super() 调用父类的构造方法，必须在构造方法的第一行**
- super() 必须只能出现在子类的方法或者构造方法中
- **super() 和 this()不能同时调用构造方法！**

```java
public class Person {
    public Person() {//无参构造器
        System.out.println("Person无参构造执行了");
    }
    protected String name = "tubo_dad";
    public void print(){
        //若这里的public为private，则无法调用，私有无法被继承
        System.out.println("Person");
    }
}
public class Student extends Person{
    public Student() {
        //隐藏代码super：这里默认调用了父类的无参构造
        //调用父类的构造器必须要在子类的第一行
        System.out.println("Student无参构造执行了");
    }
    private String name = "tubo_son";
    public void print() {
        System.out.println("Student");
    }
    public void test1(){
        print();//Student
        this.print();//Student
        super.print();//Person
    }
    public void test2(String name){
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }
}
public class Application {
    public static void main(String[] args) {
        Student student = new Student();
        student.test1();
        student.test2("tubo");
    }
}
```

运行结果为：

```java
Person无参构造执行了//new Student()>调用了Student构造器>调用了父类Person构造器
Student无参构造执行了
Student//test1中的print()
Student//test1中的this.print()，以上两个语句是等价的
Person//super调用了父类的print()方法
tubo
tubo_son
tubo_dad
```

3. **方法重写**

**重写指重写非静态方法，需要有继承关系。**

**子类重写父类的方法，和属性无关，和静态方法无关。且方法名、参数列表必须相同。**

子类方法和父类方法必须一致，但里面的方法体不同。

为什么和方法重写和静态方法无关？因为静态方法一开始就加载出来了。

**重写时修饰符的范围可以扩大，但不可以缩小。**如 private 可以重写 public（修饰符范围大小关系：public > proteted > Default > private）

重写抛出的异常范围可以被缩小，但不能被扩大。如 ClassNotFoundException < Exception

```java
public class B {
    public static void test(){//静态方法
        System.out.println("B=>test()");
    }
}
public class A extends B{
    public static void test() {//静态方法
        System.out.println("A=>test()");
    }
}
public class Application {
    public static void main(String[] args) {
        //方法的调用只和左边定义的数据类型有关
        A a = new A();
        a.test();//调用A类的方法

        //父类的引用指向了子类
        B b = new A();
        b.test();//调用B类的方法
    }
}
```

删去 A 与 B 类的 static 关键字，将 A 类下原内容删除后使用 **Alt + insert** 出现**方法重写**，默认调用了父类的 test()，重写为 System.out.println("A=>test()")后运行程序结果发生了变化。

```java
public class B {
    public void test(){
        System.out.println("B=>test()");
    }
}
public class A extends B{
    //Override 重写
    @Override//注解：有功能的注释
    public void test() {
        System.out.println("A=>test()");
    }
}
public class Application {
    public static void main(String[] args) {
        A a = new A();
        a.test();//输出A=>test()
        //父类的引用指向了子类
        B b = new A();//子类重写了父类的方法
        b.test();//输出A=>test()
    }
}
```

结论：

- 若方法为 **static 静态方法**，使用 new 关键字时，它的**结果只和最左边的类有关。**
- 对象能执行那些方法，主要看左边的类型，和右侧关系不大。
- **只有非静态方法才能重写**
- 应用场景：父类的功能，子类不一定需要或不一定满足，需要重写。
- 不能重写的方法：static 方法（属于类，它不属于实例）、final 常量（被 final 修饰就无法被重写）、private 方法。

4. **多态**

多态即**同一方法可根据发送对象不同可以采取不同的行为方式**。多态是指**方法多态**，属性没有多态性。需要有继承关系。

**一个对象的实际类型是确定的**，如 new Student() 一定是 Student 类，但**可以指向的引用类型是不确定的**。

```java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person {
    @Override
    public void run() {
        System.out.println("son");
    }
}
public class Application {
    public static void main(String[] args) {
        Student s1 = new Student();
        Person s2 = new Student();//父类的引用指向子类的类型
        Object s3 = new Student();//祖宗类的引用指向子类的类型
        //若子类重写了父类的方法，那么执行子类的方法
        s2.run();//输出son
        s1.run();//输出son
    }
}
```

结论：

- 父类与子类间需有联系。两种无联系的类无法互相转化，比如 Student 类无法转为 String 类，会报类型转换异常 ClassCostException !
- **多态存在条件：**继承关系，方法需要重写，父类引用指向子类对象 即 **father f1 = new son();**

---

### instanceof 关键字 与 类型转换

1. **instanceof**

instanceof 用来判断两个类之间**是否存在继承关系（没有继承关系就编译报错）**

```Java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person{}
public class Teacher extends Person{}
public class Application {
    public static void main(String[] args) {
        public static void main(String[] args) {
        //Object > String
        //Object > Person > Student
        //Object > Person > Teacher
        Object object = new Student();
        System.out.println(object instanceof Student);//true
        System.out.println(object instanceof Person);//true
        System.out.println(object instanceof Object);//true
        System.out.println(object instanceof Teacher);//false
        System.out.println(object instanceof String); //false
        System.out.println("===================================");
        Person person = new Student();
        System.out.println(person instanceof Student);//true
        System.out.println(person instanceof Person);//true
        System.out.println(person instanceof Object);//true
        System.out.println(person instanceof Teacher);//false
        //System.out.println(person instanceof String); //编译报错
        System.out.println("===================================");
        Student student = new Student();
        System.out.println(student instanceof Student);//true
        System.out.println(student instanceof Person);//true
        System.out.println(student instanceof Object);//true
        //System.out.println(student instanceof Teacher);//编译报错
    }
    }
}
```

2. **类型转换**

基本类型转换满足：从低转高（如 32 位转 64 位），从高转低需要**强制类型转换**，继承关系同理。

```java
public class Person {
    public void run(){
        System.out.println("run");
    }
}
public class Student extends Person {
    public void go() {
        System.out.println("go");
    }
}
public static void main(String[] args) {
    //Person 高 > Student 低
    Student aaa = new Student();
    aaa.go();
    Person bbb = aaa;//低转高 不需要强制类型转换
    //bbb.go();//子类转为父类可能丢失自己的方法

    Person xxx = new Student();
    //xxx.go();//报错
    //需要转换为Student类型才能使用Student类下的方法
    Student yyy = (Student) xxx;//强制转换成Student类
    yyy.go();
    //以上两句可以写成一句 ((Student) xxx).go();
}
```

**总结：**父类的引用 指向 子类的对象，子类转父类，不用强制转换担忧可能丢失方法，父类转子类，需要强制类型转换。使用类型转换可以方便方法的调用，减少重复的代码。

---

### static 关键字

- 静态方法与非静态方法（前文有说）

非静态方法可以调用所有的静态方法中的内容，因为静态方法一开始就加载出来了。

```java
public class Student {
    private static int age;//静态变量
    private double score;//非静态变量
    public void run(){}
    public static void go(){}
    public static void main(String[] args) {
        Student s1 = new Student();
        System.out.println(Student.age);//类变量
        //System.out.println(Student.score);//报错
        System.out.println(s1.age);
        System.out.println(s1.score);
        System.out.println("========================");
        //run();//报错，需要用对象来调用run方法
        new Student().run();
        Student.go();
        go();//以上两行等价
    }
}
```

- **匿名代码块与静态代码块**

**匿名代码块**，程序无法主动调用此模块，**创建对象时自动创建好此模块。**

**静态代码块**，类一加载直接执行，且永久**只执行一次。**

1. 结构：

```java
public class X {
    {
        //代码块（匿名代码块）
    }
    static {
        //静态代码块（方便初始化数据）
    }
}
```

2. 测试：

```java
public class Person {
    {
        System.out.println("匿名代码块");
    }
    static {
        System.out.println("静态代码块");
    }
    public Person() {
        System.out.println("构造方法");
    }
    public static void main(String[] args) {
        Person person1 = new Person();//静态代码块	匿名代码块	构造方法
        System.out.println();
        Person person2 = new Person();//匿名代码块	构造方法
    }
}
```

- 静态导入包

Math.random() 是 java . lang 包下的一个类，random() 用于生成随机数

```java
public class Test {
    public static void main(String[] args) {
        System.out.println(Math.random());
    }
}
```

但是每次用要写 Math.很麻烦，可使用 import + static 导入包下的方法

```java
import static java.lang.Math.random;
public class Test {
    public static void main(String[] args) {
        System.out.println(random());
    }
}
```

---

### final 关键字

final 是**常量**的修饰符，通过 final 修饰的类就无法继承了（即没有子类）

```java
public final class Person{}
public class Student extends Person{}//报错，无法继承
```

---

### 抽象类（abstract）

通过 **abstract** 修饰符修饰的方法称为抽象方法，即只有方法的名字，没有实现方法。修饰的类称为抽象类。

特点：

- 不能 new 这个抽象类，只能靠子类去实现它。
- 抽象类中可以有正常的方法，也可以有抽象的方法。但一旦有抽象方法，这个类必须是抽象类。
- 抽象类如果要被继承，必须要**重写**其中的抽象方法。

```java
public abstract class Action {//抽象类
    public abstract void soSomething();//抽象方法，只有方法名字没有方法实现。
}
```

---

### 接口（interface）

1. **对比**

   普通类：只有具体实现

   抽象类：具体实现、规范（抽象方法）

   接口：只有规范，**自己无法写方法。**

**声明类的关键字是 class，声明接口的关键字是 interface**，接口的本质是契约，制定好之后需要遵守。

2. 特点

   接口拥有类似**多继承**的特性。

   使用**类 + implements 可以实现接口**，但需要**重写**接口中的方法，否则会报错，使用 **Alt + Insert** 可以快速添加接口方法重写。

   接口中的属性默认为常量，前面隐藏了 public static final（但**一般不在接口里定义常量**）

   接口中的方法默认为抽象方法，前面隐藏了 public abstract

   接口不能实例化，因为接口中没有构造方法。

```java
public interface UserService {
    int AGE = 99;//默认隐藏了 public static final
    void add(String name);//默认隐藏了 public abstract
    void delete(String name);
    void update(String name);
    void query(String name);
}
public interface TimeService {
    void timer();
}
public class ServiceImpl implements UserService,TimeService {//伪多继承
    @Override
    public void add(String name) {}
    @Override
    public void delete(String name) {}
    @Override
    public void update(String name) {}
    @Override
    public void query(String name) {}
    @Override
    public void timer() {}
}
```

**命名规范：**接口的实现类的命名一般在后面加 Impl 。

---

### 泛型

假如有需求：写一个排序方法，能够对整型数组、字符串数组甚至其他任何类型的数组进行排序，那么可以使用 **Java 泛型**。

- 定义泛型方法的规则：

1. 所有泛型方法声明都有一个类型参数声明部分 **< >**，该类型参数声明部分在方法返回类型之前。
2. 每一个类型参数声明部分包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。
3. 泛型方法体的声明和其他方法一样。注意类型参数只能代表引用型类型，不能是原始类型（像 int、double、char 等）。

---

### 内部类 \*

内部类是指在一个类里面写另一个类。里面的类就称为内部类。

```java
public class Outer {//外部类
    private int id = 10;
    public void out(){
        System.out.println("这是外部类的方法");
    }
    public class Inner{//内部类
        public void in(){
            System.out.println("这是内部类的方法");
        }
        public void getID(){//获得外部类的私有属性
            System.out.println(id);
        }
    }
}
public static void main(String[] args) {
    Outer outer = new Outer();
    //通过这个外部类来实例化内部类
    Outer.Inner inner = outer.new Inner();//outer.new Inner();
    inner.in();//输出这是内部类的方法
    inner.getID();//输出10
}
```

- 内部类前加上 static 就是**静态内部类**，内部类加了 static 关键字就无法获取非静态外部类的私有属性了。
- 另一种内部类（相当于在一个 Java 文件下写了两个类）

```java
public class Outer {}
class A {}//这个class A前不能加public
```

这个 class A{} 前不能加 public，因为一个 .java 文件里**只能有一个 public class**，但可以有多个 class（可以用来写 main 方法测试）。

- **局部内部类**

方法里写类称为局部内部类。

```java
public class Outer {
    public void method(){
        class Inner{//局部内部类
            public void in(){}
        }
    }
}
```

- **匿名内部类**，指不用名字去初始化类，不用把实例保留到变量中。

```java
public class Test {
    public static void main(String[] args) {
        Apple apple = new Apple();//正常的new方式，实例化对象并赋值
        new Apple().eat();//没有名字却调用了方法，匿名内部类
    }
}
class Apple{
    public void eat(){
        System.out.println("吃苹果");
    }
}
```
