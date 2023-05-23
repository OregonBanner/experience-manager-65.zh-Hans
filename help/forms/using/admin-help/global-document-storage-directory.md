---
title: 全域檔案儲存目錄
seo-title: Global document storage directory
description: 全域檔案儲存(GDS)目錄是用來儲存處理序中使用的長期檔案的目錄。
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# 全域檔案儲存目錄{#global-document-storage-directory}

此 *全域檔案儲存(GDS)* directory是用來儲存處理序中使用的長期檔案的目錄。 這些檔案包括PDF、原則和表單範本。 長效檔案是許多AEM表單部署整體狀態的關鍵部分。 如果部分或所有長期檔案遺失或損毀，表單伺服器可能會變得不穩定。 非同步作業叫用的輸入檔案也儲存在GDS目錄中，並且必須可用於處理請求。 請務必考量裝載GDS目錄的檔案系統的可靠性。 使用獨立磁碟備援陣列(RAID)或其他技術，以因應您的品質和服務等級需求。

長效檔案可能包含敏感的使用者資訊。 使用AEM Forms API或使用者介面存取此資訊時，可能需要特殊認證。 務必透過作業系統正確保護GDS目錄。 只有用來執行應用程式伺服器的管理員帳戶才應該具有對GDS目錄的讀取/寫入存取權。

除了為GDS選取安全、高可用性的目錄之外，您也可以選擇啟用資料庫中的檔案儲存。 請注意，即使使用AEM Forms資料庫進行檔案儲存，AEM Forms仍需要GDS目錄。 (請參閱 [當資料庫用於檔案儲存時的備份選項](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms應用程式資料位於GDS目錄和AEM forms資料庫中。 下表說明資料及其位置。

<table>
 <thead>
  <tr>
   <th><p>AEM表單資料</p></th>
   <th><p>数据库</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>應用程式資料（使用者、角色、程式、原則、端點、事件等）。</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>已部署的服務容器</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>檔案管理員 </p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
  <tr>
   <td><p>Forms存放庫</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>系統設定</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>Watched資料夾</p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
 </tbody>
</table>

## 設定GDS目錄 {#configuring-the-gds-directory}

GDS目錄的位置可以在AEM表單安裝過程中手動設定。 如果在安裝期間位置設定保持空白，則該位置會預設為應用程式伺服器安裝下的目錄，如下所示：

* (JBos) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## 變更預設GDS位置 {#change-the-default-gds-location}

AEM表單安裝完成後，您可以在管理主控台中變更GDS位置。 您必須手動重新定位資料，才能完成此程式。

>[!NOTE]
>
>請以下列方式移轉資料，否則資料將會遺失。

1. 登入管理主控台，然後按一下「設定>核心系統設定>設定」。
1. 在「全域檔案儲存目錄」方塊中，輸入新GDS目錄的完整路徑，然後按一下「確定」。
1. 立即關閉應用程式伺服器。
1. 將所有檔案從舊的GDS目錄移至新的位置，保留內部目錄結構。
1. 重新啟動應用程式伺服器。

## 關於部署檔案 {#about-deployment-files}

AEM表單包含兩種型別的部署檔案：服務容器和Java 2 Platform， Enterprise Edition (J2EE) EAR檔案。 EAR檔案包含標準J2EE應用程式組合，其中包含AEM Forms的核心功能。 應用程式伺服器特定的EAR檔案如下：

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[作業系統]*.ear

實作AEM Forms包括將組裝的EAR檔案和支援檔案部署至您計畫執行AEM Forms解決方案的應用程式伺服器。 如果配置並組裝了多個模組，可部署的模組會封裝在可部署的EAR檔案中。 若要部署這些檔案，請將它們複製到 *[appserver首頁]*\server\all\deploy目錄。

模組和AEM表單封存檔封裝為JAR檔案。 因為它們不是J2EE型別檔案，所以不會部署至應用程式伺服器。 相反地，它們會複製到GDS目錄中，並且其位置的參照會儲存在AEM表單資料庫中。 因此，必須在叢集的所有節點之間共用GDS目錄。 所有節點都必須可以存取DSC的中央儲存目錄。

>[!NOTE]
>
>在部署服務容器之前，請確定您已建立並設定GDS目錄。 (請參閱 [設定GDS目錄](global-document-storage-directory.md#configuring-the-gds-directory))
