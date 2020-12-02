---
title: SRP和UGC Essentials
seo-title: SRP和UGC Essentials
description: 存储资源提供商和用户生成的内容概述
seo-description: 存储资源提供商和用户生成的内容概述
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# SRP和UGC Essentials {#srp-and-ugc-essentials}

## 简介 {#introduction}

如果不熟悉存储资源提供程序(SRP)及其与用户生成内容(UGC)的关系，请访问[社区内容存储](working-with-srp.md)和[存储资源提供程序概述](srp.md)。

本文档的这一部分提供了一些关于SRP和UGC的基本信息。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)是各种Sling资源提供程序API的扩展。 它包括对分页和原子增量的支持（对计分和评分有用）。

查询对于SCF组件是必需的，因为需要按日期、帮助、投票数等进行排序。 所有SRP选项都具有灵活的查询机制，这些机制不依赖于分段。

SRP存储位置包含组件路径。 SRP API应始终用于访问UGC，因为根路径取决于所选的SRP选项，如ASRP、MSRP或JSRP。

SRP API不是抽象类，它是接口。 不应轻率地实施自定义实施，因为在升级到新版本时，将来改进内部实施的好处将被忽略。

使用SRP API的方法是通过提供的实用程序，如SocialResourceUtilities包中的实用程序。

从AEM 6.0或更低版本升级时，必须迁移所有SRP的UGC，其中都有开放源码工具。 请参阅[升级到AEM Communities6.3](upgrade.md)。

>[!NOTE]
>
>以前，用于访问UGC的实用程序都位于SocialUtils包中，该包已不复存在。
>
>有关替换实用程序，请参阅[SocialUtils重构](socialutils.md)。

## 访问UGC {#utility-method-to-access-ugc}的实用程序方法

要访问UGC，请使用SocialResourceUtilities包中的方法，该方法返回适合从SRP访问UGC的路径，并替换SocialUtils包中已弃用的方法。

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

有关其他SocialUtils替换，请参阅[SocialUtils重构](socialutils.md)。

有关编码指南，请访问[使用SRP](accessing-ugc-with-srp.md)访问UGC。

>[!CAUTION]
>
>路径resourceToUGCStoragePath()返回的路径为&#x200B;*不*，适合于[ACL检查](srp.md#for-access-control-acls)。

## 访问ACL的实用程序方法{#utility-method-to-access-acls}

某些SRP实现（如ASRP和MSRP）将社区内容存储在不提供ACL验证的数据库中。 卷影节点在可应用ACL的本地存储库中提供一个位置。

使用SRP API，所有SRP选项在执行所有CRUD操作之前对阴影位置执行相同的检查。

要检查ACL，请使用一种方法，该方法返回适合于检查应用于资源UGC的权限的路径。

以下是在servlet中使用resourceToACLPath()方法的一个简单示例：

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
>resourceToACLPath()返回的路径为&#x200B;*不*，适合于[访问UGC](#utility-method-to-access-acls)本身。

## UGC相关存储位置{#ugc-related-storage-locations}

在使用JSRP或MSRP进行开发时，以下存储位置描述可能会有所帮助。 当前没有用于访问存储在ASRP中的UGC的UI，因为存在JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP（MongoDB工具）。

**组件位置**

当成员在发布环境中输入UGC时，他们正作为AEM站点的一部分与组件交互。

此类组件的示例是[社区组件指南](components-guide.md)站点中存在的[注释组件](http://localhost:4502/content/community-components/en/comments.html)。 本地存储库中注释节点的路径为：

* 组件路径= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**阴影节点位置**

UGC的创建还创建了[阴影节点](srp.md#about-shadow-nodes-in-jcr)，其中应用了必要的ACL。 本地存储库中相应阴影节点的路径是预先将阴影节点根路径置于组件路径中的结果：

* 根路径 = `/content/usergenerated`
* 注释阴影节点= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC位置**

UGC不在这两个位置创建，只应使用调用SRP API的[实用程序方法](#utility-method-to-access-ugc)访问。

* 根路径 = `/content/usergenerated/asi/srp-choice`
* JSRP的UGC节点= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*请注意*，对于JSRP,UGC节点 ** 将仅出现在输入它的AEM实例（作者或发布）上。如果在发布实例中输入，则无法通过创作时的审核控制台进行审核。

## 相关信息{#related-information}

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [使用SRP编码准则](accessing-ugc-with-srp.md) 访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。
