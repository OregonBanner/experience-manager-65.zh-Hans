---
title: "重用内容：多站点管理器和 Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 了解如何通过Live Copy和多站点管理器重用内容。
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 31%

---

# 重用内容：多站点管理器和 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

多站点管理器(MSM)允许您在多个位置使用相同的站点内容。 MSM使用其Live Copy功能来实现以下操作：

* 利用 MSM，您可以：

   * 创建内容一次，然后
   * 将此内容复制到其他区域，并在其他区域中重复使用([live copy](#live-copies))。

* 然后，MSM会维护源内容与其Live Copy之间的（实时）关系，以便：

   * 对源内容进行更改时，将同步源和Live Copy（以将这些更改也应用到Live Copy）。
   * 您可以通过断开单个子页面和/或组件的Live关系来调整Live Copy的内容。 这样一来，对源所做的更改将不再应用于Live Copy。

本页和以下页介绍了相关问题：

* [创建并同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 最佳实践](/help/sites-administering/msm-best-practices.md)

## 可能的情况 {#possible-scenarios}

MSM和Live Copy的用例很多，一些情景包括：

* **跨国 – 全球到本地公司**

   MSM 支持的一个典型用例是在多个采用同一语言的跨国站点中重用内容。这允许重复使用核心内容，同时允许国家变体使用。

   例如，We.Retail参考站点示例的“英语”部分是为美国客户创建的。 此站点中的大多数内容也可用于其他We.Retail网站，这些网站迎合了不同国家/地区和文化中讲英语的客户。 虽然所有站点的核心内容都相同，但可以进行区域调整。

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
   >MSM 不翻译内容。它用于创建所需的结构和部署内容。
   >
   >
   >请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md) 要扩展此类示例。

* **国内 – 总部到地区分支机构**

   或者，拥有经销商网络的公司可能希望为其各个经销商分别建立单独的网站 — 每个网站都是总部提供的主要网站的变体。 这可能适用于拥有多个地区办事处的单一公司，或由中央特许专营授权公司和多个当地特许经营人构成的全国特许经营体系。

   总部可以提供核心信息，而区域实体可以添加本地信息，例如详细联系方式、营业时间和活动。

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **多个版本**

   或者，您也可以使用MSM创建特定子分支的版本。例如，支持子站点，其中包含特定产品不同版本的详细信息，其中基本信息保持不变，只需更改更新的功能：

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
   >在这种情况下，始终会出现以下问题：是制作直接副本还是使用Live Copy。
   >
   >这有一个平衡：
   >
   >  * 在多个版本中，需要更新多少核心内容。
   >
   >相较于：
   >
   >  * 需要调整多少个副本。


## 从 UI 访问 MSM {#msm-from-the-ui}

可使用相应控制台中的各种选项直接通过 UI 访问 MSM。要进行介绍，请列出以下主要位置：

* **创建站点**（**站点**）

   * MSM可帮助您管理共享通用内容的多个网站；例如，网站通常为国际受众提供，以便大多数内容在所有国家/地区都是通用的，并且每个国家/地区都有特定内容的子集。 MSM允许您 [创建Live Copy以根据您的源站点自动更新一个或多个站点](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 这还可以帮助您实施通用的基础结构，跨多个站点使用共有内容，维护共有外观，并专注于管理各个站点之间实际不同的内容。
   * 需要预定义的 Blueprint 配置来指定源。
   * 创建（预定义）源的Live Copy。
   * 为用户提供&#x200B;**转出**&#x200B;按钮。

* **创建 Live Copy**（**站点**）

   * MSM允许您 [为网站的单个页面或子分支创建临时（一次性）Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);例如，复制子分支以提供有关产品新/更新版本的信息。
   * 创建临时Live Copy（无需Blueprint配置）。
   * 可用于（立即）创建任何页面/分支的Live Copy。
   * 需要&#x200B;**同步**（不提供&#x200B;**转出**&#x200B;按钮）。

* **查看属性**（**站点**）

   * 在适当情况下，此选项可帮助您 [监控live copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供有关 **现场警察** y或 **Blueprint**.

* **引用**（**站点**）

   * [引用](/help/sites-authoring/basic-handling.md#references)边栏提供了有关 **Live Copy** 的信息以及对相应操作的访问权限。

* **Live Copy 概述**（**站点**）

   * 此控制台允许您 [查看和管理Blueprint及其Live Copy](/help/sites-administering/msm-livecopy-overview.md).

* **Blueprint**（**工具** – **站点**）

   * 此控制台允许您 [创建和管理Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM功能的某些方面可用于其他几个AEM功能（例如，启动项、目录）；在这些情况下，live copy由该功能管理。

### 使用的术语 {#terms-used}

下表概述了与MSM一起使用的主要术语；有关这些内容的更多详细信息，请参阅后续章节和页面：

<table>
 <tbody>
  <tr>
   <td><strong>术语</strong></td>
   <td><strong>定义</strong></td>
   <td><strong>更多详细信息</strong></td>
  </tr>
  <tr>
   <td><strong>源</strong></td>
   <td>原始页面。</td>
   <td>与 Blueprint 和/或 Blueprint 页面同义.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>（源的）副本，由转出配置定义的同步操作维护. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy 配置</strong></td>
   <td>Live Copy配置详细信息的定义。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>实时关系</strong><br /> </td>
   <td>对给定资源的继承的有效定义；源副本和Live Copy之间的连接。<br /> </td>
   <td>确保对源所做的更改可以与Live Copy同步。</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>与源同义.</td>
   <td>可由 Blueprint 配置定义.</td>
  </tr>
  <tr>
   <td><strong>Blueprint 配置</strong></td>
   <td>用于指定源路径的预定义的配置。</td>
   <td>在 Blueprint 配置中引用 Blueprint 页面时，“转出”命令将变为可用.</td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>用于在源副本和Live Copy之间同步内容的通用术语（由两者同时使用） <strong>转出</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出</strong><br /> </td>
   <td>从源同步到Live Copy。<br /> 可以由作者（在Blueprint页面上）或系统事件（由转出配置定义）触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出配置</strong></td>
   <td>用于确定将同步的属性及其同步方式和时间的规则。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>从Live Copy页面发出的手动同步请求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>继承</strong></td>
   <td>发生同步时，Live Copy页面/组件会从其源页面/组件继承内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暂停</strong></td>
   <td>临时删除Live Copy及其Blueprint页面之间的Live关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分离</strong></td>
   <td>永久删除Live Copy及其Blueprint页面之间的Live关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>重置</strong></td>
   <td><p>将Live Copy页面重置为：</p>
    <ul>
     <li>删除所有继承取消并<br /> </li>
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
>请参阅 [Java API概述](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 对象名称。

## Live Copy {#live-copies}

MSM Live Copy是特定站点内容的副本，其与原始源的Live关系保持不变：

* Live Copy从其源中继承内容。
* 在对源进行更改时，同步会执行实际内容传输。
* Live Copy可以视为：

   * 浅：单页面
   * 深：页面及其子页面

* 同步规则（称为转出配置）可确定要同步的属性以及同步发生的时间。

在上一个示例中，`/content/we-retail/language-masters/en` 是英语版的全局主站点。要重复使用此站点的内容，将创建MSM Live Copy:

* `/content/we-retail/language-masters/en` 下的内容为源。

* 以下内容 `/content/we-retail/language-masters/en` 复制于 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`和 `/content/we-retail/au/en` 节点。 这些是Live Copy。

* 作者对 `/content/we-retail/language-masters/en` 下的页面进行了更改。
* 触发时，MSM会将这些更改同步到Live Copy。

### Live Copy – 构图 {#live-copies-composition}

>[!NOTE]
>
>此部分中的图表和说明表示潜在Live Copy的快照。 虽然它们并不全面，但提供了概述以重点说明具体特征。

最初创建Live Copy时，所选源页面会以1:1的方式反映在Live Copy中。 之后，还可以直接在Live Copy中创建新资源（页面和/或段落），以便了解这些变体以及它们对同步的影响。 可能的构图包括：

* [具有非 Live Copy 页面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [嵌套式 Live Copy](#nested-live-copies)

Live Copy的基本形式包括：

* 反映所选源页面的Live Copy页面比例为1:1。
* 一个配置定义。
* 为每个资源定义的实时关系：

   * 将Live Copy资源与其Blueprint/源链接。
   * 在实现继承和转出时使用。

* 可以根据要求[同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)更改。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 具有非 Live Copy 页面的 Live Copy {#live-copy-with-non-live-copy-pages}

在AEM中创建Live Copy时，您可以查看Live Copy分支并在其中导航 — 并在Live Copy分支中使用常规的AEM功能。 这意味着您（或某个流程）可以在Live Copy分支中创建新资源（页面和/或段落），例如 `myCanadaOnlyProduct`)。

* 此类资源与源/Blueprint 页面没有实时关系，并且不会同步。
* 可能会出现 MSM 作为特殊情况处理的场景。例如，当您（或某个进程）在源/Blueprint和Live Copy分支中创建具有相同位置和名称的页面时。 有关此类情况，请参阅 [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)以了解更多信息。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 嵌套式 Live Copy {#nested-live-copies}

当您（或某个进程）创建 [现有live copy中的新页面](#live-copy-with-non-live-copy-pages) 此新页面还可以设置为其他Blueprint的Live Copy。 这称为嵌套Live Copy，其中第二个（内部）Live Copy的行为受第一个（外部）Live Copy的影响，其方式如下：

* 为顶级Live Copy触发的深层转出可以继续进入嵌套的Live Copy（例如，如果触发器匹配）。
* 源之间的任何链接都将在Live Copy中重写。

   例如，从第二个Blueprint到第一个Blueprint的链接将重写为从嵌套/第二个Live Copy到第一个Live Copy的链接。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在Live Copy分支中移动/重命名页面，则（在内部）该页面将被视为嵌套的Live Copy，以启用AEM来跟踪关系。

#### 堆叠式 Live Copy {#stacked-live-copies}

将Live Copy创建为浅层Live Copy的子项时，它称为堆叠式Live Copy。 其行为方式与 [嵌套Live Copy](#nested-live-copies).

### 源、Blueprint 和 Blueprint 配置 {#source-blueprints-and-blueprint-configurations}

任何页面或页面分支都可用作Live Copy的源。

不过，MSM 还允许您定义指定源路径的 Blueprint 配置。使用 Blueprint 配置的好处是：

* 允许作者使用 **转出** blueprint上的选项 — 将修改（显式）推送到从此blueprint继承的Live Copy。
* 允许作者使用 **创建网站**;这允许用户轻松选择语言并配置Live Copy的结构。
* 为与Blueprint有关的Live Copy定义默认转出配置。

Live Copy的源可以是常规页面或Blueprint配置涵盖的页面 — 这两者都是有效用例。

源将构成Live Copy的蓝图。 在执行以下操作时定义 Blueprint：

* [创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   配置会（预先）定义用于创建Live Copy的页面。

* [创建页面的Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用于创建Live Copy（源页面）的页面是Blueprint页面。

   源页面可以被Blueprint配置引用，也可以不被引用。

### 转出和同步 {#rollout-and-synchronize}

转出是与Live Copy的源同步的中央MSM操作。 您可以手动执行转出，也可以自动执行转出：

* 可以定义[转出配置](#rollout-configurations)，以便特定[事件](/help/sites-administering/msm-sync.md#rollout-triggers)能够促使自动进行转出。
* 在创作Blueprint页面时，您可以使用 [转出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令将更改推送到Live Copy。

   **转出**&#x200B;命令适用于 Blueprint 配置引用的 Blueprint 页面。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 在创作Live Copy页面时，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 命令将更改从源拉入Live Copy。

   的 **同步** 命令始终在live copy页面上可用（无论源/blueprint页面是否包含在blueprint配置中）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 转出配置 {#rollout-configurations}

转出配置定义Live Copy何时以及如何与源内容同步。 转出配置由一个触发器和一个或多个同步操作组成：

* **触发器**

   触发器是导致实时操作同步发生的事件，例如激活源页面。 MSM 定义您可以使用的触发器。

* **同步操作**

   对Live Copy执行，以将其与源同步。 例如，复制内容、对子节点排序以及激活Live Copy页面。 MSM提供了许多同步操作。

   >[!NOTE]
   >
   >您可以使用 Java API 为实例创建自定义操作。

可以重复使用转出配置，以便多个Live Copy可以使用相同的转出配置。 标准安装包含了多个[转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)。

### 转出冲突 {#rollout-conflicts}

转出可能会变得复杂，尤其是当作者同时在源和Live Copy中编辑内容时，了解AEM如何处理任何内容会很有用 [转出过程中可能发生的冲突](/help/sites-administering/msm-rollout-conflicts.md).

### 暂停和取消继承与同步 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy中的每个页面和组件都通过Live关系与其源页面和组件相关联。 Live关系配置源中Live Copy内容的同步。

您可以 **暂停** live copy页面的live copy继承，以便您可以更改页面属性和组件。 当您暂停继承时，页面属性和组件不再与源同步。

在编辑单个页面时，作者可以为组件&#x200B;**取消继承**。取消继承后，实时关系将暂停，并且不会针对该组件进行同步。当需要自定义内容的子部分时，取消继承和同步会很有用。

### 分离 Live Copy {#detaching-a-live-copy}

您还可以 [分离live copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 从其blueprint中删除所有连接。

>[!CAUTION]
>
>分离操作是永久性且不可逆的。

“分离”会永久删除Live Copy及其Blueprint页面之间的Live关系。 所有与MSM相关的属性都将从Live Copy中删除，并且Live Copy页面会成为独立副本。

>[!NOTE]
>
>请参阅 [分离Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 详细信息；包括对子页面和父页面的相关影响。

## 使用 MSM 的标准步骤 {#standard-steps-for-using-msm}

以下步骤描述了使用MSM重复使用内容和将更改同步到Live Copy的标准过程。

1. 开发源站点的内容。
1. 决定要使用的转出配置。

   1. MSM [安装了多个转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)，可满足大量用例的要求。
   1. （可选）如果需要，您可以[创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。

1. 决定需要[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)并按需配置的情况。
1. 如果需要， [创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 来标识Live Copy的源内容。
1. [创建Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 根据需要更改源内容。您应采用您组织已制定的常规内容审查和审批流程。
1. [转出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 蓝图，或 [同步live copy](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 中。

## 自定义 MSM {#customizing-msm}

MSM提供了一些工具，以便您的实施能够适应共享内容时可能存在的异常复杂情况：

* **自定义转出配置**
   [创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 安装的转出配置不符合您的要求时。 您可以使用任何可用的转出触发器和同步操作。

* **自定义同步操作**
   [创建自定义同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 安装的操作不符合您的特定应用程序要求时。 MSM提供用于创建自定义同步操作的Java API。

## 最佳实践 {#best-practices}

[MSM 最佳实践](/help/sites-administering/msm-best-practices.md)页面包含有关您的实施的重要信息。
