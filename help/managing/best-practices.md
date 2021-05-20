---
title: 管理项目 — 最佳实践检查列表
seo-title: 管理项目 — 最佳实践检查列表
description: 管理项目以实施Adobe Experience Manager(AEM)需要规划和了解。 项目检查列表旨在作为项目交付的一组最佳实践。 它们指导您完成项目生命周期的所有阶段，并提供对您当前状态的高级监控。
seo-description: 管理项目以实施Adobe Experience Manager(AEM)需要规划和了解。 项目检查列表旨在作为项目交付的一组最佳实践。 它们指导您完成项目生命周期的所有阶段，并提供对您当前状态的高级监控。
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

---

# 管理项目 — 最佳实践检查列表{#managing-projects-best-practices-checklist}

管理用于实施Adobe Experience Manager(AEM)的项目需要进行规划和了解，以确保您了解在实施项目之前和过程中需要做出的问题和（相关）决策。

为了帮助您，最佳实践包括：

* [交互式检查列表](/help/managing/best-practices-checklist.md)允许您使用这些最佳实践跟踪和监控进度。

   * 根据阶段、里程碑和角色定义输入和交付内容。
   * 提供自动的概述（质量、运行状况和完整性），以指示进度和项目运行状况。

* 文档直接基于[清单](/help/managing/best-practices-checklist.md)，详细介绍：

   * [项目](#projectheartbeat) 心率分析。
   * [按角色显示的](#status-by-role) 状态概述。
   * [阶段和里程碑](#phases-and-milestones)。
   * [关键](#persona) 人物及其在每个阶段（相关）的参与。
   * [[所需文档和交付件](#required-documents-and-deliverables)的术语表](/help/managing/best-practices-glossary.md)。

* [进一步](/help/managing/best-practices-further-reference.md) 参考材料，以提供有关特定领域的更多详细信息。

## 项目心率功能板{#project-heartbeat-dashboard}

**项目心率**&#x200B;工作表提供了项目关键量度的图形概述：

* **阶段质量**

   * 指示项目中[所需文档和交付项](#required-documents-and-deliverables)的质量。

* **阶段健康**

   * 项目的高级状态指示器；强调可能面临风险的领域是有用的。

* **阶段完整性**

   * 在项目期间的任何时间点，此值指示项目每个阶段已完成的进度。

## 按角色{#status-by-role}列出的状态

**按角色列出的状态**&#x200B;工作表显示&#x200B;[**运行状况**、**质量**&#x200B;和&#x200B;**完整性**](#projectheartbeat)&#x200B;按&#x200B;**[阶段](#phases-and-milestones)**&#x200B;和&#x200B;**[角色](#persona)**&#x200B;的详细细目。

## 阶段和里程碑{#phases-and-milestones}

项目计划分为不同的（高级）阶段。

每个阶段都包含其自己的里程碑。 对于每个[角色](#persona)（或角色），将列出相关里程碑，以及生成定义的交付件所需的文档。

>[!NOTE]
>
>单个必需文档与交付件之间不存在直接的1:1关系。

### 准备 {#preparation}

项目准备是整个项目的基础。 您需要定义关键要求以及明确的目标和期望：

* **业务原理**

   * 开展该项目的基本原因和理由。

* **范围和计划**

   * 应该提供基本范围和粗略的时间表来定义所需内容，以及在哪个时间范围内；如果它有助于澄清情况，您还可以定义范围外的内容。

您准备、计划和运行项目以及实施解决方案的方式将受您在固定预算、固定时间表、内容数量和所需质量等操作限制的影响。

与往常一样，任何因素的调整都会影响其他因素。 例如，缩短时间，但要求达到相同质量水平可能会提高价格，同时减少您可以满足的内容数量。 预算往往是关键因素，因此这种关系不能被遗忘。

四个因素：

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **验证**

   在此阶段，您需要验证并确认项目目标；例如：

   * 您想要实现/提供什么？
   * 谁会受益？
   * 范围是什么？

      * 如果它有助于澄清情况，您还可以定义范围外的内容。
   * 如何定义成功？
   * 如何衡量成功？
   * 有哪些要求、业务和技术？
   * 是否有要替换的旧系统？如果有，是否有要迁移的数据？
   * 谁会参与？
   * 你如何衡量进度？
   * 在项目的生命周期中，您将多久审查一次进度？


* **预算**

   在开始任何项目之前，您需要对实施成本进行可靠而实际的估算：

   * 使用来自验证里程碑的信息作为估算的基础。
   * 在你的估计中要实事求是。
   * 考虑并遵守客户可能遵守的任何客户准则、流程或限制。
   * 如果在以后阶段需要对预算进行审查或改进，则考虑应急和审查程序。
   * 请记住，成本有多种形式；购买、使用资源及费用等。

### 规划 {#planning}

规划项目可整合准备。 在这里，您需要开始将目标和期望转化为一个明确的路线图，其中包括具体任务，并有明确的沟通约束，并有严格的审查来衡量进展。

#### 里程碑{#milestones-1}

* **切换**

   干净的移交可确保相应的角色/组了解其在项目中的责任。

   应提供/生成完整的详细信息，以确保他们全面了解所有相关方面，包括路线图、范围、目标、要求和KPI。

* **风险评估**

   为避免令人不快的意外，请使用风险评估来识别和量化任何潜在风险及其影响和概率。

   这应在项目生命周期的早期完成，以确保识别和评估任何可能性。 根据调查结果，您可以向利益相关方报告是否可以实施全部要求，以及是否可能规划采取和跟踪的适当行动。

* **通信**

   沟通始终是任何项目成功的关键。 您需要清晰、高效地沟通，以确保每个人：

   * 努力实现相同的基本目标
   * 从同一信息库
   * 具有相同渠道

* **启动**

   启动会议用于提高对项目正在启动的认识。 这是一个很好的机会：

   * 邀请所有感兴趣的方（或至少团体代表）。
   * 介绍有关项目的关键事实。
   * 回答问题。
   * 确保每个人拥有相同的知识库。
   * 从参与的每个人那里获得承诺 — 这必须得付出。

      * 在项目开始时让主要参与者（包括潜在作者）参与进来，就会增加他们投入项目的机会。

### 开发准备{#development-preparation}

规划开发是确保项目由具备所需知识的团队在坚实的设计基础上构建的关键。

#### 里程碑{#milestones-2}

* **开发小组人员配备和培训**

   在开始任何项目之前，您应确保开发团队配备适当的人员，并确保所有团队成员都接受手头任务的培训。

* **内容架构**

   内容架构定义并描述了内容的未来架构；包括：

   * 内容树；包括资产
   * 基本结构；包括营销活动等。
   * 多站点和多语言结构（MSM、翻译等）
   * 支持内容（包括标记和标记概念）
   * 缓存和内容重用策略

* **系统架构**

   系统架构定义了系统的概念视图；包括（其中包括其他资料）：

   * [所有](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 所需环境的系统结构
   * 子系统
   * 第三方系统
   * 界面；硬件、软件和人机交互
   * 每个环境的服务器；请参阅[技术要求](/help/sites-deploying/technical-requirements.md)和[硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md)

   * 每个环境的流程；例如，部署和维护要求
   * 维护活动（数据存储GC、TarPM优化等）
   * [](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) Dispatchercache
   * [](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) ClusteringPublish/Authorshare
   * 客户端性能（JS缩小、简化、CSS Sprite、HTTP请求总数等）

* **应用程序架构**

   应用程序架构定义并描述建议的应用程序的行为。

   重点是：

   * 用户如何彼此进行交互以及如何与用户进行交互。
   * 应用程序使用和生成的数据，而不是其内部结构。

   定义应包括：

   * 项目的基本代码结构
   * 代码工件（包、包等）
   * 模板/组件的划分及其关系
   * 所需自定义的高级详细信息（稍后将显示特定叠加）
   * 解决方案所需的工作流设计（例如，内容创建、批准、发布、转换、导入、导出等）
   * 对任何复杂模块（例如MSM、Commerce、第三方集成）进行特殊考虑


* **系统集成**

   系统集成要求您规划（然后实施）：

   * 如何将所有子系统和[解决方案集成](/help/sites-administering/integration.md)整合在一起，作为一个协调的系统运行
   * 如何集成任何第三方系统；与任何特殊注意事项一起使用，例如在第三方系统出现故障时，客户端/浏览器端或故障处理

* **测试概念**

   在开始开发之前，您应该针对项目的所有[测试](/help/sites-developing/planning.md)要求制定一个深入而全面的概念。

   这应包括（其中包括）：

   * 要执行的所有测试的详细信息
   * 准备这些测试所需的任何内容
   * 要使用的任何测试工具的信息
   * 高级别指示将参与测试的人员；尤其是QA团队以外的组
   * 测试自动化的细节；例如，使用Selenium或AEM Developer模式

* **体验设计**

   体验设计(XD)涉及为解决方案设计用户体验。

   应为您的作者和网站的最终用户分析和开发用户体验。

* **支持设置**

   在开发之前，应设置部署、发布、测试和报告问题所需的所有支持流程。

   另请参阅[Adobe支持门户](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)。

### 操作计划和操作{#operations-planning-and-operations}

在类似的基础上，必须正确规划操作，以确保您拥有项目生命周期所有阶段所需的环境。 您还需要适当的流程来维护它们。

#### 里程碑{#milestones-3}

* **权限**

   您需要为将使用该解决方案的所有用户/组规划并实施角色和权限概念。

   例如：

   * 每个角色（即组）具有`read`/ `write`访问定义的列表

   * 定义影响发布环境的权限的使用；例如，`replicate`
   * 对于具有最低权限的用户，应定义工作流
   * `editor`组中的用户不应具有`admin`权限，也不应属于`administrators`组

   有关更多信息，请参阅[用户管理和安全](/help/sites-administering/security.md)。

* **监控和维护**

   监控和维护是确保解决方案在推出后能够顺利运行的关键方面。 为此，您需要定义：

   * 需要监控的内容
   * 维护任务；经常和特殊情况

   另请参阅[监视和维护](/help/sites-deploying/monitoring-and-maintaining.md)以了解更多信息。

* **迁移**

   对于迁移，应审核并验证旧版系统中的任何内容。

* **恢复计划**

   确保您已制定恢复计划。 在紧急情况下，必须提供此功能以确保AEM的生产使用。 这应包括备份、恢复、故障诊断等情况。

### 开发 {#development}

开发是一个关键阶段，需要的不仅仅是编码。

#### 里程碑{#milestones-4}

* **开发环境**

   规划并记录您的开发环境，包括：

   * 架构
   * [开发工具](/help/sites-developing/dev-tools.md)

      * 典型的环境包括：

         * 问题跟踪系统；如吉拉
         * IDE;如Eclipse
         * 构建管理工具；如Maven
         * 持续集成的工具；如詹金斯
         * 版本控制工具；例如GIT/SVN
         * 构建对象存储库管理器；如Archiva/Nexus
   * 第三方软件集成/依赖项
   * [解决方案集成/依赖关系](/help/sites-administering/integration.md)
   * 部署频度


* **测试系统**

   规划并记录测试环境，包括：

   * 架构
   * 对开发内部版本的依赖；包括夜间构建
   * 测试第三方软件集成/依赖项的可能性或限制
   * 测试工具
   * 自动测试策略

* **生产系统**

   规划并记录您的生产环境，包括：

   * 架构
   * 部署频度
   * 第三方软件集成/依赖项
   * 安全设置
   * 通过在生产设置中运行[Tough Day测试](/help/sites-developing/tough-day.md)来验证基线性能
   * 性能测试的要求；请参阅[质量保证最佳实践](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **集成**

   规划、记录和测试系统的所有方面和[解决方案集成](/help/sites-administering/integration.md)，包括：

   * 自动测试策略
   * 将流程自动化到[，将应用程序从开发移动到测试，然后进行生产](/help/managing/enterprise-devops.md#code-movement)
   * 将流程自动化到[将内容从生产移动到测试和开发](/help/managing/enterprise-devops.md#content-movement)

* **迁移**

   规划、记录和测试内容迁移的各个方面；包括：

   * 内容架构
   * 迁移策略

* **通信**

   确保根据需要保持所有团队成员和项目角色的最新状态。

* **文档**

   全面记录解决方案；包括：

   * 操作手册
   * 任何可能影响升级的自定义设置
   * 发行说明

### 性能和测试{#performance-and-testing}

新应用程序一经推出，就需要进行严格的测试，包括功能和[性能](/help/sites-deploying/configuring-performance.md)。

>[!NOTE]
>
>应允许任何测试团队保持中立并提供测试结果。
>
>项目经理有责任评估结果的任何影响并决定采取适当行动。

#### 里程碑{#milestones-5}

* **最终用户验收测试**

   [用户接受测试](/help/sites-developing/acceptance-signoff.md) (UAT)对于确保：

   * 该解决方案满足用户/客户的要求
   * 客户/用户接受解决方案（功能、设计和性能）

   客户交接工作应有一份正式的清单；理想情况下，会针对快照自动化并在夜间运行。 结果应发送给项目经理和开发团队

* **性能和负载测试**

   性能和负载测试用于确保解决方案在平均负载和峰值负载上满足所需的性能级别。

   有关性能测试的更多信息，请参阅：

   * [性能测试](/help/sites-deploying/configuring-performance.md)
   * [如何规划和运行测试](/help/sites-developing/planning.md)

   * [基本性能准则](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >在正常使用AEM期间，这个过程必须继续下去，但最关键的是这些初始阶段。

### 转出 {#rollout}

推出新应用程序需要仔细规划以确保顺利上线。 这包括确认高级安全性、培训所有潜在用户并进行多次练习以确认已处理所有问题。

#### 里程碑{#milestones-6}

* **准备**

   准备和规划将有助于确保顺利推出。

* **培训**

   确保所有有关工作人员都接受过培训。

   请参阅课程目录中的[Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager)。

* **接受过培训的管理员**

   确保您的解决方案管理员具有：

   * 已接受培训
   * 收到了适当的培训材料
   * 已收到相应的文档

* **接受培训的用户**

   确保您的作者具有：

   * 已接受培训
   * 收到了适当的培训材料
   * 收到适当文件；例如，《用户指南》

* **渗透测试**

   渗透测试模拟对计算机系统的攻击，以识别潜在的安全弱点。

* **渗透/安全测试**

   为确保解决方案的安全性，请执行特定的渗透测试以及范围更广的安全测试。

   有关更多详细信息，请参阅[安全检查表](/help/sites-administering/security-checklist.md)。

### 上线{#go-live}

您希望“上线”尽可能顺畅。 最后的步骤同样需要规划清理执行。

#### 里程碑{#milestones-7}

* **准备**

   准备和规划将有助于确保顺利上线。

* **安全**

   确认内部和外部用户及其内容解决方案的安全性。

* **回退**

   在上线之前，请确保回退所需的所有系统、过程和机制都已到位。

* **支持**

   确保支持服务已就地并准备就绪。

* **过渡**

   规划并执行到生产环境和用户的过渡。

* **转出**

   准备并执行烟度测试。

## 角色 {#persona}

清单由人物设计。 这些角色在项目生命周期中具有重要的参与性。

特定任务中还涉及一些其他角色](#other-persona)。[

### 项目赞助商{#project-sponsor}

项目发起人是：

* 负责提供/呈报项目的业务案例。
* 确定和界定项目范围的关键；包括：

   * 成功的定义和标准
   * 主要KPI

* 根据客户端路线图提供主要里程碑。

### 项目经理{#project-manager}

项目经理是：

* 根据项目赞助商提供的要求（如范围、关键绩效指标、成功标准和定义）负责项目的整体交付。
* 负责定义预算并根据该预算为项目提供资源。
* 项目中所有角色的主要通信点。

### 架构师 {#architect}

解决方案架构师：

* 负责解决方案和系统的高级设计。
* 帮助定义AEM的实施策略。 例如，是实施群集安装，还是实施冷备用安装，或者当需要内容交付网络(CDN)时。
* 此外，还根据客户端要求定义AEM解决方案架构。 这包括用户角色（具有相关权限）的概念、模板和组件之间的关系，或何时使用多站点管理。

### 业务分析师{#business-analyst}

业务分析师：

* 主要负责收集和分析高级需求，然后将这些需求转换为规格：

   * 以便项目经理在计划开发时使用
   * 以供开发团队在设计和开发期间工作。

* 与客户密切合作以分析需求。 它们与以下内容相匹配：

   * 成功的定义。
   * 成功标准。
   * KPI（既基于业务，也基于绩效）。

### 开发领导{#development-lead}

开发领导：

* 负责项目的技术交付。
* 负责选择符合客户要求的开发方法。
* 制定发展战略：

   * 确保它与业务和性能KPI保持一致
   * 考虑成功标准和定义

* 与架构师密切合作(特别是在制定AEM开发策略时)，以定义各个方面，如模板与组件之间的关系、第三方应用程序的集成策略以及任何专门功能。

### 质量潜在客户{#quality-lead}

质量线索：

* 对交货质量负责；确保符合成功标准以及客户定义的任何KPI。
* 定义质量量度，与所有利益相关方保持一致，制定测试计划并确保执行这些计划。
* 创建报告并将其提交给项目利益相关者。

### 系统工程师{#system-engineer}

系统工程师：

* 负责监督项目基础设施。
* 负责：

   * 内部开发和测试环境的设置
   * 将这些系统与客户端系统匹配

* 在上线之前和之后，提供硬件建议、监控各种实施并提供操作支持。

### 安全线索{#security-lead}

安全主管：

* 负责解决方案的整体安全概念，确保与客户的任何要求和策略保持一致。
* 为任何基于硬件的安全概念提供安全概念、安全操作和建议；例如区域和防火墙。

### 其他角色{#other-persona}

* 利益相关方

   * 对项目成功有兴趣（参与）的人员（通常来自企业）。 他们经常为预算捐款。

* 合法的

   * 在谈判合同时需要法律建议。

* 培训员

   * 根据项目的规模和性质，可利用专门培训员为相关群体制定和举办培训班。

* 技术作家

   * 根据项目的规模和性质，可以使用专业技术作家为特定群体编写指南和手册；例如，系统管理员的维护手册或作者的用户指南。

* 系统管理员

   * 负责系统的持续运行。

* 作者和最终用户

   * 将使用系统创建和维护网站内容的人员。

## 所需文档和交付件{#required-documents-and-deliverables}

每个里程碑的&#x200B;**必需文档**&#x200B;和&#x200B;**可交付项**&#x200B;都包含检查列表。

* 两者之间没有1:1的关系；例如，一组必需的文档可产生一个可交付项。
* 同一里程碑期间，一个角色交付的内容可以是另一个角色的必需文档。

### 所需文档{#required-documents}

在生成相应的交付项时，相应角色需要&#x200B;**必需文档**。

对于每个&#x200B;**必需文档**，角色应指示：

* **Y/N**:是否收到。
* **1-3**:接收文档的质量指示。

### 交付项 {#deliverables}

对于每个里程碑，相应的角色负责提供特定文档，从而实现他们对特定里程碑的责任。

对于每个&#x200B;**可交付项**，角色必须指示：

* **Y/N**:是否已完成。

交付项通常用作当前或以后里程碑的&#x200B;**必需文档**。

## 相关最佳实践{#related-best-practices}

有关部署、管理、开发或创作的最佳实践，请参阅以下内容：

* 与管理AEM项目相关的其他最佳实践和准则：
   * [硬件大小调整规范](/help/managing/hardware-sizing-guidelines.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [SEO 和 URL 管理最佳实践](/help/managing/seo-and-url-management.md)
   * [AEM 和 Web 辅助功能规范](/help/managing/web-accessibility.md)
   * [《通用数据保护条例》](/help/managing/data-protection-and-privacy.md)* [部署和维护最佳实践](/help/sites-deploying/best-practices.md)
* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发最佳实践](/help/sites-developing/best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)

## 关键文档区域{#key-documentation-areas}

* AEM文档
此外，AEM文档的以下章节特别关注（但是，此列表并不详尽）：

   * [安全](/help/sites-developing/security.md)
   * [推荐的部署](/help/sites-deploying/recommended-deploys.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [硬件大小调整](/help/managing/hardware-sizing-guidelines.md)
   * AEM的概念：

      * [开发 — 基础知识](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)

* 相关文档

   * Adobe Experience Cloud - [规划Adobe Experience Cloud](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
