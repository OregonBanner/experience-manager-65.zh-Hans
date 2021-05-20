---
title: 使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档
seo-title: 使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档
description: 了解如何启用本机AEM搜索功能，以对受DRM保护的PDF文档执行全文搜索。
seo-description: 了解如何启用本机AEM搜索功能，以对受DRM保护的PDF文档执行全文搜索。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: 文档安全
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# 使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供了一个用户界面，用于搜索和查找存储在AEM中的各种资产。 本机搜索能够搜索和查找AEM资产，并对各种常用文档格式（如纯文本文件、Microsoft Office文档和PDF文档）执行文本搜索。 您还可以扩展并启用本机搜索，以对受DRM保护的PDF和Microsoft Office文档执行全文搜索。

请执行以下步骤，使AEM能够搜索受文档安全保护的PDF和Microsoft Office文档：

## 开始之前{#before-you-start}

* 安装和配置AEM Forms文档安全性。
* 在&#x200B;**反序列化防火墙配允许列表置的中添加包sun.util.calendar。** 配置在中列出 `https://'[server]:[port]'/system/console/configMgr`。
* 确保所有AEM包均已启动并运行。 包列在`https://'[server]:[port]'/system/console/bundles`。 如果所有包都不处于活动状态，请等待，然后在几分钟后检查包的状态。

## 在AEM Forms工作流(JEE上的AEM Forms){#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}中建立安全连接

通过安全连接，可以在JEE上的AEM Forms与在同一服务器上运行的OSGi服务之间无缝地传输信息。 使用以下方法之一建立安全连接：

* 在JEE上使用AEM Forms配置AEM Forms客户端SDK包管理员凭据
* 使用相互身份验证配置AEM Forms客户端SDK包

### 在JEE管理员凭据{#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上使用AEM Forms配置AEM Forms客户端SDK包

1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTP URL。要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE KeyStore文件上的AEM Forms路径>参数在JEE服务器上重新启动AEM Forms。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从JEE服务器上的AEM Forms启动调用的AEM Forms的用户名。指定的帐户必须有权在JEE服务器上的AEM Forms上调用文档服务。
   * **密码**:在用户名字段中指定JEE帐户上AEM Forms的密码。

   单击&#x200B;**保存**。AEM可用于搜索受文档安全保护的PDF和Microsoft Office文档。

### 使用相互身份验证{#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}配置AEM Forms客户端SDK包

1. 在JEE上为AEM Forms启用双向身份验证。 有关详细信息，请参阅[CAC和双向身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTPS URL。要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE KeyStore文件上的AEM Forms路径>参数在JEE服务器上重新启动AEM Forms。
   * **启用双向SSL**:启用启用双向SSL选项。
   * **KeyStore文件URL**:指定KeyStore文件的URL。
   * **TrustStore FIle URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定密钥库文件的密码。
   * **TrustStorePassword**:为truststore文件指定密码。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。AEM支持搜索文档安全保护的PDF和Microsoft Office文档

## 索引受策略保护的PDF或Microsoft Office文档的示例{#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF或Microsoft Office文档上传到新创建的文件夹。 现在，使用AEM搜索来搜索受策略保护的文档的内容。 它必须返回包含已搜索文本的文档。
