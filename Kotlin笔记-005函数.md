## 函数

### 函数的定义

    // 函数名getName,参数String，返回值Unit（相当于Java中的void）
    fun getName(name:String):Unit {
        println("name-$name")
    }

### 函数的类型

函数的类型由函数的参数，以及返回值决定。

在类中声明的方法，其类型必须包含所在的类对象。

| 函数                                           | 函数的类型                 |
| ---------------------------------------------- | -------------------------- |
| fun foo() {}                                   | () -> Unit                 |
| fun foo(num:Int):String {}                     | (Int) -> String            |
| class Foo{ fun bar(p0:Int,p1:String):String{}} | Foo.(Int,String) -> String |

注意：

Foo.(Int,String) -> String 等价于 (Foo,Int,String) -> String；

这两个类型本质上是一样的，只是写法不同。

### 函数的引用

函数的引用可用于函数传递，可直接赋值给变量。

函数的引用与函数的参数/返回值无关，只和函数名有关。

在类中声明的函数，未绑定 Receive 时，其引用必须包括所在的类对象。

| 函数                                    | 引用     |
| --------------------------------------- | -------- |
| fun foo(){}                             | ::foo    |
| fun foo(p0:Int):String{}                | ::foo    |
| class Foo{ fun bar(p0:String):String{}} | Foo::bar |

上述两个 foo 函数，其引用都是::foo，调用时会具体判断是调用哪个方法，可以通过声明函数类型来避免函数引用错误。

    class Foo {
        fun bar(p0: String): String {
            return "Hello $p0"
        }
    }

    fun action() {
        val foo = Foo()
        // 绑定了 Receive 后，函数类型就不再需要所在类的对象了
        val bar0: (String) -> String = foo::bar
        val bar1: Function1<String, String> = foo::bar
        // 未绑定 Receive，函数类型需要所在类的对象
        val bar2: (Foo, String) -> String = Foo::bar
        val bar3: Foo.(String) -> String = Foo::bar
        val bar4: Function2<Foo, String, String> = Foo::bar
    }

如上述写法，函数类型可用 Function1，Function2，Function3 等方式来表示。

Function1<String, String> 表示有一个参数，类型为 String，返回值为 String。

Function2<Foo, String, String>表示有两个参数，类型为 Foo 和 String，返回值为 String。

其余 Function 写法类似，最后一个表示返回值，前面的表示传入参数。

Function0 表示只有返回值，没有传入参数。

### 变长参数

    // vararg 表示可变参数
    fun getSum(vararg ints: Int) {
        println("show ${ints.size}")
    }

    fun main() {
        getSum(1, 2, 3, 4)
    }

### 默认参数

    // 第三个参数有默认值 false
    fun setAction(x: Int, y: String, z: Boolean = false) {
        println("Hello")
    }

    fun main() {
        // 传入完整的参数
        setAction(0, "Hello", true)
        // 已经有默认值的参数可不传，使用默认值
        setAction(0, "Hello")
    }

### 具名参数

    fun setAction(x: Int = 0, y: String, z: Boolean = false) {
        println("Hello")
    }

    fun main() {
        // 传入完整的参数
        setAction(0, "Hello", true)
        // 使用具名参数，只需要传入参数y
        setAction(y = "Hello")
    }
