---
title: 使用涂鸦签名将电子签名应用于表单
description: 了解如何使用涂写签名签名AEM自适应Forms。 您可以使用涂写签名和签名步骤在表单上绘制签名。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 9%

---

# 使用涂鸦签名将电子签名应用于表单{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | 本文 |


您可以使用 **潦草签名** 组件和 **签名步骤** 在自适应表单上绘制（涂鸦）签名的组件。 签名步骤组件显示自适应表单的PDF版本。 您需要启用记录文档选项或基于表单模板的自适应表单才能使用签名步骤组件。

![涂鸦符号对话框](/help/forms/using/assets/scribble-signature.png)

## 签名窗口中可用的各种选项

* **答：** 单击 **画笔** 图标，以在画布上绘制您的签名。
* **B：** 单击 **清除** 图标以清除画布上的签名。
* **C：** 单击 **地理位置** 图标以添加地理位置以及签名。
* **D：** 单击 **键盘** 图标，以在画布上键入您的姓名。

选择完成之后![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标时，无法编辑该签名。 如果想要编辑签名，则必须忽略当前签名并使用上面的“画笔/键盘”选项重新签名。

您可以选择 **配置** ![配置](assets/configure.png) 图标来设置涂写签名画布的长宽比。
* 当Scribble签名画布的长宽比小于1时，地理位置信息将添加到Scribble签名画布的底部。

* 当Scribble签名画布的长宽比大于1时，地理位置信息将添加到Scribble签名画布的右侧。

![潦草签名 — bottom](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>签名始终以PNG格式保存。
>

## 配置自适应表单以使用涂鸦签名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 创建已启用记录文档选项或基于表单模板的自适应表单。 有关分步信息，请参阅 [创建自适应表单](../../forms/using/creating-adaptive-form.md).
1. 拖放 **潦草签名** 组件从组件浏览器转换为自适应表单。
1. 选择 **配置** ![配置](assets/configure.png) 图标。 它打开属性浏览器并显示涂写签名组件的属性。 配置涂写签名组件的属性。
1. 将签名步骤组件从组件浏览器拖放到自适应表单中。

   >[!NOTE]
   >
   >签名步骤组件占据表单可用的完整宽度。 建议在包含签名步骤组件的部分中没有任何其他组件。
   >

1. 在内容浏览器中，选择 **表单容器**，然后选择 **配置** ![配置](/help/forms/using/assets/configure.png) 图标。 它可打开属性浏览器并显示自适应表单容器属性。 导航到 **自适应表单容器** > **电子签名** 并取消选择 **启用Adobe Sign** 选项。 选择完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存更改。

   >[!NOTE]
   >
   >将签名步骤组件添加到自适应表单时，会自动选择启用Adobe Sign选项。
   >

1. 选择 **配置** ![配置](assets/configure.png) 图标。 它将打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **元素名称**：指定组件的名称。

   * **标题：** 指定组件的唯一标题。
   * **模板消息：** 指定在加载签名PDF时要显示的消息。 Adobe Sign服务需要一些时间来准备和加载签名PDF。
   * **签名服务：** 选择 **潦草签名** 选项。

   * **CSS类**：指定客户端库的CSS类（如果有）。 使用 [主题](../../forms/using/themes.md) 和 [内联样式](../../forms/using/inline-style-adaptive-forms.md) 而不是CSS类。

   选择完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存更改。 已成功配置签名。

   现在，当您填写表单时，将显示自适应表单的PDF版本，并提供用于签署PDF文档的选项。 有关详细信息，请参阅 [使用涂写签名签署自适应表单](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## 使用涂写签名签署自适应表单 {#sign-an-adaptive-form-using-scribble-signature}

1. 填写自适应表单并到达签名步骤页面后，将显示签名屏幕。

   ![涂鸦符号对话框](/help/forms/using/assets/esignscribblesign.jpg)

1. 单击 **[!UICONTROL 签名]**. 出现涂写符号对话框。 签署表单，然后单击完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存签名。

   ![涂鸦符号对话框](/help/forms/using/assets/scribblewidget.png)

1. 单击“完成”完成签名过程。

   ![完成签名过程](/help/forms/using/assets/scribblecomplete.jpg)

签名将添加到窗体中，窗体控件将移至下一个面板。
