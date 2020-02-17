---
title: 计划升级
seo-title: 计划升级
description: 本文有助于在规划AEM升级时确立明确的目标、阶段和交付内容。
seo-description: 本文有助于在规划AEM升级时确立明确的目标、阶段和交付内容。
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 计划升级{#planning-your-upgrade}

## AEM项目概述 {#aem-project-overview}

AEM通常用于可能为数百万用户提供高影响力部署。 在大多数情况下，在实例上部署了自定义应用程序，这增加了复杂性。 升级此类部署的任何努力都需要有条不紊地处理。

本指南有助于在规划升级时制定明确的目标、阶段和交付内容。 它侧重于整个项目执行和准则。 虽然它提供了实际升级步骤的概述，但在适当时，它引用了可用的技术资源。 它应与文档中提到的可用技术资源一起使用。

AEM升级流程需要仔细处理规划、分析和执行阶段，并为每个阶段定义关键的可交付内容。

请注意，可以直接从AEM版本6.0和最高6.5升级。运行5.6.x及更低版本的客户需要先升级到6.0或更高版本，建议使用6.0(SP3)。 此外，新的OAK Segment Tar格式现在用于自6.3起的Segment Node Store，并且即使对于6.0、6.1和6.2，也必须将存储库迁移到这种新格式。

>[!CAUTION]
>
>如果从AEM 6.2升级到6.3，则应从版本(**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**)或从 **6.2SP1-CFP15升级** 。 否则，如果您要从 **6.2SP1-CFP13/6.2SP1CFP14** 升级到AEM 6.3，则还必须升级到至少 **6.3.2.2版**。 否则，AEM站点在升级后将失败。

## 升级范围和要求 {#upgrade-scope-requirements}

您将在下面找到一个受典型AEM升级项目影响的区域列表：

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
   <td>在AEM升级时，可能也是时候升级操作系统了，这可能会产生一些影响。</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>适度影响</td>
   <td>AEM 6.3需要JRE 1.7.x（64位）或更高版本。 JRE 1.8是Oracle目前支持的唯一版本。</td>
  </tr>
  <tr>
   <td>硬件</td>
   <td>适度影响</td>
   <td>联机修订清理需要等于<br /> 25%存储库大小的可用磁盘空间和15%的可用堆空间<br /> ，才能成功完成。 您可能需要升级硬件以确保<br /> “在线修订清理”有足够的资源才能完全执行<br /> 。 此外，如果从AEM 6之前的版本升级<br /> ，可能还有其他存储要求。</td>
  </tr>
  <tr>
   <td>内容存储库（CRX或Oak）</td>
   <td>高影响力</td>
   <td>从版本6.1开始，AEM不支持CRX2，因此，如果从旧版本升级，则需要迁移到Oak<br /> (CRX3)。 AEM 6.3已实施新的区段节点存储<br /> ，该存储也需要迁移。 crx<br /> 2oak工具用于此用途。</td>
  </tr>
  <tr>
   <td>AEM组件／内容</td>
   <td>适度影响</td>
   <td><code>/libs</code> 并且 <code>/apps</code> 通过升级可以轻松处理，但 <code>/etc</code> 通常需要手动重新应用自定义。</td>
  </tr>
  <tr>
   <td>AEM Services</td>
   <td>低影响</td>
   <td>大多数AEM核心服务都经过升级测试。 这是一个低冲击度的区域。</td>
  </tr>
  <tr>
   <td>自定义应用程序服务</td>
   <td>低到高影响</td>
   <td>根据应用程序和自定义，可能会依赖于JVM<br /> 、操作系统版本和某些与索引相关的更改<br /> ，因为索引不会在Oak中自动生成。</td>
  </tr>
  <tr>
   <td>自定义应用程序内容</td>
   <td>低到高影响</td>
   <td>升级之前，不会通过升级处理的内容可以先进行备份<br /> ，然后再移回存储库。<br /> 大多数内容都可以通过迁移工具处理。</td>
  </tr>
 </tbody>
</table>

务必确保您运行的是支持的操作系统、Java运行时、httpd和Dispatcher版本。 有关详细信息，请参阅 [AEM 6.5技术要求页](/help/sites-deploying/technical-requirements.md)。 升级这些组件需要在您的项目计划中说明，并且应在升级AEM之前完成。

## 项目阶段 {#project-phases}

规划和执行AEM升级需要做大量工作。 为了澄清这一过程中的不同努力，我们将规划和执行练习分为不同的阶段。 在以下各节中，每个阶段都会生成一个交付项，该交付项通常由项目的未来阶段利用。

### 创作培训计划 {#planning-for-author-training}

对于任何新版本，都可能引入对UI和用户工作流程的潜在更改。 此外，新版本还引入了可能对业务有利的新功能。 我们建议查看已引入的功能更改，并组织一个计划以培训您的用户有效利用这些更改。

![unu_scont](assets/unu_cropped.png)

AEM 6.5中的新增功能可在adobe.com [的AEM部分找到](/help/release-notes/release-notes.md)。 请务必注意对组织中常用的UI或产品功能所做的任何更改。 在浏览新增功能时，请注意任何对您的组织有价值的功能。 查看AEM 6.5中的更改后，为作者制定培训计划。 这可能涉及利用免费提供的资源，如通过 [Adobe数字学习服务提供的帮助功能视频或正式培训](https://www.adobe.com/training.html)。

### 创建测试计划 {#creating-a-test-plan}

每个客户对AEM的实施都是独一无二的，并且已进行自定义以满足其业务需求。 因此，务必确定对系统进行的所有自定义，以便将其包含在测试计划中。 此测试计划将为我们对升级实例执行的QA过程提供动力。

![测试计划](assets/test-plan.png)

需要复制确切的生产环境，并在升级后对其执行测试，以确保所有应用程序和自定义代码仍按需要运行。 您需要重新执行所有自定义操作，并执行性能、负载和安全测试。 在组织测试计划时，除了开箱即用的UI和日常操作中利用的工作流外，还应确保涵盖对系统进行的所有自定义。 这些功能包括自定义OSGI服务和Servlet、与Adobe Marketing cloud的集成、通过AEM连接器与第三方的集成、自定义第三方集成、自定义组件和模板、AEM中的自定义UI叠加以及自定义工作流程。 对于从AEM 6之前版本迁移的客户，应分析任何自定义查询，因为可能需要索引这些查询。 对于已使用AEM 6.x版本的客户，仍应测试这些查询以确保其索引在升级后继续有效运行。

### 确定所需的架构和基础架构更改 {#determining-architectural-and-infrastructure-changes-needed}

升级时，您可能还需要升级技术堆栈中的其他组件，如操作系统或JVM。 此外，由于存储库组成中的更改，可能需要额外的硬件。 这通常只针对从6.x以前的实例迁移的客户，但是这很重要。 最后，您的操作实践可能需要进行一些更改，包括监控、维护以及备份和灾难恢复过程。

![doi_scropten](assets/doi_cropped.png)

查看AEM 6.5的技术要求，并确保您当前的硬件和软件已足够。 有关操作流程的潜在更改，请参阅以下文档：

**监控和维护：**

[操作控制板](/help/sites-administering/operations-dashboard.md)

[资产监控最佳实践](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台监视服务器资源](/help/sites-administering/jmx-console.md)

[修订清除](/help/sites-deploying/revision-cleanup.md)

**备份／恢复和灾难恢复：**

[备份和恢复](/help/sites-administering/backup-and-restore.md)

[性能和可伸缩性](/help/sites-deploying/performance.md)

[如何使用TarMK Cold Standby运行AEM](/help/sites-deploying/tarmk-cold-standby.md)

#### 内容重组注意事项 {#content-restructuring-considerations}

AEM对存储库结构进行了更改，这有助于使升级更加无缝。 这些更改包括根据Adobe或客户是否拥有该内容，将内容从/etc文件夹移出到包括/libs、/apps和/content在内的文件夹，从而限制在发布期间覆盖内容的可能性。 存储库重组的方式是，在6.5升级时不需要进行代码更改，但建议在计划升级时查看AEM中存储库重组的详细信息 [](/help/sites-deploying/repository-restructuring-in-aem65.md) 。

### 评估升级复杂性 {#assessing-upgrade-complexity}

由于我们的客户在AEM环境中所应用的自定义数量和性质各不相同，因此，必须提前一段时间确定升级过程中应期望的总体工作级别。

您可以采用两种方法来评估升级的复杂性，初步阶段只需使用新引入的模式检测器，该检测器可在AEM 6.1、6.2和6.3实例上运行。 模式检测器是使用报告的模式评估预期的升级的总体复杂性的最简单方法。 模式检测器报告包括用于识别自定义代码库使用的不可用API的模式（这是使用6.3中的升级前兼容性检查完成的）。

在初始评估后，下一步更全面的步骤可能是对测试实例执行升级并执行一些基本烟雾测试。 Adobe还提供了一些。 此外，不仅应查看 [要升级到的版本的已弃用和已删除功能列表](/help/release-notes/deprecated-removed-features.md) ，还应查看源版本和目标版本之间的任何版本的列表。 例如，如果从AEM 6.2升级到6.5，则除了AEM 6.5的功能之外，还应查看AEM 6.3已弃用和已删除的功能。

![trei_scoffent](assets/trei_cropped.png)

最近引入的图案检测器应该能够相当准确地估计大多数情况下在升级期间的预期。 但是，对于更复杂的自定义和部署，如果您有不兼容的更改，则可以根据执行就地升级中的说明将开发实例 [升级到AEM 6.5](/help/sites-deploying/in-place-upgrade.md)。 完成后，在此环境中执行一些高级烟雾测试。 本练习的目标不是彻底完成测试用例清点并生成缺陷的正式清单，而是大致估计升级代码所需的工作量以实现6.5兼容性。 结合模式检 [测和上一节中确定的架构更改](/help/sites-deploying/pattern-detector.md) ，可以向项目管理团队提供粗略估计以规划升级。

### 构建升级和回滚操作手册 {#building-the-upgrade-and-rollback-runbook}

虽然Adobe记录了升级AEM实例的过程，但每位客户的网络布局、部署架构和自定义将需要对此方法进行微调和定制。 因此，我们建议您查看我们提供的所有文档，并使用它通知特定于项目的操作手册，其中概述了您将在环境中遵循的特定升级和回滚过程。 如果从CRX2升级，请确保评估从CRX2迁移到Oak时内容迁移需要多长时间。 对于大型存储库，它可能相当重要。

![Runbook-diagram](assets/runbook-diagram.png)

我们在升级过程中提供了升级和 [回滚过程](/help/sites-deploying/upgrade-procedure.md) ，并在执行就地升级中提供了应用升级的分 [步说明](/help/sites-deploying/in-place-upgrade.md)。 应查看这些说明并考虑系统架构、自定义和停机时间容限，以确定在升级过程中将执行的相应切换和回滚过程。 在制作自定义操作手册时，应包括对架构或服务器大小的任何更改。 必须指出，这应当作为第一稿。 当您的团队完成其QA和开发周期并部署到升级环境时，可能需要执行其他一些步骤。 理想情况下，本文档应包含足够的信息，这样，如果将信息交给您的运营人员，他们就可以完全从包含的信息中完成升级。

### 制定项目计划 {#developing-a-project-plan}

我们可以使用先前练习的输出来构建一个项目计划，涵盖测试或开发工作、培训和实际升级执行的预期时间表。

![开发项目计划](assets/develop-project-plan.png)

综合项目计划应包括：

* 最后确定开发和测试计划
* 升级开发和QA环境
* 更新AEM 6.5的自定义代码库
* QA测试和修复周期
* 升级升级环境
* 集成、性能和负载测试
* 环境认证
* 上线

### 执行开发和QA {#performing-development-and-qa}

我们提供了升级代 [码和自定义的过程](/help/sites-deploying/upgrading-code-and-customizations.md) ，以便与AEM 6.5兼容。执行此迭代过程时，应根据需要对操作手册进行更改。 另请参 [阅AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md) ，以了解自定义在大多数情况下如何保持向后兼容，而无需在升级后立即进行开发。

![patru_scrount](assets/patru_cropped.png)

开发和测试过程通常是一个迭代过程。 由于自定义，升级过程中所做的更改可能会使整个产品部分无法使用。 一旦开发人员解决了问题的根本原因并且测试团队有权测试这些功能，就有可能发现其他问题。 当发现需要调整升级过程的问题时，请确保将它们添加到自定义升级操作手册中。 经过多次测试和修复迭代后，应完全验证代码库并准备好部署到分阶段环境。

### 最终测试 {#final-testing}

我们建议在您的组织的QA团队通过代码库认证后进行最后一轮测试。 本轮测试将包括在分阶段环境中验证您的操作手册，然后是多轮用户接受、性能和安全性测试。

![cinci_scropten](assets/cinci_cropped.png)

此步骤非常重要，因为这是您能够针对类似于生产的环境验证操作手册中的步骤的唯一时间。 升级环境后，最终用户必须有时间登录并完成在日常活动中使用系统时的活动。 用户利用系统中以前未考虑过的一部分的情况并不少见。 在上线前查找和更正这些区域的问题有助于防止代价高昂的生产中断。 由于AEM的新版本包含对基础平台的重大更改，因此在系统上执行性能、负载和安全测试也很重要，就像我们第一次启动它一样。

### 执行升级 {#performing-the-upgrade}

从所有利益相关方收到最终注销后，就应该对已定义的操作手册过程执行。 我们在升级过程中提供了升级和回退 [的步骤](/help/sites-deploying/upgrade-procedure.md) ，并在将就地升级作为参考点执行 [](/help/sites-deploying/in-place-upgrade.md) 中提供了安装步骤。

![perform-upgrade](assets/perform-upgrade.png)

我们在环境验证的升级说明中提供了一些步骤。 这些检查包括扫描升级日志和验证所有OSGi捆绑包是否已正确启动等基本检查，但我们建议根据您的业务流程使用您自己的测试用例进行验证。 我们还建议检查AEM的在线修订清理计划和相关例程，以确保它们在公司的安静时间内发生。 这些例程对于AEM的长期性能至关重要。
