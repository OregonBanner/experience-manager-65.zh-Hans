---
title: 配置Adobe PhoneGap Build云服务
seo-title: 配置Adobe PhoneGap Build云服务
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

---


# 配置Adobe PhoneGap Build云服务 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

应用 **程序控制板上的PhoneGap Build Tile** ，允许通过Adobe phoneGap build服务构建和分发PhoneGap移动应用程序。

使用PhoneGap Build拼贴推送远程构建时，将 **使用PhoneGap** Build构建“管理应用程序”拼贴中定义的所有受支持 **平台** 。

您可以将远程构建推送到 [https://build.phonegap.com](https://build.phonegap.com) ，或下载源以使用 [PhoneGap CLI本地构建](https://docs.phonegap.com/references/phonegap-cli/)。

![PhoneGap Build拼贴](assets/chlimage_1-60.png)

## 配置云服务 {#configuring-the-cloud-service}

要利用PhoneGap Build，您需要使用PhoneGap build帐户信息配置AEM PhoneGap Build云服务。

如果您当前没有帐户，请导航至 [https://build.phonegap.com](https://build.phonegap.com) 并注册！ 如果您拥有Adobe Creative cloud会员资格，则最多可支持25个专用应用程序（非开放源应用程序）。

验证PhoneGap build帐户是否处于活动状态后，请导航到AEM云管理控制台，特别是 [PhoneGap Build云服务](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用“ **管理云服务** ”拼贴配置新的云服务配置。

### 使用“管理云服务”拼贴 {#using-manage-cloud-services-tile}

在开始使用 **PhoneGap Build** tile构建应用程序之前，必须使用AEM Mobile控制面板中的 **Manage Cloud Services** tile配置云服务。

要为应用程序配置云服务，请执行以下步骤：

1. 单击“管理云服务”拼贴 **的右上角** 。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 从“添 **加或编辑云服务** ”屏幕中 **选择“PhoneGap Build** ”选项。

   单击&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 输入凭据以创建新的云配置。

   验证后，单击“提 **交”**。 此配置的云配置现在显示在“管 **理云服务”拼贴中** 。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build构建应用程序 {#building-your-application-with-phonegap-build}

配置云服务后，您可以使用 **PhoneGap Build拼贴构建应用程序** 。 单击右上角的以从“构建远程”或“ **下载源** ”选 **项中进行选择** 。

![chlimage_1-64](assets/chlimage_1-64.png)

要使用Adobe phoneGap Build调用远程构建，请单击“ **构建远程”**。

>[!NOTE]
>
>如果构建因任何原因失败（下面的红色iOS图标表示平台失败），您可以将指针悬停在图标上以获取错误消息。 或者，您也可以单击三点，“...” 在拼贴底部直接导航到https://build.phonegap.com（您必须进行身份验证），并直接观察和管理您的构建。

### 使用PhoneGap CLI构建应用程序 {#building-your-application-with-phonegap-cli}

PhoneGap提供了命令行界面，用于在本地构建应用程序。

使用PhoneGap命令行界面(CLI)在您的计算机上编译PhoneGap应用程序。 要将AEM内容包含到您的应用程序中，AEM会创建一个ZIP文件，其中包含您的移动应用程序内容、内容同步配置和其他必需资产。 下载ZIP文件并将其包含在您的内部版本中。

为了利用PhoneGap的命令行界面，您需要设置本地环境以包括：

1. Platform SDK(iOS、Android、WindowsPhone、...)和
1. PhoneGap CLI

您可以在此处阅读更 [多内容](https://docs.phonegap.com/references/phonegap-cli/)。

安装前提条件后，通过创建一个简单的应用程序并在模拟器中运行或在设备上运行，从终端尝试，为它提供一个简单的测试：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>如果您不想在连接的设备上运行，请在此行末尾添加—emulate。

验证上述功能是否有效后，使用 **PhoneGap Build** Tile **下载源**。 保存文件并将其解压缩到本地系统上。 一旦这样做：

* 导航到保存的文件（文件夹）
* 运行“phonegap run ios”（或android等）

### 其他资源 {#additional-resources}

要了解作者和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行开发](/help/mobile/developing-in-phonegap.md)
* [在AEM中为Adobe phoneGap Enterprise进行创作](/help/mobile/phonegap.md)
