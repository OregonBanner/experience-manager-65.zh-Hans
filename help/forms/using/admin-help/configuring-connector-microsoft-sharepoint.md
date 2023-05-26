---
title: 配置Microsoft SharePoint的连接器
seo-title: Configuring Connector for Microsoft SharePoint
description: 配置Microsoft SharePoint的连接器，以启用AEM表单与Microsoft SharePoint之间的通信。
seo-description: Configure Connector for Microsoft SharePoint to enable communication between AEM forms and Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# 配置Microsoft SharePoint的连接器 {#configuring-connector-for-microsoft-sharepoint}

Microsoft SharePoint的连接器支持AEM表单与Microsoft SharePoint之间的通信。 有关其他背景信息，请参阅中的“Connectors for ECM” [服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

1. 在管理控制台中，单击服务>Microsoft SharePoint的连接器。
1. 为您的SharePoint服务器指定以下设置：

   **SharePoint服务器主机名：** SharePoint服务器上Web应用程序的主机名端口号，格式为 `[hostname]:'port'`.

   **用户名：** 用于连接到SharePoint服务器的用户帐户。

   **密码：** 用于连接到SharePoint服务器的用户帐户的密码

   **域名：** SharePoint服务器所在的域。

1. 单击“保存”。

## Microsoft SharePoint配置服务 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint配置服务 `(MSSharePointConfigService)` 允许您为具有模拟权限的AEM forms用户指定凭据。 有关模拟权限的信息，请参阅 [配置Microsoft SharePoint的连接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). 按照以下步骤指定设置 `MSSharePointConfigService`：

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在服务列表中导航并单击 `MSSharePointConfigService`.
1. 在“配置”页上指定以下设置：

   * 具有模拟权限的用户的用户名
   * 上述用户的密码

1. 单击“保存”。
