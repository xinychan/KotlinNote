## 空类型安全

Kotlin 在定义对象时，分为可空类型，和不可空类型。

    // 不可空类型
    var str1:String = "Kotlin"
    // 不可以赋值为null
    // str1 = null
    var size:Int = str1.length

    // 可空类型
    var str2:String? = null
    // 可空类型调用后返回的是可空类型
    var size2:Int? = str2?.length

### 可空类型与不可空类型的转换

    var str3: String? = "Kotlin"
    // 可空类型强转成不可空类型；谨慎使用，当为null时会报空指针异常
    var size3: Int = str3!!.length

    var str4: String? = "Kotlin"
    // 安全调用；当为null时不会报空指针异常
    var size4: Int? = str4?.length
    // 使用elvis运算符，返回值为不可空类型
    // 若第一个运算数不为null，运算结果就是第一个运算数
    // 若第一个运算数为null，运算结果就是第二个运算数
    var size5: Int = str4?.length ?: 0

    // 不可空类型是可空类型的子类
    // 不可空类型可以赋值给可空类型
    var sum1:Int? = size5
    // 可空类型不可赋值给不可空类型
    // var sum2:Int = size4

### 平台类型

Kotlin 支持 Java/JavaScript/Native 等平台，当 Kotlin 与 Java 等混合使用时，Kotlin 使用的对象类型是平台类型。

比如在 Java 中声明一个返回值为 String 的方法：

    public class Apple {
        public String useName(){
            return "Apple";
        }
    }

Kotlin 调用：

    var name = Apple().useName()

    var size:Int = name.length

此时 name 这个变量，就是一个平台类型--String!。

Kotlin 不能分辨平台类型是否为 null，当返回为 null 时会空指针异常。

使用安全访问可以避免空指针异常，返回值为可空类型。

    var name = Apple().useName()

    var size:Int? = name?.length

当然，如果使用注解，则 Kotlin 可以识别为对应的可空/不可空类型。

使用 NonNull 注解：

    // 使用 NonNull 注解，Kotlin会当成 String
    public class Apple {
        @NonNull
        public String useName(){
            return "null";
        }
    }

Kotlin 使用时：

    var name:String = Apple().useName()

    var size:Int = name.length

使用 Nullable 注解：

    // 使用 Nullable 注解，Kotlin会当成 String?
    public class Apple {
        @Nullable
        public String useName(){
            return "null";
        }
    }

Kotlin 使用时：

    var name:String? = Apple().useName()

    var size:Int? = name?.length
