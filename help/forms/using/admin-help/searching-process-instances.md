---
title: 搜索进程实例
seo-title: 搜索进程实例
description: 使用“流程搜索”页可输入搜索标准以查找流程实例。
seo-description: 使用“流程搜索”页可输入搜索标准以查找流程实例。
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 搜索进程实例{#searching-for-process-instances}

使用“流程搜索”页可输入搜索标准以查找流程实例。 您可以从表单工作流页面或单击“流程实例”页面上的“搜索”以访问“流程搜索”页面。

您可以输入基本标准以执行常规搜索，输入特定属性以执行详细搜索，或输入基本标准和特定属性的组合以执行组合搜索。

## 执行常规搜索{#perform-a-general-search}

如果您知道进程实例的进程ID，或者您正在查找一组相关的进程实例，或者只有少数进程实例正在运行，则对进程进行常规搜索最为合适。

输入基本标准以执行常规搜索。 如果您输入多个标准，则会使用隐含的AND条件执行搜索。

1. 在管理控制台中，单击服务> Forms工作流>流程搜索。
1. 在“流程搜索”页面的“常规搜索”下，提供以下条件：

   * **进程ID:** 标识每个唯一进程实例的正整数。
   * **进程状态：** 从列表中选择状态。
   * **应用程序：** 从列表中选择应用程序。仅显示已部署的应用程序。
   * **进程名称 — 版本：** 从菜单中选择一个进程名称。仅显示已部署的进程。

1. 单击搜索。 此时会出现“进程实例”页，其中列出了找到的实例。

## 对进程{#perform-a-detailed-search-for-a-process}执行详细搜索

您可以输入特定属性以执行详细搜索。 如果您运行了多个流程实例，并且需要按特定条件缩小可能的查找范围，则最适合进行详细搜索。

1. 在管理控制台中，单击服务> Forms工作流>流程搜索。
1. 在“流程搜索”页面的“详细搜索”下，指定第一个标准集：

   * 在“属性”列表中，选择一个属性。
   * 在过滤器列表中，选择一个运算符。
   * 在“值”(Value)框中，键入与所选属性相应的值。

1. 要添加另一行，请选择“更多过滤器”。 此时将出现另一组“属性”、“筛选器”和“值”列表，以及“条件”列表。
1. 在“条件”下，选择“与”或“或”。 根据需要重复步骤1 - 3以进一步缩小搜索范围。
1. 要添加或删除行，请单击更多过滤器或更少过滤器。 您可以有一行到四行。
1. 单击搜索。 此时会出现“进程实例”页，其中列出了找到的实例。

[关于流程实例状态](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 对进程{#perform-a-combined-search-for-a-process}执行组合搜索

要创建基于常规搜索和详细搜索的搜索（在区域之间使用默示的AND），请在“流程搜索”页面的“常规搜索”和“详细搜索”区域中输入搜索标准。

如果搜索范围太窄，则不会找到任何实例。
