---
title: 升级到 AEM 6.5 Communities
seo-title: 升级到 AEM 6.5 Communities
description: 如何从先前版本升级到AEM 6.4 Communities
seo-description: 如何从先前版本升级到AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---


# 升级到 AEM 6.5 Communities {#upgrading-to-aem-communities}

根据每个站点的拓扑和功能，在升级到AEM Communities6.5或安装最新功能包时，可能需要执行以下操作。

本部分针对社区，并补充在[升级到AEM 6.5](/help/sites-deploying/upgrade.md)（平台）中提供的信息。

## 从AEM 6.1或更高版本{#upgrading-from-aem-or-later}升级

### 重新索引Solr {#reindex-solr}

在配置了MSRP的部署上安装新的Communities功能包时，必须：

1. 安装[最新功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安装[最新的Solr配置文件](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP
请参阅[MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool)节。

### Enablement 2.0 {#enablement}

自AEM 6.3起，启用功能不再在MySQL中存储报告信息。 MySQL依赖关系仅用于跟踪SCORM内容。

请联系[客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)以获得有关从Enablement 1.0迁移内容的帮助。

## 从AEM 6.0 {#upgrading-from-aem}升级

如果需要保留预先存在的UGC，则执行此操作的方法取决于部署是存储在UGC [内部部署](#on-premise-storage)还是存储在[Adobe云](#adobe-cloud-storage)中。

### Adobe云存储{#adobe-cloud-storage}

如果已升级的站点配置为使用Adobe云存储，则可能会（错误地）显示所有UGC，因为SRP方法将无法在旧位置找到先前存在的UGC。

因此，可以指示ASRP使用`AEM 6.0 compatability-mode`访问UGC。

对于所有AEM 6.3作者和发布实例：

* 以管理员权限登录。
* 配置[ASRP](/help/communities/asrp.md)。
* 按照以下步骤使预先存在的UGC可见：

   * 浏览到Web控制台：

      * 例如，[https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找到&#x200B;**AEM Communities实用程序**&#x200B;配置。
      * 选择以展开配置面板：

         * *取消选中* `Cloud Storage`

         * 选择&#x200B;**保存**

      ![实用程序](assets/utilities.png)


### 本地存储{#on-premise-storage}

如果升级的站点未使用云存储，则任何预先存在的UGC都必须转换为符合AEM 6.1 Communities中引入的新结构，以支持公共商店。

为此，GitHub上提供了开放源码迁移工具：
[AEM CommunitiesUGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

从AEM 6.0社交社区升级到AEM 6.3社区时，请注意，许多API已重新组织为不同的包。 在使用IDE自定义社区功能时，大多数问题都应该得到轻松解决。

有关已弃用的SocialUtils包的详细信息，请访问[SocialUtils重构](/help/communities/socialutils.md)。

另请参阅[使用Maven for Communities](/help/communities/maven.md)。

### 没有JSP组件模板{#no-jsp-component-templates}

[社交组件框架](/help/communities/scf.md)(SCF)使用[HandlebarsJS](https://www.handlebarsjs.com/)(HBS)模板语言代替AEM 6.0之前使用的Java服务器页(JSP)。

在AEM 6.0中，JSP组件与新的HBS框架组件保留在同一位置，HBS组件通常位于名为“hbs”的子文件夹中。

自AEM 6.1起，JSP组件已完全删除。 对于Communities，建议将JSP组件的所有使用替换为SCF组件。

## AEM CommunitiesUGC迁移工具{#aem-communities-ugc-migration-tool}

[AEM CommunitiesUGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)是一个开放源代码迁移工具，可在GitHub上使用，可自定义该工具以从早期版本的AEM社交社区导出UGC并导入到AEM Communities6.1或更高版本。

除了将UGC从先前版本移动外，还可以使用该工具将UGC从一个[SRP](/help/communities/working-with-srp.md)移动到另一个，如从MSRP移动到DSRP。

## 从AEM 5.6.1或更低版本{#upgrading-from-aem-or-earlier}升级

从概念上讲，有三代社区组成部分：

**第1代**:大约是CQ 5.4到AEM 5.6.0，这些是 **** collabcomponents，它们将UGC存储在本地存储库中，将复制用作跨平台同步UGC的手段。其他差异包括使用Java服务器页面(JSP)的实现，以及博客功能，该功能仅包括在创作环境中进行创作。

**第2代**:从AEM 5.6.1到AEM 6.1，这是collab和socialcomponent **** 的 **** 混合。AEM 6.0引入了新的[社交组件框架](/help/communities/scf.md)(SCF)和AEM 6.2引入了[公用UGC存储](/help/communities/working-with-srp.md)，其中使用[存储资源提供商](/help/communities/srp.md)(SRP)访问UGC。

**第3代**:从AEM 6.2向前，只有在SCF中 **** 作为Handlebars(HBS)组件实现的社交组件需要为UGC选择SRP。
