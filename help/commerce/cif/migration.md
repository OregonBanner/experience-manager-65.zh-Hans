---
title: 迁移到AEM Commerce Integration Framework(CIF)附加组件
description: 如何从旧版本迁移到AEM Commerce Integration Framework(CIF)加载项
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# {#cif-migration}Experience Manager加载项的迁移指南

本指南可帮助确定您需要更新哪些区域才能进行Experience Manager附加组件迁移。

## CIF附加组件

CIF附加组件可通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)获取，用于AEM 6.5。 它兼容，并且提供与CIF附加组件相同的功能，以便与Cloud ServiceExperience Manager。

请参阅[AEM Content and Commerce快速入门](getting-started.md)。

为支持部署CIF的项目，Adobe提供了[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。

## 产品目录

CIF附加组件不支持导入产品目录数据。 使用CIF附加承担者，产品和目录请求会通过对外部商务解决方案的实时调用进行按需调用。 转到章节集成，了解有关集成商务解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用包含API的外部产品缓存进行集成。 示例[Magento开源](https://magento.com/products/magento-open-source)。

## 具有AEM渲染的产品目录体验

如果将目录Blueprint与Classic CIF结合使用，则需要更新产品目录工作流。 CIF附加组件现在可使用AEM目录模板即时呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存数据与购物互动

对于不可缓存的数据和交互（例如，添加到购物车、搜索）的客户端请求应通过CDN/Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM只是代理的任何调用。
