---
title: HTML5表單的架構
seo-title: Architecture of HTML5 forms
description: HTML5表單會部署為內嵌AEM執行個體中的套件，並使用RESTful Apache Sling架構以HTTP/S的REST端點形式公開功能。
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# HTML5表單的架構{#architecture-of-html-forms}

## 架构 {#architecture}

HTML5表單功能會以套件形式部署在內嵌AEM執行個體中，並使用RESTful作為HTTP/S上的REST端點公開 [Apache Sling架構](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### 使用Sling框架 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 以資源為中心。 它會使用請求URL來先解析資源。 每個資源都有一個 **sling：resourceType** (或 **sling：resourceSuperType**)屬性。 接著，系統會根據此屬性、要求方法和要求URL的屬性，選取Sling指令碼來處理要求。 此Sling指令碼可以是JSP或servlet。 對於HTML5表單， **設定檔** 節點會充當sling資源和 **設定檔轉譯器** 當作sling指令碼，處理請求，以使用特定設定檔轉譯行動表單。 A **設定檔轉譯器** 是一種JSP，可從請求中讀取引數並呼叫Forms OSGi服務。

如需REST端點和支援的請求引數的詳細資訊，請參閱 [呈現表單範本](/help/forms/using/rendering-form-template.md).

當使用者從使用者端裝置(例如iOS或Android™瀏覽器)提出請求時，Sling會先根據請求URL解析設定檔節點。 此設定檔節點會顯示 **sling：resourceSuperType** 和 **sling：resourceType** 以決定可處理此表單轉譯器請求的所有可用指令碼。 接著，它會使用Sling要求選取器以及要求方法，以識別最適合處理此要求的指令碼。 請求到達設定檔轉譯器JSP後，JSP會呼叫Forms OSGi服務。

如需Sling指令碼解析的詳細資訊，請參閱 [AEM Sling速查表](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 或 [Apache Sling Url分解](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### 典型的表單處理呼叫流程 {#typical-form-processing-call-flow}

HTML5表單會快取處理（轉譯或提交）第一個請求中的表單所需的所有中間物件。 它不會快取相依於資料的物件，因為這類物件可能會變更。

Mobile Form會維護兩個不同層級的快取：PreRender快取和轉譯器快取。 preRender快取包含已解析範本的所有片段和影像，而Render快取則包含HTML等轉譯內容。

![HTML5表單工作流程](assets/cacheworkflow.png)

HTML5表單工作流程

HTML5表單不會快取遺失片段和影像參考的範本。 如果HTML5表單花費的時間超過正常時間，請檢查伺服器記錄檔中是否有遺漏參考和警告。 同時請確定未達到物件大小上限。

Forms OSGi服務會分兩個步驟處理請求：

* **版面配置與初始表單狀態產生**： Forms OSGi轉譯服務會呼叫Forms快取元件，以判斷表單是否已快取且未失效。 如果表單已快取且有效，則會從快取中提供產生的HTML。 如果表單失效，Forms OSGi轉譯服務會產生XML格式的初始表單版面和表單狀態。 此XML會由Forms OSGi服務轉換為HTML版面配置和初始JSON表單狀態，然後針對後續請求進行快取。
* **預先填入的Forms**：在轉譯時，如果使用者請求具有預先填入資料的表單，Forms OSGi轉譯服務會呼叫Forms服務容器，並使用合併的資料產生新的表單狀態。 不過，由於版面配置已在上述步驟中產生，因此此呼叫的速度會比第一次呼叫快。 此呼叫只會執行資料合併，並對資料執行指令碼。

如果表單中有任何更新，或表單內使用任何資產，表單快取元件會偵測到它，且該特定表單的快取會失效。 Forms OSGi服務完成處理之後，設定檔轉譯器jsp會將JavaScript程式庫參照和樣式新增至此表單，並將回應傳回給使用者端。 典型的網頁伺服器，例如 [Apache](https://httpd.apache.org/) 可在此搭配HTML壓縮使用。 網頁伺服器可大幅減少回應大小、網路流量，以及伺服器與使用者端電腦之間資料串流所需的時間。

當使用者提交表單時，瀏覽器會將表單狀態以JSON格式傳送至 [送出服務Proxy](../../forms/using/service-proxy.md)；然後提交服務Proxy會使用JSON資料產生資料XML，並將該資料XML提交至提交端點。

## 组件 {#components}

您需要AEM Forms附加元件套件才能啟用HTML5表單。 如需有關安裝AEM Forms附加元件套件的資訊，請參閱 [安裝和設定AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi元件(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**AdobeXFA Forms轉譯器(com.adobe.livecycle.adobe-lc-forms-core)** 是從Felix Admin Console的套件組合檢視檢視時HTML5 forms OSGi套件的顯示名稱(https://[主機]：[連線埠]/system/console/bundles)。

此元件包含用於轉譯、快取管理和組態設定的OSGi元件。

#### Forms OSGi服務 {#forms-osgi-service}

此OSGi服務包含將XDP轉譯為HTML的邏輯，並處理表單提交以產生資料XML。 此服務使用Forms服務容器。 Forms服務容器會在內部呼叫原生元件 `XMLFormService.exe` 執行處理作業的URL。

如果收到轉譯要求，此元件會呼叫Forms服務容器以產生版面和狀態資訊，系統會進一步處理這些資訊以產生HTML和JSON表單DOM狀態。

此元件也負責從提交的表單狀態JSON產生資料XML。

#### 快取元件 {#cache-component}

HTML5表單會使用快取來最佳化輸送量和回應時間。 您可以設定快取服務的層級，以微調效能與空間使用率之間的平衡。

<table>
 <tbody>
  <tr>
   <th>快取策略</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>无</td>
   <td>不要快取成品<br /> </td>
  </tr>
  <tr>
   <td>保守</td>
   <td>僅快取在表單轉譯之前產生的中繼成品，例如包含內嵌片段和影像的範本</td>
  </tr>
  <tr>
   <td>積極進取</td>
   <td>快取呈現的HTML內容<br /> 快取在Conservative層級快取的所有成品。<br /> <strong>注意</strong>：此策略可提供最佳效能，但會消耗更多記憶體來儲存快取的成品。</td>
  </tr>
 </tbody>
</table>

HTML5表單使用LRU策略執行記憶體內快取。 如果快取策略設為「無」，將不會建立快取，並將清除現有的快取資料（若有的話）。 除了快取策略之外，您也可以設定記憶體中的總快取大小，這有助於使快取大小有最大限制，如果超過此限制，將使用LRU模式來釋放快取資源。

>[!NOTE]
>
>記憶體內部快取不會在叢集節點之間共用。

#### 設定服務 {#configuration-service}

Configuration Service可讓您調整HTML5表單的組態引數和快取設定值。

若要更新這些設定，請前往CQ FelixAdmin Console(位於https://&lt;&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr)，搜尋並選取「行動Forms設定」。

您可以使用設定服務來設定快取大小或停用快取。 您也可以使用「偵錯選項」引數來啟用偵錯。 如需有關除錯表單的詳細資訊，請參閱 [偵錯HTML5表單](/help/forms/using/debug.md).

### 執行階段元件(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

執行階段套件包含用於轉譯HTML表單的使用者端程式庫。

**執行階段套件中提供的重要元件：**

#### 指令碼引擎 {#scripting-engine}

Adobe XFA實作支援兩種指令碼語言，以便在表單中啟用使用者定義的邏輯執行：JavaScript和FormCalc。

HTMLForms的指令碼引擎是以JavaScript撰寫，以支援這兩種語言的XFA指令碼API。

在轉譯時，FormCalc指令碼會在伺服器上轉譯（和快取）為JavaScript，對使用者或設計人員而言是透明的。

此指令碼引擎使用ECMAScript5的某些功能，例如Object.defineProperty。 引擎/程式庫會以具有類別名稱的CQ使用者端程式庫形式提供 **xfaforms.profile**. 它也提供 **FormBridge API** 啟用外部入口網站或應用程式與表單互動。 使用FormBridge時，外部應用程式能以程式設計方式隱藏特定元素、取得或設定其值，或變更其屬性。

如需詳細資訊，請參閱 [Form Bridge](/help/forms/using/form-bridge-apis.md) 文章。

#### 版面引擎 {#layout-engine}

HTML5表單的版面與視覺效果以SVG1.1、jQuery、BackBone和CSS3功能為基礎。 表單的初始外觀會在伺服器產生並快取。 使用者端會管理該初始版面的微調以及對表單版面所做的任何進一步增量變更。 為實現此目的，Runtime套件包含以JavaScript撰寫並以jQuery/Backbone為基礎的版面引擎。 此引擎會處理所有動態行為，例如新增/移除可重複例項、可成長物件配置。 此版面引擎會一次轉譯一個表單頁面。 最初，使用者只檢視一個頁面，而水準卷軸只代表第一個頁面。 但是，當使用者向下捲動時，下一頁開始呈現。 此逐頁轉譯可減少在瀏覽器中轉譯第一頁所需的時間，並增強表單的感知效能。 此引擎/程式庫屬於具有類別名稱的CQ使用者端程式庫 **xfaforms.profile**.

版面引擎也包含一組用於從使用者擷取表單欄位值的Widget。 這些Widget的模型化為 [jQuery UI Widget](https://api.jqueryui.com/jQuery.widget/) 可實作特定額外合約，以順暢地與版面引擎搭配運作。

如需Widget和對應合約的詳細資訊，請參閱 [HTML5表單的自訂Widget](/help/forms/using/introduction-widgets.md).

#### 样式 {#styling}

與HTML元素相關聯的樣式會內嵌或根據內嵌CSS區塊新增。 有些常見樣式與形式無關，但屬於類別名稱為xfaforms.profile的CQ使用者端程式庫。

除了預設的樣式屬性外，每個表單元素也包含根據元素型別、名稱和其他屬性的特定CSS類別。 使用這些類別，使用者可以透過指定他們自己的CSS來重新樣式化元素。

如需預設樣式和類別的詳細資訊，請參閱 [樣式簡介](/help/forms/using/css-styles.md).

#### 伺服器端指令碼和Web服務 {#server-side-script-and-web-services}

任何標示為在伺服器上執行或標示為呼叫Web服務的指令碼（無論標示為要執行的位置為何）一律會在伺服器上執行。

使用者端指令碼引擎：

1. 以JSON的形式，向傳遞目前表單狀態的伺服器發出同步呼叫
1. 在伺服器上執行指令碼或Web服務
1. 產生新的JSON狀態
1. 傳回回應時，合併使用者端上的新JSON狀態。

#### 本地化資源組合 {#localization-resource-bundles}

HTML5表單支援義大利文(it)、西班牙文(es)、巴西葡萄牙文(pt_BR)、簡體中文(zh_CN)、繁體中文（僅有限支援） (zh_TW)、韓文(ko_KR)、英文(en_US)、法文(fr_FR)、德文(de_DE)和日文(ja)語言。 根據在請求標頭中收到的地區設定，相應的資源組合會傳送給使用者端。 此資源套件會以類別名稱的CQ使用者端程式庫形式新增至設定檔JSP **xfaforms.I18N**. 您可以覆寫在設定檔中提取地區設定套件的邏輯。

### Sling元件(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling套件包含與設定檔和設定檔轉譯器相關的內容。

#### 配置文件 {#profiles}

設定檔是Sling中的資源節點，代表表單或Forms系列。 在CQ層級，這些設定檔是JCR節點。 節點位於 **/content** 資料夾位於JCR存放庫中，並可位於 **/content** 資料夾。

#### 設定檔轉譯器 {#profile-renderers}

設定檔節點具有屬性 **sling：resourceSuperType** 含值 **xfaforms/profile**. 此屬性會在內部將請求轉寄給位於以下位置之設定檔節點的sling指令碼： **/libs/xfaforms/profile** 資料夾。 這些指令碼是JSP頁面，是用來組合HTML表單和必要JS/CSS人工因素的容器。 這些頁面包含對下列專案的參照：

* **xfaforms.I18N。&lt;locale>**：此程式庫包含當地語系化的資料。
* **xfaforms.profile**：此程式庫包含XFA指令碼和版面引擎的實作。

這些程式庫被模型化為CQ使用者端程式庫，這些程式庫利用CQ架構JavaScript程式庫的自動串連、縮制和壓縮功能。
如需CQ使用者端程式庫的詳細資訊，請參閱 [CQ Clientlib檔案](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

如上所述，設定檔轉譯器JSP透過sling include呼叫Forms服務。 此JSP也會根據管理員設定或請求引數設定各種偵錯選項。

HTML5表單可讓開發人員建立設定檔和設定檔轉譯器，以自訂表單的外觀。 例如，HTML表單可讓開發人員將表單整合到面板或 &lt;div> 現有HTML入口網站的區段。
如需建立自訂設定檔的詳細資訊，請參閱 [建立自訂設定檔](/help/forms/using/custom-profile.md).
