---
title: 使用文档安全网页
seo-title: 使用文档安全网页
description: 了解如何登录、导航和使用文档安全网页。
seo-description: 了解如何登录、导航和使用文档安全网页。
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# 使用文档安全网页{#using-the-document-security-webpages}

用户和管理员使用文档安全网页创建和管理策略，管理受策略保护的文档，并监视与受策略保护的文档关联的事件。 管理员还使用网页创建策略集并指定策略集协调员、配置文档安全默认设置、管理受邀用户注册和帐户以及监视和管理服务器、策略、用户和文档相关事件。

>[!NOTE]
>
>您还可以使用用户登录帐户通过Acrobat和其他客户端应用程序登录文档安全性。 (请参阅[设置从客户端应用程序访问文档安全性](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)。)

要打开网页，您需要浏览器、URL和登录信息才能确保文档安全。 用户的URL与管理员的URL不同。

由于文档安全性引用您组织的现有目录以获取用户信息，因此文档安全登录信息可能与您用于登录网络和其他应用程序的信息相同。 有关帐户信息，请咨询系统管理员或管理员。

要以管理员身份登录，您需要为您分配管理员角色。 您可以使用在安装过程中创建的默认超级管理员帐户。

## 登录网页{#log-in-to-the-web-pages}

要使用浏览器登录网页，您需要文档安全URL和帐户。 用户的URL与管理员的URL不同。 管理员还可以登录用户页以创建策略。

如果您有权访问多个文档安全安装，则需要要访问的文档安全实例的URL。 如果您没有此信息，请咨询您的管理员。 用户页面的默认URL为`https://[host]:[port]/edc`。 在某些情况下，可能不需要端口号。 请向管理员咨询详细信息。

管理员的默认URL为`https://[host]:[port]/adminui`。

对于管理员，将在安装过程中创建默认的超级管理员帐户。 首次安装文档安全时，可使用此帐户登录。

>[!NOTE]
>
>您还可以从Acrobat和其他客户端应用程序访问网页。 有关详细信息，请参阅Acrobat帮助或相应的Acrobat Reader DC扩展帮助。

1. 在浏览器中键入URL:

   文档安全URL:`https://[host]:[port]/edc`

   或管理控制台URL:`https://[host]:[port]/adminui`

1. 在登录窗口中，键入您的用户名和密码，然后单击“确定”。
1. 在管理控制台中，单击“服务”>“文档安全性”。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮，如后退按钮、刷新按钮以及后退和前进箭头，因为此操作可能会导致不需要的数据捕获和数据显示问题。

## 导航网页{#navigating-the-web-pages}

登录用户网页时，您将看到指向策略、文档和事件用户页的链接。

当您登录到管理控制台并导航到文档安全主页时，您还可能会看到一个或两个其他链接，一个用于“配置”页，一个用于“已邀请”和“本地用户”页。 仅当启用了已邀请的用户注册时，才会显示“已邀请的用户”和“本地用户”页面。

使用这些链接可访问各个页面，在这些页面中可创建和管理受策略保护的文档。

**显示页面**

1. 单击页面名称；如单击“策略”。

**返回上一页**

1. 单击要返回的页面顶部的导航链接。

**刷新页面上的数据列表**

1. 在主页上，单击要刷新的页面的链接。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮，如后退按钮、刷新按钮以及后退和前进箭头，因为此操作可能会造成不需要的数据捕获和数据显示问题。

## 设置从客户端应用程序{#setting-up-access-to-document-security-from-client-applications}访问文档安全

必须设置客户端应用程序以连接到文档安全以保护文档、打开受策略保护的文档并连接到文档安全网页。 有关在客户端应用程序中配置连接的信息，请参见&#x200B;*Acrobat帮助*&#x200B;或相应的&#x200B;*RightsManagementExtension帮助*。

文档安全性通过安全套接字层(SSL)进行访问。 必须在证书存储中安装网站的证书，以便通过客户端应用程序访问文档安全性。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

这些说明特定于Internet Explorer，但您可以使用任何支持的Web浏览器安装证书。 有关详细信息，请参阅浏览器帮助。

**使用Internet Explorer安装服务器证书**

1. 打开Web浏览器，在“地址”框中键入文档安全的基本URL。 例如，键入`https://[host]:[port]`。 出现“安全警报”对话框。
1. 单击“视图证书”，然后单击“安装证书”，然后选择默认安装设置。 该证书需要安装在受信任的根证书颁发机构中。
1. 关闭浏览器会话。
1. 打开另一个浏览器窗口，在“地址”框中键入相同的URL。 不应显示安全警报对话框。 此测试会确认证书安装正确。

## 注销网页{#log-out-of-the-web-pages}

使用完网页后注销，这样您就可以安全地将Web浏览器用于其他用途。 根据文档安全性的配置方式，您可能需要关闭浏览器以完全注销。

1. 在页面的右上角，单击“注销”。
1. 如果注销页面上显示一条消息，请关闭浏览器窗口以完全注销。 否则，您可以继续将浏览器用于其他用途。

