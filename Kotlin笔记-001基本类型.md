## 基本类型

### 基本类型

Java 的基本类型分 int/Integer 等，需要拆箱和装箱；

Kotlin 的基本类型不需要手动拆装箱，并且当类型为可空类型时，基本类型可以为 null；

Kotlin 的所有类型都有一个父类 Any，相当于 Java 中的 Object；

Kotlin 的所有类型都有一个子类 Nothing，类似 java.lang.Void；

| 类型   | Kotlin         | Java                        |
| ------ | -------------- | --------------------------- |
| 字节   | Byte           | byte/Byte                   |
| 整型   | Int & Long     | int/Integer & long/Long     |
| 浮点型 | Float & Double | float/Float & double/Double |
| 字符   | Char           | char/Character              |
| 字符串 | String         | String                      |
| 布尔值 | Boolean        | boolean/Boolean             |

### 声明变量

    // 可读写变量，后面可以再赋值
    var a:Int = 1
    // 只读变量，后面不可再赋值；相当于Java中final变量
    val b:String = "Kotlin"
    // Kotlin 中声明Long，必须使用大写L
    val c:Long = 123456789L
    // Kotlin 中声明Double，不用D结尾后缀，直接使用小数点形式
    val d:Double = 1.1

### 数值类型转换

    // 不能直接像Java一样，可以数值类型隐式转换（Int转Long），而是需要调用方法显式转换
    val e:Int = 10
    val f:Long = e.toLong()

### 无符号类型(V1.3)

无符号类型全部为正数；

无符号类型范围 = 有符号类型除去负数范围 \* 2

| 有符号类型 | 无符号类型 |
| :--------: | :--------: |
|    Byte    |   UByte    |
|   Short    |   UShort   |
|    Int     |    UInt    |
|    Long    |   ULong    |
|   String   |   String   |

### 相等判断

    val name1:String = "Kotlin"
    val name2:String = "Kotlin"
    // 比较内容
    println(name1 == name2)
    // 比较引用
    println(name1 === name2)

### 字符串

    // 支持字符串模板；在两个双引号中使用$符号
    var name:String = "Kotlin"
    println("tag $name")
    println("name ${name.length}")

    // 支持 RawString；使用三个双引号
    var content:String = """
    	Hello
    	Kotlin
    	基本类型
    """
