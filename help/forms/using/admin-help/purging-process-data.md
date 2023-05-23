---
title: 清除程式資料
seo-title: Purging process data
description: 叫用長期處理程式時產生的處理程式資料可能會變得太大，導致AEM表單效能降低及使用不必要的磁碟空間。 瞭解如何永久刪除處理資料。
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 清除程式資料 {#purging-process-data}

叫用長期處理程式時產生的處理程式資料可能會變得太大，導致AEM表單效能降低及使用不必要的磁碟空間。 當不再需要記錄時，清除程式資料是很好的做法。 AEM forms提供幾種清除程式資料的方法：

* 您可以使用管理主控台，執行一次性永久刪除與長期處理相關的過時記錄，或排程定期自動永久刪除。 (請參閱 [從「工作管理員」資料庫中清除記錄](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* 您可以使用AEM Forms Java API和Web服務API，以程式設計方式清除與長期程式相關的程式資料。 (請參閱下列主題中的「清除程式資料」： [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).)
* 使用處理永久刪除工具，根據處理名稱和其他引數永久刪除處理。 如需詳細資訊，請參閱處理清除工具Readme檔案，檔案位於 *[aem_forms根]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
