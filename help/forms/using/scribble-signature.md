---
title: 在HTML5表單中使用手寫簽名
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5表單越來越多地用於觸控裝置，常見的要求之一是支援簽名。 在行動裝置上簽署檔案已成為在行動裝置上簽署表單的認可方式。
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 在HTML5表單中使用手寫簽名{#using-scribble-signature-in-html-forms}

HTML5表單越來越多地用於觸控裝置，常見的要求之一是支援簽名。 手寫文字（使用手寫筆或手指書寫）已成為在行動裝置上簽署表單的認可方式。 HTML5 forms和Forms Designer現在可啟用在表單上有手寫簽名欄位的選項。 在瀏覽器中呈現表單時，人們可以使用手寫筆、滑鼠或觸控來登入這些欄位。

## 如何使用手寫簽名欄位設計表單 {#how-to-design-a-form-using-scribble-signature-field}

1. 在Forms Designer中開啟表單。
1. 將「簽名草寫」欄位拖放至頁面上。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >呈現欄位時，會反映在Forms Designer中選取欄位的Dimension。 不過，演算後的簽章方塊的維度是根據欄位的外觀比例來計算，而非根據Forms Designer中指定的維度來計算。

1. 設定「簽名草寫」欄位。

   依預設，「簽名塗鴉」欄位會在iPad上的簽名程式中將地理位置資訊標籤為必要（對於其他裝置為選用）。 此預設行為可透過變更 `geoLocMandatoryOnIpad` 屬性。 此屬性在「簽名草寫欄位」中顯示為額外專案。 修改它的步驟如下：

   1. 在表單上，選取「簽名草稿」欄位。
   1. 選取 **XML來源** 標籤。

      >[!NOTE]
      >
      >若要開啟「XML來源」標籤，請按一下 **檢視** > **XML來源**.

   1. 找到 `<ui>` 標籤中的變數 `<field>` 標籤並修改原始程式碼，使其如下所示：

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. 選取 **設計檢視** 標籤。 在確認方塊上，按一下 **是**.
   1. 儲存表單。

1. 在支援的裝置/案頭瀏覽器上轉譯表單。

## 與Scribble簽名連線 {#interfacing-with-the-scribble-signatures}

### 簽署 {#signing}

在將簽名草寫欄位新增至表單並呈現後，按一下或點選該欄位會開啟一個對話方塊。 使用者可以使用滑鼠、手指或手寫筆，在點狀矩形所指定的繪製區域中塗寫簽名。

![地理位置](assets/geolocation.png)

**答：** 筆刷 **B.** 橡皮擦 **C.** 地理位置 **D.** 地理位置資訊

### 地理標籤 {#geo-tagging}

建立塗鴉時按一下地理位置圖示，會將地理位置和時間資訊內嵌到欄位中。

>[!NOTE]
根據預設，在iPad上，內嵌地理位置資訊是強制性的。

在iPad上，地理位置圖示預設不會顯示，而且當您按一下時，地理位置資訊會自動內嵌 **確定**.

若是iPad，此設定可以透過修改 `geoLocManadatoryOnIpad` 引數至 `0`，在欄位的init引數中。

* 當地理位置資訊是強制性的時，使用者會看到縮小的繪製區域。 使用者按一下即可新增地理位置文字 **確定** 圖示加以檢視。
* 在其他情況下，使用者會看到一個完整的可繪製區域。 如果使用者選擇內嵌地理位置資訊，此區域會調整大小以符合地理位置文字。

### 清除簽名 {#clearing-a-signature}

使用此功能時，使用者可以按一下 **橡皮擦** 圖示來清除欄位，然後重新開始。 如果新增了地理位置資訊，也會將其清除。

### 儲存簽名 {#saving-a-signature}

按一下 **確定** 圖示會將塗鴉儲存為欄位中的影像。 影像和值可提交至伺服器以供進一步處理。 使用者按一下後 **確定**，即會鎖定塗鴉欄位。 無法使用塗鴉Widget再次編輯簽章。

點選或按一下「塗鴉」欄位會以唯讀模式開啟對話方塊。

![3](assets/3.png)

### 選取筆大小 {#selecting-pen-size}

按一下 **筆刷** 圖示來顯示可用筆大小的清單。 按一下或點選筆大小，以使用對應的筆。

### 從表單中刪除簽章 {#delete-signatures-from-the-form}

若要從表單中刪除簽名：

* （行動裝置）長按簽名欄位，然後在確認對話方塊中，點選 **是**.
* （案頭）將滑鼠游標停留在簽名欄位上，按一下 **取消** 圖示，然後在確認對話方塊上，按一下 **是**.
