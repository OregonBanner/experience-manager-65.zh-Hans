---
title: 模板
description: 建立作為新頁面基礎的頁面時，會使用範本。
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# 模板{#templates}

範本在AEM中的不同時間點使用：

* [建立頁面時，請選取範本](#templates-pages). 此範本用作新頁面的基礎。 範本會定義頁面的結構、任何初始內容，以及 [元件](/help/sites-authoring/default-components.md) （設計屬性）。

* [建立內容片段時，您也可以選取範本](#templates-content-fragments). 此範本定義結構、初始元素和變數。

以下範本將詳細說明：

* [頁面範本 — 可編輯](/help/sites-developing/page-templates-editable.md)
* [頁面範本 — 靜態](/help/sites-developing/page-templates-static.md)
* [內容片段範本](/help/sites-developing/content-fragment-templates.md)
* [最適化範本演算](/help/sites-developing/templates-adaptive-rendering.md)

## 範本 — 頁面 {#templates-pages}

AEM現在提供兩種基本型別的範本來建立頁面：

>[!NOTE]
>
>使用範本時 [建立頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)，沒有可見的差異（對頁面作者而言），也沒有指示使用的範本型別。

### 可编辑模板 {#editable-templates}

可編輯的範本現在被認為是使用AEM開發的最佳實務。

可編輯範本的優點：

* 可以是 [已建立](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 和 [已編輯](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 您的作者。

* 引入此功能，可讓您為使用範本建立的任何頁面定義下列內容：

   * 結構
   * 初始內容
   * 內容原則

* 建立新頁面後，頁面和範本之間會維持動態連線。 此連線表示範本結構的變更會反映在使用該範本建立的任何頁面上；初始內容的變更不會反映出來。
* 使用內容原則（從範本編輯器編輯）來儲存設計屬性（不使用頁面編輯器中的設計模式）。
* 儲存在 `/conf`
* 另請參閱 [可編輯的範本](/help/sites-developing/page-templates-editable.md) 以取得進一步資訊。

>[!NOTE]
>
>另請參閱 [使用可編輯的頁面範本來開發Experience Manager網站](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### 静态模板 {#static-templates}

静态模板:

* 必須由您的開發人員定義和設定。
* 已推出多個版本的AEM原始範本系統。
* 靜態範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。
* 複製來建立頁面，之後就沒有任何動態連線存在。
* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 以儲存設計屬性。
* 儲存在 `/apps`
* 另請參閱 [靜態範本](/help/sites-developing/page-templates-static.md) 以取得進一步資訊。

>[!NOTE]
>
>自AEM 6.5起，使用靜態範本並不被視為最佳實務。 請改用可編輯的範本。
>
>[AEM現代化](modernization-tools.md) 工具可協助您從靜態範本移轉至可編輯範本。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多個屬性，可控制底下允許的範本 **網站**. 但是，將它們合併可能會導致難以跟蹤和管理的複雜規則。
>
>因此，Adobe建議您先定義：
>
>* 僅限 `cq:allowedTemplates` 屬性
>
>* 僅於網站根目錄上
>
>如需範例，請參閱We.Retail： `/content/we-retail/jcr:content`
>
>屬性 `allowedPaths`， `allowedParents`、和 `allowedChildren` 亦可放置在範本上，以定義更複雜的規則。 不過，如果可能的話，它會 *很多* 更簡單以進一步定義 `cq:allowedTemplates` 屬性（若需要進一步限制允許的範本）。
>
>一個額外優點是 `cq:allowedTemplates` 作者可以在以下位置更新屬性： **進階** 的標籤 **頁面屬性**. 其他範本屬性無法使用（標準） UI更新，因此需要開發人員維護規則和每次變更的程式碼部署。

在網站管理員介面中建立頁面時，可用範本的清單取決於新頁面的位置和每個範本中指定的版位限制。

下列屬性決定是否使用範本 `T` 用於要放置為頁面子項的新頁面 `P`. 以下每個屬性都是多值字串，其中包含零個或多個用來與路徑比對的規則運算式：

* 此 `cq:allowedTemplates` 的屬性 `jcr:content` 的子節點： `P` 或祖先 `P`.

* 此 `allowedPaths` 屬性 `T`.

* 此 `allowedParents` 屬性 `T`.

* 此 `allowedChildren` 的範本屬性 `P`.

評估的運作方式如下：

* 第一個非空白 `cq:allowedTemplates` 將頁面階層從開頭遞增時發現屬性 `P` 比對的路徑 `T`. 如果沒有任何相符的值， `T` 已拒絕。

* 若 `T` 具有非空白 `allowedPaths` 屬性，但沒有值符合的路徑 `P`， `T` 已拒絕。

* 如果上述兩個屬性都空白或不存在， `T` 除非屬於與相同的應用程式，否則會遭拒 `P`. `T` 屬於與相同的應用程式 `P` 若且唯若第二層路徑的名稱 `T` 與路徑的第二層級名稱相同 `P`. 例如，範本 `/apps/geometrixx/templates/foo` 屬於與頁面相同的應用程式 `/content/geometrixx`.

* 若 `T` 具有非空白 `allowedParents` 屬性，但沒有值符合的路徑 `P`， `T` 已拒絕。

* 如果範本屬於 `P` 具有非空白 `allowedChildren` 屬性，但沒有值符合的路徑 `T`， `T` 已拒絕。

* 在所有其他情況下， `T` 允許。

下圖說明範本評估程式：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子頁面中使用的範本 {#limiting-templates-used-in-child-pages}

若要限制哪些範本可用於在指定頁面下建立子頁面，請使用 `cq:allowedTemplates` 屬性 `jcr:content` 頁面節點，用來指定允許做為子頁面的範本清單。 例如，清單中的每個值都必須是允許的子頁面範本的絕對路徑 `/apps/geometrixx/templates/contentpage`.

您可以使用 `cq:allowedTemplates` 範本的屬性  `jcr:content` 節點，將此設定套用至使用此範本的所有新建立頁面。

如果您想要新增更多限制，例如關於範本階層的限制，您可以使用 `allowedParents/allowedChildren` 範本的屬性。 然後，您可以明確指定從範本T建立的頁面必須是從範本T建立的頁面的父項/子項。

## 範本 — 內容片段 {#templates-content-fragments}

另請參閱 [內容片段範本](/help/sites-developing/content-fragment-templates.md).
