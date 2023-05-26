---
title: OWASP前10名
seo-title: OWASP Top 10
description: 了解AEM如何应对10大OWASP安全风险。
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# OWASP前10名{#owasp-top}

此 [打开Web应用程序安全项目](https://www.owasp.org) (OWASP)保存一份他们视为 [十大Web应用程序安全风险](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

下面列出了这些指标，并解释了CRX如何处理这些指标。

## 1.注射 {#injection}

* SQL — 设计禁止：默认存储库设置既不包括，也不需要传统数据库，所有数据都存储在内容存储库中。 所有访问仅限于经过身份验证的用户，并且只能通过JCR API执行。 仅搜索查询支持SQL (SELECT)。 此外，SQL还提供值绑定支持。
* LDAP - LDAP注入是不可能的，因为身份验证模块过滤输入并使用绑定方法执行用户导入。
* OS — 没有从应用程序内执行的外壳程序。

## 2.跨站点脚本(XSS) {#cross-site-scripting-xss}

一般缓解做法是使用基于的服务器端XSS保护库对用户生成内容的所有输出进行编码 [OWASP编码器](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) 和 [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

XSS是测试和开发期间的首要任务，发现的任何问题通常都会立即得到解决。

## 3.身份验证和会话管理中断 {#broken-authentication-and-session-management}

AEM使用可靠且行之有效的身份验证技术，依赖于 [Apache Jackrabbit](https://jackrabbit.apache.org/) 和 [Apache Sling](https://sling.apache.org/). AEM中未使用浏览器/HTTP会话。

## 4.不安全的直接对象引用 {#insecure-direct-object-references}

对数据对象的所有访问都由存储库进行调解，因此受到基于角色的访问控制的限制。

## 5.跨站点请求伪造(CSRF) {#cross-site-request-forgery-csrf}

通过自动将加密令牌注入所有表单和AJAX请求并在服务器上验证每个POST的此令牌，可缓解跨站点请求伪造(CSRF)。

此外，AEM附带基于反向链接标头的过滤器，可以将其配置为 *仅限* 允许来自特定主机的POST请求（在列表中定义）。

## 6.安全配置错误 {#security-misconfiguration}

无法保证始终正确配置所有软件。 但是，我们努力提供尽可能多的指导，并尽可能简化配置。 此外，AEM附带 [集成安全运行状况检查](/help/sites-administering/operations-dashboard.md) 可以帮助您一目了然地监控安全配置。

请查看 [安全核对清单](/help/sites-administering/security-checklist.md) 有关为您提供逐步强化说明的更多信息。

## 7.不安全的加密存储 {#insecure-cryptographic-storage}

密码作为加密哈希存储在用户节点中；默认情况下，此类节点仅供管理员和用户自己读取。

使用FIPS 140-2认证的加密库以加密形式存储敏感数据，例如第三方凭证。

## 8.限制URL访问失败 {#failure-to-restrict-url-access}

存储库允许设置 [细粒度权限（由JCR指定）](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) 对于任何给定路径的任何给定用户或组，通过访问控制条目。 存储库强制执行访问限制。

## 9.传输层保护不足 {#insufficient-transport-layer-protection}

通过服务器配置缓解（例如，仅使用HTTPS）。

## 10.未验证的重定向和转发 {#unvalidated-redirects-and-forwards}

通过限制所有重定向到用户提供的内部位置的目标而缓解。
