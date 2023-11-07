---
title: 配置 Live Copy 同步
seo-title: Configuring Live Copy Synchronization
description: 了解如何配置Live Copy同步。
seo-description: Learn about configuring Live Copy Synchronization.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
feature: Multi Site Manager
exl-id: ac24b8b4-b3ed-47fa-9a73-03f0c9e68ac8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2695'
ht-degree: 37%

---

# 配置 Live Copy 同步{#configuring-live-copy-synchronization}

执行以下任务可控制活动副本与其源内容同步的方式和时间。

* 确定现有转出配置是否符合您的要求，或者是否需要创建一个或多个转出配置。
* 指定要用于活动副本的转出配置。

## 已安装的自定义转出配置 {#installed-and-custom-rollout-configurations}

本部分提供有关已安装转出配置、其所使用的同步操作以及如何在需要时创建自定义配置的信息。

>[!CAUTION]
>
>更新或更改现成（已安装）转出配置是 **非** 推荐。 如果需要自定义实时操作，则应将其添加到自定义转出配置中。

### 转出触发器 {#rollout-triggers}

每个转出配置都使用一个可执行转出的转出触发器。转出配置可以使用以下触发器之一：

* **转出**：和 **转出** 命令用于blue print页，或者 **同步** 命令用于live copy页面。

* **修改**：修改源页面。

* **激活**：激活源页面。

* **停用**：停用源页面。

>[!NOTE]
>
>使用修改触发器可能会影响性能。请参阅 [MSM 最佳实践](/help/sites-administering/msm-best-practices.md#onmodify)以了解更多信息。

### 已安装的转出配置 {#installed-rollout-configurations}

下表列出了随AEM一起安装的转出配置。 该表包含每个转出配置的触发器和同步操作。如果安装的转出配置操作不符合您的要求，您可以 [创建转出配置](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>名称</th>
   <th>描述</th>
   <th>触发器</th>
   <th>同步操作<br /> <br /> 另请参阅 <a href="#installed-synchronization-actions">安装的同步操作</a></th>
  </tr>
  <tr>
   <td>标准转出配置</td>
   <td>标准转出配置，允许在触发转出时启动转出流程，并执行以下操作：创建、更新、删除内容和对子节点进行排序。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> referencesupdate<br /> 产品更新<br /> orderChildren</td>
  </tr>
  <tr>
   <td>在 Blueprint 激活时激活</td>
   <td>在发布源时发布Live Copy。</td>
   <td>激活</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>在 Blueprint 停用时停用</td>
   <td>在停用源时停用Live Copy。</td>
   <td>停用</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>修改时推送</td>
   <td><p>修改源时将内容推送到Live Copy。</p> <p>谨慎使用此转出配置，因为它使用“修改”触发器。</p> </td>
   <td>修改</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> referencesupdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>修改时推送（简略）</td>
   <td><p>修改Blueprint页面时将内容推送到Live Copy，而不更新引用（例如，对于浅层副本）。</p> <p>谨慎使用此转出配置，因为它使用“修改”触发器。</p> </td>
   <td>修改</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>提升发布内容</td>
   <td>用于提升发布页面的标准转出配置。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> referencesupdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>目录页面内容转出配置</td>
   <td>从目录 Blueprint 中应用页面模板。</td>
   <td>转出</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> referencesupdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>目录页面更新转出配置</td>
   <td>从目录Blueprint中应用目标属性。 必须在目录页面内容转出配置后运行。</td>
   <td>转出</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>DPS 发布转出配置</td>
   <td>DPS发布转出配置，允许在触发转出时启动转出过程，同时在初始转出时排除FolioProducer绑定属性</td>
   <td>转出</td>
   <td>contentupdate<br /> contentCopy<br /> contentDelete<br /> referencesupdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>旧版(5.6.0)目录转出配置</td>
   <td>已弃用。请使用 Catalog Generator 代替 MSM 进行目录转出。</td>
   <td>转出</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### 安装的同步操作 {#installed-synchronization-actions}

下表列出了随AEM一起安装的同步操作。 如果安装的操作不符合您的要求，您可以 [创建新的同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>操作名称</th>
   <th>描述</th>
   <th>属性<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>当源节点在Live Copy上不存在时，会将节点复制到Live Copy。 <a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM内容复制操作服务</a> 指定要排除的节点类型、段落项和页面属性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>删除源上不存在的Live Copy节点。 <a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 内容删除操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentupdate</td>
   <td>使用来自源的更改来更新Live Copy内容。 <a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM内容更新操作服务</a> 指定要排除的节点类型、段落项和页面属性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>编辑Live Copy的属性 editMap属性确定编辑哪些属性及其值。 editMap属性的值必须使用以下格式：</p> <p><code>[property_name_1]#[current_value]#</code>[new_value]，<br /> <code>[property_name_2]#[current_value]#</code>[new_value]，<br /> ... ，<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>此 <code>current_value</code> 和 <code>new_value</code> 项是正则表达式。 <br /> </p> <p>例如，请为editMap考虑以下值：</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage，<br /> cq：template#/contentpage#/mobilecontentpage</p> <p>此值编辑Live Copy节点的属性，如下所示：</p>
    <ul>
     <li>此 <code>sling:resourceType</code> 属性设置为 <code>contentpage</code> 或 <code>homepage</code> 设置为 <code>mobilecontentpage.</code></li>
     <li>此 <code>cq:template</code> 属性设置为 <code>contentpage</code> 设置为 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap： （字符串）标识属性、当前值和新值。 有关信息，请参阅描述。<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>发送已转出的页面的页面事件。 要接收通知，首先需要订阅转出事件。</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>在Live Copy上，它会根据Blueprint上的顺序对子项（节点）进行排序<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesupdate</td>
   <td><p>在Live Copy上，此同步操作会更新引用，例如链接。<br /> 它会搜索Live Copy页面中指向Blueprint内资源的路径。 找到后，它会更新路径以指向Live Copy中的相关资源（而不是Blueprint）。 具有 Blueprint 外部目标的引用不会发生更改。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 引用更新操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>创建Live Copy的版本。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>激活Live Copy。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>停用Live Copy。</p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流</td>
   <td><p>启动由Target属性定义的工作流（仅适用于页面），并将Live Copy作为有效负载。</p> <p>目标路径是模型节点的路径。</p> </td>
   <td>target： （字符串）工作流模型的路径。<br /> </td>
  </tr>
  <tr>
   <td>必需</td>
   <td><p>将Live Copy页面上多个ACL的权限设置为对特定用户组的只读。 已配置以下ACL：</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>仅对页面使用此操作。</p> </td>
   <td>target： （字符串）要为其设置权限的组的ID。 <br /> </td>
  </tr>
  <tr>
   <td>必选内容</td>
   <td><p>将Live Copy页面上多个ACL的权限设置为对特定用户组的只读。 已配置以下ACL：</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>仅对页面使用此操作。</p> </td>
   <td>target： （字符串）要为其设置权限的组的ID。 </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>将Live Copy页面上ActionSet.ACTION_NAME_REMOVE ACL的权限设置为特定用户组的只读。 仅对页面使用此操作。</td>
   <td>target： （字符串）要为其设置权限的组的ID。 </td>
  </tr>
  <tr>
   <td>VersionCopyaction</td>
   <td>如果已至少发布过一次Blueprint/源页面，则使用发布的版本创建Live Copy页面。 注意：此操作仅适用于基于已发布的源页面创建Live Copy页面，而不能用于更新现有Live Copy页面。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>当页面在Blueprint中移动时将应用PageMoveAction。</p> <p>该操作会将（相关的）LiveCopy页面从移动前的位置复制到移动后的位置，而不是移动页面。</p> <p>PageMoveAction不会更改位于移动前位置的LiveCopy页面。 因此，对于连续RolloutConfigurations，它具有不带Blueprint的LiveRelationship状态。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置 CQ MSM 页面移动操作服务</a>，以指定要排除的节点类型、段落项和页面属性。 </p> <p>此操作必须是转出配置中包含的唯一同步操作。</p> </td>
   <td><p>prop_referenceUpdate： （布尔值）设置为true可更新引用。 默认值为true。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>创建或更新目录中的产品资源。 此操作用于以下情况之一：
    <ul>
     <li>生成或转出目录（或目录部分）</li>
     <li>用户恢复产品组件的同步继承。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>指示启动项创建的内容存在实时关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>执行特定于目录生成的转出挂接。 调用CatalogGenerator的executePageRolloutHooks和executeProductRolloutHooks方法。<br /> 请参阅AEM Javadocs中的com.adobe.cq.commerce.pim.api.CatalogGenerator 。</td>
   <td> </td>
  </tr>
  <tr>
   <td>产品更新</td>
   <td>更新产品目录的Live Copy中的产品页面</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 创建转出配置 {#creating-a-rollout-configuration}

您可以 [创建转出配置](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) 当安装的转出配置不符合您的应用程序要求时：

* [创建转出配置](/help/sites-developing/extending-msm.md#create-the-rollout-configuration)
* [将同步操作添加到转出配置中](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

然后，在 Blueprint 或 Live Copy 页面上设置转出配置时，您就可以使用新的转出配置。

### 从同步中排除属性和节点类型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置多个支持相应同步操作的 OSGi 服务，以便它们不会影响特定的节点类型和属性。例如，许多与AEM内部功能相关的属性和子节点不应包含在Live Copy中。 只应复制与页面用户相关的内容。

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

下表列出了可以为其指定要排除节点的同步操作。该表提供了要使用 Web 控制台进行配置的服务名称以及要使用存储库节点进行配置的 PID。

| 同步操作 | Web 控制台中的服务名称 | 服务 PID |
|---|---|---|
| contentCopy | CQ MSM 内容复制操作 | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | CQ MSM 内容删除操作 | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentupdate | CQ MSM 内容更新操作 | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | CQ MSM 页面移动操作 | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesupdate | CQ MSM 引用更新操作 | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

下表描述了您可以配置的属性：

<table>
 <tbody>
  <tr>
   <th>Web控制台属性/OSGi属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>排除的节点类型</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>匹配要从同步操作中排除的节点类型的正则表达式.</td>
  </tr>
  <tr>
   <td><p>排除的段落项</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>匹配要从同步操作中排除的段落项的正则表达式.</td>
  </tr>
  <tr>
   <td><p>排除的页面属性</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>匹配要从同步操作中排除的页面属性的正则表达式.</td>
  </tr>
  <tr>
   <td><p>忽略的 Mixin 节点类型</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>仅适用于CQ MSM内容更新操作。 匹配要从同步操作中排除的mixin节点类型名称的正则表达式。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在经典UI中，LiveCopy页面的“页面属性”对话框中显示的锁图标不反映“排除的页面属性”属性的配置。 即使对于从同步操作中排除的属性，也会显示锁定图标。

>[!NOTE]
>
>在触控优化的UI中，另请参阅 [在页面属性上配置MSM锁定（触屏优化UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### CQ MSM 内容更新操作 – 排除 {#cq-msm-content-update-action-exclusions}

默认情况下，将排除多个属性和节点类型，这些属性和节点类型在 **CQ MSM 内容更新操作**&#x200B;的&#x200B;**已排除页面属性**&#x200B;下的 OSGi 配置中定义。

默认情况下，在转出时排除（即不更新）与以下正则表达式匹配的属性：

![CQ MSM 内容更新操作](assets/chlimage_1.png)

您可以根据需要更改定义排除列表的表达式。

例如，如果您希望将页面&#x200B;**标题**&#x200B;包含在考虑转出的更改中，请从排除项中删除 `jcr:title`。例如，使用正则表达式：

`jcr:(?!(title)$).*`

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置多个 OSGi 服务以支持与更新引用相关的对应同步操作。

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的做法。

下表列出了可以为其指定引用更新的同步操作。该表提供了要使用 Web 控制台进行配置的服务名称以及要使用存储库节点进行配置的 PID。

<table>
 <tbody>
  <tr>
   <th>Web控制台属性/OSGi属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>跨嵌套 Live Copy 更新引用</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>仅适用于CQ MSM引用更新操作。 选择此选项（Web控制台）或将此布尔属性设置为true（存储库配置）可替换针对位于最顶层LiveCopy分支内任何资源的引用。</td>
  </tr>
  <tr>
   <td><p>更新引用页面</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>仅适用于CQ MSM页面移动操作。 选择此选项（Web控制台）或将此布尔属性设置为 <code>true</code> （存储库配置）更新任何引用以使用原始页面来引用LiveCopy页面。</td>
  </tr>
 </tbody>
</table>

## 指定要使用的转出配置 {#specifying-the-rollout-configurations-to-use}

MSM允许您指定通常使用的转出配置集，并且在需要时，您可以覆盖特定活动副本的转出配置集。 MSM 提供了多个位置来指定要使用的转出配置。该位置可确定配置是否适用于特定的Live Copy。

下面列出了可在其中指定要使用的转出配置的位置，并描述了MSM如何确定要用于Live Copy的转出配置：

* **[Live Copy页面属性](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page)：** 当Live Copy页面配置为使用一个或多个转出配置时，MSM将使用这些转出配置。
* **[Blueprint页面属性](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page)：** 当Live Copy基于Blueprint且Live Copy页面未配置转出配置时，将使用与Blueprint源页面关联的转出配置。
* **Live Copy父页面属性：** 当Live Copy页面和Blueprint源页面均未配置转出配置时，将使用适用于Live Copy页面的父页面的转出配置。
* **[系统默认值](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)：** 当无法确定Live Copy父页面的转出配置时，将使用系统默认转出配置。

例如，某个Blueprint使用We.Retail引用站点作为源内容。 从该 Blueprint 创建一个网站。以下列表中的每个项都描述了有关使用转出配置的不同场景：

* 所有Blueprint页面或Live Copy页面均未配置为使用转出配置。 MSM对所有Live Copy页面使用系统默认转出配置。
* We.Retail引用站点的根页面配置了多个转出配置。 MSM对所有Live Copy页面使用这些转出配置。
* We.Retail引用站点的根页面配置了多个转出配置，并且Live Copy站点的根页面配置了一组不同的转出配置。 MSM使用在Live Copy站点的根页面上配置的转出配置。

### 为 Live Copy 页面设置转出配置 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用要在转出源页面时使用的转出配置配置Live Copy页面。 子页面默认情况下会继承该配置。在配置要使用的转出配置时，您将覆盖Live Copy页面从其父页面继承的配置。

您还可以在以下情况下为Live Copy页面配置转出配置 [创建live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. 使用 **站点** 控制台以选择Live Copy页面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Live Copy** 选项卡。

   **配置**&#x200B;部分将显示页面继承的转出配置。

   ![配置](assets/chlimage_1-1.png)

1. 如果需要，可调整 **Live Copy 继承**&#x200B;标记。如果选中，Live Copy配置将在所有子项上都有效。

1. 清除&#x200B;**继承父项的转出配置**&#x200B;属性，然后从列表中选择一个或多个转出配置。

   选择的转出配置将显示在下拉列表下。

   ![选定的转出配置](assets/chlimage_1-2.png)

1. 单击或点按&#x200B;**保存**。

### 为 Blueprint 页面设置转出配置 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用要在转出 Blueprint 页面时使用的转出配置对 Blueprint 页面进行配置。

Blueprint页面的子页面继承配置。 在配置要使用的转出配置时，可能会覆盖页面从其父页面继承的配置。

1. 使用&#x200B;**Sites**&#x200B;控制台选择 Blueprint 的根页面。
1. 从工具栏中选择&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡。
1. 使用下拉选择器选择一个或多个&#x200B;**转出配置**。
1. 使用&#x200B;**保存**&#x200B;持久存储您的更新。

### 设置系统默认转出配置 {#setting-the-system-default-rollout-configuration}

指定要用作系统默认值的转出配置。 要指定默认值，请配置OSGi服务：

* **Day CQ WCM Live Relationship Manager**
服务PID为 `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用任一选项配置服务 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存储库节点](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* 在 Web 控制台中，要配置的属性名称是默认转出配置。
* 使用存储库节点，要配置的属性的名称是 `liverelationshipmgr.relationsconfig.default`。

将此属性值设置为要用作系统默认值的转出配置的路径。默认值为 `/libs/msm/wcm/rolloutconfigs/default`，这是&#x200B;**标准转出配置**。
