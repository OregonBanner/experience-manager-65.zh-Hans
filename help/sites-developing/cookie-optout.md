---
title: 設定Cookie使用方式
seo-title: Configuring Cookie Usage
description: AEM提供的服務可讓您設定和控制Cookie在您的網頁中的使用方式
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# 設定Cookie使用方式{#configuring-cookie-usage}

AEM提供的服務可讓您設定及控制如何將Cookie用於您的網頁：

* 可設定的伺服器端服務會維護可用的Cookie清單。
* Javascript API可讓您的Javascript程式碼驗證Cookie是否可以使用。

使用此功能可確保您的頁面符合使用者對Cookie使用方式的同意。

## 設定允許的Cookie {#configuring-allowed-cookies}

設定AdobeGranite選擇退出服務，指定如何在您的網頁上使用Cookie。 下表說明您可以設定的特性。

若要設定服務，您可以使用 [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [將OSGi設定新增至存放庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). 下表說明任一方法所需的屬性。 若為OSGi設定，服務PID為 `com.adobe.granite.optout`.

| 属性名称（Web 控制台） | OSGi 属性名称 | 描述 |
|---|---|---|
| 選擇退出Cookie | optout.cookies | Cookie的名稱，當顯示在使用者的裝置上時，表示使用者尚未同意使用Cookie。 |
| 選擇退出HTTP標頭 | optout.headers | 表示使用者尚未同意使用Cookie的HTTP標頭名稱（如果存在）。 |
| 白名單Cookie | optout.whitelist.cookies | 此清單列出對網站運作而言不可或缺的Cookie，且可在未經使用者同意的情況下使用。 |

## 驗證Cookie使用方式 {#validating-cookie-usage}

使用使用者端JavaScript來呼叫Adobe Granite選擇退出服務，以確認您可以使用Cookie。 使用Granite.OptOutUtil javascript物件來執行下列任何工作：

* 取得Cookie名稱清單，該清單指出使用者不同意將Cookie用於追蹤目的。
* 取得可用的Cookie清單。
* 判斷網頁瀏覽器是否包含Cookie，指出使用者不同意使用Cookie進行追蹤。
* 決定是否可使用特定Cookie。

granite.utils [使用者端資料庫資料夾](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) 提供Granite.OptOutUtil物件。 將下列程式碼新增至頁面標頭JSP以包含JavaScript程式庫的連結：

`<ui:includeClientLib categories="granite.utils" />`

例如，下列javascript函式會先判斷是否允許使用COOKIE_NAME Cookie，再寫入至其中：

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil Javascript物件 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil可讓您判斷是否允許使用Cookie。

### getCookieNames()函式 {#getcookienames-function}

傳回Cookie的名稱，當出現時，表示使用者未同意使用Cookie。

**参数**

无。

**傳回**

Cookie名稱的陣列。

#### getWhitelistCookieNames()函式 {#getwhitelistcookienames-function}

不論使用者是否同意，都會傳回可使用的Cookie名稱。

**参数**

无。

**傳回**

Cookie名稱的陣列。

#### isOptedOut()函式 {#isoptedout-function}

判斷使用者的瀏覽器是否包含指出未同意使用Cookie的任何Cookie。

**参数**

无。

**傳回**

布林值 `true` 如果找到表示不同意的Cookie，且值為 `false` 如果沒有Cookie表示不同意。

### maySetCookie(cookieName)函式 {#maysetcookie-cookiename-function}

決定是否可在使用者的瀏覽器上使用特定Cookie。 此函式等同於使用 `isOptedOut` 與判斷特定Cookie是否包含在符合以下條件的清單中 `getWhitelistCookieNames` 函式傳回。

**参数**

* cookieName：字串。 Cookie的名稱。

**傳回**

布林值 `true` 如果 `cookieName` 可使用，或值為 `false` 如果 `cookieName` 無法使用。
