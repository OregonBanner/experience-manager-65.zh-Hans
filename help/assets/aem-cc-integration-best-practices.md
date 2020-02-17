---
title: AEM与Creative cloud集成的最佳实践
description: 将AEM与Adobe Creative cloud集成以简化资产转让工作流程并实现最高效率的最佳实践。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# AEM与Creative cloud集成的最佳实践 {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assets是一款数字资产管理(DAM)解决方案，可与Adobe Creative cloud集成，帮助DAM用户与创意团队协作，从而简化内容创建过程中的协作。

Adobe Creative cloud为创意团队提供解决方案和服务生态系统，帮助他们创建数字资产。 它包括桌面和移动应用程序、云服务（如具有桌面同步或Web体验的存储）以及Adobe Stock等市场。

继续阅读以了解根据您的用例在桌面和企业级DAM之间选择哪些集成，以及连接工作流程的相关最佳实践。

>[!NOTE]
>
>已弃用AEM到Creative cloud文件夹共享，本指南不再涵盖此功能。 Adobe建议使用 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) 或 [](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) AEM桌面应用程序等较新功能，为创意用户提供对AEM中管理的资产的访问权限。

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的表面 |
|---|---|---|
| 简化桌面创意人员的体验 | 简化从DAM（AEM资产）中访问资产的流程，供创意专业人士或更广泛的桌面用户使用本机资产创建应用程序。 他们需要一种简单明了的方法来发现、使用（打开）、编辑和保存对AEM的更改以及上传新文件。 | Win或Mac桌面；Creative cloud应用程序 |
| 从Adobe Stock提供高质量、随时可用的资源 | 营销人员通过协助资产采购和发现来帮助加快内容创建过程。 创意专业人士可以直接在其创意工具中使用获准的资产。 | AEM Assets;Adobe Stock市场；元数据字段 |
| 按组织分发和共享资产 | 内部部门／当地分支机构以及外部合作伙伴、分销商和代理使用父组织共享的已批准资产。 该组织希望安全、无缝地共享创建的资产以扩大重复使用。 | Brand Portal, Asset Share Commons |

## 支持协作需求的Adobe产品 {#adobe-offerings-to-support-the-collaboration-need}

| 相关角色的价值主张 | Adobe产品 | 涉及的表面 |
|---|---|---|
| 创意用户从AEM中发现资产、打开和使用资产、编辑更改并上传到AEM，以及将新文件上传到AEM，而无需离开Creative cloud应用程序。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign |
| 商业用户简化了资产的打开和使用、编辑和上传对AEM的更改，以及从桌面环境将新文件上传到AEM。 他们使用通用集成在本机桌面应用程序中打开任何资源类型，包括非Adobe资源类型。 | [AEM 桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Win和Mac桌面上的AEM桌面应用程序 |
| 营销人员和商业用户从AEM中发现、预览、许可和保存和管理Adobe Stock资产。 许可和保存的资源提供选定的Adobe Stock元数据以更好地管理。 | [Experience Manager与Adobe Stock集成](aem-assets-adobe-stock.md) | AEM web界面 |

本文主要围绕协作需求的前两个方面。 作为一个用例，资产的大规模分发和采购被简要提及。 对于此类需求解决方案，请考虑Adobe Brand Portal或Asset Share Commons。 其他解决方案，如 [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html)，可以基于 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 组件、 [Link Share](/help/assets/link-sharing.md)，使用 [](/help/assets/managing-assets-touch-ui.md) Experience Manager Assets构建的解决方案，应根据特定要求进行审阅。

![适用于AEM的Creative cloud连接：确定要使用的功能](assets/creative-connections-aem.png)

### 用例映射和Adobe解决方案 {#mapping-of-use-cases-and-adobe-solutions}

| 用例 | Adobe Asset Link | AEM 桌面应用程序 | 备注／其他解决方案 |
|---|---|---|---|
| Discover —— 浏览AEM文件夹 | 是 | AEM Web UI +桌面操作 | 浏览网络共享时，关闭缩略图以避免下载资源的二进制文件。 |
| Discover —— 访问AEM集合 | 是 | AEM Web UI +桌面操作 |  |
| Discover —— 从AEM搜索资产 | 是 | AEM Web UI +桌面操作 |  |
| 使用——打开资产 | 是 | 是 -适用于任何应用程序 | [从Web界面或从Finder](managing-assets-touch-ui.md#previewing-assets) 打开 |
| 使用——将资产从AEM置入文档 | 是——嵌入 | 是——链接或嵌入 | AEM桌面应用程序允许以文件形式访问本地文件系统上的资产。 本机应用程序中的这些链接由本地路径表示。 |
| 编辑——打开以进行编辑 | 是——结帐操作 | 是——打开操作（在网络共享中） | [AAL中的注销将资产保存到用户的Creative cloud存储帐户（默认情况下由Creative cloud应用程序同步）。](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) |
| 编辑——在AEM之外进行中的工作 | 是——用户的Creative cloud存储帐户中的可用资产已同步到桌面。 | 是 |  |
| 编辑——上传更改 | 是——带 [可选注释的登记](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 操作 | 是 |  |
| 上传——单个文件 | 是——上载当前活动文档 | 是 | [通过Web界面上传](managing-assets-touch-ui.md#uploading-assets) |
| 上传——多个文件／分层文件夹结构 | 否 | 是 | [通过Web界面上传](managing-assets-touch-ui.md#uploading-assets)；自定义<br>脚本或工具 |
| 其他——用户和登录名 | 登录到Creative cloud桌面应用程序的Creative cloud用户可被识别(SSO) | AEM用户／登录 | 两个解决方案的用户均计入AEM用户配额。 |
| 其他——网络和访问 | 需要从用户桌面访问网络上的AEM部署 | 需要从用户桌面访问网络上的AEM部署 | Adobe Asset link不共享网络代理环境。 |
| 其他——迁移大量资产 | 否 | 否 | [迁移指南](assets-migration-guide.md) |

为支持资产分发使用案例，应考虑以下其他解决方案：

* [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) ，用于向AEM资产提供可配置的SaaS加载项以发布资产。
* 自定义解决方案是基于 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) Code base创建的。
* AEM链 [接共享](/help/assets/link-sharing.md) ，以使用链接临时共享资产。
* [AEM Assets web界面](/help/assets/managing-assets-touch-ui.md) ，其中包含由AEM访问控制设置保护的外部方的区域以及必要的IT/网络配置调整，使这些外部用户可以访问AEM。

## 主要概念和用例 {#key-concepts-and-use-cases}

### 常用术语表 {#glossary-of-common-terms}

* **** 进行中作品或创作中作品(WIP):资产生命周期中的一个阶段，资产会经历多次更改，通常尚未准备好与更多团队共享。
* **** 创意就绪型资源：已准备好与更广的团队共享的资产，或者已经由创意团队选择／批准与营销或LOB团队共享的资产。
* **** 资产批准：为已上传到DAM的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **** 最终资产：已完成所有批准／元数据标记并可供更多团队使用的资产。 此类资产存储在DAM中，供所有（或所有感兴趣的）用户使用。 它可用于营销渠道或由创意团队创建设计。
* **** 次要资产更新／更改：对数字资产进行快速、小的更改。 它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度／亮度、颜色等）而生成的。
* **** 主要资产更新／更改：对数字资产进行更改需要大量工作，并且有时必须在更长的一段时间内完成。 它通常包括多个更改。 更新资产时必须多次保存。 主要资产更新通常会导致资产进入WIP阶段。
* **** DAM:数字资产管理。 在本文档中，除非另有特别提及，否则它与AEM Experience Manager资产同义。
* **** 创意用户：一位创意专业人士，他使用Creative cloud应用程序和服务创建数字资产。 在某些情况下，创意用户可能是可能使用Creative cloud但不创建数字资产（如创意总监或创意团队经理）的创意团队成员。
* **** DAM用户：DAM系统的典型用户。 根据组织的不同，DAM用户可以是营销或非营销用户，例如业务线(LOB)用户、管理员、销售人员等。

### 使用AEM和Creative cloud集成时的注意事项 {#considerations-when-using-aem-and-creative-cloud-integration}

* 查看桌 [面应用程序最佳实践](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 查看 [Adobe Stock集成](aem-assets-adobe-stock.md)
* 请参 [阅Adobe资产链接](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

这是Experience manager和Creative cloud集成的最佳实践的简短摘要。 阅读本文档的其余部分，详细了解这些内容。

* **** 对于在Photoshop、InDesign或Illustrator中工作的创意用户：Adobe Asset link提供最佳用户体验，包括对从AEM中签出的资产的在制品的干净处理
* **** 为简化从桌面访问任何通用文件格式或应用程序的资源的操作：使用AEM桌面应用程序
* **** 了解在DAM中存储资产的原因和时间：更新将提供给组织中更多团队
* **** 注意共享的资源数量：如果您的使用案例是资产分发，则治理和安全性可能是最重要的方面。 考虑使用为大规模操作而构建的工具，如Brand Portal。
* **** 了解资产生命周期：了解不同团队在组织中如何处理资产
* **** 谨慎处理对资产的频繁保存：Adobe Asset link通过PS、AI、ID为您提供相关服务。 对于其他应用程序，除非您需要DAM中的所有更改，否则不要在映射／共享文件夹中执行进行中任务

### 从AEM资产访问Adobe Stock资产 {#access-to-adobe-stock-assets-from-aem-assets}

[AEM和Adobe Stock集成使AEM用户能够从Adobe Stock中搜索、预览、许可和保存资产](/help/assets/aem-assets-adobe-stock.md) ，并将这些资产保存到AEM中。 获得许可和保存的Adobe Stock资源已选择Stock元数据，该元数据可用于使用额外的过滤器搜索这些元数据。

有关此集成的几个要点：

* 将Adobe Stock中的资产保存到AEM后，这些资产将成为常规AEM资产，并将二进制文件保存到AEM存储库。 某些与Adobe Stock相关的元数据会在AEM中为资产保存，否则，摄取过程与任何其他文件的相同。 例如，如果智能标记处于活动状态，则在保存时会将这些标记添加到这些资产。
* 保存到AEM的资产是副本，而不是返回到Adobe Stock的链接。

**处理从Adobe Stock保存到Creative cloud中的AEM的资产**。 此集成独立于Adobe Asset Link，但Adobe Asset link可以识别从Stock保存的这些资源，并在Photoshop、Illustrator或InDesign的Adobe Asset Link扩展UI中在这些资源上显示其他元数据和Stock图标。 这些文件可用于浏览、打开等——因为保存到AEM时它们是常规AEM资产。
使用Adobe Asset link扩展的Creative cloud应用程序的创意用户除了可以从Adobe Stock访问已授权的资源到AEM外，还可以使用Creative cloud库面板搜索、预览和许可Adobe Stock资源。
获得许可并保存到AEM的Adobe Stock资源可供更多团队访问AEM资产部署，而通过Creative Cloud库面板从Adobe Stock获得许可的创意人员只能在其Creative cloud帐户中默认为他们自己提供。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意和营销／业务线(LOB)团队之间设计一个高效的工作流程并选择最佳支持功能，请务必了解资产存储在DAM中的时间和原因。

### 为什么资产存储在DAM中 {#why-assets-are-stored-in-dam}

将资源存储在DAM中，可轻松访问和查找资源。 它可确保整个组织或生态系统中的众多用户（包括合作伙伴、客户等）都能够利用资产。

大多数组织选择仅存储与下游营销/LOB流程相关的资产（通过AEM Sites发布到Web渠道等渠道或Adobe Experience Cloud - Marketing Cloud、Advertising cloud提供的其他渠道发布到这些渠道，并通过Analytics cloud进行衡量，向用户／合作伙伴提供信息等）。 此外，组织会存储在DAM中可能要经过审核／批准流程的资产。 这样，DAM会存储大部分具有高杠杆率的资产，并避免存储闲置资产。

存储资产还需考虑技术和资源利用方面的考虑因素。 DAM围绕存储的资产提供其他服务，包括提取元数据、版本控制、生成预览／转码、管理引用和添加访问控制信息。 这些服务会消耗额外的时间和基础架构资源。

通常，存储所有资产和更新是不可取的。 例如，如果对特定资产的更新质量不佳，并且消耗了过多资源，则资产可能不会存储在DAM中。

#### 当资源存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对在资产生命周期的每个阶段存储资产不感兴趣。 例如，在以下情况下，它们会避免存储资产：

* 尚未完成或有待试验的资产
* 无法通过创意／内部团队审阅周期的资源
* 与相关资产相比，团队有更好的候选人来向外部团队展示其作品

通常，以下类资产存储在DAM中：

* 达到特定期限且被视为可共享的资产
* 创意团队预先选择的资源
* 根据特定合同或协议（例如，从RAW文件转换的JPG文件、从PSD原始文件转换的TIFF/图像），市场营销可使用或请求的特定资产格式

#### 资产更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

通常，只应将与更广泛的DAM用户集相关的资产更新存储在DAM中。 它可确保用户（营销和类似功能）在DAM资产时间轴中只看到相关版本。

通常与资产生命周期中的主要里程碑相关的更改。 例如，初始营销就绪资产或创意团队提供的基于请求／审阅的正式更新应存储在DAM中并进行版本控制。

创意团队在请求更改DAM中现有资产后的更新以供营销团队审阅，这是相关更新的示例。 它应存储在DAM中并进行版本控制，以便进一步参考或还原到先前版本。

以下是通常不相关的更新示例：

* 在准备好进行营销审阅之前上传的资产的早期版本
* 在创作和营销团队确定资产已准备就绪之前，在进行中工作阶段经常对资产进行创意更改

### 用户对DAM的访问 {#user-access-to-dam}

AEM资产根据用户对AEM资产部署的访问权限支持两种类型的用户。 通常，企业网络（防火墙）内的用户可以直接访问DAM。 企业网络之外的其他用户将无法直接访问。 用户类型决定了从技术角度可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，内部创意团队或已加入内部网络的代理／创意专业人士可以访问DAM实例，包括AEM登录名。 可以设置AEM和网络基础架构，以允许直接访问外部方（通常是受信任的组织，如为客户工作的机构），从而通过网络（例如，通过VPN或IP白名单）访问AEM。

在这种情况下，Adobe Asset Link或AEM桌面应用程序可帮助您轻松访问最终／批准的资产，并允许您将创意就绪资产保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

没有直接访问DAM实例的外部机构和自由职业者可能需要访问已批准的资产或希望将其新设计添加到DAM。

使用以下策略提供对最终／批准资产的访问：

* 如果“资产链接”不起作用，请使用桌面应用程序。
* 使用 [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) ，将资产安全地分发给外部合作伙伴
* 使用基于资源共享共享的分发和采购门户的自 [定义实现](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在AEM中设置的访问控制和必要的网络基础架构（例如，VPN和IP白名单），使外部方能够访问DAM中的专用内容区域。 他们可以使用AEM Web UI获取资产并将新内容上传到您的DAM。

#### 在AEM中对资产进行的处理 {#work-in-progress-on-assets-from-aem}

如本文档所述，建议对资产（有时称为进行中的工作）执行重要更新，而不要将保存到本地文件的所有编辑内容作为更改上传到AEM。 这可以加快桌面用户的工作速度、限制网络带宽的使用，并使资产时间线保持整洁，并侧重于受控的主要更新。

Adobe Asset link为此用例提供了良好的支持：

* 当Photoshop、InDesign或Illustrator中的用户希望编辑文件时，他们会对给定资源执行注销操作
* 资产将后台下载，并通过Creative cloud桌面应用程序将同步到磁盘的Creative cloud帐户放入用户中，并且在资产的AEM中会切换注销标志，以最大限度地减少编辑冲突
* 此后，用户在同步位置本地存储的文件中工作，并且可以继续工作并以任何所需频率保存必要的更改
* 此外，由于资产位于Creative cloud帐户中，因此，该资产也可在用户可能拥有的其他设备上使用（例如，可以在专用的Creative cloud移动应用程序中打开或编辑），并可与其他Creative cloud用户共享以进行协作。
* 当创意用户完成更改后，他们可以在其Creative cloud应用程序中对该文件执行登记操作，并添加可选注释。 AEM中的相应资产版本已更新，并已使用新的二进制文件更新为。 AEM用户（如营销人员或LOB用户）可通过AEM资产时间轴UI访问主要资产更改或里程碑。

AEM桌面应用程序为在本机应用程序中打开的资产提供网络共享。 默认情况下，在短暂的一段时间后，本地完成的所有更改将自动上传到AEM。 通过此配置，在进行中阶段中频繁保存的内容将全部上传到AEM并进行版本控制，这将造成大量网络流量和潜在的可扩展性挑战——更不用说AEM中不必要的版本了。

此处建议的方法是使用AEM桌面应用程序中的选项关闭自动更新，并手动将资产更改上传到AEM，从而利用应用程序的资产状态UI中的上传更改操作。

#### 批量上传到DAM {#bulk-upload-to-dam}

在某些情况下，您可能需要同时将大量文件上传到DAM，例如：

* 上传照片或大型项目的结果
* 上传由创意机构提供的资产
* 如果选择是在DAM之外完成的，则从更大的集中上传选定资产

描述将文件作为桌面用户工作流程的常规部分在操作上上传（例如，每周或每张照片上传）。 此处未涵盖大型资产迁移。

您可以利用以下上传功能：

* 要批量上传大型／分层文件夹，请使用提供文件夹上传功能的AEM [桌面应用](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) 程序。 您还可以上传分层文件夹结构。 资产在后台上传，因此不会绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请将文件直接拖动到Web界面，或使用AEM Assets web界面中的创建选项。
* 根据您的业务要求，您还可以使用自定义上传程序。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用网络文件共享管理数字资产，则仅使用由AEM桌面应用程序映射的网络共享可被视为便捷的替代方式。 从网络文件共享转换时，AEM web界面提供了丰富的数字资产管理功能集，这些功能远远超出了网络共享（搜索、集合、元数据、协作、预览等）的可能范围，而AEM桌面应用程序提供了将服务器端DAM存储库与桌面作品连接的便捷链接。

避免使用AEM桌面应用程序直接在AEM资产的网络共享中管理资产。 例如，避免使用AEM桌面应用程序移动／复制多个文件。 请改用AEM资产Web UI将文件夹从Finder/资源管理器拖动到网络共享，或使用AEM资产文件夹上传功能。

#### 资产迁移 {#asset-migration}

要规划和执行从现有系统到新系统的资产迁移或对存储在服务器上的大量资产进行迁移，请参阅迁移 [指南](/help/assets/assets-migration-guide.md)。 AEM桌面应用程序和AEM到Creative cloud的集成不支持此类迁移。 由于需要摄取大量资产，以及元数据映射、转换和摄取方面的其他要求，因此应使用不同的工具和方法来处理迁移。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [AEM桌面应用程序最佳实践](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [AEM和Adobe Stock集成](aem-assets-adobe-stock.md)

