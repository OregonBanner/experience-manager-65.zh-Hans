---
title: 资产 HTTP API
description: 了解Assets HTTP API的实施、数据模型和功能。 使用资产HTTP API可以对资产执行各种任务。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 资产 HTTP API {#assets-http-api}

## 概述 {#overview}

资产HTTP API允许对资产执行创建——读取——更新——删除(CRUD)操作，包括二进制、元数据、演绎版和注释，以及使用AEM内容片段的结构化内容。 它在上公开， `/api/assets` 并作为REST API实现。 它包含 [对内容片段的支持](/help/assets/assets-api-content-fragments.md)。

访问API:

1. 在打开API服务文档 `https://[hostname]:[port]/api.json`。
1. 按照以下链接的“资产”服务进行操 `https://[hostname]:[server]/api/assets.json`作。

API响应是某些MIME类型的JSON文件，是所有MIME类型的响应代码。 JSON响应是可选的，可能不可用，例如PDF文件。 依赖响应代码进行进一步的分析或操作。

结束 [!UICONTROL 时间后]，资产及其演绎版不能通过资产Web界面或通过HTTP API使用。 如果开始时间是将来的， [!UICONTROL 或结束时间是过去的] ，则API会返回404 [!UICONTROL 错误消息] 。

## 内容片段 {#content-fragments}

内 [容片段](/help/assets/content-fragments.md) ，是一种特殊类型的资产。 它可用于访问结构化数据，例如文本、数字、日期等。 由于资产(如图像或文档) `standard` 存在若干差异，因此某些其他规则适用于处理内容片段。

有关详细信息， [请参阅AEM Assets HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md)。

## Data model {#data-model}

资产HTTP API公开两个主要元素、文件夹和资产（对于标准资产）。

此外，它还为描述内容片段中结构化内容的自定义数据模型提供更详细的元素。 有关更 [多信息，请参阅内容片段数据模型](/help/assets/assets-api-content-fragments.md#content-fragments) 。

### 文件夹 {#folders}

文件夹类似于传统文件系统中的目录。 它们是其他文件夹或声明的容器。 文件夹具有以下组件：

**实体**:文件夹的实体是其子元素，可以是文件夹和资产。

**属性**:
* `name`  —文件夹的名称。 这与URL路径中没有扩展名的最后一个区段相同
* `title` —可显示的文件夹的可选标题，而非其名称

>[!NOTE]
>
>文件夹或资产的某些属性会映射到其他前缀。 前缀 `jcr` 、和 `jcr:title`的前缀将 `jcr:description`替换为前 `jcr:language``dc` 缀。 因此，在返回的JSON中， `dc:title` 并 `dc:description` 分别包含 `jcr:title` 和的值 `jcr:description`。

**链接** “文件夹”显示三个链接：
* `self`:链接到自身
* `parent`:链接到父文件夹
* `thumbnail`:（可选）指向文件夹缩略图的链接

### 资产 {#assets}

在AEM中，资产包含以下元素：

* 资产的属性和元数据
* 多个演绎版，如原始演绎版（最初上传的资产）、缩略图和各种其他演绎版。 其他再现可能是不同大小的图像、不同的视频编码或从PDF或InDesign中提取的页面。
* 可选注释

有关内容片段中元素的信息，请参 [阅AEM Assets HTTP API中的内容片段支持](/help/assets/assets-api-content-fragments.md#content-fragments)。

在AEM中，文件夹包含以下组件：

* 实体：资产的子项是其演绎版。
* 属性
* 链接

资产HTTP API包括以下功能：

* 检索文件夹列表
* 创建文件夹
* 创建资产
* 更新资产二进制
* 更新资产元数据
* 创建资产再现
* 更新资产演绎版
* 创建资产评论
* 复制文件夹或资产
* 移动文件夹或资产
* 删除文件夹、资产或再现

>[!NOTE]
>
>为了便于读取，以下示例省略了完整的cURL记号。 事实上，该记号确实与 [Resty](https://github.com/micha/resty) （它是的脚本包装器）相关 `cURL`。

**前提条件**

* 转到 `https://[aem_server]:[port]/system/console/configMgr`.
* 导航到 **Adobe Granite CSRF滤镜**。
* 确保属性“过滤 **器方法** ”包括：POST, PUT, DELETE。

## 检索文件夹列表 {#retrieve-a-folder-listing}

检索现有文件夹及其子实体（子文件夹或资源）的Siren表示形式。

**请求**

```
GET /api/assets/myFolder.json
```

**响应代码**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**响应**

返回的实体类是assets/folder。

包含实体的属性是每个实体的全部属性集的子集。 为了获得实体的完整表示形式，客户端应检索链接指向的URL的内容，其中 `rel` 包含 `self`:

## Create a Folder {#create-a-folder}

创建新 `sling`:在给 `OrderedFolder` 定路径。 如果给定*而不是节点名，则servlet将参数名用作节点名。 作为请求数据接受是新文件夹的Siren表示形式或一组名称——值对，编码为或 `application/www-form-urlencoded` / `multipart``form``data`- ，对于直接从HTML表单创建文件夹很有用。 此外，文件夹的属性可以指定为URL查询参数。

如果给定路径的父节 `500` 点不存在，则操作将失败并带有响应代码。 如果文件夹已存在，则 `409` 返回响应代码。

**参数**

* `name` -文件夹名称

**请求**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

或

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**响应代码**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 创建资产 {#create-an-asset}

在给定路径上使用给定文件创建DAM资产。 如果给定*而不是节点名，则servlet将使用参数名或文件名作为节点名。

**参数**

* `name` -资产名称
* `file` -文件引用

**请求**

```
POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"
```

或

```
POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"
```

**响应代码**

```
201 - CREATED - if Asset has been created successfully
409 - CONFLICT - if Asset already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 更新资产二进制文件 {#update-asset-binary}

更新资产二进制（原始名称的再现）。 这将触发默认的资产工作流（如果已配置）。

**请求**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png
```

**响应代码**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 更新资产元数据 {#update-asset-metadata}

更新资产元数据属性。 如果您更新命名空间中的任 `dc:``jcr` 何属性，API将更新命名空间中的同一属性。 API不同步两个命名空间下的属性。

**请求**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**响应代码**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 创建资产演绎版 {#create-an-asset-rendition}

为资产创建新的资产演绎版。 如果未提供请求参数名称，则文件名将用作再现名称。

**参数**

* `name` -演绎版名称
* `file` -文件引用

**请求**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

或

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**响应代码**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 更新资产演绎版 {#update-an-asset-rendition}

更新分别用新的二进制数据替换资产演绎版。

**请求**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**响应代码**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 创建资产评论 {#create-an-asset-comment}

创建新的资产评论。

**参数**

* `message` - 消息
* `annotationData` -注释数据(JSON)

**请求**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**响应代码**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 复制文件夹或资产 {#copy-a-folder-or-asset}

将给定路径下的文件夹或资产复制到新目标。

**请求标题**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**请求**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**响应代码**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 移动文件夹或资产 {#move-a-folder-or-asset}

将给定路径下的文件夹或资产移动到新目标。

**请求标题**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**请求**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**响应代码**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## 删除文件夹、资产或演绎版 {#delete-a-folder-asset-or-rendition}

删除给定路径上的资源(-tree)。

**请求**

```
DELETE /api/assets/myFolder
```

或

```
DELETE /api/assets/myFolder/myAsset.png
```

或

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**响应代码**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```
