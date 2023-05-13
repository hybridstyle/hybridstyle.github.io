mongodb的常用命令

以下是一些常用的MongoDB命令：

1. **选择或创建数据库**：

    使用`use`命令来选择一个数据库。如果这个数据库不存在，MongoDB将在插入数据时自动创建它。

    ```bash
    use myDatabase
    ```

2. **显示所有数据库**：

    使用`show dbs`命令来显示所有的数据库。

3. **创建集合**：

    MongoDB中的集合类似于SQL数据库中的表。可以使用`db.createCollection()`方法来创建集合。

    ```bash
    db.createCollection('myCollection')
    ```

4. **查看当前数据库中的所有集合**：

    使用`show collections`命令。

5. **插入文档**：

    文档在MongoDB中类似于SQL数据库中的行。可以使用`insert()`方法来插入文档。

    ```bash
    db.myCollection.insert({name: 'John', age: 25})
    ```

6. **查询文档**：

    使用`find()`方法来查询文档。如果你想要查询满足某些条件的文档，你可以将这些条件作为参数传递给`find()`方法。

    ```bash
    db.myCollection.find()
    db.myCollection.find({name: 'John'})
    ```

7. **更新文档**：

    使用`update()`方法来更新文档。你需要提供两个参数：第一个参数是查询条件，第二个参数是你想要更新的字段和新的值。

    ```bash
    db.myCollection.update({name: 'John'}, {$set: {age: 26}})
    ```

8. **删除文档**：

    使用`remove()`方法来删除文档。你需要提供一个参数，这个参数是查询条件。

    ```bash
    db.myCollection.remove({name: 'John'})
    ```

9. **创建索引**：

    索引可以提高查询的性能。使用`createIndex()`方法来创建索引。

    ```bash
    db.myCollection.createIndex({name: 1})
    ```


10. **计数**：

    使用`count()`方法来获取满足某些条件的文档的数量。

    ```bash
    db.myCollection.count({name: 'John'})
    ```

11. **查找并修改**：

    `findAndModify()`方法可以找到并修改一个文档，并返回修改后的文档。

    ```bash
    db.myCollection.findAndModify({
        query: { name: 'John' },
        update: { $set: { age: 26 } },
        new: true
    })
    ```

12. **使用投影**：

    查询时，你可以指定返回的字段，这称为投影。你可以在`find()`方法的第二个参数中指定投影。

    ```bash
    db.myCollection.find({name: 'John'}, {age: 1})
    ```

    这将返回满足条件的文档，但只包含`age`字段。

13. **使用`$or`和`$and`操作符**：

    使用`$or`和`$and`操作符来进行复杂的查询。

    ```bash
    db.myCollection.find({$or: [{name: 'John'}, {age: {$gt: 25}}]})
    db.myCollection.find({$and: [{name: 'John'}, {age: {$gt: 25}}]})
    ```

14. **查看服务器状态**：

    使用`db.serverStatus()`命令来查看MongoDB服务器的状态。

15. **查看集合状态**：

    使用`db.collection.stats()`命令来查看指定集合的状态。

    ```bash
    db.myCollection.stats()
    ```

16. **删除集合**：

    使用`drop()`方法来删除集合。

    ```bash
    db.myCollection.drop()
    ```

17. **创建和验证用户**：

    MongoDB允许你创建用户并对用户进行权限管理。以下是创建和验证用户的命令：

    ```bash
    // 在admin数据库中创建一个用户
    use admin
    db.createUser({
        user: "myUserAdmin",
        pwd: "abc123",
        roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
    })

    // 验证用户
    db.auth("myUserAdmin", "abc123")
    ```

18. **查看和修改系统参数**：

    使用`getParameter`和`setParameter`命令来查看和修改系统参数。

    ```bash
    db.runCommand({getParameter: '*'})
    db.runCommand({setParameter: {logLevel: 2}})
    ```

19. **导入和导出数据**：

    MongoDB提供了`mongoimport`和`mongoexport`工具来导入和导出数据。

    ```bash
    mongoimport --db myDatabase --collection myCollection --file myData.json
    mongoexport --db myDatabase --collection myCollection --out myData.json
    ```

20. **监控和诊断**：

    MongoDB提供了一些命令和工具来进行监控和诊断，例如`db.currentOp()`（查看当前操作）、`db.killOp()`（杀死操作）、`mongostat`（查看数据库状态）等。

    ```bash
    db.currentOp()
    db.killOp(opid)
    mongostat
    ```

21. **复制和分片**：

    MongoDB支持复制和分片来提高可用性和性能。复制提供了数据的冗余备份，并允许在多个服务器之间进行负载均衡。分片则允许你将数据分布在多个机器上。

