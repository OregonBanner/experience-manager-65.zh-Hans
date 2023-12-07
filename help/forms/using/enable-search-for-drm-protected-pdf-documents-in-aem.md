---
title: 启用AEM以搜索受Document Security保护的PDF文档
description: 了解如何启用本机AEM搜索，以对受DRM保护的PDF文档执行全文搜索。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# 启用AEM以搜索受Document Security保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM search能够搜索和定位AEM资源，并对各种常用的文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展本机搜索以对其执行全文搜索 [PDF受AEM Document Security保护的文档](../../forms/using/admin-help/document-security.md). 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 为受策略保护的PDF示例文档编制索引

## 前提条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms：

   * 安装 [AEM Forms Document Security Index包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 在AEM Forms服务器上。

   * 确保JEE服务器上的AEM Forms已启动并正在运行，并且JEE服务器上的相应AEM Forms上安装了Document Security。 需要JEE服务器上的AEM表单才能对受保护文档编制索引。

* 如果您在JEE服务器上只使用AEM Forms，则表示已安装了索引器包。
* 确保所有捆绑包都已启动并正在运行。 如果所有捆绑包都未处于活动状态，请等待所有捆绑包都启动并运行。

   * 对于OSGi上的AEM Forms，这些捆绑包位于https://&#39;[服务器]：[端口]“/system/console/bundles.
   * 对于JEE上的AEM Forms，这些捆绑包位于https://&#39;[服务器]：[端口]&#39;/[上下文路径]/system/console/bundles. 例如，https://localhost:8080/lc/system/console/bundles。

* 添加 *sun.util.calendar* 打包到允许列表。 要将软件包添加到允许列表，请执行以下步骤：

   1. 打开AEM Web控制台。 URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.
   1. 查找并打开 **反序列化防火墙配置**.

   1. 列入允许列表将sun.util.calendar软件包添加到类或软件包前缀字段，然后单击 **保存**.

### 在AEM Forms JEE和OSGi栈栈之间建立安全连接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用以下方法之一来建立安全连接：

* 使用AEM Forms通过JEE管理员凭据配置AdobeLiveCycle客户端SDK包
* 使用相互身份验证配置AdobeLiveCycle客户端SDK捆绑包

#### 使用AEM Forms通过JEE管理员凭据配置AdobeLiveCycle客户端SDK包 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM Web控制台。 URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.
1. 找到并打开 **AdobeLiveCycle客户端SDK包**. 指定以下字段的值：

   * **服务器URL：** 指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=重新启动服务器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。
   * **用户名：** 指定用于启动来自AEM服务器的调用的AEM Forms on JEE帐户的用户名。 指定的帐户必须具有在JEE服务器的AEM Forms上启动文档服务的权限。
   * **密码**：指定用户名字段中提到的AEM Forms on JEE帐户的密码。

   单击 **保存**. 启用AEM以搜索受Document Security保护的PDF文档。

#### 使用相互身份验证配置AdobeLiveCycle客户端SDK捆绑包 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 为JEE上的AEM Forms启用双向身份验证。 有关详细信息，请参阅 [CAC和双向身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. 打开AEM Web控制台。 URL为https://&#39;[服务器]：[端口]&#39;/system/console/configMgr.
1. 找到并打开 **AdobeLiveCycle客户端SDK** 捆绑。 指定以下属性的值：

   * **服务器URL**：指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=重新启动AEM服务器&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 参数。
   * **启用双向SSL**：启用启用双向SSL选项。
   * **密钥库文件URL**：指定keystore文件的URL。
   * **TrustStore文件URL**：指定truststore文件的URL。
   * **KeyStore密码**：指定keystore文件的密码。
   * **Truststorepassword**：指定truststore文件的密码。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。

   单击 **保存**. 启用AEM以搜索受Document Security保护的PDF文档

### 为受策略保护的PDF示例文档编制索引 {#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录到AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索功能搜索受策略保护的文档。
