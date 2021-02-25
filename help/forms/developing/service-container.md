---
title: 服务容器
seo-title: 服务容器
description: AEM Forms服务位于服务容器
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# 服务容器{#service-container}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

位于服务容器中的AEM Forms服务（包括标准服务，如加密服务、长期和短期进程）可以使用各种提供程序（如EJB提供程序）调用。 EJB提供程序允许通过RMI/IIOP调用AEM Forms服务。 Web服务提供商使用SOAP/HTTP和SOAP/JMS等标准将服务公开为Web服务（WSDL生成）。

下表介绍了以编程方式调用AEM Forms服务的不同方式。

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
   <td><p>远程集成使Flex客户端能够调用服务操作。 (请参阅<a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">使用(对于AEM表单已弃用)调用AEM Forms Remoting</a>。)</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API可以调用AEM Forms服务。 Java API被组织到客户端库和Java调用API中。 (请参阅<a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">使用Java API调用AEM Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>Web服务</p></td>
   <td><p>AEM Forms支持SOAP/HTTP等Web服务标准。 服务可以作为Web服务公开，WSDL符合W3C定义的Web服务标准。</p><p>可以从任何Web服务堆栈(包括.NET Framework和Sun™ Web Services SDK)调用服务。 (请参阅<a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">使用Web服务调用AEM Forms</a>。)</p></td>
  </tr>
  <tr>
   <td><p>REST请求</p></td>
   <td><p>AEM Forms支持REST请求。 可以从HTML页面直接调用服务。 (请参阅<a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">使用REST请求调用AEM Forms</a>。)</p></td>
  </tr>
 </tbody>
</table>

下图直观地显示了以编程方式调用AEM Forms服务的不同方式。

>[!NOTE]
>
>除了使用AEM Forms SDK创建可调用AEM Forms服务的客户端应用程序外，您还可以创建可部署到服务容器的组件。 例如，您可以创建一个包含可在流程中使用的自定义数据类型的银行组件。 也就是说，您可以创建`com.adobe.idp.BankAccount`等数据类型。 然后，您可以在客户端应用程序中创建`com.adobe.idp.BankAccount`实例。

服务容器提供以下功能：

* 允许使用不同方法调用AEM Forms服务。 可以通过设置端点来配置服务，以便使用所有方法调用该服务：远程处理、Java API、Web服务和REST。 （请参阅[以编程方式管理终结点](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)。）
* 将消息转换为称为调用请求的标准化格式。 从客户端应用程序（或其他服务）向位于服务容器中的服务发送调用请求。 调用请求包含诸如要调用的服务的名称和执行该操作所需的数据值等信息。 许多服务需要文档才能执行操作。 因此，调用请求通常包含文档，可以是PDF数据、XDP数据、XML数据等。
* 将调用请求路由到相应的服务（要调用的服务的名称是调用请求的一部分）。
* 执行任务，如确定调用者是否具有调用指定服务操作的权限。 调用请求必须包含有效的AEM表单用户名和密码。

   向服务发送调用请求的方式不同。 此外，向服务发送所需输入值的方式也不同。 例如，假设您使用Java API调用需要PDF文档的服务。 相应的Java方法包含接受PDF文档的参数。 在这种情况下，参数的数据类型为`com.adobe.idp.Document`。 (请参阅[使用Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)将数据传递到AEM Forms服务。)

   如果您使用监视文件夹调用服务，则当您将文件放在已配置的监视文件夹中时，将发送调用请求。 如果您使用电子邮件调用服务，则当电子邮件到达配置的收件箱中时，将向服务发送调用请求。

   服务容器在执行操作后发回调用响应。 调用响应包含操作结果等信息。 例如，如果操作修改PDF文档，则调用响应将包含修改后的PDF文档。 如果操作失败，则调用响应将包含错误消息。

   可以以发送调用请求的相同方式检索调用响应。 即，如果使用Java API发送调用请求，则可以使用Java API检索调用响应。 例如，假定某个操作修改PDF文档。 您可以通过获取调用该服务的Java方法的返回值来检索修改后的PDF文档。

   当调用长寿命进程时，调用响应包含与调用请求相关联的标识符值。 使用此标识符值，您可以在以后检查进程的状态。 例如，考虑MortgageLoan长期服务。 使用标识符值，您可以检查以确定该过程是否成功完成。 （请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

   下图显示了调用服务的客户端应用程序（使用Java API）。

   当客户端应用程序调用服务时，会出现三个事件:

   1. 客户端应用程序向服务发送调用请求。
   1. 服务执行在调用请求中指定的操作。
   1. 服务容器返回对客户端应用程序的调用响应。

**另请参阅**

[了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[使用(AEM表单已弃用)调用AEM FormsAEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[使用Java API调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用REST请求调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
