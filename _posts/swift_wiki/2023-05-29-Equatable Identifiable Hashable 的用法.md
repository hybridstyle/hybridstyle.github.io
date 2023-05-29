---
layout: post
title: "Equatable Identifiable Hashable 的用法"
date: 2023-05-29
categories: Swift
---
        `Equatable`、`Identifiable` 和 `Hashable` 都是 Swift 中的协议，用于处理比较、唯一标识和哈希化等操作。下面分别介绍它们的用法：

1. Equatable（相等性比较）：
`Equatable` 协议用于比较两个值是否相等。要让类型遵循 `Equatable` 协议，需要实现 `==` 运算符函数。下面是一个示例：

```swift
struct Person: Equatable {
    var name: String
    var age: Int
}

let person1 = Person(name: "John", age: 30)
let person2 = Person(name: "John", age: 30)
let person3 = Person(name: "Jane", age: 25)

print(person1 == person2) // 输出: true
print(person1 == person3) // 输出: false
```

在上述示例中，`Person` 结构体遵循 `Equatable` 协议，并实现了 `==` 运算符函数来比较两个 `Person` 实例的相等性。

2. Identifiable（唯一标识）：
`Identifiable` 协议用于为类型指定唯一标识符。要遵循 `Identifiable` 协议，类型必须具有 `id` 属性。下面是一个示例：

```swift
struct User: Identifiable {
    var id: Int
    var name: String
}

let user = User(id: 1, name: "John")
print(user.id) // 输出: 1
```

在上述示例中，`User` 结构体遵循 `Identifiable` 协议，并具有一个 `id` 属性作为唯一标识符。

3. Hashable（哈希化）：
`Hashable` 协议用于生成哈希值以支持集合类型的操作，如 `Set` 或 `Dictionary`。要遵循 `Hashable` 协议，类型必须实现 `hash(into:)` 方法。下面是一个示例：

```swift
struct Book: Hashable {
    var title: String
    var author: String
}

let book1 = Book(title: "Swift Programming", author: "John Smith")
let book2 = Book(title: "Swift Programming", author: "John Smith")

print(book1.hashValue) // 输出: 792699181900267401
print(book2.hashValue) // 输出: 792699181900267401
```

在上述示例中，`Book` 结构体遵循 `Hashable` 协议，并自动获得了 `hashValue` 属性。在哈希化的过程中，Swift 会根据 `title` 和 `author` 属性的值生成哈希值。

请注意，Swift 4 引入了 `Equatable` 和 `Hashable` 的合成实现机制，它们可以自动生成 `==` 运算符函数和哈希函数。如果你遵循了相应的规范，可以省略手动实现 `==` 运算符函数和 `hash(into:)` 方法。

总结来说，`Equatable` 用于比

较相等性，`Identifiable` 用于唯一标识，`Hashable` 用于哈希化。通过遵循这些协议，你可以对类型进行比较、标识和哈希化操作，并在使用集合类型时获得更好的性能和语义。