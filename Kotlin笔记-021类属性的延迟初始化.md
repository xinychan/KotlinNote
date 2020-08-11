### 类属性的延迟初始化

方式一：不推荐

    // 初始化为null，但是每次都要做可空类型参数调用
    private var tipView:TextView? = null

方式二：不推荐

    // lateinit 关键字延迟初始化；但是使用时需要自己保证不为空，否则空指针异常
    // lateinit 会让编译器忽略初始化，但是不支持Int等基本类型
    private lateinit var tipView2:TextView

方式三：推荐

    // 使用lazy；在 tipView3 首次被访问时执行
    private val tipView3:TextView by lazy {
        findViewById<TextView>(R.id.tv_main)
    }
