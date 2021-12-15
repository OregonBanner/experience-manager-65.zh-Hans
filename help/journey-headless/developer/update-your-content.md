---
title: 如何通过AEM Assets API更新您的内容
description: 在AEM无头开发人员历程的这一部分中，了解如何使用REST API访问和更新内容片段的内容。
source-git-commit: 7f43d9d6b631b26f7b9293aa109498d0c8040436
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# 如何通过AEM Assets API更新您的内容 {#update-your-content}

在 [AEM Headless开发人员历程,](overview.md) 了解如何使用REST API访问和更新内容片段的内容。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [如何通过AEM交付API访问您的内容](access-your-content.md) 您学习了如何通过AEM GraphQL API在AEM中访问无头内容，现在应该：

* 深入了解GraphQL。
* 了解AEM GraphQL API的工作方式。
* 了解一些实用的示例查询。

本文基于这些基础知识，以便您了解如何通过REST API在AEM中更新现有的无头内容。

## 目标 {#objective}

* **受众**:高级
* **目标**:了解如何使用REST API访问和更新内容片段的内容：
   * 介绍AEM Assets HTTP API。
   * 介绍并讨论API中的内容片段支持。
   * 说明API的详细信息。

<!--
  * Look at sample code to see how things work in practice.
-->

## 为什么内容片段需要资产HTTP API {#why-http-api}

在无头历程的上一步中，您了解了如何使用AEM GraphQL API来使用查询检索内容。

那么，为何需要其他API?

资产HTTP API允许您 **读取** 您的内容，但它也允许您 **创建**, **更新** 和 **删除** 内容 — GraphQL API无法执行的操作。

在最新Adobe Experience Manager版本的每次现成安装中，都提供Assets REST API。

## 资产 HTTP API {#assets-http-api}

资产HTTP API包括：

* 资产REST API
* 包括对内容片段的支持

资产HTTP API的当前实施基于 **REST** 架构样式，并允许您通过 **CRUD** 操作（创建、读取、更新、删除）。

通过这些操作，API允许您通过向JavaScript前端应用程序提供内容服务，将Adobe Experience Manager作为无头CMS（内容管理系统）进行操作。 或任何可以执行HTTP请求并处理JSON响应的其他应用程序。 例如，单页应用程序(SPA)（基于框架或自定义）需要通过API提供的内容，通常采用JSON格式。

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## 资产HTTP API和内容片段 {#assets-http-api-content-fragments}

内容片段用于无标题交付，而内容片段是一种特殊类型的资产。 它们用于访问结构化数据，例如文本、数字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用资产REST API {#using-aem-assets-rest-api}

### 访问 {#access}

资产REST API使用 `/api/assets` 端点，并且需要资产的路径才能访问该资产(不具有前导 `/content/dam`)。

* 这意味着要在以下位置访问资产：
   * `/content/dam/path/to/asset`
* 您需要请求：
   * `/api/assets/path/to/asset`

例如，要访问 `/content/dam/wknd/en/adventures/cycling-tuscany`，请求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>访问：
>
>* `/api/assets` **不** 需要使用 `.model` 选择器。
>* `/content/path/to/page` **does** 要求使用 `.model` 选择器。


### 操作 {#operation}

HTTP方法确定要执行的操作：

* **GET**  — 检索资产或文件夹的JSON表示形式
* **POST**  — 创建新资产或文件夹
* **PUT**  — 更新资产或文件夹的属性
* **DELETE**  — 删除资产或文件夹

>[!NOTE]
>
>请求正文和/或URL参数可用于配置其中的一些操作；例如，定义文件夹或资产应由 **POST** 请求。

支持的请求的确切格式在API引用文档中定义。

用法可能因您使用的是AEM创作环境还是发布环境以及特定用例而异。

* 强烈建议将创建绑定到创作实例（并且当前没有方法使用此API复制片段以发布）。
* 可以同时从两者进行交付，因为AEM仅以JSON格式提供请求的内容。

   * 从AEM创作实例进行存储和交付应足以在防火墙后部署媒体库应用程序。

   * 对于实时Web交付，建议使用AEM发布实例。

>[!CAUTION]
>
>AEM实例上的调度程序配置可能会阻止访问 `/api`.

>[!NOTE]
>
>有关更多详细信息，请参阅API引用。 特别是， [Adobe Experience Manager Assets API — 内容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### 读取/投放 {#read-delivery}

用法包括：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

响应将以内容片段中的结构化进行序列化JSON。 引用作为引用URL提供。

可以执行两种类型的读取操作：

* 按路径读取特定内容片段，将返回内容片段的JSON表示形式。
* 按路径读取内容片段的文件夹：这会返回文件夹中所有内容片段的JSON表示形式。

### 创建 {#create}

用法包括：

`POST /{cfParentPath}/{cfName}`

主体必须包含要创建的内容片段的JSON表示形式，包括应在内容片段元素中设置的任何初始内容。 必须将 `cq:model` 属性，且必须指向有效的内容片段模型。 如果不这样做，则会导致错误。 还需要添加标头 `Content-Type` 将设置为 `application/json`.

### 更新 {#update}

使用方式为

`PUT /{cfParentPath}/{cfName}`

正文必须包含要为给定内容片段更新内容的JSON表示形式。

这可以只是内容片段、单个元素或所有元素值和/或元数据的标题或描述。

### 删除 {#delete}

用法包括：

`DELETE /{cfParentPath}/{cfName}`

有关使用AEM Assets REST API的更多详细信息，您可以引用：

* Adobe Experience Manager Assets HTTP API（其他资源）
* AEM Assets HTTP API中的内容片段支持（其他资源）

## 下一步 {#whats-next}

现在，您已完成AEM Headless开发人员历程的这一部分，接下来您应该：

* 了解AEM Assets HTTP API的基础知识。
* 了解此API如何支持内容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

您应该通过下一步审阅文档来继续您的AEM无头历程 [如何使用您的无头应用程序](go-live.md) 您实际将AEM Headless项目上线！

## 其他资源 {#additional-resources}

* [资产 HTTP API](/help/assets/mac-api-assets.md)
* [内容片段REST API](/help/assets/assets-api-content-fragments.md)
   * [API参考](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API — 内容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [CORS/AEM说明](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [视频 — 使用AEM开发CORS](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
