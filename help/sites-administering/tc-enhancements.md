---
title: 翻譯增強功能
seo-title: Translation Enhancements
description: AEM中的翻譯增強功能。
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 28%

---

# 翻譯增強功能{#translation-enhancements}

此頁面提供AEM翻譯管理功能的增量增強和細化。

## 翻譯專案自動化 {#translation-project-automation}

已新增選項，以改善使用翻譯專案的生產力，例如自動提升和刪除翻譯啟動，以及排程翻譯專案的重複執行。

1. 在您的翻譯專案中，按一下或點選「 」底部的省略符號 **翻譯摘要** 圖磚。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至 **進階** 標籤。 在底部，您可以選取 **自動提升翻譯啟動**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. 或者，您可以選擇在收到翻譯內容後，是否應該自動提升和刪除翻譯啟動。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 若要選取翻譯專案的循環執行，請選取頻率，下拉式清單位於 **重複翻譯**. 循環專案執行將在指定的間隔內自動建立和執行翻譯工作。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多語言翻譯專案 {#multilingual-translation-projects}

您可以在翻譯專案中設定多種目標語言，以減少建立的翻譯專案總數。

1. 在您的翻譯專案中，按一下或點選 **翻譯摘要** 圖磚。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切換至 **進階** 標籤。 您可以在下列位置新增多種語言 **目標語言**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果您要透過Sites中的參考邊欄啟動翻譯，請新增您的語言並選取 **建立多語言翻譯專案**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 翻譯工作將在專案中針對每種目標語言建立。 您可以在專案中逐一啟動，或在「專案管理員」中全域執行專案來一次啟動。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻譯記憶庫更新 {#translation-memory-updates}

翻译内容的手动编辑可以同步回翻译管理系统 (TMS)，以训练其翻译记忆。

1. 在網站主控台中，更新翻譯頁面中的文字內容後，選取 **更新翻譯記憶庫**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 列表视图显示每个已编辑的文本组件的源和翻译的并排比较。選取應將哪些翻譯更新同步至翻譯記憶庫，然後選取 **更新記憶體**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM 会更新已配置的 TMS 的翻译记忆中现有字符串的翻译。

* 该操作会更新已配置的 TMS 的翻译记忆中现有字符串的翻译。
* 它不会创建新的翻译工作。
* 它通过 AEM 翻译 API（见下文）将翻译发送回 TMS。

要使用此功能：

* TMS 必须配置为可与 AEM 一起使用。
* 连接器需要执行该方法[`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html)。
   * 此方法中的代码确定翻译记忆更新请求的情况。
   * AEM 翻译框架通过实施该方法来将字符串值对（原始和更新的翻译）发送回 TMS。

对于使用专有翻译记忆的情况，可以拦截翻译记忆更新并将其发送到自定义目标。

## 多个级别的语言副本 {#language-copies-on-multiple-levels}

語言根現在可以在節點下分組（例如按區域），同時仍被識別為語言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>仅允许一个级别。例如，下列專案不會允許&quot;es&quot;頁面解析為語言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>此 `es` 無法偵測到語言副本，因為它位於2個層級（美洲/中美洲）之外 `en` 節點。

>[!NOTE]
>
>語言根可以有任何頁面名稱，而不僅僅是語言的ISO程式碼。 AEM一律會先檢查路徑和名稱，但如果頁面名稱未識別語言，AEM會檢查頁面的cq：language屬性以取得語言識別。

## 翻譯狀態報告 {#translation-status-reporting}

現在，您可以在網站清單檢視中選取屬性，以顯示頁面是否已翻譯、正在翻譯或尚未翻譯。 若要顯示它：

1. 在Sites中，切換至 **清單檢視。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 按一下或點選 **檢視設定**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Check **已翻譯** 核取方塊於 **翻譯** 然後點選/按一下 **更新**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您現在可以看到 **已翻譯** 欄，其中顯示頁面的翻譯狀態。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
