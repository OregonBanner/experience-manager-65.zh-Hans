---
title: 防止CSRF攻击
seo-title: Preventing CSRF attacks
description: 了解如何防止跨站点请求伪造(CSRF)攻击并保护用户数据不被泄露。
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 防止CSRF攻击 {#preventing-csrf-attacks}

## CSRF攻击的工作原理 {#how-csrf-attacks-work}

跨站点请求伪造(CSRF)是一种网站漏洞，其中使用有效用户的浏览器可能通过iFrame发送恶意请求。 由于浏览器基于域发送Cookie，因此如果用户当前登录到应用程序，则用户的数据可能会受损。

例如，考虑您登录到浏览器中的管理控制台的情况。 您会收到一封包含链接的电子邮件。 单击该链接，将在浏览器中打开一个新选项卡。 您打开的页面包含一个隐藏的iFrame，它会使用经过身份验证的AEM表单会话中的Cookie向表单服务器发出恶意请求。 由于User Management会收到有效的Cookie，因此会传递请求。

## CSRF相关术语 {#csrf-related-terms}

**引用网站：** 发出请求的源页面的地址。 例如，site1.com上的网页包含指向site2.com的链接。 单击该链接会将请求发布到site2.com。 此请求的引用网站为site1.com，因为该请求是从源为site1.com的页面发出的。

**已列入允许列表的URI：** URI标识正在请求的表单服务器上的资源，例如/adminui或/contentspace。 某些资源可能允许请求从外部站点进入应用程序。 这些资源被视为已列入允许列表的URI。 列入允许列表表单服务器从不执行来自URI的引用检查。

**Null引用：** 打开新的浏览器窗口或Tab键，然后键入地址并按Enter键时，引用为空。 该请求是全新请求，并非源自父网页；因此，不存在该请求的反向链接。 表单服务器可以从以下位置接收null引用：

* 在Acrobat的SOAP或REST端点上发出的请求
* 任何在AEM Forms SOAP或REST端点上发出HTTP请求的桌面客户端
* 打开新的浏览器窗口并输入任何AEM forms web应用程序登录页的URL时

在SOAP和REST端点上允许空引用。 在所有URI登录页面（如/adminui和/contentspace）及其对应的映射资源上也允许空引用。 例如，/contentspace的映射servlet是/contentspace/faces/jsp/login.jsp ，它应该是null引用异常。 只有在为Web应用程序启用GET过滤时才需要此例外。 您的应用程序可以指定是否允许null引用。 请参阅中的“防止跨站点请求伪造攻击” [AEM表单的强化和安全性](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**允许的反向链接异常：** “允许的引用异常”是允许的引用列表的子列表，请求将从该子列表中阻止。 允许的“引用异常”是特定于Web应用程序的。 如果不允许允许的反向链接的子集调用特定的Web应用程序，则可以通过允许的反向链接例外阻止列表反向链接。 在应用程序的web.xml文件中指定了允许的引用程序异常。 (请参阅“帮助和Tutorials”页上的“强化AEM表单和增强其安全性”中的“防止跨站点请求伪造攻击”。)

## 允许的反向链接的工作方式 {#how-allowed-referers-work}

AEM forms提供了引用筛选功能，有助于防止CSRF攻击。 以下是引用筛选的工作方式：

1. 表单服务器会检查用于调用的HTTP方法：

   * 如果POST，表单服务器将执行引用头检查。
   * 如果是GET，则表单服务器将绕过引用检查，除非CSRF_CHECK_GETS设置为true，在这种情况下，它将执行引用标头检查。 CSRF_CHECK_GETS是在应用程序的web.xml文件中指定的。 （请参阅中的“防止跨站点请求伪造攻击”） [强化和安全指南](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. 表单服务器检查请求的URI是否已列入允许列表：

   * 列入允许列表如果URI，则服务器传递请求。
   * 如果请求的URI未列入允许列表，则服务器将检索请求的引用服务器。

1. 如果请求中存在引用，则服务器会检查它是否为允许的引用。 如果允许，服务器会检查引用异常：

   * 如果出现异常，则请求被阻止。
   * 如果不是例外，则会传递请求。

1. 如果请求中没有引用，则服务器会检查是否允许使用null引用。

   * 如果允许null引用，则会传递请求。
   * 如果不允许使用null引用，则服务器会检查请求的URI是否是null引用的异常，并相应地处理请求。

## 配置允许的引用 {#configure-allowed-referers}

运行Configuration Manager时，默认主机和IP地址或表单服务器将添加到允许引用程序列表中。 您可以在管理控制台中编辑此列表。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“配置允许的引用URL”。允许的反向链接列表将显示在页面底部。
1. 要添加允许的反向链接，请执行以下操作：

   * 在“允许的反向链接”框中键入主机名或IP地址。 要一次添加多个允许的引用，请在新行上键入每个主机名或IP地址。
   * 在“HTTP端口”和“HTTPS端口”框中，指定允许使用HTTP和/或HTTPS的端口。 如果将这些框留空，则使用默认端口（HTTP使用端口80，HTTPS使用端口443）。 如果您输入 `0` （零）在框中，该服务器上的所有端口都处于启用状态。 您还可以输入特定的端口号，以仅启用该端口。
   * 单击添加。

1. 要从“允许的反向链接”列表中删除条目，请从列表中选择该条目，然后单击“删除”。

   如果“允许的引用者列表”为空，则CSRF功能将停止工作，系统变得不安全。

1. 更改允许引用程序列表后，重新启动AEM表单服务器。
