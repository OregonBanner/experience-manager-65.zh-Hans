---
title: 表达式生成器中的远程函数
seo-title: 表达式生成器
description: 通过通信管理中的表达式生成器，您可以创建表达式和远程函数。
seo-description: 通过通信管理中的表达式生成器，您可以创建表达式和远程函数。
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
feature: 通信管理
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 2%

---

# 表达式生成器{#remote-functions-in-expression-builder}中的远程函数

使用表达式生成器，您可以创建对数据字典或最终用户提供的数据值执行计算的表达式或条件。 通信管理使用表达式评估的结果来选择资产（如文本、图像、列表和条件），并根据需要将其插入通信中。

## 使用表达式生成器{#creating-expressions-and-remote-functions-with-expression-builder}创建表达式和远程函数

表达式生成器内部使用JSP EL库，因此表达式遵循JSPEL语法。 有关更多信息，请参阅[示例表达式](#exampleexpressions)。

![表达式生成器](assets/expressionbuilder.png)

### 运算符 {#operators}

表达式生成器顶栏中提供了可用于表达式的运算符。

### 示例表达式 {#exampleexpressions}

以下是一些常用的JSP EL示例，您可以在通信管理解决方案中使用这些示例：

* 要添加两个数字：${number1 + number2}
* 要连接两个字符串：${str1} ${str2}
* 要比较两个数字：${age &lt; 18}

您可以在[JSP EL规范](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)中找到更多信息。 客户端表达式管理器不支持JSP EL规范中的某些变量和函数，具体是：

* 客户端上计算的表达式的变量名称不支持集合索引和映射键（使用[]符号）。
* 以下是表达式中使用的函数的参数类型或返回类型：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔型
   * java.lang.Integer
   * 整数
   * java.util.list
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 字节
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 远程函数{#remote-function}

远程函数提供在表达式中使用自定义逻辑的功能。 您可以编写自定义逻辑，以在表达式中用作Java中的方法，而表达式中也可以使用相同的函数。 可用的远程函数列在表达式编辑器左侧的“远程函数”选项卡下。

![remotefunction](assets/remotefunction.png)

#### 添加自定义远程函数{#adding-custom-remote-functions}

您可以创建自定义包以导出您自己的远程函数，以便在表达式中使用。 要创建自定义包以导出您自己的远程功能，请执行以下任务。 它演示了如何编写自定义函数以大写其输入字符串。

1. 为OSGi服务定义一个接口，其中包含要导出以供表达式管理器使用的方法。
1. 在界面A上声明方法，然后使用@ServiceMethod annotation(com.adobe.exm.expeval.ServiceMethod)对它们添加批注。 表达式管理器会忽略任何未注释的方法。 ServiceMethod注释具有以下可选属性，这些属性也可以指定：

   1. **已启用**:确定此方法是否已启用。表达式管理器会忽略禁用的方法。
   1. **familyId**:指定方法的族（组）。如果为空，则表达式管理器会假定该方法属于缺省族。 没有从中选择函数的族的注册表（默认的除外）。 表达式管理器通过采用由各种包导出的所有函数指定的所有族ID的并集来动态创建注册表。 请确保他们在此处指定的ID可合理读取，因为该ID也显示在表达式创作用户界面中。
   1. **displayName**:函数的人类可读名称。此名称用于在创作用户界面中显示。 如果为空，则表达式管理器使用函数的前缀和local-name构建默认名称。
   1. **描述**:函数的详细描述。此描述用于在创作用户界面中进行显示。 如果为空，表达式管理器将使用函数的前缀和local-name构建默认描述。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   也可以选择使用@ServiceMethodParameter annotation(com.adobe.exm.expeval.ServiceMethodParameter)对方法的参数进行注释。 此注释仅用于指定在创作用户界面中使用的方法参数的可读名称和描述。 确保接口方法的参数和返回值属于以下类型之一：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔型
   * java.lang.Integer
   * 整数
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 字节
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. 定义接口的实现，将其配置为OSGI服务，并定义以下服务属性：

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true条目会指示表达式管理器，该服务包含适合在表达式中使用的远程函数。 &lt;service_id>值必须是有效的Java标识符(字母数字、$、_（不含其他特殊字符）)。 此值前缀为REMOTE_关键字，用作表达式内使用的前缀。 例如，可以使用REMOTE_foo:bar()在表达式中引用带有注释的方法bar()和服务ID foo的接口。

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

以下是要使用的示例存档：

* **GoodFunctions.jar.zip是** 包含包含示例远程函数定义的包的jar文件。下载GoodFunctions.jar.zip文件并解压缩，以获取jar文件。
* **GoodFunctions.** zip是用于定义自定义远程函数并为其创建包的源代码包。

GoodFunctions.jar.zip

[获取文件](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[获取文件](assets/goodfunctions.zip)
