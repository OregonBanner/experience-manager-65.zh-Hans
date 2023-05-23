---
title: Analytics與外部提供者
seo-title: Analytics with External Providers
description: 瞭解使用外部提供者的Analytics。
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Analytics與外部提供者 {#analytics-with-external-providers}

Analytics可提供您如何使用網站的重要且有趣資訊。

各種現成的設定可用於與適當的服務整合，例如：

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

您也可以設定自己的例項 **一般Analytics代碼片段** 以定義新的服務組態。

然後會透過新增至網頁的小程式碼片段來收集資訊。 例如：

>[!CAUTION]
>
>指令碼不得包含在 `script` 標籤之間。

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

這類片段可讓您收集資料並產生報表。 實際收集的資料取決於提供者和實際使用的程式碼片段。 統計資料範例包括：

* 一段時間內有多少訪客
* 造訪了多少頁面
* 使用的搜尋字詞
* 登陸頁面

>[!CAUTION]
>
>Geometrixx-Outdoors示範網站已設定為將「頁面屬性」中提供的屬性附加至html原始程式碼(位於 `</html>` endtag) `js` 指令碼。
>
>如果您自己的 `/apps` 不要繼承自預設頁面元件( `/libs/foundation/components/page`)您（或您的開發人員）必須確認 `js` 包含指令碼，例如，透過包含 `cq/cloudserviceconfigs/components/servicescomponents`，或使用類似機制。
>
>若沒有此專案，任何服務（一般、Analytics、Target等）都無法運作。

## 使用通用程式碼片段建立新服務 {#creating-a-new-service-with-a-generic-snippet}

對於基本設定：

1. 開啟 **工具** 主控台。
1. 從左窗格展開 **Cloud Services設定**.
1. 按兩下 **一般Analytics程式碼片段** 若要開啟頁面：

   ![](assets/analytics_genericoverview.png)

1. 按一下+以使用對話方塊新增設定；至少指派名稱，例如google analytics：

   ![](assets/analytics_addconfig.png)

1. 按一下 **建立**，會立即開啟程式碼片段對話方塊 — 將適當的javascript程式碼片段貼入欄位：

   ![](assets/analytics_snippet.png)

1. 按一下 **確定** 以儲存。

## 在頁面上使用您的新服務 {#using-your-new-service-on-pages}

建立服務組態後，您現在需要設定必要的頁面才能使用它：

1. 導覽至頁面。
1. 開啟 **頁面屬性** 從sidekick，然後 **Cloud Services** 標籤。
1. 按一下 **新增服務**，然後選取所需的服務；例如 **一般Analytics程式碼片段**：

   ![](assets/analytics_selectservice.png)

1. 按一下 **確定** 以儲存。
1. 您將會返回 **Cloud Services** 標籤。 此 **一般Analytics程式碼片段** 現在會與訊息一併列出 `Configuration reference missing`. 使用下拉式清單來選取您的特定服務執行個體，例如google-analytics：

   ![](assets/analytics_selectspecificservice.png)

1. 按一下 **確定** 以儲存。

   如果您檢視頁面的「頁面來源」，現在可以看到程式碼片段。

   經過適當的時間段後，您將能夠檢視已收集的統計資料。

   >[!NOTE]
   >
   >如果設定附加至具有子頁面的頁面，則服務也會被這些頁面繼承。
