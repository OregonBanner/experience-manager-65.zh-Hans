---
title: 多步骤表单序列简介
seo-title: Introduction to multi-step form sequence
description: 借助AEM Forms，您可以定义一系列表单面板，用户可在其中导航和填写自适应表单。
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 54%

---

# 多步骤表单序列简介{#introduction-to-multi-step-form-sequence}

自适应表单使表单作者能够非常轻松地创建多步数据捕获体验。 它内部支持创建多个面板并将每个面板与不同的导航模式关联。表单作者可以在逻辑部中分对表单字段进行分组，并将一个组表示为一个面板。面板之间的整体导航通过面板布局进行控制。作者可以选择以不同的布局排列面板，例如，使用向导布局按顺序放置，或使用选项卡式布局以临时方式放置。 有关面板布局的信息，请参阅 [自适应表单的布局功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表单填写体验中，涉及的步骤不只是捕获数据。完整表单提交可以包括其他步骤，例如，对表单进行数字签名、验证表单中填写的信息、处理付款等。具体因情况而异。

如果您的用例要求执行一组用于数据捕获的步骤，或者有一些法规需要遵循某些步骤，那么AEM Forms提供了一种跨表单实施该通用结构的方法。 表单结构的预先计划的实施定义了表单的步骤序列。![多步骤表单序列的示例](assets/formpipeline.png)

多步骤表单序列的示例

我们来看看一个用例，其中您需要为表单创建用于填充、验证、签名和确认步骤的序列。 创建此类序列的步骤如下所示：

1. 定义表单模板并向其中添加所需的面板。请注意，序列中的每个步骤都应该有一个面板。 但是，可以在面板中包含子面板。

   在本示例中，我们可以添加以下面板：

   * **填写**：它包含用于捕获数据的表单字段。在这里，您可以包含嵌套的子面板，以便为不同类型的信息（如个人、家庭、财务等）创建部分。

   * **验证**：它包含 **验证** 可在基于XFA的自适应表单中使用的组件。 它以只读模式显示在填充面板中捕获的信息以进行验证。

   * **电子签名**：它包含 **签名** 可在基于XFA的自适应表单中使用的组件。 它提供以下签名服务：

      * Adobe Document Cloud eSign 服务
      * 连笔签名
   * **确认**：它包含&#x200B;**摘要**&#x200B;组件，该组件在用户签署表单并到达序列中的“确认（摘要）”步骤后，显示一条确认表单提交的消息。作者可以配置摘要组件的文本、显示感谢消息、显示生成的 PDF 的链接等。


1. 选择根面板的布局作为&#x200B;**[!UICONTROL 向导]**。
1. 完成其余步骤以创建表单模板。有关更多信息，请参阅 [创建自定义自适应表单模板](../../forms/using/custom-adaptive-forms-templates.md).

在表单模板中定义表单序列后，您可以使用它创建将基本结构定义为序列的表单，但您始终能自定义表单以满足您的要求。
