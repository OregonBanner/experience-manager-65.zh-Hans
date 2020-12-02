---
title: 创作移动应用程序
seo-title: 创作移动应用程序
description: aem mobile仪表板允许您创建、构建和部署移动应用程序、创建、删除和编辑应用程序元数据。 可查看本页以了解更多信息。
seo-description: aem mobile仪表板允许您创建、构建和部署移动应用程序、创建、删除和编辑应用程序元数据。 可查看本页以了解更多信息。
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---


# 创作移动应用程序{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM Mobile仪表板允许您创建、构建和部署移动应用程序、创建、删除和编辑应用程序元数据。 应用程序上线后，您可以分析应用程序分析，包括生命周期和使用量度，以提高客户转化率和品牌忠诚度。

要构建您的AEM Mobile应用程序，请参阅[构建移动应用程序](/help/mobile/building-app-mobile-phonegap.md)页。

要设置环境并开始，请参阅[管理AEM以使用AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md)。

## AEM Mobile应用程序目录{#the-aem-mobile-apps-catalog}

[AEM Mobile应用程序目录](http://localhost:4502/aem/apps.html/content/phonegap)显示您在AEM中管理的所有移动应用程序。

将此目录看作是AEM Mobile的“登陆页”，在该目录中，管理员可以通过基于模板创建新的AEM Mobile应用程序或上传移动开发人员已启动的现有应用程序来开始新的应用程序。

请按照以下步骤操作，转到应用程序目录登陆页:

1. 浏览至&#x200B;**导航**，然后选择&#x200B;**移动**。

1. 选择&#x200B;**应用程序**&#x200B;以打开应用程序目录。

![AEM Mobile应用程序目录](assets/chlimage_1-135.png)

## AEM Mobile应用程序仪表板{#the-aem-mobile-app-dashboard}

从目录中选择一个AEM Mobile应用程序将显示其仪表板。 您可以在此处管理应用程序、视图统计、构建、部署和管理移动应用程序内容。

您可以扩展到AEM Mobile仪表板中的每个拼贴，以视图或编辑详细信息，方法是单击“...” 在右下角。

![AEM Mobile应用指挥中心](assets/chlimage_1-136.png)

### 管理应用程序磁贴{#the-manage-app-tile}

管理应用程序拼贴显示您的应用程序图标、名称、说明、支持的平台、呼叫主页以获取更新URL和版本信息。 您可以进入此拼贴以编辑和维护PhoneGap应用程序配置(config.xml)，并准备将应用程序提交到各种应用程序商店进行分发。

单击[此处](/help/mobile/phonegap-app-details-tile.md)获取详细信息。

![chlimage_1-137](assets/chlimage_1-137.png)

### 管理页面内容拼贴{#the-manage-page-content-tile}

在AEM Mobile创建、更新和删除内容的方式与在AEM Sites相同。 **管理页面内容拼贴**&#x200B;显示托管内容和上次修改时间的页数。 您可以通过单击拼贴中的每条记录，进入内容以创建、复制、移动、删除和更新页面。 内容更新后，您可以通过&#x200B;**管理内容包拼贴向客户推送内容更新。**

![内容拼贴](assets/chlimage_1-138.png)

### 管理内容包拼贴{#the-manage-content-packages-tile}

通过管理页面内容拼贴添加或修改内容后，您便可以通过内容发布更新将这些更改推送给客户。

内容包允许AEM应用程序作者管理AEM中的页面内容，并让开发团队对您的PhoneGap Shell应用程序（即应用程序框架或基础架构）进行更改，然后快速将这些更改推送给客户，无需征募开发人员重新提交到各种商店进行分发。

内容包会为每个更新创建一个ZIP文件（被视为内容发布包）。 这些包包含在渲染应用程序时生成的html资源和html页面，并且智能程度足够高，只能打包那些自上次更新后修改过的文件。

管理内容包拼贴的&#x200B;**Type**&#x200B;列将显示“App”以表示应用程序Shell内容，例如由开发人员管理的应用程序的框架或基础架构，或表示由内容作者管理的页面内容的“Content”。

内容可以表示为一种语言，或表示为应用程序的特定部分，在该应用程序中会使用多个内容发布包。 如何捆绑内容的选择设计为灵活且完全取决于您希望如何管理应用程序的内容。

**Modified**&#x200B;列指示页面最近修改的时间。

**已暂存**&#x200B;列显示上次内容更新的创建时间。 要创建新内容更新并暂存更改，请打开拼贴中的任何记录并创建新更新。

**已发布**&#x200B;列显示上次内容更新何时发布并可供客户使用。 要发布内容，您必须先暂存该内容，然后通过钻取此拼贴并从“内容发布详细信息”控制台发布更新。

![应用程](assets/chlimage_1-139.png) ![序Shell的内容发布TileContentSync包](do-not-localize/chlimage_1-5.png)

此图标表示应用程序Shell的内容发布包

![](do-not-localize/chlimage_1-6.png)

这些图标表示应用程序内容的内容发布包

### PhoneGap Build磁贴{#the-phonegap-build-tile}

**PhoneGap Build磁贴**&#x200B;与[https://build.phonegap.com](https://build.phonegap.com)连接以构建和承载远程Buid。 构建后，内部版本可供下载，也可通过QR码直接下载到设备。

或者，您也可以通过[PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html)下载设备源以本地构建。

![PhoneGap Build拼贴](assets/chlimage_1-140.png)

### 度量磁贴{#the-metrics-tile}

>[!CAUTION]
>
>“度量”拼贴仅在您配置云服务后显示。
>
>有关详细信息，请参阅[配置AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md)。

AEM Mobile通过[Adobe移动服务SDK](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html)(AMS)与Adobe Analytics进行集成。

控制中心&#x200B;**度量标题**&#x200B;显示从AMS中为您的应用程序提取的摘要分析。 您可以通过单击“...”进入分析仪表板 在右下角。

![度量拼贴](assets/chlimage_1-141.png)

### 管理实体内容拼贴{#the-manage-entity-content-tile}

管理实体内容拼贴允许您添加和管理应用程序定义。 应用程序定义是一种确定哪些空间（和其他配置）适合应用程序的方法。 这样，无需重新编译应用程序即可添加新空间。 应用程序定义将更新，其中将包含任何新空间的信息。

单击[此处](/help/mobile/phonegap-app-definitions.md)可创建和管理您的应用程序定义。

单击“...”可进入管理实体内容仪表板 在右下角。

![chlimage_1-142](assets/chlimage_1-142.png)

#### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [用AEM为Adobe PhoneGap企业发展](/help/mobile/developing-in-phonegap.md)
* [通过AEM为Adobe PhoneGap企业管理内容](/help/mobile/administer-phonegap.md)

