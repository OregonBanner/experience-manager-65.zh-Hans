---
title: 配置分段
description: 了解如何为AEM Campaign配置分段。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 13%

---


# 配置分段 {#configuring-segmentation}

>[!NOTE]
>
>本文档介绍与Client Context一起使用的区段的配置。 要使用触屏UI在ContextHub中配置区段，请参阅 [使用ContextHub配置分段](/help/sites-administering/segmentation.md).

分段是创建营销活动时的主要考虑事项。请参阅 [分段术语表](/help/sites-authoring/segmentation-overview.md) 有关分段的工作方式和关键术语的信息。

根据您收集到的有关网站访客的信息以及要实现的目标，必须定义目标内容所需的区段和策略。

之后，这些区段可用于为访客提供具体的目标内容。此内容维护于 [营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) 部分。 此处定义的Teaser页面可以包含在任何页面上作为Teaser段落，并定义专用内容适用于的访客区段。

AEM可让您轻松创建和更新区段、Teaser和营销活动。 它还允许您验证定义的结果。

此 **区段编辑器** 可让您轻松定义区段：

![“区段编辑器”窗口](assets/segmenteditor.png)

您可以 **编辑** 每个区段以指定 **标题**， **描述** 和 **提升** 因素。 使用可以添加的sidekick **和** 和 **或者** 用于定义 **区段逻辑**，然后添加所需的 **区段特征** 以定义选择标准。

## 提升因子 {#boost-factor}

每个区段都有一个 **提升** 用作加权因子的参数；数字越大，表示优先选择区段而不是数字越小的区段。

* 最小值：`0`
* 最大值：`1000000`

## 区段逻辑 {#segment-logic}

以下逻辑容器是现成可用的，可让您构建区段选择的逻辑。 他们可以被从副手拖到主编：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布尔 AND 运算符.<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布尔 OR 运算符.</td>
  </tr>
 </tbody>
</table>

## 区段特征 {#segment-traits}

以下区段特征是现成可用的；它们可以从Sidekick拖到编辑器中：

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
   <td>所访问页面的任意属性。<br /> </td>
  </tr>
  <tr>
   <td> 引用关键字<br /> </td>
   <td>与引用网站中的信息匹配的关键字。 <br /> </td>
  </tr>
  <tr>
   <td> 脚本</td>
   <td>要计算的JavaScript表达式。<br /> </td>
  </tr>
  <tr>
   <td> 区段引用 <br /> </td>
   <td>引用其他区段定义。<br /> </td>
  </tr>
  <tr>
   <td> 标记云<br /> </td>
   <td>要与所访问页面中的标记匹配的标记。<br /> </td>
  </tr>
  <tr>
   <td> 用户年龄<br /> </td>
   <td>从用户配置文件中获取。<br /> </td>
  </tr>
  <tr>
   <td> 用户属性<br /> </td>
   <td>用户配置文件中可用的任何其他信息。 </td>
  </tr>
 </tbody>
</table>

您可以使用布尔运算符OR和AND来组合这些特征(请参阅 [创建新区段](#creating-a-new-segment))，以定义选择此区段的确切场景。

当整个语句的计算结果为true时，表示该区段已解析。 如果有多个适用的区段，则 **[提升](/help/sites-administering/campaign-segmentation.md#boost-factor)** 还使用了因子。

>[!CAUTION]
>
>区段编辑器不检查任何循环引用。例如，区段 A 引用另一个区段 B，而后者又引用区段 A。您必须确保您的区段不包含任何循环引用。

>[!NOTE]
>
>具有以下特征的属性 **_i18n** 后缀由脚本设置，该脚本是个性化的UI clientlib的一部分。 所有与UI相关的clientlib仅加载到作者上，因为发布时不需要用户界面。
>
>因此，在创建具有此类属性的区段时，通常需要依赖 **browserFamily** 例如，而不是 **browserFamily_i18n**.

### 创建新区段 {#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在边栏中，选择 **“工具” > “操作” > “配置”**.
1. 单击 **分段** 页面，然后导航到所需的位置。
1. 创建 [新页面](/help/sites-authoring/editing-content.md#creatinganewpage) 使用 **区段** 模板。
1. 打开新页面以查看区段编辑器：

   ![在区段编辑器中创建区段的第一步](assets/screen_shot_2012-02-02at101726am.png)

1. 使用sidekick或上下文菜单(通常是单击鼠标右键，然后选择 **新建……** 打开“插入新组件”窗口)以查找所需的区段特征。 然后将其拖动到 **区段编辑器** 它将在默认状态下显示 **和** 容器。
1. 双击新特征以编辑特定参数；例如，鼠标位置：

   ![在区段编辑器中编辑组件](assets/screen_shot_2012-02-02at103135am.png)

1. 单击 **确定** 要保存定义，请执行以下操作：
1. 您可以 **编辑** 区段定义，用于为其 **标题**， **描述** 和 **[提升](#boost-factor)** 因子：

   ![在区段编辑器中编辑区段设置](assets/screen_shot_2012-02-02at103547am.png)

1. 如果需要，可添加更多特征。 您可以使用以下公式来制定布尔表达式： **AND容器** 和 **OR容器** 在以下位置找到组件： **区段逻辑**. 通过区段编辑器，您可以删除不再需要的特征或容器，或将它们拖到语句中的新位置。

### 使用 AND 和 OR 容器 {#using-and-and-or-containers}

您可以在AEM中构建复杂区段。 了解一些基本要点会有所帮助：

* 定义的顶级始终是最初创建的AND容器；此操作无法更改，但不会影响区段定义的其余部分。
* 确保容器的嵌套有意义。可以将容器视为布尔表达式的括号。

以下示例用于选择符合以下条件的访客：

男性和16至65岁

或

女性和16至62岁

由于主运算符为OR，因此您需要以 **OR容器**. 其中您有2个AND语句，对于每个语句，您需要 **AND容器**，可向其中添加单个特征。

![区段编辑器中的AND和OR运算符示例](assets/screen_shot_2012-02-02at105145am.png)

## 测试区段的应用程序 {#testing-the-application-of-a-segment}

定义区段后，可以借助 **[客户端上下文](/help/sites-administering/client-context.md)**：

1. 选择要测试的区段。
1. 按 **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** 以打开 **[客户端上下文](/help/sites-administering/client-context.md)**，其中显示了已收集的数据。 出于测试目的，您可以 **编辑** 某些值，或 **加载** 另一个配置文件以查看它的影响。

1. 根据定义的特征，当前页面的可用数据可能与区段定义匹配，也可能不匹配。 匹配状态显示在定义下方。

例如，简单的区段定义可以基于用户的年龄和性别。 加载特定配置文件会显示已成功解析该区段：

![使用“客户端上下文”窗口测试AND分段操作](assets/screen_shot_2012-02-02at105926am.png)

或者不是：

![使用Client Context窗口测试NOT分段操作](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>将立即解析所有特征，尽管大多数特征仅在页面重新加载时发生变化。对鼠标位置的更改会立即可见，因此可用于测试目的。

此类测试也可在内容页面上执行，并与 **Teaser** 组件。

将鼠标悬停在Teaser段落上将显示应用的区段，无论它们当前是否解析，因此也会显示选择当前Teaser实例的原因：

![区段鼠标悬停示例](assets/chlimage_1-47.png)

### 使用区段 {#using-your-segment}

区段当前使用范围 [营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). 它们用于控制特定目标受众看到的实际内容。 请参阅 [了解区段](/help/sites-authoring/segmentation-overview.md) 以了解更多信息。
