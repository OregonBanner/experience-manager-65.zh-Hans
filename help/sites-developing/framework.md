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
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# AEM 标记框架 {#aem-tagging-framework}

要标记内容并使用AEM标记基础结构，请执行以下操作：

* 标记必须作为类型的节点存在 ` [cq:Tag](#tags-cq-tag-node-type)` 在 [分类根节点](#taxonomy-root-node)

* 标记的内容节点的NodeType必须包括 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 此 [标记ID](#tagid) 添加到内容节点的 [`cq:tags`](#tagged-content-cq-tags-property) 属性并解析为类型的节点 ` [cq:Tag](#tags-cq-tag-node-type)`

## 标记：cq：Tag节点类型  {#tags-cq-tag-node-type}

标记声明在存储库中捕获的节点类型为 `cq:Tag.`

标记可以是一个简单的单词（例如，sky），也可以表示分层分类法（例如，水果/苹果，表示普通水果和更具体的苹果）。

标记由唯一的TagID标识。

标记具有可选的中继信息，例如标题、本地化的标题和描述。 如果存在，则应在用户界面中显示标题，而不是TagID。

标记框架还提供了将作者和网站访客限制为仅使用特定的预定义标记的功能。

### 标记特征 {#tag-characteristics}

* 节点类型为 `cq:Tag`
* 节点名称是 ` [TagID](#tagid)`
* 此 ` [TagID](#tagid)` 始终包括 [命名空间](#tag-namespace)

* 可选 `jcr:title` 属性（在UI中显示的标题）

* 可选 `jcr:description` 属性

* 当包含子节点时，称为 [容器标记](#container-tags)
* 存储在存储库中名为的基本路径下方 [分类根节点](#taxonomy-root-node)

### 标记 ID {#tagid}

TagID标识解析为存储库中标记节点的路径。

通常，TagID是以命名空间开头的简写TagID，也可以是以 [分类根节点](#taxonomy-root-node).

标记内容时，如果内容尚不存在，则 ` [cq:tags](#tagged-content-cq-tags-property)` 属性将添加到内容节点，TagID将添加到属性的String数组值。

TagID包含 [命名空间](#tag-namespace) 后跟本地TagID。 [容器标记](#container-tags) 具有表示分类法中层次结构顺序的子标记。 子标记可用于引用与任何本地TagID相同的标记。 例如，允许使用“fruit”标记内容，即使它是带有子标记的容器标记，例如“fruit/apple”和“fruit/banana”。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须 *非* 为类型的节点 `  cq   :Tag`.

在AEM中，基本路径为 `/content/  cq   :tags` 并且根节点的类型为 `  cq   :Folder`.

### 标记命名空间 {#tag-namespace}

命名空间允许您对事物进行分组。 最典型的使用案例是每个（网站）或大型应用程序（例如，WCM、Assets、Communities）都有一个命名空间，但命名空间可用于各种其他需求。 命名空间在用户界面中仅用于显示适用于当前内容的标记（即特定命名空间的标记）的子集。

标记的命名空间是分类子树中的第一级，即紧接在 [分类根节点](#taxonomy-root-node). 命名空间是类型的节点 `cq:Tag` 其父项不是 `cq:Tag`节点类型。

所有标记都有一个命名空间。 如果未指定命名空间，则会将标记分配给默认命名空间TagID `default` (标题为 `Standard Tags),`那是 `/content/cq:tags/default.`

### 容器标记 {#container-tags}

容器标记是类型的节点 `cq:Tag` 包含任意数量和类型的子节点，这使得使用自定义元数据增强标记模型成为可能。

此外，分类法中的容器标记（或超级标记）充当所有子标记的总和。 例如，以水果/苹果标记的内容也被视为以水果标记。 也就是说，搜索带有水果标记的内容还可以找到带有水果/苹果标记的内容。

### 解析标记ID {#resolving-tagids}

如果标记ID包含冒号“：”，则冒号会将命名空间与标记或子分类分开，然后使用普通斜杠“/”进行分隔。 如果标记ID没有冒号，则隐含默认命名空间。

标记的标准且唯一位置位于/content/cq：tags下。

引用不存在的路径或不指向cq：Tag节点的路径的标记被视为无效并被忽略。

下表显示了一些示例TagID、其元素以及TagID如何解析为存储库中的绝对路径：

下表显示了一些示例TagID、其元素以及TagID如何解析为存储库中的绝对路径：

<table>
 <tbody>
  <tr>
   <td><strong>标记 ID<br /> </strong></td>
   <td><strong>命名空间</strong></td>
   <td><strong>本地Id</strong></td>
   <td><strong>容器标记</strong></td>
   <td><strong>叶标记</strong></td>
   <td><strong>存储库<br /> 绝对标记路径</strong></td>
  </tr>
  <tr>
   <td>dam：fruit/apple/braeburn</td>
   <td>dam</td>
   <td>水果/苹果/布雷本</td>
   <td>水果，苹果</td>
   <td>braeburn</td>
   <td>/content/cq：tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>颜色/红色</td>
   <td>默认</td>
   <td>颜色/红色</td>
   <td>颜色</td>
   <td>红色</td>
   <td>/content/cq：tags/default/color/red</td>
  </tr>
  <tr>
   <td>天空</td>
   <td>默认</td>
   <td>天空</td>
   <td>(无)</td>
   <td>天空</td>
   <td>/content/cq：tags/default/sky</td>
  </tr>
  <tr>
   <td>dam：</td>
   <td>dam</td>
   <td>(无)</td>
   <td>(无)</td>
   <td>（无，命名空间）</td>
   <td>/content/cq：tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq：tags/category/car</td>
   <td>类别</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq：tags/category/car</td>
  </tr>
 </tbody>
</table>

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选标题字符串( `jcr:title`)可以通过添加属性来本地化显示的标题 `jcr:title.<locale>`.

有关更多详细信息，请参阅

* [不同语言的标记](/help/sites-developing/building.md#tags-in-different-languages)  — 介绍了API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 介绍如何使用标记控制台

### 访问控制 {#access-control}

标记作为节点存在于下的存储库中 [分类根节点](#taxonomy-root-node). 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定的命名空间中创建标记。

此外，拒绝某些标记或命名空间的读取权限会控制将标记应用于特定内容的能力。

典型做法包括：

* 允许 `tag-administrators` 对所有命名空间的组/角色写入权限(添加/修改 `/content/cq:tags`)。 此组提供开箱即用的AEM。

* 允许用户/作者读取他们应该可以读取的所有命名空间（大多数是所有命名空间）。
* 允许用户/作者写入对标记应由用户/作者自由定义的命名空间的访问权限(下的add_node `/content/cq:tags/some_namespace`)

## 可标记内容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

对于要将标记附加到内容类型的应用程序开发人员，节点的注册([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必须包括 `cq:Taggable` mixin或 `cq:OwnerTaggable` mixin。

此 `cq:OwnerTaggable` mixin，继承自 `cq:Taggable`，用于指示内容可以按所有者/作者进行分类。 在AEM中，它只是 `cq:PageContent` 节点。 此 `cq:OwnerTaggable` 标记框架不需要mixin。

>[!NOTE]
>
>建议仅在聚合内容项的顶级节点（或其jcr：content节点）上启用标记。 示例包括：
>
>* 页面( `cq:Page`)，其中 `jcr:content`节点属于类型 `cq:PageContent` 包括 `cq:Taggable` mixin。
>
>* 资产( `cq:Asset`)，其中 `jcr:content/metadata` 节点始终具有 `cq:Taggable` mixin。
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

此 `cq:tags` 属性是一个字符串数组，用于在作者或网站访客将一个或多个TagID应用于内容时存储它们。 仅当添加到使用定义的节点时，属性才有意义 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin。

>[!NOTE]
>
>要使用AEM标记功能，自定义开发的应用程序不应定义以外的标记属性 `cq:tags`.

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用移动或合并标记时存储库中各种效果的描述 [标记控制台](/help/sites-administering/tags.md)：

* 将标记A移动或合并到标记B中时， `/content/cq:tags`：

   * 标记A未删除，将获得 `cq:movedTo` 属性。
   * 创建标记B（如果移动）并获取 `cq:backlinks` 属性。

* `cq:movedTo` 指向标记B。此属性表示标记A已移动或合并到标记B中。移动标记B会相应地更新此属性。 标记A因此而隐藏，并且仅保留在存储库中以解决指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，内容节点不再指向这些标记。
的特殊值 `cq:movedTo` 属性为 `nirvana`：它会在删除标记时应用，但无法从存储库中删除，因为存在带有标记的子标记 `cq:movedTo` 必须保留下来。

  >[!NOTE]
  >
  >此 `cq:movedTo` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
  >
  >1. 标记用在内容中（这意味着它包含引用）或
  >1. 标记具有已移动的子项。

* `cq:backlinks` 使参照保持向另一个方向。 也就是说，它会保留已移动到标记B或与标记B合并的所有标记的列表。这通常需要保留 `cq:movedTo`属性是标记B移动/合并/删除或标记B激活时的最新属性，在这种情况下，还必须激活其所有反向链接标记。

  >[!NOTE]
  >
  >此 `cq:backlinks` 仅当满足以下任一条件时，属性才会添加到已移动或已合并的标记中：
  >
  >1. 标记用在内容中（这意味着它包含引用）或
  >1. 标记具有已移动的子项。

* 阅读 `cq:tags` 内容节点的属性涉及以下解析：

   1. 如果下没有匹配项 `/content/cq:tags`，则不会返回任何标记。
   1. 如果标记具有 `cq:movedTo` 属性集内，将后跟引用的标记ID。
只要以下标记具有 `cq:movedTo` 属性。

   1. 如果后跟标记不包含 `cq:movedTo` 属性，则读取标记。

* 要在移动或合并标记后发布更改，请 `cq:Tag` 必须复制节点及其所有反向链接：当在标记管理控制台中激活标记时，将自动执行此操作。

* 稍后对页面的 `cq:tags` 属性会自动清理“旧”引用。 由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID，因此会触发此事件。

>[!NOTE]
>
>标记的移动与标记的迁移不同。

## 标记迁移 {#tags-migration}

从6.4开始的Experience Manager存储于 `/content/cq:tags`，它们之前存储在 `/etc/tags`. 但是，如果Adobe Experience Manager已从以前的版本升级，则标记仍会显示在旧位置下 `/etc/tags`. 在升级后的系统中，标记必须迁移至 `/content/cq:tags`.

>[!NOTE]
>
>在标记页面的页面属性中，建议使用标记ID (`geometrixx-outdoors:activity/biking`)而不是对标记基本路径进行硬编码(例如， `/etc/tags/geometrixx-outdoors/activity/biking`)。
>
>要列出标记， `com.day.cq.tagging.servlets.TagListServlet` 可以使用。

>[!NOTE]
>
>建议使用标签管理器API作为资源。

### 如果升级的AEM实例支持TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在组件启动时，TagManager API会检测它是否为升级的AEM实例。 在升级后的系统中，标记存储在 `/etc/tags`.

1. 然后，TagManager API以向后兼容模式运行，这意味着API使用 `/etc/tags` 作为基本路径。 如果没有，则使用新位置 `/content/cq:tags`.

1. 更新标记位置。

1. 将标记迁移到新位置后，请运行以下脚本：

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

该脚本将获取所有具有 `/etc/tags` 在的值中 `cq:movedTo/cq:backLinks` 属性。 然后遍历获取的结果集并解析 `cq:movedTo` 和 `cq:backlinks` 属性值到 `/content/cq:tags` 路径(如果是 `/etc/tags` 在值中检测到)。

### 如果升级后的AEM实例在经典UI上运行 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>经典UI不符合零停机要求，并且不支持新的标记库路径。 如果要使用经典UI，则 `/etc/tags` 必须创建，后接 `cq-tagging` 组件重新启动。

如果TagManager API支持并且在Classic UI中运行已升级的AEM实例：

1. 引用旧标记基本路径一次 `/etc/tags` 替换为使用tagId或新标记位置 `/content/cq:tags`，您可以将标记迁移到新位置 `/content/cq:tags` CRX中，然后重新启动组件。

1. 将标记迁移到新位置后，请运行上述脚本。
