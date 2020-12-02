---
title: 自定义任务的选项卡
seo-title: 自定义任务的选项卡
description: 如何在LiveCycleAEM Forms工作区中自定义任务的选项卡名称。
seo-description: 如何在LiveCycleAEM Forms工作区中自定义任务的选项卡名称。
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 自定义任务{#customizing-tabs-for-a-task}的选项卡

您可以为`Start Process` Uber视图中的`Start Process`组件和`ToDo` Uber视图中的`Task Details`组件自定义选项卡名称。

1. 按照[AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md)操作。
1. 在`translation.json`文件中更改`tabname`的值。

   例如，将“英语”的`/apps/ws/locales/en-US/translation.json`更改为以下内容。

   * 对于在开始过程中启动的任务，请使用`"startprocess" : {}`块中的以下代码片断。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于To-do中的任务，请使用`"todo" : {}`块中的以下代码片断。

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
