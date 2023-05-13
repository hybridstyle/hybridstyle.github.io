macos 上如何安装 mongodb
在macOS上安装MongoDB，你可以选择使用官方的MongoDB Community Edition。以下是安装步骤：

1. **安装Homebrew**：Homebrew是一个macOS平台下的软件包管理工具，能够方便地安装软件。如果你的电脑上还没有安装Homebrew，你可以在终端中运行以下命令来安装：

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **使用Homebrew安装MongoDB**：安装好Homebrew之后，你可以使用Homebrew来安装MongoDB Community Edition。在终端中运行以下命令：

   ```bash
   brew tap mongodb/brew
   brew install mongodb-community
   ```

3. **启动MongoDB服务**：安装完MongoDB之后，你可以使用以下命令来启动MongoDB服务：

   ```bash
   brew services start mongodb-community
   ```

   这将会在后台启动MongoDB服务。

4. **连接到MongoDB**：启动服务后，你可以使用`mongo`命令来连接到MongoDB。在终端中输入`mongo`，这将启动MongoDB的交互式shell，你可以在这个shell中执行各种操作。

以上就是在macOS上安装MongoDB的基本步骤。如果你在安装过程中遇到任何问题，或者想要了解更多的信息，你可以参考MongoDB的官方文档。