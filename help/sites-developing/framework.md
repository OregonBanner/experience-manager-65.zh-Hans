---
title: AEM 标记框架
description: 标记内容并使用AEM标记基础架构
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 8dafa901bc628ee5e4823e9f8811bf4d09b7e072
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# AEM 标记框架 {#aem-tagging-framework}

标记允许对内容进行分类和整理。 标记可以按命名空间和分类法进行分类。 有关使用标记的详细信息：

* 查看文档 [使用标记](/help/sites-authoring/tags.md) 有关将内容标记为内容作者的信息。
* 查看文档 [管理标记](/help/sites-administering/tags.md) 管理员关于创建和管理标记以及已对哪些内容应用标记的观点。

本文重点介绍支持AEM中标记的基础框架以及如何作为开发人员使用它。

## 简介 {#introduction}

要标记内容并使用AEM标记基础结构，请执行以下操作：

* 标记必须作为类型的节点存在 `[cq:Tag](#tags-cq-tag-node-type)` 在 [分类根节点。](#taxonomy-root-node)

* 标记的内容节点的 `NodeType` 必须包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* 此 [`TagID`](#tagid) 添加到内容节点的 [`cq:tags`](#tagged-content-cq-tags-property) 属性并解析为类型的节点 ` [cq:Tag](#tags-cq-tag-node-type)`.

## 标记：cq：Tag节点类型  {#tags-cq-tag-node-type}

标记声明在存储库中捕获的节点类型为 `cq:Tag`.

标记可以是一个简单的单词(例如， `sky`)或表示分层分类(例如， `fruit/apple`，表示两个通用 `fruit` 以及更具体的 `apple`)。

标记由唯一的TagID标识。

标记具有可选的中继信息，例如标题、本地化的标题和描述。 如果存在，则应在用户界面中显示标题，而不是TagID。

标记框架还提供了将作者和网站访客限制为仅使用特定的预定义标记的功能。

### 标记特征 {#tag-characteristics}

* 节点类型为 `cq:Tag`n
* 节点名称是 [标记ID](#tagid).
* 此 [标记ID](#tagid) 始终包括 [命名空间。](#tag-namespace)
* 此 `jcr:title` 属性（在UI中显示的标题）是可选的。
* 此 `jcr:description` 属性是可选的。
* 当包含子节点时，标记称为 [容器标记。](#container-tags)
* 标记存储在存储库中名为的基本路径的下方 [分类根节点。](#taxonomy-root-node)

由于标记只是JCR节点，因此节点名称当然必须遵守 [JCR命名约定。](naming-conventions.md)

### 标记 ID {#tagid}

TagID标识解析为存储库中标记节点的路径。

通常，TagID是以命名空间开头的简写TagID，也可以是以 [分类根节点。](#taxonomy-root-node)

标记内容时，如果内容尚不存在，则 `[cq:tags](#tagged-content-cq-tags-property)` 属性将添加到内容节点，而TagID将添加到属性的 `String` 数组值。

TagID包含 [命名空间](#tag-namespace) 后跟本地TagID。 [容器标记](#container-tags) 具有表示分类法中层次结构顺序的子标记。 子标记可用于引用与任何本地TagID相同的标记。 例如，使用标记内容 `fruit` 允许，即使它是带有子标记的容器标记也是如此，例如 `fruit/apple` 和 `fruit/banana`.

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点不得为类型的节点 `cq:Tag`.

在AEM中，基本路径为 `/content/cq:tags` 并且根节点的类型为 `cq:Folder`.

### 标记命名空间 {#tag-namespace}

命名空间允许您对事物进行分组。 最典型的使用案例是每个站点（例如，公共、内部和门户）或大型应用程序（例如，WCM、资产、社区）的命名空间。 但命名空间可用于各种其他需求。 命名空间在用户界面中仅用于显示适用于当前内容的标记（即特定命名空间的标记）的子集。

标记的命名空间是分类子树中的第一级，即紧接在 [分类根节点](#taxonomy-root-node). 命名空间是类型的节点 `cq:Tag` 其父项不是 `cq:Tag` 节点类型。

所有标记都有一个命名空间。 如果未指定命名空间，则会将标记分配给默认命名空间TagID `default` 带有标题 `Standard Tags`，即 `/content/cq:tags/default`.

### 容器标记 {#container-tags}

容器标记是类型的节点 `cq:Tag` 包含任意数量和类型的子节点，这使得使用自定义元数据增强标记模型成为可能。

此外，分类法中的容器标记（或超级标记）充当所有子标记的包含项。 例如，使用标记的内容 `fruit/apple` 被视为已标记 `fruit` 也是。 即，搜索标记为的内容 `fruit` 也会找到带有以下标记的内容： `fruit/apple`.

### 解析标记ID {#resolving-tagids}

TagID包含冒号(`:`)，则冒号会将命名空间与标记或子分类分开，该名称用斜杠(`/`)。 如果TagID没有冒号，则隐含默认命名空间。

下面是标记的标准位置（且是唯一位置） `/content/cq:tags`.

标记引用不存在的路径或不指向的路径 `cq:Tag` 节点被视为无效，将被忽略。

下表显示了一些示例TagID、其元素以及TagID如何解析为存储库中的绝对路径：

| 标记 ID | 命名空间 | 本地Id | 容器标记 | 叶标记 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | 无 | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | 无 | 无 | 无，命名空间 | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选标题字符串( `jcr:title`)，则可以通过添加属性来本地化要显示的标题 `jcr:title.<locale>`.

有关更多详细信息，请参阅以下文档：

* [不同语言的标记](/help/sites-developing/building.md#tags-in-different-languages)，其中介绍了API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)，其中介绍了标记控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于下的存储库中 [分类根节点](#taxonomy-root-node). 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定的命名空间中创建标记。

此外，拒绝某些标记或命名空间的读取权限会控制将标记应用于特定内容的能力。

典型做法包括：

* 允许 `tag-administrators` 对所有命名空间的组/角色写入权限(添加/修改 `/content/cq:tags`)。 此组提供开箱即用的AEM。
* 允许用户/作者读取他们应该可以读取的所有命名空间（大多数是所有命名空间）。
* 允许用户/作者写入对标记应由用户/作者自由定义的命名空间的访问权限（在下添加一个节点） `/content/cq:tags/some_namespace`)

## 可标记内容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

对于要将标记附加到内容类型的应用程序开发人员，节点的注册([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必须包括 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin。

此 `cq:OwnerTaggable` mixin，继承自 `cq:Taggable`，用于指示内容可以按所有者/作者进行分类。 在AEM中，它只是 `cq:PageContent` 节点。 此 `cq:OwnerTaggable` 标记框架不需要mixin。

>[!NOTE]
>
>建议仅在聚合内容项目的顶级节点（或在其上）启用标记 `jcr:content` 节点)。 示例包括：
>
>* 页面(`cq:Page`)，其中 `jcr:content`节点属于类型 `cq:PageContent` 包括 `cq:Taggable` mixin
>* 资产( `cq:Asset`)，其中 `jcr:content/metadata` 节点始终具有 `cq:Taggable` mixin
>

### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在于存储库中。 CND表示法定义为JCR文档的一部分 [此处](https://jackrabbit.apache.org/jcr/node-type-notation.html).

AEM中包含的节点类型的基本定义如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## 标记的内容：cq：tags属性 {#tagged-content-cq-tags-property}

此 `cq:tags` 属性是 `String` 数组，用于在作者或网站访客将一个或多个标记ID应用于内容时存储这些标记ID。 仅当添加到使用定义的节点时，属性才有意义 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin。

>[!NOTE]
>
>要使用AEM标记功能，自定义开发的应用程序不应定义以外的标记属性 `cq:tags`.

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用移动或合并标记时存储库中各种效果的描述 [标记控制台](/help/sites-administering/tags.md)：

* 将标记A移动或合并到标记B中时， `/content/cq:tags`：

   * 标记A未删除，将获得 `cq:movedTo` 属性。
   * 创建标记B（如果移动）并获取 `cq:backlinks` 属性。

* `cq:movedTo` 指向标记B。

   * 此属性表示标记A已移动或合并到标记B中。移动标记B会相应地更新此属性。 标记A因此而隐藏，并且仅保留在存储库中以解决指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，内容节点不再指向这些标记。

   * 的特殊值 `cq:movedTo` 属性为 `nirvana`. 它适用于删除标记但无法从存储库中删除标记的情况，因为存在带有标记的子标记 `cq:movedTo` 必须保留下来。

  >[!NOTE]
  >
  >此 `cq:movedTo` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
  >
  >1. 标记用在内容中（这意味着它包含引用）或
  >1. 标记具有已移动的子项。

* `cq:backlinks` 使参照保持向另一个方向。 也就是说，它会保留已移动到标记B或与标记B合并的所有标记的列表。这通常需要保留 `cq:movedTo` 属性是标记B移动/合并/删除或标记B激活时的最新属性，在这种情况下，还必须激活其所有反向链接标记。

  >[!NOTE]
  >
  >此 `cq:backlinks` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
  >
  >1. 标记用在内容中（这意味着它包含引用）或
  >1. 标记具有已移动的子项。

* 阅读 `cq:tags` 内容节点的属性涉及以下分辨率：

   1. 如果下没有匹配项 `/content/cq:tags`，则不会返回任何标记。

   1. 如果标记具有 `cq:movedTo` 属性集内，将后跟引用的标记ID。

      * 只要以下标记具有 `cq:movedTo` 属性。

   1. 如果后跟标记不包含 `cq:movedTo` 属性，则读取标记。

* 要在移动或合并标记后发布更改，请 `cq:Tag` 必须复制节点及其所有反向链接。 当在标记管理控制台中激活标记时，会自动完成此操作。

* 稍后对页面的 `cq:tags` 属性会自动清除旧引用。 由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID，因此会触发此事件。

>[!NOTE]
>
>标记的移动与标记的迁移不同。

## 标记迁移 {#tags-migration}

自Adobe Experience Manager 6.4起，标记存储在 `/content/cq:tags` 而早期版本将标记存储在 `/etc/tags`.

无论何时从6.4之前的版本升级AEM系统，标记都必须迁移到 `/content/cq:tags`. 请参阅文档 [AEM 6.5中的常见存储库重组](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) 了解更多信息。
