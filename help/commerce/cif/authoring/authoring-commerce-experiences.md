---
title: 创作商务体验
description: 工作商务体验
source-git-commit: f3e286c7b5404812655f3b257de17be7bfde7487
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 创作商务体验 {#authoring-commerce-experiences}

## 概述 {#overview}

CIF附加组件通过特定于商务的功能，扩展了AEM创作。 这样，作者就可以无需离开上下文即可访问产品数据和内容，从而高效地构建和管理与商务相关的体验。

## 选手 {#pickers}

产品和类别选取器是模态UI对话框，为AEM作者提供了一种在需要时轻松查找和选择产品或类别的方法。 核心组件、内容关联和产品模板是配置中需要产品目录数据的典型区域。 选取器支持各种配置选项，例如多选、变量选择和预选值。

### 产品选取器 {#product-picker}

此选取器提供浏览目录结构或全文搜索以查找产品的功能。 具有变体的产品在“类型”列中提供了文件夹图标。 单击文件夹图标可打开选定产品的变体。

![产品选取器](/help/commerce/cif/assets/authoring/product-picker.png)

单击父类别会将作者带回产品级别。

![产品选取器](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**示例产品Teaser**

![未选择的Teaser组件](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

此组件的配置对话框需要产品。 CIF使用SKU作为产品标识符。 作者可以手动输入SKU，也可以单击文件夹图标以打开产品选取器。 选择并关闭选取器后，组件对话框会显示选定产品的名称

![具有选择的Teaser组件](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### 类别选取器 {#category-picker}

此选取器提供浏览目录结构以查找类别的功能。

![类别选取器](/help/commerce/cif/assets/authoring/category-picker.png)

**类别轮播示例**

![无选择的轮播组件](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

此组件的配置对话框需要1 :n个类别。 CIF使用UID / ID作为类别标识符。 作者可以手动输入UID，也可以单击文件夹图标以打开类别选取器。 选择并关闭选取器后，组件对话框会显示所选类别的名称。

![包含选定内容的轮播组件](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## 通用编辑器 {#universal-editor}

通用编辑器经过扩展，具有访问实时产品数据和相关产品内容的功能。

### 访问产品数据 {#access-product-data}

编辑器侧面板中的“资产”选项卡提供了通过选择类型“产品”来访问产品数据的权限。 从配置的商务端点中实时获取数据。 过滤器是在商务端点上进行的全文搜索，用于查找特定产品。

![产品数据侧面板](/help/commerce/cif/assets/authoring/products-side-panel.png)

与资产类似，产品可以在页面（默认创建Product Teaser组件）或组件（当前支持的是Product Teaser和Product Carousel）上进行分发。

### 使用RTE在文本字段中添加链接 {#rte}

CIF产品目录页面是即时呈现的虚拟页面。 因此，无法嵌入超链接(如常规AEM页面的超链接)。 CIF会向RTE（富文本编辑器）中添加一个新操作“商务链接”。 此操作的工作方式与常规“超链接”操作完全相似，但允许作者使用选取器选择产品或类别。

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!NOTE]
    >
    >如果同时选择类别和产品，则会选择产品。

这会创建一个占位符链接，在页面呈现时，该链接将被实际链接替换。

### 访问关联的产品内容 {#associated-content}

如果通用编辑器识别页面上的1:n产品，则侧面板将自动显示选项卡“关联的商务内容”。 通过此选项卡，作者可以快速访问带有产品标记的AEM内容(请参阅 [使用关联的AEM内容扩充产品数据](./enrich-product-associated-content.md) ，以了解更多信息)。 此选项卡提供了下拉列表，用于在页面上存在多个产品时筛选内容类型和特定产品。 使用内容的工作方式与使用“资产”选项卡中的内容完全相同。

![产品数据侧面板](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### 预览分阶段产品数据 {#staged-data}

编辑器中的时间扭曲模式允许作者根据时间扭曲日期，预览和浏览带有分阶段产品目录数据的AEM体验。

![时间扭曲](/help/commerce/cif/assets/authoring/timewarp.png)

如果暂存使用的日期，组件将显示一个可视指示器。

![暂存指示器](/help/commerce/cif/assets/authoring/staged-indicator.png)

## 全能搜索 {#omnisearch}

使用Omnisearch是从业人员使用全文搜索查找AEM内容和产品目录数据的简便方法。 Omnisearch将在AEM和商务后端中运行全文搜索，以在商务后端和AEM内容中查找产品目录对象。 AEM结果还包含使用产品/类别数据标记的内容。

![全能搜索](/help/commerce/cif/assets/authoring/omnisearch.png)

结果按类型分组。

    >[!NOTE]
    >
    > Omnisearch中的全文搜索不支持关联的内容片段。 使用SKU或UID查找关联的内容片段。
