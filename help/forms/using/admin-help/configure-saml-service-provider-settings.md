---
title: 配置SAML服务提供者设置
seo-title: 配置SAML服务提供者设置
description: 您可以配置SAML服务提供者设置，以允许用户通过指定的第三方标识提供者(IDP)登录AEM表单并进行身份验证。
seo-description: 您可以配置SAML服务提供者设置，以允许用户通过指定的第三方标识提供者(IDP)登录AEM表单并进行身份验证。
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置SAML服务提供者设置{#configure-saml-service-provider-settings}

安全断言标记语言(SAML)是在为企业或混合域配置授权时可选择的选项之一。 SAML主要用于支持跨多个域的SSO。 将SAML配置为身份验证提供者后，用户将通过指定的第三方标识提供者(IDP)登录并验证到AEM表单。

有关SAML的说明，请参 [阅安全断言标记语言(SAML)V2.0技术概述](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“SAML服务提供者设置”。
1. 在“服务提供者实体ID”框中，键入一个唯一ID以用作AEM表单服务提供者实施的标识符。 在配置IDP时，您还可以指定此唯一ID(例如， `um.lc.com`)。您还可以使用用于访问AEM表单的URL(例如， `https://AEMformsserver`)。
1. 在“服务提供商基本URL”框中，键入表单服务器的基本URL(例如， `https://AEMformsserver:8080`)。
1. （可选）要使AEM表单能向IDP发送已签名的身份验证请求，请执行以下任务：

   * 使用Trust Manager导入PKCS #12格式的凭据，并将“文档签名凭证”选为“信任存储类型”。 (请参阅 [管理本地凭据](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)。)
   * 在“服务提供商凭据密钥别名”列表中，选择您在信任存储中分配给凭据的别名。
   * 单击“导出”将URL内容保存到文件中，然后将该文件导入IDP。

1. （可选）在“服务提供商名称ID策略”列表中，选择IDP用来在SAML断言中标识用户的名称格式。 这些选项包括“未指定”、“电子邮件”和“Windows域限定名称”。

   >[!NOTE]
   >
   >名称格式不区分大小写。

1. （可选）选择“为本地用户启用身份验证提示”。 选择此选项后，用户将看到两个链接：

   * 指向第三方SAML标识提供者的登录页的链接，在此链接中，属于企业域的用户可以进行身份验证。
   * 指向AEM表单登录页的链接，在该页面中，属于本地域的用户可以进行身份验证。
   如果未选择此选项，则用户将直接进入第三方SAML标识提供者的登录页面，在该页面中，属于企业域的用户可以进行身份验证。

1. （可选）选择“启用对象绑定”以启用对象绑定支持。 默认情况下，POST绑定与SAML一起使用。 但是，如果您已配置“对象绑定”，请选择此选项。 选择此选项后，实际的用户断言不会通过浏览器请求传递。 相反，传递指向断言的指针并使用后端Web服务调用检索断言。
1. （可选）选择“启用重定向绑定”以支持使用重定向的SAML绑定。
1. （可选）在自定义属性中，指定其他属性。 其他属性是name=value对，用新行分隔。

   * 您可以配置AEM表单以在与第三方断言的有效期匹配的有效期内发布SAML断言。 要遵守第三方SAML断言超时，请在“自定义属性”中添加以下行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定义属性以使用RelayState确定成功验证后用户将被重定向到的URL。

      `saml.sp.use.relaystate=true`

   * 添加以下自定义属性以配置自定义Java服务器页(JSP)的URL，该URL将用于呈现标识提供者的注册列表。 如果尚未部署自定义Web应用程序，则它将使用默认的“用户管理”页面来呈现列表。
   `saml.sp.discovery.url=/custom/custom.jsp`

1. 单击保存。

