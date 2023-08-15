---
title: 内容架构
description: 关于内容架构的提示（提示 — 一切都是内容）
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 内容架构{#content-architecture}

## 遵循David的模型 {#follow-david-s-model}

《大卫模型》是大卫·纽舍勒多年前写的，但如今这种观点仍然成立。 David模型的主要原则如下：

* 先有数据，后有结构。 也许吧。
* 推动内容层次结构，不要让它发生。
* 工作区用于 `clone()`， `merge()`、和 `update()`.
* 注意同名同胞。
* 引用内容被视为有害。
* 文件就是文件。
* 身份识别是邪恶的。

大卫的模特可以在Jackrabbit维基百科上找到，网址为 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 一切都是内容 {#everything-is-content}

所有内容都应存储在存储库中，而不是依赖单独的第三方数据源，例如数据库。 这适用于创作内容以及图像、代码和配置等二进制数据。 这使我们可以使用一组API来管理所有内容，并通过复制管理此内容的提升。 您还可以获得备份、日志记录等的单一来源。

### 使用“内容模型优先”设计原则 {#use-the-content-model-first-design-principle}

构建新功能时，始终首先设计JCR内容结构，然后考虑使用默认Sling Servlet阅读和编写内容。 这使您能够确保实施与开箱即用的访问控制机制很好地配合使用，并避免生成不必要的CRUD样式的servlet。

### 是RESTful {#be-restful}

Servlet应基于resourceTypes而不是路径进行定义。 这使得使用JCR访问控制、遵守REST原则以及使用在请求中提供给我们的资源和资源解析器成为可能。 这还允许我们更改在服务器端渲染URL的脚本，而无需更改客户端的任何URL，同时隐藏客户端的服务器端实施详细信息以提高安全性。

### 避免定义新节点类型 {#avoid-defining-new-node-types}

节点类型在基础结构层中处于较低级别，通过使用分配给nt：unstructured、oak：Unstructured、sling：Folder或cq：Page节点类型的sling：resourceType可以满足大多数要求。 节点类型等同于存储库中的架构，并且将来更改节点类型可能会很昂贵。

### 遵守JCR中的命名约定 {#adhere-to-naming-conventions-in-the-jcr}

遵守命名惯例可为代码库增加一致性，从而降低缺陷的发生率，并提高开发人员在系统中工作的速度。 Adobe在开发AEM时使用以下约定：

* 节点名称

   * 全部小写
   * 使用连字符进行分词

* 属性名称

   * 驼峰式大小写，以小写字母开头

* 组件(JSP/HTML)

   * 全部小写
   * 使用连字符进行分词
