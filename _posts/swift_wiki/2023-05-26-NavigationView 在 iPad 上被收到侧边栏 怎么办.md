---
layout: post
title: "NavigationView 在 iPad 上被收到侧边栏 怎么办"
date: 2023-05-26
categories: Swift
---
        
在 iPad 或者更大的设备上，`NavigationView` 默认会以分屏的形式呈现。左侧的列表或菜单视图会保持在屏幕上，而右侧的详细视图会随着用户的导航选择而改变。

如果你想让 `NavigationView` 的行为在 iPad 上像在 iPhone 上那样，只显示一个屏幕，可以使用 `navigationViewStyle(StackNavigationViewStyle())` 修饰符。以下是一个使用 `StackNavigationViewStyle` 的例子：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        NavigationView {
            List {
                NavigationLink(destination: DetailView()) {
                    Text("Navigate to Detail View")
                }
            }
            .navigationBarTitle("Home View", displayMode: .inline)
        }
        .navigationViewStyle(StackNavigationViewStyle())
    }
}

struct DetailView: View {
    var body: some View {
        Text("This is the Detail View")
            .navigationBarTitle("Detail View", displayMode: .inline)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

在这个例子中，`.navigationViewStyle(StackNavigationViewStyle())` 确保了 `NavigationView` 在所有设备上的行为都一样，即在用户导航到新视图时，新视图会取代旧视图，而不是在旧视图旁边显示。