---
title: 使AEM能够搜索文档安全保护的PDF和Microsoft office文档
seo-title: 使AEM能够搜索文档安全保护的PDF和Microsoft office文档
description: 了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。
seo-description: 了解如何启用本机AEM搜索以对受DRM保护的PDF文档执行全文搜索。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使AEM能够搜索文档安全保护的PDF和Microsoft office文档{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供了一个用户界面，用于搜索和查找存储在AEM中的各种资产。 本机搜索能够搜索和查找AEM资产，并对各种常用文档格式（如纯文本文件、Microsoft office文档和PDF文档）执行文本搜索。 您还可以扩展和启用本机搜索功能，以对受DRM保护的PDF和Microsoft office文档执行全文搜索。

执行以下步骤以使AEM能够搜索文档安全保护的PDF和Microsoft office文档：

## Before you start {#before-you-start}

* 安装和配置AEM Forms文档安全性。
* 将sun.util.calendar包添加到反序列化防火墙配置 **的白名单中。** 配置列在 `https://[server]:[port]/system/console/configMgr`。
* 确保所有AEM捆绑包都已启动并运行。 这些包列在 `https://[server]:[port]/system/console/bundles`。 如果所有包都未激活，请等待几分钟，然后检查这些包的状态。

## 在AEM Forms工作流程（JEE上的AEM Forms）中建立安全连接 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全连接使JEE上的AEM Forms与在同一服务器上运行的OSGi服务之间能够无缝地传输信息。 使用以下方法之一建立安全连接：

* 在JEE管理员凭据上配置AEM Forms客户端SDK包和AEM Forms
* 使用相互身份验证配置AEM Forms客户端SDK包

### 在JEE管理员凭据上配置AEM Forms客户端SDK包和AEM Forms {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **** 服务器URL:在JEE服务器上指定AEM Forms的HTTP URL。 要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM表单的路径>参数在JEE服务器上重新启动AEM表单。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   * **** 用户名：指定JEE帐户上的AEM Forms的用户名，以用于从JEE服务器上的AEM Forms启动调用。 指定的帐户必须具有在JEE服务器上的AEM Forms上调用文档服务的权限。
   * **密码**:指定“用户名”字段中提到的AEM Forms on JEE帐户的口令。
   单击&#x200B;**保存**。启用AEM可搜索受文档安全保护的PDF和Microsoft office文档。

### 使用相互身份验证配置AEM Forms客户端SDK包 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 在JEE上为AEM Forms启用相互身份验证。 有关详细信息，请参 [阅CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>:&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK包。 为以下属性指定值：

   * **** 服务器URL:在JEE服务器上指定AEM Forms的HTTPS URL。 要通过https启用通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE密钥库文件上的AEM表单的路径>参数在JEE服务器上重新启动AEM表单。
   * **启用双向SSL**:启用“启用双向SSL”选项。
   * **KeyStore文件URL**:指定keystore文件的URL。
   * **TrustStore FIle URL**:指定truststore文件的URL。
   * **KeyStore密码**:指定keystore文件的口令。
   * **TrustStorePassword**:指定truststore文件的口令。
   * **服务名称**:将RightsManagementService添加到指定服务的列表。
   单击&#x200B;**保存**。启用AEM可搜索文档安全保护的PDF和Microsoft Office文档

## 为受策略保护的示例PDF或Microsoft office文档编制索引 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理员身份登录到AEM资产。
1. 在AEM Digital Asset manager中创建文件夹，并将受策略保护的PDF或Microsoft office文档上传到新创建的文件夹。 现在，使用AEM搜索搜索受策略保护的文档的内容。 它必须返回包含已搜索文本的文档。

