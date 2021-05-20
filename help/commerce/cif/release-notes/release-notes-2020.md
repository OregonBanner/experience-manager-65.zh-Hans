---
title: AEM Content and Commerce 2021发行说明
description: AEM Content and Commerce 2021发行说明
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---


# 商务集成框架GitHub发行概述

## 发行日期：2020年11月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2020.12.01 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-november}

* 模板继承已添加到特定类别页面。 此功能可提高业务用户效率，因为它允许所有子类别继承为特定顶级类别创建的模板。

* 更新了维尼亚引用店面，以在页脚中使用体验片段。 企业用户可以使用AEM创作工具编辑页脚。

### {#what-is-improved-november}的改进内容

* 改进了结帐组件，使购物者能够进入目标国家/地区，以允许美国以外的帐单/送货地址。

* 导航组件扩展到水合物Adobe客户端数据层。

* 修复了多个错误。

## 发行日期：2020年10月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2020.10.27 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-october}

* 新增了类别轮播组件，使企业用户能够将此组件拖放到AEM内容页面上，以使用商务数据扩充内容页面。

* CIF核心组件通过发送商务数据来扩展，以补充Adobe客户端数据层。 Adobe客户端数据层是一种收集数据并将数据传输到数字分析和报告服务器的标准化方法。 有关更多详细信息，请参阅[Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer/wiki)。

* 扩展了产品详细信息页面和产品列表页面，用于自动填充从Magento管理UI中配置的SEO元数据（例如标题、元描述、元关键字）

* 修复了商务Teaser组件错误。

## 发行日期：2020年9月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2020.10.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-september}

* 支持对Magento2.4.0架构的查询。

* 添加了帐户信息功能，允许购物者更新个人信息。

* 为产品列表和搜索结果页面实施的延迟加载分页样式，以允许开发人员将这些组件配置为将“加载更多”按钮显示为分页样式。

* 密码重置页面已实施，以便购物者能够更新/重置其帐户密码。

* 支持捆绑的产品类型。

* 开发人员可以为产品轮播、相关产品和特色类别列表组件配置HTML标记，以遵循SEO最佳实践。

* 我的帐户错误已修复。

* 修复了多个错误。

## 发行日期：2020年8月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2020.9.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-august}

* 添加了痕迹导航组件以支持内容和商务页面。

* 在页面属性中添加了商务选项卡，以显示登陆页面和体验片段的CIF属性。

* 改进了Searchbar组件以支持显示占位符文本的选项

* 为产品和产品Teaser组件增加了灵活性，可支持轻松的自定义。

* 增加了覆盖和配置Product Teaser组件默认CTA按钮标签的灵活性。

* 改进了通讯簿组件，以允许注册购物者在结帐期间选择保存在通讯簿中的送货地址和帐单地址。

* 修复了多个错误。

## 发行日期：2020年7月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2020.8.14 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-july}

* CIF Venia参考站点是从CIF原型存储库中提取的，现在是一个独立的GitHub存储库。

* CIF原型与AEM项目原型合并。 对于新项目，请使用[AEM项目原型](https://github.com/adobe/aem-project-archetype)作为起点。

* 添加了通讯簿管理，以允许已登录用户管理其地址。

* CIF云配置UI支持发布/取消发布操作。

### {#what-is-improved-july}的改进内容

* 登录组件已移至用户下拉列表，以便轻松访问。

* 简化了aem-core-cif-react-components包。

* 修复了多个错误。

## 发行日期：2020年6月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.1.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.1.1 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-june}

这是Adobe Experience Manager支持的CIF核心组件的第一个版本。

* 在“产品列表”页面和“搜索结果”页面上添加了产品排序，以允许购物者根据相关性、价格和产品名称进行排序。

* 添加了类别过滤作为一个方面，以允许购物者根据类别进行过滤。

* 添加了服务用户映射作为安全要求的一部分，以确保通过服务用户而不是直接处理ACL来访问/conf。 CIF核心组件现在必须使用服务用户来访问配置。

### {#what-is-improved-june}的改进内容

* “产品列表”页和“搜索结果”页显示项目总数。 购物者应用过滤器时，项目数会更新。

* 通过将类别查询与产品搜索查询组合在一起，优化了多面搜索。

* 用于页面预览的类别/产品选取器遵循cq:catalogPath。

* 修复了多个错误。

## 发行日期：2020年5月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.0.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.0.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-may}

* 支持对Magento2.3.5架构的查询。

* 向搜索页面和产品列表页面添加了多面搜索支持，以允许购物者根据产品彩块化过滤搜索结果。

* 添加了新的OSGi服务，用于自定义用于SEO的PDP/PLP URL。 有关更多详细信息，请参阅此[文档](https://github.com/adobe/aem-core-cif-components/wiki/configuration)。

* 在创建云配置时自动创建产品绑定。

### 改进内容

* 云配置扩展为显示“创建文件夹”操作。

* 应用了多个错误修复。

## 发行日期：2020年4月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.10.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.10.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.10.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-april}

* 统一和简化CIF连接器的配置设置。 有关更多详细信息，请参阅[快速入门](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)或[新建AEM CIF项目设置](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html#!AdobeDocs/commerce-cif-documentation/master/getting-started/02-new-cif-project.md)

### {#what-is-improved-april}的改进内容

* 购物车和结账流程已扩展，可支持注册购物者。

* 扩展了所有组件的国际化支持。

* 支持分组产品和虚拟产品。

* 经过改进的相关产品、产品轮播和特色类别组件支持可选标题。

* 应用了多个错误修复。

## 发行日期：2020年2月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.9.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-february}

* 支持对Magento2.3.4架构的查询。

* 在类别选取器中添加了搜索支持。

* 在类别列表组件中分页以支持大目录集。

### {#what-is-improved-february}的改进内容

* 购物车增强了显示折扣。

* 产品详细信息、产品Teaser和产品列表组件支持显示高级定价信息。

* 改进了产品控制台和产品选取器中的产品搜索。

* 应用了多个错误修复。

## 发行日期：2020年1月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.7.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-january}

* 体验片段(XF)组件，用于使客户能够在其商务项目中创建体验片段。

* 更改我帐户中可用的密码功能。

* i18n支持AEM CIF服务器端核心组件。

* 提供通用相关产品组件。

### {#what-is-improved-january}的改进内容

* 支持在产品Teaser上显示CTA按钮。

* 用于更改/选择特色类别列表组件中图像的选项。

* 在产品列表组件中隐藏/显示标题/横幅的选项。

* 拖放功能。

* 应用了多个错误修复。
