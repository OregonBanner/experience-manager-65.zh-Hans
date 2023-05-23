---
title: 使用最適化表單的最佳作法
seo-title: Best practices for working with adaptive forms
description: 說明設定AEM Forms專案、開發最適化表單和最佳化AEM Forms系統效能的最佳實務。
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: f05ddd2fb72258b7de5d361eb87f5e68e7ddd7ff
workflow-type: tm+mt
source-wordcount: '4529'
ht-degree: 0%

---

# 使用最適化表單的最佳作法 {#best-practices-for-working-with-adaptive-forms}

## 概述 {#overview}

Adobe Experience Manager (AEM)表單可協助您將複雜的交易轉換為簡單、愉快的數位體驗。 不過，您需要共同努力來實施、建立、執行及維護有效率且具生產力的AEM Forms生態系統。

本檔案提供表單管理員、作者和開發人員在使用AEM Forms （尤其是調適型表單元件）時可受益的准則和建議。 此影片探討最佳實務，從設定表單開發專案，到設定、自訂、編寫和最佳化AEM Forms。 這些最佳實務會共同為AEM Forms生態系統的整體效能作出貢獻。

此外，以下是一般AEM最佳實務的建議閱讀：

* [最佳實務：部署和維護AEM](/help/sites-deploying/best-practices.md)
* [最佳實務：製作內容](/help/sites-authoring/best-practices.md)
* [最佳實務：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳實務：開發解決方案](/help/sites-developing/best-practices.md)

## 設定和設定AEM Forms {#set-up-and-configure-aem-forms}

### 設定表單開發專案 {#setting-up-forms-development-project}

簡化和標準化的專案結構可大幅減少開發和維護工作。 Apache Maven是建置AEM專案時建議使用的開放原始碼工具。

* 使用Apache Maven `aem-project-archetype` 以建立和管理AEM專案的結構。 它會為您的AEM專案建立建議的結構和範本。 此外，它還提供建置自動化和變更控制系統，以協助管理專案。

   * 使用maven `archetype:generate` 命令以產生初始結構。
   * 使用maven `eclipse:eclipse` 命令來產生eclipse專案檔案，並將專案匯入eclipse。

如需詳細資訊，請參閱 [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md).

* FileVault工具或VLT可協助您將CRX或AEM執行個體的內容對應至您的檔案系統。 它提供變更控制管理作業，例如AEM專案內容的入庫和出庫。 另請參閱 [如何使用VLT工具](/help/sites-developing/ht-vlttool.md).

* 如果您使用Eclipse整合式開發環境，您可以使用AEM開發人員工具將Eclipse IDE與AEM執行個體緊密整合，以建立AEM應用程式。 如需詳細資訊，請參閱 [適用於Eclipse的AEM開發人員工具](/help/sites-developing/aem-eclipse.md).

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴充或覆寫預設功能。

* 當您建立套件以移動內容時，請確保套件篩選路徑正確，並且只提到必要的路徑。

* 請勿在/libs資料夾中儲存任何內容或進行任何修改。 在/app資料夾中建立覆蓋以擴充或覆寫預設功能。

* 定義套件的正確相依性，以強制預先確定的安裝順序/順序。

* 請勿在/libs或/apps中建立任何可參照的節點。

### 規劃製作環境 {#planning-for-authoring-environment}

設定AEM專案後，定義製作和自訂最適化表單範本和元件的策略。

* 調適型表單範本是專門的AEM頁面，可定義調適型表單的結構和頁首頁尾資訊。 範本已預先設定最適化表單的版面、樣式和基本結構。 AEM Forms提供現成可用的範本和元件，供您製作調適型表單。 不過，您可以根據需求建立自訂範本和元件。 建議您收集最適化表單中所需其他範本和元件的需求。 如需詳細資訊，請參閱 [自訂最適化表單和元件](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms可讓您根據下清單單模型建立最適化表單。 表單模型可作為表單與AEM系統之間資料交換的介面，並為最適化表單內外資料流提供XML型結構。 此外，表單模型會以結構描述和XFA限制的形式對調適型表單施加規則和限制。

   * **無**：使用此選項建立的最適化表單不使用任何表單模型。 从此类表单生成的数据 XML 具有带字段和相应值的平面结构。
   * **xml或JSON結構描述**： XML和JSON結構描述代表組織中後端系統產生或使用資料的結構。 您可以將結構描述關聯至最適化表單，並使用其元素將動態內容新增至最適化表單。 結構描述的元素可在內容瀏覽器的「資料模型物件」標籤中使用，以編寫調適型表單。 您可以拖放結構元素來建立表單。
   * **XFA表單範本**：如果您有投資以XFA為基礎的HTML5表單，這會是理想的表單模型。 它可讓您直接將XFA型表單轉換為最適化表單。 任何現有的XFA規則都會保留在關聯的最適化表單中。 產生的調適型表單支援XFA建構，例如驗證、事件、屬性和模式。
   * **表單資料模型**：如果您想要整合後端系統(例如資料庫、Web服務和AEM使用者設定檔)，以預先填寫最適化表單並將提交的表單資料寫入回後端系統，這會是偏好表單模型。 表單資料模型編輯器可讓您在可用來建立調適型表單的表單資料模型中定義及設定實體和服務。 如需詳細資訊，請參閱 [AEM Forms資料整合](/help/forms/using/data-integration.md).

請務必謹慎選擇資料模型，不僅要符合您的需求，還要擴大您對XFA和XSD資產的現有投資（如果有的話）。 建議您使用XSD模型來建立表單範本，因為產生的XML包含結構描述所定義的XPATH資料。 使用XSD模型作為表單資料模型的預設選擇也有幫助，因為它將表單設計從處理和使用資料的後端系統分離開，並且它由於表單欄位的一對一對應而提高了表單的效能。 此外，欄位的BindRef可以成為其資料值的XPATH （以XML表示）。

如需詳細資訊，請參閱 [建立最適化表單](/help/forms/using/creating-adaptive-form.md).

* 適用性表單中會有一些通用區段。 您可以識別它們並定義策略以促進內容重複使用。 適用性表單可讓您建立獨立的片段，並在各個表單中重複使用。 您也可以將最適化表單中的面板另存為片段。 片段中的任何變更都會反映在所有關聯的表單中。 它可幫助您減少編寫時間並確保各表單的一致性。 此外，使用片段可讓適用性表單變得更輕量，進而改善編寫體驗，尤其是大型表單。 如需詳細資訊，請參閱 [最適化表單片段](/help/forms/using/adaptive-form-fragments.md).

### 自訂最適化表單和元件 {#customize-components}

* AEM Forms提供可用於建立最適化表單的現成最適化表單範本。 您也可以建立自己的範本。 AEM提供靜態和可編輯的範本。

   * 靜態範本由開發人員定義和設定。
   * 可編輯的範本是由作者使用範本編輯器建立的。 範本編輯器可讓您定義範本中的基本結構和初始內容。 結構圖層中的任何修改都會反映在使用該範本的所有表單中。 初始內容可能包括預先設定的主題、預填服務、提交動作等。 不過，可使用表單編輯器修改表單的這些設定。 如需詳細資訊，請參閱 [最適化表單範本](/help/forms/using/template-editor.md).

* 若要設定特定欄位或面板例項的樣式，請使用 [內嵌樣式](/help/forms/using/inline-style-adaptive-forms.md). 或者，您也可以在CSS檔案中定義類別，並在元件的CSS Class屬性中指定類別名稱。
* 在元件中納入使用者端資料庫，以便一致地套用樣式至使用該元件的調適型表單或片段。 如需詳細資訊，請參閱 [建立最適化表單頁面元件](/help/forms/using/custom-adaptive-forms-templates.md).
* 藉由在適用性表單容器屬性的CSS檔案路徑欄位中指定使用者端資料庫的路徑，套用使用者端資料庫中定義的樣式以選取適用性表單。
* 若要建立樣式的使用者端資料庫，您可以在主題編輯器基底clientlib或表單容器屬性中設定自訂CSS檔案。
* 調適型表單提供面板配置（例如回應式、索引標籤、摺疊式功能表和精靈），以控制表單元件在面板中的配置方式。 您可以建立自訂面板版面配置，並讓表單作者可以使用它們。 如需詳細資訊，請參閱 [建立最適化表單的自訂版面配置元件](/help/forms/using/custom-layout-components-forms.md).
* 您也可以自訂特定的最適化表單元件，例如欄位和面板版面配置。

   * 使用 [覆蓋](/help/sites-developing/overlays.md) AEM修改元件副本的功能。 不建議修改預設元件。
   * 若要在/libs中自訂現成可用的最適化表單元件的版面， [建立自訂配置元件](/help/forms/using/custom-layout-components-forms.md) 除了 [預設版面](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * 透過建立自訂Widget或外觀來引入自訂互動。 不建議修改預設元件。 如需詳細資訊，請參閱 [外觀架構](/help/forms/using/introduction-widgets.md).

* 另請參閱 [處理個人識別資訊](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) 以取得處理PII資料的建議。

### 建立表單範本

您可以使用中啟用的表單範本來建立最適化表單 **設定瀏覽器**. 若要啟用表單範本，請參閱 [建立最適化表單範本](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

表單範本也可以從其他作者電腦上建立的最適化表單套件上傳。 可透過安裝取得表單範本 [aemforms-references-*套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans). 建議的一些最佳實務如下：
* 此 **nosamplecontent** 僅作者才建議使用runmode，不建議發佈節點使用。
* 資產（例如最適化表單、主題、範本或雲端設定）的製作只會透過製作節點執行，它們可以在已設定的發佈節點發佈。
如需詳細資訊，請參閱 [發佈和取消發佈表單和檔案](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* 製作和發佈都需要Forms附加元件套件來支援檔案服務操作；因此，可將其視為相依性。
如果您只想要Forms相關的範例範本、主題和DOR套件，可以從以下來源下載 [aemforms-references-*套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

如需進一步資訊，請參閱以下連結中的最佳實務： [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

## 製作最適化表單 {#author-adaptive-forms}

### 使用觸控最佳化的UI進行編寫 {#using-touch-optimized-ui-for-authoring}

* 使用側邊欄中的物件瀏覽器，快速存取表單階層中下方的欄位。 您可以使用搜尋方塊來搜尋表單或物件樹中的物件，以便從一個物件瀏覽至另一個物件。
* 若要在側欄的元件瀏覽器中檢視和編輯元件的屬性，請選取該元件，然後按一下 ![cmppr-1](assets/cmppr-1.png). 您也可以連按兩下元件，以在屬性瀏覽器中檢視其屬性。
* 使用鍵盤快速鍵對表單進行快速動作。 另請參閱 [AEM Forms鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md).

* 建議僅將調適型表單元件用於調適型表單頁面。 元件與其父項階層具有相依性。 因此，請勿在AEM頁面中使用這些引數。

另請參閱元件說明和最佳作法，位置在： [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

### 在最適化表單中使用規則 {#using-rules-in-adaptive-forms}

AEM Forms提供 [規則編輯器](/help/forms/using/rule-editor.md) 可讓您建立規則，以將動態行為新增至最適化表單元件。 使用這些規則，您可以評估條件並在元件上觸發動作，例如顯示或隱藏欄位、計算值、動態變更下拉式清單等。

規則編輯器提供用於編寫規則的視覺化編輯器和代碼編輯器。 使用程式碼編輯器模式撰寫規則時，請考量下列事項：

* 為表單欄位和元件使用有意義且唯一的名稱，以避免在撰寫規則時可能發生任何衝突。
* 使用 `this` 運運算元，元件可在規則運算式中參照自身。 這可確保即使元件名稱變更，規則仍保持有效。 例如：`field1.valueCommit script: this.value > 10`。

* 參照其他表單元件時使用元件名稱。 使用 `value` 屬性以擷取欄位或元件的值。 例如：`field1.value`。

* 按相對唯一階層參照元件，以避免任何衝突。 例如：`parentName.fieldName`。

* 處理複雜或常用規則時，請考慮將商業邏輯寫入單獨的使用者端程式庫中，以便指定並在調適型表單中重複使用。 使用者端程式庫應為獨立程式庫，且不應有任何外部相依性，jQuery和Underscore.js除外。 您也可以使用使用者端程式庫來強制執行 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) 提交的表單資料中。
* 調適型表單提供了一組API，您可以使用這些API與調適型表單進行通訊和對調適型表單執行動作。 部分重要API如下。 如需詳細資訊，請參閱 [Adaptive Forms的JavaScript資料庫API參考](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`：重設表單。
   * `guideBridge.submit()`：提交表單。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`：將焦點設定為欄位。
   * `guideBridge.validate(errorList, somExpression, focus)`：驗證表單。
   * `guideBridge.getDataXML(options)`：以XML格式取得表單資料。
   * `guideBridge.resolveNode(somExpression)`：取得表單物件。
   * `guideBridge.setProperty(somList, propertyName, valueList)`：設定表單物件的屬性。
   * 此外，您可以使用以下欄位屬性：

      * `field.value` 以變更欄位的值。
      * `field.enabled` 以啟用/停用欄位。
      * `field.visible` 變更欄位的可見度。

* 最適化表單作者可能需要撰寫JavaScript程式碼，才能在表單中建立商業邏輯。 雖然JavaScript功能強大且有效，但可能會影響安全性預期。 因此，您必須確保表單作者是受信任的角色，而且在表單投入生產之前，有程式可稽核和核准JavaScript程式碼。 管理員可以根據使用者群組的角色或功能，限制使用者群組對規則編輯器的存取權。 另請參閱 [授予規則編輯器存取權給選定的使用者群組](/help/forms/using/rule-editor-access-user-groups.md).
* 您可以在規則中使用運算式，使調適型表單成為動態表單。 所有運算式都是有效的JavaScript運算式，且使用適用性表單指令碼模型API。 這些運算式會傳回某些型別的值。 如需運算式和相關最佳實務的詳細資訊，請參閱 [最適化表單運算式](/help/forms/using/adaptive-form-expressions.md).

### 使用主題 {#working-with-themes}

主題適用性可讓您建立可重複使用的樣式，這些樣式可套用至各個表單，以獲得一致的外觀和樣式。 建議使用主題來定義表單元件和面板的樣式。 主題相關的最佳實務如下：

* 使用資產庫快速套用文字樣式、背景和影像。 將樣式新增至資產庫時，該樣式可用於其他主題和表單編輯器的樣式模式。
* 使用頁面層級選擇器套用字型和頁面背景等全域設定。
* 使用使用者端資料庫將現有或進階樣式匯入您的主題。
* 您可以覆寫表單樣式圖層中的特定欄位、面板或按鈕的樣式。
* 如果主題不符合您的樣式需求，您可以使用預先定義的類別（例如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）來套用表單上的通用樣式。

如需詳細資訊，請參閱 [主題](/help/forms/using/themes.md).

### 最佳化大型與複雜表單的效能 {#optimizing-performance-of-large-and-complex-forms}

表單作者和一般使用者在製作模式或執行階段載入大型表單時，通常面臨效能問題。 隨著表單中物件（欄位和面板）數量的增加，編寫和執行階段體驗會開始降低。 它也能防止多位作者同時共同作業及撰寫表單。

請考慮下列最佳實務，以克服大型表單的效能問題：

* 如有可能，建議使用XSD表單資料模型建立調適型表單，即便將XFA轉換為調適型表單亦然。
* 在適用性表單中僅包含從使用者擷取資訊的欄位和面板。 請考慮將靜態內容維持在最小限度，或使用URL在個別視窗中開啟。
* 雖然每個表單都是針對特定目的而設計，但大多數表單中都有一些常見的區段。 例如，個人詳細資訊、地址、僱用詳細資訊等。 建立 [最適化表單片段](/help/forms/using/adaptive-form-fragments.md) 以取得通用表單元素和區段，並在表單間使用這些元素和區段。 您也可以將現有表單中的面板另存為片段。 片段中的任何變更都會反映在所有關聯的適用性表單中。 它促進了合作撰寫，因為多個作者可以同時處理構成表單的不同片段。

   * 與調適型表單類似，建議使用片段容器對話方塊，在使用者端資料庫中定義所有片段特定的樣式和自訂指令碼。 此外，請嘗試建立不依賴外部物件的自給自足片段。
   * 避免使用跨片段指令碼。 如果片段外有任何您必須參照的物件，請嘗試將該物件設為父表單的一部分。 如果物件仍必須位於另一個片段中，請在指令碼中依其名稱參照。

* 使用自動儲存的儲存並繼續以定期儲存最適化表單，並讓使用者稍後重新造訪以完成表單。
* 設定片段以緩慢載入。 在執行階段，只有在需要時，才會轉譯標籤為延遲載入的片段。 它可大幅縮短大型表單的載入時間。 具有可重複面板的片段也支援此功能。 如需詳細資訊，請參閱 [設定延遲載入](/help/forms/using/lazy-loading-adaptive-forms.md).

   * 請勿在回應式格線配置或第一個面板中設定在片段上的延遲載入。
   * 延遲載入的片段不支援檔案附件和條款與條件元件。
   * 如果延遲載入面板中的某個值用於表單的其他部分，請將該值標示為「全域使用值」，以便在解除安裝包含面板時使用該值。
   * 請考慮為應根據條件顯示或隱藏的片段編寫可見性規則。
* 設定 **每個請求的呼叫數** 在 **Apache Sling主要Servlet** 到相當多的數字。 這可讓Forms伺服器允許其他呼叫。 設定會顯示預設值1500。 值1500呼叫適用於其他Experience Manager元件，例如Sites和Assets。 最適化表單的預設值集為20000。 如果您遇到 `too many calls` 記錄檔中發生錯誤或表單無法呈現，請嘗試將值增加至大量以解決問題。 如果來電次數超過20000，表示表單很複雜，可能需要一些時間才能在瀏覽器中轉譯表單。 這只有在第一次載入表單時才會發生，之後會快取表單，而且快取表單後，對效能沒有重大影響。

### 預先填寫最適化表單 {#prefilling-adaptive-forms}

您可以使用從後端擷取的資料預先填寫最適化表單欄位，以幫助使用者快速填寫表單並避免輸入錯誤。

* AEM Forms提供預填服務，用於從預先定義的資料XML檔案中讀取資料，並使用預填XML檔案中的內容預填適用性表單的欄位。
* 預填資料XML必須符合與調適型表單相關聯的表單模型結構描述。
* 包含 `afBoundedData` 和 `afUnBoundedData` 預填XML的區段，以預填最適化表單中的繫結和未繫結欄位。

* 針對以表單資料模型為基礎的適用性表單，AEM Forms提供現成的表單資料模型預填服務。 預填服務會查詢最適化表單中資料模型物件的資料來源，並在呈現表單時預填欄位值。
* 您也可以使用檔案、crx、服務或http通訊協定預填調適型表單。
* AEM Forms支援自訂預填服務，您可以以OSGi服務的形式外掛以預填調適型表單。

如需詳細資訊，請參閱 [預填自適應表單欄位](/help/forms/using/prepopulate-adaptive-form-fields.md).

### 簽署及提交最適化表單 {#signing-and-submitting-adaptive-forms}

適用性表單需要提交動作來處理使用者指定的資料。 提交動作會決定使用最適化表單提交之資料所執行的工作。

* 適用性表單中有數個現成可用的提交動作。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md).
* 如果預設提交動作不符合您的使用案例，您可以編寫自訂提交動作。 如需詳細資訊，請參閱 [為最適化表單編寫自訂提交動作](/help/forms/using/custom-submit-action-form.md).
* 包含伺服器端驗證，以防止提交無效的資料。

您可以在調適型表單中運用Adobe Sign的多重登入體驗。 在調適型表單中設定Adobe Sign時，請考量下列事項。 如需詳細資訊，請參閱 [在最適化表單中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md).

* 啟用Adobe Sign的最適化表單只會在所有簽署者簽署表單後提交。 在所有簽署者簽署表單之前，Forms會一直顯示於擱置簽署狀態。
* 您可以在提交時設定表單內簽署體驗，或將簽署者重新導向至簽署頁面。
* 視需要設定循序或平行簽署體驗。

### 正在產生記錄檔案 {#generating-document-of-record}

記錄檔案(DoR)是您可以列印、簽署或封存的最適化表單的平面化PDF版本。

* 根據最適化表單所依據的表單資料模型，您可以為DoR設定範本，如下所示：

   * **XFA表單範本**：使用關聯的XDP檔案做為DoR範本。
   * **XSD結構描述**：使用與適用性表單使用相同XML結構描述的相關XFA範本。
   * **無**：使用自動產生的DoR。

* 從最適化表單編輯器的「記錄檔案」索引標籤設定頁首、頁尾、影像、顏色、字型等。
* 使用 `DoRService` 以程式設計方式產生DoR。
* 從DoR排除隱藏欄位。
* 使用 `afAcceptLang` 要求引數以檢視其他地區設定的DoR。

### 偵錯和測試調適型表單 {#debugging-and-testing-adaptive-forms}

[AEM Chrome外掛程式](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 是Google Chrome的瀏覽器擴充功能，提供用於偵錯最適化表單的工具。 表單作者和開發人員可使用這些工具來：

* 找出瓶頸並最佳化表單轉譯效能
* 表單中的偵錯關鍵字和bindRef錯誤
* 啟用和設定記錄檔
* 表單中的偵錯規則和指令碼
* 探索和瞭解guideBridge API

如需詳細資訊，請參閱 [AEM Chrome外掛程式 — 最適化表單](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### 在AEM伺服器上驗證最適化表單 {#validating-adaptive-forms-on-aem-server}

伺服器端驗證是必要的，以防止任何嘗試略過使用者端驗證的行為，以及資料提交和業務規則違規行為可能造成的危害。 伺服器端驗證會透過載入所需的使用者端程式庫在伺服器上執行。

* 在使用者端資料庫中加入函式，以驗證最適化表單中的運算式，並在最適化表單容器對話方塊中指定使用者端資料庫。 如需詳細資訊，請參閱 [伺服器端重新驗證](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* 伺服器端驗證會驗證表單模型。 建議建立個別的使用者端程式庫進行驗證，不要將其與其他專案(例如HTML樣式和DOM操作)混合在同一個使用者端程式庫中。

### 將調適型表單當地語系化 {#localizing-adaptive-forms}

AEM提供翻譯工作流程，您可用來將最適化表單本地化。 如需詳細資訊，請參閱 [使用AEM翻譯工作流程將最適化表單本地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

將適用性表單當地語系化的一些最佳實務如下：

* 針對各表單的共同元素使用自適應表單片段，並將片段本地化。 它可確保您將片段本地化一次，並反映在使用本地化片段的所有表單中。
* 任何修改，例如新增元件或以當地語系化表單套用指令碼，都不會自動當地語系化。 因此，您必須先完成表單，再進行本地化，以避免多個本地化週期。
* 使用 `afAcceptLang` 要求引數以覆寫瀏覽器地區設定並以指定的地區設定轉譯表單。 例如，無論瀏覽器設定中指定的地區設定為何，下列URL將強制以日文地區設定轉譯表單：

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms目前支援英文(en)、西班牙文(es)、法文(fr)、義大利文(it)、德文(de)、日文(ja)、葡萄牙文 — 巴西文(pt-BR)、中文(zh-CN)、中文 — 中國台灣(zh-TW)和韓文(ko-KR)本地化的最適化表單內容。 不過，您可在執行階段為最適化表單新增地區設定的支援。 如需詳細資訊，請參閱 [支援最適化表單本地化的新地區設定](/help/forms/using/supporting-new-language-localization.md).

## 準備表單專案以進行生產 {#prepare-forms-project-for-production}

### 新增表單處理伺服器 {#adding-forms-processing-server}

您可以另外設定一個AEM Forms伺服器執行個體，駐留在防火牆後面的安全區域中。 您可以將此執行個體用於：

* **批次處理**：以負載較重的批次重複產生或排程的工作。 例如，列印陳述式、產生對應，以及使用PDF產生器、輸出和組合器等檔案服務。
* **儲存PII資料**：將PII資料儲存在處理伺服器上。 如果您已使用自訂儲存提供者來儲存PII資料，則不需要使用。

### 將專案移動到另一個環境 {#moving-project-to-another-environment}

您通常需要將AEM專案從一個環境移動到另一個環境。 移動時需要記住的一些關鍵事項如下：

* 備份您現有的使用者端程式庫、自訂程式碼和設定。
* 在新環境中，以指定的順序手動部署產品套件和修補程式。
* 手動部署專案特定的程式碼套件和套件組合，並以個別套件或套件組合的形式部署在新的AEM伺服器上。
* (*僅限JEE上的AEM Forms*)在Forms Workflow伺服器上手動部署LCA和DSC。
* 使用 [匯出 — 匯入](/help/forms/using/import-export-forms-templates.md) 將資產移動到新環境的功能。 您也可以設定復寫代理程式並發佈資產。
* 升級時，請以新的API和功能取代所有已棄用的API和功能。

### 設定AEM {#configuring-aem}

設定AEM以改善整體效能的一些最佳實務如下：

* 從Felix主控台啟用JavaScript和CSS的HTML使用者端程式庫壓縮。
* 快取所有使用者端程式庫於 `/etc.clientlibs/fd` 以及AEM Dispatcher上的任何其他自訂使用者端資料庫，以提高您發佈表單的回應速度與安全性。 如需詳細資訊，請參閱 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* 不要快取 `/content/forms/af/` 和 `/content/dam/formsanddocuments/*` 路徑。 如需設定最適化表單快取的詳細資訊，請參閱 [快取最適化表單](/help/forms/using/configure-adaptive-forms-cache.md).

* 透過網頁伺服器壓縮模組啟用HTML。 如需詳細資訊，請參閱 [AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md).
* 針對大型表單，增加每個請求設定的呼叫數。 另請參閱 [最佳化大型與複雜表單的效能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* 建立 [錯誤處理常式顯示的自訂錯誤頁面](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* 安全的AEM Forms伺服器。

   * 使用 `nosamplecontent` 執行模式以確保生產伺服器上未部署範例內容和範例使用者。 另請參閱 [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md).

* 將棧積大小維持在最小8 GB。 如需其他設定，請參閱 [AEM Forms伺服器的效能調整](/help/forms/using/performance-tuning-aem-forms.md).
* 使用服務使用者工作階段而非管理工作階段來執行服務層級工作。 如需詳細資訊，請參閱 [服務驗證](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### 為草稿和提交的表單資料設定外部儲存空間 {#external-storage}

在生產環境中，建議不要將提交的表單資料儲存在AEM存放庫中。 Forms入口網站存放區、存放區內容和存放區PDF提交動作的預設實施，會將表單資料存放在AEM存放庫中。 這些提交動作僅供示範之用。 此外，「儲存並繼續」和「自動儲存」功能預設會使用入口網站儲存空間。 因此，請考慮下列建議：

* **儲存草稿資料**：如果您使用最適化表單的草稿功能，則應實作自訂服務提供介面(SPI)，以將草稿資料儲存在更安全的儲存空間，例如資料庫。 如需詳細資訊，請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md).

* **儲存提交資料**：如果您使用Form Portal Submit Store，則應實作自訂SPI以將提交資料儲存在資料庫中。 另請參閱 [將草稿和提交元件與資料庫整合的範例](/help/forms/using/integrate-draft-submission-database.md) 以取得範例整合。

   您也可以撰寫自訂提交動作，將表單資料和附件儲存在安全的儲存空間中。 另請參閱 [為最適化表單編寫自訂提交動作](/help/forms/using/custom-submit-action-form.md) 以取得詳細資訊。

* **草稿識別碼的長度**：將最適化表單儲存為草稿時，會產生草稿ID以唯一識別草稿。 草稿ID欄位長度的最小值是26個字元。 Adobe建議將草稿ID長度設定為26個或更多字元。

### 處理個人識別資訊 {#handling-personally-identifiable-information}

組織面臨的主要挑戰之一是如何處理個人識別(PII)資料。 以下為可協助您處理這類資料的最佳實務：

* 使用安全的外部儲存裝置（例如資料庫）來儲存草稿和已提交表單的資料。 另請參閱 [為草稿和提交的表單資料設定外部儲存空間](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* 在啟用自動儲存之前，使用條款與條件表單元件取得使用者的明確同意。 在此情況下，只有當使用者同意條款與條件元件中的條件時，才會啟用自動儲存。


