---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作说明以及的详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: d0dc5dfb-25a3-4388-a1d4-abba70081cc3
source-git-commit: 61f3079a88e39c02b29bfafc7b2b9d4d098cef6b
workflow-type: tm+mt
source-wordcount: '4640'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.18.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2023年8月24日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包括的内容 [!DNL Experience Manager] 6.5.18.0 {#what-is-included-in-aem-6518}

[!DNL Experience Manager] 6.5.18.0包括自2019年4月首次推出6.5以来发布的新功能、关键客户请求的增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) 日期 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的某些主要功能和增强功能包括：

**关键功能**

* Dynamic Media的Assets - [Dynamic Media中支持视频的多字幕和多音频轨道](/help/assets/video.md#about-msma) — 您现在可以轻松地将多个字幕和多个音轨添加到主视频中。 此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

* 资源 — 现在，您可以在搜索结果中导航到包含资源的文件夹位置，以便执行各种资源管理任务。 (ASSETS-23182)

**关键增强功能**

* 内容片段中的Sites Polaris选取器改进了性能。 (SITES-14092)

* 允许站点页面编辑器/图像组件用户从远程AssetsCloud Service引用资源。 (SITES-13448和SITES-13433)

* 要在“列表”视图中快速查找项目（系统中可能有许多项目），Adobe现在支持服务器端排序。 项目节点在用户界面中呈现之前，会根据用户选择的列在后端进行排序。 (NPR-41027)

* AEM 6.5.18.0支持MongoDB 5.0到6.0。

**已弃用功能**

* 已弃用AEM中的ActiveMQ。 ActiveMQ用于两个AEM Publish实例之间的通信。 Adobe建议客户现在使用负载平衡器。

**Forms**

* **[在规则编辑器中使用自定义错误处理程序增强了错误处理](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)**  — 现在，您可以调用自定义函数（使用客户端库）来响应外部服务返回的错误。 而且，您可以为最终用户提供量身定制的响应。 或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后端中调用自定义工作流以获取特定错误代码，或通知客户服务已中断

* **[增强的Adobe Sign工作流步骤](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - AEM Workflows中的Adobe Sign工作流步骤包含以下增强功能。

   * **通过基于Government ID的身份验证增强Adobe Sign的安全性** - Adobe Acrobat Sign基于Government ID的身份验证提供额外的验证层。 它允许用户使用政府颁发的ID（驾照、身份证、护照）进行身份认证。 通过使用可信的标识文档，此增强功能为签名过程增添了更高的可信度，使其非常适合需要增强的安全性、合规性和用户验证的情况。

   * **Adobe Sign文档审核追踪的透明度增强**  — 使用审核记录功能可详细了解Adobe Sign文档的生命周期。 利用审核记录功能，您现在可保留与文档相关的所有操作和交互的全面记录。其中包括查看者、编辑者或签署文档者以及每个事件的时间戳等详细信息。此增强对于保持合规性、解决争议和确保数字协议的完整性至关重要。


   * **扩展了协议收件人的角色，而不只是签名者** - Adobe Acrobat Sign允许您扩展协议接受者的角色，而不只是签名者，以便更好地匹配他们的工作流要求。 启用后，协议中的每个收件人可以单独配置其角色，签名者是默认角色。


* **[AEM Forms on JEE完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** - Service Pack提供了AEM Forms on JEE的完整安装程序，以支持多种新软件组合，包括：
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * 在Windows Server 2022上OracleWebLogic 14C
   * Red Hat® JBoss® 7.4.10
   * MongoDB 4.4
   * MySQL JDBC连接器8

如果您在JEE环境中安装或计划使用适用于AEM 6.5 Forms的最新软件，Adobe建议使用AEM 6.5.18.0 Forms on JEE完整安装程序。 要探索新添加和已弃用的软件的完整列表，请参阅JEE上的AEM Forms或OSGi上的AEM Forms的文档。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 18中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-6518}

* 已使用批量编辑器通过下载 `tsv` 导出，进行了脱机更改，然后上传了 `tsv` 返回Experience Manager。 即使页面已更新，JCR属性 `cq:lastModified` 未更新，且位于时间线中。 (SITES-14072)
* 创建体验片段的实时副本或转出时，体验片段内的链接引用未更新。 (SITES-14759)
* 向现成的Experience Manager标准转出配置“转出页面和子页面”添加了来自父页面的工作流同步操作，并且异步作业失败并出现NullPointer异常。 源位置页面(en-us)不在父级中，但存在于目标位置(Live copy) (en)中。 (SITES-12207)
* 您有“en”页面，其中包含 `jcr:description` 并发送页面以供翻译。 此 `jcr:description` 将进行翻译，并且属性位于launch下。 但是，提升启动项时， `jcr:description` 在页面中不会更新。 (SITES-13146)
* Blueprint转出后，Live Copy上的本地化内容丢失。 (SITES-12602)

#### 管理员用户界面{#sites-adminui-6518}

* 如果用户的删除权限通过useradmin控制台删除，则用户不会再看到sites.html控制台中的“属性”按钮（在选择页面时）。 但是，如果用户打开页面编辑器，则会显示此选项。 (SITES-14341)
* 当文件夹具有多个页面，每个页面都具有多个版本时，使用比较版本功能时，实例上的负载会变得很高。 如果多个用户同时使用该功能，则实例可能会关闭。 (SITES-13026)

#### [!DNL Content Fragments]{#sites-contentfragments-6518}

* 发现以下异常处理问题： `RemoteAssetClientImpl`. 当查询元数据时发生IOException或RuntimeException时，当前线程尝试关闭并重新创建共享httpClient，这可能导致线程中出现一连串的其他错误。 (SITES-14092)
* 当作者在内容片段中填写富文本编辑器字段并在链接中插入图像时，通过GraphQL API查询内容片段时，出现错误消息 `Exception while fetching data (/genericContentByPath) : null` 会返回。 仅当链接中包含图像时才会发生此错误。 从链接中删除图像后，错误消息消失。 (SITES-13988)
* GraphQL对Experience Manager6.5的实施与主版本不一致，并且缺少几个重要修复。 (SITES-13096)
* 访问元数据服务端点时需要强制的HTTP标头。 (SITES-13068)

#### 核心组件{#sites-core-components-6518}

* 资产选择器在关闭并重新打开时不会获取更新的资产列表。 如果新资产上传到存储库，则在刷新包含资产选择器的页面之前，它们不会显示在资产选择器中。 (SITES-14828)
* 在窗口减少时，集成在站点编辑器(CS)中的资产选择器用户界面无响应。 (SITES-14127)
* 资产选择器集成的Adobe IMS (Identity Management System)配置接受不正确的值。 (SITES-13962)
* 资产选择器集成在站点图像组件中时，不应允许选择非图像资产。 (SITES-13879)
* 成功登录后，用户将被重定向到页面编辑器。 用户必须重新打开资产选择器，才能选择远程资产。 (SITES-13851)
* 远程资产选取器始终重定向到Adobe IMS (Identity Management System) Stage环境。 (SITES-13448和SITES-13433)

<!-- #### [!DNL Experience Fragments]{#sites-experiencefragments-6518}

* A -->

#### 页面编辑器{#sites-pageeditor-6518}

* 当作者打开页面属性时，对话框的视图不正确。 即，可以看到额外的水平滚动条和额外的边距。 (SITES-14502)
* 在Experience Manager6.5 Service Pack 17中为锚点和正文标记添加的样式导致CSS问题。 在“创作”中，锚点标记未显示下划线。 (SITES-14261)

### [!DNL Assets]{#assets-6518}

* 屏幕阅读器不会通告 [!UICONTROL 开始裁切] 选项。 (NPR-40593)
* 在AEM 6.5.17.0实例上上传资源时，Experience Manager显示错误和警告消息。 (ASSETS-26232)
* 当您将某个资源从具有只读访问权限的文件夹与某个资源的完全访问权限关联时，Experience Manager会显示一条错误消息，但仍会创建两个资源之间的部分关系。 (ASSETS-25832)
* 连接的资源在AMS实例和Cloud Service实例之间不起作用。 (ASSETS-24930)
* 编辑元数据架构Forms时， [!UICONTROL 准时] 和 [!UICONTROL 关闭时间] 字段未正确保存。 (ASSETS-24871)
* 在为经过训练的标记生成智能标记报表时，不会列出置信度得分较低的标记。 (ASSETS-24109)
* 在“列”视图中编辑和注释图像时，Experience Manager显示一个空白屏幕。 (ASSETS-24108)
* 创建收藏集时，屏幕阅读器不会朗读添加用户字段的用途。 (ASSETS-21736)
* 此 **收藏集** 标签未在收藏集属性页面上本地化。 (ASSETS-21102)
* 使用默认元数据架构表单添加规则或编辑现有规则时，下拉列表中的语言未本地化。 (ASSETS-21026)
* 在元数据架构中添加JSON路径时，Experience Manager显示未本地化的错误消息。 (ASSETS-21025)
* 左侧导航中的时间轴选项不显示相应的对比度。 (ASSETS-17348)
* 日历元素不使用所需的ARIA属性。 (ASSETS-17282)
* 左侧导航文本不显示相应的对比度。 (ASSETS-17268)
* 屏幕阅读器用户不会隐藏Lightbox图像。 (ASSETS-17263和ASSETS-17242)
* 活动用户界面的状态未提供有关背景的合适对比度。 (ASSETS-17260)
* 为资产添加注释时，屏幕阅读器无法识别 [!UICONTROL 另存为版本] 或 [!UICONTROL 启动工作流] 使用键盘箭头键导航这些按钮时，显示这些按钮。 (ASSETS-17253)
* 某些ARIA角色在Assets主页上不包含相应的子角色。 (ASSETS-17248)
* 使用键盘导航到图像类型资产的编辑选项时， [!UICONTROL 启动地图] 选项无法识别，键盘焦点将转往“Cancel（取消）”按钮。 (ASSETS-17238)

#### [!DNL Dynamic Media]{#assets-dm-6518}

* 当VTT下载失败时，视频不可见。 它显示一个空白屏幕，同时显示视频洗刷正在前进。 (ASSETS-21909)
* 使用键盘上的Tab导航时，焦点未移动到视频下方的多个控件。 因此，他们无法访问。 改进了交互式视频的键盘导航。 (ASSETS-25749)
* 修复了在Dynamic Media组件中显示禁用的查看器预设。 (ASSETS-22922)
* 从“常规设置”安全性选项卡中删除了“图像服务”。 (ASSETS-24618)
* 修复了无法上传到Dynamic Media和StringIndexOutOfBoundsException的资源。 (ASSETS-25787)
* 在“基本”选项卡中为必填的“宽度”编辑字段添加了可视星号。 (ASSETS-25741)
* 修复了水印Dynamic Media演绎版下载问题。 (ASSETS-26173)
* 恢复非视频资产名称不超过127个字符的限制。 (ASSETS-26074)

### [!DNL Forms]{#forms-6518}

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.18.0 Forms add-on packages release is scheduled for Thursday, August 31, 2023. A list of Forms fixes and enhancements would be added to this section post the release. -->

* **文档服务**
   * 当用户使用transformPDF服务时，它会失败，并出现异常： `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml` (FORMS-9957)
   * 如果在生成PDF文档期间服务器关闭，则会引发服务器启动后作业处理错误。 必须在服务器启动期间添加参数 — Dcom.adobe.livecycle.dsc.deferServiceStart=true。 (FORMS-9836)
   * 如果用户尝试使用AssemblerService.Invoke方法合并PDF，则汇编程序无法执行该任务。 (FORMS-9550)
   * 当您在OSGI和JEE环境中升级到AEM 6.5.15.0 Service Pack时，使用特定模板的Assembler服务将停止工作。 (FORMS-9355、FORMS-9445、FORMS-9408)
   * Java™垃圾收藏集无法清除AEM Forms OSGi服务器上的旧根栈，因为XMLFormService的全局超时未配置为适当的值。 (FORMS-9384、FORMS-9035)
   * 呈现自适应表单的PDF预览时，错误日志中会显示不需要的Java™栈栈转储。 (FORMS-8865)
   * 当用户查看文档详情部分中文档的文档状态时，无法正确显示。 (FORMS-8946、FORMS-10424)
   * 当用户升级到AEM Forms并使用sendToPrinter服务时，栈利用率会持续增加。 (FORMS-10148)
   * 在JBoss® 7.4 EAP服务器上，电子邮件功能失败 `java.io.IOException`. (FORMS-10138)
   * 当用户使用transformPDF服务时，它会失败并出现错误： `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml`(FORMS-9957)
   * 升级到AEM Service Pack 6.5.14.0后，在使用特定模板时，组装程序服务中会出现问题。 (FORMS-9445、FORMS-9408)
  <!-- *  When a user configures the watched folder endpoint for PDF Generator, it fails to pick documents on JDK 11. (FORMS-10152) -->
* **自适应表单**
   * 当用户尝试在不修改字段（例如设置另一个字段的值）的情况下调用自定义函数时，调用会失败。 (FORMS-9921)
   * 在自适应表单中使用规则编辑器的自定义错误函数时，出现以下错误：
      * 当用户尝试使用@param时{boolean} 对于函数，规则编辑器不允许将布尔值传递到函数。
      * 当用户尝试使用@param时{string} 对于函数，规则编辑器无法传递可选值，并收到不完整规则的警告。 (FORMS-9816、FORMS-9815)
   * 表单 — 用户组在自适应表单中两次调用规则编辑器失败。 (FORMS-9051)
   * 在可视编辑器中，当用户选择表单对象时，整个字段实例对象将传递到自定义函数，而不仅仅是字段的值。 (FORMS-10015)
   * 当用户创建基于核心组件的自适应表单并添加文本输入组件时， `Is Empty` 和 `Is Not Empty` 无法在规则编辑器中工作。 (FORMS-10098)
   * 如果某个字段在基于自适应表单的核心组件中标记为无效，则会启动该字段的更改事件。 (FORMS-10087)
   * 当用户尝试使用复杂的JSON架构创建自适应表单时，失败。 错误发生于：
     `GET /content/forms/af/katezeroone/testaf1.html HTTP/1.1] com.adobe.aemds.guide.service.impl.JsonObjectCreatorImpl Could not emit JSON with context java.lang.ArrayIndexOutOfBoundsException:0`. (FORMS-9639)
   * 在自适应表单中，当用户禁用“我同意条款和条件”复选框时，它会在用户向下滚动时再次启用。 (FORMS-9458)
   * 当用户使用Google Chrome/Firefox在Android™设备上打开自适应表单，并在文本框中输入允许的最大字符数时，文本框中的值无法清除。 (FORMS-9354)
   * 如果复选框的标签包含“，”、“/”或“。”等特殊字符，则单击文本/标签不会选中相应的复选框。 (FORMS-9313)
   * 当用户尝试验证条款和条件组件时，它无法验证该组件是否不在焦点上，而另一个组件是否处于验证状态。 (FORMS-8725、FORMS-8913)
   * 如果在升级到AEM 6.5.16.0 Service Pack后重新加载自适应表单，则检索文件附件失败。 (FORMS-8906)
   * 在基于XDP的自适应表单中，如果复选框组件包含分配了数字值的文本标题，则文本标题会被截断且与分配的值不匹配。 (FORMS-8743)
   * 如果用户尝试对作者环境中嵌入在自适应表单中的片段实施延迟加载，则为片段定义的规则/逻辑不会反映在表单中。 (FORMS-8554、FORMS-9182)
   * 当您尝试在AEM 6.5.16.0 Service Pack中打开任何Coral对话框时，它会生成 `error.log: cannot render resource` 例外。 (FORMS-8942)
   * 当用户尝试翻译自适应表单中带有单个选项的复选框时，会失败。 (FORMS-10181)
   * 所有记录文档(DoR)模板均无法发布。 仅发布基于区域设置的英文DoR模板及其关联的基于Forms的DoR模板。 (FORMS-10535)

* **辅助功能**
   * 在自适应表单中使用涂写签名组件时，出现以下错误：
      * 在涂鸦签名组件之后，如果有更多组件，按Tab键不会遍历签名对话框；而是会移至下一个组件。 只有在遍历所有组件后，它才最终移至签名对话框。
      * 当用户使用画笔或键盘登录签名对话框时，按Enter键不会关闭对话框。
      * 无法使用键盘访问清除签名确认对话框。
      * 屏幕阅读器无法读取在对话框中输入的信息。
      * 如果不使用鼠标，则无法清除签名。 (FORMS-9317)
   * 当用户提交自适应表单时，屏幕阅读器无法读取必填字段的错误消息。 (FORMS-9316)
   * 当屏幕阅读器读取HTML表单时，使用字距微调（间距）读取文本时出现问题。 (FORMS-9258)
   * 在自适应表单中，使用屏幕阅读器不会调出链接到文本的引用/脚注。 (FORMS-8920)
   * 在最新的设计器中，无法正确识别辅助功能标记。 (FORMS-10139)
* **交互式通信**
   * 在通信管理中，本地化不起作用。 (FORMS-8926)
   * 使用publishAll服务时，无法打开草稿书信。 (FORMS-8589)
   * Experience Manager后，在服务器上安装了Service Pack 16，如果尝试编辑这些信件，所有交互式通信信件都会开始计时。 如果它们提供任意示例有效负载来预览或查看/编辑属性页面，则它们有效。 但是，他们无法编辑字母。 (FORMS-9067)


<!-- ### [!DNL Commerce]{#commerce-6518}

* A -->

### Foundation{#foundation-6518}

#### 内容分发{#foundation-content-distribution-6518}

* 不应阻止资产删除队列，并且日志文件中不应出现任何错误。 (NPR-40570)

<!-- #### Integrations{#integrations-6518}

* A -->

<!-- #### Oak{#oak-6518}

* A -->

#### Platform{#foundation-platform-6518}

* 安装vanillaExperience ManagerService Pack 17后，您会看到 `stderr.log`. Vanilla安装不会收到错误。 (CQ-4353637)
* “标记”(Tagging)屏幕中的“创建”(Create)按钮不遵循ACL（访问控制列表）。 (NPR-40973)
* 无法在Experience Manager上创建ContextHub的缓存节点，也无法访问（或同时访问）该节点。 (NPR-40515)

#### 复制{#foundation-replication-6518}

* 复制刷新将删除请求路径的所有后代。 (NPR-40569)

#### Sling{#foundation-sling-6518}

* 在生成链接共享报表时，列链接未包含正确的值。 (NPR-40798)
* 使用AEM 6.5.15.0时，AEM重新启动后所有虚名URL、sling别名和sling映射都会断开。 (NPR-40420)

#### 翻译项目{#foundation-translation-6518}

* 翻译 `rules.xml` 从翻译配置用户界面添加规则时，排序会很差。 (NPR-40431)
* 在翻译期间支持带有查询参数的链接。 (NPR-40339)
* 更新其他上下文根目录后，未为客户加载词典用户界面。 (NPR-40650)
* 当其中一个资产是内容片段，其中包含具有ReferenceFragment或ContentFragment类型的多字段时，创建语言副本时出错。 (NPR-40892)

#### 用户界面{#foundation-ui-6518}

* 如 [配置浏览器文档](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#using-configuration-browser)， _名称将成为存储库中的节点名称_. 但是，在Configuration Browser中， Configuration Title用于CRXDE Lite中的路径，而Name of the Configuration被忽略。 (NPR-40607)

<!-- #### WCM{#wcm-6518}

* A -->

#### 工作流{#foundation-workflow-6518}

* 还原资源版本会将资源状态保留在处理模式下。 (NPR-41029)
* 资源和项目用户界面上的排序问题。 有些客户根据业务要求覆盖了“资产和项目”用户界面上的自定义列。 他们使用现成的属性实施了一种分类 `sortable=true`. 但是，当项目或资产用户界面下存在许多条目时，他们会在排序中看到不一致。 (NPR-41027)
* 日志中填充了 `NullPointerException` 在 `EMailNotificationService`工作流应发送的、和电子邮件不会发送。 (NPR-40898)
<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST  * The timeline is not providing references to the selected content. (NPR-40806) -->

## 安装 [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.18.0需要 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以获取详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上获取Service Pack下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 使用包管理器对某个Author实例执行6.5.18.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.18.0程序包。 因此，在安装该包之前，您应该创建 `crx-repository` 万一你一定要把它退回。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装服务包 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。

1. 从以下位置下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack期间，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能间歇性地在任何浏览器上出现。

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL Experience Manager] 6.5.18.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.18.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.18.0)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.16或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装服务包的说明，请参阅 [Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装 [GraphQL索引包1.1.1的Experience Manager内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

UberJar用于 [!DNL Experience Manager] 6.5.18.0可从以下网站获取： [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.18</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件可在Maven中央存储库而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，替换为 `apis` 作为值，用于 `dependency` 标记之前。

## 已弃用和已删除的功能{#removed-deprecated-features}

请参阅 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md/).

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* **升级到Service Pack 18 (6.5.18.0)后，页面发布在页面编辑器中不起作用**

  <!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0--> 将AEM 6.5.0.0 - 6.5.17.0的实例升级到AEM 6.5.18.0后，单击 **发布页面** 在页面编辑器中，您被重定向到一个不存在的URL。

  要解决此问题，请执行以下操作之一：

   * 删除以下“path”属性。

     `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

   * 将正确的URL直接粘贴到浏览器中。

     `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html`



* **与Oak相关**
在Service Pack 13及更高版本中，已开始出现以下错误日志，这会影响持久性缓存：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或者

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  要解决此异常，请执行以下操作：

   1. 从删除以下两个文件夹 `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 安装Service Pack，或重新启动Experience Manageras a Cloud Service。
的新文件夹 `cache` 和 `diff-cache` 自动创建，并且您不再遇到与相关的异常 `mvstore` 在 `error.log`.

* 更新可能已为内容模型使用自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询可能使用 `damAssetLucene` 索引而非 `fragments` 索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  要更正此问题， `damAssetLucene` 必须配置为包含以下两个属性：

   * `contentFragment`
   * `model`

  更改索引定义后，需要重新索引(`reindex` = `true`)。

  执行这些步骤后，GraphQL查询的执行速度应该会更快。

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题，因为后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您升级您的 [!DNL Experience Manager] 从6.5.0 - 6.5.4到Java™ 11上最新Service Pack的实例，请参见 `RRD4JReporter` 中的例外 `error.log` 文件。 要停止例外，请重新启动您的实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在以下位置重命名层级中的文件夹： [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题不会在中更新 [!DNL Brand Portal] 直到重新发布根文件夹。

* 安装期间可能会显示以下错误和警告消息 [!DNL Experience Manager] 6.5.x.x：
   * “当在中配置Adobe Target集成时 [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型为“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance中未找到维护窗口。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance中未找到维护窗口。
   * 通过可购物横幅查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，Rhino JavaScript引擎由 ```org.apache.servicemix.bundles.rhino``` 捆绑有新的提升行为。 使用严格模式(```use strict;```)必须正确声明其变量，否则它们不会运行，而是会引发运行时错误。

### AEM Forms的已知问题

#### 支持的平台

* WebLogic JEE服务器不支持高于1.8.0_281的JDK版本。 (FORMS-8498、CQDOC-20383)
* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支持的全包安装 [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20不支持在JEE安装程序上安装AEM Forms。 在JEE安装程序上安装AEM Forms仅支持JDK 11.0.19或更早版本。 (FORMS-10659)

#### 安装

* 在JBoss® 7.1.4平台上，当用户安装Experience Manager6.5.16.0或更高版本的Service Pack时， `adobe-livecycle-jboss.ear` 部署失败。 (CQ-4351522和CQDOC-20159)
* 在Windows Server 2022上升级到AEM Forms 6.5.18.0 JBoss Turnkey完整安装程序环境后，使用Java 11编译输出客户端应用程序代码时，可能会出现以下编译错误：

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  要解决此问题，请执行以下步骤：
   1. 导航到 `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` 和unzip `adobe-output-client.jar` 以提取 `Manifest.mf` 文件。
   1. 更新 `Manifest.mf` 通过删除条目生成文件 `${clover.jar.name}` 从class-path属性中。

      >[!NOTE]
      >
      > 您还可以使用就地编辑工具（例如7-zip）来更新 `Manifest.mf` 文件。

   1. 保存更新的 `Manifest.mf` 在 `adobe-output-client.jar` 存档。
   1. 保存修改的内容 `adobe-output-client.jar` 文件并重新运行安装程序。  (CQDOC-20878)
* 安装AEM Service Pack 6.5.18.0完整安装程序后，EAR部署在使用JBoss® Turnkey的JEE上失败。
要解决此问题，请找到 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` 文件和更新 `Adobe_Adobe_JAVA_HOME` 到 `Adobe_JAVA_HOME` 所有出现的次数。 (CQDOC-20803)

#### 自适应表单

* 发布自适应表单时，其所有依赖项（包括策略）都会重新发布，即使尚未对它们进行任何修改也是如此。 (FORMS-10454)
* 当用户选择在自适应表单中首次配置字段时，属性浏览器中不显示保存配置的选项。 选择在同一编辑器中配置自适应表单的某些其他字段可解决此问题。
* 在自适应表单的指南容器中设置重定向URL后，内联签名将停止工作。 (FORMS-10493)
* 所有记录文档(DoR)模板均无法发布。 仅发布基于区域设置的英文DoR模板及其关联的基于Forms的DoR模板。 (FORMS-10535)

#### 交互式通信

* 升级到AEM Service Pack 18后，无法在编辑模式下打开包含大型内联图像的交互式通信。 (FORMS-10578)要解决此问题，请执行以下步骤：

   1. 下载 [修补程序 — FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 从SD链接。
   1. 解压缩修补程序存档文件，以便获取Experience Manager包(.zip)和捆绑包(.jar)文件。
   1. 通过包管理器上传并安装包(.zip)。
   1. 打开配置管理器包 `https://server:host/system/console/bundles`，上传并安装捆绑包(.jar)。

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了中包含的OSGi包和内容包 [!DNL Experience Manager] 6.5.18.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.18.0中包含的OSGi包列表](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.18.0中包含的内容包列表](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)
