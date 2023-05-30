使用 UserDefaults 的SwiftUI 的 MVVM 示例
UserDefaults 用于存储个人信息，如id，昵称，性别等，个人信息需要从网络接口获取
以下是一个使用 UserDefaults 的 SwiftUI MVVM 示例，其中 UserDefaults 用于存储个人信息，包括 id、昵称和性别。个人信息从网络接口获取。

首先，我们将创建一个模型（Model）来表示个人信息：

```swift
struct UserInfo: Codable {
    let id: String
    let nickname: String
    let gender: String
}
```

接下来，我们将创建一个视图模型（ViewModel），它负责从网络接口获取个人信息并存储到 UserDefaults 中：

```swift
import SwiftUI

class UserInfoViewModel: ObservableObject {
    @Published var userInfo: UserInfo?
    
    func fetchUserInfo() {
        // 发起网络请求获取个人信息...
        // 假设我们从网络接口获取到了 userInfoData
        
        if let userInfoData = userInfoData {
            do {
                let decoder = JSONDecoder()
                self.userInfo = try decoder.decode(UserInfo.self, from: userInfoData)
                
                // 将个人信息存储到 UserDefaults
                let defaults = UserDefaults.standard
                defaults.set(userInfoData, forKey: "userInfoData")
            } catch {
                print("Error decoding userInfo: \(error)")
            }
        }
    }
    
    func loadStoredUserInfo() {
        // 从 UserDefaults 加载存储的个人信息
        let defaults = UserDefaults.standard
        if let userInfoData = defaults.data(forKey: "userInfoData") {
            do {
                let decoder = JSONDecoder()
                self.userInfo = try decoder.decode(UserInfo.self, from: userInfoData)
            } catch {
                print("Error decoding stored userInfo: \(error)")
            }
        }
    }
}
```

在上述代码中，`fetchUserInfo()` 方法用于从网络接口获取个人信息，并将其存储到 UserDefaults 中。在存储之前，我们使用 JSONDecoder 将获取的数据解码为 `UserInfo` 对象，并将其赋值给 `userInfo` 属性。随后，我们使用 UserDefaults 将 userInfoData 存储到 "userInfoData" 键中。

`loadStoredUserInfo()` 方法用于从 UserDefaults 中加载之前存储的个人信息，并将其解码为 `UserInfo` 对象。我们使用 `userInfo` 属性来存储加载的个人信息。

最后，我们将创建一个 SwiftUI 视图（View）来显示个人信息：

```swift
struct UserInfoView: View {
    @ObservedObject var viewModel = UserInfoViewModel()
    
    var body: some View {
        VStack {
            if let userInfo = viewModel.userInfo {
                Text("ID: \(userInfo.id)")
                Text("Nickname: \(userInfo.nickname)")
                Text("Gender: \(userInfo.gender)")
            } else {
                Text("Loading...")
            }
        }
        .onAppear {
            // 首先尝试从 UserDefaults 加载存储的个人信息
            viewModel.loadStoredUserInfo()
            
            // 然后再从网络获取最新的个人信息
            viewModel.fetchUserInfo()
        }
    }
}
```

在上述代码中，我们使用 `@ObservedObject` 属性包装器将视图与视图模型关联起来。视图使用 `VStack` 来显示个人信息，如果 `userInfo` 存在，我们显示 id、昵称和性别。否则，我们显示 "Loading..."。

在 `onAppear` 闭包中，我们首先尝试从 UserDefaults 加载之前存

储的个人信息，然后再发起网络请求获取最新的个人信息。

通过以上代码，我们实现了一个使用 UserDefaults 存储个人信息的 SwiftUI MVVM 示例，其中个人信息从网络接口获取。