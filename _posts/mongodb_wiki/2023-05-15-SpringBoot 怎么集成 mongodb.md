---
layout: post
title: "SpringBoot 怎么集成 mongodb"
date: 2023-05-15
categories: Mongodb
---
        在Spring Boot中集成MongoDB是一个相对简单的过程。Spring Data MongoDB项目提供了对MongoDB的支持，你只需要添加对应的依赖并进行简单的配置。

以下是步骤：

1. 添加Spring Data MongoDB的依赖。在你的`pom.xml`文件中添加以下依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

2. 在`application.properties`或`application.yml`文件中，配置你的MongoDB连接。

如果是`application.properties`文件：

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/test
```

如果是`application.yml`文件：

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost:27017/test
```

在这里，`localhost:27017`是MongoDB服务器的地址和端口，`test`是你的数据库名称。根据你的实际情况进行修改。

3. 创建你的数据模型。例如，如果你有一个名为`Person`的数据模型，你可以这样创建：

```java
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection = "persons")
public class Person {

    @Id
    private String id;

    private String name;
    private int age;

    // getters and setters
}
```

4. 创建一个继承自`MongoRepository`的接口。Spring Boot将自动实现这个接口，提供如保存、查找、删除等操作。

```java
import org.springframework.data.mongodb.repository.MongoRepository;

public interface PersonRepository extends MongoRepository<Person, String> {
    // 可以在这里添加自定义的查询方法
}
```

5. 在你的服务中使用`PersonRepository`。例如：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class PersonService {

    private final PersonRepository personRepository;

    @Autowired
    public PersonService(PersonRepository personRepository) {
        this.personRepository = personRepository;
    }

    public Person createPerson(Person person) {
        return personRepository.save(person);
    }

    // 其他方法
}
```

以上就是在Spring Boot中集成MongoDB的基本步骤。