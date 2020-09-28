---
title: '[!DNL资产] HTTP API。'
description: 使用中的HTTP API创建、读取、更新、删除和管理数字资产 [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 1%

---


# [!DNL Assets] HTTP API {#assets-http-api}

## 概述 {#overview}

HTTP [!DNL Assets] API允许对数字资产（包括元数据、演绎版和注释）以及使用内容片段的结构化内容执行创建读取更新删除(CRUD) [!DNL Experience Manager] 操作。 它在上公 `/api/assets` 开，并作为REST API实施。 它包含 [对内容片段的支持](/help/assets/assets-api-content-fragments.md)。

访问API:

1. 在打开API服务文档 `https://[hostname]:[port]/api.json`。
1. 按照服务 [!DNL Assets] 链接进行操作，以 `https://[hostname]:[server]/api/assets.json`便。

API响应是某些MIME类型的JSON文件和所有MIME类型的响应代码。 JSON响应是可选的，可能不可用，例如PDF文件。 依赖响应代码进行进一步的分析或操作。

结束 [!UICONTROL 后]，资产及其演绎版不能通过Web界 [!DNL Assets] 面和HTTP API使用。 如果“开始时间”为将来，或“结束 [!UICONTROL 时间] ”为过去，则 [!UICONTROL API会返回] 404错误消息。

>[!CAUTION]
>
>[HTTP API更新命名空间中的元](#update-asset-metadata) 数据属 `jcr` 性。 但是，Experience Manager用户界面会更新命名空间中的元数据属 `dc` 性。

## 内容片段 {#content-fragments}

内 [容片段](/help/assets/content-fragments/content-fragments.md) 是一种特殊类型的资产。 它可用于访问结构化数据，如文本、数字、日期等。 由于资产(如图像或文档 `standard` )存在多种差异，因此一些其他规则适用于处理内容片段。

有关详细信息， [请参阅Experience Manager资产HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md)。

## Data model {#data-model}

HTTP [!DNL Assets] API公开两个主要元素、文件夹和资产（对于标准资产）。

此外，它还针对描述内容片段中结构化内容的自定义数据模型显示更详细的元素。 有关更 [多信息，请参阅](/help/assets/assets-api-content-fragments.md#content-fragments) “内容片段数据模型”。

### 文件夹 {#folders}

文件夹类似于传统文件系统中的目录。 它们是其他文件夹或声明的容器。 文件夹具有以下组件：

**实体**:文件夹的实体是其子元素，可以是文件夹和资产。

**属性**:

* `name` 是文件夹的名称。 这与URL路径中没有扩展名的最后一个区段相同。
* `title` 是文件夹的可选标题，可以显示该标题而不是其名称。

>[!NOTE]
>
>文件夹或资产的某些属性会映射到其他前缀。 前缀 `jcr` 、 `jcr:title`和 `jcr:description`将替换为 `jcr:language` 前缀 `dc` 。 因此，在返回的JSON `dc:title` 中 `dc:description` ，并分别 `jcr:title` 包含和 `jcr:description`的值。

**链接** “文件夹”显示三个链接：

* `self`:链接到自身。
* `parent`:链接到父文件夹。
* `thumbnail`:（可选）指向文件夹缩略图图像的链接。

### 资产 {#assets}

在Experience Manager中，资产包含以下元素：

* 资产的属性和元数据。
* 多个演绎版，如原始演绎版（最初上传的资产）、缩略图和各种其他演绎版。 其他再现可能是不同大小、不同视频编码或从PDF或文件提取页面的 [!DNL Adobe InDesign] 图像。
* 可选注释。

有关内容片段中元素的信息，请参 [阅Experience Manager资产HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md#content-fragments)。

在文 [!DNL Experience Manager] 件夹中，具有以下组件：

* 实体：资产的子项是其演绎版。
* 属性.
* 链接.

HTTP [!DNL Assets] API包括以下功能：

* [检索文件夹列表](#retrieve-a-folder-listing)。
* [创建文件夹](#create-a-folder)。
* [创建资产](#create-an-asset)。
* [更新资产二进制](#update-asset-binary)。
* [更新资产元数据](#update-asset-metadata)。
* [创建资产演绎版](#create-an-asset-rendition)。
* [更新资产演绎版](#update-an-asset-rendition)。
* [创建资产评论](#create-an-asset-comment)。
* [复制文件夹或资产](#copy-a-folder-or-asset)。
* [移动文件夹或资产](#move-a-folder-or-asset)。
* [删除文件夹、资产或演绎版](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>为了便于读取，以下示例忽略完整的cURL记号。 事实上，该记号与Resty [相关](https://github.com/micha/resty) ,Resty是它的脚本包装器 `cURL`。

**前提条件**

* 访问 `https://[aem_server]:[port]/system/console/configMgr`.
* 导航到 **[!UICONTROL AdobeGranite CSRF滤镜]**。
* 确保属性筛选 **[!UICONTROL 器方法]** 包括： `POST`, `PUT`, `DELETE`

## 检索文件夹列表 {#retrieve-a-folder-listing}

检索现有文件夹及其子实体（子文件夹或资源）的Siren表示形式。

**请求**: `GET /api/assets/myFolder.json`

**响应代码**:响应代码为：

* 200 —— 好——成功。
* 404 —— 未找到——文件夹不存在或无法访问。
* 500 —— 内部服务器错误——如果出现其他问题。

**响应**:返回的实体类是资产或文件夹。 包含的实体的属性是每个实体的全部属性集的子集。 为了获得实体的完整表示形式，客户端应检索链接指向的URL的内容，其中 `rel` 包含 `self`:

## Create a folder {#create-a-folder}

创建新 `sling`: `OrderedFolder` 在给定路径上。 如果提 `*` 供的不是节点名称，则servlet将参数名称用作节点名称。 作为请求数据接受是新文件夹的Siren表示形式或一组名称——值对，编码为 `application/www-form-urlencoded` 或 `multipart`/ `form``data`-，对于直接从HTML表单创建文件夹很有用。 此外，文件夹的属性可以指定为URL查询参数。

如果提供路径的父节 `500` 点不存在，则API调用将失败，并带有响应代码。 如果文件夹已存在， `409` 则调用会返回响应代码。

**参数**: `name` 是文件夹名称。

**请求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**响应代码**:响应代码为：

* 201 —— 创建——成功创建时。
* 409 —— 冲突——如果文件夹已存在。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 创建资产 {#create-an-asset}

将提供的文件放在提供的路径上，以在DAM存储库中创建资产。 如果提 `*` 供的是节点名称，则servlet使用参数名称或文件名作为节点名称。

**参数**:参数用 `name` 于资产名称和 `file` 文件引用。

**请求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**响应代码**:响应代码为：

* 201 —— 已创建——如果资产创建成功。
* 409 —— 冲突——如果资产已存在。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 更新资产二进制 {#update-asset-binary}

更新资产的二进制文件（原始名称的演绎版）。 如果已配置更新，则更新会触发要执行的默认资产处理工作流。

**请求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**响应代码**:响应代码为：

* 200 —— 确定——如果资产已成功更新。
* 404 —— 未找到——如果在提供的URI中找不到或访问资产，则返回该资产。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 更新资产元数据 {#update-asset-metadata}

更新资产元数据属性。 如果更新命名空间中的任 `dc:` 何属性，API将更新命名空间中的同一属 `jcr` 性。 API不同步两个命名空间下的属性。

**请求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**响应代码**:响应代码为：

* 200 —— 确定——如果资产已成功更新。
* 404 —— 未找到——如果在提供的URI中找不到或访问资产，则返回该资产。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

### 在命名空间和之间同步元 `dc` 数据更 `jcr` 新 {#sync-metadata-between-namespaces}

API方法更新命名空间中的元数据属 `jcr` 性。 使用触屏UI进行的更新更改了命名空间中的元数据属 `dc` 性。 要在命名空间和之间 `dc` 同步元 `jcr` 数据值，您可以创建工作流并配置Experience Manager以在资产编辑时执行该工作流。 使用ECMA脚本同步所需的元数据属性。 以下示例脚本将标题字符串同步在 `dc:title` 和之 `jcr:title`间。

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## 创建资产演绎版 {#create-an-asset-rendition}

为资产创建新资产演绎版。 如果未提供请求参数名称，则文件名将用作再现名称。

**参数**:这些参数 `name` 用于再现的名称 `file` 和文件引用。

**请求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**响应代码**:响应代码为：

* 201 —— 已创建——如果再现已成功创建。
* 404 —— 未找到——如果在提供的URI中找不到或访问资产，则返回该资产。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 更新资产演绎版 {#update-an-asset-rendition}

更新分别用新的二进制数据替换资产演绎版。

**请求**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**响应代码**:响应代码为：

* 200 —— 确定——如果再现已成功更新。
* 404 —— 未找到——如果在提供的URI中找不到或访问资产，则返回该资产。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 在资产上添加评论 {#create-an-asset-comment}

创建新资产注释。

**参数**:参数用 `message` 于注释的消息正文和 `annotationData` JSON格式的注释数据。

**请求**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**响应代码**:响应代码为：

* 201 —— 已创建——如果注释已成功创建。
* 404 —— 未找到——如果在提供的URI中找不到或访问资产，则返回该资产。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。

## 复制文件夹或资产 {#copy-a-folder-or-asset}

复制提供的路径中提供到新目标的文件夹或资产。

**请求标题**:参数包括：

* `X-Destination` - API解决方案范围中要将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。 仅使 `0` 用会复制资源及其属性，而不复制其子项。
* `X-Overwrite` -使用 `F` 防止覆盖现有目标位置的资产。

**请求**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**响应代码**:响应代码为：

* 201 —— 已创建——如果文件夹／资产已复制到非现有目标。
* 204 —— 无内容——如果文件夹／资产已复制到现有目标。
* 412 - PREPOSITATION FAILED —— 如果缺少请求标头。
* 500 —— 内部服务器错误——如果出现其他问题。

## 移动文件夹或资产 {#move-a-folder-or-asset}

将给定路径上的文件夹或资产移动到新目标。

**请求标题**:参数包括：

* `X-Destination` - API解决方案范围中要将资源复制到的新目标URI。
* `X-Depth` - `infinity` 或 `0`。 仅使 `0` 用会复制资源及其属性，而不复制其子项。
* `X-Overwrite` -使用强制 `T` 删除现有资源或防止覆 `F` 盖现有资源。

**请求**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

请勿在 `/content/dam` URL中使用。 移动资产并覆盖现有资产的示例命令如下：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**响应代码**:响应代码为：

* 201 —— 已创建——如果文件夹／资产已复制到非现有目标。
* 204 —— 无内容——如果文件夹／资产已复制到现有目标。
* 412 - PREPOSITATION FAILED —— 如果缺少请求标头。
* 500 —— 内部服务器错误——如果出现其他问题。

## 删除文件夹、资产或演绎版 {#delete-a-folder-asset-or-rendition}

删除提供路径上的资源(-tree)。

**请求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**响应代码**:响应代码为：

* 200 —— 确定——如果文件夹已成功删除。
* 412 - PREPOSITATION FAILED —— 如果找不到或访问根集合。
* 500 —— 内部服务器错误——如果出现其他问题。
