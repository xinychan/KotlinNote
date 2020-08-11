## 智能类型转换

### 类型转换的判断

比如子类转父类使用的地方：

    interface People {}

    class Man(name: String, age: Int) : People {
        val myName: String = name
        val myAge: Int = age
    }

    class Woman(name: String, age: Int) : People {
        val myName: String = name
        val myAge: Int = age
    }

在判断生效的地方，可当指定类型使用：

    fun action(){
        val people = Man("Kotlin",18)
        // 判断实例是否是某个类型
        if (people is Man) {
            // 在判断条件生效的地方，可直接当Man使用
            println(people.myName)
        }
    }

### 安全转换

    fun action(){
        // 安全转换，通过 as? 将 people 转换成 Man
        println((people as? Man)?.myName)
    }

### 转换作用域

    fun action(){
        var value: String? = null
        // 通过非空判断后，在判断条件生效的作用域里面，value类型为String
        if (value != null) {
            println(value.length)
        }
        // 不在判断条件生效的作用域里面，依然是可空类型
        println(value?.length)
    }

### 不支持智能转换的情况

    // 在方法外部定义了一个全局变量
    var index:String? = null

    fun action(){
        // 不支持智能转换的情况
        if (index != null) {
            // 虽然判断了不为空，但调用外部的数据，不能保证判断后数据是否被其他线程修改
            println(index?.length)
        }
    }

**编码建议：**

- 尽量使用 val 声明变量
- 尽量减少函数对外部变量的访问
- 必要时创建局部变量指向外部变量，避免外部变量变化引发错误
