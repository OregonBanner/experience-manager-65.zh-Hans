---
title: '[!DNL Experience Manager] 6.5 service pack发行说明'
description: 特定于 [!DNL Adobe Experience Manager] 6.5 service pack 10的发行说明
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5 service pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.10.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2021 年 8 月 26 日 |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## [!DNL Adobe Experience Manager] 6.5.10.0中包含的内容 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0包括自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了Service Pack。

[!DNL Adobe Experience Manager] 6.5.10.0中引入的主要功能和增强功能包括：

* **增强的 [!DNL Content Fragment] 模型和编辑器**:您现在可以使用嵌套模型为结构化内容创建复杂的自定义 [!DNL Content Fragment] 模型。内容结构被模块化为基本元素，这些元素被建模为子片段。 更高级别的片段引用这些子片段。 更多数据类型增强功能（如高级验证规则）进一步增强了[!DNL Content Fragments]内容建模的灵活性。 [!DNL Experience Manager] [!DNL Content Fragment]编辑器支持在通用编辑器会话中嵌套的片段结构，并增强了诸如结构树视图和选项卡式痕迹导航在片段层次结构中的导航功能。

* **GraphQL API，适[!DNL Content Fragments]**&#x200B;用于：新的GraphQL API是以JSON格式交付结构化内容的标准方法。GraphQL查询允许客户端仅请求相关内容项来渲染体验。 这种选择消除了需要在客户端解析内容的内容过交付（借助HTTP REST API来实现）。 GraphQL架构是从[!DNL Content Fragment]模型派生的，API响应采用JSON格式。 在[!DNL Experience Manager]作为[!DNL Cloud Service]的中， [GraphQL查询会保留](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching)并处理缓存友好GET请求。 在[!DNL Experience Manager] 6.5中尚不可能。

* **层级管理和未来预览**:现在，用户有一个界面可访问其启动项的内 [!DNL Experience Manager] 容结构，包括在启动项中添加和删除页面的功能。此功能增强了[!DNL Experience Manager]启动项的灵活性，可创作目标内容版本以供将来发布。 [时间扭曲功能可](/help/sites-authoring/working-with-page-versions.md#timewarp) 将用户预览启动项作为未来的内容状态。

* **连接的资产**: [!DNL Experience Manager] 扩展了 [!DNL Connected Assets] 在适用的核心组 [!DNL Dynamic Media] 件中使用图像的功能。请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* **链接共享选项以下载资产或演绎版**:在将资产和收藏集共享为链接时，用户可以选择是允许下载原始资产，还是允许下载其演绎版，还是同时使用共享链接来下载这两种资产。此外，下载通过链接与他们共享的资产的用户可以选择仅下载原始资产，仅下载演绎版，或同时下载两者。

* **限制生成的子资产**:管理员可以限制为复合资产(如 [!DNL Experience Manager] PDF、PowerPoint、InDesign和Keynote文件)生成的子资产数。请参阅[管理复合资产](/help/assets/managing-linked-subassets.md#generate-subassets)。

* **Camera Raw支持**:提供了 [!DNL Camera Raw] 支持v10.4的 [!DNL Adobe Camera Raw] 新包。请参阅使 [用 [!DNL Camera Raw]](/help/assets/camera-raw.md)处理图像。

* 内置存储库(Apache Jackrabbit Oak)已更新至1.22.8。

* **辅助功能增强功能**:

   * [!DNL Dynamic Media] 为查看器提供了许多辅助功能增强功能。请参阅[[!DNL Dynamic Media] updates](#dynamic-media-65100)。

   * 平台提供了一些辅助功能增强功能。 请参阅[平台更新](#platform-65100)。

* **用户体验增强**:

   * [!DNL Experience Manager] 直接在文件夹下显示所有内容模型的列表，内容作者不必在文件结构中导航。现在，该功能需要的点击量更少，并且提高了创作效率。

   * [!DNL Sites]编辑器中的路径字段允许作者从[!DNL Content Finder]中拖动资产。

有关[!DNL Experience Manager] 6.5.10.0中引入的所有功能和增强功能的列表，请参阅 [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md)中的[新增功能。

以下是[!DNL Experience Manager] 6.5.10.0版本中提供的修复列表。

### [!DNL Sites] {#sites-65100}

* 在内容片段编辑器的&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡下的&#x200B;**[!UICONTROL 默认值]**&#x200B;字段中键入内容时，焦点会转移到另一个字段(NPR-36992)。

* 在指定路径下筛选[!DNL Content Fragment]模型时， [!DNL Experience Manager]搜索会返回所有具有`cq:Template`的节点，而不是只返回[!DNL Content Fragment]模型的路径和节点(SITES-1453)。
* [!DNL Content Fragments] 返 `null` 回为文件夹的状态(SITES-1157)。
* [!DNL Experience Manager] 不允许用户禁用和启用 [!DNL Content Fragment] 模型(SITES-1088)。
* 当用户移动、重命名或删除[!DNL Content Fragments]或媒体资产时，引用的[!DNL Content Fragments]不会自动更新(SITES-196)。
* 将组件从一个页面粘贴到另一个页面时，会产生JavaScript错误(NPR-37030)。
* 快速查看页面属性时，将打开其他页面的页面属性(NPR-37025)。
* 内容片段允许内容片段引用其自身。 选取器不支持该操作(NPR-36993)。
* 升级到Service Pack 9后，某些用户无法在Experience Manager中移动文件夹，并在日志中看到错误(SITES-1481)。
* 在编辑模式下调整布局容器中组件的宽度时，观察到闪烁(NPR-36961)。
* 提升启动项时，提升的启动项中的更改将会双重推广到其他启动项。 如果用户推广双重转出的启动项，则双重内容会反映在源页面上(NPR-36893)。
* [!DNL Experience Manager] 如果您使用图像核心组件将图像添加到页面，或者使用基础图像组件调整大小，则会向某些具有透明度的PNG图像添加灰色边框(NPR-36879)。
* [!DNL Experience Manager Sites] 管理员UI中模板数量较多，导航缓慢(NPR-36870)。
* 升级到Service Pack 9会阻止创作一些组件。 此问题不允许[!DNL Sites]用户创建新页面(NPR-36857)。
* `ContextHubImpl`方法会创建未关闭的`ResourceResolver`。 这会导致出现有关长时间运行`ResourceResolver`的警告消息，并且该服务有时会返回意外结果(NPR-36853)。
* 在从Blueprint页面属性同步单个Live Copy时，还会同步所有其他Live Copy(NPR-36829、NPR-36522)。
* 仅使用XLS MIME类型时，文件上传函数无法按预期工作(NPR-36785)。
* 带有pascal大小写和所有大写词的新标记不会显示在[!DNL Content Fragments]内的标记字段中(NPR-36742)。
* 添加[!DNL Content Fragment]时的“单个文本元素”选项会导致文本丢失，并创建与列表和嵌套列表相关的奇数格式(NPR-36565)。
* 当作者在页面上注释任何组件、删除组件并对删除操作执行撤消时，在站点控制台中尝试查看页面的时间轴数据时会遇到错误(NPR-36528)。
* 页面属性批量编辑器的[!UICONTROL 保存并关闭]选项会保存更改，但不会关闭编辑器(NPR-36527)。
* 当用户尝试将新的文本组件拖放到页面时，该组件会立即消失(NPR-36442)。
* 当用户键入包含空格（系统上不存在的标记）的按需标记并按Enter时，该标记将显示在字段下方。 但是，保存并重新打开[!DNL Content Fragment]后，不会显示按需标记(NPR-36441)。
* 通过Dispatcher访问实例时，无法删除模板(NPR-36385)。
* 移动页面时，需要手动刷新浏览器才能渲染更改(NPR-36381)。
* 选择组件时，可以按Ctrl+X或Ctrl+C（在Mac上按Command+X或Command+C）剪切或复制组件。 单击其他组件时，可以粘贴工具栏，但不能粘贴键盘（Ctrl+V或Command+V）(NPR-36379)。
* 当用户尝试使用剪刀图标剪切组件以将其移动到其他位置时，会出现控制台错误。 此外，粘贴时只移动一个组件(NPR-36378)。
* [!DNL Experience Manager] 在WCM或通知中存在没有索引的查询，会降低性能(NPR-36303)。
* 当作者恢复已删除的继承组件上的继承时，可用选项是同步所有页面内容。 内容作者需要同步完整页面，即使继承仅在一个组件上恢复也是如此。 完全同步可能会导致同步不需要的内容(NPR-34456、CQ-4310183)。
* 创作实例上组件的实时使用情况并不显示所有发生次数。 某些组件在1000多个页面中使用，但报表仅显示大约40个页面(CQ-4323724)。
* 当网站结构具有许多子页面时，与Experience Manager6.4.8.2(CQ-4322766)相比，在列视图中加载子页面需要花费更多时间。
* 取消选中“全部”在“转出页面”选项上不起作用(NPR-37070)。
* 打开页面的现有v3组件版本时，页面属性对话框未打开，并且记录了`NullPointerException`(SITES-1830)。

### [!DNL Assets] {#assets-65100}

[!DNL Assets]中修复了以下问题：

* 移动文件夹后，属性`jcr:title`的值不会在Publish实例上更新。 在创作中重命名和重新发布文件夹不会更新发布实例中该文件夹的`jcr:title`属性值(NPR-36369)。

* 如果选择了两个或更多资产并编辑了一个或多个元数据字段，则保存操作将失败，Safari浏览器中的错误代码为500(NPR-36413)。

* 由于日期格式不正确，批量元数据导入失败(NPR-36428)。

* 在[!UICONTROL 属性]页面中选择以更新元数据时，当架构提供了多个选项时，接口响应速度缓慢(NPR-36430)。

* 使用[!UICONTROL 到期状态]谓词的搜索筛选器不起作用(NPR-36436)。

* [!UICONTROL 文件夹元数据]属性中各个字段的弹出菜单不显示最后选择的值(NPR-36937、CQ-4314429)。

* 在搜索文件和文件夹时，如果用户应用过滤器并选择[!UICONTROL Files &amp; Folders]，则只显示文件，而不显示文件夹(CQ-4319543、NPR-36627)。

* 从文件夹中选择同一收藏集并从搜索结果中选择该收藏集时，工具栏选项会有所不同(NPR-36620)。

* 搜索结果页面上的[!UICONTROL 快速发布]选项不可用(NPR-36904、CQ-4317748)。

* 当用户在未指定资产扩展名的情况下创建资产的Live Copy时，下载Live Copy文件后，该文件将不可用(NPR-36903、CQ-4326305)。

* 将用户添加为子文件夹的所有者后，用户也会获得其父文件夹的所有者权限，进而获得父文件夹的其他子文件夹的所有者权限。 此外，在尝试删除用户时，该用户不会作为父文件夹的所有者被删除。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] 尝试为复合资产（如PowerPoint演示文稿）创建子资产时，会生成内存不足异常(NPR-36668)。

* 当用户移动已发布的站点页面中已使用的资产时，即使未选择用于发布的选项，站点页面也会再次发布(NPR-36636、CQ-4323500)。

* 使用Apache Tika MIME类型检测功能时，使用`AssetManager.createAsset`方法上传的资产会在临时目录中保留一个名为`apache-tika-*.tmp`文件的临时文件。 此临时文件使用所有可用的可用磁盘空间(NPR-36545)。

* 下载所有受DRM保护的资产，并且未遵循用户选择下载特定资产(CQ-4327422)。

* 无法将资产拖到用户界面上的`pathfield`(NPR-36849)。

* 在列视图中选择资产后，资产详细信息面板会消失(NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**辅助功能增强功能**

[!DNL Dynamic Media Viewers]中提供了以下辅助功能增强功能。

* 屏幕阅读器现在会讲述要搜索的占位符文本，并将电子邮件地址添加为共享资产时的必填字段，以作为链接对话框，并会朗读[!UICONTROL 请填写此字段]工具提示(CQ-4327761)。

* 现在，在使用键盘访问用户界面字段时，屏幕阅读器可以正确讲述[!UICONTROL 图像预设编辑器]中各个字段的名称和用途(CQ-4325677)。

* 现在，可从[!UICONTROL 富媒体类型]选项的资产选取器中，相应地将键盘焦点移至[!UICONTROL 查看器预设]对话框的搜索选项卡(CQ-4324736)。

* 使用键盘键在表单模式下导航时，屏幕阅读器会讲述与[!UICONTROL 图像预设]的[!UICONTROL 创建]选项卡(CQ-4323900)中的增量和减量选项对应的标签。

* 屏幕阅读器现在会朗读关于将资产共享为链接对话框的[!UICONTROL 搜索和添加电子邮件地址]选项(CQ-4323352)。

* 使用键盘键导航资产时，工具栏中会保留键盘焦点(CQ-4322037)。

* 屏幕阅读器现在会在[!UICONTROL 编辑图像处理配置文件]页面(CQ-4290734)的[!UICONTROL 响应式图像裁剪]中选择[!UICONTROL 添加裁剪]选项后，讲述新添加的[!UICONTROL 编辑]字段信息。

* 现在，在[!UICONTROL 编辑图像预设]和[!UICONTROL 创建交互式视频]页面上，屏幕阅读器在使用标题键盘快捷键(CQ-4290730)(CQ-4290701)导航页面时会相应地读出页面标题。

* 屏幕阅读器现在可以在导航以下页面时使用地标和区域快捷键识别屏幕的各个区域（如右面板区域、左面板、操作工具栏、查看器工具栏地标和可缩放图像地标）。

   * [!UICONTROL 查看器预设编辑器] (CQ-4290729)

   * [!UICONTROL 图像集编辑器] (CQ-4290710)

   * [!UICONTROL 创建交互式视频] (CQ-4290702)。

* 屏幕阅读器现在使用向下箭头键导航时，会朗读视频帧中共享选项的名称(CQ-4290728)。

* 屏幕阅读器现在会讲述[!UICONTROL Sprite]和[!UICONTROL [!UICONTROL [!UICONTROL 查看器预设编辑器]中外观]选项卡的和背景]选项卡中各种选项的名称(CQ-4290727)。

* “编辑视频编码”页面的[!UICONTROL 基本]选项卡中的必填字段，如用于编辑[!UICONTROL 宽度]的字段，现在具有星号符号(*)(CQ-4290725)。

* 屏幕阅读器现在会朗读[!UICONTROL 图像配置文件]页面(CQ-4290723)上选项的标签。

* 当焦点位于CSS编辑器上时，Windows用户现在可以在[!UICONTROL 查看器预设编辑器]上导航出扩展的CSS编辑器(CQ-4290720)。

* 在表单模式下导航时，在[!UICONTROL [!UICONTROL 编辑图像预设]的“基本”]选项卡上，屏幕阅读器现在会讲述各种编辑字段和选项的标签(CQ-4290717)。

* 屏幕阅读器现在会在资产详细信息页面的左侧导航中，为用户界面选项讲述角色和状态（已选择或未选择）(CQ-4290709)。

* 屏幕阅读器现在可以正确讲述图像的状态（已选或未选），并在[!UICONTROL 创建交互式视频]页面(CQ-4290707)的[!UICONTROL 内容]选项卡中切换图像的链接。

* 现在，当使用[!UICONTROL 创建交互式视频]页面上的向下箭头键导航时，屏幕阅读器会在视频时间轴比例尺中正确讲述各个区段的名称、角色和状态(CQ-4290706)。

* 屏幕阅读器现在会在[!UICONTROL 创建交互式视频]页面(CQ-4290704)中导航选项时，讲述名称、角色、默认状态（已选择或未选择）和属性。

* 屏幕阅读器现在会在导航[!UICONTROL Publish]页面(CQ-4290705)时，讲述[!UICONTROL 所有资产]和[!UICONTROL 所有收藏集]选项的名称、角色和默认状态（已选择或未选择）。

* 在[!UICONTROL 创建交互式视频]页面上上传不受支持的视频格式（MP4除外）时，Experience Manager会显示并宣布错误消息(CQ-4290700)。

* 现在，[!UICONTROL 创建交互式视频]页面上时间轴比例中数字的对比度（以秒为单位）符合最低要求的光度比，以便对颜色有限感知的用户可以轻松阅读(CQ-4290699)。

* 屏幕阅读器现在在导航[!UICONTROL 创建交互式视频]页面(CQ-4290697)时，会朗读[!UICONTROL 产品名称]字段的标签。

**已修复的问题**

[!DNL Dynamic Media]中提供了以下错误修复。

* 在启用`dynamicmedia_scene7`运行模式并禁用同步后，将视频上传到[!DNL Experience Manager]显示`Process failed`(CQ-4327791)。

### 平台 {#platform-65100}

此Service Pack中提供了以下增强功能：

* 当用户在树视图中选择项目时，屏幕阅读器会朗读所做的选择以及顶部显示的工具栏选项(NPR-36504)。
* 某些文本和控制名称对于出现视觉问题的用户来说更容易阅读，因为明度比率满足4.5:1的最低要求比率(NPR-36503)。
* 当用户使用日历控件时，屏幕阅读器会讲述描述性日期、月份和工作日信息。 用户使用日历快捷键时，屏幕阅读器会讲述日期、月和年的更改(NPR-36498)。
* 提供了使用ECMAScript 6功能执行自定义JavaScript `Clientlibs`而不遵守严格模式的支持。 具体而言，将`emitUseStrict`标记添加到`GCCScriptProcessor`(NPR-36411)。

以下错误修复是此Service Pack的一部分：

* 自定义运行状况检查的执行频率比计划的频率高(NPR-36985)。
* 对于别名页面，`Resourceresolver map`方法返回错误结果(NPR-36767)。
* [!DNL Experience Manager] 由于加载工作流，启动延迟(NPR-36615)。

### 集成 {#integrations-65100}

* Experience Manager在主MongoDB节点切换到另一个节点时变得无响应(NPR-36566)。
* [!DNL Sling content distribution] 执行收集成员删除操作时失败(NPR-36521、CQ-4323578)。

### 用户界面 {#user-interface-65100}

* **[!UICONTROL 引用]**&#x200B;侧面板不显示资产和站点引用(GRANITE-35078、GRANITE-34892)。

### 翻译项目 {#translation-65100}

* 将删除多翻译项目语言副本中的额外子页面(NPR-36622)。

### 工作流 {#workflow-65100}

* 如果服务器收到不在办公室的消息，它会报告内存警报并停止响应(NPR-36768)。

### [!DNL Communities] {#communities-65100}

* 对于匿名来宾用户，社区站点页面以`LoggedIn`状态打开(NPR-36908)。

* 当&#x200B;**[!UICONTROL 社区]** > **[!UICONTROL 构思]** > **[!UICONTROL 评论]**&#x200B;页面中有多个页面时，页面导航不起作用(NPR-36541)。

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


### 商务 {#commerce-65100}

* 显示的&#x200B;**[!UICONTROL 发布者]**&#x200B;字段中的值在列视图中不正确(NPR-36902)。
* 推出目录时，新产品会被错误地标记为已修改的产品(NPR-36666)。
* 重新创建已删除的产品时，不会重新创建产品页面(NPR-36665)。
* 已修改的页面会更新，但相应的链接产品在目录转出时不会更新(CQ-4321409、NPR-36422)。
* **[!UICONTROL 稍后发布]**&#x200B;和&#x200B;**[!UICONTROL 稍后取消发布]**&#x200B;工作流不起作用(CQ-4327679)。

有关安全更新的信息，请参阅[[!DNL Experience Manager] 安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安装 6.5.10.0 {#install}

**设置要求和更多信息**

* Experience Manager6.5.10.0需要Experience Manager6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载Service Pack。
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装Experience Manager6.5.10.0。

>[!NOTE]
>
>Adobe不建议移除或卸载[!DNL Adobe Experience Manager] 6.5.10.0包。

### 安装Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5实例上安装Service Pack，请执行以下步骤：

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄[!DNL Experience Manager]实例的快照或新备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip)下载Service Pack。

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅[Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题会在[!DNL Safari]浏览器中发生，但可能会间歇性地在任何浏览器上发生。

**自动安装**

在工作实例上自动安装[!DNL Experience Manager] 6.5.10.0的方法有两种：

A.当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 包会自动安装。

B.使用包管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安装嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下显示更新的版本字符串`Adobe Experience Manager (6.5.10.0)`。

1. 所有OSGi包均为OSGi控制台中的&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**(使用Web控制台：`/system/console/bundles`)。

1. OSGi包`org.apache.jackrabbit.oak-core`的版本为1.22.3或更高版本(使用Web控制台：`/system/console/bundles`)。

要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

<!--

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

适用于Experience Manager6.5.10.0的UberJar在[Maven Central存储库](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/)中提供。

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象在Maven中央存储库中可用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为`uber-jar-<version>.jar`。 因此，没有`classifier`作为`apis`值的`dependency`标记。

## 已弃用功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中标记为已弃用的特性和功能列表。在将来的版本中，这些功能最初被标记为已弃用，后来又被删除。 提供了备用选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | **[!UICONTROL AEM云服务选择加入]**&#x200B;屏幕已弃用，因为[!DNL Experience Manager]和[!DNL Adobe Target]集成已在Experience Manager6.5中更新。该集成支持Adobe Target标准API。 该API使用通过AdobeIMS和[!DNL Adobe I/O]进行身份验证，并支持AdobeLaunch发挥越来越大的作用，以便为分析和个性化设置[!DNL Experience Manager]页面，因此选择加入向导在功能上无关紧要。 | 通过相应的[!DNL Experience Manager]云服务配置系统连接、AdobeIMS身份验证和[!DNL Adobe I/O]集成。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR Connector已在Experience Manager6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 如果您要将[!DNL Experience Manager]实例从6.5版升级到6.5.10.0版，则可以在`error.log`文件中查看`RRD4JReporter`异常。 要解决此问题，请重新启动实例。

* 如果您在[!DNL Experience Manager] 6.5上安装[!DNL Experience Manager] 6.5 Service Pack 10或之前的Service Pack，则会删除资产自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以重命名[!DNL Assets]层次结构中的文件夹，并将嵌套文件夹发布到[!DNL Brand Portal]。 但是，在重新发布根文件夹之前，文件夹的标题不会在[!DNL Brand Portal]中更新。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数（如SUM、MAX和MIN）时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了[!DNL Experience Manager] 6.5.10.0中包含的OSGi包和内容包：

* [Experience Manager6.5.10.0中包含的OSGi包列表](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0中包含的内容包列表](assets/65100_packages.txt)

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅[如何联系Adobe客户关怀团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5发行说明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/subscription/priority-product-update.html)

