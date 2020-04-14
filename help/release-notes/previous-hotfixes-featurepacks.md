---
title: AEM 6.5先前的Service Pack发行说明
description: 特定于Adobe Experience Manager 6.5 Service Pack 3及更早版本的发行说明。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 以前 Service Pack 中包含的修补程序和功能包 {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.3.0

[!DNL Adobe Experience Manager] 6.5.3.0是一个重要版本，其中包括自2019年4月6.5版本正式发布以来发布的性能、稳定性、安全性以及重要客户修复和增强 **功能**。 它可安装在 [!DNL Adobe Experience Manager] 6.5之上。

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.6。

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档。

* DAM列表视图中和列表视图中的资产搜索结果中都添加了可排序的创建日期的新列。

* 已在列表视图中启用基于名称列的资产排序。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资源。 Smart Crop是一项机器学习驱动的功能，它可在移动帧以跟随场景焦点的同时重新裁剪视频。

* [!DNL Dynamic Media] 支持智能成像。

* 能够 [在工作流中设置](../forms/using/configure-out-of-office-settings.md) “出局”首 [!DNL Experience Manager] 选项。

* 能够与 [工作流中的其他用户共享收件箱](../forms/using/configure-shared-queues-osgi.md) 或收件箱项 [!DNL Experience Manager] 目。

* 能在“ [批处理”模式下生成交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* 捆绑在ContextHub中的jQuery的更新版本为3.4.1。

### 资产 {#assets-6530-enhancements}

**产品增强功能**

* [!DNL Experience Manager Assets] 现在支持使用Deflate64算法创建的ZIP存档(NPR-27573)。

* 在DAM列表视图中和列表视图中的资产搜索结果中添加了可排序的创建日期的新列(NPR-31312)。

* 已允许在列表视图中基于名称列的资产排序(NPR-31299)。

* GLB、GLTF、OBJ和STL资源文件支持在DAM的“资产详细信息”页面中预览资产(CQ-4282277)。

* 在(CQ-4281279)中的块上传期间，会为块节 [!DNL Dynamic Media] 点触发ReplicationOnModifyListener事件。

* [!DNL Dynamic Media] 现在支持智能裁剪视频资源。 Smart Crop是一项机器学习驱动的功能，它可在移动帧时重新裁剪视频以跟随场景的焦点(CQ-4278995)。

* [!DNL Dynamic Media] 支持智能成像(CQ-422249)。

* 如果在请求中传递了视图参数，则搜索／浏览视图在Foundation选取器中已设置为默认查询(NPR-31601)。

**修复**

* 某些PDF文档的元数据在修改其标题时不会更新并保存到PDF中(NPR-31629)。

* 对于名称中带有加号“+”的资产，资产共享不起作用(NPR-31547)。

* 在默认搜索表单“资产管理员”*“搜索边栏”中进行的编辑不按预期工作(NPR-31502)。

* 在使用Omnisearch搜索资产视图搜索资产时，不显示建议(NPR-31496)。

* 当引用的资产被移到其他位置时，集合中的资产引用不会更新，因为不同用户引用的不同集合也会引用相同的资产(NPR-31486)。

* 重复IPTC标记添加到资产元数据(NPR-31328)。

* 当从过滤边栏触发搜索时，右上角的搜索结果计数不会准确更新(NPR-31316)。

* 取消选择“文件类型”过滤器中的第二级复选框时，将清除所有复选框，搜索栏中的文本与选定／未选定的属性(NPR-31287)不同步。

* 不能从文件夹的“成员”部分删除所有成员（用户／用户组）;在尝试删除所有用户时，登录用户会添加到列表(NPR-31171)。

* 无法删除文件名中带有加号“+”的资源(NPR-31162)。

* 创建下拉菜单（在选择文件夹时显示在顶部菜单中）不显示“文件夹”作为创建选项(NPR-30877)。

* 当对用户应用拒绝jcr:removeChildNodes和路径上的jcr:removeNode的ACL时，文件夹选择“创建”>“文件上传”操作项丢失(NPR-30840)。

* 当上传某些mp4资源时，DAM工作流会进入陈旧状态，导致所有剩余工作流进入陈旧状态(NPR-30662)。

* 当将大型PDF文件（几GB）上传到DAM并处理其子资源时，会出现内存不足错误(NPR-30614)。

* 资产的批量移动失败并显示警告消息(NPR-30610)。

* 在 [!DNL Experience Manager][!DNL Dynamic Media]-Scene7模式中运行时，将资产从一个文件夹移到另一个文件夹时，资产名称会更改为小写字母(NPR-31630)。

* 编辑远程图像集时，对于与Scene 7公司名称相同的文件夹中的图像，会出现错误(NPR-31340)。

* [!DNL Dynamic Media] 包含引用的资源不会被发布(NPR-31180)。

* 从 [!DNL Dynamic Media]7-Scene7模式上载到Scene7的 [!DNL Dynamic Media Classic] 过程过长，无法完成(NPR-31048)。

* 添加到图像资产的热点不会通过“资产详细信息”页面中的交互式图像查看器显示(NPR-30979)。

* 当对中的资源执行的操作被传递到Scene 7时，将创建大量Sling作业并重 [!DNL Experience manager Assets] 新显示“处理”横幅(NPR-30947)。

* 在创建资产的语言副本时发生冲突，并且资产未上传到Scene 7(NPR-30932)。

* 从以混合模 [!DNL Experience Manager] 式运行的 [!DNL Dynamic Media]Dynamic Renditions被破坏（它们属于文本类型，内容为“找不到图像”而非图像内容类型）(NPR-30876)。

* [!DNL Dynamic Media] 编码视频工作流无法为从Adobe Experience Manager上的 [!DNL Dynamic Media Classic] - [!DNL Dynamic Media]Scene7模式迁移到的视频生成缩略图(CQ-4282011)。

* 使用不同的Scene7公司ID(CQ-4280548)将资源从一个实例迁移到另一个实例时观察到IpsApiException。

* 当将支持的3D模型引入(CQ-4283701)中时，3D资产缩略图 [!DNL Experience Manager] 不会提供相关信息。

* 如果3D资产的相机视图很少，则查看器中会显示滚动按钮(CQ-4283322)。

* 在“资产详细信息”页面的DimensionalViewer中预览的已上载3D模型的容器高度不正确(CQ-4283309)。

* 在Internet Explorer 11和Safari上，无法使用SmartCropVideoViewer播放视频(CQ-4281422)。

* 在 [!DNL Experience Manager][!DNL Dynamic Media]Scene7运行模式上运行时，使用移动按钮将多个资产从一个文件夹移动到另一个文件夹失败(CQ-4280384)。

* 当MIME类型不是MP4时，资产详细信息上会出现扭曲的视频(CQ-4279704)。

* 新摄取到具有视频用户档案的文件夹中的视频即使在编码百分比完成到100%后仍处于处理状态(CQ-4279389)。

* 从文件夹移动资源会创建大量sling作业（Scene 7 API调用），而不是理想的必需(CQ-4278664)。

* 在Scene 7中，当创建图像集（或mediaset）并在DAM中使用适当的命名约定进行命名时，图像集的名称将更改为小写字母(CQ-4281112)。

* Scene 7 Migrator设置发布状态的错误(CQ-4263492)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失内容片段中用户的滚动位置(CQ-4282898)。

* PDF文件没有索引，内容也无法搜索(CQ-4278916)。

* 错误“用户选取器未列出组：expected false to equal true”（预期false为true）时，添加具有不同和 `principalName` 的已关闭 `authorizableId` 用户组时会观察到(CQ-4278177)。

* 资产UI列视图显示所有路径，而不管特定租户的dam根路径如何(CQ-4278175)。

* 资产选择器的搜索未按预期工作(CQ-4275886)。

* 再现工作流失败(CQ-4271928)。

* DAM事件清除功能会删除最新的(maxSavedActivities)事件数据并保存之前创建的数据(NPR-31336)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在触屏UI中选择全部，然后取消选择某些项目（文件夹／单个资产）时，操作栏和资产计数不会更新(NPR-31118)。

* 轮询资产的作 [!DNL Experience Manager] 业详细信息时，会在中显示一个例外(CQ-4283569)。

### 站点 {#sites}

* 如果LiveCopy继承被破坏，Live Copy页面将显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数大于40，则仅显示前40条记录。 Blueprint显示其余记录的空行(NPR-31182)。
* 当用户在菜单的描述属性中添加日语或韩语字符时，该菜单显示日语和韩语文本的扭曲字符。 (NPR-31331).
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)。 意外地将内联字体大小应用于元素(NPR-31284)。
* 当用户将焦点放在左边栏字段上并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径存储在组件节点而不是多字段节点中(NPR-30882)。
* ResponsiveGridExporter API不返回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter接口。 com.day.cq.wcm.foundation.model.impl包声明为私有包(NPR-31398)。
* 当在非编辑器模式下(在“作者”模式下(不带前缀和 `editor.html``wcmmode=disabled`，或在“发布者”中)打开包含某些ExperienceFragments的页面时，请求以HTTP状态错误代码500(NPR-30743)结束。
* 用户无法更改其密码并访问其用户档案页面(NPR-31161)。

### 搜索和用户界面 {#search-ui-interface}

* 在搜索结果页面上从卡视图切换到列表视图时，在可滚动页面之前会有延迟(NPR-31286)。

* “全选”复选框隐藏在 [!DNL Sites] UI上的列表视图中(NPR-31614)。

* 搜索结果页上的“全选”计数不正确(NPR-31120)。

* 元数据编辑器显示不存在的标记(NPR-31119)。

### 翻译 {#translation}

* 在翻译作业中选择“到期日期”选项时，将显示两个日历弹出窗口(NPR-31270)。

### 平台 {#platform}

* Web控制台中的Mime类型选项不起作用(NPR-31108)。

* 配置单点登录时，客户端证书不被接受(NPR-31165)。

* 基于 Jetty 的 HTTP 服务的缓冲区大小配置中的更新未保存 (NPR-30925)。

* QueryBuilder现在支持 ``fn:name()`` xpath查询中的orderby(NPR-31322)。

* 重复激活树是在从 [!DNL Experience Manager] 6.3升级时创建的(NPR-31513)。

* 转发的请求不保留在sling身份验证过程中设置的响应头(NPR-30013)。

* 在选取器组件中搜索不起作用(NPR-31692)。

* 由于Apache POI和Apache Tika捆绑包的不同版本，将ZIP文件附加到 [!DNL Experience Manager Communities] 帖子时会显示错误(NPR-31018)。

* 捆绑 ``org.apache.sling.distribution.api`` 包隐藏在配置管理器中，因此对自定义捆绑包不可用(NPR-31720)。

### 项目 {#projects}

* 切换日历视图不起作用(NPR-31271)。

### Brand Portal {#assets-brand-portal}

**产品增强功能**

* 中的资产来源补充导入 [!DNL Experience Manager Assets][!DNL Brand Portal][!DNL Experience Manager]工作流将被修改以仅从中提取新创建的资产，并跳过NEW文件夹中已存在的资产以避免复制(CQ-4278527)。

**修复**

* 在“资产来源补充”功能中创建新的“贡献”文件夹时显示错误图标(CQ-4282825)。
* 创建新的“贡献”文件夹时，“贡献”文件夹中不显示一个或两个子文件夹（“新建”和“共享”）(CQ-4282424)。
* 如果用户在从结尾处收到Contribution文件夹中的新资产后，尝试从 [!DNL Experience Manager] Contribution文件夹重新发布到，则系统 [!DNL Brand Portal][!DNL Brand Portal] 将引发异常(CQ-4279740)。
* 禁止在“贡献”文件夹（嵌套文件夹）内创建“贡献”文件夹，以避免复杂性(CQ-4278391)。
* 上传从Admin Console导入的用 [!DNL Brand Portal] 户列表（.csv文件）时，系统会引 [!DNL Experience Manager] 发异常。 只有。csv文件中的“电子邮件”、“名字”和“姓氏”字段是必填字段(CQ-4278390)。

### 社区 {#communities}

**修复**

* 社区管理员（组管理员／站点管理员）看不到管理组（打开／编辑／发布／删除组）的快速链接(NPR-31627)。
* 除非手动刷新／重新加载页面，否则不会显示提交的博客(NPR-31599)。
* “提及次数”功能使用的JCR查询区分大小写，并且返回结果需要太长时间(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar文件引发异常， `cq-social-translation` 从 [!DNL Experience Manager] 6.5 UberJar文件中缺少捆绑包(NPR-31186)。
* Jackson Databind库已更新至版本2.9.9.3以解决新的漏洞(NPR-30967)。
* 活动和通知标题不一致 (NPR-30941)。
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Lucene索引更新导致作者服务器减速(NPR-31548)。

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含针对的修复 [!DNL Experience Manager Forms]。 它们是通过单独的 Forms 附加组件包交付的。In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. 有关详细信息，请 [参阅在JEE上安装Experience Manager Forms Add-on](#install-aem-forms-add-on-package)[和安装Experience Manager Forms](#install-aem-forms-jee-installer)。

#### Forms 附加组件包 {#forms-add-on-package-6530}

**自适应表单**

* 在本地化自适应表单时，字符串包含词典键(NPR-31110)。

**交互式通信**

* **MissingNode.toString()** 在将Jackson库升级到2.10.0(NPR-31549)后返回不准确的结果。

* 文本编辑器从从Microsoft Word复制的文本中随机删除空格字符(NPR-31113)。

**通信管理**

* 在将字母从LiveCycle ES4SP1迁移到 [!DNL Experience Manager] 6.5(NPR-31615)时，字幕和工具提示不显示。

* **将字母保存为草稿时** ，不再显示支持文本流格式的错误消息(NPR-30463)。

**工作流**

* OSGi工作流因CPU利用率为100%而失败(NPR-31233)。

**HTML5 表单**

* 在添加子表单的实例时，生成 XDP 表单的 HTML5 预览会显示闪烁 (NPR-30909)。

#### JEE安装程序上的表单 {#forms-jee-installer-6530}

**表单 - 文档服务**

* 在。NET项目中使用MTOM的SOAP Web服务显示AssemblerServiceClient调用和HtmlToPDF2方法的例外(NPR-4281771)。

**Foundation JEE**

* 操作配置不会加载调用表单工作流提交操作的进程名称(NPR-31478)。

### 包含的功能包 {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] 对Oracle 18c的表单支持(NPR-29155)。

## Adobe Experience Manager 6.5.2.0

[!DNL Adobe Experience Manager] 6.5.2.0是一个重要版本，其中包括自2019年4月推出 [!DNL Adobe Experience Manager] 6.5以来发布的性能、稳定性、安全性以及重要客户修复和增 **强功能**。 它可安装在 [!DNL Experience Manager] 6.5之上。

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.3。
* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target].
* 资产用户可以直观地搜索相似图像。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。请参阅[使用连接的资产](../assets/use-assets-across-connected-assets-instances.md)。

* 增强具有更多MIME类型的文档类型过滤器以支持多值选项。
* 引入了一个外部“重新处理”工作流以支持多种资源。
* 通过 [!DNL Dynamic Media] 使用默认的资产过滤器进行复制，优化了性能。
* 恢复了 DMS7 的裁剪/旋转资产编辑选项。
* 在 VideoPlayer 中实施了加载时使视频静音的选项。
* 修复以确保 Asset UI 列视图仅显示特定租户的内容。
* 修复以允许搜索结果中反映样式可折叠项的更改。

### 资产 {#assets}

**产品增强功能**

* 增强了“连接的资产”功能，以增加对从远程 DAM 部署中提取文档的支持。现在，站点“作者”可以在“内容查找器”中搜索和筛选受支持的文档类型。可以将远程文档添加到网页上的“下载”组件中。适用于 CQ-4270245 的修补程序. 请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Experience Manager Assets] 用户可以搜索视觉效果相似的图像。 [!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。请参阅[可视化搜索](../assets/search-assets.md#visualsearch)。

**修复**

* 通过 ACP API 生成的 URL 和文件夹元数据中的资产路径未进行 URL 编码。GRANITE-26198：适用于 CQ-4271814 的修补程序
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989：适用于 CQ-4270467 的修补程序
* 触屏UI:在管理发布向导过程中，在发布请求主体中的页面之后添加引用，导致所有资产在页面后发布，当呈现页面时，发布实例中的某些资产会丢失。 NPR-29985：适用于 CQ-4270724 的修补程序
* “取消关联资产”功能无法用于名称中包含特殊字符（成为 URI 编码的字符）的关联资产。NPR-30387：适用于 CQ-4274446 的修补程序
* 编辑内容片段时，使用错误的用户创建此版本。
* 在基于“租户”的系统上创建收藏集失败。NPR-30114：适用于 CQ-4272948 的修补程序
* Asset UI 列视图不遵循当前租户的 dam 根路径，而是访问所有租户的 dam 路径。NPR-30636：适用于 CQ-4275481 的修补程序
* 由于能够看到插入的图像，可通过受限的文件警告窗口实施跨站点脚本 (XSS) 攻击。NPR-30617：适用于 CQ-4270133 的修补程序
* 多租户：保存文件夹属性的租户会看到成功提示和错误消息，其中描述操作未成功，“无法编辑属性。 权限不足。”因此，让租户感到困惑。NPR-30545：适用于 CQ-4275333 的修补程序
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
* [!DNL Dynamic Media]:添加了默认过滤器，以排除资产被复制到发布节点 [!DNL Experience Manager] 的情况。 NPR-30538：适用于 CQ-4274678 的修补程序
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
* 3.8 SDK和5.13查看器自述文件不更新，并包含先前发行版中的信息。 适用于 CQ-4273737 的修补程序
* 即使在保存更改之前，也要对内容片段进行版本控制。NPR-30616：适用于 CQ-4273088 的修补程序
* 在缩略图进程中用 Asset#getMetadataValueFromJcr(String) 替换 Asset#getMetadata(String)。NPR-30491：适用于 CQ-4273067 的修补程序
* 上传 jpg 会导致每个资产显示消息的多个实例：“ReplicateOnModifyWorker 复制更新”，从而导致性能降低。
* 使用“提取存档”功能解压缩 zip 存档会导致标题中包含百分号 (%) 的文件夹出现问题。NPR-29990：适用于 CQ-4270467 的修补程序

### 站点 {#sites-6520}

* 如果LiveCopy继承被破坏，Live Copy页面将显示语言复制链接，而不是LiveCopy链接。 (NPR-30980)
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

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack不包含针对的修复 [!DNL Experience Manager Forms]。 They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Forms 附加组件包 {#forms-add-on-package}

**后端集成**

* 无法使用 AWS 托管的负载平衡 URL 来配置“表单数据模型”。NPR-30123：适用于 CQ-4273359 的修补程序
* 使用Web服务定义语言(WSDL)创建表单数据模型(FDM)时，将返回错 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` 误消息：NPR-30477:CQ-4272921的修补程序

**通信管理**

* “创建对应UI(CCR UI)再现间歇性地失败，控制台中出现以下错误：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**交互式通信**

* 表单数据模型中标记为必填的字段将按“创建通信 UI”(CCR UI) 中的要求显示。NPR-30623：适用于 CQ-4274902 的修补程序

**表单 - 工作流**

* “监视文件夹”中未映射的输出变量导致调用失败。适用于 CQ-4264451 的修补程序

**HTML5 表单**

* 第二次部署自定义代码或项目时，页面不会呈现，并会出现以下错误：

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

## Adobe Experience Manager 6.5.1.0 {#release-6510}

[!DNL Adobe Experience Manager] 6.5.1.0是一个重要版本，其中包括自2019年4月推出 [!DNL Adobe Experience Manager] 6.5以来发布的性能、稳定性、安全性以及重要客户修复和增强 *功能。* 它可安装在 [!DNL Experience Manager] 6.5之上。

该 Service Pack 的一些重要功能亮点包括：

* 支持在跟踪事件中包含动态 UI 状态作为自定义属性。
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### 资产

* 针对 S3 多部分支持更新了 DAM DMGateway 接口。NPR-29740：适用于 CQ-4226303 的修补程序
* 再现预览在 `Only empty tenantId is currently supported` 升级到 [!DNL Experience Manager] 6.5后会生成错误。NPR-29986:CQ-4272353的修补程序
* “删除”对话框不可见，因此不允许删除作业。NPR-29720：适用于 CQ-4271074 的修补程序
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627：适用于 CQ-4264929 的修补程序
* VersioningTimelineEventProvider 应该提供 root 版本以及 nt：version 类型的节点。适用于 GRANITE-26063 的修补程序
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. 适用于 CQ-4265131 的修补程序
* 如果编辑了源，则 Live Copy 检索错误的状态。适用于 CQ-4265451 的修补程序
* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. 适用于 CQ-4271453、CQ-4268621、CQ-4257491 的修补程序
* [!DNL Experience Manager] 界面应在时间轴历史记录中显示资产当前版本的额外条目，并显示来自的最新登记注释 [!DNL Adobe Asset Link]。 适用于 CQ-4262864 的修补程序
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

* 将体 [!DNL Experience Manager] 验片段导出到 [!DNL Adobe Target]。 适用于 CQ-4265469 的修补程序
* 智能图像导出到目标的体验片段失败。 适用于 CQ-4269606 的修补程序

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

* 使用Java11时，系统控制台中不显示内存使用情况详细信息。 NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* 仅限OSGI:支持使用Forms Service创建静态PDF文件。
* 为管理员和根用户启用了对 XMLForm.exe 的权限。
* 为 Dynamics 内部部署集成启用了对 ADFS v3.0 的支持。

#### Forms 附加组件包

**后端集成**

* 获取受保护的 Web 服务定义语言 (WSDL) 失败。NPR-29944：适用于 CQ-4270777 的修补程序
* When [!DNL Experience Manager Forms]  is installed on IBM WebSphere, creating a form data model based on SOAP fails. 适用于 CQ-4251134 的修补程序
* 为 Microsoft Dynamics 内部部署集成启用了对 Active Directory 联合身份验证服务 (ADFS) v3.0 的支持。适用于 CQ-4270586 的修补程序
* 数据源的标题发生更改时，表单数据模型不显示更新的标题。适用于 CQ-4265599 的修补程序
* 如果实体或属性的名称包含连字符或空格，则表达式无法评估此类实体和属性。 适用于 CQ-4225129 的修补程序

* 当基元字符串输出中存在冒号时，会观察到错误的输出。 适用于 CQ-4260825 的修补程序

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
* 当绑定类型从“文本片段”更改为“字符串字段／变量”的“无／数据模型对象”时，代理设置不可见，因为“由代理编辑”复选框会取消选中。 适用于 CQ-4261953 的修补程序
* 在提交代理UI时，生成的Web数据json文件会存储继承取消未绑定字段的信息。 适用于 CQ-4265621 的修补程序

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

* [!DNL Experience Manager Forms] 6.5创建对应UI(CCR UI)无法打开使用 [!DNL Experience Manager Forms] 6.3创建的对应。CQ-4266392的修补程序
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
* 添加了对Office 2019的文档安全扩展支持\。 适用于 CQ-4254369、CQ-4259764 的修补程序

**表单 - 文档服务**

* “表单”字段无法转换为PDF/A-1b，且没有外观指示。 NPR-29940：适用于 CQ-4269618 的修补程序

* OSGi:无法确定呈现过程中生成的页数。 NPR-28922：适用于 CQ-4270870 的修补程序
* 支持使用中的Forms Service对静态PDF文件的支 [!DNL Experience Manager Forms OSGi]持。 NPR-28572：适用于 CQ-4270869 的修补程序
* 无法更改对 XMLForm.exe 的权限。NPR-29828、NPR-29237：适用于 Q-4267080 的修补程序
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332：适用于 CQ-4271002 的修补程序

**Forms - Foundation JEE**

* 最终部件中不可用的 pdfg_srt 会导致安装程序失败。NPR-29854：适用于 CQ-4270137 的修补程序
* LCBackupMode.sh 不起作用。NPR-29840：适用于 CQ-4269424 的修补程序
* UDP 端口引用应该从 WebSphere 的用户界面 (UI) 中删除。适用于 CQ-4264782 的修补程序

### 包含的功能包

#### 资产——已包含

* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199：适用于 CQ-4259922 的修补程序

#### 站点——包含

* 将体 [!DNL Experience Manager] 验片段导出到 [!DNL Adobe Target]。 For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). 适用于 CQ-4265469 的修补程序

#### Forms - 文档服务 -包括

* 仅限OSGi:在Output和Forms Service中添加了新属性PAGECOUNT。 NPR-28922：适用于 CQ-4270870 的修补程序
* 仅限OSGi:支持使用Forms Service创建静态PDF文件。 NPR-28572：适用于 CQ-4270869 的修补程序
* 为管理员和根用户启用了对 XMLForm.exe 的权限。NPR-29237：适用于 CQ-4267080 的修补程序

### OSGi 包和内容包

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[获取文件](assets/6_5-content-package-list.txt)
