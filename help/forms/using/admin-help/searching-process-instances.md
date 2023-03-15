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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 搜索进程实例{#searching-for-process-instances}

使用“进程搜索”页可以输入用于查找进程实例的搜索标准。 您可以从“表单”工作流页面中访问“流程搜索”页面，也可以单击“流程实例”页面中的“搜索”。

您可以输入执行常规搜索的基本标准、执行详细搜索的特定属性或执行组合搜索的基本标准和特定属性的组合。

## 执行常规搜索 {#perform-a-general-search}

如果您知道进程实例的进程ID，或者如果您正在查找一组相关的进程实例，或者只有少数几个进程实例正在运行，则对进程进行常规搜索是最合适的。

输入执行常规搜索的基本条件。 如果输入多个标准，则搜索会使用隐含的AND条件执行。

1. 在管理控制台中，单击服务> Forms工作流>进程搜索。
1. 在“进程搜索”页的“常规搜索”下，提供以下标准：

   * **进程ID：** 标识每个唯一进程实例的正整数。
   * **进程状态：** 从列表中选择一个状态。
   * **应用程序：** 从列表中选择应用程序。 仅显示已部署的应用程序。
   * **进程名称 — 版本：** 从菜单中选择进程名称。 只显示已部署的进程。

1. 单击“搜索”。 此时将显示“进程实例”页，其中列出了找到的实例。

## 对进程执行详细搜索 {#perform-a-detailed-search-for-a-process}

您可以输入特定属性以执行详细搜索。 如果您有许多正在运行的进程实例，并且需要按特定条件来缩小可能的查找范围，则最适合使用详细搜索。

1. 在管理控制台中，单击服务> Forms工作流>进程搜索。
1. 在“进程搜索”页的“详细搜索”下，指定您的第一个标准集：

   * 在“属性”列表中，选择一个属性。
   * 在“筛选器”列表中，选择一个运算符。
   * 在“值”框中，键入适合所选属性的值。

1. 要添加另一行，请选择“更多筛选器”。 另一组“属性”、“筛选器”和“值”列表以及“条件”列表将出现。
1. 在“条件”下，选择AND或OR。 根据需要重复步骤1 - 3，以进一步缩小搜索范围。
1. 要添加或删除行，请单击“更多筛选器”或“更少筛选器”。 可以有一到四行。
1. 单击“搜索”。 此时将显示“进程实例”页，其中列出了找到的实例。

[关于流程实例状态](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 对进程执行组合搜索 {#perform-a-combined-search-for-a-process}

要基于常规搜索和详细搜索创建搜索，并在区域之间使用隐含的AND，请在“进程搜索”页的“常规搜索”和“详细搜索”区域中输入搜索条件。

如果搜索范围太窄，则找不到实例。
