---
title: MSM 最佳实践
description: 查找由Adobe工程和咨询团队编译的最佳实践，帮助启动和运行AEM多站点管理器。
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 40%

---

# MSM 最佳实践{#msm-best-practices}

## 常规 {#general}

MSM 是用于自动化内容部署的可配置框架。实施通常涉及网站的主要部分，并且跨多个组织和地理区域。因此，强烈建议您像规划网站一样仔细规划 MSM 实施：

* 在开始实施之前，仔细&#x200B;**规划结构和内容流**。
* **尽可能减少活动副本的数量。** 处理活动副本是一项资源密集型任务。 您的系统中存在的Live Copy越多，受影响的性能就越好：从处理内部Live Copy索引，到通过Live Copy操作（如转出），再到用户界面操作（如在站点管理员引用边栏中显示Live Copy关系）。 最佳实践为创建站点或站点分支的Live Copy，其中Live Copy关系继承到站点或分支中的页面。 当整个结构可以制作为Live Copy时，请避免为网站或分支中的页面创建单个Live Copy。
* **进行所需数量的自定义，越少越好。** 虽然MSM支持高度自定义（例如转出配置），但通常情况下，网站的性能、可靠性和可升级性的最佳实践旨在最大程度地减少自定义。
* 尽早建立&#x200B;**治理**&#x200B;模型，并相应地培训用户以确保成功。从治理的角度来看，最佳做法是 **最大程度地降低本地内容制作者拥有的权限** 将内容分配/连接到其他本地用户及其各自的活动副本。 这是因为，不受控制的链式继承会大大增加 MSM 结构的复杂性并降低其性能和可靠性。

* 在针对您的结构、内容流、自动化和治理制定计划后 —  **原型并全面测试您的系统**，然后开始实时实施。
* 请记住，**Adobe 咨询和领先的系统集成商**&#x200B;在使用 MSM 规划和实施内容自动化方面拥有丰富的经验，他们可以帮助您启动 MSM 项目并完成整个实施。

>[!NOTE]
>
>有关使用MSM的更多信息，请参阅知识库文章：
>
>* [解决 MSM 问题和常见问题](troubleshoot-msm.md)
>

>[!NOTE]
>
>您也可以使用 [引用组件](/help/sites-authoring/default-components-foundation.md#reference) 重复使用单个页面或段落。 但请记住：
>
>* MSM更加灵活，允许对同步的内容以及同步时间进行细粒度控制。
>* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 现在建议不要使用基础组件。
>

## Live Copy 源和 Blueprint 配置 {#live-copy-sources-and-blueprint-configurations}

请记住，可以使用以下任一方式创建Live Copy [常规页面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 或 [Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 二者都是有效的用例。

使用 Blueprint 配置的额外好处是：

* 允许作者使用 **转出** Blueprint上的选项 — 到（显式）将修改推送到从此Blueprint继承的活动副本。
* 允许作者使用 **创建站点**；这允许用户轻松选择语言并配置Live Copy的结构。
* 为与Blueprint关联的活动副本定义默认转出配置。

如果未引用Blueprint配置，则只能从活动副本本身启动转出，这实际上是从源中提取内容。

使用Live Copy创建站点时，创建Blueprint配置以确保完整MSM功能集的可用性是有利的。

>[!NOTE]
>
>请注意，“权限”选项卡中的 CUG 无法从 Blueprint 转出到 Live Copy。在配置Live Copy时对此进行规划。

## 组件和容器同步 {#components-and-container-synchronization}

通常，MSM 中关于组件同步的转出规则是：

* 组件转出时将与 Blueprint 中包含的任何资源同步。
* 容器仅同步当前资源。

这意味着组件将被视为聚合，并且在转出时，组件本身及其所有子组件都将替换为 Blueprint 中的组件。这意味着，如果本地将资源添加到此类组件中，它将在转出时移至 Blueprint 的内容中。

为了支持组件的嵌套，以便在转出中维护本地添加的组件，必须将组件声明为容器。例如，默认的parsys声明为容器，以便支持本地添加的内容。

>[!NOTE]
>
>将属性 `cq:isContainer` 添加到组件中以将它指定为容器。

## 创建站点 {#create-site}

请注意，AEM有两种创建活动副本的主要方法：

* 时间 [创建Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  可将其视为更通用的方法，允许您从任何页面创建活动副本。 Live Copy的内容结构与源完全匹配。

* 时间 [创建站点](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

  这是一种更专业的方法，主要用于创建具有多语言结构的网站。

以下是创建站点时要牢记的几个注意事项：

* 要创建站点，您需要 [Blueprint配置](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* 要允许选择在新站点中创建的语言路径，相应的语言根必须存在于 Blueprint（源）中。
* 一次 [新站点已创建为Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **创建**，则 **站点**)，此Live Copy的前两个级别为 *简略*. 页面的子级不属于实时关系，但如果找到与触发器匹配的实时关系，则转出仍会下降。

  这有助于避免：

   * 在Blueprint中手动添加语言（第一个级别下）
   * 直接在语言根下手动添加内容，
   * 不会导致在转出时自动将此新内容传送到Live Copy。

## MSM 和多语言网站 {#msm-and-multilingual-websites}

MSM 可通过两种方式来帮助创建多语言网站：

* 创建语言母版时。

   * 虽然 MSM 本身&#x200B;**不提供内容翻译**，但它可以与第三方翻译连接器集成。请注意：

      * MSM允许您在页面和/或组件级别取消继承。 这有助于防止在下一次转出时覆盖已翻译的内容（来自Live Copy，以及来自Blueprint的尚未翻译的内容）。
      * 一些第三方翻译连接器会自动实施对 MSM 继承的管理。

        请与您的翻译服务提供商联系以获取更多信息。

      * 创建并翻译语言母版的另一种方法是将语言副本与 AEM 的现成的翻译集成框架结合使用。

* 从语言母版转出内容时。

   * 例如，从法语母版到特定于国家/地区的站点，如法国/法语、加拿大/法语、瑞士/法语。

有关更多信息，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)和[翻译最佳实践。](/help/sites-administering/tc-bp.md)

## 结构更改和转出 {#structure-changes-and-rollouts}

对Blueprint/源树中内容结构的修改会以不同的方式在Live Copy中反映出来。 这取决于修改类型：

* **正在创建** Blueprint中的新页面将导致在使用标准转出配置转出后，在Live Copies中创建相应的页面。

* **正在删除** 使用标准转出配置转出后，Blueprint中的页面将导致相应的页面从活动副本中删除。

* **正在移动** Blueprint中的页面将 **非** 导致相应的页面在使用标准转出配置转出后在Live Copies中移动：

   * 此行为的原因是页面移动隐式包含页面删除。这可能会导致发布时出现意外行为，因为删除创作实例上的页面会自动停用发布实例上的相应内容。这也可能对相关项目（如链接、书签等）产生连锁反应。
   * 相应Live Copy页面中的内容继承已更新，以反映其源在Blueprint中的新位置。
   * 要完全实现从Blueprint到活动副本的页面移动，请考虑以下最佳实践：

>[!NOTE]
>
>这仅适用于 [在转出触发时](/help/sites-administering/msm-sync.md#rollout-triggers).

* 创建自定义转出配置：

   * 此新配置必须包含操作：

     `PageMoveAction`

     不要向此配置添加其他操作。

* 定位新配置：

   * 要完全转出页面移动，同时在Live Copy中的旧位置删除相应的页面，请执行以下操作：

      * 将新创建的配置放置在标准转出配置的前面。

        标准转出配置将负责删除旧位置的页面。

   * 要转出页面移动，同时将相应页面保留在活动副本中的旧位置（本质上重复内容），请执行以下操作：

      * 将新创建的配置放置在标准转出配置的后面。

        这将确保未在Live Copy中删除内容或从发布中停用内容。

## 自定义转出 {#customizing-rollouts}

MSM 转出配置是高度自定义的。自动化转出可能会产生深远的影响。 作为最佳实践，您应当 *非常* 例如，之前请务必谨慎：

* 自动化转出；例如，使用 [onModify触发器](#onmodify)，
* 自定义 [节点类型/属性](#node-types-properties)，
* 启动后续工作流，
* 和/或激活内容作为转出的一部分。

### onModify {#onmodify}

在使用[转出触发器](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` 时，您应考虑：

* 使用 `onModify` 触发器自动化转出可能会对创作性能产生负面影响，因为它们会在每次修改页面后触发转出。**

* 转出结果可能与预期结果不同：

   * 您不能指定生成的修改事件的顺序。
   * 基于事件的架构不能保证传递给 Rollout Manager 的事件的顺序。

* 如果对同一资源进行并发更新，则使用此转出配置可能会导致发生提交冲突。

因此，建议您 *仅限* 使用 `onModify` 如果自动转出启动的好处多于任何潜在的性能问题，则会触发。

### 节点类型/属性 {#node-types-properties}

请记住：

* 除了自定义转出操作之外，MSM 还让您自定义正在转出的节点属性。此 [MSM OSGi配置允许您排除节点类型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 从源复制到Live Copy的过程中。

## 更多信息 {#further-information}

本页和以下页面介绍了相关问题：

* [创建并同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
