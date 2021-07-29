---
title: AEM Content and Commerce 2021发行说明
description: AEM Content and Commerce 2021发行说明
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: d1e2a2b11bd4eaece80a2538ddc34ada59e63578
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 8%

---

# 商务集成框架GitHub发行概述

## 系统要求概述

请查看下表中的最低系统要求，了解您当前使用的CIF版本或计划将来使用的CIF版本。

**在4月版中，我们已使用Adobe软件分发中提供的CIF附加组件** 替换了GitHub上的CIF [连接器](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。切换到附加组件对项目有极大好处：

* 大多数新功能将立即在AEM 6.5上可用（无需再等待功能端口）
* 可轻松升级到新的附加版本
* 准备Cloud Service

旧AEM CIF连接器将进入维护模式，不应再使用。 请将CIF连接器更换为新的CIF附加组件。 对于大多数项目来说，只需简单地替换包即可。

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF附加组件 | 最低：AEM 6.5.7,Magento2.3.5 GraphQL模式 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期：2021年7月

| 组件 | 版本号 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2021.07.21 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF核心组件 | 1.13.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.13.0) |
| CIF Venia参考网站 | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### 新增功能 {#what-is-new-july}

* CIF核心组件v2
   * 简化和改进了PDP/PLP URL和SEO配置
   * 在创作模式下暂存产品数据的可视指示器，可更好地显示即将发生的更改
   * 用于内容和商务页面的新站点地图组件

* 支持[Adobe商务Sensei产品推荐，由AEM Storefront中的Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)提供支持，使用预定义或即时创建的推荐

## 发行日期：2021年6月

| 组件 | 版本号 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2021.06.18 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF核心组件 | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia参考网站 | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### 新增功能 {#what-is-new-june}

* 内容片段的新CIF产品和类别引用数据类型(包括 产品/类别选取器UI支持)
* 新的商务内容片段核心组件
* AEM后端支持的全文商务搜索
* 商务核心组件支持Adobe商务Sensei Recs数据收集
* 改进了类别页面的SEO友好URL
* 支持每个站点/配置的自定义HTTP标头

## 发行日期：2021年5月

| 组件 | 版本号 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2021.05.26 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF核心组件 | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia参考网站 | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### 新增功能 {#what-is-new-may}

* 产品控制台属性中对关联内容的分页支持

### 错误修复 {#bug-fixes-may}

* 产品属性的资产选项卡中未显示资产缩略图

* 痕迹导航会重置产品控制台中的预览数据

## 发行日期：2021年4月

| 组件 | 版本号 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2021.04.22 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心组件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 支持类别UID — 这将解锁对类别ID使用字符串的系统的第三方商务集成

* AEM的PWA Studio扩展，包括 示例集成

* 新的CIF导航核心组件，可扩展WCM导航核心组件

### 错误修复 {#bug-fixes-april}

* 类别页面的页面属性的商务选项卡下未显示根类别字段

## 发行日期：2021年3月 {#what-is-new-march}

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2021.03.25 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能

* 支持Magento2.4.2

### 改进内容

* 改进了内容驱动页面产品详细信息组件的重用性

* 更好地缓存，减少PDP的后端调用

* 修复了多个错误。

## 发行日期：2021年2月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2021.02.24 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 产品体验管理：使用体验片段单独丰富产品目录页面。

* 扩展的产品控制台属性，用于显示链接的资产和体验片段，包括快速导航到关联内容的操作。

### 改进内容  {#what-is-improved-february}

* 增强了客户端数据层，其中包含产品图像url和类别信息。

* 修复了多个错误。

## 发行日期：2021年1月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.7.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.7.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia参考网站 | 2021.02.02 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 产品体验管理：资产和体验片段新增了“商务”属性选项卡。 利用此选项卡，可将资产和体验片段关联到产品和类别。 选项卡还显示链接的商务对象的实时数据，以及用于在产品控制台中显示详细信息的链接。

### 改进内容  {#what-is-improved-january}

* 在验证后将用户数据发送到Adobe客户端数据层。

* 修复了多个错误。
