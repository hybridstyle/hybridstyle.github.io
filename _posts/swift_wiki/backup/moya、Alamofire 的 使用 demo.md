moya、Alamofire 的 使用 demo
以下是一个基本的 Moya 的使用示例。这个示例展示了如何使用 Moya 创建一个简单的 GitHub API 请求。

首先，你需要在你的项目中安装 Moya。如果你使用 CocoaPods，你可以在 Podfile 中添加以下代码：

```swift
pod 'Moya'
```

然后在终端运行 `pod install`。

接下来，我们创建一个 `GitHubAPI` 的 `enum`，代表 GitHub API 的各种请求：

```swift
import Moya

enum GitHubAPI {
    case userProfile(username: String)
    case repos(username: String)
}

// 扩展这个枚举以满足 Moya 的 TargetType 协议
extension GitHubAPI: TargetType {
    var baseURL: URL { return URL(string: "https://api.github.com")! }

    var path: String {
        switch self {
        case .userProfile(let username):
            return "/users/\(username)"
        case .repos(let username):
            return "/users/\(username)/repos"
        }
    }

    var method: Moya.Method {
        return .get
    }

    var task: Task {
        return .requestPlain
    }

    var headers: [String: String]? {
        return ["Content-type": "application/json"]
    }

    var sampleData: Data {
        return Data()
    }
}
```

这个 `enum` 定义了两种请求：一种是获取用户的个人信息，另一种是获取用户的仓库信息。

然后，我们可以创建一个 `MoyaProvider` 对象并发出请求：

```swift
let provider = MoyaProvider<GitHubAPI>()

provider.request(.userProfile(username: "your_username")) { result in
    switch result {
    case let .success(response):
        let data = response.data
        let statusCode = response.statusCode
        // 解析数据...
    case let .failure(error):
        // 处理错误...
    }
}
```

这就是 Moya 的基本使用。实际应用中，你可能需要处理更复杂的请求和响应，例如上传文件、解析 JSON 数据等，Moya 都提供了支持。



下面是一个使用 Alamofire 发送 GET 请求的例子：

```swift
import Alamofire

let url = "https://api.github.com/users/your_username"

AF.request(url).validate().responseJSON { response in
    switch response.result {
    case .success(let value):
        print("Response: \(value)")
        // 如果响应是 JSON，你可以使用如 SwiftyJSON 等库进行解析
    case .failure(let error):
        print("Error: \(error)")
    }
}
```

以上代码将发送一个 GET 请求到 GitHub API 获取指定用户名的用户信息，然后将响应的 JSON 数据打印到控制台。

Alamofire 还支持许多其它功能，例如 POST 请求，上传和下载文件，请求链等。你可以参考 Alamofire 的官方文档来获取更多的使用示例和教程。