---
title: 渲染交互式PDF表单
seo-title: 渲染交互式PDF表单
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 渲染交互式PDF表单 {#rendering-interactive-pdf-forms}

Forms服务将交互式PDF表单呈现到客户端设备（通常是Web浏览器），以收集用户的信息。 呈现交互式表单后，用户可以将数据输入到表单字段中，然后单击表单上的提交按钮以将信息发送回表单服务。 必须在承载客户端Web浏览器的计算机上安装Adobe Reader或Acrobat，才能显示交互式PDF表单。

>[!NOTE]
>
>在使用Forms服务渲染表单之前，请先创建表单设计。 通常，表单设计在Designer中创建并另存为XDP文件。 有关创建表单设计的信息，请参阅 [表单设计器](https://www.adobe.com/go/learn_aemforms_designer_63)。

**贷款申请范例**

引入了一个贷款申请示例，以演示Forms服务如何使用交互式表单从用户处收集信息。 此应用程序允许用户填写表格，其中包含确保贷款安全所需的数据，然后向表单服务提交数据。 下图显示了贷款应用程序的逻辑流程。

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
   <td><p>从 <code>GetLoanForm</code> HTML页面调用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Java <code>GetLoanForm</code> Servlet使用Forms服务客户端API向客户端Web浏览器呈现贷款表单。 (请参 <a href="#render-an-interactive-pdf-form-using-the-java-api">阅使用Java API渲染交互式PDF表单</a>。)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户填写贷款表单并单击提交按钮后，数据将提交到 <code>HandleData</code> Java Servlet。 (请参 <i>阅“贷款表”</i>。)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Java <code>HandleData</code> Servlet使用Forms服务客户端API处理表单提交和检索表单数据。 然后，数据被存储在企业数据库中。 (请参阅 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">处理提交的表单</a>。)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>确认表单会呈现回Web浏览器。 呈现表单之前，用户的名字和姓氏等数据会与表单合并。 (请参阅 <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流式布局预填充表单</a>。)</p></td>
  </tr>
 </tbody>
</table>

**贷款表**

此交互式贷款表由示例贷款应用程序的 `GetLoanForm` Java servlet呈现。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**确认表单**

此表由示例贷款应用程序的 `HandleData` Java servlet呈现。

![ri_ri_confirm](assets/ri_ri_confirm.png)

Java `HandleData` Servlet预填充此表单时使用用户的名和姓以及金额。 在预填充表单后，表单将发送到客户端Web浏览器。 (请参阅 [使用可流式布局预填充表单](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlets**

示例贷款应用程序是作为Java servlet存在的Forms服务应用程序的示例。 Java Servlet是在J2EE应用程序服务器（如WebSphere）上运行的Java程序，它包含Forms服务客户端API代码。

以下代码显示名为GetLoanForm的Java Servlet的语法：

```as3
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常，您不会将Forms服务客户端API代码放入Java servlet或 `doGet` 方法 `doPost` 中。 最好将此代码放在单独的类中，从方法（或方法）中实例化 `doPost` 该类，并调用相 `doGet` 应的方法。 但是，对于代码简单性，本节中的代码示例将保持为最小值，并且代码示例将放在方法中 `doPost` 。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

**步骤摘要**

要渲染交互式PDF表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 指定URI值。
1. 将文件附加到表单（可选）。
1. 渲染交互式PDF表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须先创建Forms客户端API对象。 如果您使用Java API，请创建一个对 `FormsServiceClient` 象。 如果您使用的是Forms web服务API，请创建一个对 `FormsService` 象。

**指定URI值**

您可以指定Forms服务渲染表单所需的URI值。 保存为Forms应用程序一部分的表单设计可以使用内容根URI值进行引用 `repository:///`。 例如，请考虑位于名为 *FormsApplication的Forms应用程序中的名为* Loan.xdp *的以下表单*&#x200B;设计：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

要访问此表单设计，请 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` 指定为表单名称（传递给方法的第一个参数） `renderPDFForm` 和 `repository:///` 内容根URI值。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅 [Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位于Forms应用程序中的资源的路径是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

在渲染交互式表单时，可以定义URI值，如发布表单数据的目标URL。 目标URL可通过以下方式之一进行定义：

* 在Designer中设计表单时在“提交”按钮上
* 使用Forms服务客户端API

如果在表单设计中定义了目标URL，请勿使用Forms服务客户端API覆盖它。 即，使用Forms API设置目标URL会将表单设计中指定的URL重置为使用API指定的URL。 如果要将PDF表单提交到在表单设计中指定的目标URL，请以编程方式将目标URL设置为空字符串。

如果您的表单包含提交按钮和计算按钮（具有在服务器上运行的相应脚本），则可以通过编程方式定义表单要执行脚本的URL。 使用表单设计上的提交按钮指定发布表单数据的URL。 (请参阅 [计算表单数据](/help/forms/developing/calculating-form-data.md)。)

>[!NOTE]
>
>除了指定URL值以引用XDP文件，您还可以将实例传 `com.adobe.idp.Document` 递给Forms服务。 该实 `com.adobe.idp.Document` 例包含表单设计。 (请参 [阅将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)。)

**将文件附加到表单**

可以将文件附加到表单。 当您渲染带有文件附件的PDF表单时，用户可以使用文件附件窗格在Acrobat中检索文件附件。 您可以将不同的文件类型附加到表单（如文本文件）或二进制文件（如JPG文件）。

>[!NOTE]
>
>将文件附件附加到表单是可选的。

**渲染交互式PDF表单**

要渲染表单，请使用在Designer中创建并另存为XDP或PDF文件的表单设计。 此外，您还可以渲染使用Acrobat创建并另存为PDF文件的表单。 要渲染交互式PDF表单，请调用 `FormsServiceClient` 对象的方 `renderPDFForm` 法或方 `renderPDFForm2` 法。

它 `renderPDFForm` 使用对 `URLSpec` 象。 XDP文件的内容根将使用对象的方法传递 `URLSpec` 到Forms服 `setContentRootURI` 务。 表单设计名称( `formQuery`)将作为单独的参数值进行传递。 将这两个值连接起来，以获得对表单设计的绝对引用。

该方 `renderPDFForm2` 法接受包 `com.adobe.idp.Document` 含要渲染的XDP或PDF文档的实例。

>[!NOTE]
>
>如果输入文档是PDF文档，则无法设置加标签的PDF运行时选项。 如果输入文件是XDP文件，则可以设置加标签的PDF选项。

## 使用Java API渲染交互式PDF表单 {#render-an-interactive-pdf-form-using-the-java-api}

使用Forms API(Java)渲染交互式PDF表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 指定URI值

   * 使用 `URLSpec` 其构造函数创建存储URI值的对象。
   * 调用对 `URLSpec` 象的方 `setApplicationWebRoot` 法并传递一个表示应用程序Web根目录的字符串值。
   * 调用对 `URLSpec` 象的方 `setContentRootURI` 法并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定 `repository:///`。
   * 调用对 `URLSpec` 象的方 `setTargetURL` 法并传递一个字符串值，该字符串值指定将表单数据发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 将文件附加到表单

   * 使用 `java.util.HashMap` 其构造函数创建用于存储文件附件的对象。
   * 调用每 `java.util.HashMap` 个文件的 `put` 对象方法，以附加到呈现的表单。 将以下值传递给此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名。
   * 包 `com.adobe.idp.Document` 含文件附件的对象。
   >[!NOTE]
   >
   >对要附加到表单的每个文件重复此步骤。 此步骤是可选的，如果您不 `null` 想发送文件附件，则可以通过此步骤。

1. 渲染交互式PDF表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 这是一个可选参数，您可 `null` 以指定是否不想指定运行时选项。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组，并通过调用对象的方法并将字节数 `InputStream` 组作为参数传 `read` 递，用表单数据流填充它。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

## 使用Web服务API渲染交互式PDF表单 {#render-an-interactive-pdf-form-using-the-web-service-api}

使用Forms API（Web服务）渲染交互式PDF表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 指定URI值

   * 使用 `URLSpec` 其构造函数创建存储URI值的对象。
   * 调用对 `URLSpec` 象的方 `setApplicationWebRoot` 法并传递一个表示应用程序Web根目录的字符串值。
   * 调用对 `URLSpec` 象的方 `setContentRootURI` 法并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定 `repository:///`。
   * 调用对 `URLSpec` 象的方 `setTargetURL` 法并传递一个字符串值，该字符串值指定将表单数据发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 将文件附加到表单

   * 使用 `java.util.HashMap` 其构造函数创建用于存储文件附件的对象。
   * 调用每 `java.util.HashMap` 个文件的 `put` 对象方法，以附加到呈现的表单。 将以下值传递给此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名
   * 包 `BLOB` 含文件附件的对象
   >[!NOTE]
   >
   >对要附加到表单的每个文件重复此步骤。

1. 渲染交互式PDF表单

   调用对 `FormsService` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果您不想合并数据，请传递 `null`。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 这是一个可选参数，您可 `null` 以指定是否不想指定运行时选项。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 它用于存储渲染的PDF表单。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对象。 （此参数将存储表单中的页数。）
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 （此参数将存储区域设置值。）
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `renderPDFForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 当写入到客户端Web浏览器时，用户可看到表单。
