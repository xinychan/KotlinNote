## 常量和变量

### 变量的定义

    fun action() {
        // 可读写变量
        var a: Int = 0
        a = 1

        // 只读变量
        val b: Int = 0
        // 不可再赋值
        // b = 1
    }

### 常量的定义

    // 常量只能定义在全局范围
    // 只能修饰基本类型
    // 定义时必须立即初始化
    const val index:Int = 3

    fun action() {
        println("index = $index")

        // 常量不可定义在局部范围
        // const val index:Int = 3
    }
