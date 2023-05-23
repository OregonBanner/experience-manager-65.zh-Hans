---
title: 管理视频资源
description: 上傳、預覽、註釋和發佈視訊資產 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# 管理视频资源 {#manage-video-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 本文 |

視訊格式是組織數位資產的重要部分。 [!DNL Adobe Experience Manager] 提供成熟的產品和功能，可管理視訊資產建立後的整個生命週期。

瞭解如何在中管理和編輯視訊資產 [!DNL Adobe Experience Manager Assets]. 視訊編碼和轉碼（例如FFmpeg轉碼）可使用 [!DNL Dynamic Media] 整合。

## 上傳和預覽視訊資產 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 產生擴充功能為MP4之視訊資產的預覽。 如果資產的格式不是MP4，請安裝FFmpeg套件以產生預覽。 FFmpeg會建立OGG和MP4型別的視訊轉譯。 您可以在中預覽轉譯 [!DNL Assets] 使用者介面。

1. 在數位資產資料夾或子資料夾中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請按一下 **[!UICONTROL 建立]** 從工具列中選擇 **[!UICONTROL 檔案]**. 或者，在使用者介面上拖曳檔案。 另請參閱 [上傳資產](manage-assets.md#uploading-assets) 以取得詳細資訊。
1. 若要在「卡片」檢視中預覽視訊，請按一下 **[!UICONTROL 播放]** ![播放選項](assets/do-not-localize/play.png) 視訊資產選項。 您只能在卡片檢視中暫停或播放視訊。 此 [!UICONTROL 播放] 和 [!UICONTROL 暫停] 選項在清單檢視中無法使用。

1. 若要在資產詳細資訊頁面中預覽影片，請按一下 **[!UICONTROL 編輯]** 在卡片上。 視訊會在瀏覽器的原生視訊播放器中播放。 您可以播放、暫停、控制音量，以及將視訊縮放至全熒幕。

   ![視訊播放控制項](assets/video-playback-controls.png)

## 上傳大於2 GB之資產的設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

依預設， [!DNL Assets] 不允許您上傳任何因為檔案大小限制而大於2 GB的資產。 不過，您可以進入CRXDE Lite並在下建立節點來覆寫此限制 `/apps` 目錄。 節點必須具有相同的節點名稱、目錄結構和順序的可比較節點屬性。

除了 [!DNL Assets] 設定，變更以下設定以上傳大型資產：

* 增加權杖到期時間。 另請參閱 [!UICONTROL AdobeGranite CSRF Servlet] 在Web主控台中： `https://[aem_server]:[port]/system/console/configMgr`. 如需詳細資訊，請參閱 [CSRF保護](/help/sites-developing/csrf-protection.md).
* 增加 `receiveTimeout` 在Dispatcher設定中。 如需詳細資訊，請參閱 [Experience ManagerDispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>此 [!DNL Experience Manager] 傳統使用者介面沒有2 GB檔案大小限制。 此外，也不完全支援大型視訊的端對端工作流程。

若要設定較高的檔案大小限制，請在 `/apps` 目錄。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，導覽至 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 若要檢視目錄視窗，請按一下 `>>`.
1. 在工具列中，按一下 **[!UICONTROL 覆蓋節點]**. 或者，从上下文菜单中选择&#x200B;**[!UICONTROL 覆盖节点]**。
1. 在 **[!UICONTROL 覆蓋節點]** 對話方塊，按一下 **[!UICONTROL 確定]**.

   ![覆蓋節點](assets/overlay-node-path.png)

1. 重新整理瀏覽器。 覆蓋節點 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 「 」已選取。
1. 在 **[!UICONTROL 屬性]** 索引標籤中，以位元組為單位輸入適當的值，將大小限制增加到所需的大小。 例如，若要將大小限制增加到30 GB，請輸入 `32212254720` 值。

1. 在工具列中按一下 **[!UICONTROL 全部儲存]**.
1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
1. 於 [!DNL Adobe Experience Manager] [!UICONTROL Web控制檯套裝] 頁面，在表格的「名稱」欄下，找出並按一下 **[!UICONTROL AdobeGranite工作流程外部程式工作處理常式]**.
1. 於 [!UICONTROL AdobeGranite工作流程外部程式工作處理常式] 頁面，為兩者設定秒數 **[!UICONTROL 預設逾時]** 和 **[!UICONTROL 最大逾時]** 欄位至 `18000` （5小時）。 单击“**[!UICONTROL 保存]**”。
1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 在「工作流程模型」頁面上，選擇 **[!UICONTROL Dynamic Media編碼影片]**，然後按一下 **[!UICONTROL 編輯]**.
1. 在工作流程頁面上，按兩下 **[!UICONTROL Dynamic Media視訊服務程式]** 元件。
1. 在[!UICONTROL 步骤属性]对话框的&#x200B;**[!UICONTROL 常用]**&#x200B;选项卡下，展开&#x200B;**高级设置**。
1. 在 **[!UICONTROL 逾時]** 欄位，指定值 `18000`，然後按一下 **[!UICONTROL 確定]** 以返回 **[!UICONTROL Dynamic Media編碼影片]** 工作流程頁面。
1. 靠近頁面頂端、下方的 [!UICONTROL Dynamic Media編碼影片] 頁面標題，按一下 **[!UICONTROL 儲存]**.

## 發佈視訊資產 {#publish-video-assets}

發佈後，您可以將視訊資產以URL形式納入網頁中，或直接內嵌資產。 如需詳細資訊，請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md).

## 將視訊發佈至YouTube {#publishing-videos-to-youtube}

您可以將內部部署Experience Manager視訊資產直接發佈至您先前建立的YouTube頻道。

若要將視訊資產發佈至YouTube，請使用標籤設定Experience Manager Assets。 您可以將這些標籤與YouTube頻道建立關聯。 如果影片資產的標籤符合YouTube頻道的標籤，則影片會發佈至YouTube。 只要使用關聯的標籤，發佈至YouTube就會伴隨著視訊的正常發佈。

YouTube會自行編碼。 因此，上傳至Experience Manager的原始視訊檔案會發佈至YouTube，而不是Dynamic Media的編碼建立的任何視訊轉譯。 雖然您不需要使用Dynamic Media處理影片，但預計他們會在需要檢視器預設集進行播放時這樣做。

當您略過視訊處理設定檔並直接發佈至YouTube時，這僅僅表示您在Experience Manager資產中的視訊資產沒有取得可檢視的縮圖。 這也表示如果您執行 `dynamicmedia` 或 `dynamicmedia_scene7` 執行模式，未編碼的視訊不適用於任何Dynamic Media資產型別。

將視訊資產發佈至YouTube伺服器時，需完成下列工作，以確保使用YouTube進行伺服器對伺服器驗證時安全無虞：

1. [配置Google雲端設定](#configuring-google-cloud-settings)
1. [建立YouTube頻道](#creating-a-youtube-channel)
1. [新增標籤以進行發佈](#adding-tags-for-publishing)
1. [啟用YouTube發佈復寫代理程式](#enabling-the-youtube-publish-replication-agent)
1. [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem)
1. [（可選）自動為您上傳的視訊設定預設YouTube屬性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [將影片發佈至您的YouTube頻道](#publishing-videos-to-your-youtube-channel)
1. [（可選）驗證YouTube上發佈的影片](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [將YouTube URL連結至您的網頁應用程式](#linking-youtube-urls-to-your-web-application)

您也可以 [取消發佈視訊以從YouTube中將其移除](#unpublishing-videos-to-remove-them-from-youtube).

### 配置Google雲端設定 {#configuring-google-cloud-settings}

若要發佈至YouTube，您需要Google帳戶。 如果您有GMAIL帳戶，表示您已擁有Google帳戶；如果您沒有Google帳戶，可以輕鬆建立帳戶。 您需要帳戶，因為您需要憑證才能將視訊資產發佈到YouTube。 如果您已建立帳戶，請略過此任務並直接繼續至 [建立YouTube頻道](#creating-a-youtube-channel).

Google Cloud使用的帳戶和用於YouTube的Google帳戶不需要相同。

Google會定期變更其使用者介面。 因此，將視訊發佈至YouTube的步驟可能會與以下說明稍有不同。 當您嘗試檢查影片是否已上傳到YouTube時，此警告同樣適用。

>[!NOTE]
>
>在撰寫本文時，下列步驟是正確的。 不過，Google會定期更新其網站，恕不另行通知。 因此，這些步驟可能稍有不同。

若要設定Google Cloud設定：

1. 建立Google帳戶。
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   如果您已有Google帳戶，請跳至下一個步驟。

1. 前往 [https://cloud.google.com/](https://cloud.google.com/).
1. 在Google cloud页面的右上角附近，单击控制 **[!UICONTROL 台]**。

   如有需要， **[!UICONTROL 登入]** 使用您的Google帳戶認證來檢視 **[!UICONTROL 主控台]** 選項。

1. 在「控制面板」頁面的 **[!UICONTROL Google Cloud Platform]**，按一下「專案」下拉式清單以開啟「選取專案」對話方塊。
1. 在「選取專案」對話方塊中，點選 **[!UICONTROL 新增專案]**.

   ![6_5_google帳戶 — 新專案](assets/6_5_googleaccount-newproject.png)

1. 在「新專案」對話方塊的「專案名稱」欄位中，輸入新專案的名稱。

   您的專案ID是以專案名稱為基礎。 因此，請謹慎選擇專案名稱；專案建立後即無法變更。 此外，當您稍後在Experience Manager中設定YouTube時，必須再次輸入相同的專案ID；請考慮將其寫下來。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 執行下列任一項作業：

   * 在您的專案控制面板上，在「快速入門」卡片中，點選「 」 **[!UICONTROL 探索及啟用API]**.
   * 在您的專案的「控制面板」上，在API卡片中，點選 **[!UICONTROL 前往API概述]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. 在「API和服務」頁面頂端附近，點選 **[!UICONTROL 啟用API和服務]**.
1. 在「API程式庫」頁面的左側下方 **[!UICONTROL 類別]**，點選 **[!UICONTROL YouTube]**. 在頁面右側，點選 **[!UICONTROL YouTube資料API]**.
1. 在YouTube Data API v3頁面上，點選 **[!UICONTROL 啟用]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. 若要使用API，您需要憑證。 如有必要，請按一下 **[!UICONTROL 建立認證]**.

   ![6_5_googleaccount-apis-creategrecredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 於 **[!UICONTROL 新增認證至您的專案]** 第頁，步驟1，執行下列動作：

   * 從 **[!UICONTROL 您使用哪個API？]** 下拉式清單，選取 **[!UICONTROL YouTube Data API v3]**.

   * 從 **[!UICONTROL 您從哪裡呼叫API？]** 下拉式清單，選取 **[!UICONTROL 網頁伺服器（例如node.js、Tomcat）]**

   * 從 **[!UICONTROL 您正在存取哪些資料？]** 下拉式清單，點選 **[!UICONTROL 使用者資料]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 點選 **[!UICONTROL 我需要什麼認證？]**
1. 在&#x200B;**[!UICONTROL 将凭据添加到项目]**&#x200B;页面中步骤 2 的&#x200B;**[!UICONTROL 创建 OAuth 2.0 客户端 ID]** 标题下，根据需要在“名称”字段中输入唯一名称。或者，您也可以使用 Google 指定的默认名称。
1. 在 **[!UICONTROL 授權的JavaScript來源]** 標題，在文字欄位中輸入以下路徑，在路徑中取代您自己的網域和連線埠號碼，然後按下 **[!UICONTROL 輸入]** 若要將路徑新增至清單：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   **注意**：上述路徑範例僅供示範之用。

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 在 **[!UICONTROL 授權的重新導向URI]** 標題，在文字欄位中輸入以下路徑，在路徑中取代您自己的網域和連線埠號碼，然後按下 **[!UICONTROL 輸入]** 若要將路徑新增至清單：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **注意**：上述路徑範例僅供示範之用。

1. 按一下 **[!UICONTROL 建立OAuth使用者端ID]**.
1. 在&#x200B;**[!UICONTROL 向项目添加凭据]**&#x200B;页面的步骤 3 中，在&#x200B;**[!UICONTROL 设置 OAuth 2.0 许可屏幕]**&#x200B;标题下，选择您当前使用的 Gmail 电子邮件地址。

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 在 **[!UICONTROL 向使用者顯示的產品名稱]** 標題，在文字欄位中，輸入您要在同意畫面上顯示的內容。

   當Experience Manager管理員對YouTube進行驗證時，會顯示同意畫面；Experience Manager會聯絡YouTube以取得許可權。

1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 在将凭据添加到项目页面的步骤4中，在“下载凭据 **[!UICONTROL ”标题下]** ，点按 **[!UICONTROL 下载]**。

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 儲存 `client_id.json` 檔案。

   稍後在Adobe Experience Manager中設定YouTube時，您需要此下載的json檔案。

1. 按一下 **[!UICONTROL 完成]**.

   登出您的Google帳戶。 現在建立YouTube頻道。

### 建立YouTube頻道 {#creating-a-youtube-channel}

將影片發佈至YouTube需要您有一或多個管道。 如果您已建立YouTube頻道，您可以略過此任務並前往 [新增標籤以進行發佈](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>請確定您已在YouTube中設定一或多個管道 *早於* 您在「Experience Manager中的YouTube設定」下新增管道(請參閱 [在Experience Manager中設定YouTube](#setting-up-youtube-in-aem) 下)。 如果您無法設定一或多個管道，系統不會警告您管道不存在。 不過，當您新增頻道時，Google驗證仍會發生，但無法選擇傳送視訊的頻道。

**若要建立YouTube頻道：**

1. 前往 [https://www.youtube.com](https://www.youtube.com/) 並使用您的Google帳戶憑證登入。
1. 在YouTube頁面的右上角，按一下您的個人資料圖片（也可以顯示為實色圓圈內的字母），然後按一下 **[!UICONTROL YouTube設定]** （圓形齒輪圖示）。
1. 在「概述」頁面的「其他功能」標題下，按一下 **[!UICONTROL 檢視我的所有管道或建立管道]**.
1. 在管道頁面上，按一下 **[!UICONTROL 建立新管道]**.
1. 在「品牌帳戶」頁面的「品牌帳戶名稱」欄位中，輸入您要發佈視訊資產的位置之企業名稱或任何其他管道名稱，然後按一下 **[!UICONTROL 建立]**.

   請記住您在這裡輸入的名稱，因為當您在Experience Manager中設定YouTube時，必須再次輸入此名稱。

1. （選用）如有必要，請新增更多管道。

   現在新增標籤以進行發佈。

### 新增標籤以進行發佈 {#adding-tags-for-publishing}

若要將影片發佈至YouTube，Experience Manager會將標籤與一或多個YouTube管道建立關聯。 若要新增標籤以進行發佈，請參閱 [管理標籤](/help/sites-administering/tags.md).

或者，如果您想在Experience Manager中使用預設標籤，您可以略過此任務並前往 [啟用YouTube發佈復寫代理程式](#enabling-the-youtube-publish-replication-agent).

### 啟用YouTube發佈復寫代理程式 {#enabling-the-youtube-publish-replication-agent}

啟用YouTube發佈復寫代理程式後，如果要測試與Google Cloud帳戶的連線，請點選 **[!UICONTROL 測試連線]**. 瀏覽器標籤會顯示連線結果。 如果您已新增YouTube管道，測試過程中會顯示管道清單。

1. 在Experience Manager的左上角，按一下Experience Manager標誌，然後在左側邊欄中按一下 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** > **[!UICONTROL 作者上的代理]**.
1. 在「作者代理程式」頁面上，按一下 **[!UICONTROL YouTube發佈]**.
1. 在工具列的「設定」右側，按一下 **[!UICONTROL 編輯]**.
1. 選取 **[!UICONTROL 已啟用]** 核取方塊，讓您可以開啟復寫代理。
1. 单击&#x200B;**[!UICONTROL 确定]**。

   現在在Experience Manager中設定YouTube。

### 在Experience Manager中設定YouTube {#setting-up-youtube-in-aem}

從Experience Manager6.4開始，引進了新的觸控使用者介面方法，以在Experience Manager中設定YouTube發佈。 根據您所使用的Experience Manager安裝例項，執行下列任一項作業：

* 若要在6.4之前的Experience Manager中設定YouTube，請參閱 [在6.4之前的Experience Manager中設定YouTube](/help/assets/video.md#setting-up-youtube-in-aem-before).
* 若要在Experience Manager6.4或更新版本中設定YouTube，請參閱 [在Experience Manager6.4和更新版本中設定YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4和更新版本中設定YouTube {#setting-up-youtube-in-aem-and-later}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。
1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，點選 **[!UICONTROL 工具]**（槌子圖示） > **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube發佈設定]**.
1. 點選 **[!UICONTROL 全域]** （請勿選取）。

1. 在全域頁面的右上角附近，點選 **[!UICONTROL 建立]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您已在先前初始設定Google Cloud設定時指定專案ID。
「建立YouTube設定」頁面保持開啟；稍後您將返回。

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用純文字編輯器，開啟您先前在工作中下載並儲存的JSON檔案 [配置Google雲端設定](/help/assets/video.md#configuring-google-cloud-settings).
1. 選取並複製整個JSON文字。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在頁面的右上角附近，點選 **[!UICONTROL 儲存]**.

   現在在Experience Manager中設定YouTube管道。

1. 點選 **[!UICONTROL 新增頻道]**.
1. 在管道名稱欄位中，輸入您在任務中建立的管道名稱 **[!UICONTROL 新增一或多個管道至YouTube]** 較早。

   如有需要，您可以選擇新增說明。

1. 點選 **[!UICONTROL 新增]**.
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID關聯的Google使用者名稱和密碼，以及上述JSON文字。
   * 根據您的帳戶有多少個管道，您會看到兩個或多個專案。 選取頻道。 不要選取電子郵件地址；它不是頻道。
   * 在下一頁，點選 **[!UICONTROL Accept]** 以允許存取此頻道。

1. 點選 **[!UICONTROL 允許]**.

   現在設定標籤以進行發佈。

1. **[!UICONTROL 設定標籤以供發佈]**  — 在「Cloud Services> YouTube」頁面上，點選鉛筆圖示以編輯您要使用的標籤清單。
1. 點選下拉式清單圖示（上下顛倒插入號），以便以Experience Manager顯示可用標籤清單。
1. 點選一或多個標籤，以便新增這些標籤。

   若要刪除您新增的標籤，請選取標籤，然後點選 **[!UICONTROL X]**.

1. 完成新增所需標籤後，點選 **[!UICONTROL 儲存]**.

   現在您可將影片發佈至YouTube頻道。

#### 在6.4之前的Experience Manager中設定YouTube {#setting-up-youtube-in-aem-before}

1. 請確定您以管理員身分登入您的Dynamic Media執行個體。

1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，點選 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在「協力廠商服務」標題下方的YouTube下方，點選 **[!UICONTROL 立即設定]**.
1. 在「建立組態」對話方塊中，在個別欄位中輸入標題（必要）和名稱（選用）。
1. 點選 **[!UICONTROL 建立]**.
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您最初指定專案ID時 [已設定Google雲端設定](/help/assets/video.md#configuring-google-cloud-settings) 較早。
保留「YouTube帳戶設定」對話方塊開啟；您稍後將返回該對話方塊。

1. 使用純文字編輯器，開啟您先前在「設定Google雲端設定」工作中下載並儲存的JSON檔案。
1. 選取並複製整個JSON文字。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 點選 **[!UICONTROL 確定]**.

   現在在Experience Manager中設定YouTube管道。

1. 在&#x200B;**[!UICONTROL 可用渠道]**&#x200B;右侧，点按 **+**（加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如有需要，您可以選擇新增說明。

1. 點選 **[!UICONTROL 確定]**.
1. 隨即顯示YouTube/Google驗證。 如果您尚未登入Google Cloud帳戶，請略過此步驟。

   * 輸入與Google專案ID關聯的Google使用者名稱和密碼，以及上述JSON文字。
   * 根據您的帳戶有多少個管道，您會看到兩個或多個專案。 選取頻道。 不要選取電子郵件地址；它不是頻道。
   * 在下一頁，點選 **[!UICONTROL Accept]** 以允許存取此頻道。

1. 點選 **[!UICONTROL 允許]**.

   現在設定標籤以進行發佈。

1. **[!UICONTROL 設定標籤以供發佈]**  — 在「Cloud Services> YouTube」頁面上，點選鉛筆圖示以編輯您要使用的標籤清單。
1. 點選下拉式清單圖示（上下顛倒插入號），以便以Experience Manager顯示可用標籤清單。
1. 點選一或多個標籤，以便新增這些標籤。

   若要刪除您新增的標籤，請選取標籤，然後點選 **X**.

1. 完成新增所需標籤後，點選 **[!UICONTROL 確定]**.

   現在您可將影片發佈至YouTube頻道。

### （可選）自動為您上傳的視訊設定預設YouTube屬性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以選擇在Experience Manager中建立中繼資料處理設定檔，在上傳視訊時自動設定YouTube屬性。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然後，您可以新增這些值，以建立您的YouTube視訊中繼資料處理設定檔。

若要自動為您上傳的視訊設定預設YouTube屬性：

1. 在左上角，點選Experience Manager標誌，然後在左側導軌中，按一下 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料結構]**.
1. 按一下 **[!UICONTROL 預設]**. （請勿在「預設」左側的選取方塊中新增核取記號。）
1. 於 **[!UICONTROL 預設]** 頁面，勾選左側的方塊 **[!UICONTROL 視訊]**，然後點選 **[!UICONTROL 編輯]**.
1. 在「中繼資料結構編輯器」頁面上，點選 **[!UICONTROL 進階]** 標籤。
1. 在“YouTube 发布”标题下，单击 **[!UICONTROL YouTube 类别]**。
1. 在頁面右側的 **[!UICONTROL 設定]** 索引標籤中，執行下列動作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

   * 下 **[!UICONTROL 選擇]**，選取並複製您要使用的預設值（例如People &amp; Blogs或Science &amp; Technology）。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

1. 在「YouTube發佈」標題下，點選 **[!UICONTROL YouTube隱私權]**.
1. 在頁面右側的 **[!UICONTROL 設定]** 索引標籤中，執行下列動作：

   * 在 **[!UICONTROL 對應至屬性]** 文字欄位，選取並複製值。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

   * 下 **[!UICONTROL 選擇]**，選取並複製您要使用的預設值。 請注意，「選擇」會分成兩組。 配對中的底部欄位是您要複製的預設值，例如public、unlisted或private。
將複製的值貼到開啟的文字編輯器中。 稍後當您建立中繼資料處理設定檔時，將需要此值。 讓文字編輯器保持開啟。

1. 在「中繼資料結構編輯器」頁面的右上角附近，按一下 **[!UICONTROL 取消]**.
1. 在Experience Manager的左上角，點選Experience Manager標誌，然後在左側導軌中，按一下 **[!UICONTROL 工具]** （槌子圖示） > **[!UICONTROL 資產]** > **[!UICONTROL 中繼資料設定檔]**.

1. 在「中繼資料描述檔」頁面的右上角，按一下 **[!UICONTROL 建立]**.
1. 在“添加元数据配置文件”对话框的&#x200B;**[!UICONTROL 配置文件]**&#x200B;文本字段中，输入名称 `YouTube Video`，然后单击&#x200B;**[!UICONTROL 创建]**。
1. 在「中繼資料設定檔編輯器」頁面上，按一下 **[!UICONTROL 前進]** 標籤。
1. 執行下列動作，將複製的YouTube發佈值新增至設定檔：

   * 在頁面的右側，按一下 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 區段標題]** 左側，並將它放置在表單區域中。
   * （可選）按一下 **[!UICONTROL 欄位標籤]** 以選取元件。
   * （可選）在頁面右側的「設定」標籤下方，在「欄位標籤」文字欄位中輸入 `YouTube Publishing`.
   * 按一下 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為 **[!UICONTROL 多值文字]** 並將它拖放到 **[!UICONTROL YouTube發佈]** 您建立的標題。

   * 按一下 **[!UICONTROL 欄位標籤]** 因此會選取元件。
   * 在頁面的右側，在「設定」標籤下方，將您先前複製的「YouTube發佈」值（「欄位標籤」值和「對應至屬性值」）貼到表單上各自的欄位中。 將「選擇」值貼到「預設值」欄位中。

1. 執行下列動作，將複製的YouTube隱私權值新增至設定檔：

   * 在頁面的右側，按一下 **[!UICONTROL 建置表單]** 標籤。
   * （可選）拖曳標示為 **[!UICONTROL 區段標題]** 左側，並將它放置在表單區域中。
   * （可選）按一下 **[!UICONTROL 欄位標籤]** 以選取元件。
   * （可選）在頁面右側的「設定」標籤下方，在「欄位標籤」文字欄位中輸入 `YouTube Privacy`.
   * 按一下 **[!UICONTROL 建置表單]** 標籤，然後拖曳標示為 **[!UICONTROL 多值文字]** 並將它拖放到 **[!UICONTROL YouTube隱私權]** 您建立的標題。

   * 按一下 **[!UICONTROL 欄位標籤]** 因此會選取元件。
   * 在頁面的右側，在「設定」標籤下方，將您先前複製的「YouTube發佈」值（「欄位標籤」值和「對應至屬性值」）貼到表單上各自的欄位中。 將「選擇」值貼到「預設值」欄位中。

1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 保存]**。
1. 將YouTube發佈中繼資料設定檔套用至您要上傳影片的資料夾。 您必須同時設定中繼資料設定檔和視訊設定檔。

   请参阅 [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles) 和视 [频配置文件](/help/assets/video-profiles.md)。

### 將影片發佈至您的YouTube頻道 {#publishing-videos-to-your-youtube-channel}

現在，您可將先前新增的標籤與影片資產建立關聯。 此程式可讓Experience Manager知道要將哪些資產發佈至您的YouTube頻道。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下執行時，不會立即發佈自動發佈至YouTube。 設定Dynamic Media - Scene7模式時，有兩個發佈選項可供選擇： **[!UICONTROL 立即]** 或 **[!UICONTROL 啟動時]**.
>
>**[!UICONTROL 立即發佈]** 這表示上傳的資產（與IPS同步後）會自動發佈至傳送系統。 雖然這對Dynamic Media來說是真的，但對YouTube不是這樣。 若要發佈至YouTube，您必須透過Experience Manager Author發佈。

>[!NOTE]
>
>若要從YouTube發佈內容，Experience Manager會使用 **[!UICONTROL 發佈至YouTube]** 工作流程，可讓您監視進度並檢視任何失敗資訊。
>
>另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>如需詳細進度資訊，您可以監視復寫下的YouTube記錄。 但是，請注意，此類監視需要管理員存取權。

**若要將視訊發佈至您的YouTube頻道：**

1. 在Experience Manager中，導覽至您要發佈至YouTube頻道的視訊資產。
1. 選取視訊資產（最適化視訊集）。
1. 在工具列上，按一下 **[!UICONTROL 屬性]**.
1. 在基本索引標籤的中繼資料標題下方，按一下 **[!UICONTROL 開啟選取範圍對話方塊]** 標籤欄位右側。
1. 在「選取標籤」頁面上，導覽至您要使用的標籤，然後選取一或多個標籤。

   請記住，標籤必須與YouTube管道相關聯。

1. 在頁面的右上角，按一下 **[!UICONTROL 選取]**.
1. 在視訊屬性頁面的右上角，按一下 **[!UICONTROL 儲存並關閉]**.
1. 在工具列上，按一下 **[!UICONTROL 快速發佈]**.

   另請參閱 [搭配Experience Manager Sites使用發佈管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   您可以選擇在YouTube頻道上驗證發佈的影片。

### （可選）驗證YouTube上發佈的影片 {#optional-verifying-the-published-video-on-youtube}

您可以選擇監視YouTube發佈（或取消發佈）的進度。

另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

發佈時間會因多項因素而有很大的差異，包括主要來源視訊格式、檔案大小和上傳流量。 發佈程式可能需要幾分鐘到幾小時的時間。 此外，更高解析度的格式呈現得也慢得多。 例如，720p和1080p的出現時間會比480p長。

8小時後，如果您仍然看到顯示以下訊息的狀態訊息 **[!UICONTROL 已上傳（正在處理，請稍候）]**，請嘗試從Adobe的網站移除視訊並重新上傳。

### 將YouTube URL連結至您的網頁應用程式 {#linking-youtube-urls-to-your-web-application}

您可以取得Dynamic Media在發佈影片後產生的YouTube URL字串。 當您複製YouTube URL時，它會貼到剪貼簿，以便您視需要將其貼到網站或應用程式中的頁面。

>[!NOTE]
>
>您必須先將視訊資產發佈至YouTube，才能複製YouTube URL。

**若要將YouTube URL連結至您的Web應用程式：**

1. 導覽至 *YouTube已發佈* 您要複製其URL的視訊資產，然後選取它。

   請記住，YouTube URL僅供複製 *晚於* 您有 *已發佈* 將影片資產轉移到YouTube。

1. 在工具列上，按一下 **[!UICONTROL 屬性]**.
1. 按一下 **[!UICONTROL 進階]** 標籤。
1. 在「YouTube發佈」標題下方的「YouTube URL清單」中，選取URL文字，然後複製URL文字至網頁瀏覽器，以預覽資產或新增至網頁內容頁面。

### 取消發佈影片，以便從YouTube中將其移除 {#unpublishing-videos-to-remove-them-from-youtube}

當您在Experience Manager中取消發佈視訊資產時，該視訊會從YouTube中移除。

>[!CAUTION]
>
>如果您直接從YouTube中移除視訊，Experience Manager不會察覺，並會繼續採取行動，彷彿視訊仍發佈至YouTube。 一律透過Experience Manager從YouTube取消發佈視訊資產。

>[!NOTE]
>
>若要從YouTube移除內容，Experience Manager會使用 **[!UICONTROL 從YouTube取消發佈]** 工作流程，可讓您監視進度並檢視任何失敗資訊。
>
>另請參閱 [監視視訊編碼和YouTube發佈進度](#monitoring-video-encoding-and-youtube-publishing-progress).

**若要取消發佈視訊以從YouTube中將其移除：**

1. 導覽至您要從YouTube頻道取消發佈的視訊資產。
1. 在資產選擇模式中，選取一或多個已發佈的視訊資產。
1. 在工具列上，按一下 **[!UICONTROL 管理發布]**. 點選三點圖示(...) 在工具列上，因此 **[!UICONTROL 管理發布]** 隨即開啟。
1. 在管理出版物頁面上，點選 **[!UICONTROL 取消發佈]**.
1. 在頁面的右上角，點選 **[!UICONTROL 下一個]**.
1. 在頁面的右上角，點選 **[!UICONTROL 取消發佈]**.

## 監視視訊編碼和YouTube發佈進度 {#monitoring-video-encoding-and-youtube-publishing-progress}

當您將新視訊上傳至已套用視訊編碼的資料夾，或將視訊發佈至YouTube時，您可以監視視訊編碼/Youtube發佈的進度。 實際的YouTube發佈進度只能透過記錄檔取得。 不過，失敗或成功會以其他方式列出，如下列程式所述。 此外，當YouTube發佈工作流程或視訊編碼完成或中斷時，您會收到電子郵件通知。

### 監視進度 {#monitoring-progress}

1. 在資產資料夾中檢視視訊編碼進度：

   * 在卡片檢視中，視訊編碼進度會依百分比顯示在資產上。 如果出現錯誤，資產上也會顯示此資訊。

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 在清單檢視中，視訊編碼進度會顯示在 **[!UICONTROL 處理狀態]** 欄。 如果出现错误，则同一列中将显示此消息。

   ![chlimage_1-430](assets/chlimage_1-430.png)

   默认情况下，此列不显示。要启用该列，请从视图下拉菜单中选择&#x200B;**[!UICONTROL 查看设置]**，然后添加&#x200B;**[!UICONTROL 处理状态]**&#x200B;列，然后点按或单击&#x200B;**[!UICONTROL 更新]**。

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 在資產詳細資訊中檢視進度。 點選或按一下資產時，請開啟下拉式功能表並選取 **[!UICONTROL 時間表]**. 若要將其縮小至編碼或YouTube發佈等工作流程活動，請選取「 」 **[!UICONTROL 工作流程]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   任何工作流程資訊（例如編碼）都會顯示在時間軸中。 對於YouTube發佈，工作流程時間軸也包含YouTube頻道名稱和YouTube影片URL。 此外，發佈完成後，您會在工作流程時間軸中看到任何失敗通知。

   >[!NOTE]
   >
   >由於上的多個工作流程設定，最終記錄失敗/錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >    * Apache Sling工作佇列設定
   >    * AdobeGranite工作流程外部程式工作處理常式
   >    * Granite工作流程逾時佇列

   >
   >您可以調整 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 這些設定中的屬性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   >您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   選取執行個體並點選 **[!UICONTROL 開啟歷史記錄]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   您也可以從「工作流程例證」區域暫停、終止或重新命名工作流程。 另請參閱 [管理工作流程](/help/sites-administering/workflows-administering.md) 以取得詳細資訊。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   >
   >您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由於上的多個工作流程設定，最終記錄錯誤訊息可能需要很長時間 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 從 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >
   >
   >    * Apache Sling工作佇列設定
   >    * AdobeGranite工作流程外部程式工作處理常式
   >    * Granite工作流程逾時佇列

   >
   >
   >您可以調整 **[!UICONTROL 重試]**， **[!UICONTROL 重試延遲]**、和 **[!UICONTROL 逾時]** 這些設定中的屬性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   >
   >您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 您會收到有關已中止或失敗的工作流程作業的電子郵件通知。 管理員可設定這些電子郵件通知。 另請參閱 [設定電子郵件通知](#configuring-e-mail-notifications).

#### 設定電子郵件通知 {#configuring-e-mail-notifications}

>[!NOTE]
>
>您需要管理許可權才能存取 **[!UICONTROL 工具]** 功能表。

通知的設定方式取決於您是要接收編碼作業還是YouTube發佈作業的通知：

* 對於編碼工作，您可以存取所有Experience Manager工作流程電子郵件通知的設定頁面： **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]** 並透過搜尋 **[!UICONTROL Day CQ工作流程電子郵件通知服務]**. 另請參閱 [在Experience Manager中設定電子郵件通知](/help/sites-administering/notification.md). 您可以選取或清除核取方塊 **[!UICONTROL 中止時通知]** 或 **[!UICONTROL 完成時通知]** 因此，

* 若為YouTube發佈工作，請執行以下作業：

1. 在Experience Manager中，點選 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 在「工作流程模型」頁面上，選擇 **[!UICONTROL 發佈至YouTube]**，然後點選 **[!UICONTROL 編輯]** （在工具列上）。
1. 在「發佈至YouTube」工作流程頁面的右上角附近，點選 **[!UICONTROL 編輯]**.
1. 將滑鼠指標暫留在YouTube上傳元件上，然後點選一次以顯示內嵌工具列。

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 在內嵌工具列上，點選「設定」圖示（扳手）。 按一下 **[!UICONTROL 引數]** 標籤。

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. 在「YouTube上傳程式 — 步驟屬性」對話方塊中，點選 **[!UICONTROL 引數]** 標籤。

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 您可以選取或清除下列核取方塊：

   * 发布开始
   * 发布失败
   * 發佈完成 — 包含頻道和URL的相關資訊

   清除核取方塊表示您不會從YouTube發佈工作流程收到指定的電子郵件通知。

   >[!NOTE]
   >
   >這些電子郵件是YouTube專屬的，並且是一般工作流程電子郵件通知的補充。 因此，您可以收到兩套電子郵件通知 — 中提供的通用通知 **[!UICONTROL Day CQ工作流程電子郵件通知服務]** 以及特定於YouTube的一個專案，端視您的組態設定而定。

1. 完成後，在對話方塊的右上角附近，點選 **[!UICONTROL 完成]** 圖示（勾號）。
1. 在「發佈至YouTube」工作流程頁面的右上角，點選 **[!UICONTROL 同步]**.

## 為視訊資產加上註釋 {#annotate-video-assets}

1. 從 [!DNL Assets] 主控台，選取 **[!UICONTROL 編輯]** 以顯示「資產詳細資訊」頁面。
1. 若要播放視訊，請按一下 **[!UICONTROL 預覽]**.
1. 若要為視訊加上註釋，請按一下 **[!UICONTROL 註釋]**. 註解會在視訊中的特定時間（影格）新增。 在註釋時，您可以在畫布上繪圖，並在繪圖中包含註解。 註解會自動儲存。 若要結束註解精靈，請按一下 **[!UICONTROL 關閉]**.

   ![在視訊影格上繪製和註釋](assets/annotate-video.png)

1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。

   ![搜尋視訊中的時間，以略過指定的秒數](assets/seek-in-video.png)

1. 若要在時間軸中檢視它，請按一下註釋。 若要從時間軸刪除註釋，請按一下 **[!UICONTROL 刪除]**.

   ![在時間軸中檢視註解和詳細資訊](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中管理數位資產](/help/assets/manage-assets.md)
>* [在Experience Manager Assets中管理集合](/help/assets/manage-collections.md)
>* [Dynamic Media影片檔案](/help/assets/video.md).

