---
layout: post
title:  "ObservedObject"
date:   2023-04-26
categories: Swift
---

`ObservedObject` 是 SwiftUI 框架中的一个属性包装器，它提供了一种在视图中观察和响应数据变化的机制。使用 `ObservedObject` 可以实现视图和数据的双向绑定，当数据发生变化时，视图会自动更新。

`ObservedObject` 需要一个遵循 `ObservableObject` 协议的对象作为参数，这个对象需要包含需要被观察的数据。当数据发生变化时，被观察的对象会发出通知，通知视图进行更新。

下面是一个使用 `ObservedObject` 的例子：

```swift
class MyModel: ObservableObject {
    @Published var name: String = "John"
}

struct ContentView: View {
    @ObservedObject var model = MyModel()
    
    var body: some View {
        Text("Hello, \(model.name)!")
    }
}
```

在上面的代码中，`MyModel` 是一个遵循 `ObservableObject` 协议的类，其中包含一个被观察的属性 `name`。在 `ContentView` 中，我们使用 `@ObservedObject` 将 `MyModel` 对象包装起来，使得 `ContentView` 可以观察 `MyModel` 中 `name` 的变化。在视图中使用 `model.name` 来访问 `name` 属性，当 `name` 发生变化时，视图会自动更新。

`ObservableObject` 必须是一个类或结构体的实例，也就是必须是一个对象。因为 `ObservableObject` 是一个协议，只有类或结构体才能遵循该协议，并且可以在协议的要求下实现属性的发布和通知。值类型（例如枚举）不能遵循 `ObservableObject` 协议，因为它们是值语义，不支持在内部存储引用类型的发布属性。如果需要在值类型中使用 `@Published` 属性包装器，则可以考虑使用 `@StateObject`、`@EnvironmentObject` 或 `@Binding` 等其他属性包装器来实现视图和数据的双向绑定。

# struct 可以是实现 observableobject 吗

可以，`struct` 可以实现 `ObservableObject` 协议，不过需要注意的是，`struct` 实现 `ObservableObject` 协议的属性必须使用 `@Published` 属性包装器来实现属性的发布和通知，因为 `struct` 是值类型，不支持在内部存储引用类型的发布属性。

下面是一个 `struct` 实现 `ObservableObject` 协议的示例：

```swift
struct MyModel: ObservableObject {
    @Published var name: String = "John"
}
```

在这个示例中，`MyModel` 是一个 `struct`，遵循 `ObservableObject` 协议，并使用 `@Published` 属性包装器来实现 `name` 属性的发布和通知。这样，当 `name` 属性发生变化时，视图可以自动更新。

需要注意的是，由于 `struct` 是值类型，当它们被复制时，它们的所有属性都将被复制，包括实现 `ObservableObject` 协议的属性。这意味着，如果一个 `struct` 实现了 `ObservableObject` 协议，并且在多个视图中被使用，那么每个视图都将拥有一个该 `struct` 的副本，当 `struct` 的属性发生变化时，每个视图都会收到更新通知，而不仅仅是该 `struct` 的原始实例。因此，使用 `struct` 实现 `ObservableObject` 协议时需要谨慎处理，确保每个视图都有自己的独立数据状态。
