## 运算符与中缀表达式

### 操作符重载

**一元前缀操作符**

| 表达式 | 等价于         |
| ------ | -------------- |
| +a     | a.unaryPlus()  |
| -a     | a.unaryMinus() |
| !a     | a.not()        |

**递增与递减**

| 表达式 | 等价于  |
| ------ | ------- |
| a++    | a.inc() |
| a--    | a.dec() |

**算术运算符**

| 表达式 | 等价于       |
| ------ | ------------ |
| a + b  | a.plus(b)    |
| a - b  | a.minus(b)   |
| a \* b | a.times(b)   |
| a / b  | a.div(b)     |
| a % b  | a.rem(b)     |
| a..b   | a.rangeTo(b) |

**“In”操作符**

| 表达式  | 等价于         |
| ------- | -------------- |
| a in b  | b.contains(a)  |
| a !in b | !b.contains(a) |

**索引访问操作符"[]"**

| 表达式   | 等价于      |
| -------- | ----------- |
| a[i]     | a.get(i)    |
| a[i] = b | a.set(i, b) |

**调用操作符**

| 表达式 | 等价于      |
| ------ | ----------- |
| a()    | a.invoke()  |
| a(i)   | a.invoke(i) |

**广义赋值**

| 表达式  | 等价于           |
| ------- | ---------------- |
| a += b  | a.plusAssign(b)  |
| a -= b  | a.minusAssign(b) |
| a \*= b | a.timesAssign(b) |
| a /= b  | a.divAssign(b)   |
| a %= b  | a.remAssign(b)   |

**相等与不等操作符**

| 表达式 | 等价于        |
| ------ | ------------- |
| a == b | a.equals(b)   |
| a != b | !(a.equals(b) |

**比较操作符**

| 表达式 | 等价于              |
| ------ | ------------------- |
| a > b  | a.compareTo(b) > 0  |
| a < b  | a.compareTo(b) < 0  |
| a >= b | a.compareTo(b) >= 0 |
| a <= b | a.compareTo(b) <= 0 |

### 中缀表达式

常用的中缀表达式有 Map 中的`a to b`方式

    val map:Map<String,String> = mapOf("act" to "x","act2" to "y")

我们也可以自定义中缀表达式

    // 使用 infix 可以自定义中缀表达式
    infix fun String.double(str: String): String {
        return this + str + str
    }

    fun action(){
        println("Kotlin" double "Hello")
    }
