---
title: 配置Connector for Microsoft SharePoint
seo-title: 配置Connector for Microsoft SharePoint
description: 配置Connector for Microsoft SharePoint以启用AEM表单与Microsoft SharePoint之间的通信。
seo-description: 配置Connector for Microsoft SharePoint以启用AEM表单与Microsoft SharePoint之间的通信。
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 配置Connector for Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Connector for Microsoft SharePoint支持AEM表单与Microsoft SharePoint之间的通信。 有关其他背景信息，请参阅服务参考中的“ECM [连接器”](https://www.adobe.com/go/learn_aemforms_services_63)。

1. 在管理控制台中，单击“服务”>“Connector for Microsoft SharePoint”。
1. 为SharePoint Server指定以下设置：

   **SharePoint服务器主机名：** SharePoint服务器上Web应用程序的主机名端口号，格式为 `[hostname]:'port'`。

   **用户名：** 用于连接到SharePoint服务器的用户帐户。

   **密码：** 用于连接到SharePoint服务器的用户帐户的口令

   **域名：** SharePoint服务器所在的域。

1. 单击保存。

## Microsoft SharePoint配置服务 {#microsoft-sharepoint-configuration-service}

通过Microsoft SharePoint配置服务， `(MSSharePointConfigService)` 可以指定具有模拟权限的AEM表单用户的凭据。 有关模拟权限的信息，请参 [阅配置Connector for Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 请按照以下步骤指定以下设置 `MSSharePointConfigService`:

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“服务管理”。
1. 导航服务列表，然后单击 `MSSharePointConfigService`。
1. 在“配置”页面上指定以下设置：

   * 具有模拟权限的用户的用户名
   * 上述用户的口令

1. 单击保存。

