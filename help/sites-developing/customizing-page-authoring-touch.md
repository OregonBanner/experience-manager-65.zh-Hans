---
title: 自訂頁面製作
seo-title: Customizing Page Authoring
description: AEM提供各種機制，讓您能夠自訂頁面製作功能
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 1%

---

# 自訂頁面製作{#customizing-page-authoring}

>[!CAUTION]
>
>本檔案說明如何在現代化的觸控式UI中自訂頁面編寫，而不適用於傳統UI。

AEM提供多種機制，可讓您自訂頁面製作功能(以及 [主控台](/help/sites-developing/customizing-consoles-touch.md))。

* Clientlibs

   Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在下建立自己的clientlib `/apps.` 新clientlib必須：

   * 取決於編寫clientlib `cq.authoring.editor.sites.page`
   * 屬於適當的 `cq.authoring.editor.sites.page.hook` 類別

* 叠加

   覆蓋是以節點定義為基礎，並允許您覆蓋標準功能(在 `/libs`)的自訂功能(位於 `/apps`)。 建立覆蓋圖時，不需要原始的1:1復本，因為 [sling資源合併](/help/sites-developing/sling-resource-merger.md) 允許繼承。

>[!NOTE]
>
>如需進一步資訊，請參閱 [JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

您可以透過多種方式使用這些工具，來延伸AEM例項中的頁面製作功能。 以下說明選取範圍（概略說明）。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM觸控式UI的結構](/help/sites-developing/touch-ui-structure.md) 以取得用於編寫頁面的結構區域的詳細資訊。
>



>[!CAUTION]
>
>您 ***必須*** 不變更中的任何專案 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時會被覆寫（而您在套用hotfix或feature pack時很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 重新建立所需專案（即該專案存在於中） `/libs`)下 `/apps`
>1. 進行任何變更 `/apps`


## 新增圖層（模式） {#add-new-layer-mode}

編輯頁面時，會有多種方式 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 可用。 這些模式的實作方式 [圖層](/help/sites-developing/touch-ui-structure.md#layer). 這些功能可讓使用者存取相同頁面內容的不同功能型別。 標準圖層包括：編輯、預覽、註釋、開發人員和目標定位。

### 圖層範例：即時副本狀態 {#layer-example-live-copy-status}

標準AEM例項提供MSM層。 這會存取與以下專案相關的資料： [多網站管理](/help/sites-administering/msm.md) 並在圖層中反白顯示。

若要檢視其運作情況，您可以編輯任何 [We.Retail語言副本](/help/sites-developing/we-retail-globalized-site-structure.md) 頁面（或任何其他即時副本頁面）並選取 **即時副本狀態** 模式。

您可以在下列位置找到MSM圖層定義（供參考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

此範例套件說明如何建立新圖層（模式），這是MSM檢視的新圖層。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-new-layer-mode專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 新增選擇類別至資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種型別/類別（例如影像、檔案等）的資產。 這些資產也可依資產類別進行篩選。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一個範例套件，說明如何將新群組新增至資產尋找器。 此範例連線到 [閃爍](https://www.flickr.com)的公開串流並在sidepanel中顯示。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-assetfinder-flickr專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 篩選資源 {#filtering-resources}

編寫頁面時，使用者必須經常從資源（例如頁面、元件、資產等）中進行選取。 例如，這可採取清單的形式，作者必須從中選擇專案。

為了將清單保持在合理的大小並與使用案例相關，可採用自訂述詞的形式實施篩選器。 例如，如果 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) 元件是用來讓使用者選取特定資源的路徑，可透過下列方式篩選顯示的路徑：

* 實作自訂述詞 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 介面。
* 指定述詞的名稱，並在使用時參考該名稱 `pathbrowser`.

如需建立自訂述詞的詳細資訊，請參閱 [本文](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>透過實作來實作自訂述詞 `com.day.cq.commons.predicate.AbstractNodePredicate` 介面在傳統UI中也可運作。
>
>另請參閱 [此知識庫文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 在傳統UI中實作自訂述詞的範例。

## 將動作新增至元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件（通常是）都有一個工具列，可讓您存取可對該元件執行的一系列動作。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一個範例套件，說明如何建立自訂工具列動作來轉譯元件。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-toolbar-screens專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   儲存各種可用編輯器的定義。

1. 編輯器與可以使用的每個資源型別（如元件中所示）之間有一個連線：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性: `editorType`

            定義為該元件觸發就地編輯時將使用的內嵌編輯器型別；例如 `text`， `textimage`， `image`， `title`.

1. 編輯器的其他設定詳細資料可使用 `config` 包含設定的節點以及 `plugin` 節點，以包含必要的外掛程式設定詳細資料。

   以下是為影像元件的影像裁切外掛程式定義外觀比例的範例。 請注意，由於熒幕大小可能非常有限，裁切比例已移至全熒幕編輯器，並且只能在那裡看到。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >請注意，在AEM中，裁切比例是由 `ratio` 屬性，定義為 **高度/寬度**. 這與傳統的寬度/高度定義不同，這麼做是出於舊版相容性的原因。 只要您定義「 」，製作使用者就不會知道任何差異 `name` 屬性明確，因為這是UI中顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

若要實作新的就地編輯器（在您的clientlib中）：

>[!NOTE]
>
>例如，請參閱：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 實作：

   * `setUp`
   * `tearDown`

1. 註冊編輯器（包括建構函式）：

   * `editor.register`

1. 提供編輯器與每個可使用它的資源型別（如元件中的）之間的連線。

#### 建立新就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一個範例套件，說明如何在AEM中建立新的就地編輯器。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-inplace-editor專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 設定多個就地編輯器 {#configuring-multiple-in-place-editors}

您可以設定元件，使其有多個就地編輯器。 設定多個就地編輯器時，您可以選取適當的內容並開啟適當的編輯器。 請參閱 [設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md) 說明檔案以取得詳細資訊。

## 新增頁面動作 {#add-a-new-page-action}

若要在頁面工具列中新增頁面動作，例如 **返回網站** （主控台）動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一個範例套件，說明如何建立自訂標題列動作以跳回網站主控台。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-header-backtosites專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自訂啟用請求工作流程 {#customizing-the-request-for-activation-workflow}

現成的工作流程， **請求啟用**：

* 當有內容作者時，會自動出現在適當的功能表中 **沒有** 適當的復寫許可權，但 **有** DAM使用者和作者的成員資格。

* 否則將不會顯示任何內容，因為復寫許可權已移除。

若要在發生此類啟動時具有自訂行為，您可以覆蓋 **請求啟用** 工作流程：

1. 在 `/apps` 覆蓋 **網站** 精靈：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >這本身會覆寫下列專案的常見例項：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 更新 [工作流程模型](/help/sites-developing/workflows-models.md) 以及所需的相關設定/指令碼。
1. 移除「 」的許可權 [ `replicate` 動作](/help/sites-administering/security.md#actions) 來自所有相關頁面的所有適當使用者；當任何使用者嘗試發佈（或復寫）頁面時，將此工作流程作為預設動作觸發。
