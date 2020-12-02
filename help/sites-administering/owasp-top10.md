---
title: OWASP前10
seo-title: OWASP前10
description: 了解AEM如何应对前10大OWASP安全风险。
seo-description: 了解AEM如何应对前10大OWASP安全风险。
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: cd7331f5f57ec90ea72d41d467891dc832347a3c
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# OWASP前10{#owasp-top}

[开放Web 应用程序安全项目](https://www.owasp.org)(OWASP)保持其认为[前10个Web 应用程序安全风险](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)的列表。

下面列出了这些信息，并解释了CRX如何处理这些信息。

## 1.注射{#injection}

* SQL —— 设计阻止：默认存储库设置既不包括也不需要传统数据库，所有数据都存储在内容存储库中。 所有访问权限仅限于经过身份验证的用户，并且只能通过JCR API执行。 仅搜索查询支持SQL(SELECT)。 更多SQL优惠值绑定支持。
* LDAP —— 无法注入LDAP，因为身份验证模块会过滤器输入内容，并使用绑定方法执行用户导入。
* OS —— 应用程序中不执行Shell执行。

## 2.跨站点脚本(XSS){#cross-site-scripting-xss}

一般的缓解做法是使用基于[OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project)和[AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)的服务器端XSS保护库对用户生成内容的所有输出进行编码。

在测试和开发过程中，XSS是最优先的任务，发现的任何问题（通常）都会立即得到解决。

## 3.身份验证和会话管理中断{#broken-authentication-and-session-management}

AEM使用声音和经过验证的身份验证技术，依赖[Apache Jackrabbit](https://jackrabbit.apache.org/)和[Apache Sling](https://sling.apache.org/)。 AEM中不使用浏览器/HTTP会话。

## 4.不安全的直接对象引用{#insecure-direct-object-references}

对数据对象的所有访问都由存储库进行，因此受基于角色的访问控制限制。

## 5.跨站点请求伪造(CSRF){#cross-site-request-forgery-csrf}

跨站点请求伪造(CSRF)的缓解方法是：自动向所有表单和AJAX请求中注入加密令牌，并在每个POST在服务器上验证此令牌。

此外，AEM附带基于推荐人头的过滤器，该过滤器可配置为仅&#x200B;*允许来自特定主机(在列表中定义)的POST请求。*

## 6.安全错误配置{#security-misconfiguration}

无法保证所有软件始终正确配置。 但是，我们努力提供尽可能多的指导，使配置尽可能简单。 此外，AEM附带[集成的安全运行状况检查](/help/sites-administering/operations-dashboard.md)，可帮助您一目了然地监控安全配置。

请查阅[安全清单](/help/sites-administering/security-checklist.md)以了解详细信息，它为您提供逐步强化说明。

## 7.不安全的加密存储{#insecure-cryptographic-storage}

口令作为加密哈希存储在用户节点中；默认情况下，此类节点只能由管理员和用户自己读取。

敏感数据（如第三方凭据）使用经FIPS 140-2认证的加密库以加密形式存储。

## 8.未能限制URL访问{#failure-to-restrict-url-access}

存储库允许通过访问控制条目为任何给定路径上的任何给定用户或组设置[细粒度权限（由JCR指定）](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)。 存储库强制实施访问限制。

## 9.传输层保护不足{#insufficient-transport-layer-protection}

通过服务器配置缓解（例如，仅使用HTTPS）。

## 10.未验证重定向和转发{#unvalidated-redirects-and-forwards}

通过限制所有重定向到用户提供的目标到内部位置，减轻了重定向。

