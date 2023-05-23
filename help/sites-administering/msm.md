---
title: "重用内容：多站点管理器和 Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 瞭解如何透過即時副本和多網站管理員來重複使用內容。
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 31%

---

# 重用内容：多站点管理器和 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

多網站管理員(MSM)可讓您在多個位置使用相同的網站內容。 MSM使用其Live Copy功能來達成此目的：

* 利用 MSM，您可以：

   * 创建内容一次，然后
   * 將此內容複製到其他區域並重複使用此內容([即時副本](#live-copies))或其他網站。

* 然後MSM會維護來源內容與其即時副本之間的（即時）關係，以便：

   * 當您對來源內容進行變更時，來源和即時副本會進行同步（以將這些變更也套用至即時副本）。
   * 您可以中斷個別子頁面和/或元件的即時關係，以調整即時副本的內容。 如此一來，對來源的變更將不再套用至即時副本。

本頁及以下頁面涵蓋相關問題：

* [创建并同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 最佳实践](/help/sites-administering/msm-best-practices.md)

## 可能的情况 {#possible-scenarios}

MSM和即時副本有許多使用案例，某些情況包括：

* **跨国 – 全球到本地公司**

   MSM 支持的一个典型用例是在多个采用同一语言的跨国站点中重用内容。這允許重複使用核心內容，同時允許國家差異。

   例如，We.Retail參考網站範例的英文區段是為美國客戶建立的。 此網站中的大部分內容也可用於其他迎合不同國家/地區和文化的講英語客戶的We.Retail網站。 虽然所有站点的核心内容都相同，但可以进行区域调整。

   以下結構可用於美國、英國、加拿大和澳洲的網站：

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM 不翻译内容。它用于创建所需的结构和部署内容。
   >
   >
   >另請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 如果您想要延伸此類範例。

* **国内 – 总部到地区分支机构**

   或者，擁有經銷商網路的公司可能希望為其個別經銷商提供個別網站，每個網站都是總部所提供之主要網站的變體。 这可能适用于拥有多个地区办事处的单一公司，或由中央特许专营授权公司和多个当地特许经营人构成的全国特许经营体系。

   总部可以提供核心信息，而区域实体可以添加本地信息，例如详细联系方式、营业时间和活动。

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **多个版本**

   或者，您可以使用MSM來建立特定子分支的版本，例如，包含特定產品不同版本的詳細資訊的支援子網站，其中基本資訊保持不變，只需變更更新的功能：

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >在這種情況下，總是要詢問是直接複製還是使用即時副本。
   >
   >兩者之間會取得平衡：
   >
   >  * 需要在多個版本上更新的核心內容量。
   >
   >相较于：
   >
   >  * 需要調整多少個別復本。


## 从 UI 访问 MSM {#msm-from-the-ui}

可使用相应控制台中的各种选项直接通过 UI 访问 MSM。若要提供簡介，請列出下列主要位置：

* **创建站点**（**站点**）

   * MSM可協助您管理共用相同內容的多個網站；例如，我們通常為全球受眾提供網站，因此大部分內容在所有國家/地區都是相同的，只有個別國家/地區專屬的部分內容。 MSM可讓您 [根據您的來源網站建立可自動更新一或多個網站的即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 这还可以帮助您实施通用的基础结构，跨多个站点使用共有内容，维护共有外观，并专注于管理各个站点之间实际不同的内容。
   * 需要预定义的 Blueprint 配置来指定源。
   * 建立（預先定義的）來源的即時副本。
   * 为用户提供&#x200B;**转出**&#x200B;按钮。

* **创建 Live Copy**（**站点**）

   * MSM可讓您 [建立個別頁面或網站支行的臨機（一次性）即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)；例如，複製子分支以提供產品的新/更新版本相關資訊。
   * 建立臨機即時副本（不需要Blueprint設定）。
   * 可用於（立即）建立任何頁面/分支的即時副本。
   * 需要&#x200B;**同步**（不提供&#x200B;**转出**&#x200B;按钮）。

* **查看属性**（**站点**）

   * 只要適當，此選項就能協助您 [監視您的即時副本](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供相關資訊 **即時副本** y或 **Blueprint**.

* **引用**（**站点**）

   * [引用](/help/sites-authoring/basic-handling.md#references)边栏提供了有关 **Live Copy** 的信息以及对相应操作的访问权限。

* **Live Copy 概述**（**站点**）

   * 此主控台可讓您 [檢視和管理您的Blueprint及其即時副本](/help/sites-administering/msm-livecopy-overview.md).

* **Blueprint**（**工具** – **站点**）

   * 此主控台可讓您 [建立和管理您的Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM功能的各方面可用於其他幾個AEM功能（例如，啟動、目錄）；在這些情況下，即時副本由該功能管理。

### 使用的术语 {#terms-used}

作為簡介，下表提供MSM使用的主要術語的概觀；後續章節和頁面將詳細介紹這些術語：

<table>
 <tbody>
  <tr>
   <td><strong>术语</strong></td>
   <td><strong>定义</strong></td>
   <td><strong>更多詳細資料</strong></td>
  </tr>
  <tr>
   <td><strong>源</strong></td>
   <td>原始頁面。</td>
   <td>与 Blueprint 和/或 Blueprint 页面同义.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>（源的）副本，由转出配置定义的同步操作维护. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy 配置</strong></td>
   <td>即時副本的設定詳細資訊的定義。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>实时关系</strong><br /> </td>
   <td>指定資源繼承的有效定義；來源和即時副本之間的連線。<br /> </td>
   <td>確保來源的變更可以與即時副本同步。</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>与源同义.</td>
   <td>可由 Blueprint 配置定义.</td>
  </tr>
  <tr>
   <td><strong>Blueprint 配置</strong></td>
   <td>用于指定源路径的预定义的配置。</td>
   <td>在 Blueprint 配置中引用 Blueprint 页面时，“转出”命令将变为可用.</td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>來源和即時副本之間內容同步的通用術語（兩者皆有） <strong>轉出</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出</strong><br /> </td>
   <td>從來源同步至LiveCopy。<br /> 可以由作者（在Blueprint頁面上）或系統事件（由轉出設定定義）觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出配置</strong></td>
   <td>用于确定将同步的属性及其同步方式和时间的规则。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>從LiveCopy頁面發出的手動同步要求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>继承</strong></td>
   <td>發生同步化時，即時副本頁面/元件會繼承其來源頁面/元件的內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暂停</strong></td>
   <td>暫時移除即時副本與其Blueprint頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分离</strong></td>
   <td>永久移除即時副本與其Blueprint頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>重置</strong></td>
   <td><p>將即時副本頁面重設為：</p>
    <ul>
     <li>删除所有继承取消并<br /> </li>
     <li>将页面返回到与源页面相同的状态。</li>
    </ul> <p>重置会影响您对页面属性、段落系统和组件所做的任何更改。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>浅</strong></td>
   <td>單一頁面的即時副本。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>深</strong></td>
   <td>頁面的即時副本及其子頁面。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>另請參閱 [Java API概觀](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 物件名稱。

## Live Copy {#live-copies}

MSM Live Copy是特定網站內容的副本，其會維持與原始來源的即時關係：

* 即時副本會從其來源繼承內容。
* 在对源进行更改时，同步会执行实际内容传输。
* 即時副本可視為下列其中一項：

   * 浅：单页面
   * 深：页面及其子页面

* 同步化規則（稱為轉出設定）可決定要同步的屬性以及同步發生的時間。

在上一个示例中，`/content/we-retail/language-masters/en` 是英语版的全局主站点。為了重複使用這個網站的內容，會建立MSM即時副本：

* `/content/we-retail/language-masters/en` 下的内容为源。

* 以下內容 `/content/we-retail/language-masters/en` 複製到 `/content/we-retail/us/en/`， `/content/we-retail/gb/en`， `/content/we-retail/ca/en`、和 `/content/we-retail/au/en` 節點。 這些是即時副本。

* 作者对 `/content/we-retail/language-masters/en` 下的页面进行了更改。
* 觸發時，MSM會將這些變更同步到即時副本。

### Live Copy – 构图 {#live-copies-composition}

>[!NOTE]
>
>本節中的圖表和說明代表潛在即時副本的快照。 虽然它们并不全面，但提供了概述以重点说明具体特征。

當您最初建立即時副本時，所選的來源頁面會以1:1的比例反映在即時副本中。 之後，也可以直接在即時副本中建立新資源（頁面和/或段落），因此瞭解這些變化以及它們對同步化的影響會很有用。 可能的构图包括：

* [具有非 Live Copy 页面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [嵌套式 Live Copy](#nested-live-copies)

即時副本的基本形式具有：

* 以1:1的比例反映所選來源頁面的即時副本頁面。
* 一个配置定义。
* 为每个资源定义的实时关系：

   * 連結即時副本資源與其Blueprint/來源。
   * 在实现继承和转出时使用。

* 可以根据要求[同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)更改。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 具有非 Live Copy 页面的 Live Copy {#live-copy-with-non-live-copy-pages}

當您在AEM中建立即時副本時，您可以看見並瀏覽即時副本分支，並在即時副本分支上使用一般AEM功能。 這表示您（或程式）可以在即時副本分支內建立新資源（頁面和/或段落） (例如 `myCanadaOnlyProduct`)。

* 此类资源与源/Blueprint 页面没有实时关系，并且不会同步。
* 可能会出现 MSM 作为特殊情况处理的场景。例如，當您（或程式）在來源/Blueprint和即時副本分支中建立具有相同位置和名稱的頁面時。 有关此类情况，请参阅 [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)以了解更多信息。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 嵌套式 Live Copy {#nested-live-copies}

當您（或程式）建立 [現有即時副本中的新頁面](#live-copy-with-non-live-copy-pages) 此新頁面也可以設定為其他Blueprint的即時副本。 這稱為巢狀即時副本，其中第二個（內部）即時副本的行為會以下列方式受到第一個（外部）即時副本的影響：

* 為頂層即時副本觸發的深層轉出可以繼續進入巢狀即時副本（例如，如果觸發器符合）。
* 來源之間的任何連結都將在即時副本中重寫。

   例如，從第二個到第一個Blueprint的連結將重寫為從巢狀/第二個即時副本到第一個即時副本的連結。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在即時副本分支中移動/重新命名頁面，則（在內部）這將被視為巢狀即時副本，以使AEM能夠追蹤關係。

#### 堆叠式 Live Copy {#stacked-live-copies}

即時副本建立為淺層即時副本的子項時，即稱為棧疊即時副本。 其行為與 [巢狀即時副本](#nested-live-copies).

### 源、Blueprint 和 Blueprint 配置 {#source-blueprints-and-blueprint-configurations}

任何頁面或頁面分支都可用作即時副本的來源。

不过，MSM 还允许您定义指定源路径的 Blueprint 配置。使用 Blueprint 配置的好处是：

* 允許作者使用 **轉出** blueprint上的選項 — 以（明確）推送修改至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站**；這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關聯的即時副本定義預設轉出設定。

即時副本的來源可以是一般頁面或Blueprint設定包含的頁面 — 兩者都是有效的使用案例。

來源會形成即時副本的Blueprint。 在执行以下操作时定义 Blueprint：

* [建立Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   此設定會（事前）定義要用來建立即時副本的頁面。

* [建立頁面的即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用來建立即時副本的頁面（來源頁面）為Blueprint頁面。

   Blueprint設定是否可參照來源頁面。

### 转出和同步 {#rollout-and-synchronize}

轉出是中心的MSM動作，可將即時副本與其來源同步。 您可以手動執行轉出，也可以自動進行轉出：

* 可以定义[转出配置](#rollout-configurations)，以便特定[事件](/help/sites-administering/msm-sync.md#rollout-triggers)能够促使自动进行转出。
* 編寫Blueprint頁面時，您可以使用 [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 將變更推送至即時副本的命令。

   **转出**&#x200B;命令适用于 Blueprint 配置引用的 Blueprint 页面。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 在製作即時副本頁面時，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 將變更從來源提取至即時副本的命令。

   此 **同步** 命令一律可用於即時副本頁面（無論來源/blueprint頁面是否由blueprint設定包含）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 转出配置 {#rollout-configurations}

轉出設定會定義即時副本與來源內容同步的時間和方式。 转出配置由一个触发器和一个或多个同步操作组成：

* **触发器**

   觸發器是引發即時動作同步化的事件，例如來源頁面的啟動。 MSM 定义您可以使用的触发器。

* **同步動作**

   在即時副本上執行，以使其與來源同步。 範例動作包括複製內容、排序子節點和啟動即時副本頁面。 MSM提供許多同步動作。

   >[!NOTE]
   >
   >您可以使用 Java API 为实例创建自定义操作。

轉出設定可以重複使用，以便多個即時副本可以使用相同的轉出設定。 标准安装包含了多个[转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)。

### 转出冲突 {#rollout-conflicts}

轉出可能會變得複雜，尤其是當作者同時在來源和即時副本中編輯內容時，因此瞭解AEM如何處理任何轉出會很有用 [轉出時可能發生衝突](/help/sites-administering/msm-rollout-conflicts.md).

### 暂停和取消继承与同步 {#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件都透過即時關係與其來源頁面和元件相關聯。 即時關係會設定來自來源的即時副本內容的同步化。

您可以 **暫停** 即時副本頁面的即時副本繼承，以便您可以變更頁面屬性和元件。 当您暂停继承时，页面属性和组件不再与源同步。

在编辑单个页面时，作者可以为组件&#x200B;**取消继承**。取消继承后，实时关系将暂停，并且不会针对该组件进行同步。当需要自定义内容的子部分时，取消继承和同步会很有用。

### 分离 Live Copy {#detaching-a-live-copy}

您也可以 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 從其Blueprint移除所有連線。

>[!CAUTION]
>
>分离操作是永久性且不可逆的。

分離會永久移除即時副本與其Blueprint頁面之間的即時關係。 所有MSM相關屬性都會從即時副本中移除，且即時副本頁面會成為獨立副本。

>[!NOTE]
>
>另請參閱 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 以取得完整詳細資訊；包括對子頁面和父頁面的相關影響。

## 使用 MSM 的标准步骤 {#standard-steps-for-using-msm}

下列步驟說明使用MSM重複使用內容並同步化即時副本變更的標準程式。

1. 开发源站点的内容。
1. 决定要使用的转出配置。

   1. MSM [安装了多个转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)，可满足大量用例的要求。
   1. （可选）如果需要，您可以[创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。

1. 决定需要[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)并按需配置的情况。
1. 如有需要， [建立Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 可識別即時副本的來源內容。
1. [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 根据需要更改源内容。您应采用您组织已制定的常规内容审查和审批流程。
1. [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) Blueprint，或 [同步即時副本](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 隨附變更。

## 自定义 MSM {#customizing-msm}

MSM提供工具，讓您的實作可適應共用內容時可能存在的特殊複雜性：

* **自訂轉出設定**
   [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 當安裝的轉出設定不符合您的需求時。 您可以使用任何可用的转出触发器和同步操作。

* **自訂同步動作**
   [建立自訂同步動作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 安裝的動作不符合您的特定應用程式需求時。 MSM提供Java API來建立自訂同步動作。

## 最佳实践 {#best-practices}

[MSM 最佳实践](/help/sites-administering/msm-best-practices.md)页面包含有关您的实施的重要信息。
