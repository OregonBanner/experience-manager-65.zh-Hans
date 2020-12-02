---
title: 搜索进程实例
seo-title: 搜索进程实例
description: 使用“流程搜索”页可输入查找流程实例的搜索标准。
seo-description: 使用“流程搜索”页可输入查找流程实例的搜索标准。
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# 搜索进程实例{#searching-for-process-instances}

使用“流程搜索”页可输入查找流程实例的搜索标准。 您可以从表单工作流页面或通过单击“流程实例”页上的搜索来访问“流程搜索”页。

您可以输入基本条件以执行常规搜索，输入特定属性以执行详细搜索，或输入基本条件和特定属性的组合以执行组合搜索。

## 执行常规搜索{#perform-a-general-search}

如果您知道进程实例的进程ID、要查找一组相关进程实例，或者只运行了少数进程实例，则最适合对进程进行常规搜索。

输入基本条件以执行常规搜索。 如果输入多个条件，则使用隐含的AND条件执行搜索。

1. 在管理控制台中，单击“服务”>“Forms工作流”>“进程搜索”。
1. 在“流程搜索”页的“常规搜索”下，提供以下条件：

   * **进程ID：标** 识每个唯一进程实例的正整数。
   * **进程状** 态：从列表中选择状态。
   * **应用程** 序：从列表中选择一个应用程序。只显示已部署的应用程序。
   * **进程名称——版本：** 从菜单中选择一个进程名称。只显示已部署的进程。

1. 单击“搜索”。 此时将显示“进程实例”页，其中列出了找到的实例。

## 对进程{#perform-a-detailed-search-for-a-process}执行详细搜索

您可以输入特定属性以执行详细搜索。 如果您运行了许多进程实例，并且需要按特定条件缩小可能的查找范围，则最适合进行详细搜索。

1. 在管理控制台中，单击“服务”>“Forms工作流”>“进程搜索”。
1. 在“流程搜索”页的“详细搜索”下，指定您的第一个标准集：

   * 在“属性”列表中，选择一个属性。
   * 在“筛选器”列表中，选择一个运算符。
   * 在“值”(Value)框中，键入与所选属性相适应的值。

1. 要添加其他行，请选择更多过滤器。 出现另一组“属性”、“过滤器”和“值”列表，以及“条件”列表。
1. 在“条件”下，选择“与”或“或”。 根据需要重复步骤1 - 3以进一步缩小搜索范围。
1. 要添加或删除行，请单击“更多过滤器”或“更少过滤器”。 您可以有一至四行。
1. 单击“搜索”。 此时将显示“进程实例”页，其中列出了找到的实例。

[关于进程实例状态](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## 对进程{#perform-a-combined-search-for-a-process}执行组合搜索

要创建基于常规搜索和详细搜索的搜索（区域之间带有隐含的AND），请在“流程搜索”页的“常规搜索”和“详细搜索”区域中输入搜索条件。

如果搜索范围过窄，则找不到任何实例。
