---
title: 对内容片段的远程 AEM GraphQL 查询的身份验证
description: 了解远程 AEM GraphQL 查询所需的身份验证，用于保护您的 Headless 内容投放。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 61%

---

# 对内容片段的远程 AEM GraphQL 查询的身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

的主要用例 [用于内容片段投放的Adobe Experience Manager (AEM) GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 是接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过身份验证的 API 访问，以保护 Headless 内容投放。

>[!NOTE]
>
>对于测试和开发，您还可以使用 [GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface) 接口直接访问 AEM GraphQL API。

对于身份验证，第三方服务需要使用AEM帐户用户名和密码进行身份验证。

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
