## 泛型

### 泛型基本声明方法

    // 函数声明泛型
    fun <T> action(x: T, y: T): T {}
    // 类声明泛型
    class Action<T>{}

### 泛型的约束

    // 泛型的约束：让泛型实现接口或者继承某个类
    fun <T : Comparable<T>> maxOf(x: T, y: T): T {
        return if (x > y) x else y
    }

    fun main() {
        val max: String = maxOf("Kotlin1", "Kotlin2")
        println("max $max")
    }

也可以对泛型多个约束：

    // 泛型多个约束；使用 where 继承或实现多个接口或类型
    fun <T> callMax(x: T, y: T) where T : Comparable<T>, T : () -> Unit {
        if (x > y) x() else y()
    }

以及多个泛型参数：

    // 多个泛型参数；比如 Map 就是多个泛型参数
    fun <T, R> callMax2(x: T, y: T): R where T : Comparable<T>, T : () -> R {
        return if (x > y) x() else y()
    }

### 泛型的型变

泛型的型变包括协变和逆变

    fun main() {
        // Java 的 PECS 法则：「Producer-Extends, Consumer-Super」
        // <? extends> 作为生产者向外提供数据被消费
        // Java 泛型通配符 ? extends 使泛型支持协变，但是「只能读取不能修改」，这里的修改仅指对泛型集合添加元素，如果是 remove(int index) 以及 clear 当然是可以的。
        // <? super> 作为消费者只能用来添加数据（消费数据）
        // Java 泛型通配符 ? super 使泛型支持逆变，但是「只能修改不能读取」，这里说的不能读取是指不能按照泛型类型读取，你如果按照 Object 读出来再强转当然也是可以的。

        // 使用关键字 out 来支持协变，等同于 Java 中的上界通配符 ? extends
        // 相当于 Java 中 List<? extends TextView>
        var textViews: List<out TextView>
        // 使用关键字 in 来支持逆变，等同于 Java 中的下界通配符 ? super
        // 相当于 Java 中 List<? super TextView>
        var textViews2: List<in TextView>
    }

### 协变点与逆变点

协变点：函数返回值类型为泛型参数为协变点

    interface Orange

    class OrangeStore<out T : Orange> {
        // 协变点
        fun getOrange(): T {
            TODO()
        }
    }

逆变点：函数参数类型为泛型参数为逆变点

    interface Orange

    class OrangeStore<in T : Orange> {
        // 逆变点
        fun getOrange(x: T) {
            TODO()
        }
    }

### UnsafeVariance

    interface Orange

    class OrangeStore<out T : Orange> {
        // 协变参数，但是用了逆变点，违反了型变约束
        // 使用 UnsafeVariance 排除编译器报错，让用户自己处理型变
        fun getOrange(x: @UnsafeVariance T) {
            TODO()
        }
    }

### 星投影：\*

`*` 描述一个未知类型，可用在变量类型声明的未知

`*` 替换的类型如果是协变点，协变点返回泛型参数上限类型

`*` 替换的类型如果是逆变点，逆变点接受泛型参数下限类型

星投影用于协变点

    class Action<out T : CharSequence, out R : Number> {

        fun getTypeA(): T {
            TODO()
        }

        fun getTypeB(): R {
            TODO()
        }
    }

    fun main() {
    	// 协变点返回泛型参数上限类型
        val action: Action<*, *> = Action<String, Int>()
        val type1: CharSequence = action.getTypeA()
        val type2:Number = action.getTypeB()
    }

星投影用于逆变点

    class Action<in T, in R> {
        fun getType(x: T, y: R) {
            TODO()
        }
    }

    fun main() {
        // 逆变点接受泛型参数下限类型；下限类型为 Nothing，因为 Nothing 是所有类型的子类
        val action: Action<*, *> = Action<String, Int>()
        // 只能传入 Nothing，但是 Nothing 没有实例，方法无法调用
        // action.getType(Nothing,Nothing)
    }

星投影适用范围：

- 不能直接或间接应用在属性或者函数上，不能传给函数当参数或者类中当属性
- 适用于类型描述的场景
- 综上，星投影适用于声明处，不适用于定义处

### 内联特化：inline reified

Kotlin 泛型和 Java 泛型一样，都会发生类型擦除

比如 `List<String>` 和 `List<Int>`，编译成字节码后，只留下 `List` 类型

而 `C#` 和 `C++` 中的 `List<String>` 和 `List<Int>`，编译后会生成 `List<String>` 和 `List<Int>`两个类型

    // 因为有类型擦除的限制，所以以下场景泛型类型无法当做真实类型
    fun <T> action(t:T){
        val t = T() // 无法编译；T 类型的构造器未知
        val tArray = Array<T>(10, TODO()) // 无法编译；数组中类型不会擦除，但是类型未知
        val tClass = T::class.java // 无法编译；类型被擦除，类型未知
        val tList = ArrayList<T>() // 可以编译；因为集合中反正会类型擦除
    }

为了避免类型擦除的限制，Kotlin 使用内联特化来解决

    // 内联特化之后，泛型类型可以当做真实类型
    inline fun <reified T> action(t:T){
        // 比如外部调用该方法，传入参数为 String，那么 T 类型将特化成 String 类型
        val t = T() // 仍然无法编译；T 类型的构造器未知
        val tArray = Array<T>(10, TODO()) // 可以编译；可以得到正确的类型
        val tClass = T::class.java // 可以编译；可以得到正确的类型
        val tList = ArrayList<T>() // 可以编译；因为集合中还是会类型擦除
    }
