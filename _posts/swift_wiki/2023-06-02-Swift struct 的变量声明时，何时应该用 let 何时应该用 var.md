---
layout: post
title: "Swift struct 的变量声明时，何时应该用 let 何时应该用 var"
date: 2023-06-02
categories: Swift
---
        Swift 中的 `let` 和 `var` 关键字分别用于声明常量和变量。所以，你选择使用哪个关键字，主要取决于你是否需要改变变量的值：

- 如果你打算改变变量的值，那么你应该使用 `var`。例如：

  ```swift
  struct Person {
      var name: String
  }
  ```

  在这个例子中，`name` 是一个变量，所以你可以改变它的值：

  ```swift
  var person = Person(name: "John")
  person.name = "Alice"  // 修改 person 的 name
  ```

- 如果你不打算改变变量的值，那么你应该使用 `let`。例如：

  ```swift
  struct Person {
      let name: String
  }
  ```

  在这个例子中，`name` 是一个常量，所以你不能改变它的值：

  ```swift
  let person = Person(name: "John")
  person.name = "Alice"  // 这行代码会导致编译错误
  ```

需要注意的是，即使你使用 `var` 声明了一个变量，但如果你用 `let` 声明了该变量的实例，那么你仍然不能改变该变量的值。例如：

```swift
struct Person {
    var name: String
}

let person = Person(name: "John")
person.name = "Alice"  // 这行代码会导致编译错误，因为 person 是一个常量
```

在这个例子中，即使 `name` 是一个变量，但 `person` 是一个常量，所以你不能改变 `person.name` 的值。

总的来说，你应该根据你的需求来选择 `let` 或 `var`。如果你知道变量的值在初始化后不会改变，那么你应该使用 `let`，因为它可以使你的代码更加安全和清晰。如果你需要改变变量的值，那么你应该使用 `var`。