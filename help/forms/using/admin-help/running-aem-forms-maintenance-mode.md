---
title: 在維護模式下執行AEM表單
seo-title: Running AEM forms in maintenance mode
description: 執行修補DSC、升級AEM表單或套用Service Pack等工作時，維護模式會很有用。 進一步瞭解如何在維護模式下執行AEM表單。
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 在維護模式下執行AEM表單 {#running-aem-forms-in-maintenance-mode}

執行修補DSC、升級AEM表單或套用Service Pack等工作時，維護模式會很有用。

伺服器處於維護模式時，請避免叫用任何處理程式。 如果伺服器處於維護模式時叫用程式，就會發生以下情況：

* 如果處理序為長期，則會新增至工作資料庫，但不會啟動。 當您結束維護模式時，AEM Forms會處理其佇列中的長期工作，即使伺服器是在維護模式中重新啟動亦然。
* 如果程式存留期較短，則會立即處理。

**將AEM表單置於維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「現已暫停」訊息。

   >[!NOTE]
   >
   >如果您在伺服器處於維護模式時將其關閉，則伺服器重新啟動時仍會處於維護模式。 完成維護任務後，您必須關閉維護模式。

**檢查AEM表單是否以維護模式執行**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   狀態會顯示在瀏覽器視窗中。 狀態「true」表示伺服器正在維護模式下執行，而「false」表示伺服器不在維護模式中。

**關閉維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「正在執行」訊息。
