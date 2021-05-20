---
title: 创建和管理应用程序内容
seo-title: 创建和管理应用程序内容
description: 管理应用程序内容需要开发人员、内容作者和管理员共同努力。  作者处理页面，而页面则基于由应用程序开发人员生成的模板和组件。
seo-description: 管理应用程序内容需要开发人员、内容作者和管理员共同努力。  作者处理页面，而页面则基于由应用程序开发人员生成的模板和组件。
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# 创建和管理应用程序内容{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

管理应用程序内容需要[开发人员的集体努力](#developer)、内容[作者](#author)和[管理员](#administrator)。 作者处理页面，而页面则基于由应用程序开发人员生成的模板和组件。

最后，管理员可以战略性地发布更新的应用程序内容。

>[!NOTE]
>
>**先决条件**:
>
>在[部署和维护](/help/sites-deploying/deploy.md)中，开发人员熟悉了AEM组件和模板系统。

## 管理页面内容拼贴{#the-manage-page-content-tile}

>[!CAUTION]
>
>如果您没有使用现成的应用程序模板，则要启用要发布OTA的新应用程序内容，您需要配置内容同步处理程序。
>
>有关更多详细信息，请参阅开发人员部分中的[内容同步移动设备](/help/mobile/phonegap-contentsync.md) 。

在此，可以在AEM Mobile中创建、编辑和删除内容，其方式与在AEM Sites中的方式大致相同。

**管理页面内容拼贴**&#x200B;显示受管内容的页数，并且上次针对特定负载进行修改。 您可以通过单击拼贴中的每个记录，深入内容以创建、复制、移动、删除和更新页面。

内容更新后，管理员可以通过&#x200B;**管理内容包拼贴向客户发布内容更新有效负载(OTA)。**

![chlimage_1-161](assets/chlimage_1-161.png)

选择列出的内容包之一，以创建或编辑内容，如创建、编辑或删除页面、更改导航和页面顺序、创建或更新内容，如复制（文本）和媒体。

请注意&#x200B;*所有内容均为内容*，这意味着应用程序样式、复制（文本）、媒体、页面、导航和内容定位均可通过OTA进行编辑和更新，无需前往应用商店。

要编辑AEM Mobile内容，* AEM作者*将需要对AEM内容编辑界面有一定的了解：[在AEM中创作页面。](/help/sites-authoring/qg-page-authoring.md)

## 管理内容包拼贴{#the-manage-content-packages-tile}

在此，*AEM管理员*&#x200B;可以快速轻松地更新其应用程序，以提供引人入胜的体验和最新内容，从而提高品牌参与度并实现业务目标，而无需开发人员或应用商店重新提交。

![chlimage_1-162](assets/chlimage_1-162.png)

在&#x200B;*AEM作者*&#x200B;通过“管理内容拼贴”添加或修改内容后，*AEM管理员*&#x200B;能够通过内容包更新将这些更改推送给客户。

“内容包”操作允许&#x200B;*AEM作者*&#x200B;创建和编辑页面内容，同时开发团队对主机应用程序设计和实施（包括导航、样式、服务器端逻辑、模板和组件）进行更改，然后将这些更改从OTA推送给客户，而无需重新提交到各种商店进行分发。

**发布新内容或更新内容**

从图块中选择一个内容包，在本例中为英语包。 请注意，内容更新对话框列出了相关的&#x200B;*内容同步*&#x200B;配置。 如果应用程序内容自上次更新后已被修改，则状态将显示&#x200B;*Pending*，如下所示。

![chlimage_1-163](assets/chlimage_1-163.png)

接下来，选择创建新内容更新的右上角的&#x200B;**Stage**&#x200B;操作。 添加相应的更新信息并按“Done（完成）”。

![chlimage_1-164](assets/chlimage_1-164.png)

然后，*内容同步*&#x200B;处理程序通过形成增量（*仅*&#x200B;的包已更改）来创建所需的包。 完成后，此更新内容包已分阶段进行，如下所示。

通过暂存内容更新，可在将内容发布到OTA到移动设备之前进行多次更新。

>[!NOTE]
>
>发布之前，可以使用AEM验证应用程序验证暂存内容。
>
>有关AEM Verify应用程序的更多详细信息，请参阅[Mobile Quickstart for AEM Verify](/help/mobile/phonegap-mobile-quickstart.md)。

![chlimage_1-165](assets/chlimage_1-165.png)

准备好使用内容同步OTA向应用程序用户交付新内容时，请选择&#x200B;**发布**，如下所示。

![chlimage_1-166](assets/chlimage_1-166.png)

### 后续步骤 {#the-next-steps}

在应用程序功能板中了解了有关创建和管理应用程序内容的信息后，请参阅以下资源以了解其他创作角色：

* [管理应用程序拼贴](/help/mobile/phonegap-app-details-tile.md)
* [编辑应用程序元数据](/help/mobile/phonegap-editmetadata.md)
* [应用程序定义](/help/mobile/phonegap-app-definitions.md)
* [使用创建应用程序向导创建新应用程序](/help/mobile/phonegap-create-new-app.md)
* [导入现有混合应用程序](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [使用AEM为Adobe PhoneGap企业进行开发](/help/mobile/developing-in-phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的内容](/help/mobile/administer-phonegap.md)
