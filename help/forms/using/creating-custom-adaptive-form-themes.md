---
title: 建立自訂最適化表單主題
seo-title: Creating custom adaptive form themes
description: 最適化表單主題是AEM使用者端資料庫，可用來定義最適化表單的樣式（外觀）。 瞭解如何建立自訂最適化表單主題。
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 建立自訂最適化表單主題 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供 [主題編輯器](/help/forms/using/themes.md) 建立及修改最適化表單的功能 [主題](/help/forms/using/themes.md). 執行本文中列出的步驟，前提是您升級所使用的版本沒有 [主題編輯器](/help/forms/using/themes.md) 而且您現在已投資使用Less/CSS檔案（主題前編輯器方法）建立的主題。

## 前提条件 {#prerequisites}

* LESS (Leaner CSS)架構的相關知識
* 如何在Adobe Experience Manager中建立使用者端資源庫
* [建立最適化表單範本](/help/forms/using/custom-adaptive-forms-templates.md) 用於使用您建立的主題

## 最適化表單主題 {#adaptive-form-theme}

一個 **最適化表單主題** 是AEM使用者端資料庫，可用來定義最適化表單的樣式（外觀）。

您建立 **最適化範本** 並將主題套用至範本。 然後使用此自訂範本建立 **最適化表單**.

![最適化表單和使用者端資料庫](assets/hierarchy.png)

## 建立最適化表單主題 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>以下程式使用AEM物件的範例名稱（例如節點、屬性和資料夾）進行說明。
>
>如果您使用名稱來依照這些步驟進行，產生的範本應類似於以下快照：

![樹系主題的最適化表單快照](assets/thumbnail.png)
**圖：** *樹系主題範例*

1. 建立型別的節點 `cq:ClientLibraryFolder` 在 `/apps`節點。

   例如，建立下列節點：

   `/apps/myAfThemes/forestTheme`

1. 新增多值字串屬性 `categories` 並適當地設定其值。

   例如，將屬性設定為： `af.theme.forest`.

   ![CRX存放庫快照](assets/3-2.png)

1. 新增兩個資料夾， `less` 和 `css`和檔案 `css.txt` 至步驟1中建立的節點：

   * `less` 資料夾：包含 `less` 變數檔案，在其中定義 `less` 變數和 `less mixins` 用來管理.css樣式的物件。

      此資料夾包含 `less` 變數檔案， `less` mixin檔案， `less` 使用mixin和變數定義樣式的檔案。 然後這些較少的檔案會以styles.less匯入。

   * `css`資料夾：包含.css檔案，您可以在其中定義要在主題中使用的靜態樣式。

   **較少的變數檔案**：這些檔案可讓您定義或覆寫用於定義CSS樣式的變數。

   調適型表單提供下列.less檔案中定義的OOTB變數：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   適用性表單也提供下列定義的協力廠商變數：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用最適化表單中提供的較少量變數、覆寫這些變數，或建立新的較少量變數。

   >[!NOTE]
   >
   >匯入較少前置處理器的檔案時，請在匯入陳述式中指定檔案的相對路徑。

   覆寫變數的範例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   覆寫 `less`變數：

   1. 匯入預設最適化表單變數：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然後匯入包含被覆寫變數的較少檔案。

   新變數定義範例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **較少的mixin檔案：** 您可以定義接受變數作為引數的函式。 這些函式的輸出是結果樣式。 在不同樣式中使用這些Mixin，以避免重複CSS樣式。

   調適型表單提供中定義的OOTB Mixin：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   調適型表單也提供中定義的協力廠商mixin：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   範例mixin定義：

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Styles.less檔案：** 使用此檔案可包含您必須在使用者端資料庫中使用的所有較少檔案（變數、mixin、樣式）。

   在以下範例中 `styles.less` 檔案中，匯入陳述式可以任意順序放置。

   匯入下列.less檔案的陳述式是強制性的：

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   此 `css.txt` 包含程式庫要下載的.css檔案路徑。

   例如：

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >styles.less檔案不是強制性的。 這表示如果您尚未定義任何自訂樣式、變數或mixin，則不需要建立此檔案。
   >
   >不過，如果您未建立style.less檔案，則需在css.txt檔案中取消註解下列行：
   >
   >**`#base=less`**
   >
   >並註解下列行：
   >
   >**`styles.less`**

## 在最適化表單中使用佈景主題 {#to-use-a-theme-in-an-adaptive-form}

建立最適化表單主題後，請執行以下步驟以在最適化表單中使用此主題：

1. 包含中建立的主題 [建立最適化表單主題](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) 區段，建立型別的自訂頁面 `cq:Component`.

   例如，`/apps/myAfCustomizations/myAfPages/forestPage`

   1. 新增 `sling:resourceSuperType` 屬性並將其值設為 `fd/af/components/page/base`.

      ![CRX存放庫快照](assets/1-2.png)

   1. 若要在頁面中使用主題，您必須將覆寫檔案library.jsp新增至節點。

      然後，您會匯入在本文的建立最適化表單主題一節中建立的主題。

      下列範常式式碼片段會匯入 `af.theme.forest` 主題。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可選**：在自訂頁面中，視需要覆寫header.jsp、footer.jsp和body.jsp。

1. 建立自訂範本(例如： `/apps/myAfCustomizations/myAfTemplates/forestTemplate`)的jcr：content會指向在上一步建立的自訂頁面(例如： `myAfCustomizations/myAfPages/forestPage)`.

   ![CRX存放庫快照](assets/2-1.png)

1. 使用上一步建立的範本建立最適化表單。 最適化表單的外觀是由本文章建立最適化表單主題一節中的主題所定義。
