---
title: 升级到 AEM 6.5 Communities
seo-title: 升级到 AEM 6.5 Communities
description: 如何从早期版本升级到AEM 6.5 Communities
seo-description: 如何从早期版本升级到AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# 升级到 AEM 6.5 Communities {#upgrading-to-aem-communities}

根据每个站点的拓扑和功能，在升级到AEM Communities 6.5或安装最新功能包时，可能需要执行以下操作。

此部分专门针对社区，并补充了[升级到AEM 6.5](/help/sites-deploying/upgrade.md)（平台）中提供的信息。

## 从AEM 6.1或更高版本{#upgrading-from-aem-or-later}升级

### 重新索引Solr {#reindex-solr}

在配置了MSRP的部署上安装新的Communities功能包时，需要：

1. 安装[最新功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
1. 安装[最新Solr配置文件](/help/communities/msrp.md#upgrading)。
1. 重新索引MSRP
请参阅[MSRP重新索引工具](/help/communities/msrp.md#msrp-reindex-tool)部分。

### 启用2.0 {#enablement}

自AEM 6.3起，启用功能不再将报表信息存储在MySQL中。 MySQL依赖关系仅用于跟踪SCORM内容。

请联系[客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)，以获取有关从启用1.0迁移内容的帮助。

## 从AEM 6.0 {#upgrading-from-aem}升级

如果需要保留预先存在的UGC，则执行此操作的方法取决于部署是存储在UGC [on-premise](#on-premise-storage)中，还是存储在[Adobe云](#adobe-cloud-storage)中。

### Adobe云存储{#adobe-cloud-storage}

如果已升级的站点配置为使用Adobe云存储，则它可能会（错误地）显示，好像所有UGC都丢失了一样，因为SRP方法将无法在旧位置中找到预先存在的UGC。

因此，能够指示ASRP使用`AEM 6.0 compatability-mode`访问UGC。

对于所有AEM 6.3创作和发布实例：

* 使用管理员权限登录。
* 配置[ASRP](/help/communities/asrp.md)。
* 请按照以下步骤使预先存在的UGC可见：

   * 浏览到Web控制台：

      * 例如， [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * 找到&#x200B;**AEM Communities实用程序**&#x200B;配置。
      * 选择以展开配置面板：

         * *取消选中* `Cloud Storage`

         * 选择&#x200B;**Save**

      ![实用程序](assets/utilities.png)


### 本地存储{#on-premise-storage}

如果已升级的站点不使用云存储，则必须转换任何预先存在的UGC，以符合AEM 6.1 Communities中引入的新结构，从而支持常用存储。

为此，在GitHub上提供了一个开源迁移工具：
[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### Java API {#java-apis}

从AEM 6.0社交社区升级到AEM 6.3社区时，请注意，许多API已重新组织为不同的包。 在使用IDE自定义社区功能时，大多数问题都应该易于解决。

有关已弃用的SocialUtils包的详细信息，请访问[SocialUtils重构](/help/communities/socialutils.md)。

另请参阅[使用Maven for Communities](/help/communities/maven.md)。

### 无JSP组件模板{#no-jsp-component-templates}

[社交组件框架](/help/communities/scf.md)(SCF)使用[HandlebarsJS](https://www.handlebarsjs.com/)(HBS)模板语言代替AEM 6.0之前使用的Java服务器页面(JSP)。

在AEM 6.0中，JSP组件与新的HBS框架组件一起保留在同一位置，HBS组件通常位于名为“hbs”的子文件夹中。

自AEM 6.1起，JSP组件已完全删除。 对于Communities，建议将JSP组件的所有使用替换为SCF组件。

## AEM Communities UGC迁移工具{#aem-communities-ugc-migration-tool}

[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)是一款开源迁移工具，可在GitHub上使用，可通过自定义工具将UGC从AEM社交社区的早期版本导出并导入AEM Communities 6.1或更高版本。

除了从早期版本移动UGC外，还可以使用该工具将UGC从一个[SRP](/help/communities/working-with-srp.md)移动到另一个版本，如从MSRP移动到DSRP。

## 从AEM 5.6.1或更低版本{#upgrading-from-aem-or-earlier}升级

从概念上讲，共有三代社区组件：

**第1代**:大约在CQ 5.4到AEM 5.6.0之间，这些是 **** 在本地存储库中存储UGC的Collab组件，它们使用复制作为跨平台同步UGC的手段。其他差异包括使用Java Server Pages(JSP)实现，以及仅在创作环境中创作的博客功能。

**第2代**:从AEM 5.6.1到AEM 6.1，这是collaband socialcomponents的 **** 组 **** 合。AEM 6.0引入了新的[社交组件框架](/help/communities/scf.md)(SCF)和AEM 6.2引入了[公共UGC存储](/help/communities/working-with-srp.md) ，其中使用[存储资源提供程序](/help/communities/srp.md)(SRP)访问UGC。

**第3代**:从AEM 6.2开始，只有在SCF **** 中作为Handlebars(HBS)组件实现的社交组件需要为UGC选择SRP。
