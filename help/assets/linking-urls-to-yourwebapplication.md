---
title: 将 URL 关联到您的 Web 应用程序
description: 如何將URL連結至Dynamic Media中的網頁應用程式
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configuration
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 6%

---

# 将 URL 关联到您的 Web 应用程序 {#linking-urls-to-your-web-application}

您的網站和應用程式會透過URL呼叫來存取Dynamic Media服務。 發佈資產後，Dynamic Media會啟動參考該資產的URL字串。 您可以將這些URL貼到網頁瀏覽器以進行測試。

只有當您符合以下條件時，才可連結至URL： *not* 使用Experience Manager做為WCM。 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，會使用連結（而非內嵌）。 如果您使用Experience Manager做為WCM， [您直接在頁面上新增資產](adding-dynamic-media-assets-to-pages.md).

若要將這些URL字串放入您的網頁和應用程式中，請從Dynamic Media複製它們。

>[!NOTE]
>
>URL字串僅適用於資產的動態轉譯。 它們目前不適用於位於DAM而不是Dynamic Media伺服器的靜態資產。 靜態的轉譯不會顯示URL按鈕。

另請參閱 [將視訊或影像檢視器內嵌在網頁上](embed-code.md).

另請參閱 [將YouTube URL連結至您的網頁應用程式](video.md).

另請參閱 [為回應式網站傳送最佳化的影像](responsive-site.md).

另請參閱 [上傳資產](manage-assets.md#uploading-assets).

## 取得資產的URL {#obtaining-a-url-for-an-asset}

您可以取得影像預設集或檢視器預設集產生的URL字串。 在您複製URL後，它會貼到「剪貼簿」，以便您視需要將其貼到網站或應用程式中的頁面。

>[!NOTE]
>
>在您發佈選取的資產後，才能複製URL。 此外，您也必須發佈檢視器預設集或影像預設集。
>
>另請參閱 [發佈資產](publishing-dynamicmedia-assets.md).
>
>另請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).
>
>另請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

有數種不同的方式可以取得URL字串。 不過，下列步驟只顯示一個您可以使用的方法。

**若要取得資產的URL：**

1. 導覽至 *已發佈* 您要複製其影像預設集URL或檢視器預設集URL的資產，然後選取要開啟的資產。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。此外，还必须发布查看器预设或图像预设。

   另請參閱 [發佈資產](publishing-dynamicmedia-assets.md).

   另請參閱 [發佈檢視器預設集](managing-viewer-presets.md#publishing-viewer-presets).

   另請參閱 [發佈影像預設集](managing-image-presets.md#publishing-image-presets).

1. 根據您選取的資產，執行下列任一項作業：

   * 如果您已選取影像，請在下拉式選單中選取 **[!UICONTROL 轉譯]**.

      在 **[!UICONTROL 動態]** 標題中，選取預設集名稱，即可在右側框架中檢視其轉譯。 如有必要，請捲動「轉譯」清單以檢視動態標題。

      在左側邊欄底部，選取 **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * 如果您在下拉式選單中選取了迴轉集、影像集、轉盤集或視訊，請選取 **[!UICONTROL 檢視者]**.

      在左側欄中，選取檢視器預設集名稱。 集或視訊的預覽會在個別頁面中開啟。

      在左側欄的底部，選取 **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. 選取文字並複製到網頁瀏覽器，以便預覽資產或將其新增至網頁內容頁面。

   若要結束URL視窗，請選取 **[!UICONTROL X]** 或選取 **[!UICONTROL 關閉]**.

## 取得靜態資產的URL {#obtaining-a-url-for-a-static-asset}

Dynamic Media支援靜態資產的傳送，這是影像和視訊以外的其他資產。 支援的靜態資產傳送格式包括：

* 3D檔案
* 動畫GIF
* 音訊檔案
* CSS
* JavaScript （當您的公司設定有自己的網域時）
* PDF
* SVG
* XML
* ZIP

**若要取得靜態資產的URL：**

1. 導覽至 *已發佈* 您要複製其URL的靜態資產，並選取要開啟的資產。

   請記住，URL僅供複製 *晚於* 您有 *已發佈* 靜態資產。

   另請參閱 [發佈資產](publishing-dynamicmedia-assets.md).

1. 使用下列任何方法取得已發佈靜態資產的URL：

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         例如：`https://aem.com/is/content/adobe/image.gif`。
   * 選取 **[!UICONTROL 資產]** > **[!UICONTROL 動態轉譯]**，然後選取靜態資產的動態轉譯並複製URL。

      變更複製的URL以使用 `is/content` 路徑中而不是 `is/image/`.


## 取得已發佈影片轉譯的影片URL {#obtaining-a-video-url-for-a-published-video-rendition}

1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲端]** > **[!UICONTROL Cloud Services]**.
1. 於 **[!UICONTROL Cloud Services]** 頁面，向下捲動至 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選取 **[!UICONTROL 顯示設定]**.
1. 下 **[!UICONTROL 可用的設定]**，選取您想要的設定名稱。

1. 於 **[!UICONTROL Dynamic Media雲端設定]** 頁面，底下 **[!UICONTROL 視訊服務URL]**，向下複製整個URL路徑。 您稍後需要在步驟中複製的URL路徑。

   例如，URL路徑可能如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/`

   （以上路徑只是範例，並非您所複製的實際路徑。）

1. 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。

   例如，如果註冊ID為 `87654321|MyCompany`，客戶名稱會是 `MyCompany`.

1. 在頁面的左上角附近，選取 **[!UICONTROL Cloud Services]**，然後選取Experience Manager標誌並導覽至 **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 從JCR (Java™內容存放庫)向下複製整個視訊轉譯路徑。

   例如，視訊的轉譯路徑可能如下所示：

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   （以上路徑只是範例，並非您所複製的實際路徑。）

1. 以下列順序排列複製的資訊，使其形成完整的URL路徑：

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   例如，使用上述步驟中的範例路徑和範例客戶名稱，完整路徑如下所示：

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   此範例是已發佈影片轉譯的完整影片URL。

## 取得最適化位元速率串流的視訊URL （DASH或HLS） {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. 在Experience Manager中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 雲端]** > **[!UICONTROL Cloud Services]**.
1. 於 **[!UICONTROL Cloud Services]** 頁面，向下捲動至 **[!UICONTROL Dynamic MediaCloud Services]** 標題，然後選取 **[!UICONTROL 顯示設定]**.
1. 下 **[!UICONTROL 可用的設定]**，選取您想要的設定名稱。
1. 於 **[!UICONTROL Dynamic MediaCloud Services設定]** 頁面，請執行下列動作：

   * 下 **[!UICONTROL 視訊服務URL]**，複製整個URL路徑。 您稍後需要在這些步驟中複製的URL路徑。 例如，URL路徑可能如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/`

   （以上路徑只是範例，並非您所複製的實際路徑。）

   * 在&#x200B;**[!UICONTROL 注册 ID]** 下，复制 ID 最后一部分中的客户名称。您稍後需要在這些步驟中複製的客戶名稱。

      例如，如果註冊ID為 `87654321|demoCo`，則您複製的客戶名稱為 `demoCo`.


1. 根據您使用的視訊傳送通訊協定，複製各自的通訊協定選擇器。 您稍後需要在這些步驟中複製通訊協定選擇器。

   | 您使用的視訊傳送通訊協定 | 要使用的通訊協定選擇器 |
   |---|---|
   | HTTP <br> 如果您使用HTTP （不安全視訊傳送），請務必在先前複製的視訊服務URL值中將https變更為http。 | `public/` |
   | HTTPS | `public-ssl/` |

1. 複製Dynamic Media所處理之Experience Manager中的完整視訊資產路徑。 您稍後在這些步驟中需要此複製的視訊資產路徑。

   例如：

   `/content/dam/marketing/MyVideo.mp4`

1. 合併您先前複製的所有片段，依下列順序建立字串：

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   例如，使用這些步驟中範例的複製資訊，字串會顯示如下：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. 透過附加來完成URL `.m3u8` 至字串結尾。 例如，附加 `.m3u8` 至上一步的字串，完整的URL路徑如下所示：

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## 使用HTTP/2傳遞您的Dynamic Media資產 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web通訊協定，可改善瀏覽器和伺服器的通訊方式。 它提供更快速的資訊傳輸，並減少所需的處理能力。 Dynamic Media資產的傳送現在可透過HTTP/2進行，以提供更佳的回應和載入時間。

另請參閱 [HTTP2傳送內容](http2.md) 以取得開始使用HTTP/2與Dynamic Media帳戶的完整詳細資訊。
