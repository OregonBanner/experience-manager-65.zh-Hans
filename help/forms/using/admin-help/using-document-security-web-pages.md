---
title: 使用Document Security网页
seo-title: 使用Document Security网页
description: 了解如何登录、导航和使用Document Security网页。
seo-description: 了解如何登录、导航和使用Document Security网页。
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用Document Security网页 {#using-the-document-security-webpages}

用户和管理员使用Document Security网页创建和管理策略，管理受策略保护的文档，以及监视与受策略保护的文档相关的事件。 管理员还使用网页创建策略集和指定策略集协调员，配置文档安全性默认设置，管理受邀用户注册和帐户，以及监视和管理服务器、策略、用户和文档相关事件。

>[!NOTE]
>
>您还可以使用用户登录帐户通过Acrobat和其他客户端应用程序登录到文档安全性。 (请参 [阅从客户端应用程序设置对文档安全性的访问](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)。)

要打开网页，您需要浏览器、URL和登录信息才能确保文档安全。 用户的URL与管理员的URL不同。

由于文档安全性引用组织的现有目录作为用户信息的参考，因此您的文档安全登录信息可能与您登录网络和其他应用程序时所用的信息相同。 有关帐户信息，请咨询系统管理员或管理员。

要以管理员身份登录，您需要为您分配管理员角色。 您可以使用在安装过程中创建的默认超级管理员帐户。

## 登录网页 {#log-in-to-the-web-pages}

要使用浏览器登录网页，您需要文档安全URL和帐户。 用户的URL与管理员的URL不同。 管理员还可以登录到用户页面以创建策略。

如果您有权访问多个文档安全安装，则需要要访问的文档安全实例的URL。 如果您没有此信息，请咨询您的管理员。 用户页面的默认URL是https://*[host]*:*[port]*/edc。 在某些情况下，端口号可能不是必需的。 请向管理员咨询详细信息。

管理员的默认URL为https://*[host]*:*[port]*/adminui。

对于管理员，将在安装过程中创建默认的超级管理员帐户。 首次安装文档安全性时，可使用此帐户登录。

>[!NOTE]
>
>您还可以从Acrobat和其他客户端应用程序访问网页。 有关详细信息，请参阅Acrobat帮助或相应的Acrobat Reader DC扩展帮助。

1. 在浏览器中键入URL:

   文档安全URL: `https://`*[主机&#x200B;]*`:`*[端口]*`/edc`

   或管理控制台URL: `https://`*[主机&#x200B;]*`:`*[端口]*`/adminui`

1. 在登录窗口中，键入您的用户名和密码，然后单击“确定”。
1. 在管理控制台中，单击“服务”>“文档安全性”。

>[!NOTE]
>
>使用网页时，请避免使用浏览器按钮，如后退按钮、刷新按钮以及后退和前进箭头，因为此操作可能会导致不需要的数据捕获和数据显示问题。

## 导航网页 {#navigating-the-web-pages}

登录到用户网页时，您将看到指向“策略”、“文档”和“事件”用户页的链接。

当您登录到管理控制台并导航到文档安全主页时，您还可能会看到一个或两个其他链接，一个用于“配置”页，一个用于“已邀请”和“本地用户”页。 仅当已邀请的用户注册处于启用状态时，才会显示“已邀请的用户”和“本地用户”页面。

使用这些链接可访问各个页面，在这些页面中可以创建和管理受策略保护的文档。

**显示页面**

1. 单击页面名称；例如，单击“策略”。

**返回上一页**

1. 单击页面顶部要返回到的页面的导航链接。

**刷新页面上的数据列表**

1. 在主页上，单击要刷新的页面的链接。

>[!NOTE]
>
>使用网页时，请避免使用浏览器按钮，如后退按钮、刷新按钮以及后退和前进箭头，因为此操作可能会导致不需要的数据捕获和数据显示问题。

## 从客户端应用程序设置对文档安全性的访问 {#setting-up-access-to-document-security-from-client-applications}

必须设置客户端应用程序才能连接到文档安全性以保护文档、打开受策略保护的文档并连接到文档安全网页。 有关在 *客户端应用程序内配置连接的信息* ，请参阅Acrobat帮助或相应的 ** RightsManagementExtension帮助。

文档安全性可通过安全套接字层(SSL)访问。 您必须在证书存储区中安装网站的证书，这样您就可以通过客户端应用程序访问文档安全性。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

这些说明特定于Internet Explorer，但您可以使用任何支持的Web浏览器安装证书。 有关详细信息，请参阅浏览器帮助。

**使用Internet explorer安装服务器证书**

1. 打开Web浏览器，在“地址”框中键入文档安全的基本URL。 例如，键入 `https://[host]:[port]`。 将显示“安全警报”对话框。
1. 单击“查看证书”，然后单击“安装证书”，然后选择安装的默认值。 该证书需要安装在Trusted Root Certification Authoritions中。
1. 关闭浏览器会话。
1. 打开另一个浏览器窗口，在“地址”框中键入相同的URL。 不应显示安全警报对话框。 此测试会确认证书安装正确。

## 注销网页 {#log-out-of-the-web-pages}

使用完网页后注销，这样您就可以安全地将Web浏览器用于其他用途。 根据文档安全性的配置方式，您可能需要关闭浏览器才能完全注销。

1. 在页面的右上角，单击“注销”。
1. 如果注销页面上显示一条消息，请关闭浏览器窗口以完全注销。 否则，您可以继续将浏览器用于其他用途。

