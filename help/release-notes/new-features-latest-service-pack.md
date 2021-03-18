---
title: ' [!DNL Experience Manager] 6.5 Service Pack 8中的新增功能'
description: ' [!DNL Experience Manager] 6.5 Service Pack 8的新增功能'
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: f52fc643c30babab68bcf122eb3d91da5ce37a24
workflow-type: tm+mt
source-wordcount: '3015'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack 8 {#aem-whats-new-service-pack}中的新增功能

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack每季度提供一次新功能、客户要求的增强功能以及性能、稳定性和安全性改进。每季度提供一次，便于访问和采用新功能和创新。

本文重点介绍最新Service Pack中包含的功能、前6.5 Service Pack](#key-features-previous-service-packs)中包含的[主要功能以及自上次Service Pack](#key-releases-since-last-sp)发行版以来的[主要发行版。

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### 对可用于转出{#sort-livecopy-pages}的Live Copy页面进行排序

您现在可以使用[!UICONTROL 名称]、[!UICONTROL 上次修改日期]和[!UICONTROL 上次转出日期]属性对可用于转出的Live Copy页面进行排序。 页面的[!UICONTROL 上次转出日期]是此版本中引入的新属性。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* 使用[已连接资产功能](/help/assets/use-assets-across-connected-assets-instances.md)时，您现在可以视图使用该资产的所有[!DNL Sites]页面的列表。 资产的[!UICONTROL 属性]页面中提供了对资产的这些引用。 这使管理员、营销人员和图书管理员能够对资产使用情况进行完整的视图，从而实现更好的跟踪、管理和品牌一致性。

* 删除在网页中引用的资产时，[!DNL Experience Manager]会显示警告。 您可以强制删除引用的资产，或者检查并修改资产[!DNL Properties]页面中显示的引用。 单击引用可打开本地和远程[!DNL Sites]页。

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>计划的[!DNL Experience Manager] Service Pack版本发布一周后，将提供[!DNL Experience Manager Forms]的附加程序包。

### 根据规则{#show-hide-captcha}在自适应表单中显示或隐藏CAPTCHA组件

您现在可以在自适应表单提交或用户操作时验证CAPTCHA。 您还可以添加条件以验证用户操作的CAPTCHA，并基于规则在自适应表单中显示或隐藏CAPTCHA组件。

### 添加自定义CAPTCHA服务{#add-custom-captcha-services}

[!DNL Experience Manager Forms] 提供开箱即用支持，以将Google reCAPTCHA（需要Google reCAPTCHA API的单独许可证）用作CAPTCHA验证服务。您还可以使用自定义CAPTCHA服务验证CAPTCHA。

### 其他增强功能 {#other-enhancements-forms-6580}

* 改进了[!DNL Experience Manager Forms]日期选取器组件的可访问性。

* 增加了使用PrintChannel API以PCL格式生成交互式通信的支持。

* 执行PDFG转换时，您现在可以启用或禁用[!DNL Experience Manager Forms]注册表更改以生成自定义书签。

## 以前[!DNL Experience Manager] 6.5 Service Pack {#key-features-previous-service-packs}中的主要功能

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### 页面移动和MSM转出的可用性作为异步操作(6.5.7.0){#page-moves-msm-asynchronous}

您现在可以将页面移动和MSM转出作为异步操作来执行，以减少它们对运行时性能的影响。 您可以计划操作以立即或稍后执行。 关联的作业和进程步骤的状态显示在控制台中，这有助于监视大规模MSM推出。

#### 在异步模式(6.5.6.0){#page-move-asynchronous}中可用的页面移动操作

页面移动操作现在在异步模式下可用。 除了立即执行，您还可以计划页面移动操作以便以后执行。

#### 辅助功能改进(6.5.5.0){#accessibility-sites}

* 通过添加文本信息改进了错误报告。

* 改进了键盘导航期间的用户界面焦点。

* 改进了各种用户界面元素的对比度。

* 改进了页面图像的替代属性的一致性。

* 改进了可访问的富Internet应用程序(ARIA)标签的一致性。

* 改进了非可视桌面访问(NVDA)功能。

* 改进了屏幕阅读器支持。

#### 其他关键增强功能(6.5.5.0){#other-enhancements-sites}

* 不允许匿名访问CRXDE Lite以增强安全性。 相反，用户将被定向到登录屏幕。 请参阅[使用CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)进行开发。

* 现在，在复制或粘贴页面树时，您可以选择粘贴根页面或用树的子页面粘贴根页面。

* [!DNL Adobe Experience Manager Experience Fragments] 导出到工 [!DNL Adobe Target] 作区时，现在在中显示为唯一的优惠类型和优惠 [!DNL Target]源。

* 多站点管理器 — 如果某个组件从源页面中删除，则发布触发器现在会从已发布页面中删除该组件。

* 多站点管理器 — 当[!UICONTROL Live Copy]中的本地组件名称与Blueprint中的组件名称相同且组件从Blueprint中转出时，术语`_msm_moved`现在将添加到本地组件的名称中。

#### 样式系统增强(6.5.4.0){#style-system-enhancements}

您现在可以使用增强的样式系统在组件对话框中选择样式。

#### 各个方面的性能改进(6.5.4.0){#performance-improvements}

* 缩短了在站点(`contexthub.kernel.js`)中加载和初始化ContextHub的时间。 这样，在网站访问过程中页面加载速度会更快。

* 将[!DNL Experience Fragments]拖动到[!DNL Sites]页面编辑器后，可缩短刷新页面的时间。

* 缩短了[!DNL Sites]页面上条目的加载时间，**[!UICONTROL Live Copy概述]**&#x200B;中包含200多个Live Copy。

* 改进了对不完整或无效URL的处理。 此类URL会减慢模板编辑器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* [!DNL Assets] 并提供 [!DNL Dynamic Media] 多个辅助功能增强。这些增强功能与键盘导航、屏幕阅读器的使用、启用辅助技术(AT)的类似增强功能相关。 请参阅[[!DNL Assets] enhancements](/help/release-notes/sp-release-notes.md#assets-6570)和[[!DNL Dynamic Media] enhancements](/help/release-notes/sp-release-notes.md#dynamic-media-6570)(6.5.7.0)

* 用户可以在卡片和列视图(6.5.7.0)中对数字资产进行排序。

#### 辅助功能增强(6.5.6.0){#accessibility-assets-6560}

* **增强的用户界面在键盘导航期间的焦点**，例如，侧重于：

   * `x` 图标 [!UICONTROL ,] 查看资产 。

   * 可操作的用户界面选项。

   * [!UICONTROL “共享链接]”对话框上的“电子邮件”字段，以及用于在文件夹[!UICONTROL 属性]的[!UICONTROL 权限]选项卡中添加已关闭的用户组的字段。

* **使用键盘键的增强功能**

   用户可以使用键盘键在屏幕阅读器的浏览模式下拖动元数据模式表单编辑器中的控件。

* **由于以下原因**，屏幕阅读器用户增强了可用性：

   * 屏幕阅读器会宣布视频和音频播放器的用途。

   * 屏幕阅读器会宣布用户界面选项的用途，即删除使用资产[!UICONTROL 属性]上的[!UICONTROL 标记选择对话框]选择的标记。

   * 屏幕阅读器将宣布表的行标题和行项，以便用户了解哪些条目属于同一行。

   * 搜索页面的描述性和有意义的页面标题。

   * 屏幕阅读器将搜索筛选器面板中的选项宣布为可扩展的折叠。

#### [!DNL Assets](6.5.6.0){#other-enhancements-assets-6560}中的其他增强功能

* 与文件夹（私有和非私有）关联的用户组现在会在[删除这些文件夹](/help/assets/private-folder.md#delete-private-folder)时从存储库中删除。 但是，可以使用JMX从存储库中删除现有的冗余、孤立、未使用和自动生成的用户组。

#### [!DNL Assets](6.5.5.0){#assets-accessibility}中的辅助功能增强

[!DNL Experience Manager Assets] 现在可根据Web内容辅助功能准则(WCAG)更方便地访问。辅助功能因以下增强而有所改进：

* 许多用户界面元素、控件、页面和对话框都是屏幕阅读器友好的。

* 许多用户界面元素、控件和输入表单域都可通过键盘访问。

* 某些用户界面元素的颜色和对比度已更新，以便视力有限和不能感知颜色的用户能够区分这些用户界面元素。例如，对于适当的对比度，星级图标的颜色(如资产[!UICONTROL 属性]或卡视图中[!UICONTROL 高级]选项卡的[!UICONTROL Rating]部分)会发生更改。

   ![对比度得到提高的分级图标](assets/star-rating-icons.png)

#### 增强的异常处理(6.5.5.0){#exception-handling}

[!DNL Assets] 用户界面流具有更好的异常处理。如果资产的维度没有类型，则在日志文件中记录观察到的异常。

#### 支持[!DNL Dynamic Media](6.5.5.0){#support-for-3d}中的3D资源

[!DNL Dynamic Media]中对3D图像的支持使客户能够发布3D内容并将其添加到网页和应用程序。 支持包括：

* 发布常见的3D资产格式并生成可在网页和其他应用程序中使用的资产URL。

* 由[!DNL Adobe Dimension]提供支持的3D Web查看器，可交互视图已发布的3D资源。

* 使用[!DNL Sites] WCM组件在[!DNL Experience Manager Sites]页面上发布和视图常见的3D资产。

#### 使用[!DNL Brand Portal](6.5.4.0){#configure-assets-bp}配置[!DNL Experience Manager Assets]

[!DNL Experience Manager Assets]和[!DNL Brand Portal]之间的授权渠道已更改。 以前，[!DNL Brand Portal]是通过旧版OAuth网关在经典UI中配置的，该网关使用JWT令牌交换获取IMS访问令牌以进行授权。 [!DNL Experience Manager Assets] 现在配置为 [!DNL Brand Portal] through [!DNL Adobe I/O] ，后者为您的租户获取IMS令牌进行 [!DNL Brand Portal] 授权。

根据您的[!DNL Experience Manager]版本以及您是首次配置还是升级现有配置，将[!DNL Experience Manager Assets]配置为[!DNL Brand Portal]的步骤有所不同。 有关详细信息，请参阅[配置Experience Manager资产与Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)。

#### 辅助功能增强(6.5.4.0){#accessibility-enhancements}

[!DNL Experience Manager Assets] 包括以下辅助功能增强功能：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关详细信息，请参阅[仅使用键盘键预览资源](../assets/manage-assets.md#previewing-assets)。

* 屏幕阅读器可读取“过滤器”面板中的混合状态复选框（除非您选择所有嵌套谓词，否则不会选择并穿透第一级复选框）。

* 日期和时间格式约束在日期字段的字段标签中提供，以便用户使用键盘以正确的格式输入日期。
例如，`On Time (MM-DD-YYYY HH:mm)`。 此处MM为两位数格式的月份，YYYY为年份，DD为两位数格式的日，HH为24小时军用格式的小时，mm为分钟。

* 屏幕阅读器将宣布删除选定标记（`X`符号）和选定标记数的选项。

#### 可排序列，用于在列表视图(6.5.3.0){#sortable-date-created-column}中创建资产的日期

在DAM列表视图中，将为资产的创建日期添加一个新的可排序列，并在列表视图中对资产搜索结果进行排序。

![创建日期的可排序列](assets/asset-created-date.png)

#### 可视搜索[!DNL Adobe Experience Manager Assets](6.5.2.0){#visual-search}

[!DNL Assets] 用户可以搜索视觉上相似的图像。Experience Manager显示来自DAM存储库的智能标记图像，该图像与用户选择的图像类似。 请参阅[可视搜索](../assets/search-assets.md)。

### Dynamic Media {#dynamic-media-previous-service-packs}

#### 使CDN缓存内容(6.5.6.0){#invalidate-cdn-cached-content}无效

您现在可以使用[!DNL Dynamic Media]用户界面使内容投放网络(CDN)缓存内容失效。 因此，更新后的资产会立即可用，而不是等待缓存过期。 可以通过以下方式使CDN失效：

* 创建CDN失效模板：选择资产和表单关联的基于模板的URL

* 通过资产选取器选择资产和关联的预设

* 添加完整的资产URL

#### 选择性将资源发布到[!DNL Experience Manager]和[!DNL Dynamic Media](6.5.6.0){#selective-publishing}

您现在可以选择使用[!UICONTROL 快速发布]或[!UICONTROL 管理发布]向导，选择性地将资产发布或取消发布到[!DNL Experience Manager]或[!DNL Dynamic Media]。 您还可以在文件夹级别设置`Publish`或`Unpublish`模式。

#### Dynamic Media的智能成像{#smart-imaging}

智能图像处理使用每个用户的独特查看特性自动提供为其体验优化的正确图像，从而获得更好的性能和参与度。 智能成像功能可以与您现有的图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅[智能成像](../assets/imaging-faq.md)。

#### 针对Dynamic Media(6.5.3.0){#smart-crop-video}的视频用户档案中的智能裁剪

视频智能裁剪是视频用户档案中的一项可选功能，它是一款工具，可使用Adobe Sensei中人工智能的强大功能自动检测和裁剪您上传的任何自适应视频或渐进式视频中的焦点，而不管其大小。 请参阅[关于在视频用户档案中使用智能裁剪](../assets/video-profiles.md)。

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### 性能改进(6.5.7.0){#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms提高了以下产品的性能：

* 在提交自适应表单时验证服务器上的字段值。

* 使用[!DNL Automated Forms Conversion service]将PDF表单转换为自适应表单。

#### 表单数据模型HTTP客户端配置以优化性能(6.5.7.0){#fdm-http-client-config}

[!DNL Experience Manager Forms] 与RESTful web服务作为数据源集成时的表单数据模型现在包括用于性能优化的HTTP客户端配置。请参阅[配置数据源](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration)。

#### 在布局模式(6.5.7.0){#reset-option-layout-mode}中，每个组件的重置选项可用性

您现在可以在自适应表单的布局模式中为每个组件使用重置选项。 为面板定义多列布局时，可以使用此功能重置面板中的各个组件。 请参阅[使用布局模式调整组件大小](../../help/forms/using/resize-using-layout-mode.md#resize-components)。

#### 在客户端预填自适应表单(6.5.6.0){#prefill-merge-data-at-client}

预填自适应表单时，[!DNL Experience Manager Forms]服务器将数据与自适应表单合并，并将填写的表单发送给您。 默认情况下，数据合并操作在服务器上进行。
您现在可以将[!DNL Experience Manager Forms]服务器配置为[在客户端](../../help/forms/using/prepopulate-adaptive-form-fields.md)而不是服务器上执行数据合并操作。 它显着缩短了预填和渲染自适应表单所需的时间。

#### 在具有双向SSL实现(6.5.6.0){#fdm-integration-rest-apis-two-way-ssl}的服务器上与RESTful API进行表单数据模型集成

[!DNL Experience Manager Forms] 表单数据模型现在可 [以与服务器上的RESTful API集成，该服务器上实现了双向SSL](../../help/forms/using/configure-data-sources.md)。

#### 增加了对Automated forms conversion服务(6.5.6.0){#sign-integration-acroform-afcs}中[!DNL Adobe Sign]文本标记的支持

如果AcroForm包含[!DNL Adobe Sign]文本标记，则这些字段现在在使用[!DNL Automated Forms Conversion service]转换的自适应表单中被识别并表示为[!DNL Adobe Sign]字段。 签名者可以在签名自适应表单时填写此类字段。

#### 支持将彩色PDF forms转换为自适应表单(6.5.6.0){#colored-PDF-forms}

可以使用[!DNL Automated Forms Conversion service]将彩色PDF forms转换为自适应表单。

#### 支持SMB 2和SMB 3协议(6.5.6.0){#smb-support}

[!DNL Experience Manager Forms] 现在支持SMB 2和SMB 3协议。

#### 增强了已转换的自适应表单页面的缓存(6.5.6.0){#enhanced-caching-translated-adaptive-forms}

现在可以将[区域设置指定为自适应表单URL中的选择器，而不是自适应表单URL](../../help/forms/using/supporting-new-language-localization.md)中的参数。 它有助于在[!DNL Experience Manager Dispatcher]上缓存已转换的自适应表单。 在以前版本中无法缓存已翻译的自适应表单。 有关配置缓存以在自适应表单URL中将区域设置用作选择器的详细信息，请参阅[在调度程序](../../help/forms/using/configure-adaptive-forms-cache.md)处配置自适应表单缓存。

#### 将表单数据模型服务的输出保存到变量(6.5.6.0){#save-fdm-service-to-variable}

表单数据模型允许您将表单数据模型服务的输出保存到变量。 [!DNL Experience Manager Forms] 现在自动将表单数据模型服务的类型映射到变量的类型。

#### 为文件附件组件(6.5.6.0){#attach-multiple-files}附加多个文件

您现在可以[将多个文件](../../help/forms/using/introduction-forms-authoring.md)附加到自适应表单的[!UICONTROL 文件附件]组件。

#### 自定义Adobe Experience Manager收件箱列(6.5.5.0){#customize-aem-inbox-columns}

您可以自定义[!DNL Experience Manager]收件箱以更改列的默认标题、对列的位置重新排序并根据工作流的数据显示其他列。 `administrators`或`workflow-administrators`组的成员可以自定义列。 有关详细信息，请参阅[Admin Control](../sites-authoring/inbox.md#inbox-admin-control)。

![自定义Experience Manager收件箱列](assets/customize-columns.gif)

#### 将交互通信另存为草稿(6.5.5.0){#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，并稍后检索草稿以继续处理它。 您可以为每个草稿指定一个不同的名称以标识它。 有关详细信息，请参阅[将交互通信另存为草稿](../forms/using/prepare-send-interactive-communication.md#save-as-draft)。

![另存为草稿](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] 应用程序服务器支持(6.5.5.0)  {#weblogic-support}

Adobe Experience Manager Forms在JEE上增加了对[!DNL Oracle WebLogic 12]的Adobe Experience Manager Forms支持。 您可以从先前版本升级，或在[!DNL Oracle WebLogic] 12.2.1.4及更高版本的JEE服务器上设置新的Experience Manager 6.5 Forms。 稍后版本与次要版本更改相对应，其中12.2.1.x中的x替换为版本号。

#### 辅助功能改进(6.5.5.0){#accessibility-improvements}

Adobe Experience Manager Forms包含以下辅助功能增强功能：

* 当用户将自适应表单预览为HTML表单时，[!UICONTROL 涂抹签名]字段将保留制表符焦点。

* 提交自适应表单时显示的错误消息现在包含`aria-describedBy`属性。 属性附加到错误消息中引用的字段。 `aria-describedby`属性指示描述对象的元素的ID。 它有助于在构件或组与描述它们的文本之间建立关系。

* 如果自适应表单包含一些必填字段，则在ARIA辅助功能模式中，此类字段的mandatory属性设置为`True`。

#### 针对表单数据模型(6.5.5.0){#x509-based-authentication-soap}中基于SOAP的Web服务的X-509基于证书的身份验证

表单数据模型现在支持基于X-509证书的身份验证，同时使用SOAP Web服务作为数据源。 有关详细信息，请参阅[配置SOAP Web服务](../forms/using/configure-data-sources.md#configure-soap-web-services)。

#### 其他关键改进(6.5.5.0){#other-improvements}

* Experience Manager 6.5 Forms on JEE 文档 Security现在基于[!DNL Apache Struts 2]。

* 增加了对[!DNL Oracle Real Applications Cluster (RAC) 19c]的支持。

#### 在Experience Manager Forms工作流(6.5.4.0){#generate-printable-output}中生成可打印输出

使用“生成可打印输出”工作流步骤，您可以将源模板文件与数据文件集成。 此集成允许您打印或保存模板文件的不同副本。 该步骤生成PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 有关此功能的详细信息，请参阅OSGi上的[以Forms为中心的工作流 — 步骤参考](../forms/using/aem-forms-workflow-step-reference.md)。

![生成可打印输出](assets/generate-print-output-step.gif)

#### 在布局模式(6.5.4.0){#multi-column-adaptive-forms}中支持自适应表单和交互式通信的多列

您现在可以通过自适应表单和交互式通信为面板定义列数。 切换到布局模式以使用新的多列选项。 有关详细信息，请参阅[使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

![多列布局](assets/multi-column-layout.gif)

#### Experience Manager收件箱自定义(6.5.4.0){#aem-inbox}

新的“管理控制”选项使管理员能够：

* 自定义标题文本和徽标。

* 控制标题中可用导航链接的显示。

“管理控制”选项仅对`administrators`或`workflow-administrators`组的成员可见。 有关此功能的详细信息，请参阅[您的收件箱](../sites-authoring/inbox.md)。

#### HTML5表单中的富文本支持(6.5.4.0){#rich-text-support}

将XFA表单中的文本字段转换为HTML5表单中的富文本字段。 有关详细信息，请参阅[为HTML5表单设计表单模板](../forms/using/designing-form-template.md)。

#### 辅助功能增强(6.5.4.0){#forms-accessibility-enhancements-6540}

Experience Manager Forms包含以下辅助功能增强：

* 屏幕阅读器在自适应表单中正确宣布复选框、链接、日期选取器和日期输入字段。

* 自适应表单的每个页面现在包含一个标题和一个主要地标标签。

#### 共享并请求访问Experience Manager Forms用户(6.5.3.0){#share-request-access}的收件箱项目

您可以与其他用户共享您的收件箱项目。 当其他用户获得对您的收件箱项目的访问权限后，用户可以对共享项目声明并采取相应操作。 同样，您也可以从其他用户请求对收件箱项目的访问权限。 请参阅[共享和请求对用户](../forms/using/configure-shared-queues-osgi.md)收件箱项目的访问权限。

#### 为Experience Manager Forms用户(6.5.3.0){#configure-out-of-office}的收件箱项目配置办公室外设置

如果您计划外出，您可以指定对分配给您的该期间项目会发生什么情况。
您可以选择指定开始日期和时间，以及结束日期和时间，以使您的离职设置生效。 您可以设置将您的所有项目发送到的默认人员。 请参阅[配置外出设置](../forms/using/configure-out-of-office-settings.md)。

#### 使用Batch API为Experience Manager Forms(6.5.3.0){#generate-multiple-ic}生成多个交互式通信

您可以使用批处理API从模板生成多个交互式通信。 模板是无需任何数据的交互式通信。 批处理API将数据与模板相结合以生成交互式通信。 API在大规模制作交互式通信中非常有用。 例如，电话账单、多个客户的信用卡对帐单。 请参阅[使用Batch API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)生成多个交互式通信。

<!-- TBD: Check if the wider team released anything in FY21.
-->

## 自[!DNL Adobe Experience Manager] 6.5 SP7 {#key-releases-since-last-sp}起的密钥释放

在2020年11月26日至2021年2月25日之间，除了Service Pack和Cumulative Fix Pack之外，Adobe还发布了以下软件：

* [!DNL Adobe Experience Manager] 作为 [Cloud Service2020.11](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-11-0.html).0 [、2020.12](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2020/release-notes-2020-12-0.html).0 [和](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date)2021.1.0。

* [[!DNL Experience Manager] 桌面应用程序2.1(2.1.0.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

* [Experience Manager Screens:功能包202011](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202011.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5文档](../user-guide/home.md)
>* [6.5的一 [!DNL Adobe Experience Manager] 般发行说明](release-notes.md)
>* [适用于6.5的Service [!DNL Adobe Experience Manager]  Pack发行说明](sp-release-notes.md)

