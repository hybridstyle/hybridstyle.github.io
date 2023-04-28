
在 Swift 中，对于值类型（struct 和 enum）的方法，默认情况下是不允许修改值类型实例中的属性或方法。为了在值类型的方法中修改实例的属性或方法，需要在方法前面添加 `mutating` 关键字。

简单来说，`mutating` 关键字用于标记一个方法可以修改实例中的属性或方法，因为值类型实例是通过复制来传递的，如果不使用 `mutating`，则无法修改原始值类型实例，因为这将破坏值类型的不变性。

例如，下面这个示例代码定义了一个名为 `Point` 的结构体，该结构体有两个属性 x 和 y，以及一个用于将 Point 实例移动到新位置的 `moveByX(_:y:)` 方法：

```swift
struct Point {
    var x = 0.0, y = 0.0

    mutating func moveByX(_ deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
```

由于 `moveByX(_:y:)` 方法需要修改实例的属性，因此需要添加 `mutating` 关键字。这样，我们就可以通过调用该方法来移动 Point 实例的位置，例如：

```swift
var point = Point(x: 10.0, y: 10.0)
point.moveByX(5.0, y: 5.0)
print(point.x, point.y) // 输出 "15.0, 15.0"
```

总之，`mutating` 关键字是用于值类型中修改实例属性或方法的标记，它在值类型中非常有用，并且在编写可变方法时经常使用。

`mutating` 还可以用于扩展中的方法，通过在扩展方法中添加 `mutating`，可以修改原始类型的实例。例如：

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}

var number = 2
number.square() // number 变成 4
```

在上面的例子中，我们在 `Int` 类型的扩展中添加了一个名为 `square()` 的方法，该方法可以将原始值平方并将结果赋值回原始值。由于该方法需要修改实例的值，因此需要使用 `mutating` 关键字。

值得注意的是，`mutating` 关键字只能用于值类型（struct 和 enum），而不能用于引用类型（class）。这是因为引用类型的实例是通过引用传递的，修改一个实例属性不会改变该实例的本质，只会改变属性的值，因此不需要使用 `mutating` 关键字。



`mutating` 还可以用于扩展中的方法，通过在扩展方法中添加 `mutating`，可以修改原始类型的实例。例如：

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}

var number = 2
number.square() // number 变成 4
```

在上面的例子中，我们在 `Int` 类型的扩展中添加了一个名为 `square()` 的方法，该方法可以将原始值平方并将结果赋值回原始值。由于该方法需要修改实例的值，因此需要使用 `mutating` 关键字。

值得注意的是，`mutating` 关键字只能用于值类型（struct 和 enum），而不能用于引用类型（class）。这是因为引用类型的实例是通过引用传递的，修改一个实例属性不会改变该实例的本质，只会改变属性的值，因此不需要使用 `mutating` 关键字。

除了在结构体中的方法和协议中的方法中使用 `mutating` 关键字之外，还可以在函数参数中使用 `inout` 关键字。`inout` 可以让函数的参数变为可变的，在函数内部修改该参数后，修改后的值会被保存到原始变量中。例如：

```swift
func swapInts(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}

var x = 10
var y = 20
swapInts(&x, &y)
print("x: \(x), y: \(y)") // 输出：x: 20, y: 10
```

在上面的例子中，我们定义了一个 `swapInts()` 函数，该函数有两个 `inout` 参数。在函数内部，我们通过一个临时变量来交换 `a` 和 `b` 的值。注意，我们在调用函数时需要在参数前加上 `&` 符号，以表示这是一个指向变量的指针。

总之，`inout` 关键字可以让我们在函数内部修改传入的参数，并将修改后的值保存回原始变量。这种方法对于需要修改传入参数的函数非常有用，而且可以避免创建新的对象。
