---
title: SRP和UGC Essentials
seo-title: SRP and UGC Essentials
description: 存储资源提供程序和用户生成的内容概述
seo-description: Storage resource provider and user-generated content overview
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# SRP和UGC Essentials {#srp-and-ugc-essentials}

## 简介 {#introduction}

如果不熟悉存储资源提供程序(SRP)及其与用户生成内容(UGC)的关系，请访问 [社区内容存储](working-with-srp.md) 和 [存储资源提供程序概述](srp.md).

此文档的此部分提供了有关SRP和UGC的一些基本信息。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API (SRP API)是各种Sling资源提供程序API的扩展。 它包括对分页和原子增量的支持（可用于计数和评分）。

SCF组件需要查询，因为需要按日期、有用性、票数等排序。 所有SRP选项都有灵活的查询机制，不依赖于分段。

SRP存储位置包含组件路径。 SRP API应始终用于访问UGC，因为根路径取决于所选的SRP选项，如ASRP、MSRP或JSRP。

SRP API不是抽象类，它是一个接口。 不应轻率地实施自定义实施，因为升级到新版本时将错过对内部实施进行未来改进的好处。

使用SRP API的方法是通过提供的实用程序，例如SocialResourceUtilities包中的实用程序。

从AEM 6.0或更低版本升级时，需要迁移所有SRP的UGC（有可用的开源工具）。 参见 [升级到AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>过去，用于访问UGC的实用工具在SocialUtils包中找到，但该包不再存在。
>
>有关替换实用工具，请参阅 [SocialUtils重构](socialutils.md).

## 访问UGC的实用程序方法 {#utility-method-to-access-ugc}

要访问UGC，请使用SocialResourceUtilities包中的方法，该方法返回适用于从SRP访问UGC的路径，并替换在SocialUtils包中找到的已弃用方法。

以下是在servlet中使用resourceToUGCStoragePath()方法的最小示例：

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

有关其他SocialUtils替换，请参阅 [SocialUtils重构](socialutils.md).

有关编码准则，请访问 [使用SRP访问UGC](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>resourceToUGCStoragePath()返回的路径为 *非* 适合 [ACL检查](srp.md#for-access-control-acls).

## 访问ACL的实用程序方法 {#utility-method-to-access-acls}

一些SRP实现（如ASRP和MSRP ）将社区内容存储在不提供ACL验证的数据库中。 影子节点提供本地存储库中可以应用ACL的位置。

使用SRP API，所有SRP选项在所有CRUD操作之前对阴影位置执行相同的检查。

要检查ACL，请使用返回适合检查应用于资源UGC的权限的路径的方法。

以下是在servlet中使用resourceToACLPath()方法的简单示例：

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>resourceToACLPath()返回的路径为 *非* 适合 [访问UGC](#utility-method-to-access-acls) 本身。

## 与UGC相关的存储位置 {#ugc-related-storage-locations}

以下对存储位置的描述在使用JSRP或MSRP进行开发时可能会有所帮助。 与JSRP一样，当前没有用于访问ASRP中存储的UGC的UI([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP （MongoDB工具）。

**组件位置**

当成员在发布环境中进入UGC时，他们作为AEM站点的一部分与组件交互。

以下是此类组件的示例 [注释组件](http://localhost:4502/content/community-components/en/comments.html) 中存在于 [社区组件指南](components-guide.md) 站点。 本地存储库中注释节点的路径为：

* 组件路径= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**阴影节点位置**

创建UGC还会创建 [影子节点](srp.md#about-shadow-nodes-in-jcr) 应用了必要的ACL。 本地存储库中相应影子节点的路径是影子节点根路径前置到组件路径的结果：

* 根路径 = `/content/usergenerated`
* 评论阴影节点= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC位置**

UGC既不会在这两个位置创建，也只能使用进行访问 [效用法](#utility-method-to-access-ugc) 调用SRP API。

* 根路径 = `/content/usergenerated/asi/srp-choice`
* JSRP的UGC节点= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*，对于JSRP，UGC节点将 *仅限* 在输入它的AEM实例（创作或发布）中存在。 如果在发布实例中输入，则无法从“创作”的“审阅”控制台中进行审阅。

## 相关信息 {#related-information}

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前的SRP实用程序方法。
