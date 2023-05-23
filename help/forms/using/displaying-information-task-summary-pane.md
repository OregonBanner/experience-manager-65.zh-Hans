---
title: 在工作摘要窗格中顯示資訊
seo-title: Displaying information in the Task Summary pane
description: 在AEM Forms工作區中，「任務摘要」窗格可設定為摘要任務或顯示任何其他網頁。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 在工作摘要窗格中顯示資訊 {#displaying-information-in-the-task-summary-pane}

當您在AEM Forms工作區中開啟任務時，「任務摘要」窗格會顯示任務的摘要。 這項工作的額外和相關資訊為AEM Forms工作區的一般使用者增加了更多價值。

AEM Forms工作區可讓您在「工作摘要」窗格中顯示您選擇的網頁。 您可以使用Workbench建立處理以顯示「工作摘要」窗格。

1. 在Workbench中建立「指定作業」處理。 如需「指派工作」作業的詳細資訊，請參閱以下連結中的服務參考主題： [Workbench說明](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >如果TaskSummary URL存在，預設會開啟Task Summary檢視，而不是Form檢視。 在這種情況下，即使使用者在指派任務中啟用了「以最大化模式開啟表單」選項，表單也不會以最大化模式開啟。

1. 設定「任務摘要URL」欄位。 您可以指定常值、範本、變數或XPath運算式。
1. 以下是在「任務摘要」頁面上顯示資訊的範例。

   * 登入CRXDE Lite環境： `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**範例摘要** ` under `/content` with type `nt：unstructured`. In the properties of this node, add `sling：resourceType` of type String and value `範例摘要`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr：read` privileges.`
   * `Create a folder`**範例摘要** 在 `/apps`. 在存取控制清單中 `/apps/SampleSummary`，新增專案 `PERM_WORKSPACE_USER` 允許 `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * 將任務摘要URL的值設為 `/lc/content/SampleSummary.html` 在指派工作步驟中。
   * 在AEM Forms工作區中開啟與此指派任務步驟相關聯的任務時， `html.esp` 於 `/apps/SampleSummary` 在任務摘要窗格中呈現。
