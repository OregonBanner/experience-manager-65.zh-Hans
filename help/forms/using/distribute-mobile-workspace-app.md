---
title: 分发AEM Forms应用程序
seo-title: 分发AEM Forms应用程序
description: 使用移动设备管理(MDM)在移动设备上大规模部署应用程序。
seo-description: 使用移动设备管理(MDM)在移动设备上大规模部署应用程序。
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 分发AEM Forms应用程序 {#distribute-aem-forms-app}

移动设备管理(MDM)支持在移动设备上大规模部署应用程序。

>[!NOTE]
>
>此分发仅适用于iOS和Android设备。

## 通常由MDM解决方案提供的主要功能： {#main-features-generally-provided-by-mdm-solutions}

* 在企业环境中启用设备注册
* 允许配置和更新设备设置
* 强制遵守安全规范。
* 安全地移动访问公司资源

MDM解决方案和移动应用程序管理允许您在企业中的移动设备上管理内部、公共和购买的应用程序。

MDM管理员可以将ipa和apk文件上传到MDM服务器，并控制可以访问ipa或apk文件的用户。 管理员还可以控制与每个应用程序对应的用户档案设置。

## 用户档案影响AEM Forms应用程序的设置 {#profile-settings-affecting-the-aem-forms-app-br}

设备上的以下用户档案设置将影响设备上AEM Forms应用程序的功能：

* **允许在“设备** ”功能部分 **中使用相机**

如果禁用“允 **许使用摄像机**”，则“照片”注释的 [摄像机功能将不起作用](/help/forms/using/add-attachments.md) 。 您需要启用此选项才能在应用程序中使用相机。

* **在“密码策略** ”部分要求设备上的密码

要启用应 **用程序数据加密**，建议您在设备上启用 **密码** 。 如果未在设备上设置密码，则存储在设备上的应用程序数据不会加密。
