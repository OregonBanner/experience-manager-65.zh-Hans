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
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 分发AEM Forms应用程序{#distribute-aem-forms-app}

移动设备管理(MDM)支持在移动设备上大规模部署应用程序。

>[!NOTE]
>
>此分发仅适用于iOS和Android设备。

## MDM解决方案通常提供的主要功能：{#main-features-generally-provided-by-mdm-solutions}

* 在企业环境中启用设备注册
* 允许配置和更新设备设置
* 强制实施安全合规性。
* 安全地移动访问公司资源

MDM解决方案与移动应用程序管理相结合，允许您在企业的移动设备上管理内部、公共和购买的应用程序。

MDM管理员可以将ipa和apk文件上传到MDM服务器，并控制能够访问ipa或apk文件的用户。 管理员还可以控制与每个应用程序对应的配置文件设置。

## 影响AEM Forms应用程序{#profile-settings-affecting-the-aem-forms-app-br}的配置文件设置

您设备上的以下配置文件设置将影响您设备上AEM Forms应用程序的功能：

* **允许在设备** 功能部分 **中使** 用相机

如果禁用&#x200B;**允许使用camera**，则[照片批注](/help/forms/using/add-attachments.md)的相机功能将不起作用。 您需要启用此选项才能在应用程序中使用相机。

* **在密码策略** 部分中，需要设备上的密码

要启用&#x200B;**应用程序数据加密**，建议在设备上启用&#x200B;**密码**。 如果未在设备上设置密码，则存储在设备上的应用程序数据不会加密。
