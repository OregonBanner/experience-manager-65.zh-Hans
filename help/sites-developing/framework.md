---
title: AEM Tagging Framework
seo-title: AEM Tagging Framework
description: 标记内容并利用AEM Tagging基础结构
seo-description: 标记内容并利用AEM Tagging基础结构
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM Tagging Framework{#aem-tagging-framework}

要标记内容并利用AEM Tagging基础结构，请执行以下操作：

* 标记必须作为分类根节点下的类 ` [cq:Tag](#tags-cq-tag-node-type)` 型节 [点存在](#taxonomy-root-node)

* 标记内容节点的NodeType必须包含混 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 音
* TagID [被添加到内容节点的属](#tagid) 性，并 [`cq:tags`](#tagged-content-cq-tags-property) 解析到类型的节点 ` [cq:Tag](#tags-cq-tag-node-type)`

## 标记：cq：标记节点类型 {#tags-cq-tag-node-type}

标记的声明在存储库中的类型节点中捕获 `cq:Tag.`

标签可以是简单的单词（如sky）或表示分级分类（如果／苹果，即通用水果和更具体的苹果）。

标记由唯一的TagID标识。

标记具有可选的元信息，如标题、本地化的标题和说明。 标题应在用户界面中显示，而不是TagID（如果存在）。

标记框架还允许限制作者和站点访问者仅使用特定的预定义标记。

### 标签特性 {#tag-characteristics}

* 节点类型为 `cq:Tag`
* 节点名称是 ` [TagID](#tagid)`
* 始终 ` [TagID](#tagid)` 包含命名 [空间](#tag-namespace)

* 可选 `jcr:title` 属性（要在UI中显示的标题）

* 可选属 `jcr:description` 性

* 包含子节点时，称为容 [器标记](#container-tags)
* 存储在名为分类根节点的基本路径下 [的存储库中](#taxonomy-root-node)

### 标记 ID {#tagid}

TagID标识解析到存储库中的标记节点的路径。

通常，TagID是以命名空间开始的短记TagID，也可以是从分类根节点开始的绝对 [TagID](#taxonomy-root-node)。

标记内容时，如果内容尚不存在，则将属性添加到内容节点，并将TagID添加到属性的String数组值。 ` [cq:tags](#tagged-content-cq-tags-property)`

TagID由一个命名空 [间](#tag-namespace) ，后跟本地TagID组成。 [容器标签](#container-tags) ，具有表示分类中分层顺序的子标签。 子标记可用于引用与任何本地TagID相同的标记。 例如，允许用“fruit”标记内容，即使它是带有子标签的容器标签，如“fruit/apple”和“fruit/banana”。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点不 *能是* 类型的节点 `  cq   :Tag`。

在AEM中，基本路径为， `/content/  cq   :tags` 根节点的类型为 `  cq   :Folder`。

### 标记命名空间 {#tag-namespace}

命名空间允许对事项进行分组。 最典型的用例是每个(Web)站点（例如，公共、内部和门户）或每个较大的应用程序（例如，WCM、资产、社区）具有命名空间，但命名空间可用于各种其他需求。 在用户界面中使用命名空间以仅显示适用于当前内容的标记子集（即特定命名空间的标记）。

标记的命名空间是分类子树中的第一级，该子树是紧挨分类根节点 [的节点](#taxonomy-root-node)。 命名空间是其父项不是节 `cq:Tag` 点类型的节点类 `cq:Tag`型的节点。

所有标记都有一个命名空间。 如果未指定命名空间，则将标记分配给默认的命名空间，即TagID(标 `default` 题是 `Standard Tags),``/content/cq:tags/default.`

### 容器标签 {#container-tags}

容器标签是包含任意数量和类 `cq:Tag` 型子节点的类型节点，这使得可以使用自定义元数据增强标签模型。

此外，分类中的容器标签（或超级标签）用作所有子标签的子总和：例如，用水果／苹果标记的内容也被视为用水果标记，即搜索仅用水果标记的内容也会找到用水果／苹果标记的内容。

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号“:”，则冒号将命名空间与标记或子分类分开，然后用正斜杠“/”分开。 如果标记ID没有冒号，则默示默认的命名空间。

标记的标准和唯一位置低于/content/cq:tags。

引用不指向cq:Tag节点的非现有路径或路径的标记被视为无效并被忽略。

下表显示了一些示例TagID、其元素，以及TagID解析为存储库中绝对路径的方式：

下表显示了一些示例TagID、其元素，以及TagID解析为存储库中绝对路径的方式：下表显示了一些示例TagID、其元素，以及TagID解析为存储库中绝对路径的方式：

<table>
 <tbody>
  <tr>
   <td><strong>标记 ID<br /> </strong></td>
   <td><strong>命名空间</strong></td>
   <td><strong>本地ID</strong></td>
   <td><strong>容器标签</strong></td>
   <td><strong>Leaf标签</strong></td>
   <td><strong>存储库<br /> “绝对”标记路径</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>坝</td>
   <td>水果／苹果／布雷本</td>
   <td>水果，苹果</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>默认</td>
   <td>color/red</td>
   <td>颜色</td>
   <td>红色</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>天空</td>
   <td>默认</td>
   <td>天空</td>
   <td>(无)</td>
   <td>天空</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>坝</td>
   <td>(无)</td>
   <td>(无)</td>
   <td>(none, namespace)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>类别</td>
   <td>汽车</td>
   <td>汽车</td>
   <td>汽车</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### 标记标题的本地化 {#localization-of-tag-title}

当标记包含可选的标题字符串( `jcr:title`)时，可以通过添加属性来本地化要显示的标题 `jcr:title.<locale>`。

有关详细信息，请参阅

* [不同语言的标记](/help/sites-developing/building.md#tags-in-different-languages) -描述API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages) -介绍了“标记”控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于分类根节 [点下的存储库中](#taxonomy-root-node)。 允许或拒绝作者和站点访问者在给定的命名空间中创建标记可以通过在存储库中设置适当的ACL来实现。

此外，拒绝某些标记或命名空间的读取权限将控制将标记应用到特定内容的能力。

典型做法包括：

* 允许对所 `tag-administrators` 有命名空间(在下添加／修改 `/content/cq:tags`)进行组／角色写入访问。 此组随附AEM现成功能。

* 允许用户／作者对应可读的所有命名空间（大多数）进行读取访问。
* 允许用户／作者对用户／作者可自由定义标记的命名空间进行写入访问(add_node在下 `/content/cq:tags/some_namespace`)

## 可标记内容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括 `cq:Taggable` mixin或mixin `cq:OwnerTaggable` 。

继承 `cq:OwnerTaggable` 自的混音旨在指 `cq:Taggable`示内容可由所有者／作者分类。 在AEM中，它只是节点的一个属 `cq:PageContent` 性。 标记 `cq:OwnerTaggable` 框架不需要混合。

>[!NOTE]
>
>建议仅在聚合内容项的顶级节点（或其jcr:content节点）上启用标记。 示例包括：
>
>* 页( `cq:Page`)其中节 `jcr:content`点的类型包括 `cq:PageContent` 混合的 `cq:Taggable` 节点。
   >
   >
* 资源( `cq:Asset`)节点始终 `jcr:content/metadata` 具有混合的 `cq:Taggable` 位置。
>



### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在在于存储库中。 CND记号在此定义为JCR文档的一 [部分](https://jackrabbit.apache.org/node-type-notation.html)。

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

## 标记内容：cq:tags属性 {#tagged-content-cq-tags-property}

该属 `cq:tags` 性是一个字符串数组，当作者或站点访问者将一个或多个TagID应用于内容时，它们用于存储这些TagID。 仅当属性添加到使用mixin定义的节点时，该属性才有 ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` 意义。

>[!NOTE]
>
>为了利用AEM标记功能，自定义开发的应用程序不应定义除外的标记属性 `cq:tags`。

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用标记控制台移动或合并标记时存储库中效果的 [说明](/help/sites-administering/tags.md):

* 当标记A被移动或合并到标记B时，位于 `/content/cq:tags`:

   * 不会删除标记A并获取属 `cq:movedTo` 性。
   * 将创建标记B（在移动时）并获取属 `cq:backlinks` 性。

* `cq:movedTo` 指向标记B。此属性表示标记A已被移动或合并到标记B中。移动标记B将相应地更新此属性。 因此，标记A是隐藏的，并且仅保存在存储库中以解析指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记（如标记A），不再有内容节点指向它们。
该属性的特殊 `cq:movedTo` 值为 `nirvana`:在删除标记但无法从存储库中删除标记时应用，因为存在必须保留的子标 `cq:movedTo` 记。

   >[!NOTE]
   >
   >仅 `cq:movedTo` 当满足以下任一条件时，属性才添加到已移动或合并的标记：
   > 1. 标记用于内容（即它有引用）或
   > 1. 标记包含已移动的子项。


* `cq:backlinks` 使引用保持在另一个方向，即保留已移至标记B或与标记B合并的所有标记的列表。当标记B被移动／合并／删 `cq:movedTo`除时或标记B被激活时，这通常要求保持属性保持最新，在这种情况下，必须同时激活其所有后移标记。

   >[!NOTE]
   >
   >仅 `cq:backlinks` 当满足以下任一条件时，属性才添加到已移动或合并的标记：
   > 1. 标记用于内容（即它有引用）或
   > 1. 标记包含已移动的子项。


* 读取内 `cq:tags` 容节点的属性涉及以下解决：

   1. 如果下面没有匹配项， `/content/cq:tags`则不返回标记。
   1. 如果标记设置了 `cq:movedTo` 属性，则引用的标记ID将随后显示。
只要后跟的标签有属性，就重复此步 `cq:movedTo` 骤。

   1. 如果后跟的标记没有属 `cq:movedTo` 性，则读取标记。

* 要在移动或合并标记时发布更改，必须复 `cq:Tag` 制节点及其所有后退链接：在标记管理控制台中激活标记时，会自动执行此操作。

* 稍后对页面属性的更 `cq:tags` 新会自动清除“旧”引用。 这是由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID而触发的。
