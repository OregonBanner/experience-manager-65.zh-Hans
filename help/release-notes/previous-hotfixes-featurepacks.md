---
title: '[!DNL Adobe Experience Manager] 6.5先前的Service Pack发行说明'
description: ' [!DNL Adobe Experience Manager] 6.5 Service Pack的发行说明。'
contentOwner: AK
translation-type: tm+mt
source-git-commit: 131e564e4ed50c4f08412ba39c62f15b9c362b8c
workflow-type: tm+mt
source-wordcount: '17898'
ht-degree: 16%

---


# 以前的Service Pack{#hotfixes-and-feature-packs-included-in-previous-service-packs}中包含的修补程序和功能包

## [!DNL Adobe Experience Manager] 6.5.7.0  {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0是一个重要更新，包括自2019年4月发布6.5版以来发布的新功能、关键客户请求的增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了Service Pack。

[!DNL Adobe Experience Manager] 6.5.7.0中引入的主要功能和增强功能包括：

* 将页面移动和MSM转出作为异步操作执行，以减少它们对运行时性能的影响。

* 用户可以在卡片和列视图中对数字资产进行排序。

* [!DNL Assets] 并提供 [!DNL Dynamic Media] 多个辅助功能增强。这些增强功能与键盘导航、屏幕阅读器的使用以及使用户能够使用类似的辅助技术(AT)相关。 请参阅[[!DNL Assets] enhancements](#assets-6570)和[[!DNL Dynamic Media] enhancements](#dynamic-media-6570)。

* [表单数据模型HTTP客户端](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 配置以优化性能。

* [布局模式下每个组件](../../help/forms/using/resize-using-layout-mode.md#resize-components) 的重置选项可用性

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms提高了以下产品的性能：

   * 在提交自适应表单时验证服务器上的字段值。

   * 使用[!DNL Automated Forms Conversion service]将PDF表单转换为自适应表单。

* 支持[!DNL Experience Manager Forms]中的[!DNL Microsoft SQL Server] 2019。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.5。

有关[!DNL Experience Manager] 6.5.7.0中引入的功能和增强功能的完整列表，请参阅[6.5 Service Pack 7](new-features-latest-service-pack.md)中的新增功能。 [!DNL Adobe Experience Manager] 

以下是[!DNL Experience Manager] 6.5.7.0版中提供的修复程序的列表。

### [!DNL Sites] {#sites-6570}

* 打开页面的[!UICONTROL 时间绕排]选项时，请保持打开时间轴侧边栏选项，并导航到[!UICONTROL 站点]控制台，将发生`Failed to Load`错误(NPR-34951)。

* [!UICONTROL 时间绕排]选项不显示所选日期和时间范围的图像(NPR-34951)。

* 当筛选器从包含内容片段的页面调用`getHeader()`时，将发生`java.lang.AbstractMethodError`错误(NPR-34942)。

* 当页面的路径包含多个内容子字符串时，预览无法呈现，版本比较函数也会失败(NPR-34740)。

* 为组件的`String`类型标签属性设置数值时，可以删除组件并撤消删除操作。 但是，撤消删除后，label属性从`String`更改为`Long`(NPR-34739)。

* 在将基于具有锁定布局的模板的体验片段添加到页面时，会出现以下异常(NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 移动文件夹时，会导致遍历问题，并出现以下错误(NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 创建、发布新资产并将其移动到新位置后，将创建`Request to complete move operation`工作流，并导致“已中止”状态。 上传新资产并执行`move`操作会导致创建处于挂起状态的`Request to complete move operation`工作流(NPR-34543)。

* 将体验片段从[!DNL Experience Manager] 6.5.2环境导出到[!DNL Target]标准版时，API调用将失败，因为工作区属性不可用于[!DNL Target]标准版(NPR-34557)。

* 用户无法通过[!UICONTROL 管理发布]选项发布页面，因为[!UICONTROL 发布]选项会消失(NPR-34542)。

* 向文本添加某些样式时，将向文本添加一个`<div>`标记，并且该样式不能再应用于文本(NPR-34531)。

* 当您在弹出菜单中选择一个项目并更新所需文件时，它不允许保存对话框值，因为另一个菜单的必填字段为空(NPR-34529)。

* 当您从自定义模板创建页面并将其移动到Blueprint层次结构中时，之前从Live Copy层次结构中页面上显示的页面开始中删除的组件(NPR-34527)。

* 对内容应用文章样式后，便无法删除它(NPR-34486)。

* 体验片段的所有Live Copy和副本都指向相同的[!DNL Adobe Target]优惠ID(NPR-34469)。

* 项目符号列表项除了编号列表(NPR-34455)外还显示。

* “与源比较”选项无法显示源页面与已编辑页面版本之间的差异(NPR-34285)。

* 删除页面时，无法配置版本控制详细信息(NPR-34159)。

* 当用户选择[!UICONTROL 打开选择]对话框选项时，键盘焦点将移至页面上存在的隐藏控件(CQ-4307779、CQ-4293601)。

* 在作者上移动已发布的文件夹时，Publish实例中的文件夹路径不会相应地更新(CQ-4305144)。

* 当用户在[!UICONTROL 选择全部]选项上选择`Enter`键时，键盘焦点不会移到[!UICONTROL 创建控件]选项(CQ-4293599)。

* 选择`Esc`键时，焦点不会恢复到父控件(CQ-4293593、CQ-4293590)。

* 改进了[!DNL Sites] UI和核心组件(CQ-4293448)的WCAG规范。

* [!UICONTROL 对] 页面  禁用Zoomand  [!DNL Sites Editor] Scalefunctions(CQ-4282353)。

* 使用“向右旋转”选项后，屏幕阅读器会停止对当前旋转或翻转状态的旁白(CQ-4282128)。

* “完成”和“取消配置”对话框按钮有多个制表位(CQ-4274601)。

* 不允许在同一级别上移动同名页面(NPR-35041)。

* 选择“清除(x)”选项后，键盘焦点不会移到[!UICONTROL Filter]字段(CQ-4293581)。

* 升级到[!DNL Experience Manager] 6.5.6.0时，继承的段落系统的行为会发生更改，并且无法正常工作(NPR-35117)。

* 在[!DNL AEM Sites]页面(CQ-4307786)上选择[!UICONTROL Action]部分后，键盘用户无法按适当的顺序移动Tab键焦点。

* 在编辑内容片段时，在RTE工具栏的链接目标菜单列表中选择选项后，内容片段作者对话框会开始闪烁(CQ-4305532)。

* 键盘用户无法使用向下箭头键(CQ-4295097)在[!UICONTROL 添加组件]下拉列表中选择选项。

* 在[!DNL Sites]页面(CQ-4293600)的[!UICONTROL 资产]选项卡的“日历”菜单中选择日期时，制表符焦点不会按适当的顺序移动。

* 在删除编辑“站点”页面时可用的“链接”或“文本”选项后，选项卡焦点不会转移到键盘用户的下一个或上一个选项(CQ-4293597)。

* 在查看可用选项并按`Esc`键(CQ-4293592)后，键盘用户无法将制表符焦点移回[!UICONTROL Actions]部分的“更多”选项。

* 在[!UICONTROL 编辑]模式中为图像激活[!UICONTROL 旋转]选项时，对于键盘用户，制表符焦点（而不是停留在旋转上）会移至[!UICONTROL 重做]选项(CQ-4293587)。

* 在[!UICONTROL 链接和操作]选项卡上提供的[!UICONTROL 打开选择]对话框中，在[!UICONTROL 取消]选项(CQ-4293579)后，选项卡焦点将转移到页面中的隐藏元素。

* 键盘用户编辑图像时，导航到[!UICONTROL 完成]选项，然后按Enter键，屏幕阅读器不会宣布完成(CQ-4282351)。

* [!UICONTROL “链接”和“操作”]对话框上的“上移”和“下移”选项对屏幕阅读器和键盘用户(CQ-4281120)不可用。

* 在导航至[!UICONTROL 属性]页面(CQ-4293581, NPR-34653)上的关闭(X)选项后，键盘用户无法恢复制表符焦点。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0修复 [!DNL Assets] 了以下问题并提供以下增强。

* 对此版本中[!DNL Experience Manager Assets]中的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Assets]](/help/assets/accessibility.md)中的[辅助功能。

   * 使用键盘导航时间轴时，`Esc`键可折叠[!UICONTROL 显示全部]选项而不丢失焦点(CQ-4293598)。
   * 使用键盘Tab键导航时，从添加的标签中删除最后一个标签后，标签字段将保留焦点(NPR-35109)。
   * [!DNL Experience Manager] 组件现在包含要由屏幕阅读器使用的名称、角色和值的适当信息(NPR-34255)。
   * 删除“文字/大小”组合框、“链接”组合框、“语言”组合框或“文本”编辑框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素(CQ-4293585)。
   * 将指针悬停在选项上时，将显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用`Escape`键删除选项后，可以保留焦点。 (CQ-4293554).
   * 从页面中显示的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏(CQ-4282127)。
   * 可视用户可以区分普通文本和链接，因为在[!DNL Experience Manager]主页(CQ-4282072)中显示到所有解决方案的链接的可视提示（下划线和V形图标）。

* 在[!DNL Assets]中完成了以下用户体验增强：

   * 在卡视图和列视图中启用资源排序(NPR-35097)。

* 升级到6.5后，如果使用Assets HTTP API生成JSON文件，则文件中使用的编码会出现问题(NPR-35129)。

* 未提供创建集合权限（“创建集合”选项不可用）的组的用户仍可通过直接访问URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`(NPR-35115)来创建集合。

* 当按名称排序时，搜索的资产会按区分大小写的方式排序。 这基于在搜索结果中以有序显示的大小写创建两个单独的排序列表(NPR-35068)。

* 在编辑器中打开内容片段时，警告消息(`Invalid value specified for a metadata property`)将记录在错误日志(NPR-35012)中。

* 无管理员权限的用户可以使用[Experience Manager]桌面应用程序编辑过期的资产。 (NPR-34993).

* 当将同一资产拖动到“资产”用户界面上并创建新版本时，元数据中的更改将不会持续(NPR-34940)。

* 编辑集合时，用户可以删除集合的标题并成功保存更改(NPR-34889)。

* 上传重复图像时，会显示删除选项。 选择“删除”可上传图像。 还会触发DAM更新资产工作流(NPR-34744)。

* 将[!DNL Adobe Asset Link]与[!DNL Adobe InDesign]一起使用时，搜索结果中不包含文件夹和收藏集，但仅包含资产(NPR-34699、CQ-4303666)。

* 将指针悬停在卡视图上，将屏幕滚动作为（自动）关注卡中可用的快速操作的结果(NPR-34514)。

* 在批量编辑多个资产的属性时，选择[!UICONTROL 保存]选项将关闭批量编辑器视图并重定向到主[!DNL Assets]页面。 此行为与[!UICONTROL 保存并关闭]选项的行为相同，不应为(NPR-34546)。

* 保存后，智能集合不显示正确的用户界面设置。 查询正确保存，但界面始终显示最后添加的“选项”谓词(NPR-34539)。

* 向[!DNL Experience Manager]添加资源时，不带命名空间的元数据不会导入(NPR-34530)。

* 在文件夹上拖动资产以移动资产时，用户界面还会显示以下选项：[!UICONTROL 放入Lightbox]和[!UICONTROL 放入Collection]。 即使取消移动操作，用户界面仍继续显示后两个选项(NPR-34526)。

* 符号`%>`显示在集合页面上(NPR-34499)。

* 在列视图中，[!DNL Assets]在显示所有资源之前向上和向下滚动时显示重复文件夹和资源名称(NPR-34464)。

* 如果您在创建公用文件夹后立即创建了专用文件夹，则公用文件夹会使用专用文件夹设置(NPR-34415)。

* 在卡视图中，卡不按字母顺序列出，并且卡不能按字母顺序排序(NPR-34234)。

* 重新打开级联规则时，用户界面上不会保留这些选项(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* 对[!DNL Dynamic Media](CQ-4290306)中的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[辅助功能。

   * 屏幕阅读器(JAWS，Narrator)在“嵌入大小”菜单选项(CQ-4290927)中对菜单项的名称、角色和状态进行解说。
   * 用户可以使用`Tab`键(CQ-4290926)导览“电子邮件链接”对话框。
   * 考虑到屏幕阅读器增强功能(CQ-4290623、CQ-4290622)，创建视频编码用户档案的工作流程更为用户友好。
   * 使用`Tab`键导航时，焦点将移至工作流中相应的用户界面元素，以创建交互式视频(CQ-4290621、CQ-4290620、CQ-4290619)。
   * 为符合Web标准，对“发布”页、“编辑资产”页、“编辑智能裁剪”页和“图像集编辑器”页进行了改进。 辅助技术(AT)用户现在可以轻松导航这些页面并执行裁剪图像等操作(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * 对查看器进行了改进，使用户能够使用键盘进行导航(CQ-4290615)。
   * 键盘和屏幕阅读器用户可以使用裁剪功能(CQ-4290609)。
   * 键盘用户可以更好地管理热点(CQ-4290604、CQ-4290603)。

* 如果公司名和文件夹名相同，则远程图像集在[!DNL Experience Manager]中不可编辑(NPR-31340)。

* 在将热点添加到[!DNL Dynamic Media]图像或编辑带有图像的[!DNL Dynamic Media]视频或[!DNL Experience Fragment](CQ-4307267)之后，尝试预览输出时，z索引顺序不正确。

* [!DNL Dynamic Media] 重新处理混合媒体集时，同步会失败(CQ-4307184)。

* 如果资产被移动到已配置了自动同步到[!DNL Dynamic Media]的文件夹，则资产不会同步(CQ-4307122)。

* [!DNL Dynamic Media] 使用本机HTML5视频控件(CQ-4306977、CQ-4306727),iOS设备上不播放视频。

* 无法下载应用了SmartCrop的图像(CQ-4304558)。

* 无法选择性地将文件夹发布到Dynamic Media(CQ-4304526)。

* 从[!DNL Experience Manager]取消发布视频文件时，不会从已配置的Scene7部署(CQ-4304405)取消发布自适应视频集。

* 在全景媒体组件中添加全景图像资源并刷新页面会导致`Uncaught ReferenceError: $ is not defined`错误(CQ-4302810)。

* 在[!UICONTROL 查看器预设编辑器]中，编辑[!UICONTROL PanoramicImage/PanoramicImage_VR]预设时，在`PanoramicView`组件中，`PANORAMICVIEW_AUTOROTATE`修饰符标签不可用(CQ-4302443)。

* 如果视频不是MixedMediaSet中的第一个视频字幕(CQ-4298161)，则不显示视频字幕。

* iPhone移动设备上的HTML5 eCatalog Viewer无法翻页或翻页(CQ-4296611)。

* 在移动设备上滚动色板时，色板滚动至可见区域的右侧和外侧几秒钟，然后滚动回视图(CQ-4296439)。

* 创建查看器预设主控记录后，CSS和图稿将不会被发布，而只会发布查看器预设(CQ-4262205)。

* 尝试在[!UICONTROL 交互式视频/图像]组件中链接给定热点的体验片段时，它不显示选定的体验片段路径。 而是从路径字段(NPR-35146、CQ-4298136)返回一个空值。

* 无法在IVV编辑器(CQ-4308560)中预览体验片段。

* 在向图像中添加热点并选择体验片段时，无法选择该子文件夹和体验片段的变体(CQ-4307455)。

* 上传后，非图像资产不会显示为已发布(CQ-4306415)。

#### [!DNL Experience Manager] 3D资源  {#three-d-assets-6570}

* `DAM CQ MIME Type` 服务将不正确的MIME类型应用于3D资产，导致呈现不正确(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* Commerce product collection用户界面不会列表集合中超过15个产品(NPR-34502)。

### 平台 {#platform-6570}

* 通过HTTPS的HTTP会话不会失效(NPR-35083)。
* 从用户界面启动每日或每周维护任务时，将返回`NullPointerException`(NPR-34953)。
* W3C验证程序报告兼容客户端库JavaScript文件(NPR-34898)的警告。
* `AudienceOmniSearchHandler`函数使用已弃用的索引(NPR-34870)。
* 从Experience Manager注销不会清除Cookie(NPR-34743)。
* 如果标记名称包含特殊字符(NPR-34357)，则`TagManager` API的`findByTitle`函数将不起作用。
* 导入用户同步包的过程失败(NPR-34399)。
* 为`Coral.Masonry`组件(GRANITE-29962)添加了对`ariaLabel`和`ariaLabelledby`属性的支持。
* 安装最新核心组件包(CQ-4306788)后，不会为包含内容片段的页面刷新调度程序缓存。
* 在用户界面(CQ-4305439)上未正确显示带有引号(`"`)的本地化标记名称。

### 用户界面 {#ui-6570}

* 组件属性中的[!UICONTROL 链接到]字段显示与指定字符串不匹配的自动完成建议(NPR-34865)。

* AEM在您计划在2天之间分发的每日维护窗口时显示以下错误消息(NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 集成 {#integrations-6570}

* 编辑现有[!DNL Adobe Launch]配置失败(NPR-35045)。
* 如果使用IMS配置和[!DNL Adobe Target Standard]环境(NPR-34555)，则无法将[!DNL Experience Fragments]导出到[!DNL Adobe Target]。
* 当从文件夹导航到[!UICONTROL 受众]页面(NPR-35151)时， [!UICONTROL 创建]选项显示在[!UICONTROL 受众]页面上。

### Sling {#sling-6570}

* 默认登录运行状况检查会验证不存在的用户的凭据(NPR-34686)。

### 翻译项目{#translation-6570}

* 在[!DNL Experience Manager]中取消翻译项目时，取消该项目的请求不会发送到翻译提供者(NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 产品中所有不公平术语的实例都被接受的等价物取代(NPR-34311)。
* [!DNL Google+] 从社交共享选项的列表中删除(NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* 在[!UICONTROL 列表视图](NPR-34728)中选择资产时，用户界面不会做出响应。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Forms]。它们使用单独的[!DNL Forms]加载包交付。 此外，还发布了一个累积安装程序，其中包含针对JEE上[!DNL Experience Manager Forms]的修复。 有关详细信息，请参阅[安装AEM Forms add-on](#install-aem-forms-add-on-package)和[在JEE上安装AEM Forms](#install-aem-forms-jee-installer)。

**自适应表单**

* 应用[!DNL Experience Manager] Service Pack 6(NPR-35126)后，无法使用经典UI编辑自适应表单。

* 将PDF转换为自适应表单时，无法使用选项卡式布局上的表单数据模型为嵌套面板设置值。 此外，使用代码编辑器为静态数组动态设置单选按钮组值时，也存在问题(NPR-35062)。

* 在自适应表单的文本字段组件中输入日文字符时，可以指定的字符数超过35个字符的最大限制(NPR-35039)。

* 自适应表单在提交表单后显示的&#x200B;**[!UICONTROL 感谢]**&#x200B;页面上显示不需要的参数，如`owner`和`status`(NPR-34989)。

* [!UICONTROL [!UICONTROL Attachment]组件的文件选择]对话框显示不支持的文件类型以及选择，这会导致在提交自适应表单时出错(NPR-34970)。

* 在[!DNL Experience Manager Sites]页面中插入包含表单前文本的自适应表单时，光标焦点将直接移动到表单前的文本(NPR-34947)。

* [!UICONTROL 使用] Dataoption预览使用6.2数据XML文 [!DNL Experience Manager] 件预填自适应表单不能正常工作(NPR-35087)。

* 更新自适应表单的数据字典时，该表单不会被转换，因为自适应表单返回缓存值(NPR-34845)。

* 由于缓存失效(NPR-34567)，片段以自适应形式加载需要更长的时间。

* 对于自适应表单中的屏幕阅读器，制表符导航不能正常工作(NPR-34544)。

**通信管理**

* 无法将包含数字数据（包括浮点类型）的XML标签的值保存为草稿(NPR-35050)。

* 从ES3迁移资产时，资产包括两个不可编辑的默认条件(NPR-34972)。

* 编辑字母中的数据字典时，[!UICONTROL Lent Content]部分显示旋转的矩形而不是有用信息(NPR-34853)。

**交互式通信**

* Interactive Communication的转出配置名称（安装[!DNL Forms] add-on包后可用）重复标准转出配置名称(NPR-34976)。

**Document Security**

* 保存新的文档安全策略时，Experience Manager Forms将显示`Relative validity period is required`错误消息(NPR-34679)。

* 文档安全无法保护PDF 2.0文档(CQ-4305851)。

有关安全更新的信息，请参阅[Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html)。

## [!DNL Adobe Experience Manager] 6.5.6.0  {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0是一个重要更新，其中包含新功能、关键客户请求的增强功能以及性能、稳定性和安全性改进，这些功能是自2019年4月&#x200B;**发布6.5版以来发布的。** 它可以安装在Adobe Experience Manager 6.5顶部。

Adobe Experience Manager 6.5.6.0中引入的主要功能和增强功能包括：

* 使用[!UICONTROL 快速发布]或[!UICONTROL 管理发布]向导，有选择地将资产发布或取消发布到[!DNL Experience Manager]或[!DNL Dynamic Media]。

* 使用[!DNL Dynamic Media]用户界面可使内容投放网络(CDN)缓存内容失效。

* 现在，还支持通过代理服务器将资产贡献文件夹从Brand Portal发布到Experience Manager Assets。

* 现在，在删除[!DNL Experience Manager Assets]中的专用文件夹时，将清除自动生成的专用文件夹组。

* 在[!DNL Dynamic Media]中更新了视频[!UICONTROL 查看器]预设编辑器中修饰符的说明。

* 提供了新的公司设置以反映[!DNL Dynamic Media]连接器的状态。

* `test`和`aiprocess`的默认选项会从Dynamic Media中以前的`Rasterize`更新为`Thumbnail`，以确保用户只需创建缩略图并跳过页面提取和关键字提取。

* [在客户端预填自适应表单](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client)。

* [通过双向SSL实现，在服务器上与RESTful API进行表单数据模型集成](../../help/forms/using/configure-data-sources.md)。

* [增强了已转换的自适应表单页面的缓存](../../help/forms/using/configure-adaptive-forms-cache.md)。

* 支持Automated forms conversion服务](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)中的[Adobe Sign文本标记。

* 支持使用[!DNL Automated Forms Conversion service]将彩色表单转换为自适应表单](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)。[

* 支持SMB 2和SMB 3协议。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.4。

有关Experience Manager 6.5.6.0中引入的功能和增强功能的完整列表，请参阅[Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md)中的新增功能。

以下是[!DNL Experience Manager] 6.5.6.0版中提供的修复程序的列表。

### [!DNL Sites] {#sites-6560}

* 在[!DNL Sites]或[!DNL Screens]中，选择一个项目，然后单击[!UICONTROL 管理出版物]。 由于用户界面错误，用户无法进入[!UICONTROL 管理发布]向导。 具体而言，[!UICONTROL Publish]选项不起作用(NPR-34099)。
* 在取消选择[!UICONTROL 取消继承]或[!UICONTROL 禁用继承]选项(NPR-34097)后，iParsys（继承的段落系统）的位置不会恢复到其原始默认位置。
* 如果`RolloutConfigManagerFactoryImpl`无法加载转出配置，则不会尝试加载缺少的配置。 它返回缓存的配置(NPR-34092)。
* 在Text核心组件中，使用源HTML编辑选项后，将删除`em`标记中的类(NPR-34081)。
* 从Experience Manager 6.3.3升级到Experience Manager 6.5.3后，转出过程需要更长的时间，转出失败并出现超时错误(NPR-34049)。
* `htmlwriter`不对属性值进行编码。 XF标记中存在的标记用解码的属性值（即`"`而不是`&#34`）导出。 它会在使用导出的XF的Visual Experience Composer的目标端引起问题(NPR-34048)。
* 当在[!DNL Experience Manager Sites]中移动页面时，增强日志记录以捕获因故创建版本失败(NPR-34014)。
* 在[!DNL Rich Text Editor]中，如果删除了所有文本，则段落标签也会被删除(NPR-33976)。
* 打开或刷新`siteadmin`页面（经典UI中）时，`New`菜单中的选项将被禁用(NPR-33949)。

   ![用于说明经典UI中缺少菜单问题的屏幕截图](assets/33949_missing_menu.png)

* [!DNL Content Fragment]不能用作`TemplatedResource`，因为它在`ContentFragmentUsePojo`(NPR-33911)中失败。
* 同步和异步移动操作可能会导致并发传输导致的错误。 页面移动操作仅限于异步移动。 它可防止页面的并发移动(NPR-33875)。
* [!UICONTROL 将内] 容从“作者”复制到“发布”实例的Manage Publication操作失败并生成JavaScript错误(NPR-33872)。
* 当选择多个页面或资产以创建版本时，将仅为上次选择的页面或资产创建新版本(NPR-33866)。
* 将包含Live Copy的Blueprint页面移动到另一个文件夹。 将文件夹移到原始文件夹时，移动操作将失败且无错误(NPR-33864)。
* 在[!DNL Sites]控制台中，当使用移动操作重命名网页时，向导的最后一步会显示两个重叠的对话框(NPR-33831)。

   ![用于说明NPR-33831重叠移动对话框问题的屏幕截图](assets/33831_rename_dialog.png)

* 在复制和粘贴操作期间，将删除复制中[!DNL Adobe Campaign]的`cq:acLinks`和`cq:acUUID`属性(NPR-33794)。
* 尝试在已分离父Live Copy的子页面上转出时，[!DNL Experience Manager]会生成空指针异常(NPR-33676)。
* 在页面上再次复制并粘贴布局容器时，布局容器中的[!DNL RTE]组件不可见。 [!DNL RTE]组件不可编辑，但在页面刷新时显示(NPR-33662)。
* 调整不同断点（中、大）的布局组件大小时，布局的行为不如预期(NPR-33608)。
* 在[!DNL RTE]的内联编辑模式下，拖动图像对文本组件无效(NPR-33602)。
* 可以在Blueprint页面中创建与页面名称同名的组件。 转出过程中，`_msm_moved`后缀为重命名组件。 组件移动到[!UICONTROL 段落系统](NPR-33535)的末尾。
* 当在许多页或资产上设置offTime或onTime时，会占用大量资源，并会在启动和关闭期间减慢系统速度(NPR-33482)。
* 对`/content/experience-fragment`具有CRUD权限的用户无法删除文件夹(NPR-33436)。
* 您可以选择[!UICONTROL HTML &amp; JSON]作为[!DNL Experience Fragments]部分父文件夹上的[!UICONTROL Adobe Target导出格式]选项。 此父文件夹的子文件夹的触屏优化UI中会显示相同的属性。 但是，在CRXDE中，对于`cq:adobeTargetExportFormat`，它仅显示HTML而不显示`html,json`(NPR-33423)。
* 不支持从页面别名中发布或取消发布。 删除似乎另有说明的选项(NPR-33415)。
* 特定标记可以从[!DNL Experience Manager]中的一个位置移动到另一个位置。 它还可以在移动前后应用于不同的页面。 编辑页面属性时，即使标签相同，标签也不会显示为供编辑(NPR-33353)。
* 从包含多个布局容器的模板中删除布局容器时，页面模板无法正确呈现(NPR-33347)。
* 在模板编辑器中，尝试删除`/content/`下超过100000个页面使用的模板。 显示错误，但没有任何错误消息(NPR-33312)。
* 使用锚点重定向到[!DNL Experience Manager]页面在创作实例上不起作用，因为`PageRedirectServlets`将查询字符串放在URL片段或锚点之后(NPR-34288)。
* 在`/content/campaign`下创建品牌会生成不允许创建活动的结构。 [!UICONTROL “创] 建品牌”选项会使新创建的品牌无法创建 [!UICONTROL 优惠] 和活动，因为没  有创建选项(NPR-34113)。
* 您可以暂停页面的[!DNL Live Copy]，继承会中断，如“编辑器”模式所示。 在页面属性中，表示继承的图标错误地指示继承存在且未中断(NPR-34017)。
* 具有许多引用的页面无法异步移动，有时移动操作会失败(CQ-4297969)。
* 在创作时，URL中具有`/`字符的网页会变得不响应。 在创作时添加组件时，CPU使用率会增加，浏览器会停止响应(CQ-4295749)。
* 在浏览模式下，NVDA不会解说从“类型/大小”菜单选项中选择的值。 视觉焦点不在选定元素上。 依赖屏幕阅读器的用户无法使用浏览模式(CQ-4294993)。
* 创建网页时，用户可以选择[!UICONTROL 内容页面]模板。 在[!UICONTROL 社交媒体]选项卡中，用户选择[!UICONTROL 首选XF变量]。 要在NVDA浏览模式下选择体验片段，用户无法使用键盘键(CQ-4292669)。
* 已将handlebars库更新为更安全的v4.7.3(NPR-34484)。
* [!DNL Experience Manager Sites]组件中的多个跨站点脚本实例(NPR-33925)。
* 创建新文件夹时的文件夹名称字段易受存储的跨站点脚本攻击(GRANITE-30094)。
* [!UICONTROL 欢迎]页面和路径完成模板上的搜索结果易受跨站点脚本攻击(NPR-33719、NPR-33718)。
* 在非结构化节点上创建二进制属性会导致在二进制属性对话框(NPR-33717)上进行跨站点脚本。
* 在CRX DE接口上使用[!UICONTROL 访问控制测试]选项时进行跨站点脚本编写(NPR-33716)。
* 在向客户端发送信息时，用户输入未针对各种组件进行适当编码(NPR-33695)。
* 在Calendar视图中为Experience Manager收件箱执行跨站点脚本(NPR-33545)。
* 以`childrenlist.html`结尾的URL显示HTML页面，而不是404响应。 此类URL易受跨站点脚本攻击(NPR-33441)。


### [!DNL Assets] {#assets-6560}

**Experience Manager资源中的辅助功能增强**

* 使用键盘键，用户现在可以访问资源[!UICONTROL 引用]列表(NPR-34115)中的交互式用户界面选项并将注意力集中在这些选项上。

* 屏幕阅读器现在宣布搜索页面上谓词的预期操作(NPR-34104)。

* 现在，搜索页面和搜索结果页面包含了更多信息标题，以便更好地了解屏幕阅读器用户(NPR-34093)。

* 屏幕阅读器现在会宣布删除资产[!UICONTROL 属性]页面(NPR-33972)的[!UICONTROL 基本]选项卡中选定标记的选项。

* 现在，屏幕阅读器将列表视图中每行中的元素宣布为同一行的元素(NPR-33932)。

* 使用`Tab`键导航时的用户焦点现在移动到版本预览(NPR-33863)中的关闭选项。

* 现在，在关闭Omnisearch后，用户焦点将移至搜索图标(NPR-33705)。

* 使用键盘键进行导航时，可操作的用户界面选项现在具有更加突出的视觉焦点，并增强了对比度。 键盘用户可以识别聚焦区域(NPR-33542)。

* 使用键盘的拖动功能现在在屏幕阅读器的浏览模式下的[!UICONTROL 元数据模式编辑器]中工作(CQ-4296326)。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器，

   * 加载对话框后，不会立即解说表信息。

   * 可以导航到所有列出的自动建议。

   * 为[!UICONTROL 添加电子邮件地址/搜索](CQ-4294232)解说显示的自动建议。

* 使用`Esc`键从卡视图中删除快速操作图标不再从最后一个聚焦项目(CQ-4293554)中删除键盘焦点。

* 对于用户界面上的交互式选项，屏幕阅读器现在会宣布其用途，而不是图标的文字名称(CQ-4272943)。

* 键盘焦点现在可成功移至[!UICONTROL Flyout]、[!UICONTROL InlineZoom]、[!UICONTROL Shoppable_Banner]、[!UICONTROL Zoom_dark]、[!UICONTROL Zoom_light]、[!UICONTROL ZoomVertical在资产详细信息中的查看器[!DNL Dynamic Media](CQ-4290605)中使用键盘Tab键导航时，使用a11/>和[!UICONTROL 和]ZoomVertical_light]选项。

* [!UICONTROL 现在可] 以使用键  盘键访问“资产属性”页上的“保存并关闭”选项(NPR-34107)。

* 由于登录页面上的用户名和密码组合不正确而导致的错误消息现在在每次出现错误时由屏幕阅读器宣布(NPR-33722)。

* 在[!DNL Experience Manager]标题部分，当在浏览模式下导航时，屏幕阅读器现在会宣布，

   * 在[!UICONTROL 键入以在Omnisearch中搜索]中自动编辑的建议。

   * 对于[!UICONTROL Solutions]、[!UICONTROL Help]、[!UICONTROL Inbox]和[!UICONTROL User]选项，状态为展开或折叠。

   * 当用户在[!UICONTROL 帮助]选项下的“搜索帮助]”字段中输入搜索字符串时显示的[!UICONTROL 搜索帮助]状态消息。[!UICONTROL 

   ![标题中的“帮助”菜单](assets/Help_aem_header.png)

   *图： [!UICONTROL 搜索“帮] 助”  菜单。*

   * 如果在[!UICONTROL User]选项下的[!UICONTROL Impersonate as]字段中输入了不正确的值，并且焦点正确移到文本字段(NPR-33804)，则显示错误消息。

   ![标题中的用户菜单](assets/User_aem_header.png)

   *图： [!UICONTROL 在标题] 的Usermenu  中模拟asfield。*

* 用户现在可以使用以下键盘更改焦点：

   * [!UICONTROL 在“链接共享”对] 话框中搜索/添 [!UICONTROL 加电子] 邮件地址。

   * [!UICONTROL 在文件夹属] 性的“ [!UICONTROL 权限”标] 签中的“已关  闭用户组”下添 [!UICONTROL 加] “用户”或“组”字段(NPR-34452)。

**Experience Manager资产中已修复的问题**

[!DNL Adobe Experience Manager] 6.5.6.0修复 [!DNL Assets] 了以下问题：

* 从资产的时间轴中选择注释时，不会突出显示(CQ-4302422)。

* 使用[!DNL Adobe InDesign]模板创建的营销附属品资产（如宣传册、传单和名片）的预览不显示换行和分段(NPR-34268)。

* 文本提取，因此对上传的PDF文件进行全文搜索不起作用(NPR-34164)。 要修复它，请在安装Service Pack 6后重新启动[!DNL sAdobe Experience Manager]部署。

* 多页资产的时间轴在“时间轴”视图下浏览资产时，会显示应用于所有子资产的注释，而不是显示特定子资产的特定注释(NPR-34100)。

* 如果资产文件夹包含JavaScript、CSS或JSON文件格式的资源(NPR-34090)，则不会使用[!UICONTROL 管理发布]选项来发布资产文件夹。

* 在Omnisearch中取消选择或删除已应用的标签或过滤器会多次执行搜索查询，这会导致搜索时间增加(NPR-34078)。

* 在卡视图中，当工作流（位于文件夹中的资产上）正在进行或待处理时，页面会重新加载，直到工作流完成或终止。 因此，作者无法处理必须向下滚动的文件夹中的这些资源(NPR-33986)。

* 如果用户将已发布的资产移动到新位置，则即使取消选择[!UICONTROL 重新发布]选项，也会重新发布资产。 这会导致发布实例上存在许多孤立资产。 但是，默认的行为是，对已发布资产的移动操作会自动取消发布它；如果作者在移动资产时选择[!UICONTROL 重新发布]选项，则会重新发布此资产(NPR-33934)。

* 集合中资产的[!UICONTROL 移动资产]页面不会加载所有HTML内容，如[!UICONTROL 调整/重新发布]选项。 因此，用户无法完成移动操作(NPR-33860)。

* 移动资产并在移动资产的名称和标题中添加特殊字符会在资产的新位置(NPR-33826)创建额外的文件夹（使用相同的名称）。

* [!UICONTROL 当] 在“下载”对话框上选  择“电子邮件”选项时，资  产的“下载”按钮会被禁用(NPR-33730)。

* 对资产执行批量操作时，如批量元数据编辑(NPR-33723)时，会观察到错误“Request-URI过长”。

* 如果上传的JSON文件具有空格或特殊字符(NPR-33712)值，则会发生JavaScript错误，用户无法选择或删除[!UICONTROL Dropdown]字段中由[!UICONTROL 通过JSON路径]功能生成的选项（如[!UICONTROL Dropdown]）。

* 当使用[!DNL desktop app]或[!DNL Adobe Asset Link]中的[!UICONTROL 打开]选项更新资产时，资产的静态演绎版不会更新，并会同步回[!DNL Adobe Experience Manager](CQ-4296279)。

* 在列视图中，对一组资产执行移动操作时，也会移动那些在使用[!UICONTROL 过滤器]选项之前选定的资产。 请注意，使用[!UICONTROL Filter]选项会取消选择以前的选择(NPR-34018)。

* 在资产的搜索建议中，在特殊字符前添加反斜杠，这些资产的名称中包含特殊字符(NPR-33834)。

* 在[!UICONTROL 文件夹元数据模式表单]中创建下拉列表规则时，用户无法从[!UICONTROL 字段选择]列(CQ-4297530)中选择值。

* 安装[!DNL Experience Manager] 6.5 Service Pack 5或[!DNL Experience Manager] 6.5上的先前版本(NPR-34532)时，将删除资源自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。 要检索运行时副本，请使用HTTP API将工作流模型的设计时副本与运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

**在Dynamic Media中修复的问题**

* 如果用户在创建视频用户档案后在编辑中定义编码设置，则会从视频用户档案中删除智能裁剪设置(CQ-4299177)。

* 当用户在资产详细信息页面(NPR-34235)上的侧栏选项（例如，[!UICONTROL Overview]、[!UICONTROL Timeline]、[!UICONTROL Viewers]）之间切换时，页面加载时资产会闪烁。

* 在重新处理作业时会发现以下问题：

   * 重新处理作业返回的作业句柄中缺少作业ID。

   * 仅对视频日志文件名（而非完整路径）重新处理作业。

   * 重新处理作业没有将资产类型设置为静态的选项。

   * `ExcludeFromAVS` 选项(CQ-4298401)。

* 当将图像用户档案添加到具有多个长宽比（例如，11）的文件夹时，智能裁剪功能会失败，并出现错误(NPR-34082)。

* 当用户向下滚动[!UICONTROL 工作流存档]页面上[!UICONTROL 工作流]选项卡(位于使用Dynamic Media Scene7(CQ-4299727)配置的[!UICONTROL 工具]中)时，将触发DAM更新资产工作流。[!DNL Adobe Experience Manager]

* [!UICONTROL 查看器预设编辑器]的“行为”]选项卡中的符号未本地化(CQ-4299026)。[!UICONTROL 

* 如果查看器处于响应模式，则主视图以不正确的布局显示图像，而该布局不适合查看器(CQ-4298293)。

* 对[!UICONTROL Adobe Experience Manager]中的图像预设所做的更改不会同步到Scene7 Publishing System(CQ-4299713)。

### [!DNL Commerce] {#commerce-6560}

* 在移动资产时，不会重构来自产品的资产链接(NPR-34098)。

### 平台 {#platform-6560}

* 无法使用诊断工具在升级的Experience Manager实例(NPR-34336)上下载日志。
* 由于依赖于特定版本的`cq-wcm-api`基础包(CQ-4300520)，升级失败并出错。
* 未指定默认代理（发布）配置的&#x200B;**[!UICONTROL 连接超时]**&#x200B;和&#x200B;**[!UICONTROL 套接字超时]**&#x200B;设置的默认值(NPR-33707)。
* 对`/etc/map.publish`下的映射配置的更新不会反映在站点页面上(NPR-34015)。
* [API参考](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 文档不包括包的 `com.day.cq.tagging` 文档(CQ-4295864)。

### 用户界面 {#ui-6560}

* 卸载浏览器界面不显示所有作业主题(NPR-34308)。
* [配置浏览器](/help/sites-administering/configurations.md)接口不显示所有配置(NPR-33644)。
* 在搜索要模拟的用户时按`Esc`键时，将关闭&#x200B;**[!UICONTROL 用户]**&#x200B;对话框，而不是用户列表(NPR-34084)。

### 集成 {#integrations-6560}

* 长名称的活动未与[!DNL Adobe Target](NPR-34254)同步。

* 在创建新Adobe启动配置时选择属性会导致以下错误消息(NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 翻译项目 {#translation-6560}

* 如果用户的`authorizableID`包含特殊字符(NPR-33828)，则不创建翻译项目。

### Sling {#sling-6560}

* 运行状况检查和模式检测器具有重叠功能。 因此，从产品中删除了健康检查(NPR-33928)。

### WCM {#wcm-6560}

* 基础组件 — 当您向页面添加基础图像组件并引用图像时，`Undo`操作不起作用(NPR-34516)。

* 无法使用页面移动操作(CQ-4303028)。

### [!DNL Communities] {#communities-6560}

* 在社交媒体上共享帖子显示一个过时的选项Google+(NPR-33877)。

* 社区成员无法修改组模板或其他组功能设置(NPR-33530)。

* 在论坛帖子中，未正确生成图像上的超链接标记(NPR-33464)。

* 在“社区分配”功能(NPR-33442)中可识别辅助功能故障。

* 通过admin console添加的社区组的现有用户将从“用户”列表中删除，该用户在社区组控制台中进行任何修改时都将进行此类操作(NPR-34315)。

* `TagFilterServlet`会泄露潜在敏感数据(NPR-33868)。

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Forms]。它们使用单独的[!DNL Forms]加载包交付。 此外，还发布了一个累积安装程序，其中包含针对JEE上[!DNL Experience Manager Forms]的修复。 有关详细信息，请参阅[安装AEM Forms add-on](#install-aem-forms-add-on-package)和[在JEE上安装AEM Forms](#install-aem-forms-jee-installer)。

安装[!DNL Experience Manager Forms] 6.5.6.0加载项包后：

* 停止[!DNL Experience Manager Forms]实例。

* 从`crx-repository\launchpad\ext`目录中删除`bcpkix-1.51`、`bcmail-1.51`和`bcprov-1.51` JAR文件。

* 从`sling.properties`文件中删除` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider`属性。

* 重新启动[!DNL Experience Manager Forms]实例。

**自适应表单**

* 当缺少自适应表单片段时，自适应表单无法渲染(NPR-34302)。

* 自适应表单域的帮助内容描述显示段落HTML标记(NPR-34116)。

* 选择&#x200B;**[!UICONTROL 在Server]**&#x200B;上重新验证属性时，自适应表单无法提交(NPR-33876)。

* **[!UICONTROL 提交到REST端点]**&#x200B;提交操作不适用于自适应表单(CQ-4299044)。

* 辅助功能：当您尝试提交自适应表单而不上传必填字段的附件时，焦点不会自动转移到附件字段(CQ-4298065)。

* 向自适应表单的表添加行时，**[!UICONTROL 添加到顶部]**&#x200B;和&#x200B;**[!UICONTROL 添加到底部]**&#x200B;选项不显示适当的结果(CQ-4297511)。

* [!UICONTROL 值提交]脚本触发不正确，这会导致自适应格式的数据丢失(CQ-4296874)。

* 对于本地化的自适应表单，日期选取器不能正确工作(NPR-34333)。

* 当文件名中有下划线或空格时，无法将文件附加到自适应表单(CQ-4301001)。

* 当嵌套的可重复面板比其父面板发生的次数多时，此类嵌套可重复面板的所有发生次数都无法预填充(NPR-33666)。

* 自适应表单具有一些开放的资源解析器。 这会导致提交失败。 出现间歇性问题(CQ-4299407)。

* 首次打开字段配置时，不显示属性图标(CQ-4296284)。

* 在提交自适应表单时，用户可以编辑提交元数据，如`afPath`、`afSubmissionTime`和`signers`。 要解决此问题，将从客户端的表单提交数据中删除元数据值。 用户可以使用`FormSubmitInfo`对象从服务器检索这些值(NPR-33654)。

* 向客户端发送信息时，用户输入未针对[!DNL Forms]组件进行适当编码(NPR-33611)。

**工作流**

* 当工作流审批者上传附件时，附件将重命名为`undefined`(NPR-33699)。

* [!DNL Experience Manager] “工作流清除”操作失败，并显示以下错误消息(NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 在提交 [!DNL Windows] 表单后停止响应的应用程序(NPR-34409)。

* 安装AEM Service Pack时，项目的&#x200B;**To Do**&#x200B;列表不显示为链接。 **To Do**&#x200B;项的文本包括HTML标记(NPR-34317)。

**交互式通信**

* 当您将文本文档片段包含嵌套的可重复组件时，Interactive Communication无法保存(NPR-34095)。

**通信管理**

* 当您修改包含文档字典值的文本片段时，代理UI停止响应(NPR-33930)。

* 将内容从[!DNL Microsoft Word]文档复制粘贴到字母中的文本文档片段会导致格式问题(NPR-33536)。

**文档服务**

* 使用Output和Forms服务从XDP文件生成PDF文件时，会导致缺少文本和文本重叠(NPR-34237、CQ-4299331)。

* 将HTML文件转换为PDF时，无法配置`MaxReuseCount`属性(NPR-33470)。

* 下载包含Reader扩展功能的PDF文件时，无法使用[!DNL Adobe Reader](NPR-33729)向PDF文件添加附件。

**文档安全**

* 安装[!DNL Experience Manager] Service Pack(NPR-34310)后，无法在PDF文件中使用基于HSM的证书执行Sign操作。

**设计人员**

* 无法在Designer 6.5.x版(CQ-4295322)中打开XForm。

* 打开Designer时，“欢迎”屏幕显示错误的年份(CQ-4295289)。

* 在服务器上安装[!DNL Acrobat DC]时，**[!UICONTROL 分发表单]**&#x200B;选项处于非活动状态(CQ-4296304)。

有关安全更新的信息，请参阅[Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html)。

## [!DNL Adobe Experience Manager] 6.5.5.0  {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0是一个重要更新，其中包含新功能、关键客户请求的增强功能以及性能、稳定性和安全性改进，这些功能是自2019年4月&#x200B;**发布6.5版以来发布的。** 它可以安装在Adobe Experience Manager 6.5顶部。

[!DNL Adobe Experience Manager] 6.5.5.0中引入的一些主要功能和增强功能包括：

* 不允许匿名访问CRXDE Lite。 相反，用户将被定向到登录屏幕。 请参阅[使用CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)进行开发。

* 自定义在[!DNL Adobe Experience Manager]收件箱中显示的列名。

* 改进了Experience Manager Web内容管理(WCM)中各个区域（如页面编辑器、核心组件、RTE和管理员用户界面）的辅助功能。

* 将[!DNL Interactive Communication]另存为草稿。

* 支持[!DNL Oracle WebLogic 12]在JEE上Experience ManagerForms。

* 改进了[!DNL Adobe Experience Manager Assets]用户界面流中的异常处理。

* 要获取Dynamic Media Scene7的发布URL，将新方法`getRemoteAssetPublishURL`添加到`com.day.cq.dam.api.s7dam.scene7.ImageUrlApi`接口。

* [辅助](#assets-6550) 功能 [!DNL Adobe Experience Manager Assets] 增强符合Web内容辅助功能准则(WCAG)。

* 从Adobe Experience Manager中删除了包共享集成。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.3。

有关完整列表Adobe Experience Manager 6.5 Service Pack 5中引入的功能、主要亮点和主要功能，请参阅[Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md)中的新增功能。

以下是[!DNL Experience Manager] 6.5.5.0版中提供的修复程序的列表。

### [!DNL Sites] {#sites-6550}

* Experience Manager站点提供了一个选项，用于发布或取消发布别名中的页面。 此选项无效(NPR-33415)。
* 从包含多个模板的模板中删除布局容器时，该模板无法正确呈现(NPR-33347)。
* 当“Experience Manager站点”页面是包含多个Live Copy的大型内容集的一部分时，无法加载页面版本历史预览(NPR-33311)。
* 使用“移动”命令重命名“Experience Manager站点”页面时，页面标题不会更新(NPR-33264)。
* 在列视图中移动页面时，列会消失(NPR-33216)。
* 当语言副本中的本地组件名称与Blueprint中的组件名称相同并且从Blueprint中转出该组件时，术语`_msm_moved`不会添加到本地组件的名称(NPR-33208)。
* 页面重定向servlet将.html附加到ResourceType不是`cq:Page`(NPR-33176)的Experience Manager站点URL。
* 粘贴子树时，没有选项可决定是否粘贴相应的子页面(NPR-33149)。
* 组件实时使用的结果数限制为第49个(NPR-33058)。
* 当您将内容片段基于模式并且它包含强制文本区域或路径字段时，内容片段无法保存(NPR-33007)。
* 当您使用默认的体验片段组件创建自定义组件并在Experience Manager站点页面中使用它时，Experience Manager不会显示自定义组件的引用（使用）(NPR-32852)。
* 重命名包含大量引用的文件夹时，不会更新对该文件夹的许多引用(NPR-32765)。
* 启用源代码编辑选项后，它对内嵌的全屏选项可用，但富文本编辑器的编辑对话框和全屏选项仍然缺失(NPR-32763)。
* 如果您有多个字段，并且它在Blueprint的页面属性中包含必填字段（如下拉列表或路径字段），则当转出包含此多字段的页面时，不会保存Live Copy的页面属性(NPR-32751)。
* 屏幕阅读器无法使用标题结构来导航页面。 此外，“组件”选项卡的标签错误(NPR-32648)。
* 分页开始时，Experience Fragments选取器不会加载所有项目(NPR-32605)。
* 撤消读取、修改、创建和删除Live Copy的作者权限。 每个作者都必须明确提供读取和修改权限才能在Blueprint中移动页面(NPR-32550)。
* 内容作者无法为与Adobe Analytics集成的页面创建Launch(NPR-32548)。
* 当用户通过同步恢复继承时，父页面的Live Copy不会与Blueprint同步，并显示不正确的状态(NPR-32500)。
* Experience Manager站点编辑器页面加载时间超过15秒(NPR-32413)。
* 某些字段不显示“取消继承”选项(NPR-32362)。
* 当您为体验片段组件选择路径并选中打开选择对话框复选框时，您不会导航到路径浏览器中的选定路径(NPR-32308)。
* 从Experience Manager 6.2升级到Experience Manager 6.5时，静态模板的Parsys组件显示不正确。 Parsys组件的高度设置为0且其内部的组件不可见(NPR-33663)。
* 当用户复制并粘贴同一页面上的布局容器时，布局容器中的组件不会显示(NPR-33648)。
* 调度程序运行状况检查在日志文件中显示`Invalid cookie header`警告消息(NPR-33629)。
* PreferencesServlet中反射的XSS(NPR-33438)。
* 匿名用户可以访问CRXDE Lite功能(GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>建议[!DNL Experience Manager desktop app]的Windows用户升级到[桌面应用程序版本2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added)以访问[!DNL Adobe Experience Manager 6.5.5.0]实例上的DAM存储库。 因为他们在使用桌面应用程序版本2.0.2访问[!DNL Adobe Experience Manager] 6.5.5.0实例上的DAM存储库时可能会遇到问题。

**Experience Manager资源中的辅助功能增强**

* 现在，可以将键盘焦点放在[!UICONTROL Comments]列表上，并可单击选项放在[!UICONTROL 在[!UICONTROL Timeline]资产面板(NPR-33424)下的[!UICONTROL Create]版本注释下。]

* 现在，可以访问[!UICONTROL 视图设置]选项，并使用键盘键更改[!UICONTROL 视图设置]对话框中的设置(NPR-33420)。

* 组合框的列表框弹出窗口（在不同页面上的各个字段中）现在将条目显示为可由屏幕阅读器宣布的选项的列表(NPR-33516)。

* 现在，屏幕阅读器宣布了可排序标题的排序功能(在列表视图中，[!UICONTROL 时间轴]视图和[!UICONTROL 管理出版物]页)，并且列标题的排序控件可通过键盘访问(NPR-32979)。

* 诸如注释卡、版本更新、组合框和菜单的V形图标等可单击元素现在可以使用键盘进行聚焦并与之交互(NPR-33514)。

* 现在，屏幕阅读器正确宣布了[!UICONTROL 分析视图]上的分析图标（用于使用、展示和点击）的功能（或操作目的）(NPR-33513)。

* 只读表单字段（例如，资产[!UICONTROL 属性]的“基本”选项卡]上禁用的字段）现在可使用键盘(NPR-33493, CQ-4273031)聚焦。[!UICONTROL 

* 各种输入字段中的标签现在是永久标签（因此可访问），而不仅仅是占位符标签，在输入文本时它们会消失(NPR-33475)。

* 对于屏幕阅读器用户，不同的标题级别（如页面标题和章节标题）现在被视为具有不同级别的标题(NPR-33471)。

* 现在，可使用键盘(NPR-33468、CQ-4271412)访问交互式用户界面元素，如链接和选项（位于资产页面的标题和缩放选项、文件夹导航）。

* 、[!UICONTROL 范围]和[!UICONTROL 管理出版物]页面上的工作流进度指示器现在由屏幕阅读器正确读出，作为进度指示器，而不是标签(NPR-33416)。

* 对星级图标的颜色(如资产[!UICONTROL 属性]中[!UICONTROL 高级]选项卡的[!UICONTROL Rating]部分或卡视图中)进行更改，以使视力有限且无颜色感知的用户能够看到合适的对比度(NPR-33414)。

* 现在，可使用键盘键访问资产详细信息页面上的[!UICONTROL Comment]字段旁边的V形向上箭头(NPR-33397)。

* 现在，屏幕阅读器(NPR-33396)正确地宣布了资产[!UICONTROL 属性]和左边栏导航（在资产用户界面上）上的[!UICONTROL 标记]对话框的展开和折叠状态。

* [!DNL Adobe Experience Manager]资产上所有已浏览页面的标题现在是唯一的(NPR-33343)。

* 当导航树结构时，屏幕阅读器现在正确地宣布了树视图控件的各个元素(NPR-33304)。

* 现在，可使用键盘键访问资产详细信息页面上[!UICONTROL 时间轴]视图中不同版本的资产(NPR-33283)。

* 使用搜索功能时，屏幕阅读器现在会宣布显示在“Omnisearch”组合框中的搜索建议的名称(NPR-33280)。

* 屏幕阅读器现在将[!UICONTROL 引用边栏]中的可单击元素和[!UICONTROL 转到链接]作为可单击元素(NPR-33278)。

* 屏幕阅读器在打开对话框时不再宣布[!UICONTROL 共享链接]对话框的表结构信息（如行1、单元格1、表）(NPR-33268)。

* 屏幕阅读器(NPR-33235)现在正确宣布了各种组合框元素的用途（如“路径”字段以及在“资产属性”的“基本”选项卡中打开“选择”对话框的选项）。

* 现在，当键盘焦点在列表视图表中时，向屏幕阅读器用户传递可选择的行信息。 当指针悬停在行上时，屏幕阅读器会宣布该信息(NPR-33234)。

* 现在，屏幕阅读器可访问用于删除[!UICONTROL 属性]的[!UICONTROL 基本]选项卡中标签]字段下的[!UICONTROL 标签字段下各个选定标签的选项([!UICONTROL x])(NPR-33206)。

* 日历日期选取器现在可通过屏幕阅读器用户和视力正常的键盘用户使用键盘来获得焦点，并具有可操作性(NPR-33200)。

* 切换到在列表视图和卡视图之间切换的切换现在可将其功能(调整视图)正确显示给屏幕阅读器(NPR-33069)。

* 现在可访问左边栏中的菜单。 屏幕阅读器(NPR-33068)相应地宣布了扩展菜单的功能和目的。

* 列表框和许多其他用户界面元素现在对失明的屏幕阅读器用户可访问，屏幕阅读器会宣布有关它们的以下信息(NPR-33040):

   * 在提交表单之前，是否需要对元素进行用户输入。
   * 元素是否不可编辑。
   * 是否选择了Widget。

* 现在可以使用键盘(NPR-32842、CQ-4273018)访问打开过滤器边栏的选项。

* 现在可以访问列表视图列标题中的复选框控件，屏幕阅读器(NPR-32722、NPR-33005)会宣布使用该控件的目的。

* 日历日期选取器中小时(HH)和分钟(mm)字段的标签现在是永久标签而不是占位符标签，当用户在这些字段中输入文本时不会消失(NPR-32720)。

* 通知的链接文本（在单击铃图标后显示）现在会向屏幕阅读器用户宣布，这些用户使用Tab键访问每个链接(NPR-32645)。

* [!UICONTROL 现在]，可 [!UICONTROL 以使用键]盘访 [!UICONTROL 问Asset Card中的Adobe Insights  Vieware中的Select、Download]    、Properties和More Actions选项(NPR-32609)。

* 使用键盘访问时，屏幕阅读器不再宣布以可视方式隐藏的内容（如搜索结果上标题菜单栏的内容）(NPR-32606)。

* 屏幕阅读器现在宣布，控件上标签用于移动到日历日期选取器中的下一个和上一个月(NPR-32604)。

* 星级图标现在可使用键盘键(NPR-32513)获得焦点并具有操作性。

* 控制视频音量的功能现在可通过选项卡（聚焦于音量滑块）和键盘上的箭头键（调整音量）(NPR-32065)访问。

* “文件大小”过滤器的下界([!UICONTROL From])和上界([!UICONTROL To])输入字段的目的现在已向失明屏幕阅读器用户(NPR-32064)宣布。

* 现在，在浏览模式下，屏幕阅读器可以访问[!UICONTROL 创建和翻译]表单中的[!UICONTROL 语言]菜单(CQ-4293906)。

* [!UICONTROL 引用]面板现在可通过以下增强功能(NPR-33261、CQ-4293798)访问：

   * 在浏览模式下，屏幕阅读器焦点不再移动到[!UICONTROL Site References]、[!UICONTROL Asset References]、[!UICONTROL Copys]和[!UICONTROL Form References]部分下隐藏的多行编辑字段。

   * 屏幕阅读器现在宣布[!UICONTROL 站点引用]和[!UICONTROL 语言副本]元素的角色。

   * 浏览模式下屏幕阅读器的焦点以有意义的顺序转移到各种元素。

* [!UICONTROL 元模式] 编辑器页面及其元素现在可使用键盘访问，并且屏幕阅读器友好(CQ-4290962、CQ-4272953)。

* `X`符号删除选定标记的目的现在由屏幕阅读器和选定标记的数量一起宣布(CQ-4273017)。

* 为避免使用屏幕阅读器的失明用户产生混淆，屏幕阅读器现在会忽略装饰性图标和图像(CQ-4272944)。

**Experience Manager资产中已修复的问题**

[!DNL Adobe Experience Manager] 6.5.5.0资产修复了以下问题：

* [!UICONTROL 集] 合中 [!UICONTROL 资] 源的“创建工作流”对话框的“启动”处于禁用状态，因而阻止触发工作流(NPR-32471)。

* 在元数据模式中使用级联弹出窗口时，在选择和保存包含撇号（从子项下拉框中）的下拉选项时，在重新打开资产[!UICONTROL 属性](NPR-32649)后，选定撇号选项会消失。

* [!UICONTROL 资产分析同] 步如果遇到无效条目（在Analytics端）而不是转到下一个条目(NPR-32674)，则作业停止并失败。

* 陀螺仪不能正常工作，因为在全景查看器(CQ-4272937)中，默认情况下，移动浏览器上会禁用运动传感器。

* [!UICONTROL 在6.5] .1(NPR-32730)上安装6.5.3时，“已连接资产配置向导”无法处理404错误。

* 在XMP写回过程中，所有自定义命名空间元数据属性都将自定义命名空间前缀更改为ns2，而不是配置的命名空间前缀(NPR-32748)。

* 不会触发延迟加载，选择查看通知收件箱中的任务时只显示100个资源(NPR-32750)。

* `NullPointerException` 由于新创建的用户用户档案(SAML/SSO)中缺少节点首选项，观察到。此错误会阻止新登录的用户使用[!DNL Adobe Experience Manager Stock]集成(NPR-32777)。

* 在打开包含超过10,000个资源(NPR-32980)的智能集合时，会在日志中观察到遍历警告。

* 在[!DNL Adobe Experience Manager]中，使用Dynamic Media Scene7运行模式(NPR-32995)将资源从一个文件夹移动到另一个文件夹时，资源名称将更改为小写。

* 在从搜索结果导航到其属性，然后返回到搜索结果以删除已搜索的资产后，无法删除已搜索的资产(NPR-32998)。

* [!UICONTROL 在] Move Assetsinterface(NPR-33356)中选择目标文 [!UICONTROL 件] 夹时，Nextoption仍处于禁用状态。

* [!UICONTROL 在选] 择父节点（其中显示单个子文件夹），然后选择子文件夹(NPR-33275)时，不启用“下一步”。

* 对于具有删除权限的用户，即使已授予读取、创建或修改等其他权限，Adobe资产链接(AAL)上也会禁用登记和注销权限(NPR-33272)。

* “智能裁剪”演绎版在资产下载对话框中不可用(NPR-33167)。

* 在具有智能裁剪用户档案的文件夹下打开PDF的演绎版边栏时，日志中会出现异常(CQ-4294201)。

* 如果在与Dynamic Media Scene7运行模式(CQ-4294200)进行Experience Manager时，默认情况下禁用[!UICONTROL Dynamic Media同步模式]，则不发布图像预设。

* 批量上传时的资产处理会卡住，而工作流实例会显示DAM更新资产的卡住实例(CQ-4293916)。

* 在Experience Manager上创建Dynamic Media配置有效，但在用户界面上，选择“保存”(CQ-4292442)时不会发生任何情况。

* 预览F4V视频资源在Safari/Mac上的渐进式播放中无法正常播放(CQ-4289844)。

* 在智能裁剪父文件夹中的资产时会创建额外的文件夹，父文件夹的名称中带有点`.`字符(CQ-4289337)。

* 缩览图会损坏，并且复制视频时不会显示视频处理横幅(CQ-4284125)。

* 对于相机视图为空的某些型号，Dimension查看器在Firefox中错误地显示了空缩览图(CQ-4283447)。

* 在6.5.5.0中修复的性能问题包括(CQ-4279206):

   * 将大型二进制文件上传到Dynamic Media图像处理服务器需要太长时间。

   * 由于Dynamic Media Scene7架构，Experience Manager的缩览图生成时间增加。

* Dynamic Media Scene7迁移问题对于拥有大量资源的客户失败(CQ-4279206)。

* 如果使用`setVideo`，则视频360查看器的布局将被破坏，并且视频使用`video= modifier`(CQ-4263201)时向下移动。

* 安装Experience Manager SDL包时显示错误消息(NPR-33175)。

* SSRF在Experience Manager中的漏洞(NPR-33435)。

### 平台 {#platform-6550}

* 如果在`/etc/maps`下创建`sling:match`映射条目(NPR-33362)，则不调用[!DNL Sling]筛选器。
* Experience Manager因[!DNL Apache Lucene]的分段故障而崩溃(NPR-32988)。
* [!DNL Jackson] Experience Manager uberjar文件中缺少核心包(NPR-32848)。
* CRXDE Lite不为没有节点`jcr:primaryType`属性读取权限的用户加载内容(NPR-32611)。
* [!DNL Granite] 维护任务调度程序在Experience Manager部署期间重新初始化过频繁(CQ-4294627)。
* 当SQL查询执行较长时间（例如7小时）时，Experience Manager停止响应(NPR-33044)。

### 用户界面 {#ui-6550}

* 多字段中不保留单选按钮选择(NPR-33309)。
* 延迟加载限制对列表视图(NPR-33124)无效。
* 如果没有匹配项，则搜索结果页面不显示消息(NPR-32974)。
* Omnisearch过滤器将返回`/content`节点下的所有匹配项，忽略选定的位置(NPR-32849)。

### 集成 {#integrations-6550}

* 当发布包含Adobe Target组件的页面时，将清除内部缓存(NPR-33162)。
* 与Adobe Target的集成在[!DNL Windows Internet Explorer] 11(NPR-33111)上不起作用。
* 配置Adobe Target时，在选择报告源时，[!UICONTROL 公司]和[!UICONTROL 报表包]字段不显示(NPR-32502)。
* 使用[!DNL Adobe I/O]导出[!DNL Experience Fragments]时，源产品等元数据不会导出到Adobe Target(NPR-32159)。
* 本地Experience Manager管理组中的授权IMS用户无法创建或修改IMS配置(NPR-33045)。
* Adobe启动配置页面不显示所有记录(NPR-33011)。
* 由于JavaScript错误(NPR-32996)，内容作者组中的用户无法编辑Adobe Target组件的属性。
* JSON的跨站点脚本(NPR-32744)。

### 翻译项目 {#translation-6550}

* 译文标记不会从第三方翻译服务(NPR-33154)导入Experience Manager。
* 翻译配置页显示的翻译提供程序与用于翻译的翻译提供程序(NPR-32971)不正确。
* 将体验片段文件夹添加到现有翻译项目会创建新项目(NPR-32843)。
* 运行转换作业时的日志中出现`NullPointerException`错误(NPR-32628)。

### WCM {#wcm-6550}

* 页面编辑器 — [!DNL Sites]页面编辑器不允许仅键盘用户跳到主内容，而不是在标题(CQ-4293883)中所有可用选项之间切换选项卡焦点。
* 页面编辑器 — 由于[!DNL Chrome]和[!DNL Firefox]版本(CQ-4292995)中的更新，使用Well组件并包含已保存数据的面板不显示。
* MSM — 从页面中删除组件不会从页面的已发布版本中删除组件(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* 从[!DNL Brand Portal]中删除已发布的元数据模式会导致错误(CQ-4292063)。
* 如果管理员通过Adobe Developer Console使用Brand Portal配置[!DNL Experience Manager Assets] 6.5.4，则[!DNL Brand Portal]用户无法将贡献文件夹的资产从[!DNL Brand Portal]发布到[!DNL Experience Manager](NPR-33046)。
* 重复复制父文件夹会导致冲突(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* 无法使用“快速编辑”菜单选项(NPR-33117)在审核控制台中删除信息卡。
* 访问[!UICONTROL 活动流]页面时出错(NPR-33146)。
* 在作者实例上删除的组不会从所有发布实例中删除(NPR-33199)。
* 创建新组后，作者不会被重定向到[!DNL Internet Explorer] 11(NPR-33205)上的[!UICONTROL 社区组]部分。
* 在“Experience Manager收件箱”中访问消息不会将消息的状态更改为“已读”(NPR-32764)。
* 编辑[!DNL Communities]组并更改缩略图图像不会更新组缩略图图像(NPR-32599)。
* 用户无法向社区中的其他用户发送电子邮件(NPR-32598)。
* 在用户刷新页面(NPR-32391)之前，不会显示已提交的博客。
* 在创建用户生成内容(UGC)的通知和订阅版本时，会存储源页面的不正确ID(CQ-4279355、CQ-4289703)。
* 跨站点脚本问题(NPR-33203)。

### 工作流 {#workflow-6550}

* 左边栏中的[!UICONTROL 时间轴]选项加载的时间比预期的要长(NPR-32851)。
* 重新启动Experience Manager实例后，集合的审阅任务的电子邮件包含不正确的有效负荷链接(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack不包含[!DNL Forms]的修复。 它们是通过单独的 Forms 附加组件包交付的。此外，发布了一个累计安装程序，其中包含 JEE 上对 AEM Forms 的修复。有关详细信息，请参阅[安装Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)上安装Experience Manager Forms。

* 通信管理：在目标区的资产顺序在提交信(NPR-33359、NPR-33153)后混乱。
* 自适应Forms:当用户编辑自适应表单时，[!UICONTROL 页面信息]菜单中可用的[!UICONTROL 开始工作流]选项不起作用(NPR-33004)。
* 自适应Forms:用户无法保存包含多个附件的自适应表单(NPR-32997)。
* 自适应Forms:在自适应表单中更改面板布局会导致错误(CQ-4293880)。
* 自适应Forms:自适应表单词典中字符串的新行将`&#xa;`字符添加到词典(NPR-33266)。
* 自适应Forms辅助功能：当用户将自适应表单预览为HTML表单时，[!UICONTROL “涂抹签名”]字段无法保留制表符焦点(NPR-33159)。
* 自适应Forms辅助功能：提交自适应表单时显示的错误消息不链接到`aria-describedBy`属性(NPR-33071)。
* 自适应Forms辅助功能：在ARIA辅助功能模式(NPR-33070)中，在自适应表单中标记为必填的字段没有将强制属性设置为True。
* PDFG服务：当用户将文本文件转换为PDF时，日文字符无法正确呈现(NPR-33238)。
* PDFG服务：`CreatePDF`操作无法将PDF文件转换为PDF OCR格式(NPR-32994)。
* PDFG服务：对于[!DNL OpenOffice]文档的第200个实例，PDF转换失败(NPR-32766)。
* 后端集成：由于不正确的非活动状态(NPR-33169)，表单数据模型请求在刷新令牌过期时失败。
* 设计人员：屏幕阅读器根据默认的地理顺序而不是XDP文件(NPR-32160)中定义的自定义跳位顺序执行跳位顺序。
* 设计人员：如果启用了标记选项，子表单边框将消失在生成的PDF输出中(NPR-32778)。
* 使用GuideSOMProviderServlet存储XSS(NPR-32700)。

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0是重要更新，包括新功能、关键客户请求的增强和性能、稳定性、安全性改进，自2019年4月&#x200B;**发布6.5版以来发布。**&#x200B;它可以安装在Adobe Experience Manager 6.5顶部。

Adobe Experience Manager 6.5.4.0中引入的一些主要功能和增强功能包括：

* Adobe Experience Manager Assets现在通过[!DNL Adobe I/O]控制台配置了Brand Portal。

* 现在，新的[生成可打印输出](../forms/using/aem-forms-workflow-step-reference.md)步骤可用于Adobe Experience Manager Forms工作流。

* [支持自适应](../forms/using/resize-using-layout-mode.md) 表单和交互式通信的布局模式的多列。

* 支持HTML5表单中的[富文本](../forms/using/designing-form-template.md)。

* [可访问](new-features-latest-service-pack.md#accessibility-enhancements) 性增强了Experience Manager资源。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.8。

* 您现在可以将选择性内容子树同步到&#x200B;*Dynamic Media - Scene7 mode*，而不是所有`content/dam`中的可用模式。

* 与SOAP Web服务的表单数据模型集成现在支持元素上的选择组或属性。

* SOAP输入或输出以及复杂的数据结构现在支持动态组替换。

有关最新Service Pack中引入的功能和主要亮点的完整列表，请参阅[Adobe Experience Manager 6.5 Service Pack的新增功能](new-features-latest-service-pack.md)。

### 站点 {#sites-fixes}

* 当Adobe Experience Manager Sites页面的URL包含冒号(`:`)或百分比符号(`%`)时，浏览器会停止响应，CPU使用尖峰(NPR-32369, NPR-31918)。

* 当打开“Experience Manager站点”页面进行编辑并复制组件时，某些占位符(NPR-32317)仍无法使用粘贴操作。

* 打开管理发布向导后，链接到核心组件的体验片段不会显示在已发布引用的列表中(NPR-32233)。

* Touch UI中的Live Copy概述比经典UI渲染所花费的时间要长得多(NPR-32149)。

* 当服务器时间和计算机时间位于不同时区时，计划发布时间在触屏UI中显示服务器时间，而在经典UI中显示计算机时间(NPR-32077)。

* Experience Manager站点无法打开URL中带后缀的页面(NPR-32072)。

* 当用户编辑内容片段时，内容片段的已删除变体会恢复(NPR-32062)。

* 允许用户保存内容片段，而无需在必填字段中提供任何信息(NPR-31988)。

* kernel.js和ui.js未预先编译或缓存。 这会导致在渲染页面中增加时间(NPR-31891)。

* 启用PageEventAuditListener时，提交队列的长度会增加。 它影响许多操作的性能，如批量发布、导航、批量资产移动(NPR-31890)。

* 拖动体验片段时，会观察到较高的响应时间(NPR-31878)。

* 当您在响应式网格的占位符中选择将组件拖动到此处选项时，将发送GET请求，并且该请求会导致HTTP 403错误(NPR-31845)。

* 在同一文件夹中移动内容时，会禁用页面移动选项(NPR-31840)。

* 在可编辑的模板结构模式下，布局容器中允许的组件列表显示不正确的结果。 布局容器中仅显示具有设计对话框的组件(NPR-31816)。

* 当页面对用户具有只读权限时，“打开属性”选项在sites.html中可见，但在editor.html中不可见(NPR-31770)。

* 当用户单击“创建”按钮时，页面选项不可用(NPR-31756)。

* 无法同步包含OOTB（现成）设计导入程序组件(NPR-31728)的Adobe活动中的活动。

* 当您尝试将项目符号列表更改为编号列表时，仅更改列表的前两个项(NPR-31636)。

* 在未创作页面且选择了子节点时，选择对话框仍显示初始节点。 创作页面并用户单击浏览时，页面会重定向到根节点，而不是创作的节点(NPR-31618)。

* “视图配置”对话框无法正常用于收件箱自定义工作流功能(NPR-32503和NPR-32492)。

* 当使用收件箱(CQ-4282168)查看工作流信息时，显示错误消息。

### 资产 {#assets-6540-enhancements}

* 资产收集页面上用于触发工作流的按钮被禁用(NPR-32471)。

* 在使用Dynamic Media Scene7配置(NPR-32440)Experience Manager将资源从一个文件夹移动到另一个文件夹时，将在SPS(Scene7 Publishing System)中创建无名称的文件夹。

* 将所有资产（使用全选，然后移动）移动到包含已发布资产的文件夹的操作会失败，并出现错误(NPR-32366)。

* 为${extension}的资产生成再现失败(NPR-32294)。

* 版本历史记录URL显示在资产属性页面的“引用者”字段下(NPR-31889)。

* 无法使用WinZip(NPR-32293)打开从DAM下载的ZIP文件。

* 打开“文件夹设置”以更改文件夹标题或缩略图图像，然后保存时，将更新文件夹的原始权限(NPR-32292)。

* 计划激活的日历图标不会显示在“状态”列（DAM资产列表的经典UI中）中，该激活的资产将安排在以后的日期和时间(NPR-32291)。

* 使用片段模板创建片段在片段创建过程中搜索集合时出错(NPR-32290)。

* 当从搜索筛选器中选择多个标签时，将触发多个搜索查询(NPR-32143)。

* Experience Manager资产在上传文件名超过50个字符的资产时，用户界面会显示截断的文件名(NPR-32054)。

* 当选中Adobe Stock中复选框树的级别2复选框时，清除“滤镜”面板中的所有复选框时，清除第一个复选框和第二个复选框时，清除这些复选框(NPR-31919)。

* 使用Omnisearch彩块化的文件和文件夹搜索会出现异常(NPR-31872)。

* 即使在相应的元数据模式表单中设置依赖关系规则时选择必填字段后，也不会删除元数据编辑器中强制字段选择的字段突出显示(NPR-31834)。

* 叶级标记的完整名称（来自标记层次结构）不会显示在资产属性页面(NPR-31820)中。

* 在Safari浏览器上使用资源属性页面中的返回命令时出错(NPR-31753)。

* 触屏UI搜索（通过Omnisearch完成）结果页会自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* PDF资产的资产详细信息页面不显示操作按钮，但Dynamic Media Scene7运行模式(CQ-4286705)上运行的Experience Manager中的“收藏”和“添加演绎版”按钮除外。

* 通过Scene7(CQ-4286445)的批量上传流程处理资产需要太长的时间。

* 当用户未在Dynamic Media Client(CQ-4285690)中的“设置编辑器”中进行任何更改时，“保存”按钮不会导入“远程集”。

* 当支持的3D模型被引入Experience Manager(CQ-4283701)时，3D资产缩览图不会提供信息。

* 智能裁剪视频查看器预设的未处理状态会在横幅文本中与预设名称一起显示两次(CQ-4283517)。

* 资产的详细信息页面(CQ-4283309)上会观察到在3D查看器中预览的已上传3D模型的容器高度不正确。

* 在Experience Manager Dynamic Media混合模式(CQ-4255590)上，传送编辑器未在IE 11中打开。

* 键盘焦点卡在Chrome和Safari浏览器(NPR-32067)中“下载”对话框的“电子邮件”下拉框中。

* 在尝试在Experience Manager上添加DM云配置(CQ-4288533)时，默认情况下未启用“同步所有内容”复选框。

### 基础UI {#foundation-ui-6540}

* 使用“筛选器”面板搜索资产时，鼠标控件会切换到上一个筛选器字段，而不是停留在现有筛选器字段中(NPR-32538)。

* 平台标记：通过在标记字段中键入内容来搜索标记会显示根边界以外的标记，并且不会尊重标记字段的`rootPath`属性(NPR-31895)。

* 平台UI:如果在文本字段中添加了无效的路径，则路径浏览器将断开(NPR-31884)。

* 选择页面时，通知隐藏在粘滞菜单后面(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)下划线替换URL路径部分的冒号(NPR-32231)。

### 项目 {#projects-6540}

* 即使用户有权在子文件夹中创建项目，用户也看不到“创建”按钮(NPR-31832)。

### 项目翻译{#projects-translation-6540}

* 在`Apache Sling JSP Script Handler`(NPR-32154)中激活“裁切空间”选项时，创建翻译项目会中断UI。

* 将任何要翻译的标记添加到翻译项目时，在UI中出现错误，错误日志中出现空点异常(NPR-31896)。

### 集成 {#integrations-6540}

* 启动库URL生成仅基于启动API中的`path`和`library_name`值，而不基于`library_path`值(NPR-31550)。

* 处理LiveFyre相关项目(FYR-12420)时显示错误消息。

* ReportSuitesServlet 容易遭受服务器端请求伪造 (SSRF) 攻击 (NPR-32156)。

### WCM模板编辑器{#wcm-template-editor-6540}

* 在可编辑的模板结构模式下，布局容器中允许的组件列表不显示链接按钮组件(CQ-4282099)。

### WCM页面编辑器{#wcm-page-editor-6540}

* 选择叠加，然后选择响应式网格将组件拖动到此处时会出现错误(CQ-4283342)。

### 营销活动定位 {#campaign-targeting-6540}

* 目标云配置失败，错误get mboxes请求失败(CQ-4279880)。

### Brand Portal {#assets-brand-portal-6540}

* 在升级到Experience Manager 6.5.4(CQDOC-15655)上的[!DNL Adobe I/O]时，Brand Portal用户无法将贡献文件夹资产发布到[!DNL Assets]。 要立即修复Experience Manager 6.5.4，建议[下载修补程序](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041)并安装在创作实例上。

* 元数据模式弹出窗口值在资产属性中不可见(CQ-4283287)。

* 元数据子架构不显示基于资产属性(CQ-4283288)中的mimetype的选项卡。

* 取消发布元数据模式会填充错误消息，尽管在后端删除了模式。

* 预览图像不显示于已发布的资产(CQ-4285886)。

* 用户无法发布或取消发布名称中包含单报价的资产(CQ-4272686)。

* 下载多个资产(CQ-4281224)时不显示条款和条件。

* 已解决小的安全漏洞。

### 社区 {#communities-6540}

* “创建成员”表单显示为空白页(NPR-31997)。

* 用户无法视图有关作者实例的Analytics报告(NPR-30913)。

### Oak — 索引和查询{#oak-indexing-6540}

* 使用Tika分析器分析时，包含JPEG图像的MS Word和MS Excel文档无法分析，并且发现类未找到错误(NPR-31952)。

### 表单 {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack不包含针对Experience Manager Forms的修复。 它们是通过单独的 Forms 附加组件包交付的。此外，还发布了一个累积安装程序，其中包含针对JEE上的Adobe Experience Manager Forms的修复。 有关详细信息，请参阅[安装Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)上安装Experience Manager Forms。

* 通信管理：在提交到后处理工作流(NPR-32626)后，字母会显示额外的字符。

* 通信管理：在提交到后处理工作流(NPR-32539)后，字母将下拉占位符显示为文本组件。

* 通信管理：在字母模板中定义的默认值不会在预览模式下显示(NPR-32511)。

* 移动Forms:在以HTML版本(NPR-32514)呈现XDP表单时，“提交”按钮显示为扩展大小。

* 文档服务：应用Service Pack 2后，Letter和某些其他页面的URL访问问题(NPR-32508、NPR-32509)。

* 文档服务：如果服务器上的事务数超过特定限制，则HTML到PDF的转换失败，并且从[!DNL Forms]服务器(NPR-32204)中删除文件类型设置。

* 自适应Forms:浏览器辅助工具根据WCAG2 Level AA准则(NPR-32312、NPR-32309、CQ-4285439)报告自适应表单中的故障。

* 自适应Forms:Chrome浏览器辅助工具报告了最佳实践失败(NPR-32310)。

* 自适应Forms:配置嵌入到“Experience Manager站点”页面的自适应表单时的翻译问题(NPR-32168)。

* 工作台：使用“为PDF实用程序获取PDF属性”操作服务(NPR-32150)时，显示错误消息。

* 文档安全：如果将DisableGlobalOfflineSynchronizationData选项设置为True(NPR-32078)，则受保护的PDF文件无法脱机打开。

* 设计人员：如果启用了标记选项，子表单边框将消失在生成的PDF输出中(NPR-32547、NPR-31983、NPR-31950)。

* 设计人员：如果表中存在合并的单元格，则使用输出服务(CQ-4285372)从XDP表单转换的输出PDF文件的辅助功能测试将失败。

* JEE基金会：如果Experience Manager Forms服务器与群集断开连接，缓存问题会阻止它重新连接到服务器(NPR-32412)。

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0是一个重要版本，包括自2019年4月6.5版本正式发布以来发布的性能、稳定性、安全性以及重要客户修复和 **增强功能**。它可以安装在[!DNL Adobe Experience Manager] 6.5的顶部。

此Service Pack版本的一些关键亮点是：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.6。

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档。

* 在DAM列表视图中以及在列表视图中对资产搜索结果添加了可排序的创建日期新列。

* 已在“列表”视图中启用基于“名称”列的资产排序。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。Smart Crop是一项机器学习驱动的功能，可在移动帧以跟随场景焦点的同时重新裁剪视频。

* [!DNL Dynamic Media] 支持智能成像。

* 能够在[!DNL Experience Manager]工作流中设置“Out of Office”（外出）首选项。[](../forms/using/configure-out-of-office-settings.md)

* 能与[!DNL Experience Manager]工作流中的其他用户共享收件箱或收件箱项目](../forms/using/configure-shared-queues-osgi.md)。[

* [以批处理模式](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)生成交互通信的功能。

* 捆绑在ContextHub中的jQuery的更新版本为3.4.1。

### 资产 {#assets-6530-enhancements}

**产品增强功能**

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法(NPR-27573)创建的ZIP存档。

* 在DAM列表视图中，将为创建日期添加新列（可排序），并在列表视图中的资产搜索结果中添加该列(NPR-31312)。

* 在列表视图中，用户可以使用[!UICONTROL Name]列(NPR-31299)对资产的列表进行排序。

* GLB、GLTF、OBJ和STL文件可在DAM的[!UICONTROL 资产详细信息]页中预览(CQ-4282277)。

* `ReplicationOnModifyListener` 事件在(CQ-4281279)中块上传期间为 [!DNL Dynamic Media] 块节点触发。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。Smart Crop是一项机器学习驱动的功能，可在移动帧以跟踪场景焦点时重新裁剪视频(CQ-4278995)。

* [!DNL Dynamic Media] 支持智能成像(CQ-4222249)。

* 如果在请求中传递了视图参数，则搜索或浏览查询将设置为Foundation选取器中的默认视图(NPR-31601)。

**修复**

* 某些PDF文档的元数据在标题被修改时不会更新并保存到PDF中(NPR-31629)。

* 对于文件名(NPR-31547)中带有加号(`+`)的资产，资产共享不起作用。

* 在默认搜索表单“资产管理搜索边栏”中进行的编辑无法按预期方式工作(NPR-31502)。

* 在资产视图中使用Omnisearch搜索搜索搜索资产时，不会显示建议(NPR-31496)。

* 当引用的资产被移动到其他位置时，收藏集中的资产引用不会更新，在这些情况下，不同用户引用的收藏集也会相同(NPR-31486)。

* 重复 IPTC标记会添加到资产元数据(NPR-31328)。

* 当从过滤器边栏触发搜索时，搜索结果计数不能准确更新(NPR-31316)。

* 取消选择“文件类型”过滤器中的二级复选框时，所有复选框都会被清除，并且搜索栏中的文本与选定或取消选择的属性(NPR-31287)不同步。

* 不能从文件夹的“成员”部分删除所有成员（用户/用户组）；在尝试删除所有用户时，已登录用户将添加到列表(NPR-31171)。

* 无法删除文件名中带有加号(`+`)的资源(NPR-31162)。

* “创建”下拉菜单（在选择文件夹时显示在顶部菜单中）不显示“文件夹”作为创建选项(NPR-30877)。

* 当对用户应用路径上拒绝`jcr:removeChildNodes`和`jcr:removeNode`的ACL时，缺少文件夹选择“创建”>“FileUpload”操作项(NPR-30840)。

* 上传某些mp4资源时，DAM工作流将进入陈旧状态，导致所有其余工作流进入陈旧状态(NPR-30662)。

* 当将大型PDF文件（数GB）上传到DAM并处理其子资源时，会出现内存不足错误(NPR-30614)。

* 资产的批量移动失败并显示警告消息(NPR-30610)。

* 在[!DNL Dynamic Media]-Scene7模式(NPR-31630)下运行的[!DNL Experience Manager]中，将资产从一个文件夹移动到另一个文件夹时，资产名称将更改为小写字母。

* 编辑远程图像集时，对于与Scene7公司名称(NPR-31340)相同的文件夹中的图像，观察到错误。

* [!DNL Dynamic Media] 包含引用的资产将无法发布(NPR-31180)。

* 从[!DNL Dynamic Media]7-Scene7模式到[!DNL Dynamic Media Classic]的上载时间过长，无法完成(NPR-31048)。

* 添加到图像资产的热点无法通过资产详细信息页面中的交互式图像查看器显示(NPR-30979)。

* 当对[!DNL Experience manager Assets]中的资源执行的操作传递到Scene7(NPR-30947)时，将创建大量sling作业并重新显示处理横幅。

* 创建不上传到Scene7的资产和资产的语言副本时发生冲突(NPR-30932)。

* 从[!DNL Dynamic Media]-Hybrid模式下运行的[!DNL Experience Manager]下载的动态演绎版将断开（这些演绎版属于文本类型，内容为“无法找到图像”而非图像内容类型）(NPR-30876)。

* [!DNL Dynamic Media] “编码视频”工作流无法为从Adobe Experience Manager上的Scene7模式迁移 [!DNL Dynamic Media Classic] 到 [!DNL Dynamic Media]模式的视频生成缩略图(CQ-4282011)。

* 使用不同的Scene7公司ID(CQ-4280548)将资源从一个实例迁移到另一个实例时观察到IpsApiException。

* 当支持的3D模型被引入[!DNL Experience Manager](CQ-4283701)时，3D资产缩览图不会提供信息。

* 如果3D资产的相机视图很少，则查看器中会显示滚动按钮(CQ-4283322)。

* 在“资产详细信息”页上的DimensionalViewer中预览的已上载3D模型的容器高度不正确(CQ-4283309)。

* 无法在Internet Explorer 11和Safari(CQ-4281422)上使用SmartCropVideoViewer播放视频。

* 在[!DNL Dynamic Media]-Scene7运行模式(CQ-4280384)上运行的[!DNL Experience Manager]中，使用“移动”按钮将多个资源从一个文件夹移动到另一个文件夹失败。

* 当MIME类型不是MP4时，资产详细信息上会显示扭曲的视频(CQ-4279704)。

* 新收录到具有视频用户档案的文件夹中的视频即使在编码百分比完成到100%后仍处于处理状态(CQ-4279389)。

* 从文件夹移动资源会创建大量sling作业(Scene7 API调用)，而非理想的必需(CQ-4278664)。

* 在Scene7中，创建图像集（或mediaset）并使用DAM(CQ-4281112)中的适当命名约定命名时，图像集的名称将更改为小写字母。

* Scene7 Migrator设置发布状态时不正确(CQ-4263492)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失内容片段中用户的滚动位置(CQ-4282898)。

* PDF文件不进行索引，内容也不可搜索(CQ-4278916)。

* 错误“用户选取器未列出组：添加具有不同`principalName`和`authorizableId`(CQ-4278177)的已关闭用户组时，会观察“expect false to equal true”。

* 资产UI列视图显示所有路径，而不管特定租户的dam根路径(CQ-4278175)。

* 资产选择器的搜索未按预期工作(CQ-4275886)。

* 再现工作流失败(CQ-4271928)。

* DAM事件清除将删除最新(`maxSavedActivities`)事件数据并保存之前创建的数据(NPR-31336)。

* 触屏UI搜索（通过Omnisearch完成）结果页会自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在触屏UI中选择全部，然后取消选择某些项目（文件夹/单个资产）时，操作栏和资产计数不会更新(NPR-31118)。

* 轮询资产的作业详细信息时，[!DNL Experience Manager]中显示异常(CQ-4283569)。

### 站点

* 如果LiveCopy继承中断，Live Copy页面将显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新Blueprint，如果记录数大于40，则仅显示前40条记录。 Blueprint显示其余记录的空行(NPR-31182)。
* 当用户在菜单的描述属性中添加日文或韩文字符时，该菜单显示日文和韩文文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用，基架式富文本编辑器(RTE)。 意外地将内联字体大小应用于元素(NPR-31284)。
* 如果用户的焦点位于左侧边栏字段并使用键盘快捷方式粘贴内容，则会粘贴页面编辑器剪贴板的内容，而不是从左侧边栏字段复制的内容 (NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径将存储在组件节点中，而不是多字段节点(NPR-30882)。
* `ResponsiveGridExporter` API不返回`com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`接口。 `com.day.cq.wcm.foundation.model.impl`包声明为私有包(NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 当以非编辑器模式(在“作者”模式下（没有`editor.html`前缀和`wcmmode=disabled`，或在“发布者”模式下）打开包含某些体验片段的页面时，请求以HTTP状态错误代码`500`(NPR-30743)结束。
* 用户无法更改其密码并访问其用户档案页(NPR-31161)。

### 搜索和用户界面{#ui-interface-and-search}

* 在搜索结果页面上从卡视图切换到列表视图时，在可滚动页面之前会有延迟(NPR-31286)。

* [!UICONTROL 选择全部]复选框隐藏在[!DNL Sites]用户界面(NPR-31614)上的列表视图中。

* 搜索结果页上的[!UICONTROL 全选]计数不正确(NPR-31120)。

* 元数据编辑器显示不存在的标记(NPR-31119)。

### 翻译 {#translation}

* 在翻译作业(NPR-31270)中选择“到期日”选项时，会显示两个日历弹出窗口。

### 平台

* Web控制台中的Mime类型选项不起作用(NPR-31108)。

* 配置单点登录时不接受客户端证书(NPR-31165)。

* 基于 Jetty 的 HTTP 服务的缓冲区大小配置中的更新未保存 (NPR-30925)。

* QueryBuilder现在支持xpath查询中的orderby `fn:name()`(NPR-31322)。

* 从[!DNL Experience Manager] 6.3(NPR-31513)升级时将创建重复激活树。

* 转发的请求不保留在sling身份验证过程中设置的响应标头(NPR-30013)。

* 在拾色器组件中搜索不起作用(NPR-31692)。

* 由于Apache POI和Apache Tika捆绑包(NPR-31018)的不同版本，将ZIP文件附加到[!DNL Experience Manager Communities]帖子时显示错误。

* `org.apache.sling.distribution.api`捆绑包隐藏在配置管理器中，因此对自定义捆绑包不可用(NPR-31720)。

### 项目

* 切换日历视图不起作用(NPR-31271)。

### Brand Portal {#assets-brand-portal-6530}

**产品增强功能**

* 将修改[!DNL Experience Manager Assets]中的资产来源补充导入工作流，以仅从[!DNL Brand Portal]提取新创建的资产至[!DNL Experience Manager]，并跳过NEW文件夹中已存在的资产以避免复制(CQ-4278527)。

**修复**

* 在“资产来源补充”功能(CQ-4282825)中创建新的“贡献”文件夹时显示错误图标。
* 创建新的“贡献”文件夹时，“贡献”文件夹(CQ-4282424)中不显示一个或两个子文件夹（“新建”和“共享”）。
* 如果用户在从[!DNL Brand Portal]结尾(CQ-4279740)接收Contribution文件夹中的新资源后尝试将Contribution文件夹从[!DNL Experience Manager]重新发布到[!DNL Brand Portal]，则系统会引发异常。
* 禁止在Contribution文件夹（嵌套文件夹）内创建Contribution文件夹，以避免复杂性(CQ-4278391)。
* 上传从[!DNL Experience Manager]列表导入的[!DNL Brand Portal]用户Admin Console（.csv文件）时，系统引发异常。 只有.csv文件中的“电子邮件”、“名字”和“姓氏”字段是必填字段(CQ-4278390)。

### 社区 {#communities-6530}

**修复**

* 社区管理员（组管理员/站点管理员）看不到管理组（打开/编辑/发布/删除组）的快速链接(NPR-31627)。
* 提交的博客不会显示，除非页面被手动刷新/重新加载(NPR-31599)。
* “提及次数”功能使用的JCR查询区分大小写，并且返回结果需要太长时间(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar文件引发异常， `cq-social-translation` 6.5 UberJar [!DNL Experience Manager] 文件中缺少捆绑包(NPR-31186)。
* Jackson Databind库已更新到版本2.9.9.3以解决新的漏洞(NPR-30967)。
* 活动和通知标题不一致 (NPR-30941)。
* 在[!DNL Communities]博客(NPR-30914)中分页无法正常工作。
* 分析报告未在[!DNL Experience Manager]作者环境中填充，显示空白页(NPR-30913)。

### 橡木{#oak}

* Lucene索引更新导致作者服务器速度减慢(NPR-31548)。

### 表单 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Experience Manager Forms]。它们是通过单独的 Forms 附加组件包交付的。此外，还发布了一个累积安装程序，其中包含针对JEE上[!DNL Experience Manager Forms]的修复。 有关详细信息，请参阅[安装Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)上安装Experience Manager Forms。

#### Forms 附加组件包 {#forms-add-on-package-6530}

**自适应表单**

* 在本地化自适应表单时，字符串包含词典键(NPR-31110)。

**交互式通信**

* **将Jackson库升级到2.** 10.0(NPR-31549)后，MissingNode.toString()返回不准确的结果。

* 文本编辑器从从Microsoft Word中复制的文本中随机删除空格字符(NPR-31113)。

**通信管理**

* 将字母从LiveCycle ES4SP1迁移到[!DNL Experience Manager] 6.5(NPR-31615)时，不显示字幕和工具提示。

* **将字母保存为草稿时，** Textflow格式不再显示支持的错误消息(NPR-30463)。

**工作流**

* OSGi工作流因100% CPU利用率(NPR-31233)而失败。

**HTML5 表单**

* 在添加子表单的实例时，生成 XDP 表单的 HTML5 预览会显示闪烁 (NPR-30909)。

#### Forms on JEE安装程序{#forms-jee-installer-6530}

**表单 - 文档服务**

* 在.NET项目中使用MTOM的SOAP Web服务显示AssemblerServiceClient调用和HtmlToPDF2方法(NPR-4281771)的异常。

* 在AXIS 1.4 jar中发现2012-5784和2014-3596的安全漏洞，并修复了随[AXIS1.4.1 jar](https://helpx.adobe.com/cn/aem-forms/quick-fixes/6-5/jee-patch-0014.html)(NPR-31015)提供的漏洞。

**Foundation JEE**

* 操作配置不加载调用Forms Workflow提交操作的进程名(NPR-31478)。

### 包含的功能包 {#feature-packs-included-6530}

>[!NOTE]
>
>对于[!DNL Experience Manager Forms]客户，在安装任何[!DNL Experience Manager] Service Pack、Cumulative Fix Pack或Feature Pack后，必须安装[!DNL Experience Manager Forms]附加包。

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms支持Oracle 18c(NPR-29155)。

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0是一个重要版本，包括自2019年4月6.5正式发布以来发布的性能、稳定性、安全 [!DNL Adobe Experience Manager] 性以及重要客户修 **复和增强**。它可以安装在[!DNL Experience Manager] 6.5的顶部。

此Service Pack版本的一些关键亮点是：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.3。
* 添加了配置属性，以允许将体验片段直接导出到[!DNL Adobe Target]的用户定义工作区。
* 资产用户可以直观地搜索相似图像。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。请参阅[使用连接的资产](../assets/use-assets-across-connected-assets-instances.md)。

* Enhance具有更多MIME类型的文档类型过滤器以支持多值选项。
* 引入了一个外部“重新处理”工作流以支持多种资源。
* 通过使用默认资产过滤器进行复制，优化了[!DNL Dynamic Media]性能。
* 恢复了 DMS7 的裁剪/旋转资产编辑选项。
* 在 VideoPlayer 中实施了加载时使视频静音的选项。
* 修复以确保 Asset UI 列视图仅显示特定租户的内容。
* 修复以允许搜索结果中反映样式可折叠项的更改。

### 资产

**产品增强功能**

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。适用于 CQ-4270245 的修补程序. 请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 用户可以搜索视觉上相似的图像。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

**修复**

* 通过 ACP API 生成的 URL 和文件夹元数据中的资产路径未进行 URL 编码。GRANITE-26198：适用于 CQ-4271814 的修补程序
* 无法使用[!DNL Experience Manager Assets]接口打开具有名称中包含百分号(%)的文件夹的存档解压缩。 NPR-29989：适用于 CQ-4270467 的修补程序
* 触屏UI:在“管理发布”向导中，会在帖子请求主体中的页面之后添加引用，导致所有资产在页面后发布，呈现页面时，发布实例中的部分资产会丢失。 NPR-29985：适用于 CQ-4270724 的修补程序
* “取消关联资产”功能无法用于名称中包含特殊字符（成为 URI 编码的字符）的关联资产。NPR-30387：适用于 CQ-4274446 的修补程序
* 编辑内容片段时，使用错误的用户创建此版本。
* 在基于“租户”的系统上创建收藏集失败。NPR-30114：适用于 CQ-4272948 的修补程序
* Asset UI 列视图不遵循当前租户的 dam 根路径，而是访问所有租户的 dam 路径。NPR-30636：适用于 CQ-4275481 的修补程序
* 由于能够看到插入的图像，可通过受限的文件警告窗口实施跨站点脚本 (XSS) 攻击。NPR-30617：适用于 CQ-4270133 的修补程序
* 多租户：保存文件夹属性的租户会同时观察成功提示和错误消息，说明操作未成功，“无法编辑属性。 权限不足。”因此，让租户感到困惑。NPR-30545：适用于 CQ-4275333 的修补程序
* 资产选择器对话框不允许选择资产，因此无法使用相关源替换功能来更新源。NPR-30502：适用于 CQ-4275029 的修补程序
* [!UICONTROL DAM更新资] 源流 — 上传大型mp4文件时处于过时状态。NPR-30480：适用于 CQ-4271352 的修补程序
* 由于有效负荷为空，“创建审核任务”功能不起作用，使所有后续与审核任务相关的操作失败。NPR-30468：适用于 CQ-4274263 的修补程序
* 通过 Datapower 实施的 Adobe 智能标记存在连接问题。NPR-30026：适用于 CQ-4269457 的修补程序
* 尝试打开左边栏上的筛选器时，Assets UI 列视图引发一个错误。NPR-30501：适用于 CQ-4273862 的修补程序
* 在“资产文件夹”的“已关闭的用户组”(CUG) 属性中添加从 LDAP 同步的组后，不会保存和检索组。NPR-30615：适用于 CQ-4274689 的修补程序
* 筛选搜索样式和方向字段不会将自动完成的值应用于搜索查询。NPR-30620：适用于 CQ-4275724 的修补程序
* 对于某些资产，名称中包含空格和“&amp;”字符的文件夹的资产共享链接显示为空白灰色卡片。NPR-30557：适用于 CQ-4270187 的修补程序
* 文件夹元数据架构表单不会自动检测数据类型，因此，在表单提交中没有创建相关的 TypeHint。NPR-30599：适用于 CQ-4275227 的修补程序
* DMS7 创作 UI 中的裁剪和旋转资产编辑选项被禁用。NPR-30118：适用于 CQ-4273221 的修补程序
* 共享链接功能在DMS7配置的[!DNL Experience Manager]实例上不工作。 NPR-30080、NPR-30492：适用于 CQ-4273651 的修补程序
* 将[!DNL Dynamic Media]-Scene7组件添加到页面，然后发布页面不会每次触发dmscene7配置。 NPR-30641：适用于 CQ-4275962 的修补程序
* 在[!DNL Experience Manager]中添加了IPSJobJournal，以在每个处理用户档案仅创建一个入侵防御系统(IPS)作业。 NPR-30490：适用于 CQ-4273614 的修补程序
* [!DNL Dynamic Media]:添加了默认过滤器以排除资产被复制到发 [!DNL Experience Manager] 布节点。NPR-30538：适用于 CQ-4274678 的修补程序
* 为多资源支持引入了一个外部“重新处理”工作流，以允许文件夹作为有效负载。工作流包含两个步骤 - 通过到下一步的元数据映射重新处理没有句柄的资产，并在单个 IPS 作业中将所有没有资产句柄的资产重新上传到 S7。有关详细信息，请参阅配置[!DNL Dynamic Media]Cloud Services。 NPR-30489：适用于 CQ-4272903 的修补程序
* 正确的 CSV 擦除正确的 CSV 后，会上传一个错误的 CSV。适用于 CQ-4277694、CQ-4277814 的修补程序
* 特定于要删除的贡献文件夹的图标错误。适用于 CQ-4277580 的修补程序
* 在资产贡献选项卡的用户选取器中选择用户时，表中不显示用户的名称，并且属性页面的“删除用户”对话框中显示错误文本。适用于 CQ-4277875 的修补程序
* 无法在用户选取器中通过选择用户和单击添加操作将参与者添加到资产贡献文件夹。适用于 CQ-4277824、CQ-4278087 的修补程序
* 用户选取器中按小写用户名称搜索不起作用。适用于 CQ-4277958、CQ-4277930 的修补程序
* 非管理员可以在资产贡献文件的新文件夹中发布资产。适用于 CQ-4278200 的修补程序
* dam 用户（非管理员）无法选择将参与者添加到资产贡献文件夹。适用于 CQ-4278192 的修补程序
* “创建”按钮在资产贡献文件夹中可见。适用于 CQ-4277560 的修补程序
* 按相关性对搜索查询排序将返回[!DNL InDesign]文档和[!DNL InDesign]模板。 适用于 CQ-4273864 的修补程序
* 如果用户的电子邮件 ID 为大写字母，则该用户无法签入以前签出的那些资产。适用于 CQ-4276575 的修补程序
* “删除”操作仅应用于选定的预设，如果执行该操作后屏幕自动刷新列表，则会显示已刷新的其他预设。适用于 CQ-4261461 的修补程序
* 在[!DNL Dynamic Media] — 混合模式中配置[!DNL Dynamic Media]Cloud Services会导致在[!DNL Analytics]中创建多个空报表包，并且在[!DNL Experience Manager]中未存储报表包ID，从而导致报表包重复。 适用于 CQ-4249780 的修补程序
* 将[!DNL Experience Manager]资产中的操作重命名为重复的名称无法同步到Scene7。 适用于 CQ-4276763 的修补程序
* 搜索筛选器面板中错误地显示用户生成内容。适用于 CQ-4273875 的修补程序
* “查找近似项”选项不适用于 TIFF 图像。适用于 CQ-4278238 的修补程序
* 在 VideoPlayer 中实施了加载时使视频静音的选项。适用于 CQ-4266465 的修补程序
* 查看器 — VideoViewer:poster=none在使用外部视频时工作不正确。 适用于 CQ-4265536 的修补程序
* 在 IE11 和 MS Edge 浏览器中播放视频期间显示“等待”图标。适用于 CQ-4251539 的修补程序
* 3.8 SDK和5.13查看器自述文件不会更新并包含先前发行版的信息。 适用于 CQ-4273737 的修补程序
* 即使在保存更改之前，也要对内容片段进行版本控制。NPR-30616：适用于 CQ-4273088 的修补程序
* 在缩略图进程中用 Asset#getMetadataValueFromJcr(String) 替换 Asset#getMetadata(String)。NPR-30491：适用于 CQ-4273067 的修补程序
* 上传 jpg 会导致每个资产显示消息的多个实例：“ReplicateOnModifyWorker 复制更新”，从而导致性能降低。
* 使用“提取存档”功能解压缩 zip 存档会导致标题中包含百分号 (%) 的文件夹出现问题。NPR-29990：适用于 CQ-4270467 的修补程序

### 站点 {#sites-6520}

* 如果LiveCopy继承中断，Live Copy页面将显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新Blueprint，如果记录数超过40，则只显示前40条记录。 Blueprint显示其余记录的空行(NPR-31182)。
* 文本组件的富文本编辑器(RTE)插件显示日文和韩文文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)意外地对元素应用内联字体大小(NPR-31284)。
* 当用户关注左边栏字段并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容，而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径将存储在组件节点中，而不是多字段节点(NPR-30882)。
* `ResponsiveGridExporter` API不返回`com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter`接口。 `com.day.cq.wcm.foundation.model.impl`包声明为私有包(NPR-31398)。
* 当以非编辑器模式(在“作者”模式下（没有`editor.html`前缀和`wcmmode=disabled`，或在“发布者”模式下）打开包含某些体验片段的页面时，请求以HTTP状态错误代码500(NPR-30743)结束。

### WCM - 页面编辑器 {#wcm-page-editor-6520}

**产品增强功能**

* 增强具有更多MIME类型的文档类型过滤器以支持多值选项。 适用于 CQ-4270694 的修补程序

### 内容片段管理 {#content-fragment-management-6520}

* 内容片段模式 UI 使用的查询非常缓慢，最终会导致错误。适用于 CQ-4270807 的修补程序

### UI - Foundation {#ui-foundation}

* 快捷方式触发器阻止用户在特定用户界面中使用“m”、“p”、“e”。NPR-30355：适用于 GRANITE-26346 的修补程序
* 关闭[!DNL Experience Manager Assets]搜索UI不会将左边栏重置为内容选择，阻止用户随后第二次打开过滤器边栏。 NPR-30509：适用于 CQ-4274716 的修补程序
* 多租户环境:[!DNL Experience Manager Assets] UI顶部导航不可用，并引发JavaScript错误。 NPR-30104：适用于 GRANITE-26344 的修补程序

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

### 集成

* 重新启动实例之前，发布实例上显示的自定义内容错误。NPR-30377：适用于 CQ-4273706 的修补程序
* 在网站中配置 Launch 时，库地址前面带有斜线 (\)，导致每次需要手动干预。NPR-30694：适用于 CQ-4275501 的修补程序

### 表单 {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含修复 [!DNL Experience Manager Forms]。它们使用单独的[!DNL Forms]加载包交付。 此外，还发布了一个累积安装程序，其中包含针对JEE上[!DNL Experience Manager Forms]的修复。 有关详细信息，请参阅[安装Experience Manager Forms add-on](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package)和[在JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer)上安装Experience Manager Forms。

[!DNL Experience Manager] 6.5.2.0表单的主要亮点是：

* 为[!DNL Experience Manager] Forms OSGi的`PDFFormRenderOptions` API中的`RenderAtClient`添加了“Auto”设置。

#### Forms 附加组件包

**后端集成**

* 无法使用 AWS 托管的负载平衡 URL 来配置“表单数据模型”。NPR-30123：适用于 CQ-4273359 的修补程序
* 使用Web服务定义语言(WSDL)创建表单数据模型(FDM)时，返回错误消息`Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type`:NPR-30477:CQ-4272921的修补程序

**通信管理**

* “创建通信UI(CCR UI)再现间歇性地失败，控制台中出现以下错误：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**交互式通信**

* 表单数据模型中标记为必填的字段将按“创建通信 UI”(CCR UI) 中的要求显示。NPR-30623：适用于 CQ-4274902 的修补程序

**表单 - 工作流**

* “监视文件夹”中未映射的输出变量导致调用失败。适用于 CQ-4264451 的修补程序

**HTML5 表单**

* 在第二次部署自定义代码或项目时，页面不会呈现，并出现以下错误：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：适用于 CQ-4272509 的修补程序

* 在浏览模式下使用 NonVisual Desktop Access 读取 HTML5 表单时，Chrome 浏览器会读取表单设计中每个可缩放矢量图形 (SVG) 前的“图形”。NPR-30449：适用于 CQ-4274732 的修补程序

#### Forms JEE 安装程序

**表单 - 文档安全**

* 应用带有时间戳的签名失败，并出现错误：ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 调用错误。NPR-30820：适用于 CQ-4275852 的修补程序

**表单 - 文档服务**

* 如果“SubmitURL”包含与号 (＆)，则在对 renderpdf servlet 发出 POST 请求时，日志中会出现解析错误。NPR-30865：适用于 CQ-4278232 的修补程序

**Forms - Foundation JEE**

* HTMLtoPDF服务在JMX控制台中不显示maxReuseCount。 NPR-30134、NPR-30304：适用于 CQ-4273763 的修补程序
* 通过从[!DNL Experience Manager Forms] Workbench调用Web服务来添加或编辑Web服务连接会引发错误：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105：适用于 CQ-4273217 的修补程序

### 包含的功能包

>[!NOTE]
>
>对于[!DNL Experience Manager Forms]客户，在安装任何[!DNL Experience Manager] Service Pack、Cumulative Fix Pack或Feature Pack后，必须安装[!DNL Experience Manager Forms]附加包。

#### 站点 {#sites-feature-packs-included}

* 添加了配置属性，以允许将体验片段直接导出到[!DNL Adobe Target]的用户定义工作区。 NPR-29189：适用于 CQ-4249782 的修补程序

#### 表单 - 文档服务 {#forms-document-services-1}

* 为[!DNL Experience Manager Forms] OSGi的`PDFFormRenderOptions` API中的`RenderAtClient`添加了“自动”设置。 NPR-30759：适用于 CQ-4278193 的修补程序

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是一个重要版本，包括自2019年4月6.5正式发布以来发布的性能、稳定性、安全性 [!DNL Adobe Experience Manager] 以及重要客户修 *复和增强。* 它可安装在6.5 [!DNL Experience Manager] 之上。

此Service Pack版本的一些关键亮点是：

* 支持在跟踪事件中包含动态 UI 状态作为自定义属性。
* 包括对在[!DNL Dynamic Media]-Scene7模式下投放360度视频资源的支持。
* 通过富文本编辑器的样式插件启用了&#x200B;*日文换行*&#x200B;功能。 有关详细信息，请参阅[配置日文换行](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 资产

* 针对 S3 多部分支持更新了 DAM DMGateway 接口。NPR-29740：适用于 CQ-4226303 的修补程序
* 再现预览在升级到[!DNL Experience Manager] 6.5后生成`Only empty tenantId is currently supported`错误。NPR-29986:CQ-4272353的修补程序
* “删除”对话框不可见，因此不允许删除作业。NPR-29720：适用于 CQ-4271074 的修补程序
* 在属性页面中添加资产标题后，当用户尝试关闭页面时，[!DNL Experience Manager]会再次打开属性页面。 NPR-29627：适用于 CQ-4264929 的修补程序
* VersioningTimelineEventProvider 应该提供 root 版本以及 nt：version 类型的节点。适用于 GRANITE-26063 的修补程序
* 实现了在[!DNL Experience Manager] DM-Scene7模式下上传和播放360个球面视频的功能。 适用于 CQ-4265131 的修补程序
* 如果编辑了源，则 Live Copy 检索错误的状态。适用于 CQ-4265451 的修补程序
* 已为[!DNL Experience Manager Assets]启用多站点管理器支持。 适用于 CQ-4271453、CQ-4268621、CQ-4257491 的修补程序
* [!DNL Experience Manager] 界面应在时间轴历史记录中显示资产当前版本的额外条目，并显示最新的签入注释 [!DNL Adobe Asset Link]。适用于 CQ-4262864 的修补程序
* 内容片段时间轴在属性缺失时显示错误消息。 适用于 CQ-4272560 的修补程序
* 扩展到全屏时，Scene 7 视频播放器出现问题。适用于 CQ-4266700 的修补程序
* ZoomVerticalViewer：使用单个图像资产时不应显示“全景”按钮。适用于 CQ-4264795 的修补程序
* 删除 Live Copy 中的儿童模式时应分离 liveRelationship。适用于 CQ-4270395 的修补程序
* 元数据架构仅包含来自全局配置的项目，丢失了来自活跃租户的项目。即使在更改之后，formPath URL 值也会恢复为默认值。NPR-29945：适用于 CQ-4262898 的修补程序
* 将图像预设发布到[!DNL Brand Portal]失败，出现500错误代码。 NPR-29510：适用于 CQ-4268659 的修补程序

### 站点

* 在转出期间，不会从 Blueprint 传播空属性和多属性。使用 Blueprint 重置 Live Copy 不适用于组件。NPR-29253：适用于 CQ-4264928、CQ-4264926、CQ-4267722 的修补程序
* 与`Multifield`一起使用时，CoralUI将`fileReferenceParameter`存储在组件级别，而不是多字段级别。 NPR-29537：适用于 CQ-4266129 的修补程序
* 将[!DNL Experience Manager]文本组件和文本编辑器增强为日语。 NPR-29785：适用于 CQ-4265090 的修补程序
* 使用时间扭曲恢复的页面在版本控制时应该引用正确的图片。NPR-29431：适用于 CQ-4262638 的修补程序
* 样式系统节点从父节点继承到子节点的问题。 NPR-29516：适用于 CQ-4270330 的修补程序
* 将社交发布设置为[!DNL Facebook]身份验证时显示错误消息。 NPR-29211：适用于 CQ-4266630 的修补程序
* “内容片段”上呈现的缩略图使用内部日历来表示“日期和时间”字段。NPR-29531：适用于 CQ-4269362 的修补程序
* 在 Coral2 实施中打开权限选项卡时不显示按钮。适用于 CQ-4269419 的修补程序

### 商务

* 为电子商务运行延迟内容迁移时引发 ConstraintViolationException。NPR-29247：适用于 CQ-4264383 的修补程序

### 内容片段管理

* 打开包含字符美元`($)`和大括号`({)`的内容片段时出现解析错误。 适用于 CQ-4270266 的修补程序

### 体验片段

* 将[!DNL Experience Manager]体验片段导出到[!DNL Adobe Target]。 适用于 CQ-4265469 的修补程序
* 智能图像无法导出到目标的体验片段。 适用于 CQ-4269606 的修补程序

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

* 升级到[!DNL Experience Manager] 6.4.3使多站点管理器需要很长时间才能推出。 适用于 CQ-4271410 的修补程序

### 集成

* BrightEdge 凭证失败，出现连接错误。NPR-29168：适用于 CQ-4265872 的修补程序

* 尝试编辑并保存[!DNL Experience Manager]启动配置时，将显示异常消息。 NPR-29176：适用于 CQ-4265782/CQ-4266153 的修补程序

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

* 每次复制到[!DNL Brand Portal]时，OAuth期间会话泄漏。 NPR-30001：适用于 GRANITE-26196 的修补程序

### 项目

* 将[!DNL Experience Manager Assets]从[!DNL Experience Manager]发布到[!DNL Brand Portal]的作者/content/dam/mac文件夹不起作用。 NPR-29819：适用于 CQ-4271118 的修补程序

### 平台

* HtmlLibraryManager 在缓存失效时删除 crx-quickstart 的所有内容。NPR-29863：适用于 GRANITE-26197 的修补程序

### Felix

* 使用Java11时，系统控制台中不显示内存使用情况详细信息。 NPR-29669

### 表单

[!DNL Experience Manager Forms] 6.5.1.0的关键亮点是：

* 仅OSGi:在输出和Forms服务中添加了新属性`PAGECOUNT`。

* 仅限OSGI:支持使用Forms服务创建静态PDF文件。
* 为管理员和根用户启用了对 XMLForm.exe 的权限。
* 为 Dynamics 内部部署集成启用了对 ADFS v3.0 的支持。

#### Forms 附加组件包

**后端集成**

* 获取受保护的 Web 服务定义语言 (WSDL) 失败。NPR-29944：适用于 CQ-4270777 的修补程序
* 当[!DNL Experience Manager Forms]安装在IBM WebSphere上时，基于SOAP创建表单数据模型失败。 适用于 CQ-4251134 的修补程序
* 为 Microsoft Dynamics 内部部署集成启用了对 Active Directory 联合身份验证服务 (ADFS) v3.0 的支持。适用于 CQ-4270586 的修补程序
* 数据源的标题发生更改时，表单数据模型不显示更新的标题。适用于 CQ-4265599 的修补程序
* 如果实体或属性的名称包含连字符或空格，则表达式无法计算此类实体和属性。 适用于 CQ-4225129 的修补程序

* 当基元字符串输出中存在冒号时，会观察到错误的输出。 适用于 CQ-4260825 的修补程序

* 即使 REST API 输出中没有任何内容，表单数据模型的调用操作也会引发错误。适用于 CQ-4268828 的修补程序

**自适应表单**

* 在延迟加载期间，无法在“自适应表单片段”中添加新实例。NPR-29818：适用于 CQ-4269875 的修补程序
* 验证组件没有记录或显示“记录文档”模板的任何错误。适用于 CQ-4272999 的修补程序
* 添加了对“自适应表单”禁用布局编辑器的支持。适用于 CQ-4270810 的修补程序
* 已在[!DNL Experience Manager] 6.5中恢复Adaptive Forms的验证步骤。CQ-4269583的修补程序

* 自适应表单字段验证失败将中断[!DNL Adobe Sign]。 适用于 CQ-4269463 的修补程序
* 当[!DNL Experience Manager Forms]实例包含20个以上的自适应表单片段以及所有具有相同字符串的表单片段开始的名称时，搜索将不返回或仅返回最近创建的20个片段。 适用于 CQ-4264414、CQ-4264914 的修补程序

* Adaptive Forms应用程序与大数据集一起使用时的性能问题。. 适用于 CQ-4235310 的修补程序

* 通过匿名帐户在发布实例上进行访问时，GuideRuntime 脚本加载失败。适用于 CQ-4268679 的修补程序

**表单 - 交互式通信**

* “交互式通信”模板未在允许的组件列表中列出页眉和页脚组件。适用于 CQ-4237895 的修补程序
* 创建包含图像字段的交互式通信打印模板时，图表标题将设置为空白。适用于 CQ-4264772 的修补程序
* 图表的线条颜色在删除后设置为未定义。适用于 CQ-4264762 的修补程序
* 在执行保持更改同步时，在文档片段上所做的布局图层更改会消失。 适用于 CQ-4266054 的修补程序
* “文档片段”中绑定到文本字段的表单数据模型元素不显示继承图标，并且允许绑定。适用于 CQ-4261089 的修补程序
* “打印渠道”呈现 API 没有在 API 中作为参数传递数据的选项。适用于 CQ-4263540 的修补程序
* 当将绑定类型从文本片段更改为字符串字段/变量的无/数据模型对象时，代理设置不可见，因为“可由代理编辑”复选框会被取消选中。 适用于 CQ-4261953 的修补程序
* 在提交代理UI时，生成的web数据json文件会存储继承取消未绑定字段的信息。 适用于 CQ-4265621 的修补程序

**表单 - 工作流**

* 从自适应表单应用程序的发件箱重新提交表单时，将导致数据丢失。NPR-28345：适用于 CQ-4260929 的修补程序
* 对于不可变情况，保存时不会关闭文档。适用于 CQ-4269784 的修补程序
* “自适应表单”应用程序取消了对 Microsoft Windows 8.1 的支持。适用于 CQ-4265274 的修补程序。
* 当超过2 MB的图像作为字段级附件附加到[!DNL Experience Manager Forms]应用程序的Android版本中的表单时，应用程序崩溃。 适用于 CQ-4265578 的修补程序

* 为分配任务中的“交互式通信打印渠道”启用了预填充选项。适用于 CQ-4265577 的修补程序
* 用户只有成为分配任务的组的成员之后才能查看共享任务。适用于 CQ-4248733 的修补程序
* Windows 上禁止在“自适应表单”应用程序上保存或提交 JEE 应用程序。适用于 CQ-4268704 的修补程序
* 与表单数据模型变量关联的表单数据模型不可见。适用于 CQ-4266554 的修补程序
* 使用变量支持时不支持文档签名的状态变量。适用于 CQ-4266312 的修补程序
* 从工作区中提交带有变音字符的内容失败。适用于 CQ-4263172 的修补程序
* 在升级的设置中，如果打开了工作流进行编辑，则监视文件夹用户界面 (UI) 中会显示错误而不是工作流名称。适用于 CQ-4238579 的修补程序

**表单 - 管理**

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

* 当对使用[!DNL Experience Manager Forms Designer]创建的静态PDF执行完全的辅助功能检查时，由于缺少语言属性，主语言检查将失败。 适用于 CQ-4272923、CQ-4271002 的修补程序

**表单 - 文档安全**

* 带硬件安全模块(HSM)的数字签名在Java 11和Java 8的OSGi Linux上不工作。 NPR-29838：适用于 CQ-4270441 的修补程序
* 带硬件安全模块 (HSM) 的数字签名在 JEE Linux 上，以及所有受支持的应用程序（例如，JBoss 和 Websphere）上不起作用。NPR-29839：适用于 CQ-4266721 的修补程序
* 在 PDF 中使用“PDF 高级电子签名”(PAdES) 验证签名会生成 InvalidOperationException。NPR-29842：适用于 CQ-4244837 的修补程序
* 增加了对Office 2019的文档安全扩展支持\。 适用于 CQ-4254369、CQ-4259764 的修补程序

**表单 - 文档服务**

* “表单”字段无法转换为PDF/A-1b时，PDF没有外观指示。 NPR-29940：适用于 CQ-4269618 的修补程序

* OSGi:无法确定渲染期间生成的页数。 NPR-28922：适用于 CQ-4270870 的修补程序
* [!DNL Experience Manager Forms OSGi]中使用Forms服务支持静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 无法更改对 XMLForm.exe 的权限。NPR-29828、NPR-29237：适用于 Q-4267080 的修补程序
* 由[!DNL Experience Manager Forms]服务器的输出模块创建的静态PDF不会用所创建文档的语言填充语言属性/标签。 NPR-27332：适用于 CQ-4271002 的修补程序

**Forms - Foundation JEE**

* 最终部件中不可用的 pdfg_srt 会导致安装程序失败。NPR-29854：适用于 CQ-4270137 的修补程序
* LCBackupMode.sh 不起作用。NPR-29840：适用于 CQ-4269424 的修补程序
* UDP 端口引用应该从 WebSphere 的用户界面 (UI) 中删除。适用于 CQ-4264782 的修补程序

### 包含的功能包

#### 资产  — 包含

* 已为[!DNL Experience Manager Assets]启用多站点管理器支持。 有关详细信息，请参阅[对Experience Manager资产使用MSM重用资产](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html)。 NPR-29199：适用于 CQ-4259922 的修补程序

#### 站点 — 包含

* 将[!DNL Experience Manager]体验片段导出到[!DNL Adobe Target]。 有关详细信息，请参阅[体验片段链接重写器提供程序 — HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML)。 适用于 CQ-4265469 的修补程序

#### Forms - 文档服务  — 包含

* 仅OSGi:在“输出”和“Forms服务”中添加了新属性PAGECOUNT。 NPR-28922：适用于 CQ-4270870 的修补程序
* 仅OSGi:支持使用Forms服务创建静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 为管理员和根用户启用了对 XMLForm.exe 的权限。NPR-29237：适用于 CQ-4267080 的修补程序

### OSGi 包和内容包

以下文本文档列表了[!DNL Experience Manager] 6.5.1.0中包含的OSGi包和内容包

列表[!DNL Experience Manager] 6.5.1.0中包含的OSGi包

[获取文件](assets/6_5-bundle-list.txt)

[!DNL Experience Manager] 6.5.1.0中包含的内容包列表

[获取文件](assets/6_5-content-package-list.txt)
