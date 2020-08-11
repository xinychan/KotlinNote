## 内联类

### 内联类定义：inline class

    /**
     * 内联类
     * 内联类是是对某一个类型的包装
     * 类似JAVA装箱类型的一种类型
     * 内联类包装的类型必须在主构造器中申明，且必须是 val
     * 内联类中只能定义方法，不能定义属性，因为属性有状态
     * 内联类可以实现接口，但不能继承父类，也不能被继承
     * 内联类主要是用于装箱开箱的编译的优化；也可以用于模拟枚举，因为优化了性能
     * 无符号类型就是内联类，用于包装Int等类型
     * 限制：
     * 主构造器必须有且仅有一个只读属性
     * 不能定义有 backing-field 的其他属性
     * 被包装类型不能是泛型类型
     * 不能继承父类，也不能被继承
     * 不能定义为其他类的内部类
     */
    inline class DoubleInt(val value: Int) {
        operator fun inc(): DoubleInt {
            return DoubleInt(value * 2)
        }
    }

    fun main() {
        val doubleInt: DoubleInt = DoubleInt(1) // 值 = 2
        val newValue:Int = doubleInt.value * 100 // 值 = 200
    }

### 内联类当枚举使用

    inline class RouteType(val value: Int)

    object RouteTypes {
        val WALK = RouteType(0)
        val BUS = RouteType(1)
        val CAR = RouteType(2)
    }

    fun setType(type: RouteType) {
        println("setType is : $type")
    }

    fun main() {
        // 模拟枚举
        setType(RouteTypes.BUS)
    }

### typealias 与 inline class

| 区别 | typealias    | inline class       |
| ---- | ------------ | ------------------ |
| 类型 | 没有新类型   | 有包装类型产生     |
| 实例 | 与原类型一直 | 必要时使用包装类型 |
| 场景 | 类型更直观   | 优化包装类型性能   |
