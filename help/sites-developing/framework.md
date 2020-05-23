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
source-git-commit: 4c4a0b1a76f44dcf1084a4651194e60735bc5aea
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# AEM Tagging Framework {#aem-tagging-framework}

要标记内容并利用AEM Tagging基础结构，请执行以下操作：

* 标记必须作为分类根节点下的类 ` [cq:Tag](#tags-cq-tag-node-type)` 型节 [点存在](#taxonomy-root-node)

* 标记内容节点的NodeType必须包含混 [`cq:Taggable`](#taggable-content-cq-taggable-mixin) 合
* TagID [被添加](#tagid) 到内容节点的属性 [ 并 `cq:tags`](#tagged-content-cq-tags-property) 解析到类型的节点 ` [cq:Tag](#tags-cq-tag-node-type)`

## 标记： cq：标记节点类型  {#tags-cq-tag-node-type}

标记的声明在存储库中的类型节点中捕获 `cq:Tag.`

标记可以是简单的单词（如sky）或表示分级分类（如果／苹果，即通用水果和更具体的苹果）。

标记由唯一的TagID标识。

标记具有可选的元信息，如标题、本地化标题和说明。 标题应在用户界面中显示，而不是TagID（如果存在）。

标记框架还允许限制作者和站点访客仅使用特定的预定义标记。

### 标签特性 {#tag-characteristics}

* 节点类型为 `cq:Tag`
* 节点名称是 ` [TagID](#tagid)`
* 总 ` [TagID](#tagid)` 是包含 [命名空间](#tag-namespace)

* 可选 `jcr:title` 属性（要在UI中显示的标题）

* 可选属 `jcr:description` 性

* 包含子节点时，称为 [容器标记](#container-tags)
* 存储在名为分类根节点的基路径 [下的存储库中](#taxonomy-root-node)

### 标记 ID {#tagid}

TagID标识解析到存储库中的标记节点的路径。

通常，TagID是以命名空间开头的短格式TagID，也可以是从分类根节点开始的 [绝对TagID](#taxonomy-root-node)。

标记内容时，如果内容尚不存在，则 ` [cq:tags](#tagged-content-cq-tags-property)` 将属性添加到内容节点，并将TagID添加到属性的String数组值。

TagID由命名空间 [和](#tag-namespace) 本地TagID组成。 [容器标](#container-tags) 签具有子标签，这些子标签表示分类中的分层顺序。 子标记可用于引用与任何本地TagID相同的标记。 例如，允许用“水果”标记内容，即使它是带有子标签的容器标签，如“水果／苹果”和“水果／香蕉”。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点不 *能* 是类型的节点 `  cq   :Tag`。

在AEM中，基本路径 `/content/  cq   :tags` 为，根节点类型为 `  cq   :Folder`。

### 标记命名空间 {#tag-namespace}

命名空间允许将事物分组。 最典型的用例是每个（网站）或每个较大的应用程序（如WCM、资产、社区）都有命名空间（例如，公共、内部和门户），但命名空间可用于其他各种需求。 命名空间用于用户界面中，以仅显示适用于当前内容的标记子集(即特定命名空间的标记)。

标记的命名空间是分类子树中的第一级，该子树是紧挨分类根节点 [的节点](#taxonomy-root-node)。 命名空间是父代不是节 `cq:Tag` 点类型的节 `cq:Tag`点类型。

所有标记均具有命名空间。 如果未指定命名空间，则标记将分配给默认命名空间，即TagID(标 `default` 题是 `Standard Tags),``/content/cq:tags/default.`

### 容器标记 {#container-tags}

容器标签是包含任意数 `cq:Tag` 量和子节点类型的节点，它使用自定义元数据增强标签模型成为可能。

此外，分类中的容器标签（或超级标签）用作所有子标签的子总和： 例如，用水果／苹果标记的内容也被视为用水果标记，即搜索仅用水果标记的内容也会找到用水果／苹果标记的内容。

### 解析标记ID {#resolving-tagids}

如果标记ID包含冒号“:”，冒号将命名空间与标记或子分类分开，然后用正斜杠“/”分开。 如果标记ID没有冒号，则默示默认命名空间。

标记的标准位置和唯一位置在/content/cq:tags下。

引用不指向cq:Tag节点的非现有路径或路径的标记被视为无效并被忽略。

下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：

下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：
下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：

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
   <td>braburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>默认</td>
   <td>color/red</td>
   <td>颜色</td>
   <td>红</td>
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
   <td>(无，命名空间)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/类别/car</td>
   <td>类别</td>
   <td>汽车</td>
   <td>汽车</td>
   <td>汽车</td>
   <td>/content/cq:tags/类别/car</td>
  </tr>
 </tbody>
</table>

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选的标题字符串() `jcr:title`时，可以通过添加属性来本地化要显示的标题 `jcr:title.<locale>`。

有关详细信息，请参阅

* [不同语言的标](/help/sites-developing/building.md#tags-in-different-languages) 记——描述API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages) -介绍了“标记”控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于分类根节 [点下的存储库中](#taxonomy-root-node)。 允许或拒绝作者和站点访客在给定命名空间中创建标记，可以通过在存储库中设置适当的ACL。

此外，拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的能力。

典型做法包括：

* 允许对 `tag-administrators` 所有命名空间（在下添加／修改）进行组／角色写入 `/content/cq:tags`访问。 此组随附AEM现成功能。

* 允许用户／作者读取应可读的所有命名空间（大多数）。
* 允许用户／作者对用户／作者可自由定义标记的命名空间进行写入访问(在下面添加节点 `/content/cq:tags/some_namespace`)

## 可标记内容： cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包含 `cq:Taggable` 混合或混 `cq:OwnerTaggable` 合。

继承 `cq:OwnerTaggable` 自的混音旨在 `cq:Taggable`指示内容可由所有者／作者进行分类。 在AEM中，它只是节点的属 `cq:PageContent` 性。 标 `cq:OwnerTaggable` 记框架不需要混合。

>[!NOTE]
>
>建议仅在聚集内容项的顶级节点（或其jcr:content节点）上启用标记。 示例包括：
>
>* 页面( `cq:Page`)其中节 `jcr:content`点的类型 `cq:PageContent` 包括混 `cq:Taggable` 合。
   >
   >
* 资产( `cq:Asset`)节点始 `jcr:content/metadata` 终具有混合的 `cq:Taggable` 位置。
>



### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在在存储库中。 CND记号在此定义为JCR文档的一 [部分](https://jackrabbit.apache.org/node-type-notation.html)。

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

## 标记内容： cq:tags属性 {#tagged-content-cq-tags-property}

该属 `cq:tags` 性是一个字符串数组，当作者或站点访客将一个或多个TagID应用于内容时，它们用于存储这些TagID。 仅当添加到使用mixin定义的节点时，该属性才具有 `[cq:Taggable](#taggable-content-cq-taggable-mixin)` 意义。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义除外的标记属性 `cq:tags`。

## 移动和合并标记 {#moving-and-merging-tags}

以下是使用标记控制台移动或合并标记时存储库中效果 [的说明](/help/sites-administering/tags.md):

* 当标记A被移动或合并到标记B下时 `/content/cq:tags`:

   * 标记A未被删除，并获取属 `cq:movedTo` 性。
   * 将创建标记B（在移动时）并获取属 `cq:backlinks` 性。

* `cq:movedTo` 指向标记B。此属性意味着标记A已被移动或合并到标记B中。移动标记B将相应地更新此属性。 因此，标记A是隐藏的，它仅保存在存储库中以解析指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，而不再有其他内容节点指向它们。
该属性的特殊 `cq:movedTo` 值是 `nirvana`: 在删除标记但无法从存储库中删除该标记时应用该标记，因为存在必须 `cq:movedTo` 保留的子标记。

   >[!NOTE]
   >
   >仅当 `cq:movedTo` 满足以下任一条件时，属性才会添加到已移动或合并的标记：
   > 1. 标记用于内容（即它有引用）或
   > 1. 标记包含已移动的子项。


* `cq:backlinks` 使引用保持在另一个方向，即保留已移动到标记B或与标记B合并的所有标记的列表。这通常要求在移动／合并／删除标记B以及激活标记B时使属性保持最新，在这种情况下，必须同时激活其所有背景标记。 `cq:movedTo`

   >[!NOTE]
   >
   >仅当 `cq:backlinks` 满足以下任一条件时，属性才会添加到已移动或合并的标记：
   >
   > 1. 标记用于内容（即它有引用）或>
   > 1. 标记包含已移动的子项。


* 读取内 `cq:tags` 容节点的属性涉及以下解决：

   1. 如果下面没有匹配项， `/content/cq:tags`则不返回任何标记。
   1. 如果标记设置了 `cq:movedTo` 属性，则引用的标记ID会随后显示。
只要后跟的标记具有属性，则重复此 `cq:movedTo` 步骤。

   1. 如果后面的标记没有属 `cq:movedTo` 性，则会读取标记。

* 要在标记被移动或合并后发布更改，必须 `cq:Tag` 复制节点及其所有反向链接： 在标记管理控制台中激活标记时，会自动执行此操作。

* 稍后对页面属性的更 `cq:tags` 新会自动清除“旧”引用。 这是由于通过API解析移动的标记会返回目标标记，从而提供目标标记ID而触发的。

> [!NOTE]
>
> 标记的移动不同于标记的迁移。

## 标记迁移 {#tags-migration}

从Experience Manager 6.4开始，标记存储在 `/content/cq:tags`下面，之前存储在下面 `/etc/tags`。 但是，在Adobe Experience Manager从先前版本升级的情况下，旧位置下仍会显示标记 `/etc/tags`。 在升级的系统中，需要在下迁移标记 `/content/cq:tags`。

> [!NOTE]
> 在标记页面的“页面属性”中，建议使用标记ID(`geometrixx-outdoors:activity/biking`)，而不是对标记基础路径进行硬编码(例如 `/etc/tags/geometrixx-outdoors/activity/biking`)。
> 要列表标 `com.day.cq.tagging.servlets.TagListServlet` 记，可使用。

> [!NOTE]
> 建议将标签管理器API用作资源。

### 如果升级的AEM实例支持TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在组件开始,TagManager API会检测它是否是升级的AEM实例。 在升级的系统中，标记存储在下 `/etc/tags`。

1. 然后，TagManager API以向后兼容模式运行，这意味着API `/etc/tags` 用作基本路径。 否则，将使用新位置 `/content/cq:tags`。

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

脚本将获取属性值中 `/etc/tags` 包含的所有标 `cq:movedTo/cq:backLinks` 记。 然后，它重新迭代获取的结果集，并 `cq:movedTo` 将 `cq:backlinks` 和属性值解析 `/content/cq:tags` 为路径(在值中检测到 `/etc/tags` 的情况下)。

### 如果升级的AEM实例在经典UI上运行 {#upgraded-instance-runs-classic-ui}

> [!NOTE]
> 经典UI不符合零停机时间要求，并且不支持新的标签基础路径。 如果要使用经典UI，则需 `/etc/tags` 要创建经典UI，然后重新启 `cq-tagging` 动组件。


如果TagManager API支持并在经典UI中运行的已升级AEM实例：

1. 使用tagId或新标记位置替 `/etc/tags` 换对旧标记基本路径的引用后， `/content/cq:tags`您可以在CRX中将标记迁移到新 `/content/cq:tags` 位置，然后重新启动组件。

1. 将标记迁移到新位置后，运行上述脚本。
