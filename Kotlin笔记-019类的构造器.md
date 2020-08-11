## 类的构造器

### 构造器的基本用法

    // 使用 var/val 构造器参数，就同时定义了类属性，类全局可见
    // 未使用 var/val 构造器内部可见（init块，属性初始化）
    class People(var age:Int,var name:String)

### 主构造器默认参数

    // 主构造器默认参数在Java代码中可以以重载形式调用
    class People
    @JvmOverloads
    constructor(var age:Int,var name:String = "Kotlin")

### 主构造器

constructor 主构造器只有一个，副构造器可以有多个，但是所有副构造器必须直接或者间接调用主构造器
