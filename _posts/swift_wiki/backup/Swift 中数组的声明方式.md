Swift 中数组的声明方式
在 Swift 中，有多种方式可以声明和初始化数组。以下是几种常见的数组声明方式：

1. 使用数组字面量（Array Literal）初始化数组：
使用方括号 `[]` 来表示数组字面量，并在其中添加元素，用逗号分隔。
```swift
let numbers: [Int] = [1, 2, 3, 4, 5]
```
在上述示例中，我们声明了一个名为 `numbers` 的常量数组，类型为 `[Int]`，并用包含整数元素的数组字面量进行初始化。

2. 使用初始化器（Initializer）初始化数组：
可以使用数组的初始化器来创建一个空数组，然后逐个添加元素。
```swift
var fruits = Array<String>()
fruits.append("Apple")
fruits.append("Orange")
fruits.append("Banana")
```
在上述示例中，我们使用 `Array<String>()` 初始化器创建了一个空的字符串数组，并使用 `append()` 方法逐个添加了元素。

3. 使用重复值初始化数组：
可以使用 `Array(repeating:count:)` 初始化器创建一个指定重复值的数组。
```swift
var zeros = Array(repeating: 0, count: 5)
```
在上述示例中，我们使用 `Array(repeating:count:)` 初始化器创建了一个包含重复值的数组，数组中的元素都是 `0`，重复了 5 次。

4. 使用闭包初始化数组：
可以使用闭包来初始化数组，根据指定的索引返回每个元素的值。
```swift
var squareNumbers = (0..<5).map { $0 * $0 }
```
在上述示例中，我们使用闭包和 `map` 方法来创建一个包含平方数的数组，其中闭包将每个索引的值乘以自身。

这些是在 Swift 中声明和初始化数组的几种常见方式。你可以根据需求选择最适合的方式来创建和初始化数组。另外，Swift 还提供了丰富的数组操作和方法，可以对数组进行排序、过滤、映射等操作，以满足不同的需求。