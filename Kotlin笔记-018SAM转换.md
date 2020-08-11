## SAM 转换

在 Kotlin 中，可以对参数类型为**只有一个方法的 Java 接口的 Java 方法**，调用时可用 Lambda 表达式做转换。

Kotlin 不支持 Kotlin 接口的 SAM 转换，只支持 Java 接口的 SAM 转换。（Kotlin 1.4 开始也支持 Kotlin 接口的 SAM 转换）

因为 Kotlin 本身就支持函数类型，需要的时候传入函数类型，就可以使用 Lambda 表达式。
