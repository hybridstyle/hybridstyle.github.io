---
layout: post
title: "TextField底部横线的几种实现方式"
date: 2023-05-26
categories: Swift
---
        
实现1
```swift
TextField("请输入手机号", text: $username)
                .textFieldStyle(PlainTextFieldStyle())
                .padding(.bottom,5)
                .overlay(
                    VStack{
                        Spacer().background(Color.blue)
                        Group{
                            Rectangle()
                                .frame(height: 1)
                                .foregroundColor(.gray)
                        }
                    }
                )
```

实现2
```swift
TextField("请输入手机号", text: $username)
                .textFieldStyle(PlainTextFieldStyle())
                .padding(.bottom,5)
                .overlay(
                    VStack{
                        Spacer().background(Color.blue)
                        Divider()
                    }
                )
```

实现3
```swift
VStack{
	TextField("请输入手机号", text: $username)
                .textFieldStyle(PlainTextFieldStyle())
    Divider()
	
}
```

实现3更加好用一些