---
layout: post
title:  "Kingfisher 使用"
date:   2023-04-26
categories: Swift
---
Kingfisher 是一个专门用于图片加载和缓存的 Swift 框架，它提供了一种简单而强大的方式来管理应用中的图片资源。Kingfisher 是基于 SDWebImage 和 Alamofire 的，它采用了现代 Swift 语言的最佳实践，代码清晰简洁，易于使用和扩展。

以下是 Kingfisher 的主要特点和优势：

1. 易于使用：Kingfisher 提供了一个简单而直观的 API，让你可以用极少的代码来加载和缓存图片。你只需要调用相应的方法来加载图片，Kingfisher 就会自动帮你处理图片的下载、缓存和显示。

2. 高效稳定：Kingfisher 使用了多种优化技术来提高图片加载和缓存的效率，比如图片压缩、多线程下载、内存缓存和磁盘缓存等。它还支持断点续传和自动重试，可以保证图片加载的稳定性和可靠性。

3. 多种加载方式：Kingfisher 支持多种图片加载方式，包括 URL、本地文件、二进制数据等。你可以根据需要选择不同的加载方式来适应不同的场景。

4. 自定义样式：Kingfisher 提供了丰富的自定义选项，让你可以自定义图片的大小、圆角、边框、背景色等样式。你还可以根据需要添加滤镜、旋转、裁剪等操作来处理图片。

5. 多平台支持：Kingfisher 支持多平台，包括 iOS、tvOS、watchOS 和 macOS 等平台。你可以在不同的平台上使用相同的代码来管理图片资源。

下面是一个使用 Kingfisher 加载和显示图片的示例：

```swift
import Kingfisher

let url = URL(string: "https://example.com/image.jpg")!
imageView.kf.setImage(with: url, placeholder: UIImage(named: "placeholder"))
```

在以上示例中，我们使用 Kingfisher 的 `setImage(with:placeholder:)` 方法来加载并显示图片。你只需要传递图片的 URL 和占位图片即可，Kingfisher 会自动帮你下载、缓存和显示图片。如果图片下载失败，Kingfisher 会自动使用占位图片来替代。除了这种简单的用法，Kingfisher 还提供了丰富的 API 和选项来满足不同的需求。


除了上述提到的特点和优势，Kingfisher 还提供了以下一些高级特性：

1. 扩展性：Kingfisher 提供了丰富的扩展点，让你可以根据需要来扩展和定制框架的功能。比如，你可以自定义下载器、缓存器、图片处理器等，来适应不同的应用场景。

2. 进度监听：Kingfisher 支持进度监听，你可以实时监控图片下载进度，以及显示加载进度条等功能。这对于需要显示大图或者网络不稳定的应用场景非常有用。

3. 自定义缓存策略：Kingfisher 支持自定义缓存策略，你可以根据需要来定制缓存的过期时间、容量限制、清理策略等。这对于需要灵活控制图片缓存的应用场景非常有用。

4. 对 SVG 的支持：Kingfisher 支持加载和显示 SVG 格式的图片，这对于需要展示矢量图像的应用场景非常有用。Kingfisher 使用了 SwiftSVG 库来实现对 SVG 的支持。

5. 对自定义格式的支持：Kingfisher 支持自定义格式的图片加载和显示。你可以实现自定义的图片处理器来支持加载和显示特定格式的图片。比如，你可以使用 WebPImage 库来实现对 WebP 格式的支持。

综上所述，Kingfisher 是一个强大而易用的图片加载和缓存框架，它提供了多种优化技术和丰富的选项来提高图片加载和缓存的效率和稳定性。如果你需要管理应用中的图片资源，Kingfisher 是一个不错的选择。


Kingfisher 默认使用 URLSession 的 User-Agent，你可以通过修改 URLSessionConfiguration 的 HTTPAdditionalHeaders 属性来自定义 User-Agent。具体步骤如下：

1. 创建一个 URLSessionConfiguration 实例，并设置 HTTPAdditionalHeaders 属性，用于设置 User-Agent。

```swift
let configuration = URLSessionConfiguration.default
configuration.httpAdditionalHeaders = ["User-Agent": "Custom User Agent"]
```

2. 将自定义的 URLSessionConfiguration 实例传递给 ImageDownloader 的 shared 实例。

```swift
let downloader = KingfisherManager.shared.downloader
downloader.sessionConfiguration = configuration
```

注意：在修改 URLSessionConfiguration 之前，应该先停止 ImageDownloader 中的任务。否则，修改配置后，已经在下载中的任务可能会受到影响。可以使用 ImageDownloader 的 cancelAll() 方法来停止下载任务。

```swift
KingfisherManager.shared.downloader.cancelAll()
```
