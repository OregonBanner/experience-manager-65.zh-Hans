---
title: 體驗已發佈的網站
seo-title: Experience the Published Site
description: 瀏覽至已發佈的網站
seo-description: Browse to a published site
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---

# 體驗已發佈的網站 {#experience-the-published-site}

## 在發佈時瀏覽至新網站 {#browse-to-new-site-on-publish}

現在新建立的Communities網站已發佈，請瀏覽至建立網站時顯示的URL，但在發佈伺服器上，例如：

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 發佈URL = https://localhost:4503/content/sites/engage/en.html

為了將有關哪個成員已登入作者和發佈的混淆降至最低，建議對每個執行個體使用不同的瀏覽器。

網站訪客首次造訪已發佈的網站時，通常不會登入，且會匿名。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## 匿名網站訪客 {#anonymous-site-visitor}

匿名網站訪客在UI中看到以下內容：

* 網站標題（快速入門教學課程）
* 無設定檔連結
* 無訊息連結
* 無通知連結
* 搜索字段
* 登入連結
* 品牌橫幅
* 「參考網站範本」中包含之元件的功能表連結。

如果您選取各種連結，您會發現這些連結處於唯讀模式。

### 防止JCR上的匿名存取 {#prevent-anonymous-access-on-jcr}

但已知限制會透過jcr內容和json向匿名訪客公開社群網站內容 **允許匿名存取** 網站內容停用。 不過，此行為可使用Sling限製作為因應措施加以控制。

若要保護您的社群網站內容，防止匿名使用者透過jcr內容和json存取，請執行以下步驟：

1. 在AEM Author執行個體上，前往https:// hostname：port/editor.html/content/site/sitename.html。

   >[!NOTE]
   >
   >請勿前往當地語系化網站。

1. 前往 **頁面屬性**.

   ![page-properties](assets/page-properties.png)

1. 前往 **進階** 標籤。

1. 啟用 **驗證需求**.

   ![site-authentication](assets/site-authentication.png)

1. 新增登入頁面的路徑。 例如， **/content/......./GetStarted**.
1. 發佈頁面。

## 信任的社群成員 {#trusted-community-member}

此體驗假設 [艾倫·麥當勞](/help/communities/tutorials.md#demo-users) 已指派以下角色： [社群管理員和版主](/help/communities/create-site.md#roles). 如果沒有，請返回作者環境至 [修改網站設定](/help/communities/sites-console.md#modifying-site-properties) 並選取Aaron McDonald擔任社群管理員和版主。

在右上角，選取 `Log in`，並使用使用者名稱(aaron.mcdonald@mailinator.com)和密碼（密碼）簽署。 請注意，您可以使用Twitter或Facebook憑證登入。

![登入](assets/login.png)

以註冊的社群成員身分登入後，請注意下列選單專案，以便點選並探索您的社群網站：

* **設定檔** 選項可讓您檢視及編輯您的設定檔。
* [訊息](/help/communities/configure-messaging.md) 選項會將您導向直接傳訊區段，您可在其中執行以下操作：

   1. 檢視您已接收（收件匣）、已傳送（已傳送專案）及已刪除（垃圾桶）的直接訊息。
   1. 撰寫要傳送給個人和群組的新直接訊息。

* [通知](/help/communities/notifications.md) 選項會將您導向通知區段，您可以在其中檢視感興趣的事件並編輯通知設定。
* [管理](/help/communities/published-site.md#moderationlink) 若您擁有協調許可權，系統會將您導向AEM Communities協調頁面。

![adminscreen](assets/adminscreen.png)

請注意，「行事曆」頁面是首頁，因為選擇的參考網站範本首先包含「行事曆」功能，然後包含「活動資料流」功能、「論壇」功能等。 此結構可從 [網站範本](/help/communities/sites.md#edit-site-template) 主控台或在作者環境中修改網站屬性時：

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>如需Communities元件和功能的詳細資訊，請造訪：
>
>* [Communities元件](/help/communities/author-communities.md) （適用於作者）
>* [元件、函式和Feature Essentials](/help/communities/essentials.md) （適用於開發人員）


### 論壇連結 {#forum-link}

選取論壇連結，檢視基本論壇功能。

成員可以張貼新主題或遵循主題。

網站訪客可以檢視貼文，並以各種方式排序貼文。

![forumlink](assets/forumlink.png)

### 群組連結 {#groups-link}

由於Aaron是群組管理員，選取「群組」連結將允許Aaron透過選取群組範本、影像、群組（無論群組是公開或秘密）以及邀請成員來建立新的社群群組。

這是在發佈環境中建立群組的範例。

群組也可在作者環境中建立，並在作者環境的社群網站中管理([社群群組主控台](/help/communities/groups.md))。 體驗 [建立作者群組](/help/communities/nested-groups.md) 是本教學課程的下一節。

![grouplink](assets/grouplink.png)

建立參考群組：

1. 選取 **新增群組**
1. **設定索引標籤**

   * 组名称 : `Sports`
   * 描述 : `A parent group for various sporting groups`.
   * 组 URL 名称 : `sports`
   * 選取 `Open Group` （允許任何社群成員透過加入來參與）

1. **範本索引標籤**

   * 選取 `Reference Group` （在其結構中包含群組函式，以允許巢狀群組）

1. 選取 **建立群組**

   ![creategroup](assets/creategroup.png)

建立新群組後， **選取新的運動群組** 以在其內建立兩個群組（巢狀）。 由於網站結構不能以群組功能開頭，在開啟「運動」群組後，必須選取「群組」連結：

![grouplink1](assets/grouplink1.png)

第二組連結，開頭為 `Blog`，屬於目前選取的群組 `Sports` 群組。 透過選取運動&#39; `Groups` 連結後，可在「運動」群組中巢狀內嵌兩個群組。

例如，新增兩個 `new groups`.

* 一個已命名 `Baseball`

   * 將其保留設定為 `Open Group` （必要成員資格）。
   * 在範本索引標籤上，選取 `Conversational Group`.

* 一個已命名 `Gymnastics`

   * 將其設定變更為 `Member Only Group` （限制成員資格）。
   * 在範本索引標籤上，選取 `Conversational Group`.

**通知**:

* 必須重新整理頁面才能顯示這兩個群組。
* 此範本有 *not* 包含「群組」功能，因此不可能進一步巢狀化群組。
* 對於作者， [群組主控台](/help/communities/groups.md) 提供第三個選擇 — a `Public Group` （選擇性會籍）。

建立兩個群組後，請選取「棒球」群組、開啟的群組，並注意其連結：

`Discussions` `What's New` `Members`

群組的連結會顯示在主要網站的連結下方，而結果會顯示如下：

![grouplink2](assets/grouplink2.png)

作者 — 使用管理許可權，瀏覽至 [社群群組主控台](/help/communities/members.md) 並將Weston McCall新增至 `Community Engage Gymnastics <uid> Members` 群組。

繼續發佈，以Aaron McDonald登出，並以匿名網站訪客檢視運動團體中的群組：

* 從首頁
* 選取 `Groups` 連結
* 選取 `Sports` 連結
* 選取運動&#39; `Groups` 連結

只會顯示棒球群組。

以Weston McCall (weston.mccall@dodgit.com /密碼)登入，並導覽至相同位置。 請注意，Weston能夠 `Join` 開啟 `Baseball` 群組和 `enter or Leave` 私人 `Gymnastics` 群組。

![grouplink3](assets/grouplink3.png)

### 網頁連結 {#web-page-link}

選取網頁連結，檢視網站所包含的基本網頁。 標準AEM編寫工具可用於在編寫環境中將內容新增到此頁面。

例如，前往 **作者** 執行個體，開啟 `engage` 中的資料夾 [社群網站主控台](/help/communities/sites-console.md)，選取 **開啟網站** 圖示以進入作者編輯模式。 然後選取預覽模式以選取 `Web Page` 連結，然後選取編輯模式以新增標題和文字元件。 最後，僅重新發佈頁面或整個網站。

![webpagelink](assets/webpagelink.png)

### 稽核連結 {#moderationlink}

當社群成員具有仲裁許可權時，將會顯示仲裁連結，選取它將顯示張貼的社群內容，並允許它 [已稽核](/help/communities/moderate-ugc.md) 採用類似於 [稽核主控台](/help/communities/moderation.md) 在作者環境中。

使用瀏覽器的「上一步」按鈕返回已發佈的網站。 大多數主控台無法透過發佈環境中的全域導覽存取。

![moderationlink](assets/moderationlink.png)

## 自行註冊 {#self-registration}

登出後，可以建立新的使用者註冊。

* 选择 `Log In`
* 选择 `Sign up for a new account`

![註冊](assets/registration.png)

![註冊](assets/signup.png)

依預設，電子郵件地址是登入ID。 如果取消勾選，訪客可以輸入自己的登入ID （使用者名稱）。 使用者名稱在發佈環境中必須是唯一的。

指定使用者名稱、電子郵件和密碼後，選取 `Sign Up` 將建立使用者並讓他們能夠簽署。

登入後，顯示的第一個頁面為其 `Profile` 頁面進行個人化。

![侧面像](assets/profile.png)

如果成員忘記其登入ID，則可能復原時使用他們的電子郵件地址。

![forgotusername](assets/forgotusername.png)
