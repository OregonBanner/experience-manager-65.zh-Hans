---
title: 高级评分和徽章
seo-title: 高级评分和徽章
description: 设置高级评分
seo-description: 设置高级评分
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# 高级评分和徽章{#advanced-scoring-and-badges}

## 概述 {#overview}

高级评分允许授予徽章，将会员标识为专家。 高级评分根据成员创建的 *内容* 的数量和质量分配积分，而基本评分则只根据创建的内容数量分配积分。

此差异是由于用于计算得分的得分引擎。 基本评分引擎应用简单的数学。 高级评分引擎是一种自适应算法，它奖励通过主题的自然语言处理(NLP)推导的、贡献有价值和相关内容的活跃成员。

除了内容相关性外，评分算法还考虑成员活动，如投票和答案百分比。 虽然基本评分包括定量评分，但高级评分会通过算法来使用这些评分。

因此，高级评分引擎需要足够的数据来使分析有意义。 随着算法不断调整所创建内容的体积和质量，成为专家的成就阈值会不断被重新评估。 还有一个概念是 *成员* 较旧职位的衰败。 如果专家成员停止参与他们获得专家身份的主题，在某个预定点(请参 [阅评分引擎配置](#configurable-scoring-engine))，他们可能失去专家身份。

设置高级评分与基本评分基本相同：

* 基本和高级评分和徽章规则 [以相同方式应](/help/communities/implementing-scoring.md#apply-rules-to-content) 用于内容。

   * 基本和高级评分和徽章规则可应用于相同内容。

* [为组件启用标记](/help/communities/implementing-scoring.md#enable-badges-for-component) 是通用的。

设置评分和徽章规则的区别是：

* 可配置的高级评分引擎
* 高级评分规则：

   * `scoringType` 设置为 `advanced`
   * 需要 `stopwords`

* 高级标记规则：

   * `badgingType` 设置为 `advanced`
   * `badgingLevels` 设置为 **要授予的专家级别数**
   * 需要 `badgingPaths` 标记阵列，而不是阈值阵列映射点到标记。

>[!NOTE]
>
>要使用高级评分和徽章功能，请安 [装专家识别包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)。

## 可配置的评分引擎 {#configurable-scoring-engine}

高级评分引擎提供OSGi配置，其参数影响高级评分算法。

![高级评分引擎](assets/advanced-scoring-engine.png)

* **评分权重**

   对于主题，指定在计算得分时应给予最高优先级的动词。 可输入一个或多个主题，但每个主题限 **于一个动词**。 请参 [阅主题和动词](/help/communities/implementing-scoring.md#topics-and-verbs)。
以逗号 `topic,verb` 转义的方式输入。 例如：
   `/social/forum/hbs/social/forum\,ADD`
对于QnA和论坛组件，默认设置为ADD动词。

* **评分范围**

   高级得分的范围由此值（最高可能得分）和0（最低可能得分）定义。

   默认值为100，因此评分范围为0-100。

* **实体衰减时间间隔**

   此参数表示所有实体得分被延迟的小时数。 这要求不再在社区站点的分数中包含旧内容。

   默认值为216000小时（~24年）。

* **评分增长率**&#x200B;这指定0和评分范围之间的得分，超出该范围后，增长会放缓以限制专家数量。

   默认值为 50。

## 高级评分规则 {#advanced-scoring-rules}

在基本评分中，获得徽章所需的数量是已知的。

在高级评分中，根据系统内的质量数据量不断调整所需数量。 评分会以类似钟形曲线的方式持续计算。

如果某位成员在某个主题上获得了专家徽章，而该主题不再有效，那么他们可能会因为时间的流逝而失去自己的徽章。

### scoringType {#scoringtype}

评分规则是评分子规则集，每个子规则都声明 `scoringType`。

要调用高级评分引擎， `scoringType`应将其设置为 `advanced`。

请参 [阅评分子规则](/help/communities/implementing-scoring.md#scoring-sub-rules)。

![高级评分类型](assets/advanced-scoring-type.png)

### 秒词 {#stopwords}

高级评分包会安装一个配置文件夹，其中包含一个秒词文件：

* `/libs/settings/community/scoring/configuration/stopwords`

高级评分算法使用秒词文件中包含的字的列表来识别在内容处理过程中被忽略的常见英语字。

不希望修改此文件。

如果秒词文件缺失，高级评分引擎将抛出错误。

## 高级徽章规则 {#advanced-badging-rules}

高级标记规则属性与基本标记 [规则属性不同](/help/communities/implementing-scoring.md#badging-rules)。

除了将点与徽章图像关联之外，只需确定允许的专家数量和要授予的徽章图像。

![高级徽章规则](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>类型</th>
   <th>值描述</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em>(必需</em> )徽章图像的多值字符串，最高为badgingLevels的数量。 必须对徽章图像路径进行排序，以便将第一个路径授予最高专家。 如果标记数少于badgingLevels所指示的标记数，则数组中的最后一个标记将填充数组的其余部分。 示例条目：<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>标记级别</td>
   <td>长整型</td>
   <td><em>(可选</em> )指定要授予的专业知识级别。 例如，如果应该有一个 <code>expert </code>标记 <code>almost expert</code> 和一个标记（两个标记），则值应设置为2。 badgingLevel应与为badgingPath属性列出的与专家相关的徽章图像的数量相对应。 默认值为1。</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>字符串</td>
   <td><em>（必需）</em> 将评分引擎标识为“基本”或“高级”。 如果设置为“高级”，则默认值为“基本”。</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>（可选）</em> ，用于将标记规则限制为对列出的评分规则标识的事件进行评分的多值字符串。<br /> 示例条目：<br /><code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> 默认值为无限制。</td>
  </tr>
 </tbody>
</table>

## 包含的规则和徽章 {#included-rules-and-badge}

### 包含的徽章 {#included-badge}

此测试版中包含一个基于奖励的专家徽章：

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![专家徽章](assets/included-badge.png)

要让专家徽章显示为活动奖励，请确保：

* `Badges` 功能（如论坛或问题与答案组件）。

* 高级评分和标记规则应用于放置组件的页面（或上级）

请参阅以下内容的基本信息：

* [为组件启用标记](/help/communities/implementing-scoring.md#enableforcomponent)
* [应用规则](/help/communities/implementing-scoring.md#applytopage)

### 包括评分规则和子规则 {#included-scoring-rules-and-sub-rules}

测试版包含两个用于论坛功能的高级评 [分规则](/help/communities/functions.md#forum-function) （每个规则分别用于论坛和论坛功能的评论组件）:

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**注释:**

* 节 `rules` 点和 `sub-rules` 节点都属于类型 `cq:Page`。

* `subRules` 是规则节点上[] “字符串”类型的属 `jcr:content` 性。

* `sub-rules` 可以在各种评分规则之间共享。

* `rules` 应该位于具有所有人读取权限的存储库位置。

* 规则名称必须唯一，无论位置如何。

### 包含徽章规则 {#included-badging-rules}

该版本中包含两个与高级论坛和评论评分规则相 [对应的高级标记规则](#included-scoring-rules-and-sub-rules)。

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**注释:**

* `rules` 节点的类型为cq:Page。
* `rules` 应该位于具有所有人读取权限的存储库位置。
* 规则名称必须唯一，无论位置如何。

