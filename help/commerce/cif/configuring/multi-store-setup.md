---
title: 商务多商店设置
description: 了解如何将多个商店视图从Magento映射到AEM。 这允许项目支持多租户和多语言用例。
sub-product: 商务
doc-type: technical-video
activity: setup
audience: administrator
feature: 商务集成框架
kt: 3046
thumbnail: 28952.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# 商务多商店设置{#multi-store}

AEM CIF核心组件可用于多个AEM站点结构，并且基础GraphQL客户端实施可以连接到不同的Magento存储/存储视图。 这允许项目实施复杂的多存储/多站点设置。

一个视频演练，详细介绍用于将多个Magento商店视图与Adobe Experience Manager Sites集成的选项。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM Live Copy和语言副本的多站点管理功能与商务集成框架结合使用，以全局管理跨区域和区域设置的站点。

建议的设置是在AEM网站与Magento存储视图之间使用1:1的关系。

要将AEM网站和AEM CIF核心组件连接到专用商店视图，请执行以下步骤：

## 配置 {#configuration}

1. 根据[Magento网站、商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)中描述的模式配置多个商店和商店视图

2. 确保AEM和Magento之间的连接正常工作。

3. 按照以下步骤创建CIFCloud Service配置的子配置：

   * 在AEM中，转到Tools -> General -> [Configuration Browser](/help/sites-administering/configurations.md#using-configuration-browser)
   * 选择您创建的基本配置
   * 使用上面第2点所述的步骤创建新配置

   此新配置将创建为基配置的子配置。 您现在可以转到“工具” — >“常规” — >“配置浏览器”并创建配置设置。

   >[!TIP]
   >
   > 可以使用ID或UID来寻址商务目录。 在Magento2.4.2中引入了UID。仅当商务后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。

4. 将子配置分配给AEM站点

   * 转到AEM Sites控制台
   * 导航到站点结构的区域或语言根，例如Venia示例页面的/content/venia/us _或_ /content/venia/us/en
   * 选择页面并打开页面属性
   * 选择高级选项卡
   * 在`Configuration`部分中，选择您在步骤中创建的配置

## 其他资源

* [Magento网站、商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心组件 — 多商店/站点配置](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多站点管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重用内容：多站点管理器和Live Copy](/help/sites-administering/msm.md)
