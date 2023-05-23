---
title: 创作
seo-title: Authoring
description: 在 AEM 中进行创作的概念
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 32%

---

# 创作{#authoring}

## 製作（和發佈）的概念 {#concept-of-authoring-and-publishing}

AEM提供您兩個環境：

* 创作
* 发布

這些互動可讓您在網站上提供內容，讓訪客能夠閱讀。

作者環境提供機制，可在實際發佈此內容之前建立、更新和檢閱此內容：

* 作者建立並檢閱內容（可以是數種型別；例如，頁面、資產、出版物等）
* 之後會發佈至您的網站。

![chlimage_1-132](assets/chlimage_1-132.png)

在製作環境中，AEM的功能可透過兩個UI使用。 对于发布环境，可以设计提供给用户使用的界面的整体外观。

### 创作环境 {#author-environment}

作者在称为&#x200B;**创作环境**&#x200B;的环境中工作。这为创建内容提供了易于使用的界面（图形用户界面（GUI 或 UI））。它通常位於公司防火牆後面，提供完整保護，並要求作者使用已指派適當存取許可權的帳戶登入。

>[!NOTE]
>
>您的帐户需要适当的访问权限才能创建、编辑或发布内容。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 在頁面上產生新內容或編輯現有內容
* 使用預先定義的範本來建立新內容頁面
* 建立、編輯及管理您的資產和集合
* 建立、編輯及管理您的出版物
* 開發您的行銷活動和相關資源
* 開發及管理社群網站
* 移動、複製或刪除內容頁面、資產等
* 發佈（或取消發佈）頁面、資產等

此外，还有一些管理任务可帮助管理内容：

* 控制變更管理方式的工作流程；例如。 在發佈前強制執行稽核
* 協調個別任務的專案

>[!NOTE]
>
>AEM也是 [已管理](/help/sites-administering/home.md) （適用於大部分任務）來自製作環境。

#### 发布环境 {#publish-environment}

準備就緒後，AEM網站的內容會發佈至 **發佈環境**. 在该环境中，根据设计界面的具体观感，目标受众可以使用网站页面。

通常，發佈環境位於非軍事區內；換言之，可供網際網路使用，但不再受內部網路的完全保護。

當AEM網站為 [社群網站](/help/communities/overview.md)，或包含 [Communities元件](/help/communities/author-communities.md)，登入的網站訪客（成員）可與Communities功能互動。 例如，他們可能會張貼至論壇、張貼評論或追蹤其他成員。 可以授予成員執行通常僅限於作者環境的活動的許可權，例如建立新頁面（社群群組）、部落格和稽核其他成員的文章。

>[!NOTE]
>
>遺憾的是，使用的術語有時會出現重疊。 這種情況可能發生在以下位置：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
>
>* **复制**
   >  這些是技術術語，用於表示資料（例如頁面內容、檔案、程式碼、使用者註解）從一個環境移動到另一個環境（即發佈或反向複製使用者註解時）。
>


#### Dispatcher {#dispatcher}

为了优化网站访客体验，**[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 实施了负载平衡和缓存。**
