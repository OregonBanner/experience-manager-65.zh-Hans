---
title: 協助撰寫AEM
seo-title: Contributing to AEM
description: AEM的開發遵循大型開放原始碼專案中常用的成熟方法
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 0%

---

# 協助撰寫AEM{#contributing-to-aem}

## 開發方法 {#development-methodology}

AEM的開發遵循大型開放原始碼專案中常用的成熟方法。 AEM技術棧疊中的許多核心元素實際上是作為活躍的開放原始碼專案來維護的，例如Sling和Jackrabbit，這些專案是對Apache Software Foundation貢獻的。 AEM中展現的這種精神的一個主要方面，是鼓勵您利用可用的郵寄清單和線上論壇，與開發團隊直接互動。

若您正在為AEM的元件投稿，您應該像投稿至開放原始碼專案時一樣熟悉AEM，並像您打算投稿至此專案時一樣與現有的核心團隊溝通。

## 所需體驗 {#required-experience}

HyperText傳輸通訊協定(HTTP)是我們所有工作的核心。 因此，在為AEM貢獻內容之前，您應該對HTTP有深入的瞭解，最好能夠撰寫您自己的具有執行緒集區的多執行緒HTTP伺服器Java實作。 您也應該瞭解HTTP/1.1保持連線行為，並且您應該對伺服器/使用者端與JavaScript的互動有深入的瞭解，特別是AJAX所代表的非同步互動風格。

由於頁面動態和互動式內容是WM體驗的關鍵，因此您必須相當深入地瞭解檔案物件模型，及其回應事件的程式化操作潛力。 您應該具備一些知識，例如即時DOM操作和在多個瀏覽器檔案上的拖放行為（例如使用iframe）。

因此，您應該對以下內容有深入的瞭解：

* 此 [http/1.1通訊協定](https://www.ietf.org/rfc/rfc2616.txt)
* HTML（最好） [HTML5](https://dev.w3.org/html5/spec/Overview.html))
* 階層式樣式表
* 可延伸標籤語言(XML)
* 非同步JavaScript和XML (AJAX)設計模式
* JavaScript物件標籤法(JSON)
* 檔案物件模型
* 有狀態與無狀態互動
* [統一資源識別碼](https://www.ietf.org/rfc/rfc2396.txt)
* 瀏覽器Cookie
* 和其他現代網路開發概念

Adobe Experience Manager的技術棧疊是以 [Apache Felix](https://felix.apache.org/) 具有的OSGI容器 [Apache Sling](https://sling.apache.org/site/index.html) 網頁框架並嵌入Java內容存放庫([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))根據 [Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html). 您應熟悉這些個別專案，以及您打算投稿的區域中使用的任何其他開放原始碼元件（例如Apache Lucene）。

## 部落知識 {#tribal-knowledge}

某些概念和指導原則深深地植根於舊日文化中。 本節列出您應留意的一些「深入的DNA嵌入」問題。

### 一切都是內容 {#everything-is-content}

內容不僅包含網頁應用程式儲存的所有資料。 程式碼、程式庫、指令碼、範本、HTML、CSS、影像和各種人工因素、任何專案及所有內容都會保留在內容存放庫中，並透過封裝管理器和封裝共用以封裝形式匯入/匯出。

### David模型 {#david-s-model}

在Java Content Repository中設定內容模型的方式，需要一種與軟體產業在關聯式世界中設定資料模型的一般做法完全不同的思維方式。 對於任何內容管理的新手來說，JCR方法必不可少 [David模型：內容模型指南](https://wiki.apache.org/jackrabbit/DavidsModel).

### RESTful {#restfulness}

REST方法深深根植於我們的工作。 這表示除了其他事項以外，應避免狀態互動，並記住URI是內容與服務的確切位址。

REST (REpresentational State Transfer)是指全球資訊網所依據的軟體架構樣式。 它描述了讓Web運作的關鍵元素，因此提供了一組設計網頁型軟體的原則。 因此，在設計要在網頁上使用的API時，遵循這些「最佳實務」是明智的。

因為REST提供了我們所做許多工作的指導思想，所以您應該認為精通RESTful設計的原則至關重要。 開始的好地方 [Roy Fielding的論文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

### Sling請求解析 {#sling-request-resolution}

瞭解AEM的一個重要面向是傳入請求如何與內容和應用程式行為相關、內容在內容存放庫中的結構方式，以及AEM在何處尋找處理請求的應用程式邏輯。 瞭解Apache [Sling URL分解](https://sling.apache.org/site/url-decomposition.html) 以及強制執行REST架構樣式及其無狀態、可快取及分層系統限制的方式。

要瞭解Apache Sling的請求解析度的關鍵方面是，請求如何主要對應到內容存放庫中的特定資源、請求的其他屬性以及這些內容物件的屬性如何判斷將叫用哪些應用程式程式碼來呈現內容，以及/apps中的程式碼如何覆寫/libs中的程式碼。

### 快速入门 {#quickstart}

沒有步驟三：若要安裝並執行，只要下載並連按兩下Quickstart JAR檔案即可。 沒有步驟3。 任何其他選用功能只需要從Package Share安裝適當的套件。

小型快速入門：將快速入門JAR檔案的大小維持在最小。 以智慧方式最佳化使用程式庫，將選用功能移至封裝共用。

更短的啟動時間：進行會影響啟動時間的變更時，請確定這會縮短啟動時間，而非更長。

### 精簡與中等 {#lean-and-mean}

我們偏好輕巧、小巧、快速且優雅的程式碼和專案。 「夠好」還不夠。

程式碼重複使用：我們以OSGi為基礎的產品架構和「一切都是內容」理念意味著，我們擁有重複使用程式碼和成品的絕佳機會。 我們儘可能利用這一事實，讓功能保持精簡而中庸的風格。

鬆散耦合：我們偏好鬆散耦合的互動，而非緊密相依性和「不受歡迎的親密關係」。 鬆散耦合也使得更多程式碼可以重複使用。

### 不要破壞示範 {#don-t-break-the-demo}

熟悉示範指令碼和示範中最常顯示的產品功能。 請至少瞭解，您所做的任何操作都不應中斷「示範指令碼」功能。 核心產品應一律可供展示使用，即使在開發期間亦然。

### 針對可靠性而設計 {#design-for-reliability}

我們致力於以失效軟方式設計和程式碼功能，使得（例如）單一DOM元素的問題不會導致整個頁面無法呈現。 換言之：製造致命的東西。 讓其他所有專案都能夠存活。 讓產品「原諒」。

### 異常是新常態 {#abnormal-is-the-new-normal}

不要依賴關機掛接，請確定啟動時進行清理。 異常終止是正常終止。

`shutdown == kill -9 == power outage`

### 準備好彈性叢集 {#be-ready-for-elastic-clustering}

隨時準備彈性叢集，隨時假設有叢集。 一般而言，遵守內容存放庫中的所有內容即表示內建叢集支援。

### 設計提供回溯相容性 {#design-for-backward-compatibility}

您所做的任何操作都不應破壞客戶的舊程式碼。 僅考慮 `/libs` 以包含可在升級期間更新的產品程式碼。 此 `/apps` 存放庫的區段是專案程式碼，而 `/etc` 區段包含需要保留的自訂設定。 一般而言，請勿覆寫中的任何專案 `/apps`， `/content` 和 `/home`. 升級後，舊的專案程式碼、設定和內容應會像升級前一樣繼續運作。

設計回溯相容性也可確保升級體驗與初始安裝的簡單性相符。 只需停止AEM、取代Quickstart JAR檔案並重新啟動AEM即可。 隨著安裝基礎的迅速成長，升級效率將日益成為一項顯著優勢。

雖然現有的API在更新且更完善的功能時會標示為已過時，但之前5.x版中公開的所有API都需要保持功能，因為它們可能用於自訂應用程式程式碼中。 不應移除此類API。

在內容結構和使用者體驗的一般一致性方面，也應牢記回溯相容性。

## 核心概念 {#core-concepts}

**作者執行個體**  — 一般而言，基於安全、控管和其他原因，生產網站會將AEM例項分成作者例項和發佈例項。 如需部署架構（包括作者/發佈執行個體）的詳細資訊，請參閱AEM執行個體相關檔案。

**快取、煎炸和烘烤**  — 傳統上，烘焙和油炸的概念是不同網頁內容管理系統之間的重要區別。 在CMS行話中，「烘烤」是指在發佈時讓資料認可至靜態檔案的概念，而「油炸」是指在請求時處理資料以供最終呈現（即即即及時）的概念。

**群集和負載平衡**  — 為了提高可用性並改善生產環境的效能，通常會合併多個作者和/或發佈執行個體（放入叢集中），方法是讓不同的使用者群組可以使用它們，或在Dispatcher設定後平衡它們的負載。

也可以合併內容存放庫的多個例項，以建立 *高可用性* JCR解決方案，然後可與AEM解決方案整合，以針對硬體與軟體故障提供最大程度的保護。 另請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) 以取得進一步資訊。

**元件**  — 在AEM中，元件是一種物件型別，其例項通常可透過從Sidekick拖放來建立。 舉例來說，AEM隨附的現成可用元件包括文字、標題、Tag Cloud、輪播、影像和清單元件，這些元件都可在執行階段從Sidekick取得。

**內容尋找器**  — 在製作模式中，「內容尋找器」是位於頁面左側的特殊面板（框架），視您在上方選取的標籤而定，會顯示影像、檔案、Flash資產、頁面、段落或存放庫資源的清單，您可以將這些資源從「內容尋找器」拖放至您正在處理的頁面（右方）。

**數位資產**  — 在AEM中，數位資產通常（通常）是影像和多媒體檔案。 如需詳細資訊，請參閱在DAM中使用數位資產。

**Dispatcher** - Dispatcher既是快取與負載平衡工具，也提供某些安全性保障。

**ExtJS Widget** - AEM中的大部分使用者介面元素都使用ExtJS，這是以JavaScript撰寫的協力廠商Widget程式庫。 ExtJS提供高效能、可自訂的UI Widget，以及設計良好且可擴充的元件模型。

**JCR、Java內容存放庫** - Java內容存放庫規格(JSR-283)提供抽象資料模型和應用程式設計介面，用於實現結合了檔案系統和物件資料庫功能的大規模可擴充NoSQL資料存放庫。 雖然您不需要詳盡瞭解JSR-283，但應花時間熟悉JCR的基本功能及其背後的資料模型，因為JCR才可能實現AEM的「一切都是內容」哲學。

本質上，JCR是節點和屬性的系統，節點可以從其他節點繼承，所有內容都作為屬性儲存 *值*. 請注意，除了一般繼承以外，JCR還允許使用「mixin」節點的概念，這可以啟用多個繼承的模型化。

JCR有許多預先定義的節點型別和屬性型別，但一般而言，輸入系統相當靈活，（事實上） JCR的強項之一就是允許以相同的方式儲存/管理結構化與非結構化內容。 也就是說，JCR可容納高度結構化的資料，但也可以容納任意的動態資料結構，而不受結構描述限制。

JCR的Java API適用的JavaDoc為 [此處](https://jackrabbit.apache.org/jcr/jcr-api.html).

在嘗試讀取JavaDoc或JCR規格本身之前，您可能需要先檢視 [此高階說明](/help/sites-developing/the-basics.md#java-content-repository) Adobe Experience Services實作的JCR數量。

**多站點管理員(MSM)** - AEM的MSM功能可協助客戶處理多語言和跨國內容，讓客戶在集中品牌推廣與本地化內容之間取得平衡。

**osgi** - OSGi是以服務為基礎的執行階段技術，為AEM的模組化Java開發提供基礎。 此架構不僅為程式碼資源（稱為套裝）提供高度動態（且安全）的類別載入和執行環境，而且可完全控制套裝所公開的各種服務的可見度和生命週期。 服務登入會提供結合生命週期動態（和版本需求）的合作模型。 OSGi解決了許多應用程式伺服器原本要解決的問題，但是以輕量、高度動態的方式解決的，因此可以使用熱部署服務（使新程式碼立即可用，而不需重新啟動伺服器）。

**Parsys，段落系統**  — 段落系統(parsys)是複合元件，可讓作者將不同型別的元件新增至頁面，並包含其他段落元件。 每個段落型別都表示為一個元件。 段落系統本身也是元件，包含其他段落元件。

**微核心**  — 存放庫中的每個工作區都可以個別設定，以透過特定微核心（管理資料讀取和寫入的類別）儲存其資料。 同樣地，也可以獨立設定存放庫範圍的版本存放區，以使用特定的微核心。 有許多不同的微核心可供使用，能夠以各種檔案格式或關聯式資料庫儲存資料。 (例如，有MongoDB、DB2或Oracle的持續性管理員) AEM的預設微核心為TarMK （請參閱下文）。

**發佈執行個體**  — 基於安全性、控管和其他原因，生產網站通常會將AEM例項劃分為作者例項和發佈例項。 如需部署架構（包括作者/發佈執行個體）的詳細資訊，請參閱AEM執行個體相關檔案。

**快速入門**  — 與許多其他程式不同，您是使用單一「快速入門」自我解壓縮的JAR檔案來安裝AEM。 第一次連按兩下JAR檔案時，就會自動安裝所需的一切。 快速入門JAR包含CRX存放庫（包括管理設施）、虛擬存放庫服務、索引和搜尋服務、工作流程服務、安全性和Web伺服器所需的所有檔案，以及CQ Servlet Engine (CQSE)和所有AEM服務。 沒有其他檔案可安裝：快速入門是獨立的。

第一次啟動「快速入門」時，會在背景中建立整個JCR相容的存放庫，這可能需要幾分鐘的時間。 初次啟動後，後續啟動會更快速，因為存放庫基礎架構已經奠定。

您可以適當地重新命名Quickstart檔案，以控制許多啟動選項(例如作用中的連線埠號碼以及相關AEM例項是否應為Publish例項或Author例項，等等)。 若要檢視這方面的選項清單，請在命令列上使用「 — help」執行JAR：

```shell
java -jar <quickstartfilename>.jar -help
```

**復寫代理**  — 復寫代理程式是AEM的核心，是用來將內容從製作環境發佈（啟動）到發佈環境的機制；從Dispatcher快取排清內容；將使用者產生的內容（例如表單輸入）從發佈環境傳回製作環境。

**支架**  — 使用支架，您可以建立包含欄位的表單（支架），這些欄位反映您想要用於頁面的結構，然後使用此表單以根據此結構輕鬆建立頁面。

**細分**  — 網站訪客造訪網站時，有不同的興趣和目標。 瞭解訪客的目標並達到他們的期望，是線上行銷的重要成功先決條件。 區段可透過分析和描述訪客的詳細資料來協助達成此目的。

**Sidekick** - Sidekick是出現在可編輯頁面上的浮動視窗，可從中拖曳新元件並執行套用至頁面的動作。

**Site Calyst** -SiteCatalyst為行銷人員提供一個可以測量、分析和最佳化多個行銷管道中所有線上方案的整合資料的位置。 您可以使用Adobe SiteCatalyst來分析來自AEM網站的資料。

**Tar儲存(TarMK)** - TarMK是AEM中的預設持續性系統。 雖然AEM可以設定為使用不同的持續性系統（例如MongoDB），但TarMK具有某些優勢，因為它是針對典型JCR使用案例進行效能最佳化（因此非常快速）、使用業界標準資料格式，並且可以快速輕鬆地備份。

**範本**  — 在AEM中，範本會指定特定型別的頁面。 它會定義頁面的結構（同時通常會指定縮圖影像和各種屬性）。 例如，您可以為產品頁面、網站地圖和聯絡資訊使用不同的範本。

**工作流程** - AEM Workflow系統允許建立涉及頁面或資產的自動化流程。
