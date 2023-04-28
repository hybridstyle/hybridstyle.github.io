---
layout: post
title:  "AppDelegate 怎么用"
date:   2023-04-28
categories: Swift
---
在 SwiftUI 中使用 `AppDelegate`，你可以在 `@main` 标记的 `App` 结构体中添加一个 `@UIApplicationDelegateAdaptor` 属性，该属性允许你指定一个遵循 `UIApplicationDelegate` 协议的类。

下面是一个使用 `@UIApplicationDelegateAdaptor` 的示例：

```swift
@main
struct MyApp: App {
    @UIApplicationDelegateAdaptor(AppDelegate.self) var appDelegate

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

在上面的示例中，我们使用了 `@UIApplicationDelegateAdaptor` 属性将 `AppDelegate` 类与我们的 `MyApp` 应用程序关联起来。

在 `AppDelegate` 类中，你可以实现 `UIApplicationDelegate` 协议中的方法来响应应用程序的不同状态，例如启动、暂停、终止等。下面是一个简单的 `AppDelegate` 类示例：

```swift
class AppDelegate: NSObject, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
        print("Application did finish launching.")
        return true
    }
}
```

在上面的示例中，我们实现了 `UIApplicationDelegate` 协议中的 `application(_:didFinishLaunchingWithOptions:)` 方法，该方法会在应用程序启动时被调用。在该方法中，我们打印了一条消息，以表明应用程序已经完成了启动。

注意，如果你的应用程序没有必要使用 `AppDelegate`，你可以完全不使用它。相反，你可以直接在 `@main` 标记的 `App` 结构体中编写应用程序的入口代码。


除了使用 `@UIApplicationDelegateAdaptor` 属性，你还可以通过 `UIApplication.shared.delegate` 属性来获取 `AppDelegate` 对象，然后调用其相应的方法来响应应用程序的状态变化。下面是一个示例：

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .onAppear {
                let appDelegate = UIApplication.shared.delegate as! AppDelegate
                appDelegate.myMethod()
            }
    }
}

class AppDelegate: NSObject, UIApplicationDelegate {
    func myMethod() {
        print("This is my method.")
    }
}
```

在上面的示例中，我们在 `ContentView` 中使用了 `onAppear` 修饰符来监听视图出现的事件，然后获取 `AppDelegate` 对象并调用了其中的 `myMethod` 方法。在 `myMethod` 方法中，我们打印了一条消息，以表明该方法已经被调用。

注意，如果你需要频繁地访问 `AppDelegate` 对象或其属性，建议使用 `@UIApplicationDelegateAdaptor` 属性来进行关联，而不是每次都通过 `UIApplication.shared.delegate` 属性来获取 `AppDelegate` 对象。
