---
title: 偵錯HTML5表單
seo-title: Debugging HTML5 forms
description: 本檔案列出疑難排解各種已知問題的步驟。
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# 偵錯HTML5表單 {#debugging-html-forms}

本檔案包含數個疑難排解案例。 針對每個案例，都提供一些疑難排解問題的步驟。 請依照下列步驟操作，如果問題仍然存在，請設定記錄器以取得並檢閱記錄檔中的錯誤/警告。 如需HTML5表單記錄的詳細資訊，請參閱 [產生HTML5表單的記錄](/help/forms/using/enable-logs.md).

## 問題：呈現表單時，我看到org.apache.sling.api.SlingException例外狀況頁面 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在例外狀況詳細資訊中，搜尋單字 **原因為**.

可能的原因是URL中的一個或多個引數不正確。

檢查下列引數：

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br /> 注意：路徑會定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

## 問題：無法呈現表單（顯示錯誤訊息） {#problem-unable-to-render-form}

1. 請確定指定的引數正確。 如需引數的詳細資訊，請參閱 [演算引數](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. 登入CRX封裝管理員(在https://&lt;server>：&lt;port>/crx/packmgr/index.jsp)，並檢查下列套件是否已正確安裝：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 在https://登入CQ網頁主控台（Felix主控台）&lt;server>：&lt;port>/system/console/bundles.

   確認下列套件組合的狀態為「作用中」：

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * AdobeXFA Forms轉譯器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * AdobeXFA Forms LC Connector

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：表單轉譯器沒有樣式 {#problem-form-renders-without-styles}

1. 在您的瀏覽器中，開啟 **開發人員工具**. 確保profile.css可供使用。
1. 如果profile.css檔案無法使用，請登入CRX DE，網址為https://&lt;server>：&lt;port>/crx/de.
1. 在左側的資料夾階層中，導覽至/etc/clientlibs/fd/xfaforms/。 開啟資料夾中列出的css.txt檔案。

   * 侧面像
   * 執行階段
   * scrollnav
   * 工具列
   * xfalib

1. 確認css.txt中提到的檔案存在於CRX DE lite的/libs/fd/xfaforms/clientlibs/xfalib/css中。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述檔案無法使用，請安裝adobe-lc-forms-runtime-pkg-&lt;version>.zip封裝。

### 問題：發生非預期的錯誤 {#problem-unexpected-error-encountered}

1. 在表單URL中，新增查詢引數debugClientLibs並將其值設定為true (例如：https://&lt;server>：&lt;port>/content/xfaforms/profiles/test.html？contentRoot=&lt;some path=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在Chrome等案頭瀏覽器中，前往開發人員工具 — >主控台。
1. 開啟記錄檔以識別錯誤型別。 如需有關記錄的詳細資訊，請參閱 [HTML5表單的記錄](/help/forms/using/enable-logs.md).
1. 前往「開發人員工具 — >主控台」。 使用棧疊追蹤來找出導致錯誤的程式碼。 對錯誤進行偵錯以解決問題。

   >[!NOTE]
   >
   >如果指令碼失敗，請檢查在PDF轉譯表單期間是否也發生相同問題。 如果是，則表單指令碼邏輯有問題。

## 問題：無法提交表單 {#problem-unable-to-submit-the-form}

1. 確保您有權存取AEM伺服器，且已連線至伺服器。
1. 檢查引數submitUrl是否正確。
1. 啟用使用者端記錄檔，如中所述： [HTML5表單的記錄](/help/forms/using/enable-logs.md) 將偵錯選項用作 **1-a5-b5-c5**. 然後轉譯表單並按一下提交。 開啟瀏覽器偵錯主控台，並檢查是否有錯誤。
1. 找到伺服器記錄檔，如中所述： [HTML5表單的記錄](/help/forms/using/enable-logs.md). 檢查在提交期間伺服器記錄中是否有任何錯誤。

## 問題：本地化錯誤訊息未顯示 {#problem-localized-error-messages-do-not-display}

1. 使用其他查詢引數轉譯表單 **debugClientLibs=true** ，然後前往「開發人員工具 — >資源」並檢查檔案I18N.css。
1. 如果檔案無法使用，請在https://登入CRX DE&lt;server>：&lt;port>/crx/de.
1. 在左側的資料夾階層中，導覽至/libs/fd/xfaforms/clientlibs/I18N，並確認下列檔案和資料夾存在：

   * Namespace.js
   * LogMessages.js
   * 語言資料夾

1. 如果以上任何檔案或資料夾不存在，請安裝 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 再次封裝。
1. 導覽至與地區設定名稱相同的資料夾，並檢查其內容。 資料夾必須包含下列檔案：

   * I18N.js
   * js.txt

1. 檢查js.txt的內容，並確認其中包含下列專案。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：影像未顯示 {#problem-image-not-showing-up}

1. 請確認影像URL正確無誤。
1. 檢查您的瀏覽器是否支援此型別的影像。
1. 在例外狀況詳細資訊中，搜尋單字 **原因為**.

   可能的原因是URL中的一個或多個引數不正確。

   檢查下列引數：步驟文字

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br /> 注意：路徑會定義資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

1. 在案頭瀏覽器中，前往開發人員工具 — >資源。

   在「影格」中檢查左側的影像（如果該影像顯示）。
