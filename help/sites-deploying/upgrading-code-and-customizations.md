---
title: 升级代码和自定义
seo-title: 升级代码和自定义
description: 了解有关在AEM中升级自定义代码的更多信息。
seo-description: 了解有关在AEM中升级自定义代码的更多信息。
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41

---


# 升级代码和自定义{#upgrading-code-and-customizations}

在计划升级时，需要调查并解决实施的以下方面。

* [升级代码库](#upgrade-code-base)
* [与6.5存储库结构对齐](#align-repository-structure)
* [AEM自定义](#aem-customizations)
* [测试过程](#testing-procedure)

## 概述 {#overview}

1. **模式检测器**[](/help/sites-deploying/pattern-detector.md) -按照升级计划中的说明运行模式检测器（如本页中所述），以获取模式检测器报告，该报告包含除AEM目标版中不可用的API/包外，还需要解决的区域的更多详细信息。 “模式检测”报告应指示代码中的任何不兼容性，如果没有，则您的部署已经兼容6.5，您仍然可以选择使用6.5功能进行新开发，但您不需要它来保持兼容性。 如果报告了不兼容性，则您可以选择a)以兼容性模式运行并推迟开发以获得新的6.5功能或兼容性，b)在升级后决定进行开发，然后转到步骤2。 请参阅AEM 6.5 [中的向后兼容性](/help/sites-deploying/backward-compatibility.md) ，了解更多详细信息。

1. **为6.5开发代码库**-为目标版本的代码库创建专用分支或存储库。 使用升级前兼容性中的信息来规划要更新的代码区域。
1. **使用6.5 Uber jar进行编译**-将代码基POM更新为指向6.5 uber jar并针对此编译代码。
1. **更新AEM自定义*** - *对AEM的任何自定义或扩展应更新／验证，以在6.5中工作并添加到6.5代码库。 包括UI搜索表单、资产自定义，以及使用/mnt/overlay的任何内容

1. **部署到6.5环境** -应在开发/QA环境中停止AEM 6.5（作者+发布）的干净实例。 应部署更新的代码库和代表性的内容示例（来自当前生产）。
1. **QA验证和错误修复** - QA应验证6.5的作者实例和Publish实例上的应用程序。发现的所有错误应被修复并提交到6.5代码库。 根据需要重复开发周期，直到修复所有错误。

在继续进行升级之前，您应该拥有一个稳定的应用程序代码库，该库已针对AEM的目标版本进行了彻底测试。 根据测试中的观察结果，可以有方法优化自定义代码。 这可能包括重构代码以避免遍历存储库、自定义索引以优化搜索，或在JCR中使用无序节点等。

除了升级代码库和自定义以与新AEM版本一起使用的选项外，6.5还帮助使用本页所述的向后兼容性功能更有效地管理 [自定义](/help/sites-deploying/backward-compatibility.md)。

如上所述，如下图所示，在第一步中运行 [Pattern Detector](/help/sites-deploying/pattern-detector.md) ，将帮助您评估升级的整体复杂性，以及您是希望以兼容模式运行还是更新自定义以使用所有新AEM 6.5功能。 有关详细信息， [请参阅AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md) 。
[ ![opt_scropten](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升级代码库 {#upgrade-code-base}

### 在版本控制中为6.5代码创建专用分支 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

AEM实施所需的所有代码和配置都应使用某种形式的版本控制进行管理。 应创建版本控制中的专用分支，以管理AEM目标版中代码库所需的任何更改。 将在此分支中管理针对AEM的目标版本对代码库进行的迭代测试和后续错误修复。

### 更新AEM Uber Jar版本 {#update-the-aem-uber-jar-version}

AEM Uber jar将所有AEM API作为单个依赖项包含在Maven项目的中 `pom.xml`。 将Uber Jar作为单个依赖关系而不是包含单个AEM API依赖关系，这始终是最佳做法。 升级代码库时，应将Uber Jar的版本更改为指向AEM的目标版本。 如果您的项目是在Uber Jar存在之前在AEM版本上进行开发的，则所有单独的AEM API依赖关系应被删除，并由AEM目标版本的Uber Jar的单独包含所取代。 然后，应根据新版Uber Jar重新编译代码库。 应更新任何已弃用的API或方法，使其与AEM的目标版本兼容。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 逐步停止使用管理资源解析程序 {#phase-out-use-of-administrative-resource-resolver}

在AEM 6.0之前的代 `SlingRepository.loginAdministrative()` 码库 `ResourceResolverFactory.getAdministrativeResourceResolver()` 中，使用管理会话的情况非常普遍。由于安全原因，这些方法的访问级别过于宽泛，因此已弃用。 [在Sling的未来版本中，这些方法将被删除](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication)。 强烈建议重新构造任何代码以改用服务用户。 有关服务用户以及如 [何逐步退出管理会话的更多信息，请参阅此处](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)。

### 查询和Oak索引 {#queries-and-oak-indexes}

在升级代码库时，需要对代码库中的查询进行彻底的测试。 对于从Jackrabbit 2（AEM版本低于6.0）升级的客户，这一点尤其重要，因为Oak不会自动索引内容，并且可能需要创建自定义索引。 如果从AEM 6.x版本升级，现成的Oak索引定义可能已更改，并可能影响现有查询。

有多种工具可用于分析和检查查询性能：

* [AEM索引工具](/help/sites-deploying/queries-and-indexing.md)

* [操作诊断工具-查询性能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Oak Utils](https://oakutils.appspot.com/)。 这是一个不由Adobe维护的开放源代码工具。

### Classic UI Authoring {#classic-ui-authoring}

经典UI创作在AEM 6.5中仍可用，但已弃用。 此处可找到更多 [信息](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)。 如果应用程序当前在经典UI创作环境上运行，则建议升级到AEM 6.5并继续使用经典UI。 然后，可以将迁移到触屏UI计划为单独的项目，以在多个开发周期中完成。 要在AEM 6.5中使用经典UI，需要将多个OSGi配置提交到代码库。 有关如何配置此组件的更多详细信息，请在此 [处找到](/help/sites-administering/enable-classic-ui.md)。

## 与6.5存储库结构对齐 {#align-repository-structure}

为了使升级更简单，并确保升级过程中不会覆盖配置，将存储库重新调整为6.4格式，以将内容与配置分开。

因此，必须将许多设置移至不再像 `/etc` 过去那样驻留。 要查看必须在更新到AEM 6.4中查看和修正的完整存储库重组问题集，请参阅AEM 6.4中的 [存储库重组](/help/sites-deploying/repository-restructuring.md)。

## AEM自定义 {#aem-customizations}

需要标识AEM源版本中对AEM创作环境的所有自定义。 识别后，建议将每个自定义存储在版本控制中或作为内容包的一部分以最低备份速率进行存储。 在生产升级之前，应在运行AEM目标版本的QA或分阶段环境中部署和验证所有自定义。

### 一般叠加 {#overlays-in-general}

通常，通过在/libs下覆盖节点和／或文件（在/apps下包含其他节点），将AEM功能扩展到开箱即用。 应在版本控制中跟踪这些叠加，并针对AEM的目标版本进行测试。 如果文件（无论是JS、JSP、HTL）被覆盖，建议对已增强的功能留下注释，以便更轻松地对AEM的目标版进行回归测试。 有关一般叠加的更多信息，请访 [问](/help/sites-developing/overlays.md)。 有关特定AEM叠加的说明，请参阅下文。

### 升级自定义搜索表单 {#upgrading-custom-search-forms}

自定义搜索彩块化需要在升级后进行一些手动调整，才能正常工作。 有关详细信息，请参 [阅升级自定义搜索表单](/help/sites-deploying/upgrading-custom-search-forms.md)。

### 资产UI自定义 {#assets-ui-customizations}

>[!NOTE]
>
>仅从AEM 6.2以前的版本升级时需要此过程。

需要为升级准备具有自定义资产部署的实例。 这是为了确保所有自定义内容都与新的6.4节点结构兼容而必需的。

您可以通过执行以下操作，为资产UI准备自定义：

1. 在需要升级的实例上，转到 *https://server:port/crx/de/index.jsp*

1. 转到以下节点：

   * `/apps/dam/content`

1. 将内容节点重命 **名为content_backup**。 为此，可以右键单击窗口左侧的资源管理器窗格并选择“重命名” ****。

1. 重命名节点后，在命名内容下创建一个名为content的 `/apps/dam` 新节 **点** ，并将其节点类型设置为 **sling:Folder**。

1. 将content_backup的所有子节 **点移到新创建的内容节点** 。 为此，可以在资源管理器窗格中右键单击每个子节点并选择“移 **动”**。

1. 删除 **content_backup节点** 。

1. 理想情况下，应 `/apps/dam``sling:Folder` 将具有正确节点类型的下方更新的节点保存到版本控制中，并使用代码库进行部署，或者至少备份为内容包。

### 为现有资产生成资产ID {#generating-asset-ids-for-existing-assets}

要为现有资产生成资产ID，请在将AEM实例升级到运行AEM 6.5时升级资产。这是启用资产分析功 [能所必需的](/help/assets/touch-ui-asset-insights.md)。 有关详细信息，请参阅 [添加嵌入代码](/help/assets/touch-ui-using-page-tracker.md#add-embed-code)。

要升级资产，请在JMX控制台中配置“关联资产ID”包。 根据存储库中的资产数量，可能 `migrateAllAssets` 需要很长时间。 我们的内部测试估计，TarMK上的12.5万个资产大约需要1小时。

![1487758945977](assets/1487758945977.png)

如果您需要整个资产的子集的资产ID，请使用 `migrateAssetsAtPath` API。

为所有其他目的，请使用 `migrateAllAssets()` API。

### InDesign脚本自定义 {#indesign-script-customizations}

Adobe建议将自定义脚本放在 `/apps/settings/dam/indesign/scripts` 位置。 有关InDesign Script自定义的更多信息，请访 [问](/help/assets/indesign.md#configuring-the-aem-assets-workflow)。

### 恢复ContextHub配置 {#recovering-contexthub-configurations}

ContextHub配置受升级影响。 有关如何恢复现有ContextHub配置的说明，请 [访问](/help/sites-administering/contexthub-config.md#recovering-contexthub-configurations-after-upgrading)。

### 工作流自定义 {#workflow-customizations}

更新开箱即用的修改工作流以添加或删除不需要的功能是常见的做法。 DAM更新资产工作流是自定义的常见工作流。 自定义实施所需的所有工作流都应备份并存储在版本控制中，因为升级过程中可能会覆盖它们。

### 可编辑的模板 {#editable-templates}

>[!NOTE]
>
>此过程仅对使用AEM 6.2中的可编辑模板的站点升级是必需的

可编辑模板的结构在AEM 6.2和6.3之间发生了更改。如果您是从6.2或更低版本升级，并且站点内容是使用可编辑的模板构建的，则需要使用响应式节 [点清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)。 该工具用于在升级 **后运行** ，以便清理内容。 它需要同时在作者层和发布层上运行。

### CUG实施更改 {#cug-implementation-changes}

已关闭的用户组的实施已发生重大更改，以解决AEM早期版本中的性能和可伸缩性限制。 CUG的先前版本在6.3中已弃用，新实现仅在触屏UI中受支持。 如果您是从6.2或更低版本升级，则此处可找到迁移到新CUG实施的说 [明](/help/sites-administering/closed-user-groups.md#upgradetoaem63)。

## 测试过程 {#testing-procedure}

应为测试升级准备一个全面的测试计划。 测试升级后的代码库和应用程序需要首先在较低的环境中完成。 发现的所有错误应以迭代方式修复，直到代码库稳定，然后才应升级更高级别的环境。

### 测试升级过程 {#testing-the-upgrade-procedure}

应按照自定义运行手册中的说明在开发和QA环境上测试此处所述的升级过程(请参阅 [规划您的升级](/help/sites-deploying/upgrade-planning.md))。 应重复升级过程，直到升级运行手册中记录了所有步骤并且升级过程平稳。

### 实施测试区域 {#implementation-test-areas-}

以下是任何AEM实施的关键区域，在升级环境并部署升级的代码库后，测试计划应涵盖这些区域。

<table>
 <tbody>
  <tr>
   <td><strong>功能测试区域</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>发布站点</td>
   <td>通过调度程序在发布层测试AEM实施和关联代码<br /> 。 应包含页面更新和缓存失效的条件<br /> 。</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>在创作层测试AEM实施和关联代码。 应包括页面、组件创作和对话框。</td>
  </tr>
  <tr>
   <td>与Marketing Cloud解决方案集成</td>
   <td>验证与Analytics、DTM和目标等产品的集成。</td>
  </tr>
  <tr>
   <td>与第三方系统集成</td>
   <td>任何第三方集成都应在作者层和发布层上进行验证。</td>
  </tr>
  <tr>
   <td>身份验证、安全性和权限</td>
   <td>应验证LDAP/SAML等任何身份验证机制。<br /> 应在作者层和发布层上测试权限和组<br /> 。</td>
  </tr>
  <tr>
   <td>查询</td>
   <td>应测试自定义索引和查询以及查询性能。</td>
  </tr>
  <tr>
   <td>UI自定义</td>
   <td>在创作环境中对AEM UI的任何扩展或自定义。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>自定义和／或开箱即用的工作流和功能。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td>应在模拟真实场景的作者层和发布层上执行负载测试。</td>
  </tr>
 </tbody>
</table>

### 文档测试计划和结果 {#document-test-plan-and-results}

应创建涵盖上述实施测试区域的测试计划。 在很多情况下，根据作者和发布任务列表分隔测试计划是有意义的。 升级生产环境之前，应在开发、QA和阶段环境上执行此测试计划。 应在较低的环境上捕获测试结果和性能指标，以便在升级Stage和Production环境时进行比较。
