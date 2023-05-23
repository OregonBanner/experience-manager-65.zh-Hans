---
title: 視訊設定檔
description: Dynamic Media已隨附預先定義的最適化視訊編碼設定檔。 此現成可用設定檔中的設定已最佳化，讓您的客戶獲得最佳檢視體驗。 您也可以將智慧型裁切新增至視訊。
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: Video Profiles
role: User, Admin
mini-toc-levels: 3
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '3736'
ht-degree: 8%

---

# 視訊設定檔 {#video-profiles}

Dynamic Media已隨附預先定義的最適化視訊編碼設定檔。 此現成可用設定檔中的設定已最佳化，讓您的客戶獲得最佳檢視體驗。 當您使用最適化視訊編碼設定檔編碼您的主要來源視訊時，在播放視訊期間，視訊播放器會根據客戶的網際網路連線速度自動調整視訊資料流的品質。 此功能稱為最適化位元速率串流。

以下是決定視訊品質的其他因素：

* **已上傳主要來源視訊的解析度**

   如果MP4視訊是以較低解析度（例如240p或360p）錄製，則無法以高解析度進行串流。

* **視訊播放器大小**

   根據預設，最適化視訊編碼設定檔中的「寬度」會設為「自動」。 同樣地，在播放期間，系統會根據播放器的大小使用最佳品質。

另請參閱 [視訊編碼的最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

另請參閱 [組織數位資產以使用處理設定檔的最佳實務](/help/assets/organize-assets.md).

>[!NOTE]
>
>若要產生視訊的中繼資料和相關的視訊影像縮圖，視訊本身必須經過Dynamic Media中的編碼程式。 在Adobe Experience Manager中， **[!UICONTROL Dynamic Media編碼影片]** 如果您已啟用Dynamic Media並設定視訊雲端服務，工作流程會對視訊進行編碼。 此工作流会捕获工作流进程历史记录和失败信息。另請參閱 [監視視訊編碼和YouTube發佈進度](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已啟用Dynamic Media並設定視訊雲端服務， **[!UICONTROL Dynamic Media編碼影片]** 上傳視訊時，工作流程會自動生效。 (如果您沒有使用Dynamic Media，請 **[!UICONTROL DAM更新資產]** 工作流程會生效。)
>
>中繼資料在搜尋資產時相當實用。 縮圖是在編碼期間產生的靜態視訊影像。 Experience Manager系統需要這些視訊，並用於使用者介面，以協助您在「卡片」檢視、「搜尋結果」檢視和「資產清單」檢視中以視覺化方式識別影片。 當您選取已編碼視訊的「轉譯」圖示（上色調色盤）時，可以看到產生的縮圖。

當您完成視訊描述檔的建立後，可將其套用至一個或多個資料夾。 另請參閱 [將視訊設定檔套用至資料夾](#applying-a-video-profile-to-folders).

若要定義其他資產型態的進階處理引數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

另請參閱 [用於處理中繼資料、影像和影片的設定檔](processing-profiles.md).

## 最適化視訊編碼預設集 {#adaptive-video-encoding-presets}

下表列出將最適化視訊串流傳送到行動裝置、平板電腦裝置和桌上型電腦的最佳實務編碼設定檔。 您可以將這些預設集用於任何長寬比視訊。

<table>
 <tbody>
  <tr>
   <td><strong>视频格式编解码器</strong></td>
   <td><strong>視訊大小 — 寬度(px)</strong></td>
   <td><strong>視訊大小 — 高度(px)</strong></td>
   <td><strong>保持外觀比例？</strong></td>
   <td><strong>視訊位元速率(Kbps)</strong></td>
   <td><strong>視訊影格速率(Fps)</strong></td>
   <td><strong>音频编解码器</strong></td>
   <td><strong>音訊位元速率(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>是</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>是</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>是</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## 關於在視訊設定檔中使用智慧型裁切 {#about-smart-crop-video}

視訊智慧型裁切 — 「視訊描述檔」提供的選用功能 — 是運用Adobe Sensei中人工智慧的強大功能。 它會自動偵測並裁切您上傳的任何最適化視訊或漸進式視訊中的焦點，而不論其大小為何。

支援的智慧型裁切視訊格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智慧型裁切支援的視訊檔案大小上限如下：

* 持續五分鐘。
* 每秒30個畫面(FPS)。
* 300-MB檔案大小。

Adobe Sensei限製為9000個畫面。 也就是說，30 FPS時需要5分鐘。 如果您的視訊具有較高的FPS，則支援的視訊持續時間上限會縮短。 例如，60 FPS視訊必須長達兩分鐘半，Adobe Sensei和智慧型裁切才能支援。

![視訊智慧型裁切](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>若要讓視訊智慧型裁切發揮作用，您必須在視訊設定檔中加入一或多個視訊編碼預設集。

若要針對視訊使用智慧型裁切，請建立最適化或漸進式視訊編碼設定檔。 在您的個人資料中，使用 **[!UICONTROL 智慧型裁切比例]** 工具來選取預先定義的外觀比例。 例如，定義視訊編碼預設集後，您可以新增外觀比例為16x9的「行動橫向」定義，以及外觀比例為9x16的「行動縱向」定義。 您可以選取的其他外觀或裁切比例包括1x1、4x3和4x5。

![使用智慧型裁切編輯視訊編碼設定檔](assets/edit-smart-crop-video2.png)

您可以使用最右側的滑桿，將視訊描述檔中的視訊智慧型裁切切換為開啟或關閉 **[!UICONTROL 智慧型裁切比例]** 在使用者介面中。

建立並儲存視訊設定檔後，您可以將其套用至您想要的資料夾。

另請參閱 [將視訊設定檔套用至特定資料夾](#applying-video-profiles-to-specific-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

另請參閱 [影像的智慧型裁切](image-profiles.md).

## 建立最適化位元速率串流的視訊設定檔 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media已隨附預先定義的最適化視訊編碼設定檔（MP4 H.264的一組視訊上傳設定），此設定檔已最佳化以發揮最佳檢視體驗。 您可以在上傳視訊時使用此設定檔。

不過，如果此預先定義的設定檔不符合您的需求，您可以選擇建立自己的最適化視訊編碼設定檔。 當您使用設定時 **[!UICONTROL 最適化串流編碼]**  — 最佳實務是，您新增至設定檔的所有編碼預設集都會經過驗證，以確保所有影片的外觀比例都相同。 此外，經過編碼的視訊會被視為串流的多位元速率集。

當您建立視訊編碼設定檔時，請注意大多數編碼選項都會預先填入建議的預設設定，以協助您。 不過，如果您選取的值不是建議的預設值，可能會導致錄放期間的視訊品質不佳，並出現其他效能問題。

因此，針對設定檔中的所有MP4 H.264視訊編碼預設集，會驗證下列值，以確保在設定檔中的個別編碼預設集中這些值相同，從而實現最適化位元速率串流：

* 視訊格式轉碼器 — MP4 H.264 (.mp4)
* 音频编解码器
* 音频比特率
* 保持外觀比例
* 兩次編碼
* 恒定比特率
* H264 配置文件
* 音频采样速率

如果值不同，您可以繼續按原樣建立設定檔。 不過，無法進行最適化位元速率串流。 相反地，使用者會體驗單一位元速率串流。 建議您編輯編碼設定，以在設定檔的個別編碼預設集中使用相同的值。 (視訊設定檔/預設集編輯器會在下列情況下強制執行最適化視訊編碼設定的同位檢查： **[!UICONTROL 最適化串流編碼]** 已啟用。)

另請參閱 [建立漸進式串流的視訊編碼設定檔](#creating-a-video-encoding-profile-for-progressive-streaming).

另請參閱 [視訊編碼的最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產型態的進階處理引數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**若要建立最適化位元速率串流的視訊設定檔**，

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取 **[!UICONTROL 建立]** 以新增視訊設定檔。

1. 輸入設定檔的名稱和描述。
1. 在「建立/編輯視訊編碼預設集」頁面上，選取 **[!UICONTROL 新增視訊編碼預設集]**.
1. 於 **[!UICONTROL 基本]** 索引標籤中，設定視訊和音訊選項。
選取每個選項旁的資訊圖示，以取得其他說明或根據選取的視訊格式codec建議的設定。
1. 在「視訊大小」標題下，確認 **[!UICONTROL 保持外觀比例]** 已勾選。
1. 設定視訊影格大小解析度（畫素）。 使用 **[!UICONTROL 自動]** 值會自動縮放以符合來源外觀比例（寬高比）。 例如，Auto x 480或640 x Auto。

1. 执行下列操作之一：

   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**. 在 **[!UICONTROL 高度]** 欄位，輸入畫素值。

   * 若要協助您視覺化視訊的大小，請選取右側的資訊圖示(i) **[!UICONTROL 高度]** 以開啟「大小電腦」頁面。 使用 **[!UICONTROL 大小電腦]** 以設定您想要的視訊尺寸（以藍色方塊表示）。 選取 **[!UICONTROL X]** 完成時位於右上角。

1. （可選）選取 **[!UICONTROL 進階]** 標籤並確保 **[!UICONTROL 使用預設值]** 核取方塊已選取（建議使用）。 或者，修改進階視訊與音訊設定。
1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 以儲存預設集。
1. 执行下列操作之一：
   * 重複步驟4至10，建立其他編碼預設集。 （最適化視訊串流需要多個視訊預設集。）
   * 繼續下一步驟。

1. （可選）若要將視訊智慧型裁切新增至套用此設定檔的視訊，請執行下列動作：
   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，選取「 」 **[!UICONTROL 新增]**.
   * 在「名稱」欄位中，輸入可協助您輕鬆識別裁切率的名稱。
   * 從 **[!UICONTROL 裁切比例]** 下拉式清單，選取您要使用的比例。

1. 执行下列操作之一：

   * 視需要繼續新增裁切比例。
   * 繼續下一步驟。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 以儲存設定檔。

您現在可以將設定檔套用至包含視訊的資料夾。 另請參閱 [將視訊設定檔套用至資料夾](#applying-a-video-profile-to-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

## 建立漸進式串流的視訊設定檔 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您選擇不使用選項 **[!UICONTROL 最適化串流編碼]**，您新增至設定檔的所有編碼預設集都會被視為個別視訊轉譯，以用於單位元速率串流或漸進式視訊傳送。 此外，不会进行验证，以确保所有视频呈现具有相同的纵横比。

根據您執行的模式，支援的視訊格式轉碼器如下：

* Dynamic Media-Scene7模式： H.264 (.mp4)
* Dynamic Media-Hybrid模式： H.264 (.mp4)、WebM

另請參閱 [建立最適化位元速率串流的視訊編碼設定檔](#creating-a-video-encoding-profile-for-adaptive-streaming).

另請參閱 [視訊編碼的最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產型態的進階處理引數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**若要建立漸進式串流的視訊設定檔：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取 **[!UICONTROL 建立]** 以新增視訊設定檔。
1. 輸入設定檔的名稱和描述。
1. 在「建立/編輯視訊編碼預設集」頁面上，選取 **[!UICONTROL 新增視訊編碼預設集]**.
1. 於 **[!UICONTROL 基本]** 索引標籤中，設定視訊和音訊選項。
選取每個選項旁的資訊圖示，以取得其他說明或根據選取的視訊格式codec建議的設定。
1. （選用）在「視訊大小」標題下，取消勾選 **[!UICONTROL 保持外觀比例]**.
1. 执行以下操作：
   * 在 **[!UICONTROL 寬度]** 欄位，輸入 **[!UICONTROL 自動]**.
   * 在 **[!UICONTROL 高度]** 欄位，輸入畫素值。
若要協助您視覺化視訊的大小，請選取「高度」的資訊圖示以開啟 **[!UICONTROL 大小電腦]** 頁面。 使用 **[!UICONTROL 大小電腦]** 頁面，以進一步設定您想要的視訊尺寸（藍方塊）。 完成後，在對話方塊的右上角，選取 **[!UICONTROL X]**.
1. （可選）執行下列任一項作業：

   * 選取 **[!UICONTROL 進階]** 標籤，並確定 **[!UICONTROL 使用預設值]** 核取方塊已選取（建議使用）。

   * 清除 **[!UICONTROL 使用預設值]** 核取方塊，並指定您想要的視訊設定和音訊設定。
選取每個選項旁的資訊圖示，以取得其他說明或根據選取的視訊格式codec建議的設定。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 以儲存預設集。
1. 执行下列操作之一：

   * 重複步驟4-9以建立其他編碼預設集。
   * 繼續下一步驟。

1. （可選）若要將視訊智慧型裁切新增至套用此設定檔的視訊，請執行下列動作：

   * 在「編輯視訊描述檔」頁面的「智慧型裁切比例」標題右側，選取「 」 **[!UICONTROL 新增]**.
   * 在「名稱」欄位中，輸入可協助您輕鬆識別裁切率的名稱。
   * 從 **[!UICONTROL 裁切比例]** 下拉式清單，選取您要使用的比例。

1. 执行下列操作之一：

   * 視需要繼續新增裁切比例。
   * 繼續下一步驟。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]** 以儲存設定檔。

您現在可以將設定檔套用至包含視訊的資料夾。 另請參閱 [將視訊設定檔套用至資料夾](#applying-a-video-profile-to-folders) 或 [全域套用視訊設定檔](#applying-a-video-profile-globally).

## 使用自訂新增的視訊編碼引數 {#using-custom-added-video-encoding-parameters}

您可以編輯現有的視訊編碼設定檔，以利用在Experience Manager中建立或編輯視訊設定檔時，使用者介面中找不到的進階視訊編碼引數。 新增一或多個進階引數（例如minBitrate和maxBitrate ）至您現有的設定檔。

**若要使用自訂新增的視訊編碼引數：**

1. 選取Experience Manager標誌，然後導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 從「CRXDE Lite」頁面，在左側的「總管」面板中導覽至下列專案：

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 在页面右下方的面板中，从“属性”选项卡中，指定要使用的参数的&#x200B;**[!UICONTROL 名称]**、**[!UICONTROL 类型]**&#x200B;和&#x200B;**[!UICONTROL 值]**。

   下列進階引數可供使用：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>描述</strong><br /> </td>
   <td><strong>类型</strong><br /> </td>
   <td><strong>价值</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>用於編碼的H.264層級。 通常，此引數會根據您使用的編碼設定自動決定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264層級</p> <p>例如3.0 = 30， 1.3 = 13)</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>關鍵影格之間的目標影格數。 計算此值，以便每2-10秒產生一個關鍵影格。 例如，以每秒30個影格為例，關鍵影格間隔應該是60-300。<br /> <br /> 較低的關鍵影格間隔可改善最適化視訊編碼的串流搜尋和串流切換行為，也可能改善有大量動作的視訊品質。 不過，由於關鍵影格會增加檔案的大小，因此較低的關鍵影格間隔通常會導致指定位元速率下的整體視訊品質較低。</td>
   <td><code>String</code></td>
   <td><p>正數。</p> <p>預設值為300。</p> <p>DASH或HLS的建議值為60-90。 (若要在視訊中使用DASH，必須先在您的帳戶上啟用它。 另請參閱 <a href="/help/assets/video.md#enable-dash">在您的帳戶上啟用DASH</a>.)</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允許可變位元速率編碼的最小位元速率，以Kbps （每秒千位元）表示。</p> <p>此引數僅適用於以下情況<strong> 使用固定位元速率</strong> 當您建立或編輯視訊編碼設定檔時，會在「進階」標籤中取消選取。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正數（以Kbps為單位）。</p> <p>無預設值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允許可變位元速率編碼的最大位元速率（以Kbps為單位）。</p> <p>此引數僅適用於以下情況<strong> 使用固定位元速率</strong> 當您建立或編輯視訊編碼設定檔時，會在「進階」標籤中取消選取。</p> <p>另請參閱 <a href="/help/assets/video.md#bitrate">位元速率</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>正數（以Kbps為單位）。</p> <p>無預設值。 不過，建議值最多為編碼位元速率的2倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>將值設為 <code>true</code> 強制音訊資料流採用固定的位元速率（若音訊轉碼器支援）。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>預設為 <code>false</code>.</p> <p>建議的DASH或HLS值為 <code>false</code>. (若要在視訊中使用DASH，必須先在您的帳戶上啟用它。 另請參閱 <a href="/help/assets/video.md#enable-dash">在您的帳戶上啟用DASH</a>.)</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在頁面的右下角附近，選取 **[!UICONTROL 新增]**.
1. 执行下列操作之一：

   * 重複步驟3和4，將另一個引數新增至視訊編碼設定檔。
   * 在頁面的左上角附近，選取 **[!UICONTROL 全部儲存]**.

1. 在CRXDE Lite頁面的左上角，選取 **[!UICONTROL 返回首頁]** 圖示以返回Experience Manager。

### 編輯視訊設定檔 {#editing-a-video-encoding-profile}

您可以編輯任何您建立的視訊設定檔，以新增、編輯或刪除該設定檔中的視訊預設集。

依預設，您無法編輯預先定義的現成可用的 **[!UICONTROL 自我調整視訊編碼]** Dynamic Media隨附的設定檔。 反之，您可以輕鬆複製設定檔，並以新名稱儲存。 然後，您可以在複製的設定檔中編輯所需的預設集。

另請參閱 [視訊編碼的最佳作法](/help/assets/video.md#best-practices-for-encoding-videos).

若要定義其他資產型態的進階處理引數，請參閱 [設定資產處理](/help/assets/config-dms7.md#configuring-asset-processing).

**若要編輯視訊設定檔：**

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在「視訊設定檔」頁面上，檢查一個視訊設定檔名稱。
1. 在工具列上，選取 **[!UICONTROL 編輯]**.
1. 在「視訊編碼設定檔」頁面上，視需要編輯名稱和說明。
1. 作為最佳實務，請確保 **[!UICONTROL 最適化位元速率串流的編碼]** 核取方塊已選取。
選取資訊圖示以取得最適化位元速率串流的說明。 （如果您正在編輯漸進式視訊設定檔，請勿選取此核取方塊。）
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除組成設定檔的視訊編碼預設集。

   選取上每個選項旁的資訊圖示 **[!UICONTROL 基本]** 和 **[!UICONTROL 進階]** 索引標籤，以取得其他說明或根據選取的視訊格式codec建議的設定。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

### 複製視訊設定檔 {#copying-a-video-encoding-profile}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在「視訊設定檔」頁面上，檢查一個視訊設定檔名稱。
1. 在工具列上，選取 **[!UICONTROL 複製]**.
1. 在「視訊編碼設定檔」頁面上，輸入設定檔的新名稱。
1. 作为最佳实践，请确保选中“自 **[!UICONTROL 适应流播放的编码]** ”复选框。 選取資訊圖示以取得最適化位元速率串流的說明。 （如果要复制渐进式视频配置文件，请勿选中此复选框。）

   在Dynamic Media — 混合模式中，如果WebM視訊預設集是視訊設定檔的一部分，則 **[!UICONTROL 最適化串流編碼]** 因為所有預設集都必須是MP4，所以無法使用。
1. 在「視訊編碼預設集」標題下，新增、編輯或刪除組成設定檔的視訊編碼預設集。

   選取「基本」和「進階」標籤上每個選項旁的資訊圖示，以取得建議的設定和說明。

1. 在頁面的右上角，選取 **[!UICONTROL 儲存]**.

### 刪除視訊設定檔 {#deleting-a-video-encoding-profile}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 在「視訊設定檔」頁面上，檢查一或多個視訊設定檔名稱。
1. 在工具列上，選取 **[!UICONTROL 刪除]**.
1. 選取 **[!UICONTROL 確定]**.

## 將視訊設定檔套用至資料夾 {#applying-a-video-profile-to-folders}

將視訊設定檔指派給資料夾時，任何子資料夾都會自動從其父資料夾繼承設定檔。 此規則表示您只能將一個視訊設定檔指派給資料夾。 因此，請仔細考慮您上傳、儲存、使用和封存資產的資料夾結構。

如果您將不同的視訊設定檔指派給資料夾，新的設定檔會覆寫先前的設定檔。 先前現有的資料夾資產保持不變。 新設定檔會套用至稍後新增至資料夾的資產。

在使用者介面中，會以卡片名稱中設定檔名稱的外觀來指示已為其指派設定檔的資料夾。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以將視訊設定檔套用至特定資料夾，或全域套用至所有資產。

若資料夾中已有您之後加以變更的現有視訊設定檔，您可以重新處理該資料夾中的資產。 另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

### 將視訊設定檔套用至特定資料夾 {#applying-video-profiles-to-specific-folders}

您可以从“工具”菜单中将视频配置文件应用到 **[!UICONTROL 文件夹]** ，或者如果您在文件夹中，也可以从“属 **[!UICONTROL 性”]**。 本节将介绍这两种将视频配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

#### 透過「設定檔」使用者介面將視訊設定檔套用至資料夾 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取您要套用至一個或多個資料夾的視訊設定檔。
1. 選取 **[!UICONTROL 將設定檔套用至資料夾]** 並選取您要用來接收新上傳資產的資料夾或多個資料夾，然後選取 **[!UICONTROL 套用]**. 在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，如果文件夹已经分配了配置文件，则文件夹名称的正下方会显示配置文件的名称。您可以 [監視視訊設定檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job).

#### 從「屬性」將視訊設定檔套用至資料夾 {#applying-video-profiles-to-folders-from-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** 然後移至您要套用視訊設定檔的資料夾。
1. 在資料夾中，選取核取記號以選取資料夾，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 視訊設定檔]** 標籤並從下拉式選單中選取設定檔，然後選取 **[!UICONTROL 儲存並關閉]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-518](assets/chlimage_1-518.png)
您可以 [監視視訊設定檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job).

### 全域套用視訊設定檔 {#applying-a-video-profile-globally}

除了將設定檔套用至資料夾外，您還可以全域套用設定檔，以便上傳至任何資料夾Experience Manager Assets的任何內容都會套用選取的設定檔。

另請參閱 [編輯資料夾中資產的處理設定檔後，重新處理該資料夾中的資產](processing-profiles.md#reprocessing-assets).

**若要全域套用視訊設定檔：**

* 導覽至CRXDE Lite至下列節點： `/content/dam/jcr:content`. 新增屬性 `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` 並選取 **[!UICONTROL 全部儲存]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 您可以 [監視視訊設定檔處理工作的進度](#monitoring-the-progress-of-an-encoding-job).

## 監視視訊設定檔處理工作的進度 {#monitoring-the-progress-of-an-encoding-job}

系統會顯示處理指示器（或進度列），讓您以視覺化方式監視視訊設定檔處理工作的進度。

您也可以檢視 `error.log` 檔案來監視編碼工作的進度、檢視編碼是否已完成或檢視任何工作錯誤。 此 `error.log` 可在以下位置找到： `logs` 安裝Experience Manager執行個體的資料夾。

## 從資料夾中移除視訊設定檔 {#removing-a-video-profile-from-folders}

當您從資料夾中移除視訊描述檔時，任何子資料夾都會自動繼承其父資料夾中描述檔的移除動作。 不過，在資料夾內發生的任何檔案處理作業都會維持不變。

您可以从“工具”菜单中将视频配置文件从文件夹删除 **** ，如果您在文件夹中，也可以从“文件夹设 **[!UICONTROL 置”中删除]**。 本节将介绍这两种将视频配置文件从文件夹删除的方法。

### 透過「設定檔」使用者介面，從資料夾中移除視訊設定檔 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]**.
1. 選取您要從資料夾或多個資料夾中移除的視訊設定檔。
1. 選取 **[!UICONTROL 從資料夾中移除設定檔]** 並選取您要用來從中移除設定檔的一個或多個資料夾，然後選取 **[!UICONTROL 移除]**.

   您可以確認視訊設定檔不再套用至資料夾，因為資料夾名稱下方不再有該名稱。

### 透過「屬性」從資料夾中移除視訊設定檔 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 選取Experience Manager標誌並導覽至 **[!UICONTROL 資產]** 然後移至您要從中移除視訊設定檔的資料夾。
1. 在資料夾中，選取核取記號，然後選取 **[!UICONTROL 屬性]**.
1. 選取 **[!UICONTROL 視訊設定檔]** 標籤並選取 **[!UICONTROL 無]** 從下拉式選單中選取 **[!UICONTROL 儲存並關閉]**. 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
