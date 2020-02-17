---
title: 创建和管理应用程序内容
seo-title: 创建和管理应用程序内容
description: 管理应用程序内容需要开发人员、内容作者和管理员的共同努力。  作者操作页面，而页面则基于模板和应用程序开发人员生成的组件。
seo-description: 管理应用程序内容需要开发人员、内容作者和管理员的共同努力。  作者操作页面，而页面则基于模板和应用程序开发人员生成的组件。
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 创建和管理应用程序内容{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

管理应用程序内容需要开发人员、内容作 [者和管理](#developer)员的 [集体努力](#author)[](#administrator)。 作者操作页面，而页面则基于模板和应用程序开发人员生成的组件。

最后，管理员战略性地发布更新的应用程序内容。

>[!NOTE]
>
>**入门项目**:
>
>在部 [署和维护中](/help/sites-deploying/deploy.md)，开发人员熟悉了AEM的组件和模板系统。

## 管理页面内容拼贴 {#the-manage-page-content-tile}

>[!CAUTION]
>
>如果您没有使用现成的应用程序模板，要启用新应用程序内容以发布OTA，您需要配置内容同步处理程序。
>
>有关更 [多详细信息，请参阅开发人员部分中的](/help/mobile/phonegap-contentsync.md) “与内容同步的移动”。

在此处，可以像在AEM Sites中一样在AEM mobile中创建、编辑和删除内容。

“管 **理页面内容”拼贴显示受管理内容的页数** ，以及为特定有效负荷上次修改的页数。 您可以通过单击拼贴中的每条记录来深入内容以创建、复制、移动、删除和更新页面。

内容更新后，管理员可以通过“管理内容包”拼贴向客户发布内容更新有效负 **荷(OTA)。**

![chlimage_1-161](assets/chlimage_1-161.png)

选择其中一个列出的内容包以创建或编辑内容，如创建、编辑或删除页面、更改导航和页面顺序、创建或更新内容(如复制（文本）和媒体)。

请注 *意，所有内容都是内容*，即应用程序样式、复制（文本）、媒体、页面、导航和内容定位都可以在OTA中编辑和更新，而无需访问应用商店。

要编辑AEM mobile内容，*AEM作者*需要对AEM的内容编辑界面有深入的了解：在 [AEM中创作页面。](/help/sites-authoring/qg-page-authoring.md)

## 管理内容包拼贴 {#the-manage-content-packages-tile}

在此， ** AEM管理员可以快速、轻松地更新其应用程序，以提供引人入胜的体验和最新内容，从而推动品牌参与并实现业务目标，而无需开发人员或应用商店重新提交。

![chlimage_1-162](assets/chlimage_1-162.png)

一旦 *AEM作者通过管理内容拼贴添加或修改了内容* , ** AEM管理员就可以将这些更改推送到包含内容包更新的客户。

“内容包”操作允许 ** AEM作者创建和编辑页面内容，同时开发团队对主机应用程序设计和实施（包括导航、样式、服务器端逻辑、模板和组件）进行更改，然后将这些更改从OTA推送给客户，而无需重新提交到各种商店进行分发。

**发布新内容或更新内容**

从拼贴中选择一个内容包，在此示例中为英语包。 注意，内容更新对话框会列出相关的 *内容同步配置* 。 如果应用程序内容自上次更新后已被修改，则状态将显示“ *待定*”，如下所示。

![chlimage_1-163](assets/chlimage_1-163.png)

接下来，选择右 **上角的** Stage操作以创建新内容更新。 添加相应的更新信息并按“完成”。

![chlimage_1-164](assets/chlimage_1-164.png)

然后， *Content Sync* （内容同步）处理函数通过形成delta(仅包含已更改内容的 *包* )来创建所需的包。 完成后，此更新内容包已分阶段，如下所示。

将内容更新暂存到内容允许在将内容发布到OTA到移动设备之前进行多次更新。

>[!NOTE]
>
>在发布之前，可以使用AEM验证应用程序验证分阶段的内容。
>
>有关AEM [Verify应用程序的更多详细信息，请参阅Mobile Quickstart for AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) 。

![chlimage_1-165](assets/chlimage_1-165.png)

当准备好使用内容同步OTA向应用程序用户交付新内容时，请选择 **发布** ，如下所示。

![chlimage_1-166](assets/chlimage_1-166.png)

### 后续步骤 {#the-next-steps}

在应用程序功能板中了解了创建和管理应用程序内容后，请参阅以下其他创作角色的资源：

* [管理应用程序拼贴](/help/mobile/phonegap-app-details-tile.md)
* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap Enterprise进行开发](/help/mobile/developing-in-phonegap.md)
* [通过AEM管理Adobe phoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
