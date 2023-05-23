---
title: OSGi組態設定
seo-title: OSGi Configuration Settings
description: 本文詳細說明與專案實作相關的OSGi組態設定（根據套件列示）。 此清單可作為指引，且並非詳盡無遺。
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '3430'
ht-degree: 0%

---

# OSGi組態設定{#osgi-configuration-settings}

[osgi](https://www.osgi.org/) 是AEM技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi 」*提供標準化的基本概念，讓應用程式可由小型、可重複使用的合作元件所建構。 這些元件可組成應用程式並部署*「。

此功能可讓您在個別停止、安裝和啟動套件組合時，輕鬆管理套件組合。 系統會自動處理相依性。 每個OSGi元件(請參閱 [OSGi規格](https://docs.osgi.org/specification/))包含在多個套件組合之一中。 使用AEM時，有數種方法可管理這類套裝的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

下列OSGi組態設定（根據套件組合列出）與專案實作相關。 並非所有列出的設定都需要調整，有些是為了協助您瞭解AEM的運作方式。

>[!CAUTION]
>
>此清單旨在作為指引，並非詳盡無遺。 並非所有套件組合都列出，也不是某些套件組合的所有引數都列出。
>
>所需的設定因專案而異。
>
>請參閱Web主控台，以取得使用的值以及引數的詳細資訊。

>[!NOTE]
>
>OSGi設定差異工具，屬於 [AEM工具](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=zh-Hans)，可用來列出預設的OSGi設定。

>[!NOTE]
>
>AEM中的特定功能區域可能需要其他套件組合。 在這些情況下，您可在與適當功能相關的頁面上找到設定詳細資訊。

**AEM復寫事件監聽器** 設定：

* 此 **執行模式**，其中復寫事件會分發給監聽器。 例如，如果定義為author，則是「啟動」復寫的系統。

* 新增執行模式 **發佈** 如果專案程式碼在發佈環境中處理復寫事件（反向復寫）。 例如，使用Dispatcher從發佈環境排清時，或發生對其他發佈執行個體的標準復寫時。

**AEM儲存區域變更接聽程式** 設定：

* 此 **路徑**，可監聽準備好要發佈的存放庫事件的位置。

**CRX Sling使用者端存放庫** 設定對基礎內容存放庫的存取權。

* 此 **管理員密碼** 安裝後應加以變更，以確保 [安全性](/help/sites-administering/security-checklist.md) 執行個體的。
* 您不一定要進行其他變更，也必須謹慎行事，因為變更可能會影響對存放庫的存取。

**Apache Felix OSGi管理主控台** 設定：

* **外掛程式**，則為中可用的主要導覽專案（主控台外掛程式）。 **Apache Felix Web管理主控台** 作為頂層功能表專案。 停用不需要的任何專案，因為每個專案都需要空間和資源。

>[!CAUTION]
>
>請務必設定下列專案：
>
>**使用者名稱** 和 **密碼**，此憑證用於存取Apache Felix Web管理主控台本身。
>初次安裝後必須變更密碼，以確保 [安全性](/help/sites-administering/security-checklist.md) 執行個體的。

>[!NOTE]
>
>在啟動時（在存放庫可用之前），應視需要使用Felix主控台進行此設定。

**Apache Sling可自訂請求資料記錄器** 設定：

* **記錄器名稱** 和 **記錄格式** 設定請求和存取記錄的位置和格式(預設： `request.log`)。 在分析與網頁鏈相關的效能或偵錯功能時，此記錄檔是必要的。 它與 [Apache Sling請求記錄器](#apacheslingrequestlogger).

另請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling事件執行緒集區** 設定：

* **最小集區大小** 和 **最大集區大小**，用來存放事件執行緒的集區大小。

* **佇列大小**，如果集區已耗盡，則為對話串佇列的大小上限。
建議值為 `-1` 因為它會將佇列設定為無限制。 如果設定了限制，超過限制時可能會發生損失。

* 變更這些設定有助於在有大量事件的情況下提供效能。 例如，使用大量的AEM DAM或工作流程。
* 您情境的特定值應使用測試來建立。
* 這些設定可能會影響執行個體的效能，因此請勿無故變更，並應加以妥善考慮。

**Apache SlingGETServlet** 設定轉譯的某些層面：

* **自動索引** 啟用/停用瀏覽時目錄呈現。
* **啟用** （或停用）預設轉譯，例如 **HTML**， **純文字**， **JSON**，或 **XML**.
請勿停用JSON。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Apache Sling JavaScript處理常式** 設定以指令碼(servlet)編譯.java檔案的設定。

某些設定可能會影響效能。 請儘可能停用這些設定，尤其是針對生產執行個體。

* **來源VM** 和 **目標VM**，定義作為執行階段JVM使用的JDK版本

* 對於生產執行個體：

   * disable **產生偵錯資訊**

**Apache Sling JCR安裝程式** 這些引數可能不需要設定，但在開發或偵錯時可能很實用。 例如，安裝資料夾對於入庫或出庫或建立套件很有用。

* **安裝資料夾名稱regexp** 和 **安裝資料夾的最大階層深度**  — 指定要在存放庫資料夾中搜尋要安裝的資源的位置和深度。 當使用萬用字元時（如中的）。&#42;/install)會搜尋所有適當的相符專案，例如 `/libs/sling/install` 和 `/libs/cq/core/install`.

* **搜尋路徑**，jcrinstall會搜尋要安裝的資源的路徑清單，以及指出該路徑的加權因子的數字。

**Apache Sling作業事件處理常式** 設定管理作業排程的引數：

* **重試間隔**， **最大重試次數**， **最大平行作業數**， **認可等待時間**，以及其他專案。

* 變更這些設定可以在大量工作的情況下改善效能；例如，大量使用AEM DAM和工作流程。
* 您情境的特定值應使用測試來建立。
* 請勿無故變更這些設定，只有在經過適當考慮後才會變更。

**Apache Sling JSP指令碼處理常式** 設定JSP指令碼處理常式的效能相關設定。 若要改善效能，您應該儘可能停用。

尤其是生產執行個體：

* disable **產生偵錯資訊**
* disable **保留產生的Java™**
* disable **對應的內容**
* disable **顯示來源片段**

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Apache Sling記錄設定** 設定：

* **記錄層級** 和 **記錄檔**，以定義中央記錄組態(error.log)的位置和記錄層級。 層級可以設定為其中之一 `DEBUG`， `INFO`， `WARN`， `ERROR`、和 `FATAL`.

* **記錄檔數目** 和 **記錄檔臨界值** 定義記錄檔的大小和版本輪換。

* **訊息模式** 會定義記錄訊息的格式。

另請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md#global-logging) 和 [Sling記錄](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling記錄記錄器設定（工廠設定）** 設定：

* **記錄層級**， **記錄檔** 和 **訊息格式** 以定義記錄檔和訊息的詳細資訊。

* **Logger** 以定義類別；例如，僅記錄com.day.cq。

* 透過使用 **工廠組態**，可新增任意數量的其他設定，以符合所需的各種記錄層級和類別。
* 這類設定在開發期間很有幫助；例如，將特定服務的TRACE訊息記錄在特定記錄檔中。
* 在生產環境中，這類設定很有幫助；例如，將特定服務的相關訊息記錄到個別記錄檔，以便更輕鬆地進行監視。

另請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling記錄寫入器設定（工廠設定）** 設定：

* **記錄檔** 定義記錄檔是否存在。
* **記錄檔數目** 以定義版本輪換。

* 寫入器可由 **Apache Sling記錄記錄器設定** 設定。

* 這類設定在開發期間很有幫助；例如，將特定服務的TRACE訊息記錄在特定記錄檔中。
* 在生產環境中，這類設定很有幫助；例如，將特定服務的相關訊息記錄到個別記錄檔，以便更輕鬆地進行監視。

另請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling主要Servlet** 設定：

* **每個請求的呼叫數** 和 **遞回深度** 保護您的系統不受無限遞回和過度指令碼呼叫的影響。

**Apache Sling MIME型別服務** 設定：

* **MIME型別** 以將專案所需的型別新增到系統。 這麼做可讓 `GET` 要求檔案設定連結檔案型別和應用程式所需的正確內容型別標頭。

**Apache Sling查閱者篩選器** 若要解決CRX WebDAV和Apache Sling中的跨網站請求偽造(CSRF)的已知安全性問題，您必須設定反向連結篩選器。

反向連結篩選服務是OSGi服務，可讓您設定：

* 應該篩選哪些http方法
* 是否允許空的反向連結標頭
* 以及除了伺服器主機之外還允許使用的伺服器清單。

請參閱 [安全性檢查清單 — 跨網站請求偽造問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 以取得更多詳細資料。

>[!NOTE]
>
>Apache Sling反向連結篩選取決於快速修正套件的安裝。

**Apache Sling請求記錄器** 設定：

* 用來定義記錄請求的方式的各種引數。
* **啟用請求記錄**，以啟用或停用。

* **啟用存取記錄檔**，以啟用或停用。

與 [Apache Sling可自訂請求資料記錄器](#apacheslingcustomizablerequestdatalogger).

另請參閱 [AEM記錄](/help/sites-deploying/configure-logging.md) 和 [Sling記錄](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling資源解析器工廠** 設定Sling資源解析的核心層面：

* **資源搜尋路徑**，新增任何專案專屬路徑(但不移除 `/libs` 或 `/apps`)。

* **虛擬URL** 以定義虛名URL對應。

* **URL對應** 以定義任何別名。 例如，從 `/content` 至 `/`.

* **對應位置**，對應程式設定已外部化於 `/etc/map`.

* 使用本機安裝(例如，使用 `https://localhost:4502/system/console/jcrresolver`)，以判斷作用中的資源解析程式。

請參閱： [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>在存放庫中設定這些選項。
>
>否則，對下列專案所做的變更： **URL對應** 下次啟動時，使用Felix主控台可能會被AEM覆寫。

**Apache Sling Servlet/指令碼解析器和錯誤處理常式** Sling Servlet和Script Resolver有多個任務：

1. 它被用作 `ServletResolver` 以選取要呼叫以處理請求的Servlet或指令碼。

1. 它充當 `SlingScriptResolver`.

1. 它會透過實作 `ErrorHandler` 介面，使用與用來解析請求處理servlet和指令碼相同的演演算法來選取錯誤處理servlet和指令碼。

您可以設定各種引數，包括：

* **執行路徑**  — 列出搜尋可執行指令碼的路徑。 透過設定特定路徑，您可以限制可以執行的指令碼。 如果未設定任何路徑，則會使用預設值( `/` = root)，允許執行所有指令碼。
如果設定的路徑值以斜線結尾，則會搜尋整個子樹狀結構。 若沒有此等尾端斜線，只有在指令碼完全相符時，才會執行此指令碼。

* **指令碼使用者**  — 此選擇性屬性可指定用於讀取指令碼的存放庫使用者帳戶。 若未指定帳戶，則 `admin` 預設會使用user。

* **預設副檔名**  — 使用預設行為的擴充功能清單。 資源型別的最後一個路徑區段可作為指令碼名稱使用。

**Apache HTTP元件Proxy設定**  — 使用Apache HTTP使用者端的所有程式碼的Proxy設定，在建立HTTP時使用。 例如，在復寫上。

建立組態時，請勿變更工廠組態。 請改用此處提供的組態管理員來建立此元件的出廠組態： **https://localhost:4502/system/console/configMgr/**. Proxy設定可在 **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>在AEM 6.0及舊版中，Proxy是在Day Commons HTTP Client中設定。 自AEM 6.1及更新版本起，Proxy設定已移至「Apache HTTP元件Proxy設定」而非「Day Commons HTTP Client」設定。

**Day CQ Antispam** 設定使用的反垃圾郵件服務(Akismet)。 此功能需要您註冊下列專案：

* **提供程序**
* **API金鑰**
* **已註冊的URL**

**AdobeGraniteHTML程式庫管理員** 設定以控制使用者端程式庫（css或js）的處理，包括基礎結構的顯示方式等。

* 對於生產執行個體：

   * 啟用 **最小化** （移除CRLF和空白字元）。
   * 啟用 **Gzip** （允許透過一個請求來壓縮及存取檔案）。
   * disable **偵錯**
   * disable **計時**

* 若為JS開發（尤其是在firebugging/debugging時）：

   * disable **最小化**
   * 啟用 **偵錯** 分隔檔案以進行偵錯，並與fire bug搭配使用。
   * 啟用 **計時** 如果對時間有興趣。
   * 啟用 **偵錯** 主控台以檢視JS主控台記錄訊息。

>[!CAUTION]
>
>變更其中一項的設定時 **最小化** 或 **Gzip**，刪除clientlibs快取的內容。 另請參閱 [知識庫文章](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=zh-Hans) 以取得詳細資訊。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Day CQ HTTP標頭驗證處理常式** HTTP要求的基本驗證方法的全系統設定。

使用時 [封閉式使用者群組](/help/sites-administering/cug.md)，您可以設定（其中包括）下列專案：

* **HTTP範圍**
* 此 **預設登入頁面**

**Day CQ連結檢查器服務** 檢查並視需要設定：

* **排程器週期** 定義自動檢查外部連結的間隔。

* Check **錯誤的連結容許間隔** 在外部連結失敗後被視為錯誤的時段內。
* **連結檢查覆寫模式**，以定義要從連結檢查中排除的任何路徑。

**Day CQ連結檢查器任務** 設定單一連結檢查器工作（檢查外部連結的工作）的設定：

* 檢查中定義的間隔 **良好的連結測試間隔** 和 **錯誤的連結測試間隔**

* 檢查連結時，與外部存取所需的網際網路存取代理和NTLM相關的各種引數。

**Day CQ郵件服務** 設定郵件伺服器的主機名稱和存取詳細資訊。 請參閱設定郵件服務區段。

**Day CQ MCM電子報** 設定與Newsletter搭配使用的各種設定。

**Day CQ根目錄對應** 設定：

* **目標路徑** 以定義向何處發出「 `/`」已重新導向至。

AEM中有兩個可用的UI：

* 觸控式UI是標準UI
* 而且已棄用的傳統UI仍可完全運作

您可以使用AEM根目錄對應來設定您要設為執行個體預設的UI：

* 若要將觸控式UI設為預設UI，請 **目標路徑** 應指向以下專案：

   ```shell
      /projects.html
   ```

* 若要將傳統UI設為預設UI，請 **目標路徑** 應指向以下專案：

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>在標準安裝中，觸控最佳化的UI是預設的UI。

**AdobeGranite SSO驗證處理常式**  — 設定SSO （單一登入）詳細資料。 企業製作設定通常需要這些詳細資訊，通常使用LDAP。

可以使用各種設定屬性：

* **路徑**
此驗證處理常式作用中的路徑。 如果此引數留空，則會停用驗證處理常式。 例如，路徑/會導致驗證處理常式用於整個存放庫。

* **服務排名**
OSGi框架服務排名值用於指示呼叫此服務所用的順序。 此值是一個 
`int` 值越高，代表優先順序越高。
默认值为 `0`.

* **頁首名稱**
可能包含使用者ID的標頭名稱。

* **Cookie名稱**
可能包含使用者ID的Cookie名稱。

* **引數名稱**
可能提供使用者ID的要求引數名稱。

* **使用者地圖**
對於選取的使用者，從HTTP請求擷取的使用者名稱可以取代為認證物件中的其他名稱。 此處定義對應。 若使用者名稱 
`admin` 會在地圖的兩側顯示，因此會忽略對應。 字元「=」必須以前導「\」逸出。

* **格式**
表示提供使用者ID的格式。 使用:

   * `Basic` 如果使用者ID是以HTTP基本驗證格式編碼
   * `AsIs` 如果使用者ID是以純文字提供，或任何規則運算式套用的值都應依原樣或任何規則運算式使用

**Day CQ WCM偵錯篩選器** 這在開發時很有用，因為它允許在存取頁面時使用？debug=layout之類的尾碼。 例如，https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout會提供開發人員可能感興趣的版面配置資訊。

* 為確保效能和安全性，請在生產執行個體上停用。

**Day CQ WCM篩選器** 設定：

* **WCM模式** 以定義預設模式。
* 在作者執行個體上，此模式可能是 `edit`， `disable,preview`，或 `analytics`.
其他模式可從sidekick或尾碼存取 `?wcmmode=disabled` 可用來模擬生產環境。

* 在發佈執行個體上，此模式必須設定為 `disabled` 以確保無法存取其他模式。

>[!NOTE]
>
>如果您在中執行AEM，系統會自動為生產執行個體設定此設定 [生產就緒模式](/help/sites-administering/production-ready.md).

**Day CQ WCM連結檢查器設定器** 設定：

* **重寫設定清單** 指定內容連結檢查器組態的位置清單。 這些設定可以根據執行模式。 由於連結檢查器設定可能不同，因此區分製作和發佈環境時，這個事實很重要。

**Day CQ WCM頁面管理員工廠** 設定：

* **頁面子樹狀結構啟用檢查** （沒有復寫許可權）刪除或移動頁面的方式（即使頁面未啟動）。

**Day CQ WCM頁面處理器** 設定：

* **路徑**，此為系統觸發前監聽頁面修改的位置清單 `jcr:Event`.

**Adobe頁面曝光數追蹤器** 對於作者執行個體，請設定如下：

* **sling.auth.requirements**：將此屬性的值設為 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>此設定允許向追蹤服務提出匿名請求。

>[!NOTE]
>
>另請參閱 [頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions) 以取得詳細資訊。

**Day CQ WCM頁面統計資料** 對於發佈執行個體，請設定：

* **用於傳送資料的URL** 設定用於追蹤頁面統計資料的URL （在追蹤器請求通過Dispatcher時至關重要）；例如，預設為 `https://localhost:4502/libs/wcm/stats/tracker`.

* **追蹤指令碼已啟用** 若要啟用( `true`)或停用( `false`)在頁面上納入追蹤指令碼。 默认值为 `false`。

>[!NOTE]
>
>另請參閱 [頁面印象](/help/sites-deploying/configuring.md#enabling-page-impressions) 以取得詳細資訊。

**Day CQ WCM版本管理員** 控制是否及如何在系統中管理版本：

* **啟動時建立版本**，已在標準安裝中啟用
* **啟用清除**

* **清除路徑**，即搜尋動作搜尋的路徑。
* **隱含版本設定路徑**，即使用隱含版本設定的路徑。

* **最大版本期限**，版本的最長存留期（以天為單位）

* **最大版本數量**，要保留的最大版本數量

另請參閱 [版本清除](/help/sites-deploying/version-purging.md) 以取得詳細資訊。

**Day CQ工作流程電子郵件通知服務** 針對工作流程傳送的通知設定電子郵件設定。

**CQ重寫程式HTML剖析器處理站**

控制CQ重寫程式的HTML剖析器。

* **要處理的其他標籤**  — 您可以新增或移除要由剖析器處理的HTML標籤。 預設會處理下列標籤：A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD。
* **保留大小寫**  — 依預設，HTML剖析器會以駝峰式大小寫轉換屬性(例如 `eBay`)至小寫(例如， `ebay`)。 您可以關閉此設定以保留駝峰式大小寫屬性。 使用前端架構(例如Angular2)時，此設定很有用。

**Day Commons JDBC連線集區** 設定對作為內容來源的外部資料庫的存取權。

工廠組態，因此可以設定多個執行個體。

**CDN重寫程式** 必須確保AEM和CDN之間的通訊，以便以安全的方式將資產/二進位檔傳送給一般使用者。 此程式涉及下列兩項工作：

* 第一次透過CDN從AEM存取資源（或在快取中資源過期後）。
* 安全地存取CDN中快取的資源。 在CDN中快取資源後，要求不會前往AEM，而且所有有權存取該資源的使用者應該會從CDN提供服務。

AEM提供重寫程式，可將內部資產URL重寫至外部CDN URL。 它會重寫要傳遞至CDN的連結，包括JWS簽名和過期時間，以允許安全地存取資產。 此功能將用於編寫執行個體。

整體流程如下：

1. 使用者透過AEM進行驗證並請求包含資產的頁面。
1. 請求的頁面包含與類似的資產 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. 重寫程式會將連結轉換為包含JWS簽名的CDN URL：
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. 然後使用者的瀏覽器將資產請求轉送至CDN伺服器
1. AEM CDN應設定為將請求與 `cdn_sign` 引數。
1. 驗證處理常式會驗證 `cdn_sign` 引數並傳回資產至CDN，再傳送給使用者

使用者的瀏覽器、CDN和AEM之間的流量視覺化如下所示。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>此功能僅對AEM作者執行個體啟用。

**CDNConfigServiceImpl** 提供CDN設定

CDN重寫功能可透過以下方式啟用： **CDN發佈網域名稱** com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl的設定中。

此服務也包含其他設定選項，例如啟用/停用CDN重新寫入、執行CDN重新寫入的路徑首碼、TTL值和通訊協定（HTTP或HTTPS）。

**CDNRewriter** 將內部影像URL重寫為CDN URL的重寫程式

此 **標籤屬性** com.adobe.cq.cdn.rewriter.impl.CDNRewriter中的值可定義，以便只重寫選擇性影像連結。
