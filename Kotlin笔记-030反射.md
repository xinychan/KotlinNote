## 反射

Kotlin 中反射需要使用单独反射 API，需要引入反射的依赖。

    implementation "org.jetbrains.kotlin:kotlin-reflect:1.3.61"

### 反射作用

- 列出类型的所有属性，方法，内部类等
- 调用给定名称以及签名的方法或访问指定名称的属性
- 通过签名信息获取泛型实参的具体类型
- 访问运行时注解及其信息，完成诸如或者配置操作

### 反射的数据结构

- KType:描述未擦除的类型或泛型参数等，例如 Map<String,Int>；可通过 typeOf 或者以下类型获取对应的父类、属性、函数参数等
- KClass：描述对象的实际类型，不包括泛型参数，例如 Map；可通过对象、类型名称直接获得
- KProperty：描述属性，可通过属性引用、属性所在类的 KClass 获取
- KFunction：描述函数，可通过函数引用、函数所在类的 KClass 获取

### 反射数据结构的区别

| Kotlin    | vs     | Java   |
| --------- | ------ | ------ |
| KType     | 相当于 | Type   |
| KClass    | 相当于 | Class  |
| KProperty | 近似于 | Field  |
| KFunction | 近似于 | Method |

### 反射的调用示例

    @ExperimentalStdlibApi
    fun main() {
        // 获取类
        val cls: KClass<String> = String::class
        // 获取属性
        val strProperty: KProperty1<String, *>? = cls.declaredMemberProperties.firstOrNull()
        // 获取函数
        val strFunc:KFunction<*>? = cls.declaredFunctions.firstOrNull()

        // 获取类型；只能得到类型擦除后的类型
        val mapCls: KClass<Map<*, *>> = Map::class
        // 获取类型；可以得到具体类型；方法调用需要 ExperimentalStdlibApi 注解
        val mapType: KType = typeOf<Map<String, Int>>()
        // 获取参数的类型
        val argument1: KTypeProjection = mapType.arguments[0] // 返回 String 类型
        val argument2: KTypeProjection = mapType.arguments[1] // 返回 Int 类型
    }
