---
title: 覆蓋社群元件
seo-title: Overlay communities components
description: 覆蓋社群元件
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 覆蓋社群元件 {#overlay-communities-components}

的意圖 [覆蓋](/help/communities/client-customize.md#overlays) 預設元件是全域變更元件的外觀或行為，適用於該元件的所有相對參照。 在/libs資料夾中搜尋之前，這會仰賴sling的性質解析至/apps資料夾。 因此，元件的路徑與預設元件的路徑相同，不同之處在於它位在/apps資料夾中，而非/libs資料夾中。

## 示例 {#example}

**覆蓋註解元件**

假設您想要修改註解功能，使其符合您網站的設計，方法是變更註解標題使其不再顯示任何註解的頭像。 隱藏頭像的解決方案是使用CSS，或如這裡所述，覆蓋apps資料夾中的header.jsp，這樣包含頭像的HTML就不會傳送給使用者端。

若要覆蓋註解，您需要：

1. [評論頁面](/help/communities/overlay-create-comments-page.md)
1. [建立節點](/help/communities/overlay-create-nodes.md)
1. [變更外觀](/help/communities/overlay-alter-appearance.md)

**覆蓋通知電子郵件**

假設您要自訂電子郵件通知的訊息，您可以透過以下方式進行 [覆蓋](/help/communities/client-customize.md#overlays) 範本位於 **/libs/settings/community/templates/email/html**.

例如，若要修改提及電子郵件通知（針對建立ugc的特定社群元件），請新增 **如果** 動詞的條件 **提及** 在您已啟用的元件範本中 **@mentions** 支援。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

若要修改電子郵件通知範本以新@mention部落格評論，請將現成可用的範本放置於： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
