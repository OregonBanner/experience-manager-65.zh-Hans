---
title: 对内容片段的远程AEM GraphQL查询进行身份验证
description: 了解远程AEM GraphQL查询所需的身份验证，以保护无头内容交付的安全。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: 9278ba4fe85edca4ab5741f89c0fc0ef2cf2764d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 对内容片段的远程AEM GraphQL查询进行身份验证 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

用于 [Adobe Experience Manager(AEM)用于内容片段交付的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) 接受来自第三方应用程序或服务的远程查询。 这些远程查询可能需要经过验证的API访问，以保护无头内容交付的安全。

>[!NOTE]
>
>要进行测试和开发，您还可以使用 [GraphiQL接口](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) 界面。

为了进行身份验证，第三方服务需要使用AEM帐户用户名和密码进行身份验证。

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
