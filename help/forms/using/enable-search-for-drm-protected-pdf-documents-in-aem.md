---
title: 启用AEM以搜索文档安全保护的PDF文档
seo-title: 启用AEM以搜索文档安全保护的PDF文档
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
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# 启用AEM以搜索文档安全保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜索功能可以搜索和查找AEM资产，并对各种常用文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展本机搜索功能，以对受AEM文档安全 [保护的PDF文档执行全文搜索](../../forms/using/admin-help/document-security.md)。 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 索引受策略保护的示例PDF文档

## 前提条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 在AEM Forms [服务器上安装AEM Forms文档安全索引器包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 。

   * 确保JEE服务器上的AEM Forms已启动并正在运行，并且JEE服务器上的相应AEM Forms上已安装文档安全。 JEE服务器上的AEM表单是索引受保护的文档所必需的。

* 如果仅在JEE服务器上使用AEM Forms，则已安装索引器包。
* 确保所有捆绑包都已启动并运行。 如果所有捆绑包都未激活，请等待所有捆绑包都启动并运行。

   * 对于OSGi上的AEM Forms，在https://&#39;[server]:[port]&#39;/system/console/bundles中列出捆绑包。
   * 对于JEE上的AEM Forms，这些包列在[https://&#39;]server[:port]&#39;/[context-path]/system/console/bundles中。 例如https://localhost:8080/lc/system/console/bundles。

* 将sun. *util.calendar包添加* 到allowlist。 要将包添加到allowlist，请执行以下步骤：

   1. 打开AEM Web Console。 URL为https://&#39;[server]:[]port&#39;/system/console/configMgr。
   1. 找到并打开反序 **列化防火墙配置**。

   1. 将sun.util.calendar包添加到“Allowlisted类”或“包前缀”字段，然后单击“ **保存**”。

### 在AEM FormsJEE和OSGi堆栈之间建立安全连接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用以下方法之一建立安全连接：

* 使用JEE管理员凭据上的AEM Forms配置Adobe LiveCycle Client SDK Bundle
* 使用相互身份验证配置Adobe LiveCycle Client SDK Bundle

#### 使用JEE管理员凭据上的AEM Forms配置Adobe LiveCycle Client SDK Bundle {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM Web Console。 URL为https://&#39;[server]:[]port&#39;/system/console/configMgr。
1. 找到并打 **开Adobe LiveCycle Client SDK Bundle**。 指定以下字段的值：

   * **服务器URL:** 指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动服务器。
   * **服务名称**: 将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从AEM服务器发起调用的AEM Forms的用户名。 指定的帐户必须具有在JEE服务器上的开始上文档服务的权限。
   * **密码**: 指定“用户名”字段中提到的JEE帐户AEM Forms的口令。

   单击&#x200B;**保存**。AEM已启用以搜索文档安全保护的PDF文档。

#### 使用相互身份验证配置Adobe LiveCycle Client SDK Bundle {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 为JEE上的AEM Forms启用相互身份验证。 有关详细信息，请参 [阅CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM Web Console。 URL为https://&#39;[server]:[]port&#39;/system/console/configMgr。
1. 找到并打 **开Adobe LiveCycle Client** SDK Bundle。 指定以下属性的值：

   * **服务器URL**: 指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM Forms路径>参数重新启动AEM服务器。
   * **启用双向SSL**: 启用启用双向SSL选项。
   * **密钥存储文件URL**: 指定密钥库文件的URL。
   * **TrustStore FIle URL**: 指定信任存储文件的URL。
   * **密钥存储密码**: 指定密钥库文件的口令。
   * **TrustStorePassword**: 指定truststore文件的口令。
   * **服务名称**: 将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。AEM已启用以搜索文档安全保护的PDF文档

### 索引受策略保护的示例PDF文档 {#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索搜索受策略保护的文档。

