### Lambda 表达式

Kotlin 上的 Lambda 表达式本质上是匿名函数的语法糖。

当定义一个函数，函数没有名称时，可使用 Lambda 表达式，直接写函数体赋值给变量，省略函数名称。

    // 匿名函数定义给变量 func
    val func: () -> Unit = fun() {
        println("Hello")
    }
    // 转成Lambda表达式
    val func2: () -> Unit = {
        println("Hello")
    }

    // Lambda 表达式最后一行为返回值
    val lam: (Int) -> String = { index ->
        val result: Int = index + 1
        result.toString()
    }

Kotlin 与 Java 中的 Lambda 表达式的区别在于：

Kotlin 中的 Lambda 表达式本身是一个函数，只是没有名称，而函数是有对应的类型的，所以 Lambda 表达式可赋值给变量。

Java8 中的 Lambda 表达式的类型必须是符合 SAM 的接口，只有符合 SAM 的接口才支持 Lambda 表达式。
