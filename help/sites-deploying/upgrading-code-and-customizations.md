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
feature: 升级
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---

# 升级代码和自定义{#upgrading-code-and-customizations}

在规划升级时，需要调查和解决实施的以下方面。

* [升级代码库](#upgrade-code-base)
* [与6.5存储库结构保持一致](#align-repository-structure)
* [AEM自定义](#aem-customizations)
* [测试过程](#testing-procedure)

## 概述 {#overview}

1. **模式检测器**  — 运行模式检测器(如升级计划中所述，详见本 [](/help/sites-deploying/pattern-detector.md) 页)，以获取模式检测器报告，其中除AEM Target版本中不可用的API/包之外，还包含需要解决的区域的更多详细信息。模式检测报告应当指示代码中存在任何不兼容之处，如果不存在不兼容之处，则部署已兼容6.5，您仍可以选择使用6.5功能进行新开发，但您不仅需要它来保持兼容性。 如果报告了不兼容性，则您可以选择a)在兼容性模式下运行，并推迟开发以获得新的6.5功能或兼容性；b)在升级后决定进行开发，然后转到步骤2。 有关更多详细信息，请参阅AEM 6.5](/help/sites-deploying/backward-compatibility.md)中的[向后兼容性。

1. **为6.5开发代码库** — 为Target版本的代码库创建专用分支或存储库。 使用升级前兼容性中的信息来规划要更新的代码区域。
1. **使用6.5 Uber jar **进行编译 — 更新代码库POM以指向6.5 uber jar并针对此编译代码。
1. **更新AEM自定义*** - *对AEM的任何自定义或扩展都应进行更新/验证，以便在6.5中正常工作，并添加到6.5代码库中。包括UI搜索Forms、资产自定义，以及使用/mnt/overlay的任何内容

1. **部署到6.5环境**  — 在开发/QA环境中，应当停止使用AEM 6.5（创作+发布）的干净实例。应该部署更新的代码库和具有代表性的内容示例（来自当前生产环境）。
1. **QA验证和错误修复**  - QA应在6.5的创作实例和发布实例上验证应用程序。发现的任何错误都应被修复并提交到6.5代码库。根据需要重复开发周期，直到修复所有错误。

在继续升级之前，您应该拥有一个稳定的应用程序代码库，该代码库已针对目标版本的AEM进行了彻底测试。 根据测试中的观察，可以使用各种方法来优化自定义代码。 这可能包括重构代码以避免遍历存储库、自定义索引以优化搜索，或在JCR中使用未排序的节点等。

除了升级代码库和自定义以与新AEM版本配合使用的选项外， 6.5还有助于使用[此页面](/help/sites-deploying/backward-compatibility.md)中所述的“向后兼容性”功能更高效地管理自定义。

如上图所示，在第一步中运行[模式检测器](/help/sites-deploying/pattern-detector.md)将帮助您评估升级的整体复杂性，以及您是希望在兼容模式下运行还是更新自定义以使用所有新的AEM 6.5功能。 有关更多详细信息，请参阅AEM 6.5](/help/sites-deploying/backward-compatibility.md)中的[向后兼容性页面。
[ ![opt_scrift](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升级代码库{#upgrade-code-base}

### 在版本控制{#create-a-dedicated-branch-for-6.5-code-in-version-control}中为6.5代码创建专用分支

您的AEM实施所需的所有代码和配置都应使用某种形式的版本控制进行管理。 应在版本控制中创建专用分支，以管理目标版本AEM中代码库所需的任何更改。 此分支将管理针对AEM目标版本对代码库进行的迭代测试和后续错误修复。

### 更新AEM Uber Jar版本{#update-the-aem-uber-jar-version}

AEM Uber Jar将所有AEM API作为单个依赖项包含在Maven项目的`pom.xml`中。 最好将Uber Jar作为单个依赖项包含在内，而不是包含单个AEM API依赖项。 在升级代码库时，应更改Uber Jar的版本，以指向目标版本的AEM。 如果您的项目是在AEM Jar存在之前基于Uber版本开发的，则所有单独的AEM API依赖项都应删除，并替换为目标版本AEM的Uber Jar中的单一包含。 然后，应根据新版Uber Jar重新编译代码库。 任何已弃用的API或方法都应进行更新，以与AEM的目标版本兼容。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 停止使用管理资源解析程序{#phase-out-use-of-administrative-resource-resolver}

通过`SlingRepository.loginAdministrative()`和`ResourceResolverFactory.getAdministrativeResourceResolver()`使用管理会话在AEM 6.0之前的代码库中非常普遍。由于这些方法提供的访问级别过于广泛，因此出于安全原因，这些方法已被弃用。 [在Sling的未来版本中，将删除这些方法](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication)。强烈建议重构任何代码以改用服务用户。 有关服务用户和[如何逐步停用管理会话的更多信息，请参阅此处](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)。

### 查询和Oak索引{#queries-and-oak-indexes}

在升级代码库时，需要对代码库中查询的任何使用进行全面测试。 对于从Jackrabbit 2(AEM 6.0以上版本)升级的客户，这一点尤其重要，因为Oak不会自动为内容编入索引，并且可能需要创建自定义索引。 如果从AEM 6.x版本升级，则开箱即用的Oak索引定义可能已发生更改，并且可能会影响现有查询。

有几种工具可用于分析和检查查询性能：

* [AEM索引工具](/help/sites-deploying/queries-and-indexing.md)

* [操作诊断工具 — 查询性能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Oak实用工具](https://oakutils.appspot.com/)。这是一个开源工具，不由Adobe维护。

### 经典UI创作{#classic-ui-authoring}

经典UI创作在AEM 6.5中仍可用，但现已弃用。 有关更多信息，请参见[此处](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)。 如果您的应用程序当前在经典UI创作环境中运行，则建议升级到AEM 6.5并继续使用经典UI。 然后，可以将迁移到触屏UI作为单独的项目进行规划，以在多个开发周期内完成。 要在AEM 6.5中使用经典UI，需要将多个OSGi配置提交到代码库。 有关如何配置此子域的更多详细信息，请参见[此处](/help/sites-administering/enable-classic-ui.md)。

## 与6.5存储库结构{#align-repository-structure}一致

为了简化升级过程并确保配置在升级期间不被覆盖，在6.4中重组了存储库，以将内容与配置分离。

因此，必须将许多设置移动到不再像过去那样驻留在`/etc`下。 要查看必须在更新到AEM 6.4的过程中查看和修正的完整的存储库重组问题，请参阅AEM 6.4](/help/sites-deploying/repository-restructuring.md)中的[存储库重组。

## AEM自定义{#aem-customizations}

需要识别AEM源版本中对AEM创作环境的所有自定义设置。 确定后，建议将每个自定义都存储在版本控制中，或作为内容包的一部分至少备份一次。 在生产升级之前，应在运行AEM目标版本的QA或暂存环境中部署和验证所有自定义设置。

### 一般{#overlays-in-general}的叠加

通常的做法是，通过在/libs下的节点和/或文件上叠加/apps下的其他节点，来扩展AEM的开箱即用功能。 应在版本控制中跟踪这些叠加，并针对AEM的目标版本进行测试。 如果文件（无论是JS、JSP、HTL）被覆盖，建议对已增强的功能留下注释，以便在AEM的目标版本上更轻松地进行回归测试。 有关一般叠加的详细信息，请在[此处](/help/sites-developing/overlays.md)找到。 有关特定AEM叠加的说明，请参阅下文。

### 升级自定义搜索Forms {#upgrading-custom-search-forms}

自定义搜索彩块化需要在升级后进行一些手动调整，才能正常运行。 有关更多详细信息，请参阅[升级自定义搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md)。

### 资产UI自定义{#assets-ui-customizations}

>[!NOTE]
>
>只有从AEM 6.2以前的版本升级时，才需要执行此过程。

需要为具有自定义资产部署的实例准备升级。 需要此功能才能确保所有自定义内容与新的6.4节点结构兼容。

您可以通过执行以下操作，为资产UI准备自定义设置：

1. 在需要升级的实例上，转到&#x200B;*https://server:port/crx/de/index.jsp*&#x200B;打开CRXDE Lite

1. 转到以下节点：

   * `/apps/dam/content`

1. 将内容节点重命名为&#x200B;**content_backup**。 为此，可以右键单击窗口左侧的资源管理器窗格并选择&#x200B;**重命名**。

1. 重命名节点后，在名为&#x200B;**content**&#x200B;的`/apps/dam`下创建一个名为content的新节点，并将其节点类型设置为&#x200B;**sling:Folder**。

1. 将&#x200B;**content_backup**&#x200B;的所有子节点移动到新创建的内容节点。 为此，可以右键单击资源管理器窗格中的每个子节点，然后选择&#x200B;**移动**。

1. 删除&#x200B;**content_backup**&#x200B;节点。

1. 理想情况下，应将`/apps/dam`下更新的节点（节点类型为`sling:Folder`）保存到版本控件中，并与代码库一起部署，或至少备份为内容包。

### 为现有资产生成资产ID {#generating-asset-ids-for-existing-assets}

要为现有资产生成资产ID，请在升级AEM实例以运行AEM 6.5时升级资产。要启用[资产分析功能](/help/assets/asset-insights.md)，需要此功能。 有关更多详细信息，请参阅[添加嵌入代码](/help/assets/use-page-tracker.md#add-embed-code)。

要升级资产，请在JMX控制台中配置关联资产ID包。 根据存储库中的资产数量， `migrateAllAssets`可能需要较长时间。 我们的内部测试估计TarMK上的12.5万个资产大约需要1小时。

![1487758945977](assets/1487758945977.png)

如果您需要为整个资产的子集使用资产ID，请使用`migrateAssetsAtPath` API。

出于所有其他目的，请使用`migrateAllAssets()` API。

### InDesign脚本自定义{#indesign-script-customizations}

Adobe建议在`/apps/settings/dam/indesign/scripts`位置放置自定义脚本。 有关InDesign脚本自定义的更多信息，请在[此处](/help/assets/indesign.md#configuring-the-aem-assets-workflow)找到。

### 恢复ContextHub配置{#recovering-contexthub-configurations}

ContextHub配置受升级的影响。 有关如何恢复现有ContextHub配置的说明，请参见[此处](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)。

### 工作流自定义{#workflow-customizations}

通常做法是，更新开箱即用的修改工作流，以添加或删除不需要的功能。 自定义的常见工作流是[!UICONTROL DAM更新资产]工作流。 自定义实施所需的所有工作流都应进行备份并存储在版本控制中，因为升级期间可能会覆盖这些工作流。

### 可编辑的模板 {#editable-templates}

>[!NOTE]
>
>仅当使用AEM 6.2中的可编辑模板进行站点升级时，才需要执行此过程

可编辑模板的结构在AEM 6.2和6.3之间发生了更改。如果您从6.2或更早版本进行升级，并且如果您的网站内容是使用可编辑模板构建的，则需要使用[响应式节点清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)。 该工具用于在&#x200B;**升级后运行**&#x200B;以清理内容。 它需要同时在创作层和发布层上运行。

### CUG实施更改{#cug-implementation-changes}

已关闭的用户组的实施已发生重大更改，以解决以前版本的AEM中存在的性能和可扩展性限制。 6.3中已弃用CUG的先前版本，并且仅触屏UI支持新实施。 如果您从6.2或更低版本升级，则[此处](/help/sites-administering/closed-user-groups.md#upgradetoaem63)可找到迁移到新CUG实施的说明。

## 测试过程{#testing-procedure}

应为测试升级准备全面的测试计划。 首先，需要在较低的环境中测试已升级的代码库和应用程序。 发现的任何错误都应以迭代方式修复，直到代码库稳定为止，只有这样才应升级更高级别的环境。

### 测试升级过程{#testing-the-upgrade-procedure}

应在开发和QA环境中测试此处所述的升级过程，如自定义运行手册中所述（请参阅[规划升级](/help/sites-deploying/upgrade-planning.md)）。 应重复升级过程，直到升级运行手册中记录了所有步骤，并且升级过程顺利。

### 实施测试区域{#implementation-test-areas-}

以下是任何AEM实施的关键区域，在升级环境并部署升级的代码库后，测试计划应涵盖这些区域。

<table>
 <tbody>
  <tr>
   <td><strong>功能测试区</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>已发布的站点</td>
   <td>通过调度程序在发布层<br />上测试AEM实施和关联代码。 应包括页面更新和<br />缓存失效的条件。</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>在创作层测试AEM实施和关联代码。 应包括页面、组件创作和对话框。</td>
  </tr>
  <tr>
   <td>与Marketing Cloud解决方案集成</td>
   <td>验证与Analytics、DTM和Target等产品的集成。</td>
  </tr>
  <tr>
   <td>与第三方系统集成</td>
   <td>应在创作层和发布层上验证任何第三方集成。</td>
  </tr>
  <tr>
   <td>身份验证、安全性和权限</td>
   <td>应验证任何身份验证机制，如LDAP/SAML。<br /> 应在创作层和发布层上对权限和组进行<br /> 测试。</td>
  </tr>
  <tr>
   <td>查询</td>
   <td>自定义索引和查询应与查询性能一起进行测试。</td>
  </tr>
  <tr>
   <td>UI自定义</td>
   <td>创作环境中对AEM UI的任何扩展或自定义设置。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>自定义和/或开箱即用的工作流和功能。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td>应对模拟真实情景的创作层和发布层执行负载测试。</td>
  </tr>
 </tbody>
</table>

### 文档测试计划和结果{#document-test-plan-and-results}

应创建涵盖上述实施测试区域的测试计划。 在很多情况下，可以按“创作”和“发布”任务列表来分隔测试计划。 在升级生产环境之前，应在开发、QA和暂存环境中执行此测试计划。 应在较低的环境中捕获测试结果和性能量度，以便在升级暂存环境和生产环境时进行比较。
