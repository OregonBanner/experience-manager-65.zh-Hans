---
title: 在Dynamic Media中最佳化影像品質的最佳作法
description: 瞭解在Dynamic Media中最佳化影像品質的最佳實務
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 4%

---

# 在Dynamic Media中最佳化影像品質的最佳作法 {#best-practices-for-optimizing-the-quality-of-your-images}

最佳化影像品質是耗時的程式，因為許多因素都會產生可接受的演算結果。 部分結果具有主觀性，因為個人對影像品質的看法不同。 結構化實驗是關鍵。

Adobe Experience Manager包含100多項Dynamic Media影像傳送命令，可用於調整和最佳化影像和演算結果。 以下准則可協助您使用一些基本指令和最佳實務，簡化流程並快速取得良好結果。

## 影像格式的最佳實務(`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG或PNG是提供高品質影像，且大小與重量可管理的最佳選擇。
* 如果URL中未提供任何格式命令，Dynamic Media影像傳送預設為JPG傳送。
* JPG會以10:1的比例壓縮，通常會產生較小的影像檔案大小。 PNG會以大約2:1的比例壓縮，除非有時影像包含白色背景時。 不過，PNG檔案通常比JPG檔案大。
* JPG使用有失真壓縮，這表示壓縮期間會捨棄圖片元素（畫素）。 另一方面，PNG使用無失真壓縮。
* JPG通常會以比合成影像更逼真的效果壓縮像片影像，而合成影像則具有銳利的邊緣和對比。
* 如果您的影像包含透明度，請使用PNG，因為JPG不支援透明度。

影像格式的最佳作法是從最常見的設定開始 `&fmt=JPG`.

## 影像大小的最佳實務 {#best-practices-for-image-size}

動態縮減影像大小是最常見的工作之一。 它涉及指定大小，以及（可選）用來縮減影像規模的縮減取樣模式。

* 調整影像大小時，最好且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或只是 `&hei=<value>`. 這些引數會根據長寬比自動設定影像寬度。
* `&resMode=<value>`控制縮減取樣所使用的演演算法。 開始於 `&resMode=sharp2`. 此值可提供最佳影像品質。 使用縮減取樣時 `value =bilin` 速度較快，通常會導致鋸齒狀不自然感。

如需調整影像大小的最佳作法，請使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 影像銳利化的最佳實務 {#best-practices-for-image-sharpening}

影像銳利化是控制網站上影像的最複雜方面，也會導致許多錯誤。 請參考下列實用資源，以進一步瞭解銳利化及不銳利化遮色片在Experience Manager中的運作方式：

最佳實務白皮書 [Adobe Dynamic Media Classic中的銳利化影像](/help/assets/assets/sharpening_images.pdf) 也適用於Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

透過Experience Manager，您可以在擷取時、傳送時或兩者同時銳利化影像。 不過，通常只會使用一種方法或另一種方法來銳利化影像，但不會同時使用兩者。 在URL上銳利化傳送的影像通常會產生最佳效果。

有兩種影像銳利化方法可供您使用：

* 簡單銳利化( `&op_sharpen`) — 類似於Photoshop中使用的銳利化濾鏡，簡單銳利化會在動態調整大小後，將基本銳利化套用至影像的最終檢視。 不過，使用者無法設定此方法。 除非必要，否則最好不要使用&amp;op_sharpen。
* 不銳利化遮色片( `&op_USM`) — 不銳利化遮色片是業界標準的銳利化濾鏡。 最佳作法是遵循下列准則，使用遮色片銳利化調整來銳利化影像。 「不銳利化遮色片」可讓您控制下列三個引數：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *金額&#x200B;*]**（0-5，效果強度。）
      * **[!UICONTROL *半徑&#x200B;*]**(0-250，圍繞銳利化物件繪製的「銳利化線條」寬度（以畫素為測量單位）。

      請記住，引數半徑和數量彼此對應。 減少半徑可藉由增加量來補償。 「半徑」允許更細微的控制，因為較低的值只會銳利化邊緣畫素，而較高的值會銳利化較寬的畫素範圍。

      * **[!UICONTROL *臨界值&#x200B;*]**（0-255，效果敏感度。）

             此参数确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素，而滤镜会锐化这些像素。 **[!UICONTROL threshold]**参数有助于避免过度锐化颜色相似的区域，如肤色。 例如，阈值为12时，会忽略肤色亮度的细微变化，以避免添加“杂色”，同时仍会为高对比度区域添加边缘对比度，如睫毛与皮肤相遇的地方。
         
         如需如何設定這三個引數的詳細資訊，包括篩選使用的最佳實務，請參閱下列資源：

         有關銳利化影像的Experience Manager說明主題。

         最佳實務白皮書 [Adobe Dynamic Media Classic中的銳利化影像](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager也可讓您控制第四個引數：單色(0,1)。 此引數決定使用值0將遮色片銳利化調整分別套用至每個色彩元件，或使用值1套用至影像亮度/強度。


最佳作法是從「遮色片銳利化調整半徑」引數開始。 您可以開始使用的Radius設定如下：

* **[!UICONTROL 網站]** - 0.2-0.3畫素
* **[!UICONTROL 像片列印(250-300 ppi)]** - 0.3-0.5畫素
* **[!UICONTROL 膠版列印(266-300 ppi)]** - 0.7至1.0畫素
* **[!UICONTROL 畫布列印(150 ppi)]** - 1.5至2.0畫素

逐漸將數量從1.75增加到4。 如果銳利化仍不是您想要的方式，請將半徑增加一個小數點，然後再次執行從1.75到4的量。 視需要重複。

將單色引數設定保留為0。

### JPEG壓縮的最佳作法(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此引數可控制JPG編碼品質。 較高的值表示影像品質較高，但檔案大小較大；或者，較低的值表示影像品質較低，但檔案大小較小。 此引數的範圍為0到100。
* 若要最佳化品質，請勿將引數值設為100。 設定90或95與100之間的差異幾乎無法察覺，但100卻不必要地增加了影像檔案的大小。 因此，若要最佳化影像品質，但避免影像檔案過大，請設定 `qlt= value` 至90或95。
* 若要針對較小的影像檔案大小進行最佳化，但將影像品質維持在可接受的等級，請設定 `qlt= value` 至80。 值低於70到75會導致影像品質顯著下降。
* 最佳做法是居於中間，將 `qlt= value` 到85歲才能居於中間。
* 在中使用色度旗標 `qlt=`

   * 此 `qlt=` 引數有第二個設定，可讓您使用值開啟RGB色度縮減取樣 `,1` 或使用值關閉 `,0`.
   * 若要保持簡單，請從RGB色度縮減取樣關閉(`,0`)。 此設定通常會產生更好的影像品質，尤其是對於具有大量銳利邊緣和對比的合成影像。

使用JPG壓縮當作最佳實務 `&qlt=85,0`.

## JPEG規模調整的最佳實務(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果您想要確保影像不會超過特定大小，以傳送至記憶體有限的裝置，jpegSize會是個有用的引數。

* 此引數是以千位元組(`jpegSize=&lt;size_in_kilobytes&gt;`)。 它會定義影像傳送所允許的大小上限。
* `&jpegSize=` 與JPG壓縮引數互動 `&qlt=`. 如果JPG回應具有指定的JPG壓縮引數(`&qlt=`)不會超過jpegSize值，則影像會以 `&qlt=` 依定義。 否則， `&qlt=` 會逐漸減少，直到影像符合允許的大小上限，或直到系統判斷它無法符合併傳回錯誤為止。

最佳實務是 `&jpegSize=` 並新增引數 `&qlt=` 如果您要將JPG影像傳送至記憶體有限的裝置。

## 最佳實務摘要 {#best-practices-summary}

為了達到高影像品質和小型檔案大小，最佳實務建議從下列參陣列合開始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

此設定組合可在大多數情況下產生絕佳結果。

如果影像需要進一步最佳化，請從半徑設定為0.2或0.3開始，逐步微調銳利化（不銳利化遮色片）引數。然後，逐漸將數量從1.75增加到最大值4 (相當於Photoshop中的400%)。 檢查是否達到預期結果。

如果銳利化結果仍然不令人滿意，請以小數增量增加半徑。 對於每個小數點增量，請在1.75處重新開始該數量，然後逐漸增加到4。 重複此程式，直到您達到想要的結果為止。 雖然上述值是創意工作室已驗證的方法，但請記住，您可以從其他值開始，並遵循其他策略。 結果是否令您滿意是主觀問題，因此結構化實驗是關鍵。

實驗時，以下一般建議有助於進一步最佳化您的工作流程：

* 請直接在URL上即時嘗試並測試不同的引數。
* 如需參考最佳做法，請記住，您可以將「Dynamic Media影像伺服」命令群組至影像預設集。 影像預設集基本上是含有自訂預設集名稱的URL命令巨集，例如 `$thumb_low$` 和 `&product_high$`. URL路徑中的自訂預設集名稱會呼叫這些預設集。 這類功能可協助您管理網站上不同影像使用模式的命令和品質設定，並縮短URL的整體長度。
* Experience Manager也提供更進階的影像品質調整方式，例如在擷取時套用銳利化影像。 對於有選項可調整和最佳化演算結果的進階使用案例， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可協助您提供客製化的深入分析和最佳實務。
