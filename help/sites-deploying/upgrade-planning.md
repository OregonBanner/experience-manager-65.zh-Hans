---
title: 计划升级
seo-title: 计划升级
description: 本文有助于在计划AEM升级时明确目标、阶段和交付项。
seo-description: 本文有助于在计划AEM升级时明确目标、阶段和交付项。
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
feature: 升级
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---


# 计划升级{#planning-your-upgrade}

## AEM项目概述{#aem-project-overview}

AEM经常用于可能为数百万用户提供服务的高影响力部署。 在大多数情况下，在实例上部署自定义应用程序会增加复杂性。 升级此类部署的任何努力都需要有条不紊地处理。

本指南有助于在规划升级时确定明确的目标、阶段和交付内容。 它侧重于整个项目执行和指导方针。 虽然提供了实际升级步骤的概述，但在适当时，它引用了可用的技术资源。 应将其与本文档所述的可用技术资源结合使用。

AEM升级过程需要经过仔细处理的规划、分析和执行阶段，每个阶段都定义了关键的可交付项。

请注意，可以直接从AEM 6.0版和最多6.5版升级。运行5.6.x及更低版本的客户需要首先升级到6.0或更高版本，建议升级6.0(SP3)。 此外，新的OAK Segment Tar格式现在用于自6.3起的Segment Node Store，而且即使对于6.0、6.1和6.2，也必须将存储库迁移到此新格式。

>[!CAUTION]
>
>如果从AEM 6.2升级到6.3，则应从以下版本进行升级：从版本(**6.2-SP1-CFP1 —6.2SP1-CFP12.1**)或从&#x200B;**6.2SP1-CFP15**&#x200B;开始。 否则，如果要从&#x200B;**6.2SP1-CFP13/6.2SP1CFP14**&#x200B;升级到AEM 6.3，则还必须升级到至少版本&#x200B;**6.3.2.2**。 否则，AEM Sites在升级后将失败。

## 升级范围和要求{#upgrade-scope-requirements}

以下是一列表典型AEM升级项目中受影响的区域：

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
   <td>在AEM升级时，可能也需要升级操作系统，这可能会产生一些影响。</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>适当影响</td>
   <td>AEM 6.3需要JRE 1.7.x（64位）或更高版本。 JRE 1.8是Oracle目前支持的唯一版本。</td>
  </tr>
  <tr>
   <td>硬件</td>
   <td>适当影响</td>
   <td>“联机修订清理”要求可用<br />磁盘空间等于存储库大小的25%，可用堆空间<br />为15%才能成功完成。 您可能需要将硬件升级到<br />，确保有足够的资源执行“在线修订清理”以完全执行<br />。 此外，如果从AEM 6之前的版本升级，则可能会有其他存储要求。<br /></td>
  </tr>
  <tr>
   <td>内容存储库（CRX或Oak）</td>
   <td>高影响力</td>
   <td>从6.1版开始，AEM不支持CRX2，因此从旧版本升级时，需要迁移到<br /> Oak(CRX3)。 AEM 6.3已<br />实施了新的区段节点存储，该存储也需要迁移。 <br /> crx2oak工具用于此用途。</td>
  </tr>
  <tr>
   <td>AEM组件/内容</td>
   <td>适当影响</td>
   <td><code>/libs</code> 和<code>/apps</code>可通过升级轻松处理，但<code>/etc</code>通常需要手动重新应用自定义。</td>
  </tr>
  <tr>
   <td>AEM服务</td>
   <td>低影响</td>
   <td>大多数AEM核心服务都经过升级测试。 这是一个低冲击度的区域。</td>
  </tr>
  <tr>
   <td>自定义应用程序服务</td>
   <td>低到高影响</td>
   <td>根据应用程序和自定义，可能存在与JVM、操作系统版本和某些与索引相关的<br />更改相关的<br />依赖关系，因为索引不会在Oak中自动生成。</td>
  </tr>
  <tr>
   <td>自定义应用程序内容</td>
   <td>低到高影响</td>
   <td>在进行升级之前，不会通过升级处理的内容可以备份<br />，然后再移回存储库。<br /> 大多数内容都可以通过迁移工具处理。</td>
  </tr>
 </tbody>
</table>

务必确保您运行的是受支持的操作系统、Java运行时、httpd和Dispatcher版本。 有关详细信息，请参阅[AEM 6.5技术要求页](/help/sites-deploying/technical-requirements.md)。 升级这些组件需要在您的项目计划中说明，并且应在升级AEM之前完成。

## 项目阶段{#project-phases}

规划和执行AEM升级需要做大量工作。 为了澄清这一过程中的不同努力，我们将规划和执行练习分为不同的阶段。 在以下各节中，每个阶段都生成一个交付项，经常由项目的未来阶段利用。

### 创作培训计划{#planning-for-author-training}

对于任何新版本，都可能会对UI和用户工作流进行潜在的更改。 此外，新版本还引入了一些新功能，这些功能可能对业务有利。 我们建议您查看已引入的功能更改，并组织一个计划来培训您的用户有效利用这些更改。

![unu_scoft](assets/unu_cropped.png)

AEM 6.5的新增功能可在adobe.com](/help/release-notes/release-notes.md)的AEM部分找到。 [请务必注意对组织中常用的UI或产品功能所做的任何更改。 在浏览新增功能时，请注意任何对您的组织有价值的功能。 查看AEM 6.5中的变化后，为作者制定培训计划。 这可能包括利用免费提供的资源，如通过[Adobe数字学习服务](https://www.adobe.com/training.html)提供的帮助视频或正式培训。

### 创建测试计划{#creating-a-test-plan}

每个客户的AEM实施都是独一无二的，并且已进行定制以满足其业务需求。 因此，确定对系统进行的所有自定义，以便将这些自定义包含在测试计划中非常重要。 此测试计划将为我们在升级实例上执行的QA过程提供动力。

![测试计划](assets/test-plan.png)

需要复制确切的生产环境，并在升级后对其执行测试，以确保所有应用程序和自定义代码仍按需要运行。 您需要重新执行所有自定义操作，并执行性能、负载和安全测试。 在组织测试计划时，除了开箱即用的UI和工作流之外，请确保涵盖对系统进行的所有自定义，这些UI和应用程序在日常操作中都得到利用。 这些功能包括自定义OSGI服务和Servlet、与Adobe Marketing Cloud的集成、通过AEM连接器与第三方的集成、自定义第三方集成、自定义组件和模板、AEM中的自定义UI叠加和自定义工作流。 对于从AEM 6之前版本迁移的客户，应分析任何自定义查询，因为可能需要对这些客户编制索引。 对于已使用AEM 6.x版本的客户，仍应测试这些查询，以确保其索引在升级后继续有效运行。

### 确定需要的体系结构和基础架构更改{#determining-architectural-and-infrastructure-changes-needed}

升级时，可能还需要升级技术堆栈中的其他组件，如操作系统或JVM。 此外，由于存储库组成中的更改，可能需要额外的硬件。 这通常只针对从6.x以前的实例迁移的客户，但是必须考虑。 最后，您的操作实践可能需要进行一些更改，包括监控、维护以及备份和灾难恢复过程。

![doi_scoft](assets/doi_cropped.png)

查看AEM 6.5的技术要求，并确保您当前的硬件和软件足够。 有关操作流程的潜在更改，请参阅以下文档:

**监控和维护：**

[操作仪表板](/help/sites-administering/operations-dashboard.md)

[Assets 监控最佳实践](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台监视服务器资源](/help/sites-administering/jmx-console.md)

[修订版清理](/help/sites-deploying/revision-cleanup.md)

**备份/恢复和灾难恢复：**

[备份和恢复](/help/sites-administering/backup-and-restore.md)

[性能和可伸缩性](/help/sites-deploying/performance.md)

[如何使用TarMK冷备用运行AEM](/help/sites-deploying/tarmk-cold-standby.md)

#### 内容重组注意事项{#content-restructuring-considerations}

AEM对存储库结构进行了更改，有助于更加无缝地升级。 这些更改包括根据Adobe或客户是否拥有该内容，将内容从/etc文件夹移出到包括/libs、/apps和/content在内的文件夹，从而限制在发布过程中覆盖内容的可能性。 存储库重组的方式是，它在6.5升级时不需要代码更改，但建议在计划升级时查看AEM](/help/sites-deploying/repository-restructuring.md)中[存储库重组的详细信息。

### 评估升级复杂性{#assessing-upgrade-complexity}

由于我们的客户在其AEM环境上所应用的自定义项的数量和性质各不相同，因此必须提前一段时间确定在升级过程中应该达到的总体工作水平。

有两种方法可用于评估升级的复杂性，初步阶段只能使用新引入的模式检测器，它可以在AEM 6.1、6.2和6.3实例上运行。 模式检测器是使用报告的模式评估预期的升级的总体复杂性的最简单方法。 模式检测器报告包括用于识别自定义代码库正在使用的不可用API的模式（这是使用6.3中的预升级兼容性检查完成的）。

在初始评估之后，下一步可能会是对测试实例执行升级并执行一些基本的烟雾测试。 Adobe还提供了一些。 此外，[已弃用和已删除功能](/help/release-notes/deprecated-removed-features.md)的列表不仅应查看要升级到的版本，还应查看源版本和目标版本之间的任何版本。 例如，如果从AEM 6.2升级到6.5，则除了AEM 6.5的功能外，还应查看AEM 6.3已弃用和已删除的功能。

![trei_scoft](assets/trei_cropped.png)

最近引入的图案检测器应该能够为大多数情况下在升级期间的预期提供相当准确的估计。 但是，对于更复杂的自定义和部署，如果您有不兼容的更改，则可以按照[执行就地升级](/help/sites-deploying/in-place-upgrade.md)中的说明将开发实例升级到AEM 6.5。 完成后，对此环境执行一些高级烟雾测试。 本练习的目标不是彻底完成测试用例清点并生成缺陷的正式清单，而是大致估计升级代码所需的工作量，以实现6.5兼容性。 当与[模式检测](/help/sites-deploying/pattern-detector.md)和在前一部分中确定的体系结构变化结合时，可以向项目管理小组提供粗略估计以规划升级。

### 构建升级和回滚Runbook {#building-the-upgrade-and-rollback-runbook}

虽然Adobe记录了升级AEM实例的过程，但每个客户的网络布局、部署架构和自定义将需要对此方法进行微调和定制。 因此，我们建议您查看我们提供的所有文档，并使用它通知特定于项目的Runbook，其中概述了您将在环境中遵循的特定升级和回滚过程。 如果从CRX2升级，请确保评估从CRX2迁移到Oak时内容迁移所需的时间。 对于大型存储库，它可能相当大。

![runbook-diagram](assets/runbook-diagram.png)

我们已在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚过程，并在执行[就地升级](/help/sites-deploying/in-place-upgrade.md)中提供了应用升级的分步说明。 应查看这些说明并考虑您的系统体系结构、自定义和停机时间容限，以确定在升级过程中将执行的适当切换和回滚过程。 在起草自定义Runbook时，应包括对架构或服务器大小的任何更改。 必须指出，应将此作为第一稿。 当您的团队完成其QA和开发周期并部署到暂存环境的升级时，可能需要执行一些额外步骤。 理想情况下，此文档应包含足够的信息，这样，如果将信息交给您的业务人员，他们就能够完全从中包含的信息完成升级。

### 开发项目计划{#developing-a-project-plan}

我们可以使用先前练习的输出来构建一个项目计划，涵盖测试或开发工作、培训和实际升级执行的预期时间。

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

我们为[升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)提供了与AEM 6.5兼容的过程。在执行此迭代过程时，应根据需要对Runbook进行更改。 另请参阅AEM 6.5](/help/sites-deploying/backward-compatibility.md)中的[向后兼容性，以了解在大多数情况下自定义如何保持向后兼容，而无需在升级后立即进行开发。

![patru_scoft](assets/patru_cropped.png)

开发和测试过程通常是一个迭代过程。 由于自定义，升级过程中所做的更改可能会使产品的整个部分不可用。 开发人员解决了问题的根本原因并且测试团队可以访问测试这些功能后，可能会发现其他问题。 当发现需要调整升级过程的问题时，请确保将它们添加到您的自定义升级Runbook中。 经过多次测试和修复，应完全验证代码库并准备好部署到暂存环境。

### 最终测试{#final-testing}

我们建议在代码库经过贵组织的QA团队认证后进行最后一轮测试。 本轮测试将包括在分阶环境验证您的Runbook，然后是几轮用户接受、性能和安全测试。

![cinci_scoft](assets/cinci_cropped.png)

此步骤至关重要，因为这是您能够针对类似于生产的环境验证Runbook中的步骤的唯一时间。 环境升级后，必须允许最终用户有时间登录并浏览他们在日常活动中使用系统时所做的活动。 用户利用以前未考虑过的部分系统的情况并不少见。 在上线前查找和更正这些区域的问题有助于防止代价高昂的生产中断。 由于新版AEM包含对底层平台的重大更改，因此在系统上执行性能、负载和安全测试也很重要，就像我们第一次启动它一样。

### 执行升级{#performing-the-upgrade}

从所有利益相关方收到最终注销后，就应该对已定义的Runbook过程执行。 我们已在[升级过程](/help/sites-deploying/upgrade-procedure.md)中提供了升级和回滚步骤，并在将[就地升级](/help/sites-deploying/in-place-upgrade.md)作为参考点执行中提供了安装步骤。

![perform-upgrade](assets/perform-upgrade.png)

我们已在升级说明中提供了一些步骤以验证环境。 这些检查包括基本检查，如扫描升级日志和验证所有OSGi捆绑包是否已正确启动，但我们还建议根据您的业务流程使用您自己的测试用例进行验证。 我们还建议检查AEM在线修订清理和相关例程的计划，以确保它们将在您的公司的安静时间发生。 这些例程对AEM的长期性能至关重要。
