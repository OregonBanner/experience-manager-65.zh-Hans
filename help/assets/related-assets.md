---
title: 相关资产
description: 了解如何与共享某些常见属性的数字资产关联。 还可以在数字资产之间创建源派生的关系。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# 相关资产 {#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关资产功能，根据贵组织的需求手动关联资产。 例如，您可以将许可证文件与类似主题上的资产或图像/视频相关联。 您可以与共享某些公共属性的资产相关联。 您还可以使用该功能在资产之间创建源/派生关系。 例如，如果您有一个从INDD文件生成的PDF文件，则可以将PDF文件与其源INDD文件相关联。

使用此功能，您可以灵活地与供应商或代理共享低分辨率PDF文件或JPG文件，并且仅应请求提供高分辨率INDD文件。

>[!NOTE]
>
>只有对资产具有编辑权限的用户才能与资产关联和取消关联。

## 相关资产 {#relating-assets}

1. 从 [!DNL Experience Manager] 界面，打开 **[!UICONTROL 属性]** 页面。

   ![打开资产的“属性”页面以关联资产](assets/asset-properties-relate-assets.png)

   *图： [!DNL Assets] [!UICONTROL 属性] 页面以关联资产。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将另一个资产与您选择的资产关联，请单击 **[!UICONTROL 关联]** ![相关资产](assets/do-not-localize/link-relate.png) 中。
1. 执行下列操作之一：

   * 要关联资产的源文件，请选择 **[!UICONTROL 来源]** 列表。
   * 要关联派生文件，请选择 **[!UICONTROL 派生]** 列表。
   * 要在资产之间创建双向关系，请选择 **[!UICONTROL 其他]** 列表。

1. 从 **[!UICONTROL 选择资产]** ，导航到要关联的资产的位置，然后选择该资产。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击 **[!UICONTROL 确认]**.
1. 单击 **[!UICONTROL 确定]** 来关闭对话框。 根据您在步骤3中选择的关系，相关资产会列在 **[!UICONTROL 相关]** 中。 例如，如果您所关联的资产是当前资产的源文件，则该资产会列在 **[!UICONTROL 来源]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消资产关联，请单击 **[!UICONTROL 不相关]** ![与资产无关](assets/do-not-localize/link-unrelate-icon.png) 中。

1. 从 **[!UICONTROL 删除关系]** 对话框，然后单击 **[!UICONTROL 不相关]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 单击 **[!UICONTROL 确定]** 来关闭对话框。 您删除关系的资产将从 **[!UICONTROL 相关]** 中。

## 翻译相关资产 {#translating-related-assets}

使用相关资产功能在资产之间创建源/派生关系在翻译工作流程中也非常有用。 当您对派生资产运行翻译工作流时， [!DNL Experience Manager Assets] 会自动获取源文件引用并包含在其中以进行翻译的任何资产。 这样，源资产引用的资产与源资产和派生资产一起进行折算。 例如，假定您的英语副本包含派生资产及其源文件，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与另一个资产相关， [!DNL Experience Manager Assets] 会获取引用的资产，并将其包含在内以进行翻译。

![资产属性页面显示要包含以进行翻译的相关资产的源文件](assets/asset-properties-source-asset.png)

*图：要包含以进行折算的相关资产的来源资产。*

1. 按照 [创建新的翻译项目](translation-projects.md#create-a-new-translation-project). 例如，在本例中，将资产翻译为法语。

1. 从 [!UICONTROL 项目] 页面，打开翻译文件夹。

1. 单击项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击翻译作业卡片下方的省略号可查看翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资产，然后单击 **[!UICONTROL 在资产中显示]** ，以查看资产的翻译状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证是否已翻译与源相关的资产，请单击源资产。

1. 选择与源相关的资产，然后单击 **[!UICONTROL 在资产中显示]**. 随即会显示已翻译的相关资产。
