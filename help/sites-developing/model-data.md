---
title: 数据建模- David Nuescheler的模型
seo-title: 数据建模- David Nuescheler的模型
description: David Nuescheler的内容建模推荐
seo-description: David Nuescheler的内容建模推荐
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 数据建模- David Nuescheler的模型{#data-modeling-david-nuescheler-s-model}

## 源 {#source}

以下是David Nuescheler所表达的观点和评论。

Day Software AG是Day Software AG的联合创始人兼CTO,Day Software AG是全球内容管理和内容基础架构软件的领先提供商，Adobe于2010年收购了该软件。 他现在是Adobe企业技术部的同事兼副总裁，并领导了JSR-170(Java内容存储库(JCR)应用程序编程接口(API))的开发，JSR-170是内容管理的技术标准。

有关更新的信息，请访问https://wiki.apache.org/jackrabbit/DavidsModel [查看](https://wiki.apache.org/jackrabbit/DavidsModel)。

## David简介 {#introduction-from-david}

在各种讨论中，我发现，在内容建模方面，开发人员对JCR提供的特性和功能有些不安。 在如何在存储库中对内容进行建模以及为什么一个内容模型比另一个更好方面，目前尚无指南和很少的经验。

虽然在关系世界中，软件行业在如何建模数据方面拥有大量经验，但我们仍处于内容存储库空间的早期阶段。

我希望通过就内容的建模方式发表个人意见来填补这一空白，希望有朝一日它能够成为对开发者群体更有意义的东西，这不仅仅是“我的意见”，而且更普遍地适用。 因此，请考虑一下我快速演变的第一次尝试。

>[!NOTE]
>
>免责声明：这些准则表达了我个人、有时还有争议的观点。 我期待对这些准则进行辩论和完善。

## 七条简单规则 {#seven-simple-rules}

### 规则1:数据优先，结构稍后。 也许吧。 {#rule-data-first-structure-later-maybe}

#### 说明 {#explanation-1}

我建议不要担心在ERD意义上声明的数据结构。 最初。

了解如何喜欢nt：非结构化（和朋友）的开发。

我想斯蒂法诺对这个概括很清楚。

我的底线是：结构昂贵，在很多情况下，完全不必向底层存储显式声明结构。

您的应用程序本身就使用了一个关于结构的隐式合同。 假设我将博客文章的修改日期存储在lastModified属性中。 我的应用程序将自动知道从同一属性中再次读取修改日期，因此实际上无需明确声明该日期。

出于数据完整性原因，应仅在需要时应用其他数据约束（如强制或类型和值约束）。

#### 示例 {#example-1}

上述在“blog post”节点上使用 `lastModified` Date属性的示例实际上并不表示需要特殊的nodetype。 我肯定至少最 `nt:unstructured` 初会用于我的博客帖子节点。 因为在我的博客应用程序中，我要做的就是显示lastModified日期（也许是“订购日期”），我根本不在乎它是否为“日期”。 由于我隐含地信任博客编写应用程序在那里放置一个“日期”，因此，真的不需要以nodetype的形式声明某个日期的存在。 `lastModified`

### 规则2:推动内容层次，不要让其发生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 说明 {#explanation-2}

内容层次结构是非常有价值的资产。 所以，不要只是让它发生，设计它。 如果某个节点没有“好”的、可读的名称，那么这可能是你应该重新考虑的。 武断的数字从来都不是“好名字”。

虽然将现有的关系模型快速放入分层模型可能非常容易，但在这个过程中应该考虑一下。

根据我的经验，如果考虑访问控制和限制通常是内容层次结构的好驱动因素。 将其想象成是您的文件系统。 甚至可以使用文件和文件夹在本地磁盘上对其进行建模。

个人而言，在最初的很多情况下，我更喜欢层次结构惯例而不是注释输入系统，稍后再介绍输入。

>[!CAUTION]
>
>内容存储库的结构方式也会影响性能。 为获得最佳性能，附加到内容存储库中各个节点的子节点数通常不应超过1&#39;000。
>
>请参 [阅CRX可以处理多少数据？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 的双曲余切值。

#### 示例 {#example-2}

我将建立一个简单的博客系统，如下所示。 请注意，最初我甚至不关心我目前使用的各个节点类型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我认为一个显而易见的事实是我们都理解内容的结构基于示例而没有任何进一步的解释。

最初可能意想不到的是，为什么我不会将“评论”与“帖子”一起存储，这是由于访问控制，我希望以合理的分级方式应用该控制。

使用上述内容模型，我可以轻松允许“匿名”用户“创建”评论，但将匿名用户保留为只读状态，以便在工作区的其余部分使用。

### 规则3:工作区适用于clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 说明 {#explanation-3}

如果您不在应用程 `clone()`序中 `merge()` 使用 `update()` 或方法，则可能需要单个工作区。

“对应节点”是JCR规范中定义的概念。 本质上，它归结于表示不同所谓工作区中相同内容的节点。

JCR引入了非常抽象的Workspaces概念，这使得许多开发者不清楚如何处理这些工作。 我建议将您对工作区的使用情况进行以下测试。

如果多个工作区中“对应”节点（实质上是具有相同UUID的节点）存在相当大的重叠，您可能会将工作区用到适当位置。

如果节点与UUID没有重叠，则您可能滥用工作区。

不应使用工作区进行访问控制。 对于特定用户组，内容的可见性不是将内容分离到不同工作区的好参数。 JCR在内容存储库中提供“访问控制”功能来提供此功能。

工作区是引用和查询的边界。

#### 示例 {#example-3}

将工作区用于以下事项：

* v1.2与v1.3
* “开发”、“QA”和“已发布”的内容状态

请勿将工作区用于以下事项：

* 用户主目录
* 针对不同目标受众（如公共、私有、本地、...）的不同内容
* 适用于不同用户的邮箱

### 规则4:注意同名同级。 {#rule-beware-of-same-name-siblings}

#### 说明 {#explanation-4}

虽然同名同级(SNS)已引入规范中，以允许与为XML设计并通过XML表示的数据结构兼容，因此对JCR非常有价值，但SNS为存储库带来了大量的开销和复杂性。

如果SNS被删除或重新排序，则进入其路径段中包含SNS的内容存储库的任何路径都变得不那么稳定，这会影响所有其他SNS及其子项的路径。

为了导入XML或与现有XML SNS进行交互，可能既必要又有用，但我从未使用过SNS，而且永远不会在“绿色字段”数据模型中使用。

#### 示例 {#example-4}

用法

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

而不是

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 规则5:引用被认为有害。 {#rule-references-considered-harmful}

#### 说明 {#explanation-5}

引用暗示了参照完整性。 我发现，重要的是要了解，引用不仅为管理引用完整性的存储库增加了额外成本，而且从内容灵活性的角度来说，它们也代价高昂。

我个人确保只有在我真的无法处理悬挂引用时才使用引用，否则，请使用路径、名称或字符串UUID引用其他节点。

#### 示例 {#example-5}

假设我允许从文档(a)到另一个文档(b)的“引用”。 如果我使用引用属性来建模此关系，这意味着两个文档在存储库级别上链接。 我无法单独导出／导入文档(a)，因为引用属性的目标可能不存在。 其他操作（如合并、更新、恢复或克隆）也会受到影响。

因此，我要么将这些引用建模为“weak-references”（在JCR v1.0中，这基本上归结为包含目标节点的uuid的字符串属性），要么只使用路径。 有时，路径的开头更有意义。

我认为，有些使用案例，如果某个系统的参考信息晃荡不定，它们真的无法工作，但我无法从我的直接经验中得出一个好的“真实”而简单的例子。

### 规则6:文件是文件。 {#rule-files-are-files}

#### 说明 {#explanation-6}

如果内容模型公开的东西闻起来 *甚至有点像* ，比如我试图使用（或从中扩展）的文件或文件夹 `nt:file`, `nt:folder` 以及 `nt:resource`。

在我的经验中，许多通用应用程序都允许与nt:folder和nt：文件进行隐式交互，并且知道如果这些事件富含其他元信息，如何处理和显示这些事件。 例如，与位于JCR顶部的CIFS或WebDAV等文件服务器实现的直接交互变为隐式。

我认为，作为一个很好的经验法则，你可以用下列方法：如果需要存储文件名和mime类型，则 `nt:file`/ `nt:resource` 非常匹配。 如果可以有多个“文件”，则nt:folder是存储这些文件的好地方。

如果您需要为资源添加元信息，例如“author”或“description”属性，请扩展 `nt:resource` 而不是 `nt:file`。 我很少扩展nt:file，并且经常扩展 `nt:resource`。

#### 示例 {#example-6}

假设某人希望将图像上传到博客条目，网址为：

```xml
/content/myblog/posts/iphone_shipping
```

也许最初的肠胃反应是添加一个包含图片的二元属性。

虽然在这种情况下，确实有很好的用例仅使用二进制属性（假设名称不相关，mime类型是隐式的），但我建议为博客示例使用以下结构。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 规则7:ID是邪恶的。 {#rule-ids-are-evil}

#### 说明 {#explanation-7}

在关系数据库中，ID是表示关系的必要手段，因此人们也倾向于在内容模型中使用它们。 主要是因为错误的原因才能成功。

如果您的内容模型中包含以“Id”结尾的属性，则您可能未正确利用层次结构。

确实，某些节点在整个生命周期中都需要一个稳定的标识。 比你想象的要少得多。 mix:referenceable提供了这种内置于存储库中的机制，因此实际上不需要另外提供以稳定方式标识节点的方法。

还要记住，项目可以通过路径进行标识，而“symlinks”对于大多数用户来说比UNIX文件系统中的硬链接更有意义，而路径对于大多数应用程序引用目标节点来说也更有意义。

更重要的是，它是 **mix**:referenceable，这意味着它可以应用于您实际需要引用它的时间点的节点。

因此，假设您希望能够潜在地引用“文档”类型的节点并不意味着您的“文档”节点类型必须以静态方式从mix:referenceable扩展，因为它可以动态添加到“文档”的任何实例。

#### 示例 {#example-7}

用法:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

而不是：

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```

