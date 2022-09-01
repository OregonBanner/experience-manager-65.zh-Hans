---
title: 使用涂写签名将电子签名应用于表单
seo-title: Apply electronic signatures to a form using scribble signatures
description: 使用涂写对表单进行签名
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# 使用涂写签名将电子签名应用于表单{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用 **潦草签名** 组件和 **签名步骤** 用于在自适应表单上绘制（涂写）签名的组件。 签名步骤组件显示自适应表单的PDF版本。 您需要启用记录文档选项或基于表单模板的自适应表单才能使用签名步骤组件。

![涂写符号对话框](/help/forms/using/assets/scribble-signature.png)

## 签名窗口中可用的各种选项

* **答：** 单击 **画笔** 图标，在画布上绘制您的签名。
* **B:** 单击 **清除** 图标以在画布上清除签名。
* **C:** 单击 **地理位置** 图标添加地理位置和签名。
* **D:** 单击 **键盘** 图标在画布上键入您的名称。

在您点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标，则无法编辑签名。 如果要编辑签名，则必须忽略当前签名，然后使用上述“画笔/键盘”选项重新签名。

您可以点按 **配置** ![配置](assets/configure.png) 图标来设置潦草签名画布的宽高比。
* 当涂写签名画布的宽高比小于1时，地理位置信息将添加到涂写签名画布的底部。

* 当涂写签名画布的宽高比大于1时，地理位置信息将添加到涂写签名画布的右侧。

![潦草的签名 — 底部](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>签名始终以PNG格式保存。

## 配置自适应表单以使用涂写签名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 创建“记录文档”选项，或创建基于表单模板的自适应表单。 有关分步信息，请参阅 [创建自适应表单](../../forms/using/creating-adaptive-form.md).
1. 拖放 **潦草签名** 组件从组件浏览器转换到自适应表单。
1. 点按 **配置** ![配置](assets/configure.png) 图标。 它会打开属性浏览器并显示潦草签名组件的属性。 配置潦草签名组件的属性。
1. 将签名步骤组件从组件浏览器拖放到自适应表单。

   >[!NOTE]
   >
   >签名步骤组件占用表单的全宽。 建议在包含签名步骤组件的部分上不要包含任何其他组件。

1. 在内容浏览器中，点按 **表单容器**，然后点按 **配置** ![](/help/forms/using/assets/configure.png) 图标。 它会打开属性浏览器并显示自适应表单容器属性。 导航到 **自适应表单容器** > **电子签名** 并取消选择 **启用Adobe Sign** 选项。 点按完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存更改。

   >[!NOTE]
   >
   >将签名步骤组件添加到自适应表单时，会自动选择启用Adobe Sign选项。

1. 点按 **配置** ![配置](assets/configure.png) 图标。 它会打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **元素名称**:指定组件的名称。

   * **标题：** 指定组件的唯一标题。
   * **模板消息：** 指定加载签名PDF时要显示的消息。 Adobe Sign服务需要一些时间来准备和加载签名PDF。
   * **签名服务：** 选择 **潦草签名** 选项。

   * **CSS类**:指定客户端库的CSS类（如果有）。 建议使用 [主题](../../forms/using/themes.md) 和 [内嵌样式](../../forms/using/inline-style-adaptive-forms.md) 而不是CSS类。

   点按完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存更改。 签名配置成功。

   现在，当您填写表单时，将显示自适应表单的PDF版本，并提供用于签署PDF文档的选项。 有关详细信息，请参阅 [使用涂写签名对自适应表单进行签名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## 使用涂写签名对自适应表单进行签名 {#sign-an-adaptive-form-using-scribble-signature}

1. 填写自适应表单并进入签名步骤页面后，将显示签名屏幕。

   ![涂写符号对话框](/help/forms/using/assets/esignscribblesign.jpg)

1. 单击 **[!UICONTROL Sign]**. 出现涂写符号对话框。 对表单进行签名，然后单击完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 图标以保存签名。

   ![涂写符号对话框](/help/forms/using/assets/scribblewidget.png)

1. 单击完成以完成签名过程。

   ![完成签名过程](/help/forms/using/assets/scribblecomplete.jpg)

签名将添加到表单中，表单控件将移至下一个面板。
