---
title: 資料夾共用至 [!DNL Adobe Creative Cloud] 最佳實務
description: 設定 [!DNL Adobe Experience Manager] 允許使用者進入 [!DNL Experience Manager Assets] 以與Adobe Creative Cloud使用者交換資料夾。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 至 [!DNL Adobe Creative Cloud] 資料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>此 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 已棄用資料夾共用功能。 Adobe強烈建議使用較新的功能，例如 [Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 或 [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). 進一步瞭解 [Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] 可設定為允許使用者在 [!DNL Assets] 與的使用者共用資料夾 [!DNL Adobe Creative Cloud] 應用程式，因此可做為共用資料夾用於 [!DNL Adobe Creative Cloud] assets服務。 此功能可用於在創意團隊和之間交換檔案 [!DNL Assets] 使用者，尤其是當創意使用者無權存取 [!DNL Assets] 部署（不在企業網路上）。

此類整合可用於以下使用案例，尤其是與無法直接存取的使用者合作時 [!DNL Assets]：

* [!DNL Assets] 使用者與的使用者共用一組特定的數位資產。 [!DNL Adobe Creative Cloud] 檔案（例如，創意摘要和一組已核准的資產，用於新行銷活動的設計工作）。
* [!DNL Assets] 使用者會收到由建立的新檔案 [!DNL Adobe Creative Cloud] 應用程式使用者。

>[!NOTE]
>
>閱讀本檔案前，您可以檢閱整體的 [Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md) 以取得整合的概觀。

## 概述 {#overview}

[!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用需仰賴伺服器端在檔案夾之間共用資料夾 [!DNL Assets] 和 [!DNL Creative Cloud] 帳戶。 使用 [!DNL Creative Cloud] 案頭應用程式在他們的案頭上，另外還可以使用讓共用資料夾直接在他們的磁碟上使用 [!DNL Adobe CreativeSync] 技術。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（Managed Services或內部部署）中：在這裡會起始資料夾共用。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**：充當以下兩者之間的中介： [!DNL Experience Manager] 和 [!DNL Creative Cloud] 儲存服務。 使用整合之組織的管理員需要在Marketing Cloud組織與 [!DNL Assets] 部署。 它們也 [定義核准的Creative Cloud共同作業人員清單](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)，那 [!DNL Assets] 為了增加安全性，使用者也可以共用資料夾。

* **[!DNL Creative Cloud]Assets Web服務** (儲存和 [!DNL Creative Cloud] 檔案（網頁UI）：這是特定Creative Cloud應用程式使用者 [!DNL Assets] 資料夾已共用，將能夠接受邀請並在其Creative Cloud帳戶儲存空間中檢視該資料夾。
* **Creative Cloud案頭應用程式**：（選用）可透過與同步，從創意使用者的案頭直接存取共用資料夾/檔案 [!DNL Creative Cloud] 資產儲存。

## 特性與限制 {#characteristics-and-limitations}

* **變更的單向傳輸：** 檔案變更只會沿一個方向傳播 — 從系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])，即資產最初建立（上傳）的位置。 整合不會提供兩個系統之間的完全自動化雙向同步。
* **版本控制:**

   * [!DNL Experience Manager] 只有在檔案源自以下來源時，才會更新時建立資產的版本： [!DNL Experience Manager] 並在該處更新。
   * [!DNL Creative Cloud] Assets提供自己的 [版本設定功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 此更新針對進行中工作更新（基本上會儲存更新最多10天）

* **空間限制：** 交換的檔案大小與磁碟區受特定的 [Creative Cloud資產配額](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 適用於創意使用者（視訂閱層級而定），檔案大小上限為5 GB。 此外，空間受到組織在Adobe Marketing Cloud Assets核心服務中的資產配額限制。

* **空間需求：** 共用資料夾中的檔案也需要實際儲存在 [!DNL Experience Manager] 然後在 [!DNL Creative Cloud] 帳戶，具有快取復本於 [!DNL Marketing Cloud Assets] 核心服務。
* **網路與頻寬：** 共用資料夾中的檔案和所有更新需要透過網路在系統之間傳輸。 您應確保僅共用相關檔案和更新。
* **資料夾型別**：共用 [!DNL Assets] 型別的資料夾 `sling:OrderedFolder`，不支援在中共用的內容 [!DNL Adobe Marketing Cloud]. 如果您想要共用資料夾，請在中建立資料夾時 [!DNL Assets]，請勿選取 [!UICONTROL 已訂購] 選項。

## 最佳實務 {#best-practices}

運用「 」的最佳實務 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用包括：

* **磁碟區考量：** [!DNL Experience Manager] 和 [!DNL Creative Cloud] 「資料夾共用」應該用於共用較少量檔案，例如，與特定促銷活動或活動相關的檔案。 若要共用大型資產集（如組織中的所有已核准資產），請使用其他分配方法(例如 [!DNL Assets Brand Portal])或 [!DNL Experience Manager] 案頭應用程式。
* **避免共用深層階層：** 共用會遞回運作，不允許選擇性取消共用。 通常，只有沒有子資料夾或具有非常淺層階層（如1個子資料夾層級）的資料夾才應該考慮共用。
* **分開資料夾進行單向共用：** 應該使用個別資料夾來共用來自的最後資產 [!DNL Assets] 至 [!DNL Creative Cloud] 檔案，並用於從共用創意就緒資產 [!DNL Creative Cloud] 檔案至 [!DNL Assets]. 再加上這些資料夾的命名慣例，可為您建立更易於瞭解的工作環境 [!DNL Assets] 和 [!DNL Creative Cloud] 使用者相同。
* **避免在共用資料夾中使用WIP：** 共用資料夾不應用於進行中的工作 — 在Creative Cloud檔案中使用單獨的資料夾來執行需要經常變更檔案的工作。
* **在共用資料夾之外開始新工作：** 新設計（創意檔案）應在Creative Cloud檔案的個別WIP資料夾中開始，且當它們準備就緒可與共用時 [!DNL Assets] 使用者，應將他們移動或儲存至共用資料夾。
* **簡化共用結構：** 若要更易於管理的作業設定，請考慮簡化共用結構。 與其與所有創意使用者共用， [!DNL Assets] 資料夾僅能和團隊代表共用，例如創意總監或團隊經理。 創意方面的經理將收到最終資產、決定工作指派，然後讓設計人員在其自己的Creative Cloud帳戶中處理WIP資產。 他們可以使用Creative Cloud共同作業功能來協調工作，最後選取並放置準備共用回的資產 [!DNL Assets] 至其創意就緒的共用資料夾。

下圖說明根據現有最終資產建立新設計的設定範例，該資產來自 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
