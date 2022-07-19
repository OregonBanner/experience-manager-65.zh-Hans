---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5发行说明，其中概述了发行信息、新增功能、安装方式和详细的更改列表。”'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 9f957175573eeb2b40d79a5087dc3034c56819cc
workflow-type: tm+mt
source-wordcount: '3742'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.13.0 |
| 类型 | Service Pack版本 |
| 日期 | 2022 年 5 月 26 日 |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## 中包含的内容 [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0包括自2019年4月6.5版首次发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) on [!DNL Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.13.0是：

* 在自适应表单中使用不可见的CAPTCHA:现在，您只能在可疑活动时使用隐形验证码来显示验证码挑战。 如果未发现可疑活动，则不会显示验证码质询。 它有助于评估人工表单的完成情况，而无需使用复选框要求，减少自定义工作，并改善最终用户体验。 (NPR-38500)

* 添加了对REST端点的表单数据模型后处理器中获取响应标头的支持。 (NPR-38275)

* 现在，在生成自适应表单翻译文件时，生成的XLIFF文件的文本序列与相应自适应表单中的组件序列相同。 (NPR-37700)

* 当您将自适应表单本地化，并对基本语言的文本做出哪怕是细微的更改时，所有其他语言都将丢失完整的翻译。 此问题已在 [!DNL Experience Manager] 6.5.13.0。 (NPR-37189)

* Forms的无障碍功能改进：

   * 增加了对屏幕阅读器的支持，以识别表的标题和正文作为继续和连接的实体。 它有助于屏幕阅读器正确导航表。 (NPR-37139)
   * 为屏幕阅读器添加了支持，可在对话框打开之前停止导航HTML工作区。 (NPR-37134)
   * 添加了在Forms Designer中为超链接指定屏幕Reader文本的功能。(NPR-36221)

中引入了以下错误修复、主要功能和增强功能 [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* 尝试编辑只读下拉字段时，下拉值将重置为空。 (NPR-38389)
* 如果视频文件中没有音频，则用户无法摄取视频(.mp4)资产。 DAM更新资产工作流失败，并反映一条错误消息。 (NPR-38116)
* 使用移动资产向导移动包含资产的文件夹时，工作流会失败，并会反映一条错误消息。 (NPR-38061)
* FLV视频配置文件的FFmpeg转码工作流失败。 (CQ-4343249)
* 更新到 [!DNL Experience Manager] 6.5 SP10中，资产元数据编辑器无法正常工作。 (CQ-4341359)
* 打开智能收藏集时，该收藏集会随搜索过滤器应用为“发布”而保存，搜索过滤器会自动更改为“未发布”。 (CQ-4341191)
* 在 **[!UICONTROL 用户首选项]**，标签 **[!UICONTROL 排序依据]**、下拉按钮和资产主页上排序选项中的其他选项，不会反映在选定的语言中。 (CQ-4339306)
* 向 **[!UICONTROL 元数据架构]**, **[!UICONTROL 取决于]** 列表不反映下拉列表的字段标签。 (ASSETS-9442)
* 资产元数据已禁用下拉列表，但不保留值。 (ASSETS-8918)
* 使用 **[!UICONTROL 更多详细信息]** 选项 **[!UICONTROL 列]** 视图，显示的注释不正确。 (ASSETS-8851)
* 创建具有不同版本的重复资产时，不会生成演绎版。 (ASSETS-8607)

* 非管理员用户能够发布其他用户已签出的资产。 (NPR-38128)
* 维度查看器在Chrome 97上无法正常运行。 (CQ-4340456)
* 资产下载按钮在资产详细信息页面上不显示完整菜单。 (CQ-4336703)
* 使用“链接共享”时，链接共享窗口中的某些字符串不会本地化。 (CQ-4330540)
* 在“管理发布”中添加项目时，反映选定项目计数的字符串不会进行本地化。 (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* 在AEM作者上为Dynamic Media资产进行基于令牌的安全预览。 (ASSETS-4995)
* 在中为Dynamic Media创建图像预设时 [!DNL Experience Manager]，则允许的最大值在用户界面中限制为2000x2000像素。 当宽度或高度的值增加到2001像素时， **[!UICONTROL 保存]** 按钮。 (ASSETS-5691)
* 用户可能会阻止某些文件格式上传到Dynamic Media。 (ASSETS-5693)
* 辅助功能 — 如果图像预设用户界面上的图像上未实施Alt属性，那么依赖屏幕阅读器的视觉障碍用户将受到影响。 (ASSETS-9817)
* 辅助功能 — 当屏幕阅读器在向下箭头模式下导航到时，屏幕阅读器会讲述“时间轴区段”和“操作”选项卡中存在的图像，这些图像的未标记图像会对屏幕阅读器造成影响。 (ASSETS-5651)
* 辅助功能 — 屏幕阅读器受到影响，因为在使用（浏览/光标）模式导航时，视频播放器的“EmailLink”对话框中的“Send Email”按钮的描述性名称（发送电子邮件）没有讲述。 (ASSETS-5641)
* 辅助功能 — 使用键盘上的TAB键导航时，在“图像集编辑器”页面中调用“撤消”按钮后，键盘焦点未移至“重做”按钮，该按钮会显示在该按钮中。 (ASSETS-5582)
* 辅助功能 — 依赖屏幕阅读器的用户会受到影响，因为“属性”标题下未提供图像集图像的Alt属性。 (ASSETS-5576)
* 辅助功能 — 屏幕阅读器不会讲述的是 `Cannot save this set` 文本 `Cannot save this set` 警报，使用标题快捷键导航时 `H`和向下箭头键。 (ASSETS-5569)
* 辅助功能 — 依赖屏幕阅读器的用户在表单中导航会受到影响。 如果NVDA没有讲述“宽度和高度”旋转控件的标签信息，他们很难了解有关表单控件的信息。 在NVDA表单模式“F”中导航时，响应式图像裁剪标题下显示的这些控件。 (ASSETS-5393)
* 在网站上添加Dynamic Media组件后和发布页面后，新添加的Dynamic Media资产在已发布的页面上不可见，也无法在预览页面中查看。 图像和视频资产类型均出现此问题。 (ASSETS-9467)

## 商务 {#commerce-6513}

* “everyone”有jcr:write on `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* 商务产品的本地排序不再有效。 (CQ-4343750)
* 更改属性后，无法从搜索结果页面快速发布产品。 (CQ-4343318)

## CRX {#crx-6513}

* 如果包具有特殊字符，则无法下载该包 `+` 在包名称中。 (NPR-38102)

## [!DNL Forms] {#forms-65130}

<!-- * When you use the prefill service to fill an adaptive form that contains a fragment and the fragment contains a Text box that supports rich text, the form fails to submit, and the following error occurs:

  `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542) -->

* 单选按钮、复选框和文件上传组件未正确从德语翻译为英语。 (NPR-38527)
* PDF417条形码编码由 [!DNL Experience Manager] Forms对单选按钮组无效。 (NPR-38525)
* 提交自适应表单时出现以下错误。
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* “从记录文档中排除隐藏的字段”选项不起作用。 (NPR-38512)
* 将Forms容器组件添加到站点页面后，用户无法遍历其他站点页面，并且某些情况下站点页面会挂起。 出现间歇性问题。 (NPR-38506)
* 应用后，用户在自适应Forms中体验到重叠的文本 [!DNL Experience Manager] 6.5 Service Pack 11。 (NPR-38376、CQ-4342472)
* 用户在将自适应表单面板移动到新的响应式布局时遇到异常。 (NPR-38369)
* 未为客户端库启用ECMASCRIPT 6(ES6)支持 ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* 当您使用 [!DNL Experience Manager] 工作流程用希伯来语发送电子邮件，用户端收到的电子邮件包含问号(??)，而不是希伯来语文本(NPR-38296)。
* 用户将随机注销 [!DNL Experience Manager] 发布实例和自适应表单提交失败。 问题出现在 [!DNL Experience Manager] 使用Dispatcher的实例。 (NPR-38285)
* 当您在AdobeLaunch的规则中使用getFormDataString选项捕获自适应表单数据时，该选项不会返回自适应Forms数据。 (NPR-38283)
* [!DNL Experience Manager] 6.5 Forms已弃用java.acl.Group相关API，error.log文件中显示以下错误消息：
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* 使用德语创建的Forms无法翻译成英语或任何其他语言。 (NPR-38280)
* 使用自适应表单的本地化版本时，相应的记录文档(DoR)不会本地化。 (NPR-38235)
* 当您使用“发送电子邮件”步骤将附件与电子邮件一起发送时，附件不会保留在“工作流”步骤中指定的名称。 (NPR-38216)
* 发布新版本的信件时，用户无法打开以前版本的信件的草稿。 (NPR-38215、CQ-4342515)
* 在按钮单击配置为自适应表单规则时调用AEM Forms JEE服务SOAP端点服务方法时，SOAP服务失败，但出现以下异常：
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* 使用com.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP将PDF转换为XDP格式时，将返回无效的XDP文件。 (NPR-38140、CQ-4342099)
* 当多个用户使用通信管理生成不同的信件时，在预览时，会向某些用户显示错误的信件。 (NPR-38134)
* 嵌入在SITES页面中的AEM Forms组件使用width属性，该属性的值以%为单位，且根据W3CHTML验证无效。 用户在HTML验证期间遇到解析错误。 (NPR-38124)
* 自适应表单中大多数OOTB主题的单选按钮和复选框项目未包含在Tab键顺序中(NPR-38108)
* 当用户在执行工作流时向注释部分添加HTML标记时，将呈现HTML标记。 (NPR-37591)
* 导入和发布包含新XDP文件的信件时，无法在Publish实例上预览这些信件。 但是，如果使用同一CMP文件第二次导入和发布信件，则信件会成功预览。 (CQ-4343599)
* 具有准备数据处理属性集的表单无法在HTML工作区中呈现。 (CQ-4343294)
* 对于使用Forms 6.5 Designer创建的静态PDF forms,PDF辅助功能失败，并出现错误 `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* 应用AEMForms-6.5.0-0038(log4jv2.16)修补程序后，无法使用OCR的PDFG服务将图像转换为PDF。 (CQ-4342450)
* 条形码SSCC-18显示错误值。 Forms服务器会忽略条形码右侧的值。 (CQ-4342400)
* 无法将Microsoft® Word文件导入Forms Designer。 用户遇到错误 `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)
* 在Forms 6.5 Designer中，当您打开使用Forms 6.1 Designer创建的表单并编辑文本框时，段落间距会超出指定的间距。 删除了之前对空格的所有设置，并且需要手动重新设置文本框的格式。 (CQ-4341899)
* 用户无法在作业清除计划程序中设置自定义时间。 (CQ-4339192)
* 用户无法更新端点管理UI下的任何配置，并遇到错误 ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* 对于无效标记，错误消息的正常处理无法按预期工作。 (NPR-38106和CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。


## Granite {#granite-6513}

* Omnisearch会为没有读取权限的用户返回结果。 (NPR-38373)
* 为启用ES6 `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## 集成 {#integrations-6513}

* 已弃用的UserInfoServlet中的Test &amp; Target服务上的资源解析程序会话泄漏。 (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak — 索引和查询 {#oak-6513}

* 适用于6.5.13.0的Oak版本现已更新至1.22.11。 (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## 平台 {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* 升级依赖项 `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5。 (NPR-37999)
* 由于路径字段建议导致的作者负载较高。 (CQ-4341826)
* 当用户将项目从卡片视图更改为日历视图时，必须刷新页面。 (CQ-4340368)
* 标记因权限限制而丢失。 (CQ-4339543)
* 在路径选择中报告的搜索和过滤功能存在多个问题。 (CQ-4339402)
* 停止在6.5中使用DTM — 切换到Launch for Omega Instrumentation并添加Gainsight支持。 (CQ-4337809)
* 根据设置的路径字段筛选器属性限制路径字段组件搜索函数。 (CQ-4309556)
* [!DNL Experience Manager] 平台6.5:中文区域设置命名修复。 (CQ-4308978)
* 切换到Launch for Omega Instrumentation。 (NPR-38377)
* [!DNL Experience Manager] 平台6.5:中文区域命名修复。 (CQ-4308978)

## 复制 {#replication-6513}

* 将用户节点从“创作”发布到“发布者”失败。 (NPR-38005)

## [!DNL Sites] {#sites-6513}

### 管理员 {#sites-admin-6513}

* 修复了SP 12中引入的在移动页面时可能导致问题的回归。 (SITES-5298)

### 经典用户界面 {#sites-classicui-6513}

* RTE:将新图像拖动到现有图像的顶部时，更新的图像不可见。 (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### 内容片段 {#sites-contentfragments-6513}

* 支持在子配置中创建内容片段模型。 (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* 在内容片段模型中使用“唯一字段”验证时提高性能。 (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* 缩短打开内容片段模型编辑器时的响应时间。 在Assets中具有大量片段的客户在打开时可能会遇到错误。 (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* 修复了在从6.5.11更新到6.5.12时引入的可能导致内容片段模型编辑器错误的回归。 （SITES-5088和SITES-4967）

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* 改进了内容片段模型编辑器用户界面的本地化。 (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* 修复了在Dispatcher中使用作者服务器时，关闭内容片段编辑器可能导致错误的问题。 (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* 修复了在RTE字段中使用验证时无法保存模型的问题。 (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* 布尔属性未在“title”中显示字段文本而显示“属性名称”的内容片段问题。 (NPR-38244)
* 通过查询变量通过Postman运行持久查询时出错。 (NPR-38251、NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* 内容片段组件：修复了6.5 SP7的“将标题处理为段落”选项中的回归。 (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* 修复了6.5.11中引入的可能导致资产搜索错误的回归。 (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* 使用 **[!UICONTROL 编辑]** 搜索结果可能会导致 `Not Found` 错误。 (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* 如果没有硬页面刷新，ContextHub UI模型将无法正常呈现。 (NPR-38212)

### 电子邮件编辑器 {#sites-emaileditor-6513}

* 为即将发行的电子邮件核心组件提供支持 [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445和NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### 体验片段 {#sites-experiencefragments-6513}

* 在体验片段的引用中使用导航到页面操作时，会打开错误的页面。 (NPR-38062)
* 来自XF模板的布局属性在页面侧未观察到。 (NPR-38214)
* 改进了XF参考计算的性能。 (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### 页面编辑器 {#sites-pageeditor-6513}

* 改进了中没有inlineEditing或dropTarget功能的组件的撤消 `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 样式系统下拉列表可能位于页面顶部而不是组件的上下文中(对于使用 `cq:editConfig` “afteredit:REFRESH_PAGE”。 此问题现已解决。 (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* 文本组件在添加到嵌套布局容器时未对齐。 (NPR-38193)
* 当组件没有样式系统配置时，会显示空样式选项卡；现在，当不存在配置时，选项卡处于隐藏状态。 (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 资产 `useLegacyResponsiveBehaviour` 仅在经过身份验证后才可正常工作。 (NPR-37996)
* 将jquery-ui升级到最新版本会导致编辑器损坏。 (SITES-5647)

### 安全性 {#sites-security-6513}

* 用户组管理用户界面有时无法删除用户，尤其是在具有+20个用户的组中。 (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* 站点地图生成器和规范标记添加了对不带.html的URL的支持。 (CIF-2647)
* 添加对使用noindex配置删除替代语言的支持。 (CIF-2496)
* 添加对提供自定义URL的支持，以覆盖内容接近相同的页面的默认规范URL。 (CIF-2747)

### SPA Editor和SDK {#sites-spa-sdk-6513}

* 从6.5.13开始，在通过SPA编辑器进行编辑之前，您不必再在JCR中创建容器组件节点。 A `virtual container` 会在通过SDK保存之前创建。 (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### 模板编辑器 {#sites-templateeditor-6513}

* 修复了发布更改的模板并未发布所有依赖项的回归。 (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemmiladedResource valueMap应允许根据ValueMap API进行深层读取。 (NPR-38439)

## Sling {#sling-6513}

<!-- OBSOLETE BASED ON CQDOC-19400 * Memory leak in `DiscoveryLiteDescriptor`. (NPR-38288) -->
* 更新 `sling-javax.activation` 包含SLING-8777修补程序的包。 (NPR-38077)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## 翻译项目 {#translation-6513}

* 将为引用的页面/体验片段创建多个启动项。 (NPR-38263)
* 自Service Pack 10起，更改了向翻译项目添加页面的行为。 翻译项目不包含新创建的页面 [例如：test-page-women-2] 在列表上，选择新创建页面的父项后 [而不是直接创建新页面]. (NPR-38256)
* 添加 `cq:isTranslationLaunch` 属性。 (NPR-38224)
* 正在为具有引用的XF且其中包含资产的页面创建Launch。 (NPR-38199)
* [!DNL Experience Manager] 更新翻译内存不起作用。 (NPR-38196)
* 为启用ES6 `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* 最新的18n包，用于翻译 [!DNL Experience Manager] 6.5。 (CQ-4339505)

## 用户界面 {#ui-6513}

* 更新至 `favicon.ico` 中使用的Experience Manager。 (CQ-4315324)
* 在开始页面>工具部分上，单击 [!DNL Experience Manager] 图标， [!DNL Experience Manager] 导航屏幕应会弹出。 (NPR-38417)
* 为启用ES6 `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* 为启用ES6 `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* 触屏UI中的日期选取器以韩语显示。 (NPR-38079)
* 在重新排序字段时，使用多个字段创作对话框会丢失单选按钮选择值。 (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM（营销活动）6.5:中文区域设置命名修复。 (CQ-4308973)
* com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification中的ResourceResolver未关闭(NPR-38286)

## 安装 [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0要求 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以了解详细说明。
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 6.5.13.0，在其中一个使用包管理器的创作实例上。

>[!NOTE]
>
>Adobe不建议删除或卸载 [!DNL Experience Manager] 6.5.13.0包。

### 在上安装Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。

1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包并单击 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能会间歇性地在任何浏览器上发生。

**自动安装**

可以使用两种不同的方法自动安装 [!DNL Experience Manager] 6.5.13.0。

* 将包放入 `../crx-quickstart/install` 文件夹。 包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0不支持Bootstrap安装。

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.13.0)` 在 [!UICONTROL 已安装的产品].

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.3或更高版本(使用Web控制台： `/system/console/bundles`)。


### 安装 [!DNL Experience Manager] Forms附加组件包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您没有使用 [!DNL Experience Manager] Forms。 的修复 [!DNL Experience Manager] Forms在计划后一周通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack版本。

1. 确保您已安装 [!DNL Experience Manager] Service Pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)中列出的相应 Forms 附加组件包。
1. 按照 [安装AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 安装 [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。的修复 [!DNL Experience Manager] JEE上的Forms通过单独的安装程序交付。

有关为 [!DNL Experience Manager] Forms（在JEE上）和部署后配置中，请参阅 [发行说明](jee-patch-installer-65.md).

>[!NOTE]
>
>安装的累积安装程序之后 [!DNL Experience Manager] Forms，安装最新的Forms附加组件包，从 `crx-repository\install` 文件夹，然后重新启动服务器。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.13.0在 [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://)。

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象可在Maven中央存储库中使用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，使用 `apis` 作为值，对于 `dependency` 标记。

## 已弃用功能 {#removed-deprecated-features}

以下是标记为已弃用的特性和功能列表 [!DNL Experience Manager] 6.5.7.0。功能在最初被标记为已弃用，之后在将来的版本中被删除。 提供了备用选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | 的 **[!UICONTROL AEM云服务选择加入]** 屏幕已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成在 [!DNL Experience Manager] 6.5.此集成支持Adobe Target Standard API。 API使用Adobe IMS和 [!DNL Adobe I/O]. 它支持AdobeLaunch在工具方面日益发挥的作用 [!DNL Experience Manager] 页面，则选择加入向导在功能上与此无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O] 集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR连接器已在 [!DNL Experience Manager] 6.5。 | 不适用 |

## 已知问题 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [AEM包含GraphQL索引包1.0.3的内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 10或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装 [!DNL Experience Manager] 6.5.x.x:
   * “配置Adobe Target集成时， [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target时，会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

* 在尝试移动/删除/发布内容片段或站点/页面时，当获取内容片段引用时会出现问题，因为后台查询失败；即，该功能不起作用。
要确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 [!DNL Experience Manager] 6.5.13.0:

* [Experience Manager6.5.13.0中包含的OSGi包列表](/help/release-notes/assets/65130_bundles.txt)

* [Experience Manager6.5.13.0中包含的内容包列表](/help/release-notes/assets/65130_packages.txt)

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

