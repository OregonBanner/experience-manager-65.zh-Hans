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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OWASP前10{#owasp-top}

开放 [式Web应用程序安全项目](https://www.owasp.org) (OWASP)保留了他们认为排名前10的Web应用程 [序安全风险列表](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)。

下面列出了这些内容，以及CRX如何处理这些内容的说明。

## 1.注射 {#injection}

* SQL —— 设计阻止：默认存储库设置既不包括也不需要传统数据库，所有数据都存储在内容存储库中。 所有访问权限仅限于经过身份验证的用户，并且只能通过JCR API执行。 仅搜索查询(SELECT)支持SQL。 此外，SQL还提供值绑定支持。
* LDAP - LDAP注入是不可能的，因为身份验证模块会过滤输入内容，并使用绑定方法执行用户导入。
* OS —— 应用程序内不执行Shell执行。

## 2.跨站点脚本(XSS) {#cross-site-scripting-xss}

一般的缓解做法是使用基于 [OWASP Encoder和](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) AntiSamy的服务器端XSS保护库对用户生成内容的所有输出进行编码 [](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)。

在测试和开发过程中，XSS都是最优先的任务，发现的任何问题（通常）都会立即得到解决。

## 3.断开的身份验证和会话管理 {#broken-authentication-and-session-management}

AEM使用可靠且久经考验的身份验证技术， [依赖于Apache Jackrabbit](https://jackrabbit.apache.org/)[和Apache Sling](https://sling.apache.org/)。 AEM中不使用浏览器/HTTP会话。

## 4.不安全的直接对象引用 {#insecure-direct-object-references}

对数据对象的所有访问由存储库中介，因此受基于角色的访问控制的限制。

## 5.跨站点请求伪造(CSRF) {#cross-site-request-forgery-csrf}

跨站点请求伪造(CSRF)的缓解方法是：自动向所有表单和AJAX请求中注入加密令牌，并在每个POST的服务器上验证此令牌。

此外，AEM附带基于引用标题的过滤器，该过滤器可配置为仅允许来自特别白名单的主机的POST请求。

## 6.安全配置错误 {#security-misconfiguration}

不可能保证所有软件始终正确配置。 但是，我们努力提供尽可能多的指导，使配置尽可能简单。 此外，AEM附带集成的 [安全性运行状况检查](/help/sites-administering/operations-dashboard.md) ，可帮助您一览表地监控安全配置。

请查阅安全核 [对清单](/help/sites-administering/security-checklist.md) ，以了解更多信息，这些信息为您提供逐步强化的说明。

## 7.不安全的加密存储 {#insecure-cryptographic-storage}

密码作为密码散列存储在用户节点中；默认情况下，此类节点只能由管理员和用户自己读取。

敏感数据（如第三方凭据）使用FIPS 140-2认证的加密库以加密形式存储。

## 8.限制URL访问失败 {#failure-to-restrict-url-access}

存储库允许通过访问控 [制条目，为任何给定路径上的任何给定用户或用户组设置细粒度的权限（由JCR指定）](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) 。 存储库强制实施访问限制。

## 9.传输层保护不足 {#insufficient-transport-layer-protection}

通过服务器配置缓解（例如，仅使用HTTPS）。

## 10.未验证的重定向和转发 {#unvalidated-redirects-and-forwards}

通过限制所有重定向到用户提供的目标到内部位置，缓解了问题。

