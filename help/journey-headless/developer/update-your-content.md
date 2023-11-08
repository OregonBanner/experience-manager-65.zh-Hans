---
title: 如何通过 AEM Assets API 更新您的内容
description: 在 AEM Headless 开发人员历程的这一部分中，了解如何使用 REST API 访问和更新内容片段的内容。
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 88%

---

# 如何通过 AEM Assets API 更新您的内容 {#update-your-content}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，了解如何使用 REST API 访问和更新内容片段的内容。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[如何通过 AEM 交付 API 访问您的内容](access-your-content.md)中，您已了解如何通过 AEM GraphQL API 访问 AEM 中的 Headless 内容，您现在应该：

* 深入了解 GraphQL。
* 了解 AEM GraphQL API 的工作原理。
* 了解一些实际的示例查询。

本文基于这些基础知识编写，以便您了解如何通过 REST API 更新 AEM 中现有的 Headless 内容。

## 目标 {#objective}

* **受众**：高级
* **目标**：了解如何使用 REST API 访问和更新内容片段的内容：
   * 引入 AEM Assets HTTP API。
   * 引入和讨论 API 中的内容片段支持。
   * 阐释 API 的详细信息。

<!--
  * Look at sample code to see how things work in practice.
-->

## 为什么您需要用于内容片段的 Assets HTTP API？ {#why-http-api}

在 Headless 历程的上一个阶段，您已了解如何使用 AEM GraphQL API 通过查询来检索您的内容。

那么，为什么需要另一个 API 呢？

资源HTTP API允许您 **读取** 您的内容，但它还允许您 **创建**， **更新** 和 **删除** content - GraphQL API无法执行的操作。

Assets REST API 在最新版本的 Adobe Experience Manager 的每个现成安装中提供。

## Assets HTTP API {#assets-http-api}

Assets HTTP API 包含：

* Assets REST API
* 包括对内容片段的支持

Assets HTTP API 的当前实施基于 **REST** 架构样式，并使您能够通过 **CRUD** 操作（创建、读取、更新、删除）访问内容（存储在 AEM 中）。

通过这些操作，API允许您通过向JavaScript前端应用程序提供内容服务，将Adobe Experience Manager作为Headless CMS（内容管理系统）运行。 或者，任何其他可以执行 HTTP 请求并处理 JSON 响应的应用程序。例如，基于框架或自定义的单页应用程序 (SPA) 需要通过 API 提供的内容（通常采用 JSON 格式）。

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
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

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

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## Assets HTTP API 和内容片段 {#assets-http-api-content-fragments}

内容片段用于 Headless 交付，它是一种特殊类型的资源。它们用于访问结构化数据，例如文本、数字、日期等。

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## 使用 Assets REST API {#using-aem-assets-rest-api}

### 访问 {#access}

Assets REST API 使用 `/api/assets` 端点并需要资产路径才能访问资产（不带前导 `/content/dam`）。

* 这意味着，要访问以下位置的资产：
   * `/content/dam/path/to/asset`
* 您需要请求：
   * `/api/assets/path/to/asset`

例如，要访问 `/content/dam/wknd/en/adventures/cycling-tuscany`，需要请求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>访问：
>
>* `/api/assets`**不**&#x200B;需要使用 `.model` 选择器。
>* `/content/path/to/page`**需要**&#x200B;使用 `.model` 选择器。

### 操作 {#operation}

HTTP 方法决定了要执行的操作：

* **GET** – 检索资产或文件夹的 JSON 表示形式
* **POST** – 创建新资产或文件夹
* **PUT** – 更新资产或文件夹的属性
* **DELETE** – 删除资产或文件夹

>[!NOTE]
>
>请求正文和/或 URL 参数可用于配置其中一些操作；例如，定义文件夹或资产应由 **POST** 请求创建。

API 引用文档中将定义受支持请求的准确格式。

根据您使用的是 AEM 创作环境还是发布环境以及您的具体用例，使用情况可能会有所不同。

* 强烈建议您将创建绑定到创作实例（目前无法使用此 API 复制要发布的片段）。
* 可以通过这两种方式交付，因为 AEM 仅以 JSON 格式提供请求的内容。

   * 来自 AEM 创作实例的存储和交付应足以满足防火墙背后的媒体库应用程序的需求。

   * 对于实时 Web 交付，建议使用 AEM 发布实例。

>[!CAUTION]
>
>AEM实例上的Dispatcher配置可能会阻止对的访问 `/api`.

>[!NOTE]
>
>有关更多详细信息，请参阅 API 引用。具体而言，[Adobe Experience Manager Assets API – 内容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)。

### 读取/交付 {#read-delivery}

使用者式：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

响应是序列化的 JSON，其内容的结构与内容片段中的一样。引用将作为引用 URL 提供。

可以执行两种类型的读取操作：

* 按路径读取特定内容片段，这将返回内容片段的 JSON 表示形式。
* 按路径读取内容片段的文件夹：这将返回文件夹中的所有内容片段的 JSON 表示形式。

### 创建 {#create}

使用者式：

`POST /{cfParentPath}/{cfName}`

正文必须包含要创建的内容片段的 JSON 表示形式，包括应在内容片段元素上设置的任何初始内容。必须设置 `cq:model` 属性，并且该属性必须指向有效的内容片段模型。如果不这样做，将导致出错。此外，还必须添加一个设置为 `application/json` 的标头 `Content-Type`。

### 更新 {#update}

使用者式

`PUT /{cfParentPath}/{cfName}`

正文必须包含要为给定内容片段更新的内容的 JSON 表示形式。

这可以是内容片段的标题或描述、单个元素或所有元素值和/或元数据。

### 删除 {#delete}

使用者式：

`DELETE /{cfParentPath}/{cfName}`

有关使用 AEM Assets REST API 的更多详细信息，您可以引用：

* Adobe Experience Manager Assets HTTP API（其他资源）
* AEM Assets HTTP API 中的内容片段支持（其他资源）

## 后续内容 {#whats-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 了解 AEM Assets HTTP API 的基础知识。
* 了解此 API 中如何支持内容片段。

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

您应该通过下一次查看文档来继续您的AEM Headless历程 [如何使用Headless应用程序上线](go-live.md) AEM Headless项目实际上线的位置！

## 其他资源 {#additional-resources}

* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [内容片段 REST API](/help/assets/assets-api-content-fragments.md)
   * [API 引用](/help/assets/assets-api-content-fragments.md#api-reference)
* [Adobe Experience Manager Assets API – 内容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
* [AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)
* [已说明 CORS/AEM](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [视频 – 使用 AEM 针对 CORS 进行开发](https://helpx.adobe.com/cn/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [AEM as a Headless CMS 简介](/help/sites-developing/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans)
