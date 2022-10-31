---
title: AEM 标记框架
seo-title: AEM Tagging Framework
description: 标记内容并利用AEM标记基础结构
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: efb4f9f8a97baf8d3d02160226e4f4d3f8f64c89
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# AEM 标记框架 {#aem-tagging-framework}

要标记内容并利用AEM标记基础结构，请执行以下操作：

* 标记必须作为类型的节点存在 ` [cq:Tag](#tags-cq-tag-node-type)` 下 [分类根节点](#taxonomy-root-node)

* 标记内容节点的NodeType必须包含 [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) 混合
* 的 [TagID](#tagid) 添加到内容节点的 [ `cq:tags`](#tagged-content-cq-tags-property) 属性并解析为类型的节点 ` [cq:Tag](#tags-cq-tag-node-type)`

## 标记：cq：标记节点类型  {#tags-cq-tag-node-type}

标记声明是在类型节点的存储库中捕获的 `cq:Tag.`

标记可以是一个简单的词（如sky）或表示分层分类（如果/苹果，即通用水果和更具体的苹果）。

标记由唯一的标记ID标识。

标记具有可选的元信息，如标题、本地化标题和描述。 标题应在用户界面中显示，而不是TagID（如果存在）。

标记框架还允许限制作者和网站访客仅使用特定的预定义标记。

### 标记特性 {#tag-characteristics}

* 节点类型为 `cq:Tag`
* 节点名称是 ` [TagID](#tagid)`
* the ` [TagID](#tagid)` 始终包含 [命名空间](#tag-namespace)

* 可选 `jcr:title` 属性（要在UI中显示的标题）

* 可选 `jcr:description` 属性

* 包含子节点时，称为 [容器标记](#container-tags)
* 存储在存储库中名为 [分类根节点](#taxonomy-root-node)

### 标记 ID {#tagid}

TagID标识可解析为存储库中标记节点的路径。

通常，TagID是以命名空间开头的速记TagID，也可以是从 [分类根节点](#taxonomy-root-node).

当内容已标记时，如果内容尚不存在，则 ` [cq:tags](#tagged-content-cq-tags-property)` 属性会添加到内容节点，而TagID则会添加到属性的字符串数组值。

TagID由 [命名空间](#tag-namespace) 后跟本地TagID。 [容器标记](#container-tags) 具有表示分类中分层顺序的子标记。 子标记可用于引用与任何本地TagID相同的标记。 例如，允许使用“fruit”标记内容，即使它是带有子标记的容器标记，如“fruit/apple”和“fruit/banana”。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须 *not* 是一种 `  cq   :Tag`.

在AEM中，基本路径为 `/content/  cq   :tags` 根节点是 `  cq   :Folder`.

### 标记命名空间 {#tag-namespace}

命名空间允许对事件进行分组。 最典型的用例是为每个（网站）（例如公共、内部和门户）或每个较大的应用程序（例如WCM、资产、社区）提供命名空间，但命名空间可用于各种其他需求。 命名空间用于用户界面，以仅显示适用于当前内容的标记（即特定命名空间的标记）子集。

标记的命名空间是分类子树中的第一个级别，即紧靠 [分类根节点](#taxonomy-root-node). 命名空间是类型的节点 `cq:Tag` 其父项 `cq:Tag`节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则会将标记分配给默认的命名空间，即TagID `default` (标题为 `Standard Tags),`表示 `/content/cq:tags/default.`

### 容器标记 {#container-tags}

容器标记是类型的节点 `cq:Tag` 包含任意数量和类型的子节点，从而可以使用自定义元数据增强标记模型。

此外，分类中的容器标记（或超级标记）用作所有子标记的子总和：例如，用水果/苹果标记的内容也被视为用水果标记，即搜索仅用水果标记的内容也会找到用水果/苹果标记的内容。

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号“：”，则冒号将命名空间与标记或子分类分隔开，然后用正斜杠“/”进行分隔。 如果标记ID没有冒号，则表示默认的命名空间。

标记的标准位置和唯一位置低于/content/cq:tags。

引用非现有路径或未指向cq:Tag节点的路径的标记被视为无效，将被忽略。

下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：

下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：

<table>
 <tbody>
  <tr>
   <td><strong>标记 ID<br /> </strong></td>
   <td><strong>命名空间</strong></td>
   <td><strong>本地ID</strong></td>
   <td><strong>容器标记</strong></td>
   <td><strong>叶标签</strong></td>
   <td><strong>存储库<br /> 绝对标记路径</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braburn</td>
   <td>dam</td>
   <td>水果/苹果/布雷本</td>
   <td>水果、苹果</td>
   <td>布拉本</td>
   <td>/content/cq:tags/dam/fruit/apple/braburn</td>
  </tr>
  <tr>
   <td>颜色/红色</td>
   <td>默认</td>
   <td>颜色/红色</td>
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
   <td>dam</td>
   <td>(无)</td>
   <td>(无)</td>
   <td>（无，命名空间）</td>
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

当标记包含可选的标题字符串( `jcr:title`)可通过添加属性将标题本地化以显示 `jcr:title.<locale>`.

有关更多详细信息，请参阅

* [不同语言的标记](/help/sites-developing/building.md#tags-in-different-languages)  — 描述API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 描述标记控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于 [分类根节点](#taxonomy-root-node). 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定命名空间中创建标记。

此外，拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的功能。

典型做法包括：

* 允许 `tag-administrators` 组/角色对所有命名空间的写入权限(在 `/content/cq:tags`)。 此组附带现成的AEM。

* 允许用户/作者读取所有应可读取的命名空间（大部分）的读取权限。
* 允许用户/作者对用户/作者应可自由定义标记的命名空间（下的add_node）进行写入访问 `/content/cq:tags/some_namespace`)

## 可标记内容：cq：可标记的Mixin {#taggable-content-cq-taggable-mixin}

为了让应用程序开发人员将标记附加到内容类型，节点会注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括 `cq:Taggable` mixin或 `cq:OwnerTaggable` 混合。

的 `cq:OwnerTaggable` mixin，继承自 `cq:Taggable`，旨在指示内容可以由所有者/作者分类。 在AEM中，它只是 `cq:PageContent` 节点。 的 `cq:OwnerTaggable` 标记框架不需要mixin。

>[!NOTE]
>
>建议仅在聚合内容项目的顶级节点（或其jcr:content节点）上启用标记。 示例包括：
>
>* 页面( `cq:Page`)其中 `jcr:content`节点类型 `cq:PageContent` 包括 `cq:Taggable` 混合。
>
>* 资产( `cq:Asset`)其中 `jcr:content/metadata` 节点始终具有 `cq:Taggable` 混合。
>


### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义在存储库中以CND文件形式存在。 CND符号被定义为JCR文档的一部分 [此处](https://jackrabbit.apache.org/node-type-notation.html).

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

的 `cq:tags` 属性是一个字符串数组，用于在作者或网站访客将一个或多个标记ID应用于内容时存储这些标记ID。 仅当添加到通过 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` 混合。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义标记属性，而 `cq:tags`.

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用移动或合并标记时存储库中的效果描述 [标记控制台](/help/sites-administering/tags.md):

* 将标记A移动或合并到 `/content/cq:tags`:

   * 标记A未删除，并会 `cq:movedTo` 属性。
   * 标记B（如果移动），将获得 `cq:backlinks` 属性。

* `cq:movedTo` 指向标记B。此属性表示标记A已移动或合并到标记B中。移动标记B将相应地更新此属性。 因此，标记A是隐藏的，仅保留在存储库中，以解析指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，不再再将内容节点指向它们。
的特殊值 `cq:movedTo` 属性 `nirvana`:标记被删除后会应用，但无法从存储库中删除，因为存在带有 `cq:movedTo` 必须保留。

   >[!NOTE]
   >
   >的 `cq:movedTo` 仅当满足以下任一条件时，才会将属性添加到已移动或已合并的标记中：
   >
   >1. 标记用于内容（即包含引用）或
   >1. 标记包含已移动的子项。


* `cq:backlinks` 将引用保持为相反方向，即保留已移动到标记B或与标记B合并的所有标记的列表。这通常是在 `cq:movedTo`属性。

   >[!NOTE]
   >
   >的 `cq:backlinks` 仅当满足以下任一条件时，才会将属性添加到已移动或已合并的标记中：
   >
   >1. 标记用于内容（即包含引用）或
   >1. 标记包含已移动的子项。


* 阅读 `cq:tags` 内容节点的属性涉及以下解析：

   1. 如果下没有匹配项 `/content/cq:tags`，则不会返回任何标记。
   1. 如果标记具有 `cq:movedTo` 属性设置时，引用的标记ID会跟在后面。
只要跟随的标记具有 `cq:movedTo` 属性。

   1. 如果跟随的标记没有 `cq:movedTo` 属性中，将读取标记。

* 要在移动或合并标记后发布更改，请 `cq:Tag` 节点及其所有后台链接都必须复制：当标记在标记管理控制台中激活时，将自动完成此操作。

* 稍后对页面的 `cq:tags` 属性会自动清除“旧”引用。 之所以触发此事件，是因为通过API解析移动的标记会返回目标标记，从而提供目标标记ID。

>[!NOTE]
>
>标记的移动与标记的迁移不同。

## 标记迁移 {#tags-migration}

Experience Manager6.4之后的标记存储在 `/content/cq:tags`，而之前在 `/etc/tags`. 但是，如果Adobe Experience Manager已从以前的版本升级，则标记仍位于旧位置下 `/etc/tags`. 在已升级的系统中，需要在 `/content/cq:tags`.

>[!NOTE]
>
>在标记页面的“页面属性”中，建议使用标记ID(`geometrixx-outdoors:activity/biking`)，而不是硬编码标记基本路径(例如， `/etc/tags/geometrixx-outdoors/activity/biking`)。
>
>要列出标记， `com.day.cq.tagging.servlets.TagListServlet` 中。

>[!NOTE]
>
>建议将标签管理器API用作资源。

### 如果升级的AEM实例支持TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在组件开始时，TagManager API会检测它是否是已升级的AEM实例。 在升级后的系统中，标记存储在 `/etc/tags`.

1. 然后，TagManager API在向后兼容性模式下运行，这意味着API使用 `/etc/tags` 作为基本路径。 如果没有，则使用新位置 `/content/cq:tags`.

1. 更新标记位置。

1. 将标记迁移到新位置后，运行以下脚本：

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

脚本会获取所有具有 `/etc/tags` 的值 `cq:movedTo/cq:backLinks` 属性。 然后，它遍历获取的结果集并解析 `cq:movedTo` 和 `cq:backlinks` 属性值 `/content/cq:tags` 路径(在 `/etc/tags` 在值中检测)。

### 如果已升级的AEM实例在经典UI上运行 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>经典UI不符合零停机时间规范，也不支持新的标记库路径。 如果您要使用经典UI，但 `/etc/tags` 需要创建，然后 `cq-tagging` 组件重新启动。

如果AEM实例升级后受TagManager API支持并在经典UI中运行：

1. 对旧标记基本路径的引用 `/etc/tags` 替换为使用tagId或新标记位置 `/content/cq:tags`，则可以将标记迁移到新位置 `/content/cq:tags` 在CRX中，然后重新启动组件。

1. 将标记迁移到新位置后，运行上述脚本。
