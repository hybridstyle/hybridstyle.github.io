Java 连接 Mongodb
要使用Java连接MongoDB数据库，首先你需要MongoDB Java Driver。可以通过Maven来安装，只需在你的`pom.xml`文件中添加以下依赖：

```xml
<dependency>
  <groupId>org.mongodb</groupId>
  <artifactId>mongodb-driver-sync</artifactId>
  <version>4.0.5</version>
</dependency>
```

之后，你可以使用以下代码片段来连接MongoDB数据库：

```java
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoDatabase;

public class ConnectToDB {
  public static void main( String args[] ) {

    // 连接到 MongoDB 服务，如果是远程连接可以替换“localhost”为服务器的 IP 地址
    // 这里连接的默认端口为 27017
    MongoClient mongoClient = MongoClients.create("mongodb://localhost:27017");

    // 连接到数据库。假设你的 MongoDB 实例中有一个名为 "myDatabase" 的数据库
    MongoDatabase database = mongoClient.getDatabase("myDatabase");

    // 现在你已经连接到了数据库，并可以进行相应的操作。
  }
}
```

这段代码将连接到本地运行的MongoDB实例。如果你的MongoDB在远程服务器上运行，或者运行在非默认的端口上，那么你需要修改连接字符串中的`localhost:27017`部分，使其指向正确的地址和端口。

请注意这只是一个基本的连接示例，对于生产环境，你可能需要考虑诸如认证、SSL、连接池设置等其他因素。

在你的数据库中进行增删查改等操作，你需要使用MongoDB Java Driver提供的其他类和方法。例如，`MongoCollection`类代表数据库中的一个集合，`FindIterable`类可以帮助你查询数据，等等。