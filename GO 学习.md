# GO语言学习

---

## 第一个程序

```go
package main //程序的包名，含有 main 函数的包必须是 main 包

// import "fmt"
// import "time"
import (
	"fmt"
	"time"
)
//main函数
func main() { //函数的 { 一定和函数名在同一行，否则编译错误
	fmt.Println("Hello Go!")
	time.Sleep(1 * time.Second)
}
```

## 变量声明

```go
package main

/*
四种变量声明方式
*/

import (
	"fmt"
)

//声明全局变量 方法一，二，三是可以的 方法四不支持全局
var ga int = 100
var gb = 200

func main() {
	//方法一：声明一个变量 默认值为0
	var a int
	fmt.Println("a = ", a)
	fmt.Printf("type of a = %T\n", a)
	
	//方法二：声明一个变量 初始化一个值
	var b int = 100
	fmt.Println("b = ", b)
	fmt.Printf("type of b = %T\n", b)

	var bb string = "abcd"
	fmt.Printf("bb = %s, type of bb = %T\n", bb, bb)

	//方法三：在初始化的时候，可以省去数据类型 通过值自动匹配当前变量的数据类型
	var c = 100
	fmt.Println("c = ", c)
	fmt.Printf("type of c = %T\n", c)

	var cc string = "abcd"
	fmt.Printf("cc = %s, type of cc = %T\n", cc, cc)

	//方法四：（常用方法）省去 var 关键字，直接自动匹配
	d := 100
	fmt.Println("d = ", d)
	fmt.Printf("type of d = %T\n", d)

	e := "abcd"
	fmt.Println("e = ", e)
	fmt.Printf("type of e = %T\n", e)

	f := 3.14
	fmt.Println("f = ", f)
	fmt.Printf("type of f = %T\n", f)

	//====
	fmt.Println("ga = ", ga, "gb = ", gb)

	//声明多个变量
	var xx, yy int = 100, 200
	fmt.Println("xx = ", xx , ", yy = ", yy)

	var kk, ll = 100, "abcd"
	fmt.Println("kk = ", kk , ", ll = ", ll)

	//多行的多变量声明
	var (
		vv int = 100
		jj bool = true
	)
	fmt.Println("vv = ", vv, ", jj = ", jj)
}
```

## const常量与iota

```go
package main

import "fmt"

//const 来定义枚举类型
const (
	//可以在const() 中添加一个关键字 iota，每行的iota都会累加1，第一行的iota默认值是0
	BEIJING = 10*iota  //iota = 0  BEIJING = 0
	SHANGHAI		   //iota = 1  SHANGHAI = 10
	SHENZHEN		   //iota = 2  SHENZHEN = 20
)

const (
	a, b = iota + 1, iota + 2	//iota = 0, a = iota + 1, b = iota + 2, a = 1, b = 2
	c, d						//iota = 1, c = iota + 1, d = iota + 2, c = 2, d = 3
	e, f						//iota = 2, e = iota + 1, f = iota + 2, a = 3, b = 4

	g, h = iota * 2, iota * 3	//iota = 3, g = iota * 2, h = iota * 3, g = 6, h = 9
)

func main() {
	//常量（只读属性）
	const length int = 10

	fmt.Println("length is", length)

	// length = 100 //常量是不允许被修改的

	fmt.Println("BEIJING =", BEIJING)
	fmt.Println("SHANGHAI =", SHANGHAI)
	fmt.Println("SHENZHEN =", SHENZHEN)

	fmt.Println("a =", a, "b =", b)
	fmt.Println("c =", c, "d =", d)
	fmt.Println("e =", e, "f =", f)
	fmt.Println("g =", g, "h =", h)

	//iota只能配合const() 一起使用，iota只有在const才进行累加效果
}
```

结果：

```bash
length is 10
BEIJING = 0
SHANGHAI = 10
SHENZHEN = 20
a = 1 b = 2
c = 2 d = 3
e = 3 f = 4
g = 6 h = 9
```

## 函数

### 返回值

```go
package main

import "fmt"

func foo1(a string, b int) int {
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)

	c := 100

	return c
}

//返回多个返回值，但匿名
func foo2(a string, b int) (int, int) {
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)

	return 666, 777
}

//返回多个返回值，形参带名称
func foo3(a string, b int) (r1 int, r2 int) {
	fmt.Println("----foo3----")
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)

	//给有名称的的返回值变量赋值
	r1, r2 = 1000, 2000
	return 
}

func foo4(a string, b int) (r1, r2 int) {
	//返回值类型相同可以合并
	fmt.Println("----foo4----")
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)

	r1, r2 = 1000, 2000
	return
}

func main() {
	c :=foo1("abc", 555)
	fmt.Println("c = ", c)

	ret1, ret2 := foo2("haha", 999)
	fmt.Println("ret1 = ", ret1, "ret2 = ", ret2)

	ret1, ret2 = foo3("foo3", 333)
	fmt.Println("ret1 = ", ret1, "ret2 = ", ret2)
}
```

### init函数与import导包

当前文件结构 GoStudy下

```go
>lib1 > lib1.go
>lib2 > lib2.go
main.go
```

lib1.go

```go
package lib1

import "fmt"

//当前lib1包提供的API 首字母大写表示对外开放接口（public），小写表示只能包内调用（private）
func Lib1Test() {
	fmt.Println("Lib1Test()...")
}

func init() {
	fmt.Println("lib1. init() ...")
}
```

lib2.go同

main.go下导包，（可能报错，没有GOPATH因为版本太新， go env -w GO111MODULE=off）

```go
package main

import (
	"GoStudy/lib1"
	"GoStudy/lib2"
)

func main() {
	lib1.Lib1Test()
	lib2.Lib2Test()
}
```

导包成功执行结果如下：

```bash
lib1. init() ...	//导包时执行init()
lib2. init() ...
Lib1Test()...		//main()调用
Lib2Test()...
```

若导入了包，却不使用任何接口会报错。

```go
package main

import (
	"GoStudy/lib1"
	"GoStudy/lib2"
)

func main() {
	//lib1.Lib1Test()
	lib2.Lib2Test()
}
```

- **三种导包方式**

1. 若不想使用某个包内的接口，却想使用该包内的 init() 函数，可以使用别名—**匿名**方法，在**包前加下划线与空格**。

   无法使用当前包的方法，但是会执行前面包内部的 init()

```go
package main

import (
	_ "GoStudy/lib1"
	"GoStudy/lib2"
)

func main() {
	//lib1.Lib1Test()
	lib2.Lib2Test()
}
```

2. 别名导包方式，给某个包起个别名。

```go
package main

import (
	_ "GoStudy/lib1"
	mylib2 "GoStudy/lib2"
)

func main() {
	//lib1.Lib1Test()
	//lib2.Lib2Test()
	mylib2.Lib2Test()
}
```

3. 直接在包名前，加个点和空格，将此包内全部方法导入本包，直接调用。

   （不要轻易使用此方法，因为可能导入很多包，都在前面加个点，包内恰好有同名方法，会发生歧义）

```go
package main

import (
	_ "GoStudy/lib1"
	. "GoStudy/lib2"
)

func main() {
	//lib1.Lib1Test()
	//lib2.Lib2Test()
	Lib2Test()
}
```

## 指针

简单的例子，如果没有指针，值传递，结果 a 仍然等于 1

```go
package main

import "fmt"

func changeValue(p int) {
	p = 10
}

func main() {
	var a int = 10
	changeValue(a)
	fmt.Println("a = ", a)
}
```

添加指针，引用传递，结果 a 等于 10

```go
package main

import "fmt"

func changeValue(p *int) {
	*p = 10		//修改p存储的地址指向的值
}

func main() {
	var a int = 10
	changeValue(&a)
	fmt.Println("a = ", a)
}
```

**指针的经典例子**，交换两个值：

```go
package main

import "fmt"

func snap(pa *int, pb *int) {
	var temp int
	temp = *pa	//前面有*，就是该地址下的值
	*pa = *pb
	*pb = temp
}

func main() {
	var a int = 10
	var b int = 20
	snap(&a, &b)
	fmt.Println("a = ", a , "b = ", b)
}
```

## defer关键字

defer **所在函数体结束**前触发 类似 java 中的 final

```go
package main

import "fmt"

func main() {
	//写入defer关键字 defer可以有多个，为压栈形式
	defer fmt.Println("main end1")
	defer fmt.Println("main end2")

	fmt.Println("main::hello go 1")
	fmt.Println("main::hello go 2")
}
```

输出结果为：

```bash
main::hello go 1
main::hello go 2
main end2
main end1
```

1. 感受一下 defer 的执行顺序

```go
package main

import "fmt"

func func1() {
	fmt.Println("A")
}

func func2() {
	fmt.Println("B")
}

func func3() {
	fmt.Println("C")
}

func main() {
	defer func1()
	defer func2()
	defer func3()

}
```

执行结果为：

```bash
C
B
A
```

2. 感受 defer 与 return 先后顺序

```go
package main

import "fmt"

func deferFunc() int {
	fmt.Println("defer func called...")
	return 0
}

func returnFunc() int {
	fmt.Println("return func called...")
	return 0
}

func returnAndDefer() int {
	defer deferFunc()
	return returnFunc()
}

func main() {
	returnAndDefer()
}
```

执行结果为：

```bash
return func called...
defer func called...
```

如果 defer 和 return 同时在一函数中，return 函数比 defer 先被调用。

## 数组与切片

### 数组与range遍历

**数组的长度是固定的，固定长度的数组在传参的时候，是严格匹配数组类型的。**

**range** 关键字会根据遍历不同的集合返回不同的值，**range 可以返回两个值，第一个值为元素下标，第二个值为元素值**

```go
package main

import "fmt"

func main() {
	//固定长度的数组
	var myArray1 [4]int

	//前四个元素定义值，后面默认0
	myArray2 := [7]int{1,2,3,4}
	
	//遍历数组方法1
	for i := 0; i < len(myArray1); i++ {
		fmt.Println(myArray1[i])
	}

	//遍历数组方法2
	for index, value := range myArray2 {
		fmt.Println("index =", index, ", value = ", value)
	}

	//查看数组的数据类型
	fmt.Printf("myArray1 types = %T\n", myArray1)
	fmt.Printf("myArray2 types = %T\n", myArray2)
}
```

执行结果为：

```bash
0
0
0
0
index = 0 , value =  1
index = 1 , value =  2
index = 2 , value =  3
index = 3 , value =  4
index = 4 , value =  0
index = 5 , value =  0
index = 6 , value =  0
myArray1 types = [4]int
myArray2 types = [7]int
```

**数组的传参问题：**既然不同长度的数组数据类型不同（上面的 [4] int 和 [7] int ），那么怎么进行传参呢？

```go
package main

import "fmt"

func printArray(myArray [4]int) {
	for index, value := range myArray{
		fmt.Println("index =", index, ", value = ", value)
	}
}

func main() {
	var myArray1 [4]int

	//myArray2 := [7]int{1,2,3,4}

	printArray(myArray1)
	// printArray(myArray2) //类型不匹配，报错
```

结果为：

```bash
index = 0 , value =  0
index = 1 , value =  0
index = 2 , value =  0
index = 3 , value =  0
```

go 里的数组是值传递，即数组作为参数传入是，只是将值拷贝了过去，使用**切片** / **动态数组**的方式

### 切片slice

**动态数组在传参上是引用传递，而且不同元素长度的动态数组的形参是一致的。**

注意 range 处匿名变量的用法

```go
package main

import "fmt"

func printArray(myArray []int) {
	//range返回索引和值，若只关心值不关心索引，可以使用_表示匿名变量
	for _, value := range myArray{
		fmt.Println("value = ", value)
	}

	myArray[0] = 100
}

func main() {
	//[] 内没有数字，长度可变，为动态数组/切片
	myArray := []int{1,2,3,4}

	fmt.Printf("myArray type is %T\n", myArray)

	printArray(myArray)
	println("=======")
	printArray(myArray)
}
```

执行结果

```bash
myArray type is []int
value =  1
value =  2
value =  3
value =  4
=======
value =  100
value =  2
value =  3
value =  4
```

**切片为引用传递**，而不是值传递。

1. **切片的三种声明方式**

```go
package main

import "fmt"

func isEmpty(slice []int) {
	// 判断一个 slice 是否为空
	if slice == nil {
		fmt.Println("slice 是一个空切片")
	} else {
		fmt.Println("slice 是有空间的")
	}
}

func main() {
	// 一：声明 slice1 是一个切片并且初始化，默认值是1，2，3，长度len为3
	slice1 := []int{1, 2, 3}
	// %v 表示打印任何类型的长度信息
	fmt.Printf("len = %d, slice = %v\n",len(slice1), slice1)
    fmt.Println("-----------")
    
	// 二：声明 slice2 是一个切片，但并没有为 slice2 分配空间，使用 make 开辟空间
	var slice2 []int
    fmt.Printf("len = %d, slice = %v\n",len(slice2), slice2)
	isEmpty(slice2)
	// 此时直接赋值会报错，因为没有空间
	// slice2[0] = 1
	// 开辟空间
	slice2 = make([]int, 3)
	slice2[0] = 100
	fmt.Printf("len = %d, slice = %v\n",len(slice2), slice2)
	isEmpty(slice2)
    fmt.Println("-----------")
	
	// 三：相当于第二种的多步复合，声明 slice3 是一个切片，同时给 slice3 分配空间，初始化值为 0
	var slice3 []int = make([]int, 3)
	// 另一种写法：可以使用 := 推导出 slice3 是一个切片
	// slice3 := make([]int, 3)
	fmt.Printf("len = %d, slice = %v\n",len(slice3), slice3)
}
```

结果：

```bash
len = 3, slice = [1 2 3]
-----------
len = 0, slice = []
slice 是一个空切片
len = 3, slice = [100 0 0]
slice 是有空间的
-----------
len = 3, slice = [0 0 0]
```

2. **slice 切片容量追加与截取**

**切片容量cap：** 在 make() 中没定义 cap，则 cap 等于 len

```go
package main

import "fmt"

func main() {
	var numbers = make([]int, 3, 5)
	fmt.Printf("len = %d, cap = %d, slice = %v\n", len(numbers), cap(numbers), numbers)
	// 向 numbers 切片追加一个元素1， numbers 长度len = 4， [0,0,0,1], 容量cap = 5
	numbers = append(numbers, 1)
	fmt.Printf("len = %d, cap = %d, slice = %v\n", len(numbers), cap(numbers), numbers)
	numbers = append(numbers, 2)
	fmt.Printf("len = %d, cap = %d, slice = %v\n", len(numbers), cap(numbers), numbers)
	fmt.Println("此时容量上限，自动扩容")
	// 此时容量已满，继续追加，go语言会自动开辟空间，新空间大小为容量二倍
	numbers = append(numbers, 3)
	fmt.Printf("len = %d, cap = %d, slice = %v\n", len(numbers), cap(numbers), numbers)
}
```

结果：

```bash
len = 3, cap = 5, slice = [0 0 0]
len = 4, cap = 5, slice = [0 0 0 1]
len = 5, cap = 5, slice = [0 0 0 1 2]
此时容量上限，自动扩容
len = 6, cap = 10, slice = [0 0 0 1 2 3]
```

**切片截取：**切片截取方法非常多，这里不详细展开

```go
package main

import "fmt"

func main() {
	s := []int{1, 2, 3}	//len = 3, cap = 3
	// 表示左闭右开[0,2)，截取用:表示区间
	s1 := s[0:2]	//[1, 2]
	
	fmt.Printf("s1 = %v\n", s1)
	// s1 与 s 底层指向同一位置，修改s1，s也会修改
	s1[0] = 100
	fmt.Printf("s = %v\n", s)
	fmt.Printf("s1 = %v\n", s1)
	fmt.Println("---------")
	
	// 使用copy函数实现地层slice一起进行拷贝
	s2 := make([]int, 3)	//s2 = [0,0,0]
	fmt.Printf("s2 = %v\n", s2)
	// 将 s 中的值，依次拷贝到 s2 中
	copy(s2, s)
	fmt.Printf("s2 = %v\n", s2)
}
```

结果：

```bash
s1 = [1 2]
s = [100 2 3]
s1 = [100 2]
---------
s2 = [0 0 0]
s2 = [100 2 3]
```

## map

1. **map 的三种声明方式：**

```go
package main

import "fmt"

func main() {
	// 声明 myMap1 是一种 map 类型 key 是string，value 也是string类型
	var myMap1 map[string]string
	if myMap1 == nil {
		fmt.Println("myMap1是一个空map")
	}
	
	// 使用 map 前，需要给 map 开辟空间
	myMap1 = make(map[string]string, 10)
	// 如果空间已满，map 会和 slice 一样自动动态分配空间
	myMap1["one"] = "java"
	myMap1["two"] = "go"
	myMap1["three"] = "javascript"
	fmt.Println(myMap1)

	// 第二种声明方式 可以不赋值容量
	myMap2 := make(map[int]string)
	myMap2[1] = "java"
	myMap2[2] = "go"
	myMap2[3] = "javascript"
	fmt.Println(myMap2)

	// 第三种声明方式 注意要有逗号
	myMap3 := map[string]string {
		"one" : "c++",
		"two" : "typescript",
		"three" : "c",
	}
	fmt.Println(myMap3)
}
```

结果：map 内本质是哈希表存储，不是顺序存储，因此是乱序的。

```bash
myMap1是一个空map
map[one:java three:javascript two:go]
map[1:java 2:go 3:javascript]
map[one:c++ three:c two:typescript]
```

2. **map 的使用方式**

使用 range 遍历，map 作为传参时，是**引用传递**。

```go
package main

import "fmt"

// map 作为传参，为引用传递
func printMap(cityMap map[string]string) {
	// 遍历
	for key, value := range cityMap {
		fmt.Println("key = ", key)
		fmt.Println("value = ", value)
	}
}

func main() {
	cityMap := make(map[string]string)
	// 添加
	cityMap["China"] = "Beijing"
	cityMap["Japan"] = "Tokyo"
	cityMap["USA"] = "NewYork"
	// 遍历
	printMap(cityMap)

	// 删除
	delete(cityMap,"China")
	// 修改
	cityMap["USA"] = "DC"
	fmt.Println("-----------")
	// 再次遍历
	printMap(cityMap)
}
```

结果：

```bash
key =  China
value =  Beijing
key =  Japan
value =  Tokyo
key =  USA
value =  NewYork
-----------
key =  Japan
value =  Tokyo
key =  USA
value =  DC
key =  China
value =  Beijing
```

## 面向对象

### 结构体struct

```go
package main

import "fmt"

// 声明一种新的数据类型 myint，是int的一个别名
type myint int

// 定义结构体
type Book struct {
	title string
	author string
}

func changeBook(book Book) {
	// 传递一个book的副本（值传递）
	book.author = "li4"
}

func changeBook2(book *Book) {
	// 传递为指针
	book.author = "wang5"
}

func main() {
	var a myint = 10
	fmt.Println("a = ", a)
	fmt.Printf("type of a = %T\n", a)
	fmt.Println("---------")

	var book1 Book
	book1.title = "Golong"
	book1.author = "zhang3"
	fmt.Printf("%v\n", book1)

	changeBook(book1)
	fmt.Printf("%v\n", book1)
	changeBook2(&book1)
	fmt.Printf("%v\n", book1)
}
```

结果为：

```bash
a =  10
type of a = main.myint
---------
{Golong zhang3}
{Golong zhang3}
{Golong wang5}
```

### 类的表示与封装

将结构体变成一个类，go语言中的类其实是将结构体绑定方法实现的。

**警示1：go 的 this. 与 java 中的 this. 不一样，go 中的 this. 是调用该方法的对象的一个副本（拷贝）**

在接下来的例子中，（this Hero）这种写法语法上没有任何问题，但是会发现修改的值没有生效，只考虑读是没有问题的，所以要修改成（this *Hero）

```go
package main

import "fmt"

type Hero struct {
	Name  string
	Ad    int
	level int
}

func (this *Hero) Show() {
	fmt.Println("Name =", this.Name)
	fmt.Println("Ad =", this.Ad)
	fmt.Println("level =", this.level)
}

// 此方法绑定到 Hero，this 表示当前对象
func (this *Hero) GetName() string {
	return this.Name
}

func (this *Hero) SetName(newName string) {
	// 设置名字
	this.Name = newName
}

func main() {
	// 创建一个对象
	hero := Hero{Name: "zhang3", Ad: 100, level: 1}
	hero.Show()
	hero.SetName("li4")
	hero.Show()
}
```

执行结果为：

```bash
Name = zhang3
Ad = 100
level = 1
Name = li4
Ad = 100
level = 1
```

**警示2：type Hero struct 中 Hero 为首字母大写，表示公有，大写表示其他包也可访问当前类定义对象**

类名、方法名、属性大小写都有不同含义，上例中的 Name、Ad 属性为首字母大写，公有，而 level 为小写，私有，仅能在本包中访问。

例如 fmt.Println() 中 P 就是大写，因为他是fmt包中的对外开放接口。

### 继承

go 语言的子类继承父类直接在结构体内写父类的名字，再添加新的属性。

定义子类对象的时候，有点套娃，子类里套上父类属性，或者直接先声明子类再加上每个属性的值。

```go
package main

import "fmt"

type Human struct {
	name string
	sax string
}

func (this *Human) Eat() {
	fmt.Println("Human.Eat()...")
}

func (this *Human) Walk() {
	fmt.Println("Human.Walk()...")
}

// 以上为父类 下面为继承子类
type SuperMan struct {
	Human	//SuperMan类继承了Human类的方法
	level int
}

// 重写父类方法Eat()
func (this *SuperMan) Eat() {
	fmt.Println("SuperMan.Eat()...")
}

func (this *SuperMan) Fly() {
	fmt.Println("SuperMan.Fly()...")
}

func main() {
	h := Human{"zhang3","female"}
	h.Eat()
	h.Walk()

	// 定义一个子类对象
	s := SuperMan{Human{"li4", "male"}, 100}
	
	// 也可以这么写
	/* 
		var s SuperMan
		s.name = "li4"
		s.sex = "male"
		s.level = 100
	*/
	
	s.Walk()	//父类的方法
	s.Eat()		//子类的方法（重写）
	s.Fly()		//子类的方法
}
```

结果：

```bash
Human.Eat()...
Human.Walk()...
Human.Walk()...
SuperMan.Eat()...
SuperMan.Fly()...
```

### 接口与多态

go 语言如果用上面这种继承方式，是实现不了多态的。

需要接口 interface 来实现多态。

```go
package main

import "fmt"

// interface 本质是一个指针
type AnimalIF interface {
	Sleep()				//动物睡觉
	GetColor() string	//获取动物颜色
	GetType()  string	//获取动物种类
}

// 具体的类
type Cat struct {
	// 继承接口不用在这里写接口名字，只需实现接口的方法即可
	color string	//猫的颜色
}

func (this *Cat) Sleep() {
	fmt.Println("Cat is Sleep...")
}

func (this *Cat) GetColor() string {
	return this.color
}

func (this *Cat) GetType() string {
	return "Cat"
}

// 具体的类
type Dog struct {
	color string
}

func (this *Dog) Sleep() {
	fmt.Println("Dog is Sleep...")
}

func (this *Dog) GetColor() string {
	return this.color
}

func (this *Dog) GetType() string {
	return "Dog"
}

func main() {
	var animal AnimalIF	// 接口的数据类型，父类指针
	animal = &Cat{"Green"}
    animal.Sleep()	//调用的就是Cat的Sleep()方法，多态的现象
	animal = &Dog{"Yellow"}
	animal.Sleep()	//调用Dog的Sleep()方法，多态的现象
}
```

执行结果为：

```bash
Cat is Sleep...
Dog is Sleep...
```

这种表现不是很直观，可以进行修改，提供一个方法：

```go
// 前面同：接口、猫类、狗类
func showAnimal(animal AnimalIF) {
	// 以接口为数据类型，即可以传入狗，也可传入猫
	animal.Sleep()	//多态，传什么对象调什么方法
	fmt.Println("color =", animal.GetColor())
	fmt.Println("kind =", animal.GetType())
}

func main() {
	cat := Cat{"Green"}
	dog := Dog{"Yellow"} 

	showAnimal(&cat)
	showAnimal(&dog)
}
```

执行结果为：

```bash
Cat is Sleep...
color = Green
kind = Cat
Dog is Sleep...
color = Yellow
kind = Dog
```

**总结：**

不同的语言可能对多态的定义会有区别，基本上多态的作用与效果是通用的，影响作业模式，

**基本要素：**

1. **一定有一个父类（即有接口）**
2. **且一定有一个子类（一定实现了父类的全部接口）**
3. **父类类型的变量（指针）指向（引用） 子类的具体数据变量**【如上面例子用父类animal的接口指向一个子类的具体对象 cat ，通过父类调用接口时，最终调用的就是子类的 Sleep()】

### interface空接口万能类型与类型断言机制

go 和其他语言一样有一个通用的万能类型，interface{} ，表示空接口，可以作为万能类型，类似于 java 中的 Object 类

interface{} 还提供了一种类型断言机制，可以通过 .( ) 判断此 interface{} 指向哪个具体的类型。

```go
package main

import "fmt"

func myFunc(arg interface{}) {
	// arg 表示万能类型，可以传入任何值
	fmt.Println("myFunc is called...")
	fmt.Println(arg)

	// interface{} 该如何区分 此时引用的底层数据类型到底是什么？

	// interface{} 提供了”断言“的机制
    
	// arg 所指向的变量类型是否为 string,返回两个值
	value, ok := arg.(string)
	if !ok {
		fmt.Println("arg is not string type")
	} else {
		fmt.Println("arg is string type, value =", value)
		fmt.Printf("value type is %T\n", value)
	}
}

type Book struct {
	author string
} 

func main() {
	book := Book{"Golang"}
	myFunc(book)
	myFunc(100)
	myFunc("abc")
}
```

执行结果为：

```bash
myFunc is called...
{Golang}
arg is not string type
myFunc is called...
100
arg is not string type
myFunc is called...
abc
arg is string type, value = abc
value type is string
```

结论：

**如果想定义一种数据结构，可以传入任意类型，可以把传入类型改为 interface{} 空接口。**

类型断言可以返回两个值：一个是值，一个是 bool。

## 反射

### 变量的内置pair结构

在学反射之前，要明白上面讲的类型断言为什么会成功，

因为变量分为两部分构成：类型 type  和值 value，而 type 又可以分为静态类型 static type 和具体类型 concrete type，**静态类型与具体类型二选一**。

static type 即常用的 int, string...基本类型。

concrete type 即 interface 所指向的具体数据类型，系统看得见的类型。

而变量 type + value = pair，每个变量内部都有这么一个 pair对，**反射即通过一个变量得到 type**

```go
package main

import "fmt"

func main() {
	// a - pair<static type:string, value:"bianqiang">
	var a string
	a = "bianqiang"

	// allType - pair<static type:string, value:"bianqiang">
	// allType = a ，即 allType 的 type指针指向 string, value指针指向 “bianqiang”
	var allType interface{}
	allType = a

	// value, ok = allType.(string)
	str, _ := allType.(string)
	fmt.Println(str)
}
```

上面的变量 a 的 pair对是一起传递的。

```bash
bianqiang
```

