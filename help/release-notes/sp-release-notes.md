---
title: '[!DNL Experience Manager] 6.5 service pack发行说明'
description: 特定于 [!DNL Adobe Experience Manager] 6.5 service pack 8的发行说明
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
translation-type: tm+mt
source-git-commit: 024f03c04a980c544ac59e736caeaa24f7565582
workflow-type: tm+mt
source-wordcount: '3409'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 service pack发行说明  {#aem-service-pack-release-notes}

## 发行信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本号 | 6.5.8.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2021 年 3 月 11 日 |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}中包含的内容

[!DNL Adobe Experience Manager] 6.5.8.0包括自2019年4月发布6.5版以来发布的新功能、客户要求的主要增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了服务包。

[!DNL Adobe Experience Manager] 6.5.8.0中引入的主要功能和增强功能包括：

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 使用[已连接资产功能](/help/assets/use-assets-across-connected-assets-instances.md)时，您现在可以视图使用该资产的所有[!DNL Sites]页面的列表。 资产的[!UICONTROL 属性]页面中提供了对资产的这些引用。 这使管理员、营销人员和图书管理员能够对资产使用情况进行完整的视图，从而实现更好的跟踪、管理和品牌一致性。

* 删除在网页中引用的资产时，[!DNL Experience Manager] [会显示警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)。 您可以强制删除引用的资产，或者检查并修改资产[!DNL Properties]页面中显示的引用。 单击引用可打开本地和远程[!DNL Sites]页。

* 使用[!UICONTROL Name]、[!UICONTROL 上次修改日期、]和[!UICONTROL 上次转出日期]属性对可转出的Live Copy页面进行排序。

* 内置存储库(Apache Jackrabbit Oak)已更新为1.22.6。 <!-- TBD: Mention the version -->

有关[!DNL Experience Manager] 6.5.8.0中引入的功能和增强功能的完整列表，请参阅 [!DNL Adobe Experience Manager]  6.5 Service Pack 8](new-features-latest-service-pack.md)中的[新增功能。

以下是[!DNL Experience Manager] 6.5.8.0版中提供的修复程序的列表。

### [!DNL Sites] {#sites-6580}

* 将页面移动到Blueprint时，链接的目标不会更新(NPR-35724)。
* 基于Tizen的播放器无法在某些浏览器上进行身份验证。 不支持samesite=none属性(NPR-35589)的浏览器会出现此问题。
* 解锁的响应式容器不显示允许的组件(NPR-35565)。
* 当您为新添加的页面创建Live Copy时，语言主控将为每个域创建两个副本(NPR-35545)。
* 当由于`org.apache.felix.scr.impl.ComponentRegistry`计时器导致多个线程被阻止时，SCR组件注册表中的死锁。 因此，[!DNL Experience Manager]在不确定的时间内停止响应(GRANITE-33125、FELIX-6252)。
* 当您在侧边栏中搜索特定资产时，结果将包含一些未搜索的资产(NPR-35524)。
* 为Experience Manager实例启用SSL时，将删除上下文路径(NPR-35477)。
* 创建列表时，将一些文本添加为第一个元素，将一个表添加为第二个元素，并在表内添加一个列表，父列表会扭曲(NPR-35465)。
* 对连续的列表项目使用不同的插件时，会向列表项目添加额外的<br>标签(NPR-35464)。
* 在两个段落之间放置列表时，无法向列表添加表(NPR-35356)。
* 当您将AEM实例从AEM 6.3升级到AEM 6.5时，升级实例需要更长的时间才能升级到开始(NPR-35323)。
* 复制包含括号()的AEM资产时。 在名称中，复制失败(GRANITE-27004、NPR-35315)。
* 将标题添加到富文本编辑器时，将禁用段落按钮(NPR-35256)。
* 将项目添加到现有列表时，将删除后续的可折叠或切换列表(NPR-35206)。
* 选择“转出页面”选项后，将显示一个包含所有可用Live Copy的对话框，并执行自动转出。 页面的Live Copy将转出到所有地理位置，而无需用户操作(NPR-35138)。
* 使用包含子项选项时，“管理发布”选项不会列表所有页面。 仅列出22页(NPR-35086)。
* 编辑策略时，文本组件不保留策略更改(NPR-35070)。
* 在编号列表中缩进某些项目时，所有项目的编号都保持相同，但对于具有相同缩进的项目，编号应从1开始(CQ-4313011)。
* 启用微型化后，您无法编辑任何页面或组件。 在安装AEM 6.5 Service Pack 7(CQ-4311133)后，问题开始出现。
* Omni搜索和资产过滤器返回不相关或没有结果(CQ-4312322、NPR-35793)。
* 当多个页面同时访问客户端库时，HTML库管理器无法加载客户端库。 它导致页面呈现不正确(NPR-35538)。
* 在[!DNL Experience Manager](NPR-35294)中设置SSL时，上下文路径会自动删除。
* 在单击“注销”选项(NPR-35160)后，包管理器不会注销用户。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0修复 [!DNL Assets] 了以下问题并提供以下增强。

* 恢复资产的先前版本后，事件DamEvent.Type RESTORED不会在OSGi控制台中触发(NPR-35789)。
* `IndexWriter.merge` 导 `OutOfMemoryError` 致错误，因为智能标记功 `/oak:index/lucene` 能 `/oak:index/ntBaseLucene` 会创建大索引(NPR-35651)。
* 当尝试保存名称(NPR-35605)中带多字节字符的[!UICONTROL 资产贡献]类型文件夹时，会显示一条错误消息。
* 当使用级联元数据子类型字段时，会出现错误的“请填写此字段”错误(NPR-35643)。
* 当将现有资产拖动到[!DNL Assets]用户界面并创建新版本时，元数据中的更改将不是永久的(NPR-34940)。
* 在级联菜单的元数据模式编辑器中创建规则时，[!UICONTROL 依赖于]选项重复相同的名称(NPR-35596)。
* 在编辑[!UICONTROL 资产管理搜索边栏](NPR-35588)后，相似性搜索不起作用。
* 在文件夹中，如果通过单击[!UICONTROL 过滤器]在左边栏中打开资产搜索，则[!UICONTROL 状态]>>[!UICONTROL 结帐]>[!UICONTROL 结帐]中的过滤器不工作(NPR-35530)。
* 如果您尝试删除资产的所有智能标记并保存更改，则不会删除这些标记。 但是，用户界面指示已保存更改(NPR-35519)。
* 用户无法在可排序的文件夹(NPR-35516)中重新排列列表视图中的资源或对其排序。
* 如果您编辑默认的元数据模式，资产[!UICONTROL 属性]页面中的标记字段将变为文本字段。 此更改允许不知情的用户添加点播标签，并且这些标签作为字符串存储在存储库中(NPR-35478)。
* 下载资产时，如果您提供的名称没有有效的电子邮件地址，则下载选项不可用。 但是，如果在下载对话框中选择了其他选项，则会启用按钮，但不会发送电子邮件(NPR-35365)。
* 用户在编辑[!DNL Adobe InDesign]中的资产后无法签入资产，并收到有关缺少权限的错误(NPR-35341)。
* Handlebars JavaScript库已升级到v4.7.6(NPR-35333)。
* 当您从批量元数据编辑和取消选择项目进行开始，直到选择单个项目(NPR-35144)时，元数据编辑器界面将停止按预期工作。
* 当从`assets.html`页面(CQ-4312311)中单击时，全局导航无法打开正确的控制台。
* [!DNL Assets] 不显示具有RGB再现(CQ-4310190)的资产的RGB再现。
* 菜单中的[!UICONTROL “关联]”选项未在[!UICONTROL 属性]页(CQ-4310188)中正确显示。
* 如果使用文档的文件类型过滤器搜索资产并创建智能收藏集，则在访问收藏集时不会应用该过滤器。 而是会在搜索中显示所有类型的资产(NPR-35759)。
* 您不能从[!DNL Assets]用户界面(NPR-35901)在Lightbox中拖放和添加资产。
* 在解决命名冲突后创建现有资产的新版本时，将覆盖原始资产的元数据(CQ-4313594)。
* 当您使用搜索筛选器或谓词筛选资产搜索时，打开资产以进行视图或编辑，然后返回到搜索结果页面，该筛选器将不起作用。 所有搜索的资源都将未过滤列出(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* 资产详细信息页面上启用了RESS图像预设的URL选项。 现在，在动态演绎版部分选择RESS图像预设后，资产详细信息页面上的URL和RESS选项均可用。 (CQ-4311241)
* 交互式媒体组件 — 如果用户具有具有选择性发布配置(CQ-4311054)的[!DNL Experience Manager]，则交互式视频将不起作用。
* 如果跨文件夹移动资产，则通过API在[!DNL Experience Manager]和[!DNL Dynamic Media–Scene7]之间的同步非常缓慢(CQ-4310001)。
* 使用Omnisearch时，日志的大小会显着增加(CQ-4309153)。
* 启用选择性同步后，资产将复制（未移动）到同步文件夹中时，它不会按预期同步(CQ-4307122)。
* 对于自动发布到DM的已上传资产，状态不会显示已发布到AEM。 此外，Dynamic Media发布状态列不显示正确的发布状态(CQ-4306415)。
* 如果资产发布在[!DNL Experience Manager]上，并设置为在激活上发布到[!DNL Dynamic Media]，则`scene7FileStatus`元数据值不会按预期方式更新(CQ-4308269)。
* 编辑视频用户档案时，[!DNL Experience Manager]不显示为视频预设设置的高度和比特率值。 这些字段显示为空(CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* 无法在Commerce(CQ-4310682)中为所有产品创建自定义标记。

* 产品资产引用更新导致复制线程处于等待状态，直到ProductAssetListener线程完成对JCR的提交(NPR-35269)。

### 平台 {#platform-6580}

* 当您使用没有标签的Coral Tab视图组件并触发Foundation验证程序时，会出现以下错误(NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 对于名称中包含逗号(NPR-35191)的节点，SCD转发复制失败。

* 升级到AEM 6.5.7后，构建开始失败。 原因是，uber-jar中嵌入了旧版本或没有jackson-core(GRANITE-33006)。

### 用户界面 {#ui-6580}

* 当您从“资产”控制台中的文件夹中的文档从卡视图切换到列表视图时，排序不会正常工作(NPR-35842)。

* 当您在文本组件中超链接文本时，搜索功能不显示适当的结果(NPR-35849)。

* 当未向标记为必填的隐藏字段提供值时，它会阻止您保存组件(NPR-35219)。

### 集成 {#integrations-6580}

* 对IMS租户ID和目标客户端代码使用不同的值时，[!DNL Experience Manager]无法与[!DNL Adobe Target](NPR-35342)集成。

### 翻译项目{#translation-6580}

* 在[!DNL Experience Manager](NPR-35259)中导出或导入翻译作业时的问题。

### 营销活动 {#campaign-6580}

* 当您在触屏UI中使用现成模板创建活动页面并打开页面属性对话框中的“电子邮件”选项卡时，主题和正文字段的个性化变量仍处于禁用状态(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* 在将页面结构添加到社区组时，痕迹导航中的[!UICONTROL Group]标题将更改为第一个[!UICONTROL Page]的标题(NPR-35803)。
* 与版主不同，标准社区成员无法访问和编辑任何帖子草稿(NPR-35339)。
* `DSRPReindexServlet`的访问控制和拒绝服务中断，导致社区站点瘫痪，直到索引完成(NPR-35591)。
* 从[!UICONTROL Administrators]字段删除[!UICONTROL All Users]并不实际从后端删除它们(NPR-35592、NPR-35611)。
* 当输入的文本为部分匹配时，[!UICONTROL 合成消息]组件不返回任何结果(NPR-35666)。

* 在尝试向新博客添加标记时，选择&#x200B;**[!UICONTROL 添加标记]**&#x200B;可能会注意到一些性能影响和速度变慢。 要提高性能，请安装[cqTagLucene-0.0.1.zip修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)。

### [!DNL Brand Portal] {#brandportal-6580}

* 将成员添加到[!UICONTROL 资产贡献]类型文件夹会在用户界面中显示[!UICONTROL 添加用户或组]题注，但只支持Brand Portal活动用户，不支持组(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。

**自适应表单**

* 当您将具有可重复行的表插入到在自适应表单中具有多个实例的可重复面板时，该表始终会添加到该面板的第一个实例(NPR-35635)。

* 在自适应表单中成功验证一次后，当制表符焦点再次到达CAPTCHA组件时，[!DNL Experience Manager Forms]将显示`Provide Captcha phrase to proceed`错误消息(NPR-35539)。

**交互式通信**

* 当您提交已翻译的表单时，提交的消息将以英语显示，但不会翻译为相应的语言(NPR-35808)。

* 当您在附加的XDP或文档片段中包含隐藏条件时，交互通信无法加载(NPR-35745)。

**通信管理**

* 编辑字母时，具有条件的模块加载时间较长(NPR-35325)。

* 当您从左侧导航窗格中选择一个未包含在字母中的资产，然后选择下一个资产时，不会从之前选择的资产中删除蓝色突出显示(NPR-35851)。

* 编辑字母中的文本字段时，[!DNL Experience Manager Forms]会显示`Text Edit Failed`错误消息(CQ-4313770)。

**工作流**

* 当您尝试在iOS的[!DNL Experience Manager Forms]移动应用程序上打开自适应表单时，应用程序会停止响应(CQ-4314825)。

* HTML工作区中的[!UICONTROL To-do]选项卡显示HTML字符(NPR-35298)。

**XMLFM**

* 使用输出服务生成XML文档时，某些XML文件(CQ-4311341、CQ-4313893)会出现`OutputServiceException`错误。

* 将上标属性应用于项目符号的第一个字符时，项目符号的大小会变小(CQ-4306476)。

* 使用输出服务生成的PDF forms不包括边框(CQ-4312564)。

**设计人员**

* 在[!DNL Experience Manager Forms] Designer中打开XDP文件时，将在与XDP文件(CQ-4309427、CQ-4310865)相同的文件夹中生成designer.log文件。

**HTML5 表单**

* 当您在[!DNL Safari] Web浏览器中为[!DNL iOS 14.1 or 14.2]选择自适应表单中的复选框时，不显示其他字段(NPR-35652)。

**Forms管理**

* 没有确认消息指示XDP文件成功批量上传到CRX存储库(NPR-35546)。

**文档安全**

* 针对AdminUI上的[!UICONTROL 编辑策略]选项报告了多个问题(NPR-35747)。

有关安全更新的信息，请参阅[Experience Manager安全公告页](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安装6.5.8.0 {#install}

**设置要求和更多信息**

* Experience Manager 6.5.8.0需要Experience Manager 6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 可在Adobe[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上下载服务包。
* 在使用MongoDB和多个实例的部署中，使用包管理器将Experience Manager 6.5.8.0安装在某个作者实例上。

>[!NOTE]
>
>Adobe不建议删除或卸载[!DNL Adobe Experience Manager] 6.5.8.0包。

### 安装Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5实例上安装Service Pack，请执行以下步骤：

1. 如果实例处于更新模式，则在安装前重新启动该实例（在从较早版本更新该实例时也是如此）。 Adobe还建议在实例当前正常运行时间较高时重新启动。

1. 在安装之前，请拍摄[!DNL Experience Manager]实例的快照或新备份。

1. 从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)下载服务包。

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包，然后单击&#x200B;**[!UICONTROL 安装]**。

1. 要更新S3连接器，请在安装Service Pack后停止该实例，用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动该实例。 请参阅[Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack时，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后确保安装成功。 通常，这种情况会在[!DNL Safari]上发生，但可能间歇性地在任何浏览器上发生。

**自动安装**

有两种方法可自动在工作实例上安装Adobe Experience Manager 6.5.8.0:

A.当服务器联机可用时，将软件包放入`../crx-quickstart/install`文件夹中。 软件包会自动安装。

B.使用包管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安装嵌套的包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页(`/system/console/productinfo`)在[!UICONTROL Installed Products]下显示更新的版本字符串`Adobe Experience Manager (6.5.8.0)`。

1. 所有OSGi捆绑包都是OSGi控制台(使用Web控制台：`/system/console/bundles`)。********

1. OSGi bundle `org.apache.jackrabbit.oak-core`是版本1.22.3或更高版本(使用Web控制台：`/system/console/bundles`)。

要了解经认证可与此版本一起使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

### 安装Adobe Experience Manager Forms加载项包{#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您不使用Experience Manager Forms，则跳过。 Experience Manager Forms中的修复在计划的[!DNL Experience Manager] Service Pack版本发布后一周内通过单独的附加程序包交付。

1. 确保已安装Adobe Experience Manager Service Pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照[安装Forms加载项包](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中所述安装AEM Forms加载项包。

>[!NOTE]
>
>AEM 6.5.8.0包含新版[AEM Forms兼容性包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)。 如果您使用的是旧版AEM Forms兼容程序包并更新到AEM 6.5.8.0，请在安装Forms Add-On程序包后安装该程序包的最新版本。

### 在JEE {#install-aem-forms-jee-installer}上安装Adobe Experience Manager Forms

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。Adobe Experience Manager Forms中的JEE修复通过单独的安装程序提供。

有关在JEE上安装Experience Manager Forms的累积安装程序和部署后配置的信息，请参阅[发行说明](jee-patch-installer-65.md)。

>[!NOTE]
>
>在JEE上安装Experience Manager Forms的累积安装程序后，请安装最新的Forms加载项包，从`crx-repository\install`文件夹中删除Forms加载项包，然后重新启动服务器。

### UberJar {#uber-jar}

用于Experience Manager 6.5.8.0的UberJar位于[Maven Central存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)中。

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)并在您的项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象可在Maven Central Repository上使用，而不是Adobe Public Maven Repository(`repo.adobe.com`)。 主UberJar文件已重命名为`uber-jar-<version>.jar`。 因此，`dependency`标签没有`classifier`，以`apis`为值。

## 已弃用功能 {#removed-deprecated-features}

下面是一列表在[!DNL Experience Manager] 6.5.7.0中标记为已弃用的功能。在将来的版本中，已标记为已弃用的功能已在初始阶段和稍后阶段被删除。 通常提供备选选项。

查看您在部署中是否使用功能。 此外，计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | **[!UICONTROL AEM云服务选择加入]**&#x200B;屏幕已弃用。 随着Experience Manager 6.5中更新的Experience Manager和Adobe Target集成以支持Adobe Target Standard API(它使用通过Adobe IMS和I/O的身份验证)，以及Adobe Launch在检测Experience Manager页面以进行分析和个性化方面日益重要的作用，选择加入向导在功能上已变得无关紧要。 | 通过相应的Experience Manager云服务配置系统连接、AdobeIMS身份验证和[!DNL Adobe I/O]集成。 |
| 连接器 | 针对Microsoft SharePoint 2010和Microsoft SharePoint 2013的Adobe JCR Connector已针对Experience Manager 6.5弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 如果您要将[!DNL Experience Manager]实例从6.5版升级到6.5.8.0版，可以在`error.log`文件中视图`RRD4JReporter`异常。 重新启动实例以解决问题。

* 如果您在[!DNL Experience Manager] 6.5上安装[!DNL Experience Manager] 6.5 Service Pack 5或之前的Service Pack，则会删除您的资产自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果在[!UICONTROL 文件夹元数据模式Forms Editor]和[!UICONTROL 元数据模式Forms Editor]中使用[!UICONTROL 定义规则]对话框编辑和创建层叠规则时遇到问题，请与Adobe客户关怀联系。 已创建和保存的规则将按预期运行。

* 如果层次结构中的文件夹在[!DNL Experience Manager Assets]中重命名，而包含资产的嵌套文件夹发布到[!DNL Brand Portal]，则在根文件夹再次发布之前，文件夹的标题不会在[!DNL Brand Portal]中更新。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他字段可解决此问题。

* 如果[!UICONTROL 连接的资产配置]向导在安装后返回404错误消息，请使用包管理器手动重新安装`cq-remotedam-client-ui-content`和`cq-remotedam-client-ui-components`包。

* 安装Experience Manager 6.5.x.x时，可能会显示以下错误和警告消息：
   * “当Adobe Target集成在Experience Manager中使用Target Standard API（IMS身份验证）进行配置时，将Experience Fragments导出到目标会导致创建错误的优惠类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证会失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过Shoppable Banner查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成未注册的超时。

## 包含{#osgi-bundles-and-content-packages-included}的OSGi包和内容包

以下文本文档列表了[!DNL Experience Manager] 6.5.8.0中包含的OSGi包和内容包：

* [列表Experience Manager 6.5.8.0中包含的OSGi包](assets/6580_bundles.txt)

* [列表Experience Manager 6.5.8.0中包含的内容包](assets/6580_packages.txt)

## 受限网站{#restricted-sites}

这些网站仅面向客户。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅[如何与Adobe客户服务部门联系](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5发行说明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 产品页](https://www.adobe.com/cn/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/subscription/priority-product-update.html)

