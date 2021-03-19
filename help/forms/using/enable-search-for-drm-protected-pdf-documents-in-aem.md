---
title: 使AEM能够搜索文档安全保护的PDF文档
seo-title: 使AEM能够搜索文档安全保护的PDF文档
description: '了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。  '
seo-description: '了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# 使AEM能够搜索受文档安全保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜索能够搜索和查找AEM资产，并对各种常用文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展本机搜索，以对受AEM 文档 security](../../forms/using/admin-help/document-security.md)保护的[PDF文档执行全文搜索。 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 索引受策略保护的示例PDF文档

## 前提条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在AEM Forms服务器上安装[AEM Forms 文档 Security Indexer包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)。

   * 确保JEE服务器上的AEM Forms处于运行状态，并且JEE服务器上的相应AEM Forms上安装了文档安全。 JEE服务器上的AEM表单是索引受保护文档的必需。

* 如果仅在JEE服务器上使用AEM Forms，则已安装索引器包。
* 确保所有捆绑包都已启动并运行。 如果所有捆绑包都不处于活动状态，请等待所有捆绑包都启动并运行。

   * 对于OSGi上的AEM Forms，这些包列在https://&#39;[server]:[port]&#39;/system/console/bundles中。
   * 对于JEE上的AEM Forms，这些包列在https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles中。 例如https://localhost:8080/lc/system/console/bundles。

* 将&#x200B;*sun.util.calendar*&#x200B;包添加到允许列表。 要将包添加到允许列表，请执行以下步骤：

   1. 打开AEM Web Console。 URL为https://&#39;[server]:[port]&#39;/system/console/configMgr。
   1. 找到并打开&#x200B;**反序列化防火墙配置**。

   1. 将sun.util.calendar包添加到列入允许列表的类或包前缀字段，然后单击&#x200B;**保存**。

### 在AEM Forms JEE和OSGi堆栈{#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}之间建立安全连接

可以使用以下方法之一建立安全连接：

* 在JEE管理凭据上配置Adobe LiveCycle客户端SDK包和AEM Forms
* 使用相互身份验证配置Adobe LiveCycle客户端SDK包

#### 在JEE管理员凭据{#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}上配置Adobe LiveCycle客户端SDK包和AEM Forms

1. 打开AEM Web Console。 URL为https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到并打开&#x200B;**Adobe LiveCycle客户端SDK包**。 指定以下字段的值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTPS URL。要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动服务器。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从AEM服务器启动调用的AEM Forms的用户名。指定的帐户必须具有在JEE服务器上的AEM Forms上开始文档服务的权限。
   * **密码**:在“用户名”字段中指定JEE帐户上AEM Forms的口令。

   单击&#x200B;**保存**。AEM可用于搜索文档安全保护的PDF文档。

#### 使用相互身份验证{#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}配置Adobe LiveCycle客户端SDK包

1. 在JEE上启用AEM Forms的相互身份验证。 有关详细信息，请参阅[CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM Web Console。 URL为https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 找到并打开&#x200B;**Adobe LiveCycle Client SDK** Bundle。 指定以下属性的值：

   * **服务器URL**:指定JEE服务器上AEM Forms的HTTPS URL。要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动AEM服务器。
   * **启用双向SSL**:启用“启用双向SSL”选项。
   * **KeyStore文件URL**:指定keystore文件的URL。
   * **TrustStore文件URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定密钥库文件的密码。
   * **TrustStorePassword**:指定truststore文件的口令。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。AEM已启用以搜索受安全保护的文档文档

### 索引受策略保护的示例PDF文档{#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，然后将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索来搜索受策略保护的文档。

