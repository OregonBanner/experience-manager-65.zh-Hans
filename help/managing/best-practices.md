---
title: 管理项目——最佳实践核对清单
seo-title: 管理项目——最佳实践核对清单
description: 管理项目以实施Adobe Experience Manager(AEM)需要规划和理解。 项目核对清单旨在作为一组针对项目投放的最佳实践。 它们指导您完成项目生命周期的所有阶段，并提供对您当前状态的高级监控。
seo-description: 管理项目以实施Adobe Experience Manager(AEM)需要规划和理解。 项目核对清单旨在作为一组针对项目投放的最佳实践。 它们指导您完成项目生命周期的所有阶段，并提供对您当前状态的高级监控。
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

---


# 管理项目——最佳实践核对清单{#managing-projects-best-practices-checklist}

管理项目以实施Adobe Experience Manager(AEM)需要进行规划和了解，以确保您了解需要做出的问题和（相关）决策（在实施项目之前和期间）。

为帮助您，最佳实践包括：

* 交互式 [核对清单](/help/managing/best-practices-checklist.md) ，允许您通过这些最佳实践来跟踪和监控您的进度。

   * 根据阶段、里程碑和角色定义输入和交付项。
   * 提供自动化概述（质量、运行状况和完整性），以指示进度和项目运行状况。

* 文档直接基于核对 [清单](/help/managing/best-practices-checklist.md)，详细介绍了：

   * [项目心跳](#projectheartbeat) 分析。
   * [“按角色显示状态](#status-by-role) ”概述。
   * [阶段和里程碑](#phases-and-milestones)。
   * [关键人物](#persona) ，以及他们在每个（相关）阶段的参与。
   * 必 [需文档](/help/managing/best-practices-glossary.md) 和交付 [项的词汇表](#required-documents-and-deliverables)。

* [进一步参考材料](/help/managing/best-practices-further-reference.md) ，以提供有关特定领域的更多详细信息。

## 项目心跳仪表板 {#project-heartbeat-dashboard}

项目 **心跳** (Project Heartbeat)工作表以图形形式概述了您的项目的关键指标：

* **相位质量**

   * 指示整个项目 [的必需文档和交](#required-documents-and-deliverables) 付项的质量。

* **阶段健康**

   * 项目的高级状态指标；有助于突出显示可能存在风险的区域。

* **阶段完整性**

   * 在项目期间的任何时间点，它都表示已为项目的每个阶段完成了多少。

## 按角色列出的状态 {#status-by-role}

按角 **色列出的** “状态”工作表显示“健康”、“质量”和“完 [**整性”的详细细分(**&#x200B;按的阶段) ********](#projectheartbeat)**[](#phases-and-milestones)****[](#persona)**&#x200B;和“人物角色”。

## 阶段和里程碑 {#phases-and-milestones}

项目计划分为不同的（高级）阶段。

每个阶段都包含其自己的里程碑。 对于每 [个人](#persona) （或角色），将列出相关里程碑，以及生成定义的交付项所需的文档。

>[!NOTE]
>
>个人必需文档与交付项之间不存在直接的1:1关系。

### 准备 {#preparation}

项目准备是整个项目的基础。 您需要定义关键要求以及明确的目标和期望：

* **业务原理**

   * 开展该项目的根本原因和理由。

* **范围和计划**

   * 应提供基本范围和粗略计划，以定义所需内容，以及在哪个时限内；如果有助于澄清情况，您还可以定义范围之外的内容。

您在固定预算、固定时间线、内容数量和所需质量等条件下运行的限制将影响您准备、计划和运行项目以及实施解决方案的方式。

与往常一样，调整任何因素都会影响其他因素。 例如，缩短时间，但要求相同质量的产品可能会提高价格，同时减少您可以满足的内容数量。 预算往往是关键因素，因此这种关系不能被遗忘。

四个因素：

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### Milestones {#milestones}

* **验证**

   在此阶段，您需要验证并确认项目目标；例如：

   * 您希望实现／提供什么？
   * 谁会受益？
   * 范围是什么？

      * 如果有助于澄清情况，您还可以定义范围之外的内容。
   * 如何定义成功？
   * 如何衡量成功？
   * 要求、业务和技术是什么？
   * 是否有旧系统要替换，如果是，是否有要迁移的数据？
   * 谁会参与进来？
   * 你如何衡量进展？
   * 您在项目生命周期中多长时间审查进度？


* **预算**

   在开始任何项目之前，您需要对实施成本进行可靠、真实的估计：

   * 使用验证里程碑中的信息作为估计的基础。
   * 在您的估计中实事求是。
   * 考虑并尊重客户可能遵守的任何客户端准则、流程或限制。
   * 如果在以后阶段需要对预算进行审查或改进，则考虑应急和审查程序。
   * 记住，成本有多种形式；购买、使用资源及费用等。

### 规划 {#planning}

计划项目可整合准备。 在此，您需要开始将目标和期望转化为明确定义的路线图，其中包括具体的任务，以明确的沟通为约束，并严格审查以衡量进展。

#### Milestones {#milestones-1}

* **移交**

   干净移交可确保适当的人物／组了解他们在项目中的责任。

   应提供／生成完整的详细信息，以确保他们全面了解所有相关方面，包括路线图、范围、目标、要求和关键绩效指标。

* **风险评估**

   为避免令人不快的意外，请使用风险评估来识别和量化任何潜在风险及其影响和可能性。

   应在项目生命周期的早期进行这一工作，以确保确定和评估任何可能性。 根据调查结果，您可以向利益相关方报告是否可以执行全部要求，以及是否可以计划采取和跟踪适当行动。

* **通信**

   沟通始终是任何项目成功的关键。 您需要清晰、高效地沟通，以确保每个人：

   * 努力实现相同的基本目标
   * 从同一信息库
   * 使用相同的渠道

* **开始**

   启动会议用于提高对项目正在启动的认识。 这是一个很好的机会：

   * 邀请所有利益相关方（或至少是团体代表）。
   * 提交有关项目的重要事实。
   * 回答问题。
   * 确保每个人拥有相同的知识库。
   * 让所有参与其中的人都投入其中——这一承诺必须得到实现。

      * 通过在项目的开始让主要参与者（包括潜在作者）参与，您可以增加他们致力于项目的机会。

### 开发准备 {#development-preparation}

规划开发是确保您的项目由具备所需知识的团队在可靠的设计基础上构建的关键。

#### Milestones {#milestones-2}

* **开发团队人员和培训人员**

   在开始任何项目之前，您应确保您的开发团队配备得当，并确保所有团队成员都受过相应的任务培训。

* **内容架构**

   内容架构定义和描述了内容的未来架构；包括：

   * 内容树；包括资产
   * 基本结构；包括活动等。
   * 多站点和多语言结构（MSM、翻译等）
   * 支持内容（包括标记和标记概念）
   * 缓存和内容重用策略

* **系统架构**

   系统架构定义了系统的概念视图;包括（其中包括其他资料）:

   * [所有必需环境](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 的系统结构
   * 子系统
   * 第三方系统
   * 接口；硬件、软件和人机交互
   * 每个环境的服务器；请参阅技 [术要求](/help/sites-deploying/technical-requirements.md) 和硬 [件大小指南](/help/managing/hardware-sizing-guidelines.md)

   * 每个环境的流程；例如，部署和维护要求
   * 维护活动（数据存储GC、TarPM优化等）
   * [调度程序](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 缓存
   * [群集发布](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) /作者共享
   * 客户端性能（JS微型、简化、css Sprite、http请求总数等）

* **应用程序架构**

   应用程序体系结构定义和描述所建议应用程序的行为。

   重点是：

   * 他们如何相互和与用户交互。
   * 应用程序要消耗和生成的数据，而不是其内部结构。

   定义应包括：

   * 项目的基本代码结构
   * 代码伪像（包、包等）
   * 模板／组件及其关系的细分
   * 所需自定义项的高级详细信息（稍后将显示特定叠加）
   * 解决方案所需的工作流设计（例如，内容创建、审批、发布、转换、导入、导出等）
   * 对任何复杂模块（如MSM、Commerce、第三方集成）都有特殊考虑


* **系统集成**

   系统集成要求您计划（然后实施）:

   * 如何将所有子系统和解 [决方案集成](/help/sites-administering/integration.md) 合成为一个协调的系统
   * 将如何集成任何第三方系统；以及任何特殊注意事项，如脱机／联机、客户端／浏览器端或第三方系统停机时的故障处理

* **测试概念**

   在开始开发之前，您应该对项目的所有测试要求制定深入 [而全](/help/sites-developing/planning.md) 面的概念。

   这应包括（其中包括）:

   * 要执行的所有测试的详细信息
   * 准备这些测试所需的任何内容
   * 要使用的任何测试工具的信息
   * 高级别指示谁将参与测试；特别是QA团队外的组
   * 测试自动化的详细信息；例如，使用Selenium或AEM Developer模式

* **Experience Design**

   体验设计(XD)涉及为您的解决方案设计用户体验。

   应为作者和网站的最终用户分析和开发用户体验。

* **支持设置**

   在开发之前，应设置部署、发布、测试和报告问题所需的所有支持流程。

   另请参阅 [Adobe支持门户](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)。

### 运营规划和运营 {#operations-planning-and-operations}

在类似的基础上，必须正确规划工序，以确保您拥有项目生命周期所有阶段所需的环境。 您还需要相应的流程来维护它们。

#### Milestones {#milestones-3}

* **权限**

   您需要为所有将使用该解决方案的用户／组规划并实施角色和权限概念。

   例如：

   * 角色列表（即组），其中每个角 `read`色/ `write` 访问定义

   * 定义影响发布环境的权限的使用；例如， `replicate`
   * 对于具有最低权限的用户，应定义工作流
   * 组中的 `editor` 用户不应具有 `admin` 权限，也不应成为组的一 `administrators` 部分

   For more information, see [User Administration and Security](/help/sites-administering/security.md).

* **监控和维护**

   监控和维护是确保解决方案一旦投入使用即可顺利运行的关键方面。 为此，您需要定义：

   * 需要监控的内容
   * 维护任务;常规和特殊情况

   另请参 [阅监视和维护](/help/sites-deploying/monitoring-and-maintaining.md) ，以了解更多信息。

* **迁移**

   对于迁移，应检查并验证旧版系统中的任何内容。

* **恢复计划**

   确保已制定恢复计划。 在紧急情况下，必须提供此资源以确保AEM的生产使用。 这应涵盖备份、恢复、故障处理等情况。

### 开发 {#development}

开发是一个关键阶段，它不仅需要编码。

#### Milestones {#milestones-4}

* **开发环境**

   规划和文档您的开发环境，包括：

   * 架构
   * [开发工具](/help/sites-developing/dev-tools.md)

      * 典型环境包括：

         * 问题跟踪系统；如吉拉
         * 集成开发环境；如Eclipse
         * 构建管理工具；如马文
         * 持续整合的工具；如詹金斯
         * 用于版本控制的工具；如GIT/SVN
         * 构建对象存储库管理器；如Archiva/Nexus
   * 第三方软件集成／依赖项
   * [解决方案集成／依赖关系](/help/sites-administering/integration.md)
   * 部署节奏


* **测试系统**

   规划并文档测试环境，包括：

   * 架构
   * 对开发构建的依赖；包括夜间构建
   * 测试第三方软件集成／依赖项的可能性或限制
   * 测试工具
   * 自动化测试策略

* **生产系统**

   规划和文档您的生产环境，包括：

   * 架构
   * 部署节奏
   * 第三方软件集成／依赖项
   * 安全设置
   * 通过在生产设置上运 [行Tough Day测试](/help/sites-developing/tough-day.md) ，验证基准性能
   * 性能测试要求；请参 [阅质量保证的最佳实践](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **集成**

   规划、文档和测试系统和解决方案集 [成的所](/help/sites-administering/integration.md)有方面，包括：

   * 自动化测试策略
   * 自动化流程， [将应用程序从开发转到测试，再转到生产](/help/managing/enterprise-devops.md#code-movement)
   * 将内容从制 [作转移到测试和开发的自动化流程](/help/managing/enterprise-devops.md#content-movement)

* **迁移**

   规划、文档和测试内容迁移的各个方面；包括：

   * 内容架构
   * 迁移策略

* **通信**

   确保所有团队成员和项目角色都根据需要保持最新。

* **文档**

   文档解决方案；包括：

   * 操作手册
   * 任何可能影响升级的自定义设置
   * 发行说明

### 性能和测试 {#performance-and-testing}

新应用程序一经推出，就需要进行严格的测试，包括功能和 [性能](/help/sites-deploying/configuring-performance.md)。

>[!NOTE]
>
>应允许任何测试团队保持中立并提供测试结果。
>
>项目经理负责评估结果的任何影响并决定采取适当行动。

#### Milestones {#milestones-5}

* **最终用户接受测试**

   [用户接受测试](/help/sites-developing/acceptance-signoff.md) (UAT)对于确保：

   * 该解决方案满足用户／客户的要求
   * 客户／用户接受解决方案（功能、设计和性能）

   客户移交应有一份正式的清单；最理想的自动化并针对快照在夜间运行。 结果应发送给项目经理和开发团队

* **性能和负载测试**

   性能和负载测试用于确保解决方案在平均负载和峰值负载下满足所需的性能级别。

   有关性能测试的更多信息，请参阅：

   * [性能测试](/help/sites-deploying/configuring-performance.md)
   * [如何规划和运行测试](/help/sites-developing/planning.md)

   * [基本性能指南](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >这一进程必须在AEM的正常使用期间继续进行，但这些初始阶段是最关键的。

### 转出 {#rollout}

转出您的新应用程序需要仔细规划，以确保实现顺畅的“开始”。 这包括确认高度的安全性、培训所有潜在用户并进行多次练习以确认所有问题都已解决。

#### Milestones {#milestones-6}

* **准备**

   准备和计划将帮助确保顺利推出。

* **培训**

   确保所有相关人员都得到培训。

   请参 [阅课程](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) 目录中的Adobe Experience Manager。

* **经过培训的管理员**

   确保您的解决方案管理员：

   * 已接受培训
   * 已收到适当的培训材料
   * 已收到相应的文档

* **经过培训的用户**

   确保您的作者具有：

   * 已接受培训
   * 已收到适当的培训材料
   * 收到适当文件；例如，用户指南

* **渗透测试**

   渗透测试模拟在计算机系统上的攻击，以识别潜在的安全弱点。

* **渗透／安全测试**

   要确保解决方案的安全性，请执行特定的渗透测试以及范围更广的安全测试。

   有关更多详 [细信息，请参](/help/sites-administering/security-checklist.md) 阅安全核对清单。

### 上线 {#go-live}

您希望实时移动内容尽可能平滑。 最后的步骤也需要规划以执行清理。

#### Milestones {#milestones-7}

* **准备**

   准备和规划将有助于确保顺利上线。

* **安全**

   确认内部和外部用户及其内容的解决方案的安全性。

* **回退**

   在上线前，确保所有备用所需的系统、过程和机制都已到位。

* **支持**

   确保支持服务就地就绪并准备就绪。

* **过渡**

   规划并执行过渡给生产环境和用户。

* **转出**

   准备并执行烟雾测试。

## 角色 {#persona}

核对清单按人物设计。 这些角色在项目生命周期中具有重要的参与。

还有一些其 [他角色](#other-persona) ，涉及特定的任务。

### 项目赞助商 {#project-sponsor}

项目赞助商是：

* 负责提供／呈现项目的业务案例。
* 确定项目范围的关键；包括：

   * 成功的定义和标准
   * 主要KPI

* 根据客户路线图提供主要里程碑。

### 项目经理 {#project-manager}

项目经理为：

* 根据项目赞助商提供的要求（如范围、关键绩效指标、成功标准和定义）负责项目的整体投放。
* 负责定义预算并根据该预算为项目提供资源。
* 项目中涉及的所有角色的主要沟通点。

### 架构师 {#architect}

解决方案架构师：

* 负责解决方案和系统的高层设计。
* 帮助定义AEM的实施战略。 例如，是实施群集安装，还是冷待机，还是当需要内容投放网络(CDN)时。
* 还根据客户端要求定义AEM解决方案体系结构。 这可以包括用户角色（具有相关权限）的概念、模板与组件之间的关系，或何时使用多站点管理。

### 业务分析师 {#business-analyst}

业务分析师：

* 主要负责收集和分析高层需求，然后将这些需求转化为规范：

   * 供项目经理在计划开发时使用
   * 以便开发团队在设计和开发过程中工作。

* 与客户紧密协作以分析需求。 它们与以下内容相匹配：

   * 成功的定义。
   * 成功标准。
   * 关键绩效指标（既基于业务也基于绩效）。

### 开发领导 {#development-lead}

开发领导者：

* 负责项目的技术投放。
* 负责选择符合客户要求的开发方法。
* 制定发展战略：

   * 确保它与业务和绩效KPI保持一致
   * 考虑成功标准和定义

* 与架构师紧密合作(尤其是在制定AEM的开发战略时)，以定义模板与组件之间的关系、第三方应用程序的集成战略以及任何专用功能等方面。

### 质量潜在客户 {#quality-lead}

质量线索：

* 负责投放质量；确保它符合成功标准以及客户定义的任何KPI。
* 定义质量指标，与所有利益相关方保持一致，制定测试计划并确保它们得到执行。
* 创建报告并向项目利益相关者提供。

### 系统工程师 {#system-engineer}

系统工程师：

* 负责监督项目基础结构。
* 负责：

   * 内部开发和测试环境的设置
   * 将这些系统与客户端系统相匹配

* 在上线前和上线后提供硬件建议、监控各种实现并提供操作支持。

### 安全主管 {#security-lead}

安全主管：

* 负责解决方案的总体安全概念，确保它符合客户的任何要求和策略。
* 为任何基于硬件的安全概念提供安全概念、安全操作和建议；例如区域和防火墙。

### 其他角色 {#other-persona}

* 利益相关方

   * 对项目成功有兴趣（参与）的人员（通常来自企业）。 他们经常为预算捐款。

* 合法的

   * 谈判合同时需要法律咨询。

* 培训师

   * 根据项目的规模和性质，可利用专业培训师为相关群体制定和举办培训班。

* 技术作者

   * 根据项目的规模和性质，可以使用专业技术作者为特定群体编写指南和手册；例如，系统管理员的维护手册或作者的用户指南。

* 系统管理员

   * 负责系统的持续运行。

* 作者和最终用户

   * 将使用系统创建和维护网站内容的人员。

## 所需文档和交付件 {#required-documents-and-deliverables}

核对清单涵盖每 **个里程碑的** “必 **需文档** ”和“可交付项”。

* 两者之间没有1:1的关系；例如，一组必需的文档可以生成单个可交付项。
* 在同一里程碑期间，一个人物的可交付内容可以是另一个人物的必需文档。

### 必需文档 {#required-documents}

在制 **作交付件** 时，相应角色需要必需的文档。

对于每个 **必需文档** ，人物应指示：

* **Y/N**:是否已收到。
* **1-3**:接收文档的质量指示。

### 交付件 {#deliverables}

对于每个里程碑，相应角色负责提供特定文档，从而实现他们对特定里程碑的责任。

对于每个 **可交付** ，人物必须指明：

* **Y/N**:是否已完成。

交付项通常用作当 **前里程碑** 或以后里程碑的必需文档。

## 相关最佳实践 {#related-best-practices}

有关部署、管理、开发或创作的最佳实践，请参阅以下内容：

* 与管理AEM项目相关的其他最佳实践和准则：
   * [硬件大小调整规范](/help/managing/hardware-sizing-guidelines.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [SEO 和 URL 管理最佳实践](/help/managing/seo-and-url-management.md)
   * [AEM 和 Web 辅助功能规范](/help/managing/web-accessibility.md)
   * [一般数据保护规定](/help/managing/data-protection-and-privacy.md)*部 [署和维护最佳实践](/help/sites-deploying/best-practices.md)
* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发最佳实践](/help/sites-developing/best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)

## 关键文档区域 {#key-documentation-areas}

* AEM文档此外，AEM文档的以下部分特别感兴趣(但是，本列表并非详尽无遗):

   * [安全](/help/sites-developing/security.md)
   * [建议的部署](/help/sites-deploying/recommended-deploys.md)
   * [企业 DevOps](/help/managing/enterprise-devops.md)
   * [硬件大小调整](/help/managing/hardware-sizing-guidelines.md)
   * AEM的概念：

      * [开发——基础](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)

* 相关文档

   * Adobe Experience Cloud- [Adobe Experience Cloud规划](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)

