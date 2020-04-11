---
title: 自定义任务的选项卡
seo-title: 自定义任务的选项卡
description: 如何在LiveCycle AEM Forms工作区中为任务自定义选项卡的名称。
seo-description: 如何在LiveCycle AEM Forms工作区中为任务自定义选项卡的名称。
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 自定义任务的选项卡 {#customizing-tabs-for-a-task}

您可以为Uber视图中的组 `Start Process` 件和Uber视图中的组 `Start Process` 件自定义选项卡 `Task Details``ToDo` 名称。

1. 按照AEM Forms工 [作区自定义的常规步骤操作](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 更改文件 `tabname`中的 `translation.json` 值。

   例如，将“英 `/apps/ws/locales/en-US/translation.json` 语”更改为以下内容。

   * 对于在开始过程中启动的任务，请使用块中的以下代 `"startprocess" : {}` 码片断。

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于To-do中的任务，请使用块中的以下代 `"todo" : {}` 码片断。

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。
