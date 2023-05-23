---
title: AEM Communities概觀
seo-title: AEM Communities Overview
description: AEM Communities功能和設定概觀
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# AEM Communities概觀 {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities可讓您快速建立內部部署社群網站，進而改善效能、改善網站管理，並鼓勵將網站訪客轉化為有價值的社群成員。

## Communities功能 {#communities-features}

AEM Communities可讓您發展與網站訪客的關係，這會：

* **通知** 透過部落格、Q&amp;A和事件行事曆，
* 當 **獲得深入分析** 透過論壇、評論和其他社群內容，通常稱為使用者產生的內容(UGC)。
* 它允許 **稽核** 由發佈環境中的信任成員所提供，
* **社交登入** 使用Twitter和Facebook，
* **內嵌翻譯** 社群內容，
* **社群群組建立** 從已發佈的社群網站，
* **評分** 要獎勵徽章，
* **檔案共用**，
* **通知** 和 **活動資料流**，
* 允許 **標籤** (@mention)使用者產生的內容中的其他註冊會員，以吸引他們的注意。

社群功能可透過以下方式展示： [AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) 可在GitHub.com上公開取得，或透過新的We.Retail參考實作取得。

## 社区站点 {#community-sites}

社群網站是使用簡單精靈建立的AEM網站，該精靈會產生具有許多預先連線到網站中常見功能的網站。

此 [網站建立精靈](/help/communities/sites-console.md)：

* 根據所選專案組合網站功能 [社群網站範本](/help/communities/sites.md) 即：

   * 建置來源 [社群功能](#community-functions)
   * 可選 [社群群組](#communitygroups) 功能

* 使用設定進行設定：

   * 稽核
   * 登入
   * 转换

* 提供基本功能：

   * 回應式設計：使用 [twitterBootstrap主題](https://getbootstrap.com)

   * 登入：自助註冊， [社交登入](/help/communities/social-login.md)，使用者設定檔

      * 通知：成員會看到與其相關的事件，以及使用者產生的內容 [@mentioned](/help/communities/overview.md#mentionssupport).

      * 傳送訊息：成員可在社群網站內傳送或接收訊息。
      * 搜尋：可在社群網站內搜尋。
      * 語言切換：選擇語言的功能 [多語言網站](/help/sites-administering/translation.md).

      * 管理：授權成員的存取權，以便稽核和管理社群網站內的使用者。

* 省去許多頁面層級撰寫步驟：

   * 品牌推廣：可選擇上傳橫幅影像以在社群網站的所有頁面上顯示
   * 導覽功能表：社群網站範本中包含的功能提供導覽連結。

若要體驗快速建立新社群網站的簡易性，請造訪 [AEM Communities快速入門](/help/communities/getting-started.md).

## 社群內容持續性 {#community-content-persistence}

為了改善社群內容的效能和同步化，AEM Communities需要專為使用者產生的內容(UGC)在所有AEM （製作和發佈）執行個體之間共用的公用存放區。

可透過儲存資源提供者(SRP)輕鬆存取社群內容，SRP提供將存取與基礎拓撲分隔開的圖層，並支援UGC的共同存放區。

若要進一步瞭解社群內容持續性和建議的部署，請參閱：

* [社群內容儲存](/help/communities/working-with-srp.md)，其中討論UGC的可用SRP儲存選項。
* [建議的拓撲](/help/communities/topologies.md)，會根據使用案例和SRP選擇討論拓撲。
* [升級至AEM 6.5社群](/help/communities/upgrade.md)，可提供移至AEM 6.5時關於UGC的實用資訊。

## 社群主控台 {#communities-consoles}

在製作環境中，全域導覽主控台提供對的存取權 [社群主控台](/help/communities/consoles.md)，其中包含：

* [網站](/help/communities/sites-console.md) 主控台

   * 網站建立
   * 網站編輯
   * 網站管理
   * [社群群組](/help/communities/groups.md) 主控台

* [稽核](/help/communities/moderation.md) 主控台

   * 適用於作者和發佈環境的通用大量稽核UI。
   * 新增篩選條件。

* [成員和群組](/help/communities/members.md) 管理主控台

   * 提供從作者環境建立和管理發布端使用者（成員）的功能。
   * 提供禁止成員的功能。
   * 提供從製作環境建立和管理發布端使用者群組（成員群組）的功能。

* [報表](/help/communities/reports.md) 主控台

   * 提供產生工作總攬、貼文和檢視報告的功能。

全域工具控制檯提供對以下Communities工具的存取：

* [網站範本](/help/communities/tools.md#sitetemplatesconsole) 主控台

   * 建立和管理社群網站範本。

* [群組範本](/help/communities/tools.md#grouptemplatesconsole) 主控台

   * 建立和管理社群群組範本。

* [社群功能](/help/communities/tools.md#communityfunctionsconsole) 主控台

   * 建立和管理社群功能。

* [儲存設定](/help/communities/tools.md#storageconfiguratonconsole) 主控台

   * 選取並設定 [公用存放區](/help/communities/working-with-srp.md) 用於網站。

* [组件指南](/help/communities/components-guide.md)

   * 範例網站， [社群元件](https://localhost:4502/editor.html/content/community-components/en.html)，提供所有Communities元件的範例及其預設設定，以及實驗這些元件的能力。

## 社区站点模板 {#community-site-templates}

社群網站建立是以選取的社群網站範本為基礎，以快速設定獨立於任何範例網站的社群網站。

社群網站範本是由社群功能和社群群組範本組成，提供社群網站的結構，包括登入、使用者設定檔、訊息、網站功能表、搜尋、主題設定和品牌功能。

請參閱 [網站範本主控台](/help/communities/sites.md).

## 社区功能 {#community-functions}

社群體驗的預期功能眾所周知。 透過AEM Communities，這些功能會以建置區塊的形式提供，稱為社群功能。

社群功能是一般AEM頁面，其中包含以纜線連線在一起的元件，可輕鬆整合至社群網站範本中。

請參閱 [社群功能主控台](/help/communities/functions.md).

## 社群群組和群組範本 {#community-groups-and-group-templates}

社群群組功能可讓作者和發佈環境中的授權使用者和社群成員，在社群網站中動態建立子社群。

在作者環境中，當範本的結構包含 [群組功能](/help/communities/functions.md#groups-function).

建立社群群組需要選取提供社群群組頁面設計的社群群組範本。 將「群組」功能新增至範本結構時，會將其設定為指定一個群組範本，或在建立新社群群組時提供範本選擇。

另请参阅：

* [網站群組主控台](/help/communities/groups.md) 用於在作者環境中建立子社群。
* [群組範本主控台](/help/communities/tools-groups.md) 用於建立群組的場地結構。
* [AEM Communities快速入門](/help/communities/getting-started.md) 有關快速建立包含巢狀群組的社群網站的教學課程。

## 社群元件 {#community-components}

此 [社群元件](/help/communities/author-communities.md) 從中建立社群網站可用於將Communities功能新增到任何AEM網站。

此 [社群元件指南](/help/communities/components-guide.md) 可用於以互動方式探索元件。

## 參與社群 {#engagement-community}

參與社群是社群網站，專注於吸引客戶，以資訊、徵求意見及允許客戶作為社群成員互動。

參與社群的功能可能包括：

* 登录
* 消息
* 論壇
* 评论
* 审核
* 评级
* 投票
* 部落格
* 组
* 行事曆
* 翻译
* 审核
* 通知
* 評分和預算
* Analytics報表

若要體驗快速建立新參與社群的簡易性，請造訪 [AEM Communities快速入門](/help/communities/getting-started.md).

## AEM示範電腦 {#aem-demo-machine}

此 [AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) 管理並執行AEM的示範 [網站](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)， [資產](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)， [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)， [應用程式](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 和 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)，通常需要比只啟動QuickStart執行個體更多的設定。 AEM示範電腦將設定其他 [基礎結構](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 例如MongoDB、Solr、MySQL、FFmpeg和電子郵件伺服器。

AEM示範電腦包含：

* A [圖形化使用者介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 具有可設定的Apache ANT指令碼 [屬性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 和 [目標](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* 要安裝的套件。

AEM Demo Machine已在Windows、MacOS和Linux上透過CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功進行測試。

AEM示範機器需要有效的AEM授權。

>[!NOTE]
>
>檢視 [影片簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 至AEM示範電腦(13:26)。

## AEM Communities檔案 {#aem-communities-documentation}

* 造訪 [部署社群](deploy-communities.md) 以瞭解建議的部署。
* 造訪 [管理社群網站](administer-landing.md) 瞭解有關建立社群網站、新增社群群組、設定社群網站範本、仲裁社群內容、管理成員、標籤、通知、評分和徽章等資訊。
* 造訪 [開發社群](communities.md) 瞭解社交元件架構(SCF)和自訂Communities元件和功能。
* 造訪 [Authoring Communities元件](author-communities.md) 瞭解如何使用及設定Communities元件進行創作。
