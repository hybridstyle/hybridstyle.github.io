Swift 的简单的 MVVM 的示例

在 SwiftUI 中，我们可以使用 `ForEach` 在视图中渲染一个集合。这里有一个简单的 MVVM 架构的例子，这个例子中的模型是 `User`，视图模型是 `UserViewModel`，视图是 `UserView`。

首先，定义你的 `User` 模型：

```swift
struct User: Identifiable {
    let id: Int
    let name: String
}
```

然后，创建一个视图模型 `UserViewModel`。这个视图模型会有一个 `users` 属性，它会存储一个 `User` 对象的数组：

```swift
class UserViewModel: ObservableObject {
    @Published var users = [
        User(id: 1, name: "User 1"),
        User(id: 2, name: "User 2"),
        User(id: 3, name: "User 3")
        // add more users here
    ]
}
```

最后，创建你的视图 `UserView`。这个视图会使用 `ForEach` 遍历 `users` 并显示每个用户的名称：

```swift
struct UserView: View {
    @ObservedObject var viewModel = UserViewModel()
    
    var body: some View {
        List {
            ForEach(viewModel.users) { user in
                Text(user.name)
            }
        }
    }
}
```

在这个例子中，`UserView` 视图监视 `UserViewModel` 的变化，当 `users` 发生变化时，视图会自动更新。

以上就是一个使用 SwiftUI 和 MVVM 架构的简单示例。请注意这个示例非常简单，实际的 MVVM 架构可能会涉及到更多的逻辑，例如网络请求、数据处理等。