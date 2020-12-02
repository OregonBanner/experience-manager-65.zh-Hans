---
title: 配置您的Adobe PhoneGap BuildCloud Service
seo-title: 配置您的Adobe PhoneGap BuildCloud Service
description: 可查看本页，以配置云服务并使用PhoneGap内部版本构建应用程序。
seo-description: 可查看本页，以配置云服务并使用PhoneGap内部版本构建应用程序。
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# 配置您的Adobe PhoneGap BuildCloud Service{#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

应用程序仪表板上的&#x200B;**PhoneGap Build拼贴**&#x200B;提供了通过Adobe PhoneGap Build服务构建和分发PhoneGap移动应用程序的功能。

使用&#x200B;**PhoneGap Build**&#x200B;磁贴推送远程构建时，将使用PhoneGap Build构建在&#x200B;**管理应用程序**&#x200B;磁贴中定义的所有受支持平台。

可以将远程内部版本推送到[https://build.phonegap.com](https://build.phonegap.com)或下载源以使用[PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/)本地内部版本。

![PhoneGap Build拼贴](assets/chlimage_1-60.png)

## 配置Cloud Service{#configuring-the-cloud-service}

为了利用PhoneGap Build，您需要使用PhoneGap Build帐户信息配置AEMPhoneGap BuildCloud Service。

如果您当前没有帐户，请导航到[https://build.phonegap.com](https://build.phonegap.com)并注册！ 如果您拥有Adobe Creative Cloud会员资格，则最多可支持25个私有应用程序（非开放源码应用程序）。

验证PhoneGap Build帐户是否处于活动状态后，请导航到AEM云管理控制台，特别是[PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html)(http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用&#x200B;**管理Cloud Services**&#x200B;拼贴配置新的云服务配置。

### 使用管理Cloud Services拼贴{#using-manage-cloud-services-tile}

在开始使用&#x200B;**PhoneGap Build**&#x200B;拼贴构建应用程序之前，必须使用AEM Mobile仪表板的&#x200B;**管理Cloud Services**&#x200B;拼贴来配置云服务。

要为应用程序配置云服务，请按照以下步骤操作：

1. 单击&#x200B;**管理Cloud Services**&#x200B;磁贴的右上角。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 从&#x200B;**添加或编辑PhoneGap Build**&#x200B;屏幕中选择&#x200B;**Cloud Service**&#x200B;选项。

   单击&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 输入凭据以创建新云配置。

   验证后，单击&#x200B;**Submit**。 此配置的云配置现在显示在&#x200B;**管理Cloud Services**&#x200B;磁贴中。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build{#building-your-application-with-phonegap-build}构建应用程序

配置云服务后，您可以使用&#x200B;**PhoneGap Build**&#x200B;拼贴构建应用程序。 单击右上角的&#x200B;**构建远程**&#x200B;或&#x200B;**下载源**&#x200B;选项中的选项。

![chlimage_1-64](assets/chlimage_1-64.png)

要使用Adobe PhoneGap Build调用远程内部版本，请单击&#x200B;**构建远程**。

>[!NOTE]
>
>如果生成因任何原因而失败（下面的红色iOS图标表示平台失败），您可以将指针悬停在图标上以获取错误消息。 或者，也可以单击三点，“...” 在拼贴底部直接导航到https://build.phonegap.com（您必须进行身份验证）并直接观察和管理您的构建。

### 使用PhoneGap CLI {#building-your-application-with-phonegap-cli}构建应用程序

PhoneGap提供命令行界面，用于在本地构建应用程序。

使用PhoneGap命令行界面(CLI)在您的计算机上编译PhoneGap应用程序。 要将AEM内容包含到您的应用程序中，AEM将创建一个ZIP文件，其中包含您的移动应用程序内容、内容同步配置和其他必需资源。 下载ZIP文件并将其包含在您的内部版本中。

为了利用PhoneGap的命令行界面，您需要设置本地环境以包括：

1. 平台SDK(iOS、Android、WindowsPhone、...)和，
1. PhoneGap CLI

您可以在此处阅读更多[。](https://docs.phonegap.com/references/phonegap-cli/)

安装前提条件后，通过创建一个简单的应用程序并使它在模拟器中运行或在设备上运行更好，从终端尝试，给它一个简单的测试：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>添加——如果您不想在连接的设备上运行它，则在此行末尾进行模拟。

验证上述方法是否有效后，请使用&#x200B;**PhoneGap Build**&#x200B;拼贴至&#x200B;**下载源**。 将文件保存并解压缩到本地系统上。 一旦完成：

* 导览至保存的文件（文件夹）
* 运行“phonegap run ios”（或android等）

### 其他资源 {#additional-resources}

要了解作者和开发人员的角色和职责，请参阅以下资源：

* [用AEM为Adobe PhoneGap企业发展](/help/mobile/developing-in-phonegap.md)
* [为AEM中的Adobe PhoneGap企业进行创作](/help/mobile/phonegap.md)
