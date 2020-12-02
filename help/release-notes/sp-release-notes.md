---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack发行说明'
description: 特定于 [!DNL Adobe Experience Manager] 6.5 Service Pack 7的发行说明
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed8299662139c2c2ab2fa304c9fa3448b0fce223
workflow-type: tm+mt
source-wordcount: '3789'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack发行说明  {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.7.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2020年11月26日 |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}中包含的内容

[!DNL Adobe Experience Manager] 6.5.7.0是一项重要更新，包括自2019年4月发布6.5版以来发布的新功能、关键客户请求的增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了Service Pack。

[!DNL Adobe Experience Manager] 6.5.7.0中引入的主要功能和增强功能包括：

* 使用[!UICONTROL 名称]、[!UICONTROL 上次修改日期、]和[!UICONTROL 上次转出日期]属性对可用于转出的Live Copy页面进行排序。

* 将页面移动和MSM转出作为异步操作执行，以减少它们对运行时性能的影响。

* 用户可以在卡片和列视图中对数字资产进行排序。

* [!DNL Assets] 并提供 [!DNL Dynamic Media] 多种辅助功能增强。这些增强功能与键盘导航、屏幕阅读器的使用以及使用户能够使用类似的辅助技术(AT)相关。 请参阅[[!DNL Assets] 增强](#assets-6570)和[[!DNL Dynamic Media] 增强](#dynamic-media-6570)。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.22.5。

有关[!DNL Experience Manager] 6.5.7.0中引入的功能和增强功能的完整列表，请参见 [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md)中的[新增功能。

以下是[!DNL Experience Manager] 6.5.7.0版中提供的修复列表。

### [!DNL Sites] {#sites-6570}

* 打开页面的[!UICONTROL 时间绕排]选项时，保持时间轴侧边栏选项处于打开状态，并导航到[!UICONTROL 站点]控制台时，会出现`Failed to Load`错误(NPR-34951)。

* [!UICONTROL 时间绕排]选项不显示所选日期和时间范围的图像(NPR-34951)。

* 当筛选器从包含内容片段的页面调用`getHeader()`时，会出现`java.lang.AbstractMethodError`错误(NPR-34942)。

* 当页面的路径包含多个内容子字符串时，预览无法呈现，版本比较函数也会失败(NPR-34740)。

* 为组件的`String`类型标签属性设置数值时，可以删除组件并撤消删除操作。 但是，撤消删除后，label属性从`String`更改为`Long`(NPR-34739)。

* 在将基于具有锁定布局的模板的体验片段添加到页面时发生以下异常(NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* 移动文件夹时，会导致遍历问题，并出现以下错误(NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 创建、发布新资产并将其移动到新位置后，将创建`Request to complete move operation`工作流，并导致处于“已中止”状态。 上传新资产并执行`move`操作会导致创建处于挂起状态的`Request to complete move operation`工作流(NPR-34543)。

* 将体验片段从[!DNL Experience Manager] 6.5.2环境导出到[!DNL Target]标准版时，API调用将失败，因为工作区属性不可用于[!DNL Target]标准版(NPR-34557)。

* 用户无法通过[!UICONTROL 管理发布]选项发布页面，因为[!UICONTROL 发布]选项会消失(NPR-34542)。

* 向文本添加一些样式时，将向文本添加一个`<div>`标记，该样式不能再应用于文本(NPR-34531)。

* 当您在弹出菜单中选择一个项目并更新所需文件时，它不允许保存对话框值，因为其他菜单的必填字段为空(NPR-34529)。

* 当您从自定义模板创建页面并在Blueprint层次结构中移动它时，之前从页面开始中删除的组件会显示在Live Copy层次结构中的页面上(NPR-34527)。

* 将文章样式应用于内容后，便无法删除它(NPR-34486)。

* 体验片段的所有Live Copy和副本都指向相同的[!DNL Adobe Target]优惠ID(NPR-34469)。

* 项目符号列表项除了编号列表外还显示(NPR-34455)。

* “与源比较”选项无法显示源页面与已编辑页面版本之间的差异(NPR-34285)。

* 删除页面时，无法配置版本控制详细信息(NPR-34159)。

* 当用户选择[!UICONTROL 打开选择]对话框选项时，键盘焦点将移至页面上现有的隐藏控件(CQ-4307779、CQ-4293601)。

* 在作者上移动已发布的文件夹时，Publish实例上的文件夹路径不会相应地更新(CQ-4305144)。

* 当用户在[!UICONTROL 全选]选项上选择`Enter`键时，键盘焦点不会移到[!UICONTROL 创建控件]选项(CQ-4293599)。

* 选择`Esc`键时，焦点不会恢复到父控件(CQ-4293593、CQ-4293590)。

* 改进了[!DNL Sites] UI和核心组件的WCAG兼容性(CQ-4293448)。

* [!UICONTROL 页] 面  的Zoomand Scalefunctions [!DNL Sites Editor] 被禁用(CQ-4282353)。

* 使用“向右旋转”选项后，屏幕阅读器会停止对当前旋转或翻转状态的旁白(CQ-4282128)。

* “完成”和“取消配置”对话框按钮具有多个制表位(CQ-4274601)。

* 不允许在同一级别上移动同名的页面(NPR-35041)。

* 选择“清除(x)”选项后，键盘焦点不会移到[!UICONTROL Filter]字段(CQ-4293581)。

* 升级到[!DNL Experience Manager] 6.5.6.0时，继承的段落系统的行为会发生更改，并且无法正常工作(NPR-35117)。

* 在[!DNL AEM Sites]页面(CQ-4307786)上选择[!UICONTROL 操作]部分后，键盘用户无法按适当的顺序转移选项卡焦点。

* 在编辑内容片段时，在RTE工具栏的链接目标菜单列表中选择一个选项后，内容片段作者对话框会开始闪烁(CQ-4305532)。

* 键盘用户无法使用向下箭头键在[!UICONTROL 添加组件]下拉列表中选择选项(CQ-4295097)。

* 在[!DNL Sites]页面的[!UICONTROL 资产]选项卡的“日历”菜单中选择日期时，选项卡焦点不会按适当的顺序移动(CQ-4293600)。

* 在删除编辑“站点”页面时可用的“链接”或“文本”选项后，选项卡焦点不会转移到键盘用户的下一个或以前的选项(CQ-4293597)。

* 在查看可用选项并按`Esc`键(CQ-4293592)后，键盘用户无法将选项卡焦点移回[!UICONTROL Actions]部分的“更多”选项。

* 在[!UICONTROL 编辑]模式中为图像激活[!UICONTROL 旋转]选项时，选项卡焦点不是停留在旋转上，而是转向键盘用户的[!UICONTROL 重做]选项(CQ-4293587)。

* 在[!UICONTROL 链接和操作]选项卡上提供的[!UICONTROL 打开选择]对话框中，选项卡焦点在页面中的隐藏元素上移至[!UICONTROL 取消]选项(CQ-4293579)之后。

* 键盘用户编辑图像时，导航到[!UICONTROL 完成]选项，然后按Enter键，屏幕阅读器不会宣布完成(CQ-4282351)。

* [!UICONTROL 链接和操作]对话框中的“上移”和“下移”选项对屏幕阅读器和键盘用户不可用(CQ-4281120)。

* 键盘用户在导航至[!UICONTROL 属性]页面上的关闭(X)选项(CQ-4293581, NPR-34653)后无法恢复选项卡焦点。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0修复 [!DNL Assets] 了以下问题并提供以下增强。

* 对此版本中[!DNL Experience Manager Assets]的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Assets]](/help/assets/accessibility.md)中的[辅助功能。

   * 使用键盘导航时间轴时，`Esc`键可折叠[!UICONTROL 显示全部]选项，而不会失去焦点(CQ-4293598)。
   * 使用键盘Tab键导航时，从添加的标记中删除最后一个标记后，标记字段将保留焦点(NPR-35109)。
   * [!DNL Experience Manager] 组件现在包含要由屏幕阅读器使用的名称、角色和值的适当信息(NPR-34255)。
   * 删除“类型／大小”组合框、“链接”组合框、“语言”组合框或“文本”编辑框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素(CQ-4293585)。
   * 将指针悬停在选项上时，将显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用`Escape`键删除选项后，可以保留焦点。 (CQ-4293554).
   * 从页面中出现的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏(CQ-4282127)。
   * 可视用户可以区分普通文本和链接，因为在[!DNL Experience Manager]主页(CQ-4282072)中显示到所有解决方案的链接的可视提示（下划线和V形图标）。

* 以下用户体验增强功能在[!DNL Assets]中完成：

   * 在卡视图和列视图中启用资源排序(NPR-35097)。

* 升级到6.5后，如果使用Assets HTTP API生成JSON文件，则文件中使用的编码存在问题(NPR-35129)。

* 未提供创建集合权限的组的用户（“创建集合”选项不可用）仍可通过直接访问URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`(NPR-35115)来创建集合。

* 按名称排序时，搜索的资产会按区分大小写的方式排序。 这会基于在搜索结果中以有序方式显示的大小写创建两个单独的分类列表(NPR-35068)。

* 在编辑器中打开内容片段时，错误日志(NPR-35012)中会记录警告消息(`Invalid value specified for a metadata property`)。

* 没有管理员权限的用户可以使用[Experience Manager]桌面应用程序编辑过期的资产。 (NPR-34993).

* 当在“资产”用户界面上拖动同一资产并创建新版本时，元数据中的更改将不会持续存在(NPR-34940)。

* 编辑集合时，用户可以删除集合的标题并成功保存更改(NPR-34889)。

* 上传重复图像时，会显示删除选项。 选择“删除”可上传图像。 还会触发DAM更新资产工作流(NPR-34744)。

* 将[!DNL Adobe Asset Link]与[!DNL Adobe InDesign]一起使用时，搜索结果中不包含文件夹和集合，但仅包含资产(NPR-34699、CQ-4303666)。

* 将指针悬停在卡视图上时，屏幕会因（自动）聚焦卡中可用的快速操作而滚动(NPR-34514)。

* 批量编辑多个资产的属性时，选择[!UICONTROL 保存]选项将关闭批量编辑器视图并重定向到主[!DNL Assets]页面。 此行为与[!UICONTROL 保存并关闭]选项的行为相同，不应为(NPR-34546)。

* 保存后，智能集合不显示正确的用户界面设置。 查询正确保存，但界面始终显示上次添加的“选项”谓词(NPR-34539)。

* 向[!DNL Experience Manager]添加资产时，不带命名空间的元数据不会导入(NPR-34530)。

* 在文件夹上拖动资产以移动资产时，用户界面还显示选项[!UICONTROL 放入Lightbox]和[!UICONTROL 放入收藏集]。 即使取消移动操作，用户界面仍继续显示后两个选项(NPR-34526)。

* 符号`%>`显示在集合页面上(NPR-34499)。

* 在列视图中，[!DNL Assets]在向上和向下滚动时显示重复文件夹和资产名称，然后显示所有资产(NPR-34464)。

* 如果您在创建公共文件夹后立即创建了专用文件夹，则公用文件夹将使用专用文件夹设置(NPR-34415)。

* 在卡视图中，卡不按字母顺序列出，并且卡不能按字母顺序排序(NPR-34234)。

* 重新打开级联规则时，用户界面上的选项不会保留(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* 对[!DNL Dynamic Media](CQ-4290306)中的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)中的[辅助功能。

   * 屏幕阅读器(JAWS,Narrator)在“嵌入大小”菜单选项(CQ-4290927)中为菜单项说明名称、角色和状态。
   * 用户可以使用`Tab`键(CQ-4290926)导航“电子邮件链接”对话框。
   * 考虑到屏幕阅读器增强功能(CQ-4290623、CQ-4290622)，创建视频编码用户档案的工作流程更为用户友好。
   * 使用`Tab`键导航时，焦点将移至工作流中相应的用户界面元素，以创建交互式视频(CQ-4290621、CQ-4290620、CQ-4290619)。
   * “发布”页、“编辑资产”页、“编辑智能裁切”页和“图像集编辑器”页经过改进，符合Web标准。 辅助技术(AT)用户现在可以轻松导航这些页面并采取裁剪图像等操作(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * 对查看器进行了改进，允许用户使用键盘进行导航(CQ-4290615)。
   * 键盘和屏幕阅读器用户可以使用裁剪功能(CQ-4290609)。
   * 键盘用户可以更好地管理热点(CQ-4290604、CQ-4290603)。

* 如果公司名和文件夹名称相同，则远程图像集在[!DNL Experience Manager]中不可编辑(NPR-31340)。

* 在将热点添加到[!DNL Dynamic Media]图像或编辑带图像的[!DNL Dynamic Media]视频或[!DNL Experience Fragment]后尝试预览输出时，z索引顺序不正确(CQ-4307267)。

* [!DNL Dynamic Media] 在重新处理混合媒体集时，同步会失败(CQ-4307184)。

* 如果资产被移动到已配置到[!DNL Dynamic Media]的自动同步的文件夹，则资产不会同步(CQ-4307122)。

* [!DNL Dynamic Media] 在iOS设备上，使用本机HTML5视频控件(CQ-4306977、CQ-4306727)不播放视频。

* 无法下载应用了SmartCrop的图像(CQ-4304558)。

* 无法选择性地将文件夹发布到Dynamic Media(CQ-4304526)。

* 从[!DNL Experience Manager]取消发布视频文件时，不会从已配置的Scene7部署(CQ-4304405)取消发布自适应视频集。

* 在全景媒体组件中添加全景图像资源并刷新页面会导致`Uncaught ReferenceError: $ is not defined`错误(CQ-4302810)。

* 在[!UICONTROL 查看器预设编辑器]中，编辑[!UICONTROL PanoramicImage/PanoramicImage_VR]预设时，在`PanoramicView`组件中，`PANORAMICVIEW_AUTOROTATE`修饰符标签不可用(CQ-4302443)。

* 如果视频不是MixedMediaSet中的第一个视频字幕，则不显示视频字幕(CQ-4298161)。

* iPhone移动设备上的HTML5 eCatalog Viewer无法翻页或翻页(CQ-4296611)。

* 在移动设备上滚动色板时，色板滚动至可见区域的右侧和外侧几秒钟，然后滚回视图(CQ-4296439)。

* 创建查看器预设主控记录时，CSS和图稿不会发布，只会发布查看器预设(CQ-4262205)。

* 当尝试在[!UICONTROL 交互式视频／图像]组件中链接给定热点的体验片段时，它不显示选定的体验片段路径。 而是从路径字段返回一个空值(NPR-35146、CQ-4298136)。

* 无法在IVV编辑器中预览体验片段(CQ-4308560)。

* 在向图像添加热点并选择体验片段时，无法选择该子文件夹和体验片段的变体(CQ-4307455)。

* 上传后，非图像资产不会显示为已发布状态(CQ-4306415)。

#### [!DNL Experience Manager] 3D资源  {#three-d-assets-6570}

* `DAM CQ MIME Type` 服务将不正确的MIME类型应用于3D资产，导致呈现不正确(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* 商务产品集合用户界面不会列表集合中超过15个产品(NPR-34502)。

### 平台 {#platform-6570}

* 通过HTTPS的HTTP会话不会失效(NPR-35083)。
* 从用户界面开始每日或每周维护任务时，将返回`NullPointerException`(NPR-34953)。
* W3C validator报告兼容客户端库JavaScript文件的警告(NPR-34898)。
* `AudienceOmniSearchHandler`函数使用已弃用的索引(NPR-34870)。
* 从Experience Manager注销不会清除Cookie(NPR-34743)。
* 如果标记名称包含特殊字符(NPR-34357)，则`TagManager` API的`findByTitle`函数将不起作用。
* 导入用户同步包的过程失败(NPR-34399)。
* 为`Coral.Masonry`组件添加了对`ariaLabel`和`ariaLabelledby`属性的支持(GRANITE-29962)。
* 安装最新核心组件包(CQ-4306788)后，不会刷新包含内容片段的页面的调度程序缓存。
* 带引号(`"`)的本地化标记名称在用户界面上显示不正确(CQ-4305439)。

### 用户界面 {#ui-6570}

* 组件属性中的[!UICONTROL 链接到]字段显示与指定字符串不匹配的自动完成建议(NPR-34865)。

* AEM在计划2天之间分发的每日维护窗口时显示以下错误消息(NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 集成 {#integrations-6570}

* 编辑现有[!DNL Adobe Launch]配置失败(NPR-35045)。
* 如果使用IMS配置和[!DNL Adobe Target Standard]环境(NPR-34555)，则无法将[!DNL Experience Fragments]导出到[!DNL Adobe Target]。
* 当从文件夹导航到[!UICONTROL 受众]页面时，[!UICONTROL 创建]选项显示在[!UICONTROL 受众]页面上(NPR-35151)。

### Sling {#sling-6570}

* 默认登录运行状况检查会验证不存在的用户的凭据(NPR-34686)。

### 翻译项目 {#translation-6570}

* 在[!DNL Experience Manager]中取消翻译项目时，取消该项目的请求不会发送到翻译提供者(NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 产品中所有不公平术语的实例都被接受的等价物(NPR-34311)取代。
* [!DNL Google+] 从社交共享选项列表中删除(NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* 在[!UICONTROL 列表视图](NPR-34728)中选择资产时，用户界面不会做出响应。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的Service Pack发布日期后一周内 [!DNL Experience Manager] 发布加载项包。

有关安全更新的信息，请参阅[Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安装6.5.7.0 {#install}

**设置要求和更多信息**

* AEM 6.5.7.0需要AEM 6.5。有关详细说明，请参见[升级文档](/help/sites-deploying/upgrade.md)。
* 可在Adobe[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上下载服务包。
* 在具有 MongoDB 和多个实例的部署中，使用包管理器在其中一个 Author 实例上安装 AEM 6.5.7.0。

>[!NOTE]
>
>Adobe不建议删除或卸载[!DNL Adobe Experience Manager] 6.5.7.0包。

### 安装Service Pack {#install-service-pack}

请执行以下步骤在现有的Adobe Experience Manager6.5实例上安装Service Pack:

1. 如果实例处于更新模式，则在安装前重新启动该实例（在从较早版本更新该实例时，这是这种情况）。 Adobe还建议在实例的当前正常运行时间较高时重新启动。

1. 在安装之前，请对[Experience Manager]实例执行快照或新鲜备份。

1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)下载服务包。

1. 打开包管理器，然后单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。 要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择软件包，然后单击&#x200B;**[!UICONTROL 安装]**。

1. 要更新S3连接器，请在安装Service Pack后停止该实例，将现有连接器替换为安装文件夹中提供的新二进制文件，然后重新启动该实例。 请参阅[AmazonS3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>包管理器UI上的对话框有时会在安装服务包时退出。 Adobe建议您在访问部署之前等待错误日志稳定。 请等待与卸载更新程序包相关的特定日志，然后确保安装成功。 通常，这会发生在[!DNL Safari]上，但可能间歇性地发生在任何浏览器上。

**自动安装**

在工作实例上自动安装Adobe Experience Manager6.5.7.0有两种方法：

A.当服务器联机可用时，将软件包放入`../crx-quickstart/install`文件夹。 软件包会自动安装。

B.使用包管理器](https://helpx.adobe.com/cn/experience-manager/aem-previous-versions.html)中的[ HTTP API。 使用`cmd=install&recursive=true`以安装嵌套的包。

>[!NOTE]
>
>Adobe Experience Manager6.5.7.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页(`/system/console/productinfo`)在[!UICONTROL 已安装产品]下显示更新的版本字符串`Adobe Experience Manager (6.5.7.0)`。

1. 所有OSGi捆绑包均位于OSGi控制台(使用Web控制台：`/system/console/bundles`)。]**]****[!UICONTROL **[!UICONTROL 

1. OSGi bundle `org.apache.jackrabbit.oak-core`是版本1.22.3或更高版本(使用Web控制台：`/system/console/bundles`)。

要了解经认证可与此版本一起使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

### 安装Adobe Experience Manager Forms加载项包{#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的Service Pack发布日期后一周内 [!DNL Experience Manager] 发布加载项包。

>[!NOTE]
>
>如果您未使用 AEM Forms，请跳过。Adobe Experience Manager Forms的修复通过单独的附加包提供。

1. 确保已安装Adobe Experience Manager服务包。
1. 下载操作系统[AEM Forms版本](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)中列出的相应Forms加载项包。
1. 按照[安装Forms加载项包](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中的说明安装AEM Forms加载项包。

### 在JEE上安装Adobe Experience Manager Forms{#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。Adobe Experience Manager Forms的JEE修复通过单独的安装程序提供。

有关在JEE上安装FormsExperience Manager的累积安装程序和部署后配置的信息，请参阅[发行说明](jee-patch-installer-65.md)。

### UberJar {#uber-jar}

[Maven Central存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)中提供用于Experience Manager6.5.7.0的UberJar。

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)并在项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象可在Maven Central存储库上使用，而不是AdobePublic Maven存储库(`repo.adobe.com`)。 主UberJar文件已重命名为`uber-jar-<version>.jar`。 因此，对于`dependency`标记，不存在以`apis`为值的`classifier`。

## 已弃用功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中标记为已弃用的功能列表。在将来的版本中，已标记为已弃用的功能。 通常会提供替代选项。

查看您在部署中是否使用了功能。 此外，计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | **[!UICONTROL AEM云服务选择加入]**&#x200B;屏幕已弃用。 随着AEM和目标集成在AEM 6.5中更新以支持Target Standard API(通过AdobeIMS和I/O使用身份验证)，以及AdobeLaunch在指导页面以进行分析和个性化方面的作用日益增强，选择加入向导的功能已变得无关紧要。 | 通过各自的AEM云服务配置系统连接、AdobeIMS身份验证和Adobe I/O集成。 |
| 连接器 | 针对Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR Connector已在AEM 6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 在安装Experience Manager6.5.7.0时，忽略`error.log`文件中的以下错误：

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* 如果您要将[!DNL Experience Manager]实例从6.5版升级到6.5.7.0版，则可以在`error.log`文件中视图`RRD4JReporter`异常。 重新启动实例以解决问题。

* 如果您在[!DNL Experience Manager] 6.5上安装[!DNL Experience Manager] 6.5 Service Pack 5或之前的Service Pack，则会删除资产自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果您在[!UICONTROL 文件夹元数据模式Forms编辑器]和[!UICONTROL 元数据模式Forms编辑器]中编辑和创建层叠规则时遇到问题，请与Adobe客户关怀部门联系。 已创建和保存的规则将按预期运行。

* 如果层次结构中的文件夹在[!DNL Experience Manager Assets]中重命名，且包含资产的嵌套文件夹发布到[!DNL Brand Portal]，则在[!DNL Brand Portal]中不更新该文件夹的标题，直到根文件夹再次发布。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他字段可解决此问题。

* 如果[!UICONTROL 连接的资产配置]向导在安装后返回404错误消息，请使用包管理器手动重新安装`cq-remotedam-client-ui-content`和`cq-remotedam-client-ui-components`包。

* 安装AEM 6.5.x.x时，可能会显示以下错误和警告消息：
   * “在 AEN 中使用 Target Standard API（IMS 身份验证）配置 Target 集成，然后将“体验片段”导出到 Target 时，会导致创建错误的选件类型。而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证将失败。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。

## 包含{#osgi-bundles-and-content-packages-included}的OSGi捆绑包和内容包

以下文本文档列出了 AEM 6.5.7.0 中包含的 OSGi 包和内容包:

* [AEM 6.5.7.0 中包含的 OSGi 包列表](assets/6570_bundles.txt)

* [AEM 6.5.7.0 中包含的内容包列表](assets/6570_packages.txt)

## 受限网站{#restricted-sites}

这些网站仅面向客户。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅[如何联系客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5发行说明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 产品页面](https://www.adobe.com/cn/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* 订阅[Adobe优先级产品更新](https://www.adobe.com/subscription/priority-product-update.html)

