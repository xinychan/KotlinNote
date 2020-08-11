## 集合变换与序列

### 集合映射操作

    fun main() {
        val list: List<Int> = listOf(1, 2, 3, 4)
        // 保留指定条件的元素；返回一个新的List
        val list1: List<Int> = list.filter {
            it > 2
        }
        // 元素按指定条件变换成另一个元素；返回一个新的List
        val list2: List<Int> = list.map {
            it * 2
        }
        // 每个元素都映射成一个集合，然后把所有集合拼接
        list.flatMap {
            // 接受一个返回值为 Iterable 的函数
            0 until it
        }

        // 饿汉式；会立即执行filter，然后依次执行filter->map->println
        list.filter {
            it > 2
        }.map {
            it * 2
        }.forEach {
            println("value = $it")
        }

        // 懒汉式；元素会依次filter->map->println，只有forEach调用了才会执行
        list.asSequence().filter {
            it > 2
        }.map {
            it * 2
        }.forEach {
            println("value = $it")
        }
    }

_还有集合聚合操作：sum/reduce/fold/zip 等_
