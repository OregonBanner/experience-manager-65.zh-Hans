---
title: 将水印添加到您的数字资产。
description: 了解如何使用水印功能向资产添加数字水印。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5035d3457187f4d5fe5c2af255a1a886df7291b4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 为数字资产加水印 {#watermarking}

[!DNL Adobe Experience Manager Assets] 允许您向资产添加数字水印，帮助用户验证资产的真实性和版权所有权。 [!DNL Experience Manager Assets] 支持文本以用作PNG和JPEG文件上的水印。

要能够对资产应用水印，请在DAM更新资产工作流中添 [!UICONTROL 加水印步骤] 。

1. 访问用 [!DNL Experience Manager] 户界面，然后转到 **[!UICONTROL 工具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模]**&#x200B;型。
1. 在“工作 **[!UICONTROL 流模型]** ”页中，选择 **[!UICONTROL DAM更新资产工作流]** ，然后单 **[!UICONTROL 击编辑]**。

1. 从侧面板中，将添加水 **[!UICONTROL 印步骤拖]** 到DAM更 [!UICONTROL 新资产工作流] 。

   ![拖动添 [!UICONTROL 加水印] ，并添加到 [!UICONTROL DAM更新资产工作流] 2](assets/add_watermark_step_aem_assets.png)
   *图： 拖动添[!UICONTROL 加水印]，并添加到[!UICONTROL DAM更新资产工作流]。*

   >[!NOTE]
   >
   >将添加 [!UICONTROL 水印步骤放] 在“流程缩略图 [!UICONTROL ”步骤之前的任] 意位置。

1. 打开添 **[!UICONTROL 加水印]** ，以显示其属性。
1. 在“参 **[!UICONTROL 数]** ”选项卡中，在各个字段中指定有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请单击“ **[!UICONTROL 完成]**”。

   ![在资产的添加水印步骤中提供参数](assets/arguments_add_watermark_aem_assets.png)

   *图： 在中的添加水印步骤中提供参数[!DNL Assets]。*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. 从用户 [!DNL Assets] 界面上传示例资产。 在您在上述步骤中配置的位置，将显示带有字体大小、颜色等的水印。

要以编程方式或使用动态信息对PDF文档进行水印，请考 [虑使用AEM文档服务](/help/forms/using/overview-aem-document-services.md) 。
