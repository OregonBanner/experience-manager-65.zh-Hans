---
title: ' [!DNL Experience Manager] 6.5 Service Pack 9的新增功能'
description: ' [!DNL Experience Manager] 6.5 Service Pack 9的新增功能'
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: a0f47b4e0e9f38df208ed78fde63c70813fb7dcc
workflow-type: tm+mt
source-wordcount: '3674'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 Service Pack 9的新增功能 {#aem-whats-new-service-pack}

![Whats-new](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack每季度提供新功能、客户请求的增强功能以及性能、稳定性和安全性改进。每季度提供的服务使访问和采用新功能和创新变得轻松。

本文重点介绍最新Service Pack中包含的功能、前6.5 Service Pack中包含的[关键功能以及自上一个Service Pack](#key-releases-since-last-sp)版本以来的[关键版本。](#key-features-previous-service-packs)

>[!NOTE]
>
>从[!DNL Experience Manager] Service Pack 9开始，[!DNL Experience Manager]客户可以开发和运行其[!DNL Experience Manager]应用程序，其中分发了[!DNL Azul Zulu]内部版本的OpenJDK，该版本符合Java SE的标准。
>[!DNL Azul Zulu] JDK的支持也通过Adobe提供给[!DNL Experience Manager]客户。
>您可以从[Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载[!DNL Azul Zulu] JDK的相关版本。
>由Oracle分发的AdobeJava技术的使用权限将在2022年12月底之前过期。 [!DNL Experience Manager] 我们鼓励客户在此日期之前规划并实 [!DNL Azul Zulu] 施对JDK的使用。有关[!DNL Oracle Java]技术和[!DNL Azul Zulu]技术使用的更多信息，请参阅相关的[常见问题解答](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en)。

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

### 能够恢复已删除的页面和树 {#ability-to-restore-pages-tree}

现在，您可以在[!DNL Experience Manager Sites]页面上恢复已删除的页面和整个树视图。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* 更新了与香港、澳门和台湾有关的中文地点和地区的名称，以使其符合中国社会和政治观点。

* 引入了可选配置，用于从[!DNL Adobe Experience Manager]更改ACP API响应中电子邮件ID的大小写。

   ![在ACP响应中将电子邮件ID更改为小写的配置  [!DNL Experience Manager]](assets/email-lowcase-config.png)

* 背景中的文本和图标对比度会针对各种功能得到增强。 WCAG准则的这一实施使视力和颜色感知受限的用户更易于访问[!DNL Assets]。 请参阅 [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590)中的[辅助功能增强。

### [!DNL Dynamic Media] {#assets-dynamic-media}

* [[!DNL Dynamic Media] 在以下方](sp-release-notes.md#assets-accessibility-6590) 面更易于访问：

   * 使用键盘键更方便。
   * 各种编辑器中文本、占位符文本和控件的对比度（与背景）。
   * 按屏幕阅读器显示的辅助功能和旁白。

* 借助智能成像DPR（设备像素比）和网络带宽优化，在具有高分辨率显示器和有限网络带宽的设备上高效提供最佳质量图像。 请参阅[智能成像常见问题解答](/help/assets/imaging-faq.md)。

* [!DNL Dynamic Media] 交付(`fmt` URL修饰符)现在支持下一代图像格式AVIF（AV1图像格式）。有关更多详细信息和时间轴，请参阅[图像提供和渲染API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)。

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms]的附加组件包将在计划的[!DNL Experience Manager] Service Pack版本发布后的一周内提供。

### 支持[!DNL Azul Zulu OpenJDK] {#support-azul-zulu}

现在，您可以在OSGi部署中使用[!DNL Azul Zulu]内部版本[!DNL OpenJDK]来开发和运行应用程序，[!DNL Experience Manager Forms]为。 有关更多信息，请参阅[Experience Manager6.5 Service Pack 9发行说明](sp-release-notes.md)和[技术要求](../sites-deploying/technical-requirements.md)。

### 能够使用[!UICONTROL Assign Task]向组发送通知电子邮件 {#group-notification-email}

您现在可以使用“分配任务”工作流步骤向组电子邮件地址发送通知电子邮件。

### 能够在修改源交互式通信后检索交互式通信草稿 {#retrieve-draft-after-source-modifications}

现在，在对源交互式通信进行更改后，您可以检索另存为草稿的交互式通信。

### 设置自定义域名，以加载、渲染和验证reCAPTCHA服务 {#set-custom-domain-name-recaptcha}

reCAPTCHA服务使用`https://www.recaptcha.net/`作为默认域。 现在，您可以修改设置以设置`https://www.google.com/`或任何用于加载、渲染和验证reCAPTCHA服务的自定义域名。

### [!UICONTROL 调用表单数据模型服务]工作流步骤的输入数据增强 {#input-data-enhancements-fdm}

在[!UICONTROL 调用表单数据模型服务]工作流步骤中选择表单数据模型和服务时，需为输入数据指定服务参数。

如果选择[!UICONTROL 相对于负载]选项以将文件作为服务参数附加，则现在可以指定包含该文件的文件夹路径，而不是实际的文件名。 定义文件夹名称（而不是文件附件名称）可让您重复使用工作流模型。 不要将工作流模型限制为单个文件附件名称。

### 能够在记录文档模板中使用多个主控页面 {#use-multiple-master-pages-dor-template}

现在，您可以在记录文档模板中使用多个主控页面。 因此，您现在可以在模板的标题页面和其他页面上具有不同的页眉、页脚、字体、徽标信息。

### 记录文档中的支持分页符 {#support-page-breaks-dor}

您现在可以向记录文档添加分页符。 因此，如果某个面板在页面中损坏，您可以添加一个分页符，以将该面板移动到记录文档中的新页面。

## 以前[!DNL Experience Manager] 6.5 Service Pack中的主要功能 {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### 对可用于转出的Live Copy页面进行排序(6.5.8.0) {#sort-livecopy-pages}

您现在可以使用[!UICONTROL 名称]、[!UICONTROL 上次修改日期]和[!UICONTROL 上次转出日期]属性对可供转出的Live Copy页面进行排序。 页面的[!UICONTROL 上次转出日期]是此版本中引入的新属性。

#### 页面移动和MSM转出作为异步操作(6.5.7.0)的可用性 {#page-moves-msm-asynchronous}

您现在可以将页面移动和MSM转出作为异步操作执行，以减小它们对运行时性能的影响。 您可以安排操作以便立即执行或稍后执行。 关联作业的状态和流程步骤将显示在控制台中，这有助于监控大规模MSM转出。

#### 在异步模式下执行页面移动操作(6.5.6.0)的可用性 {#page-move-asynchronous}

页面移动操作现在在异步模式下可用。 除了立即执行之外，您还可以计划页面移动操作以供以后执行。

#### 辅助功能改进(6.5.5.0) {#accessibility-sites}

* 通过添加文本信息改进了错误报告。

* 改进了键盘导航期间的用户界面焦点。

* 改进了各种用户界面元素的对比度。

* 提高了页面图像的替代属性的一致性。

* 改进了无障碍富互联网应用程序(ARIA)标签的一致性。

* 改进了非可视化桌面访问(NVDA)功能。

* 改进了屏幕阅读器支持。

#### 其他关键增强功能(6.5.5.0) {#other-enhancements-sites}

* 不允许匿名访问CRXDE Lite以增强安全性。 而是会将用户定向到登录屏幕。 请参阅[使用CRXDE Lite进行开发](/help/sites-developing/developing-with-crxde-lite.md)。

* 现在，复制或粘贴页面树时，您可以选择粘贴根页面或将根页面粘贴到树的子页面。

* [!DNL Adobe Experience Manager Experience Fragments] 现在，导出到 [!DNL Adobe Target] 工作区的选件类型和选件源在中会显示为唯一的 [!DNL Target]选件。

* 多站点管理器 — 如果某个组件从源页面中删除，则“发布”触发器现在会从已发布的页面中删除该组件。

* 多站点管理器 — 当[!UICONTROL Live Copy]中的本地组件名称与Blueprint中组件的名称相同且组件从Blueprint中转出时，术语`_msm_moved`现在会添加到本地组件的名称中。

#### 样式系统增强(6.5.4.0) {#style-system-enhancements}

您现在可以使用增强的样式系统在组件对话框中选择样式。

#### 各个方面的性能改进(6.5.4.0) {#performance-improvements}

* 缩短了在站点(`contexthub.kernel.js`)中加载和初始化ContextHub的时间。 这样可加快网站访问期间页面的加载速度。

* 减少了将[!DNL Experience Fragments]拖到[!DNL Sites]页面编辑器后刷新页面的时间。

* 缩短了[!DNL Sites]页面上&#x200B;**[!UICONTROL Live Copy概述]**&#x200B;中包含200个以上Live Copy的条目的加载时间。

* 改进了对不完整或无效URL的处理。 此类URL可能会减慢模板编辑器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

* 现在，使用[连接的资产功能](/help/assets/use-assets-across-connected-assets-instances.md)时，您可以查看使用该资产的所有[!DNL Sites]页面的列表。 资产的[!UICONTROL 属性]页面中提供了对资产的这些引用。 这允许管理员、营销人员和管理员全面了解资产使用情况，从而实现更好的跟踪、管理和品牌一致性(6.5.8.0)。

* 删除网页中引用的资产时， [!DNL Experience Manager]会显示警告。 您可以强制删除引用的资产，或检查并修改资产[!DNL Properties]页面中显示的引用。 单击引用将打开本地和远程[!DNL Sites]页面(6.5.8.0)。

* [!DNL Assets] 和提供 [!DNL Dynamic Media] 了多个辅助功能增强功能。这些增强功能与键盘导航、屏幕阅读器的使用以及启用辅助技术(AT)的类似增强功能相关。 请参阅[[!DNL Assets] 增强功能](/help/release-notes/sp-release-notes.md#assets-6570)和[[!DNL Dynamic Media] 增强功能](/help/release-notes/sp-release-notes.md#dynamic-media-6570)(6.5.7.0)

* 用户可以在卡片视图和列视图(6.5.7.0)中对数字资产进行排序。

#### 辅助功能增强(6.5.6.0) {#accessibility-assets-6560}

* **增强了用户界面在键盘导航期间的焦点**，例如，重点关注：

   * `x` 图标( [!UICONTROL 时间] 轴中资产的版本预 [!UICONTROL 览对话框)]。

   * 可操作的用户界面选项。

   * [!UICONTROL 共享链接]对话框上的电子邮件字段，以及用于在文件夹[!UICONTROL 属性]的[!UICONTROL 权限]选项卡中添加已关闭的用户组的字段。

* **使用键盘键的增强功能**

   在屏幕阅读器的浏览模式下，用户可以使用键盘键拖动元数据架构表单编辑器中的控件。

* **由于以下原因**，增强了屏幕阅读器用户的可用性：

   * 屏幕阅读器会朗读视频和音频播放器的用途。

   * 屏幕阅读器会朗读用户界面选项的用途，这些选项用于删除在资产[!UICONTROL 属性]上使用[!UICONTROL 标记选择对话框]选择的标记。

   * 屏幕阅读器会朗读表格的行标题和行项目，以便用户知道哪些条目属于同一行。

   * 搜索页面的描述性和有意义的页面标题。

   * 屏幕阅读器会将搜索过滤器面板中的选项宣布为可扩展的折叠项。

#### [!DNL Assets](6.5.6.0)中的其他增强功能 {#other-enhancements-assets-6560}

* 与文件夹（专用和非专用）关联的用户组现在会在[删除这些文件夹](/help/assets/private-folder.md#delete-private-folder)时从存储库中删除。 但是，可以使用JMX从存储库中删除现有的冗余、孤立、未使用和自动生成用户组。

#### [!DNL Assets](6.5.5.0)中的辅助功能增强功能 {#assets-accessibility}

[!DNL Experience Manager Assets] 现在，提供了更多辅助功能以符合Web内容无障碍准则(WCAG)。辅助功能因以下增强而得到改进：

* 许多用户界面元素、控件、页面和对话框都对屏幕阅读器友好。

* 许多用户界面元素、控件和输入表单字段都可使用键盘访问。

* 某些用户界面元素的颜色和对比度已更新，以便视力有限和不能感知颜色的用户能够区分这些用户界面元素。例如，根据相应的对比度，更改了星级图标的颜色（如资产[!UICONTROL 属性]或卡片视图中[!UICONTROL Advanced]选项卡的[!UICONTROL Rating]部分）。

   ![对比度提高的评级图标](assets/star-rating-icons.png)

#### 增强的异常处理(6.5.5.0) {#exception-handling}

[!DNL Assets] 用户界面流程具有更好的异常处理功能。如果资产的维度类型不为，则会在日志文件中记录观察到的异常。

#### 支持[!DNL Dynamic Media]中的3D资产(6.5.5.0) {#support-for-3d}

在[!DNL Dynamic Media]中支持3D图像使客户能够将3D内容发布并添加到网页和应用程序。 支持包括：

* 发布常见的3D资产格式，并生成可在网页和其他应用程序中使用的资产URL。

* 由[!DNL Adobe Dimension]提供支持的3D Web查看器，可以交互查看已发布的3D资产。

* 使用[!DNL Sites] WCM组件在[!DNL Experience Manager Sites]页面上发布和查看常见的3D资产。

#### 使用[!DNL Brand Portal]配置[!DNL Experience Manager Assets](6.5.4.0) {#configure-assets-bp}

[!DNL Experience Manager Assets]和[!DNL Brand Portal]之间的授权通道已更改。 以前， [!DNL Brand Portal]是通过旧版OAuth网关在经典UI中配置的，该网关使用JWT令牌交换获取IMS访问令牌以进行授权。 [!DNL Experience Manager Assets] 现在使用 [!DNL Brand Portal] 通 [!DNL Adobe I/O]过进行配置，以获取IMS令牌以授权租户 [!DNL Brand Portal] 。

使用[!DNL Brand Portal]配置[!DNL Experience Manager Assets]的步骤因您的[!DNL Experience Manager]版本以及您是首次配置还是升级现有配置而异。 有关详细信息，请参阅[使用Brand Portal配置Experience Manager资产](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)。

#### 辅助功能增强(6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] 包括以下辅助功能增强功能：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关更多信息，请参阅[仅使用键盘键预览资产](../assets/manage-assets.md#previewing-assets)。

* “过滤器”面板中的混合状态复选框（除非您选择所有嵌套谓词，否则未选择并遍历第一级复选框）可由屏幕阅读器读取。

* 日期和时间格式约束在日期字段的字段标签中提供，以使用户能够使用键盘以正确的格式输入日期。
例如，`On Time (MM-DD-YYYY HH:mm)`。 其中，MM为两位数格式的月份，YYYY为年份，DD为两位数格式的日份，HH为24小时军用格式的小时，mm为分钟。

* 屏幕阅读器会朗读用于删除选定标记的选项（`X`符号）和选定标记的数量。

#### 列表视图中资产创建日期的可排序列(6.5.3.0) {#sortable-date-created-column}

在DAM列表视图中和列表视图中的资产搜索结果中，会为资产的创建日期添加新的可排序列。

![创建日期的可排序列](assets/asset-created-date.png)

#### 可视搜索[!DNL Adobe Experience Manager Assets](6.5.2.0) {#visual-search}

[!DNL Assets] 用户可以搜索视觉上相似的图像。Experience Manager显示DAM存储库中与用户选择的图像类似的智能标记图像。 请参阅[可视搜索](../assets/search-assets.md)。

### Dynamic Media {#dynamic-media-previous-service-packs}

#### 使CDN缓存内容(6.5.6.0)失效 {#invalidate-cdn-cached-content}

现在，您可以使用[!DNL Dynamic Media]用户界面来使内容分发网络(CDN)缓存内容失效。 因此，更新后的资产会立即可用，而无需等待缓存过期。 您可以通过以下方式使CDN失效：

* 创建CDN失效模板：选择资产和表单关联的基于模板的URL

* 通过资产选取器选择资产和关联的预设

* 添加完整的资产URL

#### 选择性地将资产发布到[!DNL Experience Manager]和[!DNL Dynamic Media](6.5.6.0) {#selective-publishing}

现在，您可以使用[!UICONTROL 快速发布]或[!UICONTROL 管理发布]向导，选择有选择地将资产发布或取消发布到[!DNL Experience Manager]或[!DNL Dynamic Media]。 您还可以在文件夹级别设置`Publish`或`Unpublish`模式。

#### 适用于Dynamic Media的智能成像 {#smart-imaging}

智能成像使用每个用户的独特查看特性自动提供针对其体验优化的正确图像，从而提高性能和参与度。 智能成像可与您现有的图像预设配合使用，并在交付的最后一毫秒内使用智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 请参阅[智能成像](../assets/imaging-faq.md)。

#### 在Dynamic Media的视频配置文件中智能裁剪(6.5.3.0) {#smart-crop-video}

视频智能裁剪 — 视频配置文件中提供的可选功能 — 是一款工具，可使用Adobe Sensei中人工智能的强大功能，自动检测和裁剪您上传的任何自适应视频或渐进式视频中的焦点，而不论其大小。 请参阅[关于在视频配置文件中使用智能裁剪](../assets/video-profiles.md)。

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### 根据规则(6.5.8.0)在自适应表单中显示或隐藏CAPTCHA组件 {#show-hide-captcha}

现在，您可以在自适应表单提交或用户操作时验证CAPTCHA。 您还可以添加条件以在用户操作上验证CAPTCHA，并基于规则在自适应表单中显示或隐藏CAPTCHA组件。

#### 添加自定义CAPTCHA服务(6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] 提供开箱即用的支持，以将Google reCAPTCHA（需要单独的Google reCAPTCHA API许可证）用作CAPTCHA验证服务。您还可以使用自定义CAPTCHA服务来验证CAPTCHA。

#### 其他增强功能(6.5.8.0) {#other-enhancements-forms-6580}

* 改进了[!DNL Experience Manager Forms]日期选取器组件的辅助功能。

* 添加了对使用PrintChannel API生成PCL格式的交互式通信的支持。

* 执行PDFG转换时，现在可以启用或禁用[!DNL Experience Manager Forms]注册表更改以生成自定义书签。

#### 性能改进(6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms改进了以下性能：

* 在提交自适应表单时验证服务器上的字段值。

* 使用[!DNL Automated Forms Conversion service]将PDF表单转换为自适应表单。

#### 支持Microsoft SQL Server 2016 Always On Availability组以实现高可用性(6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] 现在支持 [!DNL Microsoft] SQL Server 2016 Always On可用性组，以实现OSGi部署的高可用性。

#### 形成数据模型HTTP客户端配置以优化性能(6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] 由于数据源现在包含用于性能优化的HTTP客户端配置，因此在与RESTful Web服务集成时会生成数据模型。请参阅[配置数据源](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration)。

#### 在布局模式下，每个组件的重置选项的可用性(6.5.7.0) {#reset-option-layout-mode}

现在，您可以在自适应表单的布局模式下为每个组件使用重置选项。 为面板定义多列布局时，可以使用此功能重置面板中的各个组件。 请参阅[使用布局模式调整组件大小](../../help/forms/using/resize-using-layout-mode.md#resize-components)。

#### 在客户端(6.5.6.0)预填自适应表单 {#prefill-merge-data-at-client}

预填自适应表单时，[!DNL Experience Manager Forms]服务器会将数据与自适应表单合并，并将填写的表单提交给您。 默认情况下，数据合并操作会在服务器中进行。
现在，您可以将[!DNL Experience Manager Forms]服务器配置为在客户端](../../help/forms/using/prepopulate-adaptive-form-fields.md)上执行数据合并操作，而不是在服务器上执行。 [它显着缩短了预填充和渲染自适应表单所需的时间。

#### 在具有双向SSL实施(6.5.6.0)的服务器上，与RESTful API形成数据模型集成 {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] 表单数据模型现 [在可以与服务器上的RESTful API集成，该服务器上已实施双向SSL](../../help/forms/using/configure-data-sources.md)。

#### 在Automated forms conversion服务(6.5.6.0)中添加了对[!DNL Adobe Sign]文本标记的支持 {#sign-integration-acroform-afcs}

如果AcroForm包含[!DNL Adobe Sign]文本标记，则这些字段现在在使用[!DNL Automated Forms Conversion service]转换的自适应表单中被识别并表示为[!DNL Adobe Sign]字段。 签名者在签名自适应表单时可以填写此类字段。

#### 支持将彩色PDF forms转换为自适应表单(6.5.6.0) {#colored-PDF-forms}

您可以使用[!DNL Automated Forms Conversion service]将彩色PDF forms转换为自适应表单。

#### 支持SMB 2和SMB 3协议(6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] 现在支持SMB 2和SMB 3协议。

#### 增强了已翻译的自适应表单页面的缓存(6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

现在，您可以在自适应表单URL中指定[区域设置作为选择器，而不是在自适应表单URL中指定参数](../../help/forms/using/supporting-new-language-localization.md)。 它有助于在[!DNL Experience Manager Dispatcher]上缓存已翻译的自适应表单。 无法缓存已翻译的自适应表单在以前的版本中。 有关配置缓存以在自适应表单URL中将区域设置用作选择器的详细信息，请参阅[在调度程序](../../help/forms/using/configure-adaptive-forms-cache.md)处配置自适应表单缓存。

#### 将表单数据模型服务的输出保存到变量(6.5.6.0) {#save-fdm-service-to-variable}

表单数据模型允许您将表单数据模型服务的输出保存到变量。 [!DNL Experience Manager Forms] 现在，会自动将表单数据模型服务的类型映射到变量类型。

#### 为文件附件组件(6.5.6.0)附加多个文件 {#attach-multiple-files}

现在，您可以将[多个文件](../../help/forms/using/introduction-forms-authoring.md)附加到自适应表单的[!UICONTROL 文件附件]组件。

#### 自定义Adobe Experience Manager收件箱列(6.5.5.0) {#customize-aem-inbox-columns}

您可以自定义[!DNL Experience Manager]收件箱以更改列的默认标题、重新排序列的位置，并根据工作流的数据显示其他列。 `administrators`或`workflow-administrators`组的成员可以自定义列。 有关更多信息，请参阅[Admin Control](../sites-authoring/inbox.md#inbox-admin-control)。

![自定义Experience Manager收件箱列](assets/customize-columns.gif)

#### 将交互式通信另存为草稿(6.5.5.0) {#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，稍后检索草稿以继续处理该草稿。 您可以为每个草稿指定不同的名称以标识它。 有关更多信息，请参阅[将交互式通信另存为草稿](../forms/using/prepare-send-interactive-communication.md#save-as-draft)。

![另存为草稿](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] 应用程序服务器支持(6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms在JEE上为Adobe Experience Manager Forms添加了[!DNL Oracle WebLogic 12]支持。 您可以从以前的版本升级，或在[!DNL Oracle WebLogic] 12.2.1.4及更高版本的JEE服务器上设置新的Experience Manager6.5 Forms。 稍后版本与次要版本更改相对应，其中12.2.1.x中的x被替换为版本号。

#### 辅助功能改进(6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms包括以下辅助功能增强功能：

* 当用户将自适应表单预览为HTML表单时，[!UICONTROL 涂写签名]字段将保留制表符焦点。

* 现在，提交自适应表单时显示的错误消息包含`aria-describedBy`属性。 属性附加到错误消息中引用的字段。 `aria-describedby`属性指示描述对象的元素的ID。 它有助于在小组件或组与描述它们的文本之间建立关系。

* 如果自适应表单包含一些必填字段，则对于ARIA辅助功能架构中的此类字段，必填属性将设置为`True`。

#### 针对表单数据模型(6.5.5.0)中基于SOAP的Web服务，使用基于X-509证书的身份验证 {#x509-based-authentication-soap}

表单数据模型现在支持使用SOAP Web服务作为数据源时，基于X-509证书的身份验证。 有关更多信息，请参阅[配置SOAP Web服务](../forms/using/configure-data-sources.md#configure-soap-web-services)。

#### 其他关键改进(6.5.5.0) {#other-improvements}

* Experience Manager6.5 JEE文档安全现在基于[!DNL Apache Struts 2]。

* 添加了对[!DNL Oracle Real Applications Cluster (RAC) 19c]的支持。

#### 在Experience ManagerForms工作流中生成可打印的输出(6.5.4.0) {#generate-printable-output}

通过生成可打印输出工作流步骤，您可以将源模板文件与数据文件集成。 此集成允许您打印或保存模板文件的不同副本。 该步骤会生成PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 有关此功能的更多信息，请参阅OSGi上以Forms为中心的工作流 — 步骤参考](../forms/using/aem-forms-workflow-step-reference.md)。[

![生成可打印输出](assets/generate-print-output-step.gif)

#### 在布局模式下支持自适应表单和交互式通信的多列(6.5.4.0) {#multi-column-adaptive-forms}

现在，您可以在自适应表单和交互式通信中为面板定义列数。 切换到布局模式以使用新的多列选项。 有关更多信息，请参阅[使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

![多列布局](assets/multi-column-layout.gif)

#### Experience Manager收件箱自定义(6.5.4.0) {#aem-inbox}

新的“管理控制”选项使管理员能够：

* 自定义标题文本和徽标。

* 控制标题中可用导航链接的显示。

“管理控制”选项仅对`administrators`或`workflow-administrators`组的成员可见。 有关此功能的更多信息，请参阅[您的收件箱](../sites-authoring/inbox.md)。

#### HTML5表单(6.5.4.0)中的富文本支持 {#rich-text-support}

将XFA表单中的文本字段转换为HTML5表单中的富文本字段。 有关更多信息，请参阅[为HTML5表单设计表单模板](../forms/using/designing-form-template.md)。

#### 辅助功能增强(6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience ManagerForms包括以下辅助功能增强功能：

* 屏幕阅读器在自适应表单中正确读出复选框、链接、日期选取器和日期输入字段。

* 自适应表单的每个页面现在都包含一个标题和一个主要地标标签。

#### 共享和请求访问Experience ManagerForms用户(6.5.3.0)的收件箱项目 {#share-request-access}

您可以与其他用户共享您的收件箱项目。 当其他用户获得对您的收件箱项目的访问权限后，用户可以声明共享项目并对其采取适当的操作。 同样，您也可以请求其他用户访问收件箱项目。 请参阅[共享和请求访问用户](../forms/using/configure-shared-queues-osgi.md)的收件箱项目。

#### 为Experience ManagerForms用户(6.5.3.0)的收件箱项目配置现成设置 {#configure-out-of-office}

如果您计划不在办公室，则可以指定在该期间分配给您的项目会发生什么情况。
您可以选择指定开始日期和时间以及结束日期和时间，以使“不在办公室”设置生效。 您可以设置将所有项目发送到的默认人员。 请参阅[配置Out of Office设置](../forms/using/configure-out-of-office-settings.md)。

#### 使用批处理API生成多个交互式通信以用于Experience ManagerForms(6.5.3.0) {#generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 模板是一种无任何数据的交互式通信。 批处理API将数据与模板组合在一起，以生成交互式通信。 该API在大规模生产交互式通信中非常有用。 例如，电话单、多个客户的信用卡对帐单。 请参阅[使用批处理API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)生成多个交互式通信。

<!-- TBD: Check if the wider team released anything in FY21.
-->

## [!DNL Adobe Experience Manager] 6.5 SP8之后的关键版本 {#key-releases-since-last-sp}

在2021年2月25日至2021年5月27日期间，除了Service Pack之外，Adobe还发布了以下内容：

* [!DNL Adobe Experience Manager] as aCloud Service [2021.2.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-2-0.html)、 [2021.3.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-3-0.html)和 [2021.4.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=en#release-date)。

* [[!DNL Experience Manager] 桌面应用程序2.1(2.1.2.0)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

* [Experience Manager Screens:功能包202103](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202103.html?lang=en)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5文档](../user-guide/home.md)
* [ [!DNL Adobe Experience Manager] 6.5的常规发行说明](release-notes.md)
* [ [!DNL Adobe Experience Manager] 6.5的Service Pack发行说明](sp-release-notes.md)

