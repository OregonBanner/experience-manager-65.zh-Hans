---
title: 持久 GraphQL 查询
description: 了解如何在 Adobe Experience Manager 中使用持久 GraphQL 查询优化性能。客户端应用程序可以使用HTTPGET方法来请求持久化查询，并且响应可以缓存在Dispatcher和CDN层，从而最终提高客户端应用程序的性能。
source-git-commit: f4a3b7edc9187c1984afedb4e3b4c558354a4d84
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 73%

---

# 持久 GraphQL 查询 {#persisted-queries-caching}

持久查询是创建并存储在 Adobe Experience Manager (AEM) as a Cloud Service 服务器上的 GraphQL 查询。它们可以经客户端应用程序以 GET 请求方式请求。GET请求的响应可以缓存在调度程序和内容交付网络(CDN)层，最终提高请求客户端应用程序的性能。 这与标准的 GraphQL 查询不同，后者使用 POST 请求执行，而在 POST 请求中，无法轻松缓存响应。

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md) 在 AEM 中可供您开发、测试和持久您的 GraphQL 查询，然后再[转移到您的生产环境](#transfer-persisted-query-production)。 对于需要自定义的情况(例如， [自定义缓存](/help/sites-developing/headless/graphql-api/graphiql-ide.md#caching-persisted-queries))，您可以使用API;请参阅 [如何保留GraphQL查询](#how-to-persist-query).

## 持久查询及端点 {#persisted-queries-and-endpoints}

持久查询必须始终使用与[相应站点配置](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)相关的端点，因此它们可以使用以下项之一或全部：

* 全球配置和端点
查询具有对所有内容片段模型的访问权限。
* 特定站点配置和端点
为特定站点配置创建持久查询需要对应的站点配置特定的端点（用于提供对相关内容片段模型的访问权限）。
例如，要创建特定于 WKND Sites 配置的持久查询，必须预先创建对应的 WKND 特定的端点。

>[!NOTE]
>
>有关更多详细信息，请参阅[在配置浏览器中启用内容片段功能](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
>
>对于适当的 Sites 配置，**需要启用 GraphQL 持久查询**。

例如，如果存在名为 `my-query` 的特定查询，使用来自站点配置 `my-conf` 的模型 `my-model`：

* 您可以使用 `my-conf` 特定的端点创建查询，然后查询将保存如下：
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* 您可以使用 `global` 端点创建相同的查询，但然后查询将保存如下：
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>这里有两种不同的查询，保存在不同的路径中。
>
>它们只是正好使用了相同的模型，但通过不同的端点。

## 如何使 GraphQL 查询持久 {#how-to-persist-query}

建议先在 AEM 作者环境中保留查询，然后将[查询转移到](#transfer-persisted-query-production) AEM 发布环境中，供应用程序使用。

有多种持久查询的方法，包括：

* GraphiQL IDE – 请参阅[保存保留的查询](/help/sites-developing/headless/graphql-api/graphiql-ide.md#saving-persisted-queries)（首选方法）
* cURL — 请参阅以下示例
* 其他工具，包括 [Postman](https://www.postman.com/)

GraphiQL IDE 是 **首选**&#x200B;保留查询的方法。 使用 **cURL** 命令行工具：

1. 使用 PUT 操作将查询放入新端点 URL `/graphql/persist.json/<config>/<persisted-label>` 来准备查询。

   例如，创建持久查询：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. 此时，检查响应。

   例如，检查是否成功：

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. 然后，您可以通过对 URL `/graphql/execute.json/<shortPath>` 执行 GET 操作来请求持久查询。

   例如，使用持久查询：

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 通过将持久查询 POST 到已经存在的查询路径来更新持久查询。

   例如，使用持久查询：

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. 创建打包的简单查询。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. 使用缓存控制创建打包的简单查询。

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. 使用参数创建持久查询：

   例如：

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## 如何执行持久查询 {#execute-persisted-query}

要执行持久查询，客户端应用程序使用以下语法发出 GET 请求：

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

其中 `PERSISTENT_PATH` 是保存持久查询的缩略路径。

1. 例如，`wknd` 是配置名称，`plain-article-query` 为持久查询的名称。要执行查询：

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 使用参数执行查询。

   >[!NOTE]
   >
   > 执行持久查询时，必须对查询变量和值进行正确地[编码](#encoding-query-url)。

   例如：

   ```bash
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   请参阅使用[查询变量](#query-variables)以了解更多详细信息。

## 使用查询变量 {#query-variables}

查询变量可与持久查询一起使用。 使用变量名称和值将查询变量附加到以分号 (`;`) 为前缀的请求中。多个变量以分号分隔。

该模式如下所示：

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例如，以下查询包含一个变量 `activity` 要根据活动值过滤列表，请执行以下操作：

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

此查询可以保留在路径 `wknd/adventures-by-activity`下。 要调用 Persisted 查询 `activity=Camping`，请求如下所示：

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

请注意，`%3B` 是 `;` 的 UTF-8 编码，`%3D` 是 `=` 的编码。 查询变量和任何特殊字符必须[正确编码](#encoding-query-url)才能执行持久查询。

## 正在缓存您的持久查询 {#caching-persisted-queries}

建议使用持久化查询，因为它们可以缓存在 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 和内容交付网络(CDN)层，最终提高请求客户端应用程序的性能。

默认情况下， AEM将根据生存时间(TTL)定义使缓存失效。 这些TTL可由以下参数定义。 这些参数可通过各种方式访问，其名称会根据所使用的机制而有所变化：

| 缓存类型 | [HTTP头](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | OSGi配置  |
|--- |--- |--- |--- |
| 浏览器 | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` |

{style="table-layout:auto"}

### 创作实例 {#author-instances}

对于创作实例，默认值为：

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

这些：

* 无法使用OSGi配置覆盖
* 会被使用cURL定义HTTP标头设置的请求覆盖；它应包括适合的设置 `cache-control` 和/或 `surrogate-control`;有关示例，请参阅 [在保留的查询级别管理缓存](#cache-persisted-query-level)

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready; add cross-reference too -->
<!--
* can be overwritten if you specify values in the **Headers** dialog of the [GraphiQL IDE](#http-cache-headers-graphiql-ide)
-->

### 发布实例 {#publish-instances}

对于发布实例，默认值为：

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

这些值可以被覆盖：

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready -->
<!--
* [from the GraphQL IDE](#http-cache-headers-graphiql-ide)
-->

* [在保留的查询级别](#cache-persisted-query-level);这包括使用命令行界面中的cURL将查询发布到AEM，以及发布持久查询。

* [具有OSGi配置](#cache-osgi-configration)

<!-- CQDOC-20186 -->
<!-- keep for future use; check link -->
<!--
### Managing HTTP Cache Headers in the GraphiQL IDE {#http-cache-headers-graphiql-ide}

The GraphiQL IDE - see [Saving Persisted Queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

### 在保留的查询级别管理缓存 {#cache-persisted-query-level}

这包括使用命令行界面中的cURL将查询发布到AEM。

有关PUT（创建）方法的示例：

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

有关POST（更新）方法的示例：

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

可以在创建时（PUT）或以后（例如，通过 POST 请求）设置 `cache-control`。在创建持久查询时，缓存控制是可选的，因为 AEM 可以提供默认值。请参阅 [如何保留GraphQL查询](#how-to-persist-query)，例如使用cURL保留查询的示例。

### 使用OSGi配置管理缓存 {#cache-osgi-configration}

要全局管理缓存，您可以 [配置OSGi设置](/help/sites-deploying/configuring-osgi.md) 对于 **持久查询服务配置**. 否则，此OSGi配置使用 [发布实例的默认值](#publish-instances).

>[!NOTE]
>
>OSGi配置仅适用于发布实例。 创作实例上存在配置，但忽略该配置。

## 为应用程序使用的查询 URL 编码 {#encoding-query-url}

对于应用程序，在构建查询变量时使用的任何特殊字符（即分号 (`;`)、等号 (`=`)、斜杠 `/`）才能使用相应的 UTF-8 编码。

例如：

```bash
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL 可以划分为以下部分：

| URL 部分 | 描述 |
|----------| -------------|
| `/graphql/execute.json` | 持久查询端点 |
| `/wknd/adventure-by-path` | 持久查询路径 |
| `%3B` | `;` 的编码 |
| `adventurePath` | 查询变量 |
| `%3D` | `=` 的编码 |
| `%2F` | `/` 的编码 |
| `%2Fcontent%2Fdam...` | 内容片段的编码路径 |

在纯文本中，请求 URI 如下所示：

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

要在客户端应用程序中使用持久查询，应使用 AEM headless 客户端 SDK [JavaScript](https://github.com/adobe/aem-headless-client-js)、[Java](https://github.com/adobe/aem-headless-client-java) 或 [NodeJS](https://github.com/adobe/aem-headless-client-nodejs)。 Headless 客户端 SDK 将自动在请求中正确编码任何查询变量。

## 正在将持久查询转移到生产环境  {#transfer-persisted-query-production}

应始终在 AEM 创作服务上创建持久查询，然后将其发布（复制）到 AEM 发布服务。 通常，持久查询会在本地或开发环境等较低环境中创建和测试。 然后，有必要将持久查询提升到更高级别的环境，最终在生产 AEM 发布环境中提供，以供客户端应用程序使用。

### 持久查询包

可以将持久查询构建在[ AEM 程序包](/help/sites-administering/package-manager.md)中。然后，可以在不同的环境中下载和安装 AEM 包。 AEM 包也可以从 AEM 创作环境复制到 AEM 发布环境。

要创建包：

1. 导航到&#x200B;**工具** > **部署** > **包**。
1. 点击&#x200B;**创建包**&#x200B;创建一个新包。 这将打开一个用于定义资源包的对话框。
1. 在包定义对话框中，在&#x200B;**常规**&#x200B;下输入&#x200B;**名称**，如“wknd-persistent-queries”。
1. 输入版本号，如“1.0”。
1. 在&#x200B;**过滤器**&#x200B;下添加新的&#x200B;**过滤器**。 使用路径查找器选择 `persistentQueries` 文件夹。 例如，`wknd` 的配置完整路径将为 `/conf/wknd/settings/graphql/persistentQueries`。
1. 点击&#x200B;**保存**&#x200B;以保存新的包定义并关闭对话框。
1. 在新创建的包定义中点击&#x200B;**生成**&#x200B;按钮。

生成包后，您可以：

* **下载** 包，并在其他环境上重新上传。
* 通过点击&#x200B;**更多** > **复制**&#x200B;来&#x200B;**复制**&#x200B;包。 这会将包复制到连接的 AEM 发布环境。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
