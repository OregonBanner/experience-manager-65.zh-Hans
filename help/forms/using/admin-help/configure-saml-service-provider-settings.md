---
title: 配置SAML服务提供程序设置
seo-title: Configure SAML service provider settings
description: 您可以配置SAML服务提供程序设置，以允许用户通过指定的第三方身份提供程序(IDP)登录并验证AEM表单。
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# 配置SAML服务提供程序设置{#configure-saml-service-provider-settings}

安全断言标记语言(SAML)是在配置企业域或混合域的授权时可以选择的一个选项。 SAML主要用于支持跨多个域的SSO。 将SAML配置为身份验证提供程序时，用户通过指定的第三方身份提供程序(IDP)登录并验证AEM Forms。

有关SAML的说明，请参阅 [安全声明标记语言(SAML) V2.0技术概述](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. 在管理控制台中，单击设置>用户管理>配置> SAML服务提供程序设置。
1. 在“服务提供者实体ID”框中，键入要用作AEM Forms服务提供者实现的标识符的唯一ID。 您还可以在配置IDP时指定此唯一ID(例如， `um.lc.com`.) 您还可以使用用于访问AEM表单的URL(例如， `https://AEMformsserver`)。
1. 在服务提供者基本URL框中，键入表单服务器的基本URL(例如， `https://AEMformsserver:8080`)。
1. （可选）要使AEM Forms能够向IDP发送已签名的身份验证请求，请执行以下任务：

   * 使用信任管理器导入PKCS #12格式的凭据，并选择文档签名凭据作为信任存储类型。 (请参阅 [管理本地凭据](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 在“服务提供者凭据密钥别名”列表中，选择在信任存储区中为凭据分配的别名。
   * 单击“导出”将URL内容保存到文件中，然后将该文件导入IDP。

1. （可选）在服务提供者名称ID策略列表中，选择IDP在SAML断言中用于标识用户的名称格式。 选项包括“未指定”、“电子邮件”和“Windows域限定名”。

   >[!NOTE]
   >
   >名称格式不区分大小写。

1. （可选）选择“为本地用户启用身份验证提示”。 选中此选项后，用户将看到两个链接：

   * 指向第三方SAML身份提供程序的登录页的链接，在该链接中，属于企业域的用户可以进行身份验证。
   * AEM forms登录页面的链接，本地域用户可以在其中进行身份验证。

   如果未选择此选项，则用户将直接转到第三方SAML身份提供程序的登录页面，在该页面中，属于企业域的用户可以进行身份验证。

1. （可选）选择启用工件绑定以启用工件绑定支持。 默认情况下，POST绑定会与SAML一起使用。 但是，如果已配置工件绑定，请选择此选项。 如果选择该选项，则不会通过浏览器请求传递实际用户断言。 而是传递指向断言的指针，并使用后端Web服务调用检索断言。
1. （可选）选择启用重定向绑定以支持使用重定向的SAML绑定。
1. （可选）在自定义属性中，指定其他属性。 其他属性为名称=值对，用新行分隔。

   * 您可以配置AEM表单以发出与第三方声明的有效期相匹配的有效期的SAML声明。 要遵循第三方SAML断言超时，请在自定义属性中添加以下行：

     `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定义属性以使用RelayState确定在成功身份验证后用户将被重定向到的URL。

     `saml.sp.use.relaystate=true`

   * 添加以下自定义属性以配置自定义Java Server Pages (JSP)的URL，该URL用于呈现已注册的身份提供程序列表。 如果您尚未部署自定义Web应用程序，它将使用默认的“用户管理”页面来呈现列表。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 单击保存。
