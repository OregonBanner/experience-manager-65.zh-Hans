---
title: CSRF保护框架
seo-title: CSRF保护框架
description: 该框架利用令牌来保证客户端请求的合法性
seo-description: 该框架利用令牌来保证客户端请求的合法性
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518

---


# CSRF保护框架{#the-csrf-protection-framework}

除了Apache Sling Referrer Filter之外，Adobe还提供新的CSRF保护框架以防止此类攻击。

该框架利用令牌来保证客户端请求的合法性。 在将表单发送到客户端时生成令牌，在将表单发回服务器时验证令牌。

>[!NOTE]
>
>发布实例上没有匿名用户的令牌。

## 要求 {#requirements}

### 依赖关系 {#dependencies}

任何依赖于依赖关系的组 `granite.jquery` 件都将自动从CSRF保护框架受益。 如果您的任何组件不是这样，则必须先将依赖关系声明为，然 `granite.csrf.standalone` 后才能使用框架。

### 复制加密密钥 {#replicating-crypto-keys}

为了利用令牌，您需要将二进制文件复制 `/etc/keys/hmac` 到部署中的所有实例。 将HMAC密钥复制到所有实例的一个便捷方法是创建一个包含密钥的包，并通过包管理器在所有实例上安装它。

>[!NOTE]
>
>确保还对 [Dispatcher配置进行必要的更改](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) ，以便使用CSRF保护框架。

>[!NOTE]
>
>如果将清单缓存与Web应用程序一起使用，请确保向清单中添加“**&amp;ast;**”，以确保令牌不使CSRF令牌生成调用脱机。 有关详细信息，请参阅此 [链接](https://www.w3.org/TR/offline-webapps/)。
>
>有关CSRF攻击及其缓解方法的详细信息，请参 [阅“跨站点请求伪造OWASP”页](https://owasp.org/www-community/attacks/csrf)。
