---
layout: post
title: "Centos8上安装 mongodb"
date: 2023-05-19
categories: Mongodb
---
        在CentOS 8上安装MongoDB的步骤如下：

1. **添加MongoDB存储库**

    首先，你需要创建一个新的MongoDB存储库。打开你的终端并输入以下命令以创建一个新的文件：

    ```bash
    sudo vi /etc/yum.repos.d/mongodb-org.repo
    ```

    这将打开一个文本编辑器。将以下内容粘贴到文件中，然后保存并关闭文件：

    ```bash
    [mongodb-org-6.0]
    name=MongoDB Repository
    baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/x86_64/
    gpgcheck=1
    enabled=1
    gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc
    ```

2. **安装MongoDB**

    有了新的存储库之后，你可以通过运行以下命令来安装MongoDB：

    ```bash
    sudo dnf install mongodb-org
    ```

3. **启动MongoDB服务**

    安装完成后，你需要启动MongoDB服务。运行以下命令来启动它：

    ```bash
    sudo systemctl start mongod
    ```

    如果你想要MongoDB在启动时自动运行，你可以运行以下命令来实现这一点：

    ```bash
    sudo systemctl enable mongod
    ```

4. **检查MongoDB的安装**

    最后，你应该检查MongoDB是否已经成功安装和运行。你可以运行以下命令来检查MongoDB的状态：

    ```bash
    sudo systemctl status mongod
    ```

    如果一切正常，你会看到输出中的 "Active: active (running)"，这表明MongoDB正在运行。

这样就可以在CentOS 8上安装和运行MongoDB了。接下来你可以开始使用MongoDB来存储和管理你的数据了。


Centos8下修改 mongodb 配置文件

在 CentOS 8 中，MongoDB 的默认配置文件位于 `/etc/mongod.conf`。你可以使用你最喜欢的文本编辑器对其进行修改。例如，使用 `vi`，你可以运行以下命令：

```bash
sudo vi /etc/mongod.conf
```

以下是可能需要修改的一些配置项：

1. **systemLog:** MongoDB 的日志设置。这包括日志文件的位置以及日志数据的格式。

2. **storage:** MongoDB 数据库文件的存储设置。这包括数据库文件的位置以及存储引擎的类型。

3. **net:** 网络接口设置，这包括服务器绑定的IP地址和端口号。

例如，如果你想更改 MongoDB 服务器绑定的 IP 地址，可以在 `net` 配置部分修改 `bindIp` 的值。

在你对配置文件进行了修改后，记得保存文件，然后重新启动 MongoDB 服务以应用新的配置。你可以使用以下命令来重启 MongoDB：

```bash
sudo systemctl restart mongod
```

然后，你可以使用下面的命令检查 MongoDB 服务的状态，确保它已经正确启动：

```bash
sudo systemctl status mongod
```

这就是在 CentOS 8 下修改 MongoDB 配置文件的方法。在修改配置文件时，要特别小心，因为错误的配置可能会导致 MongoDB 无法正确运行。

mongodb 的备份 js 文件怎么导入
你可以使用MongoDB的命令行工具 `mongosh` 来运行备份的JavaScript(JS)文件。这个工具可以执行文件中包含的所有MongoDB命令和操作。

以下是你需要执行的步骤：

1. **打开终端**：首先，打开你的命令行终端。

2. **运行文件**：接着，运行下面的命令来执行你的JS文件。将 `<yourfile.js>` 替换为你的实际JS文件路径和文件名，将 `<dbname>` 替换为你希望操作的数据库名称：

    ```bash
    mongosh <dbname> <yourfile.js>
    ```

3. **完成导入**：执行上述命令后，`mongosh` 工具将连接到本地运行的MongoDB服务器（默认连接localhost的27017端口），并在指定的数据库 `<dbname>` 上执行JS文件中的所有操作。完成后，你的JS备份文件就导入完成了。

如果你的MongoDB服务器设置了身份验证（用户名和密码），或者MongoDB服务器不在本地运行，那么你需要修改连接命令以包含正确的身份验证信息和服务器地址。例如：

```bash
mongosh --username <username> --password <password> --host <hostname>:<port> <dbname> <yourfile.js>
```

请注意，`mongosh` 命令行工具需要在你的系统PATH中，而且MongoDB服务器需要在运行中才能执行这些操作。如果在执行这些步骤时遇到任何问题，你可能需要检查你的MongoDB服务器设置和状态，以及JS文件的内容是否正确。