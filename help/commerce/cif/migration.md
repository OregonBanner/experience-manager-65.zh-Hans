---
title: 迁移到AEM Commerce Integration Framework(CIF)加载项
description: 如何从旧版本迁移到AEM Commerce Integration Framework(CIF)加载项
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# {#cif-migration}Experience Manager加载项迁移指南

本指南有助于确定您需要更新哪些区域以进行Experience Manager Add-on迁移。

## CIF Add-On

CIF加载项可通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)用于AEM 6.5。 它兼容，并提供与Experience ManagerCIF附加功能相同的功能。

请参阅[AEM Content and Commerce](getting-started.md)快速入门。

为支持部署CIF的项目，Adobe提供[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。

## 产品目录

CIF加载项不支持导入产品目录数据。 使用CIF附加主体，产品和目录请求通过对外部商务解决方案的实时调用进行点播。 转到“集成”一章，了解有关集成商务解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例[Magento开放源](https://magento.com/products/magento-open-source)。

## 利用AEM Rendering实现产品目录体验

如果将目录蓝图与Classic CIF一起使用，则需要更新产品目录工作流。 CIF加载项现在使用AEM目录模板实时呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存数据和购物互动

客户端对不可缓存数据和交互（例如，添加到购物车、搜索）的请求应通过CDN/Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM仅是代理的任何调用。
