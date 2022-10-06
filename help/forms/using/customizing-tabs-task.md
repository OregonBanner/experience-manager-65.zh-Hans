---
title: 为任务自定义选项卡
seo-title: Customizing tabs for a task
description: 如何在LiveCycleAEM Forms工作区中自定义任务的选项卡名称。
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 为任务自定义选项卡 {#customizing-tabs-for-a-task}

您可以自定义 `Start Process` 组件 `Start Process` Uber视图和 `Task Details` 组件 `ToDo` 优步视图。

1. 关注 [AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 更改 `tabname`在 `translation.json` 文件。

   例如，更改 `/apps/ws/locales/en-US/translation.json` 对下面的内容进行英语翻译。

   * 对于在启动过程中启动的任务，请使用 `"startprocess" : {}` 块。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 对于待办事项中的任务，请使用 `"todo" : {}` 块。

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
