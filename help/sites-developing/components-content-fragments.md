---
title: 內容片段的元件
seo-title: Components for Content Fragments
description: AEM內容片段會建立並管理為與頁面無關的資產
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 3%

---

# 內容片段的元件{#components-for-content-fragments}

## 用於片段編寫的元件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建議擴充或變更片段編輯器中使用的實際元件，因為它們仍可能會變更。

請參閱 [內容片段管理API — 使用者端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## 用於頁面編寫的元件 {#components-for-page-authoring}

>[!CAUTION]
>
>此 [內容片段核心元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 現在建議使用。 另請參閱 [開發核心元件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 以取得更多詳細資料。
>
>本節詳細說明用於內容片段的原始元件(**內容片段** 在 **一般** 群組)。

>[!NOTE]
>
>另請參閱 [轉譯專用內容片段設定元件](/help/sites-developing/content-fragments-config-components-rendering.md) 以取得進一步資訊。

Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变体。[然後，您可以在編寫內容頁面時使用這些片段及其變數](/help/sites-authoring/content-fragments.md). 您也可以透過以下方式使用現有的內容片段資產： [將其從資產瀏覽器拖曳至頁面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （如同其他以資產為基礎的元件，例如基礎元件影像）。 現成可用的內容片段元件只會顯示一個 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 引用內容片段的ID。 您可以使用元件對話方塊來定義 [元素、變數和片段段落範圍](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 要顯示在頁面上的資訊。

>[!NOTE]
>
>此內容片段元件在AEM 6.2中作為文章元件的增強版本引入，但已過時。

>[!NOTE]
>
>傳統UI中不支援內容片段。

### 定义 {#definition}

此 **內容片段** 元件用於儲存內容片段資產的參考（有效增強文字資產）。 內容片段的資源型別為：

`dam/cfm/components/contentfragment/contentfragment`

參照是在屬性中定義：

`fileReference`

只有觸控式UI的編輯器完全支援內容片段元件，其中包括使用者端程式庫：

`cq.authoring.editor.plugin.cfm`

此程式庫會將內容片段的特定功能新增至編輯器。 例如，支援在頁面上新增和設定內容片段的功能、在資產瀏覽器中搜尋內容片段資產的功能，以及在側面板中搜尋關聯內容的功能。

### 中間內容 {#in-between-content}

此 **內容片段** t元件可讓您在顯示的不同段落之間放置其他元件 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 基本上，顯示的元素是由不同的段落所組成（每個段落都標有歸位字元）。 在每個段落之間，您可以使用其他元件插入內容。

從技術角度來看，顯示的元素* *的每個段落都存在於自己的parsys中，您在段落之間新增的每個元件都將（在標題下）插入parsys中。

換言之，如果內容片段元件的例項由三個段落組成，則元件在存放庫中會有三個不同的parsys。 所有新增至內容片段的中間內容實際上將位於這些parsys內。

在存放庫中，中間內容會相對於其在整個段落結構中的位置儲存，也就是說，它不會附加至實際的段落內容。

為了說明這一點，讓我們考慮我們有：

* 由三個段落組成的內容片段例項
* 而且某些內容已插入第二段之後

   * 這表示內容會儲存在第二個parsys中。

基本上，如果此例項的段落結構變更（透過變更顯示的變數、元素或段落範圍），可能會影響內容片段內容時顯示的中間內容：

* 已編輯，並在第二個段落之前新增另一個段落：

   * 中間內容將顯示在新建立的段落之後（第二個parsys現在包含新建立的段落）。

* 已編輯並移除第二段：

   * 中間內容將顯示在先前為第三個的段落之後（現在第二個parsys包含先前的第三個段落）。

* 設定為只顯示第一段：

   * 將不會顯示中間內容（由於新設定，第二個parsys不再呈現）。

### 自訂內容片段元件 {#customizing-the-content-fragment-component}

若要使用現成的內容片段元件作為擴充的藍圖，您應遵守下列合約：

* 重複使用HTL演算指令碼及其關聯的POJO，檢視中間內容功能的實作方式。
* 重複使用內容片段節點： `cq:editConfig`

   * 此 `afterinsert`/ `afteredit`/ `afterdelete` 監聽器可用來觸發JS事件。 這些事件將在以下位置處理： `cq.authoring.editor.plugin.cfm` 使用者端資源庫，以在側面板中顯示關聯內容。
   * 此 `cq:dropTargets` 設定為支援拖曳內容片段資產。
   * `cq:inplaceEditing` 設定為支援在頁面編輯器中製作內容片段。 片段就地編輯器是在 `cq.authoring.editor.plugin.cfm` 使用者端程式庫，並允許快速連結以開啟目前的 [元素/變數](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 在 [片段編輯器](/help/assets/content-fragments/content-fragments-variations.md).

### 資產在轉譯前重新寫入 {#asset-rewriting-before-rendering}

內容片段管理使用內部呈現程式來產生頁面的最終HTML輸出。 這供內容片段元件內部使用，也供在參考頁面上更新參考片段的背景程式使用。

在內部，Sling重寫程式用於該轉譯。 個別設定可在下列位置找到： `/libs/dam/config/rewriter/cfm` 如有需要，可調整和。 請參閱 [Apache Sling重寫程式](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 以取得詳細資訊。

>[!CAUTION]
>
>如果您確實調整/覆蓋重寫程式的設定：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然後 `serializerType` **必須** 更新至：
>
>* `serializerType="html5-serializer"`


現成可用的設定會使用下列轉換器：

* `transformer-cfm-payloadfilter`  — 用於擷取 `body` 部分( `<body>...</body>`)僅片段HTML的

* `transformer-cfm-parfilter`  — 如果指定了段落範圍，則篩選掉不需要的段落（可以使用內容片段元件完成）
* `transformer-cfm-assetprocessor`  — 內部用於擷取片段中內嵌的資產清單

演算程式透過以下方式公開： [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 如有需要，自訂元件可運用和（例如）。
