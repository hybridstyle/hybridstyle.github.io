freemarker 实现 base64 编码指令
要在 Freemarker 中实现 Base64 编码指令，可以使用 Freemarker 的自定义指令和 Java 的 Base64 类库来完成。

下面是一个简单的示例，展示了如何在 Freemarker 中创建一个自定义指令，将指定的字符串进行 Base64 编码：

1. 首先，创建一个自定义指令类 `Base64EncodeDirective`：

```java
import java.util.List;
import java.util.Base64;
import freemarker.core.Environment;
import freemarker.template.TemplateDirectiveBody;
import freemarker.template.TemplateDirectiveModel;
import freemarker.template.TemplateException;
import freemarker.template.TemplateModel;
import freemarker.template.TemplateModelException;
import freemarker.template.utility.StringUtil;

public class Base64EncodeDirective implements TemplateDirectiveModel {
  public void execute(Environment env, Map params, TemplateModel[] loopVars,
      TemplateDirectiveBody body) throws TemplateException, IOException {

    if (params.size() != 1) {
      throw new TemplateModelException("Wrong arguments");
    }

    String strToEncode = params.get("value").toString();
    String encodedStr = Base64.getEncoder().encodeToString(strToEncode.getBytes());

    Writer out = env.getOut();
    out.write(encodedStr);
  }
}
```