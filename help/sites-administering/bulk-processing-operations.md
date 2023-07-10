---
title: 批量处理操作
seo-title: Bulk Processing Operations
description: null
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---


# 批量处理操作 {#bulk-processing-operations}

## 简介 {#introduction}

使用最新版本的AEM时，“全选”按钮已扩展到所有视图：“列表”、“列”和“卡片”视图。 现在，全选按钮可选择给定文件夹或收藏集中的所有内容，而不仅仅是客户端浏览器中加载和显示的资产和页面。

已为批量操作启用关键操作： **移动**， **删除** 和 **复制**. 新增一个对话框，让客户知道哪些操作不适用于批量处理。

## 使用方法 {#how-to-use}

名为的新按钮 **全选** 已添加到“卡片”、“列表”或“列”视图中。 此按钮可用于任何视图，以选择数据集中的所有元素。

在早期版本的AEM中，所做的选择仅限于客户端浏览器中加载的内容。 引入此新更改是为了避免在执行批量操作的元素数量方面出现混淆。

目前，已向批量处理添加了三个操作：

* 移动
* 复制
* 删除

未来将添加对更多操作的支持。
要使用此功能，您需要导航到要在其中对页面或资产执行批量操作的文件夹或收藏集。

然后，选择其中一个视图，如下所示：

### 信息卡视图 {#card-view}

![显示各种图像资源的缩略图的卡片视图。](assets/unu.png)

### 卡片视图中的批量选择 {#bulk-selection-in-card-view}

可以使用批量选择资源或页面 **全选** 右上角的按钮：

![选择卡片视图右上角显示的“全部”按钮。](assets/doi.png) ![卡片视图中图像资源的所有缩略图图像均显示为选中状态，并带有复选标记。](assets/trei.png)

### 列表视图 {#list-view}

列表视图也是如此：

![“列表视图”右上角的“全选”选项会突出显示。](assets/patru_modified.png)

### 列表视图中的批量选择 {#bulk-selection-in-list-view}

在列表视图中，使用 **全选** 按钮，或使用左侧的复选框批量选择。

![显示图像资产缩略图图像的实时视图会以水平行显示。](assets/cinci.png) ![显示图像资产的缩略图图像的列表框和“名称”左侧的复选框。](assets/sase.png)

### 列视图 {#column-view}

![列视图，显示以垂直列显示的图像资源的缩略图图像。](assets/sapte.png)

### 列视图中的批量选择 {#bulk-selection-in-column-view}

![列视图中图像资源的所有缩略图图像均显示为选中状态，并带有复选标记。](assets/opt.png)

## 批量启用的操作 {#bulk-enabled-operations}

选择后，可以执行以下三个批量启用操作之一： **移动**， **复制** 或 **删除**.

此处， **移动** 操作会对上面选择的资产执行。 在任何视图中，这都会导致所有资产被移动到所选位置，而不仅仅是屏幕上的加载资产。

![在列视图中移动显示选定文件夹的资产。](assets/noua.png)

对于未批量启用的其他操作，如 **下载，** 此时将显示一条警告，仅说明该操作中将包含浏览器中加载的元素。

![资源视图显示选定的图像资源和“不支持批量操作”弹出对话框。](assets/zece.png)
