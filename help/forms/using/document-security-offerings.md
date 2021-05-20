---
title: 文档安全产品
seo-title: 文档安全产品
description: 了解AEM Document Security的各种工具和功能
seo-description: 了解AEM Document Security的各种工具和功能
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: 文档安全
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---

# 文档安全产品{#document-security-offerings}

Adobe Experience Manager Forms文档安全确保只有授权用户才能使用您的文档。 使用文档安全，您可以安全地分发您以支持格式保存的任何信息。 支持的文件格式包括Adobe可移植文档格式(PDF)和Microsoft Word、Excel和PowerPoint文件。

您可以使用策略保护文档。 您在策略中指定的保密性设置决定了收件人如何使用您应用策略的文档。 例如，您可以指定收件人是否可以打印或复制文本、编辑文本，或向受保护的文档添加签名和注释。

策略存储在Document Security服务器上；您可以通过客户端应用程序将策略应用于文档。 将策略应用于文档时，策略中指定的机密性设置将保护文档包含的信息。 您可以将受策略保护的文档分发给受策略授权的收件人。

下图显示了AEM Forms文档安全的典型架构：

![文档安全 — 推荐的架构](do-not-localize/document_security_architecture.png)

## 文档安全客户端{#document-security-clients}

Document Security提供各种客户端来保护文档、查看和编辑受保护的文档，并提供索引器以对受保护的文档进行全文搜索。 您可以根据自己的要求和客户端的功能选择客户端。

Document Security Server是Document Security执行事务（如用户身份验证、策略的实时管理和保密性应用）的中心组件。 服务器还为策略、审计记录和其他相关信息提供中央存储库。

文档安全服务器提供基于Web的界面（网页），用于创建策略、管理受策略保护的文档并监视与受策略保护的文档关联的事件。 管理员还可以配置全局选项（如受邀用户的用户身份验证、审核和消息传送），并管理受邀的用户帐户。

服务器包含在AEM Forms Document Security附加组件产品中。 您可以联系AEM Forms [销售团队](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG)来购买Document Security加载项。

### Protect文档{#protect-documents}

AEM Forms Document Security提供了各种工具来应用安全策略。 您可以根据自己的要求和规范选择工具。

![文档安全产品](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Document Security Extension for Microsoft Office或可移植保护库来应用和跟踪安全策略：

* **文档安全SDK:** SDK是一个功能丰富的客户端。您可以使用Document Security SDK访问文档服务器功能、打开受策略保护的文档，并开发自定义扩展、插件或应用程序。 例如，您可以开发扩展以保护自定义文件格式，或将SDK与数据丢失预防(DLP)解决方案集成。 使用Document Security SDK开发的扩展、应用程序和插件会将文档发送到指定的AEM Forms服务器，并且策略会应用到服务器上。 另请注意，AEM Forms文档安全客户端SDK(CSDK)无法取消对使用可移植保护库(PPL)保护的文档的保护，反之亦然。

   文档安全SDK适用于Java和C++。 Java SDK包含在AEM Forms Document Security产品中，并且安装在JEE上部署AEM表单时。 您可以联系[AEM支持团队](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)以购买C++ SDK。 C++ SDK可以使用Microsoft Visual Studio 2013进行编译。 您可以访问[文档安全API文档](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html)站点以了解和使用SDK的功能。

* **Adobe Acrobat:** 您可以使用Adobe Acrobat对使用常用桌面应用程序（如Microsoft Office、Web浏览器或任何支持PDF格式打印的应用程序）创建的PDF文档应用安全策略。

   您可以从[Adobe网站](https://acrobat.adobe.com/us/en/free-trial-download.html)购买并下载Adobe Acrobat。 Adobe Acrobat文章[为PDF设置安全策略](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html)提供了有关在Adobe Acrobat中创建和应用策略的详细信息。

* **适用于Microsoft Office的文档安全扩展**:您可以使用Document Security Extension for Microsoft Office从Microsoft Office程序中将预定义的策略应用到Microsoft Office文件。该扩展可确保只有经授权的人员才能使用受策略保护的Microsoft Word、Excel和PowerPoint文件。 只有安装了插件的授权用户才能使用受策略保护的文件。

   Document Security扩展可作为Microsoft Office插件使用。 您可以联系[AEM支持团队](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html)以获取该扩展。 稍后，您可以访问[Document Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html)帮助以了解有关安装、配置和使用该扩展的信息。

* **可移植保护库：** 可移植保护库(PPL)在本地保护文档，而无需将文档发送到AEM Forms服务器。只有安全凭据和策略详细信息才能通过网络传输。 PPL还允许您限制仅登录用户对策略检索的访问。 您可以使用登录AEM用户的用户上下文来获取策略。

   除上述功能外，可编程保护库还具有Document Security SDK的所有功能。 您可以使用Document Security SDK访问文档服务器功能、打开受策略保护的文档，并开发自定义扩展、插件或应用程序。 另请注意，可移植保护库(PPL)无法取消对使用AEM Forms文档安全客户端SDK(CSDK)保护的文档的保护，反之亦然。

   可移植保护库提供32位和64位版本的Java和C++语言版。 它还可用作OSGi上AEM Forms的OSGi包。 C++ PPL可以使用Microsoft Visual Studio 2013进行编译。 如果您已获得AEM Forms Document Security附加组件的许可，则可以联系[AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html)支持团队以购买可移植保护库。 稍后，您可以使用“可移植保护库帮助”（与库捆绑在一起）来设置和使用可移植保护库。

### 查看或编辑受保护的文档{#view-or-edit-protected-documents}

* 对于&#x200B;**PDF文档**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile查看受保护的PDF文档。 大多数用户在其设备上已安装Acrobat Reader，因此他们无需获取或了解其他软件即可查看受保护的文档。 您也可以从[Acrobat Reader下载网站](https://get.adobe.com/reader/)下载Acrobat Reader。

* 对于&#x200B;**Microsoft Office文档**，您需要Microsoft Office和AEM Forms Document Security扩展以用于Microsoft Office。 Document Security扩展可作为Microsoft Office插件使用。 您可以从Adobe网站下载扩展。

### 索引受保护的文档{#index-protected-documents}

Microsoft Windows全文搜索引擎（SharePoint索引服务器）和Adobe Experience Manager(AEM)可以对常用的文档格式（如纯文本文件、Microsoft Office文档和PDF文档）执行全文搜索。 您可以使用文档安全索引器启用全文搜索引擎来搜索受保护的PDF文档：

* **iFilter索引器：** 您可以使用iFilter索引器对受保护的PDF文档进行索引，并启用Microsoft Windows全文搜索引擎（桌面索引服务和SharePoint索引服务器）来搜索受保护的PDF文档。有关详细信息，请参阅[AEM SharePoint IFilter for Protected Documents](assets/sharepoint-ifilter-doc-security.pdf)。

* **AEM Forms Document Security Indexer:** 您可以使用AEM Forms Document Security Indexer为受保护的PDF文档编制索引，并使Adobe Experience Manager能够搜索受保护的PDF文档。索引器是AEM Forms Document Security产品的一部分。 JEE安装程序上的AEM Forms中包含这些插件。
