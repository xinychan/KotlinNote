## 代理

### 接口代理

    interface Api {
        fun act1()
        fun act2()
        fun act3()
    }
    // ApiImpl 实现 Api 接口
    class ApiImpl : Api {
        override fun act1() {
        }

        override fun act2() {
        }

        override fun act3() {
        }
    }

    // 接口代理；使用传入的api参数来代理 ApiWrapper 实现接口 Api
    // 前提是传入的api参数要实现被代理的接口
    class ApiWrapper(val api: Api) : Api by api {
        override fun act3() {
            println("act3")
            api.act3()
        }
    }

    fun main() {
    	// 使用 ApiWrapper
        val impl = ApiImpl()
        val wrapper = ApiWrapper(impl)
    }

### 属性代理

    // 属性代理 - lazy
    // lazy 代理了属性的初始化
    public actual fun <T> lazy(initializer: () -> T): Lazy<T> = SynchronizedLazyImpl(initializer)

    // 属性代理 - observable
    // 代理了属性的 getter/setter ，可以修改属性和监听属性值的变化
