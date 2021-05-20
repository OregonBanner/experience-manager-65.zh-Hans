---
title: 使用涂写签名将电子签名应用于表单
seo-title: 使用涂写签名将电子签名应用于表单
description: 使用涂写对表单进行签名
seo-description: 使用涂写对表单进行签名
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: 自适应表单
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---

# 使用涂写签名将电子签名应用于表单{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用&#x200B;**涂写签名**&#x200B;组件和&#x200B;**签名步骤**&#x200B;组件在自适应表单上绘制（涂写）签名。 签名步骤组件显示自适应表单的PDF版本。 您需要启用记录文档选项或基于表单模板的自适应表单才能使用签名步骤组件。

这两个组件都提供了一个用于签署表单的窗口，如下所示。 您还可以单击地理位置图标![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) ，以向签名添加地理位置。

![涂写符号对话框](assets/scribble-signature.png)

## 配置自适应表单以使用涂写签名{#configure-an-adaptive-form-to-use-scribble-signature}

1. 创建“记录文档”选项，或创建基于表单模板的自适应表单。 有关分步信息，请参阅[创建自适应表单](../../forms/using/creating-adaptive-form.md)。
1. 将&#x200B;**涂写签名**&#x200B;组件从组件浏览器拖放到自适应表单。
1. 点按&#x200B;**配置** ![配置](assets/configure.png)图标。 它会打开属性浏览器并显示潦草签名组件的属性。 配置潦草签名组件的属性。
1. 将签名步骤组件从组件浏览器拖放到自适应表单。

   >[!NOTE]
   >
   >签名步骤组件占用表单的全宽。 建议在包含签名步骤组件的部分上不要包含任何其他组件。

1. 在内容浏览器中，点按&#x200B;**表单容器**，然后点按&#x200B;**配置** ![](/help/forms/using/assets/configure.png)图标。 它会打开属性浏览器并显示自适应表单容器属性。 导航到&#x200B;**自适应表单容器** > **电子签名**&#x200B;并取消选择&#x200B;**启用Adobe Sign**&#x200B;选项。 点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存更改。

   >[!NOTE]
   >
   >将签名步骤组件添加到自适应表单时，会自动选择启用Adobe Sign选项。

1. 点按&#x200B;**配置** ![配置](assets/configure.png)图标。 它会打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **元素名称**:指定组件的名称。

   * **标题：** 指定组件的唯一标题。
   * **模板消息：** 指定加载签名PDF时要显示的消息。Adobe Sign服务需要一些时间来准备和加载签名PDF。
   * **签名服务：** 选择“涂 **写签** 名”选项。

   * **CSS类**:指定客户端库的CSS类（如果有）。建议使用[主题](../../forms/using/themes.md)和[内行样式](../../forms/using/inline-style-adaptive-forms.md)，而不是CSS类。

   点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存更改。 签名配置成功。

   现在，当您填写表单时，会显示自适应表单的PDF版本，并提供对PDF文档进行签名的选项。 有关详细信息，请参阅[使用涂写签名对自适应表单进行签名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)。

## 使用涂写签名{#sign-an-adaptive-form-using-scribble-signature}对自适应表单进行签名

1. 填写自适应表单并进入签名步骤页面后，将显示签名屏幕。

   ![EchoSign页面的签名屏幕](assets/esignscribblesign.jpg)

1. 单击&#x200B;**[!UICONTROL Sign]**。 出现涂写符号对话框。 对表单进行签名，然后单击完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存签名。

   ![涂写符号对话框](assets/scribblewidget.jpg)

1. 单击完成以完成签名过程。

   ![完成签名过程](assets/scribblecomplete.jpg)

签名将添加到表单中，表单控件将移至下一个面板。
