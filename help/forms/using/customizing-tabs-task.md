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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自定义任务的选项卡 {#customizing-tabs-for-a-task}

您可以在Uber视图中为组件自 `Start Process` 定义选项卡名称， `Start Process` 在 `Task Details` Uber视图中为组件自定义 `ToDo` 选项卡名称。

1. 按照AEM Forms工 [作区自定义的常规步骤操作](/help/forms/using/generic-steps-html-workspace-customization.md)。
1. 更改文件 `tabname`中的 `translation.json` 值。

   例如，将“英 `/apps/ws/locales/en-US/translation.json` 语”更改为以下内容。

   * 对于在启动进程中启动的任务，请使用块中的以下代码 `"startprocess" : {}` 片断。

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于“待办事项”中的任务，请使用块中的以下代 `"todo" : {}` 码片断。

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

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
