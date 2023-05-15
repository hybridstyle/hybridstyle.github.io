---
layout: post
title: "SpringBoot 集成 Mongodb 实现自定义插入"
date: 2023-05-15
categories: Mongodb
---
        在Spring Boot中，你可以通过继承MongoRepository接口实现数据的CRUD操作，但是如果你想进行更多自定义的操作，你可以使用MongoTemplate。

1. 首先，你需要添加Spring Data MongoDB的依赖：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

2. 配置你的MongoDB连接信息，在`application.properties`或`application.yml`中：

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/test
```

3. 使用@Autowired注解来注入MongoTemplate，然后你就可以用它来进行更多自定义的操作了：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.stereotype.Service;
import com.mongodb.client.result.UpdateResult;

@Service
public class SomeService {
    private final MongoTemplate mongoTemplate;

    @Autowired
    public SomeService(MongoTemplate mongoTemplate) {
        this.mongoTemplate = mongoTemplate;
    }

    // 插入操作
    public void insertPerson(Person person) {
        mongoTemplate.insert(person);
    }

    // 更多自定义的操作...
}
```

在这个例子中，我们在SomeService类中注入了MongoTemplate，并提供了一个插入Person对象的方法。你可以使用这个方法来进行插入操作。

需要注意的是，如果你要插入的对象中包含了@Id注解的字段，那么MongoDB会使用这个字段作为文档的_id。如果插入的对象中没有@Id注解的字段，或者@Id注解的字段的值为null，那么MongoDB会自动为文档生成一个_id。

此外，你可以使用MongoTemplate提供的其它方法，如find、update等，来进行更多的操作。