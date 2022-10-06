---
title: 使AEM能够搜索文档安全保护的PDF文档
seo-title: Enable AEM to search document security protected PDF documents
description: 了解如何启用本机AEM搜索功能，以对受DRM保护的PDF文档执行全文搜索。
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# 使AEM能够搜索文档安全保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM搜索能够搜索和查找AEM资产，并对各种常用文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展本机搜索，以在 [PDF文档受AEM文档安全保护](../../forms/using/admin-help/document-security.md). 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 索引受策略保护的示例PDF文档

## 前提条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms:

   * 安装 [AEM Forms Document Security Indexer包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 在AEM Forms服务器上。

   * 确保JEE服务器上的AEM Forms已启动且正在运行，并且文档安全已安装在JEE服务器上相应的AEM Forms上。 需要JEE服务器上的AEM表单才能对受保护的文档进行索引。

* 如果您在JEE服务器上只使用AEM Forms，则索引器包已安装。
* 确保所有包都已启动并运行。 如果所有包都不处于活动状态，请等待所有包都启动并运行。

   * 对于OSGi上的AEM Forms，这些包列在https://&#39;上[服务器]:[端口]“/system/console/bundles”。
   * 对于JEE上的AEM Forms，这些包列在https://&#39;上[服务器]:[端口]&#39;/[上下文路径]/system/console/bundles。 例如https://localhost:8080/lc/system/console/bundles。

* 添加 *sun.util.calendar* 包添加到允许列表。 要将包添加到允许列表，请执行以下步骤：

   1. 打开AEM Web Console。 URL为https://&#39;[服务器]:[端口]“/system/console/configMgr.
   1. 找到并打开 **反序列化防火墙配置**.

   1. 将sun.util.calendar包添加到的类或包前列入允许列表缀字段中，然后单击 **保存**.

### 在AEM Forms JEE和OSGi堆栈之间建立安全连接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用以下方法之一建立安全连接：

* 在JEE上使用AEM Forms配置AdobeLiveCycle客户端SDK包管理员凭据
* 使用相互身份验证配置AdobeLiveCycle客户端SDK包

#### 在JEE上使用AEM Forms配置AdobeLiveCycle客户端SDK包管理员凭据 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM Web Console。 URL为https://&#39;[服务器]:[端口]“/system/console/configMgr.
1. 找到并打开 **AdobeLiveCycle客户端SDK包**. 为以下字段指定值：

   * **服务器URL:** 在JEE服务器上指定AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=重新启动服务器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定JEE帐户上用于从AEM服务器启动调用的AEM Forms的用户名。 指定的帐户必须具有在JEE服务器上的AEM Forms上启动文档服务的权限。
   * **密码**:在用户名字段中指定JEE帐户上AEM Forms的密码。

   单击“**保存**”。启用AEM以搜索文档安全保护的PDF文档。

#### 使用相互身份验证配置AdobeLiveCycle客户端SDK包 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上为AEM Forms启用双向身份验证。 有关详细信息，请参阅 [CAC与互认](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. 打开AEM Web Console。 URL为https://&#39;[服务器]:[端口]“/system/console/configMgr.
1. 找到并打开 **AdobeLiveCycle客户端SDK** 捆绑。 为以下属性指定值：

   * **服务器URL**:在JEE服务器上指定AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=重新启动AEM服务器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **启用双向SSL**:启用启用双向SSL选项。
   * **KeyStore文件URL**:指定KeyStore文件的URL。
   * **TrustStore FIle URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定密钥库文件的密码。
   * **TrustStorePassword**:为truststore文件指定密码。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。

   单击“**保存**”。AEM允许搜索文档安全保护的PDF文档

### 索引受策略保护的示例PDF文档 {#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索来搜索受策略保护的文档。
