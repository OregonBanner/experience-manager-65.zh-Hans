---
title: 单点登录
seo-title: 单点登录
description: 了解如何为AEM实例配置单点登录(SSO)。
seo-description: 了解如何为AEM实例配置单点登录(SSO)。
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: 配置
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 单点登录{#single-sign-on}

单点登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 单独的系统（称为受信任的验证器）执行验证并提供Experience Manager和用户凭据。 Experience Manager检查并强制用户访问权限（即确定允许用户访问哪些资源）。

SSO身份验证处理程序服务(`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)处理受信任的身份验证器提供的身份验证结果。 SSO身份验证处理程序将ssid（SSO标识符）作为特殊属性的值以此顺序搜索到以下位置：

1. 请求标头
1. Cookie
1. 请求参数

找到值后，搜索即已完成，并且会使用此值。

配置以下两项服务以识别存储ssid的属性的名称：

* 登录模块。
* SSO身份验证服务。

您必须为两个服务指定相同的属性名称。 该属性包含在提供给`Repository.login`的`SimpleCredentials`中。 属性值不相关且被忽略，仅存在属性值很重要且经过验证。

## 配置SSO {#configuring-sso}

要为AEM实例配置SSO，您需要配置[SSO身份验证处理程序](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. 使用AEM时，可通过多种方法来管理此类服务的配置设置；有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

   例如，对于NTLM集：

   * **路径：** （根据需要）；例如，  `/`
   * **标题名称**:  `LOGON_USER`
   * **ID格式**:  `^<DOMAIN>\\(.+)$`

      其中， `<*DOMAIN*>`被替换为您自己的域名。
   对于CoSign:

   * **路径：** （根据需要）；例如，  `/`
   * **标题名称**:remote_user
   * **ID格式：** 原样

   对于SiteMinder:

   * **路径：** （根据需要）；例如，  `/`
   * **标头名称：** SM_USER
   * **ID格式**:原样



1. 确认单点登录可按要求运行；包括授权。

>[!CAUTION]
>
>确保用户在配置SSO时无法直接访问AEM。
>
>通过要求用户通过运行您的SSO系统代理的Web服务器，可确保没有用户能够直接发送标头、Cookie或参数，以使用户受AEM信任，因为如果从外部发送，代理将过滤此类信息。
>
>任何无需通过Web服务器即可直接访问您的AEM实例的用户，如果知道名称，则可以通过发送标头、Cookie或参数来充当任何用户。
>
>另外，在标头、Cookie和请求参数名称中，您只需配置SSO设置所需的名称。


>[!NOTE]
>
>单点登录通常与[LDAP](/help/sites-administering/ldap-config.md)结合使用。

>[!NOTE]
>
>如果您还在Microsoft Internet Information Server(IIS)中使用[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，则需要在以下位置进行其他配置：
>
>* `disp_iis.ini`
>* IIS

>
>
在`disp_iis.ini`集中：
>（有关完整详细信息，请参阅[使用Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server)安装Dispatcher）
>
>* `servervariables=1` （将IIS服务器变量作为请求标头转发到远程实例）
>* `replaceauthorization=1` （将除“Basic”之外的任何名为“Authorization”的标头替换为其“Basic”等效项）

>
>
在IIS中：
>
>* 禁用&#x200B;**匿名访问**
   >
   >
* 启用&#x200B;**集成的Windows身份验证**

>



使用Felix控制台的&#x200B;**Authenticator**&#x200B;选项，您可以看到哪个身份验证处理程序正在应用于内容树的任何部分；例如：

`http://localhost:4502/system/console/slingauth`

首先查询最匹配路径的处理程序。 例如，如果为路径`/`配置handler-A，为路径`/content`配置handler-B，则对`/content/mypage.html`的请求将首先查询handler-B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 示例 {#example}

对于Cookie请求（使用URL `http://localhost:4502/libs/wcm/content/siteadmin.html`）：

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用以下配置：

* **路径**: `/`

* **标题名称**:  `TestHeader`

* **Cookie名称**:  `TestCookie`

* **参数名称**:  `TestParameter`

* **ID格式**:  `AsIs`

答复是：

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

如果您请求：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，也可以使用以下curl命令将`TestHeader`标头发送到`admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在浏览器中使用请求参数时，您将只看到一些HTML — 不带CSS。 这是因为HTML中的所有请求都是在没有请求参数的情况下发出的。

## 删除AEM注销链接{#removing-aem-sign-out-links}

使用SSO时，登录和注销在外部进行处理，这样AEM本身的注销链接便不再适用，应该删除。

可通过以下步骤删除欢迎屏幕上的注销链接。

1. 将`/libs/cq/core/components/welcome/welcome.jsp`叠加到`/apps/cq/core/components/welcome/welcome.jsp`
1. 从jsp中删除以下部分。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

要删除右上角用户个人菜单中可用的注销链接，请执行以下步骤：

1. 将`/libs/cq/ui/widgets/source/widgets/UserInfo.js`叠加到`/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 从文件中删除以下部分：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
