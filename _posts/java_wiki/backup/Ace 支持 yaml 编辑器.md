Ace 支持 yaml 编辑器
可以在 Ace 的官方网站上查看和下载 Ace 编辑器。官方网站地址为：https://ace.c9.io/

在该网站上，你可以找到 Ace 的最新版本、示例代码和文档，还可以下载源代码和相关资源文件。此外，该网站还提供了在线演示和代码编辑器，可以让你快速体验 Ace 编辑器的功能。

如果你想使用 Ace 编辑器，可以下载其源代码，并根据自己的需要进行自定义和扩展。Ace 的源代码托管在 GitHub 上，你可以在该页面上获取最新的源代码：https://github.com/ajaxorg/ace

要让 Ace 编辑器支持 YAML 编辑，需要使用 Ace 的扩展模块和语言模块。以下是一些简单的步骤，可以帮助你在 Ace 中添加 YAML 支持：

1. 下载 Ace 编辑器源代码，或者使用 npm 安装 Ace 模块：

   ```
   npm install ace-builds
   ```

2. 在 HTML 文件中引入 Ace 编辑器和 YAML 语言模块：

   ```
   <script src="path/to/ace.js"></script>
   <script src="path/to/mode-yaml.js"></script>
   ```

3. 创建 Ace 编辑器实例，并设置 YAML 模式：

   ```
   var editor = ace.edit("editor");
   editor.setTheme("ace/theme/monokai");
   editor.session.setMode("ace/mode/yaml");
   ```

   在这个例子中，我们创建了一个 ID 为 "editor" 的编辑器实例，并将其设置为 YAML 模式。你还可以选择其他主题和模式，根据需要进行自定义。

4. 运行你的应用程序，打开 Ace 编辑器，就可以开始编辑 YAML 文件了。

这些步骤只是一个简单的示例，你可以根据自己的需要进行更多的自定义和扩展。Ace 编辑器的文档和示例提供了更详细的说明和示例，可以帮助你更好地了解如何使用和扩展 Ace 编辑器。