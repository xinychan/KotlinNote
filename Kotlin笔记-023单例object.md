## 单例 object

### object 的定义

    // 定义单例；饿汉式
    // 类加载时实例化对象
    // Singleton既是类名也是对象名
    object Singleton{
    	// object 不能自定义构造器，默认无参构造器
        var name:String = "Kotlin"
        fun show(){
            println("Kotlin")
        }
    }

    fun main() {
        // 访问 object 成员
        Singleton.name
        Singleton.show()
    }

### 静态成员 @JvmStatic

    // 使用 @JvmStatic 注解后，Singleton 里面的属性和方法，在 Java 中就是静态的属性和方法
    object Singleton{
        @JvmStatic var name:String = "Kotlin"
        @JvmStatic fun show(){
            println("Kotlin")
        }
    }

### 不生成 get/set 方法 @JvmField

    // 使用 @JvmField 注解后，在 Java 中就没有get/set方法
    object Singleton{
        @JvmField var name:String = "Kotlin"
    }

### 伴生对象

    class People(){
        // 一个类中可以有多个 object；但是只有一个 companion object
        companion object{
            var name:String = "Kotlin"
            fun action(){}
        }
        object Friend1{
            var toy1:String = "toy1"
            fun play1(){}
        }
        object Friend2{
            var toy2:String = "toy2"
            fun play2(){}
        }
    }

    fun main() {
        // 伴生对象的使用
        People.name
        People.action()
        // 类中 object 使用
        People.Friend1.toy1
        People.Friend1.play1()
        People.Friend2.toy2
        People.Friend2.play2()
    }
