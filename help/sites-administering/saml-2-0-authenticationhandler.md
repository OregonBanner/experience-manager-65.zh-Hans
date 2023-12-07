---
title: SAML 2.0 身份验证处理程序
description: 了解AEM中的SAML 2.0身份验证处理程序。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# SAML 2.0 身份验证处理程序{#saml-authentication-handler}

AEM附带 [SAML](https://saml.xml.org/saml-specifications) 身份验证处理程序。 此处理程序支持 [SAML](https://saml.xml.org/saml-specifications) 2.0身份验证请求协议（Web-SSO配置文件）使用 `HTTP POST` 绑定。

它支持：

* 消息的签名和加密
* 自动创建用户
* 将组同步到AEM中的现有组
* 服务提供商和身份提供程序启动的身份验证

此处理程序将加密的SAML响应消息存储在用户节点( `usernode/samlResponse`)，以促进与第三方服务提供商的通信。

>[!NOTE]
>
>请参阅 [AEM与SAML集成的演示](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## 配置SAML 2.0身份验证处理程序 {#configuring-the-saml-authentication-handler}

此 [Web控制台](/help/sites-deploying/configuring-osgi.md) 提供对 [SAML](https://saml.xml.org/saml-specifications) 已调用2.0身份验证处理程序配置 **AdobeGranite SAML 2.0身份验证处理程序**. 可以设置以下属性。

>[!NOTE]
>
>默认情况下，SAML 2.0身份验证处理程序处于禁用状态。 至少设置以下属性之一以启用处理程序：
>
>* 身份提供程序POSTURL，或IDP URL。
>* 服务提供商实体ID。
>

>[!NOTE]
>
>SAML断言经过签名并可选择进行加密。 为了使其生效，您必须至少在TrustStore中提供身份提供程序的公共证书。 请参阅 [将IdP证书添加到TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 部分以了解更多信息。

**路径** Sling应使用此身份验证处理程序的存储库路径。 如果此为空，则将禁用身份验证处理程序。

**服务排名** OSGi框架服务排名值，指示调用此服务的顺序。 这是一个整数值，其中较高的值表示较高的优先级。

**IDP证书别名** IdP证书在全局信任库中的别名。 如果此属性为空，则将禁用身份验证处理程序。 有关如何设置证书，请参阅下面的“将IdP证书添加到AEM TrustStore”一章。

**IDP URL** IDP的URL，应将SAML身份验证请求发送到此处。 如果此属性为空，则将禁用身份验证处理程序。

>[!CAUTION]
>
>必须将身份提供程序主机名添加到 **Apache Sling引用过滤器** osgi配置。 请参阅 [Web控制台](/help/sites-deploying/configuring-osgi.md) 部分以了解更多信息。

**服务提供商实体ID** 使用身份提供程序唯一标识此服务提供程序的ID。 如果此属性为空，则将禁用身份验证处理程序。

**默认重定向** 成功验证后重定向到的默认位置。

>[!NOTE]
>
>此位置仅在 `request-path` 未设置Cookie。 如果您在没有有效登录令牌的情况下请求已配置路径下的任何页面，则请求的路径将存储在Cookie中
>成功验证后，浏览器将再次重定向到此位置。

**用户ID属性** 属性的名称，该属性包含用于在CRX存储库中验证和创建用户的用户ID。

>[!NOTE]
>
>用户ID将不会从 `saml:Subject` SAML断言的节点，但来自此 `saml:Attribute`.

**使用加密** 此身份验证处理程序是否需要加密的SAML声明。

**自动创建CRX用户** 在成功验证后是否自动在存储库中创建非现有用户。

>[!CAUTION]
>
>如果禁用了CRX用户的自动创建，则必须手动创建用户。

**添加到组** 在成功验证后，是否应自动将用户添加到CRX组。

**组成员资格** saml：Attribute的名称，其中包含此用户应添加到的CRX组列表。

## 将IdP证书添加到AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

SAML断言经过签名并可选择进行加密。 为了使其生效，您必须在存储库中至少提供IdP的公共证书。 为此，您需要：

1. 转到 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 按 **[!UICONTROL 创建TrustStore链接]**
1. 输入TrustStore的密码，然后按 **[!UICONTROL 保存]**.
1. 单击 **[!UICONTROL 管理Truststore]**.
1. 上传IdP证书。
1. 记下证书别名。 别名为 **[!UICONTROL 管理员#1436172864930]** 如下例所示。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 将服务提供程序密钥和证书链添加到AEM密钥库 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>必须执行以下步骤，否则将引发以下异常： `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 转到： [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 编辑 `authentication-service` 用户。
1. 通过单击 **创建密钥库** 下 **帐户设置**.

>[!NOTE]
>
>仅当处理程序应该能够签名或解密消息时，才需要执行以下步骤。

1. 为AEM创建证书/密钥对。 通过openssl生成它的命令应类似于以下示例：

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. 将密钥转换为PKCS#8格式并采用DER编码。 这是AEM密钥库所需的格式。

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. 通过单击上传私钥文件 **选择私钥文件**.
1. 通过单击上传证书文件 **选择证书链文件**.
1. 分配别名，如下所示：

   ![chlimage_1-373](assets/chlimage_1-373.png)

## 为SAML配置记录器 {#configure-a-logger-for-saml}

您可以设置日志记录器，以调试因错误配置SAML导致的任何问题。 您可以执行以下操作来实现此目标：

1. 转到Web控制台，网址为 *http://localhost:4502/system/console/configMgr*
1. 搜索并单击以下条目： **Apache Sling日志记录器配置**
1. 使用以下配置创建日志程序：

   * **日志级别：** 调试
   * **日志文件：** logs/saml.log
   * **记录器：** com.adobe.granite.auth.saml
