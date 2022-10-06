---
title: Adobe Experience Manager 6.5版本中已弃用和已删除的功能。
description: 以下发行说明特定于 Adobe Experience Manager 6.5 中已弃用和已删除功能。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 27%

---

# 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

要传达即将移除或替换的AEM功能，请应用以下规则：

1. 首先宣布弃用。虽然已弃用，但功能仍可用，但未进一步增强。
1. 最早在以下主要版本中会删除已弃用的功能。 将宣布实际删除目标的日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了 AEM 6.5 中已标记为弃用的特性和功能。通常，计划在未来发行版中删除的特性将首先设置为弃用，并提供备用方案。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 区域 | 功能 | 替换 | 版本号 (SP) |
|---|---|---|---|
| [!DNL Sites] | **社交媒体状态**&#x200B;的体验片段属性。 |  | 6.5.11.0 |
| [!DNL Sites] | 内容片段模板，用于创建简单的内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud集成 | AEM 6.2中引入了“AEM到Creative Cloud文件夹共享”功能，以便创意用户能够从AEM访问资产，以便在 [!DNL Creative Cloud] 应用程序和上传新文件或将更改保存到AEM。 在 Creative Cloud 应用程序中发布的新功能“Adobe 资产链接”提供了更佳的用户体验，能够直接从 Photoshop、InDesign 和 Illustrator 中轻松访问 AEM Assets。Adobe 不打算进一步增强“AEM 到 Creative Cloud Folder Sharing”集成。虽然AEM中包含该功能，但建议客户使用替换解决方案。 | 建议客户切换到新的Creative Cloud集成功能，包括Adobe资产链接或AEM桌面应用程序。 |  |
| Assets | `AssetDownloadServlet`默认情况下，对发布实例禁用 有关更多详细信息，请参阅 [AEM 安全核对清单](/help/sites-administering/security-checklist.md)。 | [AEM 安全核对清单](/help/sites-administering/security-checklist.md)中描述的配置。 |  |
<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->
| DTM标签管理器 |已弃用与DTM（动态标签管理器）的集成。 | 切换为使用 Adobe Experience Platform Launch 作为标记管理器. || |Adobe Target|添加AEM使用 [!DNL Adobe I/O] 在AEM 6.5中，基于Adobe Target Standard API(Rest API)，弃用了Target Classic API(XML)方式。|将集成重新配置为 [使用新API](/help/sites-administering/target.md). || |Adobe Target|使用 `mbox.js` 已弃用AEM中与Adobe Target的基于集成。|切换使用 `at.js` 1.x.|| |商务 | [CIF剩余](https://github.com/adobe/commerce-cif-api) 是在2018年作为一组微服务提供的，用于启用AEM与商务引擎之间的集成。 在2018年年中Adobe获得Magento后，Adobe决定改变其做法，原因有二。 Magento有其自己的一组商务API（REST和GraphQL），因此维护两组API并不是最佳做法。 市场趋势表明，客户正在向GraphQL转移，因为这是一种更高效的数据查询方式。 2019年，Adobe发布了新的商务集成框架，该框架使用Magento的GraphQL API作为真相来源。 Adobe不打算在CIF REST中进一步投资。 建议客户使用替换解决方案。|对于AEM-Magento集成，请切换到 [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components). 请参阅AEM和Adobe Commerce集成 [使用商务集成框架](/help/commerce/cif/integrating/magento.md). 我们的路线图上提供了对与新方法进行第三方(Magento除外)集成的支持。|| |组件(AEM Sites) |Adobe不打算进一步增强存储在 `/libs/foundation/components`. 查找 `cq:deprecated` 和 `cq:deprecatedReason` 属性。 AEM 6.5中包含Foundation组件，从早期版本升级的客户可以按原样继续使用它们。 此外，即使已弃用，也支持基础组件。 |Adobe建议在将来的项目中使用核心组件。 现有网站可以保持原样或使用 [AEM现代化工具套件](https://github.com/adobe/aem-modernize-tools) 以重构网站以使用核心组件。 || |组件(AEM Sites)|设计导入程序组件 `/libs/wcm/designimporter/components` 已从6.5开始标记为已弃用。Adobe不打算进一步增强设计导入程序的实施。 |Adobe计划在未来版本中提供用例的替代实施。 || |基础|Granite卸载框架。 Adobe不打算进一步增强CQ 5.6.1中引入的将资产处理外部化的卸载框架。|Adobe正在开发下一代云原生卸载框架。||
|开发人员|`Hobbes.js`. Adobe不打算进一步增强 `hobbes.js` 用户界面测试框架。|Adobe建议客户使用Selenium自动化。|| |开发人员|jQuery UI客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）|Adobe一部分提供的jQuery UI客户端库，该库建议仍需要jQuery UI才能将其代码添加到其项目代码库中的客户。|| |开发人员|jQuery动画客户端库(`granite.jquery.animation`)。 Adobe不打算进一步维护和更新作为分发（快速入门）|Adobe一部分提供的jQuery Animation客户端库，该客户端库建议仍需要jQuery Animations作为其代码的客户将其添加到其项目代码库中。|| |开发人员|Handlebars客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）|Adobe一部分提供的Handlebar客户端库，该库建议仍需要Handlebars代码的客户将其添加到其项目代码库中。|| |开发人员|Lawnchair客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）|Adobe一部分提供的Lawnchair客户端库，该库建议仍需Lawnchair的代码的客户将其添加到其项目代码库中。|| |开发人员|`Granite.Sling.js` 客户端库。 Adobe不打算进一步增强作为分发（快速入门）|Adobe一部分提供的Granite.Sling.js客户端库，该库建议依赖库功能的客户重构其代码以不再使用。|| |开发人员|使用YUI压缩/缩小JavaScript客户端库。 Adobe 不打算进一步更新 YUI 库。在AEM 6.4之前，默认使用YUI来缩小JavaScript，并选择切换到Google关闭编译器(GCC)。 从 AEM 6.5 开始，默认使用 GCC。|Adobe建议升级到AEM 6.5的客户转为使用GCC进行实施|| |开发人员|经典UI对话框编辑器处于CRXDE Lite中。 Adobe不打算进一步增强作为分发版（快速入门）一部分提供的经典UI对话框编辑器|无可替换项。 || |Forms|AEM Forms与AEM Mobile的集成已弃用。 |无可替换项。 ||开发人员|CRXDE Lite中的经典UI对话框编辑器。 Adobe不打算进一步增强作为分发版（快速入门）一部分提供的经典UI对话框编辑器|无可替换项。 || |开发人员|Lodash/下划线客户端库。 Adobe不打算进一步维护和更新作为分发版（快速入门）一部分提供的Lodash/下划线客户端库 |Adobe建议仍要求代码使用长划线/下划线的客户将其添加到项目代码库中。 ||

## 已删除功能 {#removed-features}

本部分列出了从AEM 6.5中删除的特性和功能。以前版本将这些功能标记为已弃用。

| 区域 | 功能 | 替换 | 版本号 (SP) |
|--- |--- |--- |--- |
| 与[!DNL Experience Cloud] 集成  | 您可以将资产与 [!DNL Experience Cloud] 使用配置 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 以前称为 [!DNL Adobe Experience Cloud]. | 如果你有任何疑问， [联系Adobe客户支持](https://experienceleague.adobe.com/?support-solution=General#support). |  |
| Analytics Activity Map | AEM 中包含的 Activity Map 的版本。 | 由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。使用 [由Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hans). |  |
| 集成 | ExactTarget集成已从默认分发版（快速入门）中删除，不再可用。 | 无替换项. |  |
| 集成 | Salesforce Force API集成已从默认分发版（快速入门）中删除，现在是要从安装的额外包 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 该功能仍然可用。 |
| Forms | 由于不再支持 Adobe Central 产品，删除了对 Adobe Central Migration Bridge 服务的支持。 | 无替换项. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 无替换项. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 无替换项 |  |
| Forms | 在JEE上从LiveCycleES4 SP1到AEM 6.5 Forms的单跳升级不可用 | 请参阅 [可用升级路径](../forms/using/upgrade.md) 在AEM Forms升级文档中。 |  |
| Forms | 从JEE上的AEM Forms中删除了基于UPD的群集支持 | 在JEE上的AEM Forms中，只能使用基于TCP的群集。 如果将UDP多播服务器从以前的版本升级到JEE上的AEM 5.5 Forms，请执行手动配置以切换到基于TCP的gemfire群集。 有关详细说明，请参阅 [升级到JEE上的AEM 6.5表单](../forms/using/upgrade-forms-jee.md) |  |
| 开发人员 | Firebug Lite 已从默认分发版（快速入门）中删除 | 使用浏览器内置的开发人员控制台 |
| 开发人员 | 删除 `customJavaScriptPath` 在HTML客户端库管理器中支持。 | 无替换项 |  |
| [!DNL Assets] | 资产卸载功能将在 [!DNL Adobe Experience Manager] 6.5。 | 没有可替换项。 |  |
| 缓存 | `system/console/slingjsp` 已删除，在AEM 6.5中不再可用。 | 类和Slightly缓存存储在Apache Sling Commons FileSystem类加载器包下。 您可以在AEM Web Console中检查包编号，并直接从文件系统中删除缓存文件夹(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |

## 下一版本的预发布 {#pre-announcement-for-next-release}

本节用于预先宣布未来版本中即将发生的更改。 已宣布的更改尚未生效，但将影响客户。 例如，这些功能尚未弃用，但会在弃用后影响用户。 这些更新旨在进行规划。

| 区域 | 功能 | 公告 |
|--- |--- |--- |
| Foundation | UI 框架 | Adobe 计划在 2019 年弃用 Coral UI 2 组件。Coral UI 3 是随 AEM 6.2 引入的，而 AEM 6.5 完全基于 Coral 3。Adobe 建议使用 Coral 2 构建自定义 UI 的客户和合作伙伴将它们重构为使用 Coral 3。Adobe 将提供将 Coral 2 对话框转换为 Coral 3 的工具 - [阅读更多](/help/sites-developing/modernization-tools.md)。 |
