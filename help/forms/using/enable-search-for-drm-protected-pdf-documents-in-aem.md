---
title: 使AEM能搜索文档安全保护的PDF文档
seo-title: 使AEM能搜索文档安全保护的PDF文档
description: '了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。  '
seo-description: '了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 使AEM能搜索文档安全保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜索能够搜索和查找AEM资产，并对各种常用文档格式（如纯文本文件、Microsoft office文档和PDF文档）执行文本搜索。 您还可以扩展本机搜索功能，以对受AEM Document安全保护的 [PDF文档执行全文搜索](../../forms/using/admin-help/document-security.md)。 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 为受策略保护的示例PDF文档编制索引

## 前提条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在 [AEM Forms服务器上安装](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms Document Security Indexer包。

   * 确保JEE服务器上的AEM Forms已启动并正在运行，并且文档安全性已安装在JEE服务器上的相应AEM Forms上。 JEE服务器上的AEM Form是索引受保护的文档所必需的。

* 如果仅在JEE服务器上使用AEM Forms，则已安装索引器包。
* 确保所有捆绑包都已启动并运行。 如果所有包都不处于活动状态，请等到所有包都启动并运行。

   * 对于OSGi上的AEM Forms，这些包列在https://[server]:[port]/system/console/bundles。
   * 对于JEE上的AEM Forms，这些包列在https://[server]:[port]/[context-path]/system/console/bundles中。 例如https://localhost:8080/lc/system/console/bundles。

* 将 *sun.util.calendar包列入白名单* 。 要将包列入白名单，请执行以下步骤：

   1. 打开AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
   1. 找到并打开反序 **列化防火墙配置**。

   1. 将sun.util.calendar包添加到列入白名单的类或包前缀字段，然后单击“保 **存”**。

### 在AEM Forms JEE和OSGi堆栈之间建立安全连接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用以下方法之一建立安全连接：

* 在JEE管理员凭据上配置带有AEM Forms的Adobe liveCycle Client SDK捆绑
* 使用相互身份验证配置Adobe LiveCycle Client SDK Bundle

#### 在JEE管理员凭据上配置带有AEM Forms的Adobe liveCycle Client SDK捆绑 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
1. 找到并打 **开Adobe LiveCycle Client SDK Bundle**。 指定以下字段的值：

   * **** 服务器URL:在JEE服务器上指定AEM Forms的HTTPS URL。 要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动服务器。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **** 用户名：指定JEE帐户上用于从AEM服务器启动调用的AEM Forms用户名。 指定的帐户必须具有在JEE服务器上的AEM Forms上启动文档服务的权限。
   * **密码**:指定“用户名”字段中提到的AEM Forms on JEE帐户的口令。
   单击&#x200B;**保存**。启用AEM可搜索文档安全保护的PDF文档。

#### 使用相互身份验证配置Adobe LiveCycle Client SDK Bundle {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上为AEM Forms启用相互身份验证。 有关详细信息，请参 [阅CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM Web Console。 URL是https://[server]:[port]/system/console/configMgr。
1. 找到并打开 **Adobe LiveCycle Client SDK** Bundle。 为以下属性指定值：

   * **服务器URL**:在JEE服务器上指定AEM Forms的HTTPS URL。 要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM表单的路径>参数重新启动AEM服务器。
   * **启用双向SSL**:启用“启用双向SSL”选项。
   * **KeyStore文件URL**:指定keystore文件的URL。
   * **TrustStore FIle URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定keystore文件的口令。
   * **TrustStorePassword**:指定truststore文件的口令。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   单击&#x200B;**保存**。启用AEM以搜索文档安全性保护的PDF文档

### 为受策略保护的示例PDF文档编制索引 {#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录到AEM资产。
1. 在AEM Digital Asset manager中创建文件夹，并将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索搜索功能搜索受策略保护的文档。

