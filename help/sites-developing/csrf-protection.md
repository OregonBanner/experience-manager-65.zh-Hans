---
title: CSRF保护框架
seo-title: CSRF保护框架
description: 框架利用令牌来保证客户端请求的合法性
seo-description: 框架利用令牌来保证客户端请求的合法性
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# CSRF保护框架{#the-csrf-protection-framework}

除了Apache Sling反向链接过滤器之外，Adobe还提供了新的CSRF保护框架来抵御此类攻击。

框架利用令牌来保证客户端请求的合法性。 令牌在表单发送到客户端时生成，并在表单发送回服务器时验证。

>[!NOTE]
>
>匿名用户的发布实例上没有令牌。

## 要求 {#requirements}

### 依赖关系 {#dependencies}

任何依赖于`granite.jquery`依赖关系的组件都将自动从CSRF保护框架中受益。 如果任何组件的情况并非如此，则必须先向`granite.csrf.standalone`声明依赖项，然后才能使用框架。

### 复制加密密钥{#replicating-crypto-keys}

要使用令牌，您需要将`/etc/keys/hmac`二进制文件复制到部署中的所有实例。 将HMAC密钥复制到所有实例的一种简便方法是，创建一个包含密钥的包，并通过包管理器在所有实例上安装该密钥。

>[!NOTE]
>
>另外，请务必进行必要的[Dispatcher配置更改](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)，以便使用CSRF保护框架。

>[!NOTE]
>
>如果将清单缓存与Web应用程序一起使用，请确保向清单中添加“**&amp;ast;**”，以确保令牌不会使CSRF令牌生成调用离线。 有关详细信息，请参阅此[链接](https://www.w3.org/TR/offline-webapps/)。
>
>有关CSRF攻击及其缓解方法的更多信息，请参阅[跨站点请求伪造OWASP页面](https://owasp.org/www-community/attacks/csrf)。
