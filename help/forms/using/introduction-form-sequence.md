---
title: 多步骤表单序列简介
description: 借助AEM Forms，您可以定义一系列希望用户在其中导航和填写自适应表单的表单面板。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 37%

---

# 多步骤表单序列简介{#introduction-to-multi-step-form-sequence}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | 本文 |


自适应表单让表单作者能够非常轻松地创建多步数据捕获体验。 它内部支持创建多个面板并将每个面板与不同的导航模式关联。表单作者可以在逻辑部中分对表单字段进行分组，并将一个组表示为一个面板。面板之间的整体导航通过面板布局进行控制。作者可以选择以不同的布局排列面板，例如，使用向导布局按顺序放置，或使用选项卡式布局以即席方式放置。 有关面板布局的信息，请参阅 [自适应表单的布局功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表单填写体验中，涉及的步骤比捕获数据多。 完整的表单提交可能包括其他步骤，如对表单进行数字签名，验证表单中填写的信息和处理付款。 具体因情况而异。

如果您的用例要求执行一组数据捕获步骤，或者存在需要遵循某些步骤的法规，那么AEM Forms提供了一种跨表单实施该通用结构的方法。 表单结构的预想实现定义了表单的步骤顺序。 ![多步骤表单序列的示例](assets/formpipeline.png)

多步骤表单序列的示例

我们来看看一个用例，其中您需要为表单创建用于填充、验证、签名和确认步骤的序列。 要创建此类序列，请执行以下步骤：

1. 定义表单模板并将所需面板添加到其中。 序列中的每个步骤都应有一个面板。但是，可以在面板中包含子面板。

   在此示例中，可以添加以下面板：

   * **填写**：它包含用于捕获数据的表单字段。在此，您可以包含嵌套的子面板，以便为不同类型的信息（如个人、家庭和财务）创建部分。

   * **验证**：它包含 **验证** 可在基于XFA的自适应表单中使用的组件。 它以只读模式显示在填充面板中捕获的信息以进行验证。

   * **电子签名**：它包含 **签名** 可在基于XFA的自适应表单中使用的组件。 它提供以下签名服务：

      * Adobe Document Cloud eSign 服务
      * 连笔签名

   * **确认**：它包含&#x200B;**摘要**&#x200B;组件，该组件在用户签署表单并到达序列中的“确认（摘要）”步骤后，显示一条确认表单提交的消息。作者可以配置摘要组件的文本、显示感谢消息、显示生成的 PDF 的链接等。

1. 选择根面板的布局作为&#x200B;**[!UICONTROL 向导]**。
1. 完成剩余的步骤，以便创建表单模板。 请参阅 [创建自定义自适应表单模板](../../forms/using/custom-adaptive-forms-templates.md).

在表单模板中定义了表单序列后，可以使用它来创建具有定义为相应序列的基本结构的表单。 您可以随时根据自己的要求自定义表单。
