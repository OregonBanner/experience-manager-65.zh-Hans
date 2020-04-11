---
title: 临时查询在进程报告
seo-title: 临时查询在进程报告
description: 创建自定义查询，以在JEE流程中搜索AEM表单，并在流程报告中搜索任务详细信息
seo-description: 创建自定义查询，以在JEE流程中搜索AEM表单，并在流程报告中搜索任务详细信息
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 临时查询在进程报告{#ad-hoc-queries-in-process-reporting}

## 临时查询在进程报告 {#ad-hoc-queries-in-process-reporting-1}

在流程查询中临时查询允许您创建自定义报告，您可以使用这些自定义搜索在AEM Forms环境中定义的AEM Forms流程实例的流程和任务详细信息。

此外，可以使用进程和任务属性查询来定义临时过滤器。 然后，可保存这些过滤器并用于稍后运行报告。

[**进程搜索&#x200B;**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p):使用基于进程属性的用户定义的搜索筛选器搜索进程实例。

[**流程详细信息&#x200B;**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p):视图进程实例的详细信息，方法是指定进程ID。

**任务搜索**:使用用户定义的基于任务属性的搜索筛选器搜索任务实例。

**任务详细信息**:视图通过指定任务ID来显示任务实例的详细信息。

### 流程和任务 {#processes-and-tasks}

您为流程详细信息创建过滤器和运行查询所执行的步骤与为任务执行的步骤相同。

这意味着“进程搜索”和“任务搜索”的用户界面仅在您可以搜索的字段和搜索结果中返回的字段中有所不同。 这仅仅是因为，虽然许多字段是相同的，但某些字段是特定于进程的，而某些字段是特定于任务的。

本文详细介绍了“流程/任务搜索”和“流程/任务详细信息”部分的说明。 在适当的位置，将特别调出任何特定差异。

## 进程/任务搜索 {#process-task-search}

您可以使用进程/任务搜索定义用于查询进程/任务实例的过滤器。

### 创建进程/任务搜索查询 {#to-create-a-process-task-search-query}

1. 要视图保存的进程/任务搜索查询或创建查询，请单击 **临时查询** ，然后单击 **进程/任务搜索**。

   ![search_nodes](assets/search_nodes.png)

   “ **我的过滤器** ”面板显示在树视图的右侧。

   在“我 **的过滤器** ”面板中，您可以创建新的临时查询并单击以执行以前保存的查询。

   ![my_过滤器_panel](assets/my_filters_panel.png)

1. 要执行现有查询，只需单击“我的过滤器”面板中 **的查询** 。
1. 要创建查询，请单 **击添加** (+)。

   此时将 **显示“创建过滤** 器”面板。

   ![create_filter_panel](assets/create_filter_panel.png)

   查询由一个或多个查询过滤器组成。 要创建过滤器，请向查询添加过滤器行。 默认情况下，将向查询添加一个过滤器行。

   **定义过滤器**

   1. 选择字段。

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >字段列表包含特定于AEM Forms进程/任务的字段。

   1. 选择条件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的条件取决于选择用于筛选的属性。

   1. 输入一个值。

      ![filter_value](assets/filter_value.png)

   1. 要向查询添加其他过滤器，请 **单击过滤器行右侧的添加** (+)。

      要从查询中删除过滤器，请单 **击过滤器行右侧的删除** (-)。

      ![filter_add_del](assets/filter_add_del.png)

创建查询后，使用“创建过滤器”面板右上角的 **选项** ，可以：

* **取消**:取消更改并返回“我的 **过滤器** ”面板。
* **运行**:执行当前查询以查看和／或验证结果。 在这种情况下，您无需在执行查询之前保存查询。 您可以验证结果，根据需要进行更改，然后在对输出满意时保存查询。
* **保存**:保存过滤器。 然后，可以从“我的过滤器”面板查看和 **执行该过滤器** 。

### “我的过滤器”面板中的选项 {#options-in-my-filters-panel}

使用“我的过滤器 **”面板中的选项** Add **pr_** add_pr_add_ ![lc_](assets/lc_pr_add_filter.png)editpr_pr, **Lc滤镜删除AddAddAddAdd_pr_add_pr_pr，或删除DeleteLicAdEdit_pr_**![](assets/lc_pr_delete_filter.png)****![](assets/lc_pr_edit_filter.png)Filteran-hoc查询中的AdAdAdAdEdit。

![my_过滤器_options](assets/my_filters_options.png)

### 执行搜索查询 {#to-execute-a-search-query}

1. 要执行查询，请单击“我的过滤器 **”面板中的过滤器，或单击“** Run **** ”按钮（如果要创建或编辑过滤器）。
1. 查询的结果显示在“进程 **报告** ”窗口的“ **报告”面板中** 。

   ![process_search_result](assets/process_search_result.png)

   您可以借助报表底部显示的分页面板对搜索结果分页。

   ![process_result_pgn](assets/process_result_pgn.png)

   在“显 **示** ”下拉列表中，选择每页要显示的结果数。

   在“页 **面** ”文本框中，输入要直接转到该页面的页码。

1. 流程搜索结果中显示以下字段：

   * **进程ID**:进程的ID。 该字段为超链接。 如果单击此字段中的进程ID，则会将您重定向到该进 **[!UICONTROL 程的“进程详细信息]** ”面板。
   * **启动器**:启动进程实例的AEM Forms用户
   * **创建时间**:进程实例开始的日期和时间
   * **完成时间**:进程实例完成的日期和时间
   * **持续时间**:从开始到完成进程实例的持续时间
   * **状态**:进程实例的当前状态。
   默认情况下，结果按进程ID排序。 但是，要按任何字段对结果进行排序，请单击字段标题。

   由于排序是切换操作，因此单击列标题可对结果进行升序排序，再次单击它可按降序排序。

   同样，以下字段显示在任务搜索结果中：

   * **任务ID**:任务的ID。 该字段为超链接。 如果单击此字段中的任务ID，您将被重定向到该任务的“ **[!UICONTROL 任务详细信息]** ”面板。
   * **启动器**:启动进程实例的AEM Forms用户
   * **创建时间**:进程实例开始的日期和时间
   * **完成时间**:进程实例完成的日期和时间
   * **持续时间**:从开始到完成进程实例的持续时间
   * **状态**:进程实例的当前状态。
   默认情况下，结果按任务ID排序。 但是，要按任何字段对结果进行排序，请单击字段标题。 结果按列排序，该列由列标题旁的暗箭头指示。

   由于排序是切换操作，因此单击字段标题可对结果进行升序排序，再次单击它可按降序排序。 当前排序顺序（升序／降序）由列标题旁边的向下箭头方向指示。

   ![任务_search_result](assets/task_search_result.png)

1. 单击左上角 ![的边栏按钮](assets/lc_pr_rail_button.png) lc_pr_rail_button可折叠“我的过滤器”窗格并展开“报告”面板的可用 **空间****** 。
1. 使用**报告**面板右上角的选项对查询结果执行操作。

   * **刷新**:刷新报表时，存储中会显示最新数据

   * **导出到CSV**:将报告数据导出到以逗号分隔的文件。
   >[!NOTE]
   >
   >导出报告时，搜索的整个结果将导出为CSV文件，而不仅仅是当前页面

## 流程/任务详细信息 {#process-task-details}

您可以使用“ **进程详细信息** ”面板来视图特定进程的详细信息。

同样，您也可以使用 **任务详细信息** 面板视图特定任务的详细信息。

### 视图流程/任务详细信息 {#to-view-process-task-details}

您可以视图特定AEM Forms流程/任务的详细信息：

* **从流程/任务搜索结果**
* **通过在“流程/任务详细信息”面板中输入流程/任务ID**

#### 从流程/任务搜索结果 {#from-a-process-task-search-result}

1. 执行进程/任务搜索。 有关详细信息，请 [参阅执行进程搜索查询](#to-execute-a-search-query)。

   请注意，结果中返回的进程ID是超链接的。

   ![process_id_列表](assets/process_id_list.png)

1. 单击列表中的进程ID，在“进程详细信息”面板中视图此进 **程的详细信息** 。

   “流 **程/任务详细信息** ”查询结果显示流程/任务中包含的任务/表单的详细信息。

   默认情况下，结果按任务/表单ID排序。 但是，要按任何字段对结果进行排序，请单击字段标题。 对结果进行排序时所依据的列由列标题旁边的一个暗箭头指示。

   由于排序是切换操作，因此单击字段标题可对结果进行升序排序，再次单击它可按降序排序。 当前排序顺序（升序／降序）由列标题旁边的向下箭头方向指示。

   **流程详细信息结果**

   ![process_details](assets/process_details.png)

   **左面板：** 显示选定流程的以下详细信息：

   * 进程名称
   * 流程创建日期时间
   * 流程完成日期时间
   * 进程持续时间
   * 进程状态
   * 进程启动器
   **右上面板：** 显示组成所选流程的任务的以下详细信息：

   * 任务ID
   * 任务名称
   * 任务所有者
   * 任务创建日期时间
   * 任务更新日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态
   **右下面板：** 显示选定进程的进程历史记录的以下详细信息：

   * 进程名称
   * 进程启动器
   * 流程更新日期时间
   * 流程完成日期时间
   * 进程状态
   **任务详细信息结果**

   ![任务_详细信息](assets/task_details.png)

   **左面板：** 显示选定任务的以下详细信息：

   * 任务名称
   * 此任务所属的进程ID
   * 任务说明
   * 任务创建日期时间
   * 任务完成日期时间
   * 任务持续时间
   * 任务状态
   * 选定的任务路线
   **右上面板：** 显示组成所选任务的表单的以下详细信息：

   * Foprm ID
   * 表单创建日期时间
   * 表单更新日期时间
   * 表单模板Url
   **右下面板：** 显示选定任务的进程历史记录的以下详细信息：

   * 任务分配类型
   * 任务所有者
   * 任务分配创建日期时间
   * 任务更新日期时间






1. 单 **击返回至进程/任务搜索** ，返回至从中向下钻取进程/任务详细信息的搜索结果。

   ![back_to_search](assets/back_to_search.png)

   但是，如果通过输入特定的进程/任务ID找到进程/任务详细信息，则单击返回进程/任务搜索将返回至进程/任务搜索 ****，而不显示任何搜索结果。

#### 通过在“流程/任务详细信息”面板中输入流程/任务ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 转到“进程/ **任务详细信息** ”面板。

   ![details_nodes](assets/details_nodes.png)

1. 在“进程/任务ID”文本框中，输入进程/任务ID。

   ![process_details-1](assets/process_details-1.png)

   流程/任务详细 **信息查询结果中的字段** ，是特定于AEM Forms流程/任务的字段。

   对于进程，查询结果显示进程中包含的任务的详细信息。

   对于任务,查询结果显示任务中包含的表单的详细信息。
