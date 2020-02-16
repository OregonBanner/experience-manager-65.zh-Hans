---
title: 使用创建向导创建新的AEM mobile应用程序
seo-title: 使用创建向导创建新的AEM mobile应用程序
description: AEM mobile应用程序基于定义页面结构和属性的蓝图。 可查看本页以了解如何基于应用程序模板创建新应用程序。
seo-description: AEM mobile应用程序基于定义页面结构和属性的蓝图。 可查看本页以了解如何基于应用程序模板创建新应用程序。
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用创建向导创建新的AEM mobile应用程序{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

AEM mobile应用程序基于定义页面结构和属性的蓝图。 您可以配置以下应用程序属性：

* **** 标题：应用程序标题。
* **** 目标路径：存储应用程序的存储库中的位置。 保留默认值以基于应用程序名称创建路径。

* **** 名称：默认值是删除空格字符的标题属性的值。 名称在AEM中用于引用应用程序，例如，用于表示应用程序的存储库节点。
* **** 说明：应用程序的说明。
* **** 服务器URL:为应用程序提供无线(OTA)内容更新的URL。 默认值是用于创建应用程序（从externalizer服务获取）的实例的发布服务器URL。 注意，这必须是发布服务器实例，而不是需要身份验证的作者。

您还可以提供一个图像文件作为应用程序缩略图，选择要使用的PhoneGap build配置，然后选择要使用的移动应用程序分析配置。 此图像仅用作缩略图，用于在Experience Manager的移动应用程序控制台中代表您的移动应用程序。

还存在其他（可选）选项卡，用于构建云服务并将Adobe Mobile Services SDK插件集成到您的应用程序中。

* 构建：单击“管理配置”并在此处设置build.phonegap.com构建服务。 然后，您将能够从下拉菜单中选择新创建的PhoneGap构建云服务。
* 分析：单击“管理配置”，然后设 [置您的Adobe Mobile Services SDK](https://marketing.adobe.com/developer/en_US/get-started/mobile/c-measuring-mobile-applications) 云服务。 然后，您将能够从下拉列表中选择新创建的Mobile service以集成到您的移动应用程序中。

## 使用应用程序模板 {#using-app-templates}

应用程序模板提供了一种轻松的方法，可利用开发人员创建的现有设计，用于在AEM内创建新应用程序。

什么是应用程序模板？ 将它视为表示应用程序基线或基础的页面模板和组件的集合。
在基于其他应用程序的模板创建新应用程序时，您将获得一个应用程序，该应用程序的起始点代表从中创建该应用程序的应用程序。

您必须拥有现有的移动应用程序模板（或安装了应用程序模板的应用程序）才能使用此功能。

最新的AEM应用程序范例包含Geometrixx应用程序的更新版本（带有应用程序模板）。 或者，您也可以安装 [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) ，该StarterKit还提供一个模板。

创建基于应用程序模板的新应用程序的步骤：

1. 导航到AEM mobile应用程序目录：&lt;*server-url*>aem/apps.html/content/mobileapps
1. 选择 **创建** ，然后选择 **应用程序** ，如下所示

![chlimage_1-158](assets/chlimage_1-158.png)

选择AEM开发人员为您提供的应用程序模板。 请参 [阅AEM Mobile应用程序的结构](/help/mobile/phonegap-structure-an-app.md) ，以获得开发人员帮助。

![chlimage_1-159](assets/chlimage_1-159.png)

根据需要填写新应用程序的详细信息，包括（可选）更改其缩略图。 稍后可以从“管理应用程序”拼贴中 **编辑这些值** 。

![chlimage_1-160](assets/chlimage_1-160.png)

## 后续步骤 {#the-next-steps}

请参阅以下资源，进一步了解其他创作角色：

* [管理应用程序拼贴](/help/mobile/phonegap-app-details-tile.md)
* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [导入现有混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

## 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行开发](/help/mobile/developing-in-phonegap.md)
* [通过AEM管理Adobe phoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
