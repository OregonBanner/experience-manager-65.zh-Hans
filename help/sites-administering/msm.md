---
title: "重用内容：多站点管理器和 Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 了解如何将内容与Live Copies和多站点管理器重复使用。
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 31%

---

# 重用内容：多站点管理器和 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

多站点管理器(MSM)允许您在多个位置使用相同的站点内容。 MSM使用其Live Copy功能来做到这一点：

* 利用 MSM，您可以：

   * 创建内容一次，然后
   * 将此内容复制到其他区域并在其中重复使用此内容([活动副本](#live-copies))或其他站点的URL名称。

* 然后，MSM将维护源内容与其活动副本之间的（实时）关系，以便：

   * 当您对源内容进行更改时，源副本和活动副本将同步（以将这些更改也应用于活动副本）。
   * 您可以通过断开单个子页面和/或组件的实时关系来调整活动副本的内容。 这样，对源所做的更改将不再应用于Live Copy。

本页和以下页面介绍了相关问题：

* [创建并同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 最佳实践](/help/sites-administering/msm-best-practices.md)

## 可能的情况 {#possible-scenarios}

MSM和活动副本有许多用例，一些情况包括：

* **跨国 – 全球到本地公司**

  MSM 支持的一个典型用例是在多个采用同一语言的跨国站点中重用内容。这允许重复使用核心内容，并允许国家变化。

  例如，We.Retail参考网站示例的英语部分是为美国客户创建的。 此网站中的大多数内容也可用于其他We.Retail网站，这些网站为不同国家/地区和文化的说英语的客户提供服务。 虽然所有站点的核心内容都相同，但可以进行区域调整。

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
  >请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md) 如果您要扩展此类示例，请执行以下操作。

* **国内 – 总部到地区分支机构**

  或者，拥有经销商网络的公司可能希望为各个经销商提供单独的网站 — 每个网站都是总部提供的主站点的变体。 这可能适用于拥有多个地区办事处的单一公司，或由中央特许专营授权公司和多个当地特许经营人构成的全国特许经营体系。

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

  或者，您可以使用MSM创建特定子分支的版本。例如，支持子站点，其中包含特定产品的不同版本的详细信息，其中基本信息保持不变，只需更改更新的功能：

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
  >在此类场景中，始终存在直接复制还是使用Live Copy的问题。
  >
  >有一个平衡点：
  >
  >  * 需要在多个版本上更新的核心内容量。
  >
  >相较于：
  >
  >  * 需要调整的单个副本数量。

## 从 UI 访问 MSM {#msm-from-the-ui}

可使用相应控制台中的各种选项直接通过 UI 访问 MSM。为了提供简介，下面列出了主要位置：

* **创建站点**（**站点**）

   * MSM可帮助您管理共享相同内容的多个网站；例如，通常为国际受众提供网站，以便大多数内容在所有国家/地区都是相同的，具有特定于每个国家/地区的部分内容。 MSM允许您 [创建可根据您的源站点自动更新一个或多个站点的活动副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 这还可以帮助您实施通用的基础结构，跨多个站点使用共有内容，维护共有外观，并专注于管理各个站点之间实际不同的内容。
   * 需要预定义的 Blueprint 配置来指定源。
   * 创建（预定义的）源的Live Copy。
   * 为用户提供&#x200B;**转出**&#x200B;按钮。

* **创建 Live Copy**（**站点**）

   * MSM允许您 [创建单个页面或网站子分支的临时（一次性）Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)；例如，复制子分支可提供有关产品的新/更新版本的信息。
   * 创建临时Live Copy（无需Blueprint配置）。
   * 可用于（立即）创建任何页面/分支的Live Copy。
   * 需要&#x200B;**同步**（不提供&#x200B;**转出**&#x200B;按钮）。

* **查看属性**（**站点**）

   * 在适当的情况下，此选项可帮助您 [监控您的live copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供相关资讯，以便 **Live Cop** y或 **Blueprint**.

* **引用**（**站点**）

   * [引用](/help/sites-authoring/basic-handling.md#references)边栏提供了有关 **Live Copy** 的信息以及对相应操作的访问权限。

* **Live Copy 概述**（**站点**）

   * 此控制台允许您 [查看和管理您的Blueprint及其活动副本](/help/sites-administering/msm-livecopy-overview.md).

* **Blueprint**（**工具** – **站点**）

   * 此控制台允许您 [创建和管理您的Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM功能的各个方面可用于其他几个AEM功能（例如，启动项、目录）；在这些情况下，Live Copy由该功能管理。

### 使用的术语 {#terms-used}

作为介绍，下表概述了用于MSM的主要术语；后续部分和页面中将更详细地介绍这些术语：

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
   <td>Live Copy的配置详细信息的定义。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>实时关系</strong><br /> </td>
   <td>给定资源的继承的有效定义；源和活动副本之间的连接。<br /> </td>
   <td>确保对源所做的更改能够与Live Copy同步。</td>
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
   <td>源和活动副本之间内容同步的通用术语(由两者 <strong>转出</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出</strong><br /> </td>
   <td>从源同步到LiveCopy。<br /> 可以由作者（在Blueprint页面上）或系统事件（由转出配置定义）触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>转出配置</strong></td>
   <td>用于确定将同步的属性及其同步方式和时间的规则。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>从livecopy页面发出的手动同步请求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>继承</strong></td>
   <td>发生同步时，Live Copy页面/组件从其源页面/组件继承内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暂停</strong></td>
   <td>临时删除Live Copy与其Blueprint页面之间的实时关系。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分离</strong></td>
   <td>永久删除Live Copy与其Blueprint页面之间的实时关系。</td>
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
>请参阅 [Java API概述](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 对象名称的。

## Live Copy {#live-copies}

MSM Live Copy是特定站点内容的副本，它保留了与原始源的实时关系：

* live copy从其源继承内容。
* 在对源进行更改时，同步会执行实际内容传输。
* Live Copy可以视为：

   * 浅：单页面
   * 深：页面及其子页面

* 同步规则（称为转出配置）可确定将同步的属性以及同步发生的时间。

在上一个示例中，`/content/we-retail/language-masters/en` 是英语版的全局主站点。要重用此站点的内容，将创建MSM活动副本：

* `/content/we-retail/language-masters/en` 下的内容为源。

* 以下内容 `/content/we-retail/language-masters/en` 复制到 `/content/we-retail/us/en/`， `/content/we-retail/gb/en`， `/content/we-retail/ca/en`、和 `/content/we-retail/au/en` 节点。 这些是活动副本。

* 作者对 `/content/we-retail/language-masters/en` 下的页面进行了更改。
* 触发时，MSM将这些更改同步到活动副本。

### Live Copy – 构图 {#live-copies-composition}

>[!NOTE]
>
>此部分中的图表和说明表示潜在活动副本的快照。 虽然它们并不全面，但提供了概述以重点说明具体特征。

最初创建Live Copy时，选定的源页面会以1:1的比例反映在Live Copy中。 之后，还可以直接在Live Copy中创建新资源（页面和/或段落），因此了解这些变体以及它们对同步有何影响会很有用。 可能的构图包括：

* [具有非 Live Copy 页面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [嵌套式 Live Copy](#nested-live-copies)

Live Copy的基本形式具有：

* 以1:1的比例反映所选源页面的Live Copy页面。
* 一个配置定义。
* 为每个资源定义的实时关系：

   * 将Live Copy资源与其Blueprint/源链接。
   * 在实现继承和转出时使用。

* 可以根据要求[同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)更改。

![同步](assets/chlimage_1-367.png)

#### 具有非 Live Copy 页面的 Live Copy {#live-copy-with-non-live-copy-pages}

在AEM中创建Live Copy时，您可以查看和浏览Live Copy分支，并在Live Copy分支上使用常规AEM功能。 这意味着您（或流程）可以在Live Copy分支中创建新资源（页面和/或段落）(例如， `myCanadaOnlyProduct`)。

* 此类资源与源/Blueprint 页面没有实时关系，并且不会同步。
* 可能会出现 MSM 作为特殊情况处理的场景。例如，当您（或流程）在源/Blueprint和Live Copy分支中创建具有相同位置和名称的页面时。 有关此类情况，请参阅 [MSM 转出冲突](/help/sites-administering/msm-rollout-conflicts.md)以了解更多信息。

![转出冲突](assets/chlimage_1-368.png)

#### 嵌套式 Live Copy {#nested-live-copies}

当您（或流程）创建 [现有Live Copy中的新页面](#live-copy-with-non-live-copy-pages) 此新页面也可以设置为其他Blueprint的Live Copy。 这称为嵌套式Live Copy，其中第二个（内部）Live Copy的行为受第一个（外部）Live Copy的影响，如下所示：

* 为顶级Live Copy触发的深层转出可以继续在嵌套式Live Copy中进行（例如，如果触发器匹配）。
* 源之间的任何链接都将在活动副本中重写。

  例如，从第二个到第一个Blueprint的链接将重写为从嵌套/第二个Live Copy到第一个Live Copy的链接。

![源之间的链接](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在Live Copy分支中移动/重命名页面，则（在内部）这将被视为嵌套式Live Copy，以使AEM能够跟踪关系。

#### 堆叠式 Live Copy {#stacked-live-copies}

Live Copy在作为浅Live Copy的子级创建时称为栈叠式Live Copy。 其行为方式与 [嵌套式Live Copy](#nested-live-copies).

### 源、Blueprint 和 Blueprint 配置 {#source-blueprints-and-blueprint-configurations}

任何页面或页面分支均可用作Live Copy的源。

但是，MSM还允许您定义指定源路径的Blueprint配置。 使用 Blueprint 配置的好处是：

* 允许作者使用 **转出** Blueprint上的选项 — 到（显式）将修改推送到从此Blueprint继承的活动副本。
* 允许作者使用 **创建站点**；这允许用户轻松选择语言并配置Live Copy的结构。
* 为与Blueprint关联的活动副本定义默认转出配置。

Live Copy的源可以是常规页面，也可以是Blueprint配置包含的页面 — 两者都是有效的用例。

源构成了Live Copy的Blueprint。 在执行以下操作时定义 Blueprint：

* [创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

  该配置会预先定义用于创建Live Copy的页面。

* [创建页面的Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  用于创建Live Copy的页面（源页面）是Blueprint页面。

  源页面是否可被Blueprint配置引用。

### 转出和同步 {#rollout-and-synchronize}

转出是将Live副本与其源同步的中心的MSM操作。 您可以手动执行转出，也可以自动进行转出：

* 可以定义[转出配置](#rollout-configurations)，以便特定[事件](/help/sites-administering/msm-sync.md#rollout-triggers)能够促使自动进行转出。
* 在创作Blueprint页面时，您可以使用 [转出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令以将更改推送到live copy。

  **转出**&#x200B;命令适用于 Blueprint 配置引用的 Blueprint 页面。

  ![转出](assets/chlimage_1-370.png)

* 在创作Live Copy页面时，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 命令以将更改从源拉入Live Copy。

  此 **同步** 命令在live copy页面上始终可用（无论源/blueprint页面是否由blueprint配置包含）。

  ![同步](assets/chlimage_1-371.png)

### 转出配置 {#rollout-configurations}

转出配置定义Live Copy与源内容同步的时间和方式。 转出配置由一个触发器和一个或多个同步操作组成：

* **触发器**

  触发器是触发实时操作同步的事件，例如源页面的激活。 MSM 定义您可以使用的触发器。

* **同步操作**

  对Live Copy执行以将其与源同步。 示例操作包括复制内容、对子节点排序和激活Live Copy页面。 MSM提供了大量同步操作。

  >[!NOTE]
  >
  >您可以使用 Java API 为实例创建自定义操作。

可以重复使用转出配置，以便多个Live Copy可以使用相同的转出配置。 标准安装包含了多个[转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)。

### 转出冲突 {#rollout-conflicts}

转出可能会变得复杂，尤其是当作者同时在源和Live Copy中编辑内容时，因此了解AEM如何处理任何内容会很有用 [转出期间可能发生冲突](/help/sites-administering/msm-rollout-conflicts.md).

### 暂停和取消继承与同步 {#suspending-and-cancelling-inheritance-and-synchronization}

Live Copy中的每个页面和组件都通过实时关系与其源页面和组件关联。 实时关系配置来自源的Live Copy内容的同步。

您可以 **暂停** live copy页面的live copy继承，以便您可以更改页面属性和组件。 当您暂停继承时，页面属性和组件不再与源同步。

在编辑单个页面时，作者可以为组件&#x200B;**取消继承**。取消继承后，实时关系将暂停，并且不会针对该组件进行同步。当需要自定义内容的子部分时，取消继承和同步会很有用。

### 分离 Live Copy {#detaching-a-live-copy}

您还可以 [分离live copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 从其Blueprint中删除所有连接。

>[!CAUTION]
>
>分离操作是永久性且不可逆的。

分离将永久删除Live Copy与其Blueprint页面之间的实时关系。 将从Live Copy中删除所有与MSM相关的属性，并且Live Copy页面会成为独立副本。

>[!NOTE]
>
>请参阅 [分离Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) ，以了解全部详细信息；包括对子页面和父页面产生的相关影响。

## 使用 MSM 的标准步骤 {#standard-steps-for-using-msm}

以下步骤描述了使用MSM重用内容并将更改同步到活动副本的标准过程。

1. 开发源站点的内容。
1. 决定要使用的转出配置。

   1. MSM [安装了多个转出配置](/help/sites-administering/msm-sync.md#installed-rollout-configurations)，可满足大量用例的要求。
   1. （可选）如果需要，您可以[创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。

1. 决定需要[指定要使用的转出配置](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)并按需配置的情况。
1. 如果需要， [创建Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 标识Live Copy的源内容。
1. [创建Live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 根据需要更改源内容。您应采用您组织已制定的常规内容审查和审批流程。
1. [转出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) Blueprint，或 [同步live copy](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 随这些变化。

## 自定义 MSM {#customizing-msm}

MSM提供了一些工具，以便您的实施能够适应共享内容时可能存在的特殊复杂性：

* **自定义转出配置**
  [创建转出配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 安装的转出配置不符合您的要求时。 您可以使用任何可用的转出触发器和同步操作。

* **自定义同步操作**
  [创建自定义同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 当安装的操作不符合您的特定应用程序要求时。 MSM提供了一个用于创建自定义同步操作的Java API。

## 最佳实践 {#best-practices}

[MSM 最佳实践](/help/sites-administering/msm-best-practices.md)页面包含有关您的实施的重要信息。
