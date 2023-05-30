Swift 中@escaping 怎么用

`@escaping` 是一个属性修饰符，在闭包参数中使用。它用于标记一个闭包是“逃逸闭包”，意味着该闭包在函数返回之后仍然可以被调用或访问。

当我们将闭包作为函数参数传递时，默认情况下，它们是“非逃逸闭包”。这意味着闭包必须在函数结束之前执行，不能在函数外部持有或存储。

然而，有时我们需要在函数结束后继续使用闭包，例如将闭包存储在属性中、将闭包传递给异步操作、将闭包传递给其他函数等。在这种情况下，我们需要使用 `@escaping` 来标记闭包，告诉编译器它是逃逸闭包。

下面是一个使用 `@escaping` 的示例：

```swift
func performOperation(completion: @escaping () -> Void) {
    DispatchQueue.main.asyncAfter(deadline: .now() + 1.0) {
        completion()
    }
}

func runOperation() {
    print("Start")
    
    performOperation {
        print("Operation completed")
    }
    
    print("End")
}
```

在上面的示例中，`performOperation` 函数接受一个逃逸闭包作为参数，并将其存储在异步队列中进行延迟执行。`runOperation` 函数调用 `performOperation` 并传递一个闭包，在闭包中打印 "Operation completed"。

由于闭包是逃逸闭包，`runOperation` 函数在打印 "End" 之前就已经结束了。然后，在延迟执行之后，闭包被调用并打印 "Operation completed"。

使用 `@escaping` 修饰符时需要注意以下几点：
- 逃逸闭包必须被显式地标记为 `@escaping`。
- 在逃逸闭包中，需要小心避免引起循环引用问题，避免强引用循环。
- 在使用逃逸闭包时，需要特别注意异步操作和执行顺序。

总结来说，`@escaping` 属性修饰符用于标记逃逸闭包，允许闭包在函数返回之后继续被调用或访问。这在需要在函数外部持有闭包或进行异步操作时非常有用。