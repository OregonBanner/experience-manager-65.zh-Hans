---
title: 設計與設計工具
seo-title: Designs and the Designer
description: 您將需要為您的網站建立設計，而且在AEM中，您需使用設計工具來建立設計
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 設計與設計工具{#designs-and-the-designer}

>[!CAUTION]
>
>本文會說明如何根據傳統UI建立網站。 Adobe建議您為網站運用最新的AEM技術，如文章所述 [開發AEM Sites快速入門](/help/sites-developing/getting-started.md).

設計工具是用來建立您網站的設計，使用 [傳統UI](/help/release-notes/touch-ui-features-status.md) 在AEM中。

>[!NOTE]
>
>如需網頁協助工具的詳細資訊，請參閱 [AEM與網頁協助工具准則](/help/managing/web-accessibility.md).

## 使用設計工具 {#using-the-designer}

您的設計可在以下位置定義： **設計** 部分 **工具** 標籤：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此處建立儲存設計所需的結構，然後上傳所需的階層式樣式表和影像。

設計儲存在 `/apps/<your-project>`. 指定網站使用之設計的路徑，使用 `cq:designPath` 的屬性 `jcr:content` 節點。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在設計模式中，對頁面所做的所有變更都會保留在網站的設計節點下，並自動套用至具有相同設計的所有頁面。

## 您將需要什麼 {#what-you-will-need}

若要實現您的設計，您需要：

**CSS**  — 階層式樣式表可定義頁面上特定區域的格式。
**影像**  — 您用於背景、按鈕等功能的任何影像。

### 設計網站時的注意事項 {#considerations-when-designing-your-website}

開發網站時，強烈建議將影像和CSS檔案儲存在 `/apps/<your-project>` 如此一來，您就可以根據目前的設計參考資源，如下列程式碼片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上述範例提供幾項優點：

* 使用不同設計路徑的每個網站元件可能有不同的外觀/感覺。
* 網站的重新設計只需從將設計路徑指向網站根目錄中的不同節點即可 `design/v1` 至 `design/v2.`

* `/etc/designs` 和 `/content` 是瀏覽器看到的唯一外部URL，可保護您免受外部使用者對您網站下的內容產生好奇心的困擾 `/apps` 樹狀結構。 上述URL的好處也可協助您的系統管理員設定更好的安全性，因為您將資產公開限制在幾個不同的位置。
