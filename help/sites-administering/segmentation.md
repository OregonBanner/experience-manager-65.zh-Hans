---
title: 使用ContextHub配置分段
seo-title: 使用ContextHub配置分段
description: 了解如何使用Context Hub配置分段。
seo-description: 了解如何使用Context Hub配置分段。
uuid: 196cfb18-317c-443d-b6f1-f559e4221baa
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6cade87c-9ed5-47d7-9b39-c942268afdad
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 使用ContextHub配置分段{#configuring-segmentation-with-contexthub}

>[!NOTE]
>
>本节介绍在使用ContextHub时配置分段。 如果您使用Client Context功能，请参阅相关文档以配 [置Client context的分段](/help/sites-administering/campaign-segmentation.md)。


分段是创建营销活动时的主要考虑事项。有关细 [分工作方式和关键术语的信息](/help/sites-authoring/managing-audiences.md) ，请参阅管理受众。

根据您已收集的有关网站访客的信息以及要实现的目标，您需要为目标内容定义所需的细分和策略。

然后，这些区段用于为访客提供特定目标内容。 此内容在网站的“个 [性化](/help/sites-authoring/personalization.md) ”部分进行维护。 [此处定义的](/help/sites-authoring/activitylib.md) “活动”可包含在任何页面上，并定义特定内容适用的访客区段。

AEM使您能够轻松个性化用户体验。 它还允许您验证区段定义的结果。

## 访问区段 {#accessing-segments}

“ [受众](/help/sites-authoring/managing-audiences.md) ”控制台用于管理ContextHub或Client context的区段以及Adobe Target帐户的受众。 本文档涵盖管理ContextHub的区段。 有关 [Client Context区段](/help/sites-administering/campaign-segmentation.md) 和Adobe Target区段，请参阅相关文档。

要访问您的区段，请在全局导航中选择 **导航>个性化>受众**。

![chlimage_1-310](assets/chlimage_1-310.png)

## 区段编辑器 {#segment-editor}

区段 **编辑器** ，可让您轻松修改区段。 要编辑区段，请在区段列表中选择 [区段](/help/sites-administering/segmentation.md#accessing-segments) ，然后单击 **编辑按钮** 。

![segmenteditor](assets/segmenteditor.png)

使用组件浏览器，您可以添加 **AND** 和 **OR** 容器来定义区段逻辑，然后添加其他组件来比较属性和值，或引用脚本和其他区段来定义选择条件(请参阅创建新区段 [](#creating-a-new-segment))以定义选择区段的精确方案。

当整个语句的计算结果为true时，段即已解析。 如果有多个区段适用，则还会 **使用提** 升因子。 有关 [提升因子的详细信息](#creating-a-new-segment) ，请参阅创建 [新区段。](/help/sites-administering/campaign-segmentation.md#boost-factor)

>[!CAUTION]
>
>区段编辑器不检查任何循环引用。 例如，区段A引用另一个区段B，而该区段B又引用区段A。您必须确保您的区段不包含任何循环引用。

### 容器 {#containers}

以下容器现成可用，允许您将比较和引用分组在一起以进行布尔评估。 可将组件从组件浏览器拖动到编辑器中。 有关详细信息，请 [参阅以下使用AND和OR容器](/help/sites-administering/segmentation.md#using-and-and-or-containers) 。

<table>
 <tbody>
  <tr>
   <td>容器 AND<br /> </td>
   <td>布尔AND运算符<br /> </td>
  </tr>
  <tr>
   <td>容器 OR<br /> </td>
   <td>布尔OR运算符</td>
  </tr>
 </tbody>
</table>

### 比较 {#comparisons}

可开箱即用地比较以下区段属性。 可将组件从组件浏览器拖动到编辑器中。

<table>
 <tbody>
  <tr>
   <td>属性值<br /> </td>
   <td>将存储的属性与定义的值进行比较<br /> </td>
  </tr>
  <tr>
   <td>属性——属性</td>
   <td>将存储的一个属性与另一个属性进行比较<br /> </td>
  </tr>
  <tr>
   <td>属性段引用</td>
   <td>将商店的属性与另一个引用的区段进行比较<br /> </td>
  </tr>
  <tr>
   <td>属性脚本参考</td>
   <td>将存储的属性与脚本的结果进行比较<br /> </td>
  </tr>
  <tr>
   <td>段参考脚本参考</td>
   <td>将引用的段与脚本的结果进行比较<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在比较值时，如果未设置比较的数据类型（即设置为自动检测）,ContextHub的分段引擎将只比较javascript的值。 它不会将值转换为其预期类型，这会导致误导性结果。 例如：
>
>`null < 30 // will return true`
>
>因此，在 [创建区段时](/help/sites-administering/segmentation.md#creating-a-new-segment)，应当在已知 **比较值类型时选择数据类型** 。 例如：
>
>在比较属性时， `profile/age`您已经知道比较的类型将是 **number**，因此即使未设置，小于30的比较也会返回 `profile/age` false `profile/age`****，如您所期望的。

### 引用 {#references}

以下参考功能现成可用，可直接链接到脚本或其他段。 可将组件从组件浏览器拖动到编辑器中。

<table>
 <tbody>
  <tr>
   <td>段引用<br /> </td>
   <td>评估引用的区段</td>
  </tr>
  <tr>
   <td>脚本引用</td>
   <td>评估引用的脚本。 有关详细信息，请参 <a href="/help/sites-administering/segmentation.md#using-script-references">阅以下使用脚本引</a> 用一节。</td>
  </tr>
 </tbody>
</table>

## 创建新区段 {#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 访问 [区段后](/help/sites-administering/segmentation.md#accessing-segments)，单击或点按创建按钮，然后选择 **创建ContextHub区段**。

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. 在“新 **ContextHub区段**”中，根据需要输入区段的标题和提升值，然后点按或单击创 **建**。

   ![chlimage_1-312](assets/chlimage_1-312.png)

   每个区段都有一个提升参数，用作加权因子。 较高的数字表示在多个区段有效的情况下，将优先选择该区段，而选择的区段数量较低。

   * Minimum value: `0`
   * Maximum value: `1000000`

1. 将比较或引用拖动到区段编辑器中，它将显示在默认的AND容器中。
1. 双击或点按新引用或区段的配置选项以编辑特定参数。 在此示例中，我们将测试圣何塞的人员。

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   请尽可能设 **置数据类型** ，以确保正确评估比较。 有关更 [多信息](/help/sites-administering/segmentation.md#comparisons) ，请参阅比较。

1. Click **OK** to save your definition:
1. 根据需要添加更多组件。您可以使用容器组件为AND和OR比较表达布尔表达式(请参阅 [使用下面的AND和Or容器](/help/sites-administering/segmentation.md#using-and-and-or-containers) )。 使用区段编辑器，您可以删除不再需要的组件，或将它们拖动到语句中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

使用AND和OR容器组件，您可以在AEM中构建复杂的区段。 在执行此操作时，请注意以下几个基本要点：

* 定义的顶级始终是最初创建的AND容器。 无法更改，但对您的其余区段定义没有影响。
* 确保容器的嵌套是合理的。 容器可以作为布尔表达式的括号查看。

以下示例用于选择在我们的黄金年龄组中被视为访客的访客：

男，30岁到59岁

或者

30岁至59岁的女性

首先，将OR容器组件放入默认的AND容器中。 在OR容器中，可添加两个AND容器，在这两个容器中，可以添加属性或引用组件。

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### 使用脚本引用 {#using-script-references}

通过使用“脚本参考”组件，可以将区段属性的评估委派给外部脚本。 正确配置脚本后，它便可用作段条件的任何其他组件。

#### 定义要引用的脚本 {#defining-a-script-to-reference}

1. 将文件添加到 `contexthub.segment-engine.scripts` clientlib。
1. 实现返回值的函数。 例如：

   ```
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. 注册脚本 `ContextHub.SegmentEngine.ScriptManager.register`。

如果脚本取决于其他属性，则脚本应调用 `this.dependOn()`。 例如，如果脚本取决于 `profile/age`:

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用脚本 {#referencing-a-script}

1. 创建ContextHub区段。
1. 在 **段的所需位置添加** “脚本参考”组件。
1. 打开“脚本参考”组件的 **编辑对话框** 。 如 [果正确配置](/help/sites-administering/segmentation.md#defining-a-script-to-reference)，则脚本应在“脚本名 **称** ”下拉框中可用。

## 测试区段的应用 {#testing-the-application-of-a-segment}

定义区段后，可以借助 **[ContextHub测试潜在结果](/help/sites-authoring/ch-previewing.md)。**

1. 预览页面
1. 单击ContextHub图标以显示ContextHub工具栏
1. 选择与您创建的区段匹配的角色
1. ContextHub将解析所选角色的适用区段

例如，我们为识别黄金年龄组中的用户而做出的简单细分定义是基于用户年龄和性别的简单细分定义。 加载符合这些条件的特定人物会显示区段是否成功解析：

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

或者，如果它未解决：

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数情况只会在页面重新加载时发生更改。

此类测试还可以在内容页面上执行，并结合目标内容以及相关的活 **动** 和 **体验**。

如果您使用上述主要年龄组区段示例设置了活动和体验，则可以使用活动轻松测试区段。 有关设置活动的详细信息，请参阅有关创作目 [标内容的相关文档](/help/sites-authoring/content-targeting-touch.md)。

1. 在已设置目标内容的页面的编辑模式下，您可以通过内容上的箭头图标来查看该内容是目标的。

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. 切换到预览模式并使用Context Hub，切换到与为体验配置的细分不匹配的人物。

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. 切换到与为体验配置的细分匹配的角色，并查看体验是否会相应发生变化。

   ![chlimage_1-315](assets/chlimage_1-315.png)

## 使用您的细分 {#using-your-segment}

区段用于控制特定目标受众看到的实际内容。 有关受 [众和区段的更多信息](/help/sites-authoring/managing-audiences.md) ，请参阅管理受众，以及创作有关使 [用受众和区段定位内容的目标内容](/help/sites-authoring/content-targeting-touch.md) 。
