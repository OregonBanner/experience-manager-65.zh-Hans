---
title: 文档安全产品
seo-title: 文档安全产品
description: 了解AEM文档安全的各种工具和功能
seo-description: 了解AEM文档安全的各种工具和功能
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: e45e335d433f17a48ba1bf27a93c5b1003369512

---


# 文档安全产品{#document-security-offerings}

Adobe Experience Manager Forms文档安全性确保只有授权用户才能使用您的文档。 使用文档安全性，您可以安全地分发以支持的格式保存的任何信息。 支持的文件格式包括Adobe可移植文档格式(PDF)和Microsoft Word、Excel和PowerPoint文件。

您可以使用策略保护文档。 您在策略中指定的机密性设置决定了收件人如何使用您应用策略的文档。 例如，您可以指定收件人是否可以打印或复制文本、编辑文本，或向受保护的文档添加签名和注释。

策略存储在文档安全服务器上；您可以通过客户端应用程序将策略应用于文档。 对文档应用策略时，策略中指定的机密性设置将保护文档包含的信息。 您可以将受策略保护的文档分发给受策略授权的收件人。

下图显示了AEM Forms文档安全的典型架构：

![文档安全性——建议的架构](do-not-localize/document_security_architecture.png)

## 文档安全客户端 {#document-security-clients}

文档安全性为各种客户端提供保护文档、视图和编辑受保护文档的功能，以及索引器，以便对受保护文档进行全文搜索。 您可以根据自己的要求和客户端的功能选择客户端。

文档安全服务器是文档安全执行用户身份验证、策略实时管理和应用机密性等事务的核心组件。 服务器还提供了一个中心存储库，用于存储策略、审计记录和其他相关信息。

文档安全服务器提供基于Web的界面（网页），用于创建策略、管理受策略保护的文档并监视与受策略保护的文档关联的事件。 管理员还可以配置全局选项，如用户身份验证、审核和被邀请用户的消息传递，以及管理受邀用户帐户。

该服务器包含在AEM Forms文档安全附加产品中。 您可以联系AEM Forms销 [售团队](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) ，以购买文档安全插件。

### 保护文档 {#protect-documents}

AEM Forms文档安全性提供了各种工具来应用安全策略。 您可以根据要求和规范选择工具。

![文档安全产品](assets/document-security-offerings.png)

您可以使用文档安全SDK、Adobe Acrobat、文档安全扩展for Microsoft Office或可移植保护库应用和跟踪安全策略：

* **文档安全SDK:** SDK是功能丰富的客户端。 您可以使用文档安全SDK访问文档服务器功能、打开受策略保护的文档并开发自定义扩展、插件或应用程序。 例如，您可以开发扩展以保护自定义文件格式，或将SDK与数据丢失预防(DLP)解决方案集成。 使用Document Security SDK开发的扩展、应用程序和插件将文档发送到指定的AEM Forms服务器，策略将应用到服务器上。 另请注意，AEM Forms文档安全客户端SDK(CSDK)无法取消保护使用可移植保护库(PPL)保护的文档，反之亦然。

   文档安全SDK可用于Java和C++。 Java SDK包含在AEM Forms文档安全产品中，它安装在JEE上部署AEM表单时。 您可以联 [系AEM支持团队](https://helpx.adobe.com/marketing-cloud/contact-support.html) ，以购买C++ SDK。 C++ SDK可以使用Microsoft Visual Studio 2013进行编译。 您可以访问 [文档安全API文档站点](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) ，了解和使用SDK的功能。

* **Adobe Acrobat:** 您可以使用Adobe Acrobat将安全策略应用于使用常用桌面应用程序（如Microsoft Office、Web浏览器或任何支持以PDF格式打印的应用程序）创建的PDF文档。

   您可以从Adobe网站购买和下载 [Adobe Acrobat](https://acrobat.adobe.com/us/en/free-trial-download.html)。 Adobe Acrobat文章 [为PDF设置安全策略](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) ，提供了有关在Adobe Acrobat中创建和应用策略的详细信息。

* **文档Security Extension for Microsoft Office**:您可以使用文档Security Extension for Microsoft Office从Microsoft Office项目中将预定义的策略应用到Microsoft Office文件。 该扩展确保只有授权人员才能使用受策略保护的Microsoft Word、Excel和PowerPoint文件。 只有已安装该插件的授权用户才能使用受策略保护的文件。

   文档安全扩展可作为Microsoft Office插件使用。 您可以联系 [AEM支持团队](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) ，以获取扩展。 稍后，您可以访问 [文档Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) ，以了解有关安装、配置和使用扩展的信息。

* **便携式保护库：** 可移植保护库(PPL)可在本地保护文档，而无需将文档发送到AEM Forms服务器。 只有安全凭据和策略详细信息才能通过网络传输。 PPL还允许您将策略检索访问权限限制为仅登录用户。 您可以使用登录AEM用户的上下文获取策略。

   除上述功能外，可文档保护库还具有Security SDK的所有功能。 您可以使用文档安全SDK访问文档服务器功能、打开受策略保护的文档并开发自定义扩展、插件或应用程序。 另请注意，可移植保护库(PPL)无法取消保护使用AEM Forms文档安全客户端SDK(CSDK)保护的文档，反之亦然。

   可移植保护库可用于32位和64位版本的Java和C++语言。 它还可作为OSGi上的AEM Forms的OSGi捆绑提供。 C++ PPL可用Microsoft Visual Studio 2013进行编译。 如果您已获得AEM Forms文档安全附加模块的许可，可联系 [](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM Forms文档安全支持团队以购买可移植保护库。 稍后，您可以使用“便携保护库帮助”（与库捆绑）来设置和使用便携保护库。

### 视图或编辑受保护的文档 {#view-or-edit-protected-documents}

* 对 **于PDF文档**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile视图受保护的PDF文档。 大多数用户的设备上已安装Acrobat Reader，因此他们无需获取或了解其他软件来视图受保护的文档。 您还可以从 [Acrobat Reader下载网站下载Acrobat Reader](https://get.adobe.com/reader/)。

* 对 **于Microsoft Office文档**，您需要Microsoft Office和AEM Forms文档安全扩展，以用于Microsoft Office。 文档安全扩展可作为Microsoft Office插件使用。 您可以从Adobe网站下载扩展。

### 索引受保护的文档 {#index-protected-documents}

Microsoft Windows全文搜索引擎(SharePoint Index Server)和Adobe Experience Manager(AEM)可以对常用的文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行全文搜索。 您可以使用文档安全索引器启用全文搜索引擎以搜索受保护的PDF文档:

* **iFilter索引器：** 您可以使用iFilter索引器为受保护的PDF文档编制索引，并启用Microsoft Windows全文搜索引擎（Desktop Indexing Service和SharePoint Indexserver）搜索受保护的PDF文档。 有关详细信息，请参 [阅AEM SharePoint IFilter for Protected文档](assets/sharepoint-ifilter-doc-security.pdf)。

* **AEM Forms文档安全索引器：** 您可以使用AEM Forms文档安全索引器为受保护的PDF文档编制索引，并使Adobe Experience Manager能够搜索受保护的PDF文档。 索引器是AEM Forms文档安全产品的一部分。 这些内容包含在JEE安装程序上的AEM Forms中。

