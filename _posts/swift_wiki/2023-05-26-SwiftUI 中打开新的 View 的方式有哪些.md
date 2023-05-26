---
layout: post
title: "SwiftUI 中打开新的 View 的方式有哪些"
date: 2023-05-26
categories: Swift
---
        在 SwiftUI 中，你可以通过以下方式打开一个新的 View：

1. `NavigationView` 和 `NavigationLink`: 这是在 SwiftUI 中导航到新视图最常用的方式。当用户点击 `NavigationLink` 时，就会导航到指定的目标视图。

```swift
NavigationView {
    NavigationLink(destination: NewView()) {
        Text("Go to New View")
    }
}
```

2. 模态视图（Modal）: 使用 `.sheet` 或 `.fullScreenCover` 修饰符，你可以从当前视图弹出一个模态视图。这些修饰符需要一个绑定到布尔值的变量，当这个变量为 `true` 时，就会显示模态视图。

```swift
@State private var showingNewView = false

Button(action: { showingNewView = true }) {
    Text("Open New View")
}
.sheet(isPresented: $showingNewView) {
    NewView()
}
```

3. `TabView`: 你可以使用 `TabView` 来在不同的视图之间切换。每个 tab 都可以有自己的视图。

```swift
TabView {
    Text("First View").tabItem { Text("First") }
    Text("Second View").tabItem { Text("Second") }
}
```

4. `Popover` 视图：你可以通过 `.popover` 修饰符在当前视图上显示一个弹出视图。

```swift
@State private var showingPopover = false

Button("Show Popover") {
    showingPopover = true
}
.popover(isPresented: $showingPopover) {
    Text("Hello from popover")
}
```

以上就是 SwiftUI 中打开新的视图的主要方式。每种方式都有其用途，你可以根据你的具体需求选择适合的方式。

`.sheet` 和 `.popover` 并不一定需要绑定到 `Button` 上。它们可以绑定到任何 SwiftUI 视图上。当 `isPresented` 参数（一个绑定到 `Bool` 的 `Binding`）变为 `true` 时，将会显示 `.sheet` 或 `.popover`。

例如，你可以将 `.sheet` 绑定到 `List` 上，当用户选择一项时，可以显示详情页面：

```swift
struct ContentView: View {
    let items = ["Item 1", "Item 2", "Item 3"]
    @State private var selectedItem: String? = nil

    var body: some View {
        List(items, id: \.self) { item in
            Text(item)
                .onTapGesture {
                    selectedItem = item
                }
        }
        .sheet(item: $selectedItem) { item in
            DetailView(item: item)
        }
    }
}

struct DetailView: View {
    let item: String

    var body: some View {
        Text("Details for \(item)")
    }
}
```

在上面的例子中，我们定义了一个 `List`，并将 `.sheet` 修饰符应用于 `List`。每当用户点击列表中的一项时，我们就更新 `selectedItem`，这会导致 `.sheet` 显示 `DetailView`，并将所选项目传递给 `DetailView`。

`.popover` 也可以类似地应用到任何 SwiftUI 视图上。只要 `isPresented` 变为 `true`，就会显示 `.popover`。