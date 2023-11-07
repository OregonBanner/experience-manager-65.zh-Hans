---
title: 搜索进程实例
seo-title: Searching for process instances
description: 使用“进程搜索”页可以输入用于查找进程实例的搜索标准。
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 搜索进程实例{#searching-for-process-instances}

使用“进程搜索”页可以输入用于查找进程实例的搜索标准。 您可以从表单工作流页面访问“流程搜索”页面，也可以通过单击“流程实例”页面上的“搜索”来访问“流程搜索”页面。

您可以输入执行常规搜索的基本标准、执行详细搜索的特定属性或执行组合搜索的基本标准和特定属性的组合。

## 执行常规搜索 {#perform-a-general-search}

如果您知道进程实例的进程ID，或者您要查找一组相关的进程实例，或者只运行少数几个进程实例，则对进程进行常规搜索是最合适的。

输入执行常规搜索的基本条件。 如果输入多个条件，则使用隐含的AND条件执行搜索。

1. 在管理控制台中，单击服务> Forms工作流>进程搜索。
1. 在“进程搜索”页的“常规搜索”下，提供以下条件：

   * **进程ID：** 正整数，用于标识每个唯一的进程实例。
   * **进程状态：** 从列表中选择状态。
   * **应用程序：** 从列表中选择应用程序。 仅显示已部署的应用程序。
   * **进程名称 — 版本：** 从菜单中选择进程名称。 只显示已部署的进程。

1. 单击“搜索”。 此时将显示“流程实例”页，其中列出了找到的实例。

## 对进程执行详细搜索 {#perform-a-detailed-search-for-a-process}

您可以输入特定属性以执行详细搜索。 如果您有许多进程实例在运行，并且需要按特定条件缩小可能的查找范围，则详细搜索是最合适的。

1. 在管理控制台中，单击服务> Forms工作流>进程搜索。
1. 在“进程搜索”页的“详细搜索”下，指定您的第一个标准集：

   * 在“属性”列表中，选择一个属性。
   * 在“筛选器”列表中，选择一个运算符。
   * 在“值”框中，键入适合所选属性的值。

1. 要添加另一行，请选择“更多筛选器”。 将显示另一组“属性”、“筛选器”和“值”列表，以及“条件”列表。
1. 在条件下，选择AND或OR。 根据需要重复步骤1 - 3，以进一步缩小搜索范围。
1. 要添加或删除行，请单击“更多筛选器”或“更少筛选器”。 一到四行即可。
1. 单击“搜索”。 此时将显示“流程实例”页，其中列出了找到的实例。

[关于流程实例状态](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 对进程执行组合搜索 {#perform-a-combined-search-for-a-process}

要基于常规搜索和详细搜索创建搜索，并在区域之间使用隐含的AND，请在“进程搜索”页的“常规搜索”和“详细搜索”区域中输入搜索条件。

如果搜索范围太窄，则不会找到任何实例。
