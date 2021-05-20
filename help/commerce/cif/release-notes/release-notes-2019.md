---
title: AEM Content and Commerce 2021发行说明
description: AEM Content and Commerce 2021发行说明
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 7%

---

# 商务集成框架GitHub发行概述

## 发行日期：2019年11月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.7.1 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以在站点编辑器中使用新的“查看产品/类别”选项预览产品详细信息页面和产品列表页面以及产品/类别页面。

* 作者可以按产品SKU标记资产，并按SKU搜索产品特定的资产。

* 添加/删除购物车中添加的优惠券支持。

* Braintree支付支持在AEM Venia商店前端添加。

### {#what-is-improved-november}的改进内容

* 类别/产品选取器在多商店设置中增强了，以符合指定的Magento商店视图。

* 基于React的组件可作为npm包使用。 这允许开发人员将React组件包用作新React项目的依赖项，以允许自定义现有组件或开发新的基于React的组件。

* GraphQL查询自定义过程得到简化。 这允许开发人员使用更少的代码自定义CIF核心组件。

## 发行日期：2019年10月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 产品详细信息页面和产品列表页面的完全可授权的模板。 作者现在可以创建新模板，并将产品列表和产品详细信息组件拖放到这些模板上。 除了添加其他组件之外，作者现在还可以更改这些模板的布局，从而无限制地为它们创建结合营销和商务内容的精彩体验。

* 所有对作者友好的CIF核心组件均已得到增强，可支持[AEM样式系统](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)。 为产品列表组件提供了示例样式。

* 用于帐户管理的基于React的客户端组件。 此版本支持以下功能：登录、忘记密码和创建帐户。

### {#what-is-improved-october}的改进内容

* 产品详细信息和产品列表组件已得到增强，可显示虚拟数据，以便当这些组件放置在模板/页面上时，为作者提供布局预览。

* 迷你卡和结账组件现在使用React挂接以提高可扩展性。

## 发行日期：2019年9月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 多模板功能，允许作者扩充特定产品详细信息页面或产品列表页面。 作者可以轻松创建自定义产品详细信息页面或产品列表页面，并使用产品或类别选取器将自定义页面分配给特定产品或类别。

* 多目录绑定，以允许作者在AEM产品控制台中绑定多个目录。 在创建绑定后，作者还可以编辑和查看目录绑定属性。

* 使用GraphQL的基于React的客户端结账和迷你购物车支持完整的基本购物历程。

* 结帐组件包括地址表单、付款选择和发运方法选择。

### {#what-is-improved-september}的改进内容

* 产品Teaser和产品轮播组件支持产品变体。

## 发行日期：2019年8月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 在CIF原型中嵌入CIF连接器使得可以选择为开发人员提供更大的灵活性。

* CIF组件与“Venia”特定CSS样式相分离，以允许开发人员应用其选择的CSS样式。

* 多存储/站点功能，允许在多个AEM站点结构上使用CIF核心组件，并且允许底层的GraphQL客户端实施连接到不同的Magento存储/存储视图。

* 通过HTTPGET为某些GraphQL查询启用了GraphQL缓存，以缩短响应时间。

* 在AEM产品控制台中启用了产品描述视图。

* Commerce Teaser扩展WCM Teaser组件，以允许作者还将CTA字段添加到产品详细信息页面或产品列表页面。

* 用于允许作者在AEM页面上放置并链接到AEM页面、产品详细信息页面、产品列表页面或外部链接的按钮。

### {#what-is-improved-august}的改进内容

* Magento存储配置已从OSGi移至AEM产品控制台，以使集成设置对作者更友好。

## 发行日期：2019年7月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 第一个CIF原型，为开发人员提供多个部署选项：1.部署AEM Venia店面2. 为新项目3部署基架。 在现有项目中使用CIF元素

* 多级别目录导航，支持在类别和子类别中进行导航。

* 在类别页面上分页，以提高UX效率。

* 在产品详细信息和产品列表组件中渲染价格属性的客户端，以支持渲染动态属性。

* 服务器端产品轮播以轮播样式显示特色产品列表。

* 服务器端特色类别列表，在AEM页面上显示类别列表。

### {#what-is-improved-july}的改进内容

* 支持Magento2.3.2，并且产品控制台中会显示与产品属性相关的错误修复。

## 发行日期：2019年6月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.1.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面，带有移动优先Venia CSS样式、登陆页面、通过产品和类别页面进行动态目录导航、产品搜索页面以及购物车功能，以启动和加速商务项目。

* CIF连接器和创作工具（产品控制台、产品选取器和类别选取器）使作者能够在AEM中创建包含商务内容的体验。

* 与Magento2.3.1兼容的CIF核心组件的第一版：
   * 产品详细信息
   * 产品列表
   * Product Teaser
   * 导航
   * 产品搜索
   * 购物车(REST)

