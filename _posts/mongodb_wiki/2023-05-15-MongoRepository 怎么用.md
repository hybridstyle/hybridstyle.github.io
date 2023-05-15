---
layout: post
title: "MongoRepository 怎么用"
date: 2023-05-15
categories: Mongodb
---
        在Spring Data MongoDB中，`MongoRepository`是一个接口，你可以通过继承这个接口为你的数据模型创建一个repository，这个repository可以让你很方便地进行增删查改等操作。

首先，你需要在你的`pom.xml`文件中添加Spring Data MongoDB的依赖：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

然后，你需要为你的数据模型创建一个repository。假设你有一个名为`Person`的数据模型，你可以这样创建一个repository：

```java
import org.springframework.data.mongodb.repository.MongoRepository;

public interface PersonRepository extends MongoRepository<Person, String> {
    // 你可以在这里添加自定义的查询方法
}
```

在这个例子中，我们创建了一个名为`PersonRepository`的接口，这个接口继承自`MongoRepository`。`MongoRepository`接口有两个泛型参数，第一个是你的数据模型的类型，第二个是你的数据模型的ID的类型。

现在，你可以在你的服务中使用这个repository了：

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

    // 更多方法...
}
```

在这个例子中，我们创建了一个名为`PersonService`的类，这个类中有一个`PersonRepository`的字段。我们可以通过Autowired注解来自动注入这个字段的值。然后，我们就可以使用这个repository来进行增删查改等操作了。

例如，我们可以使用`save`方法来保存一个新的`Person`对象，或者更新一个已经存在的`Person`对象。我们也可以使用`findById`方法来通过ID查找一个`Person`对象，使用`findAll`方法来查找所有的`Person`对象，使用`delete`方法来删除一个`Person`对象，等等。

此外，你也可以在`PersonRepository`接口中添加自定义的查询方法。例如，如果你想通过名字来查找`Person`对象，你可以添加一个如下的方法：

```java
List<Person> findByName(String name);
```

Spring Data MongoDB会自动为你实现这个方法。当你调用这个方法时，它会在后台生成一个如下的查询：

```javascript
{ "name" : name }
```

然后执行这个查询，返回查询的结果。