---
title: 管理您的数字资源
description: 瞭解資產管理工作，例如上傳、下載、編輯、搜尋、刪除、註釋和更新您的數位資產。
contentOwner: AG
role: User
feature: Asset Management,Search
mini-toc-levels: 4
exl-id: 158607e6-b4e9-4a3f-b023-4023d60c97d2
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '9970'
ht-degree: 4%

---

# 管理您的数字资源 {#manage-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-digital-assets.html?lang=en) |
| AEM 6.5 | 本文 |

在 [!DNL Adobe Experience Manager Assets]，您不單可以儲存和管理您的資產。 [!DNL Experience Manager] 提供企業級資產管理功能。 您可以編輯和共用資產、執行進階搜尋，以及建立數十種支援的檔案格式的多重轉譯。 您也可以管理版本和數位版權、自動化資產處理、管理和控管中繼資料、使用註解進行共同作業等等。

本文會說明基本資產管理工作，例如建立或上傳、中繼資料更新、複製、移動和刪除、發佈、取消發佈和搜尋資產。 若要瞭解使用者介面，請參閱 [開始使用資產使用者介面](/help/sites-authoring/basic-handling.md). 若要管理內容片段，請參閱 [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md) 資產。

## 创建文件夹 {#creating-folders}

例如，組織資產集合時，所有 `Nature` 您可以建立資料夾來將它們放在一起。 您可以使用資料夾來分類及組織您的資產。 [!DNL Experience Manager Assets] 您不需要在資料夾中組織資產才能更佳運作。

>[!NOTE]
>
>* 共用 [!DNL Assets] 型別的資料夾 `sling:OrderedFolder` 不支援在共用至Experience Cloud時使用。 如果要共用資料夾，請勿選取 [!UICONTROL 已訂購] 建立資料夾時。
>* [!DNL Experience Manager] 不允許使用 `subassets` word做為資料夾的名稱。 這是為包含複合資產之子資產的節點保留的關鍵字。


1. 導覽至數位資產資料夾中您要建立資料夾的位置。 在功能表中，按一下 **[!UICONTROL 建立]**. 選取 **[!UICONTROL 新增資料夾]**.
1. 在 **[!UICONTROL 標題]** 欄位中，提供資料夾名稱。 根據預設，DAM會使用您提供的標題作為資料夾名稱。 建立資料夾後，您可以覆寫預設值並指定另一個資料夾名稱。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的資料夾會顯示在數位資產資料夾中。

不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不能包含下列任一字元： `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不能包含下列任一字元： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

請勿在資產檔案名稱的副檔名中包含特殊字元。

## 上传资源 {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

您可以從本機資料夾或網路磁碟機將各種型別的資產(包括影像、PDF檔案、RAW檔案等)上傳到 [!DNL Experience Manager Assets].

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，預設的資產上傳檔案大小為2 GB以下。 若要設定大於2 GB資產的上傳，最高可達15 GB，請參閱 [（可選）設定Dynamic Media - Scene7模式以上傳大於2 GB的資產](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb).

您可以選擇將資產上傳到資料夾，而不論資料夾是否已指派處理設定檔。

對於已指派處理設定檔的資料夾，設定檔名稱會出現在卡片檢視的縮圖上。 在清單檢視中，設定檔名稱會出現在 **處理設定檔** 欄。 另請參閱 [處理設定檔](/help/assets/processing-profiles.md).

上傳資產之前，請確定資產位於 [格式](/help/assets/assets-formats.md) 該 [!DNL Experience Manager Assets] 支援。

1. 在 [!DNL Assets] 使用者介面，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請執行下列任一項作業：

   * 在工具列上，按一下 **[!UICONTROL 建立]**. 然後在功能表上，按一下 **[!UICONTROL 檔案]**. 如有需要，您可以在顯示的對話方塊中重新命名檔案。
   * 在支援HTML5的瀏覽器中，將資產直接拖曳至 [!DNL Assets] 使用者介面。 不會顯示重新命名檔案的對話方塊。

   ![建立上傳資產的選項](assets/create-options.png)

   若要選取多個檔案，請選取 `Ctrl` 或 `Command` 鍵，並在「檔案選擇器」對話方塊中選取資產。 使用iPad時，您一次只能選取一個檔案。

   您可以暫停上傳大型資產（大於500 MB），稍後再從相同頁面繼續上傳。 按一下 **[!UICONTROL 暫停]** 上傳開始時顯示的進度列旁邊。

   ![上傳資產進度列](assets/upload-progress-bar.png)

可設定將資產視為大型資產的大小。 例如，您可以將系統設定為將大於1000 MB （而非500 MB）的資產視為大型資產。 在這種情況下， **[!UICONTROL 暫停]** 當大小超過1000 MB的資產上傳時，進度列上會顯示。

此 [!UICONTROL 暫停] 如果上傳大於1000 MB的檔案時小於1000 MB，則選項不會顯示。 不過，如果您取消小於1000-MB的檔案上傳， **[!UICONTROL 暫停]** 選項隨即顯示。

若要修改大小限制，請設定 `chunkUploadMinFileSize` 的屬性 `fileupload` CRX存放庫中的節點位於 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`.

當您按一下 **[!UICONTROL 暫停]**，它會切換至 **[!UICONTROL 播放]** 選項。 若要繼續上傳，請按一下 **[!UICONTROL 播放]**.

若要取消進行中的上傳，請按一下關閉(`X`)。 當您取消上傳作業時， [!DNL Assets] 刪除資產中部分上傳的部分。

在低頻寬和網路故障的情況下，恢復上傳的功能特別有用，因為上傳大型資產需要很長的時間。 您可以暫停上傳操作，等情況改善後再繼續。 當您繼續時，上傳會從您暫停的時間點開始。

在上傳作業期間， [!DNL Experience Manager] 將上傳的資產部分儲存為CRX存放庫中的資料區塊。 上傳完成時， [!DNL Experience Manager] 將這些區塊整合為存放庫中的單一資料區塊。

若要設定未完成的區塊上傳工作的清理工作，請移至 `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.

>[!CAUTION]
>
>當預設值為500 MB且區塊大小為50 MB時會觸發區塊上傳。 如果您編輯 [Apache Jackrabbit Oak權杖設定](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16464.html) 並設定 `timeout configuration` 由於上傳資產所花費的時間少於，因此您在資產上傳期間會遇到工作階段逾時情況。 因此，請變更 `chunkUploadMinFileSize` 和 `chunksize` 因此每個區塊要求都會重新整理工作階段。
>
>在認證到期逾時、延遲、頻寬和預期並行上傳的指定下，可讓您確保挑選下列專案的最高值：
>
>* 確保在上傳過程中，針對很可能導致認證到期的檔案啟用區塊上傳。
>
>* 確保每個區塊在認證過期之前完成。


如果您上傳的資產名稱與上傳資產位置已有可用的資產名稱相同，系統會顯示警告對話方塊。

您可以選擇重新命名上傳的新資產，以取代現有資產、建立其他版本或保留兩者。 如果您取代現有資產，資產的中繼資料以及您先前對現有資產所做的任何修改（例如註釋或裁切）都會被刪除。 如果您選擇保留兩個資產，則新資產會以數字重新命名 `1` 附加至其名稱。

![解決資產名稱衝突的「名稱衝突」對話方塊](assets/resolve-naming-conflict.png)

>[!NOTE]
>
>當您選取 **[!UICONTROL Replace]** 在 [!UICONTROL 名稱衝突] 對話方塊中，會為新資產重新產生資產ID。 此ID與先前資產的ID不同。
>
>如果啟用資產分析來追蹤曝光次數或點按 [!DNL Adobe Analytics]，則重新產生的資產ID會使為資產擷取的資料於失效 [!DNL Analytics].

如果您上傳的資產存在於中 [!DNL Assets]，則 **[!UICONTROL 偵測到重複專案]** 對話方塊會警告您嘗試上傳重複的資產。 只有在下列情況下，對話方塊才會出現 `SHA 1` 現有資產二進位的檢查加總值與您上傳之資產的檢查加總值相符。 在這種情況下，資產的名稱並不重要。

>[!NOTE]
>
>此 [!UICONTROL 偵測到重複專案] 只有在啟用重複資料偵測功能時，對話方塊才會出現。 若要啟用重複資料偵測功能，請參閱 [啟用重複資料偵測](/help/assets/duplicate-detection.md).

![偵測到重複資產對話方塊](assets/duplicate-asset-detected.png)

若要在中保留重複資產 [!DNL Assets]，按一下 **[!UICONTROL 保留]**. 若要刪除您上傳的重複資產，請按一下 **[!UICONTROL 刪除]**.

[!DNL Experience Manager Assets] 可防止您上傳其檔案名稱中包含禁止字元的資產。 如果您嘗試上傳檔案名稱包含不允許字元以上的資產， [!DNL Assets] 顯示警告訊息並停止上傳，直到您移除這些字元或使用允許名稱上傳為止。

為了配合您組織的特定檔案命名慣例， [!UICONTROL 上傳資產] 對話方塊可讓您為上傳的檔案指定長名稱。

但是，不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不得包含 `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不得包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

請勿在資產檔案名稱的副檔名中包含特殊字元。

![上傳進度對話方塊顯示已成功上傳的檔案和無法上傳的檔案的狀態](assets/bulk-upload-progress.png)

此外， [!DNL Assets] 使用者介面會顯示您上傳的最新資產或您先建立的資料夾。

如果您在上傳檔案之前取消上傳作業， [!DNL Assets] 停止上傳目前的檔案並重新整理內容。 不過，不會刪除已上傳的檔案。

中的上傳進度對話方塊 [!DNL Assets] 顯示成功上傳的檔案數和無法上傳的檔案數。

### 序列上傳 {#serialuploads}

大量上傳資產會消耗大量的I/O資源，可能會對您的效能造成負面影響。 [!DNL Assets] 部署。 尤其當網際網路連線速度緩慢時，由於磁碟I/O尖峰，上傳的時間會大幅增加。此外，您的網頁瀏覽器可能會對POST請求的數量施加其他限制 [!DNL Assets] 可以處理同時的資產上傳。 因此，上傳作業失敗或過早終止。 換句話說， [!DNL Experience Manager Assets] 擷取一棧檔案時可能會遺漏某些檔案，或是完全無法擷取任何檔案。

若要克服這種情況， [!DNL Assets] 在大量上傳作業期間一次擷取一個資產（序列上傳），而非同時擷取所有資產。

資產序列上傳預設為啟用。 若要停用功能並允許同時上傳，請覆蓋 `fileupload` Crx-de中的節點並設定 `parallelUploads` 屬性至 `true`.

### 使用FTP上傳資產 {#uploading-assets-using-ftp}

Dynamic Media可透過FTP伺服器批次上傳資產。 如果您想要上傳大型資產（大於1 GB）或上傳整個資料夾和子資料夾，應使用FTP。 您甚至可以將FTP上傳設定為定期排程。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，預設的資產上傳檔案大小為2 GB以下。 若要設定大於2 GB資產的上傳，最高可達15 GB，請參閱 [（可選）設定Dynamic Media - Scene7模式以上傳大於2 GB的資產](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb).

>[!NOTE]
>
>若要在Dynamic Media - Scene7模式下透過FTP上傳資產，請將Feature Pack 18912安裝在 [!DNL Experience Manager] 作者執行個體。 連絡人 [Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support) 以存取FP-18912並完成FTP帳戶的設定。 如需詳細資訊，請參閱 [安裝Feature Pack 18912以進行大量資產移轉](/help/assets/bulk-ingest-migrate.md).
>
>如果您使用FTP上傳資產，請依照中指定的上傳設定 [!DNL Experience Manager] 將被忽略。 而是改用檔案處理規則(如Dynamic Media Classic中所定義)。

**若要使用FTP上傳資產**

1. 使用您選擇的FTP使用者端，使用您從布建電子郵件收到的FTP使用者名稱和密碼登入FTP伺服器。 在FTP使用者端中，將檔案或資料夾上傳至FTP伺服器。

1. 開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登入您的帳戶。

   布建時Adobe已提供您的認證和登入。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在全域導覽列上，按一下 **[!UICONTROL 上傳]**.
1. 在上傳頁面左上角附近，按一下 **[!UICONTROL 透過FTP]** 標籤。
1. 在頁面左側，選擇要上傳檔案的FTP資料夾；在頁面右側，選擇目的地資料夾。
1. 在頁面的右下角附近，按一下 **[!UICONTROL 工作選項]** ，然後根據您選取的資料夾中的資產設定您想要的選項。

   另請參閱 [上載工作選項](#upload-job-options).

   >[!NOTE]
   >
   >透過FTP上傳資產時，您在Dynamic Media Classic (S7)中設定的上傳工作選項會先於在中設定的資產處理引數 [!DNL Experience Manager].

1. 在「上傳工作選項」對話方塊的右下角，按一下 **[!UICONTROL 儲存]**.
1. 在上傳頁面的右下角，按一下 **[!UICONTROL 提交上傳]**.

   若要檢視上傳進度，請在全域導覽列上按一下 **[!UICONTROL 工作]**. 「工作」頁面會顯示上載的進度。 您可以繼續使用 [!DNL Experience Manager] 並隨時返回Dynamic Media Classic中的「工作」頁面，檢閱進行中的工作。
若要取消進行中的上載工作，請按一下 **[!UICONTROL 取消]** 在「持續時間」時間旁。

#### 上載工作選項 {#upload-job-options}

| 上傳選項 | 子選項 | 描述 |
|---|---|---|
| 作业名称 |  | 文字欄位中預先填寫的預設名稱包括使用者輸入的名稱部分和日期與時間戳記。 您可以使用預設名稱，或為此上載工作輸入您自己建立的名稱。 <br>工作和其他上載及發佈工作會記錄在「工作」頁面上，您可以在此檢查工作的狀態。 |
| 上傳後發佈 |  | 自動發佈您上傳的資產。 |
| 在任意文件夹内，使用相同的基本资源名称（不区分扩展名）进行覆盖 |  | 如果您希望上傳的檔案以相同名稱取代現有檔案，請選取此選項。 此選項的名稱可能會有所不同，視中的設定而定 **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]** > **[!UICONTROL 上傳至應用程式]** > **[!UICONTROL 覆寫影像]**. |
| 上傳時解壓縮Zip或Tar檔案 |  |  |
| 工作選項 |  | 按一下 **[!UICONTROL 工作選項]** 以便您能開啟 [!UICONTROL 上載工作選項] 對話方塊，然後選擇影響整個上載工作的選項。 這些選項對於所有檔案型別都相同。<br>您可以從「應用程式一般設定」頁面開始選擇上傳檔案的預設選項。 若要開啟此頁面，請選擇 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]**. 選取 **[!UICONTROL 預設上傳選項]** 開啟 [!UICONTROL 上載工作選項] 對話方塊。 |
|  | 时间 | 選取「一次性」或「週期性」。 若要設定週期性工作，請選擇重複選項（每日、每週、每月或自訂），以指定您希望FTP上傳工作重複的時間。 然後視需要指定排程選項。 |
|  | 包含子資料夾 | 上傳您要上傳之資料夾中的所有子資料夾。 您上傳的資料夾及其子資料夾的名稱會自動輸入到 [!DNL Experience Manager Assets]. |
|  | 裁剪选项 | 若要從影像側面手動裁切，請選取「裁切」選單，然後選擇「手動」。 然後輸入要從影像任何一面或每一面裁切的畫素數。 裁切多少影像取決於影像檔案中的ppi （每英吋畫素）設定。 例如，如果影像顯示150 ppi，而您在「上」、「右」、「下」和「左」文字方塊中輸入75，則會從每側裁切半英吋。<br> 若要自動裁切影像中的空白畫素，請開啟「裁切」選單，選擇「手動」，然後在「上」、「右」、「下」和「左」欄位中輸入畫素度量，從側面裁切。 您也可以選擇「裁切」選單上的「裁切」，然後選擇下列選項：<br> **修剪依據** <ul><li>**顏色**  — 選擇「顏色」選項。 然後選取「轉角」功能表，再選擇最能代表您要裁切之空白顏色的影像轉角。</li><li>**透明度**  — 選擇「透明度」選項。<br> **容許度**  — 拖曳滑桿以指定從0到1的容許度。若要根據顏色進行裁剪，請指定0以裁切畫素，但前提是畫素完全符合您在影像角落選取的顏色。 數字越接近1，色彩差異越大。<br>若要根據透明度進行裁剪，請指定0以裁切畫素，除非畫素是透明的。 數字越接近1，透明度越高。</li></ul><br>這些裁切選項不具破壞性。 |
|  | 色彩設定檔選項 | 當您建立用於傳送的最佳化檔案時，請選擇色彩轉換：<ul><li>預設色彩儲存：當影像包含色域資訊時，保留來源影像色彩；沒有色彩轉換。 目前幾乎所有影像都已內嵌適當的色彩設定檔。 不過，如果CMYK來源影像未包含內嵌色彩設定檔，則這些色彩會轉換為sRGB （標準紅綠藍）色彩空間。 sRGB是在網頁上顯示影像的建議色彩空間。</li><li>保留原始色域：保留原始顏色，而不進行任何色彩轉換。 對於沒有內嵌色彩設定檔的影像，任何色彩轉換都是使用在「發佈」設定中設定的預設色彩設定檔來完成。 色彩設定檔可能不會與使用此選項建立的檔案中的色彩對齊。 因此，建議您使用「預設色彩保留」選項。</li><li>自訂從>到<br> 開啟選單，讓您能夠選擇「轉換自」和「轉換至」色域。 此進階選項會覆寫任何內嵌在來源檔案中的顏色資訊。 當您提交的所有影像包含不正確或遺失色彩設定檔資料時，請選取此選項。</li></ul> |
|  | 影像編輯選項 | 您可以保留影像中的剪裁遮色片，並選擇色彩設定檔。<br> 另請參閱 [設定上傳時影像編輯的選項](#setting-image-editing-options-at-upload). |
|  | Postscript選項 | 您可以點陣化PostScript®檔案、裁切檔案、保留透明背景、選擇解析度以及選擇色域。<br> 另請參閱 [設定PostScript和Illustrator上傳選項](#setting-postscript-and-illustrator-upload-options). |
|  | Photoshop選項 | 您可以從Adobe® Photoshop®檔案建立範本、維護圖層、指定圖層的命名方式、擷取文字，以及指定影像錨定到範本的方式。<br> 不支援範本 [!DNL Experience Manager].<br> 另請參閱 [設定Photoshop上傳選項](#setting-photoshop-upload-options). |
|  | PDF選項 | 您可以點陣化檔案、擷取搜尋字詞和連結、自動產生eCatalog、設定解析度，以及選擇色域。<br>不支援eCatalog [!DNL Experience Manager]. <br> 另請參閱 [設定PDF上傳選項](#setting-pdf-upload-options).<br>**注意**：對於新上傳，PDF要考慮用於擷取的最大頁數為5000。 2022年12月31日起，所有PDF的此限制將變更為100頁。 另請參閱 [Dynamic Media限制](/help/assets/limitations.md). |
|  | Illustrator選項 | 您可以點陣化Adobe Illustrator®檔案、維持透明背景、選擇解析度，以及選擇色域。<br> 另請參閱 [設定PostScript和Illustrator上傳選項](#setting-postscript-and-illustrator-upload-options). |
|  | EVideo選項 | 您可以透過選擇視訊預設集來轉碼視訊檔案。<br> 另請參閱 [設定eVideo上傳選項](#setting-evideo-upload-options). |
|  | 批次集预设 | 若要從上傳的檔案建立「影像集」或「迴轉集」，請按一下您要使用之預設集的「作用中」欄。 您可以選取多個預設集。 您可以在Dynamic Media Classic的「應用程式設定/批次集預設集」頁面中建立預設集。<br> 另請參閱 [設定批次集預設集以自動生成影像集和迴轉集](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 以進一步瞭解如何建立批次集預設集。<br> 另請參閱 [在上傳時設定批次集預設集](#setting-batch-set-presets-at-upload). |

#### 設定上傳時影像編輯的選項 {#setting-image-editing-options-at-upload}

上傳影像檔案(包括AI、EPS和PSD檔案)時，您可以在 [!UICONTROL 上載工作選項] 對話方塊：

* 從影像邊緣裁切空白字元（請參閱上表說明）。
* 從影像側面手動裁切（請參閱上表說明）。
* 選擇色彩設定檔（請參閱上表中的選項說明）。
* 從剪裁路徑建立遮色片。
* 使用非銳利化遮色片選項銳利化影像
* 去底色背景

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop's Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone's face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or "turn on" the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### 設定PostScript和Illustrator上傳選項 {#setting-postscript-and-illustrator-upload-options}

上傳PostScript (EPS)或Illustrator (AI)影像檔案時，您可以透過各種方式格式化它們。 您可以點陣化檔案、維持透明背景、選擇解析度，以及選擇色域。 格式化PostScript和Illustrator檔案的選項可在 [!UICONTROL 上載工作選項] 對話方塊於 [!UICONTROL PostScript選項] 和 [!UICONTROL Illustrator選項].

| 选项 | 子選項 | 描述 |
|---|---|---|
| 正在处理 |  | 選擇 **[!UICONTROL 點陣化]** 將檔案中的向量圖形轉換為點陣圖格式。 |
| 在演算後的影像中維持透明背景 |  | 維持檔案的背景透明度。 |
| 解决方法 |  | 決定解析度設定。 此設定決定檔案中每英吋顯示的畫素數。 |
| 色彩空间 |  | 選取「色域」選單，然後從下列色域選項中選擇： |
|  | 自動偵測 | 保留檔案的色域。 |
|  | 強製為RGB | 轉換為RGB色域。 |
|  | 強製為CMYK | 轉換為CMYK色彩空間。 |
|  | 強製為灰階 | 轉換為灰階色彩空間。 |

#### 設定Photoshop上傳選項 {#setting-photoshop-upload-options}

Photoshop檔案(PSD)檔案最常用於建立影像範本。 上傳PSD檔案時，您可以從檔案中自動建立影像範本(選取 [!UICONTROL 建立範本] 選項)。

如果您使用檔案來建立範本，Dynamic Media會從含有圖層的PSD檔案建立多個影像；它會為每個圖層建立一個影像。

使用 [!UICONTROL 裁切選項] 和 [!UICONTROL 色彩設定檔選項]，如上所述，搭配Photoshop上傳選項。

>[!NOTE]
>
>不支援範本 [!DNL Experience Manager].

| 选项 | 子選項 | 描述 |
|---|---|---|
| 保留圖層 |  | 將PSD中的圖層（如果有的話）擷取到個別資產中。 資產圖層會維持與PSD相關聯。 您可以在「詳細資訊」檢視中開啟PSD檔案，並選取圖層面板來檢視它們。 |
| 创建模板 |  | 從PSD檔案中的圖層建立範本。 |
| 擷取文字 |  | 擷取文字，讓使用者能在檢視器中搜尋文字。 |
| 将图层扩展至背景大小 |  | 將擷取的影像圖層大小延伸至背景圖層大小。 |
| 圖層命名 |  | PSD檔案中的圖層會以個別影像的形式上傳。 |
|  | 圖層名稱 | 在PSD檔案中，將影像命名為圖層名稱后的名稱。 例如，原始PSD檔案中名為「價格標籤」的圖層會變成名為「價格標籤」的影像。 不過，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（「背景」、「圖層1」、「圖層2」等），則會以影像在PSD檔案中的圖層編號來命名影像。 它們不會以預設圖層名稱命名。 |
|  | Photoshop和圖層編號 | 將影像命名為PSD檔案中的圖層編號後方，略過原始圖層名稱。 影像以Photoshop檔案名稱及附加的圖層編號命名。 例如，名為Spring Ad.psd之檔案的第二層名為Spring Ad_2，即使它在Photoshop中有非預設名稱亦然。 |
|  | Photoshop和圖層名稱 | 在PSD檔案後面加上圖層名稱或圖層編號來命名影像。 如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱，則會使用圖層編號。 例如，在名為SpringAd的PSD檔案中，名為Price Tag的圖層名為Spring Ad_Price Tag。 具有預設名稱Layer 2的圖層稱為Spring Ad_2。 |
| 锚点 |  | 指定如何在範本中錨定影像，範本是從PSD檔案產生的圖層構成產生的。 依預設，錨點是中心。 無論取代影像的外觀比例為何，置中錨點都可讓取代影像以最佳方式填滿相同的空間。 以不同外觀取代此影像的影像，在參照範本並使用引數替代時，實際上會佔據相同的空間。 如果您的應用程式需要取代影像來填滿範本中配置的空間，請變更為其他設定。 |

#### 設定PDF上傳選項 {#setting-pdf-upload-options}

上傳PDF檔案時，您可以透過各種方式將其格式化。 您可以裁切頁面、擷取搜尋字詞、輸入每英吋畫素解析度，以及選擇色域。 PDF檔案通常包含裁切邊界、裁切標籤、對齊標籤和其他印表機標籤。 上傳PDF檔案時，您可以從頁面側面裁切這些標籤。

對於新上傳，PDF要考慮用於擷取的最大頁數為5000。 自2022年12月31日起，所有PDF的上限將變更為100頁。 另請參閱 [Dynamic Media限制](/help/assets/limitations.md).

>[!NOTE]
>
>不支援eCatalog [!DNL Experience Manager].

從下列選項中選擇：

| 选项 | 子選項 | 描述 |
|---|---|---|
| 正在处理 | 栅格化 | （預設）撕裂PDF檔案中的頁面，並將向量圖形轉換為點陣圖影像。 如果要建立eCatalog，請選擇此選項。 |
| 提取 | 搜索词 | 從PDF檔案中擷取文字，以便在eCatalog檢視器中依關鍵字搜尋檔案。 |
|  | 链接 | 從PDF檔案中擷取連結，並將其轉換成eCatalog檢視器中使用的影像地圖。 |
| 從多頁PDF自動產生eCatalog |  | 自動從PDF檔案建立eCatalog。 eCatalog是以您上傳的PDF檔案命名。 (只有在您上傳時點陣化PDF檔案時，才可使用此選項。) |
| 解决方法 |  | 決定解析度設定。 此設定會決定PDF檔案中每英吋顯示的畫素數。 預設值為150。 |
| 色彩空间 |  | 選取「色域」選單，並為PDF檔案選擇色域。 大多數PDF檔案都有RGB和CMYK彩色影像。 RGB色域較適合線上檢視。 |
|  | 自动检测 | 保留PDF檔案的色域。 |
|  | 强制渲染为 RGB | 轉換為RGB色域。 |
|  | 强制渲染为 CMYK | 轉換為CMYK色彩空間。 |
|  | 强制渲染为灰度 | 轉換為灰階色彩空間。 |

#### 設定eVideo上傳選項 {#setting-evideo-upload-options}

若要透過從各種視訊預設集進行選擇來轉碼視訊檔案。

| 选项 | 子選項 | 描述 |
|---|---|---|
| 自适应视频 |  | 單一編碼預設集可與任何長寬比搭配使用，建立視訊以傳送至行動裝置、平板電腦和案頭。 使用此預設集編碼的上傳來源視訊會設定為固定高度。 不過，寬度會自動縮放以保留視訊的外觀比例。 <br>最佳實務是使用最適化視訊編碼。 |
| 單一編碼預設集 | 排序編碼預設集 | 選取 **[!UICONTROL 名稱]** 或 **[!UICONTROL 大小]** 如果您想要依名稱或解析度大小對「案頭」、「行動裝置」和「平板電腦」下列出的編碼預設集進行排序。 |
|  | 桌面 | 建立MP4檔案，為桌上型電腦提供串流或漸進式視訊體驗。 選取一或多個外觀比例，搭配您想要的解析度大小和目標資料速率。 |
|  | 移动设备 | 建立MP4檔案，以在iPhone或Android™行動裝置上傳送。 選取一或多個外觀比例，搭配您想要的解析度大小和目標資料速率。 |
|  | 平板电脑 | 建立MP4檔案，以在iPad或Android™平板電腦裝置上傳送。 選取一或多個外觀比例，搭配您想要的解析度大小和目標資料速率。 |

#### 在上傳時設定批次集預設集 {#setting-batch-set-presets-at-upload}

如果您想要從上傳的影像自動建立「影像集」或「迴轉集」，請按一下您要使用之預設集的「作用中」欄。 您可以選取多個預設集。

另請參閱 [設定批次集預設集以自動生成影像集和迴轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 以進一步瞭解如何建立批次集預設集。

### 串流上傳 {#streamed-uploads}

如果您上傳許多資產至Adobe Experience Manager，伺服器的I/O請求會大幅增加，進而降低上傳效率，甚至可能導致部分上傳任務逾時。 [!DNL Experience Manager Assets] 支援資產串流上傳。 串流上傳可避免將資產儲存在伺服器上的暫存資料夾中，再複製到存放庫，以減少上傳作業期間的磁碟I/O。 相反地，資料會直接傳輸到存放庫。 如此一來，上傳大型資產的時間以及逾時的可能性就會降低。 串流上傳預設會在以下位置啟用： [!DNL Assets].

>[!NOTE]
>
>已針對在JEE伺服器（servlet-api版本低於3.1）上執行的Adobe Experience Manager停用串流上傳。

### 擷取包含資產的ZIP封存 {#extractzip}

您可以像上傳任何其他支援的資產一樣上傳ZIP封存檔。 相同的檔案名稱規則適用於ZIP檔案。 [!DNL Experience Manager] 可讓您將ZIP封存解壓縮至DAM位置。 如果封存檔案不包含ZIP作為副檔名，請使用內容啟用檔案型別偵測。

一次選取一個ZIP封存，按一下 **[!UICONTROL 擷取封存]**，然後選取目的地資料夾。 選取要處理衝突的選項（如果有）。 如果ZIP檔案中的資產存在於目的地資料夾中，您可以選取以下選項之一：略過擷取、取代現有檔案、透過重新命名來保留兩個資產，或建立版本。

擷取完成後， [!DNL Experience Manager] 會在通知區域通知您。 當 [!DNL Experience Manager] 解壓縮ZIP，您可以在不中斷解壓縮的情況下返回工作。

![ZIP檔案擷取通知](assets/Zip-extraction-notification.png)

此功能的一些限制包括：

* 如果目的地存在同名資料夾，則會將ZIP檔案中的資產解壓縮至現有資料夾。
* 如果取消擷取，則不會刪除已擷取的資產。
* 您無法同時選取兩個ZIP檔案並加以解壓縮。 您一次只能擷取一個ZIP封存。
* 上傳ZIP封存檔時，如果上傳對話方塊顯示500伺服器錯誤，請在安裝後重試 [最新Service Pack](/help/release-notes/release-notes.md).

## 预览资源 {#previewing-assets}

若要預覽資產，請依照下列步驟操作。

1. 從 [!DNL Assets] 使用者介面，導覽至您要預覽的資產位置。
1. 按一下所需的資產，以便開啟。

1. 在預覽模式中，縮放選項可用於 [支援的影像型別](/help/assets/assets-formats.md#supported-raster-image-formats) （使用互動式編輯）。

   若要放大資產，請按一下 `+` （或按一下資產上的放大鏡）。 若要縮小，請按一下 `-`. 放大時，您可以透過平移仔細檢視影像的任何區域。 重設縮放箭頭會將您帶回原始檢視。 若要將檢視重設為原始大小，請按一下 **[!UICONTROL 重設]** ![重設檢視](assets/do-not-localize/revert.png).

**僅使用鍵盤按鍵預覽資產**

若要使用鍵盤預覽資產，請執行下列步驟：

1. 從 [!DNL Assets] 使用者介面，使用導覽至所需的資產 `Tab` 和方向鍵。

1. 按下 `Enter` 鍵，以便開啟。 您可以在預覽模式中放大資產。

1. 放大資產：
   1. 使用 `Tab` 鍵可將焦點移動至放大選項。
   1. 使用 `Enter` 放大影像的按鍵。

   若要縮小顯示，請使用 `Tab` 按鍵將焦點置於縮小選項上，然後按下 `Enter`.

1. 使用 `Shift` + `Tab` 鍵以將焦點移回影像上。

1. 使用方向鍵在縮放的影像周圍移動。

>[!MORELIKETHIS]
>
>* [預覽Dynamic Media資產](/help/assets/previewing-assets.md).
>* [檢視子資產](managing-linked-subassets.md#viewing-subassets).


## 編輯屬性和中繼資料 {#editing-properties}

1. 導覽至您要編輯其中繼資料的資產位置。

1. 選取資產，然後從工具列選取 **[!UICONTROL 屬性]** 以便檢視資產屬性。 或者，選擇 **[!UICONTROL 屬性]** 資產卡上的快速動作。

   ![資產卡片檢視上的屬性快速動作](assets/properties_quickaction.png)

1. 在 [!UICONTROL 屬性] 頁面，編輯各種標籤下的中繼資料屬性。 例如，在 **[!UICONTROL 基本]** 索引標籤中，編輯標題和說明。

   >[!NOTE]
   >
   >「 」的版面 [!UICONTROL 屬性] 頁面和可用的中繼資料屬性取決於基礎中繼資料結構。 若要瞭解如何修改 [!UICONTROL 屬性] 頁面，請參閱 [中繼資料結構](/help/assets/metadata-schemas.md).

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![日期時間選擇器或在「準時」欄位中使用鍵盤鍵，新增資產啟用的日期和時間](assets/datepicker.png)

   *圖：使用日期選擇器來排程資產啟用。*

1. 若要在特定期間後停用資產，請從日期選擇器旁的停用日期/時間 **[!UICONTROL 關閉時間]** 欄位。 停用日期應晚於資產的啟用日期。 晚於 [!UICONTROL 關閉時間]，資產及其轉譯無法透過 [!DNL Assets] 網頁介面或透過HTTP API。

1. 在 **[!UICONTROL 標籤]** 欄位中，選取一或多個標籤。 若要新增自訂標籤，請在方塊中輸入標簽名稱，然後選取 `Enter`. 新標籤儲存在中 [!DNL Experience Manager]. [!DNL YouTube] 需要標籤才能發佈。 另請參閱 [將影片發佈至YouTube](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >若要建立標籤，您需要寫入許可權： `/content/cq:tags/default` 在CRX存放庫中。

1. 若要提供資產評等，請按一下 **[!UICONTROL 進階]** 索引標籤，然後按一下適當位置的星號，以指派所要的評分。

   ![資產屬性中的進階索引標籤以指派評等](assets/ratings.png)

   您指派給資產的評等分數會顯示在 **[!UICONTROL 您的評等]**. 資產從評分過資產的使用者那裡收到的平均評分會顯示在 **[!UICONTROL 評等]**. 此外，對平均評分有貢獻的評分劃分會顯示在 **[!UICONTROL 評等細目]**. 您可以根據平均評分來搜尋資產。

1. 若要檢視資產的使用狀況統計資料，請按一下 **[!UICONTROL 深入分析]** 標籤。

   使用狀況統計資料包括下列專案：

   * 檢視或下載資產的次數
   * 使用資產的管道/裝置
   * 最近使用資產的Creative解決方案

   如需詳細資訊，請參閱 [資產分析](/help/assets/asset-insights.md).

1. 单击“**[!UICONTROL 保存并关闭]**”。
1. 導覽至 [!DNL Assets] 使用者介面。 編輯的中繼資料屬性（包括標題、說明、評等等）會顯示在「卡片」檢視的資產卡片上，以及「清單」檢視的相關欄下。

## 复制资产 {#copying-assets}

當您複製資產或資料夾時，將會複製整個資產或資料夾及其內容結構。 複製的資產或資料夾會複製到目標位置。 來源位置的資產不會變更。

資產特定副本的少數屬性不會結轉。 部分範例包括：

* 資產ID、建立日期和時間，以及版本和版本記錄。 其中一些屬性由屬性指示 `jcr:uuid`， `jcr:created`、和 `cq:name`.

* 每個資產及其每個轉譯的建立時間和參照路徑都是唯一的。

其他屬性和中繼資料資訊會保留。 複製資產時不會建立部分副本。

1. 在 [!DNL Assets] 介面，選取一或多個資產並按一下 **[!UICONTROL 複製]** （從工具列）。 或者，選取 **[!UICONTROL 複製]** ![Assets介面工具列中的複製選項](assets/do-not-localize/copy_icon.png) 從資產卡片快速動作。

   >[!NOTE]
   >
   >如果您使用 [!UICONTROL 複製] 快速動作，您一次只能複製一個資產。

1. 導覽至您要複製資產的位置。

   >[!NOTE]
   >
   >如果您在相同位置複製資產， [!DNL Experience Manager] 會自動產生名稱的變數。 例如，如果您複製標題為 `Square`， [!DNL Experience Manager] 自動為其副本產生標題 `Square1`.

1. 按一下 **[!UICONTROL 貼上]** ![「資產」工具列中的「貼上」選項](assets/do-not-localize/paste.png) 工具列中的asset選項。 然後會將資產複製到此位置。

   >[!NOTE]
   >
   >此 **[!UICONTROL 貼上]** 選項可供工具列使用，直到完成貼上作業為止。

## 移動和重新命名資產 {#moving-or-renaming-assets}

將資產（或資料夾）移動到另一個位置時，資產（或資料夾）不會像複製資產時那樣複製。 資產（或資料夾）會放置在目標位置，並從來源位置中移除。 您也可以將資產移動到新位置時重新命名。
如果您要將已發佈的資產移至其他位置，則可選擇重新發佈資產。 根據預設，已發佈資產上的移動作業會自動取消發佈資產。 如果作者選取「 」，則會重新發佈已移動的資產 [!UICONTROL 重新發佈] 選項。

![您可以在移動已發佈的資產時重新發佈該資產](assets/republish-on-move.png)

若要移動資產或資料夾：

1. 導覽至您要移動的資產位置。

1. 選取資產，然後按一下 **[!UICONTROL 移動]** 工具列中的選項。
   ![「資產」工具列中的「移動」選項](assets/do-not-localize/move.png)

1. 在 [!UICONTROL 移動資產] 精靈，請執行下列任一項作業：

   * 指定資產移動後的名稱。 然後按一下 **[!UICONTROL 下一個]** 以繼續進行。

   * 按一下 **[!UICONTROL 取消]** 以停止程式。
   >[!NOTE]
   >
   >* 如果新位置沒有同名的資產，您可以為該資產指定相同的名稱。 不過，如果您將資產移至有相同名稱的資產存在的位置，則應使用不同的名稱。 如果您使用相同的名稱，系統會自動產生名稱的變數。 例如，如果資產的名稱為Square，則系統會為其副本產生名稱Square1。
   >* 重新命名時，檔案名稱中不允許有空格。


1. 於 **[!UICONTROL 選取目的地]** 對話方塊，請執行下列任一項作業：

   * 導覽至資產的新位置，然後按一下 **[!UICONTROL 下一個]** 以繼續進行。

   * 按一下 **[!UICONTROL 返回]** 以返回 **[!UICONTROL 重新命名]** 畫面。

1. 如果要移動的資產有任何參考頁面、資產或集合，則 **[!UICONTROL 調整引用]** 標籤會出現在 **[!UICONTROL 選取目的地]** 標籤。

   請執行以下任一項作業： **[!UICONTROL 調整引用]** 畫面：

   * 根據新的詳細資料指定要調整的參照，然後按一下 **[!UICONTROL 移動]** 以繼續進行。

   * 從 **[!UICONTROL 調整]** 欄中，選取/取消選取資產的參照。
   * 按一下 **[!UICONTROL 返回]** 以返回 **[!UICONTROL 選取目的地]** 畫面。

   * 按一下 **[!UICONTROL 取消]** 以停止移動作業。

   如果您不更新引用，引用會繼續指向資產的上一個路徑。 如果您調整參照，參照會更新為新的資產路徑。

### 使用拖曳操作移動資產 {#move-using-drag}

您可以將資產（或資料夾）拖曳至目標位置，將其移至同層級資料夾，而非使用 [!UICONTROL 移動] 使用者介面中的選項。 不過，此作業只能在清單檢視中進行。

以拖曳方式移動資產時無法開啟 [!UICONTROL 移動資產] 精靈，因此您無法在移動資產時選擇重新命名資產。 此外，已發佈的資產會在拖曳移動時重新發佈，而不會尋求使用者重新發佈的核准。

![拖曳資產，將資產移至同層級資料夾](assets/move-by-drag.gif)

## 管理轉譯 {#managing-renditions}

1. 您可以新增或移除資產的轉譯，但原始資產除外。 導覽至您要新增或移除轉譯的資產位置。

1. 按一下資產以開啟其頁面。
1. 在Experience Manager介面中，選取 **[!UICONTROL 轉譯]** 從清單中。
1. 在 **[!UICONTROL 轉譯]** 面板，檢視針對資產產生的轉譯清單。

   ![「資產詳細資訊」頁面上的「轉譯」面板](assets/renditions_panel.png)

   >[!NOTE]
   >
   >依預設， [!DNL Assets] 不會在預覽模式下顯示資產的原始轉譯。 如果您是管理員，則可以使用覆蓋圖來設定 [!DNL Assets] 在預覽模式下顯示原始轉譯。

1. 選取轉譯以檢視或刪除轉譯。

   **刪除轉譯**

   從中選擇轉譯 **[!UICONTROL 轉譯]** 面板，然後按一下 **[!UICONTROL 刪除轉譯]** ![刪除轉譯的選項](assets/do-not-localize/deleteoutline.png) 工具列中的選項。 資產處理完成後，無法大量刪除轉譯。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂Experience Manager以刪除特定轉譯或刪除資產，並重新上傳已刪除的資產。

   **上傳新轉譯**

   導覽至資產的資產詳細資訊頁面，然後按一下 **[!UICONTROL 新增轉譯]** ![新增轉譯選項以上傳新轉譯](assets/do-not-localize/add.png) 工具列中的選項，以上傳資產的新轉譯。

   >[!NOTE]
   >
   >如果从&#x200B;**[!UICONTROL “演绎版”]**&#x200B;面板选择演绎版，则工具栏更改上下文并仅显示与该演绎版相关的那些操作。選項，例如 [!UICONTROL 上傳轉譯] 選項不會顯示。 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以設定要在影像或視訊資產的詳細資訊頁面中顯示的轉譯尺寸。 根據您指定的尺寸， [!DNL Assets] 顯示具有精確或最接近維度的轉譯。

   要在资源详细信息级别配置图像的演绎版尺寸，请叠加 `renditionpicker` 节点 (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) 并配置宽度属性的值。設定屬性 **[!UICONTROL 大小（長） (KB)]** 以取代寬度，讓您能夠根據影像大小在資產詳細資料頁面上自訂轉譯。 对于基于大小的自定义，如果匹配的演绎版的大小大于原始演绎版，则属性 `preferOriginal` 将首选项分配给原始演绎版。

   同樣地，您可以透過覆蓋來自訂註釋頁面影像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![覆蓋CRXDE中的renditionpicker節點以自訂註釋頁面影像](assets/renditionpicker-node.png)

   若要設定視訊資產的轉譯維度，請導覽至 `videopicker` CRX存放庫中位於位置的節點 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`，覆蓋節點，然後編輯適當的屬性。

   >[!NOTE]
   >
   >視訊註解僅支援使用HTML5相容視訊格式的瀏覽器。 此外，視瀏覽器而定，支援不同的視訊格式。 不過，視訊註解尚不支援MXF視訊格式。

如需產生和檢視子資產的詳細資訊，請參閱 [管理子資產](managing-linked-subassets.md#generate-subassets).

## 刪除資產 {#deleting-assets}

若要刪除資產，使用者需要刪除許可權： `dam/asset`. 如果您只有修改許可權，則只能編輯資產中繼資料並將註解新增至資產。 不過，您無法刪除資產或其中繼資料。

若要從其他頁面解析或移除傳入參照，請先更新相關參照，然後再刪除資產。 若要禁止使用者刪除參照的資產並留下中斷的連結，請使用覆蓋圖停用強制刪除選項。

若要刪除資產或包含資產的檔案夾：

1. 導覽至您要刪除的資產或資料夾位置。

1. 選取資產或資料夾，然後按一下 **[!UICONTROL 刪除]** ![刪除選項](assets/do-not-localize/deleteoutline.png) （從工具列）。

   確認刪除後：

   * 如果資產沒有參考資料，則會刪除資產。

   * 如果資產有參考資料，則會出現錯誤訊息，通知您 **一個或多個資產被引用**. 您可以選取 **[!UICONTROL 強制刪除]** 或 **[!UICONTROL 取消]**.
   >[!NOTE]
   >
   >* 若要從其他頁面解析或移除傳入參照，請先更新相關參照，然後再刪除資產。 此外，使用覆蓋圖停用強制刪除選項，以禁止使用者刪除參照的資產並留下中斷的連結。
   >* 可以刪除 *資料夾* 包含已取出資產檔案的檔案。 刪除資料夾之前，請確保使用者未簽出任何數位資產。


>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則相關聯的使用者群組也會被刪除。
>
>但是，現有的備援、未使用和自動產生的使用者群組可以使用從存放庫中清除 `clean` 編寫執行個體中JMX的方法(`https://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。

## 下载资源 {#downloading-assets}

另請參閱 [從Experience Manager下載資產](/help/assets/download-assets-from-aem.md).

## 發佈或取消發佈資產 {#publish-assets}

在上傳、處理或編輯您的資產後 [!DNL Experience Manager] 作者，您會將資產發佈至發佈伺服器。 發佈後，資產即可公開發佈。 取消發佈動作會從發佈伺服器移除資產，但不會從製作伺服器移除。

有關特定資訊 [!DNL Dynamic Media]，請參閱 [發佈 [!DNL Dynamic Media] 資產](/help/assets/publishing-dynamicmedia-assets.md).

1. 導覽至您要發佈或要從發佈環境移除（取消發佈）的資產或資產資料夾位置。

1. 選取您要取消發佈的資產或資料夾，然後按一下 **[!UICONTROL 管理發布]** ![管理出版物選項](assets/do-not-localize/globe-publication.png) 工具列中的選項。 或者，若要快速發佈，請選取 **[!UICONTROL 快速發佈]** 工具列中的選項。 如果您要發佈的資料夾包含空白資料夾，則不會發佈空白資料夾。

1. 選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 選項。

   ![取消發佈動作](assets/unpublish_action.png)
   *圖：發佈和取消發佈選項以及排程選項。*

1. 選取 **[!UICONTROL 現在]** 以立即對資產採取行動，或選取 **[!UICONTROL 稍後]** 以排程動作。 如果您選擇 **[!UICONTROL 稍後]** 選項。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 發佈時，如果資產參考其他資產，其參考會列在精靈中。 只會顯示自上次發佈後未發佈或修改的參考。 選擇要發佈的參照。

1. 取消發佈時，如果資產參考其他資產，請選擇您要取消發佈的參考。 单击&#x200B;**[!UICONTROL 取消发布]**。在確認對話方塊中，按一下 **[!UICONTROL 取消]** 以停止動作，或按一下 **[!UICONTROL 取消發佈]** 以確認資產會在指定的日期取消發佈。

瞭解以下與發佈或取消發佈資產或資料夾相關的限制和提示：

* 的選項 [!UICONTROL 管理發布] 僅適用於具有復寫許可權的使用者帳戶。
* 取消發佈複雜資產時，請僅取消發佈資產。 請避免取消發佈引用，因為它們可能會被其他已發佈的資產引用。
* 未發佈空白資料夾。
* 如果您發佈正在處理的資產，只會發佈原始內容。 缺少轉譯。 請等待處理完成，然後在處理完成時發佈或重新發佈資產。

## 已关闭的用户组 {#closed-user-group}

封閉式使用者群組(CUG)可用來限制存取從發佈的特定資產資料夾 [!DNL Experience Manager]. 如果您為資料夾建立CUG，則資料夾（包括資料夾資產和子資料夾）的存取權僅限於指派的成員或群組。 若要存取資料夾，使用者必須使用其安全性認證登入。

CUG是限制資產存取權的額外方式。 您也可以為資料夾設定登入頁面。

1. 從「 」中選取資料夾 [!DNL Assets] 介面，然後按一下 [!UICONTROL 屬性] 工具列中的選項，讓您可以顯示「屬性」頁面。
1. 從 **[!UICONTROL 許可權]** 標籤，新增成員或群組 **[!UICONTROL 已關閉的使用者群組]**.

   ![在已關閉的使用者群組中新增使用者](assets/add_user.png)

1. 若要在使用者存取資料夾時顯示登入畫面，請選取 **[!UICONTROL 啟用]** 選項。 然後，選取登入頁面的路徑 [!DNL Experience Manager]，並儲存變更。

   ![啟用並選取使用者存取資料夾時顯示的登入頁面](assets/login_page.png)

   >[!NOTE]
   >
   >如果您未指定登入頁面的路徑， [!DNL Experience Manager] 會在發佈執行個體中顯示預設登入頁面。

1. 發佈資料夾，然後嘗試從發佈執行個體存取它。 登入畫面隨即顯示。
1. 如果您是CUG成員，請輸入您的安全性認證。 資料夾顯示於 [!DNL Experience Manager] 驗證您的身分。

## 搜索资源 {#assetsearch}

搜尋資產是使用數位資產管理系統的核心。 此功能對創意人員、業務使用者和行銷人員對資產的穩健管理，或DAM管理員的管理都非常重要。

如需簡單、進階和自訂搜尋以探索和使用最適當的資產，請參閱 [在Experience Manager中搜尋資產](search-assets.md).

## 快速操作 {#quick-actions}

快速動作圖示一次只適用於單一資產。 視您的裝置而定，執行下列動作以顯示快速動作圖示：

* 觸控裝置：觸控並按住。 例如，在iPad上，您可以點選並按住資產，以便顯示快速動作。
* 非觸控裝置：游標暫留。 例如，在案頭裝置上，如果您將指標停留在資產縮圖上，則會顯示快速動作列。

### 導覽並選取資產 {#navigating-and-selecting-assets}

您可以使用任何可用檢視（「卡片」、「欄」和「清單」）來檢視、瀏覽和選取資產。 **[!UICONTROL 選取]** 選項。

在清單檢視和欄檢視中， **[!UICONTROL 選取]** 選項會在您將指標停留在資產縮圖上時顯示。

在卡片檢視中， **[!UICONTROL 選取]** 選項會顯示為快速動作。

在中瀏覽資料夾或集合時 [!DNL Assets] 使用者介面中，您可以使用 [!UICONTROL 全選] 選項。 最初，卡片檢視中只會載入100個資產，清單檢視中只會載入200個資產。 捲動搜尋結果頁面時，檢視中會載入更多資產。 此 [!UICONTROL 全選] 選項只會選取載入的資產。

如需詳細資訊，請參閱 [檢視和選取您的資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

## 编辑图像 {#editing-images}

中的編輯工具 [!DNL Assets] 介面可讓您對影像資產執行小型編輯工作。 您可以裁切、旋轉、翻轉及執行影像上的其他編輯工作。 您也可以將影像地圖新增至資產。

>[!NOTE]
>
>對於某些元件，「全熒幕」模式有其他可用選項。

1. 執行下列任一項作業，在編輯模式下開啟資產：

   * 選取資產，然後按一下 **[!UICONTROL 編輯]** （在工具列中）。
   * 按一下 **[!UICONTROL 編輯]** 顯示在卡片檢視中資產上的選項。
   * 按一下 **[!UICONTROL 編輯]** （從工具列） ![工具列中的編輯選項](assets/do-not-localize/edit_icon.png).

1. 若要裁切影像，請按一下 **[!UICONTROL 裁切]** ![裁切影像的選項](assets/do-not-localize/crop.png).

1. 从列表中选择所需的选项。图像上会根据您选择的选项显示裁剪区域。利用&#x200B;**手绘**&#x200B;选项，您可以不受纵横比限制裁剪图像。

1. 選取要裁切的區域，並在影像上調整大小或重新定位。

1. 使用 **[!UICONTROL 還原]** ![復原工具列選項](assets/do-not-localize/undo.png) 和 **[!UICONTROL 取消復原]** ![重做工具列選項](assets/do-not-localize/redo.png) 分別回覆至未裁切影像或保留已裁切影像的選項。
1. 按一下適當的 **[!UICONTROL 旋轉]** 選項可順時針或逆時針旋轉影像。

   ![順時針與逆時針旋轉選項](assets/do-not-localize/rotate-options.png)

1. 按一下適當的 **[!UICONTROL 翻轉]** 選項（如果要水準翻轉影像） ![反映水準選項](assets/do-not-localize/flip-horizontal.png) 或垂直 ![反映垂直選項](assets/do-not-localize/flip-vertical.png).

1. 若要完成影像編輯，請按一下 **[!UICONTROL 完成]** ![完成選項](assets/do-not-localize/check-ok-done-icon.png). 按一下 **完成** 也會開始重新產生轉譯。

>[!NOTE]
>
>BMP、GIF、PNG和JPEG檔案格式支援影像編輯。

您也可以使用影像編輯器新增影像地圖。 如需詳細資訊，請參閱 [新增影像地圖](/help/assets/image-maps.md).

>[!NOTE]
>
>若要編輯TXT檔案，請設定 **Day CQ連結外部化器** 從Configuration Manager。

## 时间线 {#timeline}

時間軸可讓您檢視所選專案的各種事件，例如資產的使用中工作流程、註解/註解、活動記錄及版本。

![排序資產的時間軸專案](assets/sort_timeline.gif)

*圖：排序資產的時間軸專案。*

>[!NOTE]
>
>在 [集合主控台](/help/assets/manage-collections.md#navigating-the-collections-console)，則 **[!UICONTROL 全部顯示]** list提供僅檢視註解和工作流程的選項。 此外，時間軸只會顯示在主控台中列出的頂層集合。 如果您在任何集合內導覽，則不會顯示它。

>[!NOTE]
>
>時間軸包含數個 [內容片段專屬選項](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

## 為資產加上註釋 {#annotating}

註解是新增至影像或影片的評論或說明附註。 註解讓行銷人員能夠共同作業並留下有關資產的意見回饋。

只有具備HTML5相容視訊格式的瀏覽器才支援視訊註解。 符合下列條件的影片格式 [!DNL Assets] 支援情況取決於瀏覽器。 不過，視訊註解尚不支援MXF視訊格式。

>[!NOTE]
>
>對於內容片段， [註解會在片段編輯器中建立](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment).

1. 導覽至您要新增註解的資產位置。
1. 按一下 **[!UICONTROL 註釋]** 選項來自下列其中一項：

   * [快速操作](/help/assets/manage-assets.md#quick-actions)
   * 在選取資產或導覽至資產頁面後，從工具列選取。

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

1. 若要通知使用者註解的相關資訊，請指定使用者的電子郵件地址並新增註解。 例如，若要通知Aaron MacDonald註解的相關資訊，請輸入@aa。 所有相符使用者的提示都會顯示在清單中。 從清單中選取Aaron的電子郵件地址，這樣您就可以用評論標籤人員。 同樣地，您可以在註解內的任何位置或在註解之前或之後標籤更多使用者。

   ![指定使用者的電子郵件地址並新增註解以通知使用者](assets/annotate-gif.gif)

   >[!NOTE]
   >
   >對於非管理員使用者，只有在使用者擁有下列專案的讀取許可權時，才會顯示建議 `/home` CRXDE中的路徑。

1. 新增註釋後，按一下 **[!UICONTROL 新增]** 以儲存。 註解的通知會傳送給Aaron。

   >[!NOTE]
   >
   >儲存註解之前，您可以新增多個註解。

1. 按一下 **[!UICONTROL 關閉]** 退出「註釋」模式。
1. 若要檢視通知，請登入 [!DNL Assets] 使用Aaron MacDonald的認證，然後按一下 **[!UICONTROL 通知]** 選項以檢視通知。

   >[!NOTE]
   >
   >註解也可以新增到視訊資產。 在註解視訊時，播放器會暫停，讓您在影格上註解。 如需詳細資訊，請參閱 [管理視訊資產](/help/assets/managing-video-assets.md). 視訊註解尚不支援MXF視訊格式。

1. 若要選擇不同顏色以便區分使用者，請按一下「設定檔」選項，然後按一下 **[!UICONTROL 我的偏好設定]**.

   ![選取使用者設定檔選項，然後選取我的偏好設定，以開啟使用者偏好設定](assets/User-profile-preferences.png)

   在「 」中指定所要的顏色 **[!UICONTROL 附註顏色]** 方塊，然後按一下 **[!UICONTROL Accept]**.

   ![在「使用者偏好設定」中選取附註顏色以設定「使用者角色」顏色](assets/Annotation-color.png)

>[!NOTE]
>
>您也可以將註解新增至集合。 不過，如果集合包含子集合，您只能將註解/註解新增至父集合。 「註釋」選項不適用於子集合。

### 檢視儲存的註解 {#viewing-saved-annotations}

您一次只能檢視一個註解。

>[!NOTE]
>
>如果您選取多個註解，最新的註解會顯示在使用者介面上。
>
>僅支援將註解資產列印為PDF的多重選取。

**若要檢視為資產儲存的註解：**

1. 前往資產位置並開啟資產頁面。

1. 在Experience Manager介面中，選擇 **[!UICONTROL 時間表]**.
1. 从时间线的&#x200B;**[!UICONTROL 显示全部]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 注释]**&#x200B;以根据注释过滤结果。

   按一下 **[!UICONTROL 時間表]** 面板。

   ![在影像上檢視註解的時間軸面板](assets/timeline-view-annotations.png)

   按一下 **[!UICONTROL 刪除]**，以刪除特定註解。

### 列印註解 {#printing-annotations}

如果資產有註解或受到稽核工作流程的約束，您可以列印資產以及註解和稽核狀態，作為PDF檔案供離線稽核。

您也可以選擇只列印註解或檢閱狀態。

>[!NOTE]
>
>將已附註的資產列印為PDF時，您可以選取多個附註。

若要列印註解及檢閱狀態，請按一下 **[!UICONTROL 列印]** 並依照精靈中的指示操作。 此 **[!UICONTROL 列印]** 選項僅在資產至少獲指派一個註解或稽核狀態時才會出現在工具列中。

1. 從 [!DNL Assets] 介面，開啟資產的預覽頁面。
1. 执行下列操作之一：

   * 若要列印所有附註和稽核狀態，請略過步驟3並直接跳至步驟4。
   * 若要列印特定註解及檢閱狀態，請開啟 [時間表](/help/assets/manage-assets.md#timeline) 然後前往步驟3。

1. 若要列印特定註解，請從時間軸中選取註解。

   ![從時間軸選取註釋以進行列印](assets/timeline-select-annotations.png)

   若要僅列印稽核狀態，請從時間軸中選取它。

1. 按一下 **[!UICONTROL 列印]** （從工具列）。

1. 從「列印」對話方塊中，選擇您希望註釋/審閱狀態顯示在PDF上的位置。 例如，如果您希望註解/狀態列印在包含已列印影像的頁面的右上角，請使用 **左上方** 設定。 預設會選取它。

   您可以根据希望在打印的 PDF 中显示批注/状态的位置选择其他设置。如果希望批注/状态显示在与打印资产不同的页面中，请选择&#x200B;**[!UICONTROL 下一页]**。

1. 按一下 **[!UICONTROL 列印]**. 根据您在步骤 2 中选择的选项，生成的 PDF 会在指定位置显示批注/状态。例如，如果您选择使用&#x200B;**左上角**&#x200B;设置打印批注和审阅状态，则生成的输出将类似于此处描述的 PDF 文件。

   ![已產生PDF的附註和稽核狀態](assets/annotation-status-pdf.png)

1. 下載 ![PDF的下載選項](assets/do-not-localize/download.png) 或列印 ![PDF時列印選項](assets/do-not-localize/print.png) 使用右上角選項的PDF。

   >[!NOTE]
   >
   >如果資產有子資產，您可以列印所有子資產及其特定的頁面註解。

   若要編輯演算PDF檔案的外觀，例如字型顏色、大小和樣式，請開啟 **[!UICONTROL 註解PDF設定]** 從Configuration Manager中，修改所需的選項。 例如，若要變更已核准狀態的顯示顏色，請修改對應欄位中的顏色代碼。 如需有關變更註解字型顏色的資訊，請參閱 [註釋](/help/assets/manage-assets.md#annotating).

   ![在PDF檔案上列印資產附註的設定](assets/annotation-print-pdf-config.png)

   返迴轉譯的PDF檔案並重新整理。 重新整理的PDF會反映您所做的變更。

如果資產包含外文（尤其是非拉丁語言）的註解，您必須先在 [!DNL Experience Manager] 伺服器才能列印這些註解。 設定CQ-DAM-Handler-Gibson Font Manager Service時，提供所需語言字型所在的路徑。

1. 從URL開啟CQ-DAM-Handler-Gibson Font Manager服務設定頁面 `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`.
1. 若要設定CQ-DAM-Handler-Gibson Font Manager服務，請執行下列任一項作業：

   * 在System Fonts目錄選項中，指定系統上字型目錄的完整路徑。 例如，如果您是Mac使用者，您可以將路徑指定為 */Library/Fonts* 在System Fonts目錄選項中。 [!DNL Experience Manager] 會從此目錄中擷取字型。
   * 建立名為的目錄 `fonts` 內部 `crx-quickstart` 資料夾。 CQ-DAM-Handler-Gibson Font Manager Service會自動擷取該位置的字型 `crx-quickstart/fonts`. 您可以從「Adobe伺服器字型」目錄選項中覆寫此預設路徑。

   * 在您的系統中建立字型資料夾，並將所需的字型儲存在資料夾中。 然後，在Customer Fonts目錄選項中指定該資料夾的完整路徑。

1. 從URL存取註解PDF設定 `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`.
1. 使用正確的字型系列設定註釋PDF，如下所示：

   * 包含字串 `<font_family_name_of_custom_font, sans-serif>` 在font-family選項內。 例如，如果您想以中日韓文（中文、日文和韓文）列印註解，請包含字串 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` 在font-family選項中。 如果要以印地語列印註解，請下載適當的字型並將字型系列設定為Arial® Unicode MS®、Noto Sans、Noto Sans CJK JP、Noto Sans Devanagari、sans-serif。

1. 重新啟動 [!DNL Experience Manager] 部署。

以下是如何設定的範例 [!DNL Experience Manager] 若要以中日韓文（中文、日文和韓文）列印註解：

1. 從下列連結下載Google Noto CJK字型，並將其儲存在Font Manager Service中設定的字型目錄中。

   * 全部使用單一Super CJK字型： [https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans （適用於歐洲語言）： [https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 選擇哪種語言時不要使用字型： [https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. 透過將font-family引數設定為來設定註釋PDF檔案 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`. 此設定預設可用，適用於所有歐洲和CJK語言。
1. 如果您選擇的語言與步驟2中提到的語言不同，請將適當的（逗號分隔）專案附加至預設字型系列。

## 建立、管理、預覽和還原資產版本 {#asset-versioning}

版本設定功能會在特定時間點建立數位資產的快照。 版本設定功能有助於以後將資產還原成先前的狀態。 例如，如果您要復原對資產所做的變更，請還原該資產的未編輯版本。 在 [!DNL Experience Manager]，您可以建立版本、檢視目前的修訂版本、檢視兩個影像版本之間的並排差異，以及將資產還原到先前的版本。

您可以在中建立版本 [!DNL Experience Manager] 在下列情況中：

* 上傳具有相同檔案名稱、且位於相同位置的資產。 可以是新資產，也可以是相同資產的修改版本。
* 在中編輯影像 [!DNL Experience Manager] 並儲存變更。
* 編輯資產的中繼資料。
* 使用 [!DNL Experience Manager] 案頭應用程式，以取出現有資產並加以編輯，然後 [上傳您的變更](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets).

您也可以透過工作流程啟用自動版本設定。 當您建立資產的版本時，中繼資料和轉譯會與版本一起儲存。 轉譯會取代相同的影像，例如上傳之JPEG檔案的PNG轉譯。

1. 導覽至您要建立版本的資產位置，然後按一下該資產以開啟其預覽。 從頁面的左上角，開啟功能表，然後選取 **[!UICONTROL 時間表]**.

   ![從左側導覽選單中選取時間軸選項](assets/timeline.png)

   *圖：從頁面的左上角區域開啟功能表並選取 [!UICONTROL 時間表] 選項。*

1. 若要建立資產的版本：

   * 按一下 **[!UICONTROL 動作]** 在底部。
   * 按一下 **[!UICONTROL 另存為版本]** 以便建立資產的版本。 選擇性地新增標籤和註解。
   * 按一下 **[!UICONTROL 建立]** 以建立版本。

      ![從側欄建立資產版本](assets/create-new-version-from-timeline.png)

      *圖：從建立資產的版本 [!UICONTROL 時間表] 左側邊欄。*

1. 若要檢視資產的版本：

   * 按一下 **[!UICONTROL 全部顯示]** 在 [!UICONTROL 時間表].
   * 按一下 **[!UICONTROL 版本]**. 為資產建立的所有版本都會列在左側邊欄。

   * 選取資產的特定版本，然後按一下 **[!UICONTROL 預覽版本]**.

1. 若要回覆成舊版資產，請執行下列動作。 還原後，此版本會顯示在 [!DNL Assets] 介面及可供使用。

   * 按一下資產的版本。 選擇性地新增標籤和註解。
   * 按一下 **[!UICONTROL 還原為此版本]**.

      ![選取版本以還原至該版本](assets/select_version.png)

      *圖：選取一個版本並還原到該版本。 它會成為目前版本，然後可供DAM使用者使用。*

1. 若要比較兩個版本的影像，請遵循下列步驟：
   * 按一下要與目前版本進行比較的版本。
   * 將滑桿拖曳至左側，將此版本重疊至目前版本並加以比較。

   ![使用滑桿來比較資產的所選版本與目前版本](assets/version-slider.gif)

   *圖：使用滑桿輕鬆比較資產的選定版本與目前版本。*

### 在資產上開始工作流程 {#starting-a-workflow-on-an-asset}

若要套用工作流程來處理資產，請參閱 [在資產上開始工作流程](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset).

## 收藏集 {#collections}

集合是一組經過排序的資產。 使用集合可在使用者之間共用相關資產，或將類似資產叢集在一起以便輕鬆探索。

* 集合可以包含來自不同位置的資產，因為它們僅包含對這些資產的引用。 每個集合都會維護資產的參考完整性。
* 您可以與具有不同許可權層級的多個使用者共用集合，包括編輯、檢視等。

若要瞭解集合管理的詳細資訊，請參閱 [管理集合](/help/assets/manage-collections.md).

## 在案頭應用程式中檢視資產或AdobeAsset Link時隱藏過期的資產 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] 案頭應用程式可讓您從Windows或Mac案頭存取DAM存放庫。 AdobeAsset Link允許從受支援記憶體取資產 [!DNL Creative Cloud] 案頭應用程式。

從內瀏覽資產時 [!DNL Experience Manager] 使用者介面中，不會顯示過期的資產。 若要防止在從案頭應用程式和Asset Link瀏覽資產時檢視、搜尋和擷取已到期資產，管理員可以執行下列設定。 此設定適用於所有使用者，無論管理員許可權為何。

執行下列CURL命令。 確定讀取存取權於 `/conf/global/settings/dam/acpapi/` 適用於存取資產的使用者。 屬於的使用者 `dam-user` 預設為群組擁有許可權。

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

若要瞭解更多，請參閱如何 [使用案頭應用程式瀏覽DAM資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 和 [如何使用Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).
