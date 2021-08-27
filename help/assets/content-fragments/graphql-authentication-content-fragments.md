---
title: 对内容片段的远程AEM GraphQL查询进行身份验证
description: 了解远程AEM GraphQL查询所需的身份验证，以保护无头内容交付的安全。
feature: Content Fragments,GraphQL API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 对内容片段的远程AEM GraphQL查询进行身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

[Adobe Experience Manager(AEM)GraphQL API用于内容片段交付](/help/assets/content-fragments/graphql-api-content-fragments.md)的主要用例是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过验证的API访问，以保护无头内容交付的安全。

>[!NOTE]
>
>要进行测试和开发，您还可以使用[GraphiQL接口](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)接口直接访问AEM GraphQL API。

为了进行身份验证，第三方服务需要[检索访问令牌](#retrieving-access-token)，该令牌随后可以在GraphQL请求](#use-access-token-in-graphql-request)中使用。[

## 检索访问令牌 {#retrieving-access-token}

<!-- 6.5.10.0 - does this page need to be migrated? -->

<!--
See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.
-->

## 在GraphQL请求中使用访问令牌 {#use-access-token-in-graphql-request}

要使第三方服务与AEM实例连接，它需要具有&#x200B;*访问令牌*。 然后，服务必须将此令牌添加到POST请求的`Authorization`标头中。

例如，GraphQL授权标头：

```xml
Authorization: Bearer <access_token>
```

## 权限要求 {#permission-requirements}

使用访问令牌发出的所有请求实际上将由生成令牌&#x200B;*的用户帐户发出*。

这意味着您需要检查帐户是否具有运行GraphQL查询所需的权限。

您可以在本地实例上使用GraphiQL来检查此项。
