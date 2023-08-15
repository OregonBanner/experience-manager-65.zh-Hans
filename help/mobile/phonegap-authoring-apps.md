---
title: 创作移动设备应用程序
description: AEM Mobile Dashboard允许您创建、构建和部署移动应用程序，以及创建、删除和编辑应用程序元数据。 关注此页面以了解更多信息。
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# 创作移动设备应用程序{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

AEM Mobile功能板允许您创建、构建和部署移动应用程序，以及创建、删除和编辑应用程序元数据。 应用程序上线后，您可以分析应用程序分析（包括生命周期和使用量度），以提高客户转化率和品牌忠诚度。

要构建AEM Mobile应用程序，请参阅 [构建移动应用程序](/help/mobile/building-app-mobile-phonegap.md) 页面。

要设置环境并开始操作，请参阅 [管理AEM以使用AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## AEM Mobile应用程序目录 {#the-aem-mobile-apps-catalog}

此 [AEM Mobile应用程序目录](http://localhost:4502/aem/apps.html/content/phonegap) 显示在AEM中管理的所有移动设备应用程序。

将此目录视为AEM Mobile的“登录页面”，管理员可以在其中通过基于模板创建或上传已由移动设备开发人员启动的现有应用程序来启动新的AEM Mobile应用程序。

按照以下步骤转到应用程序目录登陆页面：

1. 浏览至 **导航** 然后选择 **移动设备**.

1. 选择 **应用程序** 以打开应用程序目录。

![AEM Mobile应用程序目录](assets/chlimage_1-135.png)

## AEM Mobile应用程序功能板 {#the-aem-mobile-app-dashboard}

从目录中选择AEM Mobile应用程序会显示其功能板。 在这里，您可以管理应用程序、查看统计数据、生成、部署和管理移动设备应用程序内容。

您可以展开到AEM Mobile功能板中的每个图块，以通过单击右下角的“……”来查看或编辑详细信息。

![AEM Mobile应用程序指挥中心](assets/chlimage_1-136.png)

### “管理应用程序”拼贴 {#the-manage-app-tile}

“管理应用程序拼贴”显示您的应用程序图标、名称、描述、支持的平台、呼叫总部以获取更新URL和版本信息。 您可以钻取到此拼贴，以编辑和维护PhoneGap应用程序配置(config.xml)，并准备应用程序以提交到各种应用程序存储区以供分发。

单击 [此处](/help/mobile/phonegap-app-details-tile.md) 以了解详细信息。

![chlimage_1-137](assets/chlimage_1-137.png)

### “管理页面内容”拼贴 {#the-manage-page-content-tile}

您可以在AEM Mobile中创建、更新和删除内容，其方式与在AEM Sites中执行相同操作的方式非常相似。 此 **“管理页面内容”拼贴** 显示托管内容和上次修改的页数。 您可以通过单击图块中的每个记录，深入查看内容以创建、复制、移动、删除和更新页面。 更新内容后，您可以通过以下方式将内容更新推送给客户 **“管理内容包”图块。**

![内容拼贴](assets/chlimage_1-138.png)

### “管理内容包”图块 {#the-manage-content-packages-tile}

在通过“管理页面内容”拼贴添加或修改内容后，您能够通过内容版本更新将这些更改推送到客户。

内容包允许AEM应用程序作者管理AEM中的页面内容，并让开发团队对您的PhoneGap Shell应用程序（即应用程序框架或基础架构）进行更改，然后快速将这些更改推送到您的客户，而无需招募开发人员重新提交到各个商店进行分发。

内容包会为每次更新创建一个ZIP文件（被视为内容发布包）。 这些包包含在呈现应用程序时生成的html资源和html页面，并且足够智能，可仅打包自上次更新以来修改过的文件。

“管理内容包”拼贴的 **类型** 列显示“应用程序”以表示应用程序Shell内容，例如开发人员管理的应用程序的框架或基础结构，或者显示“内容”，表示内容作者管理的页面内容。

内容可以表示为语言，也可以表示为应用程序的一个特定部分，应用程序在该部分中使用了多个内容发行包。 您如何捆绑内容的选择是灵活的，并且完全取决于您希望如何管理应用程序的内容。

此 **修改时间** 列指示页面最近修改的时间。

此 **已暂存** 列显示上次创建内容更新的时间。 要创建内容更新并暂存更改，请打开拼贴中的任何记录并创建更新。

此 **已发布** 列显示上次内容更新的发布时间和可供客户使用的时间。 要发布内容，您必须先暂存该内容，然后通过钻取此图块并从“内容发布详细信息”控制台发布来发布更新。

![“内容发布”拼贴](assets/chlimage_1-139.png) ![应用程序外壳的ContentSync包](do-not-localize/chlimage_1-5.png)

此图标表示应用程序Shell的内容发行包

![内容发布包图标，由两个重叠的正方形包符号指示。](do-not-localize/chlimage_1-6.png)

这些图标表示应用程序内容的内容发行包

### PhoneGap Build拼贴 {#the-phonegap-build-tile}

此 **PhoneGap Build拼贴** 连接 `https://build.phonegap.com` 构建和托管远程内部版本。 构建后，该内部版本可作为下载使用，或通过二维码直接提供给您的设备。

或者，您可以下载设备源，以通过PhoneGap CLI在本地构建(`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`)。

![PhoneGap Build拼贴](assets/chlimage_1-140.png)

### “量度”图块 {#the-metrics-tile}

>[!CAUTION]
>
>只有在配置云服务后，才会显示量度图块。
>
>请参阅 [配置AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 以了解详细信息。

AEM Mobile通过以下方式与Adobe Analytics集成 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS)。

控制中心 **“量度”图块** 显示从AMS为您的应用程序拉取的摘要分析。 您可以通过单击右下角的“……”深入到分析功能板。

![“量度”图块](assets/chlimage_1-141.png)

### 管理实体内容拼贴 {#the-manage-entity-content-tile}

通过“管理实体内容”拼贴，您可以添加和管理应用程序定义。 通过应用程序定义，可确定哪些空间（和其他配置）适合应用程序。 这样，可以添加新的空间，而无需重新编译应用程序。 应用程序定义已更新，其中包括任何新空间的信息。

单击 [此处](/help/mobile/phonegap-app-definitions.md) 创建和管理应用程序定义。

您可以通过单击右下角的“……”深入到管理实体内容功能板。

![chlimage_1-142](assets/chlimage_1-142.png)

#### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
