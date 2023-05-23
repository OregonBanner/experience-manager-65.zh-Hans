---
title: 稽核主控台
seo-title: Moderation Console
description: 如何存取稽核主控台
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 4%

---

# 稽核主控台 {#moderation-console}

在AEM Communities中，大量 [社群內容的稽核](/help/communities/moderate-ugc.md) 管理員和社群版主（指派為版主的受信任社群成員）可以在作者和發佈環境中使用。

管理員和社群版主也可執行 [內文中稽核](/help/communities/in-context.md) 在發佈環境中。

所有功能 [社群網站](/help/communities/sites-console.md) 是 `Administration` 以管理許可權登入的使用者可用的功能表專案。 此 `Administration` 連結可讓您存取稽核主控台。

在「稽核」控制檯中，管理員和社群版主將可存取其有權稽核的所有使用者產生內容(UGC)。 如果允許稽核多個網站，則可檢視所有網站的貼文，或依選取的社群網站進行篩選。

如需更多詳細資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).

「協調」主控台支援：

* 正在大量執行稽核工作。
* 正在搜尋UGC。
* 檢視UGC詳細資料。
* 檢視UGC作者詳細資訊。

只有在以管理員身分登入，或成員具有 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`，可以執行稽核任務。

## 發佈環境存取權 {#publish-environment-access}

若要從已發佈的社群網站存取版主主控台，需透過管理連結（當社群版主登入時便會顯示）進行。

![publishweretail](assets/publishweretail.png)

選取「管理」連結後，「協調」主控台隨即出現：

![moderation-console-publish](assets/moderation-console-publish.png)

## 作者環境存取權 {#author-environment-access}

在製作環境中，前往「協調」主控台

* 在全域導覽中選取 **[!UICONTROL Communities]** > **[!UICONTROL 稽核]**.

只有在以管理員身分登入，或以具有下列身分的成員身分登入 [版主許可權](/help/communities/in-context.md#identifyingtrustedmembers)，即可執行稽核任務。 顯示的唯一社群內容是允許登入成員稽核的內容。

>[!NOTE]
>
>只有當所選的SRP實作通用存放區時，發佈環境的UGC才對作者可見。 例如，預設的儲存體為JSRP，這不是製作和發佈的常見儲存體。 另請參閱 [社群內容儲存](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Moderation Console UI {#moderation-console-ui}

將左側導覽邊欄放開（顯示在作者上，但不顯示在發佈上），稽核UI有下列主要區域：

* **[頂端導覽列](#top-navigation-bar)**
* **[工具栏](#toolbar)**
* **[內容區域](#content-area)**

### 頂端導覽列 {#top-navigation-bar}

所有主控台的頂端導覽列都是固定的。 如需詳細資訊，請參閱 [基本處理](/help/sites-authoring/basic-handling.md).

### 工具栏 {#toolbar}

位於頂端導覽列下方的工具列在左側提供下列切換開關：

* [篩選邊欄](/help/communities/moderation.md#filterrail)
開啟邊欄，您可在邊欄上選取要篩選內容的屬性。

位於頂端導覽列下方的工具列在左側提供下列切換開關：

![切換切換](assets/toggleswitch.png)

[篩選邊欄](/help/communities/moderation.md#filterrail)
在選取「搜尋」時開啟邊欄，可讓您選取要篩選內容的屬性。

![篩選邊欄](assets/filterrail.png)

### 内容区域 {#content-area}

內容區域包含已發佈UGC的資訊：

* UGC已發佈
* 成員名稱
* 成員頭像
* 貼文的位置。
* 發佈時間。
* 回覆貼文的次數。
* [情緒](/help/communities/moderate-ugc.md#sentiment) 與貼文相關聯
* 如果核准，會顯示核取記號。
* 如果有附件，則會顯示回形針。

>[!NOTE]
> 
>內容區域具有 *無限捲動*，這表示可讓您繼續捲動，直到內容結束為止。 即使捲動時，工具列仍會維持在內容區域上方的固定可見位置。

### 篩選邊欄 {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

側面板圖示會開啟篩選邊欄。 篩選器邊欄會顯示在內容區域的左側，提供不同的篩選器，每個篩選器都會立即影響內容區域中顯示的參考UGC。

每個類別中的篩選器包括 **或**&#39;d在一起，不同類別中的篩選器為 **和**&#39;d在一起。

例如，如果您同時核取兩者 **問題** 和 **答案**，您會看到以下其中一種內容： **問題** *或* 一個 **答案**.

不過，如果您檢查 **問題** 和 **擱置中**，您只會看到 **問題** 和 **擱置中**.

>[!NOTE]
>
>社群版主可將版主主控台UI上的預先定義篩選器加入書籤。 由於這些篩選器會附加到URL的結尾（作為查詢字串引數），版主稍後可以返回書籤化篩選器，也可以共用這些連結。

![搜尋圖示](assets/searchicon.png)

開啟篩選邊欄時，「搜尋」圖示會切換關閉的側面板。 不過，若要關閉篩選邊欄並僅檢視使用者產生的內容，請按一下「搜尋」圖示並選取「僅限內容」選項。

#### 内容路径 {#content-path}

內容路徑將顯示的參考UGC限製為放置在指定內容存放庫中的帖子。

![content-path](assets/content-path.png)

#### 文本搜索 {#text-search}

文字搜尋會將參照的UGC顯示限製為包含輸入文字的貼文。

![text-search](assets/text-search.png)

#### 站点 {#site}

網站將參照的UGC顯示限製為所選社群網站的貼文。 如果未核取任何網站，則會顯示UGC的所有參考。

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>管理員存取大量仲裁控制檯時，所有對UGC的參照皆會顯示，包括未使用建立的網站 [網站建立精靈](/help/communities/sites-console.md)，例如Geometrixx範例。
>
>當信任的社群成員在發佈時存取大量稽核主控台時，則只會顯示為該成員有權稽核的社群網站所建立的UGC參考，並且可以使用網站篩選條件進行篩選。

#### 内容类型 {#content-type}

內容型別將引用的UGC顯示限製為所選資源型別的帖子。 可選取下列一或多個型別。 如果未選取任何型別，則會顯示所有型別。

* **注释**
* **论坛 - 主题**
* **论坛回复**
* **问题与解答 - 问题**
* **问题与解答 - 回答**
* **博客文章**
* **博客评论**
* **日历事件**
* **日历注释**
* **文件库文件夹**
* **文件库文档**
* **构思**
* **构思评论**

![內容型別](assets/content-types.png)

#### 其他內容型別 {#additional-content-types}

若要新增其他要篩選的資源：

* 以管理員身分登入您的作者執行個體。
* 開啟 [網頁主控台](https://localhost:4502/system/console/configMgr).
* 尋找 `AEM Communities Moderation Dashboard Filters`.
* 選取要在編輯模式下開啟的設定。
* 輸入要篩選之元件的ResourceType：

   * 例如，若要篩選包含的投票元件，請輸入：

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 选择保存。
* 重新整理Communities - Moderation主控台。

結果會針對以下專案產生新的可選取篩選器 `Voting` 在 `Content Type` 篩選群組。

選取該篩選器後，控制面板的內容會顯示符合輸入之任何ResourceTypes的UGC。

#### 状态 {#status}

狀態會將參照的UGC限製為所選取狀態的貼文，這些狀態可能是「擱置中」、「已核准」、「已拒絕」或「已關閉」等其中一或多項，以及草稿或部落格排程，以及QnA問題的已回答或未回答。 如果未選取任何專案，則會顯示所有專案。

>[!NOTE]
>
>如果只選取「未回答」狀態，版主將會看到所有內容（針對所有內容型別），但已回答的問題除外。 這是因為在未回答的問題和其他內容（例如論壇主題、部落格或評論）的情況下，負責已回答問題的屬性並不存在。

![狀態](assets/statuses.png)

#### 标记 {#flagging}

標幟會將參照的UGC顯示限製為已標幟或隱藏的貼文。

標籤內容後，該內容會一直保持已標籤狀態，直到您透過選取 **標幟** 按鈕一次。 請注意，沒有標幟層級，例如重要或後續追蹤。

![標幟](assets/flagging.png)

#### 成员 {#members}

成員限制所顯示參考UGC顯示到按輸入成員名稱張貼的UGC。

![成员](assets/members.png)

#### 发布于前一 {#posted-in-the-last}

公佈於上次將參照的UGC顯示限製為過去一小時、一天、周、月或年所做的公佈。

![最後張貼](assets/posted-last.png)

#### 情绪 {#sentiment}

[情緒](/help/communities/moderate-ugc.md#sentiment) 將參考的UGC顯示限制在具有正面、負面或中性情緒值的貼文中。

![情緒](assets/sentiment.png)

## 自訂篩選器 {#custom-filters}

除了中的現成可用篩選器 [篩選邊欄](/help/communities/moderation.md#ootbfilters)，可將中繼資料上的其他自訂篩選器新增至稽核UI。 開發人員可使用Github中的範常式式碼來擴充現有的稽核UI篩選器。

![custom-tag-filter](assets/custom-tag-filter.png)

此 [範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) 在Github上實作標籤篩選，以根據特定標籤是否已套用至使用者產生的內容來篩選UGC清單。 您可以遵循範常式式碼，並為其他類似的UGC中繼資料欄位建立類似篩選器。

若要安裝「標籤」篩選器的範例：

1. 在AEM Author上開啟套件管理器(`https://[aem-author]:4502/crx/packmgr/index.jsp`)例項和AEM發佈(`https://[aem-publish]:4503/crx/packmgr/index.jsp`)例項。
1. 建置套件 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 從Github程式碼安裝，並安裝及啟用相同程式。
1. 開啟AEM Author上的套件組合主控台( `https://[aem-author]:4502/system/console/bundles`)例項和AEM發佈( `https://[aem-publish]:4503/system/console/bundles`)例項。
1. 建置套件(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`)，並安裝及啟用相同專案。
1. 前往 **/apps/social/moderation/facets** AEM作者上的節點(`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)和AEM Publish (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)例項。
1. 新增技術使用者 **communities-utility-reader** 替換為 `jcr:read` 許可權。

若要在現有社群網站上公開自訂篩選器：

1. 編輯 `Clientlibs` 現有的稽核頁面 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 新增類別 `cq.social.hbs.moderation.v2.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 設定為新元件 `sling:resourceType = social/moderation/v2/filters.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 設定為新元件 `sling:resourceType = social/moderation/v2/modcontainer`.

## 稽核動作 {#moderation-actions}

[稽核動作](/help/communities/moderate-ugc.md#moderation-actions) 可以在內容區域或檢視內容詳細資料時，對一個或多個選取專案執行。

若要大量稽核貼文，請在內容區域中按一下選取(![選取](assets/selecticon.png))圖示，當滑鼠游標停留在張貼上（案頭）或按住手指並按住張貼（行動裝置）時，此圖示就會出現。 這樣，您就可以進入多選模式，現在只需按一下即可選取後續要大量稽核的貼文。 使用工具列上顯示的按鈕，對選取的貼文執行稽核動作。 所有動作都會提示進行確認。

若要稽核內容區域中的單一貼文，請使用滑鼠（桌上型）將滑鼠游標停留在貼文上，或按住貼文（行動型）上的手指，讓按鈕顯示在貼文上。 對單一內容詳細資料執行操作時，只有刪除動作會提示您確認。

### 稽核多個貼文 {#moderating-multiple-posts}

按一下「 」，進入大量選取模式 `Select` 貼文圖示：

![select-icon](assets/select-icon.png)

若要結束大量選取模式，請選取工具列上的取消(x)圖示：

可對多個貼文執行的稽核動作包括：

* 拒绝
* 删除
* 關閉/重新開啟貼文

只有在選取了多個貼文時，才會在工具列上顯示允許這些動作的圖示。

![bulkmoderate](assets/bulkmoderate.png)

### 稽核單一貼文 {#moderating-a-single-post}

在單一選取模式中，可以：

* 選取使用者名稱以檢視使用者詳細資訊。
* 選取貼文的連結，檢視內容中的貼文。
* [回复](#reply)
* [允许](#allow)
* [拒绝](#deny)
* [删除](#delete)
* [关闭](#close)
* 檢視 [稽核歷史記錄](#moderation-history)
* [查看详细信息](#viewdetails)

「協調動作」圖示上方卡片檢視中顯示的是貼文的文字，下方則是表示下列內容的資料：

* 如果有回覆，則會在回覆前加上回複數。
* 如果已標幟。
* 是否已核准。
* 發佈UGC的時間。

![singleselectmode](assets/singleselectmode.png)

#### 回复 {#reply}

![回覆](assets/reply.png)

處理單一貼文時，如果UGC型別支援回覆，且已設定為允許回覆，則會顯示回覆圖示。

#### 允许 {#allow}

![允许](assets/allow.png)

使用單一貼文時，當貼文被標幟或拒絕時，允許圖示就會出現。 如果已標幟，選取「允許」將清除所有標幟。

#### 拒绝 {#deny}

![拒绝](assets/deny.png)

此 **拒絕** 「調節」動作僅適用於已調節的內容，且不會出現在未調節的內容上（多選模式除外）。

未稽核的內容一律會獲得核准。

稽核的內容最初會進入「擱置中」狀態，之後可以修改為核准或拒絕。

離開擱置狀態的內容永遠無法回到擱置狀態。 標示為已核准或拒絕的內容可隨時變更為其他狀態。

#### 删除 {#delete}

![删除](assets/delete.png)

在單一選取或大量模式中，您可以選取專案並將其刪除。 刪除動作會產生確認對話方塊。 刪除後，這些專案會立即從內容區域消失。 **刪除UGC後，就會從存放庫中永久移除該UGC，且之後無法擷取**.

#### 关闭 {#close}

![关闭](assets/close.png)

使用單一貼文時，如果UGC型別支援防止該資源出現更多貼文的功能，則會顯示關閉圖示。

#### 审核历史记录 {#moderation-history}

![稽核](assets/moderation.png)

處理單一貼文時，將滑鼠懸停在單一貼文上方時，會出現「稽核歷史記錄」圖示。 選取圖示會顯示一個窗格，其中包含針對UGC貼文採取的動作歷史記錄。

若要返回多個UGC貼文的內容區域顯示，請選取檢視詳細資料窗格右上角的X。

例如：

![moderation-history](assets/moderation-history.png)

#### 查看详细信息 {#view-detail}

![檢視](assets/view.png)

使用單一貼文時，您可以在詳細模式中開啟UGC，以檢視更多詳細資訊。

若要這麼做，請將滑鼠指標停留在貼文上以顯示 `View Detail` 圖示並選取，以顯示包含貼文詳細資訊的面板。

若要返回多個UGC貼文的內容區域顯示，請選取檢視詳細資料窗格右上角的X。

例如：

![view1](assets/view1.png)
