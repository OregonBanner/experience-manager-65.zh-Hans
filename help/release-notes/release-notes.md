---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找发行信息、新增功能、安装操作方法，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: c98ca7cafd559aaf0b0b889f8f03690de880e944
workflow-type: tm+mt
source-wordcount: '3975'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2022 年 11 月 24 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包含的内容 [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0包括自2019年4月6.5版首次发布以来发布的新增功能、客户请求的关键增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* 如果Experience Manager中的资产移动失败，仍可以重命名资产。 (NPR-38753)
* 在 [!UICONTROL 列表视图]，则缺少某些标题。 (CQ-4345746)
* 屏幕阅读器不会读出 [!UICONTROL 关联] 按钮。 (ASSETS-6938)
* 屏幕阅读器会错误地检测资产导航页面上带有文件夹列表的文件夹图标。 (ASSETS-6936)
* 复制收藏集时，图像缺少空 `alt` 属性或角色=&quot;presentation&quot;。 因此，图像会向屏幕阅读器用户显示。 (ASSETS-6932)
* 对资产添加注释时显示的文本没有4个:5:与背景颜色相比，对比度为1。 (ASSETS-6931)
* 在资产属性页面的IPTC选项卡中，当您调整页面宽度时，页面内容不适合，从而导致水平滚动。 (ASSETS-6929)
* 在您过滤资产时， [!UICONTROL min] 和 [!UICONTROL max] 字段在输入值后会消失。 (ASSETS-6925)
* 在“Experience Manager收藏集”中，屏幕阅读器不会读出 [!UICONTROL 电子邮件] 字段。 (ASSETS-6923)
* 对元素添加注释时，缺少替换文本。 (ASSETS-6922)
* 如果文本在日期选取器字段的小时数和分钟数中写入，则不会显示文本错误消息。 仅使用红色标识错误。 (ASSETS-6852、ASSETS-6921、ASSETS-6920、ASSETS-6907)
* 中的替换文本 `[role='img']` 文件筛选器中缺少。 (ASSETS-6919)
* 屏幕阅读器的公告不正确 [!UICONTROL 创建] 子菜单。 (ASSETS-6916)
* 在Experience Manager收藏集中，删除按钮 `X` 没有要向屏幕阅读器朗读的任何文本。 (ASSETS-6912)
* 在Experience Manager中使用“颜色对比度分析器”时，日历小组件的日期选取器中，当前日期与所选日期之间没有颜色差异。 它的对比度与相邻颜色至少为3:1。 (ASSETS-6911)
* 在Experience Manager文件中，从 [!UICONTROL 计划] “管理发布”中的单选按钮，单选按钮选项名称和状态由屏幕阅读器宣布。 但是， **计划** 标签未宣布。 (ASSETS-6908、ASSETS-6906)
* 排序图标缺少替换文本。 (ASSETS-6904)
* 在资产属性页面上，字段名称 `Person` 在IPTC扩展选项卡中，屏幕阅读器不会宣布标签。 屏幕阅读器只会朗读可编辑且当前为空的字段，但不会朗读标签名称。 (ASSETS-6903、ASSETS-6848)
* 无法使用键盘显示注释工具。 使用鼠标绘制图像以显示“注释”工具。 (ASSETS-6899)
* 在Experience Manager收藏集中， **高级** 选项卡显示边界与相邻颜色之间的对比度不正确。 (ASSETS-6895)
* 编辑资产时，某些元素的ARIA属性值不正确。 (ASSETS-6894)
* 创建工作流时，屏幕阅读器无法正确识别标题。 (ASSETS-6892)
* 复制收藏集时，SVG图像删除按钮 `X` 缺少role=&quot;presentation&quot;的IMG。 因此，图像会向屏幕阅读器用户显示。 (ASSETS-6890)
* 在 **基本** 选项卡，屏幕阅读器无法正确地读出“标记”字段的展开或折叠状态。 (ASSETS-6889)
* 的 **基本** 选项卡，其中包含ID重复的页面。 (ASSETS-6888)
* 在文本框中指定值时，创建工作流时用于定义标题的文本字段的标签会消失。 (ASSETS-6887)
* 共享链接时的收件人列表会显示为带有标题的数据表，但从语义上讲，它不会被标识为屏幕阅读器用户的数据表。 (ASSETS-6886)
* 中未显示表示空字段的错误消息 `Add Email Address` 字段。 错误仅使用颜色表示。 (ASSETS-6885、ASSETS-6843)
* 占位符文本、路径和替换文本与其背景颜色相比，至少没有4.5:1的对比度。 (ASSETS-6884、ASSETS-6865)
* 保存智能收藏集时，某些ARIA属性的值无效。 (ASSETS-6882)
* 保存智能收藏集时，某些标签未正确与屏幕阅读器关联。 (ASSETS-6881)
* 在资产属性的IPTC选项卡中，屏幕阅读器不会读出关键字表单字段的标签。 (ASSETS-6879)
* 在Experience Manager收藏集中， [!UICONTROL 电子邮件] 字段未被标识为必填字段，如果您未指定值，则不会显示任何错误消息。 (ASSETS-6877)
* 在Experience Manager文件中， **链接共享** 屏幕显示在 `Add Email Address`. 仅在使用颜色时才识别错误。 (ASSETS-6876、ASSETS-6875)
* [!UICONTROL 裁剪和地图] 编辑资产时，选项没有程序化名称。 (ASSETS-6874)
* 与背景颜色相比，“筛选器”文本缺少4.5:1的合同比例。 (ASSETS-6873)
* 与背景颜色相比，主导航页面上文件夹名称的文本没有4.5:1的对比度。 (ASSETS-6872)
* 执行 [!UICONTROL 复制] 集合操作， **[!UICONTROL 添加用户]** 组合框表单控件与其可见标签没有正确关联。 (ASSETS-6870)
* 屏幕阅读器不会读出 [!UICONTROL 创建] 按钮。 (ASSETS-6869)
* 与背景颜色相比，“范围”、“工作流”和“时区”选项的对比度没有4.5:1。 (ASSETS-6868)
* 屏幕阅读器错误地宣布 **时间轴** 列。 (ASSETS-6864)
* 保存智能收藏集时，缺少某些ARIA角色的子元素。 (ASSETS-6862)
* 在共享资产时，需要ARIA属性 `Search/Add Email Address` 字段。 (ASSETS-6860)
* 的 **地图** 对话框无法使用键盘显示。 而是需要单击鼠标来显示“映射”对话框。 (ASSETS-6859)
* “资产属性”页面“基本”选项卡上某些ARIA角色缺少子元素。 (ASSETS-6858)
* 资产属性的IPTC选项卡中提供的空文本输入字段与其相邻颜色相比没有3:1的对比度。 (ASSETS-6854、ASSETS-6847)
* 配置文件图标位于 **时间轴** 屏幕阅读器未正确检测区域。 (ASSETS-6850)
* 屏幕阅读器不会宣布“资产属性”的“基本”选项卡中提供的“审阅状态”组合框是只读字段。 (ASSETS-6849)
* 屏幕阅读器无法正确读出“全选”和“注释”复选框的标签。 (ASSETS-6846)
* 键盘焦点跳过 `About Adobe Experience Manager` 选项 **显示帮助** 菜单。 (ASSETS-6845)
* 在卡片视图中使用键盘箭头键浏览文件夹列表时，屏幕阅读器无法正确读出选定的文件夹。 (ASSETS-6844)
* 在将PDF上传到Experience Manager时，内存使用率会不断增加。 (ASSETS-16889)
* 当工作流将.ZIP文件转换为Assets中的文件夹名称时，它不会保留.ZIP文件名的大小写。 (ASSETS-16712)
* 从Brand Portal切换到Experience Manager6.5时，当您首次应用该过滤器时，用户谓词过滤器不显示相应的结果。 (ASSETS-15932)
* 无法对视频添加注释。 (ASSETS-15217)
* **管理发布** 选项会对于没有复制访问权限的用户而消失，并且 `READ` 和 `WRITE` 访问 `ETC` 和 `VAR`. (ASSETS-15007)
* 对于具有多个引用的资产，属性页面的加载时间会增加。 (ASSETS-14182)
* 从Brand Portal取消发布图像时，Experience Manager也会从Dynamic Media取消发布该图像，因此实时网站上不会显示任何图像。 (ASSETS-14118)
* Dynamic Media中智能裁剪卡的XSS问题。 (ASSETS-14212、ASSETS-14208、ASSETS-13704)
* Dynamic Media的查看器预设中存在XSS问题。 (ASSETS-13822)
* 在AEM上预览DM资产时验证用户访问权限。 (CQ-4314757)


## 商务 {#commerce-6515}

* 创建存储页面失败，停止了整个目录转出进程。 (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### 主要功能 {#keyfeatures}

* AEM Forms Designer现在在 [西班牙语区域设置](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). (LC-3920051)
* 您现在可以使用 [使用Microsoft® Office 365邮件服务器协议（SMTP和IMAP）进行身份验证的OAuth2](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* 您可以设置 [在服务器上重新验证](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) 属性设置为true，以标识要从服务器端记录文档中排除的隐藏字段。 (NPR-38149)
* AEM Forms Designer要求使用32位版本的Visual C++ 2019 Redistributable(x86)。  (NPR-36690)

### 修复 {#fixes}

* 切换自适应表单的数据禁用属性后，单选按钮和复选框组的外观不会发生更改。 (NPR-39368)
* 翻译自适应表单后，某些翻译会丢失且无法正确显示。 (NPR-39367)
* 将页面的属性设置为隐藏时，不会从表单集中删除该页面。 (NPR-39325)
* 在“记录文档”中，页面末尾的动态脚注部分不存在。 (NPR-39322)
* 为自适应表单生成记录文档时，单选按钮和复选框仅允许垂直对齐。 用户无法为单选按钮和复选框设置水平对齐方式。 (NPR-39321)
* 部署通信管理后，如果多个用户尝试访问表单，则org.apache.sling.i18n.impl.JcrResourceBundle.loadPotementLanguageRoots会成为瓶颈，并且大部分线程都会被触发。 即使服务器的负载非常低，加载各种表单页面请求通常也需要超过1分钟。 (NPR-39176、CQ-4347710)
* 在自适应表单中，当您在延迟加载的自适应表单片段中使用富文本字段时，会遇到以下一些错误：
   * 不能编辑内容或将任何内容附加到富文本字段。
   * 不接受应用于富文本的显示模式。 
   * 提交表单时，不会显示最小字段长度的错误消息。
   * 此富文本字段的内容已多次包含在生成的submit-XML中。 (NPR-39168)
* 在自适应表单中使用日期选取器选项时，无法将值转换为正确的格式。 (NPR-39156)
* 预览自适应表单作为HTML表单时，由于某些子表单与父表单重叠，因此无法正确呈现自适应表单。 (NPR-39046)
* 如果面板具有隐藏的表，并且自适应表单使用表格视图呈现，则无法正确显示第一个选项卡上的字段。 (NPR-39025)
* 的 `Body` OOTB（现成）模板缺少标记。 (NPR-39022)
* 记录文档不是以自适应表单的语言生成。 它始终以英语生成。 (NPR-39020)
* 当自适应表单具有多个面板并且某些面板使用现成的 **文件附件** 组件， `Error occurred while draft saving` 出现错误。 (NPR-38978)
* When `=` 在“自适应表单”的复选框、下拉列表或单选按钮字段中使用符号，然后生成“记录文档”， `=` 在生成的记录文档中不显示符号。(NPR-38859)
* 升级6.5.11.0 Service Pack后，通知批处理错误的数量增加了多倍。 (NPR-39636)
* 如果不提供测试数据，则通信管理信件无法在代理UI中加载。 (CQ-4348702)
* 当用户从使用IBM® WebSphere®部署的AEM Forms中应用AEM Forms Service Pack 14(SP14)时，启动会在初始化数据库和 `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` 出现错误。(NPR-39414)
* 在OSGi服务器上的AEM表单上，使用文档服务API验证PDF时，表单失败，并出现错误：com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException:AEM-DSS-311-003。 (NPR-38855)
* 当用户尝试使用包装器服务在AEM 6.3 Forms中渲染字母时， `java.lang.reflect.UndeclaredThrowableException` 出现错误。 (CQ-4347259)
* 当XDP呈现为HTML5表单时，无论对象在自适应表单中的位置如何，都会先呈现主控页面的内容。 (CQ-4345218)
* 目标服务器上的应用程序配置更改为源服务器上定义的设置，即使 **导入完成时覆盖配置** 导入应用程序时未选中选项。 (NPR-39044)
* 当用户尝试使用配置管理器更新连接器配置时，该配置会失败。(CQ-4347077)
* 当用户在更改管理员用户的默认密码后尝试在JEE修补程序上运行AEM表单时，会出现异常 `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` 发生。 (CQ-4348277)
* 在AEM Designer中，不带字幕的表单字段放置在包括复选框在内的表单元格中。(LC-3920410)
* 当用户尝试在AEM Forms Designer中打开帮助时，该帮助未正确显示。 (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* Experience Manager Sites启动项控制台显示为空白。 (NPR-39188)
* 当在页面移动期间还需要激活具有引用的页面时，引用未进行调整。 (NPR-39061)
* 使用父容器取消隐藏布局容器时，布局更改不会应用到嵌套容器内的所有组件。 (NPR-39041)
* 内容现在不再与宽度为320像素的其他内容重叠。 (SITES-8885)
* 在关闭对话框后添加了焦点。 (SITES-8885)

### 辅助功能 {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* 的 **[!UICONTROL 注释]** 按钮缺少其辅助功能名称。 (SITES-2892)
* ACTIVE用户界面组件的状态(**[!UICONTROL 剪切]**, **[!UICONTROL 复制]**, **[!UICONTROL 粘贴]**, **[!UICONTROL 插入组件]**, **[!UICONTROL 组]**、等)与内相邻背景或外相邻背景之间没有至少三到一的光度对比度。 (SITES-8889、SITES-8756、SITES-8885)
* 状态消息未自动宣布。 (SITES-8889、SITES-8756、SITES-8885)
* 文本内容的对比度缺少4.5:1。 (SITES-8756、SITES-8885)
* 链接或按钮文本在悬停或聚焦时的对比度缺少4.5:1。 (SITES-8756、SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL引发异常。 例如，无法从内容片段获取变体标记。 没有名称为“electric”的变体。 此问题是由于调用 `getVariationTags` 对于引发异常的非现有变体。 (SITES-8898)
* 在列表视图中对标题排序（升序和降序），标题与A、C、B顺序的顺序(SITES-7585)
* 为内容片段变量添加了标记支持。 (SITES-8168)
* 从Experience Manager6.5中识别并删除了Odin特定代码，这是不必要的。 (SITES-3574)
* 从内容片段编辑器用户界面发布语言副本片段时，关联的引用将在英文文件夹下发布。 (NPR-39182)
* 日期字段正在预填充日期。 (NPR-39124)
* 当您第二次选择单选按钮选项时，标记会消失。 (NPR-39071)

### 流体XP {#sites-fluidxp-6515}

* 为客户端库启用ES6编译支持 `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* 内容片段模型中的多字段无法清空和保存，因为即使在 **[!UICONTROL 必需]** 未选择。 (NPR-39063)
* 在 **[!UICONTROL 复制]** 或 **[!UICONTROL Live Copy]** 任务， `cq:targetMetadata` 信息被错误复制。 此功能导致Experience Manager中的两个或多个体验片段指向在target中导出的同一选件。 (NPR-38970)
* 执行“恢复树”操作后，将显示消息 `Un-publication pending. #0 in the queue` 在用户界面中显示的页面最初从未发布过。 (NPR-38847)

### 页面编辑器 {#sites-pageeditor-6515}

* 撤消未删除对添加到组件中的文本所做的上次更改。 相反，当页面刷新时，整个组件会被删除。 (SITES-8597)
* 升级 `jquery-ui` 更新到最新版本后，页面编辑器无法正常工作。 (NPR-38596)
* 内容现在不再与宽度为320像素的其他内容重叠。 (SITES-8756)
* 在关闭对话框后添加了焦点(SITES-8756)

## Sling {#sling-6515}

* `Repoinit` 不支持创建或管理主体名称中包含空格的组，因为组名称被视为字符串，并且不支持引用该组。 (SLING-10952)
* 日志中意外填充了错误消息和例外。 (NPR-39024)

## 翻译项目 {#translation-6515}

* 已通过“项目”面板将目标页面添加到更新语言副本的翻译作业中；源页面未更新。 (NPR-39278)
* 翻译过程失败，无法为翻译项目中的所有页面生成预览。 (NPR-39059)
* 如果语言区域设置不存在，则在为事件配置引用规则时，仍会在区域设置文件夹中创建该区域设置。 (NPR-39054)

## 用户界面 {#ui-6515}

* 文件内发生JavaScript错误 `multifield.js` 适用于内容片段模型编辑器和内容片段编辑器中内容片段模型中的某些字段。 (NPR-39350)

## 工作流 {#workflow-6515}

* 在Experience Manager6.5.11上成功运行的工作流在Experience Manager的6.5.13上运行不一致。 (NPR-39023)

## 安装 [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0要求 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以了解详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 6.5.15.0，在其中一个使用包管理器的创作实例上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.15.0包。 因此，在安装该包之前，您应该先创建 `crx-repository` 以防你需要把它卷回去。 <!-- UPDATE FOR EACH NEW RELEASE -->

### 在上安装Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。

1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能会间歇性地在任何浏览器上发生。

**自动安装**

可以使用两种不同的方法自动安装 [!DNL Experience Manager] 6.5.15.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹。 包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.15.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.15.0)` 在 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.13或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装 [!DNL Experience Manager] Forms附加组件包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您没有使用 [!DNL Experience Manager] Forms。

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. 确保您已安装 [!DNL Experience Manager] 服务包。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)中列出的相应 Forms 附加组件包。
1. 按照 [安装AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 安装 [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。的修复 [!DNL Experience Manager] JEE上的Forms通过单独的安装程序交付。

使用除JBoss EAP 7.4.0以外的任何应用程序服务器，对JEE环境上的所有AEM Forms执行以下步骤。

1. 安装累积安装程序 [!DNL Experience Manager] Forms（在JEE上）和部署后配置中，请参阅 [发行说明](jee-patch-installer-65.md).

1. 安装 [JEE Service Pack 15上AEM 6.5 Forms的片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) servlet片段，并等待应用程序服务器稳定。
1. 安装 [AEM 6.5.15.0 service pack](#install-service-pack).

   >[!NOTE]
   >
   >如果安装最新 [AEM service pack(6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)，在 `Fragment for AEM 6.5 Forms on JEE Service Pack 15` 在JEE环境中， CRX/bundle和开始页显示服务不可用错误， [单击此处](/help/forms/using/aem-service-pack-installation-solution.md) 以了解疑难解答步骤。

1. 安装 [最新Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)，从中删除Forms附加组件包 `crx-repository\install` 文件夹，然后重新启动服务器。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.15.0在 [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
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
| 集成 | 的 **[!UICONTROL AEM云服务选择加入]** 屏幕已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成在 [!DNL Experience Manager] 6.5.此集成支持Adobe Target Standard API。 API使用Adobe IMS和 [!DNL Adobe I/O Runtime]. 它支持AdobeLaunch在工具方面日益发挥的作用 [!DNL Experience Manager] 页面，则选择加入向导在功能上与此无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O Runtime] 集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR连接器已在 [!DNL Experience Manager] 6.5。 | 不适用 |

## 已知问题 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM包含GraphQL索引包1.0.5的内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
使用GraphQL的客户需要此包；这样，用户便可以根据实际使用的功能添加所需的索引定义。

* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 10或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装 [!DNL Experience Manager] 6.5.x.x:
   * “配置Adobe Target集成时， [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target时，会导致创建错误的选件类型。 Target会创建多个类型为“HTML”/源“Adobe Experience Manager Classic”的选件，而不是“体验片段”/源“Adobe Target Classic”的选件类型。
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

以下文本文档列出了 [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.15.0中包含的OSGi包列表](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.15.0中包含的内容包列表](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

