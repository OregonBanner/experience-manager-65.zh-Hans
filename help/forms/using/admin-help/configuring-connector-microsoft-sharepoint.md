---
title: 为Microsoft SharePoint配置连接器
seo-title: 为Microsoft SharePoint配置连接器
description: 为Microsoft SharePoint配置连接器，以启用AEM表单与Microsoft SharePoint之间的通信。
seo-description: 为Microsoft SharePoint配置连接器，以启用AEM表单与Microsoft SharePoint之间的通信。
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 1%

---

# 为Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}配置连接器

Connector for Microsoft SharePoint支持AEM表单与Microsoft SharePoint之间的通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“ECM连接器”。

1. 在管理控制台中，单击“服务”>“Connector for Microsoft SharePoint”。
1. 为您的SharePoint服务器指定以下设置：

   **SharePoint Server主机名：** SharePoint服务器上Web应用程序的主机名端口号，格式为 `[hostname]:'port'`。

   **用户名：** 用于连接到SharePoint服务器的用户帐户。

   **密码：** 用于连接到SharePoint服务器的用户帐户的密码

   **域名：** SharePoint服务器所在的域。

1. 单击保存。

## Microsoft SharePoint配置服务{#microsoft-sharepoint-configuration-service}

Microsoft SharePoint配置服务`(MSSharePointConfigService)`允许您为具有模拟权限的AEM Forms用户指定凭据。 有关模拟权限的信息，请参阅[为Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)配置连接器。 按照以下步骤指定`MSSharePointConfigService`的设置：

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 导航服务列表，然后单击`MSSharePointConfigService`。
1. 在“配置”页面上指定以下设置：

   * 具有模拟权限的用户的用户名
   * 上述用户的密码

1. 单击保存。
