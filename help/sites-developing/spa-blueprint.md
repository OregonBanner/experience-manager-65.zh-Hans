---
title: SPA Blueprint
seo-title: SPA Blueprint
description: 本檔案說明任何SPA架構都應該履行的一般且獨立於架構的合約，以便在AEM中實作可編輯的SPA元件。
seo-description: This document describes the general, framework-independent contract that any SPA framework should fulfill in order to implement editable SPA components within AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: afd2afe182d65e64c0ad851b86021886078a9dd5
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# SPA Blueprint{#spa-blueprint}

若要讓作者能夠使用AEM SPA編輯器來編輯SPA的內容，SPA必須滿足以下要求，本檔案將對此進行說明。

>[!NOTE]
>
>SPA編輯器是建議解決方案，適用於需要SPA架構使用者端轉譯的專案(例如React或Angular)。

## 简介 {#introduction}

本檔案說明任何SPA架構應履行的一般合約(即AEM支援層的型別)，以便在AEM中實作可編輯的SPA元件。

>[!NOTE]
>
>下列需求與架構無關。 如果滿足這些需求，則可以提供框架特定的層，該層由模組、元件和服務組成。
>
>**AEM中的React和Angular架構已符合這些需求。** 只有當您想要實作其他框架以與AEM一起使用時，此藍圖中的需求才相關。

>[!CAUTION]
>
>雖然AEM的SPA功能與框架無關，但目前僅支援React和Angular框架。

若要讓作者能使用AEM頁面編輯器來編輯單頁應用程式架構所公開的資料，專案必須能夠解譯代表為AEM存放庫中應用程式儲存之資料語意的模型結構。 為達成此目標，我們提供兩個與架構無關的程式庫： `PageModelManager` 和 `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

此 `PageModelManager` 程式庫會作為NPM套件提供，以供SPA專案使用。 它可與SPA搭配使用，並作為資料模型管理員。

它會代表SPA抽象化代表實際內容結構的JSON結構的擷取和管理。 此外也負責與SPA同步，以便在必須重新呈現其元件時通知。

請參閱NPM套件 [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

初始化時 `PageModelManager`，程式庫會先載入應用程式提供的根模型（透過引數、中繼屬性或目前的URL）。 如果資料庫識別目前頁面的模型不是它擷取的根模型的一部分，並包含它作為子頁面的模型。

![page_model_consolidation](assets/page_model_consolidation.png)

### 元件對應 {#componentmapping}

此 `ComponentMapping` 模組以NPM封裝形式提供給前端專案。 它會儲存前端元件，並提供SPA將前端元件對應至AEM資源型別的方法。 如此一來，在剖析應用程式的JSON模型時，便可啟用元件的動態解析度。

模型中呈現的每個專案都包含 `:type` 公開AEM資源型別的欄位。 掛載後，前端元件可使用從基礎程式庫收到的模型片段來呈現自身。

#### 对组件映射进行动态建模 {#dynamic-model-to-component-mapping}

如需有關在AEM適用的Javascript SPA SDK中如何發生動態模型與元件對應的詳細資訊，請參閱文章 [SPA的動態模型到元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### 框架特定層 {#framework-specific-layer}

每個前端架構都必須實作第三層。 此第三個程式庫負責與基礎程式庫互動，並提供一系列整合良好且易於使用的入口點，以便與資料模型互動。

本檔案的其餘部分說明此中介架構特定層的需求，並渴望與架構無關。 遵循下列需求，即可為專案元件提供架構特定層，以便與負責管理資料模型的基礎程式庫互動。

## 一般概念 {#general-concepts}

### 頁面模型 {#page-model}

頁面的內容結構儲存在AEM中。 頁面模型可用來對應和例項化SPA元件。 SPA開發人員會建立對應至SPA元件的AEM元件。 為此，它們使用資源型別(或AEM元件的路徑)作為唯一索引鍵。

SPA元件必須與頁面模型同步，並隨其內容的任何變更而更新。 運用動態元件的模式必須用來依照提供的頁面模型結構即時例項化元件。

### 中繼欄位 {#meta-fields}

頁面模型會利用JSON模型匯出程式，其本身會根據 [Sling模型](https://sling.apache.org/documentation/bundles/models.html) API。 可匯出Sling模型會公開下列欄位清單，以啟用基礎程式庫來解譯資料模型：

* `:type`：AEM資源的型別（預設=資源型別）
* `:children`：目前資源的階層子系。 子系不屬於目前資源的內部內容（可在代表頁面的專案上找到）
* `:hierarchyType`：資源的階層型別。 此 `PageModelManager` 目前支援頁面型別

* `:items`：目前資源的子內容資源（巢狀結構，僅存在於容器上）
* `:itemsOrder`：子項的有序清單。 JSON對應物件不保證其欄位的順序。 透過同時使用對應和目前的陣列，API的消費者可同時擁有兩種結構的優點
* `:path`：專案的內容路徑（出現在代表頁面的專案上）

另請參閱 [AEM內容服務快速入門。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模組 {#framework-specific-module}

區隔關注點有助於促進專案實施。 因此，應提供npm專屬的套件。 此套件負責彙總及公開基本模組、服務和元件。 這些元件必須封裝資料模型管理邏輯，並提供專案元件所預期資料的存取權。 模組也負責暫時公開基礎程式庫的實用進入點。

為方便程式庫的互通性，Adobe建議框架特定模組搭售下列程式庫。 如有必要，圖層可以先封裝並調整基礎API，再將其公開至專案。

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 實作 {#implementations}

#### React {#react}

npm模組： [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### angular {#angular}

npm模組： [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## 主要服務與元件 {#main-services-and-components}

下列實體應根據每個框架的特定准則實作。 根據框架架構，實作可能會有很大的差異，但必須提供所描述的功能。

### 模型提供者 {#the-model-provider}

專案元件必須將模型片段的存取權委派給模型提供者。 然後，模型提供者會負責監聽對模型的指定片段所做的變更，並將更新的模型傳回委派元件。

為此，模型提供者必須向 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. 然後，當變更發生時，它會接收更新後的資料並傳遞至委派元件。 根據慣例，將攜帶模型片段的委派元件可用的屬性已命名為 `cqModel`. 實作可免費為元件提供此屬性，但應考量與框架架構整合、可發現性和易用性等層面。

### 元件HTML裝飾器 {#the-component-html-decorator}

「元件裝飾器」負責以「頁面編輯器」所預期的一系列資料屬性和類別名稱來裝飾每個元件例項之元素的外部HTML。

#### 元件宣告 {#component-declaration}

下列中繼資料必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器擷取對應的編輯設定。

* `data-cq-data-path`：相對於的資源的路徑 `jcr:content`

#### 編輯功能宣告和預留位置 {#editing-capability-declaration-and-placeholder}

下列中繼資料和類別名稱必須新增至專案元件產生的外部HTML元素。 它們可讓頁面編輯器提供相關功能。

* `cq-placeholder`：識別空白元件預留位置的類別名稱
* `data-emptytext`：元件例項為空白時覆蓋圖所顯示的標籤

**空白元件的預留位置**

每個元件都必須延伸使用功能，以便在將元件識別為空白時，使用預留位置和相關覆蓋圖特有的資料屬性和類別名稱來裝飾外部HTML元素。

**關於元件的空白**

* 元件在邏輯上是否為空白？
* 當元件為空白時，覆蓋圖所顯示的標籤應為何？

### 容器 {#container}

容器是用來包含和轉譯子元件的元件。 若要這麼做，容器會在 `:itemsOrder`， `:items` 和 `:children` 其模型的屬性。

容器會動態地從的存放區取得子元件 [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 資料庫。 然後容器會使用模型提供者功能來擴充子元件，最後將其例項化。

### 页面 {#page}

此 `Page` 元件延伸 `Container` 元件。 容器是用來包含和轉譯子元件（包括子頁面）的元件。 若要這麼做，容器會在 `:itemsOrder`， `:items`、和 `:children` 其模型的屬性。 此 `Page` 元件會動態地從的存放區取得子元件 [元件對應](/help/sites-developing/spa-blueprint.md#componentmapping) 資料庫。 此 `Page` 負責具現化子元件。

### 响应式网格 {#responsive-grid}

回應式格線元件是容器。 它包含模型提供者的特定變體，該變體代表其欄。 回應式格線及其欄負責使用模型中包含的特定類別名稱來裝飾專案元件的外部HTML元素。

回應式格線元件應預先對應至其AEM對應元件，因為此元件很複雜且很少自訂。

#### 特定模型欄位 {#specific-model-fields}

* `gridClassNames:` 為回應式格線提供的類別名稱
* `columnClassNames:` 為回應式欄提供的類別名稱

#### 回應格線的預留位置 {#placeholder-of-the-reponsive-grid}

SPA元件會對應至圖形容器（例如回應式格線），且必須在編寫內容時新增虛擬子項預留位置。 當頁面編輯器編寫SPA的內容時，該內容會使用iframe和 `data-cq-editor` 屬性會新增到該內容的檔案節點。 當 `data-cq-editor` 屬性存在，容器必須包括HTMLElement，以代表作者在頁面中插入新元件時與之互動的區域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>範例中使用的類別名稱目前為頁面編輯器所需。
>
>* `"new section"`：指出目前的元素是容器的預留位置
>* `"aem-Grid-newComponent"`：標準化配置編寫的元件
>


#### 元件對應 {#component-mapping}

基礎 [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 程式庫及其 `MapTo` 函式可以封裝和延伸，以提供與目前元件類別旁提供的編輯設定相關的功能。

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

在上述實作中，專案元件會在中實際註冊之前，先以空白功能延伸 [元件對應](/help/sites-developing/spa-blueprint.md#componentmapping) 商店。 這是透過封裝和延伸 [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) 程式庫，以介紹 `EditConfig` 設定物件：

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 與頁面編輯器訂約 {#contract-with-the-page-editor}

專案元件必須至少產生下列資料屬性，才能讓編輯器與其互動。

* `data-cq-data-path`：元件的相對路徑，如 `PageModel` (例如， `"root/responsivegrid/image"`)。 此屬性不應新增至頁面。

總而言之，若要由頁面編輯器解譯為可編輯，專案元件必須符合下列合約：

* 提供預期屬性，以將前端元件執行個體與AEM資源建立關聯。
* 提供可建立空白預留位置的預期屬性系列和類別名稱。
* 提供可拖放資產的預期類別名稱。

### 典型HTML元素結構 {#typical-html-element-structure}

以下片段說明頁面內容結構的典型HTML表示法。 以下是一些重要事項：

* 回應式格線元素帶有前置詞為的類別名稱 `aem-Grid--`
* 回應式欄元素包含前置詞為的類別名稱 `aem-GridColumn--`
* 回應式格線也會換行，例如前兩個字首未出現在相同元素上，此格線也是父格線的欄
* 對應至可編輯資源的元素會附帶 `data-cq-data-path` 屬性。 請參閱 [與頁面編輯器訂約](#contract-wtih-the-page-editor) 區段。

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 導覽與路由 {#navigation-and-routing}

應用程式擁有路由。 前端開發人員首先需要實作導覽元件(對應至AEM導覽元件)。 此元件會呈現URL連結，以搭配顯示或隱藏內容片段的一系列路由使用。

基礎 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 程式庫及其 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 模組（預設為啟用）負責預先擷取和提供對與指定資源路徑相關聯之模型的存取權。

這兩個圖元與繞線的概念有關，但 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 只負責執行 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 以與目前應用程式狀態同步的結構化資料模型載入。

請參閱文章 [SPA模型製程](/help/sites-developing/spa-routing.md) 以取得詳細資訊。

## SPA運作中 {#spa-in-action}

繼續參閱檔案，瞭解簡單的SPA如何運作，並親自體驗SPA [AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md).

## 深入阅读 {#further-reading}

如需AEM中SPA的詳細資訊，請參閱下列檔案：

* [SPA製作概述](/help/sites-developing/spa-overview.md) 關於AEM中的SPA和通訊模型的概述
* [AEM中的SPA快速入門](/help/sites-developing/spa-getting-started-react.md) 取得簡單SPA的指南及其運作方式
