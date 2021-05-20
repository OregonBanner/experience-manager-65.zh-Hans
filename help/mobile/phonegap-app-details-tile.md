---
title: 管理应用程序拼贴
seo-title: 管理应用程序拼贴
description: 可查看本页以了解应用程序功能板上的“管理应用程序拼贴”，该功能板提供了修改应用程序详细信息的功能。
seo-description: 可查看本页以了解应用程序功能板上的“管理应用程序拼贴”，该功能板提供了修改应用程序详细信息的功能。
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# 管理应用程序磁贴{#manage-app-tile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

应用程序功能板上的&#x200B;**管理应用程序**&#x200B;拼贴提供了修改应用程序详细信息的功能。 要打开“详细信息”页面，请单击“管理应用程序”拼贴的详细信息链接。 在“管理应用程序”页面中，您可以编辑PhoneGap应用程序配置(config.xml)设置，并准备应用程序以提交到各种应用程序商店。

![chlimage_1-116](assets/chlimage_1-116.png)

## 了解管理应用程序磁贴{#understanding-the-manage-app-tile}

您可以深入到&#x200B;**管理应用程序**&#x200B;拼贴中的每个拼贴，以通过单击“……”来查看或编辑详细信息 在右下角。

### “基本”选项卡{#the-basic-tab}

您可以在此选项卡中编辑应用程序的&#x200B;**名称**、**作者**、**简短说明**&#x200B;和&#x200B;**描述**。

![chlimage_1-117](assets/chlimage_1-117.png)

### “高级”选项卡{#the-advanced-tab}

每个移动应用程序平台都描述了收集哪些数据，并专门针对每个应用程序存储。

显示的平台由PhoneGap config.xml内容驱动：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

例如，每个供应商应用商店（如Apple App Store或Google Play Store）都需要移动应用程序的一个或多个屏幕截图，以便向客户显示应用程序详细信息。 这些屏幕截图可以对维度和内容有严格要求（基本上它们必须真正代表应用程序）。 AEM应用程序支持选择和管理受支持平台的这些屏幕截图，并根据每个供应商的应用商店的要求查看端口维度。

>[!NOTE]
>
>AEM Verify应用程序提供了在AEM中将屏幕截图直接发送到应用程序详细信息的功能。
>
>有关更多详细信息，请参阅[AEM Verify](/help/mobile/phonegap-mobile-quickstart.md)移动快速入门。

![chlimage_1-118](assets/chlimage_1-118.png)

### 元数据 {#metadata}

>[!NOTE]
>
>熟悉&#x200B;**管理应用程序**&#x200B;拼贴后，请参阅[编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)以查看和编辑元数据。

#### 通用元数据 {#common-metadata}

每个应用程序都应具有有助于配置应用程序不同方面的关联元数据。 “管理应用程序”页面被分为两个与元数据收集相关的不同区域。 平台特定的元数据和常用元数据。

所有平台都有通用配置和元数据。

在此部分中，您可以定义内容更新服务器URL、移动应用程序的登陆页面、用于编译的PhoneGap版本、应用程序版本、名称、描述等。

**应用** 程序版本是您的应用程序的工作版本。通常的最佳实践是使用3位小数表示法，并在首次发行之前从1.0.0以下开始。

**PhoneGap** Version是您希望在其中使用PhoneGap编译应用程序的版本。最佳实践是跟上当前版本，以确保您获得最新、最佳的功能和错误修复。

**Content Update Server** URL是您的应用程序将用来调用ContentSync更新的URL。必须将其设置为调度程序URL，或者（如果不使用调度程序）设置为将用于向应用程序提供ContentSync更新的某个发布实例。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非有数据填充在字段中，否则此部分可能显示为空。
>
>在详细信息视图顶部，您将看到应用程序版本、 PhoneGap版本和更新URL，这些值都可以在常用元数据部分中设置。 但是，无法编辑应用程序ID。

#### 平台元数据{#platform-metadata}

PhoneGap config.xml中定义的每个平台都可以包含自定义平台属性。 AEM开发人员必须提供内容结构才能捕获这些资产。 可以在iOS中找到提供的平台特定属性示例。

现在，所有已配置平台的元数据都会同时显示在“管理应用程序”拼贴的“高级”选项卡上。

>[!NOTE]
>
>在CLI或远程PhoneGap构建期间，平台元数据部分不由PhoneGap使用，而是AEM会尝试为平台捕获元数据，以便稍后在提交到目标供应商的应用程序存储时可以使用这些元数据部分。

对于AEM无法理解的平台，AEM开发人员仍可以扩展UI以捕获此元数据，稍后可以在应用程序提交过程中导出和使用该元数据。

#### iOS 元数据 {#ios-metadata}

Apple AppStore需要其他元数据才能提交您的应用程序进行分发。 iOS元数据部分会尝试收集Apple iTMSTransporter工具可以使用的必需信息，以将元数据发布到关联的Apple开发人员帐户。

要获取Apple特定的元数据，您首先需要在[https://itunesconnect.apple.com](https://itunesconnect.apple.com/)上创建应用程序。 创建应用程序后，如果您希望使用Apple iTMSTransporter工具验证元数据并将其上传到itunesconnect.apple.com，则Apple将生成iOS元数据部分所需的元数据。 如果您只想获取要收集的元数据，则不必填写特定于iOS的元数据。 您仍可以将将合并iOS和常用元数据的元数据导出，并将所有屏幕截图收集到一个zip文件中，以便随时下载。

下载的zip文件包含一个itmsp文件，可以检查metadata.xml是否存在。 itmsp文件包含导出的元数据（在metadata.xml文件中）以及所有关联的屏幕截图。

导出功能用于提供一种收集屏幕截图和元数据的便捷方式，这些屏幕截图和元数据可以传递到应用程序发布者以输入到供应商特定的应用程序存储中。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android 元数据 {#android-metadata}

选择Android平台时，此时没有可设置的自定义元数据。 单击下载按钮时，将生成zip文件格式的属性文件，其中包含所有元数据和关联的屏幕截图。

导出功能用于提供一种收集屏幕截图和元数据的便捷方式，这些屏幕截图和元数据可以传递到应用程序发布者以输入到供应商特定的应用程序存储中。

![chlimage_1-121](assets/chlimage_1-121.png)

### 内容更新服务器 URL {#content-update-server-url}

AEM应用程序的主要功能之一是能够让移动应用程序通过ContentSync请求新内容，其中内容可以是html资源、页面、视频、图像、文本等。 内容作者更新了内容后，服务器会发布该内容，以便该内容更新可供移动应用程序下载。

Content Update Server URL属性是必须指向发布实例的URL;直接或通过调度程序或CDN。 URL的格式很简单：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果您的创作服务器实例正在复制到多个发布服务器实例(AEM的通用架构)，则每个发布服务器将具有相同的更新内容，因为该更新是在创作上构建的，并且已复制到所有发布实例。 基本上，完全支持负载平衡和故障切换。

### “插件”选项卡{#the-plugins-tab}

**插件**&#x200B;选项卡描述与您的应用程序关联的插件。 此信息将用于在生成期间检索相应的插件。

![chlimage_1-122](assets/chlimage_1-122.png)

### 屏幕截图选项卡{#the-screenshots-tab}

**屏幕截图**&#x200B;选项卡显示不同平台上支持的屏幕截图分辨率。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>要添加和删除屏幕截图，请参阅[编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)。

### “Authentication（身份验证）”选项卡{#the-authentication-tab}

**Authentication**&#x200B;选项卡允许您选择要与您的应用程序关联的OAuth客户端，并使开发人员能够利用Adobe Experience Manager的OAuth身份验证。

![chlimage_1-124](assets/chlimage_1-124.png)

### 后续步骤 {#the-next-steps}

在应用程序功能板中了解了“管理应用程序拼贴”后，请参阅以下资源以了解其他创作角色：

* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap企业进行开发](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
