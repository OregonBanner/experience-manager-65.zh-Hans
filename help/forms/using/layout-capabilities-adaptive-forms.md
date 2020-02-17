---
title: 自适应表单的布局功能
seo-title: 自适应表单的布局功能
description: 自适应表单在各种设备上的布局和外观受布局设置的约束。 了解各种布局以及如何应用它们。
seo-description: 自适应表单在各种设备上的布局和外观受布局设置的约束。 了解各种布局以及如何应用它们。
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619

---


# 自适应表单的布局功能{#layout-capabilities-of-adaptive-forms}

Adobe Experience Manager(AEM)允许您创建易于使用的自适应表单，为最终用户提供动态体验。 表单布局控制项目或组件在自适应表单中的显示方式。

## 入门知识 {#prerequisite-knowledge}

在了解自适应表单的不同布局功能之前，请阅读以下文章以了解有关自适应表单的更多信息。

[AEM Forms简介](../../forms/using/introduction-aem-forms.md)

[表单创作简介](../../forms/using/introduction-forms-authoring.md)

## 布局类型 {#types-of-layouts}

自适应表单为您提供以下类型的布局：

**面板布局** 控制面板内的项目或组件在设备上的显示方式。

**移动布局** -控制在移动设备上导航表单。 如果设备宽度为768像素或更大，则布局被视为移动布局并针对移动设备进行优化。

**工具栏布局** -控制表单中工具栏或面板工具栏中“操作”按钮的位置。

以下位置定义了所有这些面板布局：

`/libs/fd/af/layouts`.

>[!NOTE]
>
>要更改自适应表单的布局，请使用AEM中的创作模式。

![CRX存储库中布局的位置](assets/layouts_location_in_crx.png)

## 面板布局 {#panel-layout}

表单作者可以将布局与自适应表单的每个面板（包括根面板）相关联。

面板布局在位置 `/libs/fd/af/layouts/panel` 可用。

![自适应表单根面板的面板布局列表](assets/layouts.png)

自适应表单中的面板布局列表

### Responsive - everything on one page without navigation {#responsive-everything-on-one-page-without-navigation-br}

使用此面板布局可创建响应式布局，该布局可根据设备的屏幕大小进行调整，而无需特殊导航。

使用此布局，您可以将多个面 **[!UICONTROL 板自适应表单组件]** ，一个接一个地放在面板中。

![使用响应式布局的表单（如小屏幕上所示）](assets/responsive_layout_seen_on_small_screen.png)

使用响应式布局的表单（如小屏幕上所示）

![使用响应式布局的表单，如大屏幕所示](assets/responsive_layout_seen_on_large_screen.png)

使用响应式布局的表单，如大屏幕所示

### 向导——一个多步骤表单，一次显示一个步骤 {#wizard-a-multi-step-form-showing-one-step-at-a-time}

使用此面板布局在表单内提供引导式导航。 例如，当您希望在逐步引导用户的同时捕获表单中的必需信息时，请使用此布局。

使用该 `Panel adaptive form` 组件可在面板中提供分步导航。 当您使用此布局时，用户仅在当前步骤完成后才会移动到下一步

```
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![多步骤表单的向导布局中的步骤完成表达式](assets/layout-sidebar.png)

多步骤表单的向导布局中的步骤完成表达式

![使用向导布局的表单](assets/wizard-layout.png)

使用向导的表单

### 折叠式设计的布局 {#layout-for-accordion-design}

使用此布局，您可以将组件放 `Panel adaptive form` 置到具有折叠样式导航的面板中。 使用此布局，您还可以创建可重复的面板。 可重复的面板使您能够根据需要动态添加或删除面板。 您可以定义面板重复的最小次数和最大次数。 此外，可以根据面板项目中提供的信息动态地确定面板的标题。

摘要表达式可用于在最小化面板的标题中显示最终用户提供的值。

![在自适应表单中使用折叠布局的可重复面板](assets/repeatable_panels_using_accordion_layout.png)

使用Accordion布局创建的可重复面板

### 选项卡式布局——选项卡显示在左侧 {#tabbed-layout-tabs-appear-on-the-left}

使用此布局，您可以将组件放 `Panel adaptive form` 置到具有选项卡导航的面板中。 这些选项卡位于面板内容的左侧。

![在选项卡式布局中，选项卡显示在左侧](assets/tabbed_layout_left.png)

面板左侧显示的选项卡

### 选项卡式布局——选项卡显示在顶部 {#tabbed-layout-tabs-appear-on-the-top}

使用此布局，您可以将组件放 `Panel adaptive form` 置到具有选项卡导航的面板中。 这些选项卡位于面板内容的顶部。

![自适应表单中的选项卡式布局，顶部带有选项卡](assets/tabbed_layout_top.png)

显示在面板顶部的选项卡

## 移动布局 {#mobile-layouts}

移动布局允许在屏幕相对较小的移动设备上进行用户友好的导航。 移动布局使用选项卡式或向导式样式进行表单导航。 应用移动布局可为整个表单提供单一布局。

此布局使用导航栏和导航菜单控制导航。 导航栏显示&lt; **and** >图标以指示表单中 **的下一** 个和上一个导航步骤 ******** 。

移动布局可在位 `/libs/fd/af/layouts/mobile/` 置使用。 默认情况下，自适应表单中提供以下移动布局。

![自适应表单中的移动布局列表](assets/mobile-navigation.png)

自适应表单中的移动布局列表

使用移动布局时，可通过点按 ![aem6forms_form_menu图标访问各种表单面板的表单菜单](assets/aem6forms_form_menu.png) 。

### 表单标题中带有面板标题的布局 {#layout-with-panel-titles-in-the-form-header}

该布局按名称显示面板标题以及导航菜单和导航栏。 此布局还提供“下一步”和“上一步”图标进行导航。

![在表单标题中具有面板标题的移动版面](assets/mobile_layout_with.png)

在表单标题中具有面板标题的移动版面

### 表单标题中没有面板标题的布局 {#layout-without-panel-titles-in-the-form-header}

正如名称所暗示的，此布局仅显示没有面板标题的导航菜单和导航栏。 此布局还提供“下一步”和“上一步”图标进行导航。

![在表单标题中无面板标题的移动版面](assets/mobile_layout_without.png)

在表单标题中无面板标题的移动版面

## 工具栏布局 {#toolbar-layouts}

工具栏布局控制您添加到自适应表单的任何操作按钮的定位和显示。 可以在表单级别或面板级别添加布局。

![用于控制按钮布局的自适应表单中的工具栏布局列表](assets/toolbar-layouts.png)

自适应表单中的工具栏布局列表

工具栏布局在位置 `/libs/fd/af/layouts/toolbar` 可用。 自适应表单默认提供以下工具栏布局。

### 工具栏的默认布局 {#default-layout-for-toolbar}

当您在自适应表单中添加任何操作按钮时，此布局将被选为默认布局。 选择此布局后，桌面和移动设备的布局将显示相同的布局。

此外，您还可以添加包含使用此布局配置的操作按钮的多个工具栏。 操作按钮与表单控件相关联。 您可以将工具栏配置为在面板之前或之后。

![工具栏的默认视图](assets/toolbar_layout_default.png)

工具栏的默认视图

### 工具栏的移动固定布局 {#mobile-fixed-layout-for-toolbar}

选择此布局可为桌面和移动设备提供替代布局。

对于桌面布局，您可以使用某些特定标签添加“操作”按钮。 只能使用此布局配置一个工具栏。 如果使用此布局配置了多个工具栏，则移动设备会出现重叠，并且只显示一个工具栏。 例如，您可以在表单的底部或顶部有一个工具栏，或者在表单中的面板之后或之前有一个工具栏。

对于移动布局，您可以使用图标添加操作按钮。

![工具栏的移动固定布局](assets/toolbar_layout_mobile_fixed.png)

工具栏的移动固定布局

