---
title: 升级代码和自定义项
description: 了解有关在AEM中升级代码和自定义设置的更多信息。
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 0%

---

# 升级代码和自定义项{#upgrading-code-and-customizations}

在计划升级时，必须调查并解决实施的以下方面。

* [升级代码库](#upgrade-code-base)
* [与6.5存储库结构保持一致](#align-repository-structure)
* [AEM自定义](#aem-customizations)
* [测试过程](#testing-procedure)

## 概述 {#overview}

1. **模式检测器**  — 运行模式检测器，如升级计划中所述，详见 [此页面](/help/sites-deploying/pattern-detector.md). 您会获得一个模式检测器报告，该报告包含有关AEM Target版本中除了API/捆绑包不可用之外还必须解决的区域的更多详细信息。 模式检测报告会向您指示代码中的任何不兼容性。 如果不存在任何部署，则表明您的部署已经与6.5兼容。 您仍然可以选择为使用6.5功能执行新开发，但并非只是为了保持兼容性。 如果报告了不兼容情况，您可以选择在兼容模式下运行，并推迟开发新的6.5功能或兼容性。 或者，您可以在升级后决定进行开发，并转到步骤2。 请参阅 [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md) 以了解更多详细信息。

1. **开发6.5代码库** — 为Target版本的代码库创建专用分支或存储库。 使用升级前兼容性中的信息来规划要更新的代码区域。
1. **使用6.5 Uber jar编译** — 更新代码库POM以指向6.5 uber jar并编译针对它的代码。
1. **更新AEM自定义设置*** - *AEM的任何自定义项或扩展都应更新/验证以在6.5中正常工作，并添加到6.5代码库中。 包括UI Search Forms、Assets自定义、使用/mnt/overlay的任何内容

1. **部署到6.5环境**  — 应在开发/QA环境中站立AEM 6.5的干净实例（创作+发布）。 应部署更新后的代码库和有代表性的内容示例（来自当前生产）。
1. **QA验证和错误修复** - QA应在6.5的“创作”和“发布”实例上验证应用程序。找到的任何错误都应修复并提交到6.5代码库。 根据需要重复Dev-Cycle，直到修复所有错误。

在继续升级之前，您应该有一个稳定的应用程序代码库，该代码库已针对AEM的目标版本进行了彻底测试。 根据测试中所做的观察，可以找到优化自定义代码的方法。 例如，其中可能包括重构代码以避免遍历存储库、自定义索引以优化搜索，或在JCR中使用无序节点等。

除了可以选择升级代码库和自定义以与新AEM版本配合使用外，6.5还可以通过向后兼容性功能更有效地管理自定义项，如中所述 [此页面](/help/sites-deploying/backward-compatibility.md).

如上所述和下图所示，运行 [模式检测器](/help/sites-deploying/pattern-detector.md) 在第一步中，可以帮助您评估升级的整体复杂性。 它还可以帮助您决定是要以兼容模式运行，还是更新自定义项以使用所有新的AEM 6.5功能。 请参阅 [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md) 页面，以了解更多详细信息。
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升级代码库 {#upgrade-code-base}

### 在版本控制中为6.5代码创建专用分支 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

应使用某种形式的版本控制来管理实施AEM所需的所有代码和配置。 应创建版本控制中的专用分支，以管理目标版本AEM中的代码库所需的任何更改。 此分支管理针对AEM的目标版本迭代测试代码库以及后续错误修复。

### 更新AEM Uber Jar版本 {#update-the-aem-uber-jar-version}

AEM Uber jar包含所有AEM API，作为您Maven项目的 `pom.xml`. 最佳做法始终是将Uber Jar作为单个依赖项包含在内，而不是包含单个AEM API依赖项。 升级代码库时，将Uber Jar的版本更改为指向AEM的目标版本。 如果您的项目是在Uber Jar存在之前的AEM版本上开发的，请删除所有单独的AEM API依赖项。 替换为包含AEM目标版本的Uber Jar的单个变量。 针对新版本的Uber Jar重新编译代码库。 更新任何已弃用的API或方法，以便与AEM的目标版本兼容。

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

通过使用管理会话 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 在AEM 6.0之前的代码库中非常普遍。出于安全原因，这些方法已被弃用，因为它们提供的访问级别过于宽泛。 [在Sling的未来版本中，将删除这些方法](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 强烈建议重构任何代码以改用服务用户。 有关服务用户和的详细信息 [可在此处找到如何逐步停用管理讲座](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### 查询和Oak索引 {#queries-and-oak-indexes}

在代码库中使用任何查询都必须作为升级代码库的一部分进行彻底测试。 对于从Jackrabbit 2(AEM 6.0之前的版本)升级的客户，此测试尤其重要，因为Oak不会自动为内容编制索引，并且应创建自定义索引。 如果从AEM 6.x版本升级，开箱即用的Oak索引定义可能已更改，并且可能影响现有查询。

以下工具可用于分析和检查查询性能：

* [AEM Index Tools](/help/sites-deploying/queries-and-indexing.md)

* [操作诊断工具 — 查询性能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### 经典UI创作 {#classic-ui-authoring}

经典UI创作在AEM 6.5中仍然可用，但已被弃用。 可以找到更多信息 [此处](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). 如果您的应用程序在经典UI创作环境中运行，建议升级到AEM 6.5并继续使用经典UI。 然后，可以计划作为单独的项目迁移到Touch UI，以便通过多个开发周期完成。 要在AEM 6.5中使用经典UI，必须将多个OSGi配置提交到代码库。 有关如何进行配置的更多详细信息，请参阅 [此处](/help/sites-administering/enable-classic-ui.md).

## 与6.5存储库结构保持一致 {#align-repository-structure}

为了更轻松地进行升级并确保在升级期间不会覆盖配置，在6.4中重组了存储库，以将内容与配置分开。

因此，必须移动多个设置才能使其不再位于 `/etc` 和过去一样。 要查看必须在AEM 6.4的更新版中审查和解决的整套存储库重构问题，请参阅 [AEM 6.4中的存储库重组](/help/sites-deploying/repository-restructuring.md).

## AEM自定义  {#aem-customizations}

必须标识AEM源版本中AEM创作环境的所有自定义项。 一旦标识，建议将每个自定义项都存储在版本控制中，或至少作为内容包的一部分进行备份。 在进行生产升级之前，应在运行目标版本的AEM的QA或暂存环境中部署和验证所有自定义项。

### 叠加一般信息 {#overlays-in-general}

常见的做法是扩展AEM的开箱即用功能，方法是使用/apps下的其他节点覆盖/libs下的节点和/或文件。 应在版本控制中跟踪这些叠加，并针对AEM的目标版本进行测试。 如果文件（如JS、JSP、HTL）被覆盖，Adobe建议您就增强的功能发表评论，以便于对AEM的目标版本进行回归测试。 有关叠加的一般更多信息，请参阅 [此处](/help/sites-developing/overlays.md). 特定AEM叠加图的说明可在下面找到。

### 升级自定义搜索Forms {#upgrading-custom-search-forms}

自定义搜索彩块化需要在升级后进行一些手动调整才能正常运行。 有关更多详细信息，请参阅 [升级自定义搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md).

### Assets UI自定义 {#assets-ui-customizations}

>[!NOTE]
>
>只有从AEM 6.2之前的版本进行升级时，才需要执行此过程。

必须准备已自定义Assets部署的实例以进行升级。 要确保所有自定义内容与新的6.4节点结构兼容，必须执行此操作。

您可以通过执行以下操作为Assets UI准备自定义项：

1. 在要升级的实例上，打开CRXDE Lite，方法是转到 *https://server:port/crx/de/index.jsp*

1. 转到以下节点：

   * `/apps/dam/content`

1. 将内容节点重命名为 **content_backup** 右键单击窗口左侧的浏览器窗格，然后选择 **重命名**.

1. 重命名节点后，在下创建名为内容的节点 `/apps/dam` 已命名 **内容** 并将其节点类型设置为 **sling：Folder**.

1. 移动的所有子节点 **content_backup** 到新创建的内容节点，方法是在资源管理器窗格中右键单击每个子节点并选择 **移动**.

1. 删除 **content_backup** 节点。

1. 下方的更新节点 `/apps/dam` 具有正确的节点类型 `sling:Folder` 理想情况下，应保存到版本控制中，并与代码库一起部署，或者至少作为内容包进行备份。

### 为现有资源生成资源ID {#generating-asset-ids-for-existing-assets}

要为现有资源生成资源ID，请在升级AEM实例以运行AEM 6.5时升级资源。要启用 [资产分析功能](/help/assets/asset-insights.md). 有关更多详细信息，请参阅 [添加嵌入代码](/help/assets/use-page-tracker.md#add-embed-code).

要升级资产，请在JMX控制台中配置关联资产ID包。 根据存储库中的资源数， `migrateAllAssets` 可能要花很长时间 Adobe的内部测试估计，TarMK上的125000资产大约需要1小时。

![1487758945977](assets/1487758945977.png)

如果您需要整个资产的子集具备资产ID，请使用 `migrateAssetsAtPath` API。

对于所有其他目的，请使用 `migrateAllAssets()` API。

### InDesign脚本自定义 {#indesign-script-customizations}

Adobe建议将自定义脚本放在 `/apps/settings/dam/indesign/scripts` 位置。 可以找到有关InDesign脚本自定义设置的更多信息 [此处](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### 恢复ContextHub配置 {#recovering-contexthub-configurations}

ContextHub配置受升级影响。 有关如何恢复现有ContextHub配置的说明，请参见 [此处](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### 工作流自定义 {#workflow-customizations}

常用做法是编辑现成的工作流，以添加或删除不需要的功能。 自定义的常见工作流是 [!UICONTROL DAM更新资产] 工作流。 自定义实施所需的所有工作流都应进行备份，并存储在版本控制中，因为升级期间可能会覆盖这些工作流。

### 可编辑模板 {#editable-templates}

>[!NOTE]
>
>仅当使用AEM 6.2中的可编辑模板进行站点升级时，才需要执行此过程

可编辑模板的结构在AEM 6.2和6.3之间发生了变化。如果您是从6.2或更低版本升级，并且您的站点内容是使用可编辑的模板构建的，则必须使用 [响应节点清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). 该工具旨在运行 **之后** 升级以清理内容。 在创作层和发布层上运行它。

### CUG实施更改 {#cug-implementation-changes}

封闭用户组的实施发生了重大变化，以前的版本AEM在性能和可扩展性方面存在限制。 6.3中弃用了以前版本的CUG，并且仅在Touch UI中支持新的实施。 如果您是从6.2或更早版本升级，则可以找到迁移到新CUG实施的说明 [此处](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## 测试过程 {#testing-procedure}

应该为测试升级准备全面的测试计划。 测试已升级的代码库和应用程序必须先在较低的环境中完成。 发现的错误应以迭代方式修复，直到代码库稳定为止，只有到那时才应升级更高级别的环境。

### 测试升级过程 {#testing-the-upgrade-procedure}

此处概述的升级过程应在开发和QA环境中进行测试，如自定义运行手册中所述(请参阅 [规划升级](/help/sites-deploying/upgrade-planning.md))。 应重复升级过程，直到所有步骤都记录在升级运行手册中且升级过程顺利完成。

### 实施测试区域  {#implementation-test-areas-}

以下是任何AEM实施的关键部分，在升级环境并部署升级后的代码库后，测试计划应涵盖这些关键部分。

<table>
 <tbody>
  <tr>
   <td><strong>功能测试区域</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>已发布的站点</td>
   <td>在发布层上测试AEM实现和相关代码<br /> 通过Dispatcher。 应包括页面更新的标准和<br /> 缓存失效。</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>在创作层上测试AEM实现和相关代码。 应包括页面、组件创作和对话框。</td>
  </tr>
  <tr>
   <td>与Experience Cloud解决方案集成</td>
   <td>验证与Analytics、DTM和Target等产品的集成。</td>
  </tr>
  <tr>
   <td>与第三方系统的集成</td>
   <td>验证创作层和发布层上的任何第三方集成。</td>
  </tr>
  <tr>
   <td>身份验证、安全和权限</td>
   <td>任何身份验证机制（如LDAP/SAML）都应进行验证。<br /> 应在“创作”和“发布”页面上测试权限和组<br /> 层。</td>
  </tr>
  <tr>
   <td>查询</td>
   <td>应测试自定义索引和查询以及查询性能。</td>
  </tr>
  <tr>
   <td>UI自定义</td>
   <td>创作环境中AEM UI的任何扩展或自定义设置。</td>
  </tr>
  <tr>
   <td>工作流</td>
   <td>自定义和/或现成的工作流和功能。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td>加载测试应在模拟现实场景的创作层和发布层上执行。</td>
  </tr>
 </tbody>
</table>

### 记录测试计划和结果 {#document-test-plan-and-results}

应创建涵盖上述实施测试区域的测试计划。 通常，按作者和发布任务列表划分测试计划是合理之举。 此测试计划应在升级生产环境之前在开发、QA和暂存环境中执行。 测试结果和性能量度应在较低级别环境中捕获，以便在升级暂存环境和生产环境时进行比较。
