---
title: 服务容器
description: 服务容器中的AEM Forms服务
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 服务容器 {#service-container}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

服务容器中的AEM Forms服务（包括标准服务，如加密服务、长生命周期和短生命周期进程）可以使用各种提供程序（如EJB提供程序）调用。 通过EJB提供程序，可以通过RMI/IIOP调用AEM Forms服务。 Web服务提供商使用SOAP/HTTP和SOAP/JMS等标准将服务公开为Web服务（WSDL生成）。

下表描述了以编程方式调用AEM Forms服务的各种方式。

<table>
 <thead>
  <tr>
   <th><p>调用方法</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>远程集成</p></td>
   <td><p>远程集成让Flex客户端能够调用服务操作。 (请参阅 <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">使用AEM Forms调用(已为AEM表单弃用) AEM Forms远程处理</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可以调用AEM Forms服务。 Java API分为客户端库和Java调用API。 (请参阅 <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API调用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Web服务</p></td>
   <td><p>AEM Forms支持SOAP/HTTP等Web服务标准。 服务可以公开为Web服务，WSDL遵循W3C定义的Web服务标准。</p><p>可以从任何Web服务栈调用服务，包括.NET Framework和Sun™ Web服务SDK。 (请参阅 <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用Web服务调用AEM Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>REST请求</p></td>
   <td><p>AEM Forms支持REST请求。 可以直接从HTML页面调用服务。 (请参阅 <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST请求调用AEM Forms</a>.)</p></td>
  </tr>
 </tbody>
</table>

下图直观地展示了AEM Forms服务可以通过各种方式以编程方式调用。

>[!NOTE]
>
>除了使用AEM Forms SDK创建可以调用AEM Forms服务的客户端应用程序之外，您还可以创建可以部署到服务容器的组件。 例如，您可以创建一个Bank组件，其中包含可在流程中使用的自定义数据类型。 即，您可以创建数据类型，例如 `com.adobe.idp.BankAccount`. 然后，您可以创建 `com.adobe.idp.BankAccount` 客户端应用程序中的实例。

服务容器提供以下功能：

* 允许使用其他方法调用AEM Forms服务。 您可以通过设置端点来配置服务，以便可以使用所有方法调用该服务：远程处理、Java API、Web服务和REST。 (请参阅 [以编程方式管理端点](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* 将消息转换为称为调用请求的规范化格式。 调用请求从客户端应用程序（或其他服务）发送到服务容器中的服务。 调用请求包含要调用的服务名称和执行操作所需的数据值等信息。 许多服务需要文档来执行操作。 因此，一个调用请求通常包含一份文档，其中可以是PDF数据、XDP数据、XML数据等。
* 将调用请求路由到适当的服务（要调用的服务的名称是调用请求的一部分）。
* 执行诸如确定调用方是否具有调用指定服务操作的权限之类的任务。 调用请求必须包含有效的AEM Forms用户名和密码。

  有多种不同的方法可以将调用请求发送到服务。 此外，还有不同的方法可以将所需的输入值发送到服务。 例如，假设您使用Java API调用需要PDF文档的服务。 相应的Java方法包含一个接受PDF文档的参数。 在这种情况下，参数的数据类型是 `com.adobe.idp.Document`. (请参阅 [使用Java API将数据传递到AEM Forms服务](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

  如果您使用watched文件夹调用服务，则当您将文件置于配置的watched文件夹中时，会发送调用请求。 如果使用电子邮件调用服务，则当电子邮件到达配置的收件箱时，会向服务发送调用请求。

  执行操作后，服务容器会发送回调用响应。 调用响应包含操作结果等信息。 例如，如果操作修改了PDF文档，则调用响应将包含修改后的PDF文档。 如果操作不成功，则调用响应将包含错误消息。

  调用响应的检索方式与调用请求的发送方式相同。 也就是说，如果调用请求是使用Java API发送的，则调用响应可以使用Java API进行检索。 例如，假设某个操作修改了PDF文档。 您可以通过获取调用服务的Java方法的返回值来检索修改后的PDF文档。

  在调用长期进程时，调用响应将包含与调用请求关联的标识符值。 使用此标识符值，您可以稍后检查进程的状态。 例如，以MortgageLoan长期服务为例。 使用标识符值，您可以检查以确定进程是否成功完成。 (请参阅 [调用以人为中心的长期进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  下图显示调用服务的客户端应用程序（使用Java API）。

  当客户端应用程序调用服务时，会发生三个事件：

   1. 客户端应用程序向服务发送调用请求。
   1. 服务执行调用请求中指定的操作。
   1. 服务容器向客户端应用程序返回调用响应。

**另请参阅**

[了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[使用AEM Forms调用(已为AEM表单弃用) AEM Forms远程处理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[调用以人为中心的长期进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST请求调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
