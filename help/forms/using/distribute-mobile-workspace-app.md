---
title: 分发AEM Forms应用程序
description: 使用移动设备管理(MDM)在移动设备上大规模部署应用程序。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 分发AEM Forms应用程序 {#distribute-aem-forms-app}

移动设备管理(MDM)允许在移动设备上大规模部署应用程序。

>[!NOTE]
>
>此分发仅适用于iOS和Android™设备。

## MDM解决方案提供的主要功能： {#main-features-generally-provided-by-mdm-solutions}

* 在企业环境中启用设备注册
* 允许配置和更新设备设置
* 强制执行安全合规性。
* 保护对公司资源的移动访问

MDM解决方案与移动应用程序管理一起，允许您跨企业中的移动设备管理内部、公开和购买的应用程序。

MDM管理员可以将ipa和apk文件上传到MDM服务器，并控制可以访问ipa或apk文件的用户。 管理员还可以控制对应于每个应用程序的配置文件设置。

## 影响AEM Forms应用程序的配置文件设置 {#profile-settings-affecting-the-aem-forms-app-br}

您设备上的以下配置文件设置会影响您设备上AEM Forms应用程序的运行：

* **允许使用摄像头** 在 **设备功能** 部分

如果您禁用 **允许使用摄像头**，的摄像头功能 [照片批注](/help/forms/using/add-attachments.md) 不起作用。 启用此选项以在应用程序中使用摄像头。

* **需要设备密码** 在密码策略部分中

要启用 **应用程序数据加密**，建议您启用 **密码** 在您的设备上。 如果未在设备上设置密码，则不会加密存储在设备上的应用程序数据。
