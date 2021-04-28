---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---


# Commerce Integration Framework GitHub发布概述

## 发布日期：2020年11月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2020.12.01 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-november}

* 模板继承已添加到特定类别页。 此功能提高了业务用户效率，因为它允许所有子类别继承为特定顶级类别创建的模板。

* 更新了维尼亚参考店面，以对页脚使用Experience Fragment。 商业用户可以使用AEM创作工具编辑页脚。

### {#what-is-improved-november}的改进

* 结帐组件得到改进，可让购物者能够进入目的地国家，以允许美国以外的帐单/送货地址。

* 导航组件扩展到水合物Adobe客户端数据层。

* 多个错误修复。

## 发布日期：2020年10月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2020.10.27 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-october}

* 新增了类别传送组件，使商业用户能够将此组件拖放到AEM内容页面，以用商业数据丰富内容页面。

* CIF核心组件通过发送商务数据扩展为Adobe客户端数据层的水合物。 Adobe Client Data Layer是收集数据并将数据传送到数字分析和报告服务器的标准化方法。 有关详细信息，请参阅[Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer/wiki)。

* 产品详细信息和产品列表页面已扩展，可自动填充从Magento管理员UI中配置的SEO元数据（如标题、元描述、元关键字）

* 修复了商务Teaser组件错误。

## 发布日期：2020年9月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2020.10.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-september}

* 支持Magento 2.4.0模式的查询。

* 已添加帐户信息功能，以允许购物者更新个人信息。

* 延迟加载针对产品列表和搜索结果页面实施的分页样式，以允许开发人员将这些组件配置为将“加载更多”按钮显示为分页样式。

* 已实施密码重置页面，使购物者能够更新/重置其帐户密码。

* 支持捆绑产品类型。

* 开发人员可以为产品传送、相关产品和特色类别列表组件配置HTML标记，以遵循SEO最佳实践。

* 我的帐户错误已修复。

* 多个错误修复。

## 发布日期：2020年8月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2020.9.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-august}

* 添加了痕迹导航组件以支持内容和商务页面。

* 在页面属性上添加的“商务”选项卡，用于显示登陆页和体验片段的CIF属性。

* Searchbar组件经过改进，支持显示占位符文本的选项

* 为产品和产品Teaser组件增加了灵活性，可支持轻松自定义。

* 增加了覆盖和配置产品Teaser组件默认CTA按钮标签的灵活性。

* Address Book组件得到改进，允许注册购物者在结帐期间选择保存在通讯簿中的送货和帐单地址。

* 多个错误修复。

## 发布日期：2020年7月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2020.8.14 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-july}

* CIF Venia参考站点是从CIF原型回购中提取的，现在是独立的GitHub存储库。

* CIF原型与AEM项目原型合并。 对于新项目，请使用[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)作为起点。

* 添加了通讯簿管理，以允许登录用户管理其地址。

* CIF云配置用户界面支持发布/取消发布操作。

### {#what-is-improved-july}的改进

* 登录组件已移至用户下拉框，便于访问。

* 简化了aem-core-cif-react-components包。

* 多个错误修复。

## 发布日期：2020年6月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.1.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.1.1 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-june}

这是Adobe Experience Manager支持的第一个CIF核心组件版本。

* 在“产品列表”页面和“搜索结果”页面上添加了产品排序，以允许购物者根据相关性、价格和产品名称进行排序。

* 添加了类别筛选作为彩块化，以允许购物者根据类别进行筛选。

* 增加了服务用户映射，作为安全要求的一部分，以确保通过服务用户访问/conf，而不是直接操作ACL。 CIF核心组件现在必须使用服务用户访问配置。

### {#what-is-improved-june}的改进

* 产品列表页和搜索结果页显示项目总数。 Number of items is updated when shopper applied过滤器。

* 通过将类别查询与产品搜索查询相结合，优化了彩块搜索。

* 类别/页面预览的产品选择器遵守cq:catalogPath。

* 多个错误修复。

## 发布日期：2020年5月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.0.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.0.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-may}

* 支持Magento 2.3.5模式的查询。

* 添加到搜索页面和产品列表页面的彩块化搜索支持，可让购物者根据产品彩块化筛选搜索结果。

* 为自定义用于SEO的PDP/PLP URL而添加的新OSGi服务。 有关详细信息，请参阅此[文档](https://github.com/adobe/aem-core-cif-components/wiki/configuration)。

* 在创建云配置时自动创建产品绑定。

### 改进功能

* 云配置扩展为显示“创建文件夹”操作。

* 应用了多个错误修复。

## 发布日期：2020年4月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.10.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.10.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.10.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-april}

* 统一和简化CIF连接器的配置设置。 有关更多详细信息，请查看[入门](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)或[新建AEM CIF项目设置](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html#!AdobeDocs/commerce-cif-documentation/master/getting-started/02-new-cif-project.md)

### {#what-is-improved-april}的改进

* 购物车和结帐流程扩展以支持注册购物者。

* 跨所有组件的扩展国际化支持。

* 支持分组产品和虚拟产品。

* 相关产品、产品传送和特色类别组件得到改进，可支持可选标题。

* 应用了多个错误修复。

## 发布日期：2020年2月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.9.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-february}

* 支持Magento 2.3.4模式的查询。

* 在类别选取器中添加了搜索支持。

* 类别 列表组件中的分页支持大型目录集。

### {#what-is-improved-february}的改进

* 购物车经过增强，可显示折扣。

* 产品详细信息、产品Teaser和产品列表组件支持显示高级定价信息。

* 改进了产品控制台和产品选取器中的产品搜索。

* 应用了多个错误修复。

## 发布日期：2020年1月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.7.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-january}

* 添加了体验片段(XF)组件，以使客户能够在其商务项目中创建XF。

* 更改我帐户中可用的密码功能。

* i18n支持AEM CIF服务器端核心组件。

* 可用的通用相关产品组件。

### {#what-is-improved-january}的改进

* 支持在产品teaser上显示CTA按钮。

* 用于在“特色类别”列表组件中更改/选择图像的选项。

* 用于在产品列表组件中隐藏/显示标题/横幅的选项。

* 应用于产品传送组件的拖放功能。

* 应用了多个错误修复。
