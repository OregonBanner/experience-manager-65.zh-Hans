---
title: 数据存储垃圾收集
seo-title: Data Store Garbage Collection
description: 瞭解如何設定資料存放區垃圾收藏集以釋放磁碟空間。
seo-description: Learn how to configure Data Store Garbage Collection to free up disk space.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# 数据存储垃圾收集 {#data-store-garbage-collection}

移除傳統WCM資產時，可能會從節點階層中移除對基礎資料存放區記錄的參考，但資料存放區記錄本身會保留。 然後，這個未參考的資料存放區記錄會變成不需要保留的「垃圾」。 在有大量垃圾資產的情況下，移除這些資產以保留空間，並最佳化備份和檔案系統維護效能，會很有幫助。

在大多數情況下，WCM應用程式傾向於收集資訊，但刪除資訊的頻率幾乎沒有。 雖然已新增新影像，但即使取代舊版本，版本控制系統仍會保留舊影像，並支援視需要還原成舊影像。 因此，我們視為新增至系統的大部分內容都會有效永久儲存。 那麼存放庫中，我們可能想要清理的典型「垃圾」來源是什麼？

AEM使用存放庫作為許多內部和內部管理活動的存放區：

* 建置和下載的套件
* 為發佈復寫建立的暫存檔
* 工作流程裝載
* 在DAM呈現期間暫時建立的資產

當任何這些暫存物件夠大，需要儲存在資料存放區時，且當物件最終退出使用時，資料存放區記錄本身會保留為「垃圾」。 在典型的WCM製作/發佈應用程式中，此型別記憶體的最大來源通常是發佈啟動程式。 當資料被復寫到Publish時，如果是先以稱為「Durbo」的有效資料格式在集合中收集，並儲存在下的存放庫中， `/var/replication/data`. 資料組合通常大於資料存放區的關鍵大小臨界值，因此最終會儲存為資料存放區記錄。 復寫完成後，中的節點 `/var/replication/data` 已刪除，但資料存放區記錄仍維持為「垃圾」。

另一個可回收的廢棄物來源是封裝。 封裝資料（像其他所有資料一樣）儲存在存放庫中，因此大於4KB的封裝資料會儲存在資料存放區中。 在開發專案的過程中，或在維護系統的過程中，可能會多次建置和重建套件，每個組建都會產生新的資料存放區記錄，孤立先前的組建記錄。

## 資料存放區垃圾收集如何運作？ {#how-does-data-store-garbage-collection-work}

如果存放庫已設定外部資料存放區， [資料存放區垃圾收集會自動執行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 作為「每週維護」視窗的一部分。 系統管理員也可以 [手動執行資料存放區垃圾收集](#running-data-store-garbage-collection) 視需要而定。 一般而言，建議定期執行資料存放區垃圾收集，但在規劃資料存放區垃圾收集時，應考量下列因素：

* 資料存放區垃圾收集需要時間，而且可能影響效能，因此應據此規劃。
* 移除資料存放區垃圾記錄不會影響一般效能，因此這並非效能最佳化。
* 如果不必擔心儲存空間使用率以及備份時間等相關因素，資料存放區垃圾收集可能會安全地延遲。

當程式開始時，資料存放區記憶體回收行程會先記下目前的時間戳記。 然後使用多通道標籤/掃描模式演演算法來執行收集。

在第一階段，資料存放區記憶體回收行程會執行所有存放庫內容的完整周遊作業。 對於每個參考了資料存放區記錄的內容物件，它會定位檔案系統中的檔案，執行中繼資料更新 — 修改「上次修改」或MTIME屬性。 此時，此階段存取的檔案會比初始基準時間戳記更新。

在第二階段，資料存放區垃圾收集器會以與「尋找」類似的方式周游資料存放區的實體目錄結構。 它會檢查檔案的「上次修改」或MTIME屬性，並進行以下判斷：

* 如果MTIME比初始基準時間戳記還新，則可能是檔案是在第一個階段找到，或是收集程式進行期間新增到存放庫的全新檔案。 在這兩種情況下，記錄都會被視為作用中，且檔案不應被刪除。
* 如果MTIME早於初始基準時間戳記，則檔案不是主動參照的檔案，且會視為可移除的廢棄專案。

此方法適用於具有私人資料存放區的單一節點。 不過，資料存放區可以共用，如果這表示系統不會檢查來自其他存放庫之資料存放區記錄的可能作用中即時參照，且可能會誤刪作用中參照的檔案。 系統管理員在計畫任何垃圾收集之前必須瞭解資料存放區的共用性質，並在已知資料存放區未共用時，僅使用簡單的內建資料存放區垃圾收集程式。

>[!NOTE]
>
>在叢集或共用資料存放區設定（使用Mongo或Segment Tar）中執行垃圾收集時，記錄可能會顯示無法刪除某些blob ID的警告。 發生此情況是因為其他叢集或共用節點再次錯誤地參考了先前垃圾收藏集中刪除的blob ID，而其他叢集或共用節點沒有ID刪除的相關資訊。 因此，當執行垃圾收集時，它會嘗試刪除在上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

## 正在執行資料存放區垃圾收集 {#running-data-store-garbage-collection}

根據AEM執行所在的資料存放區設定，有三種方式可執行資料存放區垃圾收集：

1. Via [修訂清除](/help/sites-deploying/revision-cleanup.md)  — 一種垃圾收集機制，通常用於節點存放區清理。

1. Via [資料存放區垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard)  — 外部資料存放區專用的垃圾收集機制，可在操作控制面板上使用。
1. 透過 [JMX主控台](/help/sites-administering/jmx-console.md).

如果TarMK同時作為節點存放區和資料存放區使用，則修訂清除可用於節點存放區和資料存放區的垃圾收集。 不過，如果設定了外部資料存放區（例如檔案系統資料存放區），則必須明確觸發資料存放區垃圾收藏集，且獨立於修訂版清理。 資料存放區垃圾收集可以透過操作儀表板或JMX主控台觸發。

下表顯示AEM 6中所有支援的資料存放區部署所需使用的資料存放區垃圾收集型別：

<table>
 <tbody>
  <tr>
   <td><strong>节点存储</strong><br /> </td>
   <td><strong>資料存放區</strong></td>
   <td><strong>垃圾收集機制</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>修訂清理（二進位檔與區段存放區內聯）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部檔案系統</td>
   <td><p>透過操作控制面板的資料存放區垃圾收集任務</p> <p>JMX主控台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>透過操作控制面板的資料存放區垃圾收集任務</p> <p>JMX主控台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部檔案系統</td>
   <td><p>透過操作控制面板的資料存放區垃圾收集任務</p> <p>JMX主控台</p> </td>
  </tr>
 </tbody>
</table>

### 透過操作儀表板執行資料存放區垃圾收集 {#running-data-store-garbage-collection-via-the-operations-dashboard}

內建的每週維護視窗，可透過 [操作控制面板](/help/sites-administering/operations-dashboard.md)，包含要在星期日凌晨1:00觸發資料存放區垃圾收集的內建工作。

如果您需要在此時間以外執行資料存放區垃圾收集，可以透過操作儀表板手動觸發。

在執行資料存放區垃圾收集之前，您應該檢查當時沒有執行任何備份。

1. 開啟「作業控制面板」的方法有： **導覽** -> **工具** -> **作業** -> **維護**.
1. 按一下或點選 **每週維護期間**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 選取 **資料存放區垃圾收集** 任務，然後按一下或點選 **執行** 圖示。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 資料存放區垃圾收集執行，其狀態會顯示在儀表板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在您已設定外部檔案資料存放區時，資料存放區垃圾收集工作才會顯示。 另請參閱 [在AEM 6中設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md#file-data-store) 有關如何設定檔案資料存放區的資訊。

### 透過JMX主控台執行資料存放區垃圾收集 {#running-data-store-garbage-collection-via-the-jmx-console}

本節說明如何透過JMX主控台手動執行資料存放區垃圾收集。 如果您的安裝設定沒有外部資料存放區，則這不適用於您的安裝。 請改為參閱下方的如何執行修訂清除的指示 [維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>如果您使用外部資料存放區執行TarMK，必須先執行修訂清除，垃圾收集才會生效。

若要執行垃圾收集：

1. 在Apache Felix OSGi Management Console中，反白顯示 **主要** 標籤並選取 **JMX** 從下列功能表。
1. 接下來，搜尋並按一下 **存放庫管理員** MBean (或前往 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`)。
1. 按一下 **startDataStoreGC（布林值markOnly）**.
1. 輸入&quot;`true`的「」 `markOnly` 引數（若有需要）：

   | **选项** | **描述** |
   |---|---|
   | 布林值markOnly | 設定為true可只標籤參照，而不會在標籤和掃描操作中掃描。 當基礎BlobStore在多個不同存放庫之間共用時，將使用此模式。 對於所有其他情況，將其設定為false以執行完整垃圾收集。 |

1. 按一下 **叫用**. CRX會執行垃圾收藏集並指示其完成時間。

>[!NOTE]
>
>資料存放區垃圾收集不會收集過去24小時內已刪除的檔案。

>[!NOTE]
>
>只有在您已設定外部檔案資料存放區時，資料存放區垃圾收集工作才會啟動。 如果尚未設定外部檔案資料存放區，工作將傳回訊息 `Cannot perform operation: no service of type BlobGCMBean found` 叫用之後。 另請參閱 [在AEM 6中設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md#file-data-store) 有關如何設定檔案資料存放區的資訊。

## 自動化資料存放區垃圾收集 {#automating-data-store-garbage-collection}

如果可能的話，資料存放區垃圾收集應在系統負載很少時執行，例如在早上。

內建的每週維護視窗，可透過 [操作控制面板](/help/sites-administering/operations-dashboard.md)，包含要在星期日凌晨1:00觸發資料存放區垃圾收集的內建工作。 您也應該檢查目前沒有執行任何備份。 必要時，可透過控制面板自訂維護視窗的開始。

>[!NOTE]
>
>不同時執行的原因是，舊的（和未使用的）資料存放區檔案也會進行備份，因此如果需要復原到舊的修訂版本，二進位檔案仍會保留在備份中。

如果您不希望在作業儀表板中的每週維護視窗中執行資料存放區垃圾收集，也可以使用wget或curl HTTP使用者端將其自動化。 以下是如何使用curl自動化備份的範例：

>[!CAUTION]
>
>在以下範例中 `curl` 命令您可能需要為您的執行個體設定各種引數；例如，主機名稱( `localhost`)，連線埠( `4502`)，管理員密碼( `xyz`)和各種引數來進行實際的資料存放區垃圾收集。

以下是透過命令列叫用資料存放區垃圾收集的curl命令範例：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令會立即傳回。

## 檢查資料存放區一致性 {#checking-data-store-consistency}

資料存放區一致性檢查會報告任何遺失但仍被參考的資料存放區二進位檔。 若要開始一致性檢查，請遵循下列步驟：

1. 前往JMX主控台。 如需有關如何使用JMX主控台的資訊，請參閱 [本文](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. 搜尋 **BlobGarbageCollection** Mbean並按一下它。
1. 按一下 `checkConsistency()` 連結。

一致性檢查完成後，訊息會顯示回報為遺失的二進位檔數目。 如果數字大於0，請檢查 `error.log` 以取得有關遺失二進位檔的詳細資訊。

下方提供如何在記錄中報告遺失的二進位檔的範例：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
