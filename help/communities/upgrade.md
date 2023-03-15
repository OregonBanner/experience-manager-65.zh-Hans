---
title: 升级到 AEM 6.5 Communities
seo-title: Upgrading to AEM 6.5 Communities
description: 如何从早期版本升级到AEM 6.5 Communities
seo-description: How to upgrade from an earlier version to AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 升级到 AEM 6.5 Communities {#upgrading-to-aem-communities}

根据每个站点的拓扑和功能，在升级到AEM Communities 6.5或安装最新的功能包时，可能需要执行以下操作。

本节专门介绍各个社区，补充了以下网站提供的信息： [升级到AEM 6.5](/help/sites-deploying/upgrade.md) （平台）。

## 从AEM 6.1或更高版本升级 {#upgrading-from-aem-or-later}

### 重新索引Solr {#reindex-solr}

在配置了MSRP的部署上安装新的Communities功能包时，需要：

1. 安装 [最新功能包](/help/communities/deploy-communities.md#latestfeaturepack).
1. 安装 [最新Solr配置文件](/help/communities/msrp.md#upgrading).
1. 重新索引MSRP，请参阅部分 [MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool).

### 启用2.0 {#enablement}

从AEM 6.3开始，启用功能不再将报表信息存储在MySQL中。 MySQL依赖项仅用于跟踪SCORM内容。

请联系 [客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html) ，以获取有关从Enablement 1.0迁移内容的帮助。

## 从AEM 6.0升级 {#upgrading-from-aem}

如果需要保留预先存在的UGC，则保留的方法取决于部署是否存储了UGC [内部部署](#on-premise-storage) 或在 [Adobe云](#adobe-cloud-storage).

### Adobe云存储 {#adobe-cloud-storage}

如果升级的站点配置为使用Adobe云存储，则它可能会出现（不正确的）好像所有UGC都已丢失，因为SRP方法无法在旧位置找到预先存在的UGC。

因此，能够指示ASRP使用 `AEM 6.0 compatability-mode` 访问UGC。

对于所有AEM 6.3创作和发布实例：

* 使用管理员权限登录。
* 配置 [ASRP](/help/communities/asrp.md).
* 请按照以下步骤使预先存在的UGC可见：

   * 浏览到Web控制台：

      * 例如， [https://&lt;host>：&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 查找 **AEM Communities实用程序** 配置。
      * 选择以展开配置面板：

         * *取消选中* `Cloud Storage`

         * 选择 **保存**

      ![实用工具](assets/utilities.png)


### 内部部署存储 {#on-premise-storage}

如果升级后的站点未使用云存储，则任何预先存在的UGC都必须转换为符合AEM 6.1 Communities中引入的新结构，以支持公用存储。

为此，GitHub上提供了开源迁移工具：
[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

从AEM 6.0社交社区升级到AEM 6.3社区时，请注意，许多API已重新组织到不同的包中。 在使用IDE自定义社区功能时，应该可以轻松解决大多数问题。

有关已弃用的SocialUtils包的详细信息，请访问 [SocialUtils重构](/help/communities/socialutils.md).

另请参阅 [使用Maven for Communities](/help/communities/maven.md).

### 无JSP组件模板 {#no-jsp-component-templates}

此 [社交组件框架](/help/communities/scf.md) (SCF)使用 [HandlebarsJS](https://handlebarsjs.com/) (HBS)模板语言取代AEM 6.0之前使用的Java Server Pages (JSP)。

在AEM 6.0中，JSP组件与新的HBS框架组件保留在同一位置，HBS组件通常位于名为“hbs”的子文件夹中。

从AEM 6.1开始，JSP组件已被完全删除。 对于社区，建议使用SCF组件替换所有使用的JSP组件。

## AEM Communities UGC迁移工具 {#aem-communities-ugc-migration-tool}

此 [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) 是一个在GitHub上提供的开源迁移工具，可自定义该工具以从早期版本的AEM社交社区中导出UGC，并将其导入AEM Communities 6.1或更高版本。

除了从早期版本中移动UGC之外，还可以使用该工具将UGC从一个版本中移动 [SRP](/help/communities/working-with-srp.md) 到另一个，例如从MSRP到DSRP。

## 从AEM 5.6.1或更低版本升级 {#upgrading-from-aem-or-earlier}

从概念上讲，社区组件分为三代：

**第1代**：大致CQ 5.4到AEM 5.6.0，这些是 **协作** 使用复制作为跨平台同步UGC的一种方式，将UGC存储在本地存储库中的组件。 其他区别包括使用Java Server Pages (JSP)进行实施，以及仅在创作环境中创作日志功能。

**第2代**：从AEM 5.6.1到AEM 6.1，这是混合使用 **协作** 和 **社交** 组件。 AEM 6.0引入了新的 [社交组件框架](/help/communities/scf.md) (SCF)和AEM 6.2引入了 [通用UGC存储](/help/communities/working-with-srp.md) 其中UGC是使用 [存储资源提供程序](/help/communities/srp.md) (SRP)。

**第3代**：从AEM 6.2开始，只有 **社交** 组件，在SCF中作为Handlebars (HBS)组件实现，需要为UGC选择SRP。
