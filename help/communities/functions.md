---
title: 社区功能
seo-title: Community Functions
description: 瞭解如何存取社群功能主控台
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 6%

---

# 社区功能{#community-functions}

社群體驗中預期的功能型別眾所周知。 社群功能可作為社群功能使用。 基本上，這些頁面是預先編排的一或多個頁面，用於實作社群功能，而不僅是在作者模式下將元件新增至頁面。 它們是用來定義 [社群網站範本](/help/communities/sites.md) 社群網站所在位置 [已建立](/help/communities/sites-console.md).

建立社群網站後，可以使用標準將內容新增到產生的頁面 [AEM製作模式](/help/sites-authoring/editing-content.md). 如社群功能主控台所示，可使用各種社群功能。

>[!NOTE]
>
>用於建立的控制檯 [社群網站](/help/communities/sites-console.md)， [社群網站範本](/help/communities/sites.md)， [社群群組範本](/help/communities/tools-groups.md)、和 [社群功能](/help/communities/functions.md) 僅供作者環境使用。

## 社群功能主控台 {#community-functions-console}

若要存取作者環境中的社群功能主控台：

* 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 社群功能]**.

![社群功能](assets/community-functions.png)

## 預先建立的函式 {#pre-built-functions}

以下簡述AEM Communities所提供的功能。 每個函式都包含一或多個AEM頁面，這些頁面包含相互連線並構成功能的Communities元件，可輕鬆整合至 [社群網站範本](/help/communities/sites.md).

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。

### 標題和URL設定 {#title-and-url-settings}

**標題** 和 **URL** 是所有社群功能通用的屬性。

將社群功能新增至社群網站範本或新增至 [修改](/help/communities/sites-console.md#modifying-site-properties) 社群網站的結構中，會開啟函式的對話方塊，以便設定標題和URL。

#### 配置功能详细信息 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **标题**

   (*必填*)顯示在網站功能選單中的文字

* **URL**

   (*必填*)用來產生URI的名稱。 名稱必須符合 [命名慣例](/help/sites-developing/naming-conventions.md) 由AEM和JCR所強制。

例如，使用從以下專案建立的網站： [快速入門](/help/communities/getting-started.md) 教學課程，如果

* 標題=網頁
* URL =頁面

接著，頁面的URL會是https://localhost:4503/content/sites/engage/en/page.html

而頁面的功能表連結會顯示為：

![engage-page](assets/engage-page.png)

### 活动流功能 {#activity-stream-function}

活動資料流函式是具有 [活動資料流元件](/help/communities/activities.md) 已選取所有檢視（所有活動、使用者活動及以下專案）。 另請參閱 [Activity Stream Essentials](/help/communities/essentials-activities.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

#### 配置功能详细信息 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [標題和URL設定](#title-and-url-settings)

* **显示“我的活动”视图**

   如果選取，「活動」頁面會包含標籤，該標籤會根據目前成員在社群內產生的活動來篩選活動。 預設值已選取。

* **显示“全部活动”视图**

   如果選取，「活動」頁面會包含標籤，其中包含目前成員有權存取的社群內產生的所有活動。 預設值已選取。

* **显示“新闻信息源”视图**

   如果選取，「活動」頁面會包含一個索引標籤，該索引標籤會根據目前成員所關注的活動進行篩選。 預設值已選取。

### 博客功能 {#blog-function}

部落格功能是具有 [部落格元件](/help/communities/blog-feature.md) 設定，用於標籤、檔案上傳、追蹤、成員自我編輯、投票及稽核。 另請參閱 [部落格要點](/help/communities/blog-developer-basics.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允许拥有权限的成员**

   如果選取，則部落格僅允許擁有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許建立所有社群成員。 「預設」已取消選取。

* **允许文件上传**

   如果選取，部落格會包含成員上傳檔案的功能。 預設值已選取。

* **允许主题回复**

   如果未選取，部落格會允許文章的回覆（評論），但不允許評論的回覆。 預設值已選取。

* **允许专题内容**

   如果選取，會將部落格識別為 [精選內容](/help/communities/featured.md). 預設值已選取。

### 日历功能 {#calendar-function}

行事曆功能是具有 [行事曆元件](/help/communities/calendar.md) 設定為允許標籤。 另請參閱 [行事曆要點](/help/communities/calendar-basics-for-developers.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

![calendar-details](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允许固定**

   如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設值已選取。

* **允许拥有权限的成员**

   如果選取，則部落格僅允許擁有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許建立所有社群成員。 「預設」已取消選取。

* **允许文件上传**

   如果選取，部落格會包含成員上傳檔案的功能。 預設值已選取。

* **允许主题回复**

   如果未選取，部落格會允許文章的回覆（評論），但不允許評論的回覆。 預設值已選取。

* **允许专题内容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 預設值已選取。

### 精選內容功能 {#featured-content-function}

精選內容功能是具有 [主要內容元件](/help/communities/featured.md) 已設定為允許新增和刪除註解。

每個元件可允許或不允許具備功能內容的能力(請參閱 [部落格功能](#blog-function)， [行事曆功能](#calendar-function)， [論壇功能](#forum-function)， [創意力功能](#ideation-function)、和 [QnA函式](#qna-function))。

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 文件库功能 {#file-library-function}

檔案庫函式是具有 [檔案庫元件](/help/communities/file-library.md) 已設定為允許新增和刪除註解。

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 论坛功能 {#forum-function}

論壇功能是具有「 」的頁面 [論壇元件](/help/communities/forum.md) 設定，用於標籤、檔案上傳、追蹤、成員自我編輯、投票及稽核。

新增至範本時，下列對話方塊隨即開啟：

#### 配置功能详细信息 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允许固定**

   如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設值已選取。

* **允许拥有权限的成员**

   如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 「預設」已取消選取。

* **允许文件上传**

   如果選取，論壇會包含成員上傳檔案的功能。 預設值已選取。

* **允许主题回复**

   如果未選取，論壇會允許對主題發表評論，但不允許回覆這些評論。 預設值已選取。

* **允许专题内容**

   如果選取，則會將元件的內容識別為 [精選內容](/help/communities/featured.md). 預設值已選取。

### 群組功能 {#groups-function}

>[!CAUTION]
>
>群組函式必須 *not* 成為 *第一個或唯一* 在網站結構或社群網站範本中運作。
>
>任何其他函式，例如 [頁面函式](#page-function)，必須先包含並列出。

群組功能可讓社群成員在發佈環境中的社群網站內建立子社群。

依據 [設定](/help/communities/sites-console.md#groupmanagement) 當Groups功能包含在 [社群網站範本](/help/communities/sites.md)，群組可以是公開或私人，而一或多個社群群組範本可設定為在實際建立社群群組時（例如從發佈環境）提供範本選擇。 A [社群群組範本](/help/communities/tools-groups.md) 指定為群組頁面（例如論壇和行事曆）建立的Communities功能。

建立社群群組時，會為新群組動態建立成員群組，成員可指派或加入該群組。 如需詳細資訊，請參閱 [管理使用者和使用者群組](/help/communities/users.md).

截至社群 [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack)，社群群組是在作者環境中使用 [社群網站的群組主控台](/help/communities/groups.md)、和，可在啟用時於發佈環境中建立。

新增至範本時，下列對話方塊隨即開啟：

![group-template-config](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **选择组模板**

   一個下拉式清單，可讓您選取一或多個啟用的群組範本，新社群群組的未來建立者（在發佈環境中）可從中進行選擇。

* **允许拥有权限的成员**

   如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 「預設」已取消選取。

* **允许发布创建**

   如果選取，經授權的社群成員可在發佈環境中建立群組。 如果取消選取，則只能從Communities Sites的「群組」主控台在作者環境中建立新群組（子社群）。
預設值已選取。

### 构思功能 {#ideation-function}

創意力功能是有一個頁面的頁面 [創意力元件](/help/communities/ideation-feature.md).

新增至範本時，會開啟下列對話方塊，其中指定預設的「標題」和URL名稱，以及範本的預設顯示設定：

![創意力功能](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允许拥有权限的成员**

   如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 「預設」已取消選取。

* **允许文件上传**

   如果選取，構思包括成員上傳檔案的能力。 預設值已選取。

* **允许主题回复**

   如果未選取，此想法允許對主題進行回覆（評論），但不允許對評論進行回覆。 預設值已選取。

* **允许专题内容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 預設值已選取。

### 排行榜功能 {#leaderboard-function}

排行榜功能是一頁有排行榜 [排行榜元件](/help/communities/enabling-leaderboard.md).

**注意**：排行榜元件需要進一步設定 *晚於* 社群網站是從包含排行榜功能的社群範本建立的。 指定排行榜元件的 [規則](/help/communities/enabling-leaderboard.md#rules-tab)，這取決於的設定 [評分和預算](/help/communities/implementing-scoring.md) 適用於社群網站。

新增至範本時，會開啟下列對話方塊，其中指定預設的「標題」和URL名稱，以及範本的預設顯示設定：

![排行榜對話方塊](assets/leaderboard-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **显示徽章**

   如果選取，則排行榜會包含徽章圖示欄。
「預設」已取消選取。

* **显示徽章名称**

   如果選取，則排行榜會包含徽章名稱的欄。
「預設」已取消選取。

* **显示头像**

   如果選取，成員的頭像影像會包含在排行榜中，位於其名稱連結至成員設定檔的旁邊。
「預設」已取消選取。

### 页面功能 {#page-function}

頁面功能會將空白頁面新增至社群網站，並與其連線至社群網站的功能：登入、功能表、通知、傳訊、主題設定和品牌推廣。 使用將內容新增至頁面 [標準AEM編寫模式](/help/sites-authoring/editing-content.md).

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 问题与解答功能 {#qna-function}

QnA函式是具有 [QnA元件](/help/communities/working-with-qna.md) 設定，用於標籤、檔案上傳、追蹤、成員自我編輯、投票及稽核。

新增至範本時，此設定允許限制擁有特殊許可權的成員：

![qna-dialog](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允许固定**

   如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設值已選取。

* **允许拥有权限的成员**

   如果選取，則QnA論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 「預設」已取消選取。

* **允许文件上传**

   如果選取，QnA論壇則包含成員上傳檔案的功能。 預設值已選取。

* **允许主题回复**

   如果未選取，QnA論壇允許對已張貼的問題進行評論（回答），但不允許對回答進行回覆。 預設值已選取。

* **允许专题内容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 預設值已選取。

## 创建社区功能 {#create-community-function}

透過選擇 `Create Community Function` 圖示加以檢視，並加以標示。 您可以建立以相同AEM Blueprint為基礎的多個函式，然後透過在作者編輯模式中開啟來唯一自訂。

![create-community-function](assets/create-community-function.png)

### 社区功能名称 {#community-function-name}

![function-name](assets/function-name.png)

在「社群功能名稱」面板上，會設定名稱、說明，以及功能是啟用還是停用：

* **社区功能名称**

   用於顯示和儲存的函式名稱。

* **社区功能描述**

   顯示的函式說明。

* **已停用/已啟用**

   控制函式是否可參照的切換開關。

### AEM Blueprint {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

於 `AEM Blueprint` 面板中，可以選取Blueprint，這是社群功能的基礎實作。

社群功能是包含一或多個頁面的迷你網站，已預先連線納入社群網站，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。 建立函式後，您可以 [開啟函式](#open-community-function) 在作者編輯模式中並自訂頁面或元件設定。

由於社群功能是以 [即時副本](/help/sites-administering/msm.md#live-copies) 的 [Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)，即可轉出對函式所進行的變更，此函式會影響到所有從 [社群網站範本](/help/communities/sites.md) 或 [社群群組範本](/help/communities/tools-groups.md) 其中包含函式。 也可以解除頁面與其上層Blueprint的關聯，以進行頁面層級的修改。

另請參閱 [多網站管理員](/help/sites-administering/msm.md).

### 缩略图 {#thumbnail}

![函式 — 縮圖](assets/funtion-thumbnail.png)

在「縮圖」面板上，可以上傳影像以顯示在 [社群功能主控台](#community-functions-console).

## 打开社区功能 {#open-community-function}

![開啟函式](assets/open-function.png)

選取 `Open Community Function` 圖示可進入作者編輯模式，以創作頁面內容並修改功能元件的設定。

### 設定元件 {#configuring-components}

社群功能會實作為AEM Blueprint的即時副本，其詳細資訊紀錄在 [多網站管理員](/help/sites-administering/msm.md).

您不僅可以編寫頁面內容，而且可以設定元件。

如果在已建立的社群網站的頁面上設定元件，則可能需要取消 [繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以設定元件。 完成設定後，應重新建立繼承。

如需設定詳細資訊，請造訪 [Communities元件](/help/communities/author-communities.md) 適用於作者。

## 编辑社区功能 {#edit-community-function}

![編輯函式](assets/edit-function.png)

選取 `Edit Community Function` 圖示來使用與相同的面板編輯函式的屬性 [建立社群功能](#create-community-function)，包括啟用或停用函式。
