---
title: 升级到 AEM 6.5 Communities
seo-title: 升级到 AEM 6.5 Communities
description: 如何从早期版本升级到AEM 6.4 Communities
seo-description: 如何从早期版本升级到AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# 升级到 AEM 6.5 Communities {#upgrading-to-aem-communities}

根据每个站点的拓扑和功能，在升级到AEM Communities 6.5或安装最新功能包时，可能需要执行以下操作。

本部分针对社区，并补充升级到AEM 6.5 [](/help/sites-deploying/upgrade.md) （平台）中提供的信息。

## 从AEM 6.1或更高版本升级 {#upgrading-from-aem-or-later}

### 重新索引Solr {#reindex-solr}

在配置了MSRP的部署中安装新的Communities功能包时，必须：

1. 安装最 [新的功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安装最 [新的Solr配置文件](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP请参阅“ [MSRP重新索引工具”一节](/help/communities/msrp.md#msrp-reindex-tool)。

### Enablement 2.0 {#enablement}

自AEM 6.3起，启用功能不再在MySQL中存储报告信息。 MySQL依赖关系仅用于跟踪SCORM内容。

请联系客 [户关怀团队](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html) ，以获取从Enablement 1.0迁移内容的帮助。

## 从AEM 6.0升级 {#upgrading-from-aem}

如果需要保留预先存在的UGC，则执行此操作的方法取决于部署是预先存储 [UGC](#on-premise-storage) ，还是 [Adobe云](#adobe-cloud-storage)。

### Adobe Cloud存储 {#adobe-cloud-storage}

如果已升级的站点配置为使用Adobe云存储，则可能会（错误地）显示该站点，好像所有UGC都已丢失，因为SRP方法将无法在旧位置找到预先存在的UGC。

因此，能够指示ASRP使用访问 `AEM 6.0 compatability-mode` UGC。

对于所有AEM 6.3作者和发布实例：

* 使用管理员权限登录。
* 配置 [ASRP](/help/communities/asrp.md)。
* 按照以下步骤使预先存在的UGC可见：

   * 浏览到Web控制台：

      * 例如， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找到 **AEM Communities实用程序配置** 。
      * 选择以展开配置面板：

         * *取消选中*`Cloud Storage`

         * Select **Save**
      ![chlimage_1-176](assets/chlimage_1-176.png)


### 预置存储 {#on-premise-storage}

如果升级的站点未使用云存储，则任何预先存在的UGC必须转换为符合AEM 6.1 Communities中引入的新结构，以支持公用商店。

为此，GitHub上提供了开放源代码迁移工具：[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

从AEM 6.0社交社区升级到AEM 6.3社区时，请注意，许多API已重新组织为不同的包。 在使用IDE自定义社区功能时，大多数问题应该很容易解决。

有关已弃用的SocialUtils包的详细信息，请访 [问SocialUtils重构](/help/communities/socialutils.md)。

另请参 [阅使用Maven for Communities](/help/communities/maven.md)。

### 无JSP组件模板 {#no-jsp-component-templates}

社 [交组件框架](/help/communities/scf.md) (SCF)使用 [HandlebarsJS](https://www.handlebarsjs.com/) (HBS)模板语言代替AEM 6.0之前使用的Java服务器页面(JSP)。

在AEM 6.0中，JSP组件将保留在新HBS框架组件旁边的同一位置，HBS组件通常位于名为“hbs”的子文件夹中。

自AEM 6.1起，JSP组件已完全删除。 对于Communities，建议将JSP组件的所有使用替换为SCF组件。

## AEM Communities UGC迁移工具 {#aem-communities-ugc-migration-tool}

[](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) AEM Communities UGC Migration Tool是一个开放源代码迁移工具，可在GitHub上使用，可以自定义该工具以从AEM社交社区的早期版本中导出UGC并导入到AEM Communities 6.1或更高版本中。

除了将UGC从先前版本移开外，还可以使用该工具将UGC从一个 [SRP](/help/communities/working-with-srp.md) 移到另一个，如从MSRP移到DSRP。

## 从AEM 5.6.1或更早版本升级 {#upgrading-from-aem-or-earlier}

从概念上讲，有三代社区组件：

**第1代**:大约是CQ 5.4到AEM 5.6.0，这些组件是 **collab** 组件，它们将UGC存储在本地存储库中，并将复制用作跨平台同步UGC的手段。 其他差异包括使用Java服务器页面(JSP)的实现以及仅在创作环境中进行创作的博客功能。

**第2代**:从AEM 5.6.1到AEM 6.1，这是协作和社交组 **件****的组合** 。 AEM 6.0引入了新的社 [交组件框架](/help/communities/scf.md) (SCF),AEM 6.2引入了一个通用的UGC store [，在该商店中，可以使用](/help/communities/working-with-srp.md) 存储资源提供者 [](/help/communities/srp.md) (SRP)访问UGC。

**第3代**:从AEM 6.2向前，只有社交组件在SCF中实现为Handlebars(HBS)组件，这要求为UGC选择SRP。 ****
