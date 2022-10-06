---
title: “教程：创建自适应表单`
seo-title: Create an adaptive form
description: 了解如何创建、布局和预览自适应表单。 此外，了解如何配置提交操作。
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# 教程：创建自适应表单 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是 [创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md) 系列。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

## 关于教程 {#about-the-tutorial}

自适应表单是新一代动态响应式表单。 您可以使用自适应表单来提供个性化体验。 您还可以将自适应表单与 [!DNL Adobe Analytics] 用于使用情况统计和 [!DNL Adobe Campaign] 用于营销活动管理。 有关自适应表单功能的更多信息，请参阅 [创作自适应表单简介](/help/forms/using/introduction-forms-authoring.md).

在遵循正确的流程后，创建和管理表单会更加容易。 在本文中，您将学习如何：

* [创建允许客户添加送货地址的自适应表单](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [用于显示和接受客户信息的自适应表单的布局字段](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [创建提交操作以发送包含表单内容的电子邮件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [预览和提交自适应表单](/help/forms/using/create-adaptive-form.md)

在文章末尾，您将拥有一个类似于以下内容的表单：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步骤1:创建自适应表单 {#step-create-the-adaptive-form}

1. 登录到AEM创作实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**. 默认URL为 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. 点按 **[!UICONTROL 创建]** 选择 **[!UICONTROL 自适应表单]**. 此时会显示用于选择模板的选项。 点按 **[!UICONTROL 空白]** 选择模板并点按 **[!UICONTROL 下一个]**.

1. 选项 **[!UICONTROL 添加属性]** 中。 的 **[!UICONTROL 标题]** 和 **[!UICONTROL 名称]** 字段为必填字段：

   * **标题：** 指定 `Add new or update shipping address` 在 **[!UICONTROL 标题]** 字段。 标题字段指定表单的显示名称。 标题可帮助您识别AEM中的表单 [!DNL Forms] 用户界面。
   * **名称：** 指定 `shipping-address-add-update-form` 在 **[!UICONTROL 名称]** 字段。 “名称”字段指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。

1. 点按&#x200B;**[!UICONTROL 创建]**。随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。 点按 **[!UICONTROL 打开]** 在新选项卡中打开新创建的表单。 随即会打开表单进行编辑。 它还会显示侧栏，以根据需要自定义新创建的表单。

   有关自适应表单创作界面和可用组件的信息，请参阅 [创作自适应表单简介](/help/forms/using/creating-adaptive-form.md).

   ![新创建的自适应表单](assets/newly-created-adaptive-form.png)

## 步骤2:添加页眉和页脚 {#step-add-header-and-footer}

AEM [!DNL Forms] 提供了许多组件，用于在自适应表单上显示信息。 页眉和页脚组件有助于为表单提供一致的外观。 标题通常包括公司徽标、表单标题和摘要。 页脚通常包括版权信息和指向其他页面的链接。

1. 点按 ![切换侧面板](assets/toggle-side-panel.png) > ![树展开](assets/treeexpandall.png). 此时会打开组件浏览器。 拖动 **[!UICONTROL 标题]** 组件从组件浏览器转换到自适应表单。
1. 点按 **[!UICONTROL 徽标]**. 此时会出现工具栏。 点按 ![aem_6_3_edit](assets/aem_6_3_edit.png) 在工具栏上，键入 **We.Retail**，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. 点按图像。 此时会出现工具栏。 点按 ![cppr](assets/cmppr.png). 此时将在屏幕左侧打开属性浏览器。 **[!UICONTROL 浏览]** 并上传徽标图像。 点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 图像显示在标题上。

   如果您没有徽标，则可以点按获取文件以下载本文中使用的徽标。

[获取文件](assets/logo.png)

1. 拖动 **[!UICONTROL 页脚]** 组件从 ![树展开](assets/treeexpandall.png) 到自适应表单。 此时，表单如下所示：

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 步骤3:添加组件以捕获和显示信息 {#step-add-components-to-capture-and-display-information}

组件是自适应表单的构建基块。 AEM [!DNL Forms] 提供了许多组件，用于在自适应表单中捕获和显示信息。 您可以将组件从 ![树展开](assets/treeexpandall.png) 到表单。 要了解可用组件和相应的功能，请参阅 [创作自适应表单简介](/help/forms/using/introduction-forms-authoring.md).

1. 拖动 **[!UICONTROL 数字框组件]** 到自适应表单。 将其放在页脚组件之前。 打开组件的属性，更改 **[!UICONTROL 标题]** 的 **`Customer ID`**，更改 **[!UICONTROL 元素名称]** to **`customer_ID`**，启用 **[!UICONTROL 必填字段]** 选项，启用 **[!UICONTROL 使用HTML5数字输入类型]** 选项，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 将三个文本框组件拖到自适应表单中。 将它们放在页脚组件之前。 为这些文本框设置以下属性。: 

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>文本框1<br/></b></td> 
      <td><b>文本框2<br/></b></td> 
      <td><b>文本框3</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>名称<br /> </td> 
      <td>配送地址</td> 
      <td>状态</td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_state</td> 
     </tr> 
     <tr> 
      <td>必填字段</td> 
      <td>启用</td> 
      <td>启用</td> 
      <td>启用</td> 
     </tr> 
     <tr> 
      <td>允许多行<br /> </td> 
      <td>已禁用</td> 
      <td>启用</td> 
      <td>已禁用</td> 
     </tr> 
    </tbody> 
   </table>

1. 拖动 **[!UICONTROL 数值框]** 组件。 打开组件的属性，设置下表中列出的值，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 值 |
   |---|---|
   | 标题 | 邮政编码 |
   | 元素名称 | customer_ZIPCode |
   | 最大数字数量 | 6 |
   | 必填字段 | 启用 |
   | 显示图案类型 | 无模式 |

1. 拖动 **[!UICONTROL 电子邮件]** 组件。 打开组件的属性，设置下表中列出的值，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 值 |
   |---|---|
   | 标题 | 电子邮件 |
   | 元素名称 | customer_Email |
   | 必填字段 | 启用 |

1. 拖动 **[!UICONTROL 文件附件]** 组件。 打开组件的属性，设置下表中列出的值，然后点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>政府批准的地址证明<br /> </td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>必填字段</td> 
      <td>启用</td> 
     </tr> 
    </tbody> 
   </table>

1. 拖动 **[!UICONTROL 提交按钮]** 组件添加到自适应表单。 将其放在页脚组件之前。 打开组件的属性，将元素名称更改为 `address_addition_update_submit`，点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 表单的布局已完成，表单如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步骤4:为自适应表单配置提交操作 {#step-configure-submit-action-for-the-adaptive-form}

当用户点按自适应表单上的“提交”按钮时，会触发提交操作。 您可以使用提交操作将表单数据保存到本地存储库、将表单数据发送到REST端点、将表单数据作为电子邮件发送，等等。 自适应表单提供了一些现成的提交操作。 有关详细信息，请参阅 [配置提交操作](/help/forms/using/configuring-submit-actions.md).

使用以下步骤，您可以配置表单的电子邮件提交操作和演示提交操作：

1. 配置电子邮件服务器。 有关详细信息，请参阅 [配置电子邮件通知](/help/sites-administering/notification.md).


1. 点按 **[!UICONTROL 表单容器]** 在内容浏览器中，然后点按 ![cppr](assets/cmppr.png). 将在左侧打开属性浏览器。
1. 转到 **[!UICONTROL 提交]** >  **[!UICONTROL 提交操作]**. 选择 **[!UICONTROL 发送电子邮件]**. 指定以下值并点按 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 属性 | 值 |
   |--- |--- |
   | 发件人 | `donotreply@weretail.com` |
   | 收件人 | `${customer_Email}` |
   | 主题 | 确认：您已在We.Retail网站上添加送货地址。 |
   | 电子邮件模板 | 你好 `${customer_Name}`，以下地址将添加为您帐户的送货地址： <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> 此致，We.Retail |
   | 包含附件 | 启用 |

   您的表单已准备就绪。 现在，您可以预览表单并测试功能。 如果您使用了本教程中提到的名称，并在运行AEM的计算机上访问该表单 [!DNL Forms] ，则表单可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## 步骤5:预览和提交自适应表单 {#step-preview-and-submit-the-adaptive-form}

您可以使用 **[!UICONTROL 预览选项]** 来评估表单的外观和行为。 您可以在预览模式下提交表单，还可以检查对表单应用的验证。 例如，如果必填字段留空时显示错误。

自适应表单还提供了一个选项，用于模拟各种设备的表单体验。 例如，iPhone、iPad和桌面。 您可以同时使用 **[!UICONTROL 预览]** 和 **[!UICONTROL 模拟器]** ![标尺](assets/ruler.png) 可预览不同屏幕大小设备的表单的选项。

1. 点按 **[!UICONTROL 预览]** 选项。 在预览模式下将打开表单。 如果您使用了教程中提到的名称，则表单的预览URL为 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![标尺](assets/ruler.png) 查看表单在各种设备上的显示方式。
1. 填写表单的字段并点按 **[!UICONTROL 提交]**. 表单已提交，您将被重定向到默认设置 **谢谢** 页面。 您还可以指定自定义的感谢页面。 有关详细信息，请参阅 [配置重定向页面](/help/forms/using/configuring-redirect-page.md).

添加地址的自适应表单已准备就绪。 如果您使用了教程中提到的名称，并在运行AEM Forms服务器的计算机上访问表单，则表单将在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
