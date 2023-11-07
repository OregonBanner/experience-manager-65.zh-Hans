---
title: AEM常见问题解答
description: 使用这些常见问题解答来了解、配置和解决AEM中的常见工作流或问题。
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# AEM常见问题解答 {#aem-faqs}

了解一些AEM故障排除和配置问题的答案。

## Sites {#sites}

### 如何配置无二进制分发？ {#how-do-i-configure-binary-less-distribution}

支持在共享数据存储上进行无二进制分发，并且涉及使用基于保险库的分发包导出程序(工厂PID： `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)包生成器。

启用无二进制模式后，分发的内容包包含对二进制文件的引用，而不是实际的二进制文件。

#### 如何启用无二进制分发？ {#how-do-i-enable-binary-less-distribution}

要启用无二进制分发，请使用共享blob存储进行部署。
查看 `useBinaryReferences` OSGI配置中的属性，带有工厂PID ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* 你的经纪人用的那个。

#### 如何在AEM Sites控制台中导航页面层次结构时自定义错误消息？ {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

检查（Chrome浏览器的）网络面板，其中个人设置（JS尚未缩小）。

查看 `Initiator` 列来确定请求的发起者。 它提供从中进行AJAX调用的文件和行号。 稍后，您可以跟踪错误处理函数，并根据需要更改错误消息。

#### 如何在AEM中为内容作者创建语言副本时启用权限？ {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

要创建语言复制功能，内容作者需要以下权限： `/content/projects` 位置。

如果还需要作者管理项目，则解决方法是将作者添加到 `projects-administrators` 组。

#### 在为项目创建语言副本时如何更改格式？ {#how-to-change-the-format-while-creating-language-copy-for-a-project}

在创建翻译项目之前，在根中创建语言根和语言副本。

例如，创建语言根于 `/content/geometrixx` 名称为 `fr_LU` (和标题为法语（卢森堡）)。 随后，从“引用”面板创建页面的语言副本并导航到 `Create structure only` 中的选项 `Create & Translate`. 最后，创建翻译项目，然后将语言副本添加到翻译作业。

有关详细信息，请参阅下面的其他资源：

* [准备内容以进行翻译](/help/sites-administering/tc-prep.md)
* [管理翻译项目](/help/sites-administering/tc-manage.md)

#### 如何审核AEM功能（如登录尝试和ACL或权限更改）？ {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM引入了记录管理更改的功能，以便更好地进行故障排除和审核。 默认情况下，该信息记录在 `error.log` 文件。 为了更便于监视，建议将它们重定向到单独的日志文件。
要将输出重定向到单独的日志文件，请参见 [如何在AEM中审核用户管理操作](/help/sites-administering/audit-user-management-operations.md).

#### 如何默认启用SSL？ {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4附带SSL向导，并提供用于配置Jetty和Granite Jetty SSL支持的用户界面。

要默认启用SSL，请参阅 [默认SSL](/help/sites-administering/ssl-by-default.md).

#### 从移动设备应用程序（最好是React Native）中使用AEM Content Services时，建议的架构是什么？ {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

内容服务基于Sling模型，并且AEM开发人员必须为导出的每个组件提供Sling模型pojo。

要了解如何从React应用程序使用AEM内容服务，请参阅 [AEM Content Services入门](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 教程。

此外，如果开发人员希望导出组件树，他们还可以实施 `ComponentExporter` 和 `ContainerExporter` 界面和使用 `ModelFactory` 对子元件进行迭代并返回其模型表示。 请参阅以下资源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling ：Sling模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何禁用AEM 6.4调查弹出窗口？ {#how-to-disable-aem-survey-pop-up}

您可以使用触屏UI或Web控制台选择收集使用情况统计数据。 有关详细说明，请参阅 [选择收集汇总的使用情况统计数据](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### 是否有重点介绍升级到AEM 6.4的主要功能的有用资源？ {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

请参阅 [了解升级AEM的原因](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 该指南为客户介绍了考虑升级到最新版Adobe Experience Manager的关键功能的高级细目。

## 资源 {#assets}

### 为什么在上传MP4文件（例如，使用拖放方法）时，资产工作流会重复其自身？ {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果用户上传的电影文件在资产节点下没有删除权限，则删除区块节点会失败，并且上传会重新启动。

#### 创建语言副本时，OOTB配置的默认设置是什么？ {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

通过Touch UI创建语言副本时(**引用** -> **更新语言副本**)，将在新语言下创建新的DAM文件夹，并从中引用资产。

这是OOTB配置的默认设置。 您可以设置 **翻译页面资产** = **不翻译** 在翻译配置中。
对于AEM 6.4， **工具** > **Cloud Service** > **翻译云服务**.

#### 如何禁用会导致AEM SegmentStore (AEM 6.3.1.1)呈指数增长的AEM组件？ {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以禁用OSGi组件禁用程序。 要使用此服务，请参阅 [OSGi组件禁用](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

作为解决方法，您还可以通过UI或手动禁用组件。 `curl` 命令（如下示例），在每次AEM重新启动后。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自定义管理控制台？ {#how-to-customize-admin-consoles}

AEM提供了各种机制，使您能够自定义创作实例的控制台和页面创作功能。 要了解如何创建自定义控制台并自定义控制台的默认视图，请参阅 [自定义控制台](/help/sites-developing/customizing-consoles-touch.md).

#### 基于CoralUI 2的组件与基于CoralUI 3的组件有何区别？ {#what-is-the-difference-between-coralui-and-coralui-based-components}

为Coral3创建了一组Granite UI Foundation的新Sling组件，该组件位于 [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 其中一组用于基于CoralUI 2的组件，另一组用于基于CoralUI 3的组件。 新集合将不仅仅是旧集合的复制粘贴，而是将被清理（例如，精简，删除已弃用的功能）。 因此，建议页面仅使用基于CoralUI 3或基于CoralUI 2的集。

要详细了解，请参阅 [基于CoralUI 3的迁移指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### 如何在AEM Assets中自定义搜索组件？ {#how-to-customize-the-search-component-in-aem-assets}

要了解搜索提升/排名以及进一步的实施信息，请参阅 [简单搜索实施指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

简单搜索实现来自2017 Summit实验室AEM Search Demystified的材料。

#### 是否可以为WordPress构建插件，以便允许客户访问Adobe资产选取器来选择图像？ {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是，使用WordPress的客户可以使用Adobe资产选取器从其AEM Assets服务器中选择图像，以添加到其WordPress网站上的帖子中。

请参阅 [资源选择器](../assets/search-assets.md#assetpicker) 以了解更多信息。
