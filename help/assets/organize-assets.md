---
title: 组织您的数字资产
description: 使用Experience Manager組織您的數位資產、影像、檔案、資料夾等。
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 2%

---

# 组织您的数字资产 {#organize-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Microsoft Office和PDF檔案的所有數位資產、中繼資料和內容都會經過擷取，並設為可搜尋。 搜尋可讓您對資產進行複雜的篩選，並完全遵循適當的許可權。 「數位資產管理」的中繼資料會詳細說明中繼資料。

[!DNL Experience Manager Assets] 支援多種組織內容的方式。 您可以使用資料夾以階層方式組織資料夾，也可以使用標籤，以無序、臨機方式組織資料夾。 使用者可以在DAM Asset Editor中編輯標籤，子資產、轉譯和中繼資料會顯示於此處。

## 組織資料夾中的資產 {#organize-using-folders}

組織資產的最基本方式是將這些資產儲存在資料夾中。 這類似於在本機檔案系統的資料夾中組織檔案。 如需有關如何建立和管理資料夾的詳細資訊，請參閱 [管理資產](manage-assets.md). 如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾中的檔案，可能會對這些資產的處理方式產生重大影響。 透過使用一致且適當的檔案和資料夾命名策略，搭配良好的中繼資料實務，您可以充份運用數位資產存放庫。

* 在大多數情況下，您的數位資產存放庫會持續成長。 因此，在內容建立週期早期，將中繼資料使用、資料夾結構和檔案命名正規化是很重要的。
* 僅使用資料夾為您的數位資產強制實施一致的儲存結構。 此一致性可協助您更好地處理和管理資產。 例如，將資產放在以下型別的資料夾中可以幫助您使用適當的 [用於資產處理的設定檔](processing-profiles.md)：

   * **開發資料夾**：包含您目前正在處理的數位資產。
   * **使用者端資料夾**：包含以使用者端或專案名稱為基礎的數位資產。
   * **主要資料夾**：包含原始的數位資產。
   * **節目資料夾**：包含原始數位資產的轉譯和復本。
   * **檔案大小資料夾**：包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **暫存資料夾**：包含已準備好在您的網站上即時發佈的數位資產。
   * **MIME型別資料夾**：包含專屬於MIME型別的數位資產，例如影像、檔案和多媒體。
   * **封存資料夾**：包含淘汰的數位資產。
   * **以日期為基礎的資料夾**：包含以建立日期或上次修改日期為基礎的數位資產。

* 建立不太可能變更的資料夾目錄，讓任何自訂或自動化功能繼續運作。 例如，指派的處理設定檔可繼續運作。
* 如果資產已發佈，則您可使用 [!DNL Experience Manager] 若要將資產移至另一個檔案夾，並從其新位置重新發佈，仍可使用原始已發佈資產位置以及新重新發佈的資產。 然而，原始發佈的資產為 *遺失* 至 [!DNL Experience Manager] 和無法取消發佈。 因此，最佳實務是先取消發佈資產，然後將其移至其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

使用標籤作為中繼資料，您可以輕鬆搜尋資產、使用搜尋結果建立集合、提升部分資產的搜尋排名，以及運用Adobe Sensei的AI演演算法來探索資產。

[!DNL Adobe Experience Manager Assets] 會使用自我學習演演算法來建立高度說明性的標籤，讓您只需按幾下滑鼠即可找到正確的資產。 智慧型標籤會使用我們的人工智慧和機器學習架構Adobe Sensei，這些架構可訓練您辨識標準標籤和業務特定標籤，並將其套用至影像。 智慧標籤也可以識別內容、個別字詞或片語，並自動將描述性標籤套用至資產

如需詳細資訊，請參閱下列文章：

* [關於Experience Manager中的標籤](/help/sites-authoring/tags.md)
* [編輯資產中繼資料](metadata.md)
* [Assets中的增強智慧標籤](enhanced-smart-tags.md)

## 組織為集合 {#organize-as-collections}

資產集合位於 [!DNL Experience Manager Assets]，您可以簡化使用者之間建立、編輯和共用資產的能力。 根據您使用收藏集的方式建立多種收藏集型別，包括包含資產、資料夾和收藏集的靜態參考清單的收藏集，以及根據搜尋條件提取資產的收藏集。  您也可以使用不同位置的資產建立集合，並與具有不同存取層級、檢視和編輯許可權的多個使用者共用這些集合。

如需詳細資訊，請參閱 [管理集合](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 組織您的資產以使用設定檔 {#organize-to-use-profiles}

處理設定檔包含 [!DNL Assets] 處理適用於上傳至預先定義資料夾之資產的命令。 設定檔可用來自動處理資料夾內容或最新上傳的資產。 您可以善用設定檔，以更妥善地組織您的資產。

將中繼資料使用、檔案命名和資料夾結構標準化，可確保隨著數位資產集區的成長，您可以更精確且一致地將處理設定檔套用至資料夾。

>[!MORELIKETHIS]
>
>* [用於處理中繼資料、影像和影片的設定檔](processing-profiles.md).
>* [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles).
>* [視訊設定檔](video-profiles.md).
>* [Dynamic Media影像設定檔](image-profiles.md).

