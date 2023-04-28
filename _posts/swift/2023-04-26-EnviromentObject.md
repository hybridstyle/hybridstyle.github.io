---
layout: post
title:  "EnvironmentObject 用法"
date:   2023-04-26
categories: Swift
---



SwiftUI中的`EnvironmentObject`是一种数据传递机制，可以方便地在应用程序的多个视图之间共享数据，无需显式地传递数据。使用`EnvironmentObject`可以避免传递大量的参数，并且可以确保多个视图之间的数据保持同步。

下面是一个简单的示例，展示如何使用`EnvironmentObject`在多个视图之间共享数据：

首先，我们定义一个简单的模型类`UserData`，其中包含一个名为`username`的字符串属性：

```swift
import Combine

final class UserData: ObservableObject {
    @Published var username: String = ""
}
```

然后，在`SceneDelegate`中创建一个`UserData`对象，并将其设置为整个应用程序的环境对象：

```swift
class SceneDelegate: UIResponder, UIWindowSceneDelegate {
    var window: UIWindow?
    let userData = UserData()

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        let contentView = ContentView().environmentObject(userData)
        if let windowScene = scene as? UIWindowScene {
            let window = UIWindow(windowScene: windowScene)
            window.rootViewController = UIHostingController(rootView: contentView)
            self.window = window
            window.makeKeyAndVisible()
        }
    }
}
```

在此示例中，我们将`UserData`对象作为`environmentObject`传递给了`ContentView`。然后，在`ContentView`中，我们可以使用`@EnvironmentObject`属性包装器来访问该对象：

```swift
struct ContentView: View {
    @EnvironmentObject var userData: UserData
    
    var body: some View {
        VStack {
            Text("Welcome, \(userData.username)!")
            TextField("Enter username", text: $userData.username)
        }
    }
}
```

在此示例中，我们使用`@EnvironmentObject`包装器访问了`UserData`对象，并在视图中使用了该对象的属性`username`。此外，我们还可以通过`$userData.username`将文本字段的绑定传递给`username`属性，以便在文本字段中输入的值与`username`属性同步更新。

这是一个非常简单的示例，展示了如何在SwiftUI中使用`EnvironmentObject`。实际应用中，您可能会创建更复杂的模型类，并在多个视图之间共享多个环境对象。
