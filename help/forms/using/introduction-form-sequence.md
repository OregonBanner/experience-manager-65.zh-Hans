---
title: 多步骤表单序列简介
seo-title: Introduction to multi-step form sequence
description: 透過AEM Forms，您可以定義一系列表單面板，讓使用者在其中導覽及填寫最適化表單。
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

最適化表單可讓表單作者輕鬆建立多步驟資料擷取體驗。 它内部支持创建多个面板并将每个面板与不同的导航模式关联。表单作者可以在逻辑部中分对表单字段进行分组，并将一个组表示为一个面板。面板之间的整体导航通过面板布局进行控制。作者可以選擇以不同的版面配置來排列面板，例如，使用「精靈」版面配置按順序放置，或使用「索引標籤」版面配置以臨機操作方式放置。 如需面板配置的相關資訊，請參閱 [調適型表單的版面配置功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表单填写体验中，涉及的步骤不只是捕获数据。完整表单提交可以包括其他步骤，例如，对表单进行数字签名、验证表单中填写的信息、处理付款等。具体因情况而异。

如果您的使用案例需要一組資料擷取步驟，或有一些法規需要遵循某些步驟，AEM Forms會提供在表單中強制執行該通用結構的方法。 表单结构的预先计划的实施定义了表单的步骤序列。![多步骤表单序列的示例](assets/formpipeline.png)

多步骤表单序列的示例

以您需要建立表單填寫、驗證、簽署和確認步驟的序列的使用案例為例。 创建此类序列的步骤如下所示：

1. 定义表单模板并向其中添加所需的面板。請注意，序列中的每個步驟都應該有一個面板。 不過，您可以在面板中包含子面板。

   在本示例中，我们可以添加以下面板：

   * **填写**：它包含用于捕获数据的表单字段。在這裡，您可以包含巢狀子面板，以針對不同型別的資訊（例如個人、家庭、財務等）建立區段。

   * **驗證**：此變數包含 **驗證** 可用於XFA型最適化表單的元件。 它以唯讀模式顯示「填滿」面板中擷取的資訊以進行驗證。

   * **電子簽章**：此變數包含 **簽署** 可用於XFA型最適化表單的元件。 它提供下列簽署服務：

      * Adobe Document Cloud eSign 服务
      * 连笔签名
   * **确认**：它包含&#x200B;**摘要**&#x200B;组件，该组件在用户签署表单并到达序列中的“确认（摘要）”步骤后，显示一条确认表单提交的消息。作者可以配置摘要组件的文本、显示感谢消息、显示生成的 PDF 的链接等。


1. 选择根面板的布局作为&#x200B;**[!UICONTROL 向导]**。
1. 完成其余步骤以创建表单模板。如需詳細資訊，請參閱 [建立自訂最適化表單範本](../../forms/using/custom-adaptive-forms-templates.md).

在表单模板中定义表单序列后，您可以使用它创建将基本结构定义为序列的表单，但您始终能自定义表单以满足您的要求。
