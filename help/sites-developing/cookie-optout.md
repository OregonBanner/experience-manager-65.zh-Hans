---
title: 配置Cookie使用情况
seo-title: 配置Cookie使用情况
description: AEM提供了一项服务，可让您配置和控制如何在网页中使用cookie
seo-description: AEM提供了一项服务，可让您配置和控制如何在网页中使用cookie
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# 配置Cookie使用情况{#configuring-cookie-usage}

AEM提供了一项服务，可让您配置和控制如何在您的网页中使用cookie:

* 可配置的服务器端服务维护可使用的Cookie列表。
* Javascript API允许您的Javascript代码验证是否可以使用Cookie。

使用此功能可确保您的页面符合用户对Cookie使用情况的同意。

## 配置允许的Cookie {#configuring-allowed-cookies}

配置AdobeGranite选择退出服务以指定如何在您的网页上使用Cookie。 下表介绍了可配置的属性。

要配置服务，可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表介绍了任一方法所需的属性。 对于OSGi配置，服务PID为`com.adobe.granite.optout`。

| 属性名称（Web控制台） | OSGi属性名称 | 描述 |
|---|---|---|
| 禁用Cookie | optout.cookies | Cookie的名称，当用户设备上存在时，该名称指示用户不同意使用Cookie。 |
| 选择禁用HTTP标头 | optout.headers | 表示用户未同意使用Cookie的HTTP标头的名称（如果存在）。 |
| 白名单Cookie | optout.whitelist.cookies | 对网站运行至关重要，且未经用户同意即可使用的Cookie列表。 |

## 验证Cookie使用情况{#validating-cookie-usage}

使用客户端Javascript调用AdobeGranite选择退出服务，以验证您是否可以使用Cookie。 使用Granite.OptOutUtil javascript对象执行以下任何任务：

* 获取表示用户不同意将Cookie用于跟踪的Cookie名称列表。
* 获取可使用的Cookie列表。
* 确定Web浏览器是否包含指示用户不同意使用Cookie进行跟踪的Cookie。
* 确定是否可以使用特定Cookie。

granite.utils [客户端库文件夹](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)提供了Granite.OptOutUtil对象。 将以下代码添加到页眉JSP，以包含指向Javascript库的链接：

`<ui:includeClientLib categories="granite.utils" />`

例如，以下javascript函数确定是否允许在写入COOKIE_NAME Cookie之前使用该Cookie:

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

## Granite.OptOutUtil Javascript对象{#the-granite-optoututil-javascript-object}

Granite.OptOutUtil允许您确定是否允许使用Cookie。

### getCookieNames()函数{#getcookienames-function}

返回Cookie的名称（如果存在），表示用户未同意使用Cookie。

**参数**

无.

**返回结果**

Cookie名称数组。

#### getWhitelistCookieNames()函数{#getwhitelistcookienames-function}

返回可在用户同意的情况下使用的Cookie的名称。

**参数**

无.

**返回结果**

Cookie名称数组。

#### isOptedOut()函数{#isoptedout-function}

确定用户的浏览器是否包含任何指示尚未同意使用Cookie的Cookie。

**参数**

无.

**返回结果**

如果找到指示未同意的Cookie，则为`true`布尔值；如果没有Cookie指示未同意，则为`false`值。

### maySetCookie(cookieName)函数{#maysetcookie-cookiename-function}

确定能否在用户的浏览器上使用特定的Cookie。 此函数等同于使用`isOptedOut`函数并结合确定给定Cookie是否包含在`getWhitelistCookieNames`函数返回的列表中。

**参数**

* cookieName:字符串。 Cookie的名称。

**返回结果**

如果可以使用`cookieName`，则为`true`布尔值；如果不能使用`cookieName`，则为`false`值。
