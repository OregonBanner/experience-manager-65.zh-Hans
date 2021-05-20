---
title: 配置SAML服务提供程序设置
seo-title: 配置SAML服务提供程序设置
description: 您可以配置SAML服务提供程序设置，以允许用户通过指定的第三方身份提供程序(IDP)登录AEM表单并对其进行身份验证。
seo-description: 您可以配置SAML服务提供程序设置，以允许用户通过指定的第三方身份提供程序(IDP)登录AEM表单并对其进行身份验证。
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# 配置SAML服务提供程序设置{#configure-saml-service-provider-settings}

安全断言标记语言(SAML)是在为企业域或混合域配置授权时可以选择的选项之一。 SAML主要用于支持跨多个域的单点登录。 将SAML配置为身份验证提供程序后，用户将通过指定的第三方身份提供程序(IDP)登录AEM表单并对其进行身份验证。

有关SAML的说明，请参阅[安全断言标记语言(SAML)V2.0技术概述](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)。

1. 在管理控制台中，单击“设置”>“用户管理”>“配置”>“SAML服务提供程序设置”。
1. 在“服务提供商实体ID”框中，键入一个唯一ID，以用作AEM表单服务提供商实施的标识符。 在配置IDP时，您还可以指定此唯一ID（例如，`um.lc.com`。） 您还可以使用用于访问AEM表单的URL（例如，`https://AEMformsserver`）。
1. 在“服务提供商基本URL”框中，键入表单服务器的基本URL（例如，`https://AEMformsserver:8080`）。
1. （可选）要启用AEM表单向IDP发送签名身份验证请求，请执行以下任务：

   * 使用信任管理器导入PKCS #12格式的凭据，并选择文档签名凭据作为信任存储类型。 （请参阅[管理本地凭据](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)。）
   * 在“服务提供商凭据密钥别名”列表中，选择您在信任存储中分配给凭据的别名。
   * 单击导出将URL内容保存到文件，然后将该文件导入您的IDP。

1. （可选）在“服务提供程序名称ID策略”列表中，选择IDP在SAML断言中用于标识用户的名称格式。 选项包括“未指定”、“电子邮件”和“Windows域限定名称”。

   >[!NOTE]
   >
   >名称格式不区分大小写。

1. （可选）选择为本地用户启用身份验证提示。 选择此选项后，用户将看到两个链接：

   * 指向第三方SAML身份提供程序登录页面的链接，属于企业域的用户可以在该页面中进行身份验证。
   * 指向AEM表单登录页面的链接，属于本地域的用户可以在该页面中进行身份验证。

   未选择此选项时，用户将直接转到第三方SAML身份提供程序的登录页面，在该页面中，属于企业域的用户可以进行身份验证。

1. （可选）选择“启用对象绑定”以启用对象绑定支持。 默认情况下，POST绑定与SAML一起使用。 但是，如果已配置“对象绑定”，请选择此选项。 选择此选项后，实际的用户断言不会通过浏览器请求传递。 而是会传递指向断言的指针，并使用后端Web服务调用来检索断言。
1. （可选）选择启用重新定向绑定以支持使用重定向的SAML绑定。
1. （可选）在自定义属性中，指定其他属性。 其他属性是名称=值对，用新行分隔。

   * 您可以将AEM表单配置为在与第三方断言的有效期匹配的有效期内发出SAML断言。 要遵循第三方SAML断言超时，请在“自定义属性”中添加以下行：

      `saml.sp.honour.idp.assertion.expiry=true`

   * 添加以下自定义属性，以便使用RelayState确定成功身份验证后用户将被重定向的URL。

      `saml.sp.use.relaystate=true`

   * 添加以下自定义属性以配置自定义Java服务器页(JSP)的URL，该URL将用于呈现身份提供程序的注册列表。 如果您尚未部署自定义Web应用程序，它将使用默认的“用户管理”页面来呈现列表。

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 单击保存。
