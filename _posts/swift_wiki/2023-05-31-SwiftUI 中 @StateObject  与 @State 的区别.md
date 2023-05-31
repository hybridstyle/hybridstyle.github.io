---
layout: post
title: "SwiftUI 中 @StateObject  与 @State 的区别"
date: 2023-05-31
categories: Swift
---
        
`@State`和`@StateObject`是两个不同的属性包装器，用于在SwiftUI中管理状态。

1. `@State`：`@State`用于管理视图内部的短暂、局部的状态。当`@State`修饰的属性发生改变时，SwiftUI会根据新的值重新计算视图的布局和显示。`@State`属性应该声明为`private`，并且只能在`View`的生命周期内使用。

   ```swift
   struct ContentView: View {
       @State private var count: Int = 0
       
       var body: some View {
           Text("Count: \(count)")
           Button("Increment") {
               count += 1
           }
       }
   }
   ```

2. `@StateObject`：`@StateObject`用于管理需要在整个视图层次结构中共享的持久性对象，例如数据模型或单例对象。与`@State`不同，`@StateObject`修饰的属性只在视图第一次创建时初始化，然后在整个视图生命周期内保持不变。当关联的对象发生更改时，视图会根据需要重新计算布局和显示。

   ```swift
   class UserViewModel: ObservableObject {
       @Published var name: String = ""
   }
   
   struct ContentView: View {
       @StateObject private var userViewModel = UserViewModel()
       
       var body: some View {
           VStack {
               Text("Name: \(userViewModel.name)")
               TextField("Enter name", text: $userViewModel.name)
           }
       }
   }
   ```

   在上面的示例中，`UserViewModel`是一个持久性的数据模型，用`@StateObject`修饰。`UserViewModel`中的`name`属性通过`@Published`属性包装器进行了标记，以便在更改时通知视图进行更新。

总结来说，`@State`用于短暂、局部的状态，而`@StateObject`用于需要在整个视图层次结构中共享的持久性对象。

