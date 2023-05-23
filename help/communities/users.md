---
title: 管理使用者和使用者群組
seo-title: Managing Users and User Groups
description: AEM Communities的使用者可以自行註冊及編輯其設定檔
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# 管理使用者和使用者群組 {#managing-users-and-user-groups}

## 概述 {#overview}

在AEM Communities中的發佈環境中，使用者可以自行註冊及編輯其設定檔。 若有適當的許可權，他們也可以：

* 在社群網站中建立子社群(請參閱 [社群群組](creating-groups.md))。

* [稽核](moderation.md) 使用者產生的內容(UGC)。

* 是 [有特殊許可權](#privileged-members-group) 為部落格、行事曆、QnA和論壇建立專案。

在發佈環境中註冊的使用者通常稱為 *社群成員（成員）* 以區別他們 *使用者* 在作者環境中。

透過將成員指派給以下任一專案來授予許可權： [成員（使用者）群組](#publish-group-roles) 社群網站為時，以動態方式建立 [已建立](sites-console.md) 或 [已修改](sites-console.md#modifying-site-properties) 來自作者環境。 使用作者環境時，成員可透過以下方式從發佈環境檢視： [通道服務](#tunnel-service).

根據設計，在發佈環境中建立的成員和成員群組不應出現在作者環境中。 在作者環境中建立的使用者和使用者群組，其目的類似地是保留在作者環境中。

當作者上的使用者與發佈上的成員來自相同的使用者清單時（例如從相同的LDAP目錄同步），在作者與發佈環境中，他們不會被視為具有相同許可權和群組成員資格的相同使用者。 成員與使用者的角色必須視情況個別建立於發佈與作者。

對於 [發佈陣列](topologies.md)，對一個發佈執行個體進行的註冊和修改需要與其他發佈執行個體同步，以便他們能夠存取相同的使用者資料。 如需詳細資訊，請參閱 [使用者同步](sync.md)，其中包含說明以下內容的區段： [當……發生什麼情況](sync.md#what-happens-when).

### 贡献限制 {#contribution-limits}

為了防止垃圾郵件，可以限制成員的張貼內容頻率。 此外，也可以自動限制新註冊成員的貢獻。

如需詳細資訊，請參閱 [成員貢獻限制](limits.md).

### 動態建立的使用者群組 {#dynamically-created-user-groups}

建立新社群網站時，新使用者群組會以唯一id (uid)和適當的許可權動態建立，這些許可權適合在製作環境中管理社群網站所需的各種管理功能(請參閱 [作者群組角色](#author-group-roles))或發佈環境(請參閱 [發佈群組角色](#publish-group-roles))。

群組的名稱是從指定網站名稱產生的。 [社群網站建立](sites-console.md#step13asitetemplate). 此唯一ID可避免相同伺服器上名稱相似的社群網站和社群群組的命名衝突。

例如，如果網站名稱是&quot;*參與*&#x200B;若為名為「We.Retail Engage」的網站，則其中一個建立的使用者群組將是：

* 社群 *參與* 成員

## 创作环境 {#author-environment}

### 通道服務 {#tunnel-service}

使用製作環境時 [建立網站](sites-console.md)， [修改網站屬性](sites-console.md#modifying-site-properties) 和 [管理社群成員和成員群組](members.md)時，必須存取在發佈環境中註冊的使用者和使用者群組。

通道服務使用作者上的復寫代理程式提供此存取。

* 如需詳細資訊，請參閱 [設定指示](deploy-communities.md#tunnel-service-on-author) （在部署頁面上）。

此 [社群成員和群組主控台](members.md) 僅用於管理在發佈環境中註冊的使用者（成員）和使用者群組（成員群組）。

若要管理在作者環境中註冊的使用者和使用者群組，請使用 [安全性主控台](../../help/sites-administering/security.md)

### 作者群組角色 {#author-group-roles}

| 如果群組的成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員群組由系統管理員組成，系統管理員擁有社群管理員的所有能力以及管理社群管理員群組的能力。 |
| 社区管理员 | 社群管理員群組會自動成為所有社群網站及網站上建立的任何社群群組的成員。 Community Administrators群組的初始成員是administrators群組。 在作者環境中，社群管理員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）和稽核內容。 |
| 社群&lt;*網站名稱*> Sitecontentmanager | 社群網站內容管理員能夠執行傳統的AEM編寫、內容建立和修改社群網站的頁面。 |
| 无 | 匿名網站訪客可能無法存取作者環境。 |

### 系統管理員 {#system-administrators}

管理員群組的成員是系統管理員，他們能夠為製作和發佈環境執行AEM安裝的初始設定。

出於示範和開發目的，管理員群組有一個成員，其使用者ID為 *管理員* 而密碼為 *管理員*.

對於生產環境，應修改預設的管理員群組。

請務必遵循 [安全性檢查清單](../../help/sites-administering/security-checklist.md).

## 发布环境 {#publish-environment}

### 成為會員 {#becoming-a-member}

在發佈環境中，取決於 [設定](sites-console.md#user-management) 在社群網站中，網站訪客可以成為社群成員：

* 當社群網站為私人（已關閉）時：
   * 透過邀請
   * 依管理員的動作

* 當社群網站為公開（開放）時：
   * 透過自助註冊
   * 透過使用Facebook和Twitter進行社交登入

>[!NOTE]
>
>如果網站訪客註冊為一個開放社群網站的成員，他們會自動成為相同發佈環境中其他開放社群網站的成員。

### 發佈群組角色 {#publish-group-roles}

| 如果群組的成員…… | 主要角色 |
|---|---|
| 社群&lt;*網站名稱*>成員 | 社群網站成員是註冊使用者。 他們可以登入、修改其設定檔、加入開放的社群群組、將內容發佈至社群、傳送訊息給其他成員，以及關注網站活動。 |
| 社群&lt;*網站名稱*>版主 | 社群網站版主是受信任的社群成員，他可以使用版主主控台（大量使用），或在內容發佈頁面的內容中檢閱UGC。 |
| 社群&lt;*網站名稱*> &lt;*群組名稱*>成員 | 社群群組成員是指已加入開放社群群組，或已受邀加入封閉式社群群組的社群成員。 他們擁有網站內該社群群組的成員能力。 |
| 社群&lt;*網站名稱*>群組管理員 | 社群網站群組管理員是受信任的社群成員，被指派在社群網站中建立和管理子社群（群組）。 包含提供內容內稽核的功能。 |
| *有特殊許可權的成員安全性群組* | 為了限制內容建立而手動建立和維護的使用者群組。 另請參閱 [有特殊許可權的成員群組](#privileged-members-group). |
| 无 | 探索到網站的匿名網站訪客可檢視和搜尋允許匿名存取的社群網站。 為了參與和發佈內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 指派成員給發佈群組角色 {#assigning-members-to-publish-group-roles}

時間 [建立社群網站](sites-console.md) 在作者環境中，或當 [修改場地屬性，](sites-console.md#modifying-site-properties) 可為成員指派在發佈環境中執行的各種角色，例如版主、群組管理員、資源聯絡人或有特殊許可權的成員。

[啟用通道服務](sync.md#accessingpublishusersfromauthor) 結果會從發佈上的成員而不是作者上的使用者顯示指派選擇。

選取的成員將會自動指派給 [適當的群組](#publish-group-roles) 和他們的成員資格將在社群網站（重新）發佈時包括在內。

### 拥有权限的成员组 {#privileged-members-group}

有特殊許可權的成員安全群組的目的是限製為某些社群功能建立內容，而僅限於社群網站成員的有特殊許可權子集。

有特殊許可權的成員群組是使用 [社群群組主控台](members.md).

建立有特殊許可權的成員群組之後，使用 [通道服務已啟用](sync.md#accessingpublishusersfromauthor)，則現有社群網站的結構可能為 [已修改](sites-console.md#modify-structure) 編輯其社群功能的設定為「允許有特殊許可權的成員」並新增建立的群組。

允許指定一或多個有特殊許可權的成員群組的社群功能如下：

* [部落格功能](functions.md#blog-function)  — 限制新文章的建立。
* [行事曆功能](functions.md#calendar-function)  — 限制建立新事件。
* [論壇功能](functions.md#forum-function)  — 限制建立新主題。
* [QnA函式](functions.md#qna-function)  — 限制新問題的建立。

當社群功能未設定為安全時（未指派擁有特殊許可權的成員群組），則允許所有社群網站成員建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>將使用者新增至社群網站的特權成員群組，只會授予他們建立許可權（如果他們也是同一社群網站的成員）。

## 建立社群成員 {#creating-community-members}

### 存放庫位置 {#repository-location}

為了讓某些功能正常運作，需要建立具有適當許可權的使用者和使用者群組。

在中建立成員時 `/home/users/community`，它們會繼承賦予成員設定檔讀取許可權的適當ACL。

同樣地，自訂社群使用者群組（例如擁有特殊許可權的成員群組）應建立於 `/home/groups/community`.

使用 [社群成員和群組主控台](members.md) 將會在這些路徑中建立使用者和群組。

若要指定自訂路徑，必須使用傳統安全性UI，此介面可供存取： [https://&lt;server>：&lt;port>/useradmin](http://localhost:4503/useradmin).

若要為自訂成員路徑提供讀取許可權，請在所有發佈執行個體上設定類似的ACL `/home/users/community`：

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

若要為所有發佈執行個體上的自訂成員群組路徑（例如/home/groups/mycompany）提供適當的許可權，請設定類似的ACL `/home/groups/community`：

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有編寫環境提供四個單獨的控制檯：

| 主控台 | 工具、安全性、使用者 | 工具、安全性、群組 | 社群、成員 | 社群、群組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者上的使用者 | 作者上的使用者群組 | 發佈上的成員 | 發佈時的成員群組 |
| 需要 | 管理員許可權 | 管理員許可權 | 管理員許可權、通道服務、發佈伺服器陣列的使用者同步 | 管理員許可權、通道服務、發佈伺服器陣列的使用者同步 |

### 社群管理員角色 {#community-administrators-role}

如 [作者群組角色](#author-group-roles) 圖表，社群管理員群組的成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）和稽核內容。

請遵循建立使用者並將其指派給啟用管理員角色的相同步驟，但新增c `ommunity-administrators` 群組（位於使用者的「群組」標籤下）。

### LDAP整合 {#ldap-integration}

AEM支援使用LDAP來驗證使用者並建立使用者帳戶。 詳情請參閱 [使用AEM 6設定LDAP](../../help/sites-administering/ldap-config.md).

以下是社群成員和成員群組專屬的一些設定詳細資料。

1. 為每個AEM發佈執行個體設定LDAP。
2. [LDAP身分提供者](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊指示

3. [同步處理常式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 使用者自動成員資格]**： `community-<site name>-<uid>-members`
      * **[!UICONTROL 使用者路徑首碼]**： `/community`
      * **[!UICONTROL 群組路徑首碼]**： `/community`

4. [外部登入模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會導致系統自動將使用者指派給社群網站的成員群組，且存放庫位置為 `/home/users/community` 和 `/home/groups/community`，因此他們會繼承適當的許可權，以便檢視彼此的設定檔。

* 此 `User auto membership` 值應為 `rep:authorizableId` 屬性，而非 `givenName` （顯示名稱）。

## 在AEM執行個體之間同步使用者 {#synchronizing-users-among-aem-instances}

使用時 [發佈陣列](topologies.md)，先將使用者匯入一個執行個體，確保使用者在每個發佈執行個體上具有相同的路徑，並 [啟用使用者同步](sync.md) 將使用者分發到其他發佈執行個體。

如果匯入使用者群組，為確保使用者群組在每個發佈執行個體上具有相同的路徑，請匯入到一個執行個體，然後 [建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package) 匯出，並在所有其他發佈執行個體上安裝該套件。

雖然透過使用者同步處理來同步使用者群組將包含在未來的版本中，但目前僅限 *會籍* 執行使用者同步時，將會同步使用者群組的。

## 關於社群群組 {#about-community-groups}

討論群組時，有兩個不同的主題：

* **[社群群組](overview.md#communitygroups)**

   社群群組是子社群，可在支援建立社群群組的社群網站之發佈環境中建立。 建立社群群組後，會有更多頁面新增至網站，且會以類似於其上層社群網站的方式進行管理。 如需詳細資訊，請造訪 [社群群組Essentials](essentials-groups.md) 適用於開發人員和 [社群群組](creating-groups.md) 適用於作者。

* **[成員群組](../../help/sites-administering/security.md)**

   成員群組是成員可能所屬的群組，並可透過「群組」主控台進行管理。 本頁大部分討論都集中在成員群組上。 自動為社群網站建立的成員群組，其前置詞為 *`Community`*，可稱為社群群組，因此必須考量討論的內容。
