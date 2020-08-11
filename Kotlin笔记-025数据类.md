## 数据类

### 数据类定义：data class

    // 数据类；属性作为参数传给主构造器，且至少要有一个属性
    // 数据类默认被final修饰，不可被继承
    data class Album(val id: Long, val name: String, val author: String)

    fun main() {
        // 数据类的结构
        val album = Album(1, "Kotlin", "JetBrains")
        val id: Long = album.component1()
        val name: String = album.component2()
        val author: String = album.component3()
    }

### 数据类合理使用

- 数据类最好不需要定义任何函数，只需要定义属性
- 属性类型最好为基本类型，String，或者其他 Data Class，保证数据类全是数据
- 属性最好为 val 不可变，保证数据一致
