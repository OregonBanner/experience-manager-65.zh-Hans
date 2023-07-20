---
title: 使用OAuth 2.0客户端凭据流将Salesforce与AEM Forms集成
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: 使用OAuth 2.0客户端凭据流将Salesforce集成与AEM Forms集成的步骤
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: 91683330024fbf1059715447073f35cecde45b0a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# 使用OAuth 2.0客户端凭据流集成Salesforce  {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html) |
| AEM 6.5 | 本文 |


要将AEM Forms与Salesforce应用程序集成，请使用OAuth 2.0客户端凭据流。 这是一种标准化的安全方法，无需用户参与即可进行直接通信。 在此流程中，客户端应用程序(AEM Form)交换在Salesforce连接的应用程序中定义的客户端凭据以获取访问令牌。 所需的客户端凭据包括使用者密钥和使用者密钥。

## 使用OAuth 2.0客户端凭据流将Salesforce与AEM Forms集成的优势 {#advantages-of-integrating-saleforce-aemforms}

除了OAuth 2.0客户端凭据流之外，AEM Forms还支持Salesforce与授权代码流的集成。 在OAuth 2.0授权代码流中，客户端应用程序(AEM Forms)代表Salesforce用户获取资源访问权限，这有一些限制：

* 每个用户最多允许五个连接。 后续连接会自动撤销旧连接。
* 如果用户被停用、失去访问权限或更新密码，AEM数据源配置将停止工作。

## 前提条件 {#prerequisites}

在Salesforce和AEM环境之间检索和获取数据需要满足某些先决条件，然后才能继续：

+++ **使用客户端凭据流和仅限API的用户设置Saleforce连接的应用程序**

必须使用OAuth 2.0客户端凭据流为您的组织创建一个Salesforce连接应用程序和一个仅API用户。 有关详细步骤，请参阅文章 [用于服务器到服务器集成的OAuth 2.0客户端凭据流](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). 这些步骤可帮助您获取使用者密钥和使用者密钥。

>[!NOTE]
>
> 确保在创建AEM数据源配置时记下使用者密钥和使用者密钥。

+++

+++ **创建Swagger文件**

Swagger是一组用于开发和描述RESTful API的开源规则、规范和工具。 [创建swagger文件](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 将Salesforce与AEM Forms集成之前。

>[!NOTE]
>
> AEM 6.5仅支持Swagger 2.0文件规范。

+++

## 使用客户端凭据配置Salesforce流的步骤 {#steps-to-create-aem-datasource-configuration}

1. 登录到您的创作实例。
1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**.
1. 选择配置文件夹。
1. 单击 **[!UICONTROL 创建]** 和 **[!UICONTROL 创建数据源配置]** 显示。
1. 指定 **[!UICONTROL 标题]** 并选择 **[!UICONTROL 服务类型]** 作为 **[!UICONTROL RESTful服务]**.
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择 **[!UICONTROL Swagger源]** 作为 **[!UICONTROL 文件].**
   >[!NOTE]
   >
   > 一旦选择了swagger文件，就会自动填充方案、主机名和基本路径。

1. 通过单击从本地计算机上传创建的swagger文件 **[!UICONTROL 浏览]**.
1. 选择 **[!UICONTROL 身份验证类型]** 作为 **[!UICONTROL OAuth 2.0]** 和 **[!UICONTROL 身份验证设置]** 面板。
1. 选择 **[!UICONTROL 授权类型]** 作为 **[!UICONTROL 客户端凭据]**.
1. 指定 **[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]** 从Salesforce连接的应用程序获取。
1. 指定 **[!UICONTROL 访问令牌URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每个组织都有其自己的特定域名。

1. 单击 **[!UICONTROL 测试连接]**.
1. 如果连接成功，请单击 **[!UICONTROL 创建]** 按钮。

现在，您可以 [创建表单数据模型](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 将配置的数据源与您的自适应Forms集成。
