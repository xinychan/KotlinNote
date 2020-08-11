## 内联函数

### 内联函数通过与高阶函数配合，实现代码优化

    inline fun action(run: () -> Unit) {
        println("Hello")
        run()
        println("World")
    }

    fun main() {
        // 使用 inline 后，创建 Lambda 表达式的开销，和调用 action 的开销都没有
        action {
            println("Kotlin")
        }
        // 使用内联后，上面action方法相当于以下代码
        println("Hello")
        println("Kotlin")
        println("World")
    }

### 内联高阶函数的 return

    fun main() {
        val ints: IntArray = intArrayOf(1, 2, 3, 4)
        ints.forEach {index ->
            if (index == 3) {
                // 跳出这一次内联函数调用；相当于 continue
                return@forEach
            }
            println("main $index")
        }
    }

### non-local return

    inline fun nonLocalReturn(act:()->Unit){
        act.invoke()
    }

    fun main() {
        nonLocalReturn {
            // 从main函数返回
            return
        }
    }

### crossinline 禁止外部返回

    inline fun nonLocalReturn(crossinline act:()->Unit){
        act.invoke()
    }

    fun main() {
        nonLocalReturn {
            // 使用crossinline后，禁止从main函数返回
            // return
        }
    }

### 内联函数的限制

- public/protected 的内联方法只能访问对应类的 public 成员
- 内联函数的内联函数参数不能被存储（赋值给变量）
- 内联函数的内联函数参数只能传递给其他内联函数
