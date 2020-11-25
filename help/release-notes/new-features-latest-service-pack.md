---
title: Adobe Experience Manager6.5 Service Pack 7的新增功能
description: Adobe Experience Manager6.5 Service Pack 7的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 34e41cf5984f5f69ae0ccead137fe4f180bd84ad
workflow-type: tm+mt
source-wordcount: '2705'
ht-degree: 1%

---


# Adobe Experience Manager6.5 Service Pack 7的新增功能 {#aem-whats-new-service-pack}

![新增功能](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Pack每季度提供新功能、客户请求的增强功能以及性能、稳定性和安全性改进。 每季度上市使访问和采用新功能和创新变得很容易。

本文重点介绍最新6.5 Service Pack包含的功能、 [先前6.5 Service Pack包含的主要功能](#key-features-previous-service-packs)，以及 [自上一个Service Pack版本以来的主要AEM版本](#key-releases-since-last-sp) 。

## Adobe [!DNL Experience Manager Sites] {#aem-sites}

### 对可用于转出的Live Copy页面进行排序 {#sort-livecopy-pages}

您现在可以使用名称、上次修改日期和上次转出日期 [!UICONTROL 属性]，对可 [!UICONTROL 用于转]出的Live Copy页 [!UICONTROL 面进] 行排序。 页面 [!UICONTROL 的上次转出] 日期是此版本中引入的一个新属性。

### 页面移动和MSM转出作为异步操作的可用性 {#page-moves-msm-asynchronous}

您现在可以将页面移动和MSM转出作为异步操作执行，以减少它们对运行时性能的影响。 您可以计划操作以立即或稍后执行。 关联的作业和进程步骤的状态显示在控制台中，这有助于监视大型MSM转出。

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* 用户可以在卡片和列视图中对数字资产进行排序。

* [!DNL Assets] 并提供 [!DNL Dynamic Media] 多个辅助功能增强功能。 这些增强功能与键盘导航、屏幕阅读器的使用、启用辅助技术(AT)的类似增强功能相关。 请参阅 [资产增强](/help/release-notes/sp-release-notes.md#assets-6570) 和增 [[!DNL Dynamic Media] 强功能](/help/release-notes/sp-release-notes.md#dynamic-media-6570)。 <!-- TBD: Add link to a11y article after go-live. Adding RN link for now. -->

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的Service Pack发布后一周内，将提供 [!DNL Experience Manager] 附加包。 [!DNL Experience Manager] 6.5 Service Pack 7(6.5.7.0)计划于2020年11月26日发布。

## 先前6.5 Service [!DNL Experience Manager] Pack的主要功能 {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### 异步模式下页面移动操作的可用性(6.5.6.0) {#page-move-asynchronous}

页面移动操作现在在异步模式下可用。 除了立即执行外，您还可以计划页面移动操作以便以后执行。

#### 辅助功能改进(6.5.5.0) {#accessibility-sites}

* 通过添加文本信息改进了错误报告。

* 改进了键盘导航期间的用户界面焦点。

* 改进了各种用户界面元素的对比度。

* 改进了页面图像的替代属性的一致性。

* 改进了可访问的富Internet应用程序(ARIA)标签的一致性。

* 改进了非可视桌面访问(NVDA)功能。

* 改进了屏幕阅读器支持。

#### 其他主要增强功能(6.5.5.0) {#other-enhancements-sites}

* 禁止匿名访问CRXDE Lite以增强安全性。 而是将用户定向到登录屏幕。 请参 [阅使用CRXDE Lite开发](/help/sites-developing/developing-with-crxde-lite.md)。

* 现在，在复制或粘贴页面树时，您可以选择粘贴根页面或将根页面与树的子页面一起粘贴。

* [!DNL Adobe Experience Manager Experience Fragments] 导出到工 [!DNL Adobe Target] 作区时，现在在中显示为唯一的优惠类型和优惠源 [!DNL Target]。

* 多站点管理器——如果某个组件从源页面中删除，则发布触发器现在会从已发布页面中删除该组件。

* 多站点管理器——当Live Copy中的本地组件的名 [!UICONTROL 称与] Blueprint中的组件的名称相同且组件从Blueprint中转出时，该术语现 `_msm_moved` 在会添加到本地组件的名称中。

#### 样式系统增强(6.5.4.0) {#style-system-enhancements}

您现在可以使用增强的样式系统在组件对话框中选择样式。

#### 不同方面的性能改进(6.5.4.0) {#performance-improvements}

* 缩短了在站点()中加载和初始化ContextHub的`contexthub.kernel.js`时间。 这样，在网站访问过程中页面加载速度会更快。

* 缩短了拖动到页面编辑器后刷新 [!DNL Experience Fragments] 页面 [!DNL Sites] 的时间。

* 缩短了Live Copy概述中包含 [!DNL Sites] 超过200个Live Copy的页面上条目 **[!UICONTROL 的加载时间]**。

* 改进了对不完整或无效URL的处理。 此类URL会减慢模板编辑器的速度。

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Accessibility enhancements (6.5.6.0) {#accessibility-assets-6560}

* **增强的用户界面在键盘导航期间的焦点**，例如，侧重于：

   * `x` 图标 [!UICONTROL 预览] (位于时间轴中的 [!UICONTROL 资产])。

   * 可操作的用户界面选项。

   * “共享链接”对 [!UICONTROL 话框上的] “电子邮件”字段，以及用于在文件夹属性的“权限”选 [!UICONTROL 项卡] 中添加已关闭 [!UICONTROL 用户组]的字段。

* **使用键盘键的增强功能**

   用户可以使用键盘键在屏幕阅读器的浏览模式下拖动元数据模式表单编辑器中的控件。

* **由于以下原因**，屏幕阅读器用户的增强可用性：

   * 屏幕阅读器宣布视频和音频播放器的用途。

   * 屏幕阅读器会通知用户界面选项的目的，即删除使用资产属性上的标记 [!UICONTROL 选择对话框选] 择的 [!UICONTROL 标记]。

   * 屏幕阅读器将公布表的行标题和行项，以便用户知道哪些条目属于同一行。

   * 搜索页面的描述性和有意义的页面标题。

   * 屏幕阅读器将搜索筛选器面板中的选项宣布为可扩展的选项。

#### (6.5. [!DNL Assets] 6.0)中的其他增强功能 {#other-enhancements-assets-6560}

* 与文件夹（私有和非私有）关联的用户组现在在删除这些文件夹时 [从存储库中删除](/help/assets/private-folder.md#delete-private-folder)。 但是，可以使用JMX从存储库中删除现有的冗余、孤立、未使用和自动生成的用户组。

#### (6.5. [!DNL Assets] 5.0)中的辅助功能增强 {#assets-accessibility}

[!DNL Experience Manager Assets] 现在可根据Web内容辅助功能准则(WCAG)更方便地访问。 辅助功能因以下增强而得到改进：

* 许多用户界面元素、控件、页面和对话框都是屏幕阅读器友好的。

* 许多用户界面元素、控件和输入表单字段都可使用键盘进行访问。

* 某些用户界面元素的颜色和对比度已更新，以便视力有限和不能感知颜色的用户能够区分这些用户界面元素。For example, the color of star rating icons (such as in [!UICONTROL Rating] section of [!UICONTROL Advanced] tab in asset [!UICONTROL Properties] or in card view) is changed for appropriate contrast.

   ![对比度得到改善的等级图标](assets/star-rating-icons.png)

#### 增强的异常处理(6.5.5.0) {#exception-handling}

[!DNL Assets] 用户界面流具有更好的异常处理。 如果资产的维度没有类型，则在日志文件中记录观察到的异常。

#### 在(6.5.5.0) [!DNL Dynamic Media] 中支持3D资源 {#support-for-3d}

中的3D图像支 [!DNL Dynamic Media] 持使客户能够发布3D内容并将其添加到网页和应用程序。 支持包括：

* 发布常见的3D资产格式，并生成可在网页和其他应用程序中使用的资产URL。

* 3D Web查看器，以交互 [!DNL Adobe Dimension]方式视图已发布的3D资源。

* 使用WCM组件在页面上发 [!DNL Experience Manager Sites] 布和视图常 [!DNL Sites] 用3D资产。

#### 配 [!DNL Experience Manager Assets] 置 [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

和之间的授 [!DNL Experience Manager Assets] 权渠道 [!DNL Brand Portal] 已更改。 以前， [!DNL Brand Portal] 在经典UI中通过旧版OAuth网关进行配置，该网关使用JWT令牌交换获得IMS访问令牌进行授权。 [!DNL Experience Manager Assets] 现在已通过 [!DNL Brand Portal] AdobeI/O进行配置，它为租户获取IMS令牌以进行授 [!DNL Brand Portal] 权。

使用进行配 [!DNL Experience Manager Assets] 置的 [!DNL Brand Portal] 步骤因您的版本、 [!DNL Experience Manager] 是首次配置还是升级现有配置而异。 有关详 [细信息，请参阅配置Experience Manager资产](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) （使用Brand Portal）。

#### Accessibility enhancements (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] 包括以下辅助功能增强：

* 键盘上的箭头键可用于移动和平移缩放图像中的区域。 有关详细信息，请参阅 [仅使用键盘键预览资源](../assets/manage-assets.md#previewing-assets)。

* 过滤器面板中的混合状态复选框（除非您选择所有嵌套的谓词，否则不会选择并遍历第一级复选框）可由屏幕阅读器读取。

* 日期和时间格式约束在日期字段的字段标签中提供，以使用户能够使用键盘以正确的格式输入日期。
For example, `On Time (MM-DD-YYYY HH:mm)`. 这里，MM是两位数格式的月份，YYYY是年份，DD是两位数格式的日份，HH是24小时军事格式的小时，mm是分钟。

* 屏幕阅读器会宣布删除选定标记(`X` 符号)和选定标记数的选项。

#### 列表视图中资产创建日期的可排序列(6.5.3.0) {#sortable-date-created-column}

在DAM列表视图中，将为资产的创建日期添加一个新的可排序列，并在列表视图中对资产搜索结果进行添加。

![创建日期的可排序列](assets/asset-created-date.png)

#### 可视 [!DNL Adobe Experience Manager Assets] 搜索(6.5.2.0) {#visual-search}

[!DNL Assets] 用户可以搜索视觉上相似的图像。 Experience Manager显示来自DAM存储库的智能标记图像，该图像与用户选择的图像类似。 See [Visual search](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### 使CDN缓存内容(6.5.6.0)无效 {#invalidate-cdn-cached-content}

您现在可以使用 [!DNL Dynamic Media] 用户界面使内容投放网络(CDN)缓存内容失效。 因此，更新的资产会立即可用，而不会等到缓存过期。 您可以通过以下方式使CDN失效：

* 创建CDN失效模板：选择资产和表单关联的基于模板的URL

* 通过资产选取器选择资产和关联的预设

* 添加完整的资产URL

#### 选择性地将资 [!DNL Experience Manager] 源发 [!DNL Dynamic Media] 布到和(6.5.6.0) {#selective-publishing}

您现在可以选择选择性地将资产发布或取消发布到 [!DNL Experience Manager] 或使 [!DNL Dynamic Media] 用快 [!UICONTROL 速发布] 或管 [!UICONTROL 理发布向导] 。 您还可以在文件 `Publish` 夹级 `Unpublish` 别设置或模式。

#### Dynamic Media的智能成像 {#smart-imaging}

智能成像使用每个用户独特的查看特性自动提供为其体验优化的正确图像，从而获得更好的性能和参与度。 智能成像可以与现有图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 请参 [阅智能成像](../assets/imaging-faq.md)。

#### Dynamic Media视频用户档案中的智能裁剪(6.5.3.0) {#smart-crop-video}

视频智能裁剪是视频用户档案中的一项可选功能，它使用Adobe Sensei人工智能的强大功能自动检测和裁剪您上传的任何自适应视频或渐进视频中的焦点，而不管其大小。 请参 [阅关于在视频用户档案中使用智能裁剪](../assets/video-profiles.md)。

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### 在客户端预填自适应表单(6.5.6.0) {#prefill-merge-data-at-client}

在您预填自适应表单时，服务器 [!DNL Experience Manager Forms] 会将数据与自适应表单合并，并将填写的表单发送给您。 默认情况下，数据合并操作在服务器上进行。
您现在可以配置服 [!DNL Experience Manager Forms] 务器 [在客户端而不是服务器执行数据合并](../../help/forms/using/prepopulate-adaptive-form-fields.md) 操作。 它显着缩短了预填和渲染自适应表单所需的时间。

#### 通过双向SSL实现(6.5.6.0)，在服务器上与RESTful API集成表单数据模型 {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] 表单数据模型现 [在可以与服务器上实现双向SSL的RESTful API集成](../../help/forms/using/configure-data-sources.md)。

#### 在Automated forms conversion服 [!DNL Adobe Sign] 务(6.5.6.0)中增加了对文本标记的支持 {#sign-integration-acroform-afcs}

如果AcroForm包含文 [!DNL Adobe Sign] 本标记，则这些字段现在可识别并表示为 [!DNL Adobe Sign] 使用转换的自适应表单中的字段 [!DNL Automated Forms Conversion service]。 签署方可以在签署自适应表单时填写此类字段。

#### Support to convert colored PDF forms to adaptive forms (6.5.6.0) {#colored-PDF-forms}

您可以使用 [!DNL Automated Forms Conversion service] 将彩色PDF forms转换为自适应表单。

#### 支持SMB 2和SMB 3协议(6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] 现在支持SMB 2和SMB 3协议。

#### 增强了已翻译的自适应表单页面的缓存(6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

您现在可以在自 [适应表单URL中将区域设置指定为选择器，而不是在自适应表单URL中指定参数](../../help/forms/using/supporting-new-language-localization.md)。 它有助于在上缓存已翻译的自适应表 [!DNL Experience Manager Dispatcher]单。 在以前版本中无法缓存已翻译的自适应表单。 有关配置缓存以将区域设置用作自适应表单URL中的选择器的详细信息，请参 [阅在调度程序中配置自适应表单缓存](../../help/forms/using/configure-adaptive-forms-cache.md)。

#### 将表单数据模型服务的输出保存到变量(6.5.6.0) {#save-fdm-service-to-variable}

表单数据模型允许您将表单数据模型服务的输出保存到变量。 [!DNL Experience Manager Forms] 现在自动将表单数据模型服务的类型映射到变量的类型。

#### 为文件附件组件附加多个文件(6.5.6.0) {#attach-multiple-files}

您现在可以 [将多个文件附](../../help/forms/using/introduction-forms-authoring.md) 加到自 [!UICONTROL 适应表单的] “文件附件”组件。

#### 自定义Adobe Experience Manager收件箱列(6.5.5.0) {#customize-aem-inbox-columns}

您可以自定义收 [!DNL Experience Manager] 件箱以更改列的默认标题，对列的位置重新排序，并根据工作流的数据显示其他列。 列或组 `administrators` 的 `workflow-administrators` 成员可以自定义列。 有关详细信息，请参阅 [管理控制](../sites-authoring/inbox.md#inbox-admin-control)。

![自定义Experience Manager收件箱列](assets/customize-columns.gif)

#### 将交互通信另存为草稿(6.5.5.0) {#save-as-draft}

您可以使用代理UI为每个交互式通信保存一个或多个草稿，稍后检索草稿以继续处理它。 您可以为每个草稿指定一个不同的名称以标识它。 有关详细信息，请参 [阅将交互式通信另存为草稿](../forms/using/prepare-send-interactive-communication.md#save-as-draft)。

![另存为草稿](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] 应用程序服务器支持(6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms在JEE上为 [!DNL Oracle WebLogic 12] Adobe Experience Manager Forms增加了支持。 您可以从先前版本升级，或在JEE服务器上的12.2.1.4及更高版本上 [!DNL Oracle WebLogic] 设置新的Experience Manager6.5Forms。 稍后的版本更改与次要版本更改相对应，其中12.2.1.x中的x替换为版本号。

#### 辅助功能改进(6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms包括以下辅助功能增强：

* 当用户将自适应表单预览为HTML表单时，“涂 [!UICONTROL 抹签名] ”字段将保留选项卡焦点。

* 现在，提交自适应表单时显示的错误消息包含该 `aria-describedBy` 属性。 属性附加到错误消息中引用的字段。 属性 `aria-describedby` 指示描述该对象的元素的ID。 它有助于在构件或组与描述它们的文本之间建立关系。

* 如果自适应表单包含一些必填字段，则在ARIA辅助功能模式中，将 `True` 此类字段的必填属性设置为。

#### 针对表单数据模型(6.5.5.0)中基于SOAP的Web服务的X-509基于证书的身份验证 {#x509-based-authentication-soap}

表单数据模型现在支持基于X-509证书的身份验证，同时使用SOAP Web服务作为数据源。 有关详细信息，请参 [阅配置SOAP Web服务](../forms/using/configure-data-sources.md#configure-soap-web-services)。

#### 其他主要改进(6.5.5.0) {#other-improvements}

* Experience Manager6.5Forms关于JEE文档安全的现在基于 [!DNL Apache Struts 2]。

* 增加了对的 [!DNL Oracle Real Applications Cluster (RAC) 19c]支持。

#### 在Experience ManagerForms工作流(6.5.4.0)中生成可打印输出 {#generate-printable-output}

使用“生成可打印输出”工作流步骤，您可以将源模板文件与数据文件集成。 此集成允许您打印或保存模板文件的不同副本。 该步骤生成PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 有关此功能的更多信息，请参 [阅OSGi —— 步骤参考上以Forms为中心的工作流程](../forms/using/aem-forms-workflow-step-reference.md)。

![生成可打印输出](assets/generate-print-output-step.gif)

#### 在布局模式下支持自适应表单和交互式通信的多列(6.5.4.0) {#multi-column-adaptive-forms}

您现在可以通过自适应表单和交互式通信为面板定义列数。 切换到布局模式以使用新的多列选项。 有关详细信息，请参 [阅使用布局模式调整组件大小](../forms/using/resize-using-layout-mode.md)。

![多列布局](assets/multi-column-layout.gif)

#### Experience Manager收件箱自定义(6.5.4.0) {#aem-inbox}

新的“管理控制”选项使管理员能够：

* 自定义标题文本和徽标。

* 控制标题中可用导航链接的显示。

“管理控制”选项仅对或组的成员 `administrators` 可 `workflow-administrators` 见。 有关此功能的详细信息，请参 [阅您的收件箱](../sites-authoring/inbox.md)。

#### HTML5表单中的富文本支持(6.5.4.0) {#rich-text-support}

将XFA表单中的文本字段转换为HTML5表单中的富文本字段。 有关详细信息，请 [参阅设计HTML5表单的表单模板](../forms/using/designing-form-template.md)。

#### Accessibility enhancements (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience ManagerForms包含以下辅助功能增强功能：

* 屏幕阅读器在自适应表单中正确宣布复选框、链接、日期选取器和日期输入字段。

* 自适应表单的每页现在包含一个标题和一个主要地标标签。

#### 共享并请求访问Experience ManagerForms用户的收件箱项目(6.5.3.0) {#share-request-access}

您可以与其他用户共享您的收件箱项目。 当其他用户获得对您的收件箱项目的访问权限后，用户可以声明共享项目并采取相应操作。 同样，您也可以请求其他用户访问收件箱项目。 请参 [阅共享和请求对用户收件箱项目的访问权限](../forms/using/configure-shared-queues-osgi.md)。

#### 为Experience ManagerForms用户(6.5.3.0)的收件箱项目配置办公室外设置 {#configure-out-of-office}

如果您计划离开办公室，您可以指定对分配给您的该期间的项目会发生什么情况。
您可以选择指定开始日期、时间以及结束日期和时间，以使您的离职设置生效。 您可以设置将所有项目发送给的默认人员。 请参 [阅配置外出设置](../forms/using/configure-out-of-office-settings.md)。

#### 使用Batch API为FormsExperience Manager(6.5.3.0)生成多个交互式通信 {#generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 模板是无任何数据的交互式通信。 批处理API将数据与模板相结合以生成交互式通信。 API在大规模制作交互式通信中非常有用。 例如，电话单、多个客户的信用卡对帐单。 请参 [阅使用Batch API生成多个交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## 自Adobe Experience Manager6.5 SP6以来的主要发行版 {#key-releases-since-last-sp}

在2020年9月3日至2020年11月26日期间，除了服务包和累积修复包外，Adobe还发布了以下内容：

* [!DNL Adobe Experience Manager] cloud service [2020.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-9-0.html?lang=en#release-notes) 和 [2020.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-10-0.html?lang=en#release-notes)。

* [[!DNL Experience Manager] 桌面应用程序2.0(2.0.3.2)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

* [WKND参考站点- 0.0.6](https://github.com/adobe/aem-guides-wknd/releases/tag/aem-guides-wknd-0.0.6)

* [Experience Manager Screens:功能包202008](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202008.html)

* [Adobe资产链接2.2版](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)

>[!MORELIKETHIS]
>
>* [[!DNL Adobe Experience Manager] 6.5文档](../user-guide/home.md)
>* [6.5的一 [!DNL Adobe Experience Manager] 般发行说明](release-notes.md)
>* [适用于6.5的Service [!DNL Adobe Experience Manager] Pack发行说明](sp-release-notes.md)

