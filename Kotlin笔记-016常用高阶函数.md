## 常用高阶函数

| 函数名 | 介绍                            |
| ------ | ------------------------------- |
| let    | val r = X.let{x -> R}           |
| run    | val r = X.run{this:X -> R}      |
| also   | val x = X.also{x -> Unit}       |
| apply  | val x = X.apply{this:X -> Unit} |
| use    | val r = Closeable.use{c -> R}   |

使用示例：

    class Student(var name: String, var age: Int)

    fun main() {
        val student: Student = Student("Kotlin", 18)

        // 调用者本身作为参数传入，返回值为 Lambda 表达式返回值
        val age: Int = student.let {
            println(it.name)
            it.age
        }
        // 调用者作为Receive传入，返回值为 Lambda 表达式返回值
        val age2: Int = student.run {
            println(name)
            this.age
        }
        // 调用者本身作为参数传入，返回值为自身类型
        val student1: Student = student.also {
            it.name = "Java"
            it.age = 18
        }
        // 调用者作为Receive传入，返回值为自身类型
        val student2: Student = student.apply {
            this.name = "Java"
            this.age = 18
        }
        // 在 use 方法作用域之外，相关的IO流和异常都会被释放和处理
        File("file-path").inputStream().reader().buffered().use {
            println(it.readLine())
        }
    }
