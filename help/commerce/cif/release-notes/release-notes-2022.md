---
title: AEM Content and Commerce 2022年发行说明
description: Adobe Experience Manager Content and Commerce 2022年发行说明。
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 37%

---

# Commerce integration frameworkGitHub版本概述

## 系统要求概述

查看下表中，您当前使用或计划将来使用的CIF版本的最低系统要求。

| 组件 | 系统要求 |
|:-------|:-----:|
| CIF加载项 | 最低配置：AEM 6.5.7、Adobe Commerce 2.3.5 GraphQL架构 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期： 2022年9月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.09.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF核心组件 | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia引用站点 | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### 新增功能 {#what-is-new-september}

* 作者可以使用体验片段动态丰富产品列表（例如：在产品列表之间放置横幅）
* 列表组件支持关联的产品/类别页面以动态显示相关页面
* 支持Peregrine 12.5组件
* 支持在产品Teaser和轮播中加载客户端价格

## 发行日期： 2022年7月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.08.02.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### 新增功能 {#what-is-new-july}

* 通过 AEM 页面属性以及产品主控室中的概述将 AEM 页面与产品和类别关联
  ![产品主控室页面关联](/help/assets/CIF/product_cockpit_page_association.png)

## 发行日期： 2022年6月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.07.05.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF核心组件 | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia引用站点 | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### 新增功能 {#what-is-new-june}

* 产品目录扩充现在支持AEM页面，使作者能够管理页面 — 产品关联。

* 多项 CIF 核心组件功能改进

### 错误修复 {#bug-fixes-june}

* 将登录令牌添加到客户端价格获取流程

* 数据层中的页面组件错误。

## 发行日期： 2022年5月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.05.31.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF核心组件 | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia引用站点 | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### 新增功能 {#what-is-new-may}

* 新产品驾驶舱属性页面，提供更好、更简化的概述

![产品驾驶舱属性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改进了I/O运行时第三方连接器的兼容性和稳健性

* 改进对GQL客户端配置覆盖的支持（例如，设置自定义缓存行为）

### 错误修复 {#bug-fixes-may}

* 多值产品选取器字段将第二个和其他产品显示为无效

* 有时，产品选取器会隐藏在组件后面

## 发行日期： 2022年4月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.04.28.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF核心组件 | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia引用站点 | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### 新增功能 {#what-is-new-april}

* 快速访问产品驾驶舱：在站点编辑器中，通过一键单击即可轻松访问完整的详细产品信息

  ![启用愿望清单](/help/assets/CIF/enable-wishlist.png)

* 支持其他营销商务组件：组件可以配置为显示添加到购物车和添加到愿望清单的号召性用语

  ![站点编辑器到产品驾驶舱的快捷键](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## 发行日期： 2022年2月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.02.24.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF核心组件 | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia引用站点 | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### 新增功能 {#what-is-new-march}

* Beta：AEM CIF 搜索核心组件支持 Commerce Live Search
* 改进了多商店场景的 SEO：PDP/PLP 的 URL 格式现在可以通过 CIF 云配置属性在商店级别进行配置
* 产品选取器通过用户界面中的新筛选器选项支持暂存产品。 使内容从业者能够为即将发布的产品准备产品内容管理
* 通过使用 CIF 云配置名称而非配置代理 URL，简化了 CIF 配置管理和错误处理
* 产品列表和轮盘组件的手动类别选择。允许内容从业者在目录体验之外的内容页面上使用这些组件

## 发行日期： 2022年1月

| 组件 | 版本 | 详细信息 |
|:-------|:-----:|---------------------:|
| CIF加载项 | 2022.01.20.00 | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF核心组件 | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia引用站点 | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### 新增功能 {#what-is-new-january}

* 增强的 myAccount 组件
* 产品推荐组件支持其他页面类型（主页、购物车、订单确认）
* **愿望清单**
   * 登录的访客可以将产品添加到愿望清单
   * 通过 myAccount 可以管理愿望清单及其产品
   * 可以通过策略（例如产品预告片、产品详细信息）在组件级别启用/禁用“添加到愿望清单”按钮
   * 作为核心组件提供，位于 AEM Venia Storefront 中

![愿望清单](/help/assets/CIF/wishlist.png)
