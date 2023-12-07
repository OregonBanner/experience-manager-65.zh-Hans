---
title: 表达式生成器中的远程函数
description: 通信管理中的表达式生成器允许您创建表达式和远程函数。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# 表达式生成器中的远程函数{#remote-functions-in-expression-builder}

使用表达式生成器，您可以创建表达式或条件，以对数据字典或最终用户提供的数据值进行计算。 通信管理使用表达式求值结果来选择资产（例如文本、图像、列表和条件），并根据需要在通信中插入这些资产。

## 使用表达式生成器创建表达式和远程函数 {#creating-expressions-and-remote-functions-with-expression-builder}

表达式生成器内部使用JSP EL库，因此表达式遵循JSPEL语法。 有关更多信息，请参阅 [表达式示例](#exampleexpressions).

![表达式生成器](assets/expressionbuilder.png)

### 运算符 {#operators}

可在表达式中使用的运算符在表达式生成器的顶栏中可用。

### 表达式示例 {#exampleexpressions}

以下是一些可在通信管理解决方案中使用的常用JSP EL示例：

* 添加两个数字： ${number1 + number2}
* 要连接两个字符串： ${str1} ${str2}
* 要比较两个数字：${age &lt; 18}

欲知更多信息，请参见 [JSP EL规范](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). 客户端表达式管理器不支持JSP EL规范中的某些变量和函数，具体为：

* 集合索引和映射键(使用 [] 表示法)不支持在客户端计算的表达式的变量名称中使用。
* 以下是表达式中使用的参数类型或函数的返回类型：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔值
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

### 远程功能 {#remote-function}

远程函数提供了在表达式中使用自定义逻辑的功能。 您可以编写自定义逻辑，以作为Java中的方法用于表达式中，并且可以在表达式中使用相同的函数。 可用的远程函数列在表达式编辑器左侧的“远程函数”选项卡下。

![remotefunction](assets/remotefunction.png)

#### 添加自定义远程函数 {#adding-custom-remote-functions}

您可以创建一个自定义捆绑包以导出您自己的远程函数，以便在表达式中使用。 要创建自定义捆绑包以导出您自己的远程函数，请执行以下任务。 它演示了如何编写自定义函数以将其输入字符串转换为大写。

1. 为OSGi服务定义一个接口，该接口包含正导出以供Expression Manager使用的方法。
1. 在接口A上声明方法，并使用@ServiceMethod注释(com.adobe.exm.expeval.ServiceMethod)对其进行注释。 Expression Manager忽略任何未注释的方法。 ServiceMethod注释具有以下可选属性，也可以指定这些属性：

   1. **已启用**：确定是否启用此方法。 表达式管理器会忽略已禁用的方法。
   1. **familyId**：指定方法的系列（组）。 如果为空，则Expression Manager假定该方法属于默认系列。 没有从中选择函数的家族的注册表（默认家族除外）。 Expression Manager通过获取由各种捆绑导出的所有函数指定的所有系列ID的并集来动态创建注册表。 由于他们在此指定的ID也会显示在表达式创作用户界面中，因此请确保该ID可合理读取。
   1. **显示名称**：人类可读的函数名称。 此名称用于创作用户界面中的显示。 如果为空，则Expression Manager将使用函数的前缀和local-name构造默认名称。
   1. **描述**：函数的详细描述。 此描述用于创作用户界面中的显示目的。 如果为空，则Expression Manager将使用函数的前缀和local-name构建默认说明。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   这些方法的参数也可以选择使用@ServiceMethodParameter注释(com.adobe.exm.expeval.ServiceMethodParameter)进行注释。 此注释仅用于指定在创作用户界面中使用的人类可读名称以及方法参数的描述。 确保接口方法的参数和返回值属于以下类型之一：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔值
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

exm.service=true条目指示Expression Manager，该服务包含适合在表达式中使用的远程函数。 此 &lt;service_id> 值必须是有效的Java标识符（字母数字、$、_且不含其他特殊字符）。 此值以REMOTE_关键字为前缀，构成表达式内部使用的前缀。 例如，可以在使用REMOTE_foo：bar()的表达式中引用带有注释方法bar()的接口以及服务属性中的服务ID foo。

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

* **GoodFunctions.jar.zip** 是带有包的jar文件，其中包含示例远程函数定义。 下载GoodFunctions.jar.zip文件并将其解压缩以获取jar文件。
* **GoodFunctions.zip** 是用于定义自定义远程函数并为其创建捆绑包的源代码包。

GoodFunctions.jar.zip

[获取文件](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[获取文件](assets/goodfunctions.zip)
