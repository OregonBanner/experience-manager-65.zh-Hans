---
title: 与Adobe Creative Cloud最佳实践集成
description: 集成 [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] 以简化资产传输工作流并实现高内容速度的最佳实践。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: 协作，Adobe资产链接，桌面应用程序
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: 19dd081674b4954498d6aa62335f6b5a9f2a4146
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 15%

---

# [!DNL Adobe Experience Manager] 和集 [!DNL Creative Cloud] 成最佳实践 {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] 是一款数字资产管理(DAM)解决方案，可与集成， [!DNL Adobe Creative Cloud] 以帮助DAM用户与创意团队合作，简化内容创建过程中的协作。

[!DNL Adobe Creative Cloud] 为创意团队提供解决方案和服务生态系统，以帮助他们创建数字资产。它包括桌面和移动设备应用程序、云服务（如具有桌面同步或Web体验的存储）以及市场（如[!DNL Adobe Stock]）。

请阅读相关内容，以了解根据您的用例在桌面与企业级DAM之间选择哪些集成，以及连接工作流的相关最佳实践。

>[!NOTE]
>
>[!DNL Experience Manager] 文件夹 [!DNL Creative Cloud] 共享已弃用，本指南中不再涵盖。Adobe建议使用较新的功能(如[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)或[Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html))，为创意用户提供对[!DNL Experience Manager]中管理的资产的访问权限。

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 简化桌面版创意人员的体验 | 简化从DAM([!DNL Experience Manager Assets])访问资产的流程，供创意专业人士（更广泛地说，是使用本机资产创建应用程序的桌面用户）使用。 他们需要一种简单明了的方式来发现、使用（打开）、编辑和保存对[!DNL Experience Manager]所做的更改，以及上传新文件。 | Win或Mac台式机；[!DNL Creative Cloud]应用程序 |
| 从[!DNL Adobe Stock]提供高质量、可随时使用的资产 | 营销人员通过协助资产采购和发现来帮助加快内容创建流程。 创意专业人士可直接在其创意工具中使用已批准的资产。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 市场；元数据字段 |
| 按组织分发和共享资产 | 内部部门/地方分支机构和外部合作伙伴、分销商和代理使用由父组织共享的已批准资产。 该组织希望安全、无缝地共享所创建的资产，以便更广泛地重复使用。 | Brand Portal、资产共享共用 |

## Adobe服务以支持协作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 参与角色的价值主张 | Adobe服务 | 涉及的曲面 |
|---|---|---|
| 创意用户从[!DNL Experience Manager]中发现资产、打开并使用资产、编辑资产并将其上传到[!DNL Experience Manager]，以及将新文件上传到[!DNL Experience Manager]，而无需离开[!DNL Creative Cloud]应用程序。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign]。 |
| 业务用户可简化资产的打开和使用、编辑和上传对[!DNL Experience Manager]所做的更改，以及从桌面环境将新文件上传到[!DNL Experience Manager]的过程。 它们使用通用集成来打开本机桌面应用程序中的任何资产类型，包括非Adobe资产类型。 | [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac桌面版上的桌面应用程序 |
| 营销人员和企业用户从[!DNL Experience Manager]内发现、预览、许可和保存并管理[!DNL Adobe Stock]资产。 授权资产和已保存的资产会提供选择[!DNL Adobe Stock]元数据，以便更好地进行管理。 | [Experience Manager和Adobe Stock集成](aem-assets-adobe-stock.md) | [!DNL Experience Manager] web界面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。诸如[Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)之类的替代解决方案、可基于[资产共享共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)组件、使用[Experience Manager资产](/help/assets/manage-assets.md)的[链接共享](/help/assets/link-sharing.md)构建的解决方案，应根据特定要求进行审核。

![Creative CloudExperience Manager连接，确定要使用的功能](assets/creative-connections-aem.png)

### 用例映射和Adobe解决方案 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 用例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面应用程序 | 备注/其他解决方案 |
|---|---|---|---|
| Discover — 浏览DAM文件夹 | 是 | [!DNL Experience Manager] Web界面和桌面操作 |  |
| Discover — 访问DAM收藏集 | 是 | [!DNL Experience Manager] Web界面和桌面操作 |  |
| Discover — 从DAM中搜索资产 | 是 | [!DNL Experience Manager] Web界面和桌面操作 |  |
| 使用 — 打开的资产 | 是 | 是 | [从Web界面或](manage-assets.md#previewing-assets) 从Finder打开 |
| 使用 — 将资产从DAM放入文档中 | 是 — 嵌入 | 是 — 链接或嵌入 | [!DNL Experience Manager] 桌面应用程序允许将资产作为本地文件系统上的文件访问。本机应用程序中的这些链接由本地路径表示。 |
| 编辑 — 打开进行编辑 | 是 — 签出操作 | 是 — 打开操作（在网络共享中） | [签出默认情](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html) 况下，将资产保存到用户的Creative Cloud存储帐户(由Creative Cloud应用程序同步)。 |
| 编辑 — 在DAM外进行中的工作 | 是 — 用户的Creative Cloud存储帐户中可用的资产已同步到桌面。 | 是 |  |
| 编辑 — 上传更改 | 是 — [签入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)，带有可选注释 | 是 |  |
| 上传 — 单个文件 | 是 — 上载当前活动文档 | 是 | [通过Web界面上传](manage-assets.md#uploading-assets) |
| 上传 — 多个文件/分层文件夹结构 | 否 | 是 | [通过Web界面或](manage-assets.md#uploading-assets) 通过自定义脚本或工具上传。 |
| 杂项 — 用户和登录 | Creative Cloud用户登录Creative Cloud桌面应用程序后被识别(SSO) | [!DNL Experience Manager] 用户和凭据 | 两个解决方案的用户都计入[!DNL Experience Manager]用户配额。 |
| 杂项 — 网络和访问 | 需要从用户的桌面访问网络上的[!DNL Experience Manager]部署 | 需要从用户的桌面访问网络上的[!DNL Experience Manager]部署 | [!DNL Adobe Asset Link] 不共享网络代理环境。 |
| 杂项 — 迁移大量资产 | 否 | 否 | [Assets迁移指南](assets-migration-guide.md) |

为了支持资产分发用例，应考虑使用其他解决方案：

* [品牌](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 组合，提供可配置的SaaS加载项来 [!DNL Experience Manager Assets] 发布资产。
* 自定义解决方案基于[资产共享共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)代码库创建。
* [!DNL Experience Manager] [链接](/help/assets/link-sharing.md) 共享，以使用链接共享临时资产。
* [Experience Manager资产Web](/help/assets/manage-assets.md) 与外部方的区域交互，这些区域由访问控制 [!DNL Experience Manager] 设置和必要的IT/网络配置调整来保护，使这些外部用户可以访问 [!DNL Experience Manager]。

## 关键概念和用例 {#key-concepts-and-use-cases}

### 常用术语表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **创意就绪资产：** [!DNL Assets] 已准备好与更广的团队共享，或者已由创意团队选择或批准与营销或LOB团队共享的资产。
* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。
* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本文档中，除非另有特别说明，否则与[!DNL Experience Manager Assets]同义。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM 用户可以是营销或非营销用户，例如业务线 (LOB) 用户、管理员、销售人员等。

### 使用[!DNL Experience Manager]和[!DNL Creative Cloud]集成时的注意事项 {#considerations-when-using-aem-and-creative-cloud-integration}

* 请参阅[桌面应用程序最佳实践](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 请参阅[Adobe Stock集成](aem-assets-adobe-stock.md)
* 请参阅[Adobe资产链接](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

以下是[!DNL Experience Manager]和[!DNL Creative Cloud]集成最佳实践的简要摘要。 阅读本文档的其余部分，以详细了解这些内容。

* **对于在Photoshop、InDesign或Illustrator中工作的创意用户：** Adobe资产链接可提供最佳的用户体验，包括清晰处理从中签出的正在进行的资产 [!DNL Experience Manager]。
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：**[!DNL Experience Manager]请使用 桌面应用程序.
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新.
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 从[!DNL Assets]访问[!DNL Adobe Stock]资产 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager和Adobe Stock](/help/assets/aem-assets-adobe-stock.md) 集成 [!DNL Experience Manager] 为用户提供了从中搜索、预览、许可和保存资产 [!DNL Adobe Stock] 的功能 [!DNL Experience Manager]。授权和保存的[!DNL Stock]资产已选择[!DNL Stock]元数据，可用于使用额外的过滤器搜索这些元数据。

有关此集成的几个重要要点：

* 将Adobe库中的资产保存到[!DNL Experience Manager]后，这些资产将变成常规的[!DNL Assets]资产，并将二进制文件保存到[!DNL Experience Manager]存储库。 与[!DNL Adobe Stock]相关的某些元数据会在[!DNL Experience Manager]中为资产保存，否则，摄取过程与任何其他文件的过程相同。 例如，如果智能标记处于活动状态，则会在保存时将标记添加到这些资产中。
* 保存到[!DNL Experience Manager]的资产是副本，而不是返回到[!DNL Adobe Stock]的链接。

**在中处理从保存 [!DNL Adobe Stock] 到 [!DNL Experience Manager] 的资[!DNL Creative Cloud]**&#x200B;产。此集成与[!DNL Adobe Asset Link]无关，但[!DNL Adobe Asset Link]可以识别从[!DNL Stock]保存的这些资产，并在[!DNL Photoshop]、[!DNL Illustrator]或[!DNL InDesign]的[!DNL Adobe Asset Link]扩展UI中的这些资产上显示其他元数据和[!DNL Adobe Stock]徽标。 这些文件可用于浏览、打开等操作 — 因为它们在保存到[!DNL Experience Manager]时是常规资产。
在扩展名为[!DNL Adobe Asset Link]的[!DNL Creative Cloud]应用程序中工作的创意用户，除了能够从[!DNL Adobe Stock]访问已许可的资产到[!DNL Experience Manager]之外，还可以使用“库”面板搜索、预览和许可[!DNL Adobe Stock]资产。
[!DNL Creative Cloud][!DNL Assets] 获得许 [!DNL Adobe Stock] 可并保存到 [!DNL Experience Manager] 的页面，以供访问部署的更广 [!DNL Experience Manager Assets] 泛团队使用，而通过库面板 [!DNL Adobe Stock] 授 [!DNL Creative Cloud] 权资产的创意人员仅在其帐户中默认 [!DNL Creative Cloud] 可用。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意团队和营销/业务线(LOB)团队之间设计一个高效的工作流并选择最佳支持功能，请务必了解资产何时以及为何存储在DAM中。

### 资产为何存储在DAM中 {#why-assets-are-stored-in-dam}

将资产存储在DAM中，可轻松访问和查找资产。 它可确保组织或生态系统（包括合作伙伴、客户等）中的众多用户都能够利用资产。

大多数组织选择仅存储与下游营销/LOB流程相关的资产(通过[!DNL Experience Manager Sites]发布到Web渠道等渠道，或者通过Adobe Experience Cloud提供的其他渠道(Marketing Cloud、Advertising Cloud和Analytics Cloud测量，提供给用户/合作伙伴等)。 此外，组织会在DAM中存储可能需要审核/批准流程的资产。 这样，DAM存储的资产大多数是极有可能被利用的资产，并避免存储闲置资产。

存储资产还需要考虑技术和资源利用方面的考虑因素。 DAM提供了有关存储资产的其他服务，包括提取元数据、版本控制、生成预览/转码、管理引用和添加访问控制信息。 这些服务需要额外的时间和基础架构资源。

通常，存储所有资产和更新是不可取的。 例如，如果对特定资产的更新质量不佳，并且消耗了过多的资源，则资产可能不会存储在DAM中。

#### 资产存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对在资产生命周期的每个阶段存储资产不感兴趣。 例如，在以下情况下，它们会避免存储资产：

* 尚未完成或有待试验的资产。
* 未能通过创意/内部团队审阅周期的资产。
* 与相关资产相比，团队有更好的候选人来向外部团队展示其工作。

通常，以下类资产存储在DAM中：

* 已达到一定期限且被视为可共享的资产。
* 创意团队预先选择的资产。
* 根据特定合同或协议（例如，从RAW文件转换的JPG文件、从PSD原始文件转换的TIFF/图像），由营销部门使用或请求的特定资产格式。

#### 资产更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

作为规则，只应将与更广泛的DAM用户集相关的资产更新存储在DAM中。 它可确保用户（营销和类似功能）在DAM资产时间轴中仅看到相关版本。

通常与资产生命周期中的主要里程碑相关的更改。 例如，初始营销就绪资产或创意团队提供的基于请求/审阅的正式更新应存储在DAM中并进行版本控制。

创意团队在请求更改DAM中的现有资产后进行的更新（供营销团队审阅）便是相关更新的一个示例。 它应存储在DAM中并进行版本控制，以供进一步引用或还原到之前的版本。

以下是一些通常与之无关的更新示例：

* 在准备好进行营销审核之前，已上传资产的早期版本
* 在进行中的阶段中对资产进行频繁的创意更改，然后创意和营销团队才会确定资产已准备就绪

### 用户对DAM的访问权限 {#user-access-to-dam}

[!DNL Assets] 根据用户对部署的访问权限支持两种类 [!DNL Assets] 型的用户。通常，企业网络（防火墙）内的用户可以直接访问DAM。 企业网络外的其他用户将无法直接访问。 用户类型从技术角度决定可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，已载入内部网络的内部创意团队或代理/创意专业人士有权访问DAM部署，包括[!DNL Experience Manager]登录。 [!DNL Experience Manager] 可以设置网络基础结构，以允许直接访问外部方（通常是受信任的组织，如为客户工作的机构），以通过网络( [!DNL Experience Manager] 例如通过VPN或IP允许列表)访问。

在这种情况下，Adobe资产链接或[!DNL Experience Manager]桌面应用程序有助于您轻松访问最终/已批准的资产，并允许您将创意就绪资产保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

无法直接访问DAM部署的外部机构和自由职业者可能需要访问已批准的资产或希望将其新设计添加到DAM。

使用以下策略提供对最终/已批准资产的访问权限：

* 如果资产链接无法正常工作，请使用桌面应用程序。
* 使用[Experience ManagerAssets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)将资产安全地分发给外部合作伙伴
* 使用基于[资产共享共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)的分发和源门户的自定义实施
* 使用在[!DNL Experience Manager]中设置的访问控制和必要的网络基础架构(例如，VPN和IP允许列表)，使外部方可以访问DAM中的专用内容区域。 他们可以使用[!DNL Experience Manager] Web UI获取资产并将新内容上传到您的DAM。

#### 正在从[!DNL Experience Manager]处理资产 {#work-in-progress-on-assets-from-aem}

如本文档中所述，建议对资产进行重大更新，有时也称为正在进行中的工作，而不要将保存到本地文件的所有编辑内容也作为更改上传到[!DNL Experience Manager]。 这可加快桌面用户的工作速度，限制所用的网络带宽，并保持资产时间线清晰，并将重点放在受控的重大更新上。

Adobe资产链接为此用例提供了良好支持：

* 当[!DNL Photoshop]、[!DNL InDesign]或[!DNL Illustrator]中的用户打算编辑文件时，他们会对给定资产执行签出操作
* 资产将在后台下载，放入通过Creative Cloud桌面应用程序同步到磁盘的用户Creative Cloud帐户中，并在资产的[!DNL Experience Manager]中切换签出标记，以最大限度地减少编辑冲突
* 此后，用户将在同步位置本地存储的文件中工作，并且可以继续工作并保存所需的任何频率的必要更改
* 此外，由于资产位于Creative Cloud帐户中，因此它也可在用户可能拥有的其他设备上使用(例如，可以在专用的Creative Cloud移动应用程序中打开或编辑)，并且可以与其他Creative Cloud用户共享以进行协作。
* 完成更改后，创意用户可以在其Creative Cloud应用程序中对该文件执行签入操作，并提供可选注释。 [!DNL Experience Manager]中的相应资产将进行版本控制，并使用新的二进制文件更新为。 [!DNL Experience Manager] 营销人员或LOB用户等用户有权通过资产时间轴UI访问主要资产更改或 [!DNL Experience Manager] 里程碑。

[!DNL Experience Manager] 桌面应用程序为本机应用程序中打开的资产提供网络共享。默认情况下，在短暂的一段时间后，所有在本地完成的更改都会自动上传到[!DNL Experience Manager]。 通过这种配置，在进行中的工作阶段中频繁保存的内容都将上传到[!DNL Experience Manager]并进行版本控制，从而产生大量网络流量和潜在的可扩展性挑战 — 更不用说[!DNL Experience Manager]中不必要的版本了。

此处推荐的方法是使用[!DNL Experience Manager]桌面应用程序中的选项，关闭自动更新，并利用应用程序资产状态UI中的上传更改操作，手动将资产更改上传到[!DNL Experience Manager]。

#### 批量上传到DAM {#bulk-upload-to-dam}

在某些情况下，您可能需要同时将大量文件上传到DAM，例如：

* 上传照片或大型项目的结果
* 上传由创意代理提供的资产
* 如果选择在DAM之外完成，则从较大的集上传选定资产

描述是指在桌面用户工作流程中正常部分，在操作上（例如，每周或每张照片上传文件）。 此处未介绍大型资产迁移。

您可以利用以下上传功能：

* 要批量上传大型/分层文件夹，请使用提供[文件夹上传](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)功能的[!DNL Experience Manager]桌面应用程序。 您还可以上传分层文件夹结构。 [!DNL Assets] 都是在后台上传的，因此不会将其绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请将文件直接拖到Web界面，或使用[!DNL Assets] Web界面中的“创建”选项。
* 根据您的业务要求，您还可以使用自定义Uploader。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用“网络文件共享”管理数字资产，则只需使用由[!DNL Experience Manager]桌面应用程序映射的网络共享即可被视为一种便捷的替代方法。 从网络文件共享进行转换时，[!DNL Experience Manager] Web界面提供了丰富的数字资产管理功能，这些功能远远超出了网络共享上的可能（搜索、收藏集、元数据、协作、预览等），而[!DNL Experience Manager]桌面应用程序提供了一个便捷的链接，用于将服务器端DAM存储库与桌面上的工作连接起来。

避免使用[!DNL Experience Manager]桌面应用程序直接在[!DNL Assets]的网络共享中管理资产。 例如，请避免使用[!DNL Experience Manager]桌面应用程序移动/复制多个文件。 请改用[!DNL Assets]界面将文件夹从Finder/Explorer拖至网络共享，或使用[!DNL Assets]文件夹上传功能。

#### 资产迁移 {#asset-migration}

要规划和执行从现有系统到新系统的资产迁移，或迁移存储在服务器上的大量资产，请参阅[迁移指南](/help/assets/assets-migration-guide.md)。 [!DNL Experience Manager] 桌面应用程 [!DNL Experience Manager] 序和 [!DNL Creative Cloud] 到集成不支持此类迁移。由于要摄取的资产量很大，并且对元数据映射、转换和摄取有其他要求，因此迁移应使用不同的工具和方法来处理。

>[!MORELIKETHIS]
>
>* [Adobe资产链接](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager桌面应用程序最佳实践](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager和Adobe Stock集成](aem-assets-adobe-stock.md)

