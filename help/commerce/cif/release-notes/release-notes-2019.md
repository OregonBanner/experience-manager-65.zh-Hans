---
title: AEM Content and Commerce 2019版发行说明
description: AEM Content and Commerce 2019版发行说明
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 7%

---

# Commerce Integration Framework GitHub发行版概述

## 发行日期： 2019年11月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.7.1 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.6.2 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-november}

* 作者可以在站点编辑器中通过新的“使用产品/类别查看”选项预览产品/类别的产品详细信息和产品列表页面。

* 作者可以按产品SKU标记资产并按SKU搜索产品特定的资产。

* 购物车中添加了添加/删除优惠券支持。

* AEM Venia店面中添加了Braintree支付支持。

### 改进内容 {#what-is-improved-november}

* 类别/产品选取器已增强，可遵循多商店设置中指定的Adobe Commerce商店视图。

* 基于React的组件可作为npm包使用。 这允许开发人员使用React组件包作为新React项目的依赖项，以便允许自定义现有组件或开发基于React的新组件。

* 简化了GraphQL查询自定义。 这允许开发人员使用较少的代码自定义CIF核心组件。

## 发行日期： 2019年10月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.5.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-october}

* 产品详细信息页面和产品列表页面的完全可创作模板。 作者现在可以创建新模板，并将产品列表和产品详细信息组件拖放到这些模板上。 除了添加其他组件外，作者现在还可以更改这些模板的布局，为他们提供无限制的自由，以便结合营销和商业内容创建令人惊艳的体验。

* 所有便于作者使用的CIF核心组件均已得到增强，可支持 [AEM样式系统](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). 为产品列表组件提供了示例样式。

* 用于帐户管理的基于React的客户端组件。 此版本支持以下功能：登录、忘记密码和创建帐户。

### 改进内容 {#what-is-improved-october}

* 产品详细信息和产品列表组件已增强以显示虚拟数据，以便在将这些组件放在模板/页面上时为作者提供布局预览。

* Minicart和Checkout组件现在使用React挂接来提高可扩展性。

## 发行日期： 2019年9月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.4.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-september}

* 多模板功能，允许作者扩充特定的产品详细信息页面或产品列表页面。 作者可以轻松创建自定义产品详细信息页面或产品列表页面，并使用产品或类别选取器将自定义页面分配给特定产品或类别。

* 多目录绑定，以允许作者在AEM产品控制台中绑定多个目录。 作者还可以在创建绑定后编辑和查看目录绑定属性。

* 基于React的客户端结账和迷你购物车使用GraphQL支持完整的基本购物之旅。

* 结帐组件包括地址表单、付款选择和配送方式选择。

### 改进内容 {#what-is-improved-september}

* 产品Teaser和产品轮播组件支持产品变体。

## 发行日期： 2019年8月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.3.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-august}

* 在CIF原型中嵌入CIF连接器成为了可选操作，从而为开发人员提供了更大的灵活性。

* CIF组件与特定于“Venia”的CSS样式分离，以允许开发人员应用他们选择的CSS样式。

* 多存储/站点功能，允许在多个AEM站点结构上使用CIF核心组件，并允许底层GraphQL客户端实施连接到不同的Adobe Commerce存储/存储视图。

* 为某些GraphQL查询启用了通过HTTPGET的GraphQL缓存，以减少响应时间。

* 产品描述视图已在AEM产品控制台中启用。

* Commerce Teaser扩展了WCM Teaser组件，以允许作者还将CTA字段添加到产品详细信息页面或产品列表页面。

* 按钮允许作者放置在AEM页面上并链接到AEM页面、产品详细信息页面、产品列表页面或外部链接。

### 改进内容 {#what-is-improved-august}

* Adobe Commerce存储配置已从OSGi移至AEM产品控制台，以使集成设置更便于创作。

## 发行日期： 2019年7月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.2.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-july}

* 第一个CIF原型为开发人员提供了多个部署选项： 1.部署AEM Venia storefront 2. 为新项目部署基架3. 在现有项目中使用CIF

* 多级目录导航，以支持通过类别和子类别的导航。

* 在类别页面上分页，以获得更好的UX。

* 产品详细信息和产品列表组件中价格属性的客户端渲染，以支持动态属性的渲染。

* 服务器端产品轮播，以轮播形式显示精选产品列表。

* 服务器端特色类别列表，用于在AEM页面上显示类别列表。

### 改进内容 {#what-is-improved-july}

* 产品控制台中会显示对Adobe Commerce 2.3.2的支持以及与产品属性相关的错误修复。

## 发行日期： 2019年6月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.1.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |

### 新增功能 {#what-is-new-june}

* AEM B2C店面，具有移动优先的Venia CSS样式、登陆页面、通过产品和类别页面进行的动态目录导航、产品搜索页面以及购物车功能，可快速启动和加快商业项目。

* CIF连接器和创作工具（产品控制台、产品选取器和类别选取器）使作者能够在AEM中创建包含商业内容的体验。

* 与Adobe Commerce 2.3.1兼容的CIF核心组件的第一个版本：
   * 产品详细信息
   * 产品列表
   * 产品Teaser
   * 导航
   * 产品搜索
   * 购物车(REST)
