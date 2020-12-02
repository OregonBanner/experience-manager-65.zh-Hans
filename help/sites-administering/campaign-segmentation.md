---
title: 配置分段
seo-title: 配置分段
description: 了解如何为AEM活动配置分段。
seo-description: 了解如何为AEM活动配置分段。
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---


# 配置分段{#configuring-segmentation}

>[!NOTE]
>
>此文档涵盖与Client Context一起使用的分段配置。 要使用触屏UI配置ContextHub的区段，请参阅[使用ContextHub配置分段](/help/sites-administering/segmentation.md)。

分段是创建营销活动时的主要考虑事项。有关分段工作方式和关键术语的信息，请参见[分段术语表](/help/sites-authoring/segmentation-overview.md)。

根据您已收集的有关网站访客和您要实现的目标的信息，您需要定义目标内容所需的细分和策略。

然后，这些区段用于为访客提供具体目标内容。 此内容将保留在网站的[活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)部分。 此处定义的Teaser页面可以作为Teaser段落包含在任何页面上，并定义专用内容适用的访客段。

AEM允许您轻松创建和更新区段、Teaser和活动。 它还允许您验证定义的结果。

**段编辑器**&#x200B;允许您轻松定义段：

![](assets/segmenteditor.png)

您可以&#x200B;**编辑**&#x200B;每个段以指定&#x200B;**标题**、**说明**&#x200B;和&#x200B;**提升**&#x200B;因子。 使用Sidekick，您可以添加&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器来定义&#x200B;**区段逻辑**，然后添加所需的&#x200B;**区段特征**&#x200B;来定义选择条件。

## 提升因子 {#boost-factor}

每个区段都有一个&#x200B;**Boost**&#x200B;参数，用作加权因子；数字越大，表示将优先选择数字越小的区段。

* 最小值：`0`
* 最大值：`1000000`

## 区段逻辑{#segment-logic}

以下逻辑容器现成可用，允许您构建区段选择的逻辑。 可以将它们从Sidekick拖动到编辑器中：

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

以下细分特征现成可用；可以将它们从Sidekick拖动到编辑器：

<table>
 <tbody>
  <tr>
   <td> IP 范围<br /> </td>
   <td>定义访客可以具有的IP地址范围。<br /> </td>
  </tr>
  <tr>
   <td> 页面点击<br /> </td>
   <td>请求页面的频率。<br /> </td>
  </tr>
  <tr>
   <td> 页面属性<br /> </td>
   <td>已访问页面的任何属性。<br /> </td>
  </tr>
  <tr>
   <td> 引用关键字<br /> </td>
   <td>要与引用网站中的信息匹配的关键字。<br /> </td>
  </tr>
  <tr>
   <td> 脚本</td>
   <td>要评估的Javascript表达式。<br /> </td>
  </tr>
  <tr>
   <td> 段引用 <br /> </td>
   <td>对另一个段定义的引用。<br /> </td>
  </tr>
  <tr>
   <td> 标记云<br /> </td>
   <td>要与访问页面中的标记相匹配的标记。<br /> </td>
  </tr>
  <tr>
   <td> 用户年龄<br /> </td>
   <td>取自用户用户档案。<br /> </td>
  </tr>
  <tr>
   <td> 用户属性<br /> </td>
   <td>用户用户档案中提供的任何其他信息。 </td>
  </tr>
 </tbody>
</table>

您可以使用布尔运算符OR和AND组合这些特征（请参阅[创建新区段](#creating-a-new-segment)）来定义选择此区段的确切方案。

当整个语句的计算结果为true时，此段已解析。 在多个段适用的事件中，还使用&#x200B;**[提升](/help/sites-administering/campaign-segmentation.md#boost-factor)**&#x200B;因子。

>[!CAUTION]
>
>段编辑器不检查任何循环引用。 例如，区段A引用了另一个区段B，这反过来又引用了区段A。您必须确保您的区段不包含任何循环引用。

>[!NOTE]
>
>具有&#x200B;**_i18n**&#x200B;后缀的属性由作为个性化UI clientlib的一部分的脚本设置。 只有作者才会加载所有与UI相关的客户端库，因为发布时不需要UI。
>
>因此，在创建具有此类属性的段时，通常需要依赖&#x200B;**browserFamily**，而不是&#x200B;**browserFamily_i18n**。

### 创建新区段{#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在边栏中，选择&#x200B;**工具>操作>配置**。
1. 单击左窗格中的&#x200B;**Segmentation**&#x200B;页面，然后导航到所需的位置。
1. 使用&#x200B;**区段**&#x200B;模板创建[新页面](/help/sites-authoring/editing-content.md#creatinganewpage)。
1. 打开新页面以查看区段编辑器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 使用Sidekick或上下文菜单(通常单击鼠标右键，然后选择&#x200B;**新建……**&#x200B;以打开“插入新组件”窗口)以查找所需的段特征。 然后将其拖动到&#x200B;**区段编辑器**&#x200B;中，它将显示在默认的&#x200B;**AND**&#x200B;容器中。
1. 多次单击新特征以编辑特定参数；例如，鼠标位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 单击&#x200B;**确定**&#x200B;以保存您的定义：
1. 您可以&#x200B;**编辑**&#x200B;区段定义，为其提供&#x200B;**标题**、**说明**&#x200B;和&#x200B;**[提升](#boost-factor)**&#x200B;因子：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 根据需要添加更多特征。 可以使用&#x200B;**段逻辑**&#x200B;下的&#x200B;**AND容器**&#x200B;和&#x200B;**OR容器**&#x200B;组件来构造布尔表达式。 利用区段编辑器，您可以删除不再需要的特征或容器，或将它们拖动到语句中的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

您可以在AEM中构建复杂的细分。 了解一些基本要点有所帮助：

* 定义的顶级始终是最初创建的AND容器;无法更改，但对区段定义的其余部分没有影响。
* 确保容器嵌套合理。 这些容器可以作为布尔表达式的括号进行查看。

以下示例用于选择以下访客:

男，16至65岁

或者

女性，16至62岁

由于主运算符为OR，您需要用&#x200B;**OR开始**。 在该语句中，您有2个AND语句，对于每个语句，您需要一个&#x200B;**AND容器**，您可以在其中添加个别特征。

![](assets/screen_shot_2012-02-02at105145am.png)

## 测试段{#testing-the-application-of-a-segment}的应用程序

定义区段后，可以借助&#x200B;**[Client Context](/help/sites-administering/client-context.md)**&#x200B;测试潜在结果：

1. 选择要测试的区段。
1. 按&#x200B;**[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**&#x200B;打开&#x200B;**[Client Context](/help/sites-administering/client-context.md)**，它显示已收集的数据。 为了进行测试，您可以&#x200B;**编辑**&#x200B;某些值，或&#x200B;**加载**&#x200B;其他用户档案，以了解影响。

1. 根据定义的特征，当前页面的可用数据可能与段定义匹配，也可能不匹配。 匹配状态显示在定义下方。

例如，简单的细分定义可以基于用户的年龄和性别。 加载特定用户档案表明区段已成功解析：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征只会在页面重新加载时发生更改。 对鼠标位置的更改会立即显示，因此对于测试非常有用。

此类测试还可以与&#x200B;**Teaser**&#x200B;组件一起在内容页面上执行。

将鼠标悬停在Teaser段落上将显示所应用的段，它们当前是否解析，因此，选择当前Teaser实例的原因：

![](assets/chlimage_1-47.png)

### 使用您的区段{#using-your-segment}

当前在[活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中使用区段。 它们用于控制特定目标受众看到的实际内容。 有关详细信息，请参阅[了解区段](/help/sites-authoring/segmentation-overview.md)。
