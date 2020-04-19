---
title: Adobe Experience Manager 6.5 Service Pack 4的新增功能
description: Adobe Experience Manager 6.5 Service Pack 4的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Adobe Experience Manager 6.5 Service Pack 4的新增功能 {#aem-whats-new-service-pack-4}

Adobe Experience Manager(6.5)使您能通过Service Pack季度发行版获得新功能和持续改进。 使用这种方法，您可以轻松地采用创新。

Experience Manager Service Pack 4(6.5.4.0)是重要更新。 它包含自2019年4月AEM 6.5发布以来发布的所有新增功能、关键客户请求的增强功能、性能、稳定性和安全性改进。 您可以在AEM 6.5和更高版本上安装服务包。

本文重点介绍最新6.5 Service Pack中包含的功能、以 [前6.5 Service Pack中包含的主要功能](#key-features-previous-service-packs)，以及Experience Manager 6.5.3.0之后的一些 [主要版本](#key-features-sice-sp3)。

## AEM Sites {#aem-sites}

### 样式系统增强

您现在可以使用增强的样式系统在组件对话框中选择样式。

### 不同方面的性能改进 {#performance-improvements}

* 缩短了在站点()中加载和初始化ContextHub的时`contexthub.kernel.js`间。 这样，在网站访问过程中页面加载速度会更快。

* 将体验片段拖动到站点页面编辑器后，可缩短刷新页面的时间。

* 缩短了“站点”页面上包含超过200个Live Copy概述的条目的加 **[!UICONTROL 载时间]**。

* 改进了对不完整或无效URL的处理。 此类URL会减慢模板编辑器的速度。

## AEM Assets {#aem-assets}

### 使用Brand Portal配置AEM资产 {#configure-assets-bp}

AEM资产与Brand Portal之间的授权渠道已更改。 以前，Brand Portal是通过旧版OAuth网关在经典UI中配置的，该网关使用JWT令牌交换获得IMS访问令牌进行授权。 AEM资产现在通过Adobe I/O配置了Brand Portal，后者为Brand Portal租户购买IMS令牌以授权。

根据AEM版本以及您是首次配置还是升级现有配置，配置带有Brand Portal的AEM资产的步骤会有所不同。 有关详 [细信息，请参阅配置AEM资产与Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) 。


### 已知问题 {#known-issues-bp}

* 在AEM 6.5.4上升级到Adobe I/O后，Brand Portal用户无法将贡献文件夹资产发布到AEM资产。

### Accessibility enhancements {#accessibility-enhancements}

Experience Manager资产包括以下辅助功能增强：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关详细信息，请参阅 [仅使用键盘键预览资源](../assets/managing-assets-touch-ui.md#previewing-assets)。

* 过滤器面板中的混合状态复选框（除非您选择所有嵌套的谓词，否则不会选择并遍历第一级复选框）可由屏幕阅读器读取。

* 日期和时间格式约束在日期字段的字段标签中提供，以使用户能够使用键盘以正确的格式输入日期。

   For example, `On Time (MM-DD-YYYY HH:mm)`. 这里，MM是两位数格式的月份，YYYY是年份，DD是两位数格式的日份，HH是24小时军用格式的小时，mm是分钟。

* 用于 `X` 删除当前选定标记的按钮上的符号现在由屏幕阅读器和选定标记的数量一起宣布。

## AEM Forms {#aem-forms}

### 在AEM Forms工作流中生成可打印输出 {#generate-printable-output}

使用“生成可打印输出”工作流步骤，可以将源模板文件与数据文件集成。 此集成允许您打印或保存模板文件的不同副本。 该步骤生成PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 有关此功能的详细信息，请参 [阅OSGi上以表单为中心的工作流——步骤参考](../forms/using/aem-forms-workflow-step-reference.md)。

![生成可打印输出](assets/generate-print-output-step.gif)

### 在布局模式下支持自适应表单和交互式通信的多列 {#multi-column-adaptive-forms}

您现在可以在自适应表单和交互式通信中为面板定义列数。 切换到布局模式以使用新的多列选项。 有关详细信息，请参 [阅使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

![多列布局](assets/multi-column-layout.gif)

### AEM收件箱自定义 {#aem-inbox}

新的“管理控制”选项使管理员能够：

* 自定义标题文本和徽标

* 控制标题中可用导航链接的显示

“管理控制”选项仅对管理员或工作流管理员组的成员可见。 有关此功能的详细信息，请参阅您 [的收件箱](../sites-authoring/inbox.md)。

### HTML5表单中的富文本支持 {#rich-text-support}

将XFA表单中的文本字段转换为HTML5表单中的富文本字段。 有关详细信息，请参 [阅设计HTML5表单的表单模板](../forms/using/designing-form-template.md)。

### Accessibility enhancements {#forms-accessibility-enhancements-6540}

Experience Manager Forms包括以下辅助功能增强：

* 屏幕阅读器在自适应表单中正确宣布复选框、链接、日期选取器和日期输入字段。

* 自适应表单的每页现在包含一个标题和一个主要地标标签。

## 以前的AEM 6.5 Service Pack中的主要功能 {#key-features-previous-service-packs}

### 动态媒体智能成像 {#smart-imaging}

智能成像使用每个用户的独特查看特性自动提供为其体验优化的正确图像，从而提高性能和参与度。 智能成像可以与现有图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅 [智能成像](../assets/imaging-faq.md)。

### Dynamic Media视频用户档案中的智能裁剪(6.5.3.0) {#smart-crop-video}

视频智能裁剪是视频用户档案中的一项可选功能，它是一款工具，它使用Adobe Sensei中人工智能的强大功能自动检测和裁剪您上传的任何自适应视频或渐进视频中的焦点，而不管大小。 请参 [阅关于在视频用户档案中使用智能裁剪](../assets/video-profiles.md)。

### AEM资产的可视搜索(6.5.2.0) {#visual-search}

资产用户可以直观地搜索相似图像。AEM 显示 DAM 存储库中与用户所选图像相似的智能标记图像。See [Visual search](../assets/search-assets.md).

### 共享并请求对AEM Forms用户收件箱项目的访问权限(6.5.3.0) {#share-request-access}

您可以与其他用户共享您的收件箱项目。 当其他用户获得对您的收件箱项目的访问权时，用户可以声明共享项目并采取相应的操作。 同样，您也可以请求其他用户访问收件箱项目。 请参 [阅共享和请求对用户收件箱项目的访问权限](../forms/using/configure-shared-queues-osgi.md)。

### 为AEM Forms用户(6.5.3.0)的收件箱项目配置办公室外设置 {#configure-out-of-office}

如果您计划离开办公室，则可以指定在该期间分配给您的项目会发生什么情况。
您可以选择指定开始日期和时间以及结束日期和时间，以使您的离职设置生效。 您可以设置将所有项目发送到的默认人员。 请参 [阅配置办公室外设置](../forms/using/configure-out-of-office-settings.md)。

### 使用AEM Forms的Batch API(6.5.3.0)生成多个交互式通信 {#generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 该模板是无任何数据的交互式通信。 Batch API将数据与模板相结合，以生成交互式通信。 该API在大规模制作交互式通信中很有用。 例如，电话单、多个客户的信用卡对帐单。 请参 [阅使用Batch API生成多个交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## 自AEM 6.5 SP3以来的主要发行版 {#key-features-since-sp3}

在2019年12月12日至2020年3月5日之间，Adobe发布了下列AEM可交付内容以外的功能：

* AEM Cloud Manager 2020.1.0和2020.2.0

   改进管道状态以及下载不同步骤的日志的能力。 请参阅：

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-2-0.html)


* AEM Cloud Manager CLI更新

   使用命令行工具实现Cloud Manager任务自动化。 请参 [阅GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEM Sites:Project Archetype 23

   开始新AEM项目的最佳方式。 Archetype 23将SPA和常规站点的 [Project Archetype合并为一个](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) ，并提供一个默认主题来启动前端开发开始。

* AEM Sites:WKND参考站点

   [新的参考项目](https://www.wknd.site/) ，其中包含有关如何使用AEM构建站点的最佳实践。 阅读更新的 [WKND教程，了解更多信息](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)。 您可以从 [GitHub获取最新代码](https://github.com/adobe/aem-guides-wknd/releases)。

* AEM Sites:商务CIF核心组件0.7.0和0.9.0

   将AEM Sites与Magento Commerce集成。 请参 [阅扩展专用的核心组件和项目原型，重点关注商务](https://github.com/adobe/aem-core-cif-components/releases)。

* AEM资产：桌面应用程序2.0.1.1

   请参 [阅获取对资产的桌面访问](https://docs.adobe.com/content/help/zh-Hans/experience-manager-desktop-app/using/release-notes.html)。

* AEM Screens:功能包202001

   直接从AEM内的数字标牌。 安装最新功能包的改进功能， [跨多媒体播放器实现同步播放](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)。

## 有用资源

* [AEM 6.5用户指南](../user-guide/home.md)

* [Adobe Experience Manager 6.5 的一般发行说明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack发行说明](sp-release-notes.md)
