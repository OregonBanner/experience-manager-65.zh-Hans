---
title: 使AEM能够搜索文档安全保护PDF和Microsoft Office文档
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: 了解如何启用本机AEM搜索功能，以对受DRM保护的PDF文档执行全文搜索。
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# 使AEM能够搜索文档安全保护PDF和Microsoft Office文档{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供了一个用户界面，用于搜索和查找存储在AEM中的各种资产。 本机搜索能够搜索和查找AEM资产，并对各种常用文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展并启用本机搜索，以对受DRM保护的PDF和Microsoft Office文档执行全文搜索。

执行以下步骤以使AEM能够搜索文档安全保护PDF和Microsoft Office文档：

## 开始之前 {#before-you-start}

* 安装和配置AEM Forms文档安全性。
* 将sun.util.calendar包添加到的允许列表中 **反序列化防火墙配置。** 配置在 `https://'[server]:[port]'/system/console/configMgr`.
* 确保所有AEM包均已启动并运行。 这些包列在 `https://'[server]:[port]'/system/console/bundles`. 如果所有包都不处于活动状态，请等待，然后在几分钟后检查包的状态。

## 在AEM Forms工作流(JEE上的AEM Forms)中建立安全连接 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

通过安全连接，可以在JEE上的AEM Forms与在同一服务器上运行的OSGi服务之间无缝地传输信息。 使用以下方法之一建立安全连接：

* 在JEE上使用AEM Forms配置AEM Forms客户端SDK包管理员凭据
* 使用相互身份验证配置AEM Forms客户端SDK包

### 在JEE上使用AEM Forms配置AEM Forms客户端SDK包管理员凭据 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **服务器URL:** 在JEE服务器上指定AEM Forms的HTTP URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=在JEE服务器上重新启动AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从JEE服务器上的AEM Forms启动调用的AEM Forms的用户名。 指定的帐户必须有权在JEE服务器上的AEM Forms上调用文档服务。
   * **密码**:在用户名字段中指定JEE帐户上AEM Forms的密码。

   单击“**保存**”。AEM可用于搜索文档安全保护PDF和Microsoft Office文档。

### 使用相互身份验证配置AEM Forms客户端SDK包 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上为AEM Forms启用双向身份验证。 有关详细信息，请参阅 [CAC与互认](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;servername>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **服务器URL:** 在JEE服务器上指定AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=在JEE服务器上重新启动AEM Forms&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **启用双向SSL**:启用启用双向SSL选项。
   * **KeyStore文件URL**:指定KeyStore文件的URL。
   * **TrustStore FIle URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定密钥库文件的密码。
   * **TrustStorePassword**:为truststore文件指定密码。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。

   单击“**保存**”。AEM可用于搜索文档安全保护PDF和Microsoft Office文档

## 索引受策略保护的示例PDF或Microsoft Office文档 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF或Microsoft Office文档上传到新创建的文件夹。 现在，使用AEM搜索来搜索受策略保护的文档的内容。 它必须返回包含已搜索文本的文档。
