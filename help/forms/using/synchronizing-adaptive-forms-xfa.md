---
title: 將最適化Forms與XFA表單範本同步
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: 將調適型表單與XFA/XDP檔案同步。
seo-description: Synchronizing Adaptive forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
feature: Adaptive Forms
exl-id: fed67c23-a9b7-403e-9199-dfd527d5f209
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# 將最適化Forms與XFA表單範本同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 简介 {#introduction}

您可以根據XFA表單範本建立最適化表單( `*.XDP` 檔案)。 此重複使用可讓您保留在現有XFA表單中的投資。 如需有關如何使用XFA表單範本建立調適型表單的資訊， [根據範本建立最適化表單](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p).

您可以在最適化表單中重複使用XDP檔案中的欄位。 這些欄位稱為繫結欄位。 繫結欄位的屬性（例如指令碼、標籤和顯示格式）會從XDP檔案複製。 您也可以選擇覆寫其中某些屬性的值。

AEM Forms可協助您保持適用性表單的欄位與稍後對XDP檔案中對應欄位所做的任何變更同步。 本文說明如何啟用此同步化。

![您可以從XFA表單將欄位拖曳到最適化表單](assets/drag-drop-xfa.gif.gif)

在AEM Forms製作環境中，您可以將XFA表單（左）的欄位拖曳至最適化表單（右）

## 前提条件 {#prerequisites}

若要使用本文中的資訊，建議您熟悉下列領域：

* [建立最適化表單](../../forms/using/creating-adaptive-form.md)

* XFA (XML Forms架構)

若要使用文章中提供的資產作為範例，請下載範例套件，如下節所述， [範例套件](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## 範例套件 {#sample-package}

文章以範例示範如何將最適化表單與更新的XFA表單範本同步。 範例中使用的資產可在套件中使用，該套件可從 [下載](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) 章節。

上傳套件後，您可以在AEM Forms UI中檢視這些資產。

使用封裝管理程式安裝封裝： `https://<server>:<port>/crx/packmgr/index.jsp`

此套件包含下列資產：

1. `sample-form.xdp`：作為範例的XFA表單範本

1. `sample-xfa-af`：根據sample-form.xdp檔案的最適化表單。 不過，此最適化表單不包含任何欄位。 在下一步中，我們將新增內容至此最適化表單。

### 將內容新增至最適化表單 {#add-content-to-adaptive-form-br}

1. 導覽至https://&lt;server>：&lt;port>/aem/forms.html. 如有要求，請輸入您的認證。
1. 開啟sample-af-xfa以在作者模式中編輯。
1. 從側邊欄中的內容瀏覽器，選擇資料模型物件索引標籤。 將NumericField1和TextField1拖曳至最適化表單上。
1. 變更NumericField1的標題，從 **數值欄位** 至 **AF數值欄位。**

>[!NOTE]
>
>在上述步驟中，我們覆寫XDP檔案中欄位的屬性。 因此，如果稍後修改XDP檔案中的對應屬性，此屬性將不會同步。

## 偵測XDP檔案中的變更 {#detecting-changes-in-xdp-file}

每當XDP檔案或片段中發生任何變更時，AEM Forms UI都會標示所有以XDP檔案或片段為基礎的最適化表單。

更新XDP檔案後，您需要在AEM Forms UI中再次上傳該檔案，才能標籤變更。

例如，讓我們更新 `sample-form.xdp` 檔案：

1. 導覽至 `https://<server>:<port>/projects.html.` 出現提示時輸入您的認證。
1. 按一下左側的Forms標籤。
1. 下載 `sample-form.xdp` 檔案。 XDP檔案下載為 `.zip` 檔案，可使用任何檔案解壓縮公用程式解壓縮。

1. 開啟 `sample-form.xdp` 檔案並變更欄位TextField1的標題 **文字欄位** 至 **我的文字欄位**.

1. 上傳 `sample-form.xdp` 檔案傳回AEM Forms UI。

如果XDP檔案更新，當您根據XDP檔案編輯調適型表單時，會在編輯器中看到圖示。 此圖示表示最適化表單與XDP檔案不同步。 在下圖中，請參閱側邊欄中的下一個圖示。

![圖示可顯示最適化表單不同步於XDP檔案](assets/sync-af-xfa.png)

## 將調適型表單與最新的XDP檔案同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

下次開啟與XDP檔案不同步的適用性表單進行製作時，會顯示下列訊息： **最適化表單的結構描述/表單範本已更新。 `Click Here` 以使用新版本重新建立基礎。**

按一下訊息會將最適化表單中的欄位與XDP檔案中的對應欄位同步。

對於本文中使用的範例，請開啟 `sample-xfa-af` 在製作模式中。 訊息會顯示在最適化表單的底部。

![提示您將最適化表單與XDP檔案同步的訊息](assets/sync-af-xfa-1.png)

### 更新屬性 {#updating-the-properties}

從XDP檔案複製到調適型表單的所有屬性都會更新，但作者在調適型表單（從元件對話方塊）中明確覆寫的內容除外。 伺服器記錄檔中提供已更新的屬性清單。

若要更新最適化表單範例中的屬性，請按一下連結(標籤為 `"Click Here"`)。 TextField1的標題變更自 **文字欄位** 至 **我的文字欄位**.

![update — 屬性](assets/update-property.png)

>[!NOTE]
>
>標籤AF數值欄位未變更，因為您已從元件屬性對話方塊覆寫此屬性，如中所述 [將內容新增至最適化表單](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### 將XDP檔案的新欄位新增至最適化表單   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

任何稍後新增至原始XDP檔案的欄位都會顯示在「表單階層」標籤中，而且您可以將這些新欄位拖曳至調適型表單。

您不需要按一下錯誤訊息中的連結，即可更新「表單階層」標籤中的欄位。

### XDP檔案中的已刪除欄位 {#deleted-fields-in-xdp-file}

如果先前複製到最適化表單的欄位從XDP檔案中刪除，則會在編寫模式下顯示一則錯誤消息，指出該欄位不存在於XDP檔案中。 在這種情況下，請從最適化表單中手動刪除欄位或清除 `bindRef` 屬性（在元件對話方塊中）。

以下步驟說明本文中所用範例中資產的此使用流程：

1. 更新 `sample-form.xdp` 檔案並刪除NumericField1。
1. 上傳 `sample-form.xdp` AEM Forms UI中的檔案
1. 開啟 `sample-xfa-af` 用於編寫的最適化表單。 顯示下列錯誤訊息：已更新最適化表單的結構描述/表單範本。 `Click Here` 以使用新版本重新建立基礎。

1. 按一下連結(標示為「 」 `Click Here`「)中。 系統會顯示錯誤訊息，指出欄位在XDP檔案中不再存在。

![刪除XDP檔案中的元素時看到的錯誤](assets/no-element-xdp.png)

已刪除的欄位也會標示圖示，以表示欄位中發生錯誤。

![欄位中的錯誤圖示](assets/error-field.png)

>[!NOTE]
>
>適用性表單中有不正確繫結（無效）的欄位 `bindRef` （例如「編輯」對話方塊中的值）也視為已刪除欄位。 如果作者未修正這些錯誤並發佈調適型表單，則該欄位會被視為一般未繫結的調適型表單欄位，並包含在輸出XML檔案的未繫結區段中。

## 下载 {#downloads}

本文範例的Content-package

[获取文件](assets/sample-xfa-af-sync-1.0.zip)
