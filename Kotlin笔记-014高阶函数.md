## 高阶函数

**高阶函数定义：**

**函数的参数类型包含函数类型，或者返回值类型是函数类型，那么这个函数就是一个高阶函数。**

常见的 forEach 函数就是一个高阶函数，其参数类型为一个函数类型。

    fun action(){
        val ints:IntArray = intArrayOf(1,2,3,4)
    	// 函数的最后一个参数为函数类型，那这最后一个参数可以写在大括号里
        ints.forEach { index ->
            println(index)
        }
    	// 当函数的参数只有一个时，默认it代指这个参数
        ints.forEach {
            println(it)
        }
    }

IntArray.forEach 源码：

    public inline fun IntArray.forEach(action: (Int) -> Unit): Unit {
        for (element in this) action(element)
    }
