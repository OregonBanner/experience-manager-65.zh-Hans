---
title: Adobe Experience Manager 6.5 Service Pack 5的新增功能
description: Adobe Experience Manager 6.5 Service Pack 5的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 4%

---


# AEM 6.5 Service Pack 5的新增功能 {#aem-whats-new-service-pack-5}

Adobe Experience Manager 6.5服务包每季度向您提供新功能、客户请求的增强功能、性能和稳定性相关改进。 季度投放模型使得访问和采用新功能和创新变得更加容易。

本文重点介绍最新6.5 Service Pack包含的功 [能、先前6.5 Service Pack包含的主要功能](#key-features-previous-service-packs)，以及 [Experience Manager 6.5.4.0发布后的部分主要版本](#key-features-sice-sp3) 。

## AEM Sites {#aem-sites}

### 辅助功能改进 {#accessibility-sites}

* 通过添加文本信息改进错误报告

* 改进了键盘导航期间的UI焦点

* 改进的文本对比度（光度比）

* 改进了页面图像的替代属性的一致性

* 改进了可访问的富Internet应用程序(ARIA)标签的一致性

* 改进的非可视桌面访问(NVDA)功能

* 改进的屏幕阅读器支持

### 其他重要增强功能 {#other-enhancements-sites}

* 现在，在复制或粘贴页面树时，您可以选择粘贴根页面或将根页面与树的子页面一起粘贴。

* AEM Experience Fragments exported to Adobe Target workspaces now appear as unique offer types and offer sources in [!DNL Target].

* 多站点管理器——如果组件从源页面中删除，则发布触发器现在可成功从已发布页面中删除组件。

* 多站点管理器——当LiveCopy中的本地组件名称与蓝图中的组件名称相同且从蓝图中转出组件时，_msm_moved术语现已成功添加到本地组件的名称中。

## AEM Assets {#aem-assets}

### 资源中的辅助功能增强 {#assets-accessibility}

[!DNL Adobe Experience Manager] 资源功能现在符合Web内容可访问性准则(WCAG)更易于访问。 辅助功能在以下方面有所改进：

* 用户界面元素、控件、页面和对话框对屏幕阅读器友好。

* 用户界面元素、控件和输入表单字段可使用键盘访问。

* 某些图形的颜色和对比度的更改可由视觉有限且无颜色感知的用户区分。 例如，星级图标的颜色(如资产属性 [!UICONTROL 中] “高级”选 [!UICONTROL 项卡的] “评级 [!UICONTROL ”部分或] 卡视图中)会更改为适当的对比度。

![星级图标的颜色已更改以提高对比度](assets/star-rating-icons.png)

### 增强的异常处理 {#exception-handling}

资产用户界面流具有更好的异常处理。 早前，如果资产的维度没有正确类型，则会发现异常，该异常以静默方式捕获，日志中没有跟踪。 此行为已更改，所有异常都捕获在日志中。

## [!DNL Dynamic Media] {#dynamic-media}

### 3D支持 [!DNL Dynamic Media] {#support-for-3d}

现在，中的3D [!DNL Dynamic Media] 支持使客户能够发布3D内容并将3D内容添加到网页和应用程序。 它包括：

* 发布常用3D资产格式以生成资产URL。

* 使用查看器库（由Adobe Dimension提供支持）中提供的新3D Web查看器， [!DNL Dynamic Media] 交互式查看已发布的3D资产。

* 使用WCM组件在页 [!DNL Experience Manager Sites] 面上进行 [!DNL Sites] 3D发布和查看。

## AEM Forms {#aem-forms}

### 自定义AEM收件箱列 {#customize-aem-inbox-columns}

您可以自定义AEM收件箱，以更改列的默认标题、对列的位置重新排序，以及根据工作流的数据显示其他列。 您应是列的成 `administrators` 员或 `workflow-administrators` 组成员以自定义列。

![自定义AEM收件箱列](assets/customize-columns.gif)

### 将交互通信另存为草稿 {#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，稍后检索草稿以继续处理它。 您可以为每个草稿指定不同的名称，以便更容易识别。

![另存为草稿](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] 应用服务器支持 {#weblogic-support}

AEM Forms已添加对JEE [!DNL Oracle WebLogic 12] 上的AEM Forms的支持。 您可以从先前版本升级，或在12.2.1.4及更高版本的JEE服务器上 [!DNL Oracle WebLogic] 设置新的AEM 6.5 Forms。 稍后的版本更改与次要版本更改相对应，其中12.2.1.x中的x替换为版本号。

### 辅助功能改进 {#accessibility-improvements}

AEM Forms包含以下辅助功能增强：

* 当用户将自适应表单预览为HTML表单时，“涂 [!UICONTROL 抹签名] ”字段将保留选项卡焦点。

* 现在，提交自适应表单时显示的错误消息包含该 `aria-describedBy` 属性。 属性附加到错误消息中引用的字段。 属性 `aria-describedby` 指示描述该对象的元素的ID。 它有助于在构件或组与描述它们的文本之间建立关系。

* 如果自适应表单包含一些必填字段，则在ARIA辅助功能模式中，将 `True` 此类字段的必填属性设置为。

### 表单数据模型中基于X-509证书的基于SOAP的Web服务身份验证 {#x509-based-authentication-soap}

表单数据模型现在支持基于X-509证书的身份验证，同时使用SOAP Web服务作为数据源。

### 其他主要改进 {#other-improvements}

* JEE文档安全上的AEM 6.5表单现在基于 [!DNL Apache Struts 2]。

* 增加了对的 [!DNL Oracle Real Applications Cluster (RAC) 19c]支持。

## 先前AEM 6.5 Service Pack的主要功能 {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### 样式系统增强(6.5.4.0) {#style-system-enhancements}

您现在可以使用增强的样式系统在组件对话框中选择样式。

#### 不同方面的性能改进(6.5.4.0) {#performance-improvements}

* 缩短了在站点()中加载和初始化ContextHub的`contexthub.kernel.js`时间。 这样，在网站访问过程中页面加载速度会更快。

* 将体验片段拖动到站点页面编辑器后，可缩短刷新页面的时间。

* 缩短了“站点”页面上包含200个以上Live Copy概述的条目 **[!UICONTROL 的加载时间]**。

* 改进了对不完整或无效URL的处理。 此类URL会减慢模板编辑器的速度。

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

AEM资产与Brand Portal之间的授权渠道已更改。 以前，品牌门户通过旧版OAuth网关在经典UI中配置，该网关使用JWT令牌交换获得IMS访问令牌进行授权。 AEM资产现在通过Adobe I/O配置了Brand Portal,Adobe I/O为您的Brand Portal租户购买IMS令牌以授权。

根据AEM版本以及您是首次配置还是升级现有配置，使用Brand Portal配置AEM资产的步骤会有所不同。 有关详 [细信息，请参阅配置AEM资产与Brand](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) Portal。

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets包括以下辅助功能增强功能：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关详细信息，请参阅 [仅使用键盘键预览资源](../assets/managing-assets-touch-ui.md#previewing-assets)。

* 过滤器面板中的混合状态复选框（除非您选择所有嵌套的谓词，否则不会选择并遍历第一级复选框）可由屏幕阅读器读取。

* 日期和时间格式约束在日期字段的字段标签中提供，以使用户能够使用键盘以正确的格式输入日期。

   For example, `On Time (MM-DD-YYYY HH:mm)`. 这里，MM是两位数格式的月份，YYYY是年份，DD是两位数格式的日份，HH是24小时军事格式的小时，mm是分钟。

* 用 `X` 于删除当前选定标记的按钮上的符号现在由屏幕阅读器和选定标记的数量一起宣布。

#### AEM资产的可视搜索(6.5.2.0) {#visual-search}

资产用户可以直观地搜索相似图像。AEM 显示 DAM 存储库中与用户所选图像相似的智能标记图像。See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Dynamic Media的智能成像 {#smart-imaging}

智能成像使用每个用户独特的查看特性自动提供为其体验优化的正确图像，从而获得更好的性能和参与度。 智能成像可以与现有图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 请参 [阅智能成像](../assets/imaging-faq.md)。

#### Dynamic Media视频用户档案中的智能裁剪(6.5.3.0) {#smart-crop-video}

视频智能裁剪是视频用户档案中的一项可选功能，它是一款工具，可利用Adobe Sensei中人工智能的强大功能自动检测和裁剪您上传的任何自适应视频或渐进视频中的焦点，而不管其大小。 请参 [阅关于在视频用户档案中使用智能裁剪](../assets/video-profiles.md)。

### AEM Forms {#aem-forms-previous-service-packs}

#### 在AEM Forms工作流(6.5.4.0)中生成可打印输出 {#generate-printable-output}

使用“生成可打印输出”工作流步骤，您可以将源模板文件与数据文件集成。 此集成允许您打印或保存模板文件的不同副本。 该步骤生成PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 有关此功能的详细信息，请参 [阅OSGi上以表单为中心的工作流程——步骤参考](../forms/using/aem-forms-workflow-step-reference.md)。

![生成可打印输出](assets/generate-print-output-step.gif)

#### 在布局模式下支持自适应表单和交互式通信的多列(6.5.4.0) {#multi-column-adaptive-forms}

您现在可以通过自适应表单和交互式通信为面板定义列数。 切换到布局模式以使用新的多列选项。 有关详细信息，请参 [阅使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

![多列布局](assets/multi-column-layout.gif)

#### AEM收件箱自定义(6.5.4.0) {#aem-inbox}

新的“管理控制”选项使管理员能够：

* 自定义标题文本和徽标

* 控制标题中可用导航链接的显示

“管理员控制”选项仅对管理员或工作流管理员组的成员可见。 有关此功能的详细信息，请参 [阅您的收件箱](../sites-authoring/inbox.md)。

#### HTML5表单中的富文本支持(6.5.4.0) {#rich-text-support}

将XFA表单中的文本字段转换为HTML5表单中的富文本字段。 有关详细信息，请 [参阅设计HTML5表单的表单模板](../forms/using/designing-form-template.md)。

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms包括以下辅助功能增强功能：

* 屏幕阅读器在自适应表单中正确宣布复选框、链接、日期选取器和日期输入字段。

* 自适应表单的每页现在包含一个标题和一个主要地标标签。

#### 共享和请求对AEM Forms用户收件箱项目的访问权限(6.5.3.0) {#share-request-access}

您可以与其他用户共享您的收件箱项目。 当其他用户获得对您的收件箱项目的访问权限后，用户可以声明共享项目并采取相应操作。 同样，您也可以请求其他用户访问收件箱项目。 请参 [阅共享和请求对用户收件箱项目的访问权限](../forms/using/configure-shared-queues-osgi.md)。

#### 为AEM Forms用户(6.5.3.0)的收件箱项目配置办公室外设置 {#configure-out-of-office}

如果您计划离开办公室，您可以指定对分配给您的该期间的项目会发生什么情况。
您可以选择指定开始日期、时间以及结束日期和时间，以使您的离职设置生效。 您可以设置将所有项目发送给的默认人员。 请参 [阅配置外出设置](../forms/using/configure-out-of-office-settings.md)。

#### 使用AEM Forms的Batch API(6.5.3.0)生成多个交互式通信 {#generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 模板是无任何数据的交互式通信。 批处理API将数据与模板相结合以生成交互式通信。 API在大规模制作交互式通信中非常有用。 例如，电话单、多个客户的信用卡对帐单。 请参 [阅使用Batch API生成多个交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## AEM 6.5 SP4后的主要发行版 {#key-releases-since-last-sp}

在2020年3月5日至2020年6月4日之间，Adobe发布了下列AEM可交付内容之外的功能：

* AEM Cloud Manager [2020.3](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html).0 [、2020.4](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html).0 [和2020.5.0](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM资产： 桌面应用程序2.0.2.0](https://docs.adobe.com/content/help/zh-Hans/experience-manager-desktop-app/using/release-notes.html)

* [AEM Screens: 功能包202004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## 有用资源

* [AEM 6.5用户指南](../user-guide/home.md)

* [Adobe Experience Manager 6.5 的一般发行说明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack发行说明](sp-release-notes.md)
