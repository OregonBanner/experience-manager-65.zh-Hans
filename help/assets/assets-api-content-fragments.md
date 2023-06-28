---
title: Assets HTTP API中的Adobe Experience Manager内容片段支持
description: 了解Assets HTTP API中对内容片段的支持，这是AEM Headless投放功能的重要部分。
feature: Content Fragments,Assets HTTP API
role: Developer
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
hide: true
source-git-commit: 48131c5accfe73b83197bd581ed5a22bc4890a56
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 24%

---

# AEM Assets HTTP API 中的内容片段支持 {#content-fragments-support-in-aem-assets-http-api}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |


## 概述 {#overview}

了解Assets HTTP API中对内容片段的支持，这是AEM Headless投放功能的重要部分。

>[!NOTE]
>
>此 [资源HTTP API](/help/assets/mac-api-assets.md) 包括：
>
>* Assets REST API
>* 包括对内容片段的支持
>
>Assets HTTP API的当前实施基于 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 建筑风格。

此 [Assets REST API](/help/assets/mac-api-assets.md) 允许Adobe Experience Manager的开发人员通过CRUD操作（创建、读取、更新、删除），直接通过HTTP API访问内容(存储在AEM中)。

该API允许您通过向JavaScript前端应用程序提供内容服务，将Adobe Experience Manager作为Headless CMS（内容管理系统）运行。 或者，任何其他可以执行 HTTP 请求并处理 JSON 响应的应用程序。

例如，基于框架或自定义的单页应用程序(SPA)需要通过HTTP API提供的内容，通常采用JSON格式。

While [AEM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 提供非常全面、灵活且可自定义的API，该API可为此目的提供所需的读取操作，并且其JSON输出可自定义，因此它们确实需要AEM WCM（Web内容管理）专门知识才能实施，因为它们必须托管在基于专用AEM模板的页面中。 并非每个SPA开发组织都能直接获得这些知识。

此时可以使用Assets REST API。 它允许开发人员直接访问资产（例如图像和内容片段），而无需先将资产嵌入页面，然后以序列化JSON格式交付其内容。

>[!NOTE]
>
>无法从Assets REST API自定义JSON输出。

Assets REST API还允许开发人员通过创建新资产、更新或删除现有资产、内容片段和文件夹来修改内容。

Assets REST API：

* 遵循 [HATEOAS原则](https://en.wikipedia.org/wiki/HATEOAS)

* 实施 [SIREN格式](https://github.com/kevinswiber/siren)

## 前提条件 {#prerequisites}

Assets REST API适用于最近的AEM版本的每个现成安装。

## 重要概念 {#key-concepts}

Assets REST API提供 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) — 样式访问AEM实例中存储的资源。

它使用 `/api/assets` 端点，并需要资源的路径才能访问它(不带 `/content/dam`)。

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

HTTP 方法决定了要执行的操作：

* **GET** – 检索资产或文件夹的 JSON 表示形式
* **POST** – 创建新资产或文件夹
* **PUT** – 更新资产或文件夹的属性
* **DELETE** – 删除资产或文件夹

>[!NOTE]
>
>请求正文和/或 URL 参数可用于配置其中一些操作；例如，定义文件夹或资产应由 **POST** 请求创建。

支持的请求的确切格式在 [API参考](/help/assets/assets-api-content-fragments.md#api-reference) 文档。

### 事务性行为 {#transactional-behavior}

所有请求都是原子的。

这意味着后续步骤(`write`)请求无法组合为单个事务，该事务可能会作为单个实体成功或失败。

### AEM (Assets) REST API与AEM组件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>宽高比</td>
   <td>Assets REST API<br/> </td>
   <td>AEM组件<br/> （使用Sling模型的组件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支持的用例</td>
   <td>一般目的。</td>
   <td><p>针对单页应用程序(SPA)或任何其他（使用内容）上下文中的使用情况进行了优化。</p> <p>还可以包含布局信息。</p> </td>
  </tr>
  <tr>
   <td>支持的操作</td>
   <td><p>创建、读取、更新、删除。</p> <p>根据实体类型执行其他操作。</p> </td>
   <td>只读.</td>
  </tr>
  <tr>
   <td>访问</td>
   <td><p>可以直接访问。</p> <p>使用 <code>/api/assets </code>端点，映射到 <code>/content/dam</code> （在存储库中）。</p> 
   <p>示例路径如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要通过AEM页面上的AEM组件引用。</p> <p>使用 <code>.model</code> 选择器创建JSON表示形式。</p> <p>示例路径如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可以使用多个选项。</p> <p>建议使用OAuth；可与标准设置分开配置。</p> </td>
   <td>使用AEM标准设置。</td>
  </tr>
  <tr>
   <td>体系结构说明</td>
   <td><p>写权限通常用于创作实例。</p> <p>也可以将读取定向到发布实例。</p> </td>
   <td>由于此方法为只读方法，因此通常用于发布实例。</td>
  </tr>
  <tr>
   <td>输出</td>
   <td>基于JSON的SIREN输出：冗长，但功能强大。 允许在内容中导航。</td>
   <td>基于JSON的专有输出；可通过Sling模型配置。 导航内容结构难以实施（但并不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果在没有特定身份验证要求的环境中使用Assets REST API，则需要正确配置AEM CORS过滤器。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* [已说明 CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [视频 – 使用 AEM 针对 CORS 进行开发](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

在具有特定身份验证要求的环境中，建议使用OAuth。

## 可用功能 {#available-features}

内容片段是资源的特定类型，请参阅 [使用内容片段](/help/assets/content-fragments/content-fragments.md).

有关通过API可用的功能的更多信息，请参阅：

* 此 [Assets REST API](/help/assets/mac-api-assets.md)
* [实体类型](/help/assets/assets-api-content-fragments.md#entity-types)，其中说明了特定于每个受支持类型（与内容片段相关）的功能

### 分页 {#paging}

Assets REST API支持通过URL参数分页(用于GET请求)：

* `offset`  — 要检索的第一个（子）实体的编号
* `limit`  — 返回的最大实体数

响应将包含寻呼信息，作为 `properties` 部分。 此 `srn:paging` 属性包含（子）实体的总数( `total`)、偏移量和限制( `offset`， `limit`)。

>[!NOTE]
>
>分页通常应用于容器实体（即包含演绎版的文件夹或资产），因为它与所请求实体的子项相关。

#### 示例：分页 {#example-paging}

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

## 实体类型 {#entity-types}

### 文件夹 {#folders}

文件夹充当资源和其他文件夹的容器。 它们反映了AEM内容存储库的结构。

Assets REST API公开对文件夹属性的访问权限；例如其名称、标题等。 资产将作为文件夹和子文件夹的子实体显示。

>[!NOTE]
>
>根据子资产和文件夹的资产类型，子实体的列表可能已经包含定义各个子实体的完整属性集。 或者，对于该子实体列表中的实体，只能公开缩减的一组属性。

### Assets {#assets}

如果请求资产，响应将返回其元数据；例如标题、名称以及各个资产架构定义的其他信息。

资产的二进制数据将作为类型的SIREN链接公开 `content`.

资产可以具有多个演绎版。 这些通常作为子实体显示，有一个例外是缩略图演绎版，它作为类型的链接显示 `thumbnail` ( `rel="thumbnail"`)。

### 内容片段 {#content-fragments}

A [内容片段](/help/assets/content-fragments/content-fragments.md) 是一种特殊类型的资产。 它们可用于访问结构化数据，如文本、数字、日期等。

由于与以下内容存在若干差异： *标准* 资产（如图像或音频）时，会应用一些其他规则来处理它们。

#### 呈现 {#representation}

内容片段：

* 不要公开任何二进制数据。
* 完全包含在JSON输出中(在 `properties` 属性)。

* 也被视为原子元素，即元素和变体作为片段属性的一部分显示，而不是作为链接或子实体显示。 这允许高效地访问片段的有效负载。

#### 内容模型和内容片段 {#content-models-and-content-fragments}

目前，定义内容片段结构的模型不会通过HTTP API公开。 因此， *消费者* 需要了解片段的模型（至少是最低限度） — 尽管大多数信息可以从有效负载中推断；数据类型等。 是定义的一部分。

要创建新内容片段，必须提供模型的（内部存储库）路径。

#### 关联的内容 {#associated-content}

关联内容当前未公开。

## 使用 {#using}

根据您使用的是 AEM 创作环境还是发布环境以及您的具体用例，使用情况可能会有所不同。

* 强烈建议将创建绑定到创作实例([并且当前没有方法复制片段以使用此API发布](/help/assets/assets-api-content-fragments.md#limitations))。
* 可以通过这两种方式交付，因为 AEM 仅以 JSON 格式提供请求的内容。

   * 来自 AEM 创作实例的存储和交付应足以满足防火墙背后的媒体库应用程序的需求。

   * 对于实时 Web 交付，建议使用 AEM 发布实例。

>[!CAUTION]
>
>AEM实例上的Dispatcher配置可能会阻止对的访问 `/api`.

>[!NOTE]
>
>欲知更多详情，请参见 [API参考](/help/assets/assets-api-content-fragments.md#api-reference). 具体而言，[Adobe Experience Manager Assets API – 内容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)。

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

## 限制 {#limitations}

有一些限制：

* **当前不支持内容片段模型**：无法读取或创建它们。 为了能够创建新内容片段或更新现有内容片段，开发人员必须知道内容片段模型的正确路径。 目前，获取这些内容的概览的唯一方法是通过管理UI。
* **引用被忽略**. 目前不检查是否引用了现有内容片段。 因此，例如，删除内容片段可能会导致包含对已删除内容片段的引用的页面出现问题。
* **JSON数据类型** 的REST API输出 *JSON数据类型* 当前为 *基于字符串的输出*.

## 状态代码和错误消息 {#status-codes-and-error-messages}

在相关情况下，可以看到以下状态代码：

* **200** （确定）在以下情况下返回：

   * 通过以下方式请求内容片段 `GET`
   * 通过以下方式成功更新内容片段 `PUT`

* **201** （已创建）在以下情况下返回：

   * 通过以下方式成功创建内容片段 `POST`

* **404** （未找到）在以下情况下返回：

   * 请求的内容片段不存在

* **500** （内部服务器错误）

  >[!NOTE]
  >
  >返回此错误：
  >
  >* 当发生无法使用特定代码标识的错误时
  >* 当给定的有效负载无效时

  下面列出了返回此错误状态并生成错误消息（等宽）的常见情况：

   * 父文件夹不存在（在通过创建内容片段时） `POST`)
   * 未提供内容片段模型（缺少cq：model）、无法读取（由于路径无效或权限问题）或没有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * 无法创建内容片段（可能是权限问题）：

      * `Could not create content fragment`

   * 无法更新标题和/或描述：

      * `Could not set value on content fragment`

   * 无法设置元数据：

      * `Could not set metadata on content fragment`

   * 无法找到或无法更新内容元素

      * `Could not update content element`
      * `Could not update fragment data of element`

  详细错误消息通常以下列方式返回：

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## API 引用 {#api-reference}

请参阅此处，了解详细的API参考：

* [Adobe Experience Manager Assets API – 内容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#assets)

## 其他资源 {#additional-resources}

有关更多信息，请参阅：

* [Assets HTTP API文档](/help/assets/mac-api-assets.md)
* [AEM Gem会话： OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
