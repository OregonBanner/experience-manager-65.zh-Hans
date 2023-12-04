---
title: 使用延迟加载改进大型表单的性能
description: 延迟加载通过将表单片段的初始化和加载推迟到它们可见时，显着提高了大型复杂自适应表单的性能。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 7%

---

# 使用延迟加载改进大型表单的性能{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/lazy-loading-adaptive-forms.html) |
| AEM 6.5 | 本文 |

## 延迟加载简介 {#introduction-to-lazy-loading}

当表单变得庞大而复杂，并包含数百个和数千个字段时，最终用户在运行时呈现表单时会遇到较长的响应时间。 为了最大限度地缩短响应时间，自适应表单允许您将表单拆分为逻辑片段，并进行配置以延迟片段的初始化或加载，直到片段需要可见为止。 这称为延迟加载。 此外，一旦用户导航到表单中的其他部分并且片段不再可见，将卸载为延迟加载配置的片段。

在配置延迟加载之前，我们先了解要求和准备步骤。

## 正在准备配置延迟加载 {#preparing-to-configure-lazy-loading}

在自适应表单中配置片段的延迟加载之前，请务必定义策略以创建片段，识别脚本中使用或在其他片段中引用的值，并定义规则以控制延迟加载片段中字段的可见性。

* **标识和创建片段**
您只能为延迟加载配置自适应表单片段。 片段是驻留在自适应表单之外的独立区段，可以跨表单重复使用。 因此，实施延迟加载的第一步是识别表单中的逻辑部分并将其转换为片段。 您可以从头开始创建片段，或将现有表单面板另存为片段。

  有关创建片段的更多信息，请参阅 [自适应表单片段](../../forms/using/adaptive-form-fragments.md).

* **标识和标记全局值**
基于Forms的交易涉及动态元素，用于从用户捕获相关数据并对其进行处理以简化表单填写体验。 例如，您的表单在片段X中有字段A，其值决定了另一个片段中字段B的有效性。 在这种情况下，如果片段X标记为延迟加载，则即使未加载片段X，字段A的值也必须可用于验证字段B。 要实现此目的，您可以将字段A标记为全局，这样可以确保在未加载片段X时，其值可用于验证字段B。

  有关如何使字段值全局的信息，请参见 [配置延迟加载](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **编写规则以控制字段的可见性**
Forms包含某些字段和部分，不适用于所有用户且在所有条件下均适用。 Forms作者和开发人员使用可见性或显示隐藏规则，根据用户输入控制他们的可见性。 例如，Office Address字段不会显示在表单的“就业状态”字段中选择“失业”的用户面前。 有关编写规则的更多信息，请参阅 [使用规则编辑器](../../forms/using/rule-editor.md).

  您可以在延迟加载的片段中使用可见性规则，以便仅在需要时显示条件字段。 此外，将条件字段标记为全局，以在延迟加载片段的可见性表达式中引用它。

## 配置延迟加载 {#configuring-lazy-loading}

执行以下步骤以在自适应表单片段上启用延迟加载：

1. 在创作模式下打开自适应表单，其中包含要启用以进行延迟加载的片段。
1. 选择自适应表单片段，然后选择 ![cmppr](assets/cmppr.png).
1. 在侧栏中，启用 **[!UICONTROL 缓慢地加载片段]** 并选择 **完成**.

   ![为自适应表单片段启用延迟加载](assets/lazy-loading-fragment.png)

   片段现在可用于延迟加载。

您可以将延迟加载片段中对象的值标记为全局，以便在未加载包含的片段时可以在脚本中使用它们。 执行以下操作：

1. 在创作模式下打开自适应表单片段。
1. 选择要将其值标记为全局的字段，然后选择 ![cmppr](assets/cmppr.png).
1. 在侧栏中，启用 **在延迟加载期间使用值**.

   ![侧栏中的延迟加载字段](assets/enable-lazy-loading.png)

   该值现在标记为全局，并且将在脚本中使用，即使卸载包含的片段时也是如此。

## 配置延迟加载的注意事项和最佳实践 {#considerations-and-best-practices-for-configuring-lazy-loading}

处理延迟加载时要牢记的一些限制、建议和要点如下：

* 在基于XFA的自适应表单上使用基于XSD架构的自适应表单来配置大型表单上的延迟加载。 在基于XFA的自适应表单中，由于延迟加载实施导致的性能增益相对低于在基于XSD的自适应表单中的增益。
* 不要在使用自适应表单的片段上配置延迟加载 **[!UICONTROL 响应式 — 页面上的所有内容，无需导航]** 根面板的布局。 作为响应式布局配置的结果，所有片段将以自适应表单同时加载。 它还会导致性能降低。
* 建议不要在自适应表单的第一个片段上配置延迟加载。
* 建议不要在加载自适应表单时呈现的第一个面板中为片段配置延迟加载。
* 片段层次结构中最多支持两个级别的延迟加载。
* 确保在自适应表单中标记为全局的字段是唯一的。
* 考虑为应根据条件显示或隐藏的片段编写可见性规则。 例如，您可以根据用户指定的婚姻状况显示或隐藏“配偶详细信息”片段。
* 延迟加载的片段不支持文件附件和条款和条件组件。

### 编写配置延迟加载的最佳实践脚本 {#scripting-best-practices-for-configuring-lazy-loading}

在开发用于延迟加载面板的脚本时要牢记以下几点：

* 确保用于延迟加载片段的字段上的初始化和计算脚本本质上为幂等。 幂等脚本是指即使在多次执行后具有相同效果的脚本。
* 使用字段的全局可用属性，使延迟加载面板中的字段值可用于表单的所有其他面板。
* 无论是否跨片段全局标记字段，都不要转发延迟面板中字段的引用值。
* 使用面板重置功能，可通过以下单击表达式重置面板上可见的所有内容。\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;： &quot;navigablePanel&quot;}))。resetData()
