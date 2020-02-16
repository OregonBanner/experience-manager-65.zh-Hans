---
title: AEM 6.5 Service Pack 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Service Pack 3。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# 以前 Service Pack 中包含的修补程序和功能包 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.2.0

AEM 6.5.2.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of AEM 6.5 in **April 2019**. It can be installed on top of AEM 6.5.

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.3。
* 添加了配置属性，允许将“体验片段”直接导出到适用于 Adobe Target 的用户定义的工作区。
* 资产用户可以直观地搜索相似图像。AEM 会显示 DAM 存储库中与用户选定图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。请参阅[使用连接的资产](../assets/use-assets-across-connected-assets-instances.md)。

* Enhance具有更多MIME类型的文档类型过滤器以支持多值选项。
* 引入了一个外部“重新处理”工作流以支持多种资源。
* 通过在复制中使用默认资产筛选器优化了 Dynamic Media 的性能。
* 恢复了 DMS7 的裁剪/旋转资产编辑选项。
* 在 VideoPlayer 中实施了加载时使视频静音的选项。
* 修复以确保 Asset UI 列视图仅显示特定租户的内容。
* 修复以允许搜索结果中反映样式可折叠项的更改。

### 资产 {#assets}

**产品增强功能**

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。适用于 CQ-4270245 的修补程序. 请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* 资产用户可以直观地搜索相似图像。AEM 会显示 DAM 存储库中与用户选定图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

**修复**

* 通过 ACP API 生成的 URL 和文件夹元数据中的资产路径未进行 URL 编码。GRANITE-26198：适用于 CQ-4271814 的修补程序
* 无法使用 Assets 界面解压缩名称中带有百分号 (%) 的文件夹的归档文件。NPR-29989：适用于 CQ-4270467 的修补程序
* 触屏UI:在管理发布向导过程中，在发布请求主体中的页面之后添加引用，导致所有资产在页面后发布，当呈现页面时，发布实例中的某些资产会丢失。 NPR-29985：适用于 CQ-4270724 的修补程序
* “取消关联资产”功能无法用于名称中包含特殊字符（成为 URI 编码的字符）的关联资产。NPR-30387：适用于 CQ-4274446 的修补程序
* 编辑内容片段时，使用错误的用户创建此版本。
* 在基于“租户”的系统上创建收藏集失败。NPR-30114：适用于 CQ-4272948 的修补程序
* Asset UI 列视图不遵循当前租户的 dam 根路径，而是访问所有租户的 dam 路径。NPR-30636：适用于 CQ-4275481 的修补程序
* 由于能够看到插入的图像，可通过受限的文件警告窗口实施跨站点脚本 (XSS) 攻击。NPR-30617：适用于 CQ-4270133 的修补程序
* 多租户：保存文件夹属性的租户会看到成功提示和错误消息，其中描述操作未成功，“无法编辑属性。 权限不足。”因此，让租户感到困惑。NPR-30545：适用于 CQ-4275333 的修补程序
* 资产选择器对话框不允许选择资产，因此无法使用相关源替换功能来更新源。NPR-30502：适用于 CQ-4275029 的修补程序
* DAM 更新资产工作流 - 在上传大尺寸的 mp4 文件时处于停滞状态。NPR-30480：适用于 CQ-4271352 的修补程序
* 由于有效负荷为空，“创建审核任务”功能不起作用，使所有后续与审核任务相关的操作失败。NPR-30468：适用于 CQ-4274263 的修补程序
* 通过 Datapower 实施的 Adobe 智能标记存在连接问题。NPR-30026：适用于 CQ-4269457 的修补程序
* 尝试打开左边栏上的筛选器时，Assets UI 列视图引发一个错误。NPR-30501：适用于 CQ-4273862 的修补程序
* 在“资产文件夹”的“已关闭的用户组”(CUG) 属性中添加从 LDAP 同步的组后，不会保存和检索组。NPR-30615：适用于 CQ-4274689 的修补程序
* 筛选搜索样式和方向字段不会将自动完成的值应用于搜索查询。NPR-30620：适用于 CQ-4275724 的修补程序
* 对于某些资产，名称中包含空格和“&amp;”字符的文件夹的资产共享链接显示为空白灰色卡片。NPR-30557：适用于 CQ-4270187 的修补程序
* 文件夹元数据架构表单不会自动检测数据类型，因此，在表单提交中没有创建相关的 TypeHint。NPR-30599：适用于 CQ-4275227 的修补程序
* DMS7 创作 UI 中的裁剪和旋转资产编辑选项被禁用。NPR-30118：适用于 CQ-4273221 的修补程序
* “共享链接”功能在使用 DMS7 配置的 AEM 实例中不起作用。NPR-30080、NPR-30492：适用于 CQ-4273651 的修补程序
* 将 Dynamic Media Scene7 组件添加到页面，然后发布该页面，不会每次都触发 dmscene7 配置。NPR-30641：适用于 CQ-4275962 的修补程序
* AEM 中添加了 IPSJobJournal，以在每个处理配置文件中仅创建一个入侵预防系统 (IPS)。NPR-30490：适用于 CQ-4273614 的修补程序
* Dynamic Media:添加了默认筛选器，以排除资产被复制到AEM发布节点的情况。 NPR-30538：适用于 CQ-4274678 的修补程序
* 为多资源支持引入了一个外部“重新处理”工作流，以允许文件夹作为有效负载。工作流包含两个步骤 - 通过到下一步的元数据映射重新处理没有句柄的资产，并在单个 IPS 作业中将所有没有资产句柄的资产重新上传到 S7。有关更多详细信息，请参阅“配置 Dynamic Media 云服务”。NPR-30489：适用于 CQ-4272903 的修补程序
* 正确的 CSV 擦除正确的 CSV 后，会上传一个错误的 CSV。适用于 CQ-4277694、CQ-4277814 的修补程序
* 特定于要删除的贡献文件夹的图标错误。适用于 CQ-4277580 的修补程序
* 在资产贡献选项卡的用户选取器中选择用户时，表中不显示用户的名称，并且属性页面的“删除用户”对话框中显示错误文本。适用于 CQ-4277875 的修补程序
* 无法在用户选取器中通过选择用户和单击添加操作将参与者添加到资产贡献文件夹。适用于 CQ-4277824、CQ-4278087 的修补程序
* 用户选取器中按小写用户名称搜索不起作用。适用于 CQ-4277958、CQ-4277930 的修补程序
* 非管理员可以在资产贡献文件的新文件夹中发布资产。适用于 CQ-4278200 的修补程序
* dam 用户（非管理员）无法选择将参与者添加到资产贡献文件夹。适用于 CQ-4278192 的修补程序
* “创建”按钮在资产贡献文件夹中可见。适用于 CQ-4277560 的修补程序
* 按相关度排序搜索查询返回 InDesign 文档以及 InDesign 模板。适用于 CQ-4273864 的修补程序
* 如果用户的电子邮件 ID 为大写字母，则该用户无法签入以前签出的那些资产。适用于 CQ-4276575 的修补程序
* “删除”操作仅应用于选定的预设，如果执行该操作后屏幕自动刷新列表，则会显示已刷新的其他预设。适用于 CQ-4261461 的修补程序
* 在 DMHybrid 模式下配置 Dynamic Media 云服务会导致在 Analytics 中创建多个空的报表包，由于 AEM 中没有存储报表包 ID，从而会导致报表包重复。适用于 CQ-4249780 的修补程序
* AEM Aeeets 中对重复名称进行的重命名操作无法同步到 Scene7。适用于 CQ-4276763 的修补程序
* 搜索筛选器面板中错误地显示用户生成内容。适用于 CQ-4273875 的修补程序
* “查找近似项”选项不适用于 TIFF 图像。适用于 CQ-4278238 的修补程序
* 在 VideoPlayer 中实施了加载时使视频静音的选项。适用于 CQ-4266465 的修补程序
* 查看器- videoViewer:poster=none在使用外部视频时工作不正确。 适用于 CQ-4265536 的修补程序
* 在 IE11 和 MS Edge 浏览器中播放视频期间显示“等待”图标。适用于 CQ-4251539 的修补程序
* 3.8 SDK和5.13查看器自述文件不更新，并包含先前发行版中的信息。 适用于 CQ-4273737 的修补程序
* 即使在保存更改之前，也要对内容片段进行版本控制。NPR-30616：适用于 CQ-4273088 的修补程序
* 在缩略图进程中用 Asset#getMetadataValueFromJcr(String) 替换 Asset#getMetadata(String)。NPR-30491：适用于 CQ-4273067 的修补程序
* 上传 jpg 会导致每个资产显示消息的多个实例：“ReplicateOnModifyWorker 复制更新”，从而导致性能降低。
* 使用“提取存档”功能解压缩 zip 存档会导致标题中包含百分号 (%) 的文件夹出现问题。NPR-29990：适用于 CQ-4270467 的修补程序

### 站点 {#sites-6520}

* 如果LiveCopy继承被破坏，Live copy页面将显示语言复制链接，而不是LiveCopy链接。 (NPR-30980)
* 对于新的Blueprint，如果记录数大于40，则仅显示前40条记录。 Blueprint显示记录其余部分的空行。 (NPR-31182)
* 文本组件的富文本编辑器(RTE)插件显示日语和韩语文本的扭曲字符。 (NPR-31331)
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入。 (NPR-30879)
* 开箱即用的基架富文本编辑器(RTE)意外地将内联字体大小应用于元素。 (NPR-31284)
* 当用户关注左边栏字段并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容而不是从左边栏字段复制的内容。 (NPR-31172)
* 当用户向多字段添加“文件上传”字段时，图像路径将存储在组件节点而不是多字段节点中。 (NPR-30882)
* ResponsiveGridExporter API不返回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter接口。 com.day.cq.wcm.foundation.model.impl包声明为私有包。 (NPR-31398)
* 当在非编辑器模式下(在“作者”模式下（不带前缀和／或在“发布者”中）打开包含某些ExperienceFragments的页面时，请求以HTTP状态错误代码500结束。 `editor.html``wcmmode=disabled`(NPR-30743)

### WCM - 页面编辑器 {#wcm-page-editor-6520}

**产品增强功能**

* Enhance具有更多MIME类型的文档类型过滤器，以支持多值选项。 适用于 CQ-4270694 的修补程序

### 内容片段管理 {#content-fragment-management-6520}

* 内容片段模式 UI 使用的查询非常缓慢，最终会导致错误。适用于 CQ-4270807 的修补程序

### UI - Foundation {#ui-foundation}

* 快捷方式触发器阻止用户在特定用户界面中使用“m”、“p”、“e”。NPR-30355：适用于 GRANITE-26346 的修补程序
* 关闭资产搜索UI不会将左边栏重置为内容选择，从而阻止用户随后第二次打开筛选器边栏。 NPR-30509：适用于 CQ-4274716 的修补程序
* 多租户环境：Asset UI 顶部导航不可用，并且引发 JavaScript 错误。NPR-30104：适用于 GRANITE-26344 的修补程序

### 翻译 {#translation-6520}

* 翻译问题 - 只有少数组件使用机器翻译进行了翻译。NPR-30079：适用于 CQ-4273764 的修补程序

### 平台 {#platform-6520}

* AEM 默认邮件发送程序无法通过 TLS v1.2 向远程 SMTP 服务器发送电子邮件。NPR-30476：适用于 GRANITE-26605 的修补程序

### 项目 {#projects-6520}

* dam:folderThumbnailPaths 值未刷新，并且在删除文件夹内的资产后，还显示旧版缩略图。NPR-30424：适用于 CQ-4273667 的修补程序
* 完成“移动”选项后，资产的“标题”和“名称”保持不变。NPR-30647：适用于 CQ-4276265 的修补程序

### 社区 {#communities-6520}

* “用户同步诊断”完全中断，无法工作。NPR-30004、NPR-29943:CQ-4270287、CQ-4271348的修补程序

### Sling {#sling}

* 从 6.3.3.2 升级到 6.5 的实例导致 OSGi 配置重复。NPR-30130：适用于 CQ-4274016 的修补程序

### 集成 {#integration}

* 重新启动实例之前，发布实例上显示的自定义内容错误。NPR-30377：适用于 CQ-4273706 的修补程序
* 在网站中配置 Launch 时，库地址前面带有斜线 (\)，导致每次需要手动干预。NPR-30694：适用于 CQ-4275501 的修补程序

### Forms {#forms-6520}

>[!NOTE]
>
>AEM Service Pack 不包含对 AEM Forms 的修复。它们是通过单独的 Forms 附加组件包交付的。此外，还会发布一个累积安装程序，其中包含对JEE上的AEM Forms的修复。 有关更多信息，请参阅[安装 AEM Forms 附加组件](#install-aem-forms-add-on-package)和[安装 AEM Forms JEE 安装程序](#forms-jee-installer)。

AEM 6.5.2.0 Forms 的重要功能亮点包括：

* 为用于 AEM Forms OSGi 的 `RenderAtClient` API 中的 `PDFFormRenderOptions` 添加了“自动”设置。

#### Forms 附加组件包 {#forms-add-on-package}

**后端集成**

* 无法使用 AWS 托管的负载平衡 URL 来配置“表单数据模型”。NPR-30123：适用于 CQ-4273359 的修补程序
* 使用Web服务定义语言(WSDL)创建表单数据模型(FDM)时，将返回错 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 误消息：NPR-30477:CQ-4272921的修补程序

**通信管理**

* “创建对应UI(CCR UI)再现间歇性地失败，控制台中出现以下错误：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**交互式通信**

* 表单数据模型中标记为必填的字段将按“创建通信 UI”(CCR UI) 中的要求显示。NPR-30623：适用于 CQ-4274902 的修补程序

**Forms - 工作流**

* “监视文件夹”中未映射的输出变量导致调用失败。适用于 CQ-4264451 的修补程序

**HTML5 表单**

* 第二次部署自定义代码或项目时，页面不会呈现，并会出现以下错误：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：适用于 CQ-4272509 的修补程序

* 在浏览模式下使用 NonVisual Desktop Access 读取 HTML5 表单时，Chrome 浏览器会读取表单设计中每个可缩放矢量图形 (SVG) 前的“图形”。NPR-30449：适用于 CQ-4274732 的修补程序

#### Forms JEE 安装程序 {#forms-jee-installer}

**Forms - 文档安全**

* 应用带有时间戳的签名失败，并出现错误：ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 调用错误。NPR-30820：适用于 CQ-4275852 的修补程序

**Forms - 文档服务**

* 如果“SubmitURL”包含与号 (＆)，则在对 renderpdf servlet 发出 POST 请求时，日志中会出现解析错误。NPR-30865：适用于 CQ-4278232 的修补程序

**Forms - Foundation JEE**

* HTMLtoPDF服务在JMX控制台中不显示maxReuseCount。 NPR-30134、NPR-30304：适用于 CQ-4273763 的修补程序
* 通过从AEM Forms Workbench调用Web服务来添加或编辑Web服务连接会引发错误：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105：适用于 CQ-4273217 的修补程序

### 包含的功能包 {#feature-packs-included}

>[!NOTE]
>
>对于 AEM Forms 客户，请先安装任意 AEM Service Pack、累计修复程序或功能包之后，再安装 AEM Forms 附加组件包，这一点至关重要。

#### 站点 {#sites-feature-packs-included}

* 添加了配置属性，允许将“体验片段”直接导出到适用于 Adobe Target 的用户定义的工作区。NPR-29189：适用于 CQ-4249782 的修补程序

#### Forms - 文档服务 {#forms-document-services-1}

* 为用于 AEM Forms OSGi 的 `RenderAtClient` API 中的 `PDFFormRenderOptions` 添加了“自动”设置。NPR-30759：适用于 CQ-4278193 的修补程序

## AEM 6.5.1.0 {#release-6510}

*AEM 6.5.1.0是一个重要版本，其中包括自2019年4月AEM 6.5通用发布以来发布的性能、稳定性、安全性以及关键客户修复和增强*&#x200B;功能。它可以安装在AEM 6.5的顶部。

该 Service Pack 的一些重要功能亮点包括：

* 支持在跟踪事件中包含动态 UI 状态作为自定义属性。
* 包括对在 Dynamic Media Scene 7 中交付 360 度视频资产的支持。
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 资产

* 针对 S3 多部分支持更新了 DAM DMGateway 接口。NPR-29740：适用于 CQ-4226303 的修补程序
* 再现预览 `Only empty tenantId is currently supported` 在升级到AEM 6.5后会生成错误。 NPR-29986：适用于 CQ-4272353 的修补程序
* “删除”对话框不可见，因此不允许删除作业。NPR-29720：适用于 CQ-4271074 的修补程序
* 在属性页面添加资产标题后，用户尝试关闭该页面时，AEM 会再次打开该属性页面。NPR-29627：适用于 CQ-4264929 的修补程序
* VersioningTimelineEventProvider 应该提供 root 版本以及 nt：version 类型的节点。适用于 GRANITE-26063 的修补程序
* 实施了在 AEM DM-Scene7 模式下上传和播放 360 度球面视频的功能。适用于 CQ-4265131 的修补程序
* 如果编辑了源，则 Live Copy 检索错误的状态。适用于 CQ-4265451 的修补程序
* 对 Assets 启用了多站点管理器支持。适用于 CQ-4271453、CQ-4268621、CQ-4257491 的修补程序
* AEM 界面应在时间轴历史记录中显示资产当前版本的其他条目，并显示 Adobe Asset Link 的最新签入注释。适用于 CQ-4262864 的修补程序
* 内容片段时间轴在属性缺失时显示错误消息。 适用于 CQ-4272560 的修补程序
* 扩展到全屏时，Scene 7 视频播放器出现问题。适用于 CQ-4266700 的修补程序
* ZoomVerticalViewer：使用单个图像资产时不应显示“全景”按钮。适用于 CQ-4264795 的修补程序
* 删除 Live Copy 中的儿童模式时应分离 liveRelationship。适用于 CQ-4270395 的修补程序
* 元数据架构仅包含来自全局配置的项目，丢失了来自活跃租户的项目。即使在更改之后，formPath URL 值也会恢复为默认值。NPR-29945：适用于 CQ-4262898 的修补程序
* 发布图像预设到 Brand Portal 失败，显示 500 错误代码。NPR-29510：适用于 CQ-4268659 的修补程序

### 站点

* 在转出期间，不会从 Blueprint 传播空属性和多属性。使用 Blueprint 重置 Live Copy 不适用于组件。NPR-29253：适用于 CQ-4264928、CQ-4264926、CQ-4267722 的修补程序
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537：适用于 CQ-4266129 的修补程序
* 针对日语增强了 AEM 文本组件和文本编辑器功能。NPR-29785：适用于 CQ-4265090 的修补程序
* 使用时间扭曲恢复的页面在版本控制时应该引用正确的图片。NPR-29431：适用于 CQ-4262638 的修补程序
* 样式系统节点从父节点继承到子节点的问题。 NPR-29516：适用于 CQ-4270330 的修补程序
* 将社交发帖设置为 Facebook 身份验证时显示错误消息。NPR-29211：适用于 CQ-4266630 的修补程序
* “内容片段”上呈现的缩略图使用内部日历来表示“日期和时间”字段。NPR-29531：适用于 CQ-4269362 的修补程序
* 在 Coral2 实施中打开权限选项卡时不显示按钮。适用于 CQ-4269419 的修补程序

### 商务

* 为电子商务运行延迟内容迁移时引发 ConstraintViolationException。NPR-29247：适用于 CQ-4264383 的修补程序

### 内容片段管理

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. 适用于 CQ-4270266 的修补程序

### 体验片段

* 将 AEM 体验片段导出到 Adobe Target。适用于 CQ-4265469 的修补程序
* 智能图像无法导出到目标的体验片段。 适用于 CQ-4269606 的修补程序

* 在卡片视图中尝试通过 Omnisearch 移动“体验片段”时，用户会陷入僵局。适用于 CQ-4263848 的修补程序

### WCM - 页面编辑器

* 使用无效选择器时导致反射型跨站点脚本攻击 (XSS)。适用于 CQ-4270397 的修补程序

### 复制

* User-provided data is not escaped on output in the `cq/replication/components/agent` component, resulting in a stored Cross-site scripting (XSS) vulnerability. 适用于 CQ-4266263 的修补程序

### 工作流

* 对话框参与者的日历选取器字段损坏。NPR-29727：适用于 CQ-4270423 的修补程序

### WCM - SPA 编辑器

* 已启用从远程端点获取预渲染的内容。适用于 CQ-4270238 的修补程序
* 打开呈现在服务器端的 SPA 模板页面时在日志中出现警告。适用于 CQ-4270238 的修补程序

### WCM - MSM

* 升级到 AEM 6.4.3 后，多站点管理器需要较长时间转出。适用于 CQ-4271410 的修补程序

### 集成

* BrightEdge 凭证失败，出现连接错误。NPR-29168：适用于 CQ-4265872 的修补程序

* 尝试编辑和保存 AEM Launch 配置时，显示异常消息。NPR-29176：适用于 CQ-4265782/CQ-4266153 的修补程序

### 用户界面

* 添加了对跟踪基础跟踪 API 中特定事件时，作为自定义属性跟踪动态 UI 状态的支持。适用于 GRANITE-26283 的修补程序
* 无法对提交按钮设置跟踪功能。适用于 GRANITE-26326 的修补程序
* 向导无法对提交按钮设置跟踪功能。NPR-29995、NPR-30025：适用于 CQ-4264289 的修补程序

### 社区

* 无法在成员个人资料页面的下拉列表中对齐新徽章。NPR-29381：适用于 CQ-4267987 的修补程序
* 没有审查方权限的访客和成员能够通过粘贴 URL 来查看未批准/待处理的帖子。NPR-29724：适用于 CQ-4271124/CQ-4271441 的修补程序
* 在社区登录时，出现长达 40-50 秒的高响应时间。NPR-29677：适用于 CQ-4269444 的修补程序

### 复制

* 复制代理组件容易受到漏洞攻击，该漏洞会向未经授权的用户泄露敏感信息。NPR-29611：适用于 GRANITE-25070 的修补程序

* OAuth 在每次复制到 Brand Portal 时发生会话泄漏。NPR-30001：适用于 GRANITE-26196 的修补程序

### 项目

* 将资产从 AEM Author /content/dam/mac 文件夹发布到 Brand Portal 不起作用。NPR-29819：适用于 CQ-4271118 的修补程序

### 平台

* HtmlLibraryManager 在缓存失效时删除 crx-quickstart 的所有内容。NPR-29863：适用于 GRANITE-26197 的修补程序

### Felix

* 使用Java11时，系统控制台中不显示内存使用情况详细信息。 NPR-29669

### Forms

AEM 6.5.1.0 Forms 的重要功能亮点包括：

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* 仅限OSGI:支持使用Forms service创建静态PDF文件。
* 为管理员和根用户启用了对 XMLForm.exe 的权限。
* 为 Dynamics 内部部署集成启用了对 ADFS v3.0 的支持。

#### Forms 附加组件包

**后端集成**

* 获取受保护的 Web 服务定义语言 (WSDL) 失败。NPR-29944：适用于 CQ-4270777 的修补程序
* AEM Forms 安装在 IBM WebSphere 上时，创建基于 SOAP 的表单数据模型失败。适用于 CQ-4251134 的修补程序
* 为 Microsoft Dynamics 内部部署集成启用了对 Active Directory 联合身份验证服务 (ADFS) v3.0 的支持。适用于 CQ-4270586 的修补程序
* 数据源的标题发生更改时，表单数据模型不显示更新的标题。适用于 CQ-4265599 的修补程序
* 如果实体或属性的名称包含连字符或空格，则表达式无法计算此类实体和属性。 适用于 CQ-4225129 的修补程序

* 当基元字符串输出中存在冒号时，会观察到错误的输出。 适用于 CQ-4260825 的修补程序

* 即使 REST API 输出中没有任何内容，表单数据模型的调用操作也会引发错误。适用于 CQ-4268828 的修补程序

**自适应表单**

* 在延迟加载期间，无法在“自适应表单片段”中添加新实例。NPR-29818：适用于 CQ-4269875 的修补程序
* 验证组件没有记录或显示“记录文档”模板的任何错误。适用于 CQ-4272999 的修补程序
* 添加了对“自适应表单”禁用布局编辑器的支持。适用于 CQ-4270810 的修补程序
* 已恢复AEM 6.5中自适应表单的验证步骤。CQ-4269583的修补程序

* 自适应表单字段验证失败会中断 Adobe Sign。适用于 CQ-4269463 的修补程序
* 当一个 AEM Forms 实例拥有超过 20 个自适应表单片段，并且所有表单片段的名称均以相同字符串开头时，搜索会返回“无”或最近创建的 20 个片段。适用于 CQ-4264414、CQ-4264914 的修补程序

* Adaptive Forms应用程序与大数据集一起使用时的性能问题。. 适用于 CQ-4235310 的修补程序

* 通过匿名帐户在发布实例上进行访问时，GuideRuntime 脚本加载失败。适用于 CQ-4268679 的修补程序

**Forms - 交互式通信**

* “交互式通信”模板未在允许的组件列表中列出页眉和页脚组件。适用于 CQ-4237895 的修补程序
* 创建包含图像字段的交互式通信打印模板时，图表标题将设置为空白。适用于 CQ-4264772 的修补程序
* 图表的线条颜色在删除后设置为未定义。适用于 CQ-4264762 的修补程序
* 在执行保持更改同步时，在文档片段上所做的布局图层更改会消失。 适用于 CQ-4266054 的修补程序
* “文档片段”中绑定到文本字段的表单数据模型元素不显示继承图标，并且允许绑定。适用于 CQ-4261089 的修补程序
* “打印渠道”呈现 API 没有在 API 中作为参数传递数据的选项。适用于 CQ-4263540 的修补程序
* 当绑定类型从“文本片段”更改为“字符串字段／变量”的“无／数据模型对象”时，代理设置不可见，因为“由代理编辑”复选框会取消选中。 适用于 CQ-4261953 的修补程序
* 在提交代理UI时，生成的Web数据json文件会存储继承取消未绑定字段的信息。 适用于 CQ-4265621 的修补程序

**Forms - 工作流**

* 从自适应表单应用程序的发件箱重新提交表单时，将导致数据丢失。NPR-28345：适用于 CQ-4260929 的修补程序
* 对于不可变情况，保存时不会关闭文档。适用于 CQ-4269784 的修补程序
* Adaptive Forms应用程序已放弃对Microsoft Windows 8.1的支持。CQ-4265274的修补程序
* 当在 AEM Forms 应用程序 Android 版中将大于 2 MB 的图像作为字段级附件附加到的表单上时，应用程序崩溃。适用于 CQ-4265578 的修补程序

* 为分配任务中的“交互式通信打印渠道”启用了预填充选项。适用于 CQ-4265577 的修补程序
* 用户只有成为分配任务的组的成员之后才能查看共享任务。适用于 CQ-4248733 的修补程序
* Windows 上禁止在“自适应表单”应用程序上保存或提交 JEE 应用程序。适用于 CQ-4268704 的修补程序
* 与表单数据模型变量关联的表单数据模型不可见。适用于 CQ-4266554 的修补程序
* 使用变量支持时不支持文档签名的状态变量。适用于 CQ-4266312 的修补程序
* 从工作区中提交带有变音字符的内容失败。适用于 CQ-4263172 的修补程序
* 在升级的设置中，如果打开了工作流进行编辑，则监视文件夹用户界面 (UI) 中会显示错误而不是工作流名称。适用于 CQ-4238579 的修补程序

**Forms - 管理**

* 上传 xsd 或 schema.json 以外的扩展名时，上传不会发生，并且不会生成任何错误消息。适用于 CQ-4266716 的修补程序

**Forms - 通信管理**

* AEM 6.5 Forms“创建通信 UI”(CCR UI) 打开由 AEM 6.3 Forms 创建的通信失败。适用于 CQ-4266392 的修补程序
* 如果 DDE 数据类型是数字类型，则 XDP 中的求和功能将不起作用。适用于 CQ-4227403 的修补程序
* 内存中的字母缓存失效逻辑将被更新，因为当资产发布时，其最后修改时间不会更新。适用于 CQ-4250465 的修补程序
* 无法发布文档片段、DD 和 Letters。适用于 CQ-4272893 的修补程序

#### Forms JEE 安装程序

**PDF 生成器**

* 使用 64 位 JDK 时，将 CAD 文件转换为 PDF 失败。NPR-29924、NPR-29925：适用于 CQ-4272113 的修补程序
* 将 PhantomJS 的名称替换为 WebToPDF 以进行 HTMLtoPDF 转换。NPR-29933：适用于 CQ-4234545 的修补程序
* 将 zip 文件转换为 PDF 时出现错误。适用于 CQ-4268628 的修补程序

**Forms - Designer**

* 对使用 AEM Form Designer 创建的静态 PDF 执行全面的辅助功能检查时，由于缺少语言属性，“主要语言”检查失败。适用于 CQ-4272923、CQ-4271002 的修补程序

**Forms - 文档安全**

* 带硬件安全模块(HSM)的数字签名在Java 11和Java 8的OSGi linux上不工作。 NPR-29838：适用于 CQ-4270441 的修补程序
* 带硬件安全模块 (HSM) 的数字签名在 JEE Linux 上，以及所有受支持的应用程序（例如，JBoss 和 Websphere）上不起作用。NPR-29839：适用于 CQ-4266721 的修补程序
* 在 PDF 中使用“PDF 高级电子签名”(PAdES) 验证签名会生成 InvalidOperationException。NPR-29842：适用于 CQ-4244837 的修补程序
* 增加了对Office 2019的Document Security Extension支持。 适用于 CQ-4254369、CQ-4259764 的修补程序

**Forms - 文档服务**

* “表单”字段无法转换为PDF/A-1b，且没有外观指示。 NPR-29940：适用于 CQ-4269618 的修补程序

* OSGi:无法确定呈现过程中生成的页数。 NPR-28922：适用于 CQ-4270870 的修补程序
* 在AEM Forms OSGi中支持使用Forms service的静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 无法更改对 XMLForm.exe 的权限。NPR-29828、NPR-29237：适用于 Q-4267080 的修补程序
* AEM Forms 服务器的输出模块创建的静态 PDF 不会使用所创建文档的语言来填充语言属性/标记。NPR-27332：适用于 CQ-4271002 的修补程序

**Forms - Foundation JEE**

* 最终部件中不可用的 pdfg_srt 会导致安装程序失败。NPR-29854：适用于 CQ-4270137 的修补程序
* LCBackupMode.sh 不起作用。NPR-29840：适用于 CQ-4269424 的修补程序
* UDP 端口引用应该从 WebSphere 的用户界面 (UI) 中删除。适用于 CQ-4264782 的修补程序

### 包含的功能包

#### 资产 -包括

* 对 Assets 启用了多站点管理器支持。For more information, see [Reuse assets using MSM for Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199：适用于 CQ-4259922 的修补程序

#### 站点——包含

* 将 AEM 体验片段导出到 Adobe Target。For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). 适用于 CQ-4265469 的修补程序

#### Forms - 文档服务 -包括

* 仅限OSGi:在Output和Forms service中添加了新属性PAGECOUNT。 NPR-28922：适用于 CQ-4270870 的修补程序
* 仅限OSGi:支持使用Forms service创建静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 为管理员和根用户启用了对 XMLForm.exe 的权限。NPR-29237：适用于 CQ-4267080 的修补程序

### OSGi 包和内容包

以下文本文档列出了 AEM 6.5.1.0 中包含的 OSGi 包和内容包

AEM 6.5.1.0 中包含的 OSGi 包列表

[获取文件](assets/6_5-bundle-list.txt)

AEM 6.5.1.0 中包含的内容包列表

[获取文件](assets/6_5-content-package-list.txt)
