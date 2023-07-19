---
title: Adobe Experience Manager Content and Commerce 2021版发行说明
description: Adobe Experience Manager Content and Commerce 2021版发行说明
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 13%

---

# Commerce Integration Framework GitHub发行版概述

## 系统要求概述

查看下表中当前使用或计划将来使用的CIF版本的最低系统要求。

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF加载项 | 最低配置：Adobe Experience Manager (AEM) 6.5.7、Adobe Commerce 2.3.5 GraphQL架构 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期： 2021年11月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.11.18.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF核心组件 | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia引用站点 | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### 新增功能 {#what-is-new-november}

* 基于 Commerce 的可扩展 Peregrine 组件的扩展 myAccount 组件

![扩展 myAccount 组件](/help/assets/CIF/extended-myAccount-components.png)

* 作者可以使用其他推荐类型来创建临时 Commerce 产品推荐

* 支持 AEM Storefront 中的礼品卡

## 发行日期： 2021年10月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.10.20.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF核心组件 | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia引用站点 | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### 新增功能 {#what-is-new-october}

* CIF加载项支持具有新GraphQL API和架构的最新Commerce v2.4.3

* 作者可以使用富文本编辑器(RTE)在文本字段中添加指向产品和目录页面的链接。 RTE工具栏中添加了一个CIF图标，该图标会打开选取器，以便在不离开上下文的情况下快速搜索和选择产品或类别。

* 现有的弹出购物车和结帐页面已替换为专用的AEM购物车和结帐页面。 这些页面上的组件是使用Adobe Commerce的可扩展Peregrine组件构建的

* 商家可以使用Commerce后端在导航中隐藏某些产品目录类别。 CIF导航核心组件遵循商务后端配置“包含在菜单中”以在导航中显示/隐藏类别

* 如果找不到类别或产品页面，AEM Storefront Venia会返回HTTP 404错误

## 发行日期： 2021年9月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.09.27 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF核心组件 | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia引用站点 | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### 新增功能 {#what-is-new-september}

* 站点编辑器中新的“关联的商业内容”选项卡通过快速访问当前上下文的相关AEM产品内容来提高创作效率

  ![关联的商务内容](/help/assets/CIF/associated-commerce-content.png)

* 改进了产品选取器UI，以提供更好的用户体验、更高的效率并支持复杂的产品目录

  ![新产品选取器](/help/assets/CIF/product-picker.png)

* 在导航组件中遵守“include_in_menu”属性

### 错误修复 {#bug-fixes-september}

* 菜单缓存刷新未按预期工作

* AEM CS部署步骤和不使用客户端组件时出现JS错误

* 无法在具有sling：configs节点的文件夹中创建CIF云配置

## 发行日期： 2021年8月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.09.02 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF核心组件 | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia引用站点 | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### 新增功能 {#what-is-new-august}

* 新的类别选择器UI改善了用户体验、提高了效率，并更好地支持复杂的产品目录

  ![新建类别选取器](/help/assets/CIF/category-picker.png)

* 对CIF核心组件的更佳A11Y支持

### 错误修复 {#bug-fixes-august}

* 打开类别筛选器折叠后，无法将其关闭

* 产品Teaser中的“行动号召文本”属性损坏

* AEM CS部署步骤期间出现CIF JS错误

* 修复对映射的产品列表项目的原始产品访问权限

## 发行日期： 2021年7月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.07.21 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF核心组件 | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia引用站点 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新增功能 {#what-is-new-july}

* CIF核心组件v2
   * 简化并改进了PDP/PLP URL和SEO的配置
   * 创作模式下暂存产品数据的视觉指示器，用于更好地显示即将发生的更改
   * 内容和商务页面的新站点地图组件

* 支持 [Adobe Commerce Sensei产品推荐，由Adobe Sensei提供支持](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用预定义或动态创建的推荐

## 发行日期： 2021年6月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.06.18 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF核心组件 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia引用站点 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新增功能 {#what-is-new-june}

* 内容片段的新CIF产品和类别引用数据类型(包括 产品/类别选取器UI支持)
* 新的Commerce内容片段核心组件
* AEM后端支持全文商务搜索
* Commerce核心组件支持Adobe Commerce Sensei Recs数据收集
* 改进了类别页面的SEO友好URL
* 支持每个站点/配置的自定义HTTP标头

## 发行日期： 2021年5月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.05.26 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF核心组件 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia引用站点 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新增功能 {#what-is-new-may}

* 产品控制台属性中的关联内容支持分页

### 错误修复 {#bug-fixes-may}

* 资产缩略图未显示在产品属性的“资产”选项卡中

* 痕迹导航在产品控制台中重置预览数据

## 发行日期： 2021年4月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2021.04.22 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心组件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 支持类别UID — 对于将字符串用作类别ID的系统，这为他们解锁了第三方商业集成

* 用于PWA Studio的AEM扩展，包括 示例集成

* 扩展WCM导航核心组件的新CIF导航核心组件

### 错误修复 {#bug-fixes-april}

* 根类别字段未显示在类别页面的页面属性中的commerce选项卡下

## 发行日期： 2021年3月 {#what-is-new-march}

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2021.03.25 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能

* 对Adobe Commerce 2.4.2的支持

### 改进内容

* 改进了内容驱动页面的产品详细信息组件的可重用性

* PDP的缓存性能更好，后端调用更少

* 多个错误修复。

## 发行日期： 2021年2月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2021.02.24 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 产品体验管理：使用体验片段单独丰富产品目录页面。

* 扩展了产品控制台属性，可显示链接的资产和体验片段，包括用于快速导航到关联内容的操作。

### 改进内容  {#what-is-improved-february}

* 使用产品图像URL和类别信息增强的客户端数据层。

* 多个错误修复。

## 发行日期： 2021年1月

| GitHub | 版本 | 详细的发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.7.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.7.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia引用站点 | 2021.02.02 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 产品体验管理：为资源和体验片段新增了“商务”属性选项卡。 利用此选项卡，可将资产和体验片段链接到产品和类别。 该选项卡还显示链接商务对象的实时数据以及在产品控制台中显示详细信息的链接。

### 改进内容  {#what-is-improved-january}

* 在验证后，将用户数据发送到Adobe客户端数据层。

* 多个错误修复。
