---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 8%

---

# Commerce Integration Framework GitHub发布概述

## 发布日期：2019年11月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.7.1 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以使用站点编辑器中新的“视图产品/类别”选项，将产品详细信息和产品列表页面与产品/类别预览。

* 作者可以按产品SKU标记资产，并按SKU搜索特定于产品的资产。

* 添加/删除购物车中添加的优惠券支持。

* Braintree支付支持在AEM Venia商店前面添加。

### 改进内容 {#what-is-improved-november}

* 类别/产品拾取器在多商店设置中增强为对指定的Magento商店视图的尊重。

* 以npm包形式提供的基于React的组件。 这允许开发人员将React Components包用作新React项目的依赖项，以允许自定义现有组件或开发新的基于React的组件。

* GraphQL查询定制简化。 这使开发者能够用更少的代码定制CIF核心组件。

## 发布日期：2019年10月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 产品详细信息页面和产品列表页面的完全可授权模板。 作者现在可以创建新模板，并在这些模板上拖放产品列表和产品详细信息组件。 除了添加其他组件外，作者现在还可以更改这些模板的布局，为他们提供无限的自由，创建将营销和商务内容结合在一起的出色体验。

* 所有对作者友好的CIF核心组件都得到了增强，可支持[AEM样式系统](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html)。 为产品列表组件提供了示例样式。

* 基于React的客户端组件，用于帐户管理。 此版本支持以下功能：登录、忘记密码和创建帐户。

### 改进内容 {#what-is-improved-october}

* 产品详细信息和产品列表组件已得到增强，可显示虚拟数据，以便当这些组件放置在模板/页面上时，为作者提供布局的预览。

* Minicart和Checkout组件现在使用React挂接提高了可扩展性。

## 发布日期：2019年9月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 允许作者丰富特定产品详细信息页面或产品列表页面的多模板功能。 作者可以轻松创建自定义产品详细信息页面或产品列表页面，并使用产品或类别选取器将自定义页面分配给特定产品或类别。

* 允许作者在AEM产品控制台中绑定多个目录的多目录绑定。 作者还可以在创建目录绑定后编辑和视图目录绑定属性。

* 使用GraphQL的基于客户端的结帐和Mini Cart支持完整的基本购物旅程。

* 结帐组件包括地址表单、付款选择和送货方式选择。

### 改进内容 {#what-is-improved-september}

* 产品Teaser和产品传送组件支持产品变体。

## 发布日期：2019年8月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 将CIF连接器嵌入CIF原型中是可选的，为开发者提供了更大的灵活性。

* CIF组件与“Venia”特定CSS样式分离，使开发人员能够应用他们选择的CSS样式。

* 允许在多个AEM站点结构上使用CIF核心组件的多商店/站点功能，并允许基础GraphQL客户端实现连接到不同的Magento存储/存储视图。

* 通过HTTP查询为某些GraphQLGET启用GraphQL缓存以缩短响应时间。

* 产品说明视图在AEM产品控制台中启用。

* Commerce Teaser扩展WCM Teaser组件，以允许作者还将CTA字段添加到产品详细信息页面或产品列表页面。

* 允许作者将作品放在AEM页面上并链接到AEM页面、产品详细信息页面、产品列表页面或外部链接的按钮。

### 改进内容 {#what-is-improved-august}

* Magento存储配置从OSGi移动到AEM产品控制台，以使集成设置更便于创作。

## 发布日期：2019年7月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 首款CIF原型，为开发者提供多种部署选项：1.部署AEM Venia店面2。 为新项目3部署基架。 在现有项目中使用CIF元素

* 多级目录导航可支持在类别和子类别中导航。

* 在类别页面上分页以获得更好的UX。

* 在客户端呈现产品详细信息和产品列表组件中的价格属性，以支持呈现动态属性。

* 服务器端产品传送，以传送方式显示特色产品的列表。

* 服务器端特色类别列表，用于在AEM页面上显示类别列表。

### 改进内容 {#what-is-improved-july}

* 产品控制台中显示对Magento 2.3.2的支持以及与产品属性相关的错误修复。

## 发布日期：2019年6月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.1.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面，带有移动优先的Venia CSS样式、登陆页、通过产品和类别页面进行的动态目录导航、产品搜索页面和购物车功能，可启动和加速商业项目。

* CIF连接器和创作工具(产品控制台、产品选取器和类别选取器)使作者能够在AEM中创建包含商务内容的体验。

* 与Magento 2.3.1兼容的CIF核心组件的第一版：
   * 产品详细信息
   * 产品列表
   * 产品Teaser
   * 导航
   * 产品搜索
   * 购物车(REST)

