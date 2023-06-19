---
layout: post
title: "Swift  Dictionary 怎么用"
date: 2023-06-19
categories: Swift
---
        在 Swift 中，您可以使用 `Dictionary` 类型来表示键值对的集合。下面是一些常见的使用方式和操作示例：

**1. 创建字典：**

```swift
var dictionary1: [String: Int] = [:] // 创建一个空的 [String: Int] 字典
var dictionary2 = [String: Any]() // 创建一个空的 [String: Any] 字典
var dictionary3 = ["key1": 1, "key2": 2, "key3": 3] // 创建一个包含键值对的字典
```

您可以使用不同的语法创建字典。在上述示例中，`dictionary1` 是一个空的 `[String: Int]` 字典，`dictionary2` 是一个空的 `[String: Any]` 字典，`dictionary3` 是一个包含键值对的字典。

**2. 添加和修改键值对：**

```swift
var dictionary = [String: String]()
dictionary["key1"] = "value1" // 添加键值对
dictionary["key2"] = "value2"
dictionary["key1"] = "new value1" // 修改键对应的值
```

通过使用字典的键来访问和修改值，您可以使用赋值运算符 `=` 来添加新的键值对或修改现有键的值。

**3. 访问和遍历字典：**

```swift
let dictionary = ["key1": 1, "key2": 2, "key3": 3]

// 通过键访问值
let value = dictionary["key1"] // 1

// 遍历字典中的键值对
for (key, value) in dictionary {
    print("Key: \(key), Value: \(value)")
}

// 遍历字典中的键
for key in dictionary.keys {
    print("Key: \(key)")
}

// 遍历字典中的值
for value in dictionary.values {
    print("Value: \(value)")
}
```

您可以使用字典的键来访问对应的值。通过使用 `for-in` 循环，您可以遍历字典中的键值对、键或值，并对它们进行相应的操作。

**4. 删除键值对：**

```swift
var dictionary = ["key1": 1, "key2": 2, "key3": 3]
dictionary["key2"] = nil // 删除指定的键值对
dictionary.removeValue(forKey: "key3") // 使用 removeValue(forKey:) 方法删除键值对
dictionary.removeAll() // 删除所有的键值对
```

使用赋值 `nil`、`removeValue(forKey:)` 方法或 `removeAll()` 方法可以删除字典中的键值对。

这些示例只是 Swift 中 Dictionary 的基本用法和操作的示例。您可以根据需求使用其他方法和属性来操作字典。


当然！这里还有一些其他常用的 Dictionary 操作：

**1. 判断字典是否为空：**

```swift
let dictionary = [String: Int]()
let isEmpty = dictionary.isEmpty // true
```

可以使用 `isEmpty` 属性来判断字典是否为空。

**2. 获取字典的键和值数量：**

```swift
let dictionary = ["key1": 1, "key2": 2, "key3": 3]
let count = dictionary.count // 3
```

使用 `count` 属性可以获取字典中键值对的数量。

**3. 更新字典的值：**

```swift
var dictionary = ["key1": 1, "key2": 2]
dictionary.updateValue(3, forKey: "key1") // 更新键为 "key1" 的值
dictionary["key2"] = 4 // 直接赋值更新键为 "key2" 的值
```

使用 `updateValue(_:forKey:)` 方法可以更新字典中指定键的值，或者直接使用赋值语句来更新键对应的值。

**4. 合并字典：**

```swift
var dictionary1 = ["key1": 1]
let dictionary2 = ["key2": 2, "key3": 3]
dictionary1.merge(dictionary2) { current, _ in current } // 合并字典
```

使用 `merge(_:uniquingKeysWith:)` 方法可以将另一个字典中的键值对合并到当前字典中。在合并时，如果遇到相同的键，则可以通过提供一个闭包来确定使用哪个值。

**5. 获取字典的键或值的集合：**

```swift
let dictionary = ["key1": 1, "key2": 2, "key3": 3]
let keys = dictionary.keys // 获取所有键的集合
let values = dictionary.values // 获取所有值的集合
```

可以使用 `keys` 属性获取字典中所有键的集合，或使用 `values` 属性获取字典中所有值的集合。

这些是一些常见的 Dictionary 操作，您可以根据需求使用它们来处理字典数据。

这里还有一些其他常用的 Dictionary 操作：

**1. 检查字典中是否包含某个键或值：**

```swift
let dictionary = ["key1": 1, "key2": 2, "key3": 3]

let containsKey = dictionary.keys.contains("key1") // 检查字典是否包含指定的键
let containsValue = dictionary.values.contains(2) // 检查字典是否包含指定的值
```

使用 `contains` 方法可以检查字典中是否包含指定的键或值。

**2. 获取字典中键或值的集合：**

```swift
let dictionary = ["key1": 1, "key2": 2, "key3": 3]

let keys = Array(dictionary.keys) // 获取所有键的数组
let values = Array(dictionary.values) // 获取所有值的数组
```

通过将 `dictionary.keys` 或 `dictionary.values` 转换为数组，可以获取字典中所有键或所有值的集合。

**3. 合并字典并创建新字典：**

```swift
let dictionary1 = ["key1": 1, "key2": 2]
let dictionary2 = ["key3": 3, "key4": 4]

let mergedDictionary = dictionary1.merging(dictionary2) { current, _ in current }
```

使用 `merging(_:uniquingKeysWith:)` 方法可以将两个字典合并并创建一个新的字典。如果遇到相同的键，可以通过提供一个闭包来决定使用哪个值。

**4. 根据键排序字典：**

```swift
let dictionary = ["key2": 2, "key1": 1, "key3": 3]

let sortedDictionary = dictionary.sorted { $0.key < $1.key }
```

通过使用 `sorted(by:)` 方法并提供一个比较闭包，可以根据键对字典进行排序。在上述示例中，字典将按键的升序排序。

这些是一些其他常用的 Dictionary 操作。希望这些信息对您有所帮助！如有需要，请继续提问。



