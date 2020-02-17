---
title: 内容架构
seo-title: 内容架构
description: 设计内容的提示（提示——一切都是内容）
seo-description: 在Adobe Experience Manager(AEM)中构建内容的提示。 （提示——所有内容均为内容）
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 内容架构{#content-architecture}

## 遵循David的模式 {#follow-david-s-model}

David’s Model是David Nuescheler几年前写的，但如今，这一理念依然成立。 David’s Model的主要原则如下：

* 数据优先，结构后来。 也许吧。
* 推动内容层次，不要让其发生。
* 工作区适 `clone()`用于 `merge()`、和 `update()`。
* 提防同名同级。
* 引用被认为有害。
* 文件是文件。
* ID是邪恶的。

David’s Model可在Jackrabbit维基百科上找到，网址为 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 一切都是内容 {#everything-is-content}

所有内容都应存储在存储库中，而不是依赖单独的第三方数据源（如数据库）。 这适用于创作内容、二进制数据（如图像、代码、配置等）。 这允许我们使用一组API来管理所有内容并通过复制来管理此内容的推广。 我们还可以获得单一的备份、记录等源。

### 使用“内容模型优先”的设计原则 {#use-the-content-model-first-design-principle}

构建新功能时，请始终首先设计JCR内容结构，然后使用默认的Sling Servlets查看内容的读写。 这样，您就可以确保实施能够与开箱即用的访问控制机制很好地配合，并且可以避免生成不必要的CRUD样式的servlet。

### RESTful {#be-restful}

Servlet应根据resourceTypes而不是路径进行定义。 这使得可以使用JCR访问控制，遵守REST原则，以及使用请求中提供给我们的资源和资源解析程序。 这还允许我们更改在服务器端呈现URL的脚本，而无需从客户端更改任何URL，同时隐藏客户端实现详细信息以增加安全性。

### 避免定义新的节点类型 {#avoid-defining-new-node-types}

节点类型在基础架构层中处于较低的级别，并且大多数要求都可以通过使用分配给nt:unstructured、oak:Unstructured、sling:Folder或cq:Page节点类型的sling:resourceType来满足。 节点类型与存储库中的架构相等，并且更改节点类型在将来可能会非常昂贵。

### 遵守JCR中的命名约定 {#adhere-to-naming-conventions-in-the-jcr}

遵循命名约定将为代码库增加一致性，降低缺陷发生率并提高系统中开发人员的速度。 Adobe在开发AEM时使用以下惯例：

* 节点名称

   * 全小写
   * 使用连字符分词

* 属性名称

   * 驼峰大小写，以小写字母开头

* 组件(JSP/HTML)

   * 全小写
   * 使用连字符分词

