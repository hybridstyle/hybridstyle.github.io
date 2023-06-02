---
layout: post
title: "@StateObject与@ObservedObject 的区别"
date: 2023-06-02
categories: Swift
---
        在 SwiftUI 中，`@StateObject` 和 `@ObservedObject` 都是用于在视图中管理对象状态的属性包装器。它们之间的主要区别在于它们对待被包装对象的生命周期管理方式。

`@StateObject` 用于管理视图自己拥有的对象的状态。当使用 `@StateObject` 时，对象的生命周期由视图管理。当视图首次创建时，它将创建一个新的对象实例，并将其存储在状态中。当视图被销毁时，它负责清理和释放对象。每当对象的状态发生更改时，视图会被刷新。

下面是一个使用 `@StateObject` 的简单示例：

```swift
class MyObject: ObservableObject {
    @Published var value: String = ""
}

struct MyView: View {
    @StateObject private var myObject = MyObject()

    var body: some View {
        TextField("Enter value", text: $myObject.value)
    }
}
```

`@ObservedObject` 用于将外部对象引入到视图中，并在视图中观察其状态的更改。当使用 `@ObservedObject` 时，对象的生命周期由外部实体管理。视图只是观察对象，并在对象的状态发生更改时进行刷新。

下面是一个使用 `@ObservedObject` 的简单示例：

```swift
class MyObject: ObservableObject {
    @Published var value: String = ""
}

struct MyView: View {
    @ObservedObject private var myObject: MyObject

    init(myObject: MyObject) {
        self.myObject = myObject
    }

    var body: some View {
        Text(myObject.value)
    }
}
```

在这个例子中，`MyObject` 对象是由外部实体创建和管理的，然后通过构造函数传递给视图。视图使用 `@ObservedObject` 将该对象标记为需要观察的对象，并在对象的状态发生更改时刷新视图。

总结来说，`@StateObject` 用于视图自己拥有和管理的对象，而 `@ObservedObject` 用于外部实体创建和管理的对象。