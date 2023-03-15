---
title: 配置Adobe PhoneGap BuildCloud Service
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: 按照此页面配置云服务并使用PhoneGap Build构建应用程序。
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 配置Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

此 **PhoneGap Build拼贴** 通过应用程序仪表板，您可以通过Adobe PhoneGap Build服务构建和分发PhoneGap移动应用程序。

内定义的所有受支持平台 **管理应用程序** 使用PhoneGap Build推送远程构建时，将使用 **PhoneGap Build** 平铺。

您可以将远程内部版本推送到 [https://build.phonegap.com](https://build.phonegap.com) 或下载源以使用本地构建 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build拼贴](assets/chlimage_1-60.png)

## 配置Cloud Service {#configuring-the-cloud-service}

为了充分利用PhoneGap Build，您需要使用PhoneGap Build帐户信息配置AEMPhoneGap BuildCloud Service。

如果您当前没有帐户，请导航到 [https://build.phonegap.com](https://build.phonegap.com) 注册！ 如果您拥有Adobe Creative Cloud会员资格，则最多可以支持25个私有应用程序（非开源应用程序）。

在验证PhoneGap Build帐户处于活动状态后，请导航到您的AEM Cloud Management Console，特别是 [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用 **管理Cloud Services** 用于配置新的云服务配置。

### 使用“管理Cloud Services”拼贴 {#using-manage-cloud-services-tile}

开始使用构建应用程序之前 **PhoneGap Build** 图块，您必须使用配置云服务 **管理Cloud Services** 从AEM Mobile功能板拼贴。

要为应用程序配置云服务，请执行以下步骤：

1. 单击右上角的 **管理Cloud Services** 图块。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 选择 **PhoneGap Build** 选项来自 **添加或编辑Cloud Service** 屏幕。

   单击&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 输入您的凭据以创建新的云配置。

   验证后，单击 **提交**. 此配置的云配置现在显示在中 **管理Cloud Services** 图块。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build构建应用程序 {#building-your-application-with-phonegap-build}

配置云服务后，您可以使用构建应用程序 **PhoneGap Build** 图块。 单击右上角的，从 **构建远程** 或 **下载源** 选项。

![chlimage_1-64](assets/chlimage_1-64.png)

要使用Adobe PhoneGap Build调用远程内部版本，请单击 **构建远程**.

>[!NOTE]
>
>如果构建由于任何原因(下面的红色iOS图标表示平台失败)而失败，您可以将鼠标悬停在该图标上以获取错误消息。 或者，您可以单击图块底部的三点图标“……”以直接导航到https://build.phonegap.com（您必须进行身份验证），并直接查看和管理您的内部版本。

### 使用PhoneGap CLI构建应用程序 {#building-your-application-with-phonegap-cli}

PhoneGap提供了一个命令行界面，用于在本地构建应用程序。

使用PhoneGap命令行界面(CLI)编译计算机上的PhoneGap应用程序。 要在应用程序中包含AEM内容，AEM会创建一个ZIP文件，其中包含移动应用程序的内容、内容同步配置和其他必需资源。 下载ZIP文件并将其包含在您的内部版本中。

为了利用PhoneGap的命令行界面，您需要设置本地环境以包括：

1. Platform SDK (iOS、Android、WindowsPhone...)和
1. PhoneGap CLI

您可以阅读更多内容 [此处](https://docs.phonegap.com/references/phonegap-cli/).

安装完前提条件后，请从终端创建一个简单的应用程序，然后让它在您的模拟器中或更好的设备上运行，以进行简单的测试：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add — 如果您不想在连接的设备上运行该行，则在该行的末尾进行模拟。

一旦您确认以上各项均有效，请使用 **PhoneGap Build** 平铺到 **下载源**. 将文件保存并解压缩到本地系统中。 完成此操作后：

* 导航到已保存的文件（文件夹）
* 运行“phonegap run ios”（或android等）

### 其他资源 {#additional-resources}

要了解作者和开发人员的角色和职责，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [在AEM中为Adobe PhoneGap Enterprise创作](/help/mobile/phonegap.md)
