---
title: '[!DNLAdobe Experience Manager] 6.5以前的Service Pack发行说明。'
description: 6.5 Service [!DNL Adobe Experience Manager] Pack的发行说明。
contentOwner: AK
translation-type: tm+mt
source-git-commit: 359eb60c0ba3845d7aa0ca58488aa945a9f45aea
workflow-type: tm+mt
source-wordcount: '11484'
ht-degree: 25%

---


# 以前 Service Pack 中包含的修补程序和功能包 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager6.5.5.0是一项重要更新，包括自2019年4月发布6.5版本以来发布的新功能、关键客户请求的增强功能以及性能、稳定性和安全 **性改进**。 它可安装在Adobe Experience Manager6.5之上。

6.5.5.0中引入的一些 [!DNL Adobe Experience Manager] 主要功能和增强功能包括：

* 不允许匿名访问CRXDE Lite。 而是将用户定向到登录屏幕。 请参 [阅使用CRXDE Lite开发](/help/sites-developing/developing-with-crxde-lite.md)。

* 自定义收件箱中显示的列 [!DNL Adobe Experience Manager] 名称。

* 改进了Experience ManagerWeb内容管理(WCM)中各个区域（如页面编辑器、核心组件、RTE和管理员用户界面）的辅助功能。

* 另存为 [!DNL Interactive Communication] 草稿。

* 支持Experience Manager [!DNL Oracle WebLogic 12] ·Forms在JEE上。

* 改进了用户界面流 [!DNL Adobe Experience Manager Assets] 中的异常处理。

* 要获取Dynamic Media Scene7的发布URL，将向界 `getRemoteAssetPublishURL` 面添加新 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 方法。

* [符合Web内容](#assets-6550)[!DNL Adobe Experience Manager Assets] 辅助功能指导原则(WCAG)的辅助功能增强。

* 从Adobe Experience Manager内删除了包共享集成。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.3。

有关列表6.5 Service Pack 5中引入的功能、主要亮点和主要功能的完整Experience Manager，请参 [阅Adobe Experience Manager6.5 Service Pack 5中的新增功能](new-features-latest-service-pack.md) 。

以下是6.5.5.0版中提 [!DNL Experience Manager] 供的修复列表。

### [!DNL Sites] {#sites-6550}

* Experience Manager站点提供了一个选项，用于发布或取消发布别名中的页面。 此选项无效(NPR-33415)。
* 从包含多个模板的模板中删除布局容器时，该模板无法正确呈现(NPR-33347)。
* 当“Experience Manager站点”页面是包含多个Live Copy的大型内容集的一部分时，页面版本历史预览无法加载(NPR-33311)。
* 使用“移动”命令重命名Experience Manager站点页面时，页面标题不会更新(NPR-33264)。
* 在列视图中移动页面时，列会消失(NPR-33216)。
* 当语言副本中的本地组件名称与蓝图中某个组件的名称相同并且从蓝图中转出该组件时，术语不会添加 `_msm_moved` 到本地组件的名称中(NPR-33208)。
* 页面重定向servlet将。html附加到ResourceType不为的Experience Manager站点URL `cq:Page` (NPR-33176)。
* 粘贴子树时，没有选项可决定是否粘贴相应的子页面(NPR-33149)。
* 组件在实时使用中的结果数限于数字49(NPR-33058)。
* 当您将内容片段基于模式并且它包含强制文本区域或路径字段时，内容片段无法保存(NPR-33007)。
* 当您使用默认的体验片段组件创建自定义组件并在Experience Manager站点页面中使用它时，Experience Manager不显示自定义组件的引用（用法）(NPR-32852)。
* 重命名具有大量引用的文件夹时，不会更新对该文件夹的许多引用(NPR-32765)。
* 启用源代码编辑选项后，该选项对内联全屏选项可用，但富文本编辑器的编辑对话框和全屏选项仍缺失(NPR-32763)。
* 如果您有多个字段，并且它在蓝图的页面属性中包含必填字段（如下拉列表或路径字段），则当转出包含此多字段的页面时，不会保存Live Copy的页面属性(NPR-32751)。
* 屏幕阅读器无法使用标题结构来导航页面。 此外，“组件”选项卡的标签错误(NPR-32648)。
* 分页开始时，体验片段选取器不加载所有项目(NPR-32605)。
* 撤消读取、修改、创建和删除Live Copy的创作权限。 每个作者都必须明确提供读取和修改权限才能在Blueprint中移动页面(NPR-32550)。
* 内容作者无法为与Adobe Analytics(NPR-32548)集成的页面创建Launch。
* 当用户通过同步恢复继承时，父页面的Live Copy不会与Blueprint同步，并显示不正确的状态(NPR-32500)。
* Experience Manager站点编辑器页面加载需要15秒以上的时间(NPR-32413)。
* 某些字段不显示“取消继承”选项(NPR-32362)。
* 当您为体验片段组件选择路径并选中打开选择对话框复选框时，您不会导航到路径浏览器中的选定路径(NPR-32308)。
* 从Experience Manager6.2升级到Experience Manager6.5时，静态模板的Parsys组件无法正确显示。 Parsys组件的高度设置为0，并且其中的组件不可见(NPR-33663)。
* 当用户复制并粘贴同一页面上的布局容器时，布局容器中的组件不会显示(NPR-33648)。
* 调度程序运行状况 `Invalid cookie header` 检查在日志文件中显示警告消息(NPR-33629)。
* PreferencesServlet中反射的XSS(NPR-33438)。
* 匿名用户可以访问CRXDE Lite功能(GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>建议的Windows [!DNL Experience Manager desktop app] 用户升级到 [桌面应用程序版本2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) ，以访问实例上的DAM存储 [!DNL Adobe Experience Manager 6.5.5.0] 库。 因为他们在使用桌面应用程序版本2.0.2 [!DNL Adobe Experience Manager] 访问6.5.5.0实例上的DAM存储库时可能会遇到问题。

**Experience Manager资源中的辅助功能增强**

* 现在，可以将键盘焦点放在“注 [!UICONTROL 释] ”列表上，并可单击选项 [!UICONTROL 在“时间轴Npr资产”面板中“] 创建新版本”下 [!UICONTROL 创建版本注释(] NPR-33424)。

* 现在可以使用键盘 [!UICONTROL 键访问资源的] “视图设置”选项 [!UICONTROL 并更改“视图设] 置”对话框中的设置(NPR-33420)。

* 组合框的列表框弹出窗口（在不同页面的各个字段中）现在将条目显示为列表选项，屏幕阅读器可以宣布这些选项(NPR-33516)。

* 可排序标题(在列表视图、 [!UICONTROL 时间轴] 视图和管理发 [!UICONTROL 布页面中] )的排序功能现在由屏幕阅读器宣布，并且列标题的排序控件可通过键盘访问(NPR-32979)。

* 可单击的元素（如注释卡、版本更新、组合框和菜单的V形图标）现在可以使用键盘进行集中处理并与之交互(NPR-33514)。

* 屏幕阅读器现在可以正确地宣布Insights视图上的洞察图标( [!UICONTROL 用于使用] 、展示和点击)的功能（或操作目的）(NPR-33513)。

* 只读表单字段(例如，资产属性 [!UICONTROL “基本] ”选项卡 [!UICONTROL 上禁用的字段])现在可使用键盘(NPR-33493、CQ-4273031)进行聚焦。

* 各种输入字段中的标签现在是永久标签（因此可访问），而不仅仅是占位符标签，在输入文本时它们会消失(NPR-33475)。

* 不同的标题级别（如页面标题和章节标题）现在被视为屏幕阅读器用户具有不同级别的标题(NPR-33471)。

* 现在可使用键盘访问交互式用户界面元素，如链接和选项（资产页面的标题和缩放选项、文件夹导航）(NPR-33468、CQ-4271412)。

* 管理 [!UICONTROL 出版物]页面 [!UICONTROL 上的选项、范围和]工作流进度指 [!UICONTROL 示符现在由屏幕阅读器正确读] 出，作为进度指示符，而不是选项卡(NPR-33416)。

* 星级图标的颜色(如资产属 [!UICONTROL 性中Advanced][!UICONTROL （高级）选项卡的] “评级”部分或卡视图中  )会更改，以使视觉受限且无颜色感知的用户能够看到相应的对比度(NPR-33414)。

* 现在，可使用键 [!UICONTROL 盘键] (NPR-33397)访问资产详细信息页面上“注释”字段旁的V形向上箭头。

* 现在，屏幕阅读器 [!UICONTROL 正确宣] 布了 [!UICONTROL “资产属性”和“左边栏导航] ”（在资产用户界面上）上的“标记”对话框的展开和折叠状态(NPR-33396)。

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* 当导航树结构时，屏幕阅读器现在可以正确地宣布树视图控件的各个元素(NPR-33304)。

* 现在可使用键盘 [!UICONTROL 键访问] “资产详细信息”页上“时间轴”视图下的不同版本的资产(NPR-33283)。

* 使用搜索功能时，屏幕阅读器现在会公布显示在Omnisearch组合框中的搜索建议的名称(NPR-33280)。

* “引用”边 [!UICONTROL 栏中的可单] 击元素和 [!UICONTROL “转到”] 链接现在由屏幕阅读器宣布为可单击元素(NPR-33278)。

* 屏幕阅读器在打开“共享链接”对话框时不再 [!UICONTROL 公布] “共享链接”对话框的表结构信息（如行1、单元格1、表）(NPR-33268)。

* 各种组合框元素（如“路径”字段以及在资产属性的“基本”选项卡中打开“选择”对话框的选项）的用途现在由屏幕阅读器正确宣布(NPR-33235)。

* 现在，当列表视图表中的行处于键盘焦点时，会向屏幕阅读器用户传达这些行可选择的信息。 当指针悬停在行上时，屏幕阅读器会宣布该信息(NPR-33234)。

* 现在，屏幕 [!UICONTROL 阅读器](NPR-33206)可以访问 [!UICONTROL 用于删除Properties] Basic( [!UICONTROL 属性)选项卡中Tags（标记）] 字段下各个选定标记的选项(  含x)。

* 日历日期选取器现在可通过屏幕阅读器用户和视力正常的键盘用户使用键盘进行聚焦和操作(NPR-33200)。

* 切换到在列表视图和卡视图之间切换的切换现在可向屏幕阅读器正确显示其功能(调整视图)(NPR-33069)。

* 现在可访问左边栏中的菜单。 屏幕阅读器会相应地宣布扩展菜单的功能和目的(NPR-33068)。

* 列表框和许多其他用户界面元素现在可供失明的屏幕阅读器用户访问，屏幕阅读器会宣布有关这些元素的以下信息(NPR-33040):

   * 提交表单之前，是否需要对元素进行用户输入。
   * 元素是否不可编辑。
   * 是否选择了构件。

* 现在可以使用键盘访问打开过滤器边栏的选项(NPR-32842、CQ-4273018)。

* 列表视图列标题中的复选框控件现在可访问，并且屏幕阅读器会宣布使用该控件的目的(NPR-32722、NPR-33005)。

* 日历日期选取器中小时(HH)和分钟(mm)字段的标签现在是永久标签而不是占位符标签，并且当用户在这些字段中输入文本时不会消失(NPR-32720)。

* 通知的链接文本（单击铃图标后显示）现在会通知屏幕阅读器用户，他们使用选项卡访问每个链接(NPR-32645)。

* [!UICONTROL 现在可]以使 [!UICONTROL 用键盘]访问Insights视图 [!UICONTROL 中资产卡的“选择”、“下载”] 、“属性”和“更多操作”选项(NPR-32609)。

* 当屏幕阅读器使用键盘访问时，可视隐藏内容（如搜索结果中标题菜单栏的内容）不再被屏幕阅读器公布(NPR-32606)。

* 屏幕阅读器现在宣布控件上标签用于移动到日历日期选取器中的下一个和上一个月(NPR-32604)。

* 星级图标现在可以使用键盘键(NPR-32513)获得焦点并具有操作性。

* 现在可通过选项卡（聚焦在音量滑块上）和箭头键（调整键盘上的音量）访问控制视频音量的功能(NPR-32065)。

* “文件大小”滤[!UICONTROL 镜的下界](From)和上界(To)输入字段的用途现在向失明的屏幕阅读器用户宣布(NPR-32064)。

* “创 [!UICONTROL 建并翻] 译”表单中的“语  言”菜单现在可供浏览模式下的屏幕阅读器访问(CQ-4293906)。

* 现 [!UICONTROL 在可] 以通过以下增强功能访问“引用”面板(NPR-33261、CQ-4293798):

   * 在浏览模式下，屏幕阅读器的焦点不再移动到“站点引用”、“资产引用”、 [!UICONTROL “副本]”和“表单引用 [!UICONTROL ”等部分下]隐藏的多行编  辑字段中。

   * 屏幕阅读器现在宣布“站点引 [!UICONTROL 用”和] “语 [!UICONTROL 言副本”元素的角色] 。

   * 浏览模式下屏幕阅读器的焦点以有意义的顺序转移到各种元素。

* [!UICONTROL 元数据模式] “编辑器”页面及其元素现在可使用键盘访问，并且屏幕阅读器友好(CQ-4290962、CQ-4272953)。

* 现在，屏 `X` 幕阅读器会宣布符号删除选定标记的目的以及选定标记的数量(CQ-4273017)。

* 为避免使用屏幕阅读器的失明用户产生混淆，屏幕阅读器现在忽略装饰性图标和图像(CQ-4272944)。

**Experience Manager资产中修复的问题**

[!DNL Adobe Experience Manager] 6.5.5.0资产修复了以下问题：

* [!UICONTROL 开始][!UICONTROL ，会禁] 用集合中资产的“创建工作流”对话框上的“创建工作流”选项，从而阻止触发工作流(NPR-32471)。

* 在元数据模式中使用级联弹出窗口时，选择并保存包含撇号的下拉选项（从子项下拉框中）时，在重新打开资产属性后，选定的撇号 [!UICONTROL 选项] 会消失(NPR-32649)。

* [!UICONTROL 如果Asset Insights Sync] Job遇到无效条目（在Analytics端）而不是转到下一个条目(NPR-32674)，则停止并失败。

* 陀螺仪无法正常工作，因为在全景查看器中，默认情况下在移动浏览器上禁用运动传感器(CQ-4272937)。

* [!UICONTROL 在6.5] .1上安装6.5.3时，连接的资产配置向导无法处理404错误(NPR-32730)。

* 在XMP写回过程中，所有自定义命名空间元数据属性都将自定义命名空间前缀更改为ns2，而不是配置的命名空间前缀(NPR-32748)。

* 不会触发延迟加载，选择从通知收件箱中查看任务时只显示100个资源(NPR-32750)。

* `NullPointerException` 由于新创建的用户用户档案(SAML/SSO)中缺少节点首选项而观察到。 此错误会阻止新登录的用户 [!DNL Adobe Experience Manager Stock] 使用集成(NPR-32777)。

* 在打开包含超过10,000个资源的智能集合时，会在日志中观察到遍历警告(NPR-32980)。

* 在Dynamic Media Scene7运行模式中将资源从一个文件夹移到另一个文件夹时， [!DNL Adobe Experience Manager] 资源名称将更改为小写(NPR-32995)。

* 在从搜索结果导航到其属性，然后返回搜索结果删除该资产后，无法删除已搜索的资产(NPR-32998)。

* [!UICONTROL 在“移动] 资产”界面中选择目标文件 [!UICONTROL 夹时] ,“下一步”选项仍处于禁用状态(NPR-33356)。

* [!UICONTROL 在选择父] 节点（其中显示单个子文件夹），然后选择子文件夹时，未启用“下一步”选项(NPR-33275)。

* 对于具有删除权限的用户，在Adobe资产链接(AAL)上会禁用登记和注销权限，即使已授予读取、创建或修改等其他权限(NPR-33272)。

* 智能裁剪演绎版在资产下载对话框中不可用(NPR-33167)。

* 在具有智能裁剪用户档案的文件夹下打开PDF的演绎版边栏的日志中会出现异常(CQ-4294201)。

* 如果在与Dynamic Media Demia Deta RunmodeExperience Manager时  ，默认情况下禁用Dynamic Media同步模式，则不发布图像预设(CQ-4294200)。

* 批量上传时的资产处理会卡住，而工作流实例会显示DAM更新资产的卡住实例(CQ-4293916)。

* 在Experience Manager上创建Dynamic Media配置是有效的，但在用户界面上，选择“保存”时不会发生任何情况(CQ-4292442)。

* F4V视频资源的预览在Safari/Mac上的渐进式播放中不工作(CQ-4289844)。

* 在智能裁剪父级文件夹内的资产时会创建额外的文件夹，其 `.` 名称中带有点字符(CQ-4289337)。

* 缩览图已断开，复制视频时不会显示视频处理横幅(CQ-4284125)。

* 对于某些型号的相机视图为空的型号，尺寸查看器在Firefox中错误地显示了空缩览图(CQ-4283447)。

* 6.5.5.0中修复的性能问题包括(CQ-4279206):

   * 将大型二进制文件上传到Dynamic Media图像处理服务器需要太长的时间。

   * Experience Manager缩略图生成时间因Dynamic MediaScene7体系结构而增加。

* 对于拥有大量资产的客户，动态媒体Scene7迁移问题失败(CQ-4279206)。

* 如果使用视频360查看器， `setVideo` 则其布局会被破坏，并且视频在使用 `video= modifier` 时会下移(CQ-4263201)。

* 安装Experience ManagerSDL包时显示错误消息(NPR-33175)。

* Experience Manager中的SSRF漏洞(NPR-33435)。

### 平台 {#platform-6550}

* 如果 [!DNL Sling] 在(NPR-33362)下 `sling:match` 创建了映射条目， `/etc/maps` 则不调用该过滤器。
* Experience Manager因分段故障而 [!DNL Apache Lucene] 崩溃(NPR-32988)。
* [!DNL Jackson] experience manageruberjar文件中缺少核心包(NPR-32848)。
* CRXDE Lite在没有节点属性读取权限的情 `jcr:primaryType` 况下不为用户加载内容(NPR-32611)。
* [!DNL Granite] 维护任务调度程序在Experience Manager部署期间重新初始化过频繁(CQ-4294627)。
* 当SQL查询执行长时（例如7小时）,Experience Manager停止响应(NPR-33044)。

### 用户界面 {#ui-6550}

* 多字段中不保留单选按钮选择(NPR-33309)。
* 延迟加载限制对列表视图无效(NPR-33124)。
* 如果没有匹配项，则搜索结果页面不显示消息(NPR-32974)。
* Omnisearch过滤器将忽略所 `/content` 选位置(NPR-32849)返回节点下的所有匹配项。

### 集成 {#integrations-6550}

* 当发布具有Adobe Target组件的页面时，将清除内部缓存(NPR-33162)。
* 与Adobe Target的整合在11 [!DNL Windows Internet Explorer] 个方面不起作用(NPR-33111)。
* 配置Adobe Target时， [!UICONTROL 选择报告][!UICONTROL 源时不显] 示公司和报告包字段(NPR-32502)。
* 使用Adobe [!DNL Experience Fragments] I/O导出时，源产品等元数据不会导出到Adobe Target(NPR-32159)。
* 本地Experience Manager管理组中的授权IMS用户无法创建或修改IMS配置(NPR-33045)。
* Adobe启动配置页面不显示所有记录(NPR-33011)。
* 由于JavaScript错误(NPR-32996)，内容作者组中的用户无法编辑Adobe Target组件的属性。
* JSON的跨站点脚本(NPR-32744)。

### 翻译项目 {#translation-6550}

* 译文标记不会从第三方翻译服务导入Experience Manager(NPR-33154)。
* 翻译配置页面显示的翻译提供程序与用于翻译的翻译提供程序不同(NPR-32971)。
* 将体验片段文件夹添加到现有翻译项目会创建新项目(NPR-32843)。
* 运 `NullPointerException` 行转换作业的日志中显示错误(NPR-32628)。

### WCM {#wcm-6550}

* 页面编辑器 [!DNL Sites] -页面编辑器不允许仅使用键盘的用户跳到主内容，而不是通过标题中的所有可用选项来切换选项卡焦点(CQ-4293883)。
* 页面编辑器——由于版本和版本中的更新，使用Well组件并包含已保存数据的面 [!DNL Chrome] 板不 [!DNL Firefox] 会显示(CQ-4292995)。
* MSM —— 从页面中删除组件不会从页面的已发布版本中删除组件(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* 从中删除已发布的元数 [!DNL Brand Portal] 据模式会导致错误(CQ-4292063)。
* 如果管理员通 [!DNL Experience Manager Assets] 过Adobe开发人员控制台使用Brand Portal配置6.5.4, [!DNL Brand Portal] 则用户无法将贡献文件夹的资产从 [!DNL Brand Portal] 发布到 [!DNL Experience Manager] (NPR-33046)。
* 重复复制父文件夹会导致冲突(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* 无法使用快速编辑菜单选项删除审核控制台中的卡(NPR-33117)。
* 访问活动流页 [!UICONTROL 面时出错] (NPR-33146)。
* 在作者实例上删除的组不会从所有发布实例中删除(NPR-33199)。
* 创建新组后，作者不会被重定向到 [!UICONTROL 第11号] “社区 [!DNL Internet Explorer] 组”部分(NPR-33205)。
* 访问Experience Manager收件箱中的邮件不会将邮件的状态更改为“已读”(NPR-32764)。
* 编辑 [!DNL Communities] 组和更改缩略图图像不会更新组缩略图图像(NPR-32599)。
* 用户无法向社区中的其他用户发送电子邮件(NPR-32598)。
* 提交的博客在用户刷新页面之前不会显示(NPR-32391)。
* 创建通知版本和用户生成内容订阅(UGC)时，会存储源页面的错误ID(CQ-4279355、CQ-4289703)。
* 跨站点脚本问题(NPR-33203)。

### 工作流 {#workflow-6550}

* 加 [!UICONTROL 载左边栏] 中的“时间轴”选项比预期花费的时间要多(NPR-32851)。
* 重新启动Experience Manager实例后，集合的审阅任务的电子邮件包含不正确的有效负荷链接(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience ManagerService Pack不包含修复 [!DNL Forms]。 它们是通过单独的 Forms 附加组件包交付的。此外，还发布了包含针对AEM Forms的JEE修复的累积安装程序。 有关详细信息，请参 [阅在JEE上安装Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[Forms加载项和安装Experience ManagerForms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

* 通信管理：在目标区的资产顺序在提交信件(NPR-33359、NPR-33153)后混乱。
* 适应性Forms:当用户编辑自适应表单时，“页 [!UICONTROL 面信息] ”菜单中可 [!UICONTROL 用的“开始工] 作流”选项将不起作用(NPR-33004)。
* 适应性Forms:用户无法保存包含多个附件的自适应表单(NPR-32997)。
* 适应性Forms:在自适应表单中更改面板布局会导致错误(CQ-4293880)。
* 适应性Forms:自适应表单词典中字符串的新行将字 `&#xa;` 符添加到词典(NPR-33266)。
* 自适应Forms辅助功能：当用户将自适应表单预览为HTML表单时，“ [!UICONTROL 涂写签名] ”字段无法保留制表符焦点(NPR-33159)。
* 自适应Forms辅助功能：提交自适应表单时显示的错误消息不链 `aria-describedBy` 接到属性(NPR-33071)。
* 自适应Forms辅助功能：在自适应表单中标记为必填的字段没有在ARIA辅助功能模式中将必填属性设置为True(NPR-33070)。
* PDFG服务：当用户将文本文件转换为PDF时，日文字符无法正确呈现(NPR-33238)。
* PDFG服务： `CreatePDF` 操作无法将PDF文件转换为PDF OCR格式(NPR-32994)。
* PDFG服务：第200个文档实例的PDF转换 [!DNL OpenOffice] 失败(NPR-32766)。
* 后端集成：表单数据模型请求失败，因为由于不正确的非活动状态，刷新令牌过期(NPR-33169)。
* 设计人员：屏幕阅读器根据默认的地理顺序而不是XDP文件中定义的自定义Tab键顺序(NPR-32160)执行Tab键顺序。
* 设计人员：如果启用标记选项，子表单边框将消失在生成的PDF输出中(NPR-32778)。
* 使用GuideSOMProviderServlet存储XSS(NPR-32700)。

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager6.5.4.0是一项重要更新，包括新功能、关键客户请求的增强功能和性能、稳定性、安全性改进，自2019年4月6.5版正式发布 **以来发布**。 它可安装在Adobe Experience Manager6.5之上。

Adobe Experience Manager6.5.4.0中引入的一些主要功能和增强功能包括：

* Adobe Experience Manager资产现在通过AdobeI/O控制台配置了Brand Portal。

* 现在，Adobe Experience Manager Forms [工作流可使用新的](../forms/using/aem-forms-workflow-step-reference.md) “生成可打印输出”步骤。

* [自适应表单](../forms/using/resize-using-layout-mode.md) 、交互式通信的布局模式支持多列。

* 支持 [HTML5表单](../forms/using/designing-form-template.md) 中的富文本。

* [Experience Manager资源中](new-features-latest-service-pack.md#accessibility-enhancements) 的辅助功能增强。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.8。

* 您现在可以将选择性内容子树同 *步到Dynamic Media -Scene7模式* ，而不是所有在 `content/dam`。

* 与SOAP Web服务的表单数据模型集成现在支持元素上的选择组或属性。

* SOAP输入或输出以及复杂的数据结构现在支持动态组替换。

有关最新服务包中引入的功能和主要亮点的完整列表, [请参阅Adobe Experience Manager6.5服务包的新增功能](new-features-latest-service-pack.md)。

### 站点 {#sites-fixes}

* 当Adobe Experience Manager Sites页面的URL包含冒号(`:`)或百分比符号(`%`)时，浏览器停止响应，CPU使用率高峰(NPR-32369、NPR-31918)。

* 当打开Experience Manager站点页面进行编辑并复制组件时，粘贴操作对于某些占位符仍然不可用(NPR-32317)。

* 打开“管理发布”向导后，链接到核心组件的体验片段不会显示在发布引用的列表中(NPR-32233)。

* 触屏UI中的Live Copy概述渲染比经典UI花费的时间要长得多(NPR-32149)。

* 当服务器时间和计算机时间位于不同时区时，计划发布时间在触屏UI中显示服务器时间，而在经典UI中显示计算机时间(NPR-32077)。

* Experience Manager站点无法打开URL中包含后缀的页面(NPR-32072)。

* 当用户编辑内容片段时，内容片段的已删除变体会被恢复(NPR-32062)。

* 允许用户保存内容片段，而无需在必填字段中提供任何信息(NPR-31988)。

* kernel.js和ui.js未预先编译或缓存。 这会导致在渲染页面中增加时间(NPR-31891)。

* 启用PageEventAuditListener时，提交队列的长度会增加。 它影响许多操作的性能，如批量发布、导航、批量资产移动(NPR-31890)。

* 拖动体验片段时，会观察到较长的响应时间(NPR-31878)。

* 当您在响应式网格的占位符中选择“将组件拖动到此处”选项时，会发送GET请求，并且该请求会导致HTTP 403错误(NPR-31845)。

* 在同一文件夹内移动内容时，会禁用页面移动选项(NPR-31840)。

* 在可编辑的模板结构模式下，布局列表中允许的组件显示不正确的结果。 布局容器中只显示具有设计对话框的组件(NPR-31816)。

* 当页面对用户具有只读权限时，“打开属性”选项在sites.html中可见，但在editor.html中则不可见(NPR-31770)。

* 当用户单击“创建”按钮时，页面选项不可用(NPR-31756)。

* 无法同步包含OOTB（现成）设计导入程序组件的Adobe活动中的活动(NPR-31728)。

* 当您尝试将项目符号列表更改为编号列表时，只更改列表的前两个项(NPR-31636)。

* 当页面被取消创作且选择了子节点时，选择对话框仍显示初始节点。 创作页面并用户单击浏览时，页面会重定向到根节点，而不是创作的节点(NPR-31618)。

* “视图配置”对话框对收件箱自定义工作流功能（NPR-32503和NPR-32492）无法正常工作。

* 使用收件箱查看工作流信息时显示错误消息(CQ-4282168)。

### 资产 {#assets-6540-enhancements}

* 在资产收集页面上触发工作流的按钮被禁用(NPR-32471)。

* 在使用Dynamic Media Scene7配置(NPR-32440)的Experience Manager下将资源从一个文件夹移到另一个文件夹时，将在SPS(Scene7出版系统)中创建一个无名称的文件夹。

* 将所有资产（使用全选，然后移动）移动到包含已发布资产的文件夹的操作会失败，并显示错误(NPR-32366)。

* 为${extension}的资产生成再现失败(NPR-32294)。

* 版本历史记录URL显示在资产属性页面的“引用者”字段下(NPR-31889)。

* 无法使用WinZip打开从DAM下载的ZIP文件(NPR-32293)。

* 打开“文件夹设置”以更改文件夹标题或缩略图图像，然后保存文件夹的原始权限(NPR-32292)。

* 计划激活的日历图标不会显示在“状态”列（DAM资产列表的经典UI中）中，该激活计划在以后的日期和时间显示(NPR-32291)。

* 使用代码片段模板创建代码片段时，在代码片段创建过程中搜索集合时出错(NPR-32290)。

* 当从搜索筛选器中选择多个标记时，将触发多个搜索查询(NPR-32143)。

* Experience Manager资产在上传文件名超过50个字符的资产时，用户界面会显示截断的文件名(NPR-32054)。

* 当选中Adobe Stock复选框树的第2级复选框时，“筛选器”面板中的所有复选框都将被清除(NPR-31919)。

* 使用Omnisearch彩块化的文件和文件夹搜索会出现异常(NPR-31872)。

* 即使在相应的元数据模式表单中设置依赖性规则时，也不会删除元数据编辑器中用于强制字段选择的字段突出显示(NPR-31834)。

* 叶级标记的完整名称（来自标记层次结构）不会显示在资产属性页面中(NPR-31820)。

* 在Safari浏览器上使用资源属性页面中的返回命令时出错(NPR-31753)。

* 触屏UI搜索（通过Omnisearch完成）结果页自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* PDF资产的资产详细信息页面不显示操作按钮，但在Dynamic MediaScene7运行模式(CQ-4286705)上运行的Experience Manager中，“到集合”和“添加演绎版”按钮除外。

* 通过Scene7的批量上传过程处理资产需要太长的时间(CQ-4286445)。

* 当用户未在Dynamic Media Client中的“设置编辑器”中进行任何更改时，“保存”按钮不会导入“远程设置”(CQ-4285690)。

* 当支持的3D模型被引入Experience Manager时，3D资产缩略图不会提供相关信息(CQ-4283701)。

* 智能裁剪视频查看器预设的未处理状态会在横幅文本中预设名称旁显示两次(CQ-4283517)。

* 资产的详细信息页面上会观察到在3D查看器中预览的已上传3D模型的容器高度不正确(CQ-4283309)。

* 在IE 11中Experience ManagerDynamic Media Hybrid模式(CQ-4255590)下，旋转式编辑器未打开。

* 键盘焦点卡在Chrome和Safari浏览器的“下载”对话框的“电子邮件”下拉菜单中(NPR-32067)。

* 尝试在Experience Manager上添加DM云配置时，默认情况下未启用“同步所有内容”复选框(CQ-4288533)。

### 基础UI {#foundation-ui-6540}

* 使用“筛选器”面板搜索资产时，鼠标控件会切换到上一个筛选器字段，而不是停留在现有筛选器字段中(NPR-32538)。

* 平台标记：通过在标记字段中键入内容搜索标记会显示根边界外的标记，并且不 `rootPath` 尊重标记字段的属性(NPR-31895)。

* 平台UI:如果在文本字段中添加了无效的路径，则路径浏览器将断开(NPR-31884)。

* 在选择页面时，通知会隐藏在粘滞菜单后面(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)下划线替换URL路径部分的冒号(NPR-32231)。

### 项目 {#projects-6540}

* 即使用户具有在子文件夹中创建项目的权限，用户也看不到“创建”按钮(NPR-31832)。

### 项目翻译 {#projects-translation-6540}

* 在中激活“裁切空格”选项时，创建翻译项目 `Apache Sling JSP Script Handler` 会中断UI(NPR-32154)。

* 将任何要翻译的标记添加到翻译项目时，在UI中出现错误，错误日志中出现空点异常(NPR-31896)。

### 集成 {#integrations-6540}

* 启动库URL生成仅基 `path` 于 `library_name` Launch API中的值，而不基于值 `library_path` (NPR-31550)。

* 处理LiveFyre相关项目时显示错误消息(FYR-12420)。

* ReportSuitesServlet易受SSRF(NPR-32156)的攻击。

### WCM模板编辑器 {#wcm-template-editor-6540}

* 在可编辑的模板结构模式下，布局列表中允许的组件不显示链接按钮组件(CQ-4282099)。

### WCM Page Editor {#wcm-page-editor-6540}

* 选择叠加，然后选择响应式网格将组件拖动到此处时会出现错误(CQ-4283342)。

### Campaign Targeting {#campaign-targeting-6540}

* 目标云配置失败，错误get mbox请求失败(CQ-4279880)。

### Brand Portal {#assets-brand-portal-6540}

* 在升级到Adobe6.5.4(CQDOC-15655) [!DNL Assets] 上的I/O时，Brand Portal用户无法将贡献文件夹资产发布到该Experience Manager。 要立即修复Experience Manager6.5.4，建议下载 [修补程序](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) ，并在创作实例上安装。

* 元数据模式弹出值在资产属性中不可见(CQ-4283287)。

* 元数据子架构不显示基于资产属性中的mimetype的选项卡(CQ-4283288)。

* 取消发布元数据模式会填充错误消息，尽管在后端删除了模式。

* 预览图像不显示已发布的资产(CQ-4285886)。

* 用户无法发布或取消发布名称中包含单报价的资产(CQ-4272686)。

* 下载多个资产时不显示条款和条件(CQ-4281224)。

* 已解决次要安全漏洞。

### 社区 {#communities-6540}

* “创建成员”表单显示为空白页面(NPR-31997)。

* 用户无法视图创作实例的Analytics报告(NPR-30913)。

### Oak-索引和查询 {#oak-indexing-6540}

* 使用Tika分析器分析时，MS Word和MS Excel文档包含JPEG图像，无法分析，并且发现类未找到错误(NPR-31952)。

### 表单 {#forms-6540}

>[!NOTE]
>
>Experience Manager服务包不包含针对Experience ManagerForms的修复。 它们是通过单独的 Forms 附加组件包交付的。此外，还发布了包含针对Adobe Experience Manager Forms的JEE修复的累积安装程序。 有关详细信息，请参 [阅在JEE上安装Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[Forms加载项和安装Experience ManagerForms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

* 通信管理：提交到后处理工作流后，字母会显示额外字符(NPR-32626)。

* 通信管理：在提交到后处理工作流后，字母将显示一个下拉占位符作为文本组件(NPR-32539)。

* 通信管理：在字母模板中定义的默认值不会在预览模式下显示(NPR-32511)。

* 移动Forms:以HTML版本呈现XDP表单时，提交按钮显示为扩展大小(NPR-32514)。

* 文档服务：应用Service Pack 2后，Letter和某些其他页面的URL访问问题(NPR-32508、NPR-32509)。

* 文档服务：如果服务器上的事务数超过特定限制，则HTML到PDF的转换将失败，并且文件类型设置将从服 [!DNL Forms] 务器中删除(NPR-32204)。

* 适应性Forms:浏览器辅助工具工具根据WCAG2 Level AA准则报告自适应表单中的故障(NPR-32312、NPR-32309、CQ-4285439)。

* 适应性Forms:Chrome浏览器辅助工具工具报告最佳实践失败(NPR-32310)。

* 适应性Forms:配置嵌入在Experience Manager站点页面中的自适应表单时的转换问题(NPR-32168)。

* 工作台：使用“为PDF实用程序获取PDF属性”操作服务时显示错误消息(NPR-32150)。

* 文档安全：如果将DisableGlobalOfflineSynchronizationData选项设置为True，则受保护的PDF文件无法脱机打开(NPR-32078)。

* 设计人员：如果启用标记选项，子表单边框将消失在生成的PDF输出中(NPR-32547、NPR-31983、NPR-31950)。

* 设计人员：如果表中存在合并的单元格，则使用输出服务从XDP表单转换的输出PDF文件的辅助功能测试将失败(CQ-4285372)。

* JEE基金会：如果Experience ManagerForms服务器与群集断开连接，缓存问题会阻止它重新连接到服务器(NPR-32412)。

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0是一个重要版本，包含自2019年4月6.5版本正式发布以来发布的性能、稳定性、安全性以及重要客户修复和 **增强功能**。 它可安装在6. [!DNL Adobe Experience Manager] 5之上。

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.6。

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档。

* 已在DAM列表视图中添加可排序的创建日期的新列，并在列表视图中添加资产搜索结果。

* 已在列表视图中启用基于名称列的资产排序。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。 Smart Crop是一项机器学习驱动的功能，它可以在移动帧以跟随场景焦点的同时重新裁剪视频。

* [!DNL Dynamic Media] 支持智能成像。

* 能够在 [工作流中设置](../forms/using/configure-out-of-office-settings.md) “出办公室” [!DNL Experience Manager] 首选项。

* 能够与 [工作流中的其他用户共享收件箱](../forms/using/configure-shared-queues-osgi.md) 或收件箱项 [!DNL Experience Manager] 目。

* 能够在 [批处理模式下生成交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* 捆绑在ContextHub中的jQuery的更新版本为3.4.1。

### 资产 {#assets-6530-enhancements}

**产品增强功能**

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档(NPR-27573)。

* 创建日期的新列（可排序）将添加到DAM列表视图中，并添加到列表视图中的资产搜索结果中(NPR-31312)。

* 在列表视图中，用户可以使用“名称”列 [!UICONTROL 对资产] 列表进行排序(NPR-31299)。

* GLB、GLTF、OBJ和STL文件可在DAM的“资 [!UICONTROL 产详细信息] ”页中预览(CQ-4282277)。

* `ReplicationOnModifyListener` 在(CQ-4281279)中的区块上 [!DNL Dynamic Media] 传期间，会为区块节点触发事件。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。 Smart Crop是一项机器学习驱动的功能，它可以在移动帧以跟随场景焦点的同时重新裁剪视频(CQ-4278995)。

* [!DNL Dynamic Media] 支持智能成像(CQ-422249)。

* 如果在请求中传递视图参数，则搜索或浏览查询将设置为Foundation选取器中的默认视图(NPR-31601)。

**修复**

* 某些PDF文档的元数据在标题被修改时不会更新并保存到PDF中(NPR-31629)。

* 对于文件名中带有加号()的资`+`产(NPR-31547)，资源共享不起作用。

* 默认搜索表单资产管理员搜索边栏中的编辑操作不按预期方式进行(NPR-31502)。

* 在对资产使用Omnisearch视图搜索资产时，不会显示建议(NPR-31496)。

* 当引用的资产被移至其他位置时，收藏集中的资产引用不会更新，因为不同用户引用的不同收藏集也存在相同的资产(NPR-31486)。

* 重复IPTC标记添加到资产元数据(NPR-31328)。

* 当从筛选器边栏触发搜索时，搜索结果计数不能准确更新(NPR-31316)。

* 取消选择“文件类型”过滤器中的二级复选框时，将清除所有复选框，并且搜索栏中的文本与选定或取消选择的属性不同步(NPR-31287)。

* 不能从文件夹的“成员”部分删除所有成员（用户／用户组）;在尝试删除所有用户时，已登录用户将添加到列表(NPR-31171)。

* 无法删除文件名`+`中包含加号()的资源(NPR-31162)。

* 创建下拉菜单（在选择文件夹时显示在顶部菜单中）不显示“文件夹”作为创建选项(NPR-30877)。

* 对用户应用拒绝ACL和路径上的ACL时， `jcr:removeChildNodes` 缺少 `jcr:removeNode` “创建”>“文件上传”操作项(NPR-30840)。

* 上传某些mp4资源时，DAM工作流会进入陈旧状态，导致所有其余工作流都进入陈旧状态(NPR-30662)。

* 将大型PDF文件（几GB）上传到DAM并处理其子资源时，会出现内存不足错误(NPR-30614)。

* 资产的批量移动失败并显示警告消息(NPR-30610)。

* 在以Scene7模式运行时，将资产从一个文件夹移到另一个文件夹时，资产名称 [!DNL Experience Manager] 将更改 [!DNL Dynamic Media]为小写字母(NPR-31630)。

* 编辑远程图像集时，对于与Scene7公司名称(NPR-31340)同名的文件夹中的图像，会出现错误。

* [!DNL Dynamic Media] 包含引用的资产将不会被发布(NPR-31180)。

* 从7- [!DNL Dynamic Media]Scene7模式上 [!DNL Dynamic Media Classic] 传到的时间太长，无法完成(NPR-31048)。

* 添加到图像资产的热点不会通过资产详细信息页面中的交互式图像查看器显示(NPR-30979)。

* 当对中的资产执行的操作被传递到Scene7时，将创建巨大的吊 [!DNL Experience manager Assets] 带作业并重新显示“处理”横幅(NPR-30947)。

* 创建资产和资产的语言副本时发生冲突(NPR-30932)。

* 从以混合模 [!DNL Experience Manager] 式运行 [!DNL Dynamic Media]下载的动态演绎版将断开（它们属于文本类型，内容为“找不到图像”而非图像内容类型）(NPR-30876)。

* [!DNL Dynamic Media] “编码视频”工作流无法为从Adobe Experience Manager的“Scene7” [!DNL Dynamic Media Classic] 模式迁 [!DNL Dynamic Media]移到“”模式的视频生成缩略图(CQ-4282011)。

* 使用不同的Scene7公司ID(CQ-4280548)将资源从一个实例迁移到另一个实例时观察到IpsApiException。

* 当3D资产缩略图被收录到支持的3D模型中( [!DNL Experience Manager] CQ-4283701)时，该缩略图不会提供相关信息。

* 如果3D资产的相机视图很少，则查看器中会显示滚动按钮(CQ-4283322)。

* 在“资产详细信息”页上的DimensionalViewer中预览的已上载3D模型的容器高度不正确(CQ-4283309)。

* 无法在Internet Explorer 11和Safari上使用SmartCropVideoViewer播放视频(CQ-4281422)。

* 在-Scene7运行模式上运行时，使用移动按钮将多个资源从一个文件夹 [!DNL Experience Manager] 移动到另 [!DNL Dynamic Media]一个文件夹失败(CQ-4280384)。

* 当MIME类型不是MP4时，资产详细信息上会显示扭曲的视频(CQ-4279704)。

* 新摄取到具有视频用户档案的文件夹中的视频即使在编码百分比完成到100%后仍处于处理状态(CQ-4279389)。

* 从文件夹移动资源会创建大量sling作业(Scene7API调用)，而非理想的必需(CQ-4278664)。

* 在Scene7，当在DAM中创建图像集（或mediaset）并使用适当的命名约定进行命名时，图像集的名称将更改为小写字母(CQ-4281112)。

* Scene7迁移程序设置发布状态不正确(CQ-4263492)。

* 触屏UI搜索（通过Omnisearch完成）结果页自动向上滚动并丢失内容片段中用户的滚动位置(CQ-4282898)。

* PDF文件不进行索引，内容也不可搜索(CQ-4278916)。

* 错误“用户选取器未列出组：在添加具有不同和的已关闭用户组时，将观察“ `principalName` 预期 `authorizableId` 为false”到“等于true”(CQ-4278177)。

* 资产UI列视图显示所有路径，而不管特定租户的dam根路径如何(CQ-4278175)。

* 资产选择器的搜索未按预期工作(CQ-4275886)。

* 再现工作流失败(CQ-4271928)。

* DAM事件清除将删除最新(`maxSavedActivities`)事件数据并保留之前创建的数据(NPR-31336)。

* 触屏UI搜索（通过Omnisearch完成）结果页自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在触屏UI中选择所有项目，然后取消选择某些项目（文件夹／单个资产）时，操作栏和资产计数不会更新(NPR-31118)。

* 轮询资产 [!DNL Experience Manager] 的作业详细信息时，会显示异常(CQ-4283569)。

### 站点 {#sites}

* 如果LiveCopy继承中断，则Live Copy页面会显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数超过40，则只显示前40个记录。 Blueprint显示其余记录的空行(NPR-31182)。
* 当用户在菜单的描述属性中添加日语或韩语字符时，该菜单显示日语和韩语文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用，基架式富文本编辑器(RTE)。 意外地将内嵌字体大小应用于元素(NPR-31284)。
* 当用户专注于左边栏字段并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容，而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径存储在组件节点而不是多字段节点中(NPR-30882)。
* API `ResponsiveGridExporter` 不返回接 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 口。 该 `com.day.cq.wcm.foundation.model.impl` 包被宣布为私人包(NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 当在非编辑器模式下(在“作者”模式下(不带前缀 `editor.html` 和 `wcmmode=disabled`，或在“发布者”中)打开包含某些体验片段的页面时，请求以HTTP状态错误代码( `500` NPR-30743)结束。
* 用户无法更改其口令并访问其用户档案页(NPR-31161)。

### 搜索和用户界面 {#ui-interface-and-search}

* 在搜索结果页面上从卡视图切换到列表视图时，在可滚动页面之前会出现延迟(NPR-31286)。

* “ [!UICONTROL 全选] ”复选框隐藏在用户界面上的 [!DNL Sites] 列表视图中(NPR-31614)。

* 搜索 [!UICONTROL 结果页] 上的“全选”计数不正确(NPR-31120)。

* 元数据编辑器显示不存在的标记(NPR-31119)。

### 翻译 {#translation}

* 在翻译作业中选择“到期日期”选项时，将显示两个日历弹出窗口(NPR-31270)。

### 平台 {#platform}

* Web控制台中的Mime类型选项无效(NPR-31108)。

* 配置单一登录时不接受客户端证书(NPR-31165)。

* 基于 Jetty 的 HTTP 服务的缓冲区大小配置中的更新未保存 (NPR-30925)。

* QueryBuilder现在支持 `fn:name()` xpath查询中的orderby(NPR-31322)。

* 重复激活树是在从6.3 [!DNL Experience Manager] 升级时创建的(NPR-31513)。

* 转发的请求不保留在sling身份验证过程中设置的响应头(NPR-30013)。

* 在选取器组件中搜索不起作用(NPR-31692)。

* 由于Apache POI和Apache Tika捆绑包的不 [!DNL Experience Manager Communities] 同版本，将ZIP文件附加到帖子时会显示错误(NPR-31018)。

* 捆绑 `org.apache.sling.distribution.api` 包隐藏在配置管理器中，因此对自定义捆绑包不可用(NPR-31720)。

### 项目 {#projects}

* 切换日历视图不起作用(NPR-31271)。

### Brand Portal {#assets-brand-portal-6530}

**产品增强功能**

* 中的资产来源补充 [!DNL Experience Manager Assets] 导入工作流将被修改为仅从中提取新创建的 [!DNL Brand Portal] 资 [!DNL Experience Manager]产，并跳过NEW文件夹中已存在的资产以避免复制(CQ-4278527)。

**修复**

* 在“资产来源补充”功能中创建新的“贡献”文件夹时显示错误图标(CQ-4282825)。
* 创建新的“贡献”文件夹时，“贡献”文件夹中不显示一个或多个子文件夹（NEW和SHARED）(CQ-4282424)。
* 如果用户在从结尾接收贡献文件夹中的新资 [!DNL Experience Manager] 源后 [!DNL Brand Portal] 尝试将贡献文件夹从重新发布到， [!DNL Brand Portal] 系统将引发异常(CQ-4279740)。
* 禁止在“贡献”文件夹（嵌套文件夹）内创建“贡献”文件夹，以避免复杂性(CQ-4278391)。
* 上传从列表导入的 [!DNL Brand Portal] 用户Admin Console（.csv文件）时，系统引发 [!DNL Experience Manager] 异常。 只有。csv文件中的“电子邮件”、“名字”和“姓氏”字段是必填字段(CQ-4278390)。

### 社区 {#communities-6530}

**修复**

* 社区管理员（组管理员／站点管理员）看不到管理组（打开／编辑／发布／删除组）的快速链接(NPR-31627)。
* 提交的博客不会显示，除非手动刷新／重新加载页面(NPR-31599)。
* “提及次数”功能使用的JCR查询区分大小写，返回结果需要太长时间(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar文件引发异常， `cq-social-translation` 6. [!DNL Experience Manager] 5 UberJar文件中缺少捆绑包(NPR-31186)。
* Jackson Databind库已更新至版本2.9.9.3以解决新的漏洞(NPR-30967)。
* 活动和通知标题不一致 (NPR-30941)。
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Lucene索引更新导致作者服务器速度减慢(NPR-31548)。

### 表单 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Experience Manager Forms]。 它们是通过单独的 Forms 附加组件包交付的。In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. 有关详细信息，请参 [阅在JEE上安装Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[Forms加载项和安装Experience ManagerForms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

#### Forms 附加组件包 {#forms-add-on-package-6530}

**自适应表单**

* 在本地化自适应表单时，字符串包含字典键(NPR-31110)。

**交互式通信**

* **将Jackson库升级到** 2.10.0(NPR-31549)后，MissingNode.toString()返回不准确的结果。

* 文本编辑器从从Microsoft Word中复制的文本中随机删除空格字符(NPR-31113)。

**通信管理**

* 将字母从LiveCycleES4SP1迁移到6.5时，字幕 [!DNL Experience Manager] 和工具提示不显示(NPR-31615)。

* **将字母另存为草稿时** ，不再显示支持文本流格式的错误消息(NPR-30463)。

**工作流**

* OSGi工作流由于CPU利用率为100%而失败(NPR-31233)。

**HTML5 表单**

* 在添加子表单的实例时，生成 XDP 表单的 HTML5 预览会显示闪烁 (NPR-30909)。

#### FormsJEE安装程序 {#forms-jee-installer-6530}

**表单 - 文档服务**

* 在。NET项目中使用MTOM的SOAP Web服务显示AssemblerServiceClient调用和HtmlToPDF2方法的异常(NPR-4281771)。

* 安全漏洞2012-5784和2014-3596与AXIS 1.4jar一起发现，并修复与 [AXIS1.4.1 jar一起提供](https://helpx.adobe.com/cn/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015)。

**Foundation JEE**

* 操作配置不加载调用Forms Workflow提交操作的进程名称(NPR-31478)。

### 包含的功能包 {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms对Oracle 18c的支持(NPR-29155)。

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0是一个重要版本，包含自2019年4月正式发布6.5以来发布的性能、稳定性、安全性以及 [!DNL Adobe Experience Manager] 关键客户修复和 **增强功能**。 它可安装在6. [!DNL Experience Manager] 5之上。

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.3。
* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target].
* 资产用户可以直观地搜索相似图像。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。请参阅[使用连接的资产](../assets/use-assets-across-connected-assets-instances.md)。

* 增强具有更多MIME类型的文档类型过滤器以支持多值选项。
* 引入了一个外部“重新处理”工作流以支持多种资源。
* 通过 [!DNL Dynamic Media] 使用默认资产过滤器进行复制，优化了性能。
* 恢复了 DMS7 的裁剪/旋转资产编辑选项。
* 在 VideoPlayer 中实施了加载时使视频静音的选项。
* 修复以确保 Asset UI 列视图仅显示特定租户的内容。
* 修复以允许搜索结果中反映样式可折叠项的更改。

### 资产 {#assets}

**产品增强功能**

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。适用于 CQ-4270245 的修补程序. 请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 用户可以搜索视觉上相似的图像。 [!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

**修复**

* 通过 ACP API 生成的 URL 和文件夹元数据中的资产路径未进行 URL 编码。GRANITE-26198：适用于 CQ-4271814 的修补程序
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989：适用于 CQ-4270467 的修补程序
* 触屏UI:在管理发布向导过程中，在发布请求主体中的页面之后添加引用，导致所有资产在页面后发布，呈现页面时，发布实例中的部分资产会丢失。 NPR-29985：适用于 CQ-4270724 的修补程序
* “取消关联资产”功能无法用于名称中包含特殊字符（成为 URI 编码的字符）的关联资产。NPR-30387：适用于 CQ-4274446 的修补程序
* 编辑内容片段时，使用错误的用户创建此版本。
* 在基于“租户”的系统上创建收藏集失败。NPR-30114：适用于 CQ-4272948 的修补程序
* Asset UI 列视图不遵循当前租户的 dam 根路径，而是访问所有租户的 dam 路径。NPR-30636：适用于 CQ-4275481 的修补程序
* 由于能够看到插入的图像，可通过受限的文件警告窗口实施跨站点脚本 (XSS) 攻击。NPR-30617：适用于 CQ-4270133 的修补程序
* 多租户：保存文件夹属性的租户会同时观察成功提示和错误消息，说明操作未成功，“无法编辑属性。 权限不足。”因此，让租户感到困惑。NPR-30545：适用于 CQ-4275333 的修补程序
* 资产选择器对话框不允许选择资产，因此无法使用相关源替换功能来更新源。NPR-30502：适用于 CQ-4275029 的修补程序
* [!UICONTROL DAM更新资产工作流] -在上传大型mp4文件时处于过时状态。 NPR-30480：适用于 CQ-4271352 的修补程序
* 由于有效负荷为空，“创建审核任务”功能不起作用，使所有后续与审核任务相关的操作失败。NPR-30468：适用于 CQ-4274263 的修补程序
* 通过 Datapower 实施的 Adobe 智能标记存在连接问题。NPR-30026：适用于 CQ-4269457 的修补程序
* 尝试打开左边栏上的筛选器时，Assets UI 列视图引发一个错误。NPR-30501：适用于 CQ-4273862 的修补程序
* 在“资产文件夹”的“已关闭的用户组”(CUG) 属性中添加从 LDAP 同步的组后，不会保存和检索组。NPR-30615：适用于 CQ-4274689 的修补程序
* 筛选搜索样式和方向字段不会将自动完成的值应用于搜索查询。NPR-30620：适用于 CQ-4275724 的修补程序
* 对于某些资产，名称中包含空格和“&amp;”字符的文件夹的资产共享链接显示为空白灰色卡片。NPR-30557：适用于 CQ-4270187 的修补程序
* 文件夹元数据架构表单不会自动检测数据类型，因此，在表单提交中没有创建相关的 TypeHint。NPR-30599：适用于 CQ-4275227 的修补程序
* DMS7 创作 UI 中的裁剪和旋转资产编辑选项被禁用。NPR-30118：适用于 CQ-4273221 的修补程序
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080、NPR-30492：适用于 CQ-4273651 的修补程序
* Adding the [!DNL Dynamic Media]–Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641：适用于 CQ-4275962 的修补程序
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490：适用于 CQ-4273614 的修补程序
* [!DNL Dynamic Media]:添加了默认过滤器，以排除资产被复制到发 [!DNL Experience Manager] 布节点。 NPR-30538：适用于 CQ-4274678 的修补程序
* 为多资源支持引入了一个外部“重新处理”工作流，以允许文件夹作为有效负载。工作流包含两个步骤 - 通过到下一步的元数据映射重新处理没有句柄的资产，并在单个 IPS 作业中将所有没有资产句柄的资产重新上传到 S7。For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489：适用于 CQ-4272903 的修补程序
* 正确的 CSV 擦除正确的 CSV 后，会上传一个错误的 CSV。适用于 CQ-4277694、CQ-4277814 的修补程序
* 特定于要删除的贡献文件夹的图标错误。适用于 CQ-4277580 的修补程序
* 在资产贡献选项卡的用户选取器中选择用户时，表中不显示用户的名称，并且属性页面的“删除用户”对话框中显示错误文本。适用于 CQ-4277875 的修补程序
* 无法在用户选取器中通过选择用户和单击添加操作将参与者添加到资产贡献文件夹。适用于 CQ-4277824、CQ-4278087 的修补程序
* 用户选取器中按小写用户名称搜索不起作用。适用于 CQ-4277958、CQ-4277930 的修补程序
* 非管理员可以在资产贡献文件的新文件夹中发布资产。适用于 CQ-4278200 的修补程序
* dam 用户（非管理员）无法选择将参与者添加到资产贡献文件夹。适用于 CQ-4278192 的修补程序
* “创建”按钮在资产贡献文件夹中可见。适用于 CQ-4277560 的修补程序
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. 适用于 CQ-4273864 的修补程序
* 如果用户的电子邮件 ID 为大写字母，则该用户无法签入以前签出的那些资产。适用于 CQ-4276575 的修补程序
* “删除”操作仅应用于选定的预设，如果执行该操作后屏幕自动刷新列表，则会显示已刷新的其他预设。适用于 CQ-4261461 的修补程序
* Configuring [!DNL Dynamic Media] Cloud Services in [!DNL Dynamic Media]–Hybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. 适用于 CQ-4249780 的修补程序
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. 适用于 CQ-4276763 的修补程序
* 搜索筛选器面板中错误地显示用户生成内容。适用于 CQ-4273875 的修补程序
* “查找近似项”选项不适用于 TIFF 图像。适用于 CQ-4278238 的修补程序
* 在 VideoPlayer 中实施了加载时使视频静音的选项。适用于 CQ-4266465 的修补程序
* 查看器- VideoViewer:poster=none在使用外部视频时工作不正确。 适用于 CQ-4265536 的修补程序
* 在 IE11 和 MS Edge 浏览器中播放视频期间显示“等待”图标。适用于 CQ-4251539 的修补程序
* 3.8 SDK和5.13查看器自述文件不会更新，并包含先前版本的信息。 适用于 CQ-4273737 的修补程序
* 即使在保存更改之前，也要对内容片段进行版本控制。NPR-30616：适用于 CQ-4273088 的修补程序
* 在缩略图进程中用 Asset#getMetadataValueFromJcr(String) 替换 Asset#getMetadata(String)。NPR-30491：适用于 CQ-4273067 的修补程序
* 上传 jpg 会导致每个资产显示消息的多个实例：“ReplicateOnModifyWorker 复制更新”，从而导致性能降低。
* 使用“提取存档”功能解压缩 zip 存档会导致标题中包含百分号 (%) 的文件夹出现问题。NPR-29990：适用于 CQ-4270467 的修补程序

### 站点 {#sites-6520}

* 如果LiveCopy继承中断，则Live Copy页面会显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数超过40，则只显示前40条记录。 Blueprint显示记录其余部分的空行(NPR-31182)。
* 文本组件的富文本编辑器(RTE)插件显示日语和韩语文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)意外地将内嵌字体大小应用于元素(NPR-31284)。
* 当用户关注左边栏字段并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容，而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径存储在组件节点而不是多字段节点中(NPR-30882)。
* API `ResponsiveGridExporter` 不返回接 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 口。 该 `com.day.cq.wcm.foundation.model.impl` 包被宣布为私人包(NPR-31398)。
* 当在非编辑器模式下(在“作者”模式下(不带前缀 `editor.html` 和 `wcmmode=disabled`，或在“发布者”中)打开包含某些体验片段的页面时，请求以HTTP状态错误代码500(NPR-30743)结束。

### WCM - 页面编辑器 {#wcm-page-editor-6520}

**产品增强功能**

* 增强具有更多MIME类型的文档类型过滤器以支持多值选项。 适用于 CQ-4270694 的修补程序

### 内容片段管理 {#content-fragment-management-6520}

* 内容片段模式 UI 使用的查询非常缓慢，最终会导致错误。适用于 CQ-4270807 的修补程序

### UI - Foundation {#ui-foundation}

* 快捷方式触发器阻止用户在特定用户界面中使用“m”、“p”、“e”。NPR-30355：适用于 GRANITE-26346 的修补程序
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509：适用于 CQ-4274716 的修补程序
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104：适用于 GRANITE-26344 的修补程序

### 翻译 {#translation-6520}

* 翻译问题 - 只有少数组件使用机器翻译进行了翻译。NPR-30079：适用于 CQ-4273764 的修补程序

### 平台 {#platform-6520}

* [!DNL Experience Manager] 默认邮件发送程序无法通过 TLS v1.2 向远程 SMTP 服务器发送电子邮件。NPR-30476：适用于 GRANITE-26605 的修补程序

### 项目 {#projects-6520}

* dam:folderThumbnailPaths 值未刷新，并且在删除文件夹内的资产后，还显示旧版缩略图。NPR-30424：适用于 CQ-4273667 的修补程序
* 完成“移动”选项后，资产的“标题”和“名称”保持不变。NPR-30647：适用于 CQ-4276265 的修补程序

### 社区 {#communities-6520}

* “用户同步诊断”完全中断，无法工作。NPR-30004、NPR-29943：适用于 CQ-4270287、CQ-4271348 的修补程序

### Sling {#sling}

* 从 6.3.3.2 升级到 6.5 的实例导致 OSGi 配置重复。NPR-30130：适用于 CQ-4274016 的修补程序

### 集成 {#integration}

* 重新启动实例之前，发布实例上显示的自定义内容错误。NPR-30377：适用于 CQ-4273706 的修补程序
* 在网站中配置 Launch 时，库地址前面带有斜线 (\)，导致每次需要手动干预。NPR-30694：适用于 CQ-4275501 的修补程序

### 表单 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Experience Manager Forms]。 They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. 有关详细信息，请参 [阅在JEE上安装Experience Manager](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)[Forms加载项和安装Experience ManagerForms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)。

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Forms 附加组件包 {#forms-add-on-package}

**后端集成**

* 无法使用 AWS 托管的负载平衡 URL 来配置“表单数据模型”。NPR-30123：适用于 CQ-4273359 的修补程序
* 使用Web服务定义语言(WSDL)创建表单数据模型(FDM)时，返回错误 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 消息：NPR-30477:CQ-4272921的修补程序

**通信管理**

* “创建对应UI(CCR UI)再现间歇性失败，控制台中出现以下错误：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**交互式通信**

* 表单数据模型中标记为必填的字段将按“创建通信 UI”(CCR UI) 中的要求显示。NPR-30623：适用于 CQ-4274902 的修补程序

**表单 - 工作流**

* “监视文件夹”中未映射的输出变量导致调用失败。适用于 CQ-4264451 的修补程序

**HTML5 表单**

* 第二次部署自定义代码或项目时，页面不呈现，并出现以下错误：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：适用于 CQ-4272509 的修补程序

* 在浏览模式下使用 NonVisual Desktop Access 读取 HTML5 表单时，Chrome 浏览器会读取表单设计中每个可缩放矢量图形 (SVG) 前的“图形”。NPR-30449：适用于 CQ-4274732 的修补程序

#### Forms JEE 安装程序 {#forms-jee-installer}

**表单 - 文档安全**

* 应用带有时间戳的签名失败，并出现错误：ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 调用错误。NPR-30820：适用于 CQ-4275852 的修补程序

**表单 - 文档服务**

* 如果“SubmitURL”包含与号 (＆)，则在对 renderpdf servlet 发出 POST 请求时，日志中会出现解析错误。NPR-30865：适用于 CQ-4278232 的修补程序

**Forms - Foundation JEE**

* HTMLtoPDF服务在JMX控制台中不显示maxReuseCount。 NPR-30134、NPR-30304：适用于 CQ-4273763 的修补程序
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105：适用于 CQ-4273217 的修补程序

### 包含的功能包 {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### 站点 {#sites-feature-packs-included}

* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target]. NPR-29189：适用于 CQ-4249782 的修补程序

#### 表单 - 文档服务 {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759：适用于 CQ-4278193 的修补程序

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是一个重要版本，包含自2019年4月正式发布6.5以来发布的性能、稳定性、安全 [!DNL Adobe Experience Manager] 性以及重要客户修 *复和增强。* 它可安装在6. [!DNL Experience Manager] 5之上。

该 Service Pack 的一些重要功能亮点包括：

* 支持在跟踪事件中包含动态 UI 状态作为自定义属性。
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 资产

* 针对 S3 多部分支持更新了 DAM DMGateway 接口。NPR-29740：适用于 CQ-4226303 的修补程序
* 再现预览 `Only empty tenantId is currently supported` 在升级到6.5 [!DNL Experience Manager] 后生成错误。NPR-29986:CQ-4272353的修补程序
* “删除”对话框不可见，因此不允许删除作业。NPR-29720：适用于 CQ-4271074 的修补程序
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627：适用于 CQ-4264929 的修补程序
* VersioningTimelineEventProvider 应该提供 root 版本以及 nt：version 类型的节点。适用于 GRANITE-26063 的修补程序
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. 适用于 CQ-4265131 的修补程序
* 如果编辑了源，则 Live Copy 检索错误的状态。适用于 CQ-4265451 的修补程序
* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. 适用于 CQ-4271453、CQ-4268621、CQ-4257491 的修补程序
* [!DNL Experience Manager] 界面应在时间轴历史记录中显示资产当前版本的额外条目，显示最新的登记注释 [!DNL Adobe Asset Link]。 适用于 CQ-4262864 的修补程序
* 内容片段时间轴在属性缺失时显示错误消息。 适用于 CQ-4272560 的修补程序
* 扩展到全屏时，Scene 7 视频播放器出现问题。适用于 CQ-4266700 的修补程序
* ZoomVerticalViewer：使用单个图像资产时不应显示“全景”按钮。适用于 CQ-4264795 的修补程序
* 删除 Live Copy 中的儿童模式时应分离 liveRelationship。适用于 CQ-4270395 的修补程序
* 元数据架构仅包含来自全局配置的项目，丢失了来自活跃租户的项目。即使在更改之后，formPath URL 值也会恢复为默认值。NPR-29945：适用于 CQ-4262898 的修补程序
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510：适用于 CQ-4268659 的修补程序

### 站点

* 在转出期间，不会从 Blueprint 传播空属性和多属性。使用 Blueprint 重置 Live Copy 不适用于组件。NPR-29253：适用于 CQ-4264928、CQ-4264926、CQ-4267722 的修补程序
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537：适用于 CQ-4266129 的修补程序
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785：适用于 CQ-4265090 的修补程序
* 使用时间扭曲恢复的页面在版本控制时应该引用正确的图片。NPR-29431：适用于 CQ-4262638 的修补程序
* 样式系统节点从父节点继承到子节点的问题。 NPR-29516：适用于 CQ-4270330 的修补程序
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211：适用于 CQ-4266630 的修补程序
* “内容片段”上呈现的缩略图使用内部日历来表示“日期和时间”字段。NPR-29531：适用于 CQ-4269362 的修补程序
* 在 Coral2 实施中打开权限选项卡时不显示按钮。适用于 CQ-4269419 的修补程序

### 商务

* 为电子商务运行延迟内容迁移时引发 ConstraintViolationException。NPR-29247：适用于 CQ-4264383 的修补程序

### 内容片段管理

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. 适用于 CQ-4270266 的修补程序

### 体验片段

* 将体 [!DNL Experience Manager] 验片段导出 [!DNL Adobe Target]到。 适用于 CQ-4265469 的修补程序
* 智能图像无法将体验片段导出到目标。 适用于 CQ-4269606 的修补程序

* 在卡片视图中尝试通过 Omnisearch 移动“体验片段”时，用户会陷入僵局。适用于 CQ-4263848 的修补程序

### WCM - 页面编辑器

* 使用无效选择器时导致反射型跨站点脚本攻击 (XSS)。适用于 CQ-4270397 的修补程序

### 复制

* 用户提供的数据不会在 `cq/replication/components/agent` 组件的输出中进行转义，从而导致存储型跨站点脚本 (XSS) 漏洞。适用于 CQ-4266263 的修补程序

### 工作流

* 对话框参与者的日历选取器字段损坏。NPR-29727：适用于 CQ-4270423 的修补程序

### WCM - SPA 编辑器

* 已启用从远程端点获取预渲染的内容。适用于 CQ-4270238 的修补程序
* 打开呈现在服务器端的 SPA 模板页面时在日志中出现警告。适用于 CQ-4270238 的修补程序

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. 适用于 CQ-4271410 的修补程序

### 集成

* BrightEdge 凭证失败，出现连接错误。NPR-29168：适用于 CQ-4265872 的修补程序

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176：适用于 CQ-4265782/CQ-4266153 的修补程序

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

* Session leak during OAuth for every replication to [!DNL Brand Portal]. NPR-30001：适用于 GRANITE-26196 的修补程序

### 项目

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819：适用于 CQ-4271118 的修补程序

### 平台

* HtmlLibraryManager 在缓存失效时删除 crx-quickstart 的所有内容。NPR-29863：适用于 GRANITE-26197 的修补程序

### Felix

* 使用Java11时，内存使用情况详细信息不会显示在系统控制台中。 NPR-29669

### 表单

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* 仅限OSGI:支持使用Forms服务创建静态PDF文件。
* 为管理员和根用户启用了对 XMLForm.exe 的权限。
* 为 Dynamics 内部部署集成启用了对 ADFS v3.0 的支持。

#### Forms 附加组件包

**后端集成**

* 获取受保护的 Web 服务定义语言 (WSDL) 失败。NPR-29944：适用于 CQ-4270777 的修补程序
* When [!DNL Experience Manager Forms] is installed on IBM WebSphere, creating a form data model based on SOAP fails. 适用于 CQ-4251134 的修补程序
* 为 Microsoft Dynamics 内部部署集成启用了对 Active Directory 联合身份验证服务 (ADFS) v3.0 的支持。适用于 CQ-4270586 的修补程序
* 数据源的标题发生更改时，表单数据模型不显示更新的标题。适用于 CQ-4265599 的修补程序
* 如果实体或属性的名称包含连字符或空格，则表达式无法评估此类实体和属性。 适用于 CQ-4225129 的修补程序

* 在基元字符串输出中存在冒号时，会观察到错误的输出。 适用于 CQ-4260825 的修补程序

* 即使 REST API 输出中没有任何内容，表单数据模型的调用操作也会引发错误。适用于 CQ-4268828 的修补程序

**自适应表单**

* 在延迟加载期间，无法在“自适应表单片段”中添加新实例。NPR-29818：适用于 CQ-4269875 的修补程序
* 验证组件没有记录或显示“记录文档”模板的任何错误。适用于 CQ-4272999 的修补程序
* 添加了对“自适应表单”禁用布局编辑器的支持。适用于 CQ-4270810 的修补程序
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. 适用于 CQ-4269463 的修补程序
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. 适用于 CQ-4264414、CQ-4264914 的修补程序

* Adaptive Forms应用程序与大数据集一起使用时的性能问题。. 适用于 CQ-4235310 的修补程序

* 通过匿名帐户在发布实例上进行访问时，GuideRuntime 脚本加载失败。适用于 CQ-4268679 的修补程序

**表单 - 交互式通信**

* “交互式通信”模板未在允许的组件列表中列出页眉和页脚组件。适用于 CQ-4237895 的修补程序
* 创建包含图像字段的交互式通信打印模板时，图表标题将设置为空白。适用于 CQ-4264772 的修补程序
* 图表的线条颜色在删除后设置为未定义。适用于 CQ-4264762 的修补程序
* 在执行保持更改同步时，文档片段上的布局图层更改会消失。 适用于 CQ-4266054 的修补程序
* “文档片段”中绑定到文本字段的表单数据模型元素不显示继承图标，并且允许绑定。适用于 CQ-4261089 的修补程序
* “打印渠道”呈现 API 没有在 API 中作为参数传递数据的选项。适用于 CQ-4263540 的修补程序
* 当绑定类型从文本片段更改为字符串字段／变量的无／数据模型对象时，代理设置不可见，因为“由代理编辑”复选框变为未选中。 适用于 CQ-4261953 的修补程序
* 提交代理UI时，生成的web数据json文件会存储继承取消未绑定字段的信息。 适用于 CQ-4265621 的修补程序

**表单 - 工作流**

* 从自适应表单应用程序的发件箱重新提交表单时，将导致数据丢失。NPR-28345：适用于 CQ-4260929 的修补程序
* 对于不可变情况，保存时不会关闭文档。适用于 CQ-4269784 的修补程序
* “自适应表单”应用程序取消了对 Microsoft Windows 8.1 的支持。适用于 CQ-4265274 的修补程序。
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. 适用于 CQ-4265578 的修补程序

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

* [!DNL Experience Manager Forms] 6.5创建通信UI(CCR UI)无法打开使用6.3创 [!DNL Experience Manager Forms] 建的通信。CQ-4266392的修补程序
* 如果 DDE 数据类型是数字类型，则 XDP 中的求和功能将不起作用。适用于 CQ-4227403 的修补程序
* 内存中的字母缓存失效逻辑将被更新，因为当资产发布时，其最后修改时间不会更新。适用于 CQ-4250465 的修补程序
* 无法发布文档片段、DD 和 Letters。适用于 CQ-4272893 的修补程序

#### Forms JEE 安装程序

**PDF 生成器**

* 使用 64 位 JDK 时，将 CAD 文件转换为 PDF 失败。NPR-29924、NPR-29925：适用于 CQ-4272113 的修补程序
* 将 PhantomJS 的名称替换为 WebToPDF 以进行 HTMLtoPDF 转换。NPR-29933：适用于 CQ-4234545 的修补程序
* 将 zip 文件转换为 PDF 时出现错误。适用于 CQ-4268628 的修补程序

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. 适用于 CQ-4272923、CQ-4271002 的修补程序

**表单 - 文档安全**

* 带硬件安全模块(HSM)的数字签名在Java 11和Java 8的OSGi Linux上不工作。 NPR-29838：适用于 CQ-4270441 的修补程序
* 带硬件安全模块 (HSM) 的数字签名在 JEE Linux 上，以及所有受支持的应用程序（例如，JBoss 和 Websphere）上不起作用。NPR-29839：适用于 CQ-4266721 的修补程序
* 在 PDF 中使用“PDF 高级电子签名”(PAdES) 验证签名会生成 InvalidOperationException。NPR-29842：适用于 CQ-4244837 的修补程序
* 增加了对Office 2019的文档安全扩展支持\。 适用于 CQ-4254369、CQ-4259764 的修补程序

**表单 - 文档服务**

* “表单”字段无法转换为PDF/A-1b，没有外观命令。 NPR-29940：适用于 CQ-4269618 的修补程序

* OSGi:无法确定渲染过程中生成的页数。 NPR-28922：适用于 CQ-4270870 的修补程序
* 使用中的Forms服务支持静态PDF文 [!DNL Experience Manager Forms OSGi]件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 无法更改对 XMLForm.exe 的权限。NPR-29828、NPR-29237：适用于 Q-4267080 的修补程序
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332：适用于 CQ-4271002 的修补程序

**Forms - Foundation JEE**

* 最终部件中不可用的 pdfg_srt 会导致安装程序失败。NPR-29854：适用于 CQ-4270137 的修补程序
* LCBackupMode.sh 不起作用。NPR-29840：适用于 CQ-4269424 的修补程序
* UDP 端口引用应该从 WebSphere 的用户界面 (UI) 中删除。适用于 CQ-4264782 的修补程序

### 包含的功能包

#### 资产——已包含

* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199：适用于 CQ-4259922 的修补程序

#### 站点——包括

* 将体 [!DNL Experience Manager] 验片段导出 [!DNL Adobe Target]到。 For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). 适用于 CQ-4265469 的修补程序

#### Forms - 文档服务 -包括

* 仅限OSGi:在“输出”和“Forms服务”中添加了新属性PAGECOUNT。 NPR-28922：适用于 CQ-4270870 的修补程序
* 仅限OSGi:支持使用Forms服务创建静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 为管理员和根用户启用了对 XMLForm.exe 的权限。NPR-29237：适用于 CQ-4267080 的修补程序

### OSGi 包和内容包

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-content-package-list.txt)
