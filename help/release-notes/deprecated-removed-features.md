---
title: Adobe Experience Manager6.5版本中已弃用和已删除的功能。
description: 以下发行说明特定于 Adobe Experience Manager 6.5 中已弃用和已删除功能。
translation-type: tm+mt
source-git-commit: 1e6feac534fe990d614997c4bd3ab999a4a8d479
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 43%

---


# 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

要传达AEM功能即将被移除或替换的信息，请遵循以下规则：

1. 首先宣布弃用。虽然已弃用，但功能仍可用，但未进一步增强。
1. 在以下主要版本中最早会删除已弃用的功能。 将宣布实际删除目标的日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了 AEM 6.5 中已标记为弃用的特性和功能。通常，计划在未来发行版中删除的特性将首先设置为弃用，并提供备用方案。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划以将其实施更改为使用提供的备选方案。

| 区域 | 功能 | 替换 |
|---|---|---|
| Creative Cloud集成 | AEM到Creative Cloud文件夹共享在AEM 6.2中引入，旨在让创意用户能够访问AEM中的资产，以便他们能够在CC应用程序中打开这些资产并上传新文件，或将更改保存到AEM。 在 Creative Cloud 应用程序中发布的新功能“Adobe 资产链接”提供了更佳的用户体验，能够直接从 Photoshop、InDesign 和 Illustrator 中轻松访问 AEM 资产。Adobe 不打算进一步增强“AEM 到 Creative Cloud Folder Sharing”集成。虽然该功能包含在 AEM 中，但强烈建议客户使用替换解决方案。 | 建议客户切换到新的Creative Cloud集成功能，包括Adobe资产链接或AEM桌面应用程序。 有关更多详细信息，请查阅AEM和Creative Cloud集成最佳实践。 |
| 资产 | `AssetDownloadServlet`默认情况下，对发布实例禁用 有关更多详细信息，请参阅 [AEM 安全核对清单](/help/sites-administering/security-checklist.md)。 | [AEM 安全核对清单](/help/sites-administering/security-checklist.md)中描述的配置。 |
| 资产 | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | 遵循用户的访问控制设置并确保具有适当的权限。 |
| Adobe Search &amp; Promote | 已弃用与Adobe Search&amp;Promote的集成。 Adobe 不打算进一步增强 Search &amp; Promote 集成。请注意，Search &amp; Promote 集成在弃用期间仍完全受支持。 |  |
| DTM 标记管理器 | 已弃用与 DTM (Dynamic Tag Manager) 的集成。 | 切换为使用 Adobe Experience Platform Launch 作为标记管理器。 |
| Adobe Target | 为 AEM 新增了一项功能，可以在 AEM 6.5 中通过基于 Adobe I/O 的 Adobe Target Standard API (Rest API) 连接到 Adobe Target 服务，与此同时，弃用 Target Classic API (XML) 方法。 | Reconfigure the integration to [use the new API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Using the `mbox.js` based integration with Adobe Target in AEM is deprecated. | Switch to use `at.js` 1.x. |
| 商务 | [CIF REST于](https://github.com/adobe/commerce-cif-api) 2018年作为一套微服务提供，以实现AEM和商务引擎之间的集成。 Adobe在2018年年中获得Magento后，Adobe决定改变其做法，原因有二。 Magento有自己的一组商务API（REST和GraphQL），维护两组API不是好做法。 市场趋势表明客户正转向GraphQL，因为它是一种更高效的数据查询方式。 2019年，Adobe发布了新的商务集成框架，将Magento的GraphQL API作为真相的来源。 Adobe不打算再投资CIF REST。 强烈建议客户使用替换解决方案。 | 对于AEM-Magento集成，请切 [换至AEM CIF](https://github.com/adobe/aem-cif-project-archetype) Archetype [和AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。 See AEM and Magento integration [using Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). 我们的产品路线图支持与新方法进行第三方(Magento除外)集成。 |
| 组件 (AEM Sites) | Adobe does not plan to make further enhancements to most of the Foundation Components stored in `/libs/foundation/components`. Look for the `cq:deprecated` and `cq:deprecatedReason` property in the component folder. AEM 6.5包含基础组件，从早期版本升级的客户可以按原样继续使用它们。 此外，即使已弃用，也完全支持基础组件。 | Adobe建议将核心组件用于将来的项目。 Existing sites can remain as is or use the [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) to refactor the site to use Core Components. |
| 组件 (AEM Sites) | Design Importer Components `/libs/wcm/designimporter/components` have been marked as deprecated starting 6.5. Adobe does not plan to make further enhancements to that implementation of the design importer. | Adobe计划在未来版本中提供使用案例的替代实施。 |
| Foundation | Granite 卸载框架. Adobe不打算对CQ 5.6.1中引入的用于将资产处理外部化的卸载框架进行进一步增强。 | Adobe 正在开发下一代云本机卸载框架。 |
| 开发人员 | `Hobbes.js`. Adobe does not plan to make further enhancements to the `hobbes.js` user interface testing framework. | Adobe建议客户使用Selenium自动化。 |
| 开发人员 | jQuery UI 客户端库. Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 jQuery UI 客户端库 | Adobe建议仍需jQuery UI才能使用其代码的客户将其添加到其项目代码库中。 |
| 开发人员 | jQuery Animation客户端库(`granite.jquery.animation`)。 Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 jQuery Animation 客户端库 | Adobe建议仍需jQuery动画作为代码的客户将其添加到其项目代码库中。 |
| 开发人员 | Handlebars 客户端库. Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 Handlebar 客户端库 | Adobe建议仍需要Handlebars代码的客户将其添加到项目代码库中。 |
| 开发人员 | Lawnchair 客户端库. Adobe 不打算进一步维护和更新作为分发版（快速入门）的一部分提供的 Lawnchair 客户端库 | Adobe建议仍需要Lawnchair编写代码的客户将其添加到其项目代码库中。 |
| 开发人员 | `Granite.Sling.js` 客户端库。 Adobe 不打算进一步增强作为分发版（快速入门）的一部分提供的 Granite.Sling.js 客户端库 | Adobe建议依赖库功能的客户重新调整其代码以不再使用它。 |
| 开发人员 | 使用 YUI 压缩/缩小 JavaScript 客户端库。Adobe 不打算进一步更新 YUI 库。在AEM 6.4之前，YUI默认为使用切换到Google Closure Compiler(GCC)的选项缩小JavaScript。 从 AEM 6.5 开始，默认使用 GCC。 | Adobe建议升级到AEM 6.5的客户切换到GCC进行实施 |
| 开发人员 | CRXDE lite 中的 Classic UI Dialog Editor. Adobe 不打算进一步增强作为分发版（快速入门）的一部分提供的 Classic UI Dialog Editor | 无可替换。 |
| 表单 | AEM Forms与AEM Mobile的集成已弃用。 | 无可用替换。 |  | 开发人员 | CRXDE lite 中的 Classic UI Dialog Editor. Adobe 不打算进一步增强作为分发版（快速入门）的一部分提供的 Classic UI Dialog Editor | 无可替换。 |
| 开发人员 | Lodash/下划线客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的Lodash/下划线客户端库 | Adobe建议仍需使用Lodash/下划线的客户将其代码添加到其项目代码库中。 |

## 已删除功能 {#removed-features}

本节列表了已从AEM 6.5中删除的特性和功能。以前的版本中已将这些功能标记为已弃用。

| 区域 | 功能 | 替换 |
|--- |--- |--- |
| Analytics Activity Map | AEM 中包含的 Activity Map 的版本。 | 由于 Adobe Analytics API 中的安全性更改，因此无法再使用 AEM 中包含的 Activity Map 版本。使用 [Adobe Analytics提供的ActivityMap插件](https://docs.adobe.com/content/help/zh-Hans/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)。 |
| 集成 | ExactTarget集成已从默认分发（快速启动）中删除，但不再可用。 | 无替换项. |
| 集成 | Salesforce Force API integration has been removed from the default distribution (Quickstart) and is now an extra package to install from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 该功能仍可用。 |
| 表单 | 由于不再支持 Adobe Central 产品，删除了对 Adobe Central Migration Bridge 服务的支持。 | 无替换项. |
| 表单 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 无替换项. |
| 表单 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 无替换项 |
| 表单 | JEE上不提供从LiveCycleES4 SP1到AEM 6.5Forms的单跳升级 | 请参 [阅AEM Forms升级文档](../forms/using/upgrade.md) 中的可用升级路径。 |
| 表单 | 删除了JEE上AEM Forms的基于UPD的群集支持 | 在JEE上的AEM Forms，只能使用基于TCP的群集。 如果将UDP多播服务器从先前版本升级到AEM 5.5FormsJEE上的UDP多播服务器，请执行手动配置以切换到基于TCP的gemfire群集。 有关详细说明，请 [参阅升级到JEE上的AEM 6.5表单](../forms/using/upgrade-forms-jee.md) |
| 开发人员 | Firebug Lite 已从默认分发版（快速入门）中删除 | 使用浏览器内置的开发人员控制台 |
| 开发人员 | Remove `customJavaScriptPath` support in HTML Client Library Manager. | 无替换项 |
| [!DNL Assets] | 资源卸载功能在6.5 [!DNL Adobe Experience Manager] 中被删除。 | 无可替换。 |
| 缓存 | `system/console/slingjsp` aem 6.5中不再提供is removed。 | 类和轻缓存存储在Apache Sling Commons FileSystem ClassLoader捆绑包下。 您可以在AEM Web Console中检查捆绑编号，并直接从文件系统()中删除缓存文`crx-quickstart/launchpad/felix/bundle<ID>`件夹。 |

## Pre-announcement for next release {#pre-announcement-for-next-release}

本部分用于预先宣布未来版本中即将进行的更改。 已宣布的更改尚未生效，但将影响客户。 例如，这些功能尚未弃用，但在弃用后会影响用户。 这些更新是为了规划目的而提供的。

| 区域 | 功能 | 发布 |
|--- |--- |--- |
| Foundation | UI 框架 | Adobe 计划在 2019 年弃用 Coral UI 2 组件。Coral UI 3 是随 AEM 6.2 引入的，而 AEM 6.5 完全基于 Coral 3。Adobe 建议使用 Coral 2 构建自定义 UI 的客户和合作伙伴将它们重构为使用 Coral 3。Adobe 将提供将 Coral 2 对话框转换为 Coral 3 的工具 - [阅读更多](/help/sites-developing/dialog-conversion.md)。 |
