## 分支表达式

### if/else 表达式

    fun action(){
        var index:Int = 5
        if (index < 10) {
            index = 0
        } else {
            index = 10
        }
    }

等价于：

    fun action(){
        var index:Int = 5
        index = if (index < 10) {
            0
        } else {
            10
        }
    }

### when 表达式

    // 用于范围判断
    fun action(){
        var index: Int = 1
        var x: String = when (index) {
            0 -> "0"
            1 -> "1"
            else -> "null"
        }
    }

    // 用于类型判断
    fun action(){
        var index: Any = "Kotlin"
        var x: Int = when (index) {
            is String -> 0
            is Int -> 1
            else -> 2
        }
    }

### try/catch 表达式

    fun action(){
        var a: Int = 10
        var b:Int = 1

        var c:Int = 0
        c = try {
            a/b
        } catch (e: Exception) {
            println(e.toString())
            0
        }
    }
