---
title: 使用REST请求调用AEM Forms
description: 使用REST请求调用在Workbench中创建的流程。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2505'
ht-degree: 0%

---

# 使用REST请求调用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

可以配置在Workbench中创建的进程，以便您可以通过代表性状态传输(REST)请求来调用它们。 从HTML页发送REST请求。 即，您可以使用REST请求直接从网页调用Forms进程。 例如，您可以打开网页的新实例。 然后，您可以调用Forms进程，并加载渲染的PDF文档，其中包含HTTPPOST请求中发送的数据。

存在两种类型的HTML客户端。 第一个HTML客户端是使用JavaScript编写的AJAX客户端。 第二个客户端是包含提交按钮的HTML表单。 基于HTML的客户端应用程序不是唯一可能的REST客户端。 任何支持HTTP请求的客户端应用程序都可以使用REST调用调用来调用服务。 例如，可以使用PDF表单中的REST调用来调用服务。 (请参阅 [从Acrobat调用MyApplication/EncryptDocument进程](#rest-invocation-examples).)

在使用REST请求时，建议您不要直接调用Forms服务。 而是调用在Workbench中创建的流程。 在创建用于REST调用的进程时，请使用程序化起点。 在这种情况下，将自动添加REST端点。 有关在Workbench中创建流程的信息，请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

使用REST调用服务时，系统会提示您输入AEM表单用户名和密码。 但是，如果不想指定用户名和密码，则可以禁用服务安全性。

要使用REST调用Forms服务（流程在激活时变为服务），请配置REST端点。 （请参阅中的“管理端点”） [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

配置REST端点后，您可以使用HTTPGET方法或POST方法调用Forms服务。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必需 `ServiceName` value是要调用的Forms服务的名称。 可选 `OperationName` value是服务操作的名称。 如果未指定此值，则此名称默认为 `invoke`，启动进程的操作名称。 可选 `ServiceVersion` value是以X.Y格式编码的版本。 如果未指定此值，则使用最新版本。 此 `enctype` 值也可为 `application/x-www-form-urlencoded`.

## 支持的数据类型 {#supported-data-types}

使用REST请求调用AEM Forms服务时，支持以下数据类型：

* Java原始数据类型，例如字符串和整数
* `com.adobe.idp.Document` 数据类型
* XML数据类型，例如 `org.w3c.Document` 和 `org.w3c.Element`
* 收藏集对象，例如 `java.util.List` 和 `java.util.Map`

  通常接受将这些数据类型作为Workbench中创建进程的输入值。

  如果使用HTTPPOST方法调用Froms服务，则参数将传递到HTTP请求正文中。 如果AEM Forms服务的签名具有字符串输入参数，则请求正文可以包含输入参数的文本值。 如果服务的签名定义了多个字符串参数，则请求可以遵循HTTP的 `application/x-www-form-urlencoded` 带有用作表单字段名称的参数名称的表示法。

  如果Forms服务返回字符串参数，则结果以文本形式表示输出参数。 如果服务返回多个字符串参数，则结果为XML文档，它按以下格式对输出参数进行编码：
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >此 `output-paramater1` value表示输出参数名称。

  如果Forms服务需要 `com.adobe.idp.Document` 参数，则只能使用HTTPPOST方法调用该服务。 如果服务需要 `com.adobe.idp.Document` 参数，则HTTP请求正文将成为输入Document对象的内容。

  如果AEM Forms服务需要多个输入参数，则HTTP请求正文必须是由RFC 1867定义的多部分MIME消息。 （RFC 1867是Web浏览器用于将文件上传到网站的标准。） 每个输入参数都必须作为多部分消息的单独部分发送，并编码在 `multipart/form-data` 格式。 每个部件的名称必须与参数的名称匹配。

  列表和映射也用作在Workbench中创建的AEM Forms进程的输入值。 因此，您可以在使用REST请求时使用这些数据类型。 不支持Java数组，因为它们未用作AEM Forms进程的输入值。

  如果输入参数是列表，则REST客户端可以通过多次指定该参数（针对列表中的每个项目指定一次）来发送该参数。 例如，如果A是文档列表，则输入必须是由多个名为A的部分组成的多部分消息。在这种情况下，每个名为A的部件都会成为输入列表中的项。 如果B是字符串列表，则输入可以是 `application/x-www-form-urlencoded` 包含多个名为B的字段的消息。在这种情况下，每个名为B的表单字段都会成为输入列表中的项。

  如果输入参数是映射并且是仅服务输入参数，则输入消息的每个部分/字段都成为映射中的键/值记录。 每个部分/字段的名称将成为记录的键。 每个部分/字段的内容将成为记录的值。

  如果输入映射不是仅服务输入参数，则属于该映射的每个键/值记录可以使用名为的参数发送，该参数是参数名称和记录键的串联。 例如，一个名为的输入映射 `attributes` 可以随以下键/值对的列表发送：

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  这将转换为包含三个记录的地图： `Color=red`， `Shape=box`、和 `Width=5`.

  列表和映射类型的输出参数会成为生成XML消息的一部分。 输出列表在XML中表示为一系列XML元素，列表中每个项目都有一个元素。 每个元素都被赋予与输出列表参数相同的名称。 每个XML元素的值是以下两个值之一：

* 列表中项目的文本表示形式（如果列表包含字符串类型）
* 指向文档内容的URL(如果列表包含 `com.adobe.idp.Document` 对象)

  以下示例是一个服务返回的XML消息，该服务具有名为的单个输出参数 *列表*，即整数的列表。
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`在生成的XML消息中，输出映射参数表示为一系列XML元素，其中映射中的每个记录都有一个元素。 每个元素的名称与映射记录的键相同。 每个元素的值是映射记录值的文本表示形式（如果映射由具有字符串值的记录组成）或指向文档内容的URL（如果映射由具有字符串值的记录组成） `com.adobe.idp.Document` 值)。 以下是由具有单个输出参数（名为）的服务返回的XML消息的示例 `map`. 此参数值是一个映射，其中包含与字母关联的记录 `com.adobe.idp.Document` 对象。
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 异步调用 {#asynchronous-invocations}

某些AEM Forms服务（例如以人为中心的长期流程）需要很长时间才能完成。 这些服务可以以非阻塞方式异步调用。 (请参阅 [调用以人为中心的长期进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

通过替换，可异步调用AEM Forms服务 `services` 替换为 `async_invoke` （在调用URL中），如以下示例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL返回负责此调用的作业的标识符值（采用“文本/普通”格式）。

可以通过以下方式检索异步调用的状态：使用调用URL `services` 替换为 `async_status`. URL必须包含 `job_id` 指定与此调用关联的作业的标识符值的参数。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL会根据作业管理器的规范（例如，2表示正在运行，3表示已完成，4表示失败，等等）返回一个整数值（以“文本/纯”格式），用于编码作业状态。

如果作业已完成，则URL将返回与同步调用服务相同的结果。

作业完成并检索到结果后，可以使用调用URL处理该作业，该调用 `services` 替换为 `async_dispose`. URL还应包含 `job_id` 指定作业的标识符值的参数。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作业处置成功，则此URL将返回空消息。

## 错误报告 {#error-reporting}

如果由于服务器上抛出异常而无法完成同步或异步调用请求，则该异常将作为HTTP响应消息的一部分报告。 如果调用URL(或 `async_result` 异步调用中的URL)没有.xml后缀，REST提供程序返回HTTP代码 `500 Internal Server Error` 后跟异常消息。

如果调用URL(或 `async_result` URL（在异步调用中）确实具有.xml后缀，REST提供程序返回HTTP代码 `200 OK`后跟一个描述异常的XML文档，格式如下。

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

此 `DSCError` 元素是可选的，并且仅当例外为的实例时才会出现 `com.adobe.idp.dsc.DSCException`.

## 安全性和身份验证 {#security-and-authentication}

要为REST调用提供安全传输，AEM Forms管理员可以在托管AEM Forms的J2EE应用程序服务器中启用HTTPS协议。 此配置特定于J2EE应用程序服务器；它不是forms服务器配置的一部分。

>[!NOTE]
>
>作为希望通过REST端点公开流程的Workbench开发人员，请记住XSS漏洞问题。 XSS漏洞可用于窃取或操纵Cookie、修改内容的呈现方式，以及危害机密信息。 如果XSS漏洞是一个问题，建议您使用其他输入和输出数据验证规则来扩展进程逻辑。

## 支持REST调用的AEM Forms服务 {#aem-forms-services-that-support-rest-invocation}

虽然建议您使用Workbench而不是直接服务来调用创建的流程，但有些一些AEM Forms服务确实支持REST调用。 建议直接调用进程而不是服务的原因是，这样可以更高效地调用进程。 请考虑以下方案。 假定您要从REST客户端创建策略。 即，您希望REST客户端定义策略名称、离线租赁期等值。

要创建策略，您必须定义复杂的数据类型，例如 `PolicyEntry` 对象。 A `PolicyEntry` 对象定义属性，例如与策略关联的权限。 (请参阅 [创建策略](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

而不是发送REST请求来创建策略(这将包括定义复杂的数据类型，例如 `PolicyEntry` 对象)，创建使用Workbench创建策略的进程。 定义进程以接受原始输入变量，如定义进程名称的字符串值或定义离线租赁期的整数。

这样，您就不必创建包含操作所需的复杂数据类型的REST调用请求。 该进程定义了复杂的数据类型，您从REST客户端执行的所有操作是调用该进程并传递原始数据类型。 有关使用REST调用进程的信息，请参见 [使用REST调用MyApplication/EncryptDocument进程](#rest-invocation-examples).

以下列表列出了支持直接REST调用的AEM Forms服务。

* Distiller服务
* Rights Management服务
* 生成PDF服务
* 生成3dPDF服务
* FormDataIntegration

## REST调用示例 {#rest-invocation-examples}

提供了以下REST调用示例：

* 将布尔值传递给AEM Forms进程
* 将日期值传递到AEM Forms进程
* 将文档传递到AEM Forms进程
* 将文档和文本值传递到AEM Forms进程
* 将枚举值传递到AEM Forms进程
* 使用REST调用MyApplication/EncryptDocument进程
* 从Acrobat调用MyApplication/EncryptDocument进程

  每个示例都演示了向AEM Forms流程传递各种数据类型

**将布尔值传递给进程**

以下HTML示例传递了两个 `Boolean` 值到AEM Forms进程，名为 `RestTest2`. 调用方法的名称为 `invoke` 版本为1.0。请注意，使用的是“HTML发布”方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**将日期值传递给进程**

以下HTML示例将日期值传递到名为的AEM Forms进程 `SOAPEchoService`. 调用方法的名称为 `echoCalendar`. 请注意，HTML `Post` 方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**将文档传递到进程**

以下HTMLAEM Forms示例调用名为 `MyApplication/EncryptDocument` 需要PDF文件。 有关此过程的信息，请参见 [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**将文档和文本值传递到进程**

以下HTMLAEM Forms示例调用名为 `RestTest3` 需要一个文档和两个文本值。 请注意，使用的是“HTML发布”方法。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**将枚举值传递给进程**

以下HTMLAEM Forms示例调用名为 `SOAPEchoService` 需要枚举值。 请注意，使用的是“HTML发布”方法。

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**使用REST调用MyApplication/EncryptDocument进程**

您可以调用名为的AEM Forms短期进程 *MyApplication/EncryptDocument* 通过使用REST。

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

   当使用REST请求调用此进程时，加密的PDF文档会显示在Web浏览器中。 在查看PDF文档之前，请指定密码（除非禁用了安全性）。 以下HTML代码表示对 `MyApplication/EncryptDocument` 进程。

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**从Acrobat调用MyApplication/EncryptDocument进程** {#invoke-process-acrobat}

您可以使用REST请求从Acrobat调用Forms进程。 例如，您可以调用 *MyApplication/EncryptDocument* 进程。 要从Acrobat调用Forms进程，请在Designer的XDP文件上放置提交按钮。 (请参阅 [Designer帮助](https://www.adobe.com/go/learn_aemforms_designer_63_cn).)

指定用于在按钮的 *提交到URL* 字段，如下图所示。

用于调用进程的完整URL为https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果流程需要PDF文档作为输入值，请确保以PDF形式提交表单，如上图所示。 此外，要成功调用进程，该进程必须返回PDF文档。 否则，Acroabt无法处理返回值并出现错误。 不必指定输入进程变量的名称。 例如， *MyApplication/EncryptDocument* 进程具有名为的输入变量 `inDoc`. 只要将表单作为PDF提交，您就不必指定inDoc。

您还可以将表单数据以XML形式提交到Forms流程。要提交XML数据，请确保 `Submit As` 下拉列表指定XML。 由于流程的返回值必须是PDF文档，因此PDF文档会显示在Acrobat中。
