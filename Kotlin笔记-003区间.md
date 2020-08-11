## 区间

### 区间的创建

        // 闭区间；范围在[1,10]
        val intRange1: IntRange = 1..10
        val charRange1: CharRange = 'a'..'z'
        val longRange1: LongRange = 1L..10L

        // 前闭后开区间；范围在[1,10)
        val intRange2: IntRange = 1 until 10
        val charRange2: CharRange = 'a' until 'z'
        val longRange2: LongRange = 1L until 10L

        // 倒序区间；范围在[10,1]
        val intRange3: IntProgression = 10 downTo 1
        val charRange3: CharProgression = 'z' downTo 'a'
        val longRange3: LongProgression = 10L downTo 1L

### 区间的步长

        val intRange1: IntProgression = 1..10 step 2
        val charRange1: CharProgression = 'a'..'z' step 2
        val longRange1: LongProgression = 1L..10L step 2

### 离散值区间与连续值区间

        // 离散值，可以一个一个取值，可数可遍历，有步长step
        val intRange: IntRange = 1..10
        println(intRange.joinToString())

        // 连续值，不可以一个一个取值，不可数不可遍历，没有步长step
        val floatRange: ClosedFloatingPointRange<Float> = 1f..2f
        val doubleRange: ClosedFloatingPointRange<Double> = 1.0..2.0
        // 没有 joinToString 方法，只能 toString
        println(floatRange.toString())
        println(doubleRange.toString())

### 区间的迭代

    	// 只有离散区间才可以迭代遍历
        val intRange: IntRange = 1..10
        for (num in intRange) {
            println(num)
        }
        intRange.forEach { num ->
            println(num)
        }

### 区间的包含关系

不论区间是离散区间，还是连续区间，都可以使用 in 来判断包含关系；

        val intRange: IntRange = 1..10
        if (3 in intRange) {
            println("num is in intRange")
        }
        if (12 in intRange) {
            println("num is not in intRange")
        }

### 区间的使用

        val ints:IntArray = intArrayOf(1, 2, 3, 4)
        // 可以使用区间来代替 i++ 的循环
        for (i in 0 until ints.size) {
            println(ints[i])
        }
        // ints.indices 等价于 0 until ints.size
        // Kotlin 中推荐使用 ints.indices
        for (i in ints.indices) {
            println(ints[i])
        }
