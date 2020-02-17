---
title: 管理多个资产和收藏集
description: 了解如何同时编辑多个资产和集合的元数据以快速传播常见的元数据更改。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 管理资产和收藏集 {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager(AEM)资产允许您同时编辑多个资产的元数据，以便快速将常见元数据更改批量传播到资产。 您还可以批量编辑多个集合的元数据。

使用属性页可对多个资产或集合执行元数据更改：

* 将元数据属性更改为通用值
* 添加或修改标记

要自定义元数据属性页面（包括添加、修改和删除元数据属性），请使用架构编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](search-assets.md#metadataupdates)。

## 编辑多个资产的元数据属性 {#editing-metadata-properties-of-multiple-assets}

1. 在“资产”用户界面中，导航到要编辑的资产所在的位置。
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，点按／单击 **[!UICONTROL 属性]** 图标以打开选定资产的属性页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最低级别的父表单。 换句话说，属性页面仅显示所有单个资产的属性页面中通用的元数据字段。

1. 修改各个选项卡下选定资产的元数据属性。
1. 要查看特定资产的元数据编辑器，请取消选择列表中的其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在属性页面中，您可以通过取消选择资产来从资产列表中删除资产。 默认情况下，资产列表会选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. 要为资产选择其他元数据架构，请点按／单击工具栏中的 **[!UICONTROL 设置]** 图标，然后选择所需的架构。
1. 保存更改。
1. 要将新元数据与包含多个值的字段中的现有元数据一起追加，请选择“ **[!UICONTROL 追加”模式]**。 如果不选择此选项，则新元数据将替换字段中的现有元数据。 点按／单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择“追加”模式，新元数据也不会附加到字段中的现有 **[!UICONTROL 值中]**。

## 编辑多个集合的元数据属性 {#editing-metadata-properties-of-multiple-collections}

1. 从收藏集控制台中，选择要编辑的收藏集。
1. 在工具栏中，点按／单 **[!UICONTROL 击属性]** ，以打开选定集合的属性页面。
1. 修改各个选项卡下选定集合的元数据属性。

   >[!NOTE]
   >
   >您为所选集合添加的元数据将覆盖这些集合的以前元数据，但标记除外。 您在“标记”字段中添 **[!UICONTROL 加的任何标记]** ，都会附加到元数据中的现有标记列表中。

1. 要查看特定集合的元数据属性，请取消选择集合列表中的其余集合。 元数据编辑器字段会填充特定集合的元数据。

   >[!NOTE]
   >
   >* 在收藏集属性页面中，可以通过取消选择收藏集从收藏集列表中删除收藏集。 集合列表默认选中所有集合。 您删除的集合的元数据不会更新。
   >* At the top of the list, select the check box near **[!UICONTROL Title]** to toggle between selecting the collections and clearing the list.


1. 保存更改。

## 配置批量元数据更新限制 {#configlimit}

为防止出现类似DOS的情况，AEM限制了Sling请求中支持的参数数。 在一次性更新许多资产的元数据时，您可能会达到限制，并且不会更新更多资产的元数据。 AEM在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

要更改限制，请访问Web控制台( **[!UICONTROL “工具]** ”>“操作” **[!UICONTROL >]** Web Prosements **[!UICONTROL )，并更改]********** Apache Sling Handling Signi配置中Maximum POST Parameters PrametersInternts Apache Shandling Osgi Configuration的值。
