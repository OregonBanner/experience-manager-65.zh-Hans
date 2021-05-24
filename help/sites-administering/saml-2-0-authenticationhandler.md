---
title: SAML 2.0 身份验证处理程序
seo-title: SAML 2.0 身份验证处理程序
description: 了解AEM中的SAML 2.0身份验证处理程序。
seo-description: 了解AEM中的SAML 2.0身份验证处理程序。
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---

# SAML 2.0 身份验证处理程序{#saml-authentication-handler}

AEM随[SAML](http://saml.xml.org/saml-specifications)身份验证处理程序一起提供。 此处理程序支持使用`HTTP POST`绑定的[SAML](http://saml.xml.org/saml-specifications) 2.0身份验证请求协议（Web-SSO配置文件）。

它支持：

* 消息的签名和加密
* 自动创建用户
* 将组同步到AEM中的现有组
* 服务提供商和身份提供商启动了身份验证

此处理程序将加密的SAML响应消息存储在用户节点(`usernode/samlResponse`)中，以便于与第三方服务提供商进行通信。

>[!NOTE]
>
>请参阅[AEM与SAML集成的演示](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)。
>
>要阅读端到端社区文章，请单击：[将SAML与Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html)集成。

## 配置SAML 2.0身份验证处理程序{#configuring-the-saml-authentication-handler}

[Web控制台](/help/sites-deploying/configuring-osgi.md)提供对[SAML](http://saml.xml.org/saml-specifications) 2.0身份验证处理程序配置(称为&#x200B;**AdobeGranite SAML 2.0身份验证处理程序**)的访问。 可以设置以下属性。

>[!NOTE]
>
>默认情况下，SAML 2.0身份验证处理程序处于禁用状态。 要启用处理程序，必须至少设置以下属性之一：
>
>* 身份提供程序POSTURL。
>* 服务提供商实体ID。

>



>[!NOTE]
>
>SAML断言已签名，并且可以选择进行加密。 要使此功能正常工作，您必须在TrustStore中至少提供身份提供商的公共证书。 有关更多信息，请参阅[将IdP证书添加到TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore)部分。

**** Sling应使用此身份验证处理程序的PathRepository路径。如果为空，则将禁用身份验证处理程序。

**服务** 排名OSGi框架服务排名值，指示调用此服务的顺序。这是一个整数值，其中较高的值指定较高的优先级。

**IDP证** 书别名全局信任存储中IdP证书的别名。如果此属性为空，则禁用身份验证处理程序。 有关如何设置IdP证书的信息，请参阅下面的“将IdP证书添加到AEM TrustStore”一章。

**应将** SAML身份验证请求发送到的IDP的身份提供程序URL。如果此属性为空，则禁用身份验证处理程序。

>[!CAUTION]
>
>必须将身份提供程序主机名添加到&#x200B;**Apache Sling反向链接过滤器** OSGi配置中。 有关更多信息，请参阅[Web控制台](/help/sites-deploying/configuring-osgi.md)部分。

**服务提供商实** 体IDID，用标识提供商唯一标识此服务提供商。如果此属性为空，则禁用身份验证处理程序。

**默认重** 定向成功身份验证后要重定向到的默认位置。

>[!NOTE]
>
>仅当未设置`request-path` Cookie时，才使用此位置。 如果您请求配置路径下的任何页面时没有有效的登录令牌，则请求的路径将存储在Cookie中
>并且，成功身份验证后，浏览器将再次重定向到此位置。

**用户ID属** 性包含用于在CRX存储库中验证和创建用户的用户ID的属性的名称。

>[!NOTE]
>
>用户ID不会从SAML断言的`saml:Subject`节点获取，而是从此`saml:Attribute`获取。

**使用加** 密此身份验证处理程序是否需要加密的SAML断言。

**自动创建CRX** 用户成功身份验证后，是否在存储库中自动创建非现有用户。

>[!CAUTION]
>
>如果禁用了CRX用户的自动创建，则必须手动创建用户。

**添加到** 组成功身份验证后是否应自动将用户添加到CRX组。

**群组** 成员资格saml:Attribute的名称，其中包含应将此用户添加到的CRX群组列表。

## 将IdP证书添加到AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML断言已签名，并且可以选择进行加密。 要使其正常工作，您必须在存储库中至少提供IdP的公共证书。 为此，您需要：

1. 转到&#x200B;*http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按&#x200B;**[!UICONTROL Create TrustStore链接]**
1. 输入TrustStore的密码，然后按&#x200B;**[!UICONTROL Save]**。
1. 单击&#x200B;**[!UICONTROL 管理TrustStore]**。
1. 上载IdP证书。
1. 请注意证书别名。 以下示例中的别名为&#x200B;**[!UICONTROL admin#1436172864930]**。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 将服务提供商密钥和证书链添加到AEM密钥库{#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>必须执行以下步骤，否则将引发以下异常：`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 转到：[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 编辑`authentication-service`用户。
1. 单击&#x200B;**帐户设置**&#x200B;下的&#x200B;**创建KeyStore**&#x200B;以创建KeyStore。

>[!NOTE]
>
>只有在处理程序应能对消息进行签名或解密时，才需要执行以下步骤。

1. 单击&#x200B;**选择私钥文件**&#x200B;上传私钥文件。 密钥要求采用PKCS#8格式，且采用DER编码。
1. 单击&#x200B;**选择证书链文件**&#x200B;上传证书文件。
1. 分配别名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 为SAML {#configure-a-logger-for-saml}配置日志记录器

您可以设置一个记录器，以调试因错误配置SAML而可能引发的任何问题。 您可以通过以下方式执行此操作：

1. 转到Web控制台，位于&#x200B;*http://localhost:4502/system/console/configMgr*
1. 搜索并单击名为&#x200B;**Apache Sling日志记录记录器配置**&#x200B;的条目
1. 使用以下配置创建日志记录器：

   * **日志级别：** 调试
   * **日志文件：** logs/saml.log
   * **记录器：** com.adobe.granite.auth.saml
