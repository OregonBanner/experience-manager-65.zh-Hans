---
title: 防止CSRF攻击
seo-title: 防止CSRF攻击
description: 了解如何防止跨站点请求伪造(CSRF)攻击并保护用户数据不被破坏。
seo-description: 了解如何防止跨站点请求伪造(CSRF)攻击并保护用户数据不被破坏。
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# 防止CSRF攻击 {#preventing-csrf-attacks}

## CSRF攻击的工作方式 {#how-csrf-attacks-work}

跨站点请求伪造(CSRF)是一个网站漏洞，有效用户的浏览器用于发送恶意请求（可能通过iFrame）。 由于浏览器按域发送cookie，因此，如果用户当前已登录到应用程序，则用户的数据可能会受到损害。

例如，考虑您登录到浏览器中的管理控制台的情况。 您会收到一封包含链接的电子邮件。 单击链接，该链接将在浏览器中打开一个新选项卡。 您打开的页面包含一个隐藏的iFrame，该iFrame使用经过身份验证的AEM表单会话中的cookie向表单服务器发出恶意请求。 由于用户管理收到有效的cookie，因此它会传递请求。

## CSRF相关术语 {#csrf-related-terms}

**参考：** 来自请求的源页面的地址。 例如，site1.com上的网页包含指向site2.com的链接。 单击该链接将请求发布到site2.com。 此请求的引用者为site1.com，因为此请求来自源为site1.com的页面。

**允许列出的URI:** URI标识正在请求的表单服务器上的资源，例如，/adminui或/contentspace。 某些资源可能允许从外部站点请求进入应用程序。 这些资源被视为允许列出的URI。 表单服务器从不从允许列出的URI中执行引用检查。

**空引用器：** 当您打开新的浏览器窗口或选项卡，然后键入地址并按Enter，引用者为null。 该请求是全新的，并非源自父网页； 因此，该请求没有引证人。 表单服务器可以从以下位置接收空引用器：

* 在SOAP或REST端点上从Acrobat发出的请求
* 对AEM表单SOAP或REST端点发出HTTP请求的任何桌面客户端
* 打开新的浏览器窗口并输入任何AEM表单Web应用程序登录页面的URL时

允许在SOAP和REST端点上使用空引用器。 还允许对/adminui和/contentspace等所有URI登录页及其相应映射资源使用空引用程序。 例如，/contentspace的映射servlet为/contentspace/faces/jsp/login.jsp，它应为空引用器异常。 仅当为Web应用程序启用GET过滤时，才需要此异常。 应用程序可以指定是否允许空引用器。 请参阅AEM表单的强化和安全性中的“防止跨站 [点请求伪造攻击”](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)。

**允许的引用者异常：** 允许的引用者例外是允许的引用者列表的子列表，从中阻止请求。 允许引用例外是Web应用程序特有的。 如果不允许允许引用者的子集调用特定的Web应用程序，您可以通过允许的引用者例外阻止引用者列表。 允许的引用例外在应用程序的web.xml文件中指定。 （请参阅帮助和教程页面上的AEM表单强化和安全性中的“防止跨站点请求伪造攻击”。）

## 允许的参考者如何工作 {#how-allowed-referers-work}

AEM表单提供引用器过滤功能，有助于防止CSRF攻击。 下面是引用筛选的工作方式：

1. 表单服务器检查用于调用的HTTP方法：

   * 如果是POST，表单服务器将执行引用器头检查。
   * 如果它为GET，则表单服务器会绕过引用器检查，除非CSRF_CHECK_GETS设置为true，在这种情况下，它将执行引用器头检查。 CSRF_CHECK_GETS在应用程序的web.xml文件中指定。 (请参阅《强化和安全指南》中的“防止跨站点请 [求伪造攻击](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)”。)

1. 表单服务器检查是否允许列出请求的URI:

   * 如果允许列出URI，则服务器将传递请求。
   * 如果未允许列出请求的URI，则服务器检索请求的引用者。

1. 如果请求中有引用者，服务器将检查它是否为允许的引用者。 如果允许，服务器将检查引用者异常：

   * 如果此请求为例外，则阻止该请求。
   * 如果不是例外，则会通过请求。

1. 如果请求中没有引用器，服务器将检查是否允许空引用器。

   * 如果允许空引用器，则会传递请求。
   * 如果不允许空引用器，服务器将检查所请求的URI是否为空引用器的例外，并相应地处理该请求。

## 配置允许的引用者 {#configure-allowed-referers}

运行Configuration Manager时，默认主机和IP地址或表单服务器将添加到允许的引用列表。 您可以在管理控制台中编辑此列表。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“配置允许的引用者URL”。 “允许的引用者”列表卡显示在页面底部。
1. 要添加允许的引用者，请执行以下操作：

   * 在“允许的引用者”框中键入主机名或IP地址。 要一次添加多个允许的引用者，请在新行上键入每个主机名或IP地址。
   * 在“HTTP端口”和“HTTPS端口”框中，指定允许HTTP、HTTPS或同时允许HTTP和／或HTTPS的端口。 如果将这些框留空，则使用默认端口（HTTP的端口80和HTTPS的端口443）。 如果在框 `0` 中输入（零），则启用该服务器上的所有端口。 您还可以输入特定端口号以仅启用该端口。
   * 单击添加。

1. 要从允许的引用列表中删除条目，请从列表中选择该项，然后单击删除。

   如果允许的引用列表为空，则CSRF功能将停止工作，并且系统将变得不安全。

1. 更改允许的引用列表后，重新启动AEM表单服务器。

