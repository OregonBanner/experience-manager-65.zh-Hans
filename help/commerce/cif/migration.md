---
title: 迁移到AEMCommerce integration framework(CIF)加载项
description: 如何从旧版本迁移到AEMCommerce integration framework(CIF)加载项。
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 4%

---

# Experience Manager加载项的迁移指南 {#cif-migration}

本指南帮助确定您需要为Experience Manager加载项迁移更新的区域。

## CIF加载项

AEM 6.5的CIF加载项可通过以下方式使用： [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 它是兼容的，提供了与用于Experience Manageras a Cloud Service的CIF加载项相同的功能。

请参阅 [AEM Content and Commerce快速入门](getting-started.md).

为了支持部署CIF的项目，Adobe提供了 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components).

## 产品目录

CIF加载项不支持导入产品目录数据。 使用CIF附加组件主体，可以通过实时调用外部商业解决方案来按需请求产品和目录。 转到集成一章，了解有关集成商业解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例 [Magento开源](https://business.adobe.com/products/magento/open-source.html).

## 具有AEM渲染的产品目录体验

如果您将目录Blueprint与Classic CIF一起使用，则需要更新产品目录工作流程。 CIF加载项现在可使用AEM目录模板动态呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存的数据和购物交互

对不可缓存的数据和交互的客户端请求（例如添加到购物车、搜索）应通过CDN/Dispatcher直接转到商业端点（商业解决方案或集成层）。 删除AEM只是代理的任何调用。
