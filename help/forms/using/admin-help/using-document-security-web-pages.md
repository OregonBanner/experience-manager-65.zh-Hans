---
title: 使用Document Security网页
description: 了解如何登录、导航和使用Document Security网页。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# 使用Document Security网页 {#using-the-document-security-webpages}

用户和管理员使用Document Security网页创建和管理策略，管理受策略保护的文档，以及监控与受策略保护文档关联的事件。 管理员还可以使用这些网页创建策略集并指定策略集协调员，配置Document Security默认设置，管理受邀的用户注册和帐户，以及监视和管理服务器、策略、用户和文档相关的事件。

>[!NOTE]
>
>您还可以使用用户登录帐户通过Acrobat和其他客户端应用程序登录到Document Security。 (请参阅 [设置从客户端应用程序访问Document Security](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

要打开网页，您需要浏览器以及URL和您的登录信息，以便Document Security。 用户的URL与管理员的URL不同。

由于Document Security引用您组织的现有目录来获取用户信息，因此Document Security登录信息可能与您用于登录网络和其他应用程序的信息相同。 有关帐户信息，请咨询您的系统管理员或管理员。

要以管理员身份登录，您需要为您分配管理员角色。 您可以使用安装过程中创建的默认超级管理员帐户。

## 登录网页 {#log-in-to-the-web-pages}

要使用浏览器登录到网页，您需要具有Document Security URL和帐户。 用户的URL与管理员的URL不同。 管理员还可以登录到用户页面以创建策略。

如果您有权访问多个document security安装，则需要要访问的document security实例的URL。 如果您没有此信息，请咨询您的管理员。 用户页面的默认URL为 `https://[host]:[port]/edc`. 在某些情况下，可能不需要端口号。 请咨询您的管理员以了解详细信息。

管理员的默认URL为 `https://[host]:[port]/adminui`.

对于管理员，会在安装期间创建默认的超级管理员帐户。 首次安装Document Security时，您可以使用此帐户登录。

>[!NOTE]
>
>您还可以从Acrobat和其他客户端应用程序访问网页。 有关详细信息，请参阅Acrobat帮助或相应的Acrobat Reader DC扩展帮助。

1. 在浏览器中键入URL：

   文档安全URL： `https://[host]:[port]/edc`

   或管理控制台URL： `https://[host]:[port]/adminui`

1. 在登录窗口中，键入用户名和密码，然后单击“确定”。
1. 在Administration Console中，单击服务>文档安全。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮（如“返回”按钮、“刷新”按钮以及“后退”和“前进”箭头），因为此操作可能会导致出现不需要的数据捕获和数据显示问题。

## 导航网页 {#navigating-the-web-pages}

登录用户网页时，您将看到指向策略、文档和事件用户页面的链接。

在登录到管理控制台并导航到Document Security主页时，您还可能会看到一个或多个其他链接，一个用于“配置”页面，另一个用于“受邀和本地用户”页面。 只有在启用了受邀用户注册的情况下，才会显示“受邀用户和本地用户”页面。

使用这些链接可访问各种页面，您可以在其中创建和管理策略及受策略保护的文档。

**显示页面**

1. 单击页面的名称，如单击策略。

**返回上一页**

1. 单击要返回到的页面的顶部导航链接。

**刷新页面上的数据列表**

1. 在主页上，单击要刷新页面的链接。

>[!NOTE]
>
>处理网页时，请避免使用浏览器按钮（如“返回”按钮、“刷新”按钮以及“后退”和“前进”箭头），因为此操作可能会导致不必要的数据捕获和数据显示问题。

## 设置从客户端应用程序访问Document Security {#setting-up-access-to-document-security-from-client-applications}

客户端应用程序必须设置为连接到Document Security以保护文档，打开受策略保护的文档，并连接到Document Security网页。 请参阅 *Acrobat帮助* 或相应的 *RightsManagementExtension帮助* 有关在客户端应用程序中配置连接的信息。

文档安全通过安全套接字层(SSL)访问。 将网站的证书安装到您的证书存储中，以便您可以通过客户端应用程序访问Document Security。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

这些说明特定于Internet Explorer，但您可以使用任何受支持的Web浏览器安装证书。 有关详细信息，请参阅浏览器的帮助。

**使用Internet Explorer安装服务器证书**

1. 打开Web浏览器，并在“地址”框中键入文档安全的基本URL。 例如，键入 `https://[host]:[port]`. 出现“Security Alert（安全警报）”对话框。
1. 单击查看证书，然后单击安装证书并选择默认安装选项。 证书需要安装在受信任的根证书颁发机构中。
1. 关闭浏览器会话。
1. 打开另一个浏览器窗口，然后在地址框中键入相同的URL。 不应出现“安全警报”对话框。 此测试用于确认证书是否正确安装。

## 注销网页 {#log-out-of-the-web-pages}

使用完网页后注销，这样您便可以安全地使用Web浏览器进行其他操作。 根据Document Security的配置方式，您可能需要关闭浏览器才能完全注销。

1. 单击页面右上角的注销。
1. 如果“注销”页上显示一条消息，请关闭浏览器窗口以完全注销。 否则，您可以继续将浏览器用于其他目的。
