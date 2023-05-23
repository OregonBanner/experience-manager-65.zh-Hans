---
title: 觀察資料夾的備份策略
seo-title: Backup strategies for watched folders
description: 本檔案說明watched資料夾如何受到不同備份與復原案例的影響、這些案例的限制與結果，以及如何將資料遺失降至最低。
seo-description: This document describes how watched folders are affected by different backup and recovery scenarios, the limitations and outcomes of these scenarios, and how to minimize data loss.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# 觀察資料夾的備份策略 {#backup-strategies-for-watched-folders}

本內容說明watched資料夾如何受到不同備份與復原案例的影響、這些案例的限制與結果，以及如何將資料遺失降至最低。

*觀察資料夾* 是一個檔案系統型應用程式，可叫用已設定的服務作業，這些作業會在watched資料夾階層的下列其中一個資料夾中操作檔案：

* 输入
* 暂存
* 输出
* 失败
* 保留

使用者或使用者端應用程式會先將檔案或資料夾拖放到輸入資料夾中。 然後，服務操作會將檔案移動到中繼資料夾中以供處理。 服務執行指定的操作後，會將修改的檔案儲存在輸出資料夾中。 成功處理的來源檔案會移至保留資料夾，而失敗的處理檔案則會移至失敗資料夾。 當 `Preserve On Failure` 已啟用watched資料夾的屬性，失敗的已處理來源檔案會移至preserve資料夾。 (請參閱 [正在設定watched資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

您可以透過備份檔案系統來備份watched資料夾。

>[!NOTE]
>
>此備份與資料庫或檔案儲存備份與復原程式無關。

## 觀察資料夾的運作方式 {#how-watched-folders-work}

此內容說明Watched資料夾檔案操作程式。 在開發復原計畫之前，請務必瞭解此程式。 在此範例中， `Preserve On Failure` 已啟用watched資料夾的屬性。 檔案會依其到達的順序進行處理。

下表說明整個處理過程中五個範例檔案(file1、file2、file3、file4、file5)的檔案操作。 在表格中，x軸代表時間，例如Time 1或T1，而y軸代表監看資料夾階層內的資料夾，例如Input。

<table>
 <thead>
  <tr>
   <th><p>文件夹</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>输入</p></td>
   <td><p>檔案1，檔案2，檔案3，檔案4</p></td>
   <td><p>file2， file3， file4</p></td>
   <td><p>檔案3，檔案4</p></td>
   <td><p>file4</p></td>
   <td><p>空白</p></td>
   <td><p>file5</p></td>
   <td><p>空白</p></td>
  </tr>
  <tr>
   <td><p>暂存</p></td>
   <td><p>空白</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>空白</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
   <td><p>file1_out， file2_out， file4_out</p></td>
  </tr>
  <tr>
   <td><p>失败</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
   <td><p>file3_fail， file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1 </p></td>
   <td><p>file1， file2 </p></td>
   <td><p>file1， file2 </p></td>
   <td><p>file1， file2， file4 </p></td>
   <td><p>file1， file2， file4 </p></td>
  </tr>
 </tbody>
</table>

下列文字說明每次的檔案操作：

**T1：** 四個範例檔案會放置在輸入資料夾中。

**T2：** 服務作業會將file1移到stage資料夾中以進行操作。

**T3：** 服務作業會將file2移到stage資料夾中以進行操作。 它會將file1的結果放在輸出資料夾中，並將file1移動到保留資料夾。

**T4：** 服務操作會將file3放置在stage資料夾中以進行操作。 它會將file2的結果放置在輸出資料夾中，並將file2放置在保留資料夾中。

**T5：** 服務操作會將file4放置在stage資料夾中以進行操作。 處理file3失敗，服務操作會將其放在失敗資料夾中。

**T6：** 服務操作會將file5放置在輸入資料夾中。 它會將file4的結果放置在輸出資料夾中，將file4放置在保留資料夾中。

**T7：** 服務操作會將file5放置在stage資料夾中以進行操作。

## 備份watched資料夾 {#backing-up-watched-folders}

建議您將整個watched資料夾檔案系統備份至另一個檔案系統。

## 還原Watched資料夾 {#restoring-watched-folders}

本節說明如何還原Watched資料夾。 監看資料夾通常會叫用在一分鐘內完成的短期程式。 在這種情況下，以每小時完成的備份還原watched資料夾無法防止資料遺失。

例如，如果在T1時間進行備份，而伺服器在T7失敗，則file1、file2、file3和file4已被操控。 以T1的備份還原watched資料夾無法防止資料遺失。

如果已進行較新的備份，您可以還原檔案。 還原檔案時，請考量目前檔案所在的監看資料夾階層資料夾：

**階段：** 還原watched資料夾後，會再次處理此資料夾中的檔案。

**輸入：** 還原watched資料夾後，會再次處理此資料夾中的檔案。

**結果：** 不會處理此資料夾中的檔案。

**輸出：** 不會處理此資料夾中的檔案。

**保留：** 不會處理此資料夾中的檔案。

## 將資料遺失減至最低的策略 {#strategies-to-minimize-data-loss}

還原watched資料夾時，下列策略可最小化輸出和輸入資料夾資料遺失：

* 經常備份輸出和失敗資料夾（例如每小時），以避免遺失結果和失敗檔案。
* 將輸入檔案備份到watched資料夾以外的資料夾中。 這可確保復原後的檔案可用性，以防您在輸出或失敗資料夾中找不到檔案。 確保您的檔案命名配置一致。

   例如，如果您要儲存輸出並包含 `%F.`*擴充功能*，則輸出檔案的名稱將與輸入檔案相同。 這可協助您判斷要處理的輸入檔案以及必須重新提交哪些輸入檔案。 如果在結果資料夾中只看到file1_out檔案，而不是file2_out、file3_out和file4_out，則必須重新提交file2、file3和file4。

* 如果可用的watched資料夾備份時間早於處理作業所需的時間，您應允許系統建立新的watched資料夾，並自動將檔案放在輸入資料夾中。
* 如果最新的可用備份不夠新，則備份時間會少於處理檔案所花的時間，而且會還原watched資料夾，因此會在下列不同階段之一中操作檔案：

   * **階段1：** 在輸入資料夾中
   * **階段2：** 已複製到階段資料夾，但尚未叫用處理序
   * **階段3：** 已複製到階段資料夾，且已叫用處理序
   * **階段4：** 操作進行中
   * **階段5：** 傳回的結果

   如果檔案位於階段1，則會加以操控。 如果檔案位於「舞台2」或「舞台3」中，請將它們放置在輸入資料夾中，以便操作再次發生。

   >[!NOTE]
   >
   >如果檔案操作超過一次，可避免資料遺失，但結果可能會重複。

## 結論 {#conclusion}

由於Watched資料夾的動態且不斷改變的性質，應在一天內備份檔案完成復原Watched資料夾。 最佳實務建議備份結果、將輸入資料夾儲存在伺服器上，以及追蹤輸入檔案，以便在失敗時可以重新提交工作。
