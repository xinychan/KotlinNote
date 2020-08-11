## 扩展方法

Java 一般要对某个对象进行多次操作，会使用工具类封装；

Kotlin 可以给这个对象添加扩展方法，直接使用扩展方法进行操作；

### 扩展方法的定义

    // 判断String是否是邮箱
    fun String.isEmail(): Boolean {
        if (this.endsWith(".com")) {
            return true
        }
        return false
    }

    fun action(){
        // 扩展方法使用
        "simple@163.com".isEmail()
    }

### 扩展方法的类型

    // 判断String是否是邮箱
    fun String.isEmail(): Boolean {
        if (this.endsWith(".com")) {
            return true
        }
        return false
    }

    fun action() {
        // 扩展方法的类型；未绑定Receive的，必须包括所在的类实例对象（Receive）
        val type: (String) -> Boolean = String::isEmail
        // 扩展方法的类型；已绑定Receive的，不包括所在的类实例对象（Receive）
        val type2: () -> Boolean = "Kotlin"::isEmail
    }
