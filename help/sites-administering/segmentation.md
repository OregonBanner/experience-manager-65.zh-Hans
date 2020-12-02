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
source-git-commit: e5e00cc181c2dc3a28e25beb52f9a4c459ee313a
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 2%

---


# 使用ContextHub{#configuring-segmentation-with-contexthub}配置分段

>[!NOTE]
>
>本节介绍在使用ContextHub时配置分段。 如果您使用Client Context功能，请参阅有关[为Client Context配置分段的相关文档](/help/sites-administering/campaign-segmentation.md)。


分段是创建营销活动时的主要考虑事项。有关分段的工作原理和关键术语的信息，请参见[管理受众](/help/sites-authoring/managing-audiences.md)。

根据您已收集的有关网站访客和您要实现的目标的信息，您需要定义目标内容所需的细分和策略。

然后，这些区段用于为访客提供具体目标内容。 此内容将保留在网站的[Personalization](/help/sites-authoring/personalization.md)部分。 [此处](/help/sites-authoring/activitylib.md) 定义的活动可以包含在任何页面上，并定义专用内容适用的访客段。

AEM允许您轻松个性化用户体验。 它还允许您验证区段定义的结果。

## 访问区段{#accessing-segments}

[受众](/help/sites-authoring/managing-audiences.md)控制台用于管理ContextHub或Client Context的受众以及您的Adobe Target帐户的数据。 本文档涵盖管理ContextHub的区段。 对于[Client Context区段](/help/sites-administering/campaign-segmentation.md)和Adobe Target区段，请参阅相关文档。

要访问您的区段，请在全局导航中选择&#x200B;**导航>个性化>受众**。

![chlimage_1-311](assets/chlimage_1-310.png)

## 区段编辑器 {#segment-editor}

**段编辑器**&#x200B;允许您轻松修改段。 要编辑段，请在段[列表中选择段](/help/sites-administering/segmentation.md#accessing-segments)，然后单击&#x200B;**编辑**&#x200B;按钮。

![塞门特迪托](assets/segmenteditor.png)

使用组件浏览器，您可以添加&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器来定义段逻辑，然后添加其他组件来比较属性和值或引用脚本以及其他段来定义选择条件（请参阅[创建新段](#creating-a-new-segment)）来定义确切的选择段方案。

当整个语句的计算结果为true时，段即已解析。 在多个段适用的事件中，还使用&#x200B;**提升**&#x200B;因子。 有关[提升因子的详细信息，请参阅[创建新区段](#creating-a-new-segment)。](/help/sites-administering/campaign-segmentation.md#boost-factor)

>[!CAUTION]
>
>段编辑器不检查任何循环引用。 例如，区段A引用了另一个区段B，这反过来又引用了区段A。您必须确保您的区段不包含任何循环引用。

### 容器{#containers}

以下容器是现成的，允许您将比较和引用分组在一起进行布尔评估。 可以将组件浏览器拖动到编辑器中。 有关详细信息，请参见下一节[使用AND和OR容器](/help/sites-administering/segmentation.md#using-and-and-or-containers)。

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

### 比较{#comparisons}

现成可使用以下细分比较来评估细分属性。 可以将组件浏览器拖动到编辑器中。

<table>
 <tbody>
  <tr>
   <td>属性——值<br /> </td>
   <td>将存储的属性与定义的值<br />进行比较 </td>
  </tr>
  <tr>
   <td>属性——属性</td>
   <td>将存储的一个属性与另一个属性<br />进行比较 </td>
  </tr>
  <tr>
   <td>属性段引用</td>
   <td>将存储的属性与另一个引用的区段<br />进行比较 </td>
  </tr>
  <tr>
   <td>属性——脚本参考</td>
   <td>将存储的属性与脚本的结果进行比较<br /> </td>
  </tr>
  <tr>
   <td>段引用脚本参考</td>
   <td>将引用的段与脚本的结果进行比较<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在比较值时，如果未设置比较的数据类型（即设置为自动检测）,ContextHub的分段引擎将简单地将值与javascript进行比较。 它不会将值转换为其预期类型，这会导致误导性结果。 例如：
>
>`null < 30 // will return true`
>
>因此，当[创建段](/help/sites-administering/segmentation.md#creating-a-new-segment)时，只要已知比较值的类型，您应选择&#x200B;**数据类型**。 例如：
>
>在比较属性`profile/age`时，您已经知道比较类型将为&#x200B;**number**，因此即使未设置`profile/age`，小于30的比较`profile/age`也会返回&#x200B;**false**。

### 引用 {#references}

以下参考功能现成可用，可直接链接到脚本或其他段。 可以将组件浏览器拖动到编辑器中。

<table>
 <tbody>
  <tr>
   <td>段引用<br /> </td>
   <td>评估引用的区段</td>
  </tr>
  <tr>
   <td>脚本引用</td>
   <td>评估引用的脚本。 有关详细信息，请参见下一节<a href="/help/sites-administering/segmentation.md#using-script-references">使用脚本引用</a>。</td>
  </tr>
 </tbody>
</table>

## 创建新区段{#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 在[访问区段](/help/sites-administering/segmentation.md#accessing-segments)后，[导航到要创建区段的文件夹](#organizing-segments)，或将其保留在根文件夹中。

1. 单击或点按创建按钮，然后选择&#x200B;**创建ContextHub区段**。

   ![chlimage_1-310](assets/chlimage_1-311.png)

1. 在&#x200B;**新建ContextHub区段**&#x200B;中，根据需要输入区段的标题和提升值，然后点按或单击&#x200B;**创建**。

   ![chlimage_1-312](assets/chlimage_1-312.png)

   每个区段都有一个提升参数，用作加权因子。 数值越大，表示在多个段有效的情况下，将优先选择数值越低的段。

   * 最小值：`0`
   * 最大值：`1000000`

1. 将比较或引用拖动到段编辑器，它将显示在默认的AND容器中。
1. 多次单击或点按新引用或区段的配置选项以编辑特定参数。 在此示例中，我们测试的是圣何塞的人员。

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   如果可能，请始终设置&#x200B;**数据类型**，以确保正确评估比较。 有关详细信息，请参阅[比较](/help/sites-administering/segmentation.md#comparisons)。

1. 单击&#x200B;**确定**&#x200B;以保存您的定义：
1. 根据需要添加更多组件。您可以使用AND和OR比较的容器组件来构造布尔表达式(请参阅下面的[使用AND和Or容器](/help/sites-administering/segmentation.md#using-and-and-or-containers))。 使用区段编辑器，您可以删除不再需要的组件，或将它们拖动到语句中的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

使用AND和OR容器组件，您可以在AEM中构建复杂的细分。 这样做时，了解一些基本要点会有所帮助：

* 定义的顶级始终是最初创建的AND容器。 无法更改，但对区段定义的其余部分没有影响。
* 确保容器嵌套合理。 这些容器可以作为布尔表达式的括号进行查看。

以下示例用于选择在我们的主要年龄组中被视为访客的人：

男，30至59岁

或者

女性，30至59岁

通过将OR容器组件放置到默认的AND容器中来开始。 在OR容器中，您可以添加两个AND容器，在这两个中，您可以添加属性或引用组件。

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### 使用脚本引用{#using-script-references}

通过使用“脚本引用”组件，可以将段属性的评估委派给外部脚本。 正确配置脚本后，该脚本便可用作段条件的任何其他组件。

#### 定义要引用的脚本{#defining-a-script-to-reference}

1. 将文件添加到`contexthub.segment-engine.scripts` clientlib。
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

1. 使用`ContextHub.SegmentEngine.ScriptManager.register`注册脚本。

如果脚本依赖于其他属性，则脚本应调用`this.dependOn()`。 例如，如果脚本依赖于`profile/age`:

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用脚本{#referencing-a-script}

1. 创建ContextHub区段。
1. 在段的所需位置添加&#x200B;**脚本引用**&#x200B;组件。
1. 打开&#x200B;**脚本引用**&#x200B;组件的编辑对话框。 如果[正确配置](/help/sites-administering/segmentation.md#defining-a-script-to-reference)，则脚本应在&#x200B;**脚本名称**&#x200B;下拉框中可用。

## 组织区段{#organizing-segments}

如果您有许多细分，它们将变得难以作为扁平列表进行管理。 在这种情况下，创建文件夹来管理您的区段非常有用。

### 新建文件夹{#create-folder}

1. 在[访问区段](#accessing-segments)后，单击或点按&#x200B;**创建**&#x200B;按钮并选择&#x200B;**文件夹**。

   ![添加文件夹](assets/contexthub-create-segment.png)

1. 为您的文件夹提供&#x200B;**标题**&#x200B;和&#x200B;**名称**。
   * **标题**&#x200B;应为描述性。
   * **名称**&#x200B;将成为存储库中的节点名称。
      * 它将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/sites-developing/naming-conventions.md)
      * 如有必要，可进行调整。

   ![创建文件夹](assets/contexthub-create-folder.png)

1. 点按或单击&#x200B;**创建**。

   ![确认文件夹](assets/contexthub-confirm-folder.png)

1. 该文件夹将显示在区段列表中。
   * 列的排序方式将影响新文件夹在列表中的显示位置。
   * 您可以点按或单击列标题以调整排序。
      ![新文件夹](assets/contexthub-folder.png)

### 修改现有文件夹{#modify-folders}

1. 在[访问区段](#accessing-segments)后，单击或点按要修改的文件夹以选择它。

   ![选择文件夹](assets/contexthub-select-folder.png)

1. 点按或单击工具栏中的&#x200B;**重命名**&#x200B;以重命名文件夹。

1. 提供新的&#x200B;**文件夹标题**，然后点按或单击&#x200B;**保存**。

   ![重命名文件夹](assets/contexthub-rename-folder.png)

>[!NOTE]
>
>重命名文件夹时，只能更改标题。 无法更改名称。

### 删除文件夹

1. 在[访问区段](#accessing-segments)后，单击或点按要修改的文件夹以选择它。

   ![选择文件夹](assets/contexthub-select-folder.png)

1. 点按或单击工具栏中的&#x200B;**删除**&#x200B;以删除文件夹。

1. 对话框显示一列表选定删除的文件夹。

   ![确认删除](assets/contexthub-confirm-segment-delete.png)

   * 点按或单击&#x200B;**删除**&#x200B;以进行确认。
   * 点按或单击&#x200B;**取消**&#x200B;以中止操作。

1. 如果任何选定的文件夹包含子文件夹或区段，则必须确认删除这些文件夹。

   ![确认删除子项](assets/contexthub-confirm-segment-child-delete.png)

   * 点按或单击&#x200B;**强制删除**&#x200B;进行确认。
   * 点按或单击&#x200B;**取消**&#x200B;以中止操作。

>[!NOTE]
>
> 无法将区段从一个文件夹移动到另一个文件夹。

## 测试段{#testing-the-application-of-a-segment}的应用程序

定义区段后，可以借助&#x200B;**[ContextHub](/help/sites-authoring/ch-previewing.md)测试潜在结果。**

1. 预览页面
1. 单击ContextHub图标以显示ContextHub工具栏
1. 选择与您创建的区段匹配的人物
1. ContextHub将解析所选角色的适用区段

例如，我们简单的细分定义，用于识别黄金年龄组的用户，它是一个简单的细分定义，它基于用户的年龄和性别。 加载符合这些条件的特定人物会显示区段是否成功解析：

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

或者，如果它未解决：

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征只会在页面重新加载时发生更改。

此类测试也可以在内容页面上执行，并结合目标内容和相关的&#x200B;**活动**&#x200B;和&#x200B;**体验**。

如果您已使用上面的主要年龄组区段示例设置活动和体验，则可以使用活动轻松测试您的区段。 有关设置活动的详细信息，请参阅有关创作目标内容的相关[文档](/help/sites-authoring/content-targeting-touch.md)。

1. 在已设置目标内容的页面的编辑模式下，可以通过内容上的箭头图标来查看内容是否为目标。

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. 切换到预览模式并使用Context Hub，切换到与为体验配置的分段不匹配的人物。

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. 切换到与为体验配置的细分相匹配的人物，并查看体验是否会相应发生更改。

   ![chlimage_1-315](assets/chlimage_1-315.png)

## 使用您的区段{#using-your-segment}

区段用于控制特定目标受众看到的实际内容。 有关受众和区段的详细信息，请参阅[管理受众](/help/sites-authoring/managing-audiences.md)，以及有关使用受众和区段来目标内容的[创作目标内容](/help/sites-authoring/content-targeting-touch.md)。
