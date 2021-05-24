---
title: MSM最佳实践
seo-title: MSM最佳实践
description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助启动和运行AEM多站点管理器。
seo-description: 查找由Adobe工程和咨询团队编译的最佳实践，以帮助启动和运行AEM多站点管理器。
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: 多站点管理器
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 1%

---

# MSM最佳实践{#msm-best-practices}

## 常规 {#general}

MSM是用于自动进行内容部署的可配置框架。 实施通常涉及网站的主要部分，并跨组织和地理区域。 因此，强烈建议在规划网站时谨慎规划MSM实施：

* 在开始实施之前，请仔细&#x200B;**规划结构和内容流**。
* **将Live Copy的数量保持在最低。** 处理Live Copy是一项资源密集型任务。系统中存在的Live Copy越多，对性能的影响就越大：从处理内部live copy索引，到Live Copy操作（如转出），再到UI操作（如在站点管理员引用边栏中显示live Copy关系）。 最佳做法是创建站点或站点分支的Live Copy，其中Live Copy关系会继承到站点或分支的页面。 当整个结构都可以制作为Live Copy时，请避免为站点或分支中的页面创建单个Live Copy。
* **根据需要尽可能多地进行自定义，但尽可能少地进行自定义。** 虽然MSM支持高度自定义（例如转出配置），但是对于网站的性能、可靠性和可升级性，通常的最佳实践是最大限度地减少自定义。
* 尽早建立&#x200B;**governance**&#x200B;模型，并相应地培训用户，以确保成功。 从治理角度来看，最佳做法是&#x200B;**最小化本地内容制作者拥有的将内容分配/连接到其他本地用户及其各自Live Copy的权限。**&#x200B;这是因为不受管理、链式继承可以显着增加MSM结构的复杂性并降低其性能和可靠性。

* 在您的结构存在计划后，内容流、自动化和管理 — **原型并对系统**&#x200B;进行全面测试，然后再开始实时实施。
* 请记住，**Adobe咨询团队和领先的系统集成商**&#x200B;具有与MSM一起进行内容自动化规划和实施的丰富经验，因此他们可以帮助您开始使用MSM项目并贯穿其整个实施过程。

>[!NOTE]
>
>有关使用MSM的更多信息，请参阅知识库文章：
>
>* [MSM常见问题解答](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [MSM问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>您还可以使用[引用组件](/help/sites-authoring/default-components-foundation.md#reference)来重复使用单个页面或段落。 但请记住：
>
>* MSM更加灵活，允许对同步的内容和时间进行细粒度控制。
>* [现在](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 推荐核心组件而不是基础组件。

>



## Live Copy源和Blueprint配置{#live-copy-sources-and-blueprint-configurations}

请记住，Live Copy可以使用[常规页面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)或[Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)创建。 这两种方法都是有效的用例。

使用Blueprint配置的其他好处是：

* 允许作者在Blueprint上使用&#x200B;**转出**&#x200B;选项 — 将修改（显式）推送到从此Blueprint继承的Live Copy。
* 允许作者使用&#x200B;**Create Site**;这允许用户轻松选择语言并配置Live Copy的结构。
* 为与Blueprint有关的Live Copy定义默认转出配置。

如果未引用Blueprint配置，则只能从Live Copy本身启动转出，实质上是从源中提取内容。

使用Live Copy创建新站点时，最好创建Blueprint配置，以确保完整MSM功能集的可用性。

>[注意!]
>
> 请注意，“权限”选项卡中的CUG无法从Blueprint中转出到Live Copy。 请在配置Live Copy时针对此进行规划。

## 组件和容器同步{#components-and-container-synchronization}

通常，MSM中有关组件同步的转出规则为：

* 组件可以同步Blueprint中包含的所有资源。
* 容器仅同步当前资源。

这意味着组件被视为聚合，在推出过程中，组件本身及其所有子代将被蓝图中的组件替换。 这意味着如果资源在本地添加到此类组件，则在转出时将会丢失到Blueprint的内容。

要支持嵌套组件以便在转出中维护本地添加的组件，必须将组件声明为容器。 例如，默认的parsys声明为容器，以便它可以支持本地添加的内容。

>[!NOTE]
>
>将属性`cq:isContainer`添加到组件以将其指定为容器。

## 创建站点 {#create-site}

请注意，AEM有两种主要方法可用于创建Live Copy:

* [创建Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)时

   这可以视为更宽泛的方法，允许您从任何页面创建Live Copy。 Live Copy的内容结构与源完全匹配。

* [创建Site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)时

   这是一种更为专门的方法，主要用于创建具有多语言结构的网站。

在创建网站时，请注意以下事项：

* 要创建新站点，您需要[blueprint配置](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 要允许选择要在新站点中创建的语言路径，相应的语言根必须存在于Blueprint（源）中。
* 将[新站点创建为Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)（使用&#x200B;**创建**，然后使用&#x200B;**Site**）后，此Live Copy的前两个级别为&#x200B;*shallow*。 页面的子项不属于实时关系，但如果找到与触发器匹配的实时关系，则转出仍将下降。

   这有助于避免：

   * 在blueprint中手动添加语言（在第一级以下）
   * 手动在语言根目录的正下方添加内容，
   * 不会导致在转出时自动将新内容传递到Live Copy中。

## MSM和多语言网站{#msm-and-multilingual-websites}

MSM可通过两种方式协助创建多语言网站：

* 创建语言母版时。

   * 虽然MSM本身&#x200B;**不提供内容翻译**，但它可以与提供内容的第三方翻译连接器集成。 请注意：

      * MSM允许您在页面和/或组件级别取消继承。 这有助于防止在下一个转出中覆盖已翻译的内容（来自Live Copy，包含来自Blueprint的尚未翻译的内容）。
      * 某些第三方翻译连接器会自动管理MSM继承。

         有关更多信息，请咨询您的翻译服务提供商。

      * 创建和翻译语言母版的另一种方法是结合AEM现成翻译集成框架使用语言副本。

* 从语言母版中推出内容时。

   * 例如，从主控法语到特定国家的地点，如法国/法语、加拿大/法语、瑞士/法语。

有关更多信息，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)和[翻译最佳实践](/help/sites-administering/tc-bp.md)。

## 结构更改和转出{#structure-changes-and-rollouts}

Blueprint/源树中内容结构的修改在Live Copy中的反映方式不同。 这取决于修改类型：

* **** 使用标准转出配置在转出后，在Blueprint中创建新页面将导致在Live Copy中创建相应的页面。

* **** 使用标准转出配置转出后，删除Blueprint中的页面将导致从Live Copy中删除相应的页面。

* **** 使用标准转出配置 **** 转出后，在Blueprint中移动页面不会导致相应页面在Live Copy中移动：

   * 此行为的原因是页面移动会隐式包含页面删除。 这可能会在发布时导致意外行为，因为删除作者的页面会在发布时自动停用相应的内容。 这也可能会对相关项目（如链接、书签和其他项目）产生连锁影响。
   * 相应Live Copy页面中的内容继承会进行更新，以反映其源在Blueprint中的新位置。
   * 要完全实现页面从Blueprint移动到Live Copy，请考虑以下最佳实践：

>[!NOTE]
>
>此操作仅适用于[On Rollout trigger](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)。

* 创建自定义转出配置：

   * 此新配置必须包含操作：

      `PageMoveAction`

      请勿向此配置添加其他操作。

* 定位新配置：

   * 要完全转出页面移动，同时在Live Copy中的旧位置删除相应的页面：

      * 将新创建的配置放在标准转出配置之前。

         标准转出配置将负责删除其旧位置中的页面。
   * 要在将相应页面保留在Live Copy中其旧位置（实质上是复制内容）的同时转出页面移动，请执行以下操作：

      * 在标准转出配置后放置新创建的配置。

         这将确保Live Copy中未删除或从发布中停用任何内容。


## 自定义转出{#customizing-rollouts}

MSM转出配置是高度可自定义的。 您应该知道，自动推广可能会产生深远的后果。 作为最佳实践，您应该先仔细规划&#x200B;*very*，然后再规划，例如：

* 自动推广；例如，使用[onModify triggers](#onmodify)时，
* 自定义[节点类型/属性](#node-types-properties),
* 启动后续工作流，
* 和/或在转出中激活内容。

### onModify {#onmodify}

使用[转出触发器](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`时，您应当考虑以下事项：

* 使用`onModify`触发器自动转出可能会对创作性能产生负面影响，因为它们会在&#x200B;*每次*&#x200B;页面修改后触发转出。

* 转出结果可能与预期结果不同，如下所示：

   * 您无法指定结果修改事件的顺序。
   * 基于事件的架构无法保证传递到转出管理器的事件的顺序。

* 如果同一资源发生并发更新，使用此类转出配置可能会导致提交冲突。

因此，如果自动推出启动的好处超过任何潜在的性能问题，则建议您&#x200B;*仅*&#x200B;使用`onModify`触发器。

### 节点类型/属性{#node-types-properties}

请记住：

* 除了自定义转出操作之外，MSM还允许您自定义正在转出的节点属性。 [MSM OSGi配置允许您排除从源复制到Live Copy的节点类型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

## 更多信息 {#further-information}

本页和以下页介绍了相关问题：

* [创建和同步Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
