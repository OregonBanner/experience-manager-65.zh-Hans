---
title: 使用OAuth 2.0客户端凭据流将Salesforce与AEM Forms集成
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: 使用OAuth 2.0客户端凭据流将Salesforce集成与AEM Forms集成的步骤
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 66%

---

# 使用OAuth 2.0客户端凭据流集成Salesforce  {#configure-salesforce-with-ouath-2.0-client-credential}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | 本文 |

您可以使用 OAuth 2.0 客户端凭据将 AEM Forms 与 Salesforce 应用程序集成。OAuth 2.0 客户端凭据是一种标准且安全的直接通信方法，无需用户参与。

![在AEM Forms和Salesforce应用程序之间设置通信时的工作流](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms交换在Salesforce连接的应用程序中定义的客户端凭据（使用者密钥和使用者密钥）以获取访问令牌。

与授权代码流身份验证相比，使用 OAuth 2.0 客户端凭据进行身份验证可获得多个好处：

* OAuth 2.0 客户端凭据身份验证允许每个用户拥有超过五个连接。
* AEM 数据源配置继续处理 AEM 用户的停用、访问权限更改、密码更新。

## 前提条件 {#prerequisites}

在设置 Salesforce 应用程序和 AEM 环境之间的通信之前：

* 为您的组织创建[采用 OAuth 2.0 客户端凭据流的 Salesforce 连接的应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5)和仅 API 用户，并获取应用程序的消费方密钥和消费方密码。

* 确保已适当配置 Swagger 文件以匹配您组织的 API。或者，您可以选择从头[创建一个 Swagger 文件](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html)，该文件专门用于您的 AEM 环境。
>[!NOTE]
>
> AEM 6.5仅支持Swagger 2.0文件规范。

+++

## 使用客户端凭据配置Salesforce流的步骤 {#steps-to-create-aem-datasource-configuration}

1. 登录您的创作实例。
1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**。
1. 选择配置文件夹。
1. 单击&#x200B;**[!UICONTROL 创建]**，**[!UICONTROL 创建数据源配置]**&#x200B;随即出现。
1. 指定&#x200B;**[!UICONTROL 标题]**&#x200B;并选择&#x200B;**[!UICONTROL 服务类型]**&#x200B;为 **[!UICONTROL RESTful 服务]**。
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择 **[!UICONTROL Swagger 源]**&#x200B;作为&#x200B;**[!UICONTROL 文件]。**
   >[!NOTE]
   >
   > 一旦选择了swagger文件， Scheme 、 Host name和Base路径将自动填充。

1. 通过单击&#x200B;**[!UICONTROL 浏览]**&#x200B;从本地计算机上传创建的 swagger 文件。
1. 选择&#x200B;**[!UICONTROL 身份验证类型]**&#x200B;为 **[!UICONTROL OAuth 2.0]**，**[!UICONTROL 身份验证设置]**&#x200B;面板随即出现。
1. 选择 **[!UICONTROL 授权类型]** 作为 **[!UICONTROL 客户端凭据]**.
1. 指定从 Salesforce 连接的应用程序获取的&#x200B;**[!UICONTROL 客户端 ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密码]**。
1. 用以下格式指定&#x200B;**[!UICONTROL 访问令牌 URL]**
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每个组织都有自己特定的域名。

1. 单击&#x200B;**[!UICONTROL 测试连接]**。
1. 如果连接成功，请单击&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。

现在，您可以 [创建表单数据模型](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 将配置的数据源与您的自适应Forms集成。
