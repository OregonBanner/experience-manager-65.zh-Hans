---
title: 使用布局模式调整组件大小以用于交互式通信
description: '使用布局模式下可用的响应式网格定义组件的位置 '
translation-type: tm+mt
source-git-commit: c62ad355469a95db89db44c34bb6df72d8f4bf77
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# 使用布局模式调整组件{#use-layout-mode-to-resize-components}的大小

交互式通信Web渠道创作界面使您能够使用布局模式调整组件大小。 在列内拖放蓝点，定义开始和终点以放置组件。 点击响应式网格中的组件后，将显示蓝点。 响应式网格由12个相等的列组成。 替代列中的白色和蓝色阴影区分一列与另一列。

您可以使用布局模式调整所有设备类型（如台式机、平板电脑、手机和其他较小设备）的组件大小。 平板电脑自动从桌面版本派生布局配置，而较小的设备从手机派生布局配置。 但是，您可以覆盖自动派生的配置以为每个设备类型定义不同的配置。

>[!NOTE]
>
>如果要使用[打印渠道作为主控](../../forms/using/create-interactive-communication.md)来创建交互通信的Web渠道，则可用于调整大小的组件还包括使用打印渠道在Web渠道中自动生成的子表单和字段。 Web渠道在“布局”模式下保留“打印渠道”元素的布局。

## 访问布局模式{#access-layout-mode}

从显示在交互式通信创作界面顶部的&#x200B;**预览**&#x200B;选项旁边的下拉列表中选择&#x200B;**布局**。 表单将以布局模式显示。

1. 登录到AEM作者实例，然后导航到&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和文档**。
1. 新建或打开现有[交互通信](../../forms/using/create-interactive-communication.md)。
1. 从显示在顶部的&#x200B;**预览**&#x200B;选项旁边的下拉列表中选择&#x200B;**布局**。 表单将以布局模式显示。

   ![交互式通信的布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式下，点按组件以调整大小。 蓝点显示在响应式网格的开始和末尾。
1. 拖放蓝点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated.png)

   点按组件后显示的工具栏包含以下选项：

   * **父项：** 选择组件的父项。
   * **浮动到新行：如** 果同一行中有多个组件，请将组件移到下一行。

   您可以使用&#x200B;**[!UICONTROL 还原断点布局]**（![还原断点](assets/reverttopreviouslypublishedversion.png)）选项撤消所有调整大小的更改，并将默认布局应用于包含已调整大小的组件的面板。 点按已调整大小的组件的父项以视图选项。

   >[!NOTE]
   >
   >不能使用布局模式调整表列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**目标：** 您要插入表组件和图像组件，并在交互通信中将它们平行放置。

1. 在交互通信的Web渠道中，使用编辑模式插入表和图像组件。 图像组件显示在表组件之后。
1. 切换到布局模式并点按表组件。 用于调整组件大小的蓝点显示在第1列和第12列。
1. 将响应式网格的第12列的蓝点拖放到第6列。

   ![定义表的端点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择图像组件，并将响应式网格的第1列的蓝点拖放到第7列。 表和图像组件彼此平行地显示。

   ![在“布局”模式下并行显示表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后点按工具栏中提供的“浮动到新行&#x200B;**”选项，将图像组件移到下一行。**

## 调整面板大小{#resize-panels-layout-mode}

如果要调整整个面板而不是单个组件的大小，请执行以下步骤：

1. 点按面板中要调整大小的任何组件，选择![选择父项](assets/select_parent_icon.svg)，然后在下拉列表中选择第一个选项（如果面板是组件的直接父项）。

   蓝点显示在响应式网格的开始和末尾。

1. 拖放蓝点以定义面板在响应式网格中的位置。
您可以重复第1步和第2步，然后选择![选择父项](assets/float_to_new_line_icon.svg)，将调整大小的面板移到下一行。

## 为面板定义多列布局

执行以下步骤来定义面板的列数：

1. 在&#x200B;**[!UICONTROL 编辑]**&#x200B;模式中，点按面板，选择![配置](assets/configure_icon.png)，然后从&#x200B;**[!UICONTROL 面板布局]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 响应式——页面上的所有内容，而无需导航]**&#x200B;选项。

1. 点按![保存](assets/save_icon.svg)以保存属性。

1. 在&#x200B;**[!UICONTROL 布局]**&#x200B;模式中，点按面板中的任意组件，选择![选择父项](assets/select_parent_icon.svg)，然后选择面板。

1. 点按![多列](assets/multi-column.svg)并从下拉列表中选择列数。 列数范围从1到12。 该面板被分为多列布局。

![布局模式中的多列](assets/multi-column-layout.png)

## 对具有旧响应式布局{#disable-layout-mode-for-forms-with-old-responsive-layout}的表单禁用布局模式

您可以通过编辑表单中使用的模板的属性，为具有响应式布局的旧表单禁用布局模式。

执行以下步骤以禁用布局模式：

1. 选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**，以&#x200B;**[!UICONTROL 编辑]**&#x200B;模式打开表单中使用的模板。
1. 在左窗格中选择文档容器，然后点按&#x200B;**[!UICONTROL 策略。]**

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 点按&#x200B;**[!UICONTROL 布局设置]**&#x200B;选项卡并选择&#x200B;**[!UICONTROL 禁用布局模式]**。
1. 点按![保存更改](assets/save_icon.png)以保存模板属性。

