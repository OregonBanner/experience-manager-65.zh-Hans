---
title: 配置Cookie使用情况
seo-title: 配置Cookie使用情况
description: AEM提供一项服务，允许您配置和控制Cookies在网页中的使用方式
seo-description: AEM提供一项服务，允许您配置和控制Cookies在网页中的使用方式
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# 配置Cookie使用情况{#configuring-cookie-usage}

AEM提供一项服务，允许您配置和控制Cookies在网页中的使用方式：

* 可配置的服务器端服务会维护可使用的cookie的列表。
* javascript API使您的javascript代码能够验证是否可以使用cookie。

使用此功能可确保您的页面符合用户对cookie使用的同意。

## 配置允许的Cookie {#configuring-allowed-cookies}

配置Adobe Granite退出服务以指定在您的网页上如何使用cookie。 下表介绍了可配置的属性。

要配置服务，可以使用Web [控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) , [或将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表描述了任何一种方法所需的属性。 对于OSGi配置，服务PID为 `com.adobe.granite.optout`。

| 属性名称（Web控制台） | OSGi属性名称 | 描述 |
|---|---|---|
| 选择退出Cookie | optout.cookies | Cookie的名称，当在用户设备上显示时，它指示用户未同意使用Cookie。 |
| 退出HTTP头 | optout.headers | HTTP头的名称，当存在时，它指示用户未同意使用cookie。 |
| 白列表Cookie | optout.whitelist.cookies | 一列表对网站功能至关重要的cookie，未经用户同意即可使用。 |

## 验证Cookie使用 {#validating-cookie-usage}

使用客户端javascript调用Adobe Granite退出服务以验证您是否可以使用cookie。 使用Granite.OptOutUtil javascript对象执行下列任一任务:

* 获取一列表cookie名称，以指示用户不同意将cookie用于跟踪目的。
* 获取可使用的列表cookie。
* 确定Web浏览器是否包含Cookie，该Cookie指示用户不同意使用Cookie进行跟踪。
* 确定是否可以使用特定Cookie。

granite.utils客 [户端库文件夹](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) 提供Granite.OptOutUtil对象。 将以下代码添加到页面标题JSP，以包含指向javascript库的链接：

`<ui:includeClientLib categories="granite.utils" />`

例如，以下javascript函数确定在写入COOKIE_NAME Cookie之前是否允许使用它：

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

## Granite.OptOutUtil Javascript对象 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil允许您确定是否允许使用cookie。

### getCookieNames()函数 {#getcookienames-function}

返回cookie的名称，当存在时，该名称表示用户尚未同意使用cookie。

**参数**

无.

**退货**

一组cookie名称。

#### getWhitelistCookieNames()函数 {#getwhitelistcookienames-function}

返回可以使用的Cookie的名称，无论用户是否同意。

**参数**

无.

**退货**

一组cookie名称。

#### isOptedOut()函数 {#isoptedout-function}

确定用户的浏览器是否包含任何表示尚未同意使用cookie的cookie。

**参数**

无.

**退货**

一个布尔值，如 `true` 果发现cookie表示未同意，则该值为，如果没有cookie表示未 `false` 同意，则该值为。

### maySetCookie(cookieName)函数 {#maysetcookie-cookiename-function}

确定是否可以在用户的浏览器上使用特定的Cookie。 此函数等效于结合使用 `isOptedOut` 函数来确定给定的cookie是否包含在函数返回的列表 `getWhitelistCookieNames` 中。

**参数**

* cookieName: 字符串。 cookie的名称。

**退货**

一个布尔值， `true` 如果 `cookieName` 可以使用，或一个值，如 `false` 果不能 `cookieName` 使用。
