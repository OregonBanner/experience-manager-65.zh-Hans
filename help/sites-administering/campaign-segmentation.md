---
title: 配置分段
seo-title: 配置分段
description: 了解如何为AEM Campaign配置分段。
seo-description: 了解如何为AEM Campaign配置分段。
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 配置分段 {#configuring-segmentation}

>[!NOTE]
>
>本文档涵盖与Client Context一起使用的分段配置。 要使用触屏UI配置ContextHub区段，请参阅 [使用ContextHub配置分段](/help/sites-administering/segmentation.md)。

分段是创建营销活动时的主要考虑事项。有关细 [分工作方式](/help/sites-authoring/segmentation-overview.md) 和关键术语的信息，请参阅分段词汇表。

根据您已收集的有关网站访客的信息以及要实现的目标，您需要为目标内容定义所需的细分和策略。

然后，这些区段用于为访客提供特定目标内容。 此内容在网站的“营 [销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) ”部分进行维护。 此处定义的Teaser页面可以作为Teaser段落包含在任何页面上，并定义专用内容适用的访客段。

AEM允许您轻松创建和更新区段、Teaser和营销活动。 它还允许您验证定义的结果。

区段 **编辑器** ，允许您轻松定义区段：

![](assets/segmenteditor.png)

您可以 **编辑** 每个区段以指定标题 **、说明**&#x200B;和提升 **因****** 子。 使用Sidekick，您可以添加 **AND****和** OR **容器来定义区段逻辑**，然后添加所需的区段特征以 **** 定义选择标准。

## 提升因子 {#boost-factor}

每个细分都有 **Boost** （提升）参数，用作加权因子；数字越大，表示将优先选择数字越低的区段。

* Minimum value: `0`
* Maximum value: `1000000`

## 细分逻辑 {#segment-logic}

以下逻辑容器现成可用，允许您构建区段选择的逻辑。 可以将它们从Sidekick拖动到编辑器：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布尔AND运算符。<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布尔OR运算符。</td>
  </tr>
 </tbody>
</table>

## 区段特征 {#segment-traits}

以下细分特征现成可用；可以将它们从Sidekick拖动到编辑器：

<table>
 <tbody>
  <tr>
   <td> IP 范围<br /> </td>
   <td>定义访客可以拥有的IP地址范围。<br /> </td>
  </tr>
  <tr>
   <td> 页面点击<br /> </td>
   <td>请求页面的频率。 <br /> </td>
  </tr>
  <tr>
   <td> 页面属性<br /> </td>
   <td>已访问页面的任何属性。<br /> </td>
  </tr>
  <tr>
   <td> 引用关键字<br /> </td>
   <td>要与引用网站中的信息匹配的关键字。 <br /> </td>
  </tr>
  <tr>
   <td> 脚本</td>
   <td>要计算的Javascript表达式。<br /> </td>
  </tr>
  <tr>
   <td> 段引用 <br /> </td>
   <td>参考其他区段定义。<br /> </td>
  </tr>
  <tr>
   <td> 标记云<br /> </td>
   <td>与访问的页面中的标记相匹配的标记。<br /> </td>
  </tr>
  <tr>
   <td> 用户年龄<br /> </td>
   <td>从用户配置文件中获取。<br /> </td>
  </tr>
  <tr>
   <td> 用户属性<br /> </td>
   <td>用户配置文件中提供的任何其他信息。 </td>
  </tr>
 </tbody>
</table>

您可以使用布尔运算符OR和AND(请参阅 [创建新区段](#creating-a-new-segment))组合这些特征，以定义选择此区段的确切方案。

当整个语句的计算结果为true时，此段已解析。 如果有多个区段适用，则还会 **[使用提](/help/sites-administering/campaign-segmentation.md#boost-factor)**升因子。

>[!CAUTION]
>
>区段编辑器不检查任何循环引用。 例如，区段A引用另一个区段B，而该区段B又引用区段A。您必须确保您的区段不包含任何循环引用。

>[!NOTE]
>
>具有 **_i18n** 后缀的属性由作为个性化UI clientlib的一部分的脚本设置。 只有作者才会加载所有与UI相关的客户端库，因为发布时不需要UI。
>
>因此，创建具有此类属性的区段时，通常需要依赖 **browserFamily** ，而不是 **browserFamily_i18n**。

### 创建新区段 {#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在边栏中，选择“工 **具”>“操作”>“配置”**。
1. 单击左侧窗 **格中的** “分段”页面，然后导航到所需的位置。
1. 使用区 [段模板](/help/sites-authoring/editing-content.md#creatinganewpage) ，创建 **新页面** 。
1. 打开新页面以查看区段编辑器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. **使用Sidekick或上下文菜单(通常是鼠标右键单击，然后选择“**&#x200B;新建……”)。打开“插入新组件”窗口)以查找所需的段特征。 然后将其拖动到区 **段编辑器** ，它将显示在默认 **AND容器中** 。
1. 双击新特征以编辑特定参数；例如，鼠标位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. Click **OK** to save your definition:
1. 您可以 **编辑** ，为区段定义指定标题 **、说明**&#x200B;和提 ******[](#boost-factor)**升因子：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 根据需要添加更多特征。 您可以使用“段逻辑”下的 **AND Container****和OR Container** 组件来表达布 **尔表达式**。 使用区段编辑器，您可以删除不再需要的特征或容器，或将它们拖动到语句中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

您可以在AEM中构建复杂的区段。 了解以下几个基本要点有所帮助：

* 定义的顶级始终是最初创建的AND容器；此操作无法更改，但对您的其余区段定义没有影响。
* 确保容器的嵌套是合理的。 容器可以作为布尔表达式的括号查看。

以下示例用于选择以下任一访客：

男，16岁至65岁

或者

16岁至62岁的女性

由于主操作符是OR，您需要从 **OR Container开始**。 在此中，您有2个AND语句，对于每个语句，您都需要一个 **AND容器**，您可以在其中添加单个特征。

![](assets/screen_shot_2012-02-02at105145am.png)

## 测试区段的应用 {#testing-the-application-of-a-segment}

定义区段后，可以借助Client Context测试潜在 **[结果](/help/sites-administering/client-context.md)**:

1. 选择要测试的区段。
1. 按 **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**，打开Client Context**[](/help/sites-administering/client-context.md)**，其中显示已收集的数据。 为便于测试，您可以 **编辑某些值** ，或加载其 **他配置文件** ，以了解其影响。

1. 根据定义的特征，当前页面可用的数据可能与区段定义匹配，也可能不匹配。 匹配状态显示在定义下方。

例如，简单的细分定义可以基于用户的年龄和性别。 加载特定配置文件表明区段已成功解析：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数情况只会在页面重新加载时发生更改。 对鼠标位置的更改会立即显示，因此对于测试而言非常有用。

此类测试还可以在内容页面上执行，并与 **Teaser组件结合** 。

将鼠标悬停在Teaser段落上将显示所应用的段，无论这些段当前是否解析，以及为何选择了当前Teaser实例：

![](assets/chlimage_1-47.png)

### 使用您的细分 {#using-your-segment}

区段当前在营销活动中 [使用](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。 它们用于控制特定目标受众看到的实际内容。 有关更 [多信息，请参阅](/help/sites-authoring/segmentation-overview.md) “了解细分”。
