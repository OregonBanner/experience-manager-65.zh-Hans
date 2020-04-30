---
title: 向数字资产中添加水印。
description: 了解如何使用“水印”功能向资产添加数字水印。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 为您的数字资产加水印 {#watermarking}

[!DNL Adobe Experience Manager Assets] 允许您向资产中添加数字水印，以帮助用户验证资产的真实性和版权所有权。 [!DNL Experience Manager Assets] 支持在PNG和JPEG文件上用作水印的文本。

要能够对资产应用水印，请在 [!UICONTROL DAM更新资产工作流中添加水印步骤] 。

1. 访问用 [!DNL Experience Manager] 户界面，然后转到“工 **[!UICONTROL 具”]** >“工 **[!UICONTROL 作流]** ” **[!UICONTROL >“模]**&#x200B;型”。
1. 从“工 **[!UICONTROL 作流模型]** ”页中，选择“ **[!UICONTROL DAM更新资产”工作流]** ，然后单击“ **[!UICONTROL 编辑”]**。

1. 从侧面板中，将添加水 **[!UICONTROL 印步骤拖动到]**[!UICONTROL DAM更新资产工作流] 。

   ![拖动“ [!UICONTROL 添加水印] ”步骤并添加到 [!UICONTROL DAM更新资产工作流]](assets/add_watermark_step_aem_assets.png)2
   *图：拖动“[!UICONTROL 添加水印]”步骤并添加到[!UICONTROL DAM更新资产工作流]。*

   >[!NOTE]
   >
   >将“添加 [!UICONTROL 水印] ”步骤放在“流程缩略图”步 [!UICONTROL 骤之前的任意位置] 。

1. 打开添 **[!UICONTROL 加水印]** ，以显示其属性。
1. 在“参 **[!UICONTROL 数]** ”选项卡中，在各个字段中指定有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请单击“完 **[!UICONTROL 成”]**。

   ![在资产的添加水印步骤中提供参数](assets/arguments_add_watermark_aem_assets.png)

   *图：在中的添加水印步骤中提供参数[!DNL Assets]。*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. 从用户 [!DNL Assets] 界面上传示例资产。 在您在上述步骤中配置的位置，将显示带有字体大小、颜色等的水印。
