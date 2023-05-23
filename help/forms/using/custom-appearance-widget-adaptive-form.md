---
title: 建立最適化表單欄位的自訂外觀
seo-title: Create custom appearances for adaptive form fields
description: 自訂Adaptive Forms中現成可用元件的外觀。
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 8a24ca02762e7902b7d0033b36560629ee711de1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# 建立最適化表單欄位的自訂外觀{#create-custom-appearances-for-adaptive-form-fields}

## 简介 {#introduction}

適用性表單會利用 [外觀架構](/help/forms/using/introduction-widgets.md) 可協助您建立最適化表單欄位的自訂外觀，並提供不同的使用者體驗。 例如，以切換按鈕取代選項按鈕和核取方塊，或使用自訂jQuery外掛程式來限制使用者在電話號碼或電子郵件ID等欄位中的輸入。

本檔案說明如何使用jQuery外掛程式，為最適化表單欄位建立這些替代體驗。 此外，它還會展示一個範例，說明如何建立自訂外觀，讓數值欄位元件以數值步進器或滑桿顯示。

讓我們先來看看本文中使用的關鍵辭彙和概念。

**外觀** 指最適化表單欄位中各種元素的樣式、外觀和風格，以及組織。 它通常包括標籤、提供輸入的互動區域、說明圖示，以及欄位的簡短和詳細說明。 本文討論的外觀自訂適用於欄位輸入區域的外觀。

**jQuery外掛程式** 提供基於jQuery Widget架構的標準機制，以實作替代外觀。

**ClientLib** AEM使用者端處理中的使用者端程式庫系統，由複雜的JavaScript和CSS程式碼驅動。 如需詳細資訊，請參閱使用使用者端資料庫。

**原型** 定義為Maven專案原始模式或模型的Maven專案範本工具組。 如需詳細資訊，請參閱原型簡介。

**使用者控制項** 指包含欄位值的Widget中的主要元素，並由外觀架構用來將自訂Widget UI與調適型表單模型繫結。

## 建立自訂外觀的步驟 {#steps-to-create-a-custom-appearance}

建立自訂外觀的高層步驟如下：

1. **建立專案**：建立可產生內容套件的Maven專案，以部署在AEM上。
1. **擴充現有的Widget類別**：擴充現有的Widget類別並覆寫必要的類別。
1. **建立使用者端資源庫**：建立 `clientLib: af.customwidget` 程式庫並新增必要的JavaScript和CSS檔案。

1. **建置並安裝專案**：建置Maven專案並在AEM上安裝產生的內容套件。
1. **更新最適化表單**：更新最適化表單欄位屬性以使用自訂外觀。

### 建立專案 {#create-a-project}

Maven原型是建立自訂外觀的起點。 要使用的原型的詳細資訊如下：

* **存放庫**： https://repo1.maven.org/maven2/com/adobe/
* **成品ID**： custom-appearance-archetype
* **群組ID**： com.adobe.aemforms
* **版本**： 1.0.4

執行以下命令，根據原型建立本機專案：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

該命令會從存放庫下載Maven外掛程式和原型資訊，並根據以下資訊產生專案：

* **groupId**：產生的Maven專案使用的群組ID
* **artifactId**：產生的Maven專案所使用的成品ID。
* **版本**：產生的Maven專案的版本。
* **封裝**：用於檔案結構的套件。
* **成品名稱**：產生的AEM封裝的成品名稱。
* **packageGroup**：產生的AEM套件的套件群組。
* **widgetName**：用於參照的外觀名稱。

產生的專案具有以下結構：

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 擴充現有的Widget類別 {#extend-an-existing-widget-class}

建立專案範本後，視需要執行下列變更：

1. 將協力廠商外掛程式相依性納入專案中。

   1. 將協力廠商或自訂jQuery外掛程式放入 `jqueryplugin/javascript` 中的資料夾和相關CSS檔案 `jqueryplugin/css` 資料夾。 如需詳細資訊，請參閱 `jqueryplugin/javascript and jqueryplugin/css` 資料夾。

   1. 修改 `js.txt` 和 `css.txt` 檔案以包含jQuery外掛程式的任何其他JavaScript和CSS檔案。

1. 將協力廠商外掛程式與框架整合，以啟用自訂外觀框架與jQuery外掛程式之間的互動。 只有在您擴充或覆寫下列功能後，新Widget才能運作。

<table>
 <tbody>
  <tr>
   <td><strong>函数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>轉譯器函式會傳回Widget預設HTML元素的jQuery物件。 預設HTML元素應為可聚焦型別。 例如， <code>&lt;a&gt;</code>， <code>&lt;input&gt;</code>、和 <code>&lt;li&gt;</code>. 傳回的元素會用作 <code>$userControl</code>. 如果 <code>$userControl</code> 指定上述限制，此限制的 <code>AbstractWidget</code> 類別如預期般運作，其他部分常見的API （焦點、點選）需要變更。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>傳回對應以將HTML事件轉換為XFA事件。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此範例顯示 <code>blur</code> 是HTML事件，且 <code>XFA_EXIT_EVENT</code> 是對應XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>傳回提供選項變更時所要執行動作詳細資訊的地圖。 鍵值是提供給Widget的選項，值是偵測到選項變更時呼叫的函式。 Widget為所有常見選項提供處理常式(除了 <code>value</code> 和 <code>displayValue</code>)。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每當jQuery Widget的值儲存在XFA模型中（例如文字欄位的退出事件），jQuery Widget架構就會載入函式。 實作應傳回儲存在Widget中的值。 處理常式會提供選項的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>根據預設，在XFA中，輸入事件時， <code>rawValue</code> 欄位的「 」會顯示。 呼叫此函式是為了顯示 <code>rawValue</code> 至使用者。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>依預設，在退出事件的XFA中， <code>formattedValue</code> 欄位的「 」會顯示。 呼叫此函式是為了顯示 <code>formattedValue</code> 至使用者。 </td>
  </tr>
 </tbody>
</table>

1. 更新中的JavaScript檔案 `integration/javascript` 資料夾（視需要）。

   * 取代文字 `__widgetName__` 包含實際Widget名稱。
   * 從適當的現成可用Widget類別延伸Widget。 在大多數情況下，它是與要取代的現有Widget相對應的Widget類別。 父類別名稱用於多個位置，因此建議搜尋字串的所有例項 `xfaWidget.textField` 並將它們替換為實際使用的父類別。
   * 擴充 `render` 提供替代UI的方法。 這是叫用jQuery外掛程式以更新UI或互動行為的位置。 此 `render` 方法應傳回使用者控制元素。

   * 擴充 `getOptionsMap` 覆寫任何因Widget變更而受影響的選項設定的方法。 此函式會傳回對應，提供選項變更時執行動作的詳細資訊。 鍵值是提供給Widget的選項，值是偵測到選項變更時呼叫的函式。
   * 此 `getEventMap` 方法將由Widget觸發的事件與最適化表單模型所需的事件對應。 預設值會對應預設Widget的標準HTML事件，而且如果觸發替代事件，則需要更新。
   * 此 `showDisplayValue` 和 `showValue` 套用display和edit picture子句，而且可以覆寫為有替代行為。

   * 此 `getCommitValue` 當以下情況時，調適型表單框架會呼叫方法： `commit`事件發生。 一般而言，這是退出事件（除了下拉式選單、選項按鈕和核取方塊元素，這些元素會在變更時發生）。 如需詳細資訊，請參閱 [最適化Forms運算式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * 範本檔案提供各種方法的範例實作。 移除不可擴充的方法。

### 建立使用者端資源庫 {#create-a-client-library}

Maven原型產生的範例專案會自動建立所需的使用者端資料庫，並將其包裝到具有類別的使用者端資料庫中 `af.customwidgets`. JavaScript和CSS檔案可用於 `af.customwidgets` 會在執行階段自動包含。

### 建置和安裝 {#build-and-install}

若要建置專案，請在殼層上執行以下命令，以產生需要安裝在AEM伺服器上的CRX套件。

`mvn clean install`

>[!NOTE]
>
>Maven專案是指POM檔案內的遠端存放庫。 此資訊僅供參考，根據Maven標準，存放庫資訊會擷取至 `settings.xml` 檔案。

### 更新最適化表單 {#update-the-adaptive-form}

若要將自訂外觀套用至最適化表單欄位：

1. 在編輯模式下開啟最適化表單。
1. 開啟 **屬性** 要套用自訂外觀之欄位的對話方塊。
1. 在 **樣式** 標籤，更新 `CSS class` 屬性來新增外觀名稱 `widget_<widgetName>` 格式。 例如： **widget_numericstepper**

## 範例：建立自訂外觀   {#sample-create-a-custom-appearance-nbsp}

現在來看看範例，如何建立自訂外觀，讓數值欄位顯示為數值步進器或滑桿。 執行下列步驟：

1. 執行以下命令以根據Maven原型建立本機專案：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它會提示您指定下列引數的值。
   *此範例中使用的值會以粗體突出顯示*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導覽至 `customWidgets` (為指定的值 `artifactID` 屬性)，然後執行下列命令來產生Eclipse專案：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具，然後執行下列操作以匯入Eclipse專案：

   1. 選取 **[!UICONTROL 檔案>匯入>將現有專案匯入工作區中]**.

   1. 瀏覽並選取您執行 `archetype:generate` 命令。

   1. 按一下 **[!UICONTROL 完成]**.

      ![eclipse熒幕擷圖](assets/eclipse-screenshot.png)

1. 選取要用於自訂外觀的Widget。 此範例使用下列數值步進器Widget：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse專案中，檢閱 `plugin.js` 檔案以確保其符合外觀要求。 在此範例中，外觀符合下列要求：

   * 數值步進器應從 `- $.xfaWidget.numericInput`.
   * 此 `set value` widget的方法會在焦點位於欄位後設定值。 這是最適化表單Widget的強制要求。
   * 此 `render` 方法必須覆寫才能叫用 `bootstrapNumber` 方法。

   * 外掛程式除了主要原始程式碼外，沒有其他相依性。
   * 範例不會在步進器上執行任何樣式，因此不需要額外的CSS。
   * 此 `$userControl` 物件應可供 `render` 方法。 它是以下欄位： `text` 使用外掛程式程式碼複製的型別。

   * 此 **+** 和 **-** 欄位停用時，按鈕應該停用。

1. 取代 `bootstrap-number-input.js` （jQuery外掛程式）及其內容 `numericStepper-plugin.js` 檔案。
1. 在 `numericStepper-widget.js` 檔案中，新增下列程式碼以覆寫render方法以叫用外掛程式並傳回 `$userControl` 物件：

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 在 `numericStepper-widget.js` 檔案，覆寫 `getOptionsMap` 屬性以覆寫存取選項，並在停用模式中隱藏+和 — 按鈕。

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 儲存變更，導覽至包含 `pom.xml` 檔案，並執行以下Maven命令來建置專案：

   `mvn clean install`

1. 使用AEM Package Manager安裝套件。

1. 在您要套用自訂外觀的編輯模式中開啟最適化表單，然後執行下列動作：

   1. 以滑鼠右鍵按一下要套用外觀的欄位，然後按一下 **[!UICONTROL 編輯]** 以開啟「編輯元件」對話方塊。

   1. 在「樣式」標籤中，更新 **[!UICONTROL CSS類別]** 要新增的屬性 `widget_numericStepper`.

您剛建立的新外觀現在可供使用。
