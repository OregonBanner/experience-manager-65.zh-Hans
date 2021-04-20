---
title: 使用涂抹签名将电子签名应用于表单
seo-title: 使用涂抹签名将电子签名应用于表单
description: 使用涂抹对表单进行签名
seo-description: 使用涂抹对表单进行签名
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 使用涂抹签名将电子签名应用于表单{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用&#x200B;**Scribble Signature**&#x200B;组件和&#x200B;**Signature Step**&#x200B;组件在自适应表单上绘制(Scribble)签名。 签名步骤组件显示自适应表单的PDF版本。 要使用签名步骤组件，您需要启用“记录”选项文档或基于表单模板的自适应表单。

这两个组件都提供一个窗口，用于对表单进行签名，如下所示。 您还可以单击geolocation图标![aem_6_3_geolocation](assets/aem_6_3_geolocation.png)向签名添加geolocation。

![“涂抹符号”对话框](assets/scribble-signature.png)

## 配置自适应表单以使用涂抹签名{#configure-an-adaptive-form-to-use-scribble-signature}

1. 创建“记录文档”选项启用或基于表单模板的自适应表单。 有关分步信息，请参阅[创建自适应表单](../../forms/using/creating-adaptive-form.md)。
1. 将&#x200B;**涂抹签名**&#x200B;组件从组件浏览器拖放到自适应表单。
1. 点按&#x200B;**配置** ![配置](assets/configure.png)图标。 它打开属性浏览器并显示“涂抹签名”组件的属性。 配置“涂抹签名”组件的属性。
1. 将签名步骤组件从组件浏览器拖放到自适应表单。

   >[!NOTE]
   >
   >签名步骤组件具有表单可用的全宽。 建议在包含签名步骤组件的部分上不要使用任何其他组件。

1. 在内容浏览器中，点按&#x200B;**表单容器**，然后点按&#x200B;**配置** ![](/help/forms/using/assets/configure.png)图标。 它打开属性浏览器并显示自适应表单容器属性。 导航到&#x200B;**自适应表单容器** > **电子签名**&#x200B;并取消选择&#x200B;**启用Adobe Sign**&#x200B;选项。 点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存更改。

   >[!NOTE]
   >
   >在向自适应表单中添加签名步骤组件时，会自动选择启用Adobe Sign选项。

1. 点按&#x200B;**配置** ![配置](assets/configure.png)图标。 它打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **元素名称**:指定组件的名称。

   * **标题：** 指定组件的唯一标题。
   * **模板消** 息：指定加载签名PDF时要显示的消息。Adobe Sign服务需要一些时间来准备和加载签名PDF。
   * **签名服务：** 选择“ **Scribble签** 名”选项。

   * **CSS类**:指定客户端库的CSS类（如果有）。建议使用[主题](../../forms/using/themes.md)和[内行样式](../../forms/using/inline-style-adaptive-forms.md)代替CSS类。

   点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存更改。 签名已成功配置。

   现在，当您填写表单时，会显示自适应表单的PDF版本，并提供用于签署PDF文档的选项。 有关详细信息，请参阅[使用涂抹签名对自适应表单进行签名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)。

## 使用涂抹签名{#sign-an-adaptive-form-using-scribble-signature}对自适应表单进行签名

1. 在您填写自适应表单并到达签名步骤页面后，将显示签名屏幕。

   ![EchoSign页面的签名屏幕](assets/esignscribblesign.jpg)

1. 单击&#x200B;**[!UICONTROL 签名]**。 出现“涂抹符号”对话框。 对表单进行签名，然后单击完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存签名。

   ![“涂抹符号”对话框](assets/scribblewidget.jpg)

1. 单击“完成”以完成签名过程。

   ![完成签名过程](assets/scribblecomplete.jpg)

签名将添加到表单，表单控件将移至下一个面板。

