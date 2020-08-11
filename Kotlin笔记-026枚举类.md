## 枚举类

### 枚举类定义:enum class

    // 枚举类；枚举的父类是 Enum，不能继承其他类，只能实现其他接口
    enum class Logo {
        Action1, Action2, Action3
    }

    fun main() {
        val act1Str: String = Logo.Action1.name // Action1
        val act1id: Int = Logo.Action1.ordinal // 0
        val act2Str: String = Logo.Action2.name // Action2
        val act2id: Int = Logo.Action2.ordinal // 1
    }

### 枚举类定义构造器

    enum class Logo2(val id: Int) {
        Action1(0), Action2(1)
    }

### 实现接口

    // 实现接口-统一实现
    enum class Logo3 : Runnable {
        Action1, Action2;

        override fun run() {
            println("Kotlin")
        }
    }

    // 实现接口-各自实现
    enum class Logo4 : Runnable {
        Action1 {
            override fun run() {
                println("Action1")
            }
        },
        Action2 {
            override fun run() {
                println("Action2")
            }
        }
    }

### 用于分支表达式

    fun main() {
        // 可用于分支表达式
        val logo: Logo = Logo.Action1

        val value = when (logo) {
            Logo.Action1 -> println("I am Action1")
            Logo.Action2 -> println("I am Action2")
            Logo.Action3 -> println("I am Action3")
        }
    }

### 枚举的区间用法

    fun main() {
        // 枚举的区间
        val range: ClosedRange<Logo> = Logo.Action1..Logo.Action2
        val r1 = Logo.Action2
        val isInRange = r1 in range
    }
