---
title: 产品 Cockpit
description: 使用产品驾驶舱，其中提供链接的产品目录和相关内容的统一概述。
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# 产品 Cockpit {#product-cockpit}

## 概述 {#overview}

产品驾驶舱提供链接的产品目录和相关内容的统一概述。 所有关联内容都有链接，可通过驾驶舱快速访问这些内容。

暂存的产品数据包括未来的任何突变，例如新类别、产品或更新的资产。

>[!NOTE]
>
>术语产品目录可与商务商店、商店视图和类似表达式互换。

## 配置 {#configuration}

必须在AEM中配置产品目录。 请参阅 [配置存储和目录](/help/commerce/cif/getting-started.md#catalog) 以了解更多信息。

启用暂存目录功能需要身份验证。 请参阅 [快速入门](/help/commerce/cif/getting-started.md) 以了解更多信息。

>[!NOTE]
>
>暂存目录功能仅适用于支持基于令牌的身份验证的Adobe Commerce和第三方连接器。

## 打开产品驾驶舱 {#opening-product-cockpit}

访问产品驾驶舱的最简单方法是通过AEM主菜单中的“商务”菜单。 也可以使用Omnisearch（搜索商业）或opening `https://<yourAEMInstance>/commerce.html`.

![AEM菜单](/help/commerce/cif/assets/aem-menu.png)

## 浏览产品目录 {#browsing-product-catalogs}

产品驾驶舱按照产品目录结构以分层方式组织。 第一级显示所有已配置产品目录的目录根级别，包括商务后端的元信息。

![已配置的目录](/help/commerce/cif/assets/catalog-overview.png)

单击某个类别可加载该已单击类别的子项。

![类别子项](/help/commerce/cif/assets/catalog-category-children.png)

单击产品可加载产品变体（如果可用）。

![产品变体](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>AEM中的产品目录数据是通过配置的商务端点实时检索的数据。 AEM中未存储任何产品目录数据。

## 搜索产品目录 {#searching-product-catalog}

左侧过滤器选项卡中提供了对完整产品目录的全文搜索，以便快速查找产品。

![搜索](/help/commerce/cif/assets/search-cockpit.png)

## 浏览暂存产品目录 {#staged-product-catalogs}

默认情况下，产品驾驶舱显示实时产品目录数据。 使用左侧过滤器选项卡中的“暂存目录”可加载任何选定日期的产品目录。

![暂存目录](/help/commerce/cif/assets/staged-cockpit.png)

## 产品目录属性 {#catalog-properties}

单击产品或类别的属性图标可打开选定对象的属性视图。 产品变体的打开属性等于打开主产品属性。

### 商业选项卡 {#tabs}

常规和变量选项卡显示来自商业后端的预定义商业属性。 此数据(包括 变体)是AEM中的只读数据，因为记录系统是商务后端。 变体选项卡仅显示具有变体的产品，并显示所有变体的列表。

![目录属性](/help/commerce/cif/assets/catalog-properties.png)

### AEM内容选项卡 {#content-tabs}

这些按AEM内容类型（体验片段、内容片段、关联的资产）分组的选项卡显示与商务对象关联的AEM内容。 “查看详细信息”操作将打开一个包含选定内容的新浏览器选项卡。

![内容属性](/help/commerce/cif/assets/content-properties.png)
