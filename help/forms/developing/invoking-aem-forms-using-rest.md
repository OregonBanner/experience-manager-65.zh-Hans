---
title: 使用REST请求调用AEM Forms
seo-title: 使用REST请求调用AEM Forms
description: 'null'
seo-description: 'null'
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 0%

---


# 使用REST请求调用AEM Forms{#invoking-aem-forms-using-rest-requests}

可以配置在Workbench中创建的流程，以便通过代表性状态转移(REST)请求调用它们。 REST请求从HTML页发送。 即，您可以使用REST请求从网页直接调用Forms进程。 例如，可以打开网页的新实例。 然后，您可以调用Forms进程，并加载呈现的PDF文档，其中包含在HTTPPOST请求中发送的数据。

存在两种类型的HTML客户端。 第一个HTML客户端是使用JavaScript编写的AJAX客户端。 第二个客户端是包含提交按钮的HTML表单。 基于HTML的客户端应用程序并非唯一可能的REST客户端。 任何支持HTTP请求的客户端应用程序都可以使用REST调用调用服务。 例如，您可以通过从PDF表单调用REST来调用服务。 (请参阅从Acrobat[调用MyApplication/EncryptDocument进程。)](#rest-invocation-examples)

使用REST请求时，建议您不要直接调用Forms服务。 而是调用在Workbench中创建的进程。 创建用于调用REST的流程时，请使用程序化开始点。 在这种情况下，将自动添加REST端点。 有关在Workbench中创建流程的信息，请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

使用REST调用服务时，系统会提示您输入AEM表单用户名和密码。 但是，如果不想指定用户名和密码，可以禁用服务安全。

要使用REST调用Forms服务（当激活进程时进程将成为服务），请配置REST端点。 （请参阅[管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)中的“管理端点”。）

配置REST端点后，可以使用HTTPGET方法或POST方法调用Forms服务。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必填`ServiceName`值是要调用的Forms服务的名称。 可选`OperationName`值是服务操作的名称。 如果未指定此值，则此名称默认为`invoke`，它是开始进程的操作名称。 可选的`ServiceVersion`值是以X.Y格式编码的版本。 如果未指定此值，则使用最新版本。 `enctype`值也可以是`application/x-www-form-urlencoded`。

## 支持的数据类型{#supported-data-types}

使用REST请求调用AEM Forms服务时，支持以下数据类型：

* Java基元数据类型，如字符串和整数
* `com.adobe.idp.Document` 数据类型
* `org.w3c.Document`和`org.w3c.Element`等XML数据类型
* 集合对象，如`java.util.List`和`java.util.Map`

   这些数据类型通常被接受为在Workbench中创建的流程的输入值。

   如果使用HTTPPOST方法调用Froms服务，则参数将在HTTP请求主体中传递。 如果AEM Forms服务的签名具有字符串输入参数，则请求主体可包含输入参数的文本值。 如果服务的签名定义了多个字符串参数，则请求可以按照HTTP的`application/x-www-form-urlencoded`记号，使用参数的名称作为表单的字段名称。

   如果Forms服务返回字符串参数，则结果是输出参数的文本表示。 如果服务返回多个字符串参数，则结果是以下格式对输出参数进行编码的XML文档:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1`值表示输出参数名称。

   如果Forms服务需要`com.adobe.idp.Document`参数，则只能使用HTTPPOST方法调用该服务。 如果服务需要一个`com.adobe.idp.Document`参数，则HTTP请求主体将成为输入文档对象的内容。

   如果AEM Forms服务需要多个输入参数，则HTTP请求主体必须是RFC 1867定义的多部分MIME消息。 （RFC 1867是Web浏览器用于将文件上传到网站的标准。） 每个输入参数必须作为多部分消息的单独部分发送，并以`multipart/form-data`格式进行编码。 每个部件的名称必须与参数的名称匹配。

   列表和映射还用作在Workbench中创建的AEM Forms进程的输入值。 因此，在使用REST请求时，您可以使用这些数据类型。 不支持Java数组，因为它们不用作AEM Forms进程的输入值。

   如果输入参数是列表,REST客户端可以多次指定该参数(对于列表中的每个项目一次)来发送该参数。 例如，如果A是列表，则输入必须是多部件消息，由多个名为A的部件组成。在这种情况下，每个名为A的部件都成为输入列表中的项。 如果B是字符串的列表，则输入可以是`application/x-www-form-urlencoded`消息，包含多个名为B的字段。在这种情况下，每个名为B的表单字段都成为输入列表中的一个项。

   如果输入参数是映射，而它是仅服务的输入参数，则输入消息的每个部分／字段将成为映射中的键／值记录。 每个部件／字段的名称成为记录的键。 每个部件／字段的内容将成为记录的值。

   如果输入映射不是仅服务的输入参数，则可以使用名为参数名称和记录密钥的级联的参数发送属于该映射的每个键／值记录。 例如，可以使用以下键／值对的列表发送名为`attributes`的输入映射：

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   这相当于一张三条记录的地图：`Color=red`、`Shape=box`和`Width=5`。

   列表和映射类型的输出参数成为生成XML消息的一部分。 输出列表以XML形式表示为一系列XML元素，该列表中的每个项都有一个元素。 每个元素的名称与输出列表参数相同。 每个XML元素的值是两件事之一：

* 列表中项的文本表示形式(如果列表包含字符串类型)
* 指向文档内容的URL(如果列表由`com.adobe.idp.Document`对象组成)

   以下示例是服务返回的XML消息，该服务具有名为&#x200B;*列表*的单个输出参数，该参数是整数的列表。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`输出映射参数在生成的XML消息中表示为一系列XML元素，其中每个记录对应一个元素。每个元素的名称都与映射记录的键相同。 每个元素的值是映射记录值的文本表示形式（如果映射包含带有字符串值的记录）或指向文档内容的URL（如果映射包含具有`com.adobe.idp.Document`值的记录）。 以下是服务返回的XML消息示例，该服务具有名为`map`的单个输出参数。 此参数值是一个由将字母与`com.adobe.idp.Document`对象关联的记录组成的映射。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 异步调用{#asynchronous-invocations}

一些AEM Forms服务，如以人为中心的长寿命服务，需要很长的时间才能完成。 可以以非阻塞方式异步调用这些服务。 （请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

通过在调用URL中用`async_invoke`替换`services`，可以异步调用AEM Forms服务，如下例所示。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

此URL返回负责此调用的作业的标识符值（以“文本／纯”格式）。

通过使用用`async_status`替换的`services`调用URL，可以检索异步调用的状态。 URL必须包含一个`job_id`参数，该参数指定与此调用关联的作业的标识符值。 例如：

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

此URL返回一个整数值（以“文本／纯”格式），根据作业管理器的规范对作业状态进行编码（例如，2表示运行，3表示已完成，4表示失败，依此类推）。

如果作业完成，URL返回的结果与同步调用服务时的结果相同。

完成作业并检索结果后，使用`services`的调用URL替换`async_dispose`即可处理作业。 该URL还应包含一个`job_id`参数，它指定作业的标识符值。 例如：

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

如果作业被成功丢弃，则此URL返回一条空消息。

## 错误报告{#error-reporting}

如果由于服务器上引发异常而无法完成同步或异步调用请求，则该异常将作为HTTP响应消息的一部分报告。 如果调用URL（或异步调用时的`async_result` URL）没有。xml后缀，则REST提供程序将返回HTTP代码`500 Internal Server Error`，后跟异常消息。

如果调用URL（或异步调用时的`async_result` URL）确实有。xml后缀，则REST提供程序将返回HTTP代码`200 OK`，后跟以下格式描述异常的XML文档。

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

`DSCError`元素是可选的，仅当异常为`com.adobe.idp.dsc.DSCException`的实例时才显示。

## 安全性和身份验证{#security-and-authentication}

要为REST调用提供安全传输，AEM表单管理员可以在承载AEM Forms的J2EE应用程序服务器上启用HTTPS协议。 此配置特定于J2EE应用程序服务器；它不是表单服务器配置的一部分。

>[!NOTE]
>
>作为希望通过REST端点展示您的流程的Workbench开发人员，请牢记XSS漏洞问题。 XSS漏洞可用于窃取或操作Cookie、修改内容演示以及泄露机密信息。 如果存在XSS漏洞，建议使用附加的输入和输出数据验证规则扩展流程逻辑。

## 支持REST调用的AEM Forms服务{#aem-forms-services-that-support-rest-invocation}

尽管建议您调用使用Workbench创建的进程而不是直接调用服务，但有一些AEM Forms服务确实支持REST调用。 建议您直接调用进程而不是直接调用服务的原因在于调用进程更加有效。 请考虑以下情况。 假定您要从REST客户端创建策略。 即，您希望REST客户端定义策略名称、脱机租用期等值。

要创建策略，必须定义复杂的数据类型，如`PolicyEntry`对象。 `PolicyEntry`对象定义与策略关联的属性，如权限。 （请参阅[创建策略](/help/forms/developing/protecting-documents-policies.md#creating-policies)。）

请不要发送REST请求以创建策略（包括定义复杂数据类型，如`PolicyEntry`对象），而是创建一个使用Workbench创建策略的进程。 定义流程以接受基本输入变量，如定义流程名称的字符串值或定义脱机租用期的整数。

这样，您就不必创建包含操作所需的复杂数据类型的REST调用请求。 该进程定义复杂的数据类型，您从REST客户端执行的所有操作都是调用该进程并传递基本数据类型。 有关使用REST调用进程的信息，请参阅[使用REST](#rest-invocation-examples)调用MyApplication/EncryptDocument进程。

以下列表指定了支持直接调用REST的AEM Forms服务。

* Distiller服务
* Rights Management服务
* GeneratePDF服务
* Generate3dPDF服务
* FormDataIntegration

## REST调用示例{#rest-invocation-examples}

提供了以下REST调用示例：

* 将布尔值传递给AEM Forms进程
* 将日期值传递给AEM Forms进程
* 将文档传递给AEM Forms进程
* 将文档和文本值传递给AEM Forms进程
* 将明细列表值传递给AEM Forms进程
* 使用REST调用MyApplication/EncryptDocument进程
* 从Acrobat调用MyApplication/EncryptDocument进程

   每个示例演示如何将不同的数据类型传递到AEM Forms进程

**将布尔值传递给进程**

以下HTML示例将两个`Boolean`值传递给名为`RestTest2`的AEM Forms进程。 调用方法的名称为`invoke`，版本为1.0。请注意，使用了HTML Post方法。

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

**将日期值传递到流程**

以下HTML示例将日期值传递给名为`SOAPEchoService`的AEM Forms进程。 调用方法的名称为`echoCalendar`。 请注意，使用了HTML `Post`方法。

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

以下HTML示例调用名为`MyApplication/EncryptDocument`的AEM Forms进程，该进程需要PDF文档。 有关此过程的信息，请参见[使用MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)调用AEM Forms。

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

以下HTML示例调用名为`RestTest3`的AEM Forms进程，该进程需要一个文档和两个文本值。 请注意，已使用HTML Post方法。

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

**将明细列表值传递给进程**

以下HTML示例调用一个名为`SOAPEchoService`的AEM Forms进程，该进程需要一个明细列表值。 请注意，已使用HTML Post方法。

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

可以使用REST调用名为&#x200B;*MyApplication/EncryptDocument*&#x200B;的AEM Forms短期进程。

>[!NOTE]
>
>这一进程不是基于AEM Forms现有进程。 要跟随代码示例，请使用Workbench创建一个名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于`SetValue`操作。 此进程的输入参数是名为`inDoc`的`document`进程变量。
1. 用密码加密PDF文档。 此操作基于`PasswordEncryptPDF`操作。 在名为`outDoc`的进程变量中返回密码加密的PDF文档。

   当使用REST请求调用此过程时，加密的PDF文档会显示在Web浏览器中。 在视图PDF文档之前，您需要指定密码（除非禁用安全性）。 以下HTML代码表示对`MyApplication/EncryptDocument`进程的REST调用请求。

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

您可以使用REST请求从Acrobat调用Forms进程。 例如，可以调用&#x200B;*MyApplication/EncryptDocument*&#x200B;进程。 要从Acrobat调用Forms进程，请在Designer中的XDP文件上放置一个提交按钮。 （请参阅[设计器帮助](https://www.adobe.com/go/learn_aemforms_designer_63)。）

在按钮的&#x200B;*“提交到URL*”字段中指定要调用进程的URL，如下图所示。

调用该过程的完整URL为https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument。

如果该过程需要PDF文档作为输入值，请确保您以PDF形式提交表单，如上图所示。 此外，要成功调用进程，该进程必须返回PDF文档。 否则，Acrobat无法处理返回值，并且出现错误。 您不必指定输入进程变量的名称。 例如，*MyApplication/EncryptDocument*&#x200B;进程具有一个名为`inDoc`的输入变量。 只要表单提交为PDF，就不必指定inDoc。

您还可以将表单数据作为XML提交到Forms进程。要提交XML数据，请确保`Submit As`下拉列表指定了XML。 由于流程的返回值必须是PDF文档，因此PDF文档显示在Acrobat。
