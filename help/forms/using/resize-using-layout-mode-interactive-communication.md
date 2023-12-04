---
title: 使用布局模式调整交互式通信组件的大小
description: 使用在布局模式下可用的响应式网格定义组件的位置
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# 使用版面模式调整组件大小 {#use-layout-mode-to-resize-components}

交互式通信Web渠道创作界面允许您使用“布局”模式调整组件大小。 在列中拖放蓝色圆点，以定义起点和终点来定位组件。 点按响应式网格中的组件后，会显示蓝点。 响应式网格由12个相等的列组成。 备用列中的白色和蓝色阴影将一列与另一列区分开来。

您可以使用布局模式为所有设备类型（如台式机、平板电脑、手机和其他小型设备）调整组件大小。 平板电脑会自动从台式机版本获取布局配置，较小的设备则从手机获取布局配置。 但是，您可以覆盖自动派生的配置以针对每种设备类型定义不同的配置。

>[!NOTE]
>
>如果您使用创建Web渠道 [将渠道打印为主渠道](../../forms/using/create-interactive-communication.md) 对于交互式通信，可用于调整大小的组件还包括使用打印渠道在Web渠道中自动生成的子表单和字段。 Web渠道在布局模式下保留打印渠道元素的布局。

## 访问布局模式 {#access-layout-mode}

选择 **布局** 在交互式通信创作界面顶部显示的下拉列表中，找到要编辑的 **预览** 选项。 该表单将以布局模式显示。

1. 登录到AEM创作实例并导航到 **Adobe Experience Manager** > **Forms** > **Forms和文档**.
1. 创建 [交互式通信](../../forms/using/create-interactive-communication.md) 或者打开一个现有的存储库。
1. 选择 **布局** 从顶部显示的下拉列表中，选择 **预览** 选项。 该表单将以布局模式显示。

   ![交互式通信的布局模式](assets/layout_mode_ic_new.png)

## 调整组件大小 {#resize-components}

1. 在布局模式下，选择要调整大小的组件。 蓝点显示在响应式网格的开头和结尾。
1. 拖放蓝点以定义组件在响应式网格中的位置。

   ![使用布局模式调整大小](assets/layout_mode_resize_new_updated.png)

   点按组件后显示的工具栏包含以下选项：

   * **父项：** 选择组件的父组件。
   * **浮动到新行：** 如果同一行中有多个组件，则将组件移至下一行。

   您可以撤消所有调整大小的更改，并使用将默认布局应用到包含已调整大小的组件的面板 **[!UICONTROL 还原断点布局]** ( ![还原断点](assets/reverttopreviouslypublishedversion.png))选项。 选择已调整大小的组件的父组件以查看选项。

   >[!NOTE]
   >
   >无法使用布局模式调整表格列、工具栏、工具栏按钮和目标区域组件的大小。 使用样式模式调整这些组件的大小。

### 示例 {#example}

**目标：** 要插入表组件和图像组件，并在交互式通信中将其彼此平行放置。

1. 在交互式通信的Web渠道中，使用编辑模式插入表和图像组件。 图像组件显示在表组件之后。
1. 切换到布局模式并选择表组件。 用于调整组件大小的蓝点显示在列1和12。
1. 将第12列中的蓝色圆点拖放到响应式网格的第6列。

   ![定义表的端点](assets/layout_mode_end_point_table_new.png)

1. 同样，选择图像组件并将响应式网格的第1列中的蓝色圆点拖放到第7列。 表格和图像组件彼此平行显示。

   ![在布局模式下并行显示表和图像](assets/table_image_parallel_new.png)

   您可以选择图像组件，然后选择 **浮动到新行** 工具栏中可用的选项以将图像组件移动到下一行。

## 调整面板大小 {#resize-panels-layout-mode}

如果要调整整个面板而非单个组件的大小，请执行以下步骤：

1. 在面板中选择要调整大小的任何组件，然后选择 ![选择父级](assets/select_parent_icon.svg)，并在下拉列表中选择第一个选项（如果面板是组件的直接父面板）。

   蓝点显示在响应式网格的开头和结尾。

1. 拖放蓝点以定义面板在响应式网格中的位置。
您可以重复步骤1和2，然后选择 ![选择父级](assets/float_to_new_line_icon.svg) 将调整大小的面板移到下一行。

## 定义面板的多列布局

执行以下步骤可定义面板的列数：

1. 在 **[!UICONTROL 编辑]** 模式，选择面板，选择 ![配置](assets/configure_icon.png)，并选择 **[!UICONTROL 响应 — 页面上的所有内容，无需导航]** 选项来自 **[!UICONTROL 面板布局]** 下拉列表。

1. 选择 ![保存](assets/save_icon.svg) 以保存属性。

1. 在 **[!UICONTROL 布局]** 模式，在面板中选择任意组件，然后选择 ![选择父级](assets/select_parent_icon.svg)，然后选择面板。

1. 选择 ![多列](assets/multi-column.svg) 并从下拉列表中选择列数。 列数可在1到12之间。 面板被分为多列布局。

![布局模式下的多列](assets/multi-column-layout.png)

## 对具有旧响应布局的表单禁用布局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以通过编辑表单中使用的模板的属性来禁用具有旧响应布局的表单的布局模式。

执行以下步骤可禁用布局模式：

1. 选择 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]** 然后打开表单中使用的模板，位置如下： **[!UICONTROL 编辑]** 模式。
1. 在左窗格中选择文档容器，然后选择 **[!UICONTROL 策略。]**

   ![禁用布局模式](assets/policy_disable_layout_mode.png)

1. 选择 **[!UICONTROL 布局设置]** 选项卡并选择 **[!UICONTROL 禁用布局模式]**.
1. 选择 ![保存更改](assets/save_icon.png) 以保存模板属性。
