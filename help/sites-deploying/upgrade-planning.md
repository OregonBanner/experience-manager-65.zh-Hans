---
title: 规划升级
seo-title: 规划升级
description: 本文可帮助在规划AEM升级时建立明确的目标、阶段和交付项。
seo-description: 本文可帮助在规划AEM升级时建立明确的目标、阶段和交付项。
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
feature: 升级
exl-id: 0dea2b3e-fd7c-4811-a04a-6852ffc1e6d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---

# 计划升级{#planning-your-upgrade}

## AEM项目概述{#aem-project-overview}

AEM通常用于可能为数百万用户提供高影响力的部署。 在大多数情况下，实例上部署了自定义应用程序，这增加了复杂性。 升级此类部署的任何努力都需要有条不紊地加以处理。

本指南可帮助在规划升级时建立明确的目标、阶段和交付项。 它侧重于项目的整体执行和准则。 虽然它提供了实际升级步骤的概述，但是它参考了适当的可用技术资源。 它应与文件中提到的可用技术资源结合使用。

AEM升级过程需要谨慎处理规划、分析和执行阶段，并为每个阶段定义关键交付项。

请注意，可以直接从AEM 6.0版和最高6.5版升级。运行5.6.x及以下版本的客户需要先升级到6.0或更高版本，并推荐使用6.0(SP3)。 此外，自6.3起，新的OAK区段Tar格式现在用于区段节点存储，而且即使对于6.0、6.1和6.2，存储库也必须迁移到这种新格式。

>[!CAUTION]
>
>如果您从AEM 6.2升级到6.3，则应从以下版本(**6.2-SP1-CFP1 —6.2SP1-CFP12.1**)或从&#x200B;**6.2SP1-CFP15**&#x200B;开始升级。 否则，如果您从&#x200B;**6.2SP1-CFP13/6.2SP1CFP14**&#x200B;升级到AEM 6.3，则还必须至少升级到版本&#x200B;**6.3.2.2**。 否则，AEM Sites在升级后将失败。

## 升级范围和要求{#upgrade-scope-requirements}

在下面，您会找到一个典型AEM升级项目中受影响的区域列表：

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>影响</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>操作系统</td>
   <td>不确定但微妙的影响</td>
   <td>在AEM升级时，也可能需要升级操作系统，这可能会产生一些影响。</td>
  </tr>
  <tr>
   <td>Java运行时</td>
   <td>适度影响</td>
   <td>AEM 6.3需要JRE 1.7.x（64位）或更高版本。 JRE 1.8是Oracle当前唯一支持的版本。</td>
  </tr>
  <tr>
   <td>硬件</td>
   <td>适度影响</td>
   <td>联机修订版清理需要等于存储库大小的25%的可用磁盘空间和15%的可用堆空间<br />才能成功完成。 <br />您可能需要将硬件升级到<br />，以确保有足够的资源进行在线修订清理，以完全执行<br />。 此外，如果从AEM 6之前的版本升级，则<br />可能会有其他存储要求。</td>
  </tr>
  <tr>
   <td>内容存储库（CRX或Oak）</td>
   <td>高影响</td>
   <td>从版本6.1开始，AEM不支持CRX2，因此从旧版本升级时，需要迁移到<br /> Oak(CRX3)。 AEM 6.3已<br />实施了新的区段节点存储，该存储也需要迁移。 <br /> crx2oak工具用于此目的。</td>
  </tr>
  <tr>
   <td>AEM组件/内容</td>
   <td>适度影响</td>
   <td><code>/libs</code> 和<code>/apps</code>可通过升级轻松处理，但<code>/etc</code>通常需要手动重新应用一些自定义设置。</td>
  </tr>
  <tr>
   <td>AEM服务</td>
   <td>低影响</td>
   <td>大多数AEM核心服务都经过升级测试。 这是低冲击度的区域。</td>
  </tr>
  <tr>
   <td>自定义应用程序服务</td>
   <td>低到高影响</td>
   <td>根据应用程序和自定义，可能存在对JVM、操作系统版本以及某些与索引相关的<br />更改的<br />依赖关系，因为索引不会在Oak中自动生成。</td>
  </tr>
  <tr>
   <td>自定义应用程序内容</td>
   <td>低到高影响</td>
   <td>在升级之前，不能通过升级处理的内容可以备份<br />，然后移回存储库。<br /> 大多数内容都可以通过迁移工具进行处理。</td>
  </tr>
 </tbody>
</table>

请务必确保您运行的是受支持的操作系统、Java运行时、httpd和Dispatcher版本。 有关更多信息，请参阅[AEM 6.5技术要求页面](/help/sites-deploying/technical-requirements.md)。 升级这些组件需要在您的项目计划中进行说明，并且应在升级AEM之前进行。

## 项目阶段{#project-phases}

规划和执行AEM升级需要做很多工作。 为了澄清这一进程中的不同努力，我们将规划和执行练习分为不同的阶段。 在以下各节中，每个阶段都会生成一个交付项，该项目的未来阶段通常会利用该交付项。

### 编写培训计划{#planning-for-author-training}

在任何新版本中，都可能会对UI和用户工作流进行潜在的更改。 此外，新版本还引入了一些新功能，这些功能可能有助于企业利用这些功能。 我们建议您审查已引入的功能更改，并组织一个计划，以培训您的用户如何有效利用这些功能。

![unu_scrift](assets/unu_cropped.png)

AEM 6.5的新增功能可在adobe.com](/help/release-notes/release-notes.md)的[AEM部分找到。 请务必注意对组织中常用的UI或产品功能所做的任何更改。 在您查看新增功能时，还应注意任何对贵组织有价值的功能。 查看AEM 6.5中的更改后，为您的作者制定培训计划。 这可能涉及利用免费提供的资源，如通过[Adobe数字学习服务](https://www.adobe.com/training.html)提供的helpx功能视频或正式培训。

### 创建测试计划{#creating-a-test-plan}

每个客户对AEM的实施都是独特的，并且经过自定义以符合其业务要求。 因此，务必确定对系统进行的所有自定义设置，以便将它们包含在测试计划中。 此测试计划将为我们在升级实例上执行的QA过程提供动力。

![测试计划](assets/test-plan.png)

需要复制确切的生产环境，并在升级后对其执行测试，以确保所有应用程序和自定义代码仍按需要运行。 您需要重新执行所有自定义设置，并执行性能、负载和安全测试。 在组织测试计划时，除了开箱即用的UI和日常操作中利用的工作流之外，还要确保涵盖对系统进行的所有自定义设置。 这些功能包括自定义OSGi服务和Servlet、与Adobe Marketing Cloud的集成、通过AEM连接器与第三方的集成、自定义第三方集成、自定义组件和模板、AEM中的自定义UI叠加以及自定义工作流。 对于从AEM 6之前的版本迁移的客户，应当分析任何自定义查询，因为它们可能需要编入索引。 对于已使用AEM 6.x版本的客户，仍应对这些查询进行测试，以确保其索引在升级后继续有效工作。

### 确定需要的体系结构和基础架构更改{#determining-architectural-and-infrastructure-changes-needed}

升级时，您可能还需要升级技术堆栈中的其他组件，如操作系统或JVM。 此外，由于存储库组成中的更改，可能需要额外的硬件。 这通常仅适用于从6.x以前的实例迁移的客户，但务必要考虑这一点。 最后，您的操作实践可能需要做出一些更改，包括监控、维护以及备份和灾难恢复过程。

![doi_scroint](assets/doi_cropped.png)

查看AEM 6.5的技术要求，并确保您当前的硬件和软件都足够。 有关操作流程的潜在更改，请参阅以下文档：

**监控和维护：**

[操作仪表板](/help/sites-administering/operations-dashboard.md)

[Assets 监控最佳实践](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台监控服务器资源](/help/sites-administering/jmx-console.md)

[修订版清理](/help/sites-deploying/revision-cleanup.md)

**备份/恢复和灾难恢复：**

[备份和恢复](/help/sites-administering/backup-and-restore.md)

[性能和可扩展性](/help/sites-deploying/performance.md)

[如何使用TarMK冷备用运行AEM](/help/sites-deploying/tarmk-cold-standby.md)

#### 内容重组注意事项{#content-restructuring-considerations}

AEM对存储库结构进行了更改，有助于使升级更加无缝。 更改涉及根据Adobe或客户是否拥有该内容，将内容从/etc文件夹移出到包括/libs、/apps和/content的文件夹，从而限制在发布期间覆盖内容的可能性。 存储库重组的完成方式是，在6.5升级时，它不应要求更改代码，不过建议在计划升级时查看AEM](/help/sites-deploying/repository-restructuring.md)中[存储库重组的详细信息。

### 评估升级复杂性{#assessing-upgrade-complexity}

由于我们的客户在其AEM环境中所应用的自定义项的数量和性质多种多样，因此请务必提前一段时间来确定在升级过程中应该付出的总体工作量。

您可以采用两种方法来评估升级的复杂性，初步阶段只能使用新引入的模式检测器，该检测器可在AEM 6.1、6.2和6.3实例上运行。 模式检测器是使用报告的模式来评估升级的整体复杂性的最简单的方法。 模式检测器报告包含用于识别自定义代码库正在使用的不可用API的模式（这是使用6.3中的升级前兼容性检查来完成的）。

初次评估后，更全面的下一步可能是对测试实例执行升级，并执行一些基本的烟雾测试。 Adobe还提供了一些。 此外，应不仅对要升级到的版本审查[已弃用和已删除功能](/help/release-notes/deprecated-removed-features.md)的列表，还应对源版本和目标版本之间的任何版本审查。 例如，如果从AEM 6.2升级到6.5，那么除了AEM 6.5的功能之外，还务必要查看已弃用和已删除的AEM 6.3功能。

![trei_scroint](assets/trei_cropped.png)

最近引入的模式检测器应该可以相当准确地估计大多数情况下在升级过程中预期的内容。 但是，对于更复杂的自定义和部署，如果您有不兼容的更改，则可以按照[执行就地升级](/help/sites-deploying/in-place-upgrade.md)中的说明将开发实例升级到AEM 6.5。 完成后，在此环境中执行一些高级烟雾测试。 本练习的目标不是详尽地完成测试用例清单并生成缺陷的正式清单，而是粗略地估计升级代码以实现6.5兼容性所需的工作量。 如果结合[模式检测](/help/sites-deploying/pattern-detector.md)和上一节中确定的体系结构变化，则可以向项目管理团队提供粗略估计，以规划升级。

### 构建升级和回滚Runbook {#building-the-upgrade-and-rollback-runbook}

虽然Adobe记录了升级AEM实例的过程，但每位客户的网络布局、部署架构和自定义将需要对此方法进行微调和定制。 因此，我们建议您查看我们提供的所有文档，并使用这些文档来通知特定于项目的Runbook，其中概述了您将在环境中遵循的特定升级和回滚过程。 如果从CRX2升级，请确保评估从CRX2迁移到Oak时内容迁移的时长。 对于大型存储库，其数量可能很大。

![runbook-diagram](assets/runbook-diagram.png)

我们在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚过程，并在执行[就地升级](/help/sites-deploying/in-place-upgrade.md)中提供了应用升级的分步说明。 这些说明应与您的系统架构、自定义和停机时间容限一起审核并加以考虑，以确定在升级期间将执行的适当切换和回滚过程。 在起草自定义Runbook时，应包含对架构或服务器大小的任何更改。 必须指出，这应作为第一稿处理。 当您的团队完成其QA和开发周期并部署到暂存环境的升级时，可能需要执行一些其他步骤。 理想情况下，本文档应包含足够的信息，这样，如果将信息交给您的业务人员，他们将能够完全从中包含的信息完成升级。

### 制定项目计划{#developing-a-project-plan}

我们可以利用先前练习中的输出，构建一个项目计划，涵盖测试或开发工作、培训以及实际升级执行的预期时间表。

![开发项目计划](assets/develop-project-plan.png)

综合项目计划应包括：

* 最后确定发展和测试计划
* 升级开发和QA环境
* 更新AEM 6.5的自定义代码库
* QA测试和修复周期
* 升级暂存环境
* 集成、性能和负载测试
* 环境认证
* 上线

### 执行开发和QA {#performing-development-and-qa}

我们为[升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)提供了与AEM 6.5兼容的过程。在执行此迭代过程时，应根据需要对Runbook进行更改。 另请参阅AEM 6.5](/help/sites-deploying/backward-compatibility.md)中的[向后兼容性，以了解有关自定义如何在大多数情况下保持向后兼容，而无需在升级后立即进行开发的信息。

![patru_scroint](assets/patru_cropped.png)

开发和测试过程通常是一个迭代过程。 由于自定义，升级期间所做的更改可能会使产品的整个部分无法使用。 开发人员解决了问题的根本原因，并且测试团队有权测试这些功能后，便有可能发现其他问题。 由于发现需要调整升级过程的问题，请确保将其添加到您的自定义升级Runbook中。 经过几次测试和修复迭代后，应充分验证代码库并准备好部署到暂存环境。

### 最终测试{#final-testing}

在代码库已通过贵组织的QA团队的认证后，我们建议进行最后一轮测试。 本轮测试将涉及在测试环境中验证您的Runbook，然后进行用户接受、性能和安全测试。

![cinci_scroft](assets/cinci_cropped.png)

此步骤至关重要，因为这是您能够针对类似生产的环境验证Runbook中的步骤的唯一时间。 升级环境后，请务必让最终用户有时间登录并完成其在日常活动中使用系统时执行的操作。 用户在系统中使用之前未考虑的部分功能的情况并不罕见。 在上线前查找并更正这些区域的问题有助于防止成本高昂的生产中断。 由于新版AEM包含对基础平台的重大更改，因此在系统上执行性能、加载和安全测试也很重要，就像我们首次启动它一样。

### 执行升级{#performing-the-upgrade}

在从所有利益相关方收到最终签名后，便可以在已定义的Runbook程序上执行。 我们在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚步骤，并在执行[就地升级](/help/sites-deploying/in-place-upgrade.md)作为参考点中提供了安装步骤。

![执行升级](assets/perform-upgrade.png)

我们在环境验证的升级说明中提供了一些步骤。 这些检查包括基本检查，例如扫描升级日志并验证所有OSGi包是否已正确启动，但我们也建议根据您的业务流程使用您自己的测试案例进行验证。 我们还建议检查AEM在线修订清理的计划和相关例程，以确保这些例程将在公司的安静时间发生。 这些例程对于AEM的长期性能至关重要。
