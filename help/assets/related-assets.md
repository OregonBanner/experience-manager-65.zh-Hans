---
title: 相关资产
description: 了解如何关联共享一些常见属性的数字资产。 还可在数字资产之间创建源源关系。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f9f745369ba0fe242dea1e5a5e5af0b8263b1ec0
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# 相关资产 {#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关资产功能根据组织的需求手动关联资产。 例如，您可以将许可证文件与资产或类似主题上的图像／视频关联。 您可以关联共享某些共同属性的资产。 您还可以使用该功能在资产之间创建源／派生关系。 例如，如果您有从INDD文件生成的PDF文件，则可以将PDF文件与其源INDD文件相关联。

使用此功能，您可以灵活地与供应商或代理共享低分辨率PDF文件或JPG文件，并且仅可应要求提供高分辨率INDD文件。

>[!NOTE]
>
>只有对资产具有编辑权限的用户才能与资产建立关系并取消资产的关联。

## Relate assets {#relating-assets}

1. 从界 [!DNL Experience Manager] 面中，打开要 **[!UICONTROL 关联的]** 资产的“属性”页面。

   ![打开资产的“属性”页面以关联资产](assets/asset-properties-relate-assets.png)

   *图：[!DNL Assets][!UICONTROL 属性]”页面以关联资产。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将其他资产与您选择的资产关联，请单 **[!UICONTROL 击工]** 具 ![栏中的](assets/do-not-localize/link-relate.png) “关联资产”。
1. 执行下列操作之一：

   * 要关联资产的源文件，请从 **[!UICONTROL 列表]** 中选择源。
   * 要关联派生文件，请从 **[!UICONTROL 列表]** 中选择“派生”。
   * 要在资产之间创建双向关系，请从列表 **[!UICONTROL 中选]** 择其他。

1. 从选 **[!UICONTROL 择资产]** ，导航到要关联的资产所在的位置，然后选择它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击 **[!UICONTROL 确认]**。
1. Click **[!UICONTROL OK]** to close the dialog. 根据您在步骤3中对关系的选择，相关资产会列在“相关”部分的相应类别 **[!UICONTROL 下]** 。 例如，如果您相关的资产是当前资产的源文件，则该资产会列在“源” **[!UICONTROL 下]**。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消资产的关联，请单击工 **[!UICONTROL 具栏中]**![的取消关](assets/do-not-localize/link-unrelate-icon.png) 联资产。

1. 从删除关系对话框中选择要取消关联的 **[!UICONTROL 资产]** ，然后单击取 **[!UICONTROL 消关联]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Click **[!UICONTROL OK]** to close the dialog. 您删除关系的资产会从相关资产的列表中删除“相关” **[!UICONTROL 部分]** 。

## 翻译相关资产 {#translating-related-assets}

使用相关资产功能在资产之间创建源／派生关系在翻译工作流也很有帮助。 当您对派生资产运行转换工作流时，会自 [!DNL Experience Manager Assets] 动获取源文件引用的任何资产并将其包含在其中以进行转换。 这样，源资产引用的资产便会与源资产和派生资产一起进行折算。 例如，假设您的英语副本包括派生资产及其源文件，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与其他资产相关，则会获取引 [!DNL Experience Manager Assets] 用的资产，并将其包含在其中以进行转换。

![“资产属性”页显示要包括的转换相关资产的源文件](assets/asset-properties-source-asset.png)

*图：要包括以进行折算的相关资产的源资产。*

1. 按照创建新翻译项目中的步骤，将源文件夹中的资 [产翻译为目标语言](translation-projects.md#create-a-new-translation-project)。 例如，在本例中，将您的资源翻译为法语。

1. 从“项 [!UICONTROL 目] ”页面打开翻译文件夹。

1. 单击项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击翻译作业卡下面的省略号以视图翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资产，然后单击工 **[!UICONTROL 具栏中的]** “在资产中显示”，以视图资产的转换状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证是否已转换与源相关的资产，请单击源资产。

1. 选择与源相关的资产，然后单击“在资 **[!UICONTROL 产中显示”]**。 此时会显示已转换的相关资产。
