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


# 相关资产{#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关资产功能根据组织的需求手动关联资产。例如，您可以将许可证文件与资产或类似主题上的图像／视频关联。 您可以关联共享某些共同属性的资产。 您还可以使用该功能在资产之间创建源／派生关系。 例如，如果您有从INDD文件生成的PDF文件，则可以将PDF文件与其源INDD文件相关联。

使用此功能，您可以灵活地与供应商或代理共享低分辨率PDF文件或JPG文件，并且仅可应要求提供高分辨率INDD文件。

>[!NOTE]
>
>只有对资产具有编辑权限的用户才能与资产建立关系并取消资产的关联。

## 相关资产{#relating-assets}

1. 从[!DNL Experience Manager]接口，打开要关联的资产的&#x200B;**[!UICONTROL 属性]**&#x200B;页面。

   ![打开资产的“属性”页面以关联资产](assets/asset-properties-relate-assets.png)

   *图： [!DNL Assets] [!UICONTROL 属] 性”页面。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将其他资产与您选择的资产关联，请单击工具栏中的&#x200B;**[!UICONTROL 关联]** ![相关资产](assets/do-not-localize/link-relate.png)。
1. 执行下列操作之一：

   * 要关联资产的源文件，请从列表中选择&#x200B;**[!UICONTROL 源]**。
   * 要关联派生文件，请从列表中选择&#x200B;**[!UICONTROL 派生]**。
   * 要在资产之间创建双向关系，请从列表中选择&#x200B;**[!UICONTROL 其他]**。

1. 在&#x200B;**[!UICONTROL 选择资产]**&#x200B;屏幕中，导航到您要关联的资产所在的位置，然后选择它。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击&#x200B;**[!UICONTROL 确认]**。
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。 根据您在步骤3中对关系的选择，相关资产会列在&#x200B;**[!UICONTROL 相关]**&#x200B;部分的相应类别下。 例如，如果您相关的资产是当前资产的源文件，则会列在&#x200B;**[!UICONTROL Source]**&#x200B;下。

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消资产关联，请单击工具栏中的&#x200B;**[!UICONTROL 取消关联]** ![取消资产关联](assets/do-not-localize/link-unrelate-icon.png)。

1. 从&#x200B;**[!UICONTROL 删除关系]**&#x200B;对话框中选择要取消关系的资产，然后单击&#x200B;**[!UICONTROL 取消关系]**。

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。 您删除了关系的资产会从&#x200B;**[!UICONTROL 相关]**&#x200B;部分的相关资产列表中删除。

## 翻译相关资产{#translating-related-assets}

使用相关资产功能在资产之间创建源／派生关系在翻译工作流也很有帮助。 当您对派生资产运行转换工作流时，[!DNL Experience Manager Assets]会自动获取源文件引用的任何资产，并包含该资产进行转换。 这样，源资产引用的资产便会与源资产和派生资产一起进行折算。 例如，假设您的英语副本包括派生资产及其源文件，如所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与另一个资产相关，[!DNL Experience Manager Assets]将获取引用的资产并包含该资产进行转换。

![“资产属性”页显示要包括的转换相关资产的源文件](assets/asset-properties-source-asset.png)

*图：要包括以进行折算的相关资产的源资产。*

1. 按照[创建新的翻译项目](translation-projects.md#create-a-new-translation-project)中的步骤，将源文件夹中的资产翻译为目标语言。 例如，在本例中，将您的资源翻译为法语。

1. 从[!UICONTROL 项目]页面，打开转换文件夹。

1. 单击项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击翻译作业卡下面的省略号以视图翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 在资产]**&#x200B;中显示，以视图资产的转换状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证是否已转换与源相关的资产，请单击源资产。

1. 选择与源相关的资产，然后单击&#x200B;**[!UICONTROL 在资产]**&#x200B;中显示。 此时会显示已转换的相关资产。
