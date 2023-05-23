---
title: 使用手寫簽名將電子簽章套用至表單
seo-title: Apply electronic signatures to a form using scribble signatures
description: 使用塗鴉簽署表單
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# 使用手寫簽名將電子簽章套用至表單{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用 **手寫簽名** 元件和 **簽章步驟** 在最適化表單上繪圖（塗鴉）簽章的元件。 簽名步驟元件會顯示最適化表單的PDF版本。 您需要啟用「記錄檔案」選項或表單範本式最適化表單，才能使用簽名步驟元件。

![塗鴉符號對話方塊](/help/forms/using/assets/scribble-signature.png)

## 簽名視窗中可用的各種選項

* **答：** 按一下 **油漆筆刷** 圖示在畫布上繪製您的簽名。
* **B：** 按一下 **清除** 圖示可清除畫布上的簽名。
* **C：** 按一下 **地理位置** 圖示以連同簽名一起新增地理位置。
* **D：** 按一下 **鍵盤** 圖示在畫布上輸入您的名稱。

點選「完成」後![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示時，您無法編輯簽名。 如果想要編輯簽名，則必須忽略目前的簽名，並使用上述「油漆筆刷/鍵盤」選項重新簽名。

您可以點選 **設定** ![設定](assets/configure.png) 圖示來設定手寫簽名畫布的外觀比例。
* 當Scribble Signature畫布的外觀比例小於1時，會在Scribble Signature畫布底部新增地理位置資訊。

* 當Scribble Signature畫布的外觀比例大於1時，地理位置資訊會新增到Scribble Signature畫布的右側。

![塗鴉簽名 — bottom](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>簽名一律以PNG格式儲存。

## 設定最適化表單以使用手寫簽名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 建立已啟用記錄檔案選項或表單範本式的最適化表單。 如需逐步資訊，請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md).
1. 拖放 **手寫簽名** 元件從元件瀏覽器變更為最適化表單。
1. 點選 **設定** ![設定](assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示「草寫簽名」元件的屬性。 設定手寫簽名元件的屬性。
1. 將「簽名步驟」元件從元件瀏覽器拖放至最適化表單。

   >[!NOTE]
   >
   >簽章步驟元件會佔據可用於表單的完整寬度。 建議在包含簽名步驟元件的區段上不要有任何其他元件。

1. 在「內容」瀏覽器中，點選 **表單容器**，然後點選 **設定** ![](/help/forms/using/assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。 導覽至 **最適化表單容器** > **電子簽章** 並取消選取 **啟用Adobe Sign** 選項。 點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。

   >[!NOTE]
   >
   >將簽名步驟元件新增至最適化表單時，會自動選取「啟用Adobe Sign」選項。

1. 點選 **設定** ![設定](assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示簽名步驟屬性。 設定下列屬性：

   * **元素名稱**：指定元件的名稱。

   * **標題：** 指定元件的唯一標題。
   * **範本訊息：** 指定在載入簽名PDF時要顯示的訊息。 Adobe Sign服務需要一些時間來準備和載入簽名PDF。
   * **簽署服務：** 選取 **手寫簽名** 選項。

   * **CSS類別**：指定使用者端程式庫的CSS類別（如有）。 建議使用 [主題](../../forms/using/themes.md) 和 [內嵌樣式](../../forms/using/inline-style-adaptive-forms.md) 而非CSS類別。

   點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。 已成功設定簽名。

   現在，當您填寫表單時，會顯示最適化表單的PDF版本，並提供簽署PDF檔案的選項。 如需詳細資訊，請參閱 [使用手寫簽名簽署調適型表單](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## 使用手寫簽名簽署調適型表單 {#sign-an-adaptive-form-using-scribble-signature}

1. 填寫最適化表單並到達簽名步驟頁面後，會顯示簽名畫面。

   ![塗鴉符號對話方塊](/help/forms/using/assets/esignscribblesign.jpg)

1. 按一下 **[!UICONTROL 簽署]**. 手寫符號對話方塊隨即顯示。 簽署表單並按一下完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存簽名。

   ![塗鴉符號對話方塊](/help/forms/using/assets/scribblewidget.png)

1. 按一下[完成]以完成簽署程式。

   ![完成簽署程式](/help/forms/using/assets/scribblecomplete.jpg)

簽名會新增至表單，而表單控制項會移至下一個面板。
