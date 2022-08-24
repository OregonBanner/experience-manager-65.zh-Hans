---
title: 使用REST请求调用AEM Forms
seo-title: Invoking AEM Forms using REST Requests
description: 使用REST请求调用在Workbench中创建的进程。
seo-description: Invoke processes created in Workbench using REST requests.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# 使用REST请求调用AEM Forms {#invoking-aem-forms-using-rest-requests}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

可以配置在Workbench中创建的流程，以便您可以通过表示状态传输(REST)请求调用这些流程。 REST请求从HTML页面发送。 即，您可以使用REST请求直接从网页调用Forms进程。 例如，您可以打开网页的新实例。 然后，您可以调用Forms进程，并加载已渲染的PDF文档，其中包含在HTTPPOST请求中发送的数据。

有两种HTML客户端。 第一个HTML客户端是使用JavaScript编写的AJAX客户端。 第二个客户端是包含提交按钮的HTML表单。 基于HTML的客户端应用程序不是唯一可能的REST客户端。 任何支持HTTP请求的客户端应用程序都可以使用REST调用来调用服务。 例如，您可以使用PDF表单中的REST调用来调用服务。 (请参阅 [从Acrobat调用MyApplication/EncryptDocument进程](#rest-invocation-examples).)

使用REST请求时，建议您不要直接调用Forms服务。 请改为调用在Workbench中创建的进程。 创建用于REST调用的进程时，请使用程序化起点。 在这种情况下，将自动添加REST端点。 有关在Workbench中创建流程的信息，请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

使用REST调用服务时，系统会提示您输入AEM Forms用户名和密码。 但是，如果您不想指定用户名和密码，则可以禁用服务安全性。

要使用REST调用Forms服务（当该进程被激活时，该进程将变为服务），请配置REST端点。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

配置REST端点后，您可以使用HTTPGET方法或POST方法调用Forms服务。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必填项 `ServiceName` value是要调用的Forms服务的名称。 可选 `OperationName` value是服务操作的名称。 如果未指定此值，则此名称默认为 `invoke`，这是启动进程的操作名称。 可选 `ServiceVersion` 值是以X.Y格式编码的版本。 如果未指定此值，则使用最新版本。 的 `enctype` 值也可以 `application/x-www-form-urlencoded`.

## 支持的数据类型 {#supported-data-types}

使用REST请求调用AEM Forms服务时支持以下数据类型：

* Java基元数据类型，如字符串和整数
* `com.adobe.idp.Document` 数据类型
* XML数据类型，例如 `org.w3c.Document` 和 `org.w3c.Element`
* 集合对象，如 `java.util.List` 和 `java.util.Map`

   这些数据类型通常作为在Workbench中创建的流程的输入值。

   如果通过HTTPPOST方法调用Froms服务，则参数将在HTTP请求正文中传递。 如果AEM Forms服务的签名具有字符串输入参数，则请求正文可以包含输入参数的文本值。 如果服务的签名定义了多个字符串参数，则请求可以遵循HTTP的 `application/x-www-form-urlencoded` 使用参数名称作为表单字段名称的符号。

   如果Forms服务返回字符串参数，则结果将作为输出参数的文本表示形式。 如果服务返回多个字符串参数，则结果将生成以下格式对输出参数进行编码的XML文档：
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >的 `output-paramater1` 值表示输出参数名称。

   如果Forms服务需要 `com.adobe.idp.Document` 参数，则只能使用HTTPPOST方法调用服务。 如果服务需要 `com.adobe.idp.Document` 参数，则HTTP请求正文将成为输入Document对象的内容。

   如果AEM Forms服务需要多个输入参数，则HTTP请求正文必须是由RFC 1867定义的多部分MIME消息。 （RFC 1867是Web浏览器将文件上传到网站时使用的标准。） 每个输入参数必须作为multipart消息的单独部分发送，并在中进行编码 `multipart/form-data` 格式。 每个部件的名称必须与参数的名称匹配。

   列表和映射还用作在Workbench中创建的AEM Forms进程的输入值。 因此，在使用REST请求时，可以使用这些数据类型。 不支持Java数组，因为它们不用作AEM Forms进程的输入值。

   如果输入参数是列表，则REST客户端可以通过多次指定该参数来发送该参数（对列表中的每个项目一次）。 例如，如果A是文档列表，则输入必须是由多个名为A的部分组成的多部分消息。在这种情况下，每个名为A的部分将成为输入列表中的项目。 如果B是字符串列表，则输入可以是 `application/x-www-form-urlencoded` 消息由多个名为B的字段组成。在这种情况下，每个名为B的表单字段都将成为输入列表中的一个项目。

   如果输入参数是映射，并且它是仅服务的输入参数，则输入消息的每个部分/字段将成为映射中的键/值记录。 每个部件/字段的名称将成为记录的键。 每个部件/字段的内容将成为记录的值。

   如果输入映射不是仅服务的输入参数，则属于该映射的每个键/值记录都可以使用名为的参数来发送，该参数是参数名称和记录键的级联。 例如，一个名为 `attributes` 可随以下键/值对列表一起发送：

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   这将转换为三条记录的地图： `Color=red`, `Shape=box`和 `Width=5`.

   列表和映射类型的输出参数将成为生成XML消息的一部分。 输出列表以XML形式表示为一系列XML元素，每个元素对应列表中的每个项。 每个元素的名称都与输出列表参数相同。 每个XML元素的值是两项之一：

* 列表中项目的文本表示形式（如果列表包含字符串类型）
* 指向文档内容的URL(如果列表包含 `com.adobe.idp.Document` 对象)

   以下示例是由具有名为的单个输出参数的服务返回的XML消息 *列表*，这是整数列表。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`输出映射参数在生成的XML消息中表示为一系列XML元素，每个元素对应于映射中的每个记录。 每个元素的名称均与映射记录的键值相同。 每个元素的值是映射记录值的文本表示形式（如果映射由具有字符串值的记录组成），或者是指向文档内容的URL(如果映射由具有 `com.adobe.idp.Document` 值)。 以下是服务返回的XML消息示例，该服务具有一个名为 `map`. 此参数值是由将字母与 `com.adobe.idp.Document` 对象。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 异步调用 {#asynchronous-invocations}

一些AEM Forms服务（例如以人为中心的长期流程）需要较长的时间才能完成。 可以以非阻塞方式异步调用这些服务。 (请参阅 [调用以人为中心的长寿过程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

可以通过替换 `services` with `async_invoke` ，如以下示例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL会返回负责此调用的作业的标识符值（以“文本/纯”格式）。

异步调用的状态可以通过使用 `services` 替换为 `async_status`. URL必须包含 `job_id` 参数，指定与此调用关联的作业的标识符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL会返回一个整数值（以“文本/纯”格式），该值将根据作业管理器的规范（例如，2表示正在运行，3表示已完成，4表示失败，等等）来编码作业状态。

如果作业完成，则URL会返回与同步调用服务相同的结果。

完成作业并检索结果后，可通过使用 `services` 替换为 `async_dispose`. 该URL还应包含 `job_id` 参数，指定作业的标识符值。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作业被成功处理，则此URL会返回空消息。

## 错误报告 {#error-reporting}

如果由于服务器上引发异常而无法完成同步或异步调用请求，则会将异常报告为HTTP响应消息的一部分。 如果调用URL(或 `async_result` 如果是异步调用，则URL不具有.xml后缀，则REST提供程序会返回HTTP代码 `500 Internal Server Error` 后跟异常消息。

如果调用URL(或 `async_result` 如果是异步调用，则URL的后缀为.xml，则REST提供程序会返回HTTP代码 `200 OK`然后是XML文档，该文档以下列格式描述例外。

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

的 `DSCError` 元素是可选的，并且仅当例外为的实例时才显示 `com.adobe.idp.dsc.DSCException`.

## 安全性和身份验证 {#security-and-authentication}

为了为REST调用提供安全传输，AEM Forms管理员可以在托管AEM Forms的J2EE应用程序服务器上启用HTTPS协议。 此配置专用于J2EE应用程序服务器；它不是forms服务器配置的一部分。

>[!NOTE]
>
>作为希望通过REST端点公开您的进程的Workbench开发人员，请牢记XSS漏洞问题。 XSS漏洞可用于窃取或操纵Cookie、修改内容呈现方式和泄露机密信息。 如果存在XSS漏洞，建议使用附加的输入和输出数据验证规则扩展进程逻辑。

## 支持REST调用的AEM Forms服务 {#aem-forms-services-that-support-rest-invocation}

尽管建议您调用使用Workbench创建的进程而不是直接调用服务，但有些AEM Forms服务确实支持REST调用。 建议直接调用流程而不是直接调用服务的原因在于调用流程的效率更高。 请考虑以下情景。 假定您要从REST客户端创建策略。 也就是说，您希望REST客户端定义策略名称、脱机租用期等值。

要创建策略，您必须定义复杂的数据类型，例如 `PolicyEntry` 对象。 A `PolicyEntry` 对象定义属性，如与策略关联的权限。 (请参阅 [创建策略](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

而不是发送REST请求以创建策略(这包括定义复杂的数据类型，例如 `PolicyEntry` 对象)，使用Workbench创建策略的流程。 定义流程以接受基元输入变量，如定义流程名称的字符串值或定义离线租赁期的整数。

这样，您就不必创建包含操作所需的复杂数据类型的REST调用请求。 该流程定义了复杂的数据类型，您从REST客户端执行的所有操作都是调用该流程并传递基元数据类型。 有关使用REST调用进程的信息，请参阅 [使用REST调用MyApplication/EncryptDocument进程](#rest-invocation-examples).

以下列表指定了支持直接REST调用的AEM Forms服务。

* Distiller服务
* Rights Management服务
* GeneratePDF服务
* Generate3dPDF服务
* FormDataIntegration

## REST调用示例 {#rest-invocation-examples}

提供了以下REST调用示例：

* 将布尔值传递到AEM Forms进程
* 将日期值传递到AEM Forms流程
* 将文档传递到AEM Forms流程
* 将文档和文本值传递到AEM Forms进程
* 将枚举值传递到AEM Forms进程
* 使用REST调用MyApplication/EncryptDocument进程
* 从Acrobat调用MyApplication/EncryptDocument进程

   每个示例都演示了如何将不同的数据类型传递到AEM Forms流程

**将布尔值传递给进程**

以下HTML示例传递了两个 `Boolean` 值到名为的AEM Forms进程 `RestTest2`. 调用方法的名称为 `invoke` 并且版本为1.0。请注意，使用了“HTML后”方法。

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

**将日期值传递给流程**

以下HTML示例将日期值传递给名为 `SOAPEchoService`. 调用方法的名称为 `echoCalendar`. 请注意，HTML `Post` 方法。

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

**将文档传递到流程**

以下HTML示例将调用名为的AEM Forms进程 `MyApplication/EncryptDocument` 需要PDF文档。 有关此过程的信息，请参阅 [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

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

**将文档和文本值传递到流程**

以下HTML示例将调用名为的AEM Forms进程 `RestTest3` 需要一个文档和两个文本值。 请注意，已使用HTMLPost方法。

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

**将枚举值传递到进程**

以下HTML示例将调用名为的AEM Forms进程 `SOAPEchoService` 需要枚举值。 请注意，已使用HTMLPost方法。

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

您可以调用名为的AEM Forms短期流程 *MyApplication/EncryptDocument* 使用REST。

>[!NOTE]
>
>此过程不基于现有的AEM Forms进程。 要遵循代码示例，请创建一个名为 `MyApplication/EncryptDocument` 使用workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此过程时，会执行以下操作：

1. 获取传递到流程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此过程的输入参数是 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为 `outDoc`.

   当使用REST请求调用此过程时，加密的PDF文档将显示在Web浏览器中。 在查看PDF文档之前，您需要指定密码（除非禁用了安全性）。 以下HTML代码表示对的REST调用请求 `MyApplication/EncryptDocument` 进程。

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

您可以使用REST请求从Acrobat调用Forms进程。 例如，您可以调用 *MyApplication/EncryptDocument* 进程。 要从Acrobat调用Forms进程，请在Designer中的XDP文件上放置提交按钮。 (请参阅 [Designer帮助](https://www.adobe.com/go/learn_aemforms_designer_63).)

指定在按钮的 *提交到URL* 字段，如下图所示。

调用该过程的完整URL是https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果流程要求将PDF文档作为输入值，请确保将表单作为PDF提交，如上图所示。 此外，要成功调用进程，该进程必须返回PDF文档。 否则，Acrobat无法处理返回值，并出现错误。 您不必指定输入进程变量的名称。 例如， *MyApplication/EncryptDocument* 进程具有名为的输入变量 `inDoc`. 只要表单提交为PDF，您就不必指定inDoc。

您还可以将表单数据作为XML提交到Forms进程。要提交XML数据，请确保 `Submit As` 下拉列表指定XML。 由于流程的返回值必须是PDF文档，因此PDF文档会显示在Acrobat中。
