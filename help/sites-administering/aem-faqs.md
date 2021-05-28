---
title: AEM常见问题解答
seo-title: AEM 6.4常见问题解答
description: 使用这些常见问题解答，可了解、配置AEM中的常见工作流或问题，并对其进行故障诊断。
seo-description: 使用这些常见问题解答，可了解、配置AEM中的常见工作流或问题，并对其进行故障诊断。
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---

# AEM常见问题解答{#aem-faqs}

了解一些AEM疑难解答和配置问题的答案。

## 站点 {#sites}

### 如何配置无二进制分发？{#how-do-i-configure-binary-less-distribution}

通过共享数据存储进行部署时支持无二进制分发，并且涉及利用基于保管库的分发包导出程序(工厂PID:`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`)包生成器。

启用无二进制模式后，分发的内容包包含对二进制文件的引用，而不是实际的二进制文件。

#### 如何启用无二进制分发？{#how-do-i-enable-binary-less-distribution}

要启用无二进制分发，请使用共享的Blob存储进行部署。
使用您的代理正在使用的工厂PID(`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;检查OSGI配置中的`useBinaryReferences`属性。

#### 在AEM站点控制台中导航页面层次结构时，如何自定义错误消息？{#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

检查个人设置（JS尚未缩小）的“网络”面板（Chrome浏览器的）。

查看`Initiator`列以确定请求的发起者。 它提供从中进行AJAX调用的文件和行号。 之后，您可以跟踪错误处理函数并根据需要更改错误消息。

#### 如何在AEM中为内容作者创建语言副本时启用权限？{#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

要创建语言副本功能，content-authors需要在`/content/projects`位置拥有权限。

如果还需要作者管理项目，则解决方法是将作者添加到`project-administrators`组。

#### 如何在为项目创建语言副本时更改格式？{#how-to-change-the-format-while-creating-language-copy-for-a-project}

在创建翻译项目之前，在根中创建语言根目录和语言副本。

例如，
在`/content/geometrixx`创建名为`fr_LU`(标题为法语（卢森堡）)的语言根目录。 随后，从引用面板中创建页面的语言副本，并导航到`Create & Translate`中的`Create structure only`选项。 最后，创建一个翻译项目，然后将语言副本添加到翻译作业。

有关详细信息，请参阅以下其他资源：

* [准备翻译内容](/help/sites-administering/tc-prep.md)
* [管理翻译项目](/help/sites-administering/tc-manage.md)

#### 如何审核AEM功能，如登录尝试次数、ACL或权限更改？{#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM引入了记录管理更改的功能，以便更好地进行疑难解答和审核。 默认情况下，该信息记录在`error.log`文件中。 为了更便于监控，建议将它们重定向到单独的日志文件。
要将输出重定向到单独的日志文件，请参阅[如何审核AEM](/help/sites-administering/audit-user-management-operations.md)中的用户管理操作。

#### 默认情况下如何启用SSL?{#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM)6.4随SSL向导一起提供，并提供用于配置Jetty和Granite Jetty SSL支持的用户界面。

要默认启用SSL，请参阅[SSL（默认）](/help/sites-administering/ssl-by-default.md)。

#### 在从移动设备应用程序（理想情况下是React Native）使用AEM Content Services时，建议使用什么架构？{#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

内容服务基于Sling模型，AEM开发人员必须为导出的每个组件提供一个Sling模型选项。

要了解如何从React应用程序使用AEM内容服务，请参阅[AEM内容服务入门](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)教程。

此外，如果开发人员想要导出组件树，他们还可以实施`ComponentExporter`和`ContainerExporter`接口，并使用`ModelFactory`在子组件上迭代并返回其模型表示形式。 请参阅以下资源：

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :Sling模型](https://sling.apache.org/documentation/bundles/models.html)

#### 如何禁用AEM 6.4调查弹出窗口？{#how-to-disable-aem-survey-pop-up}

您可以使用触屏UI或Web控制台来选择启用使用情况统计信息收集。 有关详细说明，请参阅[选择加入聚合使用统计信息集合](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

#### 是否有一个好资源重点介绍了升级到AEM 6.4的主要功能？{#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

请参阅[了解升级AEM的原因](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) ，其中介绍了考虑升级到最新版Adobe Experience Manager的客户的主要功能的高级划分。

## 资产 {#assets}

### 上传MP4文件（例如，使用拖放方法）时，资产工作流为何会重复？{#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

如果用户上传影片文件在资产节点下没有删除权限，则删除区块节点会失败，并且会重新启动上传。

#### 创建语言副本时，OOTB配置的默认设置是什么？{#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

当您通过触屏UI（**引用** -> **更新语言副本**）创建语言副本时，将使用新语言创建新的DAM文件夹，并且资产会从此处引用。

这是OOTB配置的默认设置。 在翻译配置中，您可以设置&#x200B;**翻译页面资产** = **不翻译**。
对于AEM 6.4,**工具** > **Cloud Services** > **翻译云服务**。

#### 如何禁用导致AEM SegmentStore(AEM 6.3.1.1)呈指数增长的AEM组件？{#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

您可以禁用OSGi组件禁用程序。 要使用此服务，请参阅[OSGi组件Disabler](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)。

作为解决方法，您还可以在每次重新启动AEM后，通过UI或通过`curl`命令（示例如下）手动禁用组件。

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### 如何自定义管理控制台？{#how-to-customize-admin-consoles}

AEM提供了各种机制，允许您自定义创作实例的控制台和页面创作功能。 要了解如何创建自定义控制台和自定义控制台的默认视图，请参阅[自定义控制台](/help/sites-developing/customizing-consoles-touch.md)。

#### 基于CoralUI 2和基于CoralUI 3的组件之间有何区别？{#what-is-the-difference-between-coralui-and-coralui-based-components}

为Coral3创建了一组新的Sling组件，该组件位于[/libs/granite/ui/components/coral/foundation下。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) 有一组用于基于CoralUI 2的组件，另一组用于基于CoralUI 3的组件。新集将不仅是旧集的复制粘贴，还将清理（例如，简化、删除已弃用的功能）。 因此，建议页面仅使用基于CoralUI 3的集合或基于CoralUI 2的集合。

要详细了解，请参阅[CoralUI 3-based](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)迁移指南。

#### 如何在AEM Assets中自定义搜索组件？{#how-to-customize-the-search-component-in-aem-assets}

要了解搜索提升/排名和进一步实施信息，请参阅[简单搜索实施指南](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)。

“简单搜索”实施是2017年Summit lab AEM Search Demystified中的材料。

#### 是否可以为WordPress构建插件，以允许客户访问Adobe资产选取器以选择图像？{#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

是的，使用WordPress的客户可以使用Adobe资产选取器从其AEM Assets服务器中选择图像，以将其添加到其WordPress网站上的帖子。

有关更多信息，请参阅[资产选择器](../assets/search-assets.md#assetpicker)。
