---
title: Adobe Experience Manager 6.5版本中已弃用和已删除的功能。
description: 特定于Adobe Experience Manager 6.5中已弃用和已删除的功能的发行说明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: aec2eb3303ad9747f6f56ae2eb31c3c7ed7b0c24
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 12%

---

# 已弃用和已删除的功能 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。

要传达即将移除或替换的Adobe Experience Manager (AEM)功能，请应用以下规则：

1. 首先宣布弃用。虽然已弃用，但功能仍然可用，但不会进一步增强。
1. 至少会在以下主要版本中移除已弃用的功能。 实际的目标删除日期将在稍后宣布。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了AEM 6.5中标记为已弃用的特性和功能。通常，首先将计划在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 区域 | 专题 | 替换 | 版本号 (SP) |
|---|---|---|---|
| Screens | AEM中的ActiveMQ。 ActiveMQ用于两个AEM Publish实例之间的通信。 | Adobe建议客户使用负载平衡器。 |  |
| [!DNL Sites] | **社交媒体状态**&#x200B;的体验片段属性。 |   | 6.5.11.0 |
| [!DNL Sites] | 内容片段模板，用于创建简单的内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud集成 | AEM 6.2中引入了AEM到Creative Cloud文件夹共享的功能。它提供了一种为创意用户提供访问AEM中的资源的方法，以便他们可以在中打开这些资源 [!DNL Creative Cloud] 应用程序并上传新文件或将更改保存到AEM。 Creative Cloud应用程序中发布的一项新功能AdobeAsset Link提供了更好的用户体验，以及更强大的直接从Photoshop、InDesign和Illustrator中访问AEM资源的功能。 Adobe不打算进一步增强AEM与Creative Cloud文件夹共享集成。 虽然此功能包含在AEM中，但建议使用替代解决方案。 | 建议客户切换到新的Creative Cloud集成功能，包括AdobeAsset Link或AEM桌面应用程序。 |  |
| 资源 | `AssetDownloadServlet` 对于发布实例，默认情况下处于禁用状态。 有关更多详细信息，请参阅 [AEM安全核对清单](/help/sites-administering/security-checklist.md). | 配置说明位于 [AEM安全核对清单](/help/sites-administering/security-checklist.md). |  |
| 集成 | 屏幕 **[!UICONTROL Experience Manager Cloud Service选择加入]** 已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成更新于 [!DNL Experience Manager] 6.5.该集成支持Adobe Target标准API。 API通过Adobe IMS进行身份验证，并且 [!DNL Adobe I/O Runtime]. 它支持AdobeLaunch在检测方面发挥越来越大的作用 [!DNL Experience Manager] 页面analytics和个性化，选择加入向导在功能上无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O Runtime] 通过各自的集成 [!DNL Experience Manager] 云服务。 | 6.5.7.0 |
| 连接器 | 用于Microsoft®SharePoint 2010和Microsoft®SharePoint 2013的AdobeJCR连接器已弃用 [!DNL Experience Manager] 6.5. | 不适用 |  |
| 动态标签管理器(DTM) | 已弃用与DTM的集成。 | 切换到使用Adobe Experience Platform Launch作为标签管理器。 |   |
| Adobe Target | 通过添加AEM使用以下程序连接到Adobe Target服务的功能 [!DNL Adobe I/O] 基于AEM 6.5中的Adobe Target Standard API (Rest API)，弃用Target Classic API (XML)方式。 | 将集成重新配置到 [使用新API](/help/sites-administering/target.md). |  |
| Adobe Target | 使用 `mbox.js` 已弃用与AEM中的Adobe Target的基于的集成。 | 切换以使用 `at.js` 1.x. |  |
| 商务 | [CIF REST](https://github.com/adobe/commerce-cif-api) 于2018年作为一组微服务提供，以实现AEM与商务引擎之间的集成。 在Adobe于2018年年中收购Adobe Commerce(前身为Magento)后，Adobe决定改变做法，原因有二。 Commerce具有自己的一组Commerce API(REST和GraphQL)，维护两组API是不好的做法。 市场趋势表明，客户正在转向GraphQL，因为这是一种更高效的数据查询方式。 2019年，Adobe发布了新的Commerce Integration Framework，它使用Commerce的GraphQL API作为事实来源。 Adobe不计划进一步投资CIF REST。 建议客户使用替代解决方案。 | 对于AEM-Commerce集成，切换到 [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components). 请参阅AEM与Adobe Commerce集成 [使用Commerce集成框架](/help/commerce/cif/integrating/magento.md). 支持第三方（Commerce除外）与新方法的集成位于Adobe的路线图中。 |  |
| 组件(AEM Sites) | Adobe不打算进一步增强存储在中的大多数Foundation组件 `/libs/foundation/components`. 查找 `cq:deprecated` 和 `cq:deprecatedReason` 属性。 AEM 6.5包含基础组件，从早期版本升级的客户可以继续按原样使用它们。 此外，即使已弃用，也支持基础组件。 | Adobe建议在将来的项目中使用核心组件。 现有站点可以保持不变，也可以使用 [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) 重构站点以使用核心组件。 |  |
| 组件(AEM Sites) | 设计导入程序组件 `/libs/wcm/designimporter/components` 从6.5开始标记为已弃用。Adobe不打算进一步增强设计导入程序实施。 | Adobe计划在未来版本中提供用例的替代实施。 |  |
| Foundation | Granite卸载框架。 Adobe不打算进一步增强CQ 5.6.1中引入的卸载框架，以将资源处理外部化。 | Adobe正在开发下一代云原生卸载框架。 |  |
| 开发人员 | `Hobbes.js`. Adobe不打算进一步增强 `hobbes.js` 用户界面测试框架。 | Adobe建议客户使用Selenium自动化。 |  |
| 开发人员 | jQuery用户界面客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的jQuery UI客户端库。 | Adobe建议仍需要jQuery UI才能将其代码添加到项目代码库的客户。 |  |
| 开发人员 | jQuery Animation客户端库(`granite.jquery.animation`)。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的jQuery Animation客户端库。 | Adobe建议仍需要jQuery动画才能将其代码添加到项目代码库的客户。 |  |
| 开发人员 | Handlebars客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的Handlebar客户端库。 | Adobe建议客户仍然需要 `Handlebars` ，以将其添加到其项目代码库中。 |  |
| 开发人员 | 草坪椅客户库。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的Lawnchair客户端库。 | Adobe建议仍要求代码使用Lawnchair的客户将其添加到其项目代码库中。 |  |
| 开发人员 | `Granite.Sling.js` 客户端库。 Adobe不打算进一步增强作为分发（快速入门）的一部分提供的Granite.Sling.js客户端库。 | Adobe建议依赖库功能来重构其代码的客户不再使用它。 |  |
| 开发人员 | 使用YUI压缩/缩小JavaScript客户端库。 Adobe不打算进一步更新YUI库。 在AEM 6.4之前，YUI默认使用切换到Google Closure Compiler (GCC)的选项来缩小JavaScript。 从AEM 6.5开始，默认使用GCC。 | Adobe建议客户升级到AEM 6.5，以便切换到GCC来实施 |  |
| 开发人员 | CRXDE Lite中的经典UI对话框编辑器。 Adobe不打算进一步增强作为分发（快速入门）的一部分提供的经典UI对话框编辑器 | 没有可用的替换。 |  |
| Forms | AEM Forms与AEM Mobile的集成已弃用。 | 没有可用的替代项。 |  | 开发人员 | CRXDE Lite中的经典UI对话框编辑器。 Adobe不打算进一步增强作为分发（快速入门）的一部分提供的经典UI对话框编辑器 | 没有可用的替换。 |  |
| 开发人员 | Lodash/underscore客户端库。 Adobe不打算进一步维护和更新作为分发（快速入门）的一部分提供的Lodash/underscore客户端库。 | Adobe建议仍需要对其代码使用Lodash/下划线的客户将其添加到其项目代码库中。 |  |
| Screens | Adobe不打算进一步维护和更新用于2Publishers设置的com.adobe.cq.screens.mq.activemq包和相关配置。 | Adobe建议仍需要2发布器设置的客户可以使用负载平衡器方法。 |  |

## 已删除功能 {#removed-features}

此部分列出了从AEM 6.5中删除的特性和功能。以前的版本中这些功能标记为已弃用。

| 区域 | 专题 | 替换 | 版本号 (SP) |
|--- |--- |--- |--- |
| 与[!DNL Experience Cloud] 集成  | 您可以将资源与同步 [!DNL Experience Cloud] 使用配置方式 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 以前称为 [!DNL Adobe Experience Cloud]. | 如果您有任何查询， [联系Adobe客户支持](https://experienceleague.adobe.com/?support-solution=General#support). |  |
| AnalyticsActivity Map | AEM中包含的Activity Map的版本。 | 由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。使用 [Adobe Analytics提供的ActivityMap插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hans). |  |
| 集成 | ExactTarget集成已从默认分发（快速入门）中删除，并且不再可用。 | 无替代方案。 |  |
| 集成 | Salesforce Force API集成已从默认分发（快速入门）中删除，现在是一个要从中安装的额外包 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 该功能仍然可用。 |
| Forms | 由于不再支持Adobe Central产品，因此已删除对Adobe Central Migration Bridge服务的支持。 | 无替代方案。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 无替代方案。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 无替换 |  |
| Forms | 从LiveCycleES4 SP1到AEM 6.5 Forms on JEE的单跳升级不可用 | 请参阅 [可用的升级路径](../forms/using/upgrade.md) 请参阅AEM Forms升级文档。 |  |
| Forms | 从AEM Forms on JEE中删除了基于UPD的群集支持 | 在JEE上的AEM Forms中，您只能使用基于TCP的群集。 如果您将UDP多播服务器从以前的版本升级到JEE上的AEM 5.5 Forms ，请执行手动配置以切换到基于TCP的gemfire群集。 有关详细说明，请参阅 [升级到JEE上的AEM 6.5表单](../forms/using/upgrade-forms-jee.md) |  |
| 开发人员 | Firebug Lite已从默认分发（快速入门）中删除 | 使用浏览器内置的开发人员控制台 |
| 开发人员 | 移除 `customJavaScriptPath` 支持HTML客户端库管理器。 | 无替换 |  |
| [!DNL Assets] | 在中删除了资源卸载功能 [!DNL Adobe Experience Manager] 6.5. | 没有可用的替换。 |  |
| 缓存 | `system/console/slingjsp` 已被删除，在AEM 6.5中不再可用。 | 类和Slightly缓存存储在Apache Sling Commons FileSystem ClassLoader捆绑包下。 您可以在AEM Web控制台中检查捆绑包编号，并直接从文件系统删除缓存文件夹(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
