---
title: 在Designer中變更頁面零點內容
seo-title: Changing Page Zero content in Designer
description: 您知道在非Adobe PDF檢視器中檢視XFAPDF時，如何變更顯示在第0頁的訊息嗎？
seo-description: Do you know how you can change the message displayed on Page Zero of an XFA PDF when viewing it in a non-Adobe PDF viewer?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Adaptive Forms
exl-id: 466b7e85-a2f8-4e1e-8afc-1566b0ccb84c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# 在Designer中變更頁面零點內容 {#changing-page-zero-content-in-designer}

當非Adobe PDF檢視器(例如中的預設PDF檢視器)出現時，預設會顯示「頁面零」內容 [!DNL Chrome] 或 [!DNL Firefox]，無法讀取PDF/XFA表單的內容。 預設的「頁面零」訊息顯示如下。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] 版本Designer可讓您變更顯示在Page Zero上的訊息。 若要變更「頁數零」訊息，請執行下列步驟：

1. 確保您擁有 [!DNL AEM Forms] 已安裝的Designer版本。 您可以從Designer的「關於」畫面檢查版本。

1. 開啟您要變更「頁面零」內容的表單。

1. 按一下 **[!UICONTROL 檔案]** > **[!UICONTROL 表單屬性]**.

1. 在 [!UICONTROL 表單屬性] 對話方塊，按一下 ![加](assets/plus.png) （加號圖示）以新增自訂屬性。

1. 指定 **_pagezerocontent** 作為屬性的名稱。
1. 以RTF格式新增新的「頁面零」訊息作為值。 例如：


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 將表單儲存為PDF。

1. 在瀏覽器中檢視PDF表單，以確認訊息已更新。 上述範例值顯示如下：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>當您重新開啟表單時，您剛才建立的自訂屬性可能無法正確顯示在「表單屬性」對話方塊中。 不過，它仍可正常運作，且表單會顯示更新的「頁面零」訊息。
