---
title: 支援的檔案格式和MIME型別
description: 支援的檔案格式和MIME型別 [!DNL Assets] 和 [!DNL Dynamic Media] 以及每種格式支援的功能。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
source-git-commit: c1878d6aadba9c795168459dbd5f09abfe0fc327
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 10%

---

# 中支援的格式 [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] 支援廣泛的檔案格式，且每種功能對於不同的MIME型別都有不同的支援。 若要整合 [!DNL Assets] 搭配其他符合標準的數位資產管理(DAM)解決方案和案頭軟體，使用Adobe的 [!DNL Extensible Metadata Platform] (XMP)。

使用图例了解支持级别。

| 支持级别 | 描述 |
| :-----------: | ------------------------------ |
| ✓ | 支持 |
| &#42; | 支援附加功能 |
| − | 不适用 |

## 中支援的點陣影像格式 [!DNL Experience Manager] {#supported-raster-image-formats}

中支援的點陣影像格式 [!DNL Assets] 為：

| 格式 | 存储 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | 编辑 | 中繼資料回寫 | 见解 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡合併的影像會從PSD檔案中擷取。 這是由Adobe Photoshop產生並包含在PSD檔案中的影像。 視設定而定，合併的影像不一定是實際影像。

除了上述資訊外，請考量下列事項：

* EPS檔案支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 若要新增支援， [設定ImageMagick](best-practices-for-imagemagick.md). 若要整合協力廠商工具以啟用其他功能，請參閱 [以命令列為基礎的媒體處理常式](media-handlers.md#command-line-based-media-handler).

* 當中繼資料回寫新增至PSB檔案格式時，即可使用 `NComm` 處理常式。

* 對於EPS檔案，PostScript檔案建構慣例(PS-Adobe) 3.0版或更新版本支援中繼資料回寫。

## 支援的3D格式 {#support-3d-formats}

支援下列3D格式清單。

另請參閱 [在Dynamic Media中使用3D資產。](/help/assets/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 存取控制 | 縮圖預覽 | 3D預覽 | Dynamic Media傳遞 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | − | ✓ | − |
| 物件 | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## 支援的PDF模擬轉譯器程式庫 {#supported-pdf-rasterizer-library}

Adobe PDF模擬轉譯器程式庫可為大型且需要大量內容的影片製作高品質的縮圖和預覽 [!DNL Adobe Illustrator] 和PDF檔案。 Adobe建議針對下列專案使用PDF模擬轉譯器資料庫：

* 需要處理大量資源的內容密集型AI/PDF檔案。
* 預設不會產生縮圖的AI/PDF檔案。
* 具有Pantone Matching System (PMS)顏色的AI檔案。

另請參閱 [使用PDF模擬轉譯器](aem-pdf-rasterizer.md).

## 支援的影像轉碼程式庫 {#supported-image-transcoding-library}

「Adobe影像轉碼」資料庫是影像處理解決方案，可執行核心影像處理功能，例如編碼、轉碼、重新取樣和調整大小。

影像轉碼程式庫支援JPG/JPEG、PNG （8位元和16位元）、GIF、BMP、TIFF/壓縮TIFF(32位元TIFF檔案和PTIFF檔案除外)、ICO和ICN MIME型別。

另請參閱 [影像轉碼程式庫](imaging-transcoding-library.md).

## 支援的Camera Raw {#supported-camera-raw}

此 [!DNL Adobe Camera Raw] 程式庫啟用 [!DNL Assets] 擷取原始影像。 另請參閱 [Camera Raw支援](camera-raw.md).

## 支援 [!DNL Assets] 檔案格式 {#supported-document-formats}

資產管理功能支援的檔案格式如下：

| 格式 | 存储 | [中繼資料管理](metadata.md) | 全文<br> 摘取 | [中繼資料擷取](metadata.md) | 縮圖<br> 層代 | [子資產擷取](managing-linked-subassets.md) | [中繼資料回寫](xmp-writeback.md) | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| ePub | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## 支援的多媒體格式 {#supported-multimedia-formats}

|  | 存储 | 中繼資料管理 | 中繼資料擷取 | 產生縮圖 | FFmpeg轉碼 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## 支援的封存格式 {#supported-archive-formats}

下表說明支援的封存格式及常見DAM工作流程的適用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media傳遞 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 其他支援的格式 {#other-supported-formats}

以下說明幾種特定檔案格式常見DAM功能的適用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media傳遞 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript （若已設定自己的傳送網域） | − | − | − | − | − | ✓ |

>[!NOTE]
>
>上傳和分發JavaScript檔案可能安全，也可能不安全。 如有必要，您可以使用覆蓋來防止使用者上傳JS檔案。

## 支援的MIME型別 {#supported-mime-types}

依預設， [!DNL Experience Manager] 會使用副檔名偵測檔案型別。 [!DNL Experience Manager] 可以從檔案內容偵測到它。 如果是後者，請選取 [!UICONTROL 從內容中偵測MIME] 中的選項 [!UICONTROL Day CQ DAM Mime型別服務] 在 [!DNL Experience Manager] 網頁主控台。

CRXDE Lite中有提供支援的MIME型別清單，請前往 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| 副檔名 | MIME型別/網際網路媒體型別 | 預設jobParam值 | 允許的工作引數值 |
|---|---|---|---|
| 图像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 預設jobParam會套用至所有影像MIME型別資產。<ul><li>[去底色背景選項](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

## Dynamic Media — 支援的輸入視訊格式可轉碼 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 視訊副檔名 | 容器 | 建議的視訊轉碼器 | 不支援的視訊轉碼器 |
|---|---|---|---|
| AVI | A/V交錯 | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft®Video 1 (MS-CRAM) |
| FLV、F4V | AdobeFlash | H264/AVC、Flix VP6、H263、Sorenson | SWF（向量動畫檔案） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422和HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate， Apple動畫 |
| MP4 | MPEG-4 | H264/AVC （所有設定檔） | − |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | − |
| OGV， OGG | Ogg | Theora， VP3， Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting (G2M2、G2M3、G2M4) | Microsoft®畫面(MSS2)、Microsoft®像片故事(WVP2) |

‡目前尚不支援將此視訊格式用於Dynamic Media中的互動式視訊，或用於Experience Manager Assets中的註解。

## Dynamic Media — 支援的檔案格式 {#supported-document-formats-dynamic-media}

| 格式 | 上傳<br> （輸入格式） | 建立<br> 影像<br> 預設集<br> （輸出格式） | 預覽<br> 動態<br> 轉譯 | 傳遞<br> 動態<br> 轉譯 | 下載<br> 動態<br> 轉譯 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) （請參閱下方的注意事項） | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>對於安全PDF，僅支援上傳。

除了上述功能外，請考量下列事項：

* 若要使用Dynamic Media產生PDF檔案的動態轉譯，請參閱 [Adobe Illustrator (AI)、Postscript (EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用Dynamic Media來預覽和產生AI檔案的動態轉譯，請參閱 [Adobe Illustrator (AI)、Postscript (EPS)和PDF檔案格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 若要使用Dynamic Media產生INDD檔案的動態轉譯，請參閱 [InDesign(INDD)檔案格式](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media — 支援的點陣影像格式 {#supported-raster-image-formats-dynamic-media}

| 格式 | 上傳<br> （輸入格式） | 建立<br> 影像<br> 預設集<br> （輸出格式） | 預覽<br> 動態<br> 轉譯 | 傳遞<br> 動態<br> 轉譯 | 下載<br> 動態<br> 轉譯 | 設定支援此格式的型別 |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md)， [混合媒體](/help/assets/mixed-media-sets.md)、和 [迴轉](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md)， [混合媒體](/help/assets/mixed-media-sets.md)、和 [迴轉](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [影像](/help/assets/image-sets.md)， [混合媒體](/help/assets/mixed-media-sets.md)、和 [迴轉](/help/assets/spin-sets.md) |
| BMP | ✓ | − | − | − | − | [影像](/help/assets/image-sets.md)， [混合媒體](/help/assets/mixed-media-sets.md)、和 [迴轉](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| PICT | ✓ | − | − | − | − | − |

‡合併的影像會從PSD檔案中擷取。 這是由Adobe Photoshop產生並包含在PSD檔案中的影像。 視設定而定，合併的影像不一定是實際影像。

* EPS檔案支援僅適用於點陣影像。 例如，預設不支援EPS向量影像的縮圖產生。 若要新增支援， [設定ImageMagick](best-practices-for-imagemagick.md). 若要整合協力廠商工具以啟用其他功能，請參閱 [以命令列為基礎的媒體處理常式](media-handlers.md#command-line-based-media-handler).

* 使用 [!DNL Dynamic Media] 若要預覽和產生EPS檔案的動態轉譯，請參閱 [Adobe Illustrator (AI)、Postscript (EPS)和PDF檔案格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 對於EPS檔案，PostScript檔案建構慣例(PS-Adobe) 3.0版或更新版本支援中繼資料回寫。

## Dynamic Media — 不支援的點陣影像格式 {#unsupported-image-formats-dynamic-media}

下列清單說明點陣影像檔案格式的子型別 *not* 在Dynamic Media中支援。

另請參閱 [偵測Dynamic Media不支援的檔案格式](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) 知識庫文章。

* IDAT區塊大小大於100 MB的PNG檔案。
* PSB檔案。
* 不支援色彩空間不是CMYK、RGB、灰階或點陣圖的PSD檔案。 不支援DuoTone、Lab和索引色域。
* 位元深度大於16的PSD檔案。
* TIFF含有浮點資料的檔案。
* TIFF具有Lab色域的檔案。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media — 支援的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D格式。

另請參閱 [在Dynamic Media中使用3D資產](/help/assets/assets-3d.md).

| 3D副檔名 | 檔案格式 | MIME型別 | 注释 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體光刻 | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *僅支援內嵌；不提供檢視或互動。* USDZ是專屬的3D格式，可供Safari和iOS裝置原生檢視。 |

>[!MORELIKETHIS]
>
>* [啟用MIME型別型資產和Dynamic Media Classic上傳工作引數支援](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [為上載工作引數支援設定MIME型別型](config-dynamic.md).

