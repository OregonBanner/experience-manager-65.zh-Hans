---
title: 管理应用程序拼贴
seo-title: 管理应用程序拼贴
description: 可查看本页以了解应用程序仪表板上的管理应用程序拼贴，该拼贴提供修改应用程序详细信息的功能。
seo-description: 可查看本页以了解应用程序仪表板上的管理应用程序拼贴，该拼贴提供修改应用程序详细信息的功能。
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---


# 管理应用程序拼贴{#manage-app-tile}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

通过应用程序仪表板上的&#x200B;**管理应用程序**&#x200B;拼贴，可以修改有关应用程序的详细信息。 要打开“详细信息”页面，请单击“管理应用程序”拼贴的详细信息链接。 在“管理应用程序”页面中，您可以编辑PhoneGap应用程序配置(config.xml)设置，并准备应用程序提交到各种应用程序商店。

![chlimage_1-116](assets/chlimage_1-116.png)

## 了解管理应用程序拼贴{#understanding-the-manage-app-tile}

您可以进入&#x200B;**管理应用程序**&#x200B;拼贴中的每个拼贴，以视图或通过单击“...”编辑详细信息 在右下角。

### 基本选项卡{#the-basic-tab}

您可以通过此选项卡编辑应用程序的&#x200B;**名称**、**作者**、**简短说明**&#x200B;和&#x200B;**说明**。

![chlimage_1-117](assets/chlimage_1-117.png)

### 高级选项卡{#the-advanced-tab}

每个移动应用程序平台描述收集哪些数据，具体针对每个应用程序存储。

显示的平台由PhoneGap config.xml内容驱动：

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

例如，每个供应商应用程序商店（如Apple App Store或Google Play Store）都需要移动应用程序的一个或多个屏幕截图，以便向客户显示应用程序详细信息。 这些截屏在尺寸和内容方面可能有严格要求（基本上它们必须真正代表应用程序）。 AEM应用程序支持根据每个供应商的应用程序商店的要求为受支持的平台和视图端口尺寸选择和管理这些屏幕截图。

>[!NOTE]
>
>AEM Verify应用程序能够直接将屏幕截图发送到AEM中的应用程序详细信息。
>
>有关详细信息，请参阅AEM的[移动快速启动验证](/help/mobile/phonegap-mobile-quickstart.md)。

![chlimage_1-118](assets/chlimage_1-118.png)

### 元数据 {#metadata}

>[!NOTE]
>
>熟悉&#x200B;**管理应用程序**&#x200B;拼贴后，请参阅[编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)以视图和编辑元数据。

#### 通用元数据 {#common-metadata}

每个应用程序都应具有相关的元数据，有助于配置应用程序的不同方面。 “管理应用程序”页面分为两个与元数据集合相关的不同区域。 平台特定的元数据和常见元数据。

所有平台都有通用的配置和元数据。

在本节中，您定义了Content Update Server URL、移动应用程序的登陆页、用于编译的PhoneGap版本、应用程序版本、名称、说明等。

**App** Version是您的应用程序的有效版本。通常的最佳实践是在第一个版本之前使用3位小数记号和1.0.0以下的开始。

**PhoneGap** Version是您希望用PhoneGap编译应用程序的版本。最佳实践是跟上当前版本，以确保您获得最新、最出色的功能和错误修复。

**Content Update Server** URL是应用程序用来调用ContentSync更新的URL。它必须设置为调度程序URL，或者（如果不使用调度程序）设置为将用于向应用程序提供ContentSync更新的发布实例之一。

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>除非填充字段中有数据，否则此部分可能显示为空。
>
>在详细信息视图的顶部，您将看到应用程序版本、PhoneGap版本和更新URL，这些值均可在“常用元数据”部分中设置。 但是，无法编辑应用程序 ID。

#### 平台元数据{#platform-metadata}

PhoneGap config.xml中定义的每个平台都可以包含自定义平台属性。 AEM开发人员必须提供内容结构才能捕获这些属性。 可以为iOS找到提供的平台特定属性示例。

现在，所有已配置平台的元数据都同时显示在“管理应用程序”拼贴的“高级”选项卡上。

>[!NOTE]
>
>在CLI或远程PhoneGap构建过程中，平台元数据部分不由PhoneGap使用，而是AEM尝试捕获平台的元数据，以便以后在提交到目标供应商的应用程序商店时使用这些元数据。

对于AEM不理解的平台，AEM开发人员仍可以扩展UI以捕获此元数据，以后可以在应用程序提交过程中导出和使用这些元数据。

#### iOS 元数据 {#ios-metadata}

Apple AppStore需要其他元数据才能提交应用程序进行分发。 iOS元数据部分尝试收集Apple的iTMSTransporter工具可以使用的必需信息，以将元数据发布到关联的Apple开发人员的帐户。

要获取Apple特定的元数据，您首先需要在[https://itunesconnect.apple.com](https://itunesconnect.apple.com/)上创建应用程序。 在创建应用程序时，如果您希望使用Apple iTMSTransporter工具验证元数据并将元数据上传到itunesconnect.apple.com，则Apple将生成iOS元数据部分所需的元数据。 如果您只想获取要收集的元数据，则不必填写iOS特定的元数据。 您仍可以导出将合并iOS和常用元数据的元数据，并将所有屏幕截图收集到一个zip文件中，以便随时下载。

下载的zip文件包含一个itmsp文件，可检查该文件是否有metadata.xml。 itmsp文件包含导出的元数据（在metadata.xml文件中）以及所有相关的截屏。

导出功能用于提供收集屏幕截图和元数据的便捷方式，这些截图和元数据可以传递给应用程序发布者，以便输入到供应商特定的应用程序商店。

![chlimage_1-120](assets/chlimage_1-120.png)

#### Android 元数据 {#android-metadata}

选择Android平台时，此时没有可设置的自定义元数据。 单击下载按钮时，将生成一个属性文件，其中包含所有元数据和关联的屏幕截图。

导出功能用于提供收集屏幕截图和元数据的便捷方式，这些截图和元数据可以传递给应用程序发布者，以便输入到供应商特定的应用程序商店。

![chlimage_1-121](assets/chlimage_1-121.png)

### 内容更新服务器 URL {#content-update-server-url}

AEM Apps的一个主要功能是能够让移动应用程序通过ContentSync请求新内容，其中的内容可以是html资源、页面、视频、图像、文本等。 内容作者更新了内容，然后发布该内容后，服务器将提供内容更新供移动应用程序下载。

Content Update Server URL属性是必须指向发布实例的URL;直接或通过调度程序或CDN。 URL的格式很简单：

`https://[hostname]:[port]`

>[!NOTE]
>
>如果您的作者服务器实例正在复制到多个发布服务器实例(AEM的通用体系结构)，则每个发布服务器将具有相同的更新内容，因为更新是在作者上构建的并复制到所有发布实例。 基本上，完全支持负载平衡和故障转移。

### 插件选项卡{#the-plugins-tab}

**插件**&#x200B;选项卡描述与您的应用程序关联的插件。 此信息将用于在构建过程中检索相应的插件。

![chlimage_1-122](assets/chlimage_1-122.png)

### 屏幕截图选项卡{#the-screenshots-tab}

**屏幕截图**&#x200B;选项卡显示不同平台上支持的屏幕截图分辨率。

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>要添加和删除截图，请参阅[编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)。

### 身份验证选项卡{#the-authentication-tab}

**身份验证**&#x200B;选项卡允许您选择要与应用程序关联的OAuth客户端，并允许开发人员利用Adobe Experience Manager的OAuth身份验证。

![chlimage_1-124](assets/chlimage_1-124.png)

### 后续步骤 {#the-next-steps}

在应用程序仪表板中了解管理应用程序拼贴后，请参阅以下其他创作角色的资源：

* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [用AEM为Adobe PhoneGap企业发展](/help/mobile/developing-in-phonegap.md)
* [通过AEM为Adobe PhoneGap企业管理内容](/help/mobile/administer-phonegap.md)

