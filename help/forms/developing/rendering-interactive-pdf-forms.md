---
title: 渲染交互式PDF forms
seo-title: 渲染交互式PDF forms
description: 使用Forms服务向客户端设备（通常是Web浏览器）呈现交互式PDF forms，以从用户处收集信息。 您可以使用Forms服务使用Java API和Web服务API渲染交互式表单。
seo-description: 使用Forms服务向客户端设备（通常是Web浏览器）呈现交互式PDF forms，以从用户处收集信息。 您可以使用Forms服务使用Java API和Web服务API渲染交互式表单。
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---


# 渲染交互式PDF forms{#rendering-interactive-pdf-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

Forms服务将交互式PDF forms呈现到客户端设备（通常是Web浏览器），以从用户收集信息。 呈现交互式表单后，用户可以将数据输入到表单字段中，然后单击表单上的提交按钮以将信息发送回Forms服务。 Adobe Reader或Acrobat必须安装在承载客户端Web浏览器的计算机上，才能显示交互式PDF表单。

>[!NOTE]
>
>在使用Forms服务渲染表单之前，请先创建表单设计。 通常，表单设计在Designer中创建并保存为XDP文件。 有关创建表单设计的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

**贷款申请示例**

引入了一个贷款应用程序示例，用于演示Forms服务如何使用交互式表单从用户处收集信息。 此应用程序允许用户用确保贷款安全所需的数据填写表单，然后向Forms服务提交数据。 下图显示了贷款应用程序的逻辑流。

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
   <td><p>从HTML页调用<code>GetLoanForm</code> Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java Servlet使用Forms服务客户端API向客户端Web浏览器呈现贷款表。 （请参阅<a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API</a>渲染交互式PDF表单。）</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>用户填写贷款表单并单击提交按钮后，数据将提交到<code>HandleData</code> Java Servlet。 （请参阅<i>"贷款表"</i>。）</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p><code>HandleData</code> Java Servlet使用Forms服务客户端API处理表单提交和检索表单数据。 然后，数据存储在企业数据库中。 (请参阅<a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">处理已提交的Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>确认表单将呈现回Web浏览器。 呈现表单之前，会将用户的名和姓等数据与表单合并。 (请参阅<a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流式布局预填充Forms</a>。)</p></td>
  </tr>
 </tbody>
</table>

**贷款表**

此交互式贷款表由示例贷款应用程序的`GetLoanForm` Java Servlet呈现。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**确认表单**

此表单由示例贷款应用程序的`HandleData` Java Servlet呈现。

![ri_ri_confirm](assets/ri_ri_confirm.png)

`HandleData` Java Servlet使用用户的名和姓以及amount预填充此表单。 预填充表单后，表单将发送到客户端Web浏览器。 (请参阅[使用可流式布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

示例贷款应用程序是作为Java Servlet存在的Forms服务应用程序的示例。 Java Servlet是在J2EE项目服务器（如WebSphere）上运行的Java应用程序，包含Forms服务客户端API代码。

以下代码显示名为GetLoanForm的Java Servlet的语法：

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常，您不会将Forms服务客户端API代码放在Java Servlet的`doGet`或`doPost`方法中。 最好将此代码放在单独的类中，从`doPost`方法（或`doGet`方法）实例化该类，并调用相应的方法。 但是，对于代码简单性，本节中的代码示例将保持为最小值，并且代码示例将放在`doPost`方法中。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)的服务参考。

**步骤摘要**

要渲染交互式PDF表单，请执行以下任务:

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 指定URI值。
1. 将文件附加到表单（可选）。
1. 渲染交互式PDF表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms客户端API对象。 如果您使用Java API，请创建`FormsServiceClient`对象。 如果您使用Forms Web服务API，请创建`FormsService`对象。

**指定URI值**

您可以指定Forms服务渲染表单所需的URI值。 使用内容根URI值`repository:///`可以引用作为Forms应用程序一部分保存的表单设计。 例如，请考虑以下名为&#x200B;*Loan.xdp*&#x200B;的表单设计，该表单设计位于名为&#x200B;*FormsApplication*&#x200B;的Forms应用程序中：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

要访问此表单设计，请指定`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`作为表单名称（传递给`renderPDFForm`方法的第一个参数），指定`repository:///`作为内容根URI值。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅[Workbench帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位于Forms应用程序中的资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值显示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

在渲染交互式表单时，您可以定义URI值，如发布表单数据的目标URL。 目标URL可通过以下方式之一进行定义：

* 在设计器中设计表单设计时的“提交”按钮
* 通过使用Forms服务客户端API

如果表单设计中定义了目标URL，请勿使用Forms服务客户端API覆盖它。 即，使用Forms API设置目标URL会将表单设计中指定的URL重置为使用API指定的URL。 如果您希望将PDF表单提交到在表单设计中指定的目标URL，请以编程方式将目标URL设置为空字符串。

如果您的表单包含提交按钮和计算按钮（带有在服务器上运行的相应脚本），则可以通过编程方式定义将表单发送到的URL以执行脚本。 使用表单设计上的提交按钮指定将表单数据发布到的URL。 （请参阅[计算表单数据](/help/forms/developing/calculating-form-data.md)。）

>[!NOTE]
>
>您还可以将`com.adobe.idp.Document`实例传递给Forms服务，而不是指定URL值以引用XDP文件。 `com.adobe.idp.Document`实例包含表单设计。 (请参阅[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)。)

**将文件附加到表单**

您可以将文件附加到表单。 当您渲染带有文件附件的PDF表单时，用户可以使用文件附件窗格在Acrobat中检索文件附件。 可以将不同文件类型附加到表单（如文本文件）或二进制文件（如JPG文件）。

>[!NOTE]
>
>将文件附件附加到表单是可选的。

**渲染交互式PDF表单**

要渲染表单，请使用在Designer中创建并另存为XDP或PDF文件的表单设计。 此外，您还可以渲染使用Acrobat创建并另存为PDF文件的表单。 要渲染交互式PDF表单，请调用`FormsServiceClient`对象的`renderPDFForm`方法或`renderPDFForm2`方法。

`renderPDFForm`使用`URLSpec`对象。 XDP文件的内容根将使用`URLSpec`对象的`setContentRootURI`方法传递到Forms服务。 表单设计名称(`formQuery`)将作为单独的参数值传递。 将这两个值连接起来，以获得对表单设计的绝对引用。

`renderPDFForm2`方法接受一个`com.adobe.idp.Document`实例，该实例包含要渲染的XDP或PDF文档。

>[!NOTE]
>
>如果输入文档是PDF文档，则无法设置加标签的PDF运行时选项。 如果输入文件是XDP文件，则可以设置加标签的PDF选项。

## 使用Java API {#render-an-interactive-pdf-form-using-the-java-api}渲染交互式PDF表单

使用Forms API(Java)渲染交互式PDF表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 指定URI值

   * 创建一个`URLSpec`对象，该对象使用其构造函数存储URI值。
   * 调用`URLSpec`对象的`setApplicationWebRoot`方法并传递一个字符串值，该值表示应用程序的Web根目录。
   * 调用`URLSpec`对象的`setContentRootURI`方法并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定`repository:///`。
   * 调用`URLSpec`对象的`setTargetURL`方法并传递一个字符串值，该字符串值指定将表单目标发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 将文件附加到表单

   * 使用`java.util.HashMap`的构造函数创建一个用于存储文件附件的对象。
   * 为要附加到渲染的表单的每个文件调用`java.util.HashMap`对象的`put`方法。 将以下值传递给此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名。
   * 包含文件附件的`com.adobe.idp.Document`对象。

   >[!NOTE]
   >
   >对要附加到表单的每个文件重复此步骤。 此步骤是可选的，如果您不想发送文件附件，可以传递`null`。

1. 渲染交互式PDF表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递空`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是可选参数，如果不想指定运行时选项，可以指定`null`。
   * `URLSpec`对象，其中包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象&#39;s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建一个字节数组并将其填充为表单数据流。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

## 使用Web服务API {#render-an-interactive-pdf-form-using-the-web-service-api}渲染交互式PDF表单

使用Forms API（Web服务）渲染交互式PDF表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建`FormsService`对象并设置身份验证值。

1. 指定URI值

   * 创建一个`URLSpec`对象，该对象使用其构造函数存储URI值。
   * 调用`URLSpec`对象的`setApplicationWebRoot`方法并传递一个字符串值，该值表示应用程序的Web根目录。
   * 调用`URLSpec`对象的`setContentRootURI`方法并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定`repository:///`。
   * 调用`URLSpec`对象的`setTargetURL`方法并传递一个字符串值，该字符串值指定将表单目标发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 将文件附加到表单

   * 使用`java.util.HashMap`的构造函数创建一个用于存储文件附件的对象。
   * 为要附加到渲染的表单的每个文件调用`java.util.HashMap`对象的`put`方法。 将以下值传递给此方法：

      * 一个字符串值，它指定文件附件的名称，包括文件扩展名
   * 包含文件附件的`BLOB`对象

   >[!NOTE]
   >
   >对要附加到表单的每个文件重复此步骤。

1. 渲染交互式PDF表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是可选参数，如果不想指定运行时选项，可以指定`null`。
   * `URLSpec`对象，其中包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 用于存储渲染后的PDF表单。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数将存储表单中的页数。）
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数将存储区域设置值。）
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建一个包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现表单时，它返回一个必须写入客户端Web浏览器的表单数据流。 写入到客户端Web浏览器时，用户可以看到表单。
