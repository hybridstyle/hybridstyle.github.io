---
layout: post
title: "提供一个通过网络 API 获取数据的SwfitUI的 MVVM 示例"
date: 2023-05-30
categories: Swift
---
        
当在 SwiftUI 中使用 MVVM（Model-View-ViewModel）架构来获取数据并更新视图时，以下是一个简单的示例：

首先，我们将创建一个模型（Model）来表示从 API 获取的数据。在这个示例中，我们将使用 GitHub API 获取用户的仓库列表。

```swift
struct Repository: Codable {
    let name: String
    let description: String
}
```

接下来，我们将创建一个视图模型（ViewModel），它负责从 API 获取数据并处理数据的状态和逻辑。

```swift
import SwiftUI

class RepositoryViewModel: ObservableObject {
    @Published var repositories: [Repository] = []
    @Published var isLoading: Bool = false
    
    func fetchRepositories() {
        isLoading = true
        
        // 发起网络请求
        let url = URL(string: "https://api.github.com/users/username/repos")!
        URLSession.shared.dataTask(with: url) { (data, response, error) in
            DispatchQueue.main.async {
                self.isLoading = false
                
                if let data = data {
                    do {
                        let decoder = JSONDecoder()
                        self.repositories = try decoder.decode([Repository].self, from: data)
                    } catch {
                        print("Error decoding data: \(error)")
                    }
                }
            }
        }.resume()
    }
}
```

在上述代码中，我们使用 `@Published` 属性包装器来声明可观察的属性。`repositories` 属性存储从 API 获取的仓库列表。`isLoading` 属性用于在数据加载期间显示加载状态。

`fetchRepositories()` 方法发起了一个网络请求，使用 `URLSession` 发送请求，并在获取到响应数据后使用 JSONDecoder 将数据解码为 `[Repository]` 类型。解码完成后，我们更新 `repositories` 属性，并将 `isLoading` 设置为 `false`。

最后，我们将创建一个 SwiftUI 视图（View）来显示从 API 获取的数据。

```swift
struct RepositoryListView: View {
    @ObservedObject var viewModel = RepositoryViewModel()
    
    var body: some View {
        VStack {
            if viewModel.isLoading {
                ProgressView()
            } else {
                List(viewModel.repositories, id: \.name) { repository in
                    VStack(alignment: .leading) {
                        Text(repository.name)
                            .font(.headline)
                        Text(repository.description)
                            .font(.subheadline)
                    }
                }
            }
        }
        .onAppear {
            viewModel.fetchRepositories()
        }
    }
}
```

在上述代码中，我们使用 `@ObservedObject` 属性包装器将视图与视图模型关联起来。视图使用 `VStack` 和 `List` 来显示仓库列表。如果数据正在加载中，我们显示一个 `ProgressView`，否则，我们遍历 `repositories` 属性，并显示每个仓库的名称和描述。

在 `onAppear` 闭包中，我们在视图出现时调用 `fetchRepositories()` 方法来获取数据。

这是一个简单的使用 SwiftUI 和 MVVM 架构从网络 API 获取数据的示例。当视图模型中的数据发生变化时，SwiftUI 将自动更新视图，以反映最新的数据状态。这种架构可以使代码更具可测试性、可维护性和可扩展性。