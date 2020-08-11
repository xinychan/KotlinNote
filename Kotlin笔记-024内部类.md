## 内部类

### 内部类定义

    // 内部类
    class Outer {
        // 非静态，实例持有外部类实例引用
        inner class Inner
        // 静态
        class StaticInner
    }

    fun main() {
        val inner: Outer.Inner = Outer().Inner()
        val staticInner: Outer.StaticInner = Outer.StaticInner()
    }

### 内部 Object

    // 内部Object
    object OuterObject{
        // 内部Object不存在非静态的情况，不可用 inner 修饰
        object StaticInnerObject
    }

    fun main() {
        val staticInnerObject = OuterObject.StaticInnerObject
    }

### 匿名内部类

    fun main() {
        // 匿名内部类
        val runnable = object : Runnable {
            override fun run() {
            }
        }
        // 交叉类型： Cloneable & Runnable
        val runnable2 = object : Cloneable,Runnable {
            override fun run() {
            }
        }
    }

### 本地类与本地函数

    fun main() {
        // 本地类；嵌套在函数里面
        class LocalClass{}
        // 本地函数；嵌套在函数里面
        fun localFunc(){}
    }
