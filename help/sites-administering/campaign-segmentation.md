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
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---

# 配置分段{#configuring-segmentation}

>[!NOTE]
>
>本文档介绍了与Client Context一起使用的分段配置。 要使用触屏UI配置ContextHub区段，请参阅[使用ContextHub配置分段](/help/sites-administering/segmentation.md)。

分段是创建营销活动时的主要考虑事项。有关分段工作方式和关键术语的信息，请参阅[分段术语表](/help/sites-authoring/segmentation-overview.md)。

根据您已收集的有关网站访客的信息以及要实现的目标，您需要定义目标内容所需的区段和策略。

然后，这些区段用于向访客提供具体目标内容。 此内容在网站的[Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)部分中进行维护。 此处定义的Teaser页面可以作为Teaser段落包含在任何页面上，并定义专用内容适用的访客区段。

AEM允许您轻松创建和更新区段、Teaser和营销活动。 它还允许您验证定义的结果。

使用&#x200B;**区段编辑器**&#x200B;可轻松定义区段：

![](assets/segmenteditor.png)

您可以&#x200B;**编辑**&#x200B;每个区段以指定&#x200B;**标题**、**描述**&#x200B;和&#x200B;**提升**&#x200B;因子。 使用Sidekick ，您可以添加&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器以定义&#x200B;**区段逻辑**，然后添加所需的&#x200B;**区段特征**&#x200B;以定义选择标准。

## 提升因子 {#boost-factor}

每个区段都有一个&#x200B;**Boost**&#x200B;参数，用作加权因子；数字越大，表示将优先选择具有较低数字的区段。

* 最小值：`0`
* 最大值：`1000000`

## 区段逻辑{#segment-logic}

以下逻辑容器现成可用，允许您构建区段选择的逻辑。 可以将它们从Sidekick拖到编辑器中：

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

## 区段特征{#segment-traits}

以下区段特征现成可用；可将它们从sidekick拖到编辑器中：

<table>
 <tbody>
  <tr>
   <td> IP 范围<br /> </td>
   <td>定义访客可以拥有的IP地址范围。<br /> </td>
  </tr>
  <tr>
   <td> 页面点击<br /> </td>
   <td>请求页面的频率。<br /> </td>
  </tr>
  <tr>
   <td> 页面属性<br /> </td>
   <td>访问页面的任何属性。<br /> </td>
  </tr>
  <tr>
   <td> 引用关键字<br /> </td>
   <td>与引荐网站中的信息匹配的关键词。<br /> </td>
  </tr>
  <tr>
   <td> 脚本</td>
   <td>要计算的Javascript表达式。<br /> </td>
  </tr>
  <tr>
   <td> 段引用 <br /> </td>
   <td>对另一个区段定义的引用。<br /> </td>
  </tr>
  <tr>
   <td> 标记云<br /> </td>
   <td>与访问页面中的标记匹配的标记。<br /> </td>
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

您可以使用布尔运算符OR和AND组合这些特征（请参阅[创建新区段](#creating-a-new-segment)）以定义选择此区段的确切方案。

当整个语句的计算结果为true时，此区段即已解析。 如果有多个区段适用，则还会使用&#x200B;**[提升](/help/sites-administering/campaign-segmentation.md#boost-factor)**&#x200B;因子。

>[!CAUTION]
>
>区段编辑器不检查是否有任何循环引用。 例如，区段A引用了另一个区段B，而这反过来又引用了区段A。您必须确保区段不包含任何循环引用。

>[!NOTE]
>
>具有&#x200B;**_i18n**&#x200B;后缀的属性由脚本设置，该脚本是个性化UI clientlib的一部分。 只有在发布时不需要UI，才会在作者上加载所有与UI相关的clientlib。
>
>因此，在创建具有此类属性的区段时，通常需要依赖&#x200B;**browserFamily**，而不是&#x200B;**browserFamily_i18n**。

### 创建新区段{#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在边栏中，选择&#x200B;**工具>操作>配置**。
1. 单击左窗格中的&#x200B;**Segmentation**&#x200B;页面，然后导航到所需的位置。
1. 使用&#x200B;**区段**&#x200B;模板创建[新页面](/help/sites-authoring/editing-content.md#creatinganewpage)。
1. 打开新页面以查看区段编辑器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 使用Sidekick或上下文菜单(通常单击鼠标右键，然后选择&#x200B;**新建……**&#x200B;打开“插入新组件”窗口)以查找所需的区段特征。 然后，将其拖动到&#x200B;**区段编辑器**&#x200B;中，该编辑器将显示在默认的&#x200B;**AND**&#x200B;容器中。
1. 双击新特征以编辑特定参数；例如，鼠标位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 单击&#x200B;**OK**&#x200B;以保存您的定义：
1. 您可以&#x200B;**编辑**&#x200B;区段定义，为其提供&#x200B;**标题**、**描述**&#x200B;和&#x200B;**[提升](#boost-factor)**&#x200B;因子：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 根据需要添加更多特征。 您可以使用&#x200B;**区段逻辑**&#x200B;下的&#x200B;**AND Container**&#x200B;和&#x200B;**OR Container**&#x200B;组件来构建布尔表达式。 利用区段编辑器，您可以删除不再需要的特征或容器，或将它们拖动到语句中的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

您可以在AEM中构建复杂区段。 了解以下几个基本要点：

* 定义的顶级始终是最初创建的AND容器；无法更改，但对区段定义的其余部分没有影响。
* 确保对容器进行嵌套是合理的。 容器可以作为布尔表达式的括号查看。

以下示例用于选择以下任一访客：

男，16至65岁

或者

女性，16至62岁

由于主运算符为OR，因此您需要从&#x200B;**OR Container**&#x200B;开始。 在此语句中，您有2个AND语句，对于每个语句，您都需要一个&#x200B;**AND Container**，可以在其中添加各个特征。

![](assets/screen_shot_2012-02-02at105145am.png)

## 测试区段{#testing-the-application-of-a-segment}的应用

定义区段后，可借助&#x200B;**[Client Context](/help/sites-administering/client-context.md)**&#x200B;测试潜在结果：

1. 选择要测试的区段。
1. 按&#x200B;**[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**&#x200B;以打开&#x200B;**[Client Context](/help/sites-administering/client-context.md)**，其中显示已收集的数据。 出于测试目的，您可以&#x200B;**编辑**&#x200B;某些值，或者&#x200B;**加载其他配置文件，以查看其影响。**

1. 根据定义的特征，当前页面可用的数据可能与区段定义匹配，也可能与区段定义不匹配。 匹配的状态显示在定义下方。

例如，简单的区段定义可以基于用户的年龄和性别。 加载特定用户档案会显示区段已成功解析：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征仅在重新加载页面时发生更改。 鼠标位置的更改会立即显示，因此可用于测试。

此类测试也可以在内容页面上与&#x200B;**Teaser**&#x200B;组件结合使用来执行。

Teaser段落上的鼠标悬停将显示已应用的区段，无论这些区段当前是否解析，以及选择当前Teaser实例的原因：

![](assets/chlimage_1-47.png)

### 使用区段{#using-your-segment}

当前在[促销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中使用区段。 它们用于控制特定目标受众看到的实际内容。 有关更多信息，请参阅[了解区段](/help/sites-authoring/segmentation-overview.md)。
