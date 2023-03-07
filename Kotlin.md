## Kotlin学习资源

-   [](https://thoughtworks.udemy.com/course/kotlinmasterclass/)[https://thoughtworks.udemy.com/course/kotlinmasterclass/](https://thoughtworks.udemy.com/course/kotlinmasterclass/)
-   [](https://thoughtworks.udemy.com/course/build-restful-apis-using-kotlin-and-spring-boot/)[https://thoughtworks.udemy.com/course/build-restful-apis-using-kotlin-and-spring-boot/](https://thoughtworks.udemy.com/course/build-restful-apis-using-kotlin-and-spring-boot/)

# Kotlin笔记

<aside> 💡 `Kotlin` 是现代的、简洁的、安全的、开源的编程语言，是当今时代流行的JVM语言之一。

它还可以与Java和其他语言互操作，并提供了许多在多个平台之间重用代码的方法，以实现高效编程。由 `Jet Brain` 和 `Google` 主导

</aside>

以下是一段 `Kotlin` 代码示例：

```kotlin
fun main() {
    val name = "Kotlin"
    println("Hello, $name!")
}
```

这段代码定义了一个`main`函数，其中声明了一个名为`name`的字符串变量，然后使用字符串模板打印了一条消息。在字符串模板中可以用 `$` 写 `kotlin 的表达式`

## 基本语法

### 声明变量

> 通过 `var` & `val` 声明变量

```kotlin
// val 声明的是 不可变的(immutable)
val name : String = "Dilip"

// var 声明的是 可变的(mutable)
var age : Int = 33
```

### 类型

> 在Kotlin中，基本类型和包装类型之间没有区别

**kotlin 会根据赋值类型 自动推断 变量类型 ( 和 TypeScript 一样) , 不需要显式声明**

```kotlin
var age = 35   // age : Int

val course = "kotlin - spring"

println("course: $course and the length is ${course.length}")
```

### 条件判断

<aside> 💡 `kotlin` 的 `if - else` 是一个表达式 (expression)

</aside>

```kotlin
var result = if (name.length == 4) {
	 println("Name is Four Characters")
	 name
} else {
	 println("Name is Not Four Characters")
	 name
}
```

> `kotlin` 的 `when` 允许我们在处理多个条件时编写简洁而表达力强的代码

```kotlin
val position = 1

val medal = when(position) {
    1 -> "GOLD"
    2 -> "SILVER"
    3 -> {
        println("Inside position 3")
        "BRONZE"
    }
    else -> "NO MEDAL"
}
println(medal)
```

### 循环语句

**Ranges**
```kotlin
// 用 .. 创建 一个起点到终点的范围
val range = 1..10
for (i in range){
		println(i) 
}

// 倒序
val reverseRange = 10 down to 1
for (i in reverseRange){
		println(i) 
}

// 跳过
for (i in reverseRange step 2){
	  println(i)
}

```

**While & doWhile***

```kotlin
// while  先进行条件判断 再执行循环
fun exploreWhile() {
	var x = 1
	while (x < 5) {
		println("value of x is: $x")
		x++
	}
}
exploreWhile()

// do while 先执行循环体再条件判断
fun exporeDoWhile() {
	var i = 0
	do {
		println("Inside do while : $i")
		i++
	} while ( i < 5 )
}
```

### break & label & return
在 Kotlin 中任何表达式都可以用标签（label）来标记。 标签的格式为标识符后跟 @ 符号，例如：abc@、fooBar@都是有效的标签。 要为一个表达式加标签，我们只要在其前加标签即可。
```kotlin
// break 跳出循环
for (i in 1..5 ) {
	println("i is  $i ")
	if( i == 3) break
}

// label  
fun label() {
	loop@ for(i in 1..5 ) {
		println("i in label $i: ")
		innerLoop@ for (j in 1..10) {
			//if( j == 2 ) break@innerLoop
			if( j == 2 ) break@loop	
		}
	}
}

// return 返回语句, 后面的语句不再执行
listOf( 1,2,3,4,5).forEach each@ {
	// if( it == 3 ) return@forEach
	if( it == 3) return@each
}
```

### 函数

**Unit — 没有返回值的函数在Kotlin中被表示为Unit**

```kotlin
// 不需要主动声明 Unit 类型, 编译器会自动推断
fun printHello() : Unit {
		println("Hello")
}
```

**函数简写**

```kotlin
fun addition (x: Int , y : Int) : Int {
		return x + y 
}

// 可以被简写成以下样子
fun addition ( x: Int, y: Int)  = x + y
```

**默认参数**

```kotlin
// 如果没有传入 实参, 则参数是默认值
fun printPersonDetails(name: String, email: String = "",
											 dob: LocalDate = LocalDate.now()) {
		println("Name is $name and the email is $email and the dob is $dob ")
}
```

**Named Argument**


## class

<aside> 💡 类 是面向对象的重要概念, 可以看做 创建对象的蓝图, 如 汽车图纸(class) 批量 生产汽车 (object)

</aside>

```kotlin
// 定义一个类 -> Person
class Person {
		fun action() {
			println("Person walks")
	}
}

// 类的实例 -> person 对象 
val person = Person() // 不需要 new 关键词 , 即可实例化对象

person.action()
```

### Constructor

**构造器, 可以看做创建对象的初始值**

```kotlin
// 在 Person 类 这个例子中, name , age 就是构造器
class Person(val name: string, val age: Int ) {
		fun action() {
				println("Person walks")	
	}
}

// 填入构造器所需要的参数 创建类的实例
val person = Person("Alex" , 25)
```

**你也可以用传统的方式写构造器, 类似 java**

```kotlin
// 这是另外一种定义构造器的方法

class Item() {
	var name : String = ""
	constructor( _name : String) : this() {
			 name = _name
	} 
}

// 1. constructor 关键字
// 2. this() 必须调用 this() 来指向内部变量
```

**推荐使用的 第一种构造器方法, 且有默认参数**

```kotlin
class Person (val name: String = "", 
							val age: Int = 0 ) {

			fun action() {
					println("Person Walks")
	}
}
```

**init 初始化代码**

> `init` 代码块可以用来在实例创建期间运行一些初始化逻辑。

```kotlin
init {
	println("Inside Init Block")
}
```

### data class

-   `拥有数据` 的 类 都可以 被归类为 `data class`
	-   **DTOs, domain classes and value object classes fall under this category**
	-   在 `java` , 这些类 都被称为 `java beans`


```kotlin
data class Course(
	val id : Int,
	val name: String,
	val author: String
)

Automatically generates the equals(), hashCode() and toString() methods

// 不需要 lombok
```