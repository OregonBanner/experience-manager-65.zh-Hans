---
title: 在Adobe Enterprise Manager中管理许多资产和集合的元数据。
description: 同时编辑许多资产和收藏集的元数据，以快速传播常见的元数据更改。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 16%

---


# 管理资产和收藏集 {#managing-multiple-assets-and-collections}

通过Adobe Enterprise Manager Assets，您可以同时编辑多个资产的元数据，以便快速将常见元数据更改批量传播到资产。 您还可以批量编辑多个集合的元数据。

使用属性页可以对多个资产或收藏集执行元数据更改：

* 将元数据属性更改为通用值
* 添加或修改标记

要自定义元数据属性页面，包括添加、修改和删除元数据属性，请使用模式编辑器。

>[!NOTE]
>
>批量编辑方法适用于文件夹或集合中的可用资产。 对于跨文件夹可用或符合通用标准的资产，可在搜索后 [批量更新元数据](search-assets.md#metadataupdates)。

## 编辑多个资产的元数据属性 {#editing-metadata-properties-of-multiple-assets}

1. 在资产用户界面中，导航到要编辑的资产所在的位置。
1. 选择要编辑其通用属性的资产。
1. 在工具栏中，点按／单 **[!UICONTROL 击属]** 性图标以打开选定资产的属性页面。

   >[!NOTE]
   >
   >当您选择多个资产时，系统会为资产选择最常见的父表单。 换言之，属性页面仅显示所有单个资产的属性页面中通用的元数据字段。

1. 修改各个选项卡下选定资产的元数据属性。
1. 要视图特定资产的元数据编辑器，请在列表中取消选择其余资产。 元数据编辑器字段会填充特定资产的元数据。

   >[!NOTE]
   >
   >* 在属性页面中，您可以通过取消选择资产来从资产列表中删除资产。 默认情况下，资产列表会选择所有资产。 您从列表中删除的资产的元数据不会更新。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. 要为资产选择其他元数据模式，请点按／单击工 **[!UICONTROL 具栏]** 中的设置图标，然后选择所需的模式。
1. 保存更改。
1. 要将新元数据与现有元数据追加到包含多个值的字段中，请选择&#x200B;**[!UICONTROL 追加模式]**。如果不选中此选项，则新元数据将替换字段中的现有元数据。点按／单击 **[!UICONTROL 提交]**。

   >[!CAUTION]
   >
   >对于单值字段，即使选择&#x200B;**[!UICONTROL 追加模式]**，新元数据也不会追加到字段中的现有值中。

## 配置元数据批量更新限制 {#configlimit}

为防止出现类似DOS的情况，Enterprise Manager限制了Sling请求中支持的参数数。 在一次性更新多个资产的元数据时，您可能会达到限制，并且不会更新更多资产的元数据。 Enterprise Manager在日志中生成以下警告：

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

>[!MORELIKETHIS]
>
>* [编辑多个集合的元数据属性](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

