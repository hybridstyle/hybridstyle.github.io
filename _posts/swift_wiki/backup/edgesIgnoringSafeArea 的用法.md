ignoresSafeArea、edgesIgnoringSafeArea 的用法

`.edgesIgnoringSafeArea(_:)`是一种用于设置视图边缘忽略安全区域的修饰符，可用于控制视图在屏幕上的布局和显示。它接受一个`Edge.Set`参数，用于指定要忽略的边缘。

`Edge.Set`是一个包含不同边缘选项的结构体。以下是`Edge.Set`中可用的选项：

- `.all`：忽略所有边缘（顶部、底部、左侧和右侧）的安全区域。
- `.top`：忽略顶部边缘的安全区域。
- `.bottom`：忽略底部边缘的安全区域。
- `.leading`：忽略左侧边缘的安全区域（在左到右的语言环境中通常指左侧）。
- `.trailing`：忽略右侧边缘的安全区域（在左到右的语言环境中通常指右侧）。

您可以根据需要组合这些选项，例如 `.edgesIgnoringSafeArea([.top, .bottom])` 可以让视图忽略顶部和底部的安全区域。

以下是一个示例代码，演示如何使用`.edgesIgnoringSafeArea(_:)`修饰符：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, SwiftUI!")
            .font(.largeTitle)
            .padding()
            .background(Color.blue)
            .foregroundColor(.white)
            .edgesIgnoringSafeArea(.top)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

在上述示例中，我们将`.edgesIgnoringSafeArea(.top)`应用于`Text`视图，使其顶部边缘忽略安全区域，因此文本将延伸到屏幕的顶部。

请注意，`.edgesIgnoringSafeArea(_:)`修饰符对于根视图可能不起作用，因为根视图通常会自动填充整个安全区域。因此，对于根视图，您可能需要将其放置在其他容器内，然后对该容器应用`.edgesIgnoringSafeArea(_:)`修饰符。


ignoresSafeArea 怎么用

在 SwiftUI 中，您可以使用 `.ignoresSafeArea(_:)` 修饰符来控制视图是否忽略安全区域。该修饰符可以应用于任何视图，以使其在布局和显示时忽略安全区域。

`.ignoresSafeArea(_:)` 修饰符接受一个名为 `edges` 的参数，用于指定要忽略的边缘。以下是可用的选项：

- `.all`：忽略所有边缘（顶部、底部、左侧和右侧）的安全区域。
- `.top`：忽略顶部边缘的安全区域。
- `.bottom`：忽略底部边缘的安全区域。
- `.leading`：忽略左侧边缘的安全区域（在左到右的语言环境中通常指左侧）。
- `.trailing`：忽略右侧边缘的安全区域（在左到右的语言环境中通常指右侧）。

您可以根据需要组合这些选项，例如 `.ignoresSafeArea([.top, .bottom])` 可以让视图忽略顶部和底部的安全区域。

以下是一个示例代码，演示如何使用 `.ignoresSafeArea(_:)` 修饰符：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, SwiftUI!")
            .font(.largeTitle)
            .padding()
            .background(Color.blue)
            .foregroundColor(.white)
            .ignoresSafeArea(.top)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

在上述示例中，我们将 `.ignoresSafeArea(.top)` 应用于 `Text` 视图，使其忽略顶部边缘的安全区域。因此，文本将延伸到屏幕的顶部，忽略了状态栏的安全区域。

请注意，`.ignoresSafeArea(_:)` 修饰符对于根视图可能不起作用，因为根视图通常会自动填充整个安全区域。因此，对于根视图，您可能需要将其放置在其他容器内，并对该容器应用 `.ignoresSafeArea(_:)` 修饰符。


ignoresSafeArea 与 edgesIgnoringSafeArea 的区别

在 SwiftUI 中，`.ignoresSafeArea(_:)` 和 `.edgesIgnoringSafeArea(_:)` 是用于控制视图忽略安全区域的两个不同的修饰符。

1. `.ignoresSafeArea(_:)`：这是一个针对视图的修饰符，可以应用于任何 SwiftUI 视图。它接受一个 `SafeAreaRegions` 参数，用于指定要忽略的安全区域。通过使用 `.ignoresSafeArea(_:)` 修饰符，您可以使视图在布局和显示时忽略指定的安全区域。例如，`.ignoresSafeArea(.top)` 将使视图忽略顶部安全区域，从而延伸到屏幕的顶部。

2. `.edgesIgnoringSafeArea(_:)`：这是一个针对容器视图的修饰符，可以应用于 SwiftUI 中的容器视图，如 `VStack`、`HStack`、`ZStack` 等。它接受一个 `Edge.Set` 参数，用于指定要忽略的边缘。通过使用 `.edgesIgnoringSafeArea(_:)` 修饰符，您可以使容器视图的边缘忽略安全区域，从而使其内容延伸到屏幕的边缘。例如，`.edgesIgnoringSafeArea(.top)` 将使容器视图的顶部边缘忽略安全区域，从而使其内容延伸到屏幕的顶部。

区别总结如下：

- `.ignoresSafeArea(_:)` 修饰符应用于任何 SwiftUI 视图，并用于控制指定视图是否忽略指定的安全区域。
- `.edgesIgnoringSafeArea(_:)` 修饰符应用于容器视图，并用于控制容器视图的边缘是否忽略安全区域，从而使其内容延伸到屏幕的边缘。

根据您的需求，您可以选择使用适当的修饰符来控制视图或容器的安全区域行为。