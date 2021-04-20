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
feature: Tagging
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# AEM Tagging Framework {#aem-tagging-framework}

要标记内容并利用AEM Tagging基础结构：

* 标记必须作为[分类根节点](#taxonomy-root-node)下` [cq:Tag](#tags-cq-tag-node-type)`类型的节点存在

* 标记内容节点的NodeType必须包含[ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 将[TagID](#tagid)添加到内容节点的[ `cq:tags`](#tagged-content-cq-tags-property)属性，并解析到类型为` [cq:Tag](#tags-cq-tag-node-type)`的节点

## 标记：cq：标记节点类型{#tags-cq-tag-node-type}

标记的声明捕获在`cq:Tag.`类型节点的存储库中

标签可以是简单的词（例如，sky）或表示分级分类（例如，水果/苹果，即通用水果和更具体的苹果）。

标记由唯一的TagID标识。

标记具有可选的元信息，如标题、本地化标题和描述。 标题应当显示在用户界面中，而不是TagID（如果存在）。

标记框架还允许限制作者和站点访客仅使用特定的预定义标记。

### 标记特征{#tag-characteristics}

* 节点类型为`cq:Tag`
* 节点名称是` [TagID](#tagid)`的组件
* ` [TagID](#tagid)`始终包含[命名空间](#tag-namespace)

* 可选`jcr:title`属性（要在UI中显示的标题）

* 可选`jcr:description`属性

* 包含子节点时，称为[容器标签](#container-tags)
* 存储在名为[分类根节点](#taxonomy-root-node)的基本路径下的存储库中

### 标记 ID {#tagid}

TagID标识解析到存储库中的标记节点的路径。

通常，TagID是从命名空间开始的短TagID，也可以是从[分类根节点](#taxonomy-root-node)开始的绝对TagID。

标记内容时，如果内容尚不存在，则` [cq:tags](#tagged-content-cq-tags-property)`属性将添加到内容节点，而TagID将添加到属性的String数组值。

TagID由[命名空间](#tag-namespace)和本地TagID组成。 [容器](#container-tags) 标签子标签，表示分类中的分层顺序。子标签可用于引用与任何本地TagID相同的标签。 例如，允许用“水果”标记内容，即使它是带有子标签的容器标签，如“水果/苹果”和“水果/香蕉”。

### 分类根节点{#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须&#x200B;*不*&#x200B;为`  cq   :Tag`类型的节点。

在AEM中，基路径为`/content/  cq   :tags`，根节点的类型为`  cq   :Folder`。

### 标记命名空间{#tag-namespace}

命名空间允许对内容进行分组。 最典型的用例是每个（网站）（例如公共、内部和门户）或每个较大的应用程序（例如WCM、资产、社区）具有命名空间，但命名空间可用于各种其他需求。 命名空间在用户界面中用于仅显示适用于当前内容的标签子集(即特定命名空间的标签)。

标记的命名空间是分类子树中的第一级，该子树是紧挨[分类根节点](#taxonomy-root-node)的节点。 命名空间是`cq:Tag`类型的节点，其父节点不是`cq:Tag`节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则将标记分配给默认命名空间，即TagID `default`（标题为`Standard Tags),`，即`/content/cq:tags/default.`）

### 容器标签{#container-tags}

容器标记是`cq:Tag`类型的节点，包含任意数量和类型的子节点，这使得可以使用自定义元数据增强标记模型。

此外，分类中的容器标签（或超标签）用作所有子标签的子总和：例如，用水果/苹果标记的内容也被视为用水果标记，即搜索仅用水果标记的内容也会找到用水果/苹果标记的内容。

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号“：”，则冒号将命名空间与标记或子分类分开，然后用正斜杠“/”分开。 如果标记ID没有冒号，则默示默认命名空间。

标记的标准和唯一位置位于/content/cq:tags下。

引用不指向cq:Tag节点的非现有路径或路径的标记被视为无效并被忽略。

下表显示了一些TagID示例、其元素，以及TagID如何解析为存储库中的绝对路径：

下表显示了一些TagID示例、其元素，以及TagID如何解析为存储库中的绝对路径：
下表显示了一些TagID示例、其元素，以及TagID如何解析为存储库中的绝对路径：

<table>
 <tbody>
  <tr>
   <td><strong>标记 ID<br /> </strong></td>
   <td><strong>命名空间</strong></td>
   <td><strong>本地ID</strong></td>
   <td><strong>容器标签</strong></td>
   <td><strong>Leaf标签</strong></td>
   <td><strong>存储库<br />绝对标记路径</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>坝</td>
   <td>水果/苹果/布雷本</td>
   <td>水果，苹果</td>
   <td>布雷本</td>
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

### 本地化标记标题{#localization-of-tag-title}

当标记包含可选的标题字符串(`jcr:title`)时，可以通过添加属性`jcr:title.<locale>`来本地化显示的标题。

有关详细信息，请参阅

* [不同语言中的标](/help/sites-developing/building.md#tags-in-different-languages) 记 — 描述API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 其中描述了“标记”控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于[分类根节点](#taxonomy-root-node)下的存储库中。 允许或拒绝作者和站点访客在给定命名空间中创建标记，可以通过在存储库中设置适当的ACL。

此外，拒绝某些标签或命名空间的读取权限将控制将标签应用于特定内容的能力。

典型的做法包括：

* 允许`tag-administrators`组/角色写入访问所有命名空间（在`/content/cq:tags`下添加/修改）。 此组随附AEM开箱即用。

* 允许用户/作者读取应可读取的所有命名空间（大部分）。
* 允许用户/作者对用户/作者可自由定义标签的命名空间（`/content/cq:tags/some_namespace`下的add_node）进行写入访问

## 可标记内容：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

为了使应用程序开发者能够将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包括`cq:Taggable`混音或`cq:OwnerTaggable`混音。

继承自`cq:Taggable`的`cq:OwnerTaggable`混音旨在指示内容可由所有者/作者分类。 在AEM中，它只是`cq:PageContent`节点的属性。 标记框架不需要`cq:OwnerTaggable`混音。

>[!NOTE]
>
>建议仅在聚合内容项的顶级节点（或其jcr:content节点）上启用标记。 示例包括：
>
>* 页面(`cq:Page`)，其中`jcr:content`节点的类型为`cq:PageContent`，其中包含`cq:Taggable` mixin。
   >
   >
* 资产(`cq:Asset`)，其中`jcr:content/metadata`节点始终具有`cq:Taggable` mixin。

>



### 节点类型表示法(CND){#node-type-notation-cnd}

存储库中存在节点类型定义（CND文件）。 CND记号定义为JCR文档[此处](https://jackrabbit.apache.org/node-type-notation.html)的一部分。

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

## 标记内容：cq:tags属性{#tagged-content-cq-tags-property}

`cq:tags`属性是一个String数组，当作者或站点访客将一个或多个TagID应用于内容时，它们用于存储这些TagID。 仅当将该属性添加到用`[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin定义的节点时，该属性才有意义。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义`cq:tags`以外的标记属性。

## 移动和合并标记{#moving-and-merging-tags}

以下是使用[标记控制台](/help/sites-administering/tags.md)移动或合并标记时存储库中效果的说明：

* 当标记A被移动或合并到`/content/cq:tags`下的标记B时：

   * 未删除标记A并获取`cq:movedTo`属性。
   * 将创建标记B（在移动时）并获取`cq:backlinks`属性。

* `cq:movedTo` 指向标记B。此属性表示标记A已移动或合并到标记B中。移动标记B将相应地更新此属性。因此，标记A是隐藏的，仅保存在存储库中以解析指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，而不再有指向它们的内容节点。
`cq:movedTo`属性的特殊值为`nirvana`:在删除标记但无法从存储库中删除该标记时应用，因为必须保留具有`cq:movedTo`的子标记。

   >[!NOTE]
   >
   >`cq:movedTo`属性仅在满足以下任一条件时添加到移动或合并的标记：
   > 1. 标记用于内容（即它有引用）或
   > 1. 标记包含已移动的子项。


* `cq:backlinks` 使引用保持在另一个方向，即保留已移动到标记B或与标记B合并的所有标记的列表。这主要是为了使属性在移动/合并/删除标记B以及激活标记B时保持最新，在这种情况下，必须同时激活其所有后台标记。 `cq:movedTo`

   >[!NOTE]
   >
   >`cq:backlinks`属性仅在满足以下任一条件时添加到移动或合并的标记：
   >
   > 1. 标记用于内容（即它有引用）或    >
   > 1. 标记包含已移动的子项。


* 读取内容节点的`cq:tags`属性涉及以下解决方法：

   1. 如果`/content/cq:tags`下没有匹配项，则不返回标记。
   1. 如果标记设置了`cq:movedTo`属性，则引用的标记ID将跟随。
只要后面的标签具有`cq:movedTo`属性，就重复此步骤。

   1. 如果后面的标记没有`cq:movedTo`属性，则读取该标记。

* 要在标记被移动或合并时发布更改，必须复制`cq:Tag`节点及其所有反向链接：在标记管理控制台中激活标记时，会自动执行此操作。

* 稍后对页面的`cq:tags`属性的更新会自动清理“旧”引用。 触发这是因为通过API解析移动的标记会返回目标标记，从而提供目标标记ID。

>[!NOTE]
>
>标记的移动不同于标记的迁移。

## 标记迁移{#tags-migration}

从Experience Manager 6.4开始的标签存储在`/content/cq:tags`下，而之前的标签存储在`/etc/tags`下。 但是，在已从先前版本升级Adobe Experience Manager的情况下，旧位置`/etc/tags`下仍存在标记。 在升级的系统中，需要在`/content/cq:tags`下迁移标记。

>[!NOTE]
>
>在标记页面的“页面属性”中，建议使用标记ID(`geometrixx-outdoors:activity/biking`)，而不是硬编码标记基本路径（例如，`/etc/tags/geometrixx-outdoors/activity/biking`）。
>
>要列表标签，可使用`com.day.cq.tagging.servlets.TagListServlet`。

>[!NOTE]
>
>建议使用标签管理器API作为资源。

### 如果升级的AEM实例支持TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在组件开始,TagManager API会检测它是否是升级的AEM实例。 在升级的系统中，标记存储在`/etc/tags`下。

1. 然后，TagManager API以向后兼容模式运行，这意味着API使用`/etc/tags`作为基本路径。 否则，将使用新位置`/content/cq:tags`。

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

脚本将获取`cq:movedTo/cq:backLinks`属性值中具有`/etc/tags`的所有标记。 然后，它迭代读取的结果集并将`cq:movedTo`和`cq:backlinks`属性值解析为`/content/cq:tags`路径（在该值中检测到`/etc/tags`的情况下）。

### 如果升级的AEM实例在经典UI上运行{#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>经典UI不符合零停机时间要求，也不支持新的标签基础路径。 如果要使用经典UI，则需要先创建`/etc/tags`，然后再重新启动`cq-tagging`组件。

如果AEM实例升级后由TagManager API支持并在经典UI中运行：

1. 使用tagId或新标签位置`/content/cq:tags`替换对旧标签基路径`/etc/tags`的引用后，您可以将标签迁移到CRX中的新位置`/content/cq:tags`，然后重新启动组件。

1. 将标记迁移到新位置后，运行上述脚本。
