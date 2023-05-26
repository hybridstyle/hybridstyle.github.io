SwiftUI 的 NavigationView 怎么用

在 SwiftUI 中，`NavigationView` 是一个非常有用的组件，可以帮助我们创建导航栈，用于在屏幕之间切换。以下是一个基本的 `NavigationView` 示例：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        NavigationView {
            List {
                NavigationLink(destination: Text("Detail View")) {
                    Text("Navigate to Detail View")
                }
            }
            .navigationBarTitle("Home", displayMode: .inline)
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

在这个例子中，我们创建了一个 `NavigationView`。在这个 `NavigationView` 内部，我们创建了一个 `List`。`List` 中包含一个 `NavigationLink`，这个 `NavigationLink` 将 "Home" 视图链接到 "Detail View" 视图。当你点击 "Navigate to Detail View" 文字时，会切换到 "Detail View" 视图。

`.navigationBarTitle("Home", displayMode: .inline)` 是在 `NavigationView` 中设置标题的方法，可以在导航条中显示标题。`displayMode: .inline` 表示标题应以内联样式显示，也就是说，标题在导航栏中居中。

这只是 `NavigationView` 的基本使用。还可以进行更复杂的操作，如传递数据，使用 TabView 进行分页，等等。希望这个例子能帮到你！如果你还有其他问题，欢迎继续提问。


