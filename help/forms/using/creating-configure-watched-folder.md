---
title: 建立或設定watched資料夾
seo-title: Create or Configure a watched folder
description: 瞭解如何建立或刪除watched資料夾，或修改現有watched資料夾的屬性。
seo-description: Learn how to create or delete a watched folder, or modify the properties of an existing watched folder.
uuid: 659d4d8c-99b8-40dd-b884-bfee4d476fe1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 0ce7b338-6686-49b3-b58b-e7ab6b670708
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# 建立或設定watched資料夾 {#create-or-configure-a-watched-folder}

管理員可以設定網路資料夾，稱為 *觀察資料夾*，因此當使用者將檔案(例如PDF檔案)放入watched資料夾時，會啟動預先設定的作業並操作檔案。 執行指定的操作後，該操作會將修改的檔案儲存在指定的輸出資料夾中。 如需有關管理watched資料夾的詳細資訊，請參閱 [管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

您可以使用watched資料夾使用者介面來：

* 建立watched資料夾
* 修改現有Watched資料夾的屬性
* 刪除watched資料夾

## 建立watched資料夾 {#create-a-watched-folder}

在設定watched資料夾之前，請確定下列事項：

* Watched資料夾是AEM表單的進階功能。 它需要AEM Forms附加元件套件才能運作。 確保已安裝並設定適當的AEM Forms附加元件套件。
* 您可以在共用或本機存放區中建立watched資料夾。 確定設定為執行watched資料夾的AEM表單使用者擁有watched資料夾的讀取和寫入許可權。
* 您可以使用服務、工作流程或指令碼，自動執行watched資料夾的操作。 確保對應的服務、工作流程或指令碼已建立並準備執行。 如需建立服務、工作流程和指令碼的詳細資訊，請參閱 [處理檔案的各種方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* 觀察資料夾有各種屬性，請參閱 [Watched資料夾屬性](watched-folder-in-aem-forms.md#watchedfolderproperties).

執行以下步驟來建立watched資料夾：

1. 點選 **Adobe Experience Manager** 圖示加以檢視。
1. 點選 **工具** > **Forms** > **設定Watched資料夾。** 顯示已設定的Watched資料夾清單。
1. 點選 **新增**. 隨即顯示建立Watched資料夾所需的欄位清單：

   * **名稱**：識別watched資料夾。 名稱僅使用英數字元。
   * **路徑**：指定watched資料夾位置。 在叢集環境中，此設定必須指向共用網路資料夾，叢集不同節點上執行AEM的每個使用者都可以存取該資料夾。
   * **處理檔案，使用**：要啟動的程式型別。 您可以指定工作流程、指令碼或服務。
   * **服務名稱/指令碼路徑/工作流程路徑**：欄位的行為根據為指定的值 **處理檔案，使用** 欄位。 您可以指定下列值：

      * 針對「工作流程」，指定要執行的工作流程模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：content/model
      * 在指令碼中，指定要執行的指令碼的JCR路徑。 例如， /etc/watchfolder/test/testScript.ecma
      * 針對服務，指定用於找到OSGi服務的篩選器。 此服務註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實作。 例如，下列程式碼是具有custom (foo=bar)屬性的ContentProcessor介面的自訂實作。

   >[!NOTE]
   >
   >如果您已選取 **服務** 的 **處理檔案，使用** 欄位，服務名稱(inputProcessorType)欄位的值必須括在括弧中。 例如，(foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **輸出檔案模式**：指定以(；)分號分隔的模式清單，監看資料夾會使用這些模式來判斷輸出檔案和資料夾的名稱和位置。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).


1. 點選 **進階**. 進階索引標籤包含更多欄位。 這些欄位大多包含預設值。

   * **承載對應程式篩選器：** 當您建立watched資料夾時，它會在被監視的資料夾中建立資料夾結構。 資料夾結構有階段、結果、保留、輸入和失敗資料夾。 資料夾結構可作為工作流程的輸入裝載，並接受來自工作流程的輸出。 它也可以列出失敗點（如果有）。 承載的結構與watched資料夾的結構不同。 您可以撰寫自訂指令碼，將watched資料夾的結構對應至裝載。 此類指令碼稱為裝載對應程式篩選器。 提供兩種現成的裝載對應程式實作。 如果您沒有 [自訂實施](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，使用其中一種現成可用的實作：

      * **預設對應程式：** 使用預設的裝載對應程式，將watched資料夾的輸入和輸出內容保留在裝載中的個別輸入和輸出資料夾中。
      * **簡單的檔案型裝載對應程式：** 使用簡單檔案型裝載對應程式，將輸入和輸出內容直接保留在裝載資料夾中。 它不會建立任何額外的階層，例如預設對應程式。
   * **執行模式**：指定工作流程執行所允許的執行模式清單（以逗號分隔）。
   * **分段檔案逾時時間**：指定已擷取以供處理的輸入檔案/資料夾被視為已逾時並標籤為失敗之前，要等待的秒數。 逾時機制只會在這個屬性的值為正數時啟動。
   * **調整時刪除已逾時的階段檔案**：如果已啟用， **分段檔案逾時時間** 只有在watched資料夾的節流開啟時機制才會啟動。
   * **每隔以下時間掃描輸入資料夾：** 指定掃描watched資料夾以輸入內容的時間間隔（以秒為單位）。 除非啟用「限制」設定，否則「輪詢間隔」應比處理平均作業的時間長；否則，系統可能會超載。 間隔值必須大於或等於1。
   * **排除檔案模式**：指定以(；)分號分隔的模式清單，監看資料夾會使用這些模式來決定要掃描和擷取的檔案和資料夾。 不會掃描任何具有指定模式的檔案或資料夾以進行處理。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **包含檔案模式**：指定以分號(；)分隔的模式清單，Watched資料夾會使用該清單來決定要掃描和擷取的資料夾和檔案。 例如，如果「包含檔案模式」是input&amp;ast；，則會擷取符合input&amp;ast；的所有檔案和資料夾。 預設值為&amp;ast；，表示所有檔案和資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案陣列](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **等待時間：** 指定在建立資料夾或檔案後，掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 默认值为 0。

      此設定對於確保檔案或資料夾的所有內容都複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，且檔案下載需要10分鐘，請將等待時間設定為10&amp;ast；60 &amp;ast；1000毫秒。 此間隔可防止watched資料夾在檔案不是十分鐘之前掃描檔案。

   * **刪除早於以下時間的結果：** 指定刪除超過指定值的檔案和資料夾之前的等待時間（以天為單位）。 此設定對於確保結果資料夾未填滿非常有用。 值–1天表示從不刪除結果資料夾。 預設值為–1。
   * **結果資料夾名稱：** 指定要儲存結果的資料夾名稱。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理並儲存在失敗資料夾中。 您可以使用絕對或相對路徑配合下列檔案模式：

      * %F =檔案名稱前置詞
      * %E =副檔名
      * %Y =年（完整）
      * %y =年（最後兩位數）
      * %M =月
      * %D =日期
      * %d =一年中的第幾天
      * %H =小時（24小時時鐘）
      * %h =小時（12小時時鐘）
      * %m =分鐘
      * %s =秒
      * %l =毫秒
      * %R =隨機數字（介於0到9之間）
      * %P =處理程式或工作識別碼
      * 例如，如果是2009年7月17日晚上8點，而您指定C：/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾是C：/Test/WF0/failure/2009/07/17/20。
      * 如果路徑不是絕對路徑而是相對路徑，則會在watched資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，這是Watched資料夾內的Result資料夾。 如需檔案模式的詳細資訊，請參閱 [關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **失敗資料夾名稱：** 指定儲存失敗檔案的資料夾。 此位置永遠是相對於watched資料夾。 您可以使用檔案模式，如「結果資料夾」中所述。
   * **保留資料夾名稱：** 指定在成功掃描和擷取後儲存檔案的資料夾。 路徑可以是絕對、相對或null目錄。 您可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
   * **批次大小：** 指定每次掃描要擷取的檔案或資料夾數目。 它可防止系統過載；一次掃描太多檔案可能會導致當機。 默认值为 2。

      如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到watched資料夾中，則您應該將掃描間隔保持較小。 如果檔案不常被捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

   * **調整日期：** 啟用此選項時，會限制AEM表單在任何指定時間處理的監看資料夾工作數目。 「批次大小」值決定作業的最大數量。 如需詳細資訊，請參閱 [節流](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **以類似名稱覆寫現有檔案**：設為True時，會覆寫結果資料夾和保留資料夾中的檔案。 設定為False時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為False。
   * **失敗時保留檔案：** 設定為True時，會在失敗時保留輸入檔案。 預設值為true。
   * **包含具有模式的檔案：** 指定以分號(；)分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的資料夾和檔案。 例如，如果輸入「包含檔案模式」，則會擷取符合輸入的所有檔案和資料夾。 如需詳細資訊，請參閱 [管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **非同步叫用Watched資料夾：** 將呼叫型別識別為非同步或同步。 預設值為非同步。 建議將非同步處理用於長效處理作業，而建議將同步處理用於暫時性或短效處理作業。
   * **啟用Watched資料夾：** 啟用此選項時，會啟用監看資料夾。 預設值為True。



## 修改現有Watched資料夾的屬性 {#modify-properties-of-an-existing-watched-folder}

除了變更watched資料夾的名稱之外，您還可以修改現有watched資料夾的所有屬性。 執行以下步驟來修改現有watched資料夾的屬性：

1. 點選 **Adobe Experience Manager** 圖示加以檢視。
1. 點選 **工具** > **Forms** > **設定Watched資料夾。** 顯示已設定的Watched資料夾清單。
1. 在Watched Folder畫面的左側，選取watchfolder並點選 **編輯。** 隨即顯示建立Watched資料夾所需的欄位清單。 下列欄位中列出的資訊： **基本** 索引標籤為必填欄位。 進階索引標籤包含更多欄位。 這些欄位大多包含預設值。 您可以依需求修改這些屬性。
1. 修改屬性後，點選 **更新**. 修改後的屬性會儲存。
