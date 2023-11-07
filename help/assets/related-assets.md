---
title: 相关资产
description: 了解如何关联共享某些通用属性的数字资源。 此外，还可以在数字资源之间创建源派生的关系。
contentOwner: AG
role: User
feature: Collaboration,Asset Management
exl-id: ddb69727-74a0-4a4d-a14e-7d3bb5ceea2a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 相关资产 {#related-assets}

[!DNL Adobe Experience Manager Assets] 允许您使用相关资源功能，根据组织的需求手动关联资源。 例如，您可以将许可证文件与类似主题中的资产或图像/视频相关联。 您可以关联共享某些通用属性的资源。 您还可以使用该功能创建资源之间的源/派生关系。 例如，如果有一个从INDD文件生成的PDF文件，则可以将PDF文件与其源INDD文件相关联。

使用此功能，您可以灵活地与供应商或机构共享低分辨率PDF文件或JPG文件，并使高分辨率INDD文件仅在请求时才可用。

>[!NOTE]
>
>只有对资源具有编辑权限的用户才能关联和取消关联资源。

## 关联资源 {#relating-assets}

1. 从 [!DNL Experience Manager] 界面，打开 **[!UICONTROL 属性]** 要关联的资源的页面。

   ![打开资产的“属性”页面以关联资产](assets/asset-properties-relate-assets.png)

   *图： [!DNL Assets] [!UICONTROL 属性] 页面关联资产。*

   或者，从列表视图中选择资产。

   ![chlimage_1-273](assets/chlimage_1-273.png)

   您还可以从收藏集中选择资产。

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. 要将其他资源与您选择的资源相关联，请单击 **[!UICONTROL 相关]** ![相关资产](assets/do-not-localize/link-relate.png) 工具栏中。
1. 执行下列操作之一：

   * 要关联资产的源文件，请选择 **[!UICONTROL 来源]** 从名单上。
   * 要关联派生文件，请选择 **[!UICONTROL 派生]** 从名单上。
   * 要在资产之间创建双向关系，请选择 **[!UICONTROL 其他]** 从名单上。

1. 从 **[!UICONTROL 选择资源]** 屏幕中，导航到要关联的资源的位置，然后选择该资源。

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. 单击 **[!UICONTROL 确认]**.
1. 单击 **[!UICONTROL 确定]** 以关闭对话框。 根据您在步骤3中选择的关系，相关资产列在 **[!UICONTROL 相关]** 部分。 例如，如果您相关的资产是当前资产的源文件，则它列在 **[!UICONTROL 来源]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. 要取消关联资产，请单击 **[!UICONTROL 取消关联]** ![取消关联资源](assets/do-not-localize/link-unrelate-icon.png) 工具栏中。

1. 从中选择要取消关联的资源 **[!UICONTROL 删除关系]** 对话框，然后单击 **[!UICONTROL 取消关联]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. 单击 **[!UICONTROL 确定]** 以关闭对话框。 您为其删除关系的资产将从下的相关资产列表中删除 **[!UICONTROL 相关]** 部分。

## 翻译相关资源 {#translating-related-assets}

使用相关资源功能在资源之间创建源/派生关系在翻译工作流中也很有帮助。 在派生资产上运行翻译工作流时， [!DNL Experience Manager Assets] 自动获取源文件引用的任何资产并将其包含用于翻译。 通过这种方式，源资产引用的资产将随源和派生资产一起转换。 例如，假定您的英语副本包含派生的资源及其源文件，如图所示。

![chlimage_1-281](assets/chlimage_1-281.png)

如果源文件与另一个资产相关， [!DNL Experience Manager Assets] 获取引用的资产并将其包含以供翻译。

![资产属性页面显示要包含以进行翻译的相关资产的源文件](assets/asset-properties-source-asset.png)

*图：要包含以进行翻译的相关资产的源资产。*

1. 按照中的步骤，将源文件夹中的资产翻译为目标语言 [创建翻译项目](translation-projects.md#create-a-new-translation-project). 例如，在本例中，请将您的资产翻译为法语。

1. 从 [!UICONTROL 项目] 页面，打开翻译文件夹。

1. 单击项目拼贴以打开详细信息页面。

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. 单击翻译作业信息卡下方的省略号可查看翻译状态。

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. 选择资产，然后单击 **[!UICONTROL 在资产中展现]** 工具栏以查看资源的翻译状态。

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. 要验证与源相关的资产是否已翻译，请单击源资产。

1. 选择与源相关的资产，然后单击 **[!UICONTROL 在资产中展现]**. 将显示已翻译的相关资产。
