---
title: 自訂任務的標籤
seo-title: Customizing tabs for a task
description: 如何在LiveCycleAEM Forms工作區中自訂您工作的標簽名稱。
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

# 自訂任務的標籤 {#customizing-tabs-for-a-task}

您可以自訂的標簽名稱 `Start Process` 中的元件 `Start Process` Uber檢視和 `Task Details` 中的元件 `ToDo` Uber檢視。

1. 請遵循 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md).
1. 變更值 `tabname`在 `translation.json` 檔案。

   例如，變更 `/apps/ws/locales/en-US/translation.json` 英文譯成下列內容。

   * 對於在啟動程式中啟動的任務，請使用以下來自的代碼片段 `"startprocess" : {}` 區塊。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * 對於待辦事項中的工作，使用以下檔案中的片段 `"todo" : {}` 區塊。

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
   >為所有支援的語言新增對應的機碼值組。
