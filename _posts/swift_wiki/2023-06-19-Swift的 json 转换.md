---
layout: post
title: "Swift的 json 转换"
date: 2023-06-19
categories: Swift
---
        在 Swift 中，你可以使用 `Codable` 协议来进行 JSON 的转换。`Codable` 是 Swift 中的一个协议，用于实现自动的编码和解码操作。通过实现 `Codable` 协议，你可以方便地将自定义类型与 JSON 数据进行相互转换。

下面是一个简单的示例，演示了如何将自定义类型编码为 JSON 数据以及如何将 JSON 数据解码为自定义类型：

```swift
struct Person: Codable {
    var name: String
    var age: Int
    var email: String
}

// 将自定义类型编码为 JSON 数据
let person = Person(name: "Alice", age: 30, email: "alice@example.com")
let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted

do {
    let jsonData = try encoder.encode(person)
    if let jsonString = String(data: jsonData, encoding: .utf8) {
        print(jsonString)
    }
} catch {
    print(error)
}

// 将 JSON 数据解码为自定义类型
let jsonString = """
{
    "name": "Bob",
    "age": 25,
    "email": "bob@example.com"
}
"""

let decoder = JSONDecoder()

do {
    let jsonData = jsonString.data(using: .utf8)!
    let decodedPerson = try decoder.decode(Person.self, from: jsonData)
    print(decodedPerson)
} catch {
    print(error)
}
```

在上面的代码中，我们定义了一个名为 `Person` 的结构体，并将其声明为遵循 `Codable` 协议。结构体的属性对应 JSON 数据的键，因此它们具有相同的名称和类型。

要将自定义类型编码为 JSON 数据，我们使用 `JSONEncoder` 类进行编码操作。我们可以设置编码器的输出格式，例如使用 `.prettyPrinted` 选项对生成的 JSON 数据进行漂亮的格式化。

要将 JSON 数据解码为自定义类型，我们使用 `JSONDecoder` 类进行解码操作。我们使用提供的 JSON 字符串创建了一个 `Data` 对象，并通过 `decode(_:from:)` 方法将其解码为指定的类型。

需要注意的是，为了能够正确进行编码和解码操作，自定义类型必须遵循 `Codable` 协议，并且类型的属性必须是支持编码和解码的类型，如 `String`、`Int`、`Double`、`Array`、`Dictionary` 等。如果需要处理嵌套的结构，可以通过在相应的类型中嵌套使用 `Codable` 类型来实现。
