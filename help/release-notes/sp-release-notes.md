---
title: AEM 6.5 Service Pack 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Service Pack 4。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 34f5cfc692241da4b9f5330e5abc324998fadb23

---


# Adobe Experience Manager 6.5 Service Pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | **Adobe Experience Manager 6.5** |
|---|---|
| 版本 | 6.5.4.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2020年3月5日 |
| 下载 URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), [Software Distribution（测试版）](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Adobe Experience Manager 6.5.4.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0是一个重要更新，包括自2019年4月6.5版本正式发布以来发布的新功能、关键客户请求的增强功能以及性能、稳定性、安全性 **改进**。 它可以安装在Adobe Experience Manager(AEM)6.5的顶部。

AEM 6.5.4.0中引入的一些主要功能和增强功能包括：

* AEM资产现已通过Adobe I/O控制台配置了Brand Portal。

* AEM Forms工作流 [现在提供了新的“生成可打印输出](../forms/using/aem-forms-workflow-step-reference.md) ”步骤。

* [自适应表单](../forms/using/resize-using-layout-mode.md) 、交互式通信的布局模式支持多列。

* 支持 [HTML](../forms/using/designing-form-template.md) 5表单中的富文本。

* [Experience Manager](new-features-latest-service-pack.md#accessibility-enhancements) Assets中的辅助功能增强。

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.8。

* 您现在可以将选择性内容子树同 *步到Dynamic Media - Scene7模式* ，而不是所有可在上使用的子树 `content/dam`。

* 与SOAP Web服务的表单数据模型集成现在支持元素上的选择组或属性。

* SOAP输入或输出以及复杂的数据结构现在支持动态组替换。

有关完整列表之前AEM 6.5 Service Pack中引入的功能、主要亮点和主要功能的信息，请参阅 [Adobe Experience Manager 6.5 Service Pack 4的新增功能](new-features-latest-service-pack.md)。

### 站点 {#sites-fixes}

* 当AEM站点页面的URL包含冒号(:)或百分比符号(%)，基础浏览器停止响应，CPU周期显示尖峰(NPR-32369、NPR-31918)。

* 当打开AEM站点页面进行编辑并复制组件时，粘贴操作对于某些占位符将保持不可用(NPR-32317)。

* 打开“管理发布”向导后，链接到核心组件的体验片段不会显示在发布引用的列表中(NPR-32233)。

* Touch UI中的Live Copy概述比经典UI渲染要耗时得多(NPR-32149)。

* 当服务器时间和机器时间位于不同时区时，计划发布时间在触屏UI中显示服务器时间，而在经典UI中显示机器时间(NPR-32077)。

* AEM Sites无法打开URL中带后缀的页面(NPR-32072)。

* 当用户编辑内容片段时，内容片段的已删除变体会被恢复(NPR-32062)。

* 允许用户保存内容片段，而无需在必填字段中提供任何信息(NPR-31988)。

* kernel.js和ui.js未预先编译或缓存。 这会导致在渲染页面中增加时间(NPR-31891)。

* 启用PageEventAuditListener时，提交队列的长度会增加。 它影响许多操作的性能，如批量发布、导航、批量资产移动(NPR-31890)。

* 拖动体验片段时，会观察到较长的响应时间(NPR-31878)。

* 当您在响应式网格的占位符中选择“将组件拖动到此处”选项时，将发送GET请求，并且该请求会导致HTTP 403错误(NPR-31845)。

* 在同一文件夹内移动内容时，页面移动选项被禁用(NPR-31840)。

* 在可编辑的模板结构模式下，布局容器中允许的组件列表显示错误的结果。 只有具有设计对话框的组件才会显示在布局容器中(NPR-31816)。

* 当页面对用户具有只读权限时，“打开属性”选项在sites.html中可见，但在editor.html中不可见(NPR-31770)。

* 当用户单击“创建”按钮时，页面选项不可用(NPR-31756)。

* 无法同步包含OOTB（现成）设计导入程序组件的Adobe活动中的活动(NPR-31728)。

* 当您尝试将项目符号列表更改为编号列表时，仅更改列表的前两个项目(NPR-31636)。

* 当页面被取消创作且子节点被选中时，选择对话框仍显示初始节点。 创作页面并用户单击浏览时，页面将重定向到根节点而不是创作的节点(NPR-31618)。

* “视图配置”对话框对收件箱自定义工作流功能（NPR-32503和NPR-32492）无法正常工作。

* 使用收件箱查看工作流信息时显示错误消息(CQ-4282168)。

### 资产 {#assets-6540-enhancements}

* 在资产收集页面上触发工作流的按钮被禁用(NPR-32471)。

* 在Experience Manager中使用Dynamic Media Scene7配置将资源从一个文件夹移到另一个文件夹(NPR-32440)时，将在SPS(Scene7 Publishing System)中创建一个无名称的文件夹。

* 将所有资产（使用全选，然后移动）移动到包含已发布资产的文件夹的操作会失败，并显示错误(NPR-32366)。

* 为${extension}的资产生成再现失败(NPR-32294)。

* 版本历史记录URL显示在资产属性页面的“引用者”字段下(NPR-31889)。

* 无法使用WinZip打开从DAM下载的ZIP文件(NPR-32293)。

* 打开“文件夹设置”以更改文件夹标题或缩略图图像，然后保存文件夹的原始权限(NPR-32292)。

* 计划激活的日历图标不会显示在“状态”列（DAM资产列表的经典UI中）中，该激活的资产将安排在以后的日期和时间内(NPR-32291)。

* 使用代码片断模板创建代码片断时，在代码片断创建过程中搜索集合时出错(NPR-32290)。

* 当从搜索筛选器中选择多个标记时，将触发多个搜索查询(NPR-32143)。

* 当上传文件名超过50个字符的资产时，Experience Manager资产用户界面会显示截断的文件名(NPR-32054)。

* 当选中Adobe Stock中复选框树的第2级复选框时，“筛选器”面板中的所有复选框都会被清除(NPR-31919)。

* 使用Omnisearch彩块化进行文件和文件夹搜索会出现异常(NPR-31872)。

* 即使在相应的元数据模式表单中设置了依赖关系规则时，元数据编辑器中用于强制字段选择的字段突出显示也不会被删除(NPR-31834)。

* 叶级标记的完整名称（来自标记层次结构）不显示在资产属性页面中(NPR-31820)。

* 在Safari浏览器上使用资源属性页面中的返回命令会出错(NPR-31753)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* PDF资产的资产详细信息页面不显示操作按钮，但在Dynamic Media Scene7运行模式(CQ-4286705)上运行的Experience Manager中的“到集合”和“添加演绎版”按钮除外。

* 大于2GB的资产现在可以在Dynamic Media-Scene7中上传(CQ-4286561)。

* 通过Scene7的批量上传过程处理资产需要太长时间(CQ-4286445)。

* 当用户未在Dynamic Media Client中对“集编辑器”进行任何更改时，“保存”按钮不导入“远程集”(CQ-4285690)。

* 将支持的3D模型引入AEM时，3D资产缩略图不提供信息(CQ-4283701)。

* 智能裁剪视频查看器预设的未处理状态在横幅文本上与预设名称一起显示两次(CQ-4283517)。

* 资产的详细信息页面上会观察到在3D查看器中预览的已上载3D模型的容器高度不正确(CQ-4283309)。

* 在IE 11中，Experience Manager Dynamic Media Hybrid模式(CQ-4255590)中不打开传送编辑器。

* 键盘焦点卡在Chrome和Safari浏览器的“下载”对话框的“电子邮件”下拉菜单中(NPR-32067)。

* 在尝试在AEM上添加DM云配置时，默认情况下未启用“同步所有内容”复选框(CQ-4288533)。

### 基础UI {#foundation-ui-6540}

* 使用“筛选器”面板搜索资产时，鼠标控制会切换到以前的筛选器字段，而不是停留在现有的筛选器字段中(NPR-32538)。

* 平台标记：通过在标记字段中键入内容来搜索标记会显示根边界以外的标记，而不考虑标记字段 `rootPath` 的属性(NPR-31895)。

* 平台UI:如果在文本字段中添加了无效路径，则路径浏览器会断开(NPR-31884)。

* 选择页面时，通知隐藏在粘性菜单后面(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)下划线替换URL路径部分的冒号(NPR-32231)。

### 项目 {#projects-6540}

* 即使用户具有在子文件夹中创建项目的权限，用户也看不到“创建”按钮(NPR-31832)。

### 项目翻译 {#projects-translation-6540}

* 在中激活“裁切空间”选项时，翻译项目创建会 `Apache Sling JSP Script Handler` 中断UI(NPR-32154)。

* 将任何要翻译的标记添加到翻译项目时，UI中出现错误，错误日志中出现空点异常(NPR-31896)。

### 集成 {#integrations-6540}

* 启动库URL的生成仅基 `path` 于Launch API `library_name` 中的值和值，而不基于值( `library_path` NPR-31550)。

* 处理LiveFyre相关项目时显示错误消息(FYR-12420)。

### WCM模板编辑器 {#wcm-template-editor-6540}

* 在可编辑的模板结构模式下，布局容器中允许的组件列表不显示链接按钮组件(CQ-4282099)。

### WCM Page Editor {#wcm-page-editor-6540}

* 选择叠加，然后选择响应式网格将组件拖动到此处时会出现错误(CQ-4283342)。

### Campaign Targeting {#campaign-targeting-6540}

* 目标云配置失败，错误get mbox请求失败(CQ-4279880)。

### Brand Portal {#assets-brand-portal}

* 在AEM 6.5.4上升级到Adobe I/O时，Brand Portal用户无法将贡献文件夹资产发布到AEM资产(CQDOC-15655)。

   此问题将在下一个Service Pack AEM 6.5.5中得到修复。

   对于AEM 6.5.4上的即时修复，建议下载 [修补程序](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) ，并在创作实例上安装。


* 元数据模式下拉值在资产属性中不可见(CQ-4283287)。

* 元数据子架构不显示基于资产属性中的mimetype的选项卡(CQ-4283288)。

* 取消发布元数据模式会填充错误消息，但模式会在后端删除。

* 预览图像不显示已发布的资产(CQ-4285886)。

* 用户无法发布或取消发布名称中包含单报价的资产(CQ-4272686)。

* 下载多个资产时不显示条款和条件(CQ-4281224)。

* 已解决较小的安全漏洞。

### 社区 {#communities}

* “创建成员”表单显示为空白页面(NPR-31997)。

* 用户无法视图有关作者实例的Analytics报告(NPR-30913)。

### Oak-索引和查询 {#oak-indexing-6540}

* 使用Tika分析器分析时，包含JPEG图像的MS Word和MS Excel文档无法解析，并且发现类未找到错误(NPR-31952)。

### Forms {#forms-6530}

>[!NOTE]
>
>AEM Service Pack 不包含对 AEM Forms 的修复。它们是通过单独的 Forms 附加组件包交付的。此外，还会发布一个累积安装程序，其中包含对JEE上的AEM Forms的修复。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* 通信管理：在提交到后期处理工作流后，字母会显示额外的字符(NPR-32626)。

* 通信管理：在提交到后期处理工作流后，字母显示一个下拉占位符作为文本组件(NPR-32539)。

* 通信管理：在字母模板中定义的默认值不会在预览模式下显示(NPR-32511)。

* 移动表单：在以HTML版本呈现XDP表单时，提交按钮显示为扩展大小(NPR-32514)。

* 文档服务：应用Service Pack 2后，Letters和某些其他页面的URL访问问题(NPR-32508、NPR-32509)。

* 文档服务：如果服务器上的事务处理数超过特定限制，则HTML到PDF的转换将失败，并且文件类型设置将从AEM Forms服务器中删除(NPR-32204)。

* 自适应表单：浏览器辅助工具根据WCAG2 AA级准则报告自适应表单中的故障(NPR-32312、NPR-32309、CQ-4285439)。

* 自适应表单：Chrome浏览器辅助工具报告了最佳实践失败(NPR-32310)。

* 自适应表单：配置嵌入在AEM站点页面中的自适应表单时的翻译问题(NPR-32168)。

* 工作台：使用“为PDF实用程序获取PDF属性”操作时，将显示一条错误消息(NPR-32150)。

* 文档安全：受保护的PDF文件无法脱机打开，DisableGlobalOfflineSynchronizationData选项设置为True(NPR-32078)。

* 设计人员：如果启用了标记选项，子表单边框将消失在生成的PDF输出中(NPR-32547、NPR-31983、NPR-31950)。

* 设计人员：如果表中有合并的单元格，则使用输出服务从XDP表单转换的输出PDF文件的辅助功能测试将失败(CQ-4285372)。

* 基础JEE:如果AEM Forms服务器与群集断开连接，缓存问题会阻止它重新连接到服务器(NPR-32412)。

## Install 6.5.4.0 {#install}

**设置要求**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 可在 Adobe Package Share 中下载 Service Pack，您可以通过 AEM 6.5 实例直接访问 Adobe Package Share。
* 在具有 MongoDB 和多个实例的部署中，使用包管理器在其中一个 Author 实例上安装 AEM 6.5.4.0。
* 在安装 Service Pack 之前，请确保具有 AEM 实例的快照或全新备份。
* 安装之前请重新启动该实例。虽然仅当实例仍处于更新模式时才需要这样做（实例从较早版本更新时也需这样），但如果实例运行较长时间，则建议执行此操作。

>[!CAUTION]
>
>Adobe 建议不要移除或卸载 AEM 6.5.4.0 包。

### 通过 Package Share 安装 Service Pack {#install-service-pack-via-package-share}

执行以下步骤以在现有 AEM 6.5 实例上安装 Service Pack：

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. 使用包管理器安装下载的包。

>[!NOTE]
>
>**包管理器 UI 中的对话框有时会在 AEM 6.5.4.0 的安装过程中退出**
>
>因此，建议在访问该实例之前先等待错误日志稳定下来。用户必须等待与卸载更新程序包相关的特定日志，才能确保安装成功。 这通常出现在 Safari 中，但也可能会间歇性发生在任何浏览器中。

**自动安装**

可通过两种方法将 AEM 6.5.4.0 自动安装到正在运行的实例上：

答：将包放入……*/crx-quickstart/install* folder whice the server is available online. 包会自动进行安装。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0 不支持 Bootstrap 安装。

**验证安装**

1. “产品信息”页(/system/console/productinfo)在“已安装产品”下显示更新 `Adobe Experience Manager, Version 6.5.4.0` 的版本字符串。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGI捆绑包org.apache.jackrabbit.oak-core在版本1.10.6或更高版本上(使用Web控制台：/system/console/bundles)。

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 AEM Forms，请跳过。AEM Forms 中的修复通过单独的附加包来交付。

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 如果您使用的是旧版AEM Forms兼容性包并更新到AEM 6.5.4.0，请在安装Forms Add-On包后安装最新版本的AEM Forms兼容性包。

1. 确保您已安装了 AEM Service Pack。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。JEE上的AEM Forms中的修复通过单独的安装程序提供。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Workbench 安装程序

由于它是完整安装程序，因此与补丁程序版本相比，文件大小更大。在安装新版本之前，请先卸载旧版Workbench。

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 已弃用功能 {#removed-deprecated-features}

本节列表了AEM 6.5.4.0中已标记为已弃用的特性和功能。计划在将来版本中删除的功能将设置为先弃用，然后使用替代选项。

建议客户检查是否在当前部署中使用了该功能，并计划更改其实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. 随着AEM 6.5中更新的AEM和目标集成以支持目标标准API（通过Adobe IMS和I/O使用身份验证），以及Adobe Launch在指导AEM页面进行分析和个性化方面日益重要的角色，选择加入向导在功能上已变得无关紧要。 | 通过各自的AEM云服务配置系统连接、Adobe IMS身份验证和Adobe I/O集成 |

## 已知问题 {#known-issues}

* 如果 **连接的资产配置向导在安装后返回404错误消息，请使用包管理器手动重新安装** cq-remotedam-client-ui-content **和****** cq-remotedam-client-ui-components包。
* 在安装AEM 6.5.x.x过程中，可能会显示以下错误和警告消息：
   * “在 AEN 中使用 Target Standard API（IMS 身份验证）配置 Target 集成，然后将“体验片段”导出到 Target 时，会导致创建错误的选件类型。而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * com.adobe.granite.maintenance.impl.TaskScheduler：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合功能时，Adaptive Form服务器端验证将失败。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用购物横幅查看器预览资产时，Dynamic Media 交互式图像中的热点不可见。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 AEM 6.5.4.0 中包含的 OSGi 包和内容包

AEM 6.5.4.0 中包含的 OSGi 包列表

[获取文件](assets/6540_bundles.txt)

AEM 6.5.4.0 中包含的内容包列表

[获取文件](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

这些网站仅适用于客户。如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系客户支](https://daycare.day.com/public/contact.html)持有关访问支持门户的详细信息，请参 [阅访问支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

>[!MORE 这样]
>
>* [AEM 6.5 发行说明](/help/release-notes/release-notes.md)
>* [AEM 产品页面](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 文档](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

