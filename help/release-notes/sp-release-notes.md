---
title: '[!DNLAdobe Experience Manager] 6.5 Service Pack发行说明。'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 6.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: b6db346f7ec2570972329a8edb089fe909120b75
workflow-type: tm+mt
source-wordcount: '4402'
ht-degree: 6%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.6.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2020年9月3日 |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6.zip) |

## 包含在Adobe Experience Manager6.5.6.0中的内容 {#what-s-included-in-aem}

Adobe Experience Manager6.5.6.0是一项重要更新，包括自2019年4月发布6.5版本以来发布的新功能、关键客户请求的增强功能以及性能、稳定性和安全 **性改进**。 它可安装在Adobe Experience Manager6.5之上。

Adobe Experience Manager6.5.6.0中引入的主要功能和增强功能包括：

* 现在，还支持通过代理服务器将资产贡献文件夹从Brand Portal发布到Experience Manager资产。

* 现在，删除中的专用文件夹时，将清除自动生成的专用文件夹组 [!DNL Experience Manager Assets]。

* 视频查看器预设编辑器 [!UICONTROL 中的] 修饰符说明已在中更新 [!DNL Dynamic Media]。

* 提供新的公司设置以反映连接器的 [!DNL Dynamic Media] 状态。

* 和的默认 `test` 选项 `aiprocess` 会从Dynamic Media `Thumbnail`中更新为以 `Rasterize` 前的默认选项，以确保用户只需创建缩略图并跳过页面提取和关键字提取。

* 在客户端预填自适应表单。

* 通过双向SSL实现，在服务器上与RESTful API形成数据模型集成。

* 增强了已翻译的自适应表单页面的缓存。

* 支持自动化Forms转换服务中的Adobe Sign文本标记。

* 支持使用将彩色表单转换为自适应表单 [!DNL Automated Forms Conversion service]。

* 支持SMB 2和SMB 3协议。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.4。

有关Experience Manager6.5.6.0中引入的功能和增强功能的完整列表，请参 [阅Adobe Experience Manager6.5 Service Pack 6中的新增功能](new-features-latest-service-pack.md)。

以下是6.5.6.0版中提 [!DNL Experience Manager] 供的修复列表。

### [!DNL Sites] {#sites-6560}

* 在或 [!DNL Sites] 中， [!DNL Screens]选择一个项目，然后单击“管 [!UICONTROL 理出版物”]。 由于用户界面错误， [!UICONTROL 用户无法进入] “管理发布”向导。 具体而 [!UICONTROL 言] ,“发布”选项不起作用(NPR-34099)。
* 取消选择“取消继承”或“禁用继承”选项后，iParsys（继承的段落系统） [!UICONTROL 的位置][!UICONTROL 将不会恢复为其原始默认位置(] NPR-34097)。
* 如果 `RolloutConfigManagerFactoryImpl` 无法加载转出配置，则不会尝试加载缺少的配置。 它返回缓存的配置(NPR-34092)。
* 在文本核心组件中，使用源HTML编辑选项后，将删 `em` 除标记中的类(NPR-34081)。
* 从Experience Manager6.3.3升级到Experience Manager6.5.3后，转出过程需要更长的时间，转出失败，出现超时错误(NPR-34049)。
* 属 `htmlwriter` 性值不进行编码。 XF标记中存在的标记以解码的属性值(即，而 `"` 不是 `&#34`)导出。 它会在使用XF导出的Visual Experience Composer的目标端引起问题(NPR-34048)。
* 在移入页面 [!DNL Experience Manager Sites]时，增强日志记录以捕获因故而导致的版本创建失败(NPR-34014)。
* 如 [!DNL Rich Text Editor] 果删除了所有文本，则也会删除段落标记(NPR-33976)。
* 打开 `siteadmin` 或刷新页面（在经典UI中）时，菜单中的 `New` 选项将被禁用(NPR-33949)。

   ![用于说明经典UI中缺少菜单的问题的屏幕截图](assets/33949_missing_menu.png)

* A不 [!DNL Content Fragment] 能用作A, `TemplatedResource` 因为它在 `ContentFragmentUsePojo` (NPR-33911)中失败。
* 同步和异步移动操作可能会导致并发传输导致的错误。 页面移动操作仅限于同步移动。 它可防止页面的并发移动(NPR-33875)。
* [!UICONTROL 将内容从] Author复制到Publish实例的“管理发布”操作失败，并生成JavaScript错误(NPR-33872)。
* 当选择多个页面或资产以创建版本时，将仅为上次选择的页面或资产创建新版本(NPR-33866)。
* 将包含Live Copy的Blueprint页面移到另一个文件夹。 将文件夹移到原始文件夹时，移动操作将失败且没有任何错误(NPR-33864)。
* 当使用移动操作在控制台中重命名网页时， [!DNL Sites] 向导的最后一步会显示两个重叠的对话框(NPR-33831)。

   ![用于说明NPR-33831重叠移动对话框问题的屏幕截图](assets/33831_rename_dialog.png)

* 复制 `cq:acLinks` 和粘 `cq:acUUID` 贴操作 [!DNL Adobe Campaign] 期间，将删除复制上的属性和属性(NPR-33794)。
* 当尝试在已分离父Live Copy的子页面上转出时， [!DNL Experience Manager] 将生成空指针异常(NPR-33676)。
* 再 [!DNL RTE] 次复制并粘贴布局容器时，布局容器中的组件不可见。 组 [!DNL RTE] 件不可编辑，但在刷新页面时显示(NPR-33662)。
* 调整不同断点（中、大）的布局组件大小时，布局的行为不如预期(NPR-33608)。
* 在的内联编辑模 [!DNL RTE]式下，拖动图像对文本组件无效(NPR-33602)。
* 可以在Blueprint页面中创建与页面名称同名的组件。 转出过程 `_msm_moved` 中，后缀为重命名组件。 该组件将移至段落系 [!UICONTROL 统的末尾] (NPR-33535)。
* 当在许多页面或资产上设置offTime或onTime时，会占用大量资源，并在启动和关闭期间减慢系统速度(NPR-33482)。
* 具有CRUD权限的用 `/content/experience-fragment` 户无法删除文件夹(NPR-33436)。
* 您可以选 [!UICONTROL 择HTML和JSON] ，作为部分父 [!UICONTROL 级文件夹上的] “Adobe Target”导出格式 [!DNL Experience Fragments] 的选项。 此父文件夹的子文件夹的触屏优化UI中显示的属性相同。 但是，在CRXDE中， `cq:adobeTargetExportFormat`它仅显示HTML而不 `html,json` 显示(NPR-33423)。
* 不支持从页面别名发布或取消发布。 删除似乎另有声明的选项(NPR-33415)。
* 可以将特定标记从一个位置移动到另一个位置 [!DNL Experience Manager]。 移动之前和移动之后，还可以将其应用于不同的页面。 编辑页面属性时，即使标记相同，标签也不会显示为进行编辑(NPR-33353)。
* 从包含多个布局容器的模板中删除布局容器时，页面模板无法正常呈现(NPR-33347)。
* 在模板编辑器中，尝试删除一个模板，该模板已在下方超过100000个页面使用 `/content/`。 显示错误，没有任何错误消息(NPR-33312)。
* 使用锚 [!DNL Experience Manager] 点重定向到页面在创作实例上不起作用，因 `PageRedirectServlets` 为在URL片段或锚点后放置查询字符串(NPR-34288)。
* 在下面创建 `/content/campaign` 品牌会生成不允许创建活动的结构。 [!UICONTROL “创建品牌] ”选项会使新创建的品牌无法 [!UICONTROL 创建优惠和活动] ，因为没有 [!UICONTROL “创建] ”选项(NPR-34113)。
* 您可以暂停页 [!DNL Live Copy] 面，继承会在编辑器模式中断开。 在页面属性中，表示继承的图标错误地指示继承存在且未中断(NPR-34017)。
* 具有许多引用的页面无法异步移动，有时移动操作会失败(CQ-4297969)。
* 创作时，URL中 `/` 包含字符的网页变得不响应。 在创作时添加组件时，CPU使用率会增加，浏览器会停止响应(CQ-4295749)。
* 在浏览模式下，NVDA不解说从“类型／大小”菜单选项中选择的值。 视觉焦点不在所选元素上。 依赖屏幕阅读器的用户无法使用浏览模式(CQ-4294993)。
* 创建网页时，用户可以选择 [!UICONTROL 内容页面] 模板。 在“社 [!UICONTROL 交媒体] ”选项卡中，用户选 [!UICONTROL 择首选XF变体]。 要在NVDA浏览模式下选择体验片段，用户无法使用键盘键(CQ-4292669)。
* 已将handlebars库更新为更安全的v4.7.3(NPR-34484)。

### [!DNL Assets] {#assets-6560}

**Experience Manager资源中的辅助功能增强**

* 使用键盘键，用户现在可以访问资源的引用列表中的交互式 [!UICONTROL 用户界面] 选项(NPR-34115)。

* 屏幕阅读器现在宣布搜索页面上谓词的预期操作(NPR-34104)。

* 现在，搜索页面和搜索结果页面包含更多信息标题，以便更好地了解屏幕阅读器用户(NPR-34093)。

* 屏幕阅读器现在会宣布删除资产属性页面 [!UICONTROL 的] “基本” [!UICONTROL 选项卡中选] 定标记的选项(NPR-33972)。

* 列表视图中每行中的元素现在由屏幕阅读器作为同一行的元素进行宣布(NPR-33932)。

* 使用键导航时的 `Tab` 用户焦点现在移动到版本预览中的关闭选项(NPR-33863)。

* 关闭Omnisearch后，用户焦点现在移动到搜索图标(NPR-33705)。

* 使用键盘键进行导航时，可操作的用户界面选项现在具有更加突出的视觉焦点，并增强了对比度。 键盘用户可以识别聚焦区域(NPR-33542)。

* 使用键盘的拖动功能现在在屏幕 [!UICONTROL 阅读器的浏览模式] (CQ-4296326)下在元数据模式编辑器中工作。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器，

   * 加载对话框后，不立即对表信息进行解说。

   * 可导航到所有列出的自动建议。

   * 为“添加电子邮件地址／搜索” [!UICONTROL (Add Email Address/Search] )解说显示的自动建议(CQ-4294232)。

* 使用键 `Esc` 从卡视图中删除快速操作图标不再从最后一个聚焦项目中删除键盘焦点(CQ-4293554)。

* 对于用户界面上的交互式选项，屏幕阅读器现在会宣布其用途，而不是图标的文字名称(CQ-4272943)。

* 现在，键盘焦点可 [!UICONTROL 以成功移]动到 [!UICONTROL Flyout、InlineZoom、ShopBanner]、Zoom、 [!DNL Dynamic Media] ZoomDark光线、DarkZoom、DarkZoom的（使用CA中的ShopAsset Details标签，垂直导航）q-4290605)。

* [!UICONTROL 现在可以使用] 键盘键访 [!UICONTROL 问资产] “属性”页面上的“保存并关闭”选项(NPR-34107)。

* 现在，由于登录页面上的用户名和密码组合不正确而导致的错误消息在每次出现错误时都由屏幕阅读器宣布(NPR-33722)。

* 在标 [!DNL Experience Manager] 题部分，在浏览模式下导航时，屏幕阅读器现在会宣布，

   * 在类型中自动编辑 [!UICONTROL 建议，以便在Omnisearch] 中进行搜索。

   * 解决方案、帮助、收件箱 [!UICONTROL 和用户]选项 [!UICONTROL 的状]态已展 [!UICONTROL 开或] 折叠。

   * 搜索 [!UICONTROL 帮助] ，当用户在帮助选项下的“搜索帮助”字段中输入 [!UICONTROL 搜索字符串时] ，将显 [!UICONTROL 示该消息] 。

   ![标题中的帮助菜单](assets/Help_aem_header.png)

   *图：[!UICONTROL 在“帮助”菜单]中[!UICONTROL 搜索]“帮助”。*

   * 如果在“User”选项下的“Impersonate as [!UICONTROL ”字段中输入了不] 正确的值 [!UICONTROL ，并且焦点会正确移] 动到文本字段(NPR-33804)，则显示错误消息。

   ![标题中的用户菜单](assets/User_aem_header.png)

   *图：[!UICONTROL 在标题的]“用户[!UICONTROL ”菜单]中模拟为字段。*

* 用户现在可以使用键盘更改焦点：

   * [!UICONTROL 搜索／添加链接共享] 对话框中 [!UICONTROL 的电子邮件地址] 。

   * [!UICONTROL 在文件夹属性] 的“权 [!UICONTROL 限”选项卡的“关闭的用] 户组” [!UICONTROL 下添加“用户或用户组”] 字段 [!UICONTROL (NPR] -34452)。

**Experience Manager资产中修复的问题**

[!DNL Adobe Experience Manager] 6.5.6.0修 [!DNL Assets] 复了以下问题：

* 预览使用模板创建的营销附属品资产（如宣传册、传单和名片） [!DNL Adobe InDesign] 不显示换行符和分段符(NPR-34268)。

* 文本提取，因此无法对上传的PDF文件进行全文搜索(NPR-34164)。 要修复此问题，请在安 [!DNL sAdobe Experience Manager] 装Service Pack 6后重新启动部署。

* 多页资产的时间轴在时间轴视图下浏览资产时显示应用于所有子资产的注释，而不是显示特定子资产的特定注释(NPR-34100)。

* 如果资产文件夹包含JavaScript、 [!UICONTROL CSS或JSON] 文件格式的资源(NPR-34090)，则不会使用“管理发布”选项来发布资产文件夹。

* 在Omnisearch中取消选择或删除已应用的标记或过滤器会多次执行搜索查询，这会导致搜索时间增加(NPR-34078)。

* 在卡视图中，当工作流（位于文件夹中的资产上）正在进行或待处理时，页面会重新加载，直到工作流完成或终止。 因此，作者无法处理文件夹中必须向下滚动的那些资源(NPR-33986)。

* 如果用户将已发布的资产移动到新位置，则即使取消选择“重新发布”选项，资产 [!UICONTROL 也会重] 新发布。 这会导致发布实例上存在许多孤立资产。 但是，默认的行为是，已发布资产上的移动操作会自动取消发布；如果作者在移动资产时选择 [!UICONTROL 了“重新发布] ”选项，则会重新发布此资产(NPR-33934)。

* 集合 [!UICONTROL 中资产的] “移动资产”页面不会加载所有HTML内容，如调 [!UICONTROL 整／重新发布选项] 。 因此，用户无法完成移动操作(NPR-33860)。

* 移动资产并在移动资产的名称和标题中添加特殊字符会在资产的新位置(NPR-33826)创建额外的文件夹（使用相同的名称）。

* [!UICONTROL 当在] “下载”对话框 [!UICONTROL 中选择] “电子邮件 [!UICONTROL ”选项时，资] 产的“下载”按钮会被禁用(NPR-33730)。

* 对资产执行批量操作时，会出现错误“Request-URI过长”，如批量元数据编辑(NPR-33723)。

* 如果上传的JSON文件有空格或特殊字 [!UICONTROL 符值] (NPR-33712)，则会发现JavaScript错误，用户无法通过文件夹元数据模式表单编辑器中的 “通过JSON路径添加”功能选择或删除“下拉框”字段中生成的选项。

* 资产的静态演绎版在使用或中的“打开”选 [!UICONTROL 项更新资] 产时不会更新 [!DNL desktop app] ，并会 [!DNL Adobe Asset Link] 同步回( [!DNL Adobe Experience Manager] CQ-4296279)。

* 在列视图中，对一组资产执行移动操作时也会移动那些在使用过滤器选项之 [!UICONTROL 前选定] 的资产。 请注意，使用 [!UICONTROL Filter] 选项会取消选择以前的选择(NPR-34018)。

* 在资产的搜索建议中，在特殊字符前添加反斜杠，这些特殊字符在其名称中具有特殊字符(NPR-33834)。

* 在文件夹元数据模式 [!UICONTROL 表单中创建下拉列表]，用户无法从“字段 [!UICONTROL 选择] ”列中选择值(CQ-4297530)。

* 在6.5上安装6.5 Service Pack 5或先前版本( `/var/workflow/models/dam`NPR-34532)时，将删除资源自定义工作流模型 [!DNL Experience Manager] (在 [!DNL Experience Manager] 中创建)的运行时副本。 要检索运行时副本，请使用HTTP API将工作流模型的设计时副本与运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

**Dynamic Media中修复的问题**

* 如果用户在创建视频用户档案后在编辑中定义编码设置，则会从视频用户档案中删除智能裁剪设置(CQ-4299177)。

* 当用户在资产详细信息页面的侧边栏选项(例如， [!UICONTROL 概述]、时间 [!UICONTROL 轴]、查 [!UICONTROL 看器])之间切换时，页面加载时资产闪烁(NPR-34235)。

* 重新处理作业时会发现以下问题：

   * 重新处理作业返回的作业句柄中缺少作业ID。

   * 重新处理视频日志的作业（仅文件名，而非完整路径）。

   * 重新处理作业没有将资产类型设置为静态的选项。

   * `ExcludeFromAVS` 选项(CQ-4298401)。

* 当将图像用户档案添加到具有多个长宽比（例如，11）的文件夹时，智能裁剪功能会出错而失败(NPR-34082)。

* 当用户在配置了Dynamic Media Scene7的工具 [!UICONTROL 中] ,“工作流”选项卡的“工作流 [!UICONTROL 存档] ”页面上向下滚动时， [!DNL Adobe Experience Manager] 将触发DAM更新资产工作流(CQ-4299727)。

* 查看器预 [!UICONTROL 设编] 辑器 [!UICONTROL “行为”] 选项卡中的符号未本地化(CQ-4299026)。

* 如果查看器处于响应模式，则主视图以不正确的布局显示图像，而该布局不适合查看器(CQ-4298293)。

* 对Adobe Experience Manager图像预设 [!UICONTROL 的更] 改不会同步到Scene7出版系统(CQ-4299713)。

### [!DNL Commerce] {#commerce-6560}

* 移动资产时，不会重新计算产品中资产的链接(NPR-34098)。

### 平台 {#platform-6560}

* 无法使用诊断工具在升级的Experience Manager实例上下载日志(NPR-34336)。
* 由于依赖于特定版本的基础包(CQ-4300520), `cq-wcm-api` 升级失败并出现错误。
* 未指定默认 **[!UICONTROL 代理]** (发 **[!UICONTROL 布)配置的Connect]** Timeout和Socket Timeout(NPR-33707)设置的默认值。
* 对下的映射配置 `/etc/map.publish` 的更新不反映在站点页面上(NPR-34015)。
* [API参考文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 不包括包的文 `com.day.cq.tagging` 档(CQ-4295864)。

### 用户界面 {#ui-6560}

* 卸载浏览器界面不显示所有作业主题(NPR-34308)。
* 配置浏览器界面不显示所有配置(NPR-33644)。
* 搜索要模 `Esc` 拟的用户时按键时，“用 **[!UICONTROL 户]** ”对话框将关闭，而不是用户列表(NPR-34084)。

### 集成 {#integrations-6560}

* 长名称的活动未与 [!DNL Adobe Target] 同步(NPR-34254)。

### 翻译项目 {#translation-6560}

* 如果用户包含特殊字符，则不会 `authorizableID` 创建翻译项目(NPR-33828)。

### Sling {#sling-6560}

* 运行状况检查和模式检测器具有重叠的功能。 结果，Heath检查从产品中删除(NPR-33928)。

### WCM {#wcm-6560}

* 基础组件——将基础图像组件添加到页面并引用图像时， `Undo` 此操作不起作用(NPR-34516)。

* 无法使用页面移动操作(CQ-4303028)。

### [!DNL Communities] {#communities-6560}

* 在社交媒体上共享帖子显示一个过时的选项Google+(NPR-33877)。

* 社区成员无法修改组模板或其他组功能设置(NPR-33530)。

* 论坛帖子中未正确生成图像上的超链接标记(NPR-33464)。

* 在“社区分配”功能(NPR-33442)中可识别辅助功能故障。

* 通过admin console添加的社区组的现有用户将在社区组控制台中进行任何修改时从用户列表中删除(NPR-34315)。

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Forms]。 They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

**自适应表单**

* 当缺少自适应表单片段时，自适应表单无法呈现(NPR-34302)。

* 自适应表单字段的帮助内容描述显示段落HTML标记(NPR-34116)。

* 当您选择“在服 **[!UICONTROL 务器上重新验证]** ”属性时，自适应表单无法提交(NPR-33876)。

* “提 **[!UICONTROL 交到REST端点]** ”提交操作不适用于自适应表单(CQ-4299044)。

* 辅助功能：当您尝试提交自适应表单而不上传必填字段的附件时，焦点不会自动转移到附件字段(CQ-4298065)。

* 向自适应表单的表中添加行时，“ **[!UICONTROL 添加到顶部]** ” **[!UICONTROL 和“添加到底部]** ”选项不显示适当的结果(CQ-4297511)。

* 值 [!UICONTROL 提交脚本] 触发不正确，这会导致自适应格式的数据丢失(CQ-4296874)。

* 对于本地化的自适应表单，日期选取器无法正常工作(NPR-34333)。

* 当文件名中有下划线或空格时，无法将文件附加到自适应表单(CQ-4301001)。

* 当嵌套可重复面板的出现次数多于其父面板时，此类嵌套可重复面板的所有出现次数都无法预填充(NPR-33666)。

* 自适应表单具有一些开放的资源解析器。 这会导致提交失败。 出现间歇性问题(CQ-4299407)。

**工作流**

* 当工作流审批者上传附件时，附件将重命 `undefined` 名为(NPR-33699)。

* [!DNL Experience Manager] 工作流清除操作失败并显示以下错误消息(NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 应用程序 [!DNL Windows] 在提交表单后停止响应(NPR-34409)。

* 安装AEM Service Pack时，项 **目的** “待办事项”列表不显示为链接。 “待办事项 **”项的** 文本包括HTML标记(NPR-34317)。

**交互式通信**

* 当包含包含嵌套可重复组件的文本文档片段时，交互通信无法保存(NPR-34095)。

**通信管理**

* 修改包含文档字典值的文本片段时，代理UI停止响应(NPR-33930)。

* 将内容从文档复制 [!DNL Microsoft Word] 粘贴到字母中的文本文档片段会导致格式问题(NPR-33536)。

**文档服务**

* 使用Output和Forms服务从XDP文件生成PDF文件时，会导致缺少文本和文本重叠(NPR-34237、CQ-4299331)。

* 将HTML文件转换为PDF时， `MaxReuseCount` 无法配置属性(NPR-33470)。

* 下载包含Reader扩展的交互功能的PDF文件时，无法使用(NPR-33729)向PDF文 [!DNL Adobe Reader] 件添加附件。

**文档安全**

* 在安装Service Pack(NPR-34310)后，无法在PDF文件中使用基于HSM的 [!DNL Experience Manager] 证书执行签名操作。

**设计人员**

* 无法在Designer 6.5.x版中打开XForm(CQ-4295322)。

* 打开Designer时，“欢迎”屏幕显示错误的年份(CQ-4295289)。

* 在服务器 [!DNL Acrobat DC] 上安装时，“分 **[!UICONTROL 发表单]** ”选项处于非活动状态(CQ-4296304)。

有关安全更新的信息，请参阅 [Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html)。

## Install 6.5.6.0 {#install}

**设置要求**

* AEM 6.5.6.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 可在Adobe软件分发上下载 [服务包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。
* 在具有 MongoDB 和多个实例的部署中，使用包管理器在其中一个 Author 实例上安装 AEM 6.5.6.0。
* 在安装之前，请拍摄AEM实例的快照或新备份。
* 安装之前请重新启动该实例。虽然仅当实例仍处于更新模式时才需要这样做（实例从较早版本更新时也需这样），但如果实例运行较长时间，则建议执行此操作。

>[!NOTE]
>
>Adobe不建议删除或卸载Adobe Experience Manager6.5.6.0包。

### 安装Service Pack {#install-service-pack}

请执行以下步骤在现有的Adobe Experience Manager6.5实例上安装Service Pack:

1. 从“软件分发”下 [载服务包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6.zip)。

1. 打开包管理器，然 **[!UICONTROL 后单击]** “上传包”以上传包。 要了解如何使用它，请参阅 [包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)。

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>包管理器UI上的对话框有时会在安装服务包时退出。 Adobe建议您在访问部署之前等待错误日志稳定。 请等待与卸载更新程序包相关的特定日志，然后确保安装成功。 Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**自动安装**

在工作实例上自动安装Adobe Experience Manager6.5.6.0有两种方法：

答：当服务器联机 `../crx-quickstart/install` 可用时，将包放入文件夹。 软件包会自动安装。

B.使用包 [管理器中的HTTP API](https://helpx.adobe.com/cn/experience-manager/aem-previous-versions.html)。 使 `cmd=install&recursive=true` 用以安装嵌套包。

>[!NOTE]
>
>Adobe Experience Manager6.5.6.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页()`/system/console/productinfo`在“已安装产品”下显示更 `Adobe Experience Manager (6.5.6.0)` 新的 [!UICONTROL 版本字符串]。

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi捆绑包 `org.apache.jackrabbit.oak-core` 版本为1.22.3或更高版本(使用Web控制台： `/system/console/bundles`)。

要了解经认证可与此版本一起使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md)。

### 安装Adobe Experience Manager Forms加载项包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 AEM Forms，请跳过。Adobe Experience Manager Forms的修复通过单独的附加包提供。

1. 确保已安装Adobe Experience Manager服务包。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### 在JEE上安装Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。Adobe Experience Manager Forms的JEE修复通过单独的安装程序提供。

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0018](jee-patch-installer-65.md).

### UberJar {#uber-jar}

Maven Central存储库中提供UberJar 6.5.6.0Experience Manager [版](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.6-1.0/)。

要在Maven项目中使用UberJar，请 [了解如何使用UberJar](/help/sites-developing/ht-projects-maven.md) ，并在项目POM中包含以下依赖项：

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.6-1.0</version>  
      <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>从此版本开始，UberJar和其他相关对象可在Maven Central存储库中使用，而不是Adobe公共Maven存储库(repo.adobe.com)。 主UberJar文件已重命名为 `uber-jar-<version>.jar`。 因此，标签没 `classifier`有 `apis` 任何值（作为值） `dependency` 。

## 已弃用功能 {#removed-deprecated-features}

本节将列表6.5.6.0Experience Manager中标记为已弃用的特性和功能。计划在将来版本中删除的功能将首先设置为已弃用，并设置一个替代选项。

建议客户检查他们是否在当前部署中使用了该功能，并制定计划更改其实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | 已 **[!UICONTROL 弃用AEM云服务选择]** -加入屏幕。 随着AEM和目标集成在AEM 6.5中更新以支持Target Standard API(通过AdobeIMS和I/O使用身份验证)，以及AdobeLaunch在指导页面以进行分析和个性化方面的作用日益增强，选择加入向导的功能已变得无关紧要。 | 通过各自的AEM云服务配置系统连接、AdobeIMS身份验证和AdobeI/O集成。 |
| 连接器 | 针对Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR Connector已在AEM 6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 如果您 [!DNL Experience Manager] 在6.5上安装6.5 Service Pack 5或以前的 [!DNL Experience Manager] Service Pack，则会删除资产自定义工作流模型(在中创建 `/var/workflow/models/dam`)的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果在文件夹元数据AdobeForms编辑器和元数据Forms编辑器中编 [!UICONTROL 辑和创建层叠规则时遇到问题，请] 与支持部门联系 [!UICONTROL 。使用“定义规则] ”对话框，您可 [!UICONTROL 以在“文件夹元数据模式”和“元数据模式] 编辑器”中编辑和创建层叠规则时遇到问题，请与支持部门联系。 请注意，已创建和保存的规则正按预期运行。

* 如果层次结构中的文件夹已重 [!DNL Experience Manager Assets] 命名，且包含资产的嵌套文件夹已发布到 [!DNL Brand Portal]，则只有在根文件夹再次发布后，才会更新 [!DNL Brand Portal] 该文件夹的标题。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他字段可解决此问题。

* 如果 [!UICONTROL 连接的资产配置向导] 在安装后返回404错误消息，请使用包管理器 `cq-remotedam-client-ui-content` 手动重 `cq-remotedam-client-ui-components` 新安装和包。

* 安装AEM 6.5.x.x时，可能会显示以下错误和警告消息：
   * “在 AEN 中使用 Target Standard API（IMS 身份验证）配置 Target 集成，然后将“体验片段”导出到 Target 时，会导致创建错误的选件类型。而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证将失败。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 AEM 6.5.6.0 中包含的 OSGi 包和内容包:

* [AEM 6.5.6.0 中包含的 OSGi 包列表](assets/6560_bundles.txt)

* [AEM 6.5.6.0 中包含的内容包列表](assets/6560_packages.txt)

## Restricted sites {#restricted-sites}

这些网站仅适用于客户。如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系客户支](https://docs.adobe.com/content/help/en/customer-one/using/home.html)持有关访问支持门户的详细信息，请参 [阅访问支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

>[!MORELIKETHIS]
>
>* [AEM 6.5 发行说明](/help/release-notes/release-notes.md)
>* [AEM 产品页面](https://www.adobe.com/cn/marketing/experience-manager.html)
>* [AEM 6.5 文档](https://helpx.adobe.com/cn/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

