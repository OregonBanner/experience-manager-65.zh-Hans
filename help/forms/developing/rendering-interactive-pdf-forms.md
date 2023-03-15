---
title: 渲染交互式PDF forms
seo-title: Rendering Interactive PDF Forms
description: 使用Forms服务向客户端设备（通常是Web浏览器）呈现交互式PDF forms，以从用户那里收集信息。 您可以使用Forms服务通过Java API和Web服务API呈现交互式表单。
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# 渲染交互式PDF forms {#rendering-interactive-pdf-forms}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

Forms服务向客户端设备（通常是Web浏览器）呈现交互式PDF forms，以从用户那里收集信息。 呈现交互式表单后，用户可以在表单字段中输入数据，然后单击表单上的提交按钮以将信息发送回Forms服务。 必须在托管客户端Web浏览器的计算机上安装Adobe Reader或Acrobat，以便交互式PDF表单可见。

>[!NOTE]
>
>在使用Forms服务呈现表单之前，请先创建表单设计。 通常，窗体设计会在Designer中创建，并保存为XDP文件。 有关创建表单设计的信息，请参阅 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63).

**贷款申请示例**

引入了一个示例贷款应用程序，以演示Forms服务如何使用交互式表单从用户那里收集信息。 通过此应用程序，用户可在表单中填写保护贷款所需的数据，然后将数据提交到Forms服务。 下图显示了贷款申请的逻辑流程。

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>此 <code>GetLoanForm</code> 从HTML页调用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>此 <code>GetLoanForm</code> Java Servlet使用Forms服务客户端API将贷款表单渲染到客户端Web浏览器。 (请参阅 <a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API渲染交互式PDF表单</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户填写贷款表单并单击提交按钮后，数据将提交到 <code>HandleData</code> Java Servlet。 (请参阅 <i>"贷款表"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>此 <code>HandleData</code> Java Servlet使用Forms服务客户端API处理表单提交和检索表单数据。 然后，将数据存储在企业数据库中。 (请参阅 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">处理提交的Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>确认表单将呈现回Web浏览器。 诸如用户名字和姓氏的数据在呈现之前与表单合并。 (请参阅 <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流布局预填充Forms</a>.)</p></td>
  </tr>
 </tbody>
</table>

**贷款表**

此交互式贷款表单由示例贷款申请的 `GetLoanForm` Java Servlet。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**确认表单**

此表格由范例贷款申请的 `HandleData` Java Servlet。

![ri_ri_confirm](assets/ri_ri_confirm.png)

此 `HandleData` Java Servlet会使用用户的名字和姓氏以及数量预填充此表单。 预填充表单后，该表单会被发送到客户端Web浏览器。 (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

示例贷款应用程序是作为Java Servlet存在的Forms服务应用程序示例。 Java Servlet是在J2EE应用程序服务器（如WebSphere）上运行的Java程序，它包含Forms服务客户端API代码。

以下代码显示了名为GetLoanForm的Java Servlet的语法：

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常，您不会将Forms服务客户端API代码放入Java Servlet的 `doGet` 或 `doPost` 方法。 更好的编程做法是将此代码放在单独的类中，从内部实例化类 `doPost` 方法(或 `doGet` 方法)，并调用适当的方法。 但是，为了代码简洁，本节中的代码示例尽量少，代码示例放在 `doPost` 方法。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

**步骤摘要**

要渲染交互式PDF表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 指定URI值。
1. 将文件附加到表单（可选）。
1. 渲染交互式PDF表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式执行Forms服务客户端API操作之前，您必须创建Forms客户端API对象。 如果您使用的是Java API，请创建 `FormsServiceClient` 对象。 如果您使用的是Forms Web服务API，请创建 `FormsService` 对象。

**指定URI值**

您可以指定Forms服务渲染表单所需的URI值。 可以使用内容根URI值引用另存为Forms应用程序一部分的表单设计 `repository:///`. 例如，考虑以下名为的表单设计 *Loan.xdp* 位于名为的Forms应用程序中 *表单应用程序*：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

要访问此表单设计，请指定 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` 作为表单名称(传递给 `renderPDFForm` 方法)和 `repository:///` 作为内容根URI值。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅 [Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63).

位于Forms应用程序中的资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示了一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

渲染交互式表单时，您可以定义URI值，例如将表单数据发布到的目标URL。 可通过以下方式之一定义目标URL：

* 在Designer中设计表单设计时显示提交按钮
* 通过使用Forms服务客户端API

如果在表单设计内定义了目标URL，请勿使用Forms服务客户端API覆盖它。 也就是说，使用Forms API设置目标URL会将表单设计中的指定URL重置为使用API指定的URL。 如果要将PDF表单提交到表单设计中指定的目标URL，则以编程方式将目标URL设置为空字符串。

如果您的表单包含提交按钮和计算按钮（具有在服务器上运行的相应脚本），则可以通过编程方式定义将表单发送到哪个URL以执行脚本。 使用表单设计上的提交按钮指定将表单数据发布到的URL。 (请参阅 [计算表单数据](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>您还可以传递URL值来引用XDP文件，而不是指定 `com.adobe.idp.Document` 实例添加到Forms服务。 此 `com.adobe.idp.Document` 实例包含窗体设计。 (请参阅 [将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md).)

**将文件附加到表单**

您可以将文件附加到表单。 渲染带有文件附件的PDF表单时，用户可以使用文件附件窗格在Acrobat中检索文件附件。 您可以将不同的文件类型附加到表单（如文本文件）或二进制文件(如JPG文件)。

>[!NOTE]
>
>将文件附件附加到表单是可选的。

**渲染交互式PDF表单**

要呈现表单，请使用在Designer中创建并另存为XDP或PDF文件的表单设计。 此外，您还可以呈现使用Acrobat创建并另存为PDF文件的表单。 要渲染交互式PDF表单，请调用 `FormsServiceClient` 对象的 `renderPDFForm` 方法或 `renderPDFForm2` 方法。

此 `renderPDFForm` 使用 `URLSpec` 对象。 Forms XDP文件的内容根目录通过使用 `URLSpec` 对象的 `setContentRootURI` 方法。 窗体设计名称( `formQuery`)作为单独的参数值传递。 将这两个值连接起来以获得对窗体设计的绝对引用。

此 `renderPDFForm2` 方法接受 `com.adobe.idp.Document` 包含要渲染的XDP或PDF文档的实例。

>[!NOTE]
>
>如果输入文档是PDF文档，则无法设置标记的PDF运行时选项。 如果输入文件是XDP文件，则可以设置标记的PDF选项。

## 使用Java API渲染交互式PDF表单 {#render-an-interactive-pdf-form-using-the-java-api}

使用Forms API (Java)渲染交互式PDF表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 指定URI值

   * 创建 `URLSpec` 使用其构造函数存储URI值的对象。
   * 调用 `URLSpec` 对象的 `setApplicationWebRoot` 方法，并传递一个表示应用程序的Web根目录的字符串值。
   * 调用 `URLSpec` 对象的 `setContentRootURI` 方法，并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 如果不存在，则Forms服务会引发异常。 要引用存储库，请指定 `repository:///`.
   * 调用 `URLSpec` 对象的 `setTargetURL` 方法，并传递一个字符串值，该值指定将表单数据发布到的目标URL值。 如果您在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL，以执行计算。

1. 将文件附加到表单

   * 创建 `java.util.HashMap` 对象以使用其构造函数存储文件附件。
   * 调用 `java.util.HashMap` 对象的 `put` 每个文件附加到渲染表单的方法。 将以下值传递到此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名。
   * A `com.adobe.idp.Document` 包含文件附件的对象。

   >[!NOTE]
   >
   >对每个要附加到表单的文件重复此步骤。 此步骤是可选的，您可以通过 `null` 如果您不想发送文件附件。

1. 渲染交互式PDF表单

   调用 `FormsServiceClient` 对象的 `renderPDFForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * A `PDFFormRenderSpec` 存储运行时选项的对象。 这是一个可选参数，您可以指定 `null` 如果您不想指定运行时选项。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `renderPDFForm` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，并通过调用 `InputStream` 对象的 `read` 方法，并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

## 使用Web服务API渲染交互式PDF表单 {#render-an-interactive-pdf-form-using-the-web-service-api}

使用Forms API（Web服务）渲染交互式PDF表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 指定URI值

   * 创建 `URLSpec` 使用其构造函数存储URI值的对象。
   * 调用 `URLSpec` 对象的 `setApplicationWebRoot` 方法，并传递一个表示应用程序的Web根目录的字符串值。
   * 调用 `URLSpec` 对象的 `setContentRootURI` 方法，并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 如果不存在，则Forms服务会引发异常。 要引用存储库，请指定 `repository:///`.
   * 调用 `URLSpec` 对象的 `setTargetURL` 方法，并传递一个字符串值，该值指定将表单数据发布到的目标URL值。 如果您在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL，以执行计算。

1. 将文件附加到表单

   * 创建 `java.util.HashMap` 对象以使用其构造函数存储文件附件。
   * 调用 `java.util.HashMap` 对象的 `put` 每个文件附加到渲染表单的方法。 将以下值传递到此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名
   * A `BLOB` 包含文件附件的对象

   >[!NOTE]
   >
   >对每个要附加到表单的文件重复此步骤。

1. 渲染交互式PDF表单

   调用 `FormsService` 对象的 `renderPDFForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`.
   * A `PDFFormRenderSpec` 存储运行时选项的对象。 这是一个可选参数，您可以指定 `null` 如果您不想指定运行时选项。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 用于存储渲染的PDF表单。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的对象。 （此参数将存储表单中的页数。）
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 （此参数将存储区域设置值。）
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值（具有必须写入客户端Web浏览器的表单数据流）传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**将表单数据流写入客户端Web浏览器**

Forms服务渲染表单时，会返回一个您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，该表单对用户可见。
