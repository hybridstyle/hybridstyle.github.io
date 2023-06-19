Swift 的字符串格式化
在 Swift 中，您可以使用字符串格式化来创建带有占位符的字符串。以下是一些常见的字符串格式化示例：

**1. 格式化整数：**

```swift
let age = 25
let formattedString = String(format: "My age is %d", age)
print(formattedString) // Output: "My age is 25"
```

在上面的示例中，使用占位符 `%d` 表示整数，然后使用 `String(format: ...)` 构造函数来将整数格式化到字符串中。

**2. 格式化浮点数：**

```swift
let temperature = 25.5
let formattedString = String(format: "The temperature is %.1f", temperature)
print(formattedString) // Output: "The temperature is 25.5"
```

在这个例子中，使用占位符 `%.1f` 表示浮点数，并指定保留一位小数。同样，使用 `String(format: ...)` 构造函数将浮点数格式化为字符串。

**3. 格式化字符串：**

```swift
let name = "John"
let formattedString = String(format: "Hello, %@", name)
print(formattedString) // Output: "Hello, John"
```

在这个例子中，使用占位符 `%@` 来表示字符串，并使用 `String(format: ...)` 构造函数将字符串格式化到另一个字符串中。

**4. 多个占位符：**

```swift
let firstName = "John"
let lastName = "Doe"
let age = 25
let formattedString = String(format: "Name: %@ %@, Age: %d", firstName, lastName, age)
print(formattedString) // Output: "Name: John Doe, Age: 25"
```

在这个示例中，使用多个占位符来表示不同的值，并在 `String(format: ...)` 构造函数中按顺序提供相应的值。

这些示例只是演示了一些常见的字符串格式化方法。在实际应用中，您可以根据需求使用不同的占位符和格式选项来格式化字符串。