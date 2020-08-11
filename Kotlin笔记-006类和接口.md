## 类和接口

### 类的定义

    // 默认为 public；类如果没有内容，可以省略大括号
    class Simple

    class Simple2 {
        // 默认情况下，属性定义时必须初始化
        var index: Int = 0

        fun action() {}
    }

    class Simple3 {
        // 通过构造方法来初始化
        var index: Int

        // 构造器
        constructor(x: Int) {
            this.index = x
        }
    }

    class Simple4 {
        // 可声明多个副构造器
        constructor() {}
        constructor(x: Int) {}
        constructor(x: Int, y: String) {}
    }

    // 主构造器与类写在一起，且只有一个主构造器
    class Simple5 constructor(x: Int) {
        var index:Int = x
        // 副构造器必须直接或者间接调用主构造器
        constructor(x: Int, y: String) : this(x) {}
        constructor(x: Int, y: String, z: Int) : this(x, y) {}
    }

    // 主构造器简略写法
    class Simple6(x: Int) {
        var index: Int = x
        // 副构造器必须直接或者间接调用主构造器
        constructor(x: Int, y: String) : this(x) {}
        constructor(x: Int, y: String, z: Int) : this(x, y) {}
    }

    // 参数直接在主构造器中定义
    class Simple7(var index: Int) {
        // 副构造器必须直接或者间接调用主构造器
        constructor(x: Int, y: String) : this(x) {}
        constructor(x: Int, y: String, z: Int) : this(x, y) {}
    }

### 接口的定义

    // 接口都是public，可省略声明
    interface SimpleInf{
        // 没有实现的方法，必须是public，可省略声明
        fun action()

        // 已经实现的方法，可以是private
        private fun action2(){
            println("Hello")
        }
    }

### 接口的实现

    interface SimpleInf {
        fun action()
    }

    // 接口的实现
    class SimpleClass : SimpleInf {
        // 重写方法时，使用 override 关键字
        override fun action() {
        }
    }

### 抽象类定义

    abstract class AbsClass {
        abstract fun action1()
        // 非抽象方法默认不可复写，要子类可以复写必须使用 open 关键字
        open fun action2() {}
        // 方法默认使用final修饰，所以不可复写；可省略final声明
        final fun action3() {}
    }

    class SimpleClass: AbsClass() {
        override fun action1() {
        }
        override fun action2() {
            super.action2()
        }
    }

### 类的继承

    // 类默认使用final修饰，不可被继承
    // 使用open关键字，类可以被继承
    open class SuperClass {
        // 方法默认使用final修饰，不可复写
        fun action1(){}
        // 使用open关键字，方法可以被子类复写
        open fun action2(){}
    }

    // 继承父类，必须调用父类的构造方法
    // SuperClass()是带括号的，表明调用SuperClass的默认无参构造方法
    class SimpleClass: SuperClass() {

        // 不能复写action1，只能调用
        var x = action1()

        // 可以复写action2
        override fun action2() {
            super.action2()
        }
    }

### 类的属性

    class Student(age: Int, name: String) {
        // 在属性的get/set方法中进行打印操作
        var age: Int = age
            get() {
                println("Hello")
                return field
            }
            set(value) {
                field = value
                println("Hello")
            }
        // 属性默认有get/set方法；可省略
    	// 属性默认是public
        var name: String = name
    }

    fun action(){
        // 属性的引用；属性未绑定类实例对象，需要传入类实例对象
        val ageRef: (Student) -> Int = Student::age
        val ageRef2: Function1<Student, Int> = Student::age

        // 属性的引用；属性绑定类实例对象，不需要再传入类实例对象
        val student: Student = Student(18, "Nemo")
        val nameRef: () -> String = student::name
        val nameRef2: Function0<String> = student::name
    }
