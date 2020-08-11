## 协程

协程的使用主要有以下几种方式：

- runBlocking
- GlobalScope.launch
- GlobalScope.async

### runBlocking

    suspend fun main() {
        //  runBlocking 方法中的 delay 是阻塞当前的线程的，阻塞效果和Thread.sleep() 一样
        runBlocking {
            Log.i(TAG, "runBlocking 1")
            delay(1000L)
            Log.i(TAG, "runBlocking 2")
        }

        Log.i(TAG, "main 1")
        Thread.sleep(1000L)
        Log.i(TAG, "main 2")
    }

### GlobalScope.launch

    suspend fun main() {
        //  GlobalScope.launch 方法中 delay 不阻塞当前的线程，只阻塞当前协程
        val job: Job = GlobalScope.launch {
            Log.i(TAG, "GlobalScope 1")
            delay(1000L)
            Log.i(TAG, "GlobalScope 2")
        }

        Log.i(TAG, "main 1")
        // join 方法会等待协程执行完毕，才会继续执行后续的方法
        job.join()
        Log.i(TAG, "main 2")
    }

launch 方法源码：

    public fun CoroutineScope.launch(
        context: CoroutineContext = EmptyCoroutineContext, // 上下文
        start: CoroutineStart = CoroutineStart.DEFAULT, // 启动模式
        block: suspend CoroutineScope.() -> Unit // 协程体
    ): Job {
        val newContext = newCoroutineContext(context)
        val coroutine = if (start.isLazy)
            LazyStandaloneCoroutine(newContext, block) else
            StandaloneCoroutine(newContext, active = true)
        coroutine.start(start, coroutine, block)
        return coroutine
    }

通过源码可以看到，写在协程中的代码，被封装在协程体中，被协程调用和处理；

而且 launch 方法的协程体是没有返回值的；

### GlobalScope.async

    suspend fun main() {
        GlobalScope.launch {
            // async 返回的是 Deferred 类型，Deferred 继承自 Job 接口，增加了一个方法 await
            // async 不会阻塞当前线程，但会阻塞所在协程
            val deferred = GlobalScope.async {
                Log.i(TAG, "async 1")
                delay(1000L)
                Log.i(TAG, "async 2")
                return@async "GlobalScope.async"
            }
            Log.i(TAG, "launch 1")
            // 获取协程体中的返回值
            val tip = deferred.await()
            Log.i(TAG, "launch 2")
            Log.i(TAG, tip)
        }
        Log.i(TAG, "main 1")
    }

async 源码：

    public fun <T> CoroutineScope.async(
        context: CoroutineContext = EmptyCoroutineContext, // 上下文
        start: CoroutineStart = CoroutineStart.DEFAULT, // 启动模式
        block: suspend CoroutineScope.() -> T // 协程体
    ): Deferred<T> {
        val newContext = newCoroutineContext(context)
        val coroutine = if (start.isLazy)
            LazyDeferredCoroutine(newContext, block) else
            DeferredCoroutine<T>(newContext, active = true)
        coroutine.start(start, coroutine, block)
        return coroutine
    }

通过源码可以看到，写在协程中的代码，被封装在协程体中，被协程调用和处理；

而且 async 方法的协程体是有返回值的，可以被 Deferred.await() 使用；

_相关参考：_

<https://www.jianshu.com/p/6e6835573a9c>

<https://www.bennyhuo.com/2019/04/08/coroutines-start-mode/>
