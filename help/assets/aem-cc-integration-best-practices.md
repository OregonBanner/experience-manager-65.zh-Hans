---
title: 与Adobe Creative Cloud集成的最佳实践
description: 要集成的最佳实践 [!DNL Adobe Experience Manager] 替换为 [!DNL Adobe Creative Cloud] 简化资产传输工作流并实现高内容速度。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3264'
ht-degree: 15%

---

# [!DNL Adobe Experience Manager] 和 [!DNL Creative Cloud] 集成最佳实践 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 是一个可与集成的数字资产管理(DAM)解决方案 [!DNL Adobe Creative Cloud] 为了帮助DAM用户与创意团队合作，请简化内容创建过程中的协作。

[!DNL Adobe Creative Cloud] 为创意团队提供解决方案和服务的生态系统，帮助他们创建数字资产。 它包括桌面和移动设备应用程序、具有桌面同步或Web体验的存储等云服务，以及诸如以下类型的市场 [!DNL Adobe Stock].

请阅读并了解，根据您的用例，在桌面版和企业级DAM之间可选择哪些集成，以及连接工作流的关联最佳实践是什么。

>[!NOTE]
>
>[!DNL Experience Manager] 到 [!DNL Creative Cloud] 文件夹共享已弃用，不再包含在本指南中。 Adobe建议使用较新的功能，例如 [Adobe资源链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 或 [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) 为创意用户提供对在中管理的资源的访问权限 [!DNL Experience Manager].

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 简化创意人员在桌面上的体验 | 简化从DAM对资源的访问([!DNL Experience Manager Assets])适用于创意专业人士或更广义地说，适用于在本机资产创建应用程序中工作的桌面用户。 他们需要一种简单明了的方法来发现、使用（打开）、编辑和保存对所做的更改 [!DNL Experience Manager]，并上传新文件。 | Win或Mac台式机； [!DNL Creative Cloud] 应用程序 |
| 从以下位置提供高质量、现成可用的资产： [!DNL Adobe Stock] | 营销人员通过协助进行资产来源和发现，帮助加快内容创建过程。 创意专业人士直接在其创意工具中使用批准的资产。 | [!DNL Experience Manager Assets]； [!DNL Adobe Stock] 市场；元数据字段 |
| 按组织分发和共享资产 | 内部部门/本地分支机构和外部合作伙伴、分销商和代理机构使用由上级组织共享的已批准资产。 公司希望安全、无缝地共享所创建的资产，以便更广泛地重复使用。 | Brand Portal、资产共享公域 |

## 支持协作需要的Adobe产品 {#adobe-offerings-to-support-the-collaboration-need}

| 针对所涉角色的价值主张 | Adobe产品 | 涉及的曲面 |
|---|---|---|
| 创意用户从中发现资源 [!DNL Experience Manager]，打开并使用它们，编辑和上传更改到 [!DNL Experience Manager]，并将新文件上传到 [!DNL Experience Manager]，不离开 [!DNL Creative Cloud] 应用程序。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], 和 [!DNL Adobe InDesign]. |
| 企业用户可简化打开和使用资产、编辑和上传更改的操作 [!DNL Experience Manager]，并将新文件上传到 [!DNL Experience Manager] 桌面环境中的。 他们使用通用集成在本机桌面应用程序中打开任何资源类型，包括非Adobe资源类型。 | [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac桌面上的桌面应用程序 |
| 营销人员和企业用户可发现、预览、许可并保存和管理 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager]. 许可和保存的资产提供选择 [!DNL Adobe Stock] 元数据以实现更好的管理。 | [Experience Manager与Adobe Stock集成](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web界面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。其他解决方案，例如 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可根据以下项构建的解决方案： [资产共享公用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 组件， [链接共享](/help/assets/link-sharing.md)，使用 [Experience Manager Assets](/help/assets/manage-assets.md) 应根据特定要求进行审查。

![Creative CloudExperience Manager连接，确定要使用的功能](assets/creative-connections-aem.png)

### 用例和Adobe解决方案的映射 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 用例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面应用程序 | 备注/其他解决方案 |
|---|---|---|---|
| 发现 — 浏览DAM文件夹 | 是 | [!DNL Experience Manager] Web界面和桌面操作 | |
| 发现 — 访问DAM收藏集 | 是 | [!DNL Experience Manager] Web界面和桌面操作 | |
| 发现 — 从DAM搜索资源 | 是 | [!DNL Experience Manager] Web界面和桌面操作 | |
| 使用 — 打开资源 | 是 | 是 | [从Web界面打开](manage-assets.md#previewing-assets) 或从Finder访问 |
| 使用 — 将来自DAM的资源放入文档中 | 是 — 嵌入 | 是 — 链接或嵌入 | [!DNL Experience Manager] 通过桌面应用程序，可访问本地文件系统上的作为文件的资产。 本机应用程序中的这些链接由本地路径表示。 |
| 编辑 — 打开以进行编辑 | 是 — 签出操作 | 是 — 打开操作（在网络共享中） | [在AAL中签出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 默认情况下，将资源保存到用户的creative cloud storage帐户(由Creative Cloud应用程序同步)。 |
| 编辑 — DAM外部正在进行工作 | 是 — 在同步到桌面的Creative Cloud存储帐户中可用的资源。 | 是 | |
| 编辑 — 上传更改 | 是 —  [签到操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 带有可选注释 | 是 | |
| 上传 — 单个文件 | 是 — 上传当前活动文档 | 是 | [通过Web界面上传](manage-assets.md#uploading-assets) |
| 上传 — 多个文件/分层文件夹结构 | 否 | 是 | [通过Web界面上传](manage-assets.md#uploading-assets) 或通过自定义脚本或工具。 |
| 其他 — 用户和登录 | 可识别登录到Creative Cloud桌面应用程序的Creative Cloud用户(SSO) | [!DNL Experience Manager] 用户和凭据 | 这两种解决方案的用户都依赖于 [!DNL Experience Manager] 用户配额。 |
| 杂项 — 网络和访问 | 需要从用户桌面访问到 [!DNL Experience Manager] 通过网络部署 | 需要从用户桌面访问到 [!DNL Experience Manager] 通过网络部署 | [!DNL Adobe Asset Link] 不共享网络代理环境。 |
| 杂项 — 迁移大量资产 | 否 | 否 | [Assets迁移指南](assets-migration-guide.md) |

要支持资产分发用例，应考虑其他解决方案：

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 对于可配置的SaaS加载项 [!DNL Experience Manager Assets] 以发布资产。
* 自定义解决方案是基于 [资产共享公用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 代码库。
* [!DNL Experience Manager] [链接共享](/help/assets/link-sharing.md) 以使用链接按需共享资产。
* [Experience Manager Assets Web界面](/help/assets/manage-assets.md) 至外部人士之业务范围已抵押 [!DNL Experience Manager] 访问控制设置以及必要的IT/网络配置调整，使这些外部用户能够访问 [!DNL Experience Manager].

## 主要概念和用例 {#key-concepts-and-use-cases}

### 常用术语词汇表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **创意就绪资产：** [!DNL Assets] 已准备好与更广的团队共享，或者已经由创意团队选择或批准与营销或LOB团队共享。
* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。
* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本文档中，它是的同义词 [!DNL Experience Manager Assets]，除非另有特别说明。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM用户可以是营销或非营销用户，例如业务线(LOB)用户、管理员、销售人员等。

### 使用时的注意事项 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 集成 {#considerations-when-using-aem-and-creative-cloud-integration}

* 请参阅 [桌面应用程序最佳实践](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 请参阅 [Adobe Stock集成](aem-assets-adobe-stock.md)
* 请参阅 [Adobe资源链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)

以下是对以下项目的最佳实践的简要总结 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 集成。 请阅读本文档的其余部分以了解这些内容。

* **对于在Photoshop、InDesign或Illustrator中工作的创意用户：** AdobeAsset Link提供了最佳用户体验，包括清晰处理从签出的正在进行的资源 [!DNL Experience Manager].
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：**[!DNL Experience Manager]请使用 桌面应用程序.
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新.
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 访问 [!DNL Adobe Stock] 资源来自 [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager与Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md) 提供 [!DNL Experience Manager] 能够从中搜索、预览、许可和保存资产的用户 [!DNL Adobe Stock] 到 [!DNL Experience Manager]. 已许可并保存 [!DNL Stock] 已选择资源 [!DNL Stock] 元数据，可用于通过额外的过滤器搜索这些元数据。

此集成的一些要点：

* 当Adobe库存中的资源保存到的时间 [!DNL Experience Manager]，则成为常规 [!DNL Assets]，并将二进制文件保存到 [!DNL Experience Manager] 存储库。 一些元数据与 [!DNL Adobe Stock] 为资源保存在 [!DNL Experience Manager]否则，摄取过程将与任何其他文件相同。 例如，如果智能标记处于活动状态，则会在保存时将标记添加到这些资源。
* 资源保存到 [!DNL Experience Manager] 是副本，而不是指向的链接 [!DNL Adobe Stock].

**使用从保存的资产 [!DNL Adobe Stock] 到 [!DNL Experience Manager] 在[!DNL Creative Cloud]**. 此集成独立于 [!DNL Adobe Asset Link]，但 [!DNL Adobe Asset Link] 识别从中保存的这些资源 [!DNL Stock] 这样，会显示其他元数据和 [!DNL Adobe Stock] 这些资产上的徽标 [!DNL Adobe Asset Link] 中的扩展用户界面 [!DNL Photoshop]， [!DNL Illustrator]，或 [!DNL InDesign]. 这些文件可用于浏览、打开等 — 因为它们是保存到时的常规资源 [!DNL Experience Manager].
创意用户使用 [!DNL Creative Cloud] 带以下功能的应用程序 [!DNL Adobe Asset Link] 除了可以从访问已许可的资源之外，该扩展还存在 [!DNL Adobe Stock] 到 [!DNL Experience Manager]，也可以使用 [!DNL Creative Cloud] 用于搜索、预览和许可的“库”面板 [!DNL Adobe Stock] 资产。
[!DNL Assets] 从 [!DNL Adobe Stock] 已许可并保存到 [!DNL Experience Manager] 可供更广泛的团队访问 [!DNL Experience Manager Assets] 部署，而创意人员从获取资产许可 [!DNL Adobe Stock] via [!DNL Creative Cloud] 默认情况下，库面板仅在其中 [!DNL Creative Cloud] 帐户。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意团队和营销团队/业务线(LOB)团队之间设计高效的工作流并选择最佳支持功能，务必要了解资产存储在DAM中的时间和原因。

### 为何将资产存储在DAM中 {#why-assets-are-stored-in-dam}

将资产存储在DAM中可使其轻松访问和查找。 它确保资产可供整个组织或生态系统（包括合作伙伴、客户等）中的众多用户使用。

大多数组织选择仅存储与下游营销/LOB流程相关的资产（通过发布到Web渠道等渠道） [!DNL Experience Manager Sites] 或Adobe Experience Cloud提供服务的其他渠道 — Marketing Cloud、Advertising Cloud，由Analytics Cloud测量，提供给用户/合作伙伴等)。 此外，组织还会在DAM中存储可能接受审核/批准流程的资产。 这样，DAM存储的大部分资产都极有可能被使用，并且可避免存储闲置资产。

存储资产还受技术和资源利用率考虑的约束。 DAM围绕存储的资产提供其他服务，包括提取元数据、版本控制、生成预览/转码、管理引用和添加访问控制信息。 这些服务会占用额外的时间和基础架构资源。

通常，存储所有资产和更新都是不理想的。 例如，如果对特定资产的更新质量不佳并占用过多的资源，则这些资产可能未存储在DAM中。

#### 当资产存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对存储资产生命周期每个阶段的资产不感兴趣。 例如，它们避免在以下情况下存储资产：

* 尚未完成或需要进行试验的资产。
* 未通过创意/内部团队审核周期的资产。
* 与相关资产相比，该团队拥有更好的候选人来向外部团队代表其工作。

通常，以下类资产存储在DAM中：

* 达到一定到期日并被视为可共享资产。
* 创意团队预先选择的资产。
* 营销活动可使用或请求的特定资源格式，具体取决于特定合同或协议(例如，从RAW文件转换的JPG文件、来自PSD原始文件的TIFF/图像)。

#### 当资产的更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

通常，只有与更广泛的DAM用户集相关的资产更新才应存储在DAM中。 它可确保用户（营销和类似功能）在DAM资产时间轴中仅看到相关版本。

通常，更改与资产生命周期中的主要里程碑相关。 例如，初始营销就绪型资产或基于创意团队提供的请求/审阅的官方更新应在DAM中存储和版本控制。

在请求更改DAM中的现有资产后，创意团队的更新以供营销团队查看，这是相关更新的示例。 它应存储在DAM中并进行版本控制，以供进一步参考或还原到以前的版本。

以下是通常不相关的更新示例：

* 在资产准备好进行营销审查之前上传资产的早期版本
* 在创意和营销团队确定资产已准备就绪之前，经常对正在进行阶段的资产进行创意更改

### 用户对DAM的访问权限 {#user-access-to-dam}

[!DNL Assets] 根据对以下内容的访问，支持两种类型的用户： [!DNL Assets] 部署。 通常，企业网络（防火墙）中的用户可以直接访问DAM。 企业网络以外的其他用户无法直接访问。 用户类型从技术角度确定可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，内部创意团队或载入内部网络的代理/创意专业人士有权访问DAM部署，包括 [!DNL Experience Manager] 登录。 [!DNL Experience Manager] 而且网络基础架构可以设置为允许直接访问外部各方（通常是受信任的组织，如为客户工作的机构），以便能够访问 [!DNL Experience Manager] 通过网络，例如，通过VPN或IP允许列表。

在这种情况下，请AdobeAsset Link或 [!DNL Experience Manager] 桌面应用程序有助于提供对最终/已批准资产的轻松访问，并让您能够将创意就绪的资产保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

无法直接访问DAM部署的外部机构和自由职业者可能需要访问批准的资产，或希望将其新设计添加到DAM。

使用以下策略提供对最终/已批准资产的访问：

* 如果Asset Link不起作用，请使用桌面应用程序。
* 使用 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用于将资产安全地分发给外部合作伙伴
* 使用基于的分发和采购门户的自定义实施 [资产共享公用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在中设置的访问控制 [!DNL Experience Manager] 以及必要的网络基础设施(例如VPN和IP允许列表)，以便外部各方能够访问DAM中的专用内容区域。 他们可以使用 [!DNL Experience Manager] 用于获取资产并将新内容上传到DAM的Web UI。

#### 正在处理来自的资产 [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

如本文档中所述，建议对资产执行重大更新，有时也称为正在进行中的工作，而不需将所有编辑内容保存到本地文件也不上载到 [!DNL Experience Manager] 随变化而变化。 这可以加快桌面用户的工作，限制使用的网络带宽，保持资产时间线整洁并专注于受控的重大更新。

Adobe Asset Link为以下用例提供了良好的支持：

* 当用户在 [!DNL Photoshop]， [!DNL InDesign]，或 [!DNL Illustrator] 要编辑文件，用户会对给定资源执行签出操作
* 在后台下载资产，通过Creative Cloud桌面应用程序将同步到磁盘的Creative Cloud帐户放入用户中，并切换签出标记 [!DNL Experience Manager] 在资源上最大程度地减少编辑冲突
* 从此处，用户可在本地存储在同步位置的文件中工作，并可继续以所需的任何频率工作和保存必要的更改
* 此外，由于资产位于Creative Cloud帐户中，因此该资产也可在用户可能拥有的其他设备上使用(例如，可在专用的Creative Cloud移动设备应用程序中打开或编辑)，并可与其他Creative Cloud用户共享以进行协作。
* 当创意用户完成更改后，他们可以在其Creative Cloud应用程序中对该文件执行签入操作，并带有可选注释。 中的相应资产 [!DNL Experience Manager] 进行版本控制，并使用新二进制文件更新到。 [!DNL Experience Manager] 营销人员或LOB用户等用户可以通过访问主要资源更改或里程碑 [!DNL Experience Manager] 资产时间轴UI。

[!DNL Experience Manager] 桌面应用程序为在本机应用程序中打开的资产提供网络共享。 默认情况下，在本地完成的所有更改都将上传到 [!DNL Experience Manager] 在一段短暂的时间后自动完成。 通过此类配置，在进行中的阶段频繁进行的保存操作都将上传到 [!DNL Experience Manager] 版本化，带来了大量网络流量和潜在的可扩展性挑战 — 更不用说中的不必要版本了 [!DNL Experience Manager].

此处推荐的方法是在中使用选项 [!DNL Experience Manager] 桌面应用程序，用于关闭自动更新并将对资产所做的更改上传到 [!DNL Experience Manager] 手动，使用应用程序的资源状态UI中的上传更改操作。

#### 批量上传至DAM {#bulk-upload-to-dam}

在某些情况下，您可能要求同时将大量文件上传到DAM，例如：

* 上传照片拍摄或较大项目的结果
* 上传创意机构提供的资产
* 如果在DAM之外完成选择，则从更大的集中上传选定的资产

描述是指以可操作方式（例如，每周或每次拍照）上传文件，作为桌面用户工作流的常规部分。 此处不包含大型资产迁移。

您可以使用以下上载功能：

* 要批量上传大型/分层文件夹，请使用 [!DNL Experience Manager] 桌面应用程序，提供 [文件夹上载](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 功能。 您还可以上载分层文件夹结构。 [!DNL Assets] 将在后台上传，因此不会绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请将这些文件直接拖到Web界面中，或者使用 [!DNL Assets] web界面。
* 根据您的业务要求，您还可以使用自定义上传程序。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用网络文件共享来管理数字资产，则只需使用映射的网络共享 [!DNL Experience Manager] 桌面应用程序可以被视为一个方便的替代品。 从网络文件共享转换时， [!DNL Experience Manager] Web界面提供了一组丰富的数字资产管理功能，这些功能远远超出了网络共享（搜索、收藏集、元数据、协作、预览等）上的范围，并且 [!DNL Experience Manager] 桌面应用程序提供了一个用于将服务器端DAM存储库与桌面上的工作关联的方便链接。

避免使用 [!DNL Experience Manager] 用于直接在的网络共享中管理资产的桌面应用程序 [!DNL Assets]. 例如，避免使用 [!DNL Experience Manager] 桌面应用程序，用于移动/复制多个文件。 请改用 [!DNL Assets] 界面将文件夹从Finder/Explorer拖至网络共享或使用 [!DNL Assets] 文件夹上传功能。

#### 资源迁移 {#asset-migration}

要规划并执行从现有系统到新系统的资产迁移，或迁移存储在服务器上的大量资产，请参见 [迁移指南](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] 桌面应用程序和 [!DNL Experience Manager] 到 [!DNL Creative Cloud] 集成不支持此类迁移。 由于要引入大量资产，并且存在有关元数据映射、转换和引入的额外要求，因此应使用不同的工具和方法处理迁移。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [Experience Manager桌面应用程序最佳实践](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager与Adobe Stock集成](aem-assets-adobe-stock.md)
