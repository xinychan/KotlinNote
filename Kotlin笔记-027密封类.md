## 密封类

### 密封类定义：sealed class

    // 密封类是一个抽象类
    // 密封类的子类必须定义在自身相同的文件中，类似枚举类，枚举类值有限，密封类子类有限
    sealed class Tree{
        // 构造器默认私有，不允许外部调用，因此外部文件不能继承密封类
        // private constructor()
    }
    object Tree1 : Tree() {}
    class Tree2(val id: Int) : Tree() {}
    class Tree3(val name: String) : Tree() {}

    fun main() {
        // 子类分支的使用
        val treeAct: Tree = Tree2(0)
        when (treeAct) {
            is Tree1 -> println("Tree1")
            is Tree2 -> println("Tree2")
            is Tree3 -> println("Tree3")
        }
    }

### 密封类与枚举类的区别

| 状态     | 密封类   | 枚举类   |
| -------- | -------- | -------- |
| 状态实现 | 子类继承 | 类实例化 |
| 状态可数 | 子类可数 | 实例可数 |
| 状态差异 | 类型差异 | 值差异   |
