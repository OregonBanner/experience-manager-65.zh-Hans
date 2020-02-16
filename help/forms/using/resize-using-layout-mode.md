---
title: 使用布局模式调整组件大小
seo-title: 使用布局模式调整组件大小
description: '使用布局模式中可用的响应式网格定义组件的位置 '
seo-description: '使用布局模式中可用的响应式网格定义组件的位置 '
uuid: 6b077ebe-caea-4ae3-b17a-be2dca94eeb3
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9e9aaf36-bb86-4954-83cc-fa6b3e80ae4b
docset: aem65
translation-type: tm+mt
source-git-commit: cc4b667bb20622949c71eee64b07d679109482c1

---


# 使用布局模式调整组件大小{#use-layout-mode-to-resize-components}

自适应表单和交互式通信Web渠道创作界面使您能够使用布局模式调整组件大小。 在列中拖放蓝点，以定义开始点和结束点以放置组件。 点击响应式网格中的组件后，将显示蓝点。 响应式网格由12个相等的列组成。 替代列中的白色和蓝色底纹使一列与另一列区分开。

您可以使用布局模式调整所有设备类型（如桌面、平板电脑、手机和其他较小设备）的组件大小。 平板电脑自动从桌面版本派生布局配置，而较小的设备从手机派生布局配置。 但是，您可以覆盖自动派生的配置以为每个设备类型定义不同的配置。

如果您使用打印渠道作为交互式通信的主渠道 [](../../forms/using/create-interactive-communication.md) ，则可用于调整大小的组件还包括使用打印渠道在Web渠道中自动生成的子表单和字段。 Web渠道在“布局”模式下保留打印渠道元素的布局。

## 访问布局模式 {#access-layout-mode}

从自 **适应表单顶部显示的下拉列表中选择布局** ，并从“预览”选项旁边的“交互通信”创作界面顶部 **选择** 。 表单将以布局模式显示。

1. 登录到AEM作者实例，然后导航到 **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**。
1. [创建新表单](../../forms/using/create-interactive-communication.md) ，或打开现有的自适应表单或交互式通信。
1. 从“ **预览** ”选项旁边顶部显示的下拉列表中选择“布 **局** ”。 表单将以布局模式显示。

   ![交互式通信的布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式中，点按组件以调整大小。 蓝点显示在响应式网格的开始和结束处。
1. 拖放蓝点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated.png)

   点击组件后显示的工具栏包含以下选项：

   * **** 父项：选择组件的父项。
   * **** 浮动到新行：如果同一行中有多个组件，请将组件移到下一行。
   您可以撤消所有调整大小的更改，并使用“还原断点”布局 **[!UICONTROL (“还原断点”]**![](assets/reverttopreviouslypublishedversion.png))选项将默认布局应用到包含已调整大小的组件的面板。 点按已调整大小的组件的父项以查看选项。

   >[!NOTE]
   >
   >不能使用布局模式调整表列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**** 目标：您希望插入表组件和图像组件，并在交互通信中将它们彼此平行放置。

1. 在Web渠道中使用编辑模式插入表和图像组件。 图像组件显示在表组件之后。
1. 切换到布局模式并点按表组件。 用于调整组件大小的蓝点显示在第1列和第12列。
1. 将响应式网格的第12列的蓝点拖放到第6列。

   ![定义表的端点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择图像组件，并将响应式网格的第1列的蓝点拖放到第7列。 表和图像组件彼此平行地显示。

   ![在“布局”模式下并行显示表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后点按工具栏中 **提供的浮动到新行** ，以将图像组件移到下一行。

## 调整面板大小 {#resize-panels-layout-mode}

如果要调整整个面板而不是单个组件的大小，请执行以下步骤：

1. 点按面板中要调整大小的任何组件，选择 ![Select Parent](assets/select_parent_icon.svg)，然后在下拉列表中选择第一个选项（如果面板是组件的直接父项）。

   蓝点显示在响应式网格的开始和结束处。

1. 拖放蓝点以定义面板在响应式网格中的位置。
您可以重复第1步和第2步，然后选择“ ![选择父项](assets/float_to_new_line_icon.svg) ”，将调整大小的面板移到下一行。

## 为旧的响应式布局启用新的响应式网格 {#enableresponsivegrid}

为使用AEM Forms 6.4或更低版本创建的表单启用新的响应式网格，以调整组件大小。

>[!NOTE]
>
>切换到新的响应式网格将放弃已为表单中使用的组件定义的布局属性。

请执行以下步骤以启用新的响应式网格：

1. 从“ **预览** ”选项旁边顶部显示的下拉列表中选择“布 **局** ”。 此时会显示启用布局模式的确认信息。
1. 点 **按是** ，为表单启 **用布局模式** 。

### 使用新的响应式布局将旧片段嵌入自适应表单 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

自适应表单的全新响应式布局允许您向表单添加具有旧的响应式布局的自适应表单片段。 但是，新布局会放弃为片段中使用的组件定义的布局属性。 可切换到布局模式以定义片段中使用的组件的布局属性。

### 在旧的自适应表单中嵌入具有新响应式布局的片段 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

如果您在具有旧响应式布局的自适应表单中嵌入了具有新响应式布局的片段，系统会提示您为该表单启用布局模式并重新嵌入该片段。

要启用布局模式，请从“预 **览** ”选项旁边顶部显示的下拉列表中选择“布局”，然后点按“是 **”****** 进行确认。 选择 **编辑模式** ，以重新嵌入片段。

## 使用旧的响应式布局禁用表单的布局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以通过编辑表单中使用的模板的属性，为具有响应式布局的旧表单禁用布局模式。

执行以下步骤以禁用布局模式：

1. 选择 **[!UICONTROL “]** >常规 **[!UICONTROL ” > “模]** 板” **[!UICONTROL ，然后在“编辑工具”模式中打开在表单]****** 中使用的模板。
1. 在左侧窗格中选择文档容器，然后点按 **[!UICONTROL 策略。]**

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 点按布局 **[!UICONTROL 设置选项卡]** ，然后选择 **[!UICONTROL 禁用布局模式]**。
1. 点按 ![保存更改](assets/save_icon.png) ，以保存模板属性。

