---
title: AEM 6.5 Service Pack 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Service Pack 5。
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 11%

---


# Adobe Experience Manager 6.5 Service Pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | **Adobe Experience Manager 6.5** |
|---|---|
| 版本 | 6.5.5.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2020年6月4日 |
| 下载 URL | [包共享](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0)，软 [件分发 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Adobe Experience Manager 6.5.5.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0是一项重要更新，包含自2019年4月6.5版正式发布以来发布的新功能、关键客户请求的增强功能以及性能、稳定性、安 **全性改进**。 它可以安装在Adobe Experience Manager(AEM)6.5的顶部。

AEM 6.5.5.0中引入的一些主要功能和增强功能包括：

* 自定义在AEM收件箱中显示的列名。

* 改进AEM Web内容管理(WCM)中各个区域（如页面编辑器、核心组件、RTE和管理员用户界面）的辅助功能。

* 将交互式通信另存为草稿。

* 在JEE上 [!DNL Oracle WebLogic 12] 支持AEM Forms。

* 现在，资产用户界面流中 [!DNL Adobe Experience Manager] 的异常处理得到改进。

* 在界面中 `getRemoteAssetPublishURL` 添加了一 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 种新方法，以获取Dynamic Media Scene7的发布URL。

* [资源中的辅](#assets-6550-changes) 助功 [!DNL Adobe Experience Manager] 能增强功能符合Web内容辅助功能准则(WCAG)。

* 删除了与Adobe Experience Manager的包共享集成。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.3。

有关AEM 6.5 Service Pack 5中引入的功能、主要重点和主要功能的完整列表，请 [参阅Adobe Experience Manager 6.5 Service Pack 5的新增功能](new-features-latest-service-pack.md) 。

以下是6.5.5.0版中提 [!DNL Experience Manager] 供的修复列表。

### 站点 {#sites-6550}

* AEM Sites提供了一个选项，用于发布或取消发布别名中的页面。 此选项无效(NPR-33415)。
* 从包含多个模板的模板中删除布局容器时，该模板无法正确呈现(NPR-33347)。
* 当AEM站点页面是包含多个Live Copy的大型内容集的一部分时，无法加载页面版本历史记录预览(NPR-33311)。
* 使用“移动”命令重命名AEM站点页面时，页面标题不会更新(NPR-33264)。
* 在列视图中移动页面时，列会消失(NPR-33216)。
* 当语言副本中的本地组件名称与蓝图中的组件名称相同且从蓝图中转出该组件时，术语_msm_moved不会添加到本地组件的名称(NPR-33208)。
* 页面重定向servlet将。html附加到ResourceType不为cq:Page的AEM站点URL(NPR-33176)。
* 粘贴子树时，没有选项可决定是否粘贴相应的子页面(NPR-33149)。
* 组件在实时使用中的结果数限于数字49(NPR-33058)。
* 当您将内容片段基于模式并且它包含强制文本区域或路径字段时，内容片段无法保存(NPR-33007)。
* 当您使用现成的体验片段组件创建自定义组件并在AEM站点页面中使用它时，AEM不显示自定义组件的引用（用法）(NPR-32852)。
* 重命名具有大量引用的文件夹时，不会更新对该文件夹的许多引用(NPR-32765)。
* 启用源代码编辑选项后，该选项对内联全屏选项可用，但富文本编辑器的编辑对话框和全屏选项仍缺失(NPR-32763)。
* 如果您有多个字段，并且它在蓝图的页面属性中包含必填字段（如下拉列表或路径字段），则当转出包含此类多字段的页面时，不会保存Live Copy的页面属性。 (NPR-32751)
* 屏幕阅读器无法使用标题结构来导航页面。 此外，“组件”选项卡的标签错误(NPR-32648)。
* 分页开始时，体验片段选取器不加载所有项目(NPR-32605)。
* 撤消读取、修改、创建和删除Live Copy的创作权限。 每个作者都必须明确提供读取和修改权限才能在Blueprint中移动页面(NPR-32550)。
* 内容作者无法为与Adobe Analytics集成的页面创建Launch(NPR-32548)。
* 当用户通过同步恢复继承时，父页面的Live Copy不会与Blueprint同步，并显示不正确的状态(NPR-32500)。
* 加载AEM Sites编辑器页面需要超过15秒(NPR-32413)。
* 某些字段不显示“取消继承”选项(NPR-32362)。
* 当您为体验片段组件选择路径并选中打开选择对话框复选框时，您不会导航到路径浏览器中的选定路径(NPR-32308)。
* 从AEM 6.2升级到AEM 6.5时，静态模板的Parsys组件无法正确显示。 Parsys组件的高度设置为0，其中的组件不可见。 (NPR-33663).
* 当用户复制并粘贴同一页面上的布局容器时，布局容器中的组件不会显示(NPR-33648)。
* 调度程序运行状况 `Invalid cookie header` 检查在日志文件中显示警告消息(NPR-33629)。

### 资产 {#assets-6550-changes}

**Experience Manager Assets中的辅助功能增强**

* 现在，可以将键盘焦点放在“注 [!UICONTROL 释] ”列表上，并可单击选项 [!UICONTROL 在“时间轴Npr资产”面板中“] 创建新版本”下 [!UICONTROL 创建版本注释(] NPR-33424)。

* 现在可以使用键盘 [!UICONTROL 键访问资源的] “视图设置”选项 [!UICONTROL 并更改“视图设] 置”对话框中的设置(NPR-33420)。

* 组合框的列表框下拉框（在不同页面的各个字段中）现在将条目显示为列表选项，屏幕阅读器可以宣布这些选项(NPR-33516)。

* 可排序标题(在列表视图、 [!UICONTROL 时间轴] 视图和管理发 [!UICONTROL 布页面中] )的排序功能现在由屏幕阅读器宣布，并且列标题的排序控件可通过键盘访问(NPR-32979)。

* 可单击的元素（如注释卡、版本更新、组合框和菜单的V形图标）现在可以使用键盘(NPR-33514)进行聚焦和操作。

* 屏幕阅读器现在可以正确地宣布“洞察”视图上 [!UICONTROL 的洞察图标] （用于使用、展示和点击）的功能（或操作目的）(NPR-33513)。

* 只读表单字段(例如，资产属性 [!UICONTROL “基本] ”选项卡 [!UICONTROL 上禁用的字段])现在可使用键盘(NPR-33493、CQ-4273031)进行聚焦。

* 各种输入字段中的标签现在是永久标签（因此可访问），而不仅仅是占位符标签，在输入文本时它们会消失(NPR-33475)。

* 不同的标题级别（如页面标题和章节标题）对屏幕阅读器用户来说现在被视为具有不同级别的标题(NPR-33471)。

* 现在可使用键盘访问交互式用户界面元素，如链接和选项（资产页面的标题和缩放选项、文件夹导航）(NPR-33468、CQ-4271412)。

* 管理 [!UICONTROL 出版物]页面 [!UICONTROL 上的选项、范围和]工作流进度指 [!UICONTROL 示符现在由屏幕阅读器正确读] 出，作为进度指示符，而不是选项卡(NPR-33416)。

* 星级图标的颜色(如资产属 [!UICONTROL 性中Advanced][!UICONTROL （高级）选项卡的] “评级”部分或卡视图中  )会更改，以使视觉受限且无颜色感知的用户能够看到相应的对比度(NPR-33414)。

* 现在，可使用键 [!UICONTROL 盘键] (NPR-33397)访问资产详细信息页面上“注释”字段旁的V形向上箭头。

* 现在，屏幕阅读器 [!UICONTROL 正确宣] 布了 [!UICONTROL “资产属性”和“左边栏导航] ”（在资产用户界面上）上的“标记”对话框的展开和折叠状态(NPR-33396)。

* 资产上所有已浏览页面 [!DNL Adobe Experience Manager] 的标题现在是唯一的(NPR-33343)。

* 当导航树结构时，屏幕阅读器现在可以正确地宣布树视图控件的各个元素(NPR-33304)。

* 现在可使用键盘 [!UICONTROL 键访问] “资产详细信息”页上“时间轴”视图下的不同版本的资产(NPR-33283)。

* 使用搜索功能时，屏幕阅读器现在会公布显示在Omnisearch组合框中的搜索建议的名称(NPR-33280)。

* “引用”边 [!UICONTROL 栏中的可单] 击元素和 [!UICONTROL “转到”] 链接现在由屏幕阅读器宣布为可单击元素(NPR-33278)。

* 屏幕阅读器在打开“共享链接”对话框时不再 [!UICONTROL 公布] “共享链接”对话框的表结构信息（如行1、单元格1、表）(NPR-33268)。

* 各种组合框元素（如“路径”字段以及在资产属性的“基本”选项卡中打开“选择”对话框的选项）的用途现在由屏幕阅读器正确宣布(NPR-33235)。

* 现在，当列表视图表中的行处于键盘焦点时，会向屏幕阅读器用户传达这些行可选择的信息。 当鼠标悬停在行上时，会宣布此信息(NPR-33234)。

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

   * 在浏览模式下，屏幕阅读器的焦点不再移到“站点引用”、“资产引用”、 [!UICONTROL “副本]”和“表单引用 [!UICONTROL ”部分下]，隐藏的多行  编辑字段中。

   * 屏幕阅读器现在宣布“站点引 [!UICONTROL 用”和] “语 [!UICONTROL 言副本”元素的角色] 。

   * 浏览模式下屏幕阅读器的焦点以有意义的顺序转移到各种元素。

* [!UICONTROL 元数据模式] “编辑器”页面及其元素现在可使用键盘访问，并且屏幕阅读器友好(CQ-4290962、CQ-4272953)。

* 该选项 [!UICONTROL 上] x图标用于删除当前选定标记的用途以及选定标记的数量(CQ-4273017)。

* 屏幕阅读器现在忽略装饰性图标和图像，以避免使用屏幕阅读器的失明用户产生混淆(CQ-4272944)。

**Experience Manager资产中修复的问题**

[!DNL Adobe Experience Manager] 6.5.5.0资产修复了以下问题：

* [!UICONTROL 开始][!UICONTROL ，会禁] 用集合中资产的“创建工作流”对话框上的“创建工作流”选项，从而阻止触发工作流(NPR-32471)。

* 在元数据模式中使用级联下拉框时，选择并保存包含撇号（从子项下拉框中）的下拉选项时，在重新打开资产属性(NPR- [!UICONTROL 32649] )后，选定撇号选项会消失。

* [!UICONTROL 如果Asset Insights Sync] Job遇到无效条目（在Analytics端）而不是转到下一个条目(NPR-32674)，则停止并失败。

* 陀螺仪无法正常工作，因为在全景查看器中，默认情况下在移动浏览器上禁用运动传感器(CQ-4272937)。

* [!UICONTROL 在6.5] .1上安装6.5.3时，连接的资产配置向导无法处理404错误(NPR-32730)。

* 在XMP写回过程中，所有自定义命名空间元数据属性都将自定义命名空间前缀更改为ns2，而不是配置的命名空间前缀(NPR-32748)。

* 不会触发延迟加载，选择从通知收件箱中查看任务时只显示100个资源(NPR-32750)。

* `NullPointerException` 由于新创建的用户用户档案(SAML/SSO)中缺少节点首选项而观察到。 此错误会阻止新登录的用户 [!DNL Adobe Experience Manager Stock] 使用集成(NPR-32777)。

* 在打开包含超过10,000个资源的智能集合时，会在日志中观察到遍历警告(NPR-32980)。

* 使用Dynamic Media Scene7运行模式时，将资产从一个文件夹移 [!DNL Adobe Experience Manager] 动到另一个文件夹时，资产名称将更改为小写(NPR-32995)。

* 在从搜索结果导航到其属性，然后返回搜索结果删除该资产后，无法删除已搜索的资产(NPR-32998)。

* [!UICONTROL 在“移动] 资产”界面中选择目标文件 [!UICONTROL 夹时] ,“下一步”选项仍处于禁用状态(NPR-33356)。

* [!UICONTROL 在选择父] 节点（其中显示单个子文件夹），然后选择子文件夹时，未启用“下一步”选项(NPR-33275)。

* 对于具有删除权限的用户，Adobe资产链接(AAL)上禁用登记和注销权限，即使允许他们使用其他权限（如读取、创建或修改）(NPR-33272)。

* 智能裁剪演绎版在资产下载对话框中不可用(NPR-33167)。

* 在具有智能裁剪用户档案的文件夹下打开PDF的演绎版边栏的日志中会出现异常(CQ-4294201)。

* 如果在具有Dynamic Media Scene7运 [!UICONTROL 行模式的AEM] 上默认禁用了Dynamic Media同步模式，则不发布图像预设(CQ-4294200)。

* 批量上传时的资产处理会卡住，而工作流实例会显示DAM更新资产的卡住实例(CQ-4293916)。

* 在AEM上创建Dynamic Media配置是有效的，但在用户界面上，选择保存时不会发生任何情况(CQ-4292442)。

* f4v视频资源的预览在Safari/Mac上的渐进式播放中不工作(CQ-4289844)。

* 在智能裁剪父级文件夹内的资产时会创建额外的文件夹，其 `.` 名称中带有点字符(CQ-4289337)。

* 缩览图已断开，复制视频时不会显示视频处理横幅(CQ-4284125)。

* 对于某些型号的相机视图为空的型号，尺寸查看器在Firefox中错误地显示了空缩览图(CQ-4283447)。

* 6.5.5.0中修复的性能问题包括(CQ-4279206):

   * 将大型二进制文件上传到Dynamic Media图像处理服务器需要太长的时间。

   * 由于Dynamic Media Scene7体系结构，AEM上的缩略图生成时间增加。

* 对于拥有大量资产的客户，Dynamic Media Scene7迁移问题失败(CQ-4279206)。

* 如果使用视频360查看器， `setVideo` 则其布局会被破坏，并且视频在使用 `video= modifier` 时会下移(CQ-4263201)。

* 安装AEM SDL包时显示错误消息(NPR-33175)。

### 平台 {#platform-6550}

* 如果 [!DNL Sling] 在(NPR-33362)下 `sling:match` 创建了映射条目， `/etc/maps` 则不调用该过滤器。
* AEM因分段故障而崩溃( [!DNL Apache Lucene] NPR-32988)。
* [!DNL Jackson] AEM uber jar文件中缺少核心包(NPR-32848)。
* CRXDE Lite不为没有节点属性READ权限的 `jcr:primaryType` 用户加载内容(NPR-32611)。
* [!DNL Granite] 维护任务调度程序在AEM部署期间重新初始化过频繁(CQ-4294627)。
* 当SQL查询运行时间较长（例如7小时）时，AEM停止响应(NPR-33044)。

### 用户界面 {#ui-6550}

* 多字段中不保留单选按钮选择(NPR-33309)。
* 延迟加载限制对列表视图无效(NPR-33124)。
* 如果没有匹配项，搜索结果页面不显示消息(NPR-32974)。
* Omnisearch过滤器将忽略所 `/content` 选位置(NPR-32849)返回节点下的所有匹配项。

### 集成 {#integrations-6550}

* 当发布包含Adobe目标组件的页面时，会清除内部缓存(NPR-33162)。
* 与Adobe目标的集成在11上 [!DNL Windows Internet Explorer] 不起作用(NPR-33111)。
* 配置Adobe目标时， [!UICONTROL 公司] 和报告  包字段在选择报告源时不显示(NPR-32502)。
* 使用Adobe I/O导出体验片段时，源产品等元数据不会导出到Adobe目标(NPR-32159)。
* 本地AEM管理员组中的授权IMS用户无法创建或修改IMS配置(NPR-33045)。
* Adobe Launch配置页面不显示所有记录(NPR-33011)。
* 由于JavaScript错误(NPR-32996)，内容作者组中的用户无法编辑Adobe目标组件的属性。

### 翻译项目 {#translation-6550}

* 译文标记不会从第三方翻译服务(NPR-33154)导入到AEM中。
* 翻译配置页面显示的翻译提供程序与用于翻译的翻译提供程序不同(NPR-32971)。
* 将体验片段文件夹添加到现有翻译项目会创建新项目(NPR-32843)。
* 运 `NullPointerException` 行转换作业的日志中显示错误(NPR-32628)。

### WCM {#wcm-6550}

* 页面编辑器 [!DNL Sites] -页面编辑器不允许仅使用键盘的用户跳到主内容，而不是通过标题中的所有可用选项来切换选项卡焦点(CQ-4293883)。
* 页面编辑器——由于版本和版本中的更新，使用Well组件并包含已保存数据的面 [!DNL Chrome] 板不 [!DNL Firefox] 会显示(CQ-4292995)。
* MSM —— 从页面中删除组件不会从页面的已发布版本中删除组件(CQ-4292360)。

### Brand Portal {#assets-brand-portal-6550}

* 从中删除已发布的元数 [!DNL Brand Portal] 据模式会导致错误(CQ-4292063)。
* 如果管理员通 [!DNL Experience Manager Assets] 过Adobe Developer Console使用Brand Portal配置6.5.4, [!DNL Brand Portal] 则用户无法从发布到发布贡献文件夹的 [!DNL Brand Portal] 资产 [!DNL Experience Manager]。 (NPR-33046).
* 重复复制父文件夹会导致冲突(NPR-33001)。

### 社区 {#communities-6550}

* 无法使用快速编辑菜单选项删除审核控制台中的卡(NPR-33117)。
* 访问活动流页 [!UICONTROL 面时出错] (NPR-33146)。
* 在作者实例上删除的组不会从所有发布实例中删除(NPR-33199)。
* 创建新组后，作者不会被重定向到 [!UICONTROL 第11号] “社区 [!DNL Internet Explorer] 组”部分(NPR-33205)。
* 在AEM收件箱中访问邮件不会将邮件的状态更改为“已读”(NPR-32764)。
* 编辑 [!DNL Communities] 组和更改缩略图图像不会更新组缩略图图像(NPR-32599)。
* 用户无法向社区中的其他用户发送电子邮件(NPR-32598)。
* 提交的博客在用户刷新页面之前不会显示(NPR-32391)。
* 创建通知版本和用户生成内容订阅(UGC)时，会存储源页面的错误ID(CQ-4279355、CQ-4289703)。

### 工作流 {#workflow-6550}

* 加 [!UICONTROL 载左边栏] 中的“时间轴”选项比预期花费的时间要多(NPR-32851)。
* 重新启动AEM实例后，集合的审阅任务的电子邮件包含不正确的有效负荷链接(NPR-32774)。

### 表单 {#forms-6550}

>[!NOTE]
>
>AEM Service Pack 不包含对 AEM Forms 的修复。它们是通过单独的 Forms 附加组件包交付的。此外，还会发布一个包含AEM Forms在JEE上的修复的累积安装程序。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* 通信管理： 在目标区的资产顺序在提交信件(NPR-33359、NPR-33153)后混乱。
* 自适应表单： 当用户编辑自适应表单时，“页 [!UICONTROL 面信息] ”菜单中可 [!UICONTROL 用的“开始工] 作流”选项将不起作用(NPR-33004)。
* 自适应表单： 用户无法保存包含多个附件的自适应表单(NPR-32997)。
* 自适应表单： 在自适应表单中更改面板布局会导致错误(CQ-4293880)。
* 自适应表单： 自适应表单词典中字符串的新行将字 `&#xa;` 符添加到词典(NPR-33266)。
* 自适应表单辅助功能： 当用户将自适应表单预览为HTML表单时，“ [!UICONTROL 涂写签名] ”字段无法保留制表符焦点(NPR-33159)。
* 自适应表单辅助功能： 提交自适应表单时显示的错误消息不链 `aria-describedBy` 接到属性(NPR-33071)。
* 自适应表单辅助功能： 在自适应表单中标记为必填的字段没有在ARIA辅助功能模式中将必填属性设置为True(NPR-33070)。
* PDFG服务： 当用户将文本文件转换为PDF时，日文字符无法正确呈现(NPR-33238)。
* PDFG服务： `CreatePDF` 操作无法将PDF文件转换为PDF OCR格式(NPR-32994)。
* PDFG服务： 第200个文档实例的PDF转换 [!DNL OpenOffice] 失败(NPR-32766)。
* 后端集成： 表单数据模型请求失败，因为由于不正确的非活动状态，刷新令牌过期(NPR-33169)。
* 设计人员： 屏幕阅读器根据默认的地理顺序而不是XDP文件中定义的自定义Tab键顺序(NPR-32160)执行Tab键顺序。
* 设计人员： 如果启用标记选项，子表单边框将消失在生成的PDF输出中(NPR-32778)。

## Install 6.5.5.0 {#install}

**设置要求**

* AEM 6.5.5.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 可在 Adobe Package Share 中下载 Service Pack，您可以通过 AEM 6.5 实例直接访问 Adobe Package Share。
* 在具有 MongoDB 和多个实例的部署中，使用包管理器在其中一个 Author 实例上安装 AEM 6.5.5.0。
* 在安装之前，请拍摄AEM实例的快照或新鲜备份。
* 安装之前请重新启动该实例。虽然仅当实例仍处于更新模式时才需要这样做（实例从较早版本更新时也需这样），但如果实例运行较长时间，则建议执行此操作。

>[!NOTE]
>
>Adobe 建议不要移除或卸载 AEM 6.5.5.0 包。

### 安装Service Pack {#install-service-pack}

执行以下步骤以在现有 AEM 6.5 实例上安装 Service Pack：

1. 单击“ [包共享](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.5.0) ”或“ [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) ”链接以下载包。

1. 打开 [包管理器](http://localhost:4502/crx/packmgr/index.jsp) ，然后单 **击“上传包** ”以上传包。

1. 选择包名称，然后单击“ **安装**”。

>[!NOTE]
>
>**包管理器 UI 中的对话框有时会在 AEM 6.5.5.0 的安装过程中退出**
>
>因此，建议在访问该实例之前先等待错误日志稳定下来。用户必须等待与卸载更新程序包相关的特定日志，才能确保安装成功。 这通常出现在 Safari 中，但也可能会间歇性发生在任何浏览器中。

**自动安装**

可通过两种方法将 AEM 6.5.5.0 自动安装到正在运行的实例上：

答：当服务器联机 `../crx-quickstart/install ` 可用时，将包放入文件夹。 包会自动进行安装。

B. Use the [HTTP API from Package Manager](https://helpx.adobe.com/cn/experience-manager/aem-previous-versions.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.5.0 不支持 Bootstrap 安装。

**验证安装**

1. “产品信息”页(/system/console/productinfo)在“已安装产品”下显示更新 `Adobe Experience Manager, Version 6.5.5.0` 的版本字符串。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. The OSGI bundle `org.apache.jackrabbit.oak-core` is on version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 AEM Forms，请跳过。AEM Forms 中的修复通过单独的附加包来交付。

1. 确保您已安装了 AEM Service Pack。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。JEE上的AEM Forms中的修复通过单独的安装程序提供。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/cn/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

The UberJar for AEM 6.5.5.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 已弃用功能 {#removed-deprecated-features}

本节列表了在AEM 6.5.5.0中标记为已弃用的特性和功能。计划在将来版本中删除的功能将设置为先弃用，并设置一个替代选项供您使用。

建议客户检查他们是否在当前部署中使用了该功能，并制定计划更改其实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. 随着AEM 6.5中更新的AEM和目标集成以支持目标标准API（它使用通过Adobe IMS和I/O进行身份验证）以及Adobe Launch在指导AEM页面进行分析和个性化方面的作用日益增强，选择加入向导的功能已变得无关紧要。 | 通过各自的AEM云服务配置系统连接、Adobe IMS身份验证和Adobe I/O集成 |

## 已知问题 {#known-issues}

* 如果安装的 [!DNL Experience Manager] 是带有11的6.5.5.0, [!DNL Java] 请在安装Service Pack后重新启动服务器。 如果安装带有8的Service Pack，则无需重新启 [!DNL Java] 动。

* 如果层次结构中的文件夹已重 [!DNL Experience Manager Assets] 命名，且包含资产的嵌套文件夹已发布到 [!DNL Brand Portal]，则只有在根文件夹再次发布后，才会更新 [!DNL Brand Portal] 该文件夹的标题。

* 更新版 [!DNL chrome] 本83导致在构建包时出现问题。 使用其他可用的浏览器(如 [!DNL Internet Explorer] 和 [!DNL Firefox]或其他AEM标准包安装选项)来解决此问题。

* 无法使用AEM默认邮件发送器将电子邮件发送到远程SMTP服务器，因为它仅允许使用TLS v1.2进行通信。请从 `javax.mail:mail:1.5.0-b01` 包 `system/console` 中删除包并刷新包以解决此问题。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他字段可解决此问题。

* 如果 [!UICONTROL 连接的资产配置向导] 在安装后返回404错误消息，请使用包管理器 `cq-remotedam-client-ui-content` 手动重 `cq-remotedam-client-ui-components` 新安装和包。

* 在安装AEM 6.5.x.x过程中，可能会显示以下错误和警告消息：
   * “在 AEN 中使用 Target Standard API（IMS 身份验证）配置 Target 集成，然后将“体验片段”导出到 Target 时，会导致创建错误的选件类型。而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证将失败。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用购物横幅查看器预览资产时，Dynamic Media 交互式图像中的热点不可见。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 AEM 6.5.5.0 中包含的 OSGi 包和内容包:

* [AEM 6.5.5.0 中包含的 OSGi 包列表](assets/6550_bundles.txt)

* [AEM 6.5.5.0 中包含的内容包列表](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

这些网站仅适用于客户。如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系客户支](https://docs.adobe.com/content/help/en/customer-one/using/home.html)持有关访问支持门户的详细信息，请参 [阅访问支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

>[!MORELIKETHIS]
>
>* [AEM 6.5 发行说明](/help/release-notes/release-notes.md)
>* [AEM 产品页面](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 文档](https://helpx.adobe.com/cn/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

