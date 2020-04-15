---
title: 支持IPTC元数据
description: 了解Adobe Experience Manager(AEM)资产如何支持通过Adobe Bridge和其他Creative Apps添加到资产的IPTC元数据、创意评级和关键字。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 支持IPTC元数据 {#support-for-iptc-metadata}

了解Adobe Experience Manager(AEM)资产如何支持通过Adobe Bridge和其他Creative Apps添加到资产的IPTC元数据、创意评级和关键字。

Adobe Experience Manager(AEM)资产支持IPTC元数据标准，该标准被广泛用于描述资产。 这样，AEM Assets就增强了各方对其图像的接受，包括摄影师、创意机构、图书馆、博物馆等。

资产的默认元数据模式现在整合了IPTC核心和IPTC扩展元数据模式，以定义全面的元数据属性，这些属性允许用户添加有关图像中显示的人物、位置和产品的精确可靠的数据。 它还支持有关创建图像的日期、名称和标识符，以及表达权限信息的灵活方式。

资产的“属性”页面现在包括单独的选项卡，用于在可编辑字段中显示IPTC核心和IPTC扩展元数据。

1. 从“资产”用户界面中，选择一个图像。
1. Click **[!UICONTROL Properties]** from the toolbar.
1. 单击 **[!UICONTROL IPTC]** 选项卡以视图资产的IPTC元数据。
1. 根据需要编辑IPTC元数据属性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. 根据需要编辑IPTC扩展元数据属性。
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

## 创意评级支持 {#creative-rating-support}

除了显示单个用户评级和聚合评级外，“属性”页面现在还显示通过Adobe Bridge和其他Creative Apps分配给资产的评级

这些评级位于&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡的&#x200B;**[!UICONTROL 创意评分]**&#x200B;部分下。

此等级为只读属性，范围在1-5之间。 您可以从“搜索”面板中根据资产的创意等级搜索资产。

但是，此属性当前没有索引以避免与用户所做的自定义更改发生冲突。

## 关键字支持 {#keyword-support}

“属 **[!UICONTROL 性]** ”页面的  IPTC选项卡还显示通过Adobe Bridge和其他Adobe Creative Cloud应用程序添加到资产的关键字。 您还可以编辑这些关键字，并从 **[!UICONTROL IPTC选项卡添加更多关]** 键字。

![关键字](assets/keywords-in-iptc-tab.png)
