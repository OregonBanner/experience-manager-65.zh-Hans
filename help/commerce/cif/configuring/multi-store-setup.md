---
title: Commerce多商店设置
description: 了解如何将多个商店视图从Adobe Commerce映射到AEM。 这允许项目支持多租户和多语言用例。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Commerce多商店设置 {#multi-store}

AEM CIF核心组件可用于多个AEM站点结构，并且底层GraphQL客户端实施可以连接到不同的Adobe Commerce商店/商店视图。 这允许项目实施复杂的多存储/多站点设置。

视频演练，详细介绍用于将多个Adobe Commerce Store视图与Adobe Experience Manager Sites集成的选项。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy和Language Copy的AEM多站点管理功能与Commerce Integration Framework一起使用，以全局方式跨区域和区域管理站点。

建议的设置是在AEM网站与Adobe Commerce商店视图之间使用1:1关系。

要将AEM站点和AEM CIF核心组件也连接到专用存储视图，请执行以下步骤：

## 配置 {#configuration}

1. 根据中所述的模式配置多个商店和商店视图 [Adobe Commerce网站、商店和视图](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. 确保AEM与Adobe Commerce之间的连接正常。

3. 按照以下步骤创建CIFCloud Service配置的子配置：

   * 在AEM中，转到“工具”>“常规”> [配置浏览器](/help/sites-administering/configurations.md#using-configuration-browser)
   * 选择您创建的基本配置
   * 使用上述第2点所述的步骤创建配置

   此新配置是作为基础配置的子配置创建的。 您现在可以转到工具>常规>配置浏览器并创建配置设置。

   >[!TIP]
   >
   >商业目录可以使用ID或UID来寻址。 Adobe Commerce 2.4.2中引入了UID。仅当您的Commerce后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。

4. 将子配置分配给AEM站点

   * 转到AEM Sites控制台
   * 导航到站点结构的区域或语言根，例如/content/venia/us _或_ /content/venia/us/en用于Venia示例页面
   * 选择页面并打开页面属性
   * 选择高级选项卡
   * 在 `Configuration` 部分，选择您在步骤中创建的配置

## 其他资源

* [Adobe Commerce网站、商店和视图](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [AEM CIF核心组件 — 多存储/站点配置](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [使用多站点管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重用内容：多站点管理器和 Live Copy](/help/sites-administering/msm.md)
