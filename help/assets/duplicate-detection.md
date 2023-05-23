---
title: 啟用偵測重複資產
description: 瞭解如何在Experience Manager中啟用重複資產偵測。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 啟用偵測重複資產 {#enable-detection-of-duplicate-assets}

如果您嘗試上傳中存在的資產 [!DNL Adobe Experience Manager Assets]，重複資料偵測功能會將其識別為重複資料。 重複資料偵測預設為停用。 若要啟用此功能，請執行下列步驟：

1. 開啟 [!DNL Experience Manager] 存取Web主控台設定頁面 `https://[aem_server]:[port]/system/console/configMgr`.
1. 編輯servlet的設定 **[!UICONTROL Day CQ DAM建立資產]**.
1. 選取 **[!UICONTROL 偵測重複專案]** 選項，然後按一下 **[!UICONTROL 儲存]**.

   ![選取servlet中的偵測重複選項](assets/chlimage_1-377.png)

   *圖：選取servlet中的偵測重複選項。*

現在已在中啟用偵測重複功能 [!DNL Assets]. 當使用者嘗試上傳中存在的資產時 [!DNL Experience Manager]，系統會檢查衝突並加以指示。 資產識別使用儲存於的SHA-1雜湊 `jcr:content/metadata/dam:sha1`，這表示不論檔案名稱為何，都會偵測到重複的資產。

>[!MORELIKETHIS]
>
>* [複製現有存放庫中的資產（來自社群成員的教學課程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

