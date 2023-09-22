---
title: 数据建模 — David Nuescheler模型
description: David Nuescheler的内容建模建议
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 数据建模 — David Nuescheler模型{#data-modeling-david-nuescheler-s-model}

## 源 {#source}

以下是David Nuescheler发表的意见和评论。

David是Day Software AG的联合创始人兼首席技术官，该公司是全球内容管理和内容基础架构软件的领先提供商，于2010年被Adobe收购。 David现在是Adobe企业技术部副总裁，还领导内容管理的技术标准Java™ Content Repository (JCR)应用程序编程接口(API)JSR-170的开发。

您还可以在以下网址查看更多更新： [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## David的简介 {#introduction-from-david}

在各种讨论中，我发现开发人员对JCR在内容建模时提供的特性和功能有点不安。 目前尚无指南，也鲜有经验介绍如何对存储库中的内容进行建模，以及为什么一种内容模型优于另一种内容模型。

虽然在关系型世界中，软件行业在如何建模数据方面有着丰富的经验，但对于内容存储库空间的研究仍处于早期阶段。

我想通过表达我关于内容应如何建模的意见，来填补这一空白。 我希望有朝一日，这个项目会发展成为对开发商社区更有意义的事情，不仅仅是“我的观点”，而是更普遍适用的东西。 所以，试想一下我快速发展的第一针试刺它。

>[!NOTE]
>
>免责声明：这些准则表达了我个人的观点，有时是有争议的。 我期待着对这些准则进行辩论并加以完善。

## 七个简单规则 {#seven-simple-rules}

### 规则#1：数据优先，结构优先。 也许吧。 {#rule-data-first-structure-later-maybe}

#### 解释 {#explanation-1}

我建议不要担心ERD意义上的声明数据结构。 最初。

学习在开发过程中喜爱nt：unstructured (&amp; friends)。

我的结论是：结构非常昂贵，通常完全没有必要向底层存储显式声明结构。

对于应用程序本身使用的结构，存在隐式约定。 假设我将博客帖子的修改日期存储在lastModified属性中。 我的应用程序会自动知道再次从同一资产中读取修改日期，因此实际上不需要显式声明该日期。

只有在出于数据完整性原因需要时，才应应用其他数据约束，如强制或类型和值约束。

#### 示例 {#example-1}

上述使用 `lastModified` 日期属性，例如“博客帖子”节点，实际上并不表示需要特殊的节点类型。 我一定会用 `nt:unstructured` 对于我的博客帖子节点，至少在一开始是这样。 由于在我的博客应用程序中，我所要做的就是显示上次修改日期（可能为“order by”），因此我根本不在乎它是否为日期。 因为我暗地里相信我的博客写信申请，会在这里放一个“日期”，所以真的不需要宣布一个日期。 `lastModified` 节点类型形式的日期。

### 规则#2：推动内容层次结构；不要任其发生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 解释 {#explanation-2}

内容层次结构是一项宝贵的资源。 不要让它发生，设计它。 如果您没有易于用户识别的“良好”节点名称，则可能需要重新考虑这个问题。 任意数字很难算是“好名字”。

虽然将现有的关系模型快速纳入层次模型可能比较容易，但在这一过程中应该有所思考。

根据我的经验，如果有人认为访问控制和密封是内容层次结构的良好驱动因素。 将其视为您的文件系统。 甚至可以使用文件和文件夹在本地磁盘上对其进行建模。

就我个人而言，我最初倾向于使用层次结构约定，而不是节点键入系统，并在以后引入键入方法。

>[!CAUTION]
>
>内容存储库的结构方式也会影响性能。 为获得最佳性能，附加到内容存储库中单个节点的子节点数不应超过1,000。
>
>请参阅 [CRX可以处理多少数据？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html)

#### 示例 {#example-2}

我将用一个简单的博客系统建模如下。 最初，我甚至不在乎此时我使用的各个节点类型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我认为，显而易见的一点是，内容的结构是基于这个例子理解的，没有任何进一步的解释。

最初可能会出乎意料的是，为什么我不将“评论”与“帖子”一起存储，这是由于访问控制，我希望以合理的分层方式应用访问控制。

使用上述内容模型，我可以轻松地允许“匿名”用户“创建”评论，但可以只读方式让匿名用户保留工作区的其余部分。

### 规则#3：工作区用于clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 解释 {#explanation-3}

如果您不使用 `clone()`， `merge()` 或 `update()` 在您的应用程序中，可能适合使用单个工作区。

“对应节点”是JCR规范中定义的一个概念。 本质上，它归结为在不同所谓的工作区中表示相同内容的节点。

JCR引入了工作区的抽象概念，使得许多开发人员不知道如何处理这些工作区。 我建议检验一下您对工作区的使用。

如果在多个工作区中存在“相应”节点（本质上是具有相同UUID的节点）的大量重叠，则可能需要很好地使用工作区。

如果同一UUID的节点没有重叠，则可能是滥用工作区。

请勿使用工作区进行访问控制。 特定用户组的内容可见性不是将内容划分到不同工作区的好参数。 JCR在内容存储库中提供了“访问控制”功能，可做到这一点。

工作区是参照和查询的边界。

#### 示例 {#example-3}

将工作区用于如下内容：

* 项目的v1.2与项目的v1.3
* “开发”、“QA”和内容的“已发布”状态

请勿将工作区用于以下内容：

* 用户主目录
* 不同目标受众的不同内容，如公共、私有、本地……
* 不同用户的邮件收件箱

### 规则#4：注意同名同级。 {#rule-beware-of-same-name-siblings}

#### 解释 {#explanation-4}

同名同级(SNS)已引入规范，以允许与通过XML设计和表达的数据结构兼容，因此对JCR很有价值。 但是， SNS给存储库带来了开销和复杂性。

如果内容存储库的某个路径区段包含SNS，则该路径会变得不那么稳定。 如果SNS被删除或重新排序，则会影响所有其他SNS及其子级的路径。

对于导入XML或与现有XML交互，SNS可能是必要且有用的，但我从未在我的“绿色领域”数据模型中使用SNS（也从未打算使用）。

#### 示例 {#example-4}

使用

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

而不是

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 规则#5：引用被视为有害。 {#rule-references-considered-harmful}

#### 解释 {#explanation-5}

引用表示引用完整性。 必须了解的是，引用不仅会增加存储库管理引用完整性的成本，而且从内容灵活性的角度来看，还会带来高昂的成本。

就个人而言，只有在我真的无法处理挂起的引用时，我才会使用引用，否则，我将使用路径、名称或字符串UUID来引用其他节点。

#### 示例 {#example-5}

假设我允许从一个文档(a)到另一个文档(b)的“引用”。 如果使用引用属性对此关系进行建模，这意味着这两个文档在存储库级别上链接。 我无法单独导出/导入文档(a)，因为引用属性的目标可能不存在。 合并、更新、恢复或克隆等其他操作也会受到影响。

因此，我会将这些引用建模为“弱引用”（在JCR v1.0中，这实际上归结为包含目标节点的uuid的字符串属性），或者简单地使用路径。 有时候，这条道路从一开始就更有意义。

我认为在某些用例中，当引用悬停时，系统真的无法正常工作，但我无法从我的直接体验中给出一个良好的“真实”但简单的示例。

### 规则#6：文件是文件。 {#rule-files-are-files}

#### 解释 {#explanation-6}

如果内容模型泄露的东西甚至远程闻起来像文件或文件夹，我会尝试使用（或从扩展） `nt:file`， `nt:folder`、和 `nt:resource`.

根据我的经验，许多通用应用程序允许隐式与nt：folder和nt：files进行交互，并且如果它们富含其他元信息，则知道如何处理和显示这些事件。 例如，与JCR之上的文件服务器实现(如CIF或WebDAV)的直接交互变为隐式。

我认为根据经验，可以使用以下内容：如果必须存储文件名和mime类型，则 `nt:file`/ `nt:resource` 很配对。 如果您可以有多个“文件”，则nt：folder是存储这些文件的理想位置。

如果必须为资源添加元信息，例如“author”或“description”属性，请扩展 `nt:resource` 不是 `nt:file`. 我很少扩展nt：file ，而且经常扩展 `nt:resource`.

#### 示例 {#example-6}

假设有人希望将图像上传到以下位置的博客条目：

```xml
/content/myblog/posts/iphone_shipping
```

也许最初的直觉反应是添加一个包含图片的二进制属性。

虽然有一些很好的用例可以只使用二进制属性（比如名称无关且mime类型是隐式的），但在此示例中，我建议为我的博客示例使用以下结构。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 规则#7：ID是邪恶的。 {#rule-ids-are-evil}

#### 解释 {#explanation-7}

在关系数据库中，ID是表示关系的必要手段，因此人们也倾向于在内容模型中使用它们。 大部分都是因为错误的理由。

如果您的内容模型包含以“Id”结尾的属性，则可能无法正确使用层次结构。

诚然，某些节点在其整个生命周期中都需要稳定的标识；但比您想象的要少。 但是 `mix:referenceable` 在存储库中内置了此类机制，因此无需提出以稳定方式标识节点的额外方法。

另请注意，项目可以通过路径进行标识。 而且，尽管“符号链接”对于大多数用户来说比对UNIX®文件系统中的硬链接更有意义，但是对于大多数应用程序而言，引用目标节点也是有意义的。

更重要的是 **mix**：referenceable，这意味着它可以在您实际必须引用它的时间点应用于节点。

因此，仅仅因为您希望能够潜在地引用“文档”类型的节点并不意味着您的“文档”节点类型必须从扩展 `mix:referenceable` 以静态方式。 这是因为可将其动态添加到“文档”的任何实例。

#### 示例 {#example-7}

使用:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

而非：

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
