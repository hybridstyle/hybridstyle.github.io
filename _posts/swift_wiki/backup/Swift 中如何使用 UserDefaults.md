Swift 中如何使用 UserDefaults
在 Swift 中，您可以使用 UserDefaults 来存储和读取简单的键值对数据，例如用户的偏好设置、应用的配置信息等。下面是使用 UserDefaults 的基本步骤：

1. 存储数据：
   使用 `UserDefaults.standard` 实例来访问默认的 UserDefaults 单例，并使用下列方法来存储数据：
   
   ```swift
   let defaults = UserDefaults.standard
   defaults.set("John Doe", forKey: "username")
   defaults.set(25, forKey: "age")
   defaults.set(true, forKey: "isSubscribed")
   ```
   
   在上述示例中，我们使用 `set(_:forKey:)` 方法来存储不同类型的值，分别使用了键 "username"、"age" 和 "isSubscribed"。根据需要，您可以存储各种 Swift 基本类型、数组、字典以及遵循 NSCoding 协议的自定义对象。

2. 读取数据：
   使用 `UserDefaults.standard` 实例来访问默认的 UserDefaults 单例，并使用下列方法来读取存储的数据：
   
   ```swift
   let defaults = UserDefaults.standard
   if let username = defaults.string(forKey: "username") {
       print("Username: \(username)")
   }
   
   let age = defaults.integer(forKey: "age")
   print("Age: \(age)")
   
   let isSubscribed = defaults.bool(forKey: "isSubscribed")
   print("Is Subscribed: \(isSubscribed)")
   ```
   
   在上述示例中，我们使用 `string(forKey:)`、`integer(forKey:)` 和 `bool(forKey:)` 方法来读取之前存储的字符串、整数和布尔值。如果键不存在，这些方法将返回默认值（nil 或对应类型的零值）。

3. 删除数据：
   要删除存储的数据，可以使用下列方法：
   
   ```swift
   let defaults = UserDefaults.standard
   defaults.removeObject(forKey: "username")
   ```
   
   在上述示例中，我们使用 `removeObject(forKey:)` 方法来删除键为 "username" 的数据。

注意事项：
- UserDefaults 是一个轻量级的存储机制，适用于存储少量简单的数据。对于大量或复杂的数据，应该考虑使用其他存储方式，如数据库或文件存储。
- 存储的数据类型必须是可序列化的，即可以使用 `NSKeyedArchiver` 进行编码和解码。因此，自定义对象需要遵循 `NSCoding` 协议才能直接存储到 UserDefaults 中。
- 由于 UserDefaults 是单例模式，应该谨慎使用它存储敏感数据，因为它存储在应用的沙盒中并且可以被其他应用访问。
- 如果需要存储大量或复杂的数据，或者需要支持复杂的查询和操作，考虑使用更强大的存储解决方案，如 Core Data 或数据库。

以上是在 Swift 中使用 UserDefaults 存储和读取简单数据的基本方法。