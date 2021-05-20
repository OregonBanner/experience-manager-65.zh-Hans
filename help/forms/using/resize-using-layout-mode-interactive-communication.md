---
title: 使用布局模式调整组件大小以用于交互式通信
description: '使用布局模式中可用的响应式网格定义组件的位置 '
feature: 交互式通信
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 使用布局模式调整组件{#use-layout-mode-to-resize-components}的大小

交互式通信Web渠道创作界面允许您使用布局模式调整组件大小。 在列中拖放蓝色圆点以定义要放置组件的起始点和终点。 点按响应式网格中的组件后，将显示蓝色圆点。 响应式网格由12个相等的列组成。 替代列中的白色和蓝色底纹将一列与另一列区分开。

您可以使用布局模式调整所有设备类型（如台式机、平板电脑、手机和其他较小设备）的组件大小。 平板电脑自动从桌面版本导出布局配置，而较小的设备从手机导出布局配置。 但是，您可以覆盖自动派生的配置，以便为每种设备类型定义不同的配置。

>[!NOTE]
>
>如果您使用[将打印渠道作为交互式通信的主控](../../forms/using/create-interactive-communication.md)来创建Web渠道，则可用于调整大小的组件还包括使用打印渠道在Web渠道中自动生成的子表单和字段。 Web渠道在“布局”模式下保留“打印”渠道元素的布局。

## 访问布局模式{#access-layout-mode}

从下拉列表中选择&#x200B;**布局** ，该下拉列表显示在&#x200B;**预览**&#x200B;选项旁边的交互式通信创作界面顶部。 表单将在布局模式下显示。

1. 登录到AEM创作实例，然后导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
1. 创建新的或打开现有的[交互式通信](../../forms/using/create-interactive-communication.md)。
1. 从显示在&#x200B;**预览**&#x200B;选项旁边顶部的下拉列表中选择&#x200B;**布局**。 表单将在布局模式下显示。

   ![交互式通信的布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式下，点按组件以调整大小。 蓝色圆点显示在响应式网格的开始和结束处。
1. 拖放蓝色圆点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated.png)

   点按组件后显示的工具栏包含以下选项：

   * **父项：** 选择组件的父项。
   * **浮动到新行：** 如果同一行中存在多个组件，请将组件移到下一行。

   您可以撤消所有调整大小的更改，并使用&#x200B;**[!UICONTROL 还原断点布局]**（![还原断点](assets/reverttopreviouslypublishedversion.png)）选项将默认布局应用于包含已调整大小的组件的面板。 点按已调整大小的组件的父组件以查看选项。

   >[!NOTE]
   >
   >无法使用布局模式调整表列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**目标：** 要插入表组件和图像组件，并在交互式通信中将它们平行放置。

1. 在交互式通信的Web渠道中使用编辑模式插入表和图像组件。 图像组件在表组件之后显示。
1. 切换到布局模式，然后点按表组件。 用于调整组件大小的蓝色圆点显示在第1列和第12列。
1. 将响应式网格的第12列蓝色圆点拖放到第6列。

   ![定义表的端点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择图像组件，并将响应式网格的第1列和第7列的蓝色圆点拖放到该位置。 表和图像组件彼此平行显示。

   ![在“布局”模式下并行的表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后点按工具栏中提供的&#x200B;**浮动到新行**&#x200B;选项，以将图像组件移到下一行。

## 调整面板大小{#resize-panels-layout-mode}

如果要调整整个面板的大小而不是单个组件的大小，请执行以下步骤：

1. 点按面板中要调整大小的任何组件，选择![选择父项](assets/select_parent_icon.svg)，然后在下拉列表中选择第一个选项（如果该面板是组件的直接父项）。

   蓝色圆点显示在响应式网格的开始和结束处。

1. 拖放蓝色圆点以定义面板在响应式网格中的位置。
您可以重复步骤1和2，然后选择![选择父项](assets/float_to_new_line_icon.svg)以将调整大小的面板移到下一行。

## 为面板定义多列布局

执行以下步骤以定义面板的列数：

1. 在&#x200B;**[!UICONTROL 编辑]**&#x200B;模式中，点按面板，选择![配置](assets/configure_icon.png)，然后从&#x200B;**[!UICONTROL 面板布局]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 响应 — 页面上所有没有导航的内容]**&#x200B;选项。

1. 点按![Save](assets/save_icon.svg)以保存属性。

1. 在&#x200B;**[!UICONTROL 布局]**&#x200B;模式中，点按面板中的任意组件，选择![选择父项](assets/select_parent_icon.svg)，然后选择面板。

1. 点按![多列](assets/multi-column.svg)，然后从下拉列表中选择列数。 列数可以介于1到12之间。 该面板将分为多列布局。

![布局模式中的多列](assets/multi-column-layout.png)

## 对于具有旧响应式布局的表单，禁用布局模式{#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以通过编辑表单中所用模板的属性，来禁用具有旧响应式布局的表单的布局模式。

执行以下步骤以禁用布局模式：

1. 选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**&#x200B;并在&#x200B;**[!UICONTROL 编辑]**&#x200B;模式下打开表单中使用的模板。
1. 选择左窗格中的文档容器，然后点按&#x200B;**[!UICONTROL 策略。]**

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 点按&#x200B;**[!UICONTROL 布局设置]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 禁用布局模式]**。
1. 点按![保存更改](assets/save_icon.png)以保存模板属性。
