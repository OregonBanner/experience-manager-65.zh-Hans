---
title: 使用延迟加载改进大型表单的性能
seo-title: Improve performance of large forms with lazy loading
description: 延迟加载通过将表单片段的初始化和加载推迟到它们可见之前，显着提高了大型和复杂自适应表单的性能。
seo-description: Lazy loading significantly improves the performance of large and complex adaptive forms by deferring initialization and loading of form fragments until they are visible.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
feature: Adaptive Forms
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 3%

---

# 使用延迟加载改进大型表单的性能{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/lazy-loading-adaptive-forms.html) |
| AEM 6.5 | 本文 |

## 延迟加载简介 {#introduction-to-lazy-loading}

当表单变得庞大而复杂，包含成千上万个字段时，最终用户在运行时呈现表单时会遇到较长的响应时间。 为了最大限度地缩短响应时间，自适应表单允许您将表单拆分为逻辑片段，并进行配置以推迟片段的初始化或加载，直到片段需要可见为止。 这称为延迟加载。 此外，当用户导航到表单中的其他部分并且片段不再可见时，将卸载为延迟加载配置的片段。

在配置延迟加载之前，我们先了解要求和准备步骤。

## 正在准备配置延迟加载 {#preparing-to-configure-lazy-loading}

在自适应表单中配置片段的延迟加载之前，请务必定义创建片段的策略、识别脚本中使用或在其他片段中引用的值，以及定义用于控制延迟加载片段中字段的可见性的规则。

* **标识和创建片段**
您只能为延迟加载配置自适应表单片段。 片段是驻留在自适应表单之外的独立区段，可以跨表单重复使用。 因此，实施延迟加载的第一步是识别表单中的逻辑部分并将其转换为片段。 您可以从头开始创建片段或将现有表单面板另存为片段。

  有关创建片段的更多信息，请参阅 [自适应表单片段](../../forms/using/adaptive-form-fragments.md).

* **标识和标记全局值**
基于Forms的交易涉及动态元素，用于从用户捕获相关数据并对其进行处理以简化表单填写体验。 例如，您的表单在片段X中有字段A，其值决定了另一个片段中字段B的有效性。 在这种情况下，如果片段X标记为延迟加载，则字段A的值必须可用于验证字段B，即使未加载片段X也是如此。 要实现此目的，您可以将字段A标记为全局字段，以确保在未加载片段X时，其值可用于验证字段B。

  有关如何使字段值全局的信息，请参见 [配置延迟加载](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **编写规则以控制字段的可见性**
Forms包含一些字段和部分，不适用于所有用户且适用于所有条件。 Forms作者和开发人员使用可见性或显示隐藏规则，根据用户输入控制他们的可见性。 例如，Office Address字段不会显示在表单的就业状态字段中选择失业的用户面前。 有关编写规则的更多信息，请参阅 [使用规则编辑器](../../forms/using/rule-editor.md).

  您可以利用延迟加载片段中的可见性规则，以便仅在需要时显示条件字段。 此外，标记条件字段全局，以便在延迟加载片段的可见性表达式中引用它。

## 配置延迟加载 {#configuring-lazy-loading}

执行以下步骤以在自适应表单片段上启用延迟加载：

1. 在创作模式下打开自适应表单，该表单包含要启用以进行延迟加载的片段。
1. 选择自适应表单片段并点按 ![cmppr](assets/cmppr.png).
1. 在侧栏中，启用 **[!UICONTROL 缓慢地加载片段]** 并点按 **完成**.

   ![为自适应表单片段启用延迟加载](assets/lazy-loading-fragment.png)

   片段现在支持延迟加载。

您可以将延迟加载片段中对象的值标记为全局，以便在未加载包含的片段时可以在脚本中使用它们。 执行以下操作：

1. 在创作模式下打开自适应表单片段。
1. 点按要将其值标记为全局的字段，然后点按 ![cmppr](assets/cmppr.png).
1. 在侧栏中，启用 **在延迟加载期间使用值**.

   ![侧栏中的延迟加载字段](assets/enable-lazy-loading.png)

   该值现在标记为全局，并且将在脚本中使用，即使卸载包含的片段时也是如此。

## 配置延迟加载的注意事项和最佳实践 {#considerations-and-best-practices-for-configuring-lazy-loading}

处理延迟加载时要牢记的一些限制、建议和重要要点如下：

* 建议在基于XFA的自适应表单上使用基于XSD架构的自适应表单，以配置大型表单上的延迟加载。 在基于XFA的自适应表单中，由于延迟加载实现导致的性能增益相对小于在基于XSD的自适应表单中。
* 不要在使用自适应表单的片段上配置延迟加载 **[!UICONTROL 响应式 — 页面上的所有内容，无需导航]** 根面板的布局。 作为响应式布局配置的结果，所有片段都将以自适应表单同时加载。 它还会导致性能下降。
* 建议不要在自适应表单的第一个片段上配置延迟加载。
* 建议不要在加载自适应表单时呈现的第一个面板中为片段配置延迟加载。
* 片段层次结构中最多支持两级延迟加载。
* 确保标记为全局的字段在自适应表单中是唯一的。
* 考虑为应根据条件显示或隐藏的片段编写可见性规则。 例如，您可以根据用户指定的婚姻状况显示或隐藏“配偶详细信息”片段。
* 延迟加载的片段不支持文件附件和条款和条件组件。

### 配置延迟加载的脚本最佳实践 {#scripting-best-practices-for-configuring-lazy-loading}

在开发用于延迟加载面板的脚本时，请记住以下要点：

* 确保用于延迟加载片段的字段上的初始化和计算脚本本质上为幂等。 幂等脚本是指即使在多次执行后具有相同效果的脚本。
* 使用字段的全局可用属性，使位于延迟加载面板中的字段值可用于表单的所有其他面板。
* 无论字段是否在片段中全局标记，都不要转发延迟面板中字段的引用值。
* 使用面板重置功能，可通过以下单击表达式重置面板上可见的所有内容。\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;： &quot;navigablePanel&quot;}))。resetData()
