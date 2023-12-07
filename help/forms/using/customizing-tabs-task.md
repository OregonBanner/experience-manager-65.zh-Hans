---
title: 自定义任务的选项卡
description: 如何在LiveCycleAEM Forms工作区中自定义任务的选项卡名称。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 自定义任务的选项卡 {#customizing-tabs-for-a-task}

您可以自定义的选项卡名称 `Start Process` 中的组件 `Start Process` Uber视图和 `Task Details` 中的组件 `ToDo` Uber视图。

1. 请遵循 [AEM Forms工作区自定义的常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 更改的值 `tabname`在 `translation.json` 文件。

   例如，更改 `/apps/ws/locales/en-US/translation.json` 英语的译文。

   * 对于在启动过程中启动的任务，请使用以下代码片段： `"startprocess" : {}` 封锁。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于待办事项中的任务，使用以下代码片段： `"todo" : {}` 封锁。

   ```json
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
