---
title: 内容架构
seo-title: Content Architecture
description: 关于内容架构的提示（提示 — 一切都是内容）
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 内容架构{#content-architecture}

## 遵循David的模型 {#follow-david-s-model}

大卫·纽舍勒早在多年前就写出了《大卫模型》，但如今这种观点仍然成立。 David模型的主要原理如下：

* 数据是第一位的，结构是后来的。 也许吧。
* 推动内容层级，不要让这种情况发生。
* 工作区用于 `clone()`， `merge()`、和 `update()`.
* 注意同名同胞。
* 引用内容被认为是有害的。
* 文件就是文件。
* 身份证是邪恶的。

David&#39;s Model可在Jackrabbit维基百科上找到，网址为 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 一切都是内容 {#everything-is-content}

所有内容都应存储在存储库中，而不是依赖单独的第三方数据源，例如数据库。 这适用于创作内容以及图像、代码、配置等二进制数据。 这样，我们就可以使用一组API来管理所有内容，并通过复制管理此内容的促销活动。 我们还可以获得备份、日志记录等的单一来源。

### 采用“内容模型优先”的设计原则 {#use-the-content-model-first-design-principle}

构建新功能时，始终首先设计JCR内容结构，然后考虑使用默认Sling servlet阅读和编写内容。 这样，您就可以确保实施与开箱即用的访问控制机制很好地配合使用，并避免生成不必要的CRUD样式的servlet。

### Be RESTful {#be-restful}

Servlet应基于resourceTypes而不是路径进行定义。 这使得使用JCR访问控制、遵守REST原则以及使用在请求中提供给我们的资源和资源解析器成为可能。 这还允许我们更改在服务器端渲染URL的脚本，而无需更改客户端的任何URL，同时隐藏客户端的服务器端实施详细信息以提高安全性。

### 避免定义新节点类型 {#avoid-defining-new-node-types}

节点类型在基础结构层中处于较低级别，大多数需求可以通过使用分配给nt：unstructured、oak：Unstructured、sling：Folder或cq：Page节点类型的sling：resourceType来满足。 节点类型等同于存储库中的架构，今后更改节点类型可能会非常昂贵。

### 遵守JCR中的命名惯例 {#adhere-to-naming-conventions-in-the-jcr}

遵守命名惯例将增强代码库的一致性，从而降低缺陷发生率，并提高开发人员在系统中工作的速度。 Adobe在开发AEM时使用以下约定：

* 节点名称

   * 全部小写
   * 使用连字符进行分词

* 属性名称

   * 驼峰式大小写，以小写字母开头

* 组件(JSP/HTML)

   * 全部小写
   * 使用连字符进行分词
