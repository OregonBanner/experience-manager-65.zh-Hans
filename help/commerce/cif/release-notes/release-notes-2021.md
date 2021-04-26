---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
translation-type: tm+mt
source-git-commit: 1a6d713e74056333b18ed68f58876c2a75d535b8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 11%

---

# Commerce Integration Framework GitHub发布概述

## 系统要求概述

请查看下表中关于您当前使用或计划将来使用的CIF版本的最低系统要求。

**CIF加载项现可通过 [Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。旧的AEM CIF连接器正进入维护模式，不应再使用。 请迁移到新的CIF加载项。**

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF附加 | 最低：AEM 6.5.7、Magento 2.3.5 GraphQL模式 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发布日期：2021年4月

| 组件 | 版本号 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加 | v021.04.22 | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF核心组件 | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-april}

* 支持类别UID — 这将解锁对类别ID使用字符串的系统的第三方商务集成

* AEM extension for PWA Studio，包括 示例集成

* 扩展WCM导航核心组件的新CIF导航核心组件

* AEM商店中分阶段目录数据的可视指示器

### 错误修复 {#bug-fixes-april}

* 根类别字段未显示在类别页面页面属性中的“商务”选项卡下

## 发布日期：2021年3月{#what-is-new-march}

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.9.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.9.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2021.03.25 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能

* 支持Magento 2.4.2

### 改进内容

* 改进了内容驱动页面产品详细信息组件的可重用性

* 更好的缓存和更少的PDP后端调用

* 多个错误修复。

## 发布日期：2021年2月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.8.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.8.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2021.02.24 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-february}

* 产品体验管理：使用Experience Fragments单独丰富产品目录页面。

* 可显示链接资产和体验片段的扩展产品控制台属性，包括快速导航到相关内容的操作。

### 改进内容  {#what-is-improved-february}

* 增强的客户端数据层，包含产品图像url和类别信息

* 多个错误修复。

## 发布日期：2021年1月

| GitHub | 版本号 | 详细发行说明 |
|:-------|:-----:|---------------------:|
| CIF连接器 | 1.7.0 | [发行说明](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF核心组件 | 1.7.0 | [发行说明](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF韦尼亚参考站 | 2021.02.02 | [发行说明](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新增功能 {#what-is-new-january}

* 产品体验管理：资产和体验片段的新“商务”属性选项卡。 通过此选项卡，您可以将资产和体验片段关联到产品和类别。 该选项卡还显示链接的商务对象的实时数据以及用于在产品控制台中显示详细信息的链接。

### 改进内容  {#what-is-improved-january}

* 在验证后将用户数据发送到Adobe客户端数据层。

* 多个错误修复。
