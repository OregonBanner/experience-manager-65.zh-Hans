---
title: Adobe Experience Manager 6.5 Service Pack 4的新增功能
description: Adobe Experience Manager 6.5 Service Pack 4的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed756d785864131c2e031aec4331388bc057576b

---


# Adobe Experience Manager 6.5 Service Pack 4的新增功能 {#aem-whats-new-service-pack-4}

Adobe Experience Manager(AEM)6.5今年通过季度Service Pack提供功能并不断改进。 新方法使我们的客户能够更快地采用创新。

最新的AEM Service Pack 4(6.5.4.0)将于2020年3 **月5日发布**。 本文重点介绍了最新Service Pack提供的功能，以使您的AEM旅程更加丰富。

## AEM Sites {#aem-sites}

### 不同方面的性能改进 {#performance-improvements}

* 缩短了在站点(contexthub.kernel.js)中加载和初始化ContextHub的时间。 这样，在网站访问过程中页面加载速度会更快。

* 将体验片段拖放到站点页面编辑器后，可缩短刷新页面的时间。

* 缩短了在Live Copy概述中为包含200多个Live Copy的“站点”页面加载条目的时间。

* 改进了对不完整或无效URL的处理。 此类URL会减慢模板编辑器的速度。

此外，AEM 6.5.4.0还包含样式系统增强功能。 您现在可以在组件对话框中选择样式。

## AEM Assets {#aem-assets}

### 通过Adobe I/O Console与Brand Portal集成 {#assets-integration-bp}

您现在可以通过Adobe I/O控制台配置带有Brand Portal的AEM资产。 Adobe I/O Console为Brand Portal租户购买IMS令牌以授权。 以前，AEM资产通过旧版OAuth网关在经典UI中配置了品牌门户。 在2020年4月6日之前，将支持使用传统OAuth网关的配置。 如果不修改集成，则现有配置将继续工作。

您可以创建新集成或将集成设置升级到Adobe I/O控制台。

### Accessibility enhancements {#accessibility-enhancements}

Experience Manager资产包括以下辅助功能增强：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关详细信息，请参阅 [仅使用键盘键预览资源](../assets/managing-assets-touch-ui.md#previewing-assets)。

* “筛选器”面板中的混合状态复选框（除非您选择所有嵌套谓词，否则不会选择第一级复选框，并将其删除）可由屏幕阅读器读取。

* 日期和时间格式约束在日期字段的字段标签中提供，以使用户能够使用键盘以正确的格式输入日期。

   For example, `On Time (MM-DD-YYYY HH:mm)`. 这里，MM是两位数格式的月份，YYYY是年份，DD是两位数格式的日份，HH是24小时军用格式的小时，mm是分钟。

* 用于 `X` 删除当前选定标记的按钮上的符号现在由屏幕阅读器和选定标记的数量一起宣布。

## AEM Forms {#aem-forms}

### 在AEM Forms工作流程中生成可打印输出 {#generate-printable-output}

如果您希望解决方案打印或保存源模板文件的多个副本并将其与具有大量记录的数据文件集成，AEM Forms中将提供新的“生成可打印输出”工作流步骤。 例如，如果要在每次打印源表单时打印其名称不同的表单，则可以在数据文件中具有这些名称，并将其与标准模板文件集成。

充分利用此功能，使用“工 **具** ”>“工作流 **[!UICONTROL ”]** >“模型 **[!UICONTROL ”]********** >“创建并创建模型”，然后对“可打印输出”工作流步骤生成可打印的搜索。

![生成可打印输出](assets/generate-print-output-demo.gif)

有关此功能的详细信息，请参 [阅OSGi上以表单为中心的工作流——步骤参考](../forms/using/aem-forms-workflow-step-reference.md)。

### 在布局模式下支持自适应表单和交互式通信的多列 {#multi-column-adaptive-forms}

您现在可以在自适应表单和交互式通信中为面板定义列数。

可通过切换到布局模式来查找新选项。 点按要转换为多列格式的面板，选择其父项，然后点按多列图标，以定义该面板的列数。

![多列布局](assets/multi-column-layout.gif)

有关详细信息，请参 [阅使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

### AEM收件箱自定义 {#aem-inbox}

您是否曾感到需要自定义AEM标题中的可用选项？ 现在，通过引入“管理控制”选项，我们的新Service Pack版本可 **[!UICONTROL 以实现]** 。

**自定义标题文本**

工作流管理员现在可以指定您自己选择的标题文本。

您可以在视图选择器( **[!UICONTROL 工具栏右上角提供]** )>管理控制下找到新的自定义标题文 **[!UICONTROL 本选项]**。

**自定义徽标**

与自定义标题文本类似，工作流管理员现在可以指定您自己选择的标题标志。

您可以在视图选择器> **[!UICONTROL Admin Control下找到新的自定]** 义徽标 ****。

有关此功能的详细信息，请参阅您 [的收件箱](../sites-authoring/inbox.md)。

### 用户导航控件 {#user-navigation-control}

工作流管理员现在可以选择让用户基于角色在受限模式下处理AEM。 管理员可以控制标题中可用导航选项的显示，以限制用户切换到工作流创作模式或其他解决方案链接。

查看视图选择器> **[!UICONTROL Admin Control下的]** “隐藏”导航 **[!UICONTROL 选项]**。

有关此功能的详细信息，请参阅您 [的收件箱](../sites-authoring/inbox.md)。

### HTML5表单中的富文本支持 {#rich-text-support}

文本字段现在可以在呈现的HTML5表单中显示格式选项列表。 您必须为Forms Designer中的文本字段定义一种格式，才能将相应的设置应用于该字段。

要使用此功能，请点按Forms Designer中“设计” **[!UICONTROL 视图中的]** “文本”字段。 在“字 **[!UICONTROL 段]** ”选项卡中，从“字段格式”下拉列表中选择“富文本 ******** ”以应用这些设置。

有关详细信息，请参 [阅设计HTML5表单的表单模板](../forms/using/designing-form-template.md)。

## 主要亮点

除了新增功能外，AEM 6.5 Service Pack 4还包含以下主要亮点：

* 您现在可以将选择性内容子树同 *步到Dynamic Media - Scene7模式* ，而不是所有可在上使用的子树 `content/dam`。

* 与SOAP Web服务的表单数据模型集成现在支持元素上的选择组或属性。

* SOAP输入或输出以及复杂的数据结构现在支持动态组替换。

## 以前的AEM 6.5 Service Pack中的主要功能

### 动态媒体智能成像 {#smart-imaging}

智能成像利用每个用户的独特查看特性自动提供针对其体验优化的正确图像，从而提高性能和参与度。 智能成像可以与现有图像预设配合使用，并在传送的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅 [智能成像](../assets/imaging-faq.md)。

### AEM资产的可视搜索 {#visual-search}

资产用户可以直观地搜索相似图像。AEM 显示 DAM 存储库中与用户所选图像相似的智能标记图像。See [Visual search](../assets/search-assets.md).

### 共享和请求对用户收件箱项目的访问权限 {#share-request-access}

您可以与其他用户共享您的收件箱项目。 在其他用户可以访问您的收件箱项目后，用户可以声明共享项目并采取相应的操作。 同样，您也可以请求其他用户访问收件箱项目。 请参 [阅共享和请求对用户收件箱项目的访问权限](../forms/using/configure-shared-queues-osgi.md)。

### 为收件箱项目配置离职设置 {#configure-out-of-office}

如果您计划离开办公室，则可以指定在该期间分配给您的项目会发生什么情况。
您可以选择指定开始日期、时间以及结束日期和时间，以使您的离职设置生效。 您可以设置将所有项目发送到的默认人员。 请参 [阅配置办公室外设置](../forms/using/configure-out-of-office-settings.md)。

### 使用Batch API生成多个交互式通信 {#generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 该模板是无任何数据的交互式通信。 Batch API将数据与模板相结合，以生成交互式通信。 该API在大规模制作交互式通信中很有用。 例如，电话单、多个客户的信用卡对帐单。 请参 [阅使用Batch API生成多个交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

### 自适应表单的标准验证错误消息 {#standard-validation}

自适应表单现在可以与自定义服务集成以执行数据验证。 如果输入值不满足验证条件并且服务器返回的验证错误消息为标准消息格式，则错误消息在表单的字段级别显示。 如果输入值不满足验证标准并且服务器验证错误消息不是标准消息格式，自适应表单提供将验证错误消息转换为标准格式以便它们在表单的字段级别显示的机制。 请参 [阅自适应表单的标准验证错误消息](../forms/using/standard-validation-error-messages-adaptive-forms.md)。

## 自AEM 6.5 SP3以来的主要发行版

在2019年12月12日至2020年3月5日之间，Adobe发布了下列AEM可交付内核以外的功能：

* AEM Cloud Manager 2020.1.0和2020.2.0对Cloud Manager的月度改进，最后两个版本侧重于改进管道状态和下载不同步骤的日志的能力。 请阅读此处的完整发行说明：
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* AEM Cloud Manager CLI更新——使用命令行工具自动执行Cloud Manager任务。 我们不断扩展CLI —— 在 [GitHub上加入](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEM Sites:Project Archetype 23启动新AEM项目的最佳方式。 借助Archetype 23，我们将 [SPA和常规站点的Project Archetype合并为一个](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23)，进一步提供一个默认主题以启动您的前端开发。

* AEM Sites:WKND参考站点全 [新参考项目](https://www.wknd.site/) ，其中包含有关如何使用AEM构建站点的最佳实践。 阅读完全更新的 [WKND教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) ，并从 [GitHub获取代码，了解更多信息](https://github.com/adobe/aem-guides-wknd/releases)。

* AEM Sites:Commerce CIF Core Components 0.7.0和0.9.0Integrating AEM Sites and Magento Commerce. 我们不断扩 [展专用的核心组件和项目原型，重点关注商务](https://github.com/adobe/aem-core-cif-components/releases)。

* AEM资产：桌面应用程序2.0.1.1
   [在桌面上访问资源](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens:功能包202001直接从AEM内的数字标牌。 利用最新的功能包获得最新改进，这次我们支持 [跨多媒体播放器同步播放](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)。

## 有用资源

* [AEM 6.5用户指南](../user-guide/capabilities.md)

* [Adobe Experience Manager 6.5 的一般发行说明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack发行说明](sp-release-notes.md)
