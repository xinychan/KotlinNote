## 集合框架

Kotlin 中区分不可变集合与可变集合；

不可变集合定义后不能添加和删除元素，可变集合定义后可以添加和删除元素；

| 类型        | Kotlin         | Java    |
| ----------- | -------------- | ------- |
| 不可变 List | List<T>        | List<T> |
| 可变 List   | MutableList<T> | List<T> |
| 不可变 Map  | Map<T>         | Map<T>  |
| 可变 Map    | MutableMap<T>  | Map<T>  |
| 不可变 Set  | Set<T>         | Set<T>  |
| 可变 Set    | MutableSet<T>  | Set<T>  |

### 集合的创建

        // 不可添加删除元素
        val intList1: List<Int> = listOf(1, 2, 3, 4)
        // 可以添加删除元素
        val intList2: MutableList<Int> = mutableListOf(1, 2, 3, 4)
        // 使用ArrayList
        val intList3:ArrayList<Int> = ArrayList<Int>()

        // Map 的创建
        val map: Map<String, String> = mapOf("name1" to "Kotlin", "name2" to "Java")
        val map2: MutableMap<String, String> = mutableMapOf("name1" to "Kotlin", "name2" to "Java")

### 集合的读写

        // List
        val stringList: ArrayList<String> = ArrayList()
        // 增加和删除
        for (i in 0..10) {
            stringList.add("num:$i")
            // 使用操作符重载，和add方法效果一致
            stringList += "num:$i"
        }
        for (i in 0..10) {
            stringList.remove("num:$i")
            // 使用操作符重载，和remove方法效果一致
            stringList -= "num:$i"
        }
        // 读写数据
        stringList[0] = "Hello"
        val string: String = stringList[0]

        // Map
        val map: HashMap<String, String> = HashMap()
        // 写入数据；不推荐使用put
        map.put("Hello", "Kotlin")
        map["Hello"] = "Kotlin"
        // 读取数据；不推荐使用get
        val tip2: String? = map.get("Hello")
        val tip: String? = map["Hello"]

### Pair

        val pair: Pair<String, String> = "Hello" to "Kotlin"
        val pair2: Pair<String, String> = Pair("Hello", "Kotlin")
        val first: String = pair.first
        val second: String = pair.second
        val (x, y) = pair2
        println("show $x - $y")

### Triple

        val triple: Triple<String, Int, Int> = Triple("Hello", 0, 0)
        val first: String = triple.first
        val second: Int = triple.second
        val third: Int = triple.third
        val (x, y, z) = triple
        println("show $x - $y - $z")
