---
title: MSM最佳实践
seo-title: MSM最佳实践
description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助AEM多站点管理器快速入门和运行。
seo-description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助AEM多站点管理器快速入门和运行。
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 1%

---


# MSM最佳实践{#msm-best-practices}

## 常规 {#general}

MSM是一个可配置的框架，用于自动进行内容部署。 实施通常涉及网站的主要部分，并且跨组织和地理位置。 因此，强烈建议在规划网站时像计划一样仔细地规划MSM实施：

* 开始 **实施之前，请仔细规划结构** 和内容流。
* **自定义所需数量，但尽可能少。** 虽然MSM支持高度自定义（例如转出配置），但网站的性能、可靠性和可升级性的最佳实践是最大限度地减少自定义。
* 尽早建 **立治理模** 式，并相应地培训用户，确保成功。 从视图的治理角度来说，最佳做法是尽 **可能减少本地内容制作者向其他本地用户** 及其各自的Live Copy分配／连接内容的权限。 这是因为不受管制的链式继承可以显着增加MSM结构的复杂性并降低其性能和可靠性。

* 一旦存在针对您的结构、内容流、自动化和管理的计划， **在开始实时实施之前，为您的系统**&#x200B;构建原型并进行彻底测试。
* 请记住，Adobe咨 **询和领先的系统集成商在MSM的规划和实施内容自动化方面具有丰富的经验** ，因此他们可以帮助您开始使用MSM项目并贯穿整个实施过程。

>[!NOTE]
>
>有关与MSM协作的更多信息，请参阅知识库文章：
>
>* [MSM常见问题解答](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [MSM问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>您还可以使用引 [用组件](/help/sites-authoring/default-components-foundation.md#reference) ，重用单个页面或段落。 但是，请牢记：
>
>* MSM更灵活，允许对同步的内容和时间进行细致的控制。
>* [现在](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) ，在基础组件上推荐核心组件。

>



## Live Copy源和Blueprint配置 {#live-copy-sources-and-blueprint-configurations}

请记住，Live Copy可以使用常规页面 [或Blueprint配](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 置 [创建](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。 这两种情况都是有效的用例。

使用Blueprint配置的额外好处是：

* 允许作者在Blueprint上使 **用** “转出”选项——将修改（显式）推送到继承自此Blueprint的Live Copy。
* 允许作者使用创 **建站点**;这允许用户轻松选择语言并配置Live Copy的结构。
* 为与Blueprint有关系的Live Copy定义默认转出配置。

如果未引用Blueprint配置，则只能从Live Copy本身启动转出，实质上是从源中提取内容。

创建包含Live Copy的新站点时，创建蓝图配置是非常有利的，这可确保完整的MSM功能集可用。

## 组件和容器同步 {#components-and-container-synchronization}

通常，MSM中关于组件同步的转出规则为：

* 组件将被执行同步蓝图中包含的任何资源。
* 容器仅同步当前资源。

这意味着组件被视为聚合，在推广中，组件本身及其所有子项将替换为Blueprint中的子项。 这意味着，如果资源在本地添加到此类组件，则在转出时将丢失到Blueprint的内容。

要支持组件的嵌套，以便在本地添加的组件在转出中进行维护，必须将该组件声明为容器。 例如，默认的parsys声明为容器，因此它可以支持本地添加的内容。

>[!NOTE]
>
>将属性添 `cq:isContainer` 加到组件，以将其指定为容器。

## 创建站点 {#create-site}

请注意，AEM有两种主要方法可用于创建Live Copy:

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   这可以视为更通用的方法，允许您从任何页面创建Live Copy。 Live Copy的内容结构与源完全匹配。

* 创 [建站点时](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   这是一种更专业的方法，主要用于创建具有多语言结构的网站。

以下是创建站点时要注意的几个注意事项：

* 要创建新站点，您需要Blueprint [配置](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 要允许选择要在新站点中创建的语言路径，蓝图（源）中必须存在相应的语言根。
* 将新 [站点创建为Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **创建**，然后 **使用站点**)后，此Live Copy的前两个级别为 **&#x200B;浅。 页面的子项不属于实时关系，但如果找到与触发器匹配的实时关系，则滚动仍将下降。

   它有助于避免：

   * 在blueprint中手动添加语言（在第一层下）
   * 手动将内容直接添加到语言根目录下，
   * 不会导致在转出时自动将新内容转移到Live Copy。

## MSM和多语言网站 {#msm-and-multilingual-websites}

MSM可通过两种方式协助创建多语言网站：

* 创建语言母版时。

   * 虽然MSM本身 **不提供内容翻译**，但可以与提供内容翻译的第三方翻译连接器集成。 请注意：

      * MSM允许您在页面和／或组件级别取消继承。 这有助于防止在下一个转出时覆盖已翻译的内容（来自Live Copy，含来自蓝图的尚未翻译的内容）。
      * 某些第三方翻译连接器可自动管理MSM继承。

         请咨询您的翻译服务提供商以了解更多信息。

      * 创建和翻译语言母版的另一种方法是将语言副本与AEM现成的翻译集成框架结合使用。

* 从语言大师那里推出内容时。

   * 例如，从法语主控到国家特定网站，如法国／法语、加拿大／法语、瑞士／法语。

有关详细信息，请 [参阅翻译多语言站点的内容](/help/sites-administering/translation.md) 和翻 [译最佳实践](/help/sites-administering/tc-bp.md)。

## 结构更改和转出 {#structure-changes-and-rollouts}

对蓝图／源树中内容结构的修改在Live Copy中反映的不同。 这取决于修改类型：

* **在Blueprint** 中创建新页面将导致在使用标准转出配置转出后在Live Copy中创建相应的页面。

* **在Blueprint中** ，删除页面将导致在使用标准转出配置转出后从Live Copy中删除相应页面。

* **使用** 标准转出配置转 **出后** ，移动Blueprint中的页面不会导致相应页面被移动到Live Copy中：

   * 此行为的原因是页面移动隐式包括页面删除。 这可能会导致发布时出现意外行为，因为在作者上删除页面会在发布时自动停用相应内容。 这也可能对链接、书签等相关项目产生连锁效应。
   * 相应Live Copy页面中的内容继承将更新，以反映其源在蓝图中的新位置。
   * 要完全实现页面从蓝图移动到Live Copy，请考虑以下最佳实践：

>[!NOTE]
>
>此操作仅适用于“转 [出时”触发器](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)。

* 创建自定义转出配置：

   * 此新配置必须包括操作：

      `PageMoveAction`

      请勿向此配置添加其他操作。

* 定位新配置：

   * 在Live Copy中删除各自旧位置的页面时，要完全滚出页面移动：

      * 在标准转出配置之前放置新创建的配置。

         标准转出配置将负责删除旧位置中的页面。
   * 要在将各个页面保留在Live Copy的旧位置（实质上是复制内容）的同时滚出页面移动，请执行以下操作：

      * 在标准转出配置之后定位新创建的配置。

         这将确保Live Copy中未删除任何内容或从发布中取消激活任何内容。


## 自定义转出 {#customizing-rollouts}

MSM转出配置可高度自定义。 您应该知道，自动推广可能会产生深远的影响。 作为最佳实践，您应在 *之前* ，非常谨慎地进行规划，例如：

* 自动推广；例如，使用 [onModify触发器](#onmodify),
* 自定义 [节点类型／属性](#node-types-properties),
* 开始后续工作流,
* 和／或激活内容作为推广的一部分。

### onModify {#onmodify}

使用转出 [触发器](/help/sites-administering/msm-sync.md#rollout-triggers)`onModify` 时，您应考虑：

* 使用触发器 `onModify` 实现自动转出可能会对创作性能产生负面影响，因为它们在每次页面修改后都 *会触发* 转出。

* 转出结果可能与预期结果不同：

   * 您不能指定生成的修改事件的顺序。
   * 基于事件的体系结构无法保证传递给转出管理器的事件的序列。

* 如果同一资源的并发更新发生，使用此类转出配置可能会导致提交冲突。

因此，建议您仅在自动转 *出启动*`onModify` 的好处超过任何潜在性能问题时使用触发器。

### 节点类型／属性 {#node-types-properties}

记住：

* 除了自定义转出操作之外，MSM还允许您自定义正在转出的节点属性。 MSM [OSGi配置允许您排除从源](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) - Live Copy复制到节点类型的情况。

## 更多信息 {#further-information}

本页和以下各页介绍相关问题：

* [创建和同步Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM转出冲突](/help/sites-administering/msm-rollout-conflicts.md)

