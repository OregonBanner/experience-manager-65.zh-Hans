---
title: 使用ContextHub配置分段
seo-title: 使用ContextHub配置分段
description: 了解如何使用ContextHub配置分段。
seo-description: 了解如何使用ContextHub配置分段。
uuid: 196cfb18-317c-443d-b6f1-f559e4221baa
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6cade87c-9ed5-47d7-9b39-c942268afdad
exl-id: 8bd6c88b-f36a-422f-ae6c-0d59f365079a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 2%

---

# 使用ContextHub{#configuring-segmentation-with-contexthub}配置分段

>[!NOTE]
>
>本节介绍如何在使用ContextHub时配置分段。 如果您使用的是Client Context功能，请参阅有关[为Client Context配置分段的相关文档](/help/sites-administering/campaign-segmentation.md)。


分段是创建营销活动时的主要考虑事项。请参阅[管理受众](/help/sites-authoring/managing-audiences.md) ，以了解有关分段工作方式和关键术语的信息。

根据您已收集的有关网站访客的信息以及要实现的目标，您需要定义目标内容所需的区段和策略。

然后，这些区段用于向访客提供具体目标内容。 此内容在网站的[Personalization](/help/sites-authoring/personalization.md)部分中进行维护。 [](/help/sites-authoring/activitylib.md) 此处定义的活动可以包含在任何页面上，并定义专用内容适用的访客区段。

AEM使您能够轻松地个性化用户体验。 它还允许您验证区段定义的结果。

## 访问区段{#accessing-segments}

[受众](/help/sites-authoring/managing-audiences.md)控制台用于管理ContextHub或Client Context的区段，以及您的Adobe Target帐户的受众。 本文档介绍如何管理ContextHub的区段。 对于[Client Context区段](/help/sites-administering/campaign-segmentation.md)和Adobe Target区段，请参阅相关文档。

要访问您的区段，请在全局导航中选择&#x200B;**导航>个性化>受众**。

![chlimage_1-311](assets/chlimage_1-310.png)

## 区段编辑器 {#segment-editor}

使用&#x200B;**区段编辑器**&#x200B;可轻松修改区段。 要编辑区段，请在[区段列表](/help/sites-administering/segmentation.md#accessing-segments)中选择一个区段，然后单击&#x200B;**编辑**&#x200B;按钮。

![segmenteditor](assets/segmenteditor.png)

使用组件浏览器，您可以添加&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器以定义区段逻辑，然后添加其他组件以比较属性和值，或引用脚本和其他区段以定义选择标准（请参阅[创建新区段](#creating-a-new-segment)）以定义选择区段的确切方案。

当整个语句的计算结果为true时，区段即已解析。 如果有多个区段适用，则还会使用&#x200B;**提升**&#x200B;因子。 有关[提升因子的详细信息，请参阅[创建新区段](#creating-a-new-segment)。](/help/sites-administering/campaign-segmentation.md#boost-factor)

>[!CAUTION]
>
>区段编辑器不检查是否有任何循环引用。 例如，区段A引用了另一个区段B，而这反过来又引用了区段A。您必须确保区段不包含任何循环引用。

### 容器 {#containers}

以下容器现成可用，允许您将比较和引用分组在一起进行布尔值评估。 可将组件从组件浏览器拖至编辑器。 有关更多信息，请参阅以下章节[使用AND和OR容器](/help/sites-administering/segmentation.md#using-and-and-or-containers)。

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

以下区段比较功能现成可用，可用于评估区段属性。 可将组件从组件浏览器拖至编辑器。

<table>
 <tbody>
  <tr>
   <td>Property-Value<br /> </td>
   <td>将存储的属性与定义的值<br />进行比较 </td>
  </tr>
  <tr>
   <td>Property-Property</td>
   <td>将存储的一个属性与另一个属性<br />进行比较 </td>
  </tr>
  <tr>
   <td>属性区段引用</td>
   <td>将存储的属性与另一个引用区段进行比较<br /> </td>
  </tr>
  <tr>
   <td>属性脚本引用</td>
   <td>将存储的属性与脚本的结果<br />进行比较 </td>
  </tr>
  <tr>
   <td>区段引用脚本参考</td>
   <td>将引用的区段与脚本的结果进行比较<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在比较值时，如果未设置比较的数据类型（即设置为自动检测），则ContextHub的分段引擎将只比较Javascript所示的值。 它不会将值转换为其预期类型，这可能会导致误导性结果。 例如：
>
>`null < 30 // will return true`
>
>因此，在[创建区段](/help/sites-administering/segmentation.md#creating-a-new-segment)时，只要已知比较值的类型，您就应选择&#x200B;**数据类型**。 例如：
>
>在比较属性`profile/age`时，您已经知道比较类型将为&#x200B;**number**，因此即使未设置`profile/age`，小于30的比较`profile/age`也将返回&#x200B;**false**，这与您预期的相同。

### 引用 {#references}

以下引用现成可用，可直接链接到脚本或其他区段。 可将组件从组件浏览器拖至编辑器。

<table>
 <tbody>
  <tr>
   <td>段引用<br /> </td>
   <td>评估引用的区段</td>
  </tr>
  <tr>
   <td>脚本引用</td>
   <td>评估引用的脚本。 有关更多信息，请参阅以下章节<a href="/help/sites-administering/segmentation.md#using-script-references">使用脚本引用</a>。</td>
  </tr>
 </tbody>
</table>

## 创建新区段{#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在[访问区段](/help/sites-administering/segmentation.md#accessing-segments)后， [导航到要创建区段的文件夹](#organizing-segments)，或将其保留在根目录中。

1. 单击或点按创建按钮，然后选择&#x200B;**创建ContextHub区段**。

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. 在&#x200B;**New ContextHub Segment**&#x200B;中，根据需要输入区段的标题和提升值，然后点按或单击&#x200B;**创建**。

   ![chlimage_1-312](assets/chlimage_1-312.png)

   每个区段都有一个提升参数，用作加权因子。 数值越大，表示将优先选择该区段，以在多个区段有效的情况下选择数量较低的区段。

   * 最小值：`0`
   * 最大值：`1000000`

1. 将比较或引用拖到区段编辑器中，该编辑器将显示在默认的AND容器中。
1. 双击或点按新引用或区段的配置选项，以编辑特定参数。 在此示例中，我们正在测试圣何塞的人员。

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   如果可能，请始终设置&#x200B;**数据类型**，以确保正确评估比较。 有关更多信息，请参阅[比较](/help/sites-administering/segmentation.md#comparisons)。

1. 单击&#x200B;**OK**&#x200B;以保存您的定义：
1. 根据需要添加更多组件。您可以使用容器组件来构建布尔表达式，以用于“与”和“或”比较（请参阅下面的[使用AND和Or Containers](/help/sites-administering/segmentation.md#using-and-and-or-containers)）。 使用区段编辑器，您可以删除不再需要的组件，或将它们拖动到语句中的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

使用AND和OR容器组件，您可以在AEM中构建复杂的区段。 执行此操作时，了解一些基本要点：

* 定义的顶级始终是最初创建的AND容器。 无法更改，但对区段定义的其余部分没有影响。
* 确保对容器进行嵌套是合理的。 容器可以作为布尔表达式的括号查看。

以下示例用于选择在我们的主要年龄组中被视为的访客：

男，30至59岁

或者

女性，30至59岁

首先，在默认的AND容器中放置OR容器组件。 在OR容器内，添加两个AND容器，并在这两个容器内都可以添加属性或引用组件。

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### 使用脚本引用{#using-script-references}

通过使用脚本引用组件，可以将区段属性的评估委派给外部脚本。 正确配置脚本后，即可将其用作区段条件的任何其他组件。

#### 定义要引用的脚本{#defining-a-script-to-reference}

1. 将文件添加到`contexthub.segment-engine.scripts` clientlib。
1. 实施返回值的函数。 例如：

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

1. 使用`ContextHub.SegmentEngine.ScriptManager.register`注册脚本。

如果脚本依赖于其他属性，则脚本应调用`this.dependOn()`。 例如，如果脚本依赖于`profile/age`:

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用脚本{#referencing-a-script}

1. 创建ContextHub区段。
1. 将&#x200B;**脚本引用**&#x200B;组件添加到区段的所需位置。
1. 打开&#x200B;**脚本引用**&#x200B;组件的编辑对话框。 如果[正确配置了](/help/sites-administering/segmentation.md#defining-a-script-to-reference)，则该脚本应在&#x200B;**脚本名称**&#x200B;下拉列表中可用。

## 组织区段{#organizing-segments}

如果您有多个区段，它们可能会变得难以作为平面列表进行管理。 在这种情况下，创建文件夹以管理区段会非常有用。

### 创建新文件夹{#create-folder}

1. 在[访问区段](#accessing-segments)后，单击或点按&#x200B;**创建**&#x200B;按钮，然后选择&#x200B;**文件夹**。

   ![添加文件夹](assets/contexthub-create-segment.png)

1. 为文件夹提供&#x200B;**标题**&#x200B;和&#x200B;**名称**。
   * **Title**&#x200B;应该是描述性的。
   * **Name**&#x200B;将成为存储库中的节点名称。
      * 它将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/sites-developing/naming-conventions.md)
      * 如有必要，可进行调整。

   ![创建文件夹](assets/contexthub-create-folder.png)

1. 点按或单击&#x200B;**创建**。

   ![确认文件夹](assets/contexthub-confirm-folder.png)

1. 文件夹将显示在区段列表中。
   * 对列的排序方式将影响新文件夹在列表中显示的位置。
   * 您可以点按或单击列标题以调整排序。
      ![新文件夹](assets/contexthub-folder.png)

### 修改现有文件夹{#modify-folders}

1. 在[访问区段](#accessing-segments)后，单击或点按要修改的文件夹以将其选中。

   ![选择文件夹](assets/contexthub-select-folder.png)

1. 点按或单击工具栏中的&#x200B;**重命名**&#x200B;以重命名文件夹。

1. 提供新的&#x200B;**文件夹标题** ，然后点按或单击&#x200B;**保存**。

   ![重命名文件夹](assets/contexthub-rename-folder.png)

>[!NOTE]
>
>重命名文件夹时，只能更改标题。 名称无法更改。

### 删除文件夹

1. 在[访问区段](#accessing-segments)后，单击或点按要修改的文件夹以将其选中。

   ![选择文件夹](assets/contexthub-select-folder.png)

1. 点按或单击工具栏中的&#x200B;**删除**&#x200B;以删除文件夹。

1. 出现一个对话框，其中显示了选定要删除的文件夹的列表。

   ![确认删除](assets/contexthub-confirm-segment-delete.png)

   * 点按或单击&#x200B;**Delete**&#x200B;以确认。
   * 点按或单击&#x200B;**取消**&#x200B;以中止操作。

1. 如果任何选定的文件夹包含子文件夹或区段，则必须确认删除这些文件夹或区段。

   ![确认删除子项](assets/contexthub-confirm-segment-child-delete.png)

   * 点按或单击&#x200B;**强制删除**&#x200B;以进行确认。
   * 点按或单击&#x200B;**取消**&#x200B;以中止操作。

>[!NOTE]
>
> 无法将区段从一个文件夹移动到另一个文件夹。

## 测试区段{#testing-the-application-of-a-segment}的应用

定义区段后，可借助&#x200B;**[ContextHub](/help/sites-authoring/ch-previewing.md)测试潜在结果。**

1. 预览页面
1. 单击ContextHub图标以显示ContextHub工具栏
1. 选择与您创建的区段匹配的角色
1. ContextHub将解析选定角色的适用区段

例如，我们用于识别主要年龄组中用户的简单区段定义是一个基于用户年龄和性别的简单区段定义。 加载与这些条件匹配的特定角色时，会显示区段是否成功解析：

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

或者，如果它未得到解决：

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征仅在重新加载页面时发生更改。

此类测试还可以在内容页面上结合目标内容和相关的&#x200B;**活动**&#x200B;和&#x200B;**体验**&#x200B;执行。

如果您已使用上述主要年龄组区段示例设置了活动和体验，则可以使用该活动轻松测试区段。 有关设置活动的详细信息，请参阅有关创作目标内容的相关[文档](/help/sites-authoring/content-targeting-touch.md)。

1. 在已设置目标内容的页面的编辑模式下，您可以通过内容上的箭头图标来查看该内容是否已定位。

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. 切换到预览模式并使用ContextHub，切换到与为体验配置的分段不匹配的人物。

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. 切换到与为体验配置的区段匹配的角色，并查看体验是否会相应地发生更改。

   ![chlimage_1-315](assets/chlimage_1-315.png)

## 使用区段{#using-your-segment}

区段用于控制特定目标受众看到的实际内容。 请参阅[管理受众](/help/sites-authoring/managing-audiences.md) ，以了解有关受众和区段的更多信息，以及有关使用受众和区段定位内容的[创作目标内容](/help/sites-authoring/content-targeting-touch.md)信息。
