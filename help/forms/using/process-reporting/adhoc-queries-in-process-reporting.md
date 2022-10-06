---
title: 进程报表中的临时查询
seo-title: Ad-hoc Queries in Process Reporting
description: 创建自定义查询，以在流程报表中搜索JEE上的AEM Forms流程和任务详细信息
seo-description: Create custom queries to search for AEM Forms on JEE  process and task details in Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# 进程报表中的临时查询{#ad-hoc-queries-in-process-reporting}

## 进程报表中的临时查询 {#ad-hoc-queries-in-process-reporting-1}

流程报表中的临时查询允许您创建自定义查询，以用于搜索在AEM Forms环境中定义的AEM Forms流程实例的流程和任务详细信息。

此外，可以使用进程和任务属性筛选器来定义临时查询。 然后，可以保存这些过滤器，并用于稍后运行报表。

[**流程搜索**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p):使用基于流程属性的用户定义的搜索过滤器搜索流程实例。

[**流程详细信息**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p):通过指定进程ID查看进程实例的详细信息。

**任务搜索**:使用基于任务属性的用户定义的搜索过滤器搜索任务实例。

**任务详细信息**:通过指定任务ID查看任务实例的详细信息。

### 流程和任务 {#processes-and-tasks}

创建过滤器和运行流程详细信息查询所遵循的步骤与任务的步骤相同。

这意味着“流程搜索”和“任务搜索”的用户界面仅在可搜索的字段和搜索结果中返回的字段中不同。 这仅仅是因为，尽管许多字段是相同的，但某些字段是特定于进程的，某些字段是特定于任务的。

本文详细介绍了“流程/任务搜索”和“流程/任务详细信息”部分的说明。 在适当的位置，将专门标注任何具体差异。

## 进程/任务搜索 {#process-task-search}

您可以使用“流程/任务搜索”定义用于查询流程/任务实例的过滤器。

### 创建流程/任务搜索查询 {#to-create-a-process-task-search-query}

1. 要查看保存的“流程/任务搜索”查询或创建查询，请单击 **临时查询** 然后单击 **进程/任务搜索**.

   ![search_nodes](assets/search_nodes.png)

   的 **我的过滤器** 面板。

   在 **我的过滤器** 面板中，您可以创建新的临时查询并单击，以执行之前保存的查询。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 要执行现有查询，只需在 **我的过滤器** 的上界。
1. 要创建查询，请单击 **添加** (+)。

   的 **创建过滤器** 面板。

   ![create_filter_panel](assets/create_filter_panel.png)

   查询由一个或多个查询过滤器组成。 要创建过滤器，请向查询中添加过滤器行。 默认情况下，查询中会添加一个过滤器行。

   **定义过滤器**

   1. 选择字段。

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >字段列表包含特定于AEM Forms进程/任务的字段。

   1. 选择一个条件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的条件取决于选择进行筛选的属性。

   1. 输入一个值。

      ![filter_value](assets/filter_value.png)

   1. 要向查询添加其他过滤器，请单击 **添加(+)** 的双曲余切值。

      要从查询中删除过滤器，请单击 **删除(-)** 的双曲余切值。

      ![filter_add_del](assets/filter_add_del.png)

创建查询后，请使用 **创建过滤器** 面板：

* **取消**:取消更改并返回到 **我的过滤器** 的上界。
* **运行**:执行当前查询以查看和/或验证结果。 在这种情况下，您无需在执行查询之前保存查询。 您可以验证结果，根据需要进行更改，然后在对输出满意时保存查询。
* **保存**:保存过滤器。 然后，可以从 **我的过滤器** 的上界。

### “我的过滤器”面板中的选项 {#options-in-my-filters-panel}

使用 **我的过滤器** 面板至 **添加** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **编辑** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)或 **删除** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)临时查询。

![my_filters_options](assets/my_filters_options.png)

### 执行搜索查询 {#to-execute-a-search-query}

1. 要执行查询，请在 **我的过滤器** 面板，或单击 **运行** 按钮。
1. 查询的结果显示在 **报表** 面板 **流程报告** 窗口。

   ![process_search_result](assets/process_search_result.png)

   您可以借助报表底部显示的分页面板，对搜索结果进行分页。

   ![process_result_pgn](assets/process_result_pgn.png)

   在 **显示** 下拉列表中，选择每页显示的结果数。

   在 **页面** ，请输入要直接转到该页面的页码。

1. 流程搜索结果中显示以下字段：

   * **进程ID**:进程的ID。 该字段具有超链接。 如果您单击此字段中的进程ID，则会被重定向到 **[!UICONTROL 流程详细信息]** 面板。
   * **发起者**:启动进程实例的AEM Forms用户
   * **创建时间**:流程实例开始的日期和时间
   * **完成时间**:流程实例完成的日期和时间
   * **持续时间**:进程实例从开始到完成的持续时间
   * **状态**:进程实例的当前状态。

   默认情况下，结果按流程ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。

   由于排序是切换操作，因此单击列标题可对结果进行升序排序，然后再次单击该列标题可对结果进行降序排序。

   同样，任务搜索结果中也显示以下字段：

   * **任务ID**:任务的ID。 该字段具有超链接。 如果单击此字段中的任务ID，则会被重定向到 **[!UICONTROL 任务详细信息]** 面板。
   * **发起者**:启动进程实例的AEM Forms用户
   * **创建时间**:流程实例开始的日期和时间
   * **完成时间**:流程实例完成的日期和时间
   * **持续时间**:进程实例从开始到完成的持续时间
   * **状态**:进程实例的当前状态。

   默认情况下，结果按任务ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。 结果按列排序，列标题旁边的向下箭头表示。

   由于排序是切换操作，因此单击字段标题可对结果进行升序排序，然后再次单击该字段标题可对结果进行降序排序。 当前排序顺序（升序/降序）由列标题旁边的下箭头方向指示。

   ![task_search_result](assets/task_search_result.png)

1. 单击边栏按钮 ![lc_pr_rail_button](assets/lc_pr_rail_button.png) 在左上角折叠 **我的过滤器** 窗格，并展开 **报表** 的上界。
1. 使用**报表**面板右上角的选项对查询结果执行操作。

   * **刷新**:使用存储中的最新数据刷新报表

   * **导出到CSV**:将报表数据导出到以逗号分隔的文件。
   >[!NOTE]
   >
   >导出报表时，搜索的整个结果都会导出为CSV文件，而不仅仅是当前页面

## 进程/任务详细信息 {#process-task-details}

您使用 **流程详细信息** 面板，以查看特定流程的详细信息。

同样，您也使用 **任务详细信息** 面板，以查看特定任务的详细信息。

### 查看流程/任务详细信息 {#to-view-process-task-details}

您可以查看特定AEM Forms进程/任务的详细信息：

* **从进程/任务搜索结果**
* **通过在“流程/任务详细信息”面板中输入流程/任务ID**

#### 从进程/任务搜索结果 {#from-a-process-task-search-result}

1. 执行进程/任务搜索。 有关详细信息，请参阅 [执行进程搜索查询](#to-execute-a-search-query).

   请注意，结果中返回的进程ID是超链接的。

   ![process_id_list](assets/process_id_list.png)

1. 单击列表中的进程ID，以在 **流程详细信息** 的上界。

   的 **进程/任务详细信息** 查询结果显示流程/任务中包含的任务/表单的详细信息。

   默认情况下，结果按任务/表单ID排序。 但是，要按任意字段对结果进行排序，请单击字段标题。 对结果排序所依据的列由列标题旁边的一个暗箭头指示。

   由于排序是切换操作，因此单击字段标题可对结果进行升序排序，然后再次单击该字段标题可对结果进行降序排序。 当前排序顺序（升序/降序）由列标题旁边的下箭头方向指示。

   **流程详细信息结果**

   ![process_details](assets/process_details.png)

   **左面板：** 显示选定流程的以下详细信息：

   * 进程名称
   * 流程创建日期时间
   * 流程完成日期时间
   * 进程持续时间
   * 进程状态
   * 进程启动器

   **右上面板：** 显示构成选定流程的任务的以下详细信息：

   * 任务ID
   * 任务名称
   * 任务所有者
   * 任务创建日期时间
   * 任务更新日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态

   **右下面板：** 显示选定流程的流程历史记录的以下详细信息：

   * 进程名称
   * 进程启动器
   * 流程更新日期时间
   * 流程完成日期时间
   * 进程状态

   **任务详细信息结果**

   ![task_details](assets/task_details.png)

   **左面板：** 显示选定任务的以下详细信息：

   * 任务名称
   * 此任务所属的进程ID
   * 任务描述
   * 任务创建日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态
   * 选定的任务路线

   **右上面板：** 显示构成选定任务的表单的以下详细信息：

   * Foprm ID
   * 表单创建日期时间
   * 表单更新日期时间
   * 表单模板Url

   **右下面板：** 显示选定任务的流程历史记录的以下详细信息：

   * 任务分配类型
   * 任务所有者
   * 任务分配创建日期时间
   * 任务更新日期时间






1. 单击 **返回进程/任务搜索** 返回到从中向下钻取流程/任务详细信息的搜索结果。

   ![back_to_search](assets/back_to_search.png)

   但是，如果通过输入特定流程/任务ID找到流程/任务详细信息，则单击返回至流程/任务搜索会返回至 **进程/任务搜索**，而不显示任何搜索结果。

#### 通过在“流程/任务详细信息”面板中输入流程/任务ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 转到 **进程/任务详细信息** 的上界。

   ![details_nodes](assets/details_nodes.png)

1. 在“流程/任务ID”文本框中，输入流程/任务ID。

   ![process_details-1](assets/process_details-1.png)

   中的字段 **进程/任务详细信息** 查询结果是特定于AEM Forms进程/任务的字段。

   对于某个流程，查询结果会显示该流程中包含的任务的详细信息。

   对于任务，查询结果会显示任务中包含的表单的详细信息。
