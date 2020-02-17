---
title: AEM 6.5 Service Pack 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Service Pack 3。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: bd0b8e1605f6d8f6cc04a4173731351df002a67d

---


# Adobe Experience Manager 6.5 Service pack发行说明 {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | **Adobe Experience Manager 6.5** |
|---|---|
| 版本 | 6.5.3.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2019年12月12日 |
| 下载 URL | [包共享](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0)，软 [件分发](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aem.html#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.3.zip) |

## Adobe Experience Manager 6.5.3.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0是一个重要版本，包括自2019年4月发布6.5版本以来发布的性能、稳定性、安全性以及重要客户修复和增强 **功能**。 它可以安装在Adobe Experience Manager(AEM)6.5的顶部。

该 Service Pack 的一些重要功能亮点包括：

* 内置存储库 (Apache Jackrabbit Oak) 已更新至版本 1.10.6。

* Experience Manager Assets现在支持使用Deflate 64算法创建的ZIP存档。

* 创建日期的新列（可排序）已添加到DAM列表视图中，并添加到列表视图中的资产搜索结果中。

* 已在列表视图中启用基于名称列的资产排序。

* Dynamic media现在支持智能裁剪视频资产。 Smart Crop是一项机器学习驱动的功能，它可在移动帧以跟随场景焦点的同时重新裁剪视频。

* Dynamic media支持智能成像。

* 在AEM工 [作流程中设置](../forms/using/configure-out-of-office-settings.md) “出局”首选项。

* 能够与AEM工 [作流中的其他用户共享收件箱](../forms/using/configure-shared-queues-osgi.md) 或收件箱项目。

* 能在“ [批处理”模式下生成交互式通信](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* 捆绑在ContextHub中的jQuery的更新版本为3.4.1。

### 更改列表 {#list-of-changes}

#### 资产 {#assets-6530-enhancements}

**产品增强功能**

* Experience Manager Assets现在支持使用Deflate 64算法创建的ZIP存档(NPR-27573)。

* 在DAM列表视图中和列表视图中的资产搜索结果中都添加了新的创建日期列（可排序）(NPR-31312)。

* 已允许在“列表”视图中基于“名称”列的资产排序(NPR-31299)。

* GLB、GLTF、OBJ和STL资源文件支持在DAM的“资产详细信息”页面中预览资产(CQ-4282277)。

* 在Dynamic Media中的区块上传期间，会为区块节点触发ReplicationOnModifyListener事件(CQ-4281279)。

* Dynamic media现在支持智能裁剪视频资产。 Smart Crop是一项机器学习驱动的功能，它可在移动帧时重新裁剪视频以跟随场景的焦点(CQ-4278995)。

* Dynamic media支持智能成像(CQ-422249)。

* 如果查询参数在请求中传递，则搜索／浏览视图已设置为Foundation选取器中的默认视图(NPR-31601)。

**修复**

* 某些PDF文档的元数据在修改其标题时不会更新并保存到PDF中(NPR-31629)。

* 对于名称中带有加号“+”的资产，资产共享不起作用(NPR-31547)。

* 在默认搜索表单“资产管理员”*“搜索边栏”中进行的编辑不按预期工作(NPR-31502)。

* 在“资产视图”中使用Omnisearch搜索搜索资产时，不会显示建议(NPR-31496)。

* 当引用的资产被移到其他位置时，集合中的资产引用不会更新，因为不同用户引用的不同集合也会引用相同的资产(NPR-31486)。

* 重复的IPTC标记会添加到资产元数据(NPR-31328)。

* 当从过滤边栏触发搜索时，右上角的搜索结果计数不会准确更新(NPR-31316)。

* 取消选择“文件类型”过滤器中的第二级复选框时，将清除所有复选框，搜索栏中的文本与选定／未选定的属性(NPR-31287)不同步。

* 不能从文件夹的“成员”部分删除所有成员（用户／用户组）;在尝试删除所有用户时，登录用户将添加到列表(NPR-31171)。

* 无法删除文件名中带有加号“+”的资源(NPR-31162)。

* 创建下拉菜单（在选择文件夹时显示在顶部菜单中）不显示“文件夹”作为创建选项(NPR-30877)。

* 当对用户应用拒绝jcr:removeChildNodes和路径上的jcr:removeNode的ACL时，文件夹选择“创建”>“文件上传”操作项丢失(NPR-30840)。

* 上传某些mp4资源时，DAM工作流将进入过时状态，导致所有剩余的工作流进入过时状态(NPR-30662)。

* 当将大型PDF文件（几GB）上传到DAM并处理其子资源时，会出现内存不足错误(NPR-30614)。

* 资产的批量移动失败并显示警告消息(NPR-30610)。

* 在Dynamic Media Scene 7运行模式上运行的AEM中，将资产从一个文件夹移到另一个文件夹时，资产名称将更改为小写字母(NPR-31630)。

* 编辑远程图像集时，对于与Scene 7公司名称相同的文件夹中的图像，会出现错误(NPR-31340)。

* 包含引用的Dynamic media资产将不会被发布(NPR-31180)。

* 从AEM Dynamic Media上传- Scene 7运行模式到Scene 7的过长时间无法完成(NPR-31048)。

* 添加到图像资产的热点不会通过“资产详细信息”页面中的交互式图像查看器显示(NPR-30979)。

* 当对AEM资产中的资产执行的操作传递到Scene 7时，将创建巨大的Sling作业并重新显示处理横幅(NPR-30947)。

* 在创建资产的语言副本时发生冲突，并且资产未上传到Scene 7(NPR-30932)。

* 从运行在Dynamic Media Hybrid模式上的AEM下载的动态演绎版将断开（它们属于文本类型，内容为“找不到图像”而非图像内容类型）(NPR-30876)。

* Dynamic Media编码视频工作流无法为从Scene 7迁移到Dynamic Media - Scene 7运行模式的视频生成缩略图(CQ-4282011)。

* 使用不同的Scene 7公司ID(CQ-4280548)将资源从一个实例迁移到另一个实例时观察到IpsApiException。

* 当支持的3D模型被收录到AEM中时，3D资产缩略图不会提供相关信息(CQ-4283701)。

* 如果3D资产的相机视图很少，则查看器中会显示滚动按钮(CQ-4283322)。

* 在“资产详细信息”页面的DimensionalViewer中预览的已上载3D模型的容器高度不正确(CQ-4283309)。

* 在Internet Explorer 11和Safari上，无法使用SmartCropVideoViewer播放视频(CQ-4281422)。

* 使用移动按钮将多个资产从一个文件夹移动到另一个文件夹时，在Dynamic Media上运行的AEM中失败- scene7运行模式(CQ-4280384)。

* 当MIME类型不是MP4时，资产详细信息上会出现扭曲的视频(CQ-4279704)。

* 新摄取到具有视频配置文件的文件夹中的视频即使在编码百分比完成到100%后仍处于处理状态(CQ-4279389)。

* 从文件夹移动资源会创建大量sling作业（Scene 7 API调用），而不是理想的必需(CQ-4278664)。

* 在Scene 7中，当创建图像集（或mediaset）并在DAM中使用适当的命名约定进行命名时，图像集的名称将更改为小写字母(CQ-4281112)。

* Scene 7 Migrator设置发布状态的错误(CQ-4263492)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失内容片段中用户的滚动位置(CQ-4282898)。

* PDF文件没有索引，内容也无法搜索(CQ-4278916)。

* 错误“用户选取器未列出组：expected false to equal true”（预期false为true）时，添加具有不同和 `principalName` 的已关闭 `authorizableId` 用户组时会观察到(CQ-4278177)。

* 资产UI列视图显示所有路径，而不管特定租户的dam根路径如何(CQ-4278175)。

* 资产选择器的搜索未按预期工作(CQ-4275886)。

* 再现工作流失败(CQ-4271928)。

* DAM事件清除将删除最新(maxSavedActivities)事件数据并保存先前创建的数据(NPR-31336)。

* 触屏UI搜索（通过Omnisearch完成）结果页面会自动向上滚动并丢失用户的滚动位置(NPR-31307)。

* 在触屏UI中选择全部，然后取消选择某些项目（文件夹／单个资产）时，操作栏和资产计数不会更新(NPR-31118)。

* 在轮询资产的作业详细信息时，AEM中会显示一个例外(CQ-4283569)。

#### 站点 {#sites}

* 如果LiveCopy继承被破坏，Live copy页面将显示语言复制链接，而不是LiveCopy链接(NPR-30980)。
* 对于新的Blueprint，如果记录数大于40，则仅显示前40条记录。 Blueprint显示其余记录的空行(NPR-31182)。
* 当用户在菜单的描述属性中添加日语或韩语字符时，该菜单显示日语和韩语文本的扭曲字符。 (NPR-31331).
* 富文本编辑器(RTE)不允许将嵌入的表作为列表项插入(NPR-30879)。
* 开箱即用的基架富文本编辑器(RTE)。 意外地将内联字体大小应用于元素(NPR-31284)。
* 当用户将焦点放在左边栏字段上并使用键盘快捷键粘贴内容时，它会粘贴页面编辑器剪贴板的内容而不是从左边栏字段复制的内容(NPR-31172)。
* 当用户向多字段添加“文件上传”字段时，图像路径存储在组件节点而不是多字段节点中(NPR-30882)。
* ResponsiveGridExporter API不返回com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter接口。 com.day.cq.wcm.foundation.model.impl包声明为私有包(NPR-31398)。
* 当在非编辑器模式下(在“作者”模式下(不带前缀和 `editor.html``wcmmode=disabled`，或在“发布者”中)打开包含某些ExperienceFragments的页面时，请求以HTTP状态错误代码500(NPR-30743)结束。
* 用户无法更改其密码并访问其配置文件页面(NPR-31161)。

#### 搜索和用户界面 {#search-ui-interface}

* 从搜索结果页面的“卡片”视图切换到“列表”视图时，页面滚动有一个延迟(NPR-31286)。

* “全选”复选框隐藏在站点UI的“列表”视图中(NPR-31614)。

* 搜索结果页上的“全选”计数不正确(NPR-31120)。

* 元数据编辑器显示不存在的标记(NPR-31119)。

#### 翻译 {#translation}

* 在翻译作业中选择“到期日期”选项时，将显示两个日历弹出窗口(NPR-31270)。

#### 平台 {#platform}

* Web控制台中的Mime类型选项不起作用(NPR-31108)。

* 配置单点登录时，客户端证书不被接受(NPR-31165)。

* 不保存基于Jetty的HTTP服务的缓冲区大小配置中的更新(NPR-30925)。

* QueryBuilder现在支持 ``fn:name()`` xpath查询中的orderby(NPR-31322)。

* 从AEM 6.3升级时会创建重复的激活树(NPR-31513)。

* 转发的请求不保留在sling身份验证过程中设置的响应头(NPR-30013)。

* 在选取器组件中搜索不起作用(NPR-31692)。

* 由于Apache POI和Apache Tika捆绑包的不同版本，将ZIP文件附加到AEM Communities帖子时会显示错误(NPR-31018)。

* 捆绑 ``org.apache.sling.distribution.api`` 包隐藏在配置管理器中，因此对自定义捆绑包不可用(NPR-31720)。

#### 项目 {#projects}

* 切换日历视图不起作用(NPR-31271)。

#### 品牌门户 {#assets-brand-portal}

**产品增强功能**

* 将修改AEM资产中的资产来源补充导入工作流，以仅将新创建的资产从Brand Portal提取到AEM，并跳过NEW文件夹中已存在的资产以避免复制(CQ-4278527)。

**修复**

* 在“资产来源补充”功能中创建新的“贡献”文件夹时显示错误图标(CQ-4282825)。
* 创建新的“贡献”文件夹时，“贡献”文件夹中不显示一个或两个子文件夹（“新建”和“共享”）(CQ-4282424)。
* 如果用户在从Brand Portal端接收Contribution文件夹中的新资产后尝试从AEM将Contribution文件夹重新发布到Brand Portal，则系统会引发异常(CQ-4279740)。
* 禁止在“贡献”文件夹（嵌套文件夹）内创建“贡献”文件夹，以避免复杂性(CQ-4278391)。
* 上传从AEM Admin Console导入的Brand Portal用户列表（.csv文件）时，系统会引发异常。 只有。csv文件中的“电子邮件”、“名字”和“姓氏”字段是必填字段(CQ-4278390)。

#### 社区 {#communities}

**修复**

* 社区管理员（组管理员／站点管理员）看不到管理组（打开／编辑／发布／删除组）的快速链接(NPR-31627)。
* 除非手动刷新／重新加载页面，否则不会显示提交的博客(NPR-31599)。
* “提及次数”功能使用的JCR查询区分大小写，并且返回结果需要太长时间(NPR-31475)。
* AEM 6.5 uberJar文件引发异常， `cq-social-translation` AEM 6.5 uberJar文件中缺少捆绑包(NPR-31186)。
* Jackson Databind库已更新至版本2.9.9.3以解决新的漏洞(NPR-30967)。
* 活动和通知标题不一致(NPR-30941)。
* 分页在社区博客中无法正常工作(NPR-30914)。
* 分析报告未在AEM创作环境中填充，显示空白页面(NPR-30913)。

#### Oak {#oak}

* Lucene索引更新导致作者服务器减速(NPR-31548)。

#### Forms {#forms-6530}

>[!NOTE]
>
>AEM Service Pack 不包含对 AEM Forms 的修复。它们是通过单独的 Forms 附加组件包交付的。此外，还会发布一个累积安装程序，其中包含对JEE上的AEM Forms的修复。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Forms 附加组件包 {#forms-add-on-package-6530}

**自适应表单**

* 在本地化自适应表单时，字符串包含词典键(NPR-31110)。

**交互式通信**

* **MissingNode.toString()** 在将Jackson库升级到2.10.0(NPR-31549)后返回不准确的结果。

* 文本编辑器从从Microsoft Word复制的文本中随机删除空格字符(NPR-31113)。

**通信管理**

* 在将字母从LiveCycle ES4SP1迁移到AEM 6.5(NPR-31615)时，字幕和工具提示不显示。

* **将字母保存为草稿时** ，不再显示支持文本流格式的错误消息(NPR-30463)。

**工作流**

* OSGi工作流因CPU利用率为100%而失败(NPR-31233)。

**HTML5 表单**

* 在添加子表单实例时，生成XDP表单的HTML5预览会显示闪烁(NPR-30909)。

##### JEE安装程序上的表单 {#forms-jee-installer-6530}

**Forms - 文档服务**

* 在。NET项目中使用MTOM的SOAP web服务显示AssemblerServiceClient调用和HtmlToPDF2方法的例外(NPR-4281771)。

**基础JEE**

* 操作配置不会加载调用表单工作流提交操作的进程名称(NPR-31478)。

### 包含的功能包 {#feature-packs-included-6530}

>[!NOTE]
>
>对于 AEM Forms 客户，请先安装任意 AEM Service Pack、累计修复程序或功能包之后，再安装 AEM Forms 附加组件包，这一点至关重要。

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* AEM Forms对Oracle 18c的支持(NPR-29155)。

## Install 6.5.3.0 {#install}

**设置要求**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* 可在 Adobe Package Share 中下载 Service Pack，您可以通过 AEM 6.5 实例直接访问 Adobe Package Share。
* 在具有 MongoDB 和多个实例的部署中，使用包管理器在其中一个 Author 实例上安装 AEM 6.5.3.0。
* 在安装 Service Pack 之前，请确保具有 AEM 实例的快照或全新备份。
* 安装之前请重新启动该实例。虽然仅当实例仍处于更新模式时才需要这样做（实例从较早版本更新时也需这样），但如果实例运行较长时间，则建议执行此操作。

>[!CAUTION]
>
>Adobe 建议不要移除或卸载 AEM 6.5.3.0 包。

### 通过 Package Share 安装 Service Pack {#install-service-pack-via-package-share}

执行以下步骤以在现有 AEM 6.5 实例上安装 Service Pack：

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. 使用包管理器安装下载的包。

>[!NOTE]
>
>**包管理器 UI 中的对话框有时会在 AEM 6.5.3.0 的安装过程中退出**
>
>因此，建议在访问该实例之前先等待错误日志稳定下来。用户必须等待与卸载更新程序包相关的特定日志，才能确保安装成功。 这通常出现在 Safari 中，但也可能会间歇性发生在任何浏览器中。

**自动安装**

可通过两种方法将 AEM 6.5.3.0 自动安装到正在运行的实例上：

答：将包放入……*/crx-quickstart/install* folder whice the server is available online. 包会自动进行安装。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 不支持 Bootstrap 安装。

**验证安装**

1. “产品信息”页(/system/console/productinfo)在“已安装产品”下显示更新 `Adobe Experience Manager, Version 6.5.3.0` 的版本字符串。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGI捆绑包org.apache.jackrabbit.oak-core在版本1.10.6或更高版本上(使用Web控制台：/system/console/bundles)。

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用 AEM Forms，请跳过。AEM Forms 中的修复通过单独的附加包来交付。

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 如果您使用的是旧版AEM Forms兼容性包并更新到AEM 6.5.3.0，请在安装Forms Add-On包后安装最新版本的AEM Forms兼容性包。

1. 确保您已安装了 AEM Service Pack。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。JEE上的AEM Forms中的修复通过单独的安装程序提供。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Workbench 安装程序

由于它是完整安装程序，因此与补丁程序版本相比，文件大小更大。在安装新版本之前，请先卸载旧版Workbench。

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 已弃用功能 {#removed-deprecated-features}

此部分列出了AEM 6.5.3.0中已标记为已弃用的特性和功能。计划在将来版本中删除的功能将设置为先弃用，然后使用替代选项。

建议客户检查是否在当前部署中使用了该功能或功能，并计划更改其实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. 随着AEM 6.5中更新的AEM和Target集成以支持Target Standard API（通过Adobe IMS和I/O进行身份验证），以及Adobe Launch在指导AEM页面进行分析和个性化方面日益重要的角色，选择加入向导在功能上已变得无关紧要。 | 通过各自的AEM云服务配置系统连接、Adobe IMS身份验证和Adobe I/O集成 |

## 已知问题 {#known-issues}

* 如果 **连接的资产配置向导在安装AEM 6.5.3.0后返回一条404错误消息，请使用包管理器手动重新安装** cq-remotedam-client-ui-content **和****** cq-remotedam-client-ui-components包。
* 在安装AEM 6.5.x.x过程中，可能会显示以下错误和警告消息：
   * “在 AEN 中使用 Target Standard API（IMS 身份验证）配置 Target 集成，然后将“体验片段”导出到 Target 时，会导致创建错误的选件类型。而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * com.adobe.granite.maintenance.impl.TaskScheduler：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证将失败。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用购物横幅查看器预览资产时，Dynamic Media 交互式图像中的热点不可见。

## 包含的 OSGi 包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 AEM 6.5.3.0 中包含的 OSGi 包和内容包

AEM 6.5.3.0 中包含的 OSGi 包列表

[获取文件](assets/6530_bundles.txt)

AEM 6.5.3.0 中包含的内容包列表

[获取文件](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [AEM 6.5 发行说明](/help/release-notes/release-notes.md)
* [AEM 产品页面](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 开发人员支持](https://docs.adobe.com/content/ddc/en.html)
* [AEM 6.5 文档](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe Priority Product Updates](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## 受限的网站 {#restricted-sites}

这些网站仅适用于客户。如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系客户支](https://daycare.day.com/public/contact.html)持有关访问支持门户的详细信息，请参 [阅访问支持门户](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。
