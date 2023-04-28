#strokeBorder 与 fill 冲突吗？
在 SwiftUI 中，`strokeBorder` 和 `fill` 会冲突，因为它们都用于修改形状的外观。当你同时应用它们时，SwiftUI 将无法确定如何显示该形状，因此会抛出冲突的异常。在绝大多数情况下，你只需要选择其中一种来设置形状的外观。
一种常见的情况是，在使用 `strokeBorder` 时，为了让形状更好地与其他视图对齐，你可能需要设置 `fill` 以使形状变得不透明。在这种情况下，你可以使用 `.opacity(0)` 或 `.background(Color.clear)` 来将 `fill` 设置为透明，以便只使用 `strokeBorder` 来修改形状的外观。

