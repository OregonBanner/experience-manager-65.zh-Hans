---
title: 防止CSRF攻击
seo-title: 防止CSRF攻击
description: 了解如何防止跨站点请求伪造(CSRF)攻击，并保护用户数据免遭入侵。
seo-description: 了解如何防止跨站点请求伪造(CSRF)攻击，并保护用户数据免遭入侵。
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 防止CSRF攻击{#preventing-csrf-attacks}

## CSRF攻击的工作原理{#how-csrf-attacks-work}

跨站点请求伪造(CSRF)是一个网站漏洞，有效用户的浏览器可能通过iFrame发送恶意请求。 由于浏览器基于域发送Cookie，因此如果用户当前已登录到应用程序，则用户数据可能会受到损害。

例如，假定您在浏览器中登录到管理控制台。 您会收到一封包含链接的电子邮件。 单击该链接，即会在浏览器中打开一个新选项卡。 您打开的页面包含一个隐藏的iFrame，该iFrame会使用经过身份验证的AEM Forms会话中的Cookie向Forms服务器发出恶意请求。 由于用户管理收到有效的Cookie，因此它会传递请求。

## 与CSRF相关的术语{#csrf-related-terms}

**Referer:** 请求从中发生的源页面的地址。例如，site1.com上的网页包含指向site2.com的链接。 单击该链接会向site2.com发布请求。 此请求的引用者是site1.com ，因为该请求来自源为site1.com的页面。

**列入允许列表的URI:** URI标识正在请求的表单服务器上的资源，例如/adminui或/contentspace。某些资源可能允许请求从外部站点进入应用程序。 这些资源被视列入允许列表为已URI。 表单服务器从不从的URI中执行列入允许列表引用检查。

**Null引用：** 当您打开新的浏览器窗口或选项卡，然后键入地址并按Enter时，引用为null。该请求是全新的，并非源自父网页；因此，请求没有引用。 表单服务器可从以下位置接收空引用：

* 对来自Acrobat的SOAP或REST端点发出的请求
* 在AEM表单SOAP或REST端点上发出HTTP请求的任何桌面客户端
* 当打开新的浏览器窗口并输入任何AEM forms web应用程序登录页面的URL时

允许在SOAP和REST端点上使用空引用。 此外，还允许在所有URI登录页面（如/adminui和/contentspace）及其相应映射资源上使用空引用。 例如，/contentspace的映射Servlet是/contentspace/faces/jsp/login.jsp，这应该是空引用器异常。 仅当您为Web应用程序启用GET过滤时，才需要此例外。 您的应用程序可以指定是否允许空反向链接。 请参阅[Harding and Security for AEM forms](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)中的“避免跨站点请求伪造攻击”。

**允许的引用程序异常：** 允许的引用程序异常是允许的引用程序列表的子列表，从中可以阻止请求。允许的引用例外特定于Web应用程序。 如果不允许允许的反向链接的子集调用特定的Web应用程序，则可以通过允许的阻止列表反向链接例外来反向链接。 允许的引用例外在应用程序的web.xml文件中指定。 (请参阅帮助和Tutorials页面上针对AEM表单的强化和安全功能中的“避免跨站点请求伪造攻击”。)

## 允许的引荐如何工作{#how-allowed-referers-work}

AEM Forms提供反向链接过滤，这有助于防止CSRF攻击。 以下是引用过滤的工作方式：

1. 表单服务器检查用于调用的HTTP方法：

   * 如果是POST，则表单服务器会执行引用头检查。
   * 如果是GET，则Forms服务器会绕过反向链接检查，除非将CSRF_CHECK_GETS设置为true，在这种情况下，它会执行反向链接标头检查。 CSRF_CHECK_GETS在应用程序的web.xml文件中指定。 (请参阅[Hardening and Security Guide](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)中的“Protecting for Cross-Site Request Furshing attacks”（防止跨站点请求伪造攻击）。)

1. 表单服务器检查请求的URI是否列入允许列表被：

   * 如果URI被列入允许列表，服务器将传递请求。
   * 如果未请求的URI列入允许列表，则服务器将检索请求的引用。

1. 如果请求中存在引用，则服务器会检查它是否为允许的引用。 如果允许，则服务器会检查是否存在引用者异常：

   * 如果是异常，则阻止请求。
   * 如果不是例外，则会传递请求。

1. 如果请求中没有引用器，则服务器检查是否允许空引用器。

   * 如果允许空引用，则会传递请求。
   * 如果不允许空引用，则服务器检查所请求的URI是否为空引用的例外，并相应地处理该请求。

## 配置允许的反向链接{#configure-allowed-referers}

运行配置管理器时，默认主机和IP地址或表单服务器会添加到允许的引用列表。 您可以在管理控制台中编辑此列表。

1. 在管理控制台中，单击设置>用户管理>配置>配置允许的引用URL。允许的引用列表将显示在页面底部。
1. 要添加允许的引用，请执行以下操作：

   * 在允许的反向链接框中键入主机名或IP地址。 要一次添加多个允许的引用，请在新行上键入每个主机名或IP地址。
   * 在“HTTP端口”和“HTTPS端口”框中，指定允许HTTP和/或HTTPS的端口。 如果将这些框留空，则使用默认端口（HTTP的端口80和HTTPS的端口443）。 如果在框中输入`0`（零），则该服务器上的所有端口都将启用。 您还可以输入特定端口号以仅启用该端口。
   * 单击添加。

1. 要从允许的引用列表中删除条目，请从列表中选择该项目，然后单击删除。

   如果允许的引用列表为空，则CSRF功能将停止工作，并且系统将变得不安全。

1. 更改允许的引用列表后，重新启动AEM表单服务器。
