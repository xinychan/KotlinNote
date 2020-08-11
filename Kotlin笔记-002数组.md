## 数组

| 类型     | Kotlin        | Java        |
| -------- | ------------- | ----------- |
| 整型     | IntArray      | int[]       |
| 整型装箱 | Array<Int>    | Integer[]   |
| 字符     | CharArray     | char[]      |
| 字符装箱 | Array<Char>   | Character[] |
| 字符串   | Array<String> | String[]    |

类似 float/double 等类型的数组也一样

### 数组的创建

        val c0: IntArray = intArrayOf(1, 2, 3, 4)
        val c1: IntArray = IntArray(5) {
            it + 1
        }
        println(c1.contentToString())

### 数组的长度

        val c0: IntArray = intArrayOf(1, 2, 3, 4)
        println(c0.size)

### 数组的读写

        val tips: Array<String> = arrayOf("Hello", "World")
        tips[1] = "Kotlin"
        println("${tips[0]},${tips[1]}")

### 数组的遍历

        val ints = intArrayOf(1, 2, 3, 4)
        // 使用for循环
        for (num in ints) {
            println(num)
        }
        // 使用forEach
        ints.forEach { num ->
            println(num)
        }

### 判断值是否在数组中

        val ints = intArrayOf(1, 2, 3, 4)
        if (1 in ints) {
            println("num is in ints")
        }
        if (5 !in ints) {
            println("num is not in ints")
        }
