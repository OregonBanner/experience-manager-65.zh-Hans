---
title: 使用创建向导创建新的AEM Mobile应用程序
seo-title: Creating a new AEM Mobile app using create wizard
description: AEM Mobile应用程序基于定义页面结构和属性的Blueprint。 关注此页面，了解如何基于应用程序模板创建新应用程序。
seo-description: AEM Mobile apps are based on a blueprint that defines a page structure and properties. Follow this page to learn about how to create a new app based on an app template.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 使用创建向导创建新的AEM Mobile应用程序{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM Mobile应用程序基于定义页面结构和属性的Blueprint。 您可以配置以下应用程序属性：

* **标题：** 应用程序标题。
* **目标路径：** 存储库中存储应用程序的位置。 保留默认值以根据应用程序名称创建路径。

* **名称：** 默认值为删除了空格字符的Title属性的值。 该名称在AEM中用于引用应用程序，例如表示该应用程序的存储库节点。
* **描述：** 应用程序的描述。
* **服务器URL：** 为应用程序提供Over-the-Air (OTA)内容更新的URL。 默认值为用于创建应用程序的实例的发布服务器URL（取自外部化器服务）。 注意，这必须是发布服务器实例，而不是需要身份验证的作者。

您还可以提供用作应用程序缩略图的图像文件，选择要使用的PhoneGap Build配置，然后选择要使用的移动设备应用程序分析配置。 此图像仅用作缩略图，在Experience Manager的移动应用程序控制台中表示您的移动应用程序。

存在用于构建Cloud Service和将AdobeMobile Services SDK插件集成到应用程序中的其他（和可选）选项卡。

* 构建：单击管理配置并在此处设置您的build.phonegap.com构建服务。 然后，您可以从下拉菜单中选择新创建的PhoneGap Build云服务。
* Analytics：单击管理配置并设置您的 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) 云服务。 然后，您可以从下拉菜单中选择新创建的移动服务以集成到移动应用程序中。

## 使用应用程序模板 {#using-app-templates}

应用程序模板提供了一种简单的方式来利用开发人员创建的现有设计，这些设计用于在AEM中创建新的应用程序。

什么是应用程序模板？ 可将其视为页面模板和组件的集合，这些模板和组件表示应用程序的基线或基础。
在基于其他应用程序的模板创建新应用程序时，您将获得一个应用程序，其起点代表从中创建该应用程序的应用程序。

您必须拥有现有的移动设备应用程序模板（或已安装的应用程序具有应用程序模板），才能使用此功能。

最新的AEM应用程序示例包中包含带应用程序模板的Geometrixx应用程序的更新版本。 或者，您可以安装 [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) 其中还提供了模板。

基于应用程序模板创建新应用程序的步骤：

1. 导航到AEM Mobile应用程序目录： &lt;*server-url*>aem/apps.html/content/mobileapps
1. 选择 **创建** 然后选择 **应用程序** 如下所示

![chlimage_1-158](assets/chlimage_1-158.png)

选择AEM开发人员为您提供的应用程序模板。 参见 [AEM Mobile应用程序的结构](/help/mobile/phonegap-structure-an-app.md) 开发人员帮助。

![chlimage_1-159](assets/chlimage_1-159.png)

根据需要填写新应用程序的详细信息，包括选择性地更改其缩略图图像。 稍后可以从以下位置编辑这些值 **管理应用程序** 图块。

![chlimage_1-160](assets/chlimage_1-160.png)

## 后续步骤 {#the-next-steps}

请参阅以下资源，了解有关其他创作角色的更多信息：

* [“管理应用程序”拼贴](/help/mobile/phonegap-app-details-tile.md)
* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [导入现有的混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM开发Adobe PhoneGap Enterprise](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
