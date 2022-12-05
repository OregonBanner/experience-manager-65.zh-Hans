---
title: CSRF保护框架
seo-title: The CSRF Protection Framework
description: 框架利用令牌来保证客户端请求的合法性
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: f841e3886771fb00eee6e476d7111d4a335a9d51
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# CSRF保护框架{#the-csrf-protection-framework}

除了Apache Sling反向链接过滤器之外，Adobe还提供了新的CSRF保护框架来抵御此类攻击。

框架利用令牌来保证客户端请求的合法性。 令牌在表单发送到客户端时生成，并在表单发送回服务器时验证。

>[!NOTE]
>
>匿名用户的发布实例上没有令牌。

## 要求 {#requirements}

### 依赖项 {#dependencies}

依赖于 `granite.jquery` 依赖项将自动从CSRF保护框架中受益。 如果任何组件的情况并非如此，则必须声明依赖项为 `granite.csrf.standalone` 之后才能使用框架。

### 复制加密密钥 {#replicating-crypto-keys}

要使用令牌，您需要将HMAC二进制文件复制到部署中的所有实例。 请参阅 [复制HMAC密钥](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 以了解更多详细信息。

>[!NOTE]
>
>请务必确保 [Dispatcher配置更改](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 以便使用CSRF保护框架。

>[!NOTE]
>
>如果将清单缓存与Web应用程序一起使用，请确保添加“**&amp;ast;**“ ”添加到清单，以确保令牌不会使CSRF令牌生成调用离线。 有关详细信息，请参阅 [链接](https://www.w3.org/TR/offline-webapps/).
>
>有关CSRF攻击及其缓解方法的更多信息，请参阅 [跨站点请求伪造OWASP页](https://owasp.org/www-community/attacks/csrf).
