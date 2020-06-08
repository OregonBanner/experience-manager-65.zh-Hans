---
title: SAML 2.0身份验证处理程序
seo-title: SAML 2.0身份验证处理程序
description: 了解AEM中的SAML 2.0身份验证处理程序。
seo-description: 了解AEM中的SAML 2.0身份验证处理程序。
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: d559a15e3c1c65c39e38935691835146f54a356e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# SAML 2.0身份验证处理程序{#saml-authentication-handler}

AEM随SAML身份验 [证处理](http://saml.xml.org/saml-specifications) 程序一起提供。 此处理函数支持 [使用](http://saml.xml.org/saml-specifications) 绑定的SAML 2.0身份验证请求协议(Web-SSO `HTTP POST` 用户档案)。

它支持：

* 消息签名和加密
* 自动创建用户
* 将组同步到AEM中的现有组
* 服务提供商和标识提供者启动的身份验证

此处理函数将加密的SAML响应消息存储在用户节点() `usernode/samlResponse`中，以便与第三方服务提供商进行通信。

>[!NOTE]
>
>查 [看AEM和SAML集成的演示](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)。
>
>要阅读端到端社区文章，请单击： [将SAML与Adobe Experience Manager集成](https://helpx.adobe.com/experience-manager/using/aem63_saml.html)。

## 配置SAML 2.0身份验证处理程序 {#configuring-the-saml-authentication-handler}

Web控 [制台](/help/sites-deploying/configuring-osgi.md) ，提供对称为Adobe Granite SAML 2.0身份验证处理程 [序配置的访问权](http://saml.xml.org/saml-specifications)****。 可以设置以下属性。

>[!NOTE]
>
>默认情况下，SAML 2.0身份验证处理程序处于禁用状态。 要启用该处理函数，必须至少设置以下属性之一：
>
>* 标识提供者POST URL。
>* 服务提供商实体ID。

>



>[!NOTE]
>
>SAML声明已签名，并可以选择进行加密。 为使此工作正常，您必须至少在TrustStore中提供身份提供者的公共证书。 有关 [详细信息，请参阅将IdP证书添加到](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) TrustStore部分。

**路径** Sling应使用此身份验证处理程序的存储库路径。 如果此为空，则将禁用身份验证处理程序。

**服务排名** OSGi框架服务排名值用于指示调用此服务的顺序。 这是一个整数值，其中值越高，表示优先级越高。

**IDP证书别名** 全局信任存储中IdP证书的别名。 如果此属性为空，则会禁用身份验证处理程序。 有关如何设置IdP证书，请参阅下面的“将IdP证书添加到AEM TrustStore”一章。

**SAML身份验证** 请求应发送到的IDP的标识提供者URL。 如果此属性为空，则会禁用身份验证处理程序。

>[!CAUTION]
>
>必须将标识提供者主机名添加 **到Apache Sling推荐人过滤器** OSGi配置。 有关详细 [信息，请参](/help/sites-deploying/configuring-osgi.md) 阅Web控制台部分。

**服务提供商实体** ID，它通过标识提供者唯一标识此服务提供商。 如果此属性为空，则会禁用身份验证处理程序。

**默认重定向** ：成功验证后要重定向到的默认位置。

>[!NOTE]
>
>此位置仅在未设置 `request-path` Cookie时使用。 如果您请求配置路径下的任何页面时没有有效的登录令牌，则请求的路径将存储在cookie中
>并且，成功验证后，浏览器将再次重定向到此位置。

**User-ID Attribute** 包含用于在CRX存储库中验证和创建用户的用户ID的属性的名称。

>[!NOTE]
>
>用户ID不会从SAML断言的节 `saml:Subject` 点中获取，而是从中获取 `saml:Attribute`。

**使用加密** 无论此身份验证处理程序是否需要加密的SAML声明。

**自动创建CRX用户** 成功验证后是否自动在存储库中创建非现有用户。

>[!CAUTION]
>
>如果禁用了CRX用户的自动创建，则用户必须手动创建。

**添加到组** 成功验证后是否应将用户自动添加到CRX组。

**组成员** ：包含此用户应添加到的CRX组列表的saml：属性的名称。

## 将IdP证书添加到AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML声明已签名，并可以选择进行加密。 要使此功能正常工作，您必须至少在存储库中提供IdP的公共证书。 为此，您需要：

1. 转到 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按“创建 **[!UICONTROL TrustStore”链接]**
1. 输入TrustStore的口令，然后按“保 **[!UICONTROL 存”]**。
1. 单击“管 **[!UICONTROL 理信任商店]**”。
1. 上传IdP证书。
1. 记下证书别名。 别名 **[!UICONTROL 为admin#1436172864930]** ，如下例所示。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 将服务提供商密钥和证书链添加到AEM密钥库 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下步骤是必需的，否则将引发以下异常： `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 转到： [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 编辑用 `authentication-service` 户。
1. 单击“帐户设置” **下的“创建** KeyStore **”**&#x200B;创建KeyStore。

>[!NOTE]
>
>仅当处理程序应能对消息进行签名或解密时，才需要以下步骤。

1. 通过单击“选择私钥文件”, **上传私钥文件**。 PKCS#8格式的密钥需要DER编码。
1. 单击“选择证书链文 **件”上载证书文件**。
1. 分配别名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 为SAML配置记录器 {#configure-a-logger-for-saml}

您可以设置记录器以调试因错误配置SAML而可能出现的任何问题。 可通过以下方式执行此操作：

1. 转到Web控制台，网址为 *http://localhost:4502/system/console/configMgr*
1. 搜索并单击名为Apache Sling日志记录 **器配置的条目**
1. 使用以下配置创建记录器：

   * **日志级别：** 调试
   * **日志文件：** logs/saml.log
   * **记录器：** com.adobe.granite.auth.saml

