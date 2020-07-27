---
title: 计算表单数据
seo-title: 计算表单数据
description: 'null'
seo-description: 'null'
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 0%

---


# 计算表单数据 {#calculating-form-data}

Forms服务可以计算用户在表单中输入的值并显示结果。 要计算表单数据，您必须执行两个任务。 首先，创建一个计算表单数据的表单设计脚本。 表单设计支持三种类型的脚本。 一种脚本类型在客户端上运行，另一种脚本类型在服务器上运行，第三种类型在服务器和客户端上运行。 本主题中讨论的脚本类型在服务器上运行。 HTML、PDF和表单指南（已弃用）转换支持服务器端计算。

在表单设计过程中，您可以利用计算和脚本来提供更丰富的用户体验。 计算和脚本可以添加到大多数表单字段和对象。 必须创建表单设计脚本，以对用户输入到交互式表单的数据执行计算操作。

用户在表单中输入值并单击“计算”按钮以视图结果。 以下过程描述了一个允许用户计算数据的示例应用程序：

* 用户访问名为StartLoan.html的HTML页面，充当Web应用程序的开始页。 此页调用名为的Java Servlet `GetLoanForm`。
* Servlet `GetLoanForm` 可呈现贷款表单。 此表单包含脚本、交互字段、计算按钮和提交按钮。
* 用户在表单的字段中输入值，然后单击“计算”按钮。 表单将发送到执 `CalculateData` 行脚本的Java Servlet。 表单将返回给用户，计算结果将显示在表单中。
* 用户继续输入和计算值，直到显示满意的结果。 满意后，用户单击“提交”按钮以处理表单。 表单将发送到另一个名为Java Servlet `ProcessForm` 的表单，该Java Servlet负责检索提交的数据。 (请参阅 [处理提交的表](/help/forms/developing/rendering-forms.md#handling-submitted-forms)单。)


下图显示了应用程序的逻辑流。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

下表介绍了此图中的步骤。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>从 <code>GetLoanForm</code> HTML开始页调用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java <code>GetLoanForm</code> Servlet使用Forms服务客户端API向客户端Web浏览器呈现贷款表单。 呈现包含配置为在服务器上运行的脚本的表单与呈现不包含脚本的表单之间的区别在于，您必须指定用于执行脚本的目标位置。 如果未指定目标位置，则不执行配置为在服务器上运行的脚本。 例如，请考虑本节介绍的应用程序。 Java <code>CalculateData</code> Servlet是执行脚本的目标位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户将数据输入到交互字段中并单击“计算”按钮。 表单将发送到执 <code>CalculateData</code> 行脚本的Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表单将呈现回Web浏览器，并且计算结果显示在表单中。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>当值满意时，用户单击“提交”按钮。 表单将发送到另一个名为的Java Servlet <code>ProcessForm</code>。</p></td>
  </tr>
 </tbody>
</table>

通常，作为PDF内容提交的表单包含在客户端上执行的脚本。 但是，也可以执行服务器端计算。 “提交”按钮不能用于计算脚本。 在这种情况下，不执行计算，因为Forms服务认为交互是完成的。

为了说明表单设计脚本的用法，本节将检查一个简单的交互式表单，该表单包含一个配置为在服务器上运行的脚本。 下图显示了一个包含脚本的表单设计，该脚本将用户输入到前两个字段中的值相加，并在第三个字段中显示结果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A** .名为NumericField1的 **字段B.** 名为NumericField2的 **字段C.** A名为NumericField3的字段

此表单设计中的脚本语法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此表单设计中，“计算”按钮是一个命令按钮，脚本位于此按钮的 `Click` 事件。 当用户在前两个字段（NumericField1和NumericField2）中输入值并单击“计算”按钮时，表单将发送到执行脚本的Forms服务。 Forms服务将表单呈现回客户端设备，计算结果显示在NumericField3字段中。

>[!NOTE]
>
>有关创建表单设计脚本的信息，请参 [阅表单设计器](https://www.adobe.com/go/learn_aemforms_designer_63)。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要计算表单任务，请执行以下操作：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 检索包含计算脚本的表单。
1. 将表单数据流写回客户端Web浏览器

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms服务客户端。 如果您使用Java API，请创建一个 `FormsServiceClient` 对象。 如果您使用Forms Web服务API，请创建一个 `FormsServiceService` 对象。

**检索包含计算脚本的表单**

使用Forms服务客户端API创建应用程序逻辑，该逻辑处理包含配置为在服务器上运行的脚本的表单。 该过程类似于处理提交的表单。 (请参阅 [处理提交的表](/help/forms/developing/handling-submitted-forms.md)单。)

验证与提交的表单关联的处理状 `1` 态是否 `(Calculate)`为，这意味着表单服务正在对表单数据执行计算操作，并且结果必须写回给用户。 在这种情况下，将自动执行配置为在服务器上运行的脚本。

**将表单数据流写回客户端Web浏览器**

验证与提交的表单关联的处理状态 `1`后，必须将结果写回客户端Web浏览器。 显示表单时，计算值将显示在相应的字段中。

**另请参阅**

[包括AEM Forms库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[使用Java API计算表单数据使用Web服务API](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)Api设置连接属性[](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)[](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)[](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)[](/help/forms/developing/rendering-interactive-pdf-forms.md)[Web服务API Service API Signs PropertiesFormsQuickJava Rendering Interactive Adrictive Interactive 开始，创建创建创建PDF forms的Java表单的交互式Web 应用程序的Java表单的RapSASSSp APIAASSSASSASSSSPAASSSSSASSSSSASSSSSSSSSASSASASSASASSASSS PRES](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API计算表单数据 {#calculate-form-data-using-the-java-api}

使用Forms API(Java)计算表单数据：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索包含计算脚本的表单

   * 要检索包含计算脚本的表单数据，请使 `com.adobe.idp.Document` 用对象的构造函数并从构造函数中调 `javax.servlet.http.HttpServletResponse` 用对象 `getInputStream` 的方法来创建对象。
   * 调用对 `FormsServiceClient` 象的方 `processFormSubmission` 法并传递以下值：

      * 包 `com.adobe.idp.Document` 含表单数据的对象。
      * 一个字符串值，它指定包括所有相关HTTP头的环境变量。 必须通过为环境变量指定一个或多个值来指定要处理的内容 `CONTENT_TYPE` 类型。 例如，要处理XML和PDF数据，请为此参数指定以下字符串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 一个字符串值，它指定 `HTTP_USER_AGENT` 标题值； 例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`,
      * 存 `RenderOptionsSpec` 储运行时选项的对象。

      该方 `processFormSubmission` 法返回 `FormsResult` 包含表单提交结果的对象。

   * 通过调用对象的方法验证与已提交表单 `1` 关联的处 `FormsResult` 理状态是否 `getAction` 为。 如果此方法返回该 `1`值，则执行计算并将数据写回客户端Web浏览器。


1. 将表单数据流写回客户端Web浏览器

   * 创建用 `javax.servlet.ServletOutputStream` 于将表单数据流发送到客户端Web浏览器的对象。
   * 通过 `com.adobe.idp.Document` 调用对象的 `FormsResult` 方法创建 `getOutputContent` 对象。
   * 通过 `java.io.InputStream` 调用对象的 `com.adobe.idp.Document` 方法创建 `getInputStream` 对象。
   * 通过调用对象的方法并将字节数组作为参数进行传递，创 `InputStream` 建一个字 `read` 节数组并用表单数据流填充它。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给 `write` 方法。

**另请参阅**


[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API计算表单数据 {#calculate-form-data-using-the-web-service-api}

使用Forms API（Web服务）计算表单数据：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 检索包含计算脚本的表单

   * 要检索发布到Java Servlet的表单数据，请使用其构 `BLOB` 造函数创建一个对象。
   * 使用 `java.io.InputStream` 对象的方法 `javax.servlet.http.HttpServletResponse` 创建对 `getInputStream` 象。
   * 通过使用 `java.io.ByteArrayOutputStream` 对象的构造函数并传递对象的长度来创建 `java.io.InputStream` 对象。
   * 将对象的内 `java.io.InputStream` 容复制到对 `java.io.ByteArrayOutputStream` 象中。
   * 通过调用对象的方法 `java.io.ByteArrayOutputStream` 创建字节 `toByteArray` 数组。
   * 通过调 `BLOB` 用对象的方 `setBinaryData` 法并将字节数组作为参数进行传递来填充对象。
   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。 通过调用对象的方法并 `RenderOptionsSpec` 传递指定 `setLocale` 区域设置值的字符串值来设置区域设置值。
   * 调用对 `FormsServiceClient` 象的方 `processFormSubmission` 法并传递以下值：

      * 包 `BLOB` 含表单数据的对象。
      * 一个字符串值，它指定环境变量包括所有相关的HTTP头。 例如，可以指定以下字符串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 一个字符串值，它指定 `HTTP_USER_AGENT` 标题值； 例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`,
      * 存 `RenderOptionsSpec` 储运行时选项的对象。 有关详细信息，请访问。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `BLOBHolder` 法填充的空对象。
      * 由方 `javax.xml.rpc.holders.ShortHolder` 法填充的空对象。
      * 由方 `MyArrayOf_xsd_anyTypeHolder` 法填充的空对象。 此参数用于存储随表单一起提交的文件附件。
      * 由方 `FormsResultHolder` 法填充的空对象，其中包含提交的表单。

      该方 `processFormSubmission` 法使用 `FormsResultHolder` 表单提交的结果填充参数。 该方 `processFormSubmission` 法返回 `FormsResult` 包含表单提交结果的对象。

   * 通过调用对象的方法验证与已提交表单 `1` 关联的处 `FormsResult` 理状态是否 `getAction` 为。 如果此方法返回该 `1`值，则执行计算并将数据写回客户端Web浏览器。


1. 将表单数据流写回客户端Web浏览器

   * 创建用 `javax.servlet.ServletOutputStream` 于将表单数据流发送到客户端Web浏览器的对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的 `getOutputContent` 对象。
   * 创建一个字节数组，并通过调用对 `BLOB` 象的方法来填 `getBinaryData` 充它。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给 `write` 方法。

**另请参阅**[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
