## 注解

### 注解的定义：annotation

    // 限定标注对象；只能给 class 注解
    @Target(AnnotationTarget.CLASS)
    // 指定作用时机；作用于运行时
    @Retention(AnnotationRetention.RUNTIME)
    annotation class Action(val name:String) // 注解的参数

注解的参数类型，仅支持以下类型以及数组：

基本类型，KClass，枚举，其他注解（都是编译期能确定值的类型）

### 注解的使用

    // 注解的使用；Action 注解只能作用于类
    @Action("ActionUser")
    class ActionUser{}

### 常见内置注解

Kotlin 标准库的通用注解

- Metadata - Kotlin 反射的信息通过该注解附带在元素上
- UnsafeVariance - 泛型用来破除型变限制
- Suppress - 用来消除编译器警告，警告类型作为参数传入

JVM 相关注解

- JvmField - 生成 Java Field
- JvmName - 指定类/文件/函数等生成的 JVM 名称
- JvmOverloads - 函数默认参数生成函数重载
- JvmStatic - 生成静态成员
- Throws - 抛出指定异常
- Synchronized - 生成同步方法
