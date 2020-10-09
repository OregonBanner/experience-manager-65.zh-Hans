---
title: AEM常见问题解答
seo-title: AEM 6.4常见问题
description: 使用这些常见问题解答来了解、配置和排除AEM中常见的工作流或问题。
seo-description: 使用这些常见问题解答来了解、配置和排除AEM中常见的工作流或问题。
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# AEM常见问题解答 {#aem-faqs}

了解某些AEM疑难解答和配置问题的答案。

## 站点 {#sites}

### 如何配置无二进制分发？ {#how-do-i-configure-binary-less-distribution}

通过共享数据存储进行部署支持无二进制分发，并且涉及使用基于存储库的分发包导出器(工厂PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)package builder。

启用无二进制模式后，所分发的内容包包含对二进制的引用，而不是实际的二进制。

#### 如何启用无二进制分发？ {#how-do-i-enable-binary-less-distribution}

要启用无二进制分发，请使用共享的Blob存储进行部署。
使用 `useBinaryReferences` 您的代理正在使用的工厂PID()检查 `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*OSGI* 配置中的属性。

#### 如何在AEM站点控制台中导航页面层次结构时自定义错误消息？ {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

检查个人设置（JS尚未缩小）的“网络”面板（Chrome浏览器）。

视图 `Initiator` 列以确定请求的发起者。 它提供从AJAX调用开始的文件和行号。 之后，您可以跟踪错误处理函数并根据需要更改错误消息。

#### 如何在AEM中创建内容作者语言副本时启用权限？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

要创建语言复制功能，内容作者需要在位置获得 `/content/projects` 权限。

如果还需要作者管理项目，则解决方法是将作者添加到 `project-administrators` 组。

#### 如何在为项目创建语言副本时更改格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在创建翻译项目之前，在根中创建语言根和语言副本。

例如，在创建名为( `/content/geometrixx` 标题为 `fr_LU` 法语（卢森堡）)的语言根。 随后，从“引用”面板创建页面的语言副本，并导航到 `Create structure only` 中的选项 `Create & Translate`。 最后，创建一个翻译项目，然后将语言副本添加到翻译作业。

有关详细信息，请参阅以下其他资源：

* [准备翻译内容](/help/sites-administering/tc-prep.md)
* [管理翻译项目](/help/sites-administering/tc-manage.md)

#### 如何审核AEM功能，如登录尝试次数和ACL或权限更改？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM引入了记录管理更改的功能，以便更好地进行故障排除和审核。 默认情况下，该信息记录在文 `error.log` 件中。 为了简化监控，建议将它们重定向到单独的日志文件。
要将输出重定向到单独的日志文件，请参 [阅如何审核AEM中的用户管理操作](/help/sites-administering/audit-user-management-operations.md)。

#### 默认情况下如何启用SSL? {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4随SSL向导提供，并优惠一个用户界面来配置Jetty和Granite Jetty SSL支持。

要默认启用SSL，请默 [认参阅SSL](/help/sites-administering/ssl-by-default.md)。

#### 从移动应用程序使用AEM的内容服务时，推荐使用什么架构，最好是React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

内容服务基于Sling Models,AEM开发人员必须为导出的每个组件提供Sling Model pojo。

要了解如何从React应用程序使用AEM内容服务，请参 [阅AEM内容服务入门](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 教程。

此外，如果开发人员要导出组件树，他们还可以实现 `ComponentExporter` 和 `ContainerExporter` 接口，并使用 `ModelFactory` 子组件进行迭代并返回其模型表示。 请参阅以下资源：

[1][Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] Apache [Sling:Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### 如何禁用AEM 6.4调查弹出窗口？ {#how-to-disable-aem-survey-pop-up}

您可以使用触屏UI或Web控制台选择加入使用情况统计信息收集。 有关详细说明，请参 [阅选择聚合使用统计信息收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

#### 是否有好的资源突出了升级到AEM 6.4的主要功能？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

请参阅“了 [解升级AEM的理由](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) ”，其中描述了考虑升级到最新版Adobe Experience Manager的客户的主要功能的高级细分。

## 资产 {#assets}

### 上传MP4文件（例如，使用拖放方法）时，“资产”工作流为何会重复？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果用户在资产节点下上传电影文件时没有删除权限，则删除区块节点将失败，并且上传将重新启动。

#### 每次可使用AEM 6.4运行的最大数字资产数量是多少？ {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager(AEM)6.5当前允许您一次上传最多2 GB的资源。

有关可以使用AEM 6.5操作的最大资产数量的其他信息，请参阅资产规 [模调整指南](/help/assets/assets-sizing-guide.md)。

#### 创建语言副本时OOTB配置的默认设置是什么？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

通过经典UI创建语言副本时，资产不会移动到新语言层次结构下，而是从语言主控使用。

但是，当您通过触屏UI(引&#x200B;**用** ->更新语 **言副本)创建语言副本时**，将使用新语言创建新的DAM文件夹，并从中引用资产。

这是OOTB配置的默认设置。 在翻译配 **置中，您可以设置** “ **翻译页面资产** =不翻译”。
对于AEM 6.4,“工 **具** ”> **“Cloud Services** ” **>“**&#x200B;翻译云服务”。

#### 如何禁用AEM组件，使AEM SegmentStore(AEM 6.3.1.1)呈指数增长？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以禁用OSGi组件禁用程序。 要使用此服务，请参 [阅OSGi组件禁用](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)。

作为解决方法，您还可以在每次AEM重新启动后通过UI或 `curl` 命令（示例如下）手动禁用组件。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何使用AEM 6.5实例配置资产分析？ {#how-to-configure-asset-insights-with-aem-instance}

要为通过Adobe激活(DTM)部署的Experience Manager设置和配置资产分析，请参阅如 [何通过AEM Assets设置资产分析](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)。

#### 如何自定义管理控制台？ {#how-to-customize-admin-consoles}

AEM提供了各种机制，使您能够自定义创作实例的控制台和页面创作功能。 要了解如何创建自定义控制台和自定义控制台的默认视图，请参 [阅自定义控制台](/help/sites-developing/customizing-consoles-touch.md)。

#### CoralUI 2和基于CoralUI 3的组件之间有何区别？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

为Coral3创建了一套新的Granite UI Foundation的Sling组件，位于 [/libs/granite/ui/components/coral/foundation下。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 有一组用于基于CoralUI 2的组件，另一组用于基于CoralUI 3的组件。 新集将不仅是旧集的复制粘贴，还将清理它（例如，简化、删除已弃用的功能）。 因此，建议页面仅使用基于CoralUI 3的集或基于CoralUI 2的集。

要详细了解，请参阅CoralUI 3 [迁移指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)。

#### 如何在AEM Assets自定义搜索组件？ {#how-to-customize-the-search-component-in-aem-assets}

要了解搜索提升／排名和进一步实施信息，请参 [阅简单搜索实施指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)。

简单搜索实施是2017年峰会实验室AEM Search Demystified的材料。

#### AEM Assets和AEM MediaLibrary有何区别？ {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets是AEM Platform上的一个应用程序，允许我们的客户在基于Web的存储库中管理其数字资产(图像、视频、文档和音频剪辑)，而AEM Media Library是存储图像和其他共享资源的AEM WCM内容存储库的指定部分。

请参 [阅AEM Assets与AEM](/help/assets/medialibrary.md) MediaLibrary。

#### 是否可以为WordPress构建插件，允许客户访问Adobe资产选取器以选择图像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是的，使用WordPress的Adobe可以使用AEM Assets资产选取器从其服务器选择图像以添加到其WordPress站点上的帖子。

有关详细 [信息，请参](../assets/search-assets.md#assetpicker) 阅资产选择器。

#### 是否可以在AEM Assets扩展搜索彩块化以添加其他谓词？ {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Adobe Experience Manager(AEM)资产在整个企业范围内的部署能够存储许多资产。 您可以向默认表单添加谓词，或使用包含您选择的彩块化的自定义表单。

请参阅搜 [索彩块化](/help/assets/search-facets.md) ，了解更多信息。
