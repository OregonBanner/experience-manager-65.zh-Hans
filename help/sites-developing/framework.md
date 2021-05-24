---
title: AEM Tagging Framework
seo-title: AEM Tagging Framework
description: 标记内容并利用AEM标记基础结构
seo-description: 标记内容并利用AEM标记基础结构
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: 标记
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# AEM标记框架{#aem-tagging-framework}

要标记内容并利用AEM标记基础结构，请执行以下操作：

* 标记必须作为[分类根节点](#taxonomy-root-node)下的` [cq:Tag](#tags-cq-tag-node-type)`类型的节点存在

* 标记内容节点的NodeType必须包含[ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* 将[TagID](#tagid)添加到内容节点的[ `cq:tags`](#tagged-content-cq-tags-property)属性中，并解析为` [cq:Tag](#tags-cq-tag-node-type)`类型的节点

## 标记：cq：标记节点类型{#tags-cq-tag-node-type}

标记声明是在`cq:Tag.`类型的节点的存储库中捕获的

标记可以是一个简单的词（如sky）或表示分层分类（如果/苹果，即通用水果和更具体的苹果）。

标记由唯一的标记ID标识。

标记具有可选的元信息，如标题、本地化标题和描述。 标题应在用户界面中显示，而不是TagID（如果存在）。

标记框架还允许限制作者和网站访客仅使用特定的预定义标记。

### 标记特征{#tag-characteristics}

* 节点类型为`cq:Tag`
* 节点名称是` [TagID](#tagid)`的组件
* ` [TagID](#tagid)`始终包含[namespace](#tag-namespace)

* 可选`jcr:title`属性（要在UI中显示的标题）

* 可选`jcr:description`属性

* 包含子节点时，称为[容器标记](#container-tags)
* 存储在名为[分类根节点](#taxonomy-root-node)的基本路径下的存储库中

### 标记 ID {#tagid}

TagID标识可解析为存储库中标记节点的路径。

通常，TagID是以命名空间开头的简写TagID，也可以是从[分类根节点](#taxonomy-root-node)开始的绝对TagID。

标记内容后，如果内容尚不存在，则会将` [cq:tags](#tagged-content-cq-tags-property)`属性添加到内容节点，并将TagID添加到属性的字符串数组值。

TagID由[namespace](#tag-namespace)和本地TagID组成。 [容器](#container-tags) 标记子标记，表示分类中的分层顺序。子标记可用于引用与任何本地TagID相同的标记。 例如，允许使用“fruit”标记内容，即使它是带有子标记的容器标记，例如“fruit/apple”和“fruit/banana”。

### 分类根节点{#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点必须&#x200B;*不*&#x200B;是`  cq   :Tag`类型的节点。

在AEM中，基本路径为`/content/  cq   :tags`，根节点类型为`  cq   :Folder`。

### 标记命名空间{#tag-namespace}

命名空间允许对事件进行分组。 最典型的用例是为每个（网站）（例如公共、内部和门户）或每个较大的应用程序（例如WCM、Assets、Communities）提供命名空间，但命名空间可用于各种其他需求。 命名空间用于用户界面，以仅显示适用于当前内容的标记（即特定命名空间的标记）子集。

标记的命名空间是分类子树中的第一级，即紧靠[分类根节点](#taxonomy-root-node)下的节点。 命名空间是`cq:Tag`类型的节点，其父节点不是`cq:Tag`节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则会将标记分配给默认的命名空间，即TagID `default`（标题为`Standard Tags),`，即`/content/cq:tags/default.`）

### 容器标记{#container-tags}

容器标记是`cq:Tag`类型的节点，包含任意数量的子节点和类型的子节点，这使得可以使用自定义元数据增强标记模型。

此外，分类中的容器标记（或超级标记）用作所有子标记的子总和：例如，用水果/苹果标记的内容也被视为用水果标记，即搜索仅用水果标记的内容也会找到用水果/苹果标记的内容。

### 解析TagID {#resolving-tagids}

如果标记ID包含冒号“：”，则冒号将命名空间与标记或子分类分隔开，然后用正斜杠“/”进行分隔。 如果标记ID没有冒号，则表示默认的命名空间。

标记的标准位置和唯一位置低于/content/cq:tags。

引用非现有路径或未指向cq:Tag节点的路径的标记被视为无效，将被忽略。

下表显示了一些示例TagID、其元素，以及TagID如何解析为存储库中的绝对路径：

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
   <td><strong>存储库<br />绝对标记路径</strong></td>
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

### 标记标题{#localization-of-tag-title}的本地化

当标记包含可选的标题字符串(`jcr:title`)时，可以通过添加属性`jcr:title.<locale>`将标题本地化以显示。

有关更多详细信息，请参阅

* [不同语言的标记](/help/sites-developing/building.md#tags-in-different-languages)  — 描述API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)  — 描述了标记控制台的使用

### 访问控制 {#access-control}

标记作为节点存在于[分类根节点](#taxonomy-root-node)下的存储库中。 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定命名空间中创建标记。

此外，拒绝某些标记或命名空间的读取权限将控制将标记应用于特定内容的功能。

典型做法包括：

* 允许`tag-administrators`组/角色对所有命名空间进行写访问（在`/content/cq:tags`下添加/修改）。 此组附带现成的AEM。

* 允许用户/作者读取所有应可读取的命名空间（大部分）的读取权限。
* 允许用户/作者对用户/作者应可自由定义标记的命名空间进行写入访问（`/content/cq:tags/some_namespace`下的add_node）

## 可标记内容：cq：可标记的混合{#taggable-content-cq-taggable-mixin}

为了使应用程序开发人员将标记附加到内容类型，节点的注册([CND](https://jackrabbit.apache.org/node-type-notation.html))必须包含`cq:Taggable` mixin或`cq:OwnerTaggable` mixin。

从`cq:Taggable`继承的`cq:OwnerTaggable`混合文件旨在指示内容可由所有者/作者分类。 在AEM中，它只是`cq:PageContent`节点的属性。 标记框架不需要`cq:OwnerTaggable`混合。

>[!NOTE]
>
>建议仅在聚合内容项目的顶级节点（或其jcr:content节点）上启用标记。 示例包括：
>
>* 页面(`cq:Page`)，其中`jcr:content`节点类型为`cq:PageContent`，其中包含`cq:Taggable` mixin。
   >
   >
* 资产(`cq:Asset`)，其中`jcr:content/metadata`节点始终具有`cq:Taggable` mixin。

>



### 节点类型表示法(CND){#node-type-notation-cnd}

节点类型定义在存储库中以CND文件形式存在。 CND符号被定义为JCR文档[此处](https://jackrabbit.apache.org/node-type-notation.html)的一部分。

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

`cq:tags`属性是一个字符串数组，用于在作者或网站访客将一个或多个TagID应用于内容时，将其存储起来。 仅当添加到通过`[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin定义的节点时，该属性才有意义。

>[!NOTE]
>
>要利用AEM标记功能，自定义开发的应用程序不应定义标记属性，而不应定义`cq:tags`。

## 移动和合并标记{#moving-and-merging-tags}

以下是使用[标记控制台](/help/sites-administering/tags.md)移动或合并标记时存储库中的效果描述：

* 当标记A被移动或合并到`/content/cq:tags`下的标记B中时：

   * 标记A未被删除，并且会获得`cq:movedTo`属性。
   * 标记B将创建（如果移动）并获取`cq:backlinks`属性。

* `cq:movedTo` 指向标记B。此属性表示标记A已移动或合并到标记B中。移动标记B将相应地更新此属性。因此，标记A是隐藏的，仅保留在存储库中，以解析指向标记A的内容节点中的标记ID。标记垃圾收集器会删除标记A等标记，不再再将内容节点指向它们。
`cq:movedTo`属性的特殊值为`nirvana`:当标记被删除但无法从存储库中删除时，将应用该标记，因为必须保留具有`cq:movedTo`的子标记。

   >[!NOTE]
   >
   >仅当满足以下任一条件时，才会将`cq:movedTo`属性添加到已移动或合并的标记中：
   > 1. 标记用于内容（即包含引用）或
   > 1. 标记包含已移动的子项。


* `cq:backlinks` 使引用沿另一个方向保持，即保留已移动到标记B或与标记B合并的所有标记的列表。这通常是为了在移动/合并/删除标记B以及激 `cq:movedTo`活标记B时使属性保持最新所必需的，在这种情况下，还必须激活其所有后台标记。

   >[!NOTE]
   >
   >仅当满足以下任一条件时，才会将`cq:backlinks`属性添加到已移动或合并的标记中：
   >
   > 1. 标记用于内容（即包含引用）或    >
   > 1. 标记包含已移动的子项。


* 读取内容节点的`cq:tags`属性涉及以下解决方法：

   1. 如果`/content/cq:tags`下没有匹配项，则不返回任何标记。
   1. 如果标记设置了`cq:movedTo`属性，则遵循引用的标记ID。
只要后跟的标记具有`cq:movedTo`属性，就会重复此步骤。

   1. 如果后跟的标记没有`cq:movedTo`属性，则读取该标记。

* 要在移动或合并标记时发布更改，必须复制`cq:Tag`节点及其所有回链接：当标记在标记管理控制台中激活时，将自动完成此操作。

* 稍后对页面`cq:tags`属性的更新会自动清理“old”引用。 之所以触发此事件，是因为通过API解析移动的标记会返回目标标记，从而提供目标标记ID。

>[!NOTE]
>
>标记的移动与标记的迁移不同。

## 标记迁移{#tags-migration}

从Experience Manager6.4开始的标记存储在`/content/cq:tags`下，而之前的标记存储在`/etc/tags`下。 但是，如果Adobe Experience Manager已从以前的版本升级，则标记仍位于旧位置`/etc/tags`下。 在已升级的系统中，需要在`/content/cq:tags`下迁移标记。

>[!NOTE]
>
>在“标记的页面属性”页面中，建议使用标记ID(`geometrixx-outdoors:activity/biking`)，而不是对标记基本路径（例如，`/etc/tags/geometrixx-outdoors/activity/biking`）进行硬编码。
>
>要列出标记，可使用`com.day.cq.tagging.servlets.TagListServlet`。

>[!NOTE]
>
>建议将标签管理器API用作资源。

### 如果已升级的AEM实例支持TagManager API {#upgraded-instance-support-tagmanager-api}

1. 在组件开始时，TagManager API会检测它是否是已升级的AEM实例。 在已升级的系统中，标记存储在`/etc/tags`下。

1. 然后，TagManager API在向后兼容模式下运行，这意味着API使用`/etc/tags`作为基本路径。 如果没有，则使用新位置`/content/cq:tags`。

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

脚本将获取值为`cq:movedTo/cq:backLinks`的所有`/etc/tags`的标记。 然后，它遍历获取的结果集，并将`cq:movedTo`和`cq:backlinks`属性值解析为`/content/cq:tags`路径（在值中检测到`/etc/tags`的情况下）。

### 如果已升级的AEM实例在经典UI {#upgraded-instance-runs-classic-ui}上运行

>[!NOTE]
>
>经典UI不符合零停机时间规范，也不支持新的标记库路径。 如果要使用经典UI，则需要先创建`/etc/tags`组件，然后再重新启动`cq-tagging`组件。

如果AEM实例升级后受TagManager API支持并在经典UI中运行：

1. 使用tagId或新标记位置`/content/cq:tags`替换对旧标记基本路径`/etc/tags`的引用后，您可以在CRX中将标记迁移到新位置`/content/cq:tags`，然后重新启动组件。

1. 将标记迁移到新位置后，运行上述脚本。
