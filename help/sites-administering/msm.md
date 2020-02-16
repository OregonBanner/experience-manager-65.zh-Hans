---
title: “重用内容：多站点管理器和Live Copy”
seo-title: “重用内容：多站点管理器和Live Copy”
description: 了解如何使用Live Copy和多站点管理器重用内容。
seo-description: 了解如何使用Live Copy和多站点管理器重用内容。
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 重用内容：多站点管理器和Live Copy{#reusing-content-multi-site-manager-and-live-copy}

多站点管理器(MSM)允许您在多个位置使用相同的站点内容。 MSM使用其Live copy功能来实现以下目的：

* 通过MSM，您可以：

   * 一次创建内容
   * 将此内容复制到同一站点或其他站点的其他区域([Live Copy](#live-copies))中，并在其中重复使用此内容。

* 然后，MSM会保持源内容与其Live Copy之间的（实时）关系，以便：

   * 当您对源内容进行更改时，将同步源和Live Copy（以将这些更改也应用于Live Copy）。
   * 通过断开各个子页面和／或组件的Live关系，可以调整Live Copy的内容。 通过执行此操作，对源所做的更改将不再应用于Live Copy。

本页和下一页介绍了相关问题：

* [创建和同步Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live copy概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM最佳实践](/help/sites-administering/msm-best-practices.md)

## 可能的场景 {#possible-scenarios}

MSM和Live Copy有许多用例，一些场景包括：

* **跨国公司——全球对本地公司**

   MSM支持的一个典型用例是在多个跨国的同语言站点中重复使用内容。 这允许重新使用核心内容，同时允许国家变体。

   例如，We.Retail参考站点示例的“英语”部分是为美国客户创建的。 此站点中的大多数内容也可用于其他We.Retail站点，这些站点面向不同国家和文化的英语客户。 核心内容在所有站点上保持不变，而区域性调整可以进行。

   以下结构可用于美国、英国、加拿大和澳大利亚的站点：

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM不翻译内容。 它用于创建所需的结构和部署内容。
   >
   >
   >如果 [](/help/sites-administering/translation.md) 要扩展此类示例，请参阅翻译多语言站点的内容。

* **国家——总办事处至区域分支**

   或者，拥有经销商网络的公司可能希望为各自的经销商单独创建网站——每个网站都是总部提供的主要网站的变体。 这可能适用于一家拥有多个地区办事处的公司，或由中央加盟商和多个当地加盟商组成的全国加盟系统。

   总部可以提供核心信息，而区域实体可以添加当地信息，如联系细节、开业时间和活动。

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **多个版本**

   或者，您可以使用MSM创建特定子分支的版本。例如，包含特定产品不同版本的详细信息的支持子站点，其中基本信息保持不变，只需更改更新的功能：

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >在这种情况下，始终存在制作直接副本还是使用Live copy的问题。
   >
   >在以下方面有平衡：
   >
   >  * 多少核心内容需要在多个版本上进行更新。
   >
   >反对：
   >
   >  * 需要调整单个副本的数量。


## 通过UI进行MSM {#msm-from-the-ui}

MSM可通过相应控制台中的各种选项直接在UI中访问。 要进行介绍，请列出以下主要位置：

* **创建站点** (**站点**)

   * MSM可帮助您管理共享公共内容的多个网站；例如，网站通常为国际受众提供，因此大多数内容在所有国家／地区都是通用的，并且每个国家／地区都有特定内容的子集。 MSM允许您创建 [Live Copy，这些Live Copy会根据源站点自动更新一个或多个站点](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。 这还有助于您强制实施通用的基本结构，跨多个站点使用通用内容，保持通用的外观，并将精力集中在管理网站之间实际不同的内容上。
   * 需要预定义的Blueprint配置才能指定源。
   * 创建（预定义）源的Live Copy。
   * 为用户提供“转 **出** ”按钮。

* **创建Live Copy** (**Sites**)

   * MSM允许您 [为网站的单个页面或子分支创建临时（一次性）Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);例如，复制子分支以提供有关产品的新／更新版本的信息。
   * 创建点对点Live Copy（无需Blueprint配置）。
   * 可用于（立即）创建任何页面／分支的Live Copy。
   * 需要 **同步** (不提供转出 **按钮** )。

* **查看属性** (**站点**)

   * 在适当的情况下，此选项可 [通过提供有关Live](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) Copy或 **Blueprint的信息来帮助您监**&#x200B;视Live Copy ****。

* **引用** (**站点**)

   * “引 [用](/help/sites-authoring/basic-handling.md#references) ”边栏提供有关 **** Live Copy的信息以及对相应操作的访问。

* **Live copy概述** (**Sites**)

   * 此控制台允许您查 [看和管理您的Blueprint及其Live Copy](/help/sites-administering/msm-livecopy-overview.md)。

* **Blueprint** (工&#x200B;**具** -站 **点**)

   * 此控制台允许您创 [建和管理Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)。

>[!NOTE]
>
>MSM功能的某些方面用于其他几个AEM功能（例如，启动项、目录）;在这些情况下，Live copy由该功能管理。

### 使用的条款 {#terms-used}

作为简介，下表概述了MSM使用的主要术语；这些内容将在后续章节和页面中的更多详细信息中介绍：

<table>
 <tbody>
  <tr>
   <td><strong>期限</strong></td>
   <td><strong>定义</strong></td>
   <td><strong>更多详细信息</strong></td>
  </tr>
  <tr>
   <td><strong>源</strong></td>
   <td>原始页面。</td>
   <td>与Blueprint和／或Blueprint页面同义。</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>由同步操作（由转出配置定义）维护的源副本。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live copy配置</strong></td>
   <td>Live copy的配置详细信息定义。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>实时关系</strong><br /> </td>
   <td>对给定资源的继承进行有效定义；源副本与Live Copy之间的连接。<br /> </td>
   <td>确保对源的更改可以与Live copy同步。</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>与源同义。</td>
   <td>可以由Blueprint配置定义。</td>
  </tr>
  <tr>
   <td><strong>Blueprint配置</strong></td>
   <td>指定源路径的预定义配置。</td>
   <td>在Blueprint配置中引用Blueprint页面时，Rollout命令将变为可用。</td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>用于在源和Live Copy之间同步内容的通用术语(由 <strong>Rollout</strong> 和 <strong>Synchronize</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出</strong><br /> </td>
   <td>从源同步到Live Copy。<br /> 可以由作者（在Blueprint页面上）或系统事件（由转出配置定义）触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出配置</strong></td>
   <td>确定将同步哪些属性的规则、同步方式和同步时间。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>从Live copy页面发出的手动同步请求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>继承</strong></td>
   <td>Live Copy页面／组件在进行同步时会从其源页面／组件继承内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暂停</strong></td>
   <td>临时删除Live copy与其Blueprint页面之间的Live关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分离</strong></td>
   <td>永久删除Live copy与其Blueprint页面之间的Live关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>重置</strong></td>
   <td><p>将Live copy页面重置为：</p>
    <ul>
     <li>删除所有继承取消和<br /> </li>
     <li>将页面返回到与源页面相同的状态。</li>
    </ul> <p>重置会影响您对页面属性、段落系统和组件所做的任何更改。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>浅</strong></td>
   <td>单个页面的Live Copy。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>深</strong></td>
   <td>页面的Live Copy及其子页面。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>有关 [对象名称，请参阅Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 的概述。

## Live Copy {#live-copies}

MSM Live Copy是与原始源保持Live Relations的特定站点内容的副本：

* Live copy会从其源继承内容。
* 同步在对源进行更改时执行内容的实际传输。
* Live Copy可以视为：

   * 浅：单页
   * 深：页面及其子页面

* 同步规则（称为转出配置）可确定要同步的属性以及同步发生的时间。

在上一个示例中， `/content/we-retail/language-masters/en` 全局主站点是英语。 要重复使用此站点的内容，将创建MSM Live Copy:

* 以下内容 `/content/we-retail/language-masters/en` 是源。

* 以下内容 `/content/we-retail/language-masters/en` 将复制到 `/content/we-retail/us/en/`、 `/content/we-retail/gb/en`、 `/content/we-retail/ca/en`和节 `/content/we-retail/au/en` 点下。 这些是Live Copy。

* 作者对以下页面进行了更改 `/content/we-retail/language-masters/en`。
* 触发后，MSM会将这些更改同步到Live Copy。

### Live Copy —— 合成 {#live-copies-composition}

>[!NOTE]
>
>本节中的图表和说明代表潜在Live Copy的快照。 它们不是全面的，但提供了概述以突出特定特征。

最初创建Live Copy时，所选源页面会在Live copy中以1:1为基准反映。 之后，还可以直接在Live copy中创建新资源（页面和／或段落），因此了解这些变体及其对同步的影响非常有用。 可能的合成包括：

* [包含非Live-Copy页面的Live Copy](#live-copy-with-non-live-copy-pages)
* [嵌套Live Copy](#nested-live-copies)

Live copy的基本形式有：

* 反映所选源页面的Live Copy页面的分辨率为1:1。
* 一个配置定义。
* 为每个资源定义的实时关系：

   * 将Live copy资源与其Blueprint/source链接。
   * 在实现继承和转出时使用。

* 可以根据需 [求同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) 更改。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 包含非Live-Copy页面的Live Copy {#live-copy-with-non-live-copy-pages}

在AEM中创建Live Copy时，您可以查看并浏览Live copy分支——并在Live copy分支上使用常规AEM功能。 这意味着您（或进程）可以在Live copy分支中创建新资源（页面和／或段落），例如 `myCanadaOnlyProduct`)。

* 此类资源与源/Blueprint页面没有实时关系，且未同步。
* 可能会出现MSM作为特殊情况处理的情况。 例如，当您（或进程）在源/Blueprint和Live copy分支中创建位置和名称相同的页面时。 有关此类情况，请参 [阅MSM转出冲突](/help/sites-administering/msm-rollout-conflicts.md) ，以了解更多信息。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 嵌套Live Copy {#nested-live-copies}

当您（或进程）在现有Live [Copy中创建新页面时](#live-copy-with-non-live-copy-pages) ，此新页面也可以设置为其他Blueprint的Live Copy。 这称为嵌套Live Copy，其中第二个（内部）Live Copy的行为受第一个（外部）Live copy的影响方式如下：

* 为顶级Live Copy触发的深层转出可以继续到嵌套Live Copy中（例如，如果触发器匹配）。
* 源之间的任何链接都将在Live Copy中重写。

   例如，从第二个到第一个蓝图的链接将重写为从嵌套的／第二个Live Copy到第一个Live Copy的链接。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在Live copy分支中移动／重命名页面，则（在内部）会将其视为嵌套Live Copy，以使AEM能够跟踪关系。

#### 堆叠的Live Copy {#stacked-live-copies}

当Live Copy创建为浅层Live Copy的子项时，它称为“堆叠式Live Copy”。 它的行为方式与嵌套Live Copy [相同](#nested-live-copies)。

### 源、Blueprint和Blueprint配置 {#source-blueprints-and-blueprint-configurations}

任何页面或页面分支都可用作Live copy的源。

但是，MSM还允许您定义指定源路径的Blueprint配置。 使用Blueprint配置的好处是：

* 允许作者在Blueprint上使用 **Rollout** （转出）选项——将修改（显式）推送到继承自此Blueprint的Live Copy。
* 允许作者使用创 **建站点**;这允许用户轻松选择语言并配置Live copy的结构。
* 为与Blueprint有关系的Live Copy定义默认转出配置。

Live Copy的源可以是常规页面或由Blueprint配置包含的页面——两者都是有效的用例。

源将构成Live copy的蓝图。 Blueprint是在以下任一情况下定义的：

* [创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   配置会（预先）定义用于创建Live Copy的页面。

* [创建页面的Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用于创建Live Copy（源页面）的页面是Blueprint页面。

   源页面可以由Blueprint配置引用，也可以不引用。

### 转出和同步 {#rollout-and-synchronize}

转出是集中的MSM操作，用于将Live Copy与其源同步。 您可以手动执行转出，也可以自动执行：

* 可以 [定义转出配置](#rollout-configurations) ，以便特定事 [件](/help/sites-administering/msm-sync.md#rollout-triggers) ，可能导致自动转出。
* 创作Blueprint页面时，您可以使用 [Rollout](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令将更改推送到Live Copy。

   **Rollout** （转出）命令在由Blueprint配置引用的Blueprint页面上可用。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 在创作Live copy页面时，您可以使用 [同步命令](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) ，将更改从源提取到Live Copy。

   Synchronize **(同步** )命令始终在Live Copy页面上可用（无论源/Blueprint页面是否包含在Blueprint配置中）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 转出配置 {#rollout-configurations}

转出配置定义Live Copy与源内容同步的时间和方式。 转出配置由触发器和一个或多个同步操作组成：

* **触发器**

   触发器是导致实时操作同步的事件，如激活源页面。 MSM定义您可以使用的触发器。

* **同步操作**

   对Live Copy执行，以将其与源同步。 示例操作包括复制内容、对子节点排序以及激活Live copy页面。 MSM提供了许多同步操作。

   >[!NOTE]
   >
   >您可以使用Java API为实例创建自定义操作。

转出配置可以重新使用，这样多个Live Copy可以使用相同的转出配置。 标准 [安装中包含](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 若干转出配置。

### 转出冲突 {#rollout-conflicts}

转出可能变得复杂，尤其是当作者同时编辑源和Live Copy中的内容时，因此了解AEM如何处理转出过程中可能发 [生的任何冲突很有用](/help/sites-administering/msm-rollout-conflicts.md)。

### 挂起和取消继承和同步 {#suspending-and-cancelling-inheritance-and-synchronization}

Live copy中的每个页面和组件都通过Live Relationship与其源页面和组件关联。 Live关系配置源中Live copy内容的同步。

您可以 **暂停** Live copy页面的Live copy继承，以便更改页面属性和组件。 暂停继承时，页面属性和组件不再与源同步。

编辑单个页面时，作者可以取消 **组件的继承** 。 取消继承后，将暂停实时关系，并且该组件不会进行同步。 当需要自定义内容的子部分时，取消继承和同步很有用。

### 分离Live Copy {#detaching-a-live-copy}

您还可以将 [Live Copy从其Blueprint中分离](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) ，以删除所有连接。

>[!CAUTION]
>
>“分离”(Detach)操作是永久的且不可撤消的。

“分离”将永久删除Live Copy与其Blueprint页面之间的Live关系。 所有与MSM相关的属性都将从Live copy中删除，并且Live copy页面将变为独立副本。

>[!NOTE]
>
>有关 [完整详细信息，请参阅分离Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) ;包括对子页面和父页面的相关影响。

## 使用MSM的标准步骤 {#standard-steps-for-using-msm}

以下步骤介绍了使用MSM重复使用内容以及同步对Live copy的更改的标准过程。

1. 开发源站点的内容。
1. 确定要使用的转出配置。

   1. MSM安 [装了若干可满足多种用例的转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 。
   1. （可选）您可 [以根据需要创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 。

1. 确定需要指定转 [出配置以根据需要使用](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) 和配置的位置。
1. 如果需要， [请创建标识Live Copy源内容的Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 。
1. [创建Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy)。
1. 根据需要更改源内容。 您应采用贵组织已建立的正常内容审阅和批准流程。
1. [推出Blueprint](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) ，或将 [Live Copy与更改同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 。

## 自定义MSM {#customizing-msm}

MSM提供了多种工具，使您的实施能够适应共享内容时可能存在的异常复杂情况：

* **自定义转出配置**
   [当安装的转出配置不满足您的要求](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) ，请创建转出配置。 您可以使用任何可用的转出触发器和同步操作。

* **自定义同步操作**
   [当安装的操作不满足您的特定应用程序要求时](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) ，创建自定义同步操作。 MSM提供了用于创建自定义同步操作的Java API。

## 最佳实践 {#best-practices}

“ [MSM最佳实践](/help/sites-administering/msm-best-practices.md) ”页包含有关实施的重要信息。
