---
title: AEM Content and Commerce 2022发行说明
description: AEM Content and Commerce 2022发行说明
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 27%

---

# 商务集成框架GitHub发行概述

## 系统要求概述

请查看下表中的最低系统要求，了解您当前使用的CIF版本或计划将来使用的CIF版本。

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF附加组件 | 最低：AEM 6.5.7,Magento2.3.5 GraphQL模式 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期：2022年3月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.02.24.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心组件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia参考网站 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* 测试版：AEM CIF搜索核心组件支持商务LiveSearch
* 改进了多存储方案的SEO:现在，可以通过CIF云配置属性在存储级别配置PDP/PLP的URL格式
* 产品选取器通过UI中的新筛选器选项支持暂存产品。  这样，内容从业者就可以为即将推出的产品准备产品内容管理
* 使用CIF云配置名称（而不是配置代理URL）简化CIF配置管理和错误处理
* 产品列表和轮播组件的手动类别选择。 这允许内容从业者在目录体验之外的内容页面上使用这些组件

## 发行日期：2022年1月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.01.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心组件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia参考网站 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增强的 myAccount 组件
* “产品推荐”组件支持额外的页面类型（主页、购物车、订单确认）
* **愿望清单**
   * 登录的访客可以将产品添加到愿望清单
   * 可以通过 myAccount 管理愿望清单及其产品
   * 可以通过策略（例如产品预告片、产品详细信息）在组件级别启用/禁用“添加到愿望清单”按钮
   * 作为核心组件提供，位于 AEM Venia Storefront 中

![愿望清单](/help/assets/CIF/wishlist.png)
