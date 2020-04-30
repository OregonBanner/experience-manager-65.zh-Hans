---
title: 相关资产
description: 了解如何关联共享一些常见属性的数字资产。 还可以在数字资产之间创建源源关系。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 相关资产 {#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关资产功能根据组织的需求手动关联资产。 例如，您可以将许可证文件与资产或类似主题上的图像／视频相关联。 您可以与共享某些共同属性的资产相关联。 您还可以使用该功能在资产之间创建源／派生关系。 例如，如果您有一个从INDD文件生成的PDF文件，则可以将PDF文件与其源INDD文件相关联。

使用此功能，您可以灵活地与供应商或代理共享低分辨率PDF文件或JPG文件，并且只有在请求时才可用高分辨率INDD文件。

>[!NOTE] 只有对资产具有编辑权限的用户才能与资产建立关系并取消资产的关联。
>

## Relate assets {#relating-assets}

1. 从Experience Manager界面中，打开 **[!UICONTROL 要关联的资产]** “属性”页面。

   ![打开资产的“属性”页面以关联资产](assets/asset-properties-relate-assets.png)

   *图：属性[!DNL Assets]页，以关联资产。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将其他资产与您选择的资产关联起来，请单击／点按工具栏中 **[!UICONTROL 的]** “关联”图标。

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. 执行下列操作之一：

   * 要关联资产的源文件，请从列表 **[!UICONTROL 中选择]** “源”。
   * 要关联派生的文件，请从列表 **[!UICONTROL 中选择]** “派生”。
   * 要在资产之间创建双向关系，请从列表中 **[!UICONTROL 选择]** “其他”。
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. 在选择 **[!UICONTROL 资产屏幕中]** ，导航到要关联的资产所在的位置，然后选择它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击／点按确 **[!UICONTROL 认图]** 标。
1. 单击／点按 **[!UICONTROL 确定]** ，以关闭对话框。 根据您在步骤3中对关系的选择，相关资产会列在“相关”部分的相应类别 **[!UICONTROL 下]** 。 例如，如果您相关的资产是当前资产的源文件，则该资产会列在“源” **[!UICONTROL 下]**。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消资产的关联，请单击／点按工具 **[!UICONTROL 栏中的]** “取消关联”。

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. 从“删除关系”对话框中选择要取消关联的资 **[!UICONTROL 产]** ，然后单击／点按取消关 **[!UICONTROL 联]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 单击／点按 **[!UICONTROL 确定]** ，以关闭对话框。 您删除了关系的资产会从“相关”部分下相关资产的列表中 **[!UICONTROL 删除]** 。

## 翻译相关资产 {#translating-related-assets}

使用“相关资产”功能在资产之间创建源／派生关系在翻译工作流中也很有帮助。 当您对派生的资产运行转换工作流时，会自动获取源文件引用的任 [!DNL Experience Manager Assets] 何资产，并将其包含在其中以进行转换。 这样，源资产引用的资产与源资产和派生资产一起进行换算。 例如，假设您的英语副本包含派生的资产及其源文件，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与另一个资产相关，则获取引 [!DNL Experience Manager Assets] 用的资产并将其包含在其中以进行转换。

![“资产属性”页显示要包括以进行翻译的相关资产的源文件](assets/asset-properties-source-asset.png)

*图：要包括以进行翻译的相关资产的源资产。*

1. 按照创建新翻译项目中的步骤，将源文件夹中的资产翻译 [为目标语言](translation-projects.md#create-a-new-translation-project)。 例如，在本例中，将您的资产翻译为法语。

1. 从“项 [!UICONTROL 目] ”页面，打开翻译文件夹。

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. 单击／点按项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击／点按翻译作业卡下方的省略号以视图翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资产，然后单击／点按工 **[!UICONTROL 具栏中的资产中的显示]** ，以视图资产的转换状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证是否已转换与源相关的资产，请单击／点按源资产。

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. 选择与源相关的资产，然后单击／点按资产中 **[!UICONTROL 的显示]**。 此时会显示已翻译的相关资产。

   ![chlimage_1-288](assets/chlimage_1-288.png)
