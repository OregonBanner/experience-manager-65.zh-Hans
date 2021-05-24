---
title: 数据建模 — 大卫·纽谢勒的模型
seo-title: 数据建模 — 大卫·纽谢勒的模型
description: 大卫·纽谢勒的内容建模推荐
seo-description: 大卫·纽谢勒的内容建模推荐
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# 数据建模 — David Nuescheler的模型{#data-modeling-david-nuescheler-s-model}

## 源 {#source}

以下是David Nuescheler所表达的想法和评论。

Day Software AG是Day Software AG的联合创始人兼首席技术官，该公司是全球内容管理和内容基础架构软件的领先提供商，于2010年被Adobe收购。 他现在是Adobe企业技术部的资深副总裁，还领导了JSR-170(Java内容存储库(JCR)应用程序编程接口(API))的开发，该接口是内容管理的技术标准。

您还可以在[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)上查看更新。

## David {#introduction-from-david}的简介

在各种讨论中，我发现开发人员对JCR在内容建模方面提供的特性和功能有些不安。 在如何对存储库中的内容建模以及为什么一个内容模型比另一个内容模型更好方面，还没有任何指南和很少的经验。

虽然在关系世界中，软件行业在如何对数据建模方面拥有许多经验，但我们在内容存储库空间方面仍处于初级阶段。

我想通过表达我对内容如何建模的个人意见来填补这一空白，希望有朝一日能够让内容变得对开发人员社区更有意义，这不仅仅是“我的意见”，还是更普遍适用的内容。 所以，请考虑一下，这是我第一次尝试它时迅速演变的。

>[!NOTE]
>
>免责声明：这些准则表达了我的个人观点，有时是有争议的。 我期待着对这些准则进行辩论并加以完善。

## 7个简单规则{#seven-simple-rules}

### 规则#1:数据先，结构后。 也许吧。{#rule-data-first-structure-later-maybe}

#### 说明{#explanation-1}

我建议您不要担心ERD意义上声明的数据结构。 最初。

了解如何喜欢nt：开发中的非结构化（和朋友）。

我觉得斯蒂法诺很总结这个。

我的底线是：结构成本很高，在很多情况下，完全不需要向底层存储中明确声明结构。

您的应用程序本身使用的结构有一个隐含的约定。 假设我将博客帖子的修改日期存储在lastModified属性中。 我的应用程序会自动知道要再次从同一资产中读取修改日期，因此实际上不需要明确声明该日期。

出于数据完整性原因，仅在需要时应用强制或类型和值约束等其他数据约束。

#### 示例 {#example-1}

上例在“blog post”节点上使用`lastModified`日期属性，实际上并不表示需要特殊的节点类型。 至少在最初，我一定会使用`nt:unstructured`作为博客帖子节点。 因为在我的博客应用程序中，我要做的就是显示lastModified日期（可能是“订购日期”），我根本不在乎它是否是日期。 由于我暗中信任博客写作应用程序在此处设置“日期”，因此实际上没有必要以nodetype的形式声明`lastModified`日期的存在。

### 规则#2:驱动内容层次结构，不要让它发生。{#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 说明{#explanation-2}

内容层次结构是一项非常有价值的资产。 所以别让它发生，设计它。 如果某个节点没有“好”、人类可读的名称，那可能是您应该重新考虑的问题。 任意数字从来都不是“好名字”。

虽然将现有的关系模型快速放入分层模型中可能非常容易，但在这个过程中应该考虑一些。

在我的体验中，如果考虑访问控制和控制通常是内容层次结构的良好驱动因素。 把它想成是你的文件系统。 甚至可以使用文件和文件夹在本地磁盘上对其进行建模。

个人而言，在很多情况下，我最初更喜欢等级制度惯例，而不是登录系统，然后在以后介绍输入。

>[!CAUTION]
>
>内容存储库的结构方式也会影响性能。 为获得最佳性能，附加到内容存储库中各个节点的子节点数通常不应超过1&#39;000。
>
>请参阅[CRX可以处理多少数据？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 以了解更多信息。

#### 示例 {#example-2}

我给一个简单的博客系统建模如下。 请注意，我最初甚至不关心我此时使用的各个节点类型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我认为有一点显而易见那就是我们都理解内容的结构是以这个例子为基础没有进一步的解释。

最初可能出人意料的是，为什么我不会将“评论”与“帖子”一起存储，这是由于访问控制，我希望以合理的层级方式应用访问控制。

使用上述内容模型，我可以轻松允许“匿名”用户“创建”评论，但将匿名用户保留为工作区其余部分的只读状态。

### 规则#3:工作区适用于clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 说明{#explanation-3}

如果您的应用程序中没有使用`clone()`、`merge()`或`update()`方法，则可能需要使用单个工作区。

“对应节点”是JCR规范中定义的概念。 基本上，它可以归结为表示相同内容的节点，这些节点位于不同的所谓工作区中。

JCR引入了Workspaces的非常抽象的概念，这使得许多开发人员不清楚该如何处理它们。 我建议您将工作区的使用情况放在以下方面进行测试。

如果您在多个工作区中存在大量“对应”节点（即具有相同UUID的节点）重叠，则可能会将工作区放置到适当的位置。

如果没有与使用相同UUID的节点重叠，则您可能会滥用工作区。

不应将工作区用于访问控制。 查看特定用户组的内容不是将内容划分到不同工作区中的好参数。 JCR在内容存储库中具有“访问控制”功能，可为其提供。

工作区是引用和查询的边界。

#### 示例 {#example-3}

将工作区用于以下内容：

* 项目的v1.2与项目的v1.3
* 内容的“开发”、“QA”和“已发布”状态

请勿将工作区用于以下内容：

* 用户主目录
* 不同目标受众（如公共、私有、本地、...）的不同内容
* 适用于不同用户的邮箱

### 规则#4:请注意同名兄弟姐妹。{#rule-beware-of-same-name-siblings}

#### 说明{#explanation-4}

虽然在规范中引入了同名同级(SNS)，以允许与为XML设计并通过XML表示的数据结构兼容，因此对JCR极其有价值，但SNS对存储库带来了巨大的开销和复杂性。

进入内容存储库的任何路径（其其中一个路径段中包含SNS）都变得不那么稳定，如果删除或重新排序了SNS，则会对所有其他SNS及其子SNS的路径产生影响。

为了导入XML或与现有XML SNS进行交互，可能既必要又有用，但我从未使用过SNS，而且永远不会在我的“绿色字段”数据模型中使用。

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

### 规则#5:被认为有害的参考资料。{#rule-references-considered-harmful}

#### 说明{#explanation-5}

引用表示参照完整性。 我发现，重要的是要了解，引用不仅为管理引用完整性的存储库增加了额外成本，而且从内容灵活性的角度来说，这些引用也成本高昂。

就个人而言，我确保仅在我确实无法处理悬挂引用时才使用引用，否则，我会使用路径、名称或字符串UUID来引用其他节点。

#### 示例 {#example-5}

假设我允许将文档(a)中的“引用”到另一个文档(b)。 如果我使用引用属性对此关系建模，则意味着两个文档在存储库级别上进行链接。 无法单独导出/导入文档(a)，因为引用属性的目标可能不存在。 其他操作（如合并、更新、恢复或克隆）也会受到影响。

因此，我要么将这些引用建模为“弱引用”（在JCR v1.0中，这基本上归结为包含目标节点uuid的字符串属性），要么只使用路径。 有时路径的开头更有意义。

我认为，有些用例，如果某个系统的引用被悬空，它真的不能工作，但是，我无法从直接体验中得出一个好的“真实”而简单的例子。

### 规则#6:文件是文件。{#rule-files-are-files}

#### 说明{#explanation-6}

如果内容模型公开的东西甚至远程&#x200B;*闻起*，就像我尝试使用（或从中扩展）`nt:file`、`nt:folder`和`nt:resource`的文件或文件夹。

在我的体验中，许多通用应用程序允许与nt:folder和nt:files进行隐式交互，并且知道如果这些事件通过附加的元信息进行了扩充，该如何处理和显示这些事件。 例如，与位于JCR顶部的CIFS或WebDAV等文件服务器实施的直接交互变为隐式。

我认为，作为经验法则，人们可以使用以下方法：如果需要存储文件名和mime类型，则`nt:file`/ `nt:resource`非常匹配。 如果您可以有多个“文件”，则nt:folder是存储这些文件的好地方。

如果需要为资源添加元信息，例如“author”或“description”属性，请扩展`nt:resource`，而不是`nt:file`。 我很少扩展nt:file ，并经常扩展`nt:resource`。

#### 示例 {#example-6}

假设有人希望将图像上传到以下博客条目：

```xml
/content/myblog/posts/iphone_shipping
```

也许最初的肠胃反应是添加一个包含图片的二进制属性。

虽然在这种情况下，当然有很好的用例来仅使用二进制属性（例如，名称不相关且mime类型是隐式的），但我建议为博客示例使用以下结构。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 规则#7:身份是邪恶的。{#rule-ids-are-evil}

#### 说明{#explanation-7}

在关系数据库中，ID是表达关系的必要手段，因此人们往往也会在内容模型中使用ID。 主要是因为错误的原因。

如果您的内容模型中包含以“Id”结尾的属性，则可能无法正确利用层级。

确实，某些节点在其整个生命周期中都需要稳定的标识。 比你想的要少。 mix:referenceable提供了此类内置于存储库中的机制，因此实际上不需要以稳定的方式提供其他标识节点的方法。

还要记住，项目可以按路径进行标识，而“符号链接”对于大多数用户而言比对Unix文件系统中的硬链接更有意义，因此，对于大多数应用程序而言，路径对于引用目标节点是有意义的。

更重要的是，它是&#x200B;**mix**:referenceable，这意味着它可以在实际需要引用时应用到某个节点。

因此，假设您希望能够引用“文档”类型的节点，并不意味着您的“文档”节点类型必须从mix:referenceable以静态方式扩展，因为它可以动态添加到“文档”的任何实例。

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
