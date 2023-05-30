Swift 中的Codable是什么意思
在 Swift 中，Codable 是一个协议（Protocol），用于实现数据的编码（Encoding）和解码（Decoding）。它是 Swift 标准库提供的一种方便的方式，用于在数据模型对象和外部表示（如 JSON、Property List 等）之间进行相互转换。

通过遵循 Codable 协议，可以轻松地实现对象与外部数据表示之间的转换，而无需手动编写大量的解析代码。Codable 协议实际上是两个子协议的组合：Encodable 和 Decodable。

- Encodable 协议：用于将对象编码为外部表示。它要求实现 encode(to:) 方法，将对象的属性编码为外部表示的格式，如 JSON 数据、Property List 数据等。

- Decodable 协议：用于从外部表示解码为对象。它要求实现 init(from:) 初始化方法，从外部表示的格式中解析数据并初始化对象的属性。

遵循 Codable 协议的对象可以使用 Swift 的编解码器（Encoder 和 Decoder）来进行编码和解码操作。标准库提供了 JSONEncoder 和 JSONDecoder 等编解码器的默认实现，可以方便地将对象与 JSON 数据进行转换。

例如，假设我们有一个数据模型对象 Person，它包含了姓名和年龄信息：

```swift
struct Person: Codable {
    let name: String
    let age: Int
}
```

通过让 Person 类型遵循 Codable 协议，我们可以轻松地将 Person 对象编码为 JSON 数据，或者从 JSON 数据解码为 Person 对象：

```swift
let person = Person(name: "John Doe", age: 30)

// 编码为 JSON 数据
let encoder = JSONEncoder()
if let jsonData = try? encoder.encode(person) {
    let jsonString = String(data: jsonData, encoding: .utf8)
    print(jsonString) // 输出：{"name":"John Doe","age":30}
}

// 从 JSON 数据解码为对象
let jsonString = """
    {"name":"Jane Smith","age":25}
"""
let decoder = JSONDecoder()
if let jsonData = jsonString.data(using: .utf8),
   let decodedPerson = try? decoder.decode(Person.self, from: jsonData) {
    print(decodedPerson) // 输出：Person(name: "Jane Smith", age: 25)
}
```

通过 Codable 和相关的编解码器，我们可以方便地进行对象的序列化和反序列化操作，从而在 Swift 中实现数据的编码和解码功能。这在处理网络请求、持久化数据等场景中非常有用。
