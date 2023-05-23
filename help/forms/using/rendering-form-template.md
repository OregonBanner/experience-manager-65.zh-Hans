---
title: 呈現HTML5表單的表單範本
seo-title: Rendering form template for HTML5 forms
description: HTML5表單設定檔與設定檔轉譯器相關聯。 設定檔轉譯器是JSP頁面，負責呼叫Forms OSGi服務來產生表單的HTML表示。
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# 呈現HTML5表單的表單範本 {#rendering-form-template-for-html-forms}

## 轉譯端點 {#render-endpoint}

HTML5表單的概念為 **設定檔** 會顯示為REST端點，以啟用表單範本的行動轉譯。 這些設定檔已 **設定檔轉譯器**. 這些是JSP頁面，負責呼叫Forms OSGi服務來產生表單的HTML表示。 設定檔節點的JCR路徑會決定轉譯器端點的URL。 指向「預設」設定檔之表單的預設轉譯端點看起來像這樣：

https://&lt;*主機*>：&lt;*連線埠*>/content/xfaforms/profiles/default.html？contentRoot=&lt;*包含表單xdp的資料夾路徑*>&amp;template=&lt;*xdp的名稱*>

例如，`http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

對於自訂設定檔，端點會據此變更。 例如，名稱為表單的自訂設定檔的端點是：

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

如果您的範本位於AEM存放庫中，且應用程式名為FormSubmission，則URI會是：

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 演算引數 {#render-parameters}

以HTML呈現表單時支援的要求引數包括：

<table>
 <tbody>
  <tr>
   <th><strong>参数 </strong></th>
   <th><strong>描述</strong></th>
  </tr>
  <tr>
   <td>範本<br /> </td>
   <td>此引數會指定範本檔案的名稱。<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>此引數會指定範本和相關資源所在的路徑。 此路徑可以是伺服器檔案系統路徑或存放庫路徑、http或ftp路徑。<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>此引數會指定表單資料xml張貼到的URL。<br /> </td>
  </tr>
 </tbody>
</table>

### 將資料與表單範本合併 {#merge-data-with-form-template}

| 参数 | 描述 |
|---|---|
| dataRef | 此引數會指定 **絕對路徑** 與範本合併的資料檔案中。 此引數可以是Rest服務的URL，此服務會以xml格式傳回資料。 |
| 資料 | 此引數會指定與範本合併的UTF-8編碼資料位元組。 如果指定此引數，HTML5表單會忽略dataRef引數。 |

### 傳遞轉譯器引數 {#passing-the-render-parameter}

HTML5表單支援三種傳遞轉譯器引數的方法。 您可以透過URL、索引鍵值配對和設定檔節點傳遞引數。 在轉譯器引數中，機碼值組擁有最高的優先順序，其後是設定檔節點。 URL要求引數的優先順序最低。

* **URL要求引數**：您可以在URL中指定轉譯器引數。 在URL要求引數中，一般使用者可看見引數。 例如，下列提交URL在URL中包含範本引數： `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute要求引數**：您可以將轉譯器引數指定為機碼值組。 在SetAttribute要求引數中，一般使用者看不到這些引數。 您可以將請求從任何其他JSP轉送到HTML5表單設定檔轉譯器JSP並使用 *setAttribute* 請求物件以傳遞所有轉譯器引數。 此方法具有最高優先順序。

* **設定檔節點要求引數：** 您可以將轉譯器引數指定為設定檔節點的節點屬性。 在設定檔節點請求引數中，一般使用者看不到引數。 設定檔節點是傳送請求的節點。 若要將引數指定為節點屬性，請使用CRXDE lite。

### 提交引數 {#submit-parameters}

HTML5表單提交資料；在AEM伺服器上執行伺服器端指令碼和Web服務。 如需用於在AEM伺服器上執行伺服器端指令碼和Web服務的引數的詳細資訊，請參閱 [HTML5表單服務Proxy](/help/forms/using/service-proxy.md).
