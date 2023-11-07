---
title: AEM Content and Commerce 2020版发行说明
description: Adobe Experience Manager Content and Commerce 2020版发行说明。
exl-id: 440ecd8e-55dc-4606-8678-c65cda1d2b3a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 11%

---

# Commerce integration frameworkGitHub版本概述

## 发行日期： 2020年11月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.6.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.6.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2020.12.01 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-november}

* 模板继承已添加到特定类别页面。 此功能可提高业务用户的效率，因为所有子类别都可以继承为特定的顶级类别创建的模板。

* Venia引用店面已更新，使用体验片段作为页脚。 商业用户可以使用AEM创作工具编辑页脚。

### 改进内容 {#what-is-improved-november}

* 改进了结账组件，使购物者能够进入目标国家/地区，以允许在美国以外的账单/运送地址。

* 导航组件已扩展到水合Adobe客户端数据层。

* 多个错误修复。

## 发行日期：2020年10月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.5.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.5.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2020.10.27 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-october}

* 添加了新类别轮盘组件，以允许商业用户将此组件拖放到AEM内容页面上，以使用商业数据扩充内容页面。

* 扩展了CIF核心组件，以通过发送商业数据来水合Adobe客户端数据层。 Adobe客户端数据层是一种标准化方法，用于收集数据并将数据传递到Digital Analytics和报表服务器。 有关更多详细信息，请参阅 [Adobe客户端数据层](https://github.com/adobe/adobe-client-data-layer/wiki).

* 扩展了“产品详细信息”和“产品列表”页面，以自动填充从Adobe Commerce管理UI中配置的SEO元数据（如标题、元描述、元关键词）

* 修复了Commerce Teaser组件错误。

## 发行日期：2020年9月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.4.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.4.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2020.10.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-september}

* 支持Adobe Commerce 2.4.0架构的查询。

* 添加了帐户信息功能，以允许购物者更新个人信息。

* 为产品列表和搜索结果页面实施延迟加载分页样式，以允许开发人员配置这些组件以将“加载更多”按钮显示为分页样式。

* 实施密码重置页面以允许购物者能够更新/重置其帐户密码。

* 提供了对捆绑产品类型的支持。

* 开发人员可以为“产品轮播”、“相关产品”和“精选类别列表”组件配置HTML标记，以遵循SEO最佳实践。

* 修复了“我的帐户”错误。

* 多个错误修复。

## 发行日期：2020年8月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.3.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.3.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2020.9.2 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-august}

* 添加了痕迹导航组件以支持内容和商务页面。

* 在页面属性上添加了商务选项卡，以显示登陆页面和体验片段的CIF属性。

* 改进了Searchbar组件，以支持显示占位符文本的选项

* 为Product和Product Teaser组件增加了灵活性，以支持轻松的自定义。

* 增加了覆盖和配置Product Teaser组件的默认CTA按钮标签的灵活性。

* 通讯簿组件经过改进，允许注册购物者在结帐时选择保存在通讯簿中的送货地址和帐单地址。

* 多个错误修复。

## 发行日期：2020年7月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.2.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.2.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2020.8.14 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-july}

* CIF Venia引用站点是从CIF Archetype存储库中提取的，现在是一个独立的GitHub存储库。

* CIF原型与AEM项目原型合并。 对于新项目，请使用 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 作为起点。

* 添加了通讯簿管理，以允许登录用户管理其地址。

* CIF Cloud配置UI支持发布/取消发布操作。

### 改进内容 {#what-is-improved-july}

* 登录组件已移至用户下拉列表以方便访问。

* 简化了aem-core-cif-react-components包。

* 多个错误修复。

## 发行日期：2020年6月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.1.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.1.1 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-june}

这是Adobe Experience Manager支持的CIF核心组件的第一个版本。

* 在产品列表页面和搜索结果页面上添加了产品排序，以允许购物者根据相关性、价格和产品名称进行排序。

* 添加了类别过滤作为Facet，以允许购物者根据类别过滤。

* 添加了服务用户映射，作为安全要求的一部分，以确保通过服务用户访问/conf，而不是直接处理ACL。 CIF核心组件现在必须使用服务用户来访问配置。

### 改进内容 {#what-is-improved-june}

* “产品列表”页面和“搜索结果”页面显示项目总数。 购物者应用过滤器时更新项目数。

* 通过将类别查询与产品搜索查询结合来优化多面搜索。

* 页面预览的类别/产品选取器执行cq：catalogPath。

* 多个错误修复。

## 发行日期：2020年5月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.0.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.0.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.11.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-may}

* 支持Adobe Commerce 2.3.5架构的查询。

* “搜索页面”和“产品列表页面”中添加了Facet搜索支持，以允许购物者根据产品Facet筛选搜索结果。

* 添加了新的OSGi服务，以自定义用于SEO的PDP/PLP URL。 欲知更多详情，请参见 [文档](https://github.com/adobe/aem-core-cif-components).

* 创建云配置时，会自动创建产品绑定。

### 改进内容

* 扩展了云配置以显示“创建文件夹”操作。

* 应用了多个错误修复。

## 发行日期： 2020年4月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.10.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.10.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.10.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-april}

* 统一并简化了CIF Connector的配置设置。 有关更多详细信息，请查看 [快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html) 或 [新建AEM CIF项目设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html)

### 改进内容 {#what-is-improved-april}

* 扩大购物车和结账流程以支持注册购物者。

* 扩展了所有组件的国际化支持。

* 支持分组产品和虚拟产品。

* 改进了相关产品、产品轮播和特色类别组件，以支持可选标题。

* 应用了多个错误修复。

## 发行日期：2020年2月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.9.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-february}

* 支持Adobe Commerce 2.3.4架构的查询。

* 在类别选取器中添加了搜索支持。

* 在类别列表组件中进行分页，以支持大型目录集。

### 改进内容 {#what-is-improved-february}

* 购物车已增强以显示折扣。

* 产品详细信息、产品Teaser和产品列表组件支持显示高级定价信息。

* 改进了产品控制台和产品选取器中的产品搜索。

* 应用了多个错误修复。

## 发行日期：2020年1月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 0.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 0.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF原型 | 0.7.0 | [发行说明](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新增功能 {#what-is-new-january}

* 添加了体验片段(XF)组件，以使客户能够在其商业项目中创建XF。

* 更改我的帐户中可用的密码功能。

* i18n支持AEM CIF服务器端核心组件。

* 提供了通用相关产品组件。

### 改进内容 {#what-is-improved-january}

* 支持在产品Teaser上显示CTA按钮。

* 用于更改/选择特色类别列表组件中的图像的选项。

* 用于在产品列表组件中隐藏/显示标题/横幅的选项。

* 应用于产品轮盘组件的拖放功能。

* 应用了多个错误修复。
