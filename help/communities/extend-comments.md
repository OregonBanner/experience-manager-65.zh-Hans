---
title: 延伸註解元件
seo-title: Extend Comments Component
description: 擴充Comments元件以改變其外觀或特定用途的行為
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 延伸註解元件  {#extend-comments-component}

的意圖 [延伸](client-customize.md#extensions) 預設元件是針對特定用途變更元件的外觀或行為。

元件的路徑是唯一的，會將預設元件參照為超級資源型別。 與元件覆蓋的整個範圍相比，範圍是有限的，因此風險較低。

>[!NOTE]
>
>擴充 [重疊](client-customize.md#overlays) 不支援元件。

## 示例 {#example}

假設註解元件的標題必須以替代外觀顯示在AEM例項的一個網站上，而以預設顯示出現在另一個網站上。 取代覆蓋預設註解（會變更所有例項的註解元件）的更好的解決方案是確保有多個註解元件可用於各種網站。

若要實作此解決方案，請建立延伸（覆寫）現有元件的新元件，並修改Handlebars指令碼。 使用新註解的網站區域可使用延伸區域，而使用預設外觀的網站則不受影響。

註解元件實際上是構成註解系統的兩個元件之一。 因此，有兩個元件需要擴充： *評論* 和 *評論*. 要編輯的指令碼位於 *評論* 元件的 `header.hbs` 檔案，而父系 *評論* 元件（註解系統）是作者實際新增至頁面的專案。

若要擴充註解，您必須：

1. [建立元件](extend-create-components.md)
1. [新增註解至範例頁面](extend-sample-page.md)
1. [變更外觀](extend-alter-appearance.md)
