---
title: AEM Content and Commerce 2022发行说明
description: AEM Content and Commerce 2022发行说明
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: b493e7bd73d679aa46bf41fad105f13215226dd4
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 34%

---

# 商务集成框架GitHub发行概述

## 系统要求概述

请查看下表中的最低系统要求，了解您当前使用的CIF版本或计划将来使用的CIF版本。

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF附加组件 | 最低：AEM 6.5.7,Magento2.3.5 GraphQL模式 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期：2022年6月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.06.xx.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF核心组件 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia参考网站 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新增功能 {#what-is-new-june}

* 产品目录扩充现在支持AEM页面。 这样，作者就可以管理页面 — 产品关联。

* 各种CIF核心组件改进

### 错误修复 {#bug-fixes-june}

* 将登录令牌添加到客户端价格获取

* 数据层中的页面组件错误

## 发行日期：2022年5月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.05.31.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF核心组件 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia参考网站 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新增功能 {#what-is-new-may}

* 新产品驾驶舱属性页面，以获得更好和简化的概述

![产品驾驶舱属性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改进了I/O运行时第三方连接器的兼容性和稳健性

* 改进对GQL客户端配置覆盖的支持（例如，设置自定义缓存行为）

### 错误修复 {#bug-fixes-may}

* 多值产品选取器字段将第2个和其他产品显示为无效

* 有时，产品选取器会隐藏在组件后面

## 发行日期：2022年4月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.04.28.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF核心组件 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia参考网站 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新增功能 {#what-is-new-april}

* 快速访问产品驾驶舱：在站点编辑器中，通过一键单击即可轻松访问完整的详细产品信息

   ![启用愿望清单](/help/assets/CIF/enable-wishlist.png)

* 支持其他营销商务组件：组件可配置为显示加货车和加货车清单行动动员

   ![站点编辑器到产品驾驶舱的快捷键](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 发行日期：2022年2月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.02.24.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心组件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia参考网站 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* Beta：AEM CIF 搜索核心组件支持 Commerce Live Search
* 改进了多商店场景的 SEO：PDP/PLP 的 URL 格式现在可以通过 CIF 云配置属性在商店级别进行配置
* 产品挑选器通过 UI 中新的过滤器选项支持阶段性产品。这使内容从业者能够为即将发布的产品准备产品内容管理
* 通过使用 CIF 云配置名称而非配置代理 URL，简化了 CIF 配置管理和错误处理
* 产品列表和轮盘组件的手动类别选择。这允许内容从业者在目录体验之外的内容页面上使用这些组件

## 发行日期：2022年1月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF附加组件 | 2022.01.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心组件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia参考网站 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增强的 myAccount 组件
* 产品推荐组件支持其他页面类型（主页、购物车、订单确认）
* **愿望清单**
   * 登录的访客可以将产品添加到愿望清单
   * 通过 myAccount 可以管理愿望清单及其产品
   * 可以通过策略（例如产品预告片、产品详细信息）在组件级别启用/禁用“添加到愿望清单”按钮
   * 作为核心组件提供，位于 AEM Venia Storefront 中

![愿望清单](/help/assets/CIF/wishlist.png)
