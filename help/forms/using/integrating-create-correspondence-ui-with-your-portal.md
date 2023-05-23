---
title: 整合建立通訊UI與您的自訂入口網站
seo-title: Integrating Create Correspondence UI with your custom portal
description: 瞭解如何整合建立通訊UI與您的自訂入口網站
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# 整合建立通訊UI與您的自訂入口網站{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概述 {#overview}

本文詳細說明如何將建立通訊解決方案與您的環境整合。

## 以URL為基礎的叫用 {#url-based-invocation}

從自訂入口網站呼叫「建立通訊」應用程式的一種方法是使用下列請求引數準備URL：

* 信件範本的識別碼（使用cmLetterId引數）。

* 從所需資料來源擷取之XML資料的URL （使用cmDataUrl引數）。

例如，自訂入口網站會將URL準備為\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`，這可能是來自入口網站連結的href。

>[!NOTE]
>
>以這種方式呼叫並不安全，因為必要的引數會作為GET請求傳遞，方法是在URL中公開相同的（清楚可見）。

>[!NOTE]
>
>在呼叫「建立通訊」應用程式之前，請儲存並上傳資料以在指定的dataURL呼叫「建立通訊」UI。 您可以從自訂入口網站本身或透過其他後端程式完成此操作。

## 內嵌資料型叫用 {#inline-data-based-invocation}

呼叫建立通訊應用程式的另一個（且更安全）方法可能是直接點選https://&#39;的URL[伺服器]：[連線埠]&#39;/[contextPath]/aem/forms/createcorrespondence.html ，同時傳送引數和資料以作為POST要求呼叫建立通訊應用程式（對一般使用者隱藏它們）。 這也表示您現在可以內嵌傳遞「建立對應」應用程式的XML資料（作為相同請求的一部分，使用cmData引數），這在先前的方法中是不可能/理想的。

### 指定字母的引數 {#parameters-for-specifying-letter}

| **名称** | **类型** | **描述** |
|---|---|---|
| cmLetterInstanceId | 字符串 | 信件例項的識別碼。 |
| cmLetterId | 字符串 | Letter範本的名稱。 |

表格中引數的順序會指定用來載入字母的引數偏好設定。

### 用於指定XML資料來源的引數 {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>來自使用基本通訊協定（例如cq、ftp、http或檔案）之來源檔案的XML資料。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>字符串</td> 
   <td>使用信件例項中可用的xml資料。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>布尔值</td> 
   <td>重複使用資料字典中附加的測試資料。</td> 
  </tr>
 </tbody>
</table>

表格中引數的順序會指定用來載入XML資料的引數偏好設定。

### 其他引數 {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td> 
   <td><strong>类型</strong></td> 
   <td><strong>描述</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>布尔值</td> 
   <td>若為True，則在預覽模式下開啟字母<br /> </td> 
  </tr>
  <tr>
   <td>随机</td> 
   <td>時間戳記</td> 
   <td>若要解決瀏覽器快取問題。</td> 
  </tr>
 </tbody>
</table>

如果您對cmDataURL使用http或cq通訊協定，應可匿名存取http/cq的URL。
