---
title: 管理应用程序磁贴
description: 关注此页面，了解应用程序仪表板上的“管理应用程序”拼贴，该拼贴提供了修改有关应用程序的详细信息的功能。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 1%

---

# 管理应用程序磁贴{#manage-app-tile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

此 **管理应用程序** 通过应用程序仪表板上的磁贴，可以修改有关应用程序的详细信息。 要打开“详细信息”页面，请单击“管理应用程序”拼贴的详细信息链接。 在“管理应用程序”页面中，您可以编辑PhoneGap应用程序配置(config.xml)设置，并准备应用程序以提交到各种应用程序商店。

![chlimage_1-116](assets/chlimage_1-116.png)

## 了解“管理应用程序”拼贴 {#understanding-the-manage-app-tile}

您可以深入了解 **管理应用程序** 通过单击右下角的“……”来查看或编辑详细信息的拼贴。

### “基本”选项卡 {#the-basic-tab}

您可以编辑 **名称**， **作者**， **简要说明**，和 **描述** 选项卡中针对您的应用程序设置的区段。

![chlimage_1-117](assets/chlimage_1-117.png)

### “高级”选项卡 {#the-advanced-tab}

每个移动应用程序平台都描述了要收集哪些数据，并专门针对每个应用程序商店。

显示的平台由PhoneGap config.xml内容驱动：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

每个供应商应用程序商店(例如，Apple App Store或Google Play Store)都需要移动设备应用程序的一个或多个屏幕截图，才能向客户显示您的应用程序详细信息。 这些屏幕截图可能对维度和内容有严格的要求（基本上它们必须真正代表应用程序）。 AEM Apps支持选择和管理所支持平台的这些屏幕截图，并根据每个供应商的应用商店的要求查看端口维度。

>[!NOTE]
>
>AEM Verify应用程序允许在AEM中直接将屏幕截图发送到应用程序详细信息。
>
>请参阅 [适用于AEM的Mobile Quickstart验证](/help/mobile/phonegap-mobile-quickstart.md) 以了解更多详细信息。

![chlimage_1-118](assets/chlimage_1-118.png)

### 元数据 {#metadata}

>[!NOTE]
>
>在您熟悉 **管理应用程序** 图块，请参见 [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md) 查看和编辑元数据。

#### 通用元数据 {#common-metadata}

每个应用程序都应该具有关联的元数据，这些元数据有助于配置应用程序的不同方面。 “管理应用程序”页面被分为与元数据收集相关的两个不同区域。 特定于平台的元数据和常用元数据。

所有平台都有通用配置和元数据。

在此部分中，您可以定义内容更新服务器URL、移动应用程序的登陆页面、用于编译的PhoneGap版本、应用程序版本、名称、描述等。

**应用程序版本** 是应用程序的工作版本。 通常的最佳做法是使用3位小数表示法，并且在首次发布之前的1.0.0以下开始。

**PhoneGap版本** 是您希望使用PhoneGap编译应用程序的版本。 最佳实践是与当前版本保持同步，以确保您获得最新、最大的功能和错误修复。

**内容更新服务器URL** 是应用程序将用于调用ContentSync更新的URL。 必须将其设置为您的Dispatcher URL，或者，如果不使用Dispatcher，则设置为将用于向应用程序提供ContentSync更新的发布实例之一。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非有数据填充字段，否则此部分可能显示为空。
>
>在详细信息视图的顶部，您会看到应用程序版本、PhoneGap版本和更新URL，其中的每个值都可以在通用元数据部分中进行设置。 但是，无法编辑应用程序ID。

#### 平台元数据 {#platform-metadata}

PhoneGap config.xml中定义的每个平台都可以包含自定义平台属性。 AEM开发人员必须贡献内容结构才能捕获这些属性。 可以找到iOS的特定于平台的属性的已提供示例。

现在，所有已配置平台的元数据会同时显示在“管理应用程序”拼贴的“高级”选项卡中。

>[!NOTE]
>
>PhoneGap在CLI或远程PhoneGap Build期间不使用平台元数据部分，而使用AEM尝试捕获平台的元数据，以便稍后在提交到目标供应商的应用程序存储区时使用这些元数据。

对于AEM不了解的平台，AEM开发人员仍可以扩展UI以捕获此元数据，这些元数据以后可以在应用程序提交过程中导出和使用。

#### iOS 元数据 {#ios-metadata}

Apple AppStore需要其他元数据来提交您的应用程序以进行分发。 iOS元数据部分尝试收集所需的信息，Apple的iTMSTransporter工具可使用这些信息将元数据发布到关联的Apple开发人员帐户。

要获取特定于Apple的元数据，您首先需要在上创建应用程序 [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). 在创建应用程序时，如果您希望使用Apple iTMSTransporter工具验证元数据并将其上传到itunesconnect.apple.com，则Apple将生成iOS元数据部分所需的元数据。 如果您只想获取要收集的元数据，则无需填写特定于iOS的元数据。 您仍然可以导出将iOS与常用元数据合并的元数据，并将所有屏幕截图收集到一个zip文件中，可以随时下载。

下载的zip文件包含一个itmsp文件，可检查该文件是否包含metadata.xml。 itmsp文件包含导出的元数据（在metadata.xml文件中）以及所有关联的屏幕截图。

导出功能用于提供一种收集屏幕截图和元数据的便捷方式，这些屏幕截图和元数据可以传递给应用程序发布者，以输入到供应商特定的应用程序存储中。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android™元数据 {#android-metadata}

选择Android™平台时，此时无法设置自定义元数据。 单击下载按钮后，将生成一个zip文件，其中属性文件包含所有元数据和关联的屏幕截图。

导出功能用于提供一种收集屏幕截图和元数据的便捷方式，这些屏幕截图和元数据可以传递给应用程序发布者，以输入到供应商特定的应用程序存储中。

![chlimage_1-121](assets/chlimage_1-121.png)

### 内容更新服务器 URL {#content-update-server-url}

AEM Apps的一项重要功能是，移动应用程序可以通过ContentSync请求新内容，其中内容可以是html资源、页面、视频、图像、文本等。 内容作者更新内容并发布该内容后，服务器将内容更新提供给移动设备应用程序下载。

内容更新服务器URL属性是必须指向发布实例的URL；可直接指向或通过Dispatcher或CDN指向。 URL的格式很简单：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果您的作者服务器实例复制到多个发布服务器实例(AEM的通用架构)，则每个发布服务器都将具有相同的更新内容，因为更新是在创作实例上构建的，并且已复制到所有发布实例。 基本上，完全支持负载平衡和故障切换。

### “插件”选项卡 {#the-plugins-tab}

此 **插件** 选项卡描述与应用程序关联的插件。 此信息将用于在Build期间检索相应的插件。

![chlimage_1-122](assets/chlimage_1-122.png)

### 屏幕截图选项卡 {#the-screenshots-tab}

此 **屏幕截图** 选项卡显示不同平台上支持的屏幕快照分辨率。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>要添加和删除屏幕截图，请参见 [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md).

### “身份验证”选项卡 {#the-authentication-tab}

此 **身份验证** 选项卡，可让您选择要与应用程序关联的OAuth客户端，并使开发人员能够使用Adobe Experience Manager的OAuth身份验证。

![chlimage_1-124](assets/chlimage_1-124.png)

### 后续步骤 {#the-next-steps}

在应用程序仪表板中了解了管理应用程序图块后，请参阅以下资源以了解其他创作角色：

* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有的混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
