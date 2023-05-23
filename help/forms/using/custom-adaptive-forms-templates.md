---
title: 建立自訂最適化表單範本
seo-title: Creating a custom adaptive form template
description: 本文介紹如何建立自訂最適化表單範本。
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# 建立自訂最適化表單範本{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms已推出動態範本。 您可以使用AEM Sites範本編輯器 [建立或編輯動態範本](../../forms/using/template-editor.md). 下文中提及的範本為靜態範本。 預設安裝中無法提供這些選項。 [安裝相容性套件](../../forms/using/compatibility-package.md) 以便在您的環境中取得這些範本。

## 前提条件 {#prerequisites}

* 瞭解AEM [頁面範本](/help/sites-authoring/templates.md) 和 [最適化表單製作](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* 瞭解AEM [使用者端資源庫](/help/sites-developing/clientlibs.md)

## 自適應表單範本 {#adaptive-form-template}

調適型表單範本是專用的AEM頁面範本，具有用來建立調適型表單的特定屬性和內容結構。 範本有預先設定的版面、樣式和基本初始內容結構。

建立表單後，對原始範本內容結構所做的任何變更都不會反映在表單中。

## 預設最適化表單範本 {#default-adaptive-form-templates}

AEM QuickStart提供下列最適化表單範本：

* 調查範本：可讓您使用已設定多個欄的回應式版面，建立單頁最適化表單。 版面會根據您想要顯示表單的各種熒幕的尺寸自動調整。
* Simple Enrollment範本：可讓您使用精靈版面配置建立多步驟最適化表單。 在此配置中，您可以為每個步驟指定步驟完成運算式，在精靈繼續下一步之前驗證此運算式。
* 索引標籤式註冊範本：可讓您使用索引標籤左側的版面配置建立多索引標籤最適化表單，您可以在其中以任意順序瀏覽索引標籤。
* 進階註冊範本：可讓您建立包含多個索引標籤和精靈的表單。 它使用索引標籤在左側的版面，可讓您以任意順序造訪索引標籤。 它使用Adobe Document Cloud設計服務來簽署和驗證。
* 空白範本：可讓您建立不含任何頁首、頁尾和初始內容的表單。 您可以新增文字方塊、按鈕和影像等元件。 空白範本可讓您建立表單，您可以 [內嵌於AEM網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md).

這些範本具有 `sling:resourceType` 屬性會設定為對應的頁面元件。 頁面元件會轉譯CQ頁面（包含調適型表單容器），接著轉譯調適型表單。

下表列舉範本與頁面元件之間的關聯：

<table>
 <tbody>
  <tr>
   <td><p><strong>模板</strong></p> </td>
   <td><p><strong>页面组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## 使用範本編輯器建立最適化表單範本 {#creating-an-adaptive-form-template-using-template-editor}

您可以使用範本編輯器來指定最適化表單的結構和初始內容。 例如，您希望所有表單作者在登錄檔單中都擁有一些文字方塊、導覽按鈕和提交按鈕。 您可以建立範本，供作者用來建立與其他登錄檔單一致的表單。 AEM範本編輯器可讓您：

* 在結構層中新增表單的頁首與頁尾元件
* 提供表單的初始內容。
* 指定主題。
* 指定提交、重設和導覽等動作。

如需詳細資訊，請參閱 [範本編輯器](../../forms/using/template-editor.md).

## 從CRXDE建立最適化表單範本 {#creating-an-adaptive-form-template-from-crxde}

您可以建立範本並使用它來建立調適型表單，而不使用可用的範本。 自訂範本是以參照最適化表單容器和頁面元素（例如頁首和頁尾）的各種頁面元件為基礎。

您可以使用網站的基底頁面元件來建立這些元件。 或者，您也可以擴充現成範本使用的最適化表單的頁面元件。

執行以下步驟來建立自訂範本，例如simpleEnrollmentTemplate。

1. 導覽至您編寫執行個體上的CRXDE Lite。

1. 在/apps目錄下，為您的應用程式建立資料夾結構。 例如，如果應用程式名稱為mycompany，請建立具有此名稱的資料夾。 通常，應用程式資料夾包含元件、設定、範本、src和安裝目錄。 在此範例中，請建立元件、設定和範本資料夾。

1. 導覽至/libs/fd/af/templates資料夾。
1. 複製 `simpleEnrollmentTemplate` 節點。
1. 導覽至/apps/mycompany/templates資料夾。 以滑鼠右鍵按一下並選取 **[!UICONTROL 貼上]**.
1. 如有必要，請重新命名您所複製的範本節點。 例如，將其重新命名為註冊範本。

1. 導覽至/apps/mycompany/templates/enrollment-template位置。

1. 修改 `jcr:title` 和 `jcr:description` 屬性 `jcr:content` 節點，以區別範本與您所複製的範本。

1. 此 `jcr:content` 修改後範本的節點包含 `guideContainer` 和 `guideformtitle` 元件。 `guideContainer` 是儲存最適化表單的容器。 此 `guideformtitle` 元件會顯示應用程式名稱、說明等。

   而非 `guideformtitle`，您可以包含自訂元件或 `parsys` 元件。 例如，移除 `guideformtitle`，並新增自訂元件或 `parsys` 元件節點。 確保 `sling:resourceType` 元件的屬性會參照元件，並在頁面中定義相同的屬性 `component.jsp` 檔案。

1. 導覽至/apps/mycompany/templates/enrollment-template/jcr：content位置。

1. 開啟 **[!UICONTROL 屬性]** 標籤並變更的值 `cq:designPath` 屬性至/etc/designs/mycompany。

1. 現在建立/etc/designs/mycompany節點，用於 `cq:Page` 型別。

## 建立最適化表單頁面元件 {#create-an-adaptive-form-page-component}

自訂範本與預設範本的樣式相同，因為範本參照頁面元件/libs/fd/af/components/page/base。 您可以找到作為屬性的元件參照 `sling:resourceType` 定義於/apps/mycompany/templates/enrollment-template/jcr：content節點。 由於基礎是核心產品元件，請勿修改此元件。

1. 導覽至/apps/mycompany/templates/enrollment-template/jcr：content節點，並修改屬性的值 `sling:resourceType` 至/apps/mycompany/components/page/enrollmentpage
1. 將節點/libs/fd/af/components/page/base複製到資料夾/apps/mycompany/components/page。

1. 將複製的元件重新命名為 `enrollmentpage`.

1. **（只有在您已擁有內容頁面時）** 如果您有現有的，請執行下列步驟(a-d) `contentpage`您網站的元件。 如果您沒有現有的 `contentpage`元件時，您可以將 `resourceSuperType`屬性以指向OOTB基本頁面。

   1. 對於 `enrollmentpage` 節點，設定屬性的值 `sling:resourceSuperType` 至mycompany/components/page/contentpage。 此 `contentpage` component是您網站的基本頁面元件。 其他頁面元件可加以擴充。 移除下的指令碼檔案 `enrollmentpage`，除了 `head.jsp`， `content.jsp`、和 `library.jsp`. 此 `sling:resourceSuperType` 元件，也就是 `contentpage` 在此情況下，會包含所有這類指令碼。 頁首（包括導覽列和頁尾）繼承自 `contentpage` 元件。

   1. 開啟檔案 `head.jsp`.

      JSP檔案包含這行 `<cq.include script="library.jsp"/>`.

      此 `library.jsp` 檔案包含 `guide.theme.simpleEnrollment` 使用者端資料庫，其中包含最適化表單的樣式。

      頁面元件 `enrollmentpage` 具有獨佔 `head.jsp` 覆寫 `head.jsp` 的檔案 `contentpage` 元件。

   1. 將所有指令碼包含在 `head.jsp` 的檔案 `contentpage` 元件至 `head.jsp` 的檔案 `enrollmentpage` 元件。
   1. 在 `content.jsp` 指令碼，您可以新增其他頁面內容或參考至頁面轉譯時包含的其他元件。 例如，如果您新增自訂元件 `applicationformheader`，請確定您在JSP檔案中新增下列元件參考：

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      同樣地，如果您新增 `parsys` 元件在範本節點結構中，也包含自訂元件。

## 建立最適化表單使用者端資料庫 {#creating-an-adaptive-form-client-library}

此 `head.jsp` 的檔案 `enrollmentpage` 新範本的元件包含使用者端程式庫 `guide.theme.simpleEnrollment`. 預設範本也會使用此使用者端程式庫。 使用以下方法之一變更新範本中的樣式：

* 定義自訂主題並取代預設主題 `guide.theme.simpleEnrollment` 自訂佈景主題。
* 在/etc/designs/mycompany下定義新的使用者端程式庫。 在jsp頁面中的預設主題專案之後包含從屬端程式庫。 在此使用者端資料庫中包含所有覆寫樣式和其他Java Script檔案。

>[!NOTE]
>
>主題是指包含在用於呈現最適化表單的頁面元件中的使用者端資料庫。 使用者端資料庫主要控管最適化表單的外觀。
