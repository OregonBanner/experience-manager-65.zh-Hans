---
title: '[!DNL Adobe Experience Manager] 6.5以前的service pack发行说明'
description: 的发行说明 [!DNL Adobe Experience Manager] 6.5 service pack
contentOwner: AK
mini-toc-levels: 2
exl-id: aeed49a0-c7c2-44da-b0b8-ba9f6b6f7101
source-git-commit: 45673270ec839377f941860c098f965f7b35c59e
workflow-type: tm+mt
source-wordcount: '26608'
ht-degree: 11%

---

# 以前的Service Pack中包含的修补程序和功能包 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.10.0 {#experience-manager-65100}

[!DNL Adobe Experience Manager] 6.5.10.0包括自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。 Service Pack安装在 [!DNL Adobe Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.10.0是：

* **增强功能 [!DNL Content Fragment] 模型和编辑器**:您现在可以使用嵌套方式为结构化内容创建复杂的自定义模型 [!DNL Content Fragment] 模型。 内容结构被模块化为基本元素，这些元素被建模为子片段。 更高级别的片段引用这些子片段。 更多数据类型增强功能（如高级验证规则），进一步增强了内容建模的灵活性 [!DNL Content Fragments]. 的 [!DNL Experience Manager] [!DNL Content Fragment] 编辑器支持在通用编辑器会话中嵌套的片段结构，增强功能如结构树视图和选项卡式痕迹导航在片段层次结构中导航。

* **用于的GraphQL API[!DNL Content Fragments]**:新的GraphQL API是以JSON格式交付结构化内容的标准方法。 GraphQL查询允许客户端仅请求相关内容项来渲染体验。 这种选择消除了需要在客户端解析内容的内容过交付（借助HTTP REST API来实现）。 GraphQL架构是从 [!DNL Content Fragment] 模型和API响应采用JSON格式。 在 [!DNL Experience Manager] as a [!DNL Cloud Service], [GraphQL查询会保留](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) 和处理缓存友好GET请求。 在 [!DNL Experience Manager] 6.5.10.0。

* **层级管理和未来预览**:用户现在有一个界面可访问其内容结构 [!DNL Experience Manager] 启动项，包括在启动项中添加和删除页面的功能。 此功能增强了 [!DNL Experience Manager] 启动项以创作目标内容版本，以供将来发布。 [时间扭曲功能](/help/sites-authoring/working-with-page-versions.md#timewarp) 允许用户将启动项预览为将来的内容状态。

* **连接的资产**: [!DNL Experience Manager] 扩展 [!DNL Connected Assets] 功能 [!DNL Dynamic Media] 图像。 请参阅 [使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md).

* **链接共享选项以下载资产或演绎版**:在将资产和收藏集共享为链接时，用户可以选择是允许下载原始资产，还是允许下载其演绎版，还是同时使用共享链接来下载这两种资产。 此外，下载通过链接与他们共享的资产的用户可以选择仅下载原始资产，仅下载演绎版，或同时下载两者。

* **限制生成的子资产**:管理员可以限制 [!DNL Experience Manager] 为复合资产(如PDF、PowerPoint、InDesign和Keynote文件)生成。 请参阅 [管理复合资产](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Camera Raw支持**:新 [!DNL Camera Raw] 包可支持 [!DNL Adobe Camera Raw] v10.4。请参阅 [处理图像 [!DNL Camera Raw]](/help/assets/camera-raw.md).

* 内置存储库(Apache Jackrabbit Oak)已更新至1.22.8。

* **辅助功能增强功能**:

   * [!DNL Dynamic Media] 为查看器提供了许多辅助功能增强功能。 请参阅 [[!DNL Dynamic Media] 更新](#dynamic-media-65100).

   * 平台提供了一些辅助功能增强功能。 请参阅 [平台更新](#platform-65100).

* **用户体验增强**:

   * [!DNL Experience Manager] 直接在文件夹下显示所有内容模型的列表，内容作者不必在文件结构中导航。 现在，该功能需要的点击量更少，并且提高了创作效率。

   * 路径字段 [!DNL Sites] 编辑器允许作者从 [!DNL Content Finder].

* 添加了 `GuideBridge#getGuidePath` 中的API [!DNL AEM Forms].

* 您现在可以使用Automated forms conversion服务 [以法语、德语、西班牙语、意大利语和葡萄牙语语言转换PDF forms语](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) 到自适应表单。

* **属性浏览器中的错误消息**:为自适应Forms属性浏览器中的每个属性添加了错误消息。 这些消息有助于了解字段的允许值。

* **支持使用文字选项为JSON类型变量设置值**:您可以使用文字选项在AEM工作流的设置变量步骤中为JSON类型变量设置值。 利用文本选项，可以指定字符串形式的JSON。

* [平台更新](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] 在JEE上添加了对以下平台的支持：
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

有关 [!DNL Experience Manager] 6.5.10.0，见 [的新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

以下是 [!DNL Experience Manager] 6.5.10.0版本。

### [!DNL Sites] {#sites-65100}

* 在 **[!UICONTROL 默认值]** 字段 **[!UICONTROL 属性]** 选项卡(NPR-36992)。

* 筛选时 [!DNL Content Fragment] 模型， [!DNL Experience Manager] 搜索会返回所有节点 `cq:Template` 而不是仅返回 [!DNL Content Fragment] 型号(SITES-1453)。
* [!DNL Content Fragments] 返回 `null` 作为文件夹的状态(SITES-1157)。
* [!DNL Experience Manager] 不允许用户禁用和启用 [!DNL Content Fragment] 模型(SITES-1088)。
* 用户移动、重命名或删除时 [!DNL Content Fragments] 或媒体资产，引用 [!DNL Content Fragments] 不会自动更新(SITES-196)。
* 将组件从一个页面粘贴到另一个页面时，会产生JavaScript错误(NPR-37030)。
* 快速查看页面属性时，将打开其他页面的页面属性(NPR-37025)。
* 内容片段允许内容片段引用其自身。 选取器不支持该操作(NPR-36993)。
* 升级到Service Pack 9后，某些用户无法在Experience Manager中移动文件夹，并在日志中看到错误(SITES-1481)。
* 在编辑模式下调整布局容器中组件的宽度时，观察到闪烁(NPR-36961)。
* 提升启动项时，提升的启动项中的更改将会双重推广到其他启动项。 如果用户推广双重转出的启动项，则双重内容会反映在源页面上(NPR-36893)。
* [!DNL Experience Manager] 如果您使用图像核心组件将图像添加到页面，或者使用基础图像组件调整大小，则会向某些具有透明度的PNG图像添加灰色边框(NPR-36879)。
* [!DNL Experience Manager Sites] 管理员UI中模板数量较多，导航缓慢(NPR-36870)。
* 升级到Service Pack 9会阻止创作一些组件。 此问题不允许 [!DNL Sites] 用户创建新页面(NPR-36857)。
* 的 `ContextHubImpl` 方法创建 `ResourceResolver` 尚未关闭。 这会导致有关长时间运行的警告消息 `ResourceResolver` 并且服务有时会返回意外结果(NPR-36853)。
* 在从Blueprint页面属性同步单个Live Copy时，还会同步所有其他Live Copy(NPR-36829、NPR-36522)。
* 仅使用XLS MIME类型时，文件上传函数无法按预期工作(NPR-36785)。
* 新的标记（带有pascal大小写和所有大写字）不会显示在 [!DNL Content Fragments] (NPR-36742)。
* 添加 [!DNL Content Fragment] 导致文本丢失，并创建与列表和嵌套列表相关的奇数格式(NPR-36565)。
* 当作者在页面上注释任何组件、删除组件并对删除操作执行撤消时，在站点控制台中尝试查看页面的时间轴数据时会遇到错误(NPR-36528)。
* 页面属性批量编辑器 [!UICONTROL 保存并关闭] 选项会保存更改，但不会关闭编辑器(NPR-36527)。
* 当用户尝试将新的文本组件拖放到页面时，该组件会立即消失(NPR-36442)。
* 当用户键入包含空格（系统上不存在的标记）的按需标记并按Enter时，该标记将显示在字段下方。 但是，当 [!DNL Content Fragment] 保存并重新打开后，不会显示按需标记(NPR-36441)。
* 通过Dispatcher访问实例时，无法删除模板(NPR-36385)。
* 移动页面时，需要手动刷新浏览器才能渲染更改(NPR-36381)。
* 选择组件时，可以按Ctrl+X或Ctrl+C(以及Mac上的Command+X或Command+C)剪切或复制组件。 单击其他组件时，可以粘贴工具栏，但不能粘贴键盘（Ctrl+V或Command+V）(NPR-36379)。
* 当用户尝试使用剪刀图标剪切组件以将其移动到其他位置时，会出现控制台错误。 此外，粘贴时只移动一个组件(NPR-36378)。
* [!DNL Experience Manager] 在WCM或通知中存在没有索引的查询，会降低性能(NPR-36303)。
* 当作者恢复已删除的继承组件上的继承时，可用选项是同步所有页面内容。 内容作者需要同步完整页面，即使继承仅在一个组件上恢复也是如此。 完全同步可能会导致同步不需要的内容(NPR-34456、CQ-4310183)。
* 创作实例上组件的实时使用情况并不显示所有发生次数。 某些组件在1000多个页面中使用，但报表仅显示大约40个页面(CQ-4323724)。
* 当网站结构具有许多子页面时，与Experience Manager6.4.8.2(CQ-4322766)相比，在列视图中加载子页面需要花费更多时间。
* 取消选中“全部”在“转出页面”选项上不起作用(NPR-37070)。
* 打开页面的现有v3组件版本时，页面属性对话框未打开，并且 `NullPointerException` 已记录(SITES-1830)。

### [!DNL Assets] {#assets-65100}

中修复了以下问题 [!DNL Assets]:

* 属性的值 `jcr:title` 文件夹移动后，不会在发布实例上更新。 在作者中重命名和重新发布文件夹不会更新 `jcr:title` 的属性值(NPR-36369)。

* 如果选择了两个或更多资产并编辑了一个或多个元数据字段，则保存操作将失败，Safari浏览器中的错误代码为500(NPR-36413)。

* 由于日期格式不正确，批量元数据导入失败(NPR-36428)。

* 在 [!UICONTROL 属性] 页面更新元数据时，当架构提供了多个选项时，界面响应速度会很慢(NPR-36430)。

* 使用 [!UICONTROL 到期状态] 谓词无法工作(NPR-36436)。

* 中各个字段的弹出菜单 [!UICONTROL 文件夹元数据] 属性不显示最后选择的值(NPR-36937、CQ-4314429)。

* 在搜索文件和文件夹时，如果用户应用过滤器并选择 [!UICONTROL 文件和文件夹]，则只显示文件，而不显示文件夹(CQ-4319543、NPR-36627)。

* 从文件夹中选择同一收藏集并从搜索结果中选择该收藏集时，工具栏选项会有所不同(NPR-36620)。

* 的 [!UICONTROL 快速发布] 选项在搜索结果页面上不可用(NPR-36904、CQ-4317748)。

* 当用户在未指定资产扩展名的情况下创建资产的Live Copy时，下载Live Copy文件后，该文件将不可用(NPR-36903、CQ-4326305)。

* 将用户添加为子文件夹的所有者后，用户也会获得其父文件夹的所有者权限，进而获得父文件夹的其他子文件夹的所有者权限。 此外，在尝试删除用户时，该用户不会作为父文件夹的所有者被删除。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] 尝试为复合资产（如PowerPoint演示文稿）创建子资产时，会生成内存不足异常(NPR-36668)。

* 当用户移动已发布的站点页面中已使用的资产时，即使未选择用于发布的选项，站点页面也会再次发布(NPR-36636、CQ-4323500)。

* 使用Apache Tika MIME类型检测功能时，使用 `AssetManager.createAsset` 方法保留名为的临时文件 `apache-tika-*.tmp` 文件。 此临时文件使用所有可用的可用磁盘空间(NPR-36545)。

* 下载所有受DRM保护的资产，并且未遵循用户选择下载特定资产(CQ-4327422)。

* 无法将资产拖动到 `pathfield` (NPR-36849)。

* 在列视图中选择资产后，资产详细信息面板会消失(NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**辅助功能增强功能**

在 [!DNL Dynamic Media Viewers].

* 屏幕阅读器现在会讲述用于搜索的占位符文本，并将电子邮件地址添加为共享资产作为链接对话框中的必填字段，同时还会朗读 [!UICONTROL 请填写此字段] 工具提示(CQ-4327761)。

* 屏幕阅读器现在可以正确讲述 [!UICONTROL 图像预设编辑器] 使用键盘访问用户界面字段时(CQ-4325677)。

* 现在，可以将键盘焦点适当地移动到 [!UICONTROL 查看器预设] 对话框 [!UICONTROL 富媒体类型] 选项(CQ-4324736)。

* 使用键盘键在表单模式下导航时，屏幕阅读器会讲述与上的递增和递减选项对应的标签 [!UICONTROL 创建] 选项卡 [!UICONTROL 图像预设] (CQ-4323900)。

* 屏幕阅读器现在会发布 [!UICONTROL 搜索和添加电子邮件地址] “将资产共享为链接”对话框的选项(CQ-4323352)。

* 使用键盘键导航资产时，工具栏中会保留键盘焦点(CQ-4322037)。

* 屏幕阅读器现在会讲述新添加的 [!UICONTROL 编辑] 字段信息 [!UICONTROL 添加裁剪] 选项 [!UICONTROL 响应式图像裁剪] on [!UICONTROL 编辑图像处理配置文件] 页面(CQ-4290734)。

* 开 [!UICONTROL 编辑图像预设] 和 [!UICONTROL 创建交互式视频] 页面、屏幕阅读器现在可以在使用标题键盘快捷键(CQ-4290730)(CQ-4290701)导航页面时，适当地读出页面标题。

* 屏幕阅读器现在可以在导航以下页面时使用地标和区域快捷键识别屏幕的各个区域（如右面板区域、左面板、操作工具栏、查看器工具栏地标和可缩放图像地标）。

   * [!UICONTROL 查看器预设编辑器] (CQ-4290729)

   * [!UICONTROL 图像集编辑器] (CQ-4290710)

   * [!UICONTROL 创建交互式视频] (CQ-4290702)。

* 屏幕阅读器现在使用向下箭头键导航时，会朗读视频帧中共享选项的名称(CQ-4290728)。

* 屏幕阅读器现在会讲述 [!UICONTROL 斯普里特] 和 [!UICONTROL 背景] 选项卡 [!UICONTROL 外观] 选项卡 [!UICONTROL 查看器预设编辑器] (CQ-4290727)。

* 必填字段，如要编辑的字段 [!UICONTROL 宽度]，在 [!UICONTROL 基本] 选项卡 [!UICONTROL 编辑视频编码] 页面现在具有星号符号(*)(CQ-4290725)。

* 屏幕阅读器现在会在 [!UICONTROL 图像配置文件] 页面(CQ-4290723)。

* Windows用户现在可以在 [!UICONTROL 查看器预设编辑器] 焦点在CSS编辑器上时(CQ-4290720)。

* 开 [!UICONTROL 基本] 选项卡 [!UICONTROL 编辑图像预设] 在表单模式下导航时，屏幕阅读器现在会讲述各种编辑字段和选项的标签(CQ-4290717)。

* 屏幕阅读器现在会在资产详细信息页面的左侧导航中，为用户界面选项讲述角色和状态（已选择或未选择）(CQ-4290709)。

* 屏幕阅读器现在可以正确讲述在 [!UICONTROL 内容] 选项卡 [!UICONTROL 创建交互式视频] 页面(CQ-4290707)。

* 现在，在上使用向下箭头键导航时，屏幕阅读器可以正确讲述视频时间轴比例中各个区段的名称、角色和状态 [!UICONTROL 创建交互式视频] 页面(CQ-4290706)。

* 屏幕阅读器现在会在中导航选项时，讲述名称、角色、默认状态（已选或未选）和属性 [!UICONTROL 创建交互式视频] 页面(CQ-4290704)。

* 屏幕阅读器现在会讲述 [!UICONTROL 所有资产] 和 [!UICONTROL 所有收藏集] 选项 [!UICONTROL 发布] 页面(CQ-4290705)。

* 上传不支持的视频格式（MP4除外）时， [!UICONTROL 创建交互式视频] 页面，Experience Manager会显示并宣布错误消息(CQ-4290700)。

* 时间轴上数字（时间，以秒为单位）的对比度 [!UICONTROL 创建交互式视频] 页面现在满足最低要求的光度比，以便对颜色有限感知的用户可以轻松阅读(CQ-4290699)。

* 屏幕阅读器现在会朗读 [!UICONTROL 产品名称] 字段 [!UICONTROL 创建交互式视频] 页面(CQ-4290697)。

**已修复的问题**

中提供了以下错误修复 [!DNL Dynamic Media].

* 将视频上传到 [!DNL Experience Manager] 显示 `Process failed` after `dynamicmedia_scene7` runmode已启用且同步已禁用(CQ-4327791)。

### 平台 {#platform-65100}

此Service Pack中提供了以下增强功能：

* 当用户在树视图中选择项目时，屏幕阅读器会朗读所做的选择以及顶部显示的工具栏选项(NPR-36504)。
* 某些文本和控制名称对于出现视觉问题的用户来说更容易阅读，因为明度比率满足4.5:1的最低要求比率(NPR-36503)。
* 当用户使用日历控件时，屏幕阅读器会讲述描述性日期、月份和工作日信息。 用户使用日历快捷键时，屏幕阅读器会讲述日期、月和年的更改(NPR-36498)。
* 为执行自定义JavaScript提供支持 `Clientlibs` 使用ECMAScript 6功能，而不遵循严格模式。 具体而言， `emitUseStrict` 标记会添加到 `GCCScriptProcessor` (NPR-36411)。

以下错误修复是此Service Pack的一部分：

* 自定义运行状况检查的执行频率比计划的频率高(NPR-36985)。
* 的 `Resourceresolver map` 方法为别名页返回错误结果(NPR-36767)。
* [!DNL Experience Manager] 由于加载工作流，启动延迟(NPR-36615)。

### 集成 {#integrations-65100}

* Experience Manager在主MongoDB节点切换到另一个节点时变得无响应(NPR-36566)。
* [!DNL Sling content distribution] 执行收集成员删除操作时失败(NPR-36521、CQ-4323578)。

### 用户界面 {#user-interface-65100}

* 的 **[!UICONTROL 引用]** 侧面板不显示资产和站点引用(GRANITE-35078、GRANITE-34892)。

### 翻译项目 {#translation-65100}

* 将删除多翻译项目语言副本中的额外子页面(NPR-36622)。

### 工作流 {#workflow-65100}

* 如果服务器收到不在办公室的消息，它会报告内存警报并停止响应(NPR-36768)。

### [!DNL Communities] {#communities-65100}

* 社区网站页面在 `LoggedIn` 匿名来宾用户的状态(NPR-36908)。

* 当 **[!UICONTROL 社区]** > **[!UICONTROL 构思]** > **[!UICONTROL 评论]** 页面，则页面导航无法正常工作(NPR-36541)。

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。


[!DNL AEM 6.5.10.0 Forms] 包括以下错误修复：

* 安装时 [!DNL AEM 6.5 Forms]，则会自动安装以下第三方库(CQDOC-18373):
   * [!DNL Microsoft Visual C++ 2008 Service Pack 1 (x86)]
   * [!DNL Microsoft Visual C++ 2010 Service Pack 1 (x86)]

**自适应表单**

* 如果对自适应表单中的字段值执行的验证成功， [!DNL AEM Forms] 无法调用表单数据模型(CQ-4325491)。

* 当您向翻译项目添加语言词典，然后打开该项目时， [!DNL AEM Forms] 显示错误消息(CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* 安装后出现性能问题 [!DNL AEM Forms] Service Pack 7(CQ-4326828)。

**通信管理**

* 在 [!UICONTROL 数据] 选项卡以及HTML信件预览(NPR-37020)中的“隐藏主体”选项卡。

* 编辑文本文档片段时，保存片段后，新词将显示为HTML标记(NPR-36837)。

* 无法查看另存为草稿的信件(NPR-36816)。

* 编辑文本文档片段并预览信件时，AEM Forms会在HTML信件预览中显示表达式语言(CQ-4322331)。

* 使用自助信件模板渲染数据时出现问题(NPR-37161)。


**交互式通信**

* 编辑文本文档片段后，每次打印预览交互式通信时，制表符都会在两个单词之间重复(NPR-37021)。

* [!DNL AEM Forms] 保存超过最大大小限制的文本文档片段时显示错误(NPR-36874)。

* 向交互式通信添加图像时，该图像后会再显示一个空块(NPR-36659)。

* 在编辑器中选择所有文本时，无法将字体文本更改为Arial(NPR-36646)。

* 在编辑器中创建URL并预览更改时，将显示黑色背景而不是URL文本(NPR-36640)。

* 将文本复制并粘贴到编辑器时，如果文档中提供了项目符号，则将字体更改为Arial时会出现问题(NPR-36628)。

* 文本编辑器中的项目符号缩进问题(NPR-36513)。

**Designer**

* 屏幕Reader无法读取置于动态PDF中主控页面或子表单页面上文本标签内的浮动字段数据(CQ-4321587)。

**文档服务**

* 将XDP文件转换为PDF文件，然后组合生成PDF时，PDF层代会失败，并显示以下错误消息：

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**表单工作流**

* 升级到AEM Forms Service Pack 8后，无法将表单提交到Workbench进程(CQ-4325846)。

**HTML5 表单**

* 当您为 `mfAllowAttachments` 属性 `True` 在CRX DE存储库中， `dataXml` 提交HTML5表单时损坏(NPR-37035)。

* 在使用 `dataXml`, [!DNL AEM Forms] 显示 `Page Unresponsive` 错误(NPR-36631)。

### 商务 {#commerce-65100}

* 的值 **[!UICONTROL 发布者]** 列视图中显示的字段不正确(NPR-36902)。
* 推出目录时，新产品会被错误地标记为已修改的产品(NPR-36666)。
* 重新创建已删除的产品时，不会重新创建产品页面(NPR-36665)。
* 已修改的页面会更新，但相应的链接产品在目录转出时不会更新(CQ-4321409、NPR-36422)。
* 的 **[!UICONTROL 稍后发布]** 和 **[!UICONTROL 稍后取消发布]** 工作流不起作用(CQ-4327679)。

有关安全更新的信息，请参阅 [[!DNL Experience Manager] 安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html).

## Experience Manager6.5.10.0中的已知问题 {#known-issues}

* 作为 [!DNL Microsoft Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 10或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## [!DNL Adobe Experience Manager] 6.5.9.0 {#experience-manager-6590}

[!DNL Adobe Experience Manager] 6.5.9.0包含自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。 Service Pack安装在 [!DNL Adobe Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.9.0包括：

* [!DNL Experience Manager Sites] Dynamic Media Foundation组件现在允许您在使用响应式图像预设或智能裁剪时，打开或关闭针对高分辨率设备的优化功能。

* 为了提高性能， `hidden=false` 条件会从JCR查询移至 [!UICONTROL QueryBuilder] 计算器。 要验证隐藏的谓词是否在更改后正常工作， [!DNL Experience Manager] 检查是否未显示任何隐藏文件夹。

* 能够在 [!DNL Experience Manager Sites] 页面。

* 支持新用户使用邮件程序配置服务的刷新令牌刷新访问令牌。

* [支持SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) 邮件配置服务的机制。

* 支持 [!DNL MongoDB] 版本4.2和4.4。

* 与香港、澳门和台湾有关的名称的出现情况将根据适用于中国地区和地区的新命名惯例进行更新。

* 中的辅助功能增强功能 [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) 和 [[!DNL Dynamic Media]](#accessibility-dm-6590).

* 智能成像DPR（设备像素比）和网络带宽优化让您能够高效地交付最佳质量的图像；在具有高分辨率显示器和网络带宽受限的设备上。 有关详细信息和时间轴，请参阅 [智能成像常见问题解答](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] 投放(`fmt` URL修饰符)支持下一代图像格式AVIF（AV1图像格式）。 有关更多详细信息和时间轴，请参阅 [图像提供和渲染API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

* 能够使用 [!UICONTROL 分配任务] 工作流步骤。

* 能够在修改源交互式通信后检索交互式通信草稿。

* 设置自定义域名，以在中加载、渲染和验证reCAPTCHA服务 [!DNL Experience Manager Forms].

* 的输入数据增强功能 [!UICONTROL 调用表单数据模型服务] 工作流步骤。

* 能够在的记录文档模板中使用多个主控页面 [!DNL Experience Manager Forms].

* 支持记录文档中的分页符 [!DNL Experience Manager Forms].

* 内置存储库(Apache Jackrabbit Oak)已更新至1.22.7。

有关 [!DNL Experience Manager] 6.5.9.0，见 [的新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>从Service Pack 9开始， [!DNL Experience Manager] 客户可以开发和运营 [!DNL Experience Manager] 分布的应用程序 [!DNL Azul Zulu] 构建了OpenJDK，该JDK符合Java™ SE的标准。
>支持 [!DNL Azul Zulu] Adobe还会向 [!DNL Experience Manager] 客户。
>您可以下载 [!DNL Azul Zulu] 来自的JDK [AdobeSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>由Oracle分发的AdobeJava™技术的使用权限将于2022年12月底之前过期。 [!DNL Experience Manager] 我们鼓励客户规划和实施 [!DNL Azul Zulu] 此日期之前最新的JDK。 有关 [!DNL Oracle Java™] 技术和 [!DNL Azul Zulu] 技术，请参阅 [常见问题解答](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf).

以下是 [!DNL Experience Manager] 6.5.9.0版本。

### [!DNL Sites] {#sites-6590}

* 启用了“身份验证要求”属性的已发布页面不会重定向到登录页面并返回404错误消息(NPR-36354)。

* 创建超链接时，文本组件中无法使用搜索链接的选项(NPR-35849)。

* 使用 `com.day.cq.wcm.commons.ReferenceSearch` API。 它会影响 [!DNL Experience Manager] 服务器(NPR-36407)。

* 另一个大小调整的布局容器内的嵌套布局容器显示其子组件的列数不正确，从而导致这些组件未与网格对齐(NPR-36359)。

* 外部链接检查程序将有效的外部链接显示为无效链接(NPR-36289)。

* 显示引用一段时间后，引用面板开始显示错误消息(NPR-36167)。

* 移动组件时，自动创建的Parsys不具有 `sling:resourceType` 节点(NPR-36165)。

* 尝试同步Live Copy时（使用转出配置时） [!UICONTROL 激活Blueprint时激活] 和 [!UICONTROL 在Blueprint激活时取消激活])，则当某个组件在Live Copy主控中删除时，同步会失败，并且 `NullPointerException` 已记录(NPR-36127)。

* 当用户键入标记的临时文本（系统中不存在的标记）并按Enter时，该标记会显示在字段下方，但当内容片段被保存并重新打开时，临时标记会消失(NPR-36132)。

* 收件箱中没有显示异步操作状态的选项(NPR-36104)。

* 恢复继承后会创建重复的组件(NPR-36000)。

* 使用 `RemoteContentRenderingService`，向 `RemoteContentRendererRequestHandler.getRequest` 始终包含的根页面  `ComponentExporter`，但不包含请求的页面（如果根模型未根据遍历深度和筛选选项集包含该页面）。 请求必须始终包含请求的页面，以便SPA具有足够的信息来渲染响应(NPR-35961)。

* onTime/offTime项目不会在预期的onTime/offTime上激活/取消激活(NPR-35936)。

* 在发布包含没有的体验片段的页面时 `cq:lastModified` 资产， a `NullPointerException` 发生(NPR-35914)。

* 尝试在容器中调整组件大小时，无法重新调整到原始大小。 减小组件容器大小时，无法将大小重新设置为原始容器(NPR-35809)。

* 在转出对话框中（在编辑器中或从Live Copy概述中触发），“已分离”、“已暂停”或“未创建”页面的状态图标错误(NPR-35691)。

* 主控忽略转出页面和子页面的多站点管理器转出页面属性复选框(NPR-35634)。

* 触屏UI中缺少经典UI中可用的恢复树功能(CQ-4315352、CQ-4309415)。

* 在 [!DNL Experience Manager Sites] 页面(NPR-36033)。

### [!DNL Assets] {#assets-6590}

在 [!DNL Assets]:

* 要查看未基于以下任一 [!UICONTROL 创建], [!UICONTROL 修改]或 [!UICONTROL 名称] 参数， [!DNL Adobe Experience Manager] 选件 [!UICONTROL 无] 选项 [!UICONTROL 排序依据] 选项。 的 [!UICONTROL 无] 选项可确保“资产”用户界面（在“卡片”、“列”和“分析”视图中）中的资产与JCR节点中资产的顺序相同(NPR-36356)。

* 在ACP API响应中，将电子邮件ID设为小写，来自 [!DNL Adobe Experience Manager] 引入了可选设置；作为 [!DNL Adobe Asset Link] 如果用户的ID没有全部使用小写字符，则用户无法签入资产。 的 [!DNL Adobe Asset Link] 面板使用来自的ACP API响应 [!DNL Adobe Experience Manager] (CQ-4317704)。

在 [!DNL Assets] 作为service pack 9的一部分：

对以下文本和图标的对比度（与背景）进行了改进，以便视力和颜色感知受限的用户能够理解：

* 上的资产标题 [!UICONTROL 属性] 页面(NPR-35967)。
* 星级评级图标 [!UICONTROL 评级] 部分(NPR-36009)。
* 资产和文件夹卡片视图上的文本(NPR-35966)。
* 上的占位符文本 [!UICONTROL 时间轴] 视图(NPR-35965)。
* 资产搜索结果上的资产名称(NPR-35964)。
* 上的占位符文本 [!UICONTROL 链接共享] 对话框(NPR-35963)。
* [!UICONTROL 元数据], [!UICONTROL 状态]和 [!UICONTROL 其他] 文本 [!UICONTROL 列表] 选项 [!UICONTROL 查看设置] 对话框(NPR-35910)。
* [!UICONTROL 位置] 和 [!UICONTROL 要搜索的类型] 全局搜索中的占位符文本(NPR-35909)。
* 展开和折叠 [!UICONTROL 内容树] (NPR-35908)。
* 的 [!UICONTROL 资产] 显示资产文件夹的页面上的文本(NPR-35905)。
* 中的文本 [!UICONTROL 资产元数据], [!UICONTROL 使用情况统计信息] within [!UICONTROL 概述] 选项(NPR-35904)。
* 快捷键的文本 [!UICONTROL 属性] 和 [!UICONTROL 编辑] 资产详细信息页面中的选项(NPR-35904)。

中提供了以下错误修复 [!DNL Assets] 作为service pack 9的一部分：

* 从 [!UICONTROL 文件夹元数据架构] 表单未保存(NPR-36119)。

* 当使用小椭圆对资产添加注释时，该椭圆与打印版本中的注释数量重叠(NPR-36114)。

* 有时，在列视图中， [!DNL Experience Manager] 上传重复的资产时，不会提示出现重复的资产冲突(NPR-36048)。

* 如果共享链接对话框处于打开状态且未进行任何更改，则单击关闭按钮不会将其关闭(NPR-36030)。

* 选择多个资产以更新属性时，有时会发生错误，或更新已取消选择资产的属性(NPR-36002)。

* 当资产上传时，在资产文件名的开头或结尾处添加空格，其余字符与存储库中现有资产的名称相同，则会替换现有资产，而不会记录任何错误(NPR-36001)。

* 在资产详细信息页面中播放视频时，播放和暂停选项不起作用(NPR-35999)。

* 批量取消发布资产时，Brand Portal会生成一个错误，提示请求URI太长(NPR-35954)。

* 打印具有长注释文本的资产时，即使有空格，注释文本也会被裁剪(NPR-35948)。

* 在“创建目录”页面上的“选择模板”视图上选择该页面时，将禁用用于移动到下一页的选项(CQ-4315462)。

* 在视频资产上启动更新资产工作流后，页面会重复刷新(CQ-4313375)。

* 无法删除或移动DAM文件夹，并记录异常(NPR-35942)。

### [!DNL Dynamic Media] {#dynamic-media-6590}

在 [!DNL Adobe Experience Manager] 6.5.9.0中提供了以下辅助功能增强功能 [!DNL Dynamic Media]:

* 当您打开对话框以使用键盘键在 [!UICONTROL 图像集] 编辑器：
   * 屏幕阅读器会讲述该对话框是否已打开。
   * 键盘焦点在打开时移至对话框。
   * 关闭对话框后，键盘焦点会移回“添加资产”选项(CQ-4312134)。

* 您现在可以在热点编辑器中使用键盘键在资产上添加和编辑热点(CQ-4305965)。

* 现在，您可以使用键盘键通过热点管理将超链接置于热点上。 屏幕阅读器焦点现在移至字段以编辑URL路径，并选择打开选择对话框(CQ-4290735)。

* 改进了“图像集编辑器”页面上文本和控件的对比度（与背景），使视力和颜色感知受限的用户能够理解(CQ-4290733)。

* 现在，您可以导航到查看器预设编辑器上的资产共享选项，然后使用键盘键折叠展开的共享选项(CQ-4290724)。

* 现在，您可以使用键盘键在“编辑视频编码”页面的基本和高级选项卡上导航和查看信息图标和警报图标的工具提示(CQ-4290722)。

* 屏幕阅读器现在在查看器预设编辑器的外观选项卡和行为选项卡中讲述各个字段的说明(CQ-4290721)。

* 在表单模式下导航“编辑图像预设”页面时，屏幕阅读器会讲述各个字段和控件的用途和名称(CQ-4290717)。

* 现在，在导览资产详细信息页面时，屏幕阅读器会介绍查看器中各种选项的用途(CQ-4290716)。

* 资产详细信息页面的占位符文本的对比度（与背景）“所有演绎版”选项得到了改进，以便视力和颜色感知受限的用户能够理解(CQ-4290713)。

* 用于表示必填字段的可视星号现在在图像集编辑器的资产标题字段中提供，屏幕阅读器会朗读该字段的必填信息(CQ-4290712)。

* 屏幕阅读器现在可以在资产详细信息页面的查看器中访问并讲述各种交互式选项的用途(CQ-4290708)。

Adobe Experience Manager 6.5.9.0资产修复了 [!DNL Dynamic Media]:

* 自定义查看器预设和CSS不会复制到 [!DNL Dynamic Media] when [!DNL Dynamic Media] 选择性地激活和禁用 [默认](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) (NPR-36232)。

* 尝试在资产详细信息页面上预览视频演绎版时，视频加载速度缓慢(CQ-4320122)。

* 在启用了重复资产检测器的情况下上传200多个资产时，浏览器页面无响应且速度会减慢(CQ-4319633)。

* 在页面的全景媒体组件中添加全景图像资产时，将记录“未捕获引用”错误(CQ-4317666)。

* 使用体验片段实施交互式媒体查看器时，不会从发布者中打开体验片段，并记录错误(CQ-4317655)。

* [!UICONTROL 发布到Dynamic Media] 选项在 [!UICONTROL 快速发布] 选项 [!UICONTROL 属性] 页面(CQ-4317199)。

* 具有只读权限的网站作者可以在资产上使用智能裁剪功能，并编辑智能裁剪演绎版(CQ-4316450)。

* 视频注释不适用于文件夹路径，其中 [!DNL Dynamic Media] 未启用配置，即使 [!DNL Experience Manager] 在中设置实例 [!DNL Dynamic Media] 模式(CQ-4314950)。

* 当资产标题具有双字节、多字节、高ASCII、西里尔文、代理对、希伯来语、阿拉伯语和GB18030字符时，资产标题将带有问号(?) (CQ-4311872).

>Dynamic Media中的已知视频播放问题 *仅在Experience Manager6.5.9.0上*:
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### 平台 {#platform-6590}

* 在为Blueprint生成缩略图并将更改转出到Live Copy时，某些字段的继承不起作用(CQ-4319517)。

* 创建文件夹时，选择可排序属性，并向文件夹添加20多个资产，选择文件夹中的所有资产会显示错误计数(CQ-4316243)。

* 刷新页面时，对文件夹或资产进行排序，不会显示相应的结果(CQ-4316200)。

* Handlebars JavaScript库已升级到v4.7.7(NPR-36375)。

* 使用包管理器安装新代码包时，自定义包不会更新(NPR-35949)。

* A `resourceresolver` Sling包导致 `Sling:alias` 查询失败(NPR-35335)。

* 在Experience Manager中设置SSL时，上下文路径将被删除(NPR-35294)。

* 的 `SegmentNotFound` 长时间运行的会话后返回异常(NPR-36405)。

### 集成 {#integrations-6590}

* 无法保存为Cloud Services体验片段启用继承的页面属性(NPR-36107)。

* IMS用户界面分页和延迟加载不显示相应结果(NPR-36046)。

* 在创建A4T Target配置并将报表源选择为 [!DNL Adobe Analytics]，则下拉列表中没有启用Adobe Target的报表包可用(NPR-36006)。

### 项目 {#projects-6590}

* 无法保存项目的属性，因为项目的JCR路径由于额外的正斜杠(`/`)附加到项目路径(NPR-36191)。

### 屏幕 {#screens-6590}

* [!DNL Experience Manager Screens] 如果使用自定义的双重身份验证处理程序，则播放器无法进行身份验证(NPR-35854)。

### 商务 {#commerce-6590}

* 的 [!UICONTROL 商务目录] 向导无法在“列”视图中加载40多个项目(CQ-4318379)。

### 翻译项目 {#translation-6590}

* 在重译 `es` to `es_es` 页面(NPR-36170)。

* 为具有人工翻译的项目选择自动批准选项后，作业状态显示为 `Unknown` (NPR-35981)。

* 在翻译页面时， [!DNL Experience Fragments] 未更新到目标 [!DNL Experience Fragment] 引用路径(NPR-35911)。

* 在父页面和子页面中进行更改并发送父页面进行翻译时，子页面也会被错误翻译(NPR-35896)。

* 如果选定页面有多个并行翻译项目，则 [!UICONTROL 转到项目] 选项不会链接到最新的翻译项目(NPR-35454)。

* 将资产发布到 [!DNL Dynamic Media], [!DNL Experience Manager] 未发布的标记显示错误消息(CQ-4315914、CQ-4315913)。

* 打开已删除的作业时， [!DNL Experience Manager] 显示错误消息(CQ-4315910)。

### 工作流 {#workflow-6590}

* 对收件箱中可用的项目单击完成、委派或打开操作后，看不到完成这些操作的任何可见线索(NPR-36317)。

### [!DNL Communities] {#communities-6590}

* 在垃圾邮件过滤中，系统会占用100%的Java™堆空间，从而导致Experience Manager服务器无响应(NPR-36316、NPR-36493)。
* 在论坛中，JCR会话数据源自 `SearchCommentSocialComponentListProvider` 被泄露(NPR-36235)。
* 打开特定收件箱消息会反映所有分页不正确的消息以及其他问题(NPR-35917)。

### [!DNL Brand Portal] {#brandportal-6590}

* 在配置时，将自动启用资产源功能标记 [!DNL Experience Manager Assets] with [!DNL Brand Portal] (NPR-36010)。

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。


**自适应表单**

* 中的语言初始化问题 [!DNL Experience Manager Forms] 6.5.7.0生成多个翻译字典时(NPR-36439)。
* 在向自适应表单片段添加附件并提交表单时， [!DNL Experience Manager Forms] 显示以下错误消息(NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 当您使用人工翻译更新字典并预览自适应表单时，不会显示修改(NPR-36035)。

**交互式通信**

* 使用交互式通信打印渠道上传图像并对其进行编辑时，该图像不再可见(NPR-36518)。

* 编辑文本资产和填充占位符时，将从导航窗格中删除所有交互元素(NPR-35991)。

**工作流**

* 调用的REST端点时 [!DNL Experience Manager Forms] 在JBoss®上提供服务， [!DNL Experience Manager] 显示以下错误消息(NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**后端集成**

* 将读取服务参数绑定到包含短划线的文字值时，无法保存表单数据模型(NPR-36366)。

**文档安全**

* 当您为GlobalSign设置认证和HSM时， [!DNL Experience Manager Forms] 显示 `Unsuported Algorithm` 和 `Invalid TSA Certificate` 向LTV添加时间戳时出错消息(NPR-36026、NPR-36025)。

**文档服务**

* 更新了 [!DNL Gibson] 与集成的库 [!DNL Experience Manager Forms] (NPR-36211)。

**Foundation JEE**

* 在AdminUI中选择端点管理时， [!DNL Experience Manager Forms] 显示 `endpoint registry failure` 错误消息(CQ-4320249)。

有关安全更新的信息，请参阅 [[!DNL Experience Manager] 安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html).

### Experience Manager6.5.9.0中的已知问题 {#known-issues-6590}

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 5或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## [!DNL Adobe Experience Manager] 6.5.8.0 {#experience-manager-6580}

[!DNL Adobe Experience Manager] 6.5.8.0包含自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。 Service Pack安装在 [!DNL Adobe Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.8.0包括：

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 使用 [“连接的资产”功能](/help/assets/use-assets-across-connected-assets-instances.md)，您现在可以查看 [!DNL Sites] 使用资产的页面。 资产的 [!UICONTROL 属性] 页面。 这允许管理员、营销人员和管理员全面了解资产使用情况，从而实现更好的跟踪、管理和品牌一致性。

* 删除网页中引用的资产时， [!DNL Experience Manager] [显示警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). 您可以强制删除引用的资产，或检查并修改 [!DNL Properties] 页面。 单击引用将打开本地和远程 [!DNL Sites] 页面。

* 使用对可用于转出的Live Copy页面进行排序 [!UICONTROL 名称], [!UICONTROL 上次修改日期，] 和 [!UICONTROL 上次转出日期] 属性。

* 内置存储库(Apache Jackrabbit Oak)已更新至1.22.6。 <!-- TBD: Mention the version -->

有关 [!DNL Experience Manager] 6.5.8.0，见 [的新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

以下是 [!DNL Experience Manager] 6.5.8.0版本。

### [!DNL Sites] {#sites-6580}

* 将页面移动到Blueprint后，链接的目标不会更新(NPR-35724)。
* 基于Tizen的播放器无法在某些浏览器上进行身份验证。 不支持samesite=none属性的浏览器出现问题(NPR-35589)。
* 已解锁的响应式容器不显示允许的组件(NPR-35565)。
* 创建新添加页面的Live Copy时，语言主控会为每个域创建两个副本(NPR-35545)。
* 当由于 `org.apache.felix.scr.impl.ComponentRegistry` 计时器。 因此， [!DNL Experience Manager] 停止无限期响应(GRANITE-33125、FELIX-6252)。
* 在侧边栏中搜索特定资产时，结果中会包含一些未搜索的资产(NPR-35524)。
* 为Experience Manager实例启用SSL时，上下文路径将被删除(NPR-35477)。
* 创建列表时，将一些文本添加为第一个元素，将一个表添加为第二个元素，并在表内添加一个列表，父列表会扭曲(NPR-35465)。
* 如果对连续的列表项目使用不同的插件，则 <br> 标记会添加到列表项目(NPR-35464)。
* 将列表放置在两个段落之间时，无法向列表添加表(NPR-35356)。
* 开始从AEM 6.3升级到AEM 6.5的AEM实例时，启动升级实例会花费较长时间(NPR-35323)。
* 复制包含括号()的AEM资产时。 在名称中，复制失败(GRANITE-27004、NPR-35315)。
* 向富文本编辑器添加标题时，段落按钮处于禁用状态(NPR-35256)。
* 将项目添加到现有列表时，将删除后续的可折叠或切换列表(NPR-35206)。
* 选择转出页面选项后，将显示一个包含所有可用Live Copy的对话框，并自动转出。 页面的Live Copy将在所有地理位置推出，而无需用户操作(NPR-35138)。
* 使用“包括子项”选项时，“管理发布”选项不会列出所有页面。 仅列出22页(NPR-35086)。
* 编辑策略时，文本组件不会保留策略更改(NPR-35070)。
* 当缩进编号列表中的某些项目时，所有项目都会保持相同的编号，但对于具有相同缩进的项目，编号应从1开始(CQ-4313011)。
* 启用缩小后，您将无法编辑任何页面或组件。 安装AEM 6.5 Service Pack 7后，便开始出现问题(CQ-4311133)。
* Omni搜索和资产过滤器会返回不相关或没有结果(CQ-4312322、NPR-35793)。
* 当多个页面同时访问客户端库时，HTML库管理器无法加载客户端库。 这会导致页面呈现不正确(NPR-35538)。
* 在中设置SSL时，上下文路径会自动删除 [!DNL Experience Manager] (NPR-35294)。
* 单击“注销”选项后，包管理器不会注销用户(NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 [!DNL Assets] 修复了以下问题并提供了以下增强功能。

* 恢复资产的早期版本时，OSGi控制台中不会触发事件DamEvent.Type RESTORED(NPR-35789)。
* `IndexWriter.merge` 原因 `OutOfMemoryError` 智能标记功能会创建大量错误 `/oak:index/lucene` 和 `/oak:index/ntBaseLucene` 索引(NPR-35651)。
* 尝试保存时，会显示错误消息 [!UICONTROL 资产贡献] 键入名称中包含多字节字符的文件夹(NPR-35605)。
* 使用级联元数据子类型字段时，出现错误的“请填写此字段”错误(NPR-35643)。
* 将现有资产拖动到 [!DNL Assets] 用户界面并创建新版本后，元数据中的更改不会持久保留(NPR-34940)。
* 在元数据架构编辑器中为级联菜单创建规则时， [!UICONTROL 取决于] 选项会重复同一名称(NPR-35596)。
* 编辑后，相似性搜索不起作用 [!UICONTROL 资产管理搜索边栏] (NPR-35588)。
* 在文件夹中，如果您通过单击 [!UICONTROL 过滤器]，中的过滤器 [!UICONTROL 状态] > [!UICONTROL 结帐] > [!UICONTROL 已签出] 不起作用(NPR-35530)。
* 如果您尝试删除资产的所有智能标记并保存更改，则不会删除这些标记。 但是，用户界面会指示已保存更改(NPR-35519)。
* 用户无法在可排序文件夹的列表视图中重新排列或排序资产(NPR-35516)。
* 如果您编辑默认的元数据架构，则资产的 [!UICONTROL 属性] 页面会变为文本字段。 这项更改允许不了解的用户添加按需标记，并且这些标记将作为字符串存储在存储库中(NPR-35478)。
* 下载资产时，如果您提供的名称没有有效的电子邮件地址，则下载选项将不可用。 但是，如果选择了下载对话框中的其他选项，则会启用按钮，但不会发送电子邮件(NPR-35365)。
* 用户在中编辑资产后无法签入资产 [!DNL Adobe InDesign] 和收到有关缺少权限的错误(NPR-35341)。
* Handlebars JavaScript库已升级到v4.7.6(NPR-35333)。
* 当您从批量元数据编辑开始并取消选择项目时，元数据编辑器界面会停止按预期工作，直到保留选中单个项目为止(NPR-35144)。
* 全局导航在从中单击时，无法打开正确的控制台 `assets.html` 页面(CQ-4312311)。
* [!DNL Assets] 不显示具有RGB演绎版的RGB演绎版(CQ-4310190)。
* 的 [!UICONTROL 关联] 的 [!UICONTROL 属性] 页面(CQ-4310188)。
* 如果使用文档的文件类型过滤器搜索资产并创建智能收藏集，则在访问收藏集时不会应用该过滤器。 而是会在搜索中显示所有类型的资产(NPR-35759)。
* 您不能从 [!DNL Assets] 用户界面(NPR-35901)。
* 在解决命名冲突后创建现有资产的新版本时，会覆盖原始资产的元数据(CQ-4313594)。
* 当您使用搜索过滤器或谓词过滤资产搜索时，打开资产以查看或编辑资产，然后返回到搜索结果页面，则该过滤器不起作用。 所有搜索的资产都将列出为未过滤资产(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* 资产详细信息页面上启用了RESS图像预设的URL选项。 现在，在动态演绎版部分中选择RESS图像预设后，资产详细信息页面上会提供URL和RESS选项。 (CQ-4311241)
* 交互式媒体组件 — 如果用户具有 [!DNL Experience Manager] (CQ-4311054)。
* 如果您跨文件夹移动资产，则同步 [!DNL Experience Manager] 和 [!DNL Dynamic Media–Scene7] 通过API的速度非常慢(CQ-4310001)。
* 使用Omnisearch时，日志大小会显着增加(CQ-4309153)。
* 启用选择性同步并将资产复制（未移动）到同步文件夹中后，它不会按预期同步(CQ-4307122)。
* 对于自动发布到DM的已上传资产，状态不会在AEM上显示“已发布”。 此外，Dynamic Media发布状态列不显示正确的已发布状态(CQ-4306415)。
* 如果资产在 [!DNL Experience Manager] 和设置为 [!DNL Dynamic Media] 激活时， `scene7FileStatus` 元数据值未按预期进行更新(CQ-4308269)。
* 编辑视频配置文件时， [!DNL Experience Manager] 不显示为视频预设设置的高度和比特率值。 字段显示为空(CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* 无法为商务中的所有产品创建自定义标记(CQ-4310682)。

* 产品资产引用更新会导致复制线程处于等待状态，直到ProductAssetListener线程完成对JCR的提交为止(NPR-35269)。

### 平台 {#platform-6580}

* 在使用不带选项卡的Coral选项卡视图组件后触发Foundation验证器时，会出现以下错误(NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 对于名称中包含逗号的节点，其删除事件的SCD转发复制失败(NPR-35191)。

* 升级到AEM 6.5.7后，内部版本开始失败。 原因是，uber-jar中嵌入了旧版本或没有jackson-core(GRANITE-33006)。

### 用户界面 {#ui-6580}

* 在“资产”控制台中，当您从文件夹中的文档的卡片视图切换到列表视图时，无法正确排序(NPR-35842)。

* 在文本组件中超链接文本时，搜索功能不显示相应的结果(NPR-35849)。

* 如果未将值提供给标记为必填的隐藏字段，则会阻止您保存组件(NPR-35219)。

### 集成 {#integrations-6580}

* 当您对IMS租户ID和Target客户端代码使用不同的值时， [!DNL Experience Manager] 集成失败 [!DNL Adobe Target] (NPR-35342)。

### 翻译项目 {#translation-6580}

* 在中导出或导入翻译作业时出现问题 [!DNL Experience Manager] (NPR-35259)。

### 营销活动 {#campaign-6580}

* 在触屏UI中使用现成模板创建促销活动页面，并打开页面属性对话框中的“电子邮件”选项卡时，主题和正文字段的个性化变量保持禁用状态(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* 向社区组添加页面结构时， [!UICONTROL 组] 痕迹导航中的标题将更改为第一个 [!UICONTROL 页面] (NPR-35803)。
* 与审核者不同，标准社区成员无法访问和编辑任何草稿帖子(NPR-35339)。
* 中断的访问控制和拒绝服务 `DSRPReindexServlet` 这会将社区站点一直拉下来，直到索引完成(NPR-35591)。
* 删除 [!UICONTROL 所有用户] 从 [!UICONTROL 管理员] 字段不会实际从后端删除它们(NPR-35592、NPR-35611)。
* 的 [!UICONTROL 撰写消息] 当输入的文本与部分匹配时，组件不会返回任何结果(NPR-35666)。

* 尝试通过选择 **[!UICONTROL 添加标记]**. 要提高性能，请安装 [cqTagLucene-0.0.1.zip修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip).

### [!DNL Brand Portal] {#brandportal-6580}

* 将成员添加到 [!UICONTROL 资产贡献] 类型文件夹显示 [!UICONTROL 添加用户或群组] 用户界面中的描述，尽管仅支持Brand Portal活动用户，而不支持组(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。

**自适应表单**

* 将具有可重复行的表插入到在自适应表单中具有多个实例的可重复面板时，始终会将该表添加到面板的第一个实例(NPR-35635)。

* 当制表符焦点在自适应表单中成功验证一次后再次到达CAPTCHA组件时， [!DNL Experience Manager Forms] 显示 `Provide Captcha phrase to proceed` 错误消息(NPR-35539)。

**交互式通信**

* 提交翻译后的表单时，提交消息将以英语显示，且不会翻译成相应的语言(NPR-35808)。

* 在附加的XDP或文档片段中包含隐藏条件时，交互式通信无法加载(NPR-35745)。

**通信管理**

* 编辑信件时，包含条件的模块需要较长时间才能加载(NPR-35325)。

* 从左侧导航窗格中选择信件中未包含的资产，然后选择下一个资产时，不会从之前选择的资产中删除蓝色突出显示(NPR-35851)。

* 编辑信件中的文本字段时， [!DNL Experience Manager Forms] 显示 `Text Edit Failed` 错误消息(CQ-4313770)。

**工作流**

* 当您尝试在 [!DNL Experience Manager Forms] 适用于iOS的移动应用程序时，该应用程序会停止响应(CQ-4314825)。

* 的 [!UICONTROL 待办事项] 选项卡，会显示HTML字符(NPR-35298)。

**XMLFM**

* 使用输出服务生成XML文档时， `OutputServiceException` 某些XML文件(CQ-4311341、CQ-4313893)出错。

* 将上标属性应用于项目符号的第一个字符时，项目符号大小会变小(CQ-4306476)。

* 使用输出服务生成的PDF forms不包括边框(CQ-4312564)。

**Designer**

* 在中打开XDP文件时 [!DNL Experience Manager Forms] Designer，将在与XDP文件(CQ-4309427、CQ-4310865)相同的文件夹中生成designer.log文件。

**HTML5 表单**

* 当您在 [!DNL Safari] Web浏览器 [!DNL iOS 14.1 or 14.2]，则不显示其他字段(NPR-35652)。

**Forms管理**

* 没有确认消息来指示XDP文件已成功批量上传到CRX存储库(NPR-35546)。

**文档安全**

* 针对 [!UICONTROL 编辑策略] 选项(NPR-35747)。

### Experience Manager6.5.8.0中的已知问题 {#known-issues-6580}

* 如果您要升级 [!DNL Experience Manager] 实例从6.5到6.5.8.0版本，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 重新启动实例以解决问题。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 5或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果在中编辑和创建级联规则时遇到问题，请联系Adobe客户支持 [!UICONTROL 文件夹元数据架构Forms编辑器] 和 [!UICONTROL 元数据架构Forms编辑器] 使用 [!UICONTROL 定义规则] 对话框。 已创建和保存的规则可按预期运行。

* 如果层级中的文件夹在 [!DNL Experience Manager Assets] ，则包含资产的嵌套文件夹会发布到 [!DNL Brand Portal]，则文件夹的标题不会在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 如果 [!UICONTROL 连接的资产配置] 向导在安装后返回404错误消息，请手动重新安装 `cq-remotedam-client-ui-content` 和 `cq-remotedam-client-ui-components` 包。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## [!DNL Adobe Experience Manager] 6.5.7.0 {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0是一项重要更新，其中包括自2019年4月6.5版发布以来发布的新功能、关键客户请求的增强功能以及性能、稳定性和安全性改进。 Service Pack安装在 [!DNL Adobe Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.7.0包括：

* 将页面移动和MSM转出作为异步操作执行，以减少它们对运行时性能的影响。

* 用户可以在卡片视图和列视图中对数字资产进行排序。

* [!DNL Assets] 和 [!DNL Dynamic Media] 提供了多项辅助功能增强功能。 这些增强功能与键盘导航、屏幕阅读器的使用以及用户使用类似的辅助技术(AT)相关。 请参阅 [[!DNL Assets] 增强功能](#assets-6570) 和 [[!DNL Dynamic Media] 增强功能](#dynamic-media-6570).

* [表单数据模型HTTP客户端配置](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 以优化性能。

* [每个组件的重置选项可用性](../../help/forms/using/resize-using-layout-mode.md#resize-components) 在布局模式下

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms改进了以下性能：

   * 在提交自适应表单时验证服务器上的字段值。

   * 使用将PDF表单转换为自适应表单 [!DNL Automated Forms Conversion service].

* 支持 [!DNL Microsoft SQL Server] 2019英寸 [!DNL Experience Manager Forms].

* 支持 [!DNL Microsoft] SQL Server 2016始终处于可用性组上，以实现OSGi部署的高可用性。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.5。

有关 [!DNL Experience Manager] 6.5.7.0，见 [的新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

以下是 [!DNL Experience Manager] 6.5.7.0版本。

### [!DNL Sites] {#sites-6570}

* 当您打开 [!UICONTROL 时间换行] 选项，保持时间轴侧边栏选项处于打开状态，然后导航到 [!UICONTROL 站点] 控制台， `Failed to Load` 出现错误(NPR-34951)。

* 的 [!UICONTROL 时间换行] 选项不显示选定日期和时间范围的图像(NPR-34951)。

* 当过滤器调用 `getHeader()` 从包含内容片段的页面中， `java.lang.AbstractMethodError` 出现错误(NPR-34942)。

* 当页面的路径包含多个内容子字符串时，无法渲染预览，并且版本比较函数也失败(NPR-34740)。

* 当您为 `String` 键入组件的label属性，则可以删除组件并撤消删除操作。 但是，撤消删除后，标签属性会从 `String` to `Long` (NPR-34739)。

* 基于具有锁定布局的模板将体验片段添加到页面时发生以下异常(NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 移动文件夹时，会导致遍历问题，并出现以下错误(NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 创建、发布新资产并将其移动到新位置后， `Request to complete move operation` 将创建工作流，并导致出现“中止”状态。 上传新资产并执行 `move` 操作结果创建 `Request to complete move operation` 工作流处于待处理状态(NPR-34543)。

* 从导出体验片段时 [!DNL Experience Manager] 6.5.2环境到 [!DNL Target] Standard中，API调用失败，因为工作区属性不可用于 [!DNL Target] 标准(NPR-34557)。

* 用户无法通过 [!UICONTROL 管理发布] 选项，因为 [!UICONTROL 发布] 选项会消失(NPR-34542)。

* 在文本中添加一些样式时， `<div>` 标记已添加到文本中，且样式无法再应用于文本(NPR-34531)。

* 在弹出菜单中选择项目并更新所需文件时，不允许保存对话框值，因为其他菜单的必填字段为空(NPR-34529)。

* 从自定义模板创建页面并在Blueprint层次结构中移动该页面时，之前从页面中删除的组件开始显示在Live Copy层次结构中的页面上(NPR-34527)。

* 将文章样式应用于内容后，便无法删除该内容(NPR-34486)。

* 体验片段的所有Live Copy和副本都指向同一个 [!DNL Adobe Target] 选件ID(NPR-34469)。

* 项目符号列表项显示在编号列表之外(NPR-34455)。

* “与源比较”选项无法显示源页面与页面编辑版本之间的差异(NPR-34285)。

* 删除页面时，无法配置版本控制详细信息(NPR-34159)。

* 当用户选择 [!UICONTROL 打开选择] 对话框选项时，键盘焦点会移至页面上存在的隐藏控件(CQ-4307779、CQ-4293601)。

* 在作者上移动已发布的文件夹时，文件夹路径在发布实例上不会相应地更新(CQ-4305144)。

* 当用户选择 `Enter` 键 [!UICONTROL 全选] 选项，则键盘焦点不会移到 [!UICONTROL 创建控件] 选项(CQ-4293599)。

* 当您选择 `Esc` 键，则焦点不会还原到父控件(CQ-4293593、CQ-4293590)。

* 改进了 [!DNL Sites] UI和核心组件(CQ-4293448)。

* [!UICONTROL 缩放] 和 [!UICONTROL 缩放] 函数已禁用 [!DNL Sites Editor] 页面(CQ-4282353)。

* 使用“向右旋转”选项后，屏幕阅读器会停止讲述当前的旋转或反向状态(CQ-4282128)。

* 完成和取消配置对话框按钮有许多制表位(CQ-4274601)。

* 不允许在同一级别上移动名称相似的页面(NPR-35041)。

* 选择“清除(x)”选项后，键盘焦点不会移到 [!UICONTROL 过滤器] 字段(CQ-4293581)。

* 当您升级到 [!DNL Experience Manager] 6.5.6.0，继承段落系统的行为发生更改，并且无法正常工作(NPR-35117)。

* 选择 [!UICONTROL 操作] 部分 [!DNL AEM Sites] 页面(CQ-4307786)。

* 在编辑内容片段时，在RTE工具栏的链接目标菜单列表中选择一个选项后，内容片段创作对话框将开始闪烁(CQ-4305532)。

* 键盘用户无法在 [!UICONTROL 添加组件] 下拉列表（使用向下箭头键）(CQ-4295097)。

* 从 [!UICONTROL 资产] 选项卡 [!DNL Sites] 页面(CQ-4293600)。

* 在删除编辑站点页面时可用的链接或文本选项后，选项卡焦点不会转移到键盘用户的下一个或上一个选项(CQ-4293597)。

* 键盘用户无法将选项卡焦点切换回 [!UICONTROL 操作] 中的选项，然后按 `Esc` 键(CQ-4293592)。

* 激活 [!UICONTROL 旋转] 选项 [!UICONTROL 编辑] 模式时，选项卡焦点（而不是停留在“旋转”上）会移至 [!UICONTROL 重做] 选项(CQ-4293587)。

* 在 [!UICONTROL 打开选择] 对话框 [!UICONTROL 链接和操作] 选项卡，则选项卡焦点会在 [!UICONTROL 取消] 选项(CQ-4293579)。

* 键盘用户编辑图像时，导航到 [!UICONTROL 完成] ，然后按Enter键，屏幕阅读器不会宣布完成(CQ-4282351)。

* 在 [!UICONTROL 链接和操作] 屏幕阅读器和键盘用户无法使用对话框(CQ-4281120)。

* 在导航到 [!UICONTROL 属性] 页面(CQ-4293581、NPR-34653)。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 [!DNL Assets] 修复了以下问题并提供了以下增强功能。

* 对中的辅助功能进行了以下增强 [!DNL Experience Manager Assets] 在此版本中。 有关更多信息，请参阅 [辅助功能 [!DNL Assets]](/help/assets/accessibility.md).

   * 使用键盘导航时间轴时， `Esc` 键可以折叠 [!UICONTROL 显示全部] (CQ-4293598)。
   * 使用键盘Tab键导航时，在从添加的标记中删除最后一个标记后，标记字段会保留焦点(NPR-35109)。
   * [!DNL Experience Manager] 组件现在包含要供屏幕阅读器使用的名称、角色和值的相应信息(NPR-34255)。
   * 删除“类型/大小”组合框、“链接”组合框、“语言”组合框或“文本编辑”框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素(CQ-4293585)。
   * 将指针悬停在选项上时，会显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用删除选项后，可以保留焦点 `Escape` 键。 (CQ-4293554).
   * 从页面中存在的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏(CQ-4282127)。
   * 可视化用户可以区分普通文本和链接，因为在中，将显示指向所有解决方案的链接的可视线索（下划线和V形图标） [!DNL Experience Manager] 主页(CQ-4282072)。

* 在中完成了以下用户体验增强 [!DNL Assets]:

   * 在卡片视图和列视图中启用资产排序(NPR-35097)。

* 升级到6.5后，如果使用Assets HTTP API生成JSON文件，则文件中使用的编码会出现问题(NPR-35129)。

* 未提供创建收藏集权限（“创建收藏集”选项不可用）的组的用户仍可以通过直接访问URL来创建收藏集 `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115)。

* 按名称排序时，搜索的资产会区分大小写。 这会根据搜索结果中以有序方式显示的大小写，创建两个单独的排序列表(NPR-35068)。

* 在编辑器中打开内容片段时，出现警告消息(`Invalid value specified for a metadata property`)记录在错误日志中(NPR-35012)。

* 没有管理员权限的用户可以使用 [Experience Manager] 桌面应用程序。 (NPR-34993).

* 当在Assets用户界面中拖动同一资产并创建新版本时，元数据中的更改不会持久(NPR-34940)。

* 编辑收藏集时，用户可以删除收藏集的标题并成功保存更改(NPR-34889)。

* 上传重复图像时，会显示删除选项。 选择删除可上传图像。 还会触发DAM更新资产工作流(NPR-34744)。

* 使用 [!DNL Adobe Asset Link] with [!DNL Adobe InDesign]，则搜索结果中不包含文件夹和收藏集，但只包含资产(NPR-34699、CQ-4303666)。

* 将指针悬停在卡片视图上时，屏幕会因（自动）聚焦卡片中可用的快速操作而滚动(NPR-34514)。

* 批量编辑多个资产的属性时，请选择 [!UICONTROL 保存] 选项会关闭批量编辑器视图并重定向到主 [!DNL Assets] 页面。 此行为与 [!UICONTROL 保存并关闭] 选项，且不为预期(NPR-34546)。

* 智能收藏集在保存后不显示正确的用户界面设置。 查询已正确保存，但界面始终显示最后添加的“选项”谓词(NPR-34539)。

* 将资产添加到 [!DNL Experience Manager]，将无法导入没有命名空间的元数据(NPR-34530)。

* 在文件夹上拖动资产以移动资产时，用户界面还会显示 [!UICONTROL 放入灯箱] 和 [!UICONTROL 放入收藏集]. 即使取消移动操作，用户界面仍会继续显示后两个选项(NPR-34526)。

* 符号 `%>` 显示在收藏集页面上(NPR-34499)。

* 在列视图中， [!DNL Assets] 在显示所有资产之前，向上和向下滚动时，会显示重复的文件夹和资产名称(NPR-34464)。

* 如果您在创建公用文件夹后立即创建专用文件夹，则公用文件夹会使用专用文件夹设置(NPR-34415)。

* 在卡片视图中，卡片未按字母顺序列出，且卡片无法按字母顺序排序(NPR-34234)。

* 重新打开级联规则时，用户界面上不会保留所做的选择(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* 对中的辅助功能进行了以下增强 [!DNL Dynamic Media] (CQ-4290306)。 有关详细信息，请参阅 [辅助功能 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * 屏幕阅读器(JAWS、Narrator)在“嵌入大小”菜单选项中讲述菜单项的名称、角色和状态(CQ-4290927)。
   * 用户可以使用 `Tab` 键(CQ-4290926)。
   * 鉴于屏幕阅读器增强功能(CQ-4290623、CQ-4290622)，创建视频编码配置文件的工作流更易于用户使用。
   * 使用 `Tab` 键，焦点会移至工作流中相应的用户界面元素以创建交互式视频(CQ-4290621、CQ-4290620、CQ-4290619)。
   * 对“发布”页面、“编辑资产”页面、“编辑智能裁剪”页面和“图像集编辑器”页面进行了改进，以符合Web标准。 辅助技术(AT)用户现在可以轻松导航这些页面并执行裁剪图像等操作(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * 对查看器进行了改进，允许用户使用键盘进行导航(CQ-4290615)。
   * 键盘和屏幕阅读器用户可以使用裁剪功能(CQ-4290609)。
   * 键盘用户可以更好地管理热点(CQ-4290604、CQ-4290603)。

* 远程图像集在 [!DNL Experience Manager] 如果公司名称和文件夹名称相同(NPR-31340)。

* 当您尝试在将热点添加到 [!DNL Dynamic Media] 图像或编辑后 [!DNL Dynamic Media] 视频或 [!DNL Experience Fragment] (CQ-4307267)。

* [!DNL Dynamic Media] 重新处理混合媒体集时，同步失败(CQ-4307184)。

* 如果资产被移动到自动同步到的文件夹 [!DNL Dynamic Media] 配置后，资产无法同步(CQ-4307122)。

* [!DNL Dynamic Media] 使用本机HTML5视频控件在iOS设备上不播放视频(CQ-4306977、CQ-4306727)。

* 无法下载应用了SmartCrop的图像(CQ-4304558)。

* 无法选择性地将文件夹发布到Dynamic Media(CQ-4304526)。

* 从中取消发布视频文件 [!DNL Experience Manager] 请勿从已配置的Scene7部署中取消发布自适应视频集(CQ-4304405)。

* 在全景媒体组件中添加全景图像资产并刷新页面会导致 `Uncaught ReferenceError: $ is not defined` 错误(CQ-4302810)。

* 在 [!UICONTROL 查看器预设编辑器]，编辑时 [!UICONTROL 全景图像/全景图像_VR] 预设，在 `PanoramicView` 组件， `PANORAMICVIEW_AUTOROTATE` 修饰符标签不可用(CQ-4302443)。

* 如果视频不是MixedMediaSet中的第一个视频，则不会显示视频字幕(CQ-4298161)。

* iPhone移动设备上的HTML5 eCatalog查看器无法翻页或翻页(CQ-4296611)。

* 在移动设备上滚动样本时，样本会在可见区域的右侧和外部滚动几秒钟，然后再滚动回视图(CQ-4296439)。

* 创建查看器预设主控记录后，不会发布CSS和图稿，而只发布查看器预设(CQ-4262205)。

* 尝试在 [!UICONTROL 交互式视频/图像] 组件中，它不显示选定的体验片段路径。 它而是会从路径字段中返回一个空值(NPR-35146、CQ-4298136)。

* 无法在IVV编辑器中预览体验片段(CQ-4308560)。

* 在向图像添加热点并选择体验片段时，无法选择子文件夹和体验片段的变体(CQ-4307455)。

* 上传后，非图像资产不会显示为已发布(CQ-4306415)。

#### [!DNL Experience Manager] 3D资产 {#three-d-assets-6570}

* `DAM CQ MIME Type` 服务将不正确的MIME类型应用于3D资产，从而导致呈现错误(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* 商务产品收藏集用户界面中的收藏集中未列出超过15个产品(NPR-34502)。

### 平台 {#platform-6570}

* 通过HTTPS的HTTP会话不会失效(NPR-35083)。
* A `NullPointerException` 从用户界面启动每日或每周维护任务时返回(NPR-34953)。
* W3C验证器报告兼容客户端库JavaScript文件的警告(NPR-34898)。
* 的 `AudienceOmniSearchHandler` 函数使用已弃用的索引(NPR-34870)。
* 从Experience Manager注销不会清除Cookie(NPR-34743)。
* 的 `findByTitle` 函数 `TagManager` 如果标记名称包含特殊字符，则API不起作用(NPR-34357)。
* 导入用户同步包的过程失败(NPR-34399)。
* 添加了 `ariaLabel` 和 `ariaLabelledby` 属性 `Coral.Masonry` 组件(GRANITE-29962)。
* 安装最新核心组件包后，对于包含内容片段的页面，不会刷新调度程序缓存(CQ-4306788)。
* 带引号的本地化标记名称(`"`)未在用户界面中正确显示(CQ-4305439)。

### 用户界面 {#ui-6570}

* 的 [!UICONTROL 链接到] 组件属性中的字段显示与指定字符串不匹配的自动完成建议(NPR-34865)。

* 当您计划在2天之间分发的每日维护时间范围时，AEM会显示以下错误消息(NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 集成 {#integrations-6570}

* 编辑现有 [!DNL Adobe Launch] 配置失败(NPR-35045)。
* 无法导出 [!DNL Experience Fragments] to [!DNL Adobe Target] 如果使用IMS配置，则 [!DNL Adobe Target Standard] 环境(NPR-34555)。
* 的 [!UICONTROL 创建] 选项 [!UICONTROL 受众] 页面 [!UICONTROL 受众] 页面(NPR-35151)。

### Sling {#sling-6570}

* 默认的登录运行状况检查将验证不存在的用户的凭据(NPR-34686)。

### 翻译项目 {#translation-6570}

* 关于在 [!DNL Experience Manager]，则不会向翻译提供商发送取消该页面的请求(NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 产品中所有不公平术语的实例都被接受的对等术语替换(NPR-34311)。
* [!DNL Google+] 已从社交共享选项列表中删除(NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* 在 [!UICONTROL 列表视图] (NPR-34728)。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含 [!DNL Forms]. 它们使用单独的 [!DNL Forms] 附加组件包。 此外，还发布了累积安装程序，其中包含针对 [!DNL Experience Manager Forms] 在JEE上。 有关更多信息，请参阅 [安装AEM Forms附加组件](#install-aem-forms-add-on-package) 和 [在JEE上安装AEM Forms](#install-aem-forms-jee-installer).

**自适应表单**

* 应用后，无法使用经典UI编辑自适应表单 [!DNL Experience Manager] Service Pack 6(NPR-35126)。

* 将PDF转换为自适应表单时，无法使用选项卡式布局上的表单数据模型为嵌套面板设置值。 此外，使用代码编辑器通过静态数组动态设置单选按钮组值时还会出现问题(NPR-35062)。

* 在自适应表单的文本字段组件中输入日语字符时，可以指定的字符数超过最大35个字符限制(NPR-35039)。

* 自适应表单显示不需要的参数，例如 `owner` 和 `status`，在 **[!UICONTROL 谢谢]** 页面(NPR-34989)。

* 的 [!UICONTROL 文件选择] 对话框 [!UICONTROL 附件] 组件显示不支持的文件类型以及在提交自适应表单期间由于选择而导致错误的选项(NPR-34970)。

* 在 [!DNL Experience Manager Sites] 包含表单前文本的页面中，光标焦点会直接移动到表单而不是表单前的文本(NPR-34947)。

* [!UICONTROL 使用数据预览] 使用 [!DNL Experience Manager] 6.2数据XML文件无法正常工作(NPR-35087)。

* 更新自适应表单的数据字典时，表单未被翻译，因为自适应表单返回缓存值(NPR-34845)。

* 由于缓存失效，以自适应形式加载片段需要较长时间(NPR-34567)。

* 自适应表单中的屏幕阅读器无法正常使用选项卡导航(NPR-34544)。

**通信管理**

* 无法将包含数字数据（包括浮点类型）的XML标记的值保存为草稿(NPR-35050)。

* 从ES3迁移资产时，这些资产包含两个不可编辑的默认条件(NPR-34972)。

* 在信件中编辑数据字典时， [!UICONTROL 借出内容] 部分显示旋转的矩形，而不是有用信息(NPR-34853)。

**交互式通信**

* 交互式通信的转出配置名称，安装后可用 [!DNL Forms] 附加组件包中，会复制标准转出配置名称(NPR-34976)。

**文档安全**

* 保存新文档安全策略时，Experience Manager Forms会显示 `Relative validity period is required` 错误消息(NPR-34679)。

* 文档安全无法保护PDF2.0文档(CQ-4305851)。

有关安全更新的信息，请参阅 [Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0是一项重要更新，其中包括自6.5版的正式发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进 **2019年4月**. 它可以安装在Adobe Experience Manager 6.5的顶部。

Adobe Experience Manager 6.5.6.0中引入的主要功能和增强功能包括：

* 有选择地将资产发布或取消发布到 [!DNL Experience Manager] 或 [!DNL Dynamic Media] 使用 [!UICONTROL 快速发布] 或 [!UICONTROL 管理发布] 向导。

* 使用 [!DNL Dynamic Media] 使内容交付网络(CDN)缓存内容失效的用户界面。

* 现在，还支持通过代理服务器将资产贡献文件夹从Brand Portal发布到Experience Manager Assets。

* 现在，在删除 [!DNL Experience Manager Assets].

* 视频中修饰符的描述 [!UICONTROL 查看器] 在中更新了预设编辑器 [!DNL Dynamic Media].

* 提供了新的公司设置，以反映 [!DNL Dynamic Media] 连接器。

* 的默认选项 `test` 和 `aiprocess` 已更新为 `Thumbnail`从 `Rasterize` 以前在Dynamic Media中，要确保用户只需创建缩略图，并跳过页面提取和关键词提取。

* [在客户端预填自适应表单](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [通过双向SSL实施，在服务器上与RESTful API形成数据模型集成](../../help/forms/using/configure-data-sources.md).

* [增强了已翻译的自适应表单页面的缓存](../../help/forms/using/configure-adaptive-forms-cache.md).

* 支持 [Adobe SignAutomated forms conversion服务中的文本标记](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* 支持 [将彩色表单转换为自适应表单](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) 使用 [!DNL Automated Forms Conversion service].

* 支持SMB 2和SMB 3协议。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.4。

有关Experience Manager6.5.6.0中引入的功能和增强功能的完整列表，请参阅 [Adobe Experience Manager 6.5 Service Pack 6的新增功能](new-features-latest-service-pack.md).

以下是 [!DNL Experience Manager] 6.5.6.0版本。

### [!DNL Sites] {#sites-6560}

* 在 [!DNL Sites] 或 [!DNL Screens]，选择一个项目并单击 [!UICONTROL 管理出版物]. 用户无法在 [!UICONTROL 管理发布] 向导。 具体而言， [!UICONTROL 发布] 选项无效(NPR-34099)。
* 取消选择后，iParsys（继承的段落系统）的位置不会恢复到其原始默认位置 [!UICONTROL 取消继承] 或 [!UICONTROL 禁用继承] 选项(NPR-34097)。
* 如果 `RolloutConfigManagerFactoryImpl` 无法加载转出配置，它不会尝试加载缺少的配置。 它会返回缓存的配置(NPR-34092)。
* 在文本核心组件中，使用源HTML编辑选项后， `em` 标记已删除(NPR-34081)。
* 从Experience Manager6.3.3升级到Experience Manager6.5.3后，转出过程会花费更长的时间，并且转出失败，并出现超时错误(NPR-34049)。
* 的 `htmlwriter` 不会对属性值进行编码。 XF标记中存在的标记用解码属性值(即 `"` 而不是 `&#34`)。 它会在使用导出的体验片段的可视化体验编辑器的Target端导致问题(NPR-34048)。
* 在 [!DNL Experience Manager Sites]，增强日志记录以捕获因故而导致的版本创建失败(NPR-34014)。
* 在 [!DNL Rich Text Editor] 如果删除了所有文本，则也会删除段落标记(NPR-33976)。
* 当 `siteadmin` 页面（在经典UI中）打开或刷新时， `New` 菜单被禁用(NPR-33949)。

   ![屏幕截图，以说明经典UI中缺少菜单的问题](assets/33949_missing_menu.png)

* A [!DNL Content Fragment] 不能用作 `TemplatedResource` 因为失败 `ContentFragmentUsePojo` (NPR-33911)。
* 同步和异步移动操作可能会导致并发传输导致错误。 页面移动操作仅限于异步移动。 它可防止页面并行移动(NPR-33875)。
* [!UICONTROL 管理发布] 将内容从创作实例复制到发布实例的操作失败，并生成JavaScript错误(NPR-33872)。
* 选择多个页面或资产以创建版本后，将仅为最后一个选定页面或资产创建新版本(NPR-33866)。
* 将包含Live Copy的Blueprint页面移动到其他文件夹。 将文件夹移到原始文件夹时，移动操作会失败，并且没有任何错误(NPR-33864)。
* 当使用移动操作来重命名 [!DNL Sites] 控制台中，向导的最后一步会显示两个重叠的对话框(NPR-33831)。

   ![屏幕截图以说明NPR-33831中重叠的移动对话框问题](assets/33831_rename_dialog.png)

* 的 `cq:acLinks` 和 `cq:acUUID` 属性 [!DNL Adobe Campaign] 在复制并粘贴操作期间，会删除复制上的(NPR-33794)。
* 尝试在分离的父Live Copy的子页面上转出时， [!DNL Experience Manager] 生成空指针异常(NPR-33676)。
* 的 [!DNL RTE] 再次在页面上复制并粘贴布局容器时，布局容器中的组件不可见。 的 [!DNL RTE] 组件不可编辑，但会在刷新页面时显示(NPR-33662)。
* 调整不同断点（中等和大）的布局组件大小时，布局的行为不按预期方式运行(NPR-33608)。
* 在内联编辑模式下， [!DNL RTE]，则对于文本组件无法拖动图像(NPR-33602)。
* 可以在Blueprint页面中使用与页面名称相同的名称创建组件。 在转出过程中， `_msm_moved` 后缀可重命名组件。 组件将移至 [!UICONTROL 段落系统] (NPR-33535)。
* 在许多页面或资产上设置offTime或onTime时，会占用大量资源，并会在启动和关闭期间减慢系统速度(NPR-33482)。
* 对具有CRUD权限的用户 `/content/experience-fragment` 无法删除文件夹(NPR-33436)。
* 您可以选择 [!UICONTROL HTML和JSON] 作为 [!UICONTROL Adobe Target导出格式] 在的父文件夹上 [!DNL Experience Fragments] 中。 此父文件夹的子文件夹的触屏UI中会显示相同的属性。 但是，在CRXDE中， `cq:adobeTargetExportFormat`，则它仅显示HTML而不显示 `html,json` (NPR-33423)。
* 不支持从页面别名发布或取消发布。 删除似乎另有声明的选项(NPR-33415)。
* 可以将特定标记从一个位置移动到 [!DNL Experience Manager]. 也可以在移动前后应用于不同的页面。 编辑页面属性时，即使标记相同，也不会显示标记进行编辑(NPR-33353)。
* 从包含多个布局容器的模板中删除布局容器时，页面模板无法正确呈现(NPR-33347)。
* 在模板编辑器中，尝试删除下超过100000个页面使用的模板 `/content/`. 显示错误，但未显示任何错误消息(NPR-33312)。
* 重定向到 [!DNL Experience Manager] 具有锚点的页面在创作实例上无法作为 `PageRedirectServlets` 在URL片段或锚点之后放置查询字符串(NPR-34288)。
* 在下创建品牌 `/content/campaign` 会生成一个不允许创建营销活动的结构。 [!UICONTROL 创建品牌] 选项会使新创建的品牌无法创建 [!UICONTROL 选件和活动] 因为没有 [!UICONTROL 创建] 选项(NPR-34113)。
* 您可以暂停 [!DNL Live Copy] 中的页面和继承会断开，如在编辑器模式中所示。 在页面属性中，表示继承的图标错误地指示继承存在且未中断(NPR-34017)。
* 具有许多引用的页面无法异步移动，有时移动操作会失败(CQ-4297969)。
* 网页 `/` 创作时，URL中的字符会变得无响应。 在创作时添加组件时，CPU使用率会增加，浏览器停止响应(CQ-4295749)。
* 在浏览模式下，NVDA不会讲述从“类型/大小”菜单选项中选择的值。 可视化焦点不在选定的元素上。 依赖屏幕阅读器的用户无法使用浏览模式(CQ-4294993)。
* 创建网页时，用户可以选择 [!UICONTROL 内容页面] 模板。 在 [!UICONTROL 社交媒体] 选项卡，用户选择 [!UICONTROL 首选体验片段变量]. 要在NVDA浏览模式下选择体验片段，用户无法使用键盘键(CQ-4292669)。
* 已将handlebars库更新为更安全的v4.7.3(NPR-34484)。
* 中的多个跨站点脚本实例 [!DNL Experience Manager Sites] 组件(NPR-33925)。
* 创建新文件夹时的文件夹名称字段容易遭受存储型跨站点脚本攻击(GRANITE-30094)。
* 上的搜索结果[!UICONTROL  欢迎] 页面和路径完成模板容易遭受跨站点脚本攻击(NPR-33719、NPR-33718)。
* 在非结构化节点上创建二进制属性会导致在二进制属性对话框上出现跨站点脚本攻击(NPR-33717)。
* 使用时跨站点脚本 [!UICONTROL 访问控制测试] 选项(NPR-33716)。
* 向客户端发送信息时，不会针对各种组件对用户输入进行适当的编码(NPR-33695)。
* Experience Manager收件箱的日历视图中存在跨站点脚本(NPR-33545)。
* 以 `childrenlist.html` 显示HTML页面，而不是404响应。 此类URL容易遭受跨站点脚本攻击(NPR-33441)。


### [!DNL Assets] {#assets-6560}

**Experience Manager Assets中的辅助功能增强功能**

* 使用键盘键，用户现在可以访问 [!UICONTROL 引用] 资产列表(NPR-34115)。

* 屏幕阅读器现在会朗读搜索页面上谓词的预期操作(NPR-34104)。

* 搜索页面和搜索结果页面现在提供了更多信息标题，以便更好地了解屏幕阅读器用户(NPR-34093)。

* 屏幕阅读器现在会朗读用于删除 [!UICONTROL 基本] 资产选项卡 [!UICONTROL 属性] 页面(NPR-33972)。

* 现在，屏幕阅读器会将列表视图中每行的元素宣布为同一行的元素(NPR-33932)。

* 用户在使用 `Tab` 现在，键会在版本预览中移动到关闭选项(NPR-33863)。

* 现在，在Omnisearch关闭后，用户焦点将移至搜索图标(NPR-33705)。

* 使用键盘键导航时，可操作的用户界面选项现在具有更突出的可视化焦点，对比度增强。 键盘用户可以识别焦点区域(NPR-33542)。

* 现在，使用键盘的拖动功能在 [!UICONTROL 元数据架构编辑器] 在屏幕阅读器的浏览模式下(CQ-4296326)。

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器会：

   * 加载对话框后，不会立即讲述表信息。

   * 可以导航到所有列出的自动建议。

   * 讲述为 [!UICONTROL 添加电子邮件地址/搜索] (CQ-4294232)。

* 使用 `Esc` 从卡片视图中删除快速操作图标的键不再从最后一个聚焦项目中删除键盘焦点(CQ-4293554)。

* 对于用户界面上的交互式选项，屏幕阅读器现在会朗读其用途，而不是图标的文字名称(CQ-4272943)。

* 现在，键盘焦点已成功移至 [!UICONTROL 弹出], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark]和 [!UICONTROL ZoomVertical_light] 在资产详细信息中使用键盘Tab键导航时的选项 [!UICONTROL 查看器] in [!DNL Dynamic Media] (CQ-4290605)。

* [!UICONTROL 保存并关闭] 资产上的选项 [!UICONTROL 属性] 现在可以使用键盘键访问页面(NPR-34107)。

* 由于登录页面上的用户名和密码组合不正确导致的错误消息现在会在每次发生错误时由屏幕阅读器通知(NPR-33722)。

* 在 [!DNL Experience Manager] 标题部分，屏幕阅读器现在会朗读，

   * 在中自动编辑建议 [!UICONTROL 要搜索的类型] 在Omnisearch中。

   * 展开或折叠的状态 [!UICONTROL 解决方案], [!UICONTROL 帮助], [!UICONTROL 收件箱]和 [!UICONTROL 用户] 选项。

   * 的 [!UICONTROL 搜索帮助] 用户在 [!UICONTROL 搜索帮助] 字段 [!UICONTROL 帮助] 选项。

   ![标题中的帮助菜单](assets/Help_aem_header.png)

   *图： [!UICONTROL 搜索帮助] in [!UICONTROL 帮助] 菜单。*

   * 在中输入的值不正确时显示错误消息 [!UICONTROL 模拟为] 字段 [!UICONTROL 用户] 选项和焦点可正确移到文本字段(NPR-33804)。

   ![标题中的用户菜单](assets/User_aem_header.png)

   *图： [!UICONTROL 模拟为] 字段 [!UICONTROL 用户] 菜单。*

* 用户现在可以在以下位置使用键盘更改焦点：

   * [!UICONTROL 搜索/添加电子邮件地址] 字段 [!UICONTROL 链接共享] 对话框。

   * [!UICONTROL 添加用户或群组] 字段 [!UICONTROL 已关闭的用户组] 在 [!UICONTROL 权限] 文件夹选项卡 [!UICONTROL 属性] (NPR-34452)。

**在Experience Manager Assets中修复的问题**

[!DNL Adobe Experience Manager] 6.5.6.0 [!DNL Assets] 提供了对以下问题的修复：

* 从资产的时间轴中选择注释时，不会高亮显示注释(CQ-4302422)。

* 预览使用 [!DNL Adobe InDesign] 模板不显示换行符和段落分隔符(NPR-34268)。

* 文本提取因此无法对上传的PDF文件进行全文搜索(NPR-34164)。 要修复该问题，请重新启动 [!DNL sAdobe Experience Manager] 安装Service Pack 6后进行部署。

* 多页面资产的时间轴在时间轴视图中浏览资产时，会显示应用于所有子资产的注释，而不是显示特定于特定子资产的注释(NPR-34100)。

* 无法使用 [!UICONTROL 管理发布] 选项。

* 在Omnisearch中取消选择或删除已应用的标记或过滤器会多次执行搜索查询，这会导致搜索时间增加(NPR-34078)。

* 在卡片视图中，当工作流（位于文件夹中的资产上）正在进行或待处理时，页面会重新加载，直到工作流完成或终止为止。 因此，作者无法处理必须向下滚动的文件夹中的这些资产(NPR-33986)。

* 如果用户将已发布的资产移动到新位置，则即使资产被重新发布， [!UICONTROL 重新发布] 选项。 这会导致发布实例上存在许多孤立的资产。 但是，默认行为是对已发布资产的移动操作会自动取消发布该操作；如果作者选择 [!UICONTROL 重新发布] 选项(NPR-33934)。

* 的 [!UICONTROL 移动资产] 收藏集中资产的页面不会加载所有HTML内容，例如 [!UICONTROL 调整/重新发布] 选项。 因此，用户无法完成移动操作(NPR-33860)。

* 移动资产并在移动资产的名称和标题中添加特殊字符会在资产的新位置创建一个额外的文件夹（具有相同的名称）(NPR-33826)。

* [!UICONTROL 下载] 的 [!UICONTROL 电子邮件] 选项 [!UICONTROL 下载] 对话框(NPR-33730)。

* 对资产执行批量操作（例如批量元数据编辑）时，观察到错误“Request-URI过长”(NPR-33723)。

* 观察到JavaScript错误，用户无法选择或删除在 [!UICONTROL 下拉列表] 字段 [!UICONTROL 通过JSON路径添加] 功能 [!UICONTROL 文件夹元数据架构表单编辑器]，则上传的JSON文件的值中包含空格或特殊字符(NPR-33712)。

* 在使用 [!UICONTROL 打开] 选项 [!DNL desktop app] 或 [!DNL Adobe Asset Link] 和同步回 [!DNL Adobe Experience Manager] (CQ-4296279)。

* 在列视图中，对一组资产执行移动操作时，也会移动在使用 [!UICONTROL 过滤器] 选项。 请注意， [!UICONTROL 过滤器] 选项会取消选择之前的选择(NPR-34018)。

* 在资产的搜索建议中，会在特殊字符之前添加反斜杠，这些字符的名称中带有特殊字符(NPR-33834)。

* 在中为下拉列表创建规则时 [!UICONTROL 文件夹元数据架构表单]，用户无法从 [!UICONTROL 字段选择] 列(CQ-4297530)。

* 资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`) [!DNL Experience Manager] 6.5 Service Pack 5或上的先前版本 [!DNL Experience Manager] 6.5(NPR-34532)。 要检索运行时副本，请使用HTTP API将工作流模型的设计时副本与运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

**在Dynamic Media中修复的问题**

* 如果用户在创建视频配置文件后在编辑中定义编码设置，则会从视频配置文件中删除智能裁剪设置(CQ-4299177)。

* 当用户在侧边栏选项之间切换时，页面加载时资产会闪烁(例如， [!UICONTROL 概述], [!UICONTROL 时间轴], [!UICONTROL 查看器])（在资产详细信息页面上）(NPR-34235)。

* 在重新处理作业时发现以下问题：

   * 重新处理作业返回的作业句柄中缺少作业ID。

   * 重新处理视频日志的作业（仅文件名，而非完整路径）。

   * 重新处理作业没有将资产类型设置为静态的选项。

   * `ExcludeFromAVS` 选项(CQ-4298401)。

* 将图像配置文件添加到具有多个（例如11）宽高比的文件夹后，智能裁剪功能会失败，并出现错误(NPR-34082)。

* 用户向下滚动时，会触发DAM更新资产工作流 [!UICONTROL 工作流存档] 页面 [!UICONTROL 工作流] 选项卡 [!UICONTROL 工具] in [!DNL Adobe Experience Manager] 已配置Dynamic Media Scene7(CQ-4299727)。

* 符号 [!UICONTROL 行为] 选项卡 [!UICONTROL 查看器预设编辑器] 未本地化(CQ-4299026)。

* 如果查看器处于响应模式，则主视图以不正确的布局显示图像，而该布局不适合查看器(CQ-4298293)。

* 对 [!UICONTROL Adobe Experience Manager] 请勿同步到Scene7 Publishing System(CQ-4299713)。

### [!DNL Commerce] {#commerce-6560}

* 移动资产时，产品中资产的链接不会重构(NPR-34098)。

### 平台 {#platform-6560}

* 无法在已升级的Experience Manager实例上使用诊断工具下载日志(NPR-34336)。
* 由于依赖于 `cq-wcm-api` 基础包(CQ-4300520)。
* 的默认值 **[!UICONTROL 连接超时]** 和 **[!UICONTROL 套接字超时]** 未指定默认代理（发布）配置的设置(NPR-33707)。
* 更新了 `/etc/map.publish` 请勿在网站页面上反映(NPR-34015)。
* [API参考文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) 不包括 `com.day.cq.tagging` 软件包(CQ-4295864)。

### 用户界面 {#ui-6560}

* 卸载浏览器界面不显示所有作业主题(NPR-34308)。
* 的 [配置浏览器](/help/sites-administering/configurations.md) 界面未显示所有配置(NPR-33644)。
* 按 `Esc` 键值 **[!UICONTROL 用户]** 对话框关闭，而不是用户列表(NPR-34084)。

### 集成 {#integrations-6560}

* 名称较长的活动未与同步 [!DNL Adobe Target] (NPR-34254)。

* 在创建新Adobe启动配置时选择属性会导致出现以下错误消息(NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 翻译项目 {#translation-6560}

* 如果用户的 `authorizableID` 包括特殊字符(NPR-33828)。

### Sling {#sling-6560}

* 运行状况检查和模式检测器具有重叠的功能。 因此，已从产品中删除了“健康”检查(NPR-33928)。

### WCM {#wcm-6560}

* 基础组件 — 在向页面添加基础图像组件并引用图像时， `Undo` 操作无效(NPR-34516)。

* 无法使用页面移动操作(CQ-4303028)。

### [!DNL Communities] {#communities-6560}

* 在社交媒体上共享帖子时，会显示一个过时的选项Google+(NPR-33877)。

* 社区成员无法修改组模板或其他组函数设置(NPR-33530)。

* 论坛帖子中未正确生成图像上的超链接标记(NPR-33464)。

* 社区分配功能会识别无障碍故障(NPR-33442)。

* 通过管理控制台添加的社区组的现有用户将从社区组控制台中的任何修改的用户列表中删除(NPR-34315)。

* 的 `TagFilterServlet` 泄漏可能敏感的数据(NPR-33868)。

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含 [!DNL Forms]. 它们使用单独的 [!DNL Forms] 附加组件包。 此外，还发布了累积安装程序，其中包含针对 [!DNL Experience Manager Forms] 在JEE上。 有关更多信息，请参阅 [安装AEM Forms附加组件](#install-aem-forms-add-on-package) 和 [在JEE上安装AEM Forms](#install-aem-forms-jee-installer).

安装 [!DNL Experience Manager Forms] 6.5.6.0附加组件包：

* 停止 [!DNL Experience Manager Forms] 实例。

* 删除 `bcpkix-1.51`, `bcmail-1.51`和 `bcprov-1.51` 从 `crx-repository\launchpad\ext` 目录访问Advertising Cloud的帮助。

* 删除` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` 属性 `sling.properties` 文件。

* 重新启动 [!DNL Experience Manager Forms] 实例。

**自适应表单**

* 当缺少自适应表单片段时，自适应表单无法呈现(NPR-34302)。

* 自适应表单字段的帮助内容描述显示段落HTML标记(NPR-34116)。

* 当您选择 **[!UICONTROL 在服务器上重新验证]** 属性，则自适应表单提交失败(NPR-33876)。

* 的 **[!UICONTROL 提交到REST端点]** 提交操作不适用于自适应表单(CQ-4299044)。

* 辅助功能：当您尝试在未上传必填字段附件的情况下提交自适应表单时，焦点不会自动转移到附件字段(CQ-4298065)。

* 向自适应表单的表格添加行时， **[!UICONTROL 添加到顶部]** 和 **[!UICONTROL 添加到底部]** 选项不显示相应的结果(CQ-4297511)。

* 的 [!UICONTROL 值提交] 脚本触发不正确，从而导致自适应表单中的数据丢失(CQ-4296874)。

* 本地化的自适应表单的日期选取器无法正常工作(NPR-34333)。

* 当文件名中有下划线或空格时，无法将文件附加到自适应表单(CQ-4301001)。

* 当嵌套的可重复面板的发生次数多于其父面板时，此类嵌套可重复面板的所有发生次数都无法预填充(NPR-33666)。

* 自适应表单具有一些打开的资源解析器。 这会导致提交失败。 此问题间歇性发生(CQ-4299407)。

* 首次打开字段配置时，不显示属性图标(CQ-4296284)。

* 用户可以编辑提交元数据，例如 `afPath`, `afSubmissionTime` 和 `signers`，在提交自适应表单时。 要解决此问题，将从客户端的表单提交数据中删除元数据值。 用户可以使用 `FormSubmitInfo` 对象从服务器中检索这些值(NPR-33654)。

* 用户输入未针对 [!DNL Forms] 组件(NPR-33611)。

**工作流**

* 当工作流审批者上传附件时，附件将重命名为 `undefined` (NPR-33699)。

* [!DNL Experience Manager] 工作流清除操作失败，并显示以下错误消息(NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] 应用程序 [!DNL Windows] 提交表单后停止响应(NPR-34409)。

* 安装AEM Service Pack时， **待办事项** 项目列表不显示为链接。 的文本 **待办事项** 项目包括HTML标记(NPR-34317)。

**交互式通信**

* 如果包含包含嵌套可重复组件的文本文档片段，则无法保存交互式通信(NPR-34095)。

**通信管理**

* 修改包含数据字典值的文本文档片段时，代理UI停止响应(NPR-33930)。

* 从 [!DNL Microsoft Word] 将文档记录到信件中的文本文档片段会导致格式问题(NPR-33536)。

**文档服务**

* 使用“输出”和“Forms”服务从XDP文件生成PDF文件时，会导致缺少文本和文本重叠(NPR-34237、CQ-4299331)。

* 将HTML文件转换为PDF时， `MaxReuseCount` 属性不可配置(NPR-33470)。

* 下载包含Reader扩展交互功能的PDF文件时，无法使用 [!DNL Adobe Reader] (NPR-33729)。

**文档安全**

* 安装后，无法在PDF文件中使用基于HSM的证书执行Sign操作 [!DNL Experience Manager] Service Pack(NPR-34310)。

**Designer**

* 无法在Designer版本6.5.x中打开XForms(CQ-4295322)。

* 打开Designer时，欢迎屏幕显示错误的年份(CQ-4295289)。

* 安装时 [!DNL Acrobat DC] 在服务器上， **[!UICONTROL 分发表单]** 选项不活动(CQ-4296304)。

有关安全更新的信息，请参阅 [Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0是一项重要更新，其中包括自6.5版的正式发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进 **2019年4月**. 它可以安装在Adobe Experience Manager 6.5的顶部。

中引入的一些主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.5.0包括：

* 不允许匿名访问CRXDE Lite。 而是会将用户定向到登录屏幕。 请参阅 [使用CRXDE Lite进行开发](/help/sites-developing/developing-with-crxde-lite.md).

* 自定义在中显示的列名称 [!DNL Adobe Experience Manager] 收件箱。

* 改进了Experience ManagerWeb内容管理(WCM)中各个区域（如页面编辑器、核心组件、RTE和管理员用户界面）的辅助功能。

* 保存 [!DNL Interactive Communication] 草稿。

* 支持 [!DNL Oracle WebLogic 12] 为Experience Manager Forms准备的。

* 改进了中的异常处理 [!DNL Adobe Experience Manager Assets] 用户界面流程。

* 要获取Dynamic Media Scene7的发布URL，请使用一种新方法 `getRemoteAssetPublishURL` 添加到 `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` 界面。

* [辅助功能增强](#assets-6550) in [!DNL Adobe Experience Manager Assets] 符合Web内容无障碍准则(WCAG)。

* 从Adobe Experience Manager中删除了包共享集成。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.3。

有关Experience Manager6.5 Service Pack 5中引入的完整功能列表、主要亮点和主要功能，请参阅 [Adobe Experience Manager 6.5 Service Pack 5的新增功能](new-features-latest-service-pack.md) .

以下是 [!DNL Experience Manager] 6.5.5.0版本。

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites提供了一个选项，用于从别名发布或取消发布页面。 选项无效(NPR-33415)。
* 从包含多个模板的模板中删除布局容器后，该模板无法正确呈现(NPR-33347)。
* 当Experience Manager Sites页面包含在具有多个Live Copy的大型内容集中时，页面版本历史记录预览无法加载(NPR-33311)。
* 使用“移动”命令重命名Experience Manager Sites页面时，页面标题不会更新(NPR-33264)。
* 在列视图中移动页面时，列会消失(NPR-33216)。
* 当语言副本中的本地组件名称与Blueprint中组件的名称相同，并且该组件从Blueprint、Term中转出时 `_msm_moved` 未添加到本地组件的名称中(NPR-33208)。
* 页面重定向Servlet将.html附加到Experience Manager Sites URL，其中ResourceType不是 `cq:Page` (NPR-33176)。
* 粘贴子树时，没有选项可决定是否粘贴相应的子页面(NPR-33149)。
* 组件在实时使用中的结果数量限制为第49个(NPR-33058)。
* 如果内容片段基于架构并且包含必填文本区域或路径字段，则内容片段无法保存(NPR-33007)。
* 使用默认的体验片段组件创建自定义组件并在Experience Manager Sites页面中使用该组件时，Experience Manager不显示自定义组件的引用（用法）(NPR-32852)。
* 重命名包含大量引用的文件夹时，对该文件夹的许多引用都不会更新(NPR-32765)。
* 启用源代码编辑选项后，该选项将可用于内嵌的全屏选项，但富文本编辑器的编辑对话框和全屏选项仍缺少该选项(NPR-32763)。
* 如果您有多个字段，并且它在Blueprint的页面属性中包含必填字段（如下拉列表或路径字段），则在转出包含此类多字段的页面时，不会保存Live Copy的页面属性(NPR-32751)。
* 屏幕阅读器无法使用标题结构来导航页面。 此外，“组件”选项卡的标签错误(NPR-32648)。
* 开始分页时，体验片段选取器不会加载所有项目(NPR-32605)。
* 读取、修改、创建和删除Live Copy的创作权限将被撤销。 每个作者都必须明确提供读取和修改权限，才能在Blueprint中移动页面(NPR-32550)。
* 内容作者无法为具有Adobe Analytics集成的页面创建Launch(NPR-32548)。
* 当用户恢复继承并进行同步时，父页面的Live Copy与Blueprint不同步，并显示错误状态(NPR-32500)。
* Experience Manager Sites编辑器页面加载花费的时间超过15秒(NPR-32413)。
* 某些字段不显示“取消继承”选项(NPR-32362)。
* 选择体验片段组件的路径并选择打开选择对话框复选框时，您不会在路径浏览器中导航到选定的路径(NPR-32308)。
* 从Experience Manager6.2升级到Experience Manager6.5时，静态模板的Parsys组件无法正确显示。 Parsys组件的高度设置为0，且其中的组件不可见(NPR-33663)。
* 当用户在同一页面上复制并粘贴布局容器时，布局容器中的组件不会显示(NPR-33648)。
* 显示调度程序运行状况检查 `Invalid cookie header` 日志文件中出现警告消息(NPR-33629)。
* PreferencesServlet中已反映XSS(NPR-33438)。
* 匿名用户可以访问CRXDE Lite功能(GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>的Windows用户 [!DNL Experience Manager desktop app] 建议升级到 [桌面应用程序版本2.0.3.2](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html#what-is-new) 访问 [!DNL Adobe Experience Manager 6.5.5.0] 实例。 因为他们在访问 [!DNL Adobe Experience Manager] 使用桌面应用程序版本2.0.2的6.5.5.0实例。

**Experience Manager Assets中的辅助功能增强功能**

* 现在可以将键盘焦点放在 [!UICONTROL 评论] 列出和可单击选项 [!UICONTROL 创建] 版本注释 [!UICONTROL 创建新版本] in [!UICONTROL 时间轴] 资产面板(NPR-33424)。

* 现在可以访问 [!UICONTROL 查看设置] 中的 [!UICONTROL 查看设置] 对话框(NPR-33420)。

* 组合框的列表框弹出窗口（位于不同页面上的各种字段中）现在将条目显示为可由屏幕阅读器朗读的选项列表(NPR-33516)。

* 排序标题的排序功能(在列表视图中， [!UICONTROL 时间轴] 查看，和 [!UICONTROL 管理发布] 页面)现在由屏幕阅读器朗读，并且可使用键盘访问列标题的排序控件(NPR-32979)。

* 现在，可以重点查看可单击的元素，如评论卡、版本更新、组合框和V形菜单图标，并使用键盘进行交互(NPR-33514)。

* 分析图标的功能（或操作目的）(用于 [!UICONTROL 分析视图] 现在，屏幕阅读器可正确地发布消息(NPR-33513)。

* 只读表单字段(例如 [!UICONTROL “基本”选项卡] 资产 [!UICONTROL 属性])现在可使用键盘聚焦(NPR-33493、CQ-4273031)。

* 各种输入字段中的标签现在是永久性标签（因此可访问），而不仅仅是占位符标签，在输入文本时这些标签会消失(NPR-33475)。

* 不同的标题级别（如页面标题和区域标题）现在被视为屏幕阅读器用户具有不同级别的标题(NPR-33471)。

* 交互式用户界面元素，如链接和选项（资产页面的标题和缩放选项、文件夹导航），现在可使用键盘访问(NPR-33468、CQ-4271412)。

* 的 [!UICONTROL 选项], [!UICONTROL 范围]和 [!UICONTROL 工作流] 进展指标 [!UICONTROL 管理发布] 页面现在由屏幕阅读器正确读出为进度指示器，而不是选项卡(NPR-33416)。

* 星级图标的颜色(例如 [!UICONTROL 评级] 部分 [!UICONTROL 高级] 选项卡 [!UICONTROL 属性] 对于视力有限且无颜色感知的用户而言，为了显示相应的对比度，卡片视图中会发生更改(NPR-33414)。

* 旁边的V形向上箭头 [!UICONTROL 注释] 现在可以使用键盘键访问“资产详细信息”页面上的字段(NPR-33397)。

* 的扩展和折叠状态 [!UICONTROL 标记] 对话框 [!UICONTROL 属性] 屏幕阅读器现在可以正确地显示和左边栏导航（在资产用户界面上）(NPR-33396)。

* 上所有已浏览页面的标题 [!DNL Adobe Experience Manager] 资产现在是唯一的(NPR-33343)。

* 现在，在导航树结构时，屏幕阅读器会正确地指示树视图控件的各种元素(NPR-33304)。

* 中资产的不同版本 [!UICONTROL 时间轴] 现在可以使用键盘键访问资产查看详细信息页面(NPR-33283)。

* 现在，使用搜索功能时，屏幕阅读器会朗读在Omnisearch组合框中显示的搜索建议的名称(NPR-33280)。

* 可单击的元素和 [!UICONTROL 转到链接] in [!UICONTROL 引用边栏] 现在由屏幕阅读器宣布为可单击的元素(NPR-33278)。

* 表格结构信息（如行1、单元格1、表格） [!UICONTROL 共享链接] 对话框打开时，屏幕阅读器不再会显示对话框(NPR-33268)。

* 屏幕阅读器现在可以正确地宣布各种组合框元素的用途（例如，“路径”字段和用于在资产属性的“基本”选项卡中打开“选择”对话框的选项）(NPR-33235)。

* 现在，当键盘焦点位于列表视图表格中的行上时，系统会向屏幕阅读器用户传达可供选择的信息。 当指针悬停在行上时，屏幕阅读器会朗读该信息(NPR-33234)。

* 选项(具有 [!UICONTROL x])以删除 [!UICONTROL 标记] 字段 [!UICONTROL 基本] 选项卡 [!UICONTROL 属性] 现在可供屏幕阅读器访问(NPR-33206)。

* 日历日期选取器现在可供屏幕阅读器用户和视力正常的键盘用户使用，并且可使用键盘(NPR-33200)。

* 现在，在列表视图和卡片视图之间切换的切换可正确将其功能（调整视图）显示给屏幕阅读器(NPR-33069)。

* 现在可以访问左边栏中的菜单。 屏幕阅读器会相应地宣布扩展菜单的功能和用途(NPR-33068)。

* 现在，失明的屏幕阅读器用户可以访问列表框和许多其他用户界面元素，屏幕阅读器会发布有关这些元素的以下信息(NPR-33040):

   * 在提交表单之前是否需要对元素进行用户输入。
   * 元素是否不可编辑。
   * 是否选择小组件。

* 现在，可以使用键盘访问用于打开过滤器侧栏的选项(NPR-32842、CQ-4273018)。

* 列表视图列标题中的复选框控件现在可以访问，屏幕阅读器会宣布使用该控件的目的(NPR-32722、NPR-33005)。

* 日历日期选取器中小时(HH)和分钟(mm)字段的标签现在是永久性标签，而不是占位符标签，并且当用户在这些字段中输入文本时不会消失(NPR-32720)。

* 通知的链接文本（在单击铃铛图标后显示）现在会向屏幕阅读器用户发布，用户可以使用选项卡访问每个链接(NPR-32645)。

* [!UICONTROL 选择], [!UICONTROL 下载], [!UICONTROL 属性]和 [!UICONTROL 更多操作] 中的资产卡片选项 [!UICONTROL 分析视图] 现在可使用键盘访问(NPR-32609)。

* 使用键盘访问视觉上隐藏的内容（如搜索结果中标题菜单栏的内容）后，屏幕阅读器不再会显示这些内容(NPR-32606)。

* 屏幕阅读器现在会宣布日历日期选取器中用于移至下个月和上个月控件的标签用途(NPR-32604)。

* 星级图标现在可以聚焦，并且可使用键盘键(NPR-32513)。

* 控制视频音量的功能现在可通过选项卡（聚焦于音量滑块）和键盘上的箭头键（调整音量）访问(NPR-32065)。

* 下限([!UICONTROL 从])和上限([!UICONTROL 至])“文件大小”筛选器的输入字段现已发送给失明的屏幕阅读器用户(NPR-32064)。

* 的 [!UICONTROL 语言] 菜单 [!UICONTROL 创建和翻译] 现在，屏幕阅读器可在浏览模式下访问表单(CQ-4293906)。

* 的 [!UICONTROL 引用] 面板现在可通过以下增强功能访问(NPR-33261、CQ-4293798):

   * 在浏览模式下，屏幕阅读器焦点不再移至下面隐藏的多行编辑字段 [!UICONTROL 网站引用], [!UICONTROL 资产引用], [!UICONTROL 副本]和 [!UICONTROL 表单引用] 中。

   * 屏幕阅读器现在会宣布 [!UICONTROL 网站引用] 和 [!UICONTROL 语言副本] 元素。

   * 浏览模式下屏幕阅读器的焦点按有意义的顺序转移到各种元素上。

* [!UICONTROL 元数据架构编辑器] 页面及其元素现在可使用键盘访问，并且屏幕阅读器友好(CQ-4290962、CQ-4272953)。

* 的目的 `X` 用于删除所选标记的符号现在由屏幕阅读器和选定标记的数量一起宣布(CQ-4273017)。

* 为避免使用屏幕阅读器的失明用户产生混淆，屏幕阅读器现在会忽略装饰图标和图像(CQ-4272944)。

**在Experience Manager Assets中修复的问题**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets提供了对以下问题的修复：

* [!UICONTROL 开始] 选项开启 [!UICONTROL 创建工作流] 收藏集中资产对话框被禁用，从而阻止触发工作流(NPR-32471)。

* 在元数据架构中使用级联弹出窗口时，在选择和保存包含撇号的下拉选项（从子项下拉菜单中）时，选定的撇号选项会在重新打开资产后消失 [!UICONTROL 属性] (NPR-32649)。

* [!UICONTROL 资产分析同步作业] 如果遇到无效条目（在Analytics端），而不是移动到下一个条目，则停止并失败(NPR-32674)。

* 陀螺仪不起作用，因为全景查看器中的移动浏览器默认禁用运动传感器(CQ-4272937)。

* [!UICONTROL 连接的资产配置] 在6.5.1上安装6.5.3时，向导无法处理404错误(NPR-32730)。

* 在XMP写回过程中，所有自定义命名空间元数据属性会将自定义命名空间前缀更改为ns2，而不是配置的命名空间前缀(NPR-32748)。

* 不会触发延迟加载，选择从通知收件箱中查看任务时只会显示100个资产(NPR-32750)。

* `NullPointerException` 由于新创建的用户配置文件(SAML/SSO)中缺少节点首选项，观察到。 此错误会阻止新登录的用户使用 [!DNL Adobe Experience Manager Stock] 集成(NPR-32777)。

* 在打开包含超过10,000个资产的智能收藏集时，日志中出现遍历警告(NPR-32980)。

* 在将资产从一个文件夹移动到另一个文件夹(位于 [!DNL Adobe Experience Manager] 正在使用Dynamic Media Scene7运行模式(NPR-32995)。

* 从搜索结果导航到搜索资产的属性，然后返回搜索结果以将其删除后，无法删除已搜索的资产(NPR-32998)。

* [!UICONTROL 下一个] 选项在选择目标文件夹时保持禁用状态 [!UICONTROL 移动资产] 界面(NPR-33356)。

* [!UICONTROL 下一个] 选择父节点（其中显示单个子文件夹），然后选择子文件夹时，未启用选项(NPR-33275)。

* 对于具有删除权限的用户，即使已授予读取、创建或修改等其他权限，Adobe资产链接(AAL)上的签入和签出权限也会被禁用(NPR-33272)。

* “资产下载”对话框中不提供智能裁剪演绎版(NPR-33167)。

* 在具有智能裁剪配置文件的文件夹下打开PDF的演绎版边栏时，日志中发现异常(CQ-4294201)。

* 如果为，则不会发布图像预设 [!UICONTROL Dynamic Media同步模式] 在使用Dynamic Media Scene7运行模式Experience Manager时，默认情况下处于禁用状态(CQ-4294200)。

* 批量上传时的资产处理卡住，工作流实例显示DAM更新资产的卡住实例(CQ-4293916)。

* 在Experience Manager上创建Dynamic Media配置是可行的，但在用户界面上，选择“保存”(CQ-4292442)时，不会发生任何情况。

* 在Safari/Mac上的渐进式播放中，无法预览F4V视频资产(CQ-4289844)。

* 对于位于父文件夹中且带圆点的资产，在智能裁剪时会创建额外的文件夹 `.` 字符(CQ-4289337)。

* 缩略图已损坏，在复制视频时不会显示视频处理横幅(CQ-4284125)。

* 对于某些具有空相机视图的型号，维度查看器在Firefox中无法正确显示空缩略图(CQ-4283447)。

* 6.5.5.0中修复的性能问题包括(CQ-4279206):

   * 将大二进制文件上传到Dynamic Media图像处理服务器需要过长时间。

   * 由于Dynamic Media Scene7架构，Experience Manager的缩略图生成时间增加。

* Dynamic Media Scene7迁移问题对于具有大量资产的客户失败(CQ-4279206)。

* 如果 `setVideo` ，并且视频会在使用 `video= modifier` (CQ-4263201)。

* 安装Experience ManagerSDL包时显示错误消息(NPR-33175)。

* Experience Manager中的SSRF漏洞(NPR-33435)。

### 平台 {#platform-6550}

* 的 [!DNL Sling] 如果 `sling:match` 在下创建映射条目 `/etc/maps` (NPR-33362)。
* Experience Manager崩溃，原因是 [!DNL Apache Lucene] (NPR-32988)。
* [!DNL Jackson] Experience Manageruberjar文件中缺少核心包(NPR-32848)。
* CRXDE Lite不会为没有 `jcr:primaryType` 节点的属性(NPR-32611)。
* [!DNL Granite] 在Experience Manager部署期间，维护任务计划程序重新初始化的频率过高(CQ-4294627)。
* 当SQL查询长时间执行（例如7小时）时，Experience Manager停止响应(NPR-33044)。

### 用户界面 {#ui-6550}

* 多字段中不会保留单选按钮选择(NPR-33309)。
* 列表视图不适用延迟加载限制(NPR-33124)。
* 如果没有匹配项，Omnisearch结果页面不会显示消息(NPR-32974)。
* Omnisearch筛选器会返回 `/content` 节点忽略选定的位置(NPR-32849)。

### 集成 {#integrations-6550}

* 发布包含Adobe Target组件的页面时，会清除内部缓存(NPR-33162)。
* 与Adobe Target的集成在 [!DNL Windows Internet Explorer] 11(NPR-33111)。
* 配置Adobe Target时， [!UICONTROL 公司] 和 [!UICONTROL 报表包] 选择报表源时不显示字段(NPR-32502)。
* 导出时 [!DNL Experience Fragments] 使用 [!DNL Adobe I/O]，则源产品等元数据不会导出到Adobe Target中(NPR-32159)。
* 本地Experience Manager管理员组中的已授权IMS用户无法创建或修改IMS配置(NPR-33045)。
* Adobe启动配置页面未显示所有记录(NPR-33011)。
* 由于JavaScript错误，内容作者组中的用户无法编辑Adobe Target组件的属性(NPR-32996)。
* JSON跨站点脚本(NPR-32744)。

### 翻译项目 {#translation-6550}

* 翻译后的标记不会从第三方翻译服务导入到Experience Manager中(NPR-33154)。
* 翻译配置页面显示的翻译提供程序与用于翻译的翻译提供程序不正确(NPR-32971)。
* 将体验片段文件夹添加到现有翻译项目会创建一个新项目(NPR-32843)。
* A `NullPointerException` 运行翻译作业时在日志中显示错误(NPR-32628)。

### WCM {#wcm-6550}

* 页面编辑器 —  [!DNL Sites] 页面编辑器不允许仅键盘用户跳到主内容，而不是通过标题中可用的所有选项来切换选项卡焦点(CQ-4293883)。
* 页面编辑器 — 使用良好组件并包含已保存数据的面板由于在 [!DNL Chrome] 和 [!DNL Firefox] 版本(CQ-4292995)。
* MSM — 从页面中删除组件时，不会从页面的已发布版本中删除组件(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* 从中删除已发布的元数据架构 [!DNL Brand Portal] 导致错误(CQ-4292063)。
* 如果管理员配置 [!DNL Experience Manager Assets] 6.5.4与Brand Portal(通过Adobe开发人员控制台) [!DNL Brand Portal] 用户无法从 [!DNL Brand Portal] to [!DNL Experience Manager] (NPR-33046)。
* 导致冲突的父文件夹复制重复(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* 无法使用快速编辑菜单选项在审核控制台中删除信息卡(NPR-33117)。
* 访问 [!UICONTROL 活动流] 页面(NPR-33146)。
* 不会从所有发布实例中删除在创作实例上删除的组(NPR-33199)。
* 创建新组后，作者不会被重定向到 [!UICONTROL 社区组] 部分 [!DNL Internet Explorer] 11(NPR-33205)。
* 在“Experience Manager收件箱”中访问消息时，该消息的状态不会更改为“已读”(NPR-32764)。
* 编辑 [!DNL Communities] 组和更改缩略图图像不会更新组缩略图图像(NPR-32599)。
* 用户无法向社区中的其他用户发送电子邮件(NPR-32598)。
* 在用户刷新页面之前，不会显示已提交的博客(NPR-32391)。
* 在创建用户生成内容(UGC)的通知和订阅版本时，会存储不正确的源页面ID(CQ-4279355、CQ-4289703)。
* 跨站点脚本问题(NPR-33203)。

### 工作流 {#workflow-6550}

* 的 [!UICONTROL 时间轴] 左边栏中的选项加载所花费的时间比预期要长(NPR-32851)。
* 重新启动Experience Manager实例后，用于集合审阅任务的电子邮件中包含错误的有效负荷链接(NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience ManagerService Pack不包含 [!DNL Forms]. 它们是通过单独的 Forms 附加组件包交付的。此外，发布了一个累计安装程序，其中包含 JEE 上对 AEM Forms 的修复。有关更多信息，请参阅 [安装Experience Manager Forms附加组件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 和 [在JEE上安装Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* 通信管理：在提交信件后，目标区域的资产顺序会随之移动(NPR-33359、NPR-33153)。
* 自适应Forms:用户编辑自适应表单时， [!UICONTROL 启动工作流] 选项 [!UICONTROL 页面信息] 菜单无效(NPR-33004)。
* 自适应Forms:用户无法保存包含多个附件的自适应表单(NPR-32997)。
* 自适应Forms:在自适应表单中更改面板布局会导致错误(CQ-4293880)。
* 自适应Forms:自适应表单词典中的字符串新行会添加 `&#xa;` 字符到词典(NPR-33266)。
* 自适应Forms辅助功能：当用户预览自适应表单作为HTML表单时， [!UICONTROL 潦草签名] 字段无法保留制表符焦点(NPR-33159)。
* 自适应Forms辅助功能：提交自适应表单时显示的错误消息不会链接到 `aria-describedBy` 属性(NPR-33071)。
* 自适应Forms辅助功能：在ARIA辅助功能架构中，自适应表单中标记为必填字段的必填属性未设置为“True”(NPR-33070)。
* PDFG服务：当用户将文本文件转换为PDF时，日语字符无法正确呈现(NPR-33238)。
* PDFG服务： `CreatePDF` 无法将PDF文件转换为PDFOCR格式(NPR-32994)。
* PDFG服务：PDF转换对于第200个实例失败 [!DNL OpenOffice] 文档(NPR-32766)。
* 后端集成：表单数据模型请求因不正确的非活动状态而失败，因为刷新令牌过期(NPR-33169)。
* 设计器：屏幕阅读器根据默认的地理顺序而不是XDP文件中定义的自定义Tab键顺序来执行Tab键顺序(NPR-32160)。
* 设计器：如果启用了标记选项，则子表单边框会在生成的PDF输出中消失(NPR-32778)。
* 将XSS与GuideSOMProviderServlet一起存储(NPR-32700)。

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0是一项重要更新，其中包括自6.5版的正式发布以来发布的新功能、关键客户请求的增强功能和性能、稳定性、安全性改进 **2019年4月**. 它可以安装在Adobe Experience Manager 6.5的顶部。

Adobe Experience Manager 6.5.4.0中引入的一些主要功能和增强功能包括：

* Adobe Experience Manager Assets现在通过Brand Portal配置 [!DNL Adobe I/O] 控制台。

* 新 [生成可打印输出](../forms/using/aem-forms-workflow-step-reference.md) 步骤现在可用于Adobe Experience Manager Forms工作流。

* [多列支持](../forms/using/resize-using-layout-mode.md) 用于自适应表单和交互式通信的布局模式。

* 支持 [富文本](../forms/using/designing-form-template.md) HTML。

* [辅助功能增强](new-features-latest-service-pack.md#accessibility-enhancements) 在Experience Manager Assets。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.8。

* 您现在可以将选择性内容子树同步到 *Dynamic Media -Scene7模式* 而不是所有可用的 `content/dam`.

* 与SOAP Web服务的表单数据模型集成现在支持元素上的选择组或属性。

* SOAP输入或输出以及复杂的数据结构现在支持动态组替换。

有关最新Service Pack中引入的功能和主要功能的完整列表，请参阅 [Adobe Experience Manager 6.5 Service Pack的新增功能](new-features-latest-service-pack.md).

### 站点 {#sites-fixes}

* 当Adobe Experience Manager Sites页面的URL包含冒号(`:`)或百分比符号(`%`)，则浏览器停止响应，CPU使用率出现峰值(NPR-32369、NPR-31918)。

* 打开Experience Manager Sites页面进行编辑并复制组件后，某些占位符仍无法执行粘贴操作(NPR-32317)。

* 打开“管理发布”向导后，链接到核心组件的体验片段不会显示在已发布引用列表中(NPR-32233)。

* 触屏UI中的Live Copy概述渲染时间比经典UI要长得多(NPR-32149)。

* 当服务器时间和计算机时间位于不同时区时，计划发布时间在触屏UI中显示服务器时间，而在经典UI中，则显示计算机时间(NPR-32077)。

* Experience Manager Sites无法打开URL中带有后缀的页面(NPR-32072)。

* 用户编辑内容片段时，将恢复内容片段的已删除变量(NPR-32062)。

* 允许用户保存内容片段，而无需在必填字段中提供任何信息(NPR-31988)。

* kernel.js和ui.js未预先编译或缓存。 这会导致在渲染页面时额外花费时间(NPR-31891)。

* 启用PageEventAuditListener后，提交队列的长度会增加。 它会影响许多操作的性能，例如批量发布、导航、批量资产移动(NPR-31890)。

* 拖动体验片段时，会观察到较长的响应时间(NPR-31878)。

* 在响应式网格的占位符中选择将组件拖动到此处选项时，将发送GET请求，并且该请求会导致HTTP 403错误(NPR-31845)。

* 在同一文件夹中移动内容时，页面移动选项处于禁用状态(NPR-31840)。

* 在可编辑的模板结构模式下，布局容器中允许的组件列表显示错误结果。 布局容器中仅显示具有设计对话框的组件(NPR-31816)。

* 当页面具有用户的只读权限时，打开属性选项在sites.html中可见，但在editor.html中不可见(NPR-31770)。

* 用户单击创建按钮时，页面选项不可用(NPR-31756)。

* 无法同步包含OOTB（现成）设计导入器组件的Adobe促销活动中的促销活动(NPR-31728)。

* 尝试将项目符号列表更改为编号列表时，只更改列表的前两个项目(NPR-31636)。

* 在未创作页面并选择子节点时，选择对话框仍会显示初始节点。 在创作页面并单击“浏览”后，页面会重定向到根节点，而不是创作的节点(NPR-31618)。

* “查看配置”对话框无法正常用于收件箱自定义工作流功能(NPR-32503和NPR-32492)。

* 使用收件箱查看工作流信息时，会显示错误消息(CQ-4282168)。

### 资产 {#assets-6540-enhancements}

* 资产收集页面上用于触发工作流的按钮处于禁用状态(NPR-32471)。

* 在使用Dynamic Media Scene7配置将资产从一个文件夹移动到另一个Experience Manager的SPS(Scene7 Publishing System)中创建一个无名称的文件夹(NPR-32440)。

* 将所有资产（使用全选，然后移动）移动到包含已发布资产的文件夹的操作失败，并出现错误(NPR-32366)。

* 为具有${extension}的资产生成演绎版失败(NPR-32294)。

* 版本历史记录URL显示在资产属性页面的引用者字段下(NPR-31889)。

* 无法使用WinZip打开从DAM下载的ZIP文件(NPR-32293)。

* 在打开“文件夹设置”以更改文件夹标题或缩略图图像并保存后，文件夹的原始权限会进行更新(NPR-32292)。

* 计划激活的日历图标未显示在状态列（在DAM资产列表的经典UI中）中，对于计划在稍后的日期和时间激活的资产(NPR-32291)。

* 使用代码片段模板创建代码片段时，在创建代码片段过程中搜索收藏集时出错(NPR-32290)。

* 从搜索筛选器中选择多个标记时，会触发多个搜索查询(NPR-32143)。

* Experience Manager Assets UI在上传文件名中包含50个以上字符的资产时显示截断的文件名(NPR-32054)。

* 在选中Adobe Stock中复选框树的级别2复选框时，如果清除第一个和第二个复选框，则“筛选器”面板中的所有复选框都会清除(NPR-31919)。

* 使用Omnisearch Facet的文件和文件夹搜索会出现异常(NPR-31872)。

* 在相应的元数据架构表单中设置依赖关系规则时，即使选择必填字段后，也不会删除元数据编辑器中必填字段选择的字段突出显示(NPR-31834)。

* 资产属性页面中未显示叶级别标记的完整名称（来自标记层次结构）(NPR-31820)。

* 使用Safari浏览器上资产属性页面中的返回命令时出错(NPR-31753)。

* 触屏UI搜索（通过Omnisearch完成）结果页自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在Dynamic Media Scene7运行模式下运行的Experience Manager中，PDF资产的“资产详细信息”页面不显示操作按钮，但“收集”和“添加演绎版”按钮除外(CQ-4286705)。

* 通过Scene7的批量上传流程处理资产需要过长(CQ-4286445)。

* 当用户在Dynamic Media客户端的集编辑器中未进行任何更改时，保存按钮不会导入远程集(CQ-4285690)。

* 当将受支持的3D模型摄取到Experience Manager中时，3D资产缩略图不会提供信息(CQ-4283701)。

* 智能裁剪视频查看器预设的未处理状态在横幅文本上与预设名称旁边显示两次(CQ-4283517)。

* 在资产的详细信息页面上，观察到在3D查看器中预览的已上传3D模型的容器高度不正确(CQ-4283309)。

* 在Experience ManagerDynamic Media混合模式(CQ-4255590)上，轮播编辑器未在IE 11中打开。 **对于AdobeDynamic Media — 混合模式客户：** Adobe将于2022年5月之后，在Dynamic Media — 混合模式中终止对Internet Explorer 11的支持。

* 在Chrome和Safari浏览器中，“下载”对话框的“电子邮件”下拉菜单中，键盘焦点卡住(NPR-32067)。

* 尝试在Experience Manager上添加DM云配置时，默认情况下未启用“同步所有内容”复选框(CQ-4288533)。

### 基础UI {#foundation-ui-6540}

* 使用“筛选器”面板搜索资产时，鼠标控件会切换到上一个筛选器字段，而不是停留在现有筛选器字段中(NPR-32538)。

* 平台标记：通过在标记字段中键入内容来搜索标记，可显示根边界以外的标记，且不遵循 `rootPath` 标记字段的属性(NPR-31895)。

* 平台UI:如果在文本字段中添加了无效路径，则路径浏览器会损坏(NPR-31884)。

* 选择页面时，通知会隐藏在置顶菜单后面(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)URL路径部分中的下划线替换冒号(NPR-32231)。

### 项目 {#projects-6540}

* 即使用户有权在子文件夹中创建项目，用户也看不到创建按钮(NPR-31832)。

### 项目翻译 {#projects-translation-6540}

* 在中激活“裁切空格”选项时，翻译项目创建会中断UI `Apache Sling JSP Script Handler` (NPR-32154)。

* 将任何要翻译的标记添加到翻译项目时，发现UI中错误，并且错误日志中出现空点异常(NPR-31896)。

### 集成 {#integrations-6540}

* Launch库URL生成仅基于 `path` 和 `library_name` 值，并且不基于 `library_path` 值(NPR-31550)。

* 处理LiveFyre相关项目时显示错误消息(FYR-12420)。

* ReportSuitesServlet 容易遭受服务器端请求伪造 (SSRF) 攻击 (NPR-32156)。

### WCM模板编辑器 {#wcm-template-editor-6540}

* 在可编辑的模板结构模式下，布局容器中允许的组件列表不显示链接按钮组件(CQ-4282099)。

### WCM页面编辑器 {#wcm-page-editor-6540}

* 选择叠加并选择响应式网格将组件拖动到此处时出现错误(CQ-4283342)。

### 营销活动定位 {#campaign-targeting-6540}

* Target云配置失败，错误为get mbox请求失败(CQ-4279880)。

### Brand Portal {#assets-brand-portal-6540}

* Brand Portal用户无法将贡献文件夹资产发布到 [!DNL Assets] 升级到 [!DNL Adobe I/O] Experience Manager6.5.4(CQDOC-15655)。 要立即修复Experience Manager6.5.4，建议 [下载修补程序](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) 并在创作实例上安装。

* 元数据架构弹出窗口值在资产属性中不可见(CQ-4283287)。

* 元数据子架构不显示基于资产属性中MIME类型的选项卡(CQ-4283288)。

* 取消发布元数据架构会填充一条错误消息，尽管该架构已在后端删除。

* 预览图像不显示已发布的资产(CQ-4285886)。

* 用户无法发布或取消发布名称中包含单引号的资产(CQ-4272686)。

* 下载多个资产时，不会显示条款和条件(CQ-4281224)。

* 已解决较小的安全漏洞。

### 社区 {#communities-6540}

* “创建成员”表单显示为空白页面(NPR-31997)。

* 用户无法查看有关创作实例的Analytics报表(NPR-30913)。

### Oak — 索引和查询 {#oak-indexing-6540}

* 使用Tika解析器解析时，包含JPEG图像的MS Word和MS Excel文档无法解析，并且发现类未找到错误(NPR-31952)。

### 表单 {#forms-6540}

>[!NOTE]
>
>Experience ManagerService Pack不包含针对Experience Manager Forms的修复。 它们是通过单独的 Forms 附加组件包交付的。此外，还发布了累积安装程序，其中包含JEE上的Adobe Experience Manager Forms修复。 有关更多信息，请参阅 [安装Experience Manager Forms附加组件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 和 [在JEE上安装Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* 通信管理：信件在提交到帖子流程工作流后显示额外的字符(NPR-32626)。

* 通信管理：信件在提交到后处理工作流后，会将下拉占位符显示为文本组件(NPR-32539)。

* 通信管理：信件模板中定义的默认值不会在预览模式下显示(NPR-32511)。

* 移动Forms:在以HTML版本呈现XDP表单时，提交按钮显示为已扩展的大小(NPR-32514)。

* 文档服务：应用Service Pack 2后，信件和其他一些页面的URL访问问题(NPR-32508、NPR-32509)。

* 文档服务：如果服务器上的事务数量超过特定限制，则PDF转换HTML失败，并且文件类型设置将从 [!DNL Forms] 服务器(NPR-32204)。

* 自适应Forms:根据WCAG2 AA级准则，浏览器辅助工具会报告自适应表单中的故障(NPR-32312、NPR-32309、CQ-4285439)。

* 自适应Forms:Chrome浏览器辅助工具报告最佳实践失败(NPR-32310)。

* 自适应Forms:配置嵌入到Experience Manager Sites页面中的自适应表单时出现翻译问题(NPR-32168)。

* 工作台：使用“获取PDF属性”操作获取PDF实用工具服务时显示错误消息(NPR-32150)。

* 文档安全：将DisableGlobalOfflineSynchronizationData选项设置为True时，无法脱机打开受保护的PDF文件(NPR-32078)。

* 设计器：如果启用了标记选项，则子表单边框会在生成的PDF输出中消失(NPR-32547、NPR-31983、NPR-31950)。

* 设计器：如果表中存在合并的单元格，则使用输出服务从XDP表单转换的输出PDF文件的辅助功能测试将失败(CQ-4285372)。

* Foundation JEE:如果Experience Manager Forms服务器与群集断开连接，则缓存问题会阻止它重新连接到服务器(NPR-32412)。

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0是一个重要版本，其中包括自6.5版本的正式发布以来发布的性能、稳定性、安全性以及关键客户修复和增强功能 **2019年4月**. 它可以安装在 [!DNL Adobe Experience Manager] 6.5。

此Service Pack版本的一些主要亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.6。

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档。

* 在DAM列表视图和列表视图中的资产搜索结果中添加了创建日期的新列（可排序）。

* 已在列表视图中启用基于名称列的资产排序。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。 “智能裁剪”是机器学习驱动的功能，用于在移动帧以跟踪场景焦点的同时重新裁剪视频。

* [!DNL Dynamic Media] 支持智能成像。

* 能够 [不在办公室](../forms/using/configure-out-of-office-settings.md) 首选项 [!DNL Experience Manager] 工作流。

* 能够 [共享收件箱或收件箱项目](../forms/using/configure-shared-queues-osgi.md) 中的其他用户 [!DNL Experience Manager] 工作流。

* 能够 [在批处理模式下生成交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* 将ContextHub中捆绑的jQuery版本更新为3.4.1。

### 资产 {#assets-6530-enhancements}

**产品增强功能**

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档(NPR-27573)。

* 在DAM列表视图中和列表视图中的资产搜索结果中添加了创建日期的新列（可排序）(NPR-31312)。

* 在列表视图中，用户可以使用 [!UICONTROL 名称] 列(NPR-31299)。

* GLB、GLTF、OBJ和STL文件可在 [!UICONTROL 资产详细信息] 页面(CQ-4282277)。

* `ReplicationOnModifyListener` 在区块上传期间为区块节点触发事件 [!DNL Dynamic Media] (CQ-4281279)。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资产。 “智能裁剪”是机器学习驱动的功能，用于在移动帧以跟踪场景焦点的同时重新裁剪视频(CQ-4278995)。

* [!DNL Dynamic Media] 支持智能成像(CQ-4222249)。

* 如果在请求中传递查询参数，则搜索或浏览视图将设置为Foundation选取器中的默认视图(NPR-31601)。

**修复**

* 某些PDF文档的元数据在其标题被修改时不会更新并保存到PDF中(NPR-31629)。

* 对于具有加号(`+`)（在文件名中）(NPR-31547)。

* 在默认搜索表单资产管理员搜索边栏中进行的编辑无法按预期工作(NPR-31502)。

* 对资产视图使用Omnisearch搜索搜索资产时，不会显示建议(NPR-31496)。

* 当引用的资产被移动到其他位置时，如果不同的用户引用了不同的收藏集，则不会更新收藏集中的资产引用(NPR-31486)。

* 资产元数据中添加了重复的IPTC标记(NPR-31328)。

* 从过滤器边栏触发搜索时，搜索结果计数不会准确更新(NPR-31316)。

* 取消选中“文件类型”筛选器中的二级复选框时，所有复选框都会被清除，并且搜索栏中的文本与选定或取消选中的属性不同步(NPR-31287)。

* 不能从文件夹的“成员”部分删除所有成员（用户/组）；尝试删除所有用户时，已登录的用户会添加到列表中(NPR-31171)。

* 带加号的资产(`+`)(NPR-31162)。

* “创建”下拉菜单（在选择文件夹的顶部菜单中可见）不会将“文件夹”显示为创建选项(NPR-30877)。

* 拒绝ACL时，缺少文件夹选择创建>文件上载操作项 `jcr:removeChildNodes` 和 `jcr:removeNode` 对用户应用路径(NPR-30840)。

* 上传某些mp4资产后，DAM工作流会进入过时状态，从而导致所有剩余的工作流都进入过时状态(NPR-30662)。

* 将大型PDF文件（数GB）上传到DAM并处理其子资产时，出现内存不足错误(NPR-30614)。

* 资产批量移动失败并显示警告消息(NPR-30610)。

* 将资产从一个文件夹移动到另一个文件夹(位于 [!DNL Experience Manager] 正在运行 [!DNL Dynamic Media]-Scene7模式(NPR-31630)。

* 对于位于与Scene7公司名称相同的文件夹中的图像，在编辑远程图像集时出错(NPR-31340)。

* [!DNL Dynamic Media] 未发布包含引用的资产(NPR-31180)。

* 上载自 [!DNL Dynamic Media]7-Scene7模式到 [!DNL Dynamic Media Classic] 需要过长时间才能完成(NPR-31048)。

* 通过交互式图像查看器在资产详细信息页面中不显示添加到图像资产的热点(NPR-30979)。

* 在中对资产执行操作后，将创建大量Sling作业，并重新显示“处理”横幅 [!DNL Experience manager Assets] 传递到Scene7(NPR-30947)。

* 创建资产的语言副本时出现冲突，且资产未上传到Scene7(NPR-30932)。

* 从下载的动态演绎版 [!DNL Experience Manager] 正在运行 [!DNL Dynamic Media] — 混合模式已损坏（它们属于内容为“无法找到图像”而不是图像内容类型的文本类型）(NPR-30876)。

* [!DNL Dynamic Media] 编码视频工作流无法为从中迁移的视频生成缩略图 [!DNL Dynamic Media Classic] to [!DNL Dynamic Media]-Scene7模式(CQ-4282011)。

* 在使用不同的Scene7公司ID将资产从一个实例迁移到另一个实例时观察到IpsApiException(CQ-4280548)。

* 当将受支持的3D模型摄取到中时，3D资产缩略图将不会提供信息 [!DNL Experience Manager] (CQ-4283701)。

* 如果3D资产的相机视图很少，则查看器中会显示滚动按钮(CQ-4283322)。

* 在“资产详细信息”页面的DimensionalViewer中预览的上传3D模型的容器高度不正确(CQ-4283309)。

* 在Internet Explorer 11和Safari(CQ-4281422)上，无法使用SmartCropVideoViewer播放视频。

* 使用“移动”按钮将多个资产从一个文件夹移动到另一个文件夹，在 [!DNL Experience Manager] 运行 [!DNL Dynamic Media]-Scene7运行模式(CQ-4280384)。

* 当MIME类型不是MP4时，资产详细信息中会显示扭曲的视频(CQ-4279704)。

* 在具有视频配置文件的文件夹中新摄取的视频即使在编码百分比完成到100%后仍处于处理状态(CQ-4279389)。

* 从文件夹移动资产会创建大量sling作业(Scene7 API调用)，而不是理想的必需作业(CQ-4278664)。

* 在Scene7中创建图像集（或媒体集）并使用DAM中的相应命名约定进行命名时，图像集的名称会更改为小写(CQ-4281112)。

* Scene7迁移器未正确设置发布状态(CQ-4263492)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动，并丢失用户在内容片段中的滚动位置(CQ-4282898)。

* PDF文件不会编入索引，并且中的内容也无法搜索(CQ-4278916)。

* 错误“用户选取器未列出组：在添加具有不同 `principalName` 和 `authorizableId` (CQ-4278177)。

* 资产UI列视图显示所有路径，而不考虑特定租户的dam根路径(CQ-4278175)。

* 资产选择器的搜索无法按预期工作(CQ-4275886)。

* 演绎版工作流失败(CQ-4271928)。

* DAM事件清除删除最新(`maxSavedActivities`)事件数据并保存之前创建的数据(NPR-31336)。

* 触屏UI搜索（通过Omnisearch完成）结果页自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在触屏UI中选择所有项目，然后取消选择某些项目（文件夹/单个资产）时，操作栏和资产计数不会进行更新(NPR-31118)。

* 中会显示一个例外 [!DNL Experience Manager] 轮询资产的作业详细信息时(CQ-4283569)。

### 站点

* 如果LiveCopy继承被破坏，则Live Copy页面会显示语言副本链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数超过40，则仅显示前40条记录。 Blueprint会为其余记录显示空行(NPR-31182)。
* 当用户在菜单的描述属性中添加日语或韩语字符时，该菜单会显示日语和韩语文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)。 意外地将内嵌字体大小应用于元素(NPR-31284)。
* 如果用户的焦点位于左侧边栏字段并使用键盘快捷方式粘贴内容，则会粘贴页面编辑器剪贴板的内容，而不是从左侧边栏字段复制的内容 (NPR-31172)。
* 当用户将文件上传字段添加到多字段时，图像路径将存储在组件节点中，而不是多字段节点中(NPR-30882)。
* 的 `ResponsiveGridExporter` API不返回 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 界面。 的 `com.day.cq.wcm.foundation.model.impl` 包声明为专用包(NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 在非编辑器模式下打开包含某些体验片段的页面时(在“创作”模式下，不使用 `editor.html` 前缀和 `wcmmode=disabled`，或在Publisher中)。请求以HTTP状态错误代码结束 `500` (NPR-30743)。
* 用户无法更改密码并访问其配置文件页面(NPR-31161)。

### 搜索和用户界面 {#ui-interface-and-search}

* 从搜索结果页面上的卡片视图切换到列表视图时，在可以滚动页面之前会出现延迟(NPR-31286)。

* 的 [!UICONTROL 全选] 复选框在列表视图中处于隐藏状态 [!DNL Sites] 用户界面(NPR-31614)。

* 的 [!UICONTROL 全选] 搜索结果页面上的计数不正确(NPR-31120)。

* 元数据编辑器会显示不存在的标记(NPR-31119)。

### 翻译 {#translation}

* 在翻译作业中选择到期日期选项时，会显示两个日历弹出窗口(NPR-31270)。

### 平台

* Web控制台中的Mime类型选项不起作用(NPR-31108)。

* 配置单点登录时不接受客户端证书(NPR-31165)。

* 基于 Jetty 的 HTTP 服务的缓冲区大小配置中的更新未保存 (NPR-30925)。

* QueryBuilder现在支持orderby `fn:name()` 在xpath查询中(NPR-31322)。

* 从升级时会创建重复的激活树 [!DNL Experience Manager] 6.3(NPR-31513)。

* 转发的请求不会保留在Sling身份验证期间设置的响应标头(NPR-30013)。

* 在选取器组件中搜索不起作用(NPR-31692)。

* 将ZIP文件附加到 [!DNL Experience Manager Communities] 帖子是由于Apache POI和Apache Tika包的不同版本所致(NPR-31018)。

* 的 `org.apache.sling.distribution.api` 包隐藏在配置管理器中，因此不可用于自定义包(NPR-31720)。

### 项目

* 切换日历视图不起作用(NPR-31271)。

### Brand Portal {#assets-brand-portal-6530}

**产品增强功能**

* 中的资产源导入工作流 [!DNL Experience Manager Assets] 已修改，以便仅从获取新创建的资产 [!DNL Brand Portal] to [!DNL Experience Manager]，并跳过NEW文件夹中已存在的资产，以避免复制(CQ-4278527)。

**修复**

* 在资产源功能(CQ-4282825)中创建新的Contribution文件夹时，显示错误图标。
* 创建新的Contribution文件夹时，Contribution文件夹(CQ-4282424)中不显示一个或多个子文件夹（NEW和SHARED）。
* 如果用户尝试从中重新发布Contribution文件夹，则系统会引发异常 [!DNL Experience Manager] to [!DNL Brand Portal] 在Contribution文件夹中从接收新资产后 [!DNL Brand Portal] end(CQ-4279740)。
* 禁止在Contribution文件夹（嵌套文件夹）中创建Contribution文件夹，以避免复杂性(CQ-4278391)。
* 上传时系统引发异常 [!DNL Brand Portal] 从导入的用户列表（.csv文件） [!DNL Experience Manager] Admin Console。 只有.csv文件中的“电子邮件”、“名字”和“姓氏”字段是必填字段(CQ-4278390)。

### 社区 {#communities-6530}

**修复**

* 社区管理员（组管理员/站点管理员）看不到管理组（打开/编辑/发布/删除组）的快速链接(NPR-31627)。
* 除非手动刷新/重新加载页面，否则不会显示提交的博客(NPR-31599)。
* “提及次数”功能使用的JCR查询区分大小写，并且需要过长时间才能返回结果(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar文件引发异常， `cq-social-translation` 缺少包 [!DNL Experience Manager] 6.5 UberJar文件(NPR-31186)。
* Jackson数据库库已更新到版本2.9.9.3，以解决新的漏洞(NPR-30967)。
* 活动和通知标题不一致 (NPR-30941)。
* 在中分页无法正常工作 [!DNL Communities] 博客(NPR-30914)。
* 未在中填充Analytics报表 [!DNL Experience Manager] 创作环境中显示空白页面(NPR-30913)。

### Oak {#oak}

* Lucene索引更新导致作者服务器减速(NPR-31548)。

### 表单 {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含 [!DNL Experience Manager Forms]. 它们是通过单独的 Forms 附加组件包交付的。此外，还发布了累积安装程序，其中包含针对 [!DNL Experience Manager Forms] 在JEE上。 有关更多信息，请参阅 [安装Experience Manager Forms附加组件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 和 [在JEE上安装Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Forms 附加组件包 {#forms-add-on-package-6530}

**自适应表单**

* 本地化自适应表单时，字符串包含词典键(NPR-31110)。

**交互式通信**

* **MissingNode.toString()** 将Jackson库升级到2.10.0后，返回不准确的结果(NPR-31549)。

* 文本编辑器从从Microsoft Word复制的文本中随机删除空格字符(NPR-31113)。

**通信管理**

* 将字母从LiveCycleES4SP1迁移到 [!DNL Experience Manager] 6.5(NPR-31615)。

* **不再支持文本流格式** 将信件另存为草稿时显示错误消息(NPR-30463)。

**工作流**

* OSGi工作流因100%的CPU利用率而失败(NPR-31233)。

**HTML5 表单**

* 在添加子表单的实例时，生成 XDP 表单的 HTML5 预览时会出现闪烁 (NPR-30909)。

#### Forms on JEE安装程序 {#forms-jee-installer-6530}

**表单 - 文档服务**

* 在.NET项目中使用MTOM的SOAP Web服务显示AssemblerServiceClient调用和HtmlToPDF2方法的异常(NPR-4281771)。

* 安全漏洞2012-5784和2014-3596随AXIS 1.4 jar一起发现，并修复了随 [AXIS1.4.1jar](https://helpx.adobe.com/cn/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015)。

**Foundation JEE**

* 操作配置不会加载调用Forms Workflow提交操作的进程名称(NPR-31478)。

### 包含的功能包 {#feature-packs-included-6530}

>[!NOTE]
>
>对于 [!DNL Experience Manager Forms] 客户，安装时必须 [!DNL Experience Manager Forms] 安装任何 [!DNL Experience Manager] Service Pack、累积修补程序包或功能包。

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms支持Oracle18c(NPR-29155)。

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0是一个重要版本，其中包括自推出以来发布的性能、稳定性、安全性以及关键客户修复和增强功能 [!DNL Adobe Experience Manager] 6.5英寸 **2019年4月**. 它可以安装在 [!DNL Experience Manager] 6.5。

此Service Pack版本的一些主要亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.3。
* 添加了配置属性，以允许将体验片段直接导出到用户定义的工作区，以便 [!DNL Adobe Target].
* 资产用户可以直观地搜索相似图像。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。请参阅[使用连接的资产](../assets/use-assets-across-connected-assets-instances.md)。

* EnhanceDocument类型筛选器具有更多MIME类型以支持多值选项。
* 引入了一个外部“重新处理”工作流以支持多种资源。
* 已优化 [!DNL Dynamic Media] 性能。
* 恢复了 DMS7 的裁剪/旋转资产编辑选项。
* 在 VideoPlayer 中实施了加载时使视频静音的选项。
* 修复以确保 Asset UI 列视图仅显示特定租户的内容。
* 修复以允许搜索结果中反映样式可折叠项的更改。

### 资产

**产品增强功能**

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。适用于 CQ-4270245 的修补程序. 请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 用户可以搜索视觉上相似的图像。 [!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

**修复**

* 通过 ACP API 生成的 URL 和文件夹元数据中的资产路径未进行 URL 编码。GRANITE-26198：适用于 CQ-4271814 的修补程序
* 无法使用名称中带有百分比符号(%)的文件夹解压缩存档 [!DNL Experience Manager Assets] 界面。 NPR-29989：适用于 CQ-4270467 的修补程序
* 触屏UI:在“管理发布”向导期间，会在帖子请求正文中的页面之后添加引用，从而导致所有资产在页面后发布，并且当页面呈现时，发布实例中的某些资产会丢失。 NPR-29985：适用于 CQ-4270724 的修补程序
* “取消关联资产”功能无法用于名称中包含特殊字符（成为 URI 编码的字符）的关联资产。NPR-30387：适用于 CQ-4274446 的修补程序
* 编辑内容片段时，使用错误的用户创建此版本。
* 在基于“租户”的系统上创建收藏集失败。NPR-30114：适用于 CQ-4272948 的修补程序
* Asset UI 列视图不遵循当前租户的 dam 根路径，而是访问所有租户的 dam 路径。NPR-30636：适用于 CQ-4275481 的修补程序
* 由于能够看到插入的图像，可通过受限的文件警告窗口实施跨站点脚本 (XSS) 攻击。NPR-30617：适用于 CQ-4270133 的修补程序
* 多租户：保存文件夹属性的租户会看到成功提示和描述操作失败的错误消息：“无法编辑属性。 权限不足。”因此，让租户感到困惑。NPR-30545：适用于 CQ-4275333 的修补程序
* 资产选择器对话框不允许选择资产，因此无法使用相关源替换功能来更新源。NPR-30502：适用于 CQ-4275029 的修补程序
* [!UICONTROL DAM更新资产] 工作流 — 上传大型mp4文件时处于过时状态。 NPR-30480：适用于 CQ-4271352 的修补程序
* 由于有效负荷为空，“创建审核任务”功能不起作用，使所有后续与审核任务相关的操作失败。NPR-30468：适用于 CQ-4274263 的修补程序
* 通过 Datapower 实施的 Adobe 智能标记存在连接问题。NPR-30026：适用于 CQ-4269457 的修补程序
* 尝试打开左边栏上的筛选器时，Assets UI 列视图引发一个错误。NPR-30501：适用于 CQ-4273862 的修补程序
* 在“资产文件夹”的“已关闭的用户组”(CUG) 属性中添加从 LDAP 同步的组后，不会保存和检索组。NPR-30615：适用于 CQ-4274689 的修补程序
* 筛选搜索样式和方向字段不会将自动完成的值应用于搜索查询。NPR-30620：适用于 CQ-4275724 的修补程序
* 对于某些资产，名称中包含空格和“&amp;”字符的文件夹的资产共享链接显示为空白灰色卡片。NPR-30557：适用于 CQ-4270187 的修补程序
* 文件夹元数据架构表单不会自动检测数据类型，因此，在表单提交中没有创建相关的 TypeHint。NPR-30599：适用于 CQ-4275227 的修补程序
* DMS7 创作 UI 中的裁剪和旋转资产编辑选项被禁用。NPR-30118：适用于 CQ-4273221 的修补程序
* “共享链接”功能无法使用 [!DNL Experience Manager] 具有DMS7配置的实例。 NPR-30080、NPR-30492：适用于 CQ-4273651 的修补程序
* 添加 [!DNL Dynamic Media]-Scene7组件添加到页面，然后发布页面不会每次触发dmscene7配置。 NPR-30641：适用于 CQ-4275962 的修补程序
* 在 [!DNL Experience Manager] 为每个处理配置文件仅创建一个入侵防御系统(IPS)作业。 NPR-30490：适用于 CQ-4273614 的修补程序
* [!DNL Dynamic Media]:添加了默认过滤器，用于排除将资产复制到 [!DNL Experience Manager] 发布节点。 NPR-30538：适用于 CQ-4274678 的修补程序
* 为多资源支持引入了一个外部“重新处理”工作流，以允许文件夹作为有效负载。工作流包含两个步骤 - 通过到下一步的元数据映射重新处理没有句柄的资产，并在单个 IPS 作业中将所有没有资产句柄的资产重新上传到 S7。有关更多详细信息，请参阅配置 [!DNL Dynamic Media] Cloud Services。 NPR-30489：适用于 CQ-4272903 的修补程序
* 正确的 CSV 擦除正确的 CSV 后，会上传一个错误的 CSV。适用于 CQ-4277694、CQ-4277814 的修补程序
* 特定于要删除的贡献文件夹的图标错误。适用于 CQ-4277580 的修补程序
* 在资产贡献选项卡的用户选取器中选择用户时，表中不显示用户的名称，并且属性页面的“删除用户”对话框中显示错误文本。适用于 CQ-4277875 的修补程序
* 无法在用户选取器中通过选择用户和单击添加操作将参与者添加到资产贡献文件夹。适用于 CQ-4277824、CQ-4278087 的修补程序
* 用户选取器中按小写用户名称搜索不起作用。适用于 CQ-4277958、CQ-4277930 的修补程序
* 非管理员可以在资产贡献文件的新文件夹中发布资产。适用于 CQ-4278200 的修补程序
* dam 用户（非管理员）无法选择将参与者添加到资产贡献文件夹。适用于 CQ-4278192 的修补程序
* “创建”按钮在资产贡献文件夹中可见。适用于 CQ-4277560 的修补程序
* 按相关性返回对搜索查询进行排序 [!DNL InDesign] 文档及 [!DNL InDesign] 模板。 适用于 CQ-4273864 的修补程序
* 如果用户的电子邮件 ID 为大写字母，则该用户无法签入以前签出的那些资产。适用于 CQ-4276575 的修补程序
* “删除”操作仅应用于选定的预设，如果执行该操作后屏幕自动刷新列表，则会显示已刷新的其他预设。适用于 CQ-4261461 的修补程序
* 配置 [!DNL Dynamic Media] Cloud Services [!DNL Dynamic Media] — 混合模式会导致在 [!DNL Analytics]，并且 [!DNL Experience Manager]，从而导致报表包重复。 适用于 CQ-4249780 的修补程序
* 中的重命名操作 [!DNL Experience Manager] 资产到重复名称的同步失败，无法与Scene7同步。 适用于 CQ-4276763 的修补程序
* 搜索筛选器面板中错误地显示用户生成内容。适用于 CQ-4273875 的修补程序
* “查找近似项”选项不适用于 TIFF 图像。适用于 CQ-4278238 的修补程序
* 在 VideoPlayer 中实施了加载时使视频静音的选项。适用于 CQ-4266465 的修补程序
* 查看器 — VideoViewer:如果使用外部视频，则poster=none无法正常工作。 适用于 CQ-4265536 的修补程序
* 在 IE11 和 MS Edge 浏览器中播放视频期间显示“等待”图标。适用于 CQ-4251539 的修补程序
* 3.8 SDK和5.13查看器自述文件未更新，并包含以前版本的信息。 适用于 CQ-4273737 的修补程序
* 即使在保存更改之前，也要对内容片段进行版本控制。NPR-30616：适用于 CQ-4273088 的修补程序
* 在缩略图进程中用 Asset#getMetadataValueFromJcr(String) 替换 Asset#getMetadata(String)。NPR-30491：适用于 CQ-4273067 的修补程序
* 上传 jpg 会导致每个资产显示消息的多个实例：“ReplicateOnModifyWorker 复制更新”，从而导致性能降低。
* 使用“提取存档”功能解压缩 zip 存档会导致标题中包含百分号 (%) 的文件夹出现问题。NPR-29990：适用于 CQ-4270467 的修补程序

### 站点 {#sites-6520}

* 如果LiveCopy继承被破坏，则Live Copy页面会显示语言副本链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数超过40，则仅显示前40条记录。 Blueprint为其余记录显示空行(NPR-31182)。
* 文本组件的富文本编辑器(RTE)插件会显示日语和韩语文本的扭曲字符(NPR-31331)。
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)会意外地将内嵌字体大小应用于元素(NPR-31284)。
* 当用户的焦点位于左边栏字段并使用键盘快捷键粘贴内容时，会粘贴页面编辑器剪贴板的内容，而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户将文件上传字段添加到多字段时，图像路径将存储在组件节点中，而不是多字段节点中(NPR-30882)。
* 的 `ResponsiveGridExporter` API不返回 `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` 界面。 的 `com.day.cq.wcm.foundation.model.impl` 包声明为专用包(NPR-31398)。
* 在非编辑器模式下打开包含某些体验片段的页面时(在“创作”模式下，不使用 `editor.html` 前缀和 `wcmmode=disabled`，或在“发布者”中)，请求以HTTP状态错误代码500(NPR-30743)结束。

### WCM - 页面编辑器 {#wcm-page-editor-6520}

**产品增强功能**

* `EnhanceDocument` 键入包含更多MIME类型的过滤器，以支持多值选项。 适用于 CQ-4270694 的修补程序

### 内容片段管理 {#content-fragment-management-6520}

* 内容片段模式 UI 使用的查询非常缓慢，最终会导致错误。适用于 CQ-4270807 的修补程序

### UI - Foundation {#ui-foundation}

* 快捷方式触发器阻止用户在特定用户界面中使用“m”、“p”、“e”。NPR-30355：适用于 GRANITE-26346 的修补程序
* 关闭 [!DNL Experience Manager Assets] 搜索UI不会将左边栏重置为内容选择，从而阻止用户随后第二次打开过滤器边栏。 NPR-30509：适用于 CQ-4274716 的修补程序
* 多租户环境： [!DNL Experience Manager Assets] UI顶部导航不可用，并且引发JavaScript错误。 NPR-30104：适用于 GRANITE-26344 的修补程序

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
>[!DNL Experience Manager] Service Pack不包含 [!DNL Experience Manager Forms]. 它们使用单独的 [!DNL Forms] 附加组件包。 此外，还发布了累积安装程序，其中包含针对 [!DNL Experience Manager Forms] 在JEE上。 有关更多信息，请参阅 [安装Experience Manager Forms附加组件](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 和 [在JEE上安装Experience Manager Forms](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

的主要亮点 [!DNL Experience Manager] 6.5.2.0表单包括：

* 将“自动”设置添加到 `RenderAtClient` in `PDFFormRenderOptions` API [!DNL Experience Manager] FormsOSGi。

#### Forms 附加组件包

**后端集成**

* 无法使用 AWS 托管的负载平衡 URL 来配置“表单数据模型”。NPR-30123：适用于 CQ-4273359 的修补程序
* 使用Web服务定义语言(WSDL)创建表单数据模型(FDM)时，出现错误消息 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 返回：NPR-30477:适用于CQ-4272921的修补程序

**通信管理**

* “创建通信UI(CCR UI)呈现间歇性失败，控制台中出现以下错误：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**交互式通信**

* 表单数据模型中标记为必填的字段将按“创建通信 UI”(CCR UI) 中的要求显示。NPR-30623：适用于 CQ-4274902 的修补程序

**表单 - 工作流**

* “监视文件夹”中未映射的输出变量导致调用失败。适用于 CQ-4264451 的修补程序

**HTML5 表单**

* 第二次部署自定义代码或项目时，页面不会呈现，并且会出现以下错误：

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：适用于 CQ-4272509 的修补程序

* 在浏览模式下使用 NonVisual Desktop Access 读取 HTML5 表单时，Chrome 浏览器会读取表单设计中每个可缩放矢量图形 (SVG) 前的“图形”。NPR-30449：适用于 CQ-4274732 的修补程序

#### Forms JEE 安装程序

**表单 - 文档安全**

* 应用带有时间戳的签名失败，并出现错误：ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: 调用错误。NPR-30820：适用于 CQ-4275852 的修补程序

**表单 - 文档服务**

* 如果“SubmitURL”包含与号(&amp;)，则在对 `renderpdf` servlet. NPR-30865：适用于 CQ-4278232 的修补程序

**Forms - Foundation JEE**

* HTMLtoPDF服务在JMX控制台中不显示maxReuseCount。 NPR-30134、NPR-30304：适用于 CQ-4273763 的修补程序
* 通过从调用Web服务来添加或编辑Web服务连接 [!DNL Experience Manager Forms] Workbench会引发错误：ClassNotFoundException org.apache.axis.message.SOAPBodyElement。 NPR-30105：适用于 CQ-4273217 的修补程序

### 包含的功能包

>[!NOTE]
>
>对于 [!DNL Experience Manager Forms] 客户，安装时必须 [!DNL Experience Manager Forms] 安装任何 [!DNL Experience Manager] Service Pack、累积修补程序包或功能包。

#### 站点 {#sites-feature-packs-included}

* 添加了配置属性，以允许将体验片段直接导出到用户定义的工作区，以便 [!DNL Adobe Target]. NPR-29189：适用于 CQ-4249782 的修补程序

#### 表单 - 文档服务 {#forms-document-services-1}

* 将“自动”设置添加到 `RenderAtClient` in `PDFFormRenderOptions` API [!DNL Experience Manager Forms] OSGi。 NPR-30759：适用于 CQ-4278193 的修补程序

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是一个重要版本，其中包括自推出以来发布的性能、稳定性、安全性以及关键客户修复和增强功能 [!DNL Adobe Experience Manager] 6.5英寸 *2019年4月。* 它可以安装在 [!DNL Experience Manager] 6.5。

此Service Pack版本的一些主要亮点包括：

* 支持在跟踪事件中包含动态 UI 状态作为自定义属性。
* 包括支持在 [!DNL Dynamic Media]-Scene7模式。
* 已启用 *日文自动换行* 功能。 有关更多信息，请参阅 [配置日语自动换行](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 资产

* 针对 S3 多部分支持更新了 DAM DMGateway 接口。NPR-29740：适用于 CQ-4226303 的修补程序
* 演绎版预览会生成 `Only empty tenantId is currently supported` 升级到 [!DNL Experience Manager] 6.5. NPR-29986:适用于CQ-4272353的修补程序
* “删除”对话框不可见，因此不允许删除作业。NPR-29720：适用于 CQ-4271074 的修补程序
* 在属性页面中添加资产标题后，当用户尝试关闭页面时， [!DNL Experience Manager] 再次打开属性页面。 NPR-29627：适用于 CQ-4264929 的修补程序
* VersioningTimelineEventProvider 应该提供 root 版本以及 nt：version 类型的节点。适用于 GRANITE-26063 的修补程序
* 实现了在中上传和播放360个球面视频的功能 [!DNL Experience Manager] DM-Scene7模式。 适用于 CQ-4265131 的修补程序
* 如果编辑了源，则 Live Copy 检索错误的状态。适用于 CQ-4265451 的修补程序
* 为 [!DNL Experience Manager Assets]. 适用于 CQ-4271453、CQ-4268621、CQ-4257491 的修补程序
* [!DNL Experience Manager] 界面应在时间轴历史记录中为资产的当前版本显示一个额外条目，并显示 [!DNL Adobe Asset Link]. 适用于 CQ-4262864 的修补程序
* 内容片段时间轴在属性缺失时显示一条错误消息。 适用于 CQ-4272560 的修补程序
* 扩展到全屏时，Scene 7 视频播放器出现问题。适用于 CQ-4266700 的修补程序
* ZoomVerticalViewer：使用单个图像资产时不应显示“全景”按钮。适用于 CQ-4264795 的修补程序
* 删除 Live Copy 中的儿童模式时应分离 liveRelationship。适用于 CQ-4270395 的修补程序
* 元数据架构仅包含来自全局配置的项目，丢失了来自活跃租户的项目。即使在更改之后，formPath URL 值也会恢复为默认值。NPR-29945：适用于 CQ-4262898 的修补程序
* 将图像预设发布到 [!DNL Brand Portal] 失败，错误代码为500。 NPR-29510：适用于 CQ-4268659 的修补程序

### 站点

* 在转出期间，不会从 Blueprint 传播空属性和多属性。使用 Blueprint 重置 Live Copy 不适用于组件。NPR-29253：适用于 CQ-4264928、CQ-4264926、CQ-4267722 的修补程序
* CoralUI(与 `Multifield`，存储 `fileReferenceParameter` 在组件级别，而不是多字段级别。 NPR-29537：适用于 CQ-4266129 的修补程序
* 增强 [!DNL Experience Manager] 文本组件和文本编辑器转换为日语。 NPR-29785：适用于 CQ-4265090 的修补程序
* 使用时间扭曲恢复的页面在版本控制时应该引用正确的图片。NPR-29431：适用于 CQ-4262638 的修补程序
* 样式系统节点从父节点继承到子节点时出现问题。 NPR-29516：适用于 CQ-4270330 的修补程序
* 将社交帖子设置为 [!DNL Facebook] 身份验证。 NPR-29211：适用于 CQ-4266630 的修补程序
* “内容片段”上呈现的缩略图使用内部日历来表示“日期和时间”字段。NPR-29531：适用于 CQ-4269362 的修补程序
* 在 Coral2 实施中打开权限选项卡时不显示按钮。适用于 CQ-4269419 的修补程序

### 商务

* 为电子商务运行延迟内容迁移时引发 ConstraintViolationException。NPR-29247：适用于 CQ-4264383 的修补程序

### 内容片段管理

* 打开包含字符元的内容片段时解析错误 `($)` 左大括号 `({)`. 适用于 CQ-4270266 的修补程序

### 体验片段

* 导出 [!DNL Experience Manager] 体验片段到 [!DNL Adobe Target]. 适用于 CQ-4265469 的修补程序
* 使用智能图像将体验片段导出到target失败。 适用于 CQ-4269606 的修补程序

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

* 升级到 [!DNL Experience Manager] 6.4.3使多站点管理器需要很长时间才能推出。 适用于 CQ-4271410 的修补程序

### 集成

* BrightEdge 凭证失败，出现连接错误。NPR-29168：适用于 CQ-4265872 的修补程序

* 尝试编辑和保存时，会显示异常消息 [!DNL Experience Manager] 启动配置。 NPR-29176：适用于 CQ-4265782/CQ-4266153 的修补程序

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

* 在OAuth期间，每次复制到 [!DNL Brand Portal]. NPR-30001：适用于 GRANITE-26196 的修补程序

### 项目

* 发布 [!DNL Experience Manager Assets] 从 [!DNL Experience Manager] 将/content/dam/mac文件夹创作到 [!DNL Brand Portal] 没用。 NPR-29819：适用于 CQ-4271118 的修补程序

### 平台

* HtmlLibraryManager 在缓存失效时删除 crx-quickstart 的所有内容。NPR-29863：适用于 GRANITE-26197 的修补程序

### Felix

* 使用Java11\时，系统控制台中未显示内存使用情况详细信息。 NPR-29669

### 表单

的主要亮点 [!DNL Experience Manager Forms] 6.5.1.0包括：

* 仅OSGi:添加了新属性 `PAGECOUNT` 输出和Forms服务。

* 仅限OSGI:支持使用Forms服务创建静态PDF文件。
* 为管理员和根用户启用了对 XMLForm.exe 的权限。
* 为 Dynamics 内部部署集成启用了对 ADFS v3.0 的支持。

#### Forms 附加组件包

**后端集成**

* 获取受保护的 Web 服务定义语言 (WSDL) 失败。NPR-29944：适用于 CQ-4270777 的修补程序
* When [!DNL Experience Manager Forms] 安装在IBM WebSphere上，因此基于SOAP创建表单数据模型失败。 适用于 CQ-4251134 的修补程序
* 为 Microsoft Dynamics 内部部署集成启用了对 Active Directory 联合身份验证服务 (ADFS) v3.0 的支持。适用于 CQ-4270586 的修补程序
* 数据源的标题发生更改时，表单数据模型不显示更新的标题。适用于 CQ-4265599 的修补程序
* 如果实体或属性的名称包含连字符或空格，则表达式无法计算此类实体和属性。 适用于 CQ-4225129 的修补程序

* 原始字符串输出中存在冒号时，观察到错误的输出。 适用于 CQ-4260825 的修补程序

* 即使 REST API 输出中没有任何内容，表单数据模型的调用操作也会引发错误。适用于 CQ-4268828 的修补程序

**自适应表单**

* 在延迟加载期间，无法在“自适应表单片段”中添加新实例。NPR-29818：适用于 CQ-4269875 的修补程序
* 验证组件没有记录或显示“记录文档”模板的任何错误。适用于 CQ-4272999 的修补程序
* 添加了对“自适应表单”禁用布局编辑器的支持。适用于 CQ-4270810 的修补程序
* 已在中恢复自适应Forms的验证步骤 [!DNL Experience Manager] 6.5.适用于CQ-4269583的修补程序

* 自适应表单字段验证失败中断 [!DNL Adobe Sign]. 适用于 CQ-4269463 的修补程序
* 当 [!DNL Experience Manager Forms] 实例具有20多个自适应表单片段，且所有表单片段的名称以同一字符串开头，则搜索将返回“不”或仅返回最近创建的20个片段。 适用于 CQ-4264414、CQ-4264914 的修补程序

* 将自适应Forms应用程序与大数据集一起使用时出现性能问题。. 适用于 CQ-4235310 的修补程序

* 通过匿名帐户在发布实例上进行访问时，GuideRuntime 脚本加载失败。适用于 CQ-4268679 的修补程序

**表单 - 交互式通信**

* “交互式通信”模板未在允许的组件列表中列出页眉和页脚组件。适用于 CQ-4237895 的修补程序
* 创建包含图像字段的交互式通信打印模板时，图表标题将设置为空白。适用于 CQ-4264772 的修补程序
* 图表的线条颜色在删除后设置为未定义。适用于 CQ-4264762 的修补程序
* 执行保留更改同步时，对文档片段所做的布局层更改消失。 适用于 CQ-4266054 的修补程序
* “文档片段”中绑定到文本字段的表单数据模型元素不显示继承图标，并且允许绑定。适用于 CQ-4261089 的修补程序
* “打印渠道”呈现 API 没有在 API 中作为参数传递数据的选项。适用于 CQ-4263540 的修补程序
* 当字符串字段/变量的绑定类型从文本片段更改为无/数据模型对象时，代理设置不可见，因为“可编辑者代理”复选框处于未选中状态。 适用于 CQ-4261953 的修补程序
* 在提交代理UI时，生成的Web数据json文件存储了取消继承的未绑定字段的信息。 适用于 CQ-4265621 的修补程序

**表单 - 工作流**

* 从自适应表单应用程序的发件箱重新提交表单时，将导致数据丢失。NPR-28345：适用于 CQ-4260929 的修补程序
* 对于不可变情况，保存时不会关闭文档。适用于 CQ-4269784 的修补程序
* “自适应表单”应用程序取消了对 Microsoft Windows 8.1 的支持。适用于 CQ-4265274 的修补程序。
* 当超过2 MB的图像作为字段级别附件附加到Android版本中的表单时 [!DNL Experience Manager Forms] 应用程序崩溃。 适用于 CQ-4265578 的修补程序

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

* [!DNL Experience Manager Forms] 6.5创建通信UI(CCR UI)无法打开通过 [!DNL Experience Manager Forms] 6.3.适用于CQ-4266392的修补程序
* 如果 DDE 数据类型是数字类型，则 XDP 中的求和功能将不起作用。适用于 CQ-4227403 的修补程序
* 内存中的字母缓存失效逻辑将被更新，因为当资产发布时，其最后修改时间不会更新。适用于 CQ-4250465 的修补程序
* 无法发布文档片段、DD 和 Letters。适用于 CQ-4272893 的修补程序

#### Forms JEE 安装程序

**PDF 生成器**

* 使用 64 位 JDK 时，将 CAD 文件转换为 PDF 失败。NPR-29924、NPR-29925：适用于 CQ-4272113 的修补程序
* 将 PhantomJS 的名称替换为 WebToPDF 以进行 HTMLtoPDF 转换。NPR-29933：适用于 CQ-4234545 的修补程序
* 将 zip 文件转换为 PDF 时出现错误。适用于 CQ-4268628 的修补程序

**Forms - Designer**

* 对使用创建的静态PDF执行完整的辅助功能检查时 [!DNL Experience Manager Forms Designer]，主语言检查因缺少语言属性而失败。 适用于 CQ-4272923、CQ-4271002 的修补程序

**表单 - 文档安全**

* 带硬件安全模块(HSM)的数字签名在Java 11和Java 8上的OSGi Linux上不起作用。 NPR-29838：适用于 CQ-4270441 的修补程序
* 带硬件安全模块 (HSM) 的数字签名在 JEE Linux 上，以及所有受支持的应用程序（例如，JBoss 和 Websphere）上不起作用。NPR-29839：适用于 CQ-4266721 的修补程序
* 在 PDF 中使用“PDF 高级电子签名”(PAdES) 验证签名会生成 InvalidOperationException。NPR-29842：适用于 CQ-4244837 的修补程序
* 添加了对Office 2019\的文档安全扩展支持。 适用于 CQ-4254369、CQ-4259764 的修补程序

**表单 - 文档服务**

* PDF无法转换为PDF/A-1b，但表单字段没有外观dict。 NPR-29940：适用于 CQ-4269618 的修补程序

* OSGi:无法确定渲染期间生成的页数。 NPR-28922：适用于 CQ-4270870 的修补程序
* 在中使用Forms服务启用了对静态PDF文件的支持 [!DNL Experience Manager Forms OSGi]. NPR-28572：适用于 CQ-4270869 的修补程序
* 无法更改对 XMLForm.exe 的权限。NPR-29828、NPR-29237：适用于 Q-4267080 的修补程序
* 由创建的静态PDF [!DNL Experience Manager Forms] 服务器的输出模块不会使用所创建文档的语言填充语言属性/标记。 NPR-27332：适用于 CQ-4271002 的修补程序

**Forms - Foundation JEE**

* 最终部件中不可用的 pdfg_srt 会导致安装程序失败。NPR-29854：适用于 CQ-4270137 的修补程序
* LCBackupMode.sh 不起作用。NPR-29840：适用于 CQ-4269424 的修补程序
* UDP 端口引用应该从 WebSphere 的用户界面 (UI) 中删除。适用于 CQ-4264782 的修补程序

### 包含的功能包

#### 资产 — 已包含

* 为 [!DNL Experience Manager Assets]. 有关更多信息，请参阅 [使用MSM for Experience Manager Assets重复使用资产](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199：适用于 CQ-4259922 的修补程序

#### 站点 — 包含

* 导出 [!DNL Experience Manager] 体验片段到 [!DNL Adobe Target]. 有关更多详细信息，请参阅 [体验片段链接重写程序提供程序 — HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). 适用于 CQ-4265469 的修补程序

#### Forms — 文档服务 — 已包含

* 仅OSGi:在“输出”和“Forms服务”中添加了新属性PAGECOUNT。 NPR-28922：适用于 CQ-4270870 的修补程序
* 仅OSGi:支持使用Forms服务创建静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 为管理员和根用户启用了对 XMLForm.exe 的权限。NPR-29237：适用于 CQ-4267080 的修补程序

### OSGi 包和内容包

以下文本文档列出了 [!DNL Experience Manager] 6.5.1.0

中包含的OSGi包列表 [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-bundle-list.txt)

中包含的内容包列表 [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-content-package-list.txt)
