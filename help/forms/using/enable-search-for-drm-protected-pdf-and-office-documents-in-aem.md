---
title: 使AEM能够搜索文档安全保护的PDF和Microsoft Office文档
seo-title: 使AEM能够搜索文档安全保护的PDF和Microsoft Office文档
description: 了解如何启用本机AEM搜索以在受DRM保护的PDF文档上执行全文搜索。
seo-description: 了解如何启用本机AEM搜索以在受DRM保护的PDF文档上执行全文搜索。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# 使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供了一个用户界面，用于搜索和查找存储在AEM中的各种资产。 本机搜索功能可以搜索和查找AEM资产，并对各种常用文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展和启用本机搜索，以对受DRM保护的PDF和Microsoft Office文档执行全文搜索。

执行以下步骤使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档:

## 开始{#before-you-start}之前

* 安装和配置AEM Forms文档安全。
* 将sun.util.calendar包添加到&#x200B;**反序允许列表列化防火墙配置的。** 配置列在 `https://'[server]:[port]'/system/console/configMgr`。
* 确保所有AEM捆绑套件都已启动并运行。 捆绑包列在`https://'[server]:[port]'/system/console/bundles`。 如果所有捆绑包都未激活，请等待，并在几分钟后检查捆绑包的状态。

## 在AEM Forms工作流程(JEE上的AEM Forms){#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}内建立安全连接

安全连接使JEE上的AEM Forms与在同一服务器上运行的OSGi服务之间的信息无缝流动。 使用以下方法之一建立安全连接：

* 在JEE管理员凭据上配置AEM Forms客户端SDK包和AEM Forms
* 使用相互身份验证配置AEM Forms客户端SDK包

### 在JEE管理员凭据{#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上配置AEM Forms客户端SDK包和AEM Forms

1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 指定以下属性的值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTP URL。要启用通过https进行通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动JEE服务器上的AEM Forms。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从JEE服务器上的AEM Forms发起呼叫的用户名。指定的帐户必须具有在JEE服务器上调用AEM Forms上的文档服务的权限。
   * **密码**:在“用户名”字段中提到的JEE帐户上指定AEM Forms的密码。

   单击&#x200B;**保存**。AEM可用于搜索受文档安全保护的PDF和Microsoft Office文档。

### 使用相互身份验证{#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}配置AEM Forms客户端SDK包

1. 在JEE上为AEM Forms启用相互身份验证。 有关详细信息，请参阅[CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 指定以下属性的值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTPS URL。要启用通过https进行通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动JEE服务器上的AEM Forms。
   * **启用双向SSL**:启用启用双向SSL选项。
   * **密钥存储文件URL**:指定密钥库文件的URL。
   * **TrustStore FIle URL**:指定信任存储文件的URL。
   * **密钥存储密码**:指定密钥库文件的口令。
   * **TrustStorePassword**:指定truststore文件的口令。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。AEM可用于搜索受文档安全保护的PDF和Microsoft Office文档

## 索引受策略保护的示例PDF或Microsoft Office文档{#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF或Microsoft Office文档上传到新创建的文件夹。 现在，使用AEM搜索搜索功能搜索受策略保护的文档的内容。 它必须返回包含已搜索文本的文档。

