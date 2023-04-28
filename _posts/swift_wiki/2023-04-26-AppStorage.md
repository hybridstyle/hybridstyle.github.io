---
layout: post
title:  "AppStorage介绍"
date:   2023-04-26
categories: Swift
---

`AppStorage` 是一个用于在 SwiftUI 应用程序中存储和检索应用程序级别的永久数据的属性包装器。它允许我们在应用程序的生命周期中存储和检索简单的数据类型，例如字符串、布尔值和数字等。

`AppStorage` 的使用非常简单，只需要在需要存储数据的属性前添加 `@AppStorage` 属性包装器即可。例如，以下代码演示了如何使用 `AppStorage` 存储一个布尔值：

```swift
@AppStorage("isOnboardingCompleted") var isOnboardingCompleted = false
```

在上面的示例中，我们创建了一个名为 `isOnboardingCompleted` 的布尔类型属性，并使用 `@AppStorage` 属性包装器将其标记为需要永久存储。`"isOnboardingCompleted"` 是用于标识存储的键名，它将用于在应用程序的生命周期中检索存储的值。

一旦我们定义了一个带有 `@AppStorage` 的属性，我们可以像访问普通属性一样使用它。例如，我们可以通过以下方式将值从 `isOnboardingCompleted` 属性中读取出来：

```swift
let isCompleted = isOnboardingCompleted
```

我们也可以通过以下方式更新该属性的值：

```swift
isOnboardingCompleted = true
```

`AppStorage` 还支持自动同步，这意味着当我们更新存储的值时，它会自动同步到设备上的其他实例和其他设备。例如，如果我们在一个设备上更新了 `isOnboardingCompleted` 属性的值，它将自动同步到我们使用相同 iCloud 帐户登录的其他设备上。

需要注意的是，`AppStorage` 在 iOS 14 及以上版本可用，且需要 iOS 14 及以上版本的设备才能正常运行。如果应用程序需要支持 iOS 13 及以下版本的设备，可以考虑使用 `UserDefaults` 或其他存储方式来代替 `AppStorage`。


SceneStorage是SwiftUI中的一个property wrapper，用于在不同场景之间存储和检索持久化数据。它可以存储基本数据类型（例如String、Int、Bool等）和可选类型（例如String?、Int?、Bool?等）。

使用SceneStorage时，可以将其声明为视图的属性，并将其绑定到要存储和检索数据的唯一键。每当存储的值更改时，它将自动更新，并在不同场景之间保持一致。

以下是使用SceneStorage的示例：

```swift
struct ContentView: View {
    @SceneStorage("username") var username: String = "John"
    
    var body: some View {
        VStack {
            Text("Hello, \(username)!")
            Button("Change Username") {
                username = "Jane"
            }
        }
    }
}
```

在上面的示例中，我们使用@SceneStorage将username属性绑定到名为“username”的唯一键。默认情况下，username的初始值为“John”。当我们在应用程序的不同场景之间切换时，username的值将始终保持一致。当我们点击“Change Username”按钮时，username将被更新为“Jane”，并且文本“Hello，John！”将被更新为“Hello，Jane！”

# AppStorage 与 SceneStorage 的区别

AppStorage和SceneStorage都是用于持久化存储数据的属性包装器，但它们在应用中的使用情境和作用范围上有所不同。

AppStorage用于在应用程序的不同场景之间存储和检索持久化数据，它将值存储在应用的UserDefaults中，并在应用重新启动时保持不变。AppStorage通常用于存储全局性质的数据，如用户偏好设置或应用程序的主题。

SceneStorage是用于在同一场景的不同状态之间存储和检索数据的属性包装器。它将值存储在场景相关的持久性存储中，使得在场景生命周期内，即使场景被暂停并且应用程序处于后台状态，也可以保留数据。SceneStorage通常用于存储场景特定的数据，如文本编辑器中的文本内容或游戏中的当前分数。

因此，AppStorage和SceneStorage都可以用于持久化存储数据，但它们的作用范围不同。如果需要在应用程序的不同场景之间存储数据，则应使用AppStorage，如果需要在同一场景的不同状态之间存储数据，则应使用SceneStorage。
