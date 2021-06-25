---
title: '[!DNL Experience Manager] 6.5 service pack发行说明'
description: 特定于 [!DNL Adobe Experience Manager] 6.5 service pack 9的发行说明
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: a0f47b4e0e9f38df208ed78fde63c70813fb7dcc
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 service pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本号 | 6.5.9.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2021 年 5 月 27 日 |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## [!DNL Adobe Experience Manager] 6.5.9.0中包含的内容 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0包含自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了Service Pack。

[!DNL Adobe Experience Manager] 6.5.9.0中引入的主要功能和增强功能包括：

* [!DNL Experience Manager Sites] Dynamic Media Foundation组件现在允许在使用响应式图像预设或智能裁剪时打开或关闭针对高分辨率设备的优化功能。

* 为了提高性能，将`hidden=false`条件从JCR查询移动到[!UICONTROL QueryBuilder]计算器。 要验证隐藏的谓词是否在更改后正常工作，[!DNL Experience Manager]会检查是否未显示任何隐藏的文件夹。

* 能够在[!DNL Experience Manager Sites]页面上恢复已删除的页面和树。

* 支持新用户使用邮件程序配置服务的刷新令牌刷新访问令牌。

* [支持邮件配置服务的SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) 机制。

* 支持[!DNL MongoDB]版本4.2和4.4。

* 与香港、澳门和台湾有关的名称的出现情况将根据适用于中国地区和地区的新命名惯例进行更新。

* [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590)和[[!DNL Dynamic Media]](#accessibility-dm-6590)中的辅助功能增强功能。

* 智能成像DPR（设备像素比）和网络带宽优化让您能够高效地交付最佳质量的图像；在具有高分辨率显示器和网络带宽受限的设备上。 有关详细信息和时间轴，请参阅[智能成像常见问题解答](/help/assets/imaging-faq.md)。

* [!DNL Dynamic Media] 交付(`fmt` URL修饰符)支持下一代图像格式AVIF（AV1图像格式）。有关更多详细信息和时间轴，请参阅[图像提供和渲染API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)。

* 能够使用[!UICONTROL 分配任务]工作流步骤向组发送通知电子邮件。

* 能够在修改源交互式通信后检索交互式通信草稿。

* 在[!DNL Experience Manager Forms]中设置自定义域名，用于加载、渲染和验证reCAPTCHA服务。

* 增强了[!UICONTROL 调用表单数据模型服务]工作流步骤的输入数据。

* 能够在[!DNL Experience Manager Forms]的记录文档模板中使用多个主控页面。

* [!DNL Experience Manager Forms]的记录文档中的支持分页符。

* 内置存储库(Apache Jackrabbit Oak)已更新至1.22.7。

有关[!DNL Experience Manager] 6.5.9.0中引入的功能和增强功能的完整列表，请参阅 [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md)中的[新增功能。

>[!NOTE]
>
>从Service Pack 9开始，[!DNL Experience Manager]客户可以开发和运行其[!DNL Experience Manager]应用程序，其中分发了[!DNL Azul Zulu]版本的OpenJDK，该版本符合Java SE的标准。
>[!DNL Azul Zulu] JDK的支持也通过Adobe提供给[!DNL Experience Manager]客户。
>您可以从[Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载[!DNL Azul Zulu] JDK的相关版本。
>由Oracle分发的AdobeJava技术的使用权限将在2022年12月底之前过期。 [!DNL Experience Manager] 我们鼓励客户在此日期之前规划并实 [!DNL Azul Zulu] 施对JDK的使用。有关[!DNL Oracle Java]技术和[!DNL Azul Zulu]技术使用的更多信息，请参阅相关的[常见问题解答](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en)。

以下是[!DNL Experience Manager] 6.5.9.0版中提供的修复列表。

### [!DNL Sites] {#sites-6590}

* 启用了“身份验证要求”属性的已发布页面不会重定向到登录页面并返回404错误消息(NPR-36354)。

* 创建超链接时，文本组件中无法使用搜索链接的选项(NPR-35849)。

* 使用`com.day.cq.wcm.commons.ReferenceSearch` API时会触发遍历查询。 它会影响[!DNL Experience Manager]服务器的性能(NPR-36407)。

* 另一个大小调整的布局容器内的嵌套布局容器显示其子组件的列数不正确，从而导致这些组件未与网格对齐(NPR-36359)。

* 外部链接检查器将有效的外部链接显示为无效链接(NPR-36289)。

* 显示引用一段时间后，引用面板开始显示错误消息(NPR-36167)。

* 移动组件时，自动创建的Parsys没有`sling:resourceType`节点(NPR-36165)。

* 在尝试同步Live Copy时（使用转出配置[!UICONTROL 在Blueprint激活时激活]和[!UICONTROL 在Blueprint激活时取消激活]），如果在Live Copy主控中删除了组件，则同步会失败并记录`NullPointerException`(NPR-36127)。

* 当用户键入标记的临时文本（系统中不存在的标记）并按Enter时，标记将显示在字段下方，但当内容片段保存并重新打开时，临时标记会消失(NPR-36132)。

* 收件箱中没有显示异步操作状态的选项(NPR-36104)。

* 恢复继承后会创建重复的组件(NPR-36000)。

* 使用`RemoteContentRenderingService`时，对`RemoteContentRendererRequestHandler.getRequest`的请求将始终包含`ComponentExporter`的根页面，但如果根模型未基于设置的遍历深度和筛选选项包含请求的页面，则不包含该页面。 请求必须始终包含请求的页面，以便SPA具有足够的信息来渲染响应(NPR-35961)。

* onTime/offTime项目不会在预期的onTime/offTime上激活/取消激活(NPR-35936)。

* 发布包含没有`cq:lastModified`属性的体验片段的页面时，会出现`NullPointerException`(NPR-35914)。

* 尝试在容器中调整组件大小时，无法重新调整到原始大小。 减小组件容器大小时，无法将大小重新设置为原始容器(NPR-35809)。

* 在转出对话框中（在编辑器中触发或从Live Copy概述中触发），“已分离”、“已暂停”或“未创建”页面的状态图标错误(NPR-35691)。

* 主控忽略转出页面和子页面的多站点管理器转出页面属性复选框(NPR-35634)。

* 触屏UI中缺少经典UI中可用的恢复树功能(CQ-4315352、CQ-4309415)。

* [!DNL Experience Manager Sites]页面上的还原继承和转出页面时出现问题(NPR-36033)。

### [!DNL Assets] {#assets-6590}

在[!DNL Assets]中完成了以下用户体验增强：

* 要查看未基于[!UICONTROL 创建]、[!UICONTROL 修改]或[!UICONTROL 名称]参数进行排序的资产，[!DNL Adobe Experience Manager]在[!UICONTROL 排序]选项中提供了[!UICONTROL 无]选项。 [!UICONTROL 无]选项可确保“资产”用户界面（在卡片视图、列视图和分析视图中）中的资产与JCR节点中资产的顺序相同(NPR-36356)。

* 要在[!DNL Adobe Experience Manager]的ACP API响应中将电子邮件ID设为小写，可引入可选设置；由于[!DNL Adobe Asset Link]用户的ID没有全部使用小写字符，因此无法签入资产。 请注意，[!DNL Adobe Asset Link]面板使用来自[!DNL Adobe Experience Manager]的ACP API响应(CQ-4317704)。

[!DNL Adobe Experience Manager] 6.5.9.0提供了以 [!DNL Assets] 下辅助功能增强。

对以下文本和图标的对比度（与背景）进行了改进，以便视力和颜色感知受限的用户能够理解：

* [!UICONTROL 属性]页面上的资产标题(NPR-35967)。
* [!UICONTROL 评级]部分中各个位置的星级评级图标(NPR-36009)。
* 资产和文件夹卡片视图上的文本(NPR-35966)。
* [!UICONTROL 时间轴]视图上的占位符文本(NPR-35965)。
* 资产搜索结果上的资产名称(NPR-35964)。
* [!UICONTROL 链接共享]对话框上的占位符文本(NPR-35963)。
* [!UICONTROL 查看设置对话框]的列 [!UICONTROL 表选项中的元数]据  、状态    和其他文本(NPR-35910)。
*  位置和 [!UICONTROL 类型] 以在全局搜索中搜索占位符文本(NPR-35909)。
* 展开和折叠[!UICONTROL 内容树]下的图标(NPR-35908)。
* 显示资产文件夹的页面上的[!UICONTROL Assets]文本(NPR-35905)。
* 资产详细信息页面中[!UICONTROL 资产元数据]、[!UICONTROL [!UICONTROL 概述]选项内的使用情况统计信息]中的文本(NPR-35904)。
* 资产详细信息页面中[!UICONTROL 属性]和[!UICONTROL 编辑]选项的快捷键文本(NPR-35904)。

[!DNL Adobe Experience Manager] 6.5.9.0修复 [!DNL Assets] 了以下问题。

* 未保存从[!UICONTROL 文件夹元数据架构]表单中的标记选择元素中创建的标记(NPR-36119)。

* 当使用小椭圆对资产添加注释时，该椭圆与打印版本中的注释数量重叠(NPR-36114)。

* 在列视图中，在某些情况下，上传重复的资产后，[!DNL Experience Manager]不会提示出现重复的资产冲突(NPR-36048)。

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

[!DNL Adobe Experience Manager] 6.5.9.0在中提供 [!DNL Assets] 了以下辅助功能增强 [!DNL Dynamic Media]功能。

* 在[!UICONTROL 图像集]编辑器中打开对话框以使用键盘键添加资产时：
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

Adobe Experience Manager 6.5.9.0 Assets修复了[!DNL Dynamic Media]中的以下问题：

* 当[!DNL Dynamic Media]被[默认](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config)选择性激活和禁用时，自定义查看器预设和CSS不会复制到[!DNL Dynamic Media](NPR-36232)。

* 尝试在资产详细信息页面上预览视频演绎版时，视频加载速度缓慢(CQ-4320122)。

* 在启用了重复资产检测器的情况下上传200多个资产时，浏览器页面无响应且速度会减慢(CQ-4319633)。

* 在页面的全景媒体组件中添加全景图像资产时，将记录“未捕获引用”错误(CQ-4317666)。

* 使用体验片段实施交互式媒体查看器时，不会从发布者中打开体验片段，并记录错误(CQ-4317655)。

* [!UICONTROL 在“属性”] 页面的快速发布 [!UICONTROL 中，] “发布到  动态媒体”选项不可用(CQ-4317199)。

* 具有只读权限的网站作者可以在资产上使用智能裁剪功能，并编辑智能裁剪演绎版(CQ-4316450)。

* 即使在[!DNL Dynamic Media]模式下设置了[!DNL Experience Manager]实例(CQ-4314950)，视频注释对未启用[!DNL Dynamic Media]配置的文件夹路径也不起作用。

* 当资产标题具有双字节、多字节、高ASCII、西里尔文、代理对、希伯来语、阿拉伯语和GB18030字符时，资产标题将带有问号(?) (CQ-4311872).

### 平台 {#platform-6590}

* 在为Blueprint生成缩略图并将更改转出到Live Copy时，某些字段的继承不起作用(CQ-4319517)。

* 创建文件夹时，选择可排序属性，并向文件夹添加20多个资产，选择文件夹中的所有资产会显示错误计数(CQ-4316243)。

* 刷新页面时，对文件夹或资产进行排序，不会显示相应的结果(CQ-4316200)。

* Handlebars JavaScript库已升级到v4.7.7(NPR-36375)。

* 使用包管理器安装新代码包时，自定义包不会更新(NPR-35949)。

* `resourceresolver` Sling包导致`Sling:alias`查询失败(NPR-35335)。

* 在Experience Manager中设置SSL时，上下文路径将被删除(NPR-35294)。

* 长时间运行的会话后，会返回`SegmentNotFound`异常(NPR-36405)。

### 集成 {#integrations-6590}

* 无法保存为Cloud Services体验片段启用继承的页面属性(NPR-36107)。

* IMS用户界面分页和延迟加载不显示相应结果(NPR-36046)。

* 创建A4T Target配置并选择报表源作为[!DNL Adobe Analytics]时，下拉列表中没有可用的启用Adobe Target的报表包(NPR-36006)。

### 项目 {#projects-6590}

* 无法保存项目的属性，因为项目的JCR路径未解析，原因是项目路径中附加了额外的正斜杠(`/`)(NPR-36191)。

### 屏幕 {#screens-6590}

* [!DNL Experience Manager Screens] 如果使用自定义的双重身份验证处理程序，则播放器无法进行身份验证(NPR-35854)。

### 商务 {#commerce-6590}

* [!UICONTROL 商务目录]向导无法在列视图中加载40个以上的项目(CQ-4318379)。

### 翻译项目 {#translation-6590}

* 将`es`翻译为`es_es`页面时，不显示更新或覆盖选项(NPR-36170)。

* 为具有人工翻译的项目选择自动批准选项后，作业状态显示为`Unknown`(NPR-35981)。

* 翻译页面时，[!DNL Experience Fragments]的引用路径不会更新到目标[!DNL Experience Fragment]引用路径(NPR-35911)。

* 在父页面和子页面中进行更改并发送父页面进行翻译时，子页面也会被错误翻译(NPR-35896)。

* 如果选定页面有多个并发翻译项目，则[!UICONTROL 转到项目]选项不会链接到最新的翻译项目(NPR-35454)。

* 将资产发布到[!DNL Dynamic Media]时， [!DNL Experience Manager]会显示一条有关未发布标记的错误消息(CQ-4315914、CQ-4315913)。

* 打开已删除的作业时，[!DNL Experience Manager]显示错误消息(CQ-4315910)。

### 工作流 {#workflow-6590}

* 对收件箱中可用的项目单击完成、委派或打开操作后，看不到完成这些操作的任何可见线索(NPR-36317)。

### [!DNL Communities] {#communities-6590}

* 在垃圾邮件过滤中，系统会占用100%的Java堆空间，从而导致Experience Manager服务器无响应(NPR-36316、NPR-36493)。
* 在论坛中，源自`SearchCommentSocialComponentListProvider`的JCR会话数据会被泄露(NPR-36235)。
* 打开特定收件箱消息会反映所有分页不正确的消息以及其他问题(NPR-35917)。

### [!DNL Brand Portal] {#brandportal-6590}

* 使用[!DNL Brand Portal]配置[!DNL Experience Manager Assets]时，会自动启用资产源功能标记(NPR-36010)。

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。
>* 现在，您可以在OSGi部署中使用[!DNL Azul Zulu]内部版本[!DNL OpenJDK]来开发和运行应用程序，[!DNL Experience Manager Forms]为。


**自适应表单**

* 生成多个翻译字典时，[!DNL Experience Manager Forms] 6.5.7.0中出现语言初始化问题(NPR-36439)。
* 在向自适应表单片段添加附件并提交表单时， [!DNL Experience Manager Forms]会显示以下错误消息(NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 当您使用人工翻译更新字典并预览自适应表单时，不会显示修改(NPR-36035)。

**交互式通信**

* 使用交互式通信打印渠道上传图像并对其进行编辑时，该图像不再可见(NPR-36518)。

* 编辑文本资产和填充占位符时，将从导航窗格中删除所有交互元素(NPR-35991)。

**工作流**

* 在JBoss上调用[!DNL Experience Manager Forms]服务的REST端点时， [!DNL Experience Manager]会显示以下错误消息(NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**后端集成**

* 将读取服务参数绑定到包含短划线的文字值时，无法保存表单数据模型(NPR-36366)。

**文档安全**

* 设置GlobalSign的认证和HSM后，[!DNL Experience Manager Forms]在向LTV添加时间戳时显示`Unsuported Algorithm`和`Invalid TSA Certificate`错误消息(NPR-36026、NPR-36025)。

**文档服务**

* 更新了[!DNL Gibson]库以与[!DNL Experience Manager Forms]集成(NPR-36211)。

**Foundation JEE**

* 在AdminUI中选择“端点管理”时， [!DNL Experience Manager Forms]会显示`endpoint registry failure`错误消息(CQ-4320249)。

有关安全更新的信息，请参阅[[!DNL Experience Manager] 安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安装 6.5.9.0 {#install}

**设置要求和更多信息**

* Experience Manager6.5.9.0需要Experience Manager6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载Service Pack。
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装Experience Manager6.5.9.0。

>[!NOTE]
>
>Adobe不建议移除或卸载[!DNL Adobe Experience Manager] 6.5.9.0包。

### 安装Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5实例上安装Service Pack，请执行以下步骤：

1. 如果实例处于更新模式，请在安装前重新启动该实例（在从早期版本更新该实例时，即为此情况）。 Adobe还建议，如果实例的当前正常运行时间较高，则应重新启动。

1. 在安装之前，请拍摄[!DNL Experience Manager]实例的快照或新备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip)下载Service Pack。

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅[Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常情况下，这会在[!DNL Safari]上发生，但是可能会间歇性地在任何浏览器上发生。

**自动安装**

在工作实例上自动安装[!DNL Experience Manager] 6.5.9.0的方法有两种：

A.当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 包会自动安装。

B.使用包管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安装嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下显示更新的版本字符串`Adobe Experience Manager (6.5.9.0)`。

1. 所有OSGi包均为OSGi控制台中的&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**(使用Web控制台：`/system/console/bundles`)。

1. OSGi包`org.apache.jackrabbit.oak-core`的版本为1.22.3或更高版本(使用Web控制台：`/system/console/bundles`)。

要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

### 安装Adobe Experience Manager Forms附加组件包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您没有使用Experience ManagerForms，请跳过。 在计划的[!DNL Experience Manager] Service Pack版本发布后一周，Experience ManagerForms中的修复将通过单独的附加组件包提供。

1. 确保您已安装Adobe Experience Manager Service Pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)中列出的相应 Forms 附加组件包。
1. 按照[安装Forms附加组件包](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中所述安装AEM Forms附加组件包。

>[!NOTE]
>
>AEM 6.5.9.0包含新版本的[AEM Forms兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)。 如果您使用的是旧版AEM Forms兼容包并更新到AEM 6.5.9.0，请在安装Forms附加组件包后安装该包的最新版本。

### 在JEE上安装Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。JEE上的Adobe Experience Manager Forms中的修复通过单独的安装程序提供。

有关在JEE上安装用于Experience ManagerForms的累积安装程序以及部署后配置的信息，请参阅[发行说明](jee-patch-installer-65.md)。

>[!NOTE]
>
>在JEE上安装用于Experience ManagerForms的累积安装程序后，安装最新的Forms附加组件包，从`crx-repository\install`文件夹中删除Forms附加组件包，然后重新启动服务器。

### UberJar {#uber-jar}

适用于Experience Manager6.5.9.0的UberJar在[Maven Central存储库](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/)中提供。

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象在Maven中央存储库中可用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为`uber-jar-<version>.jar`。 因此，没有`classifier`作为`apis`值的`dependency`标记。

## 已弃用功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中标记为已弃用的特性和功能列表。在将来的版本中，这些功能最初被标记为已弃用，后来又被删除。 通常会提供替代选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | **[!UICONTROL AEM云服务选择加入]**&#x200B;屏幕已弃用。 随着Experience Manager6.5中更新了Experience Manager和Adobe Target集成，以支持Adobe Target Standard API(通过AdobeIMS和[!DNL Adobe I/O]进行身份验证)，以及Launch在检测Experience Manager页面以进行分析和个性化方面日益发挥的作用，选择加入向导在功能上已变得无关紧要。 | 通过相应的[!DNL Experience Manager]云服务配置系统连接、AdobeIMS身份验证和[!DNL Adobe I/O]集成。 |
| 连接器 | 适用于Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR Connector已在Experience Manager6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 如果您要将[!DNL Experience Manager]实例从6.5版升级到6.5.9.0版，则可以在`error.log`文件中查看`RRD4JReporter`异常。 重新启动实例以解决问题。

* 如果您在[!DNL Experience Manager] 6.5上安装[!DNL Experience Manager] 6.5 Service Pack 5或之前的Service Pack，则会删除资产自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果层级结构中的文件夹在[!DNL Assets]中重命名，并且包含资产的嵌套文件夹发布到[!DNL Brand Portal]，则在重新发布根文件夹之前，文件夹的标题不会在[!DNL Brand Portal]中更新。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数（如SUM、MAX和MIN）时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了[!DNL Experience Manager] 6.5.9.0中包含的OSGi包和内容包：

* [Experience Manager6.5.9.0中包含的OSGi包列表](assets/6590_bundles.txt)

* [Experience Manager6.5.9.0中包含的内容包列表](assets/6590_packages.txt)

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅[如何联系Adobe客户关怀团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5发行说明](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 产品页面](https://www.adobe.com/cn/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
* [订阅 Adobe 产品更新早知道](https://www.adobe.com/subscription/priority-product-update.html)

