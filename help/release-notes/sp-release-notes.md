---
title: '[!DNL Experience Manager] 6.5 service pack发行说明'
description: 特定于 [!DNL Adobe Experience Manager] 6.5 service pack 8的发行说明
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
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
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}中包含的内容

[!DNL Adobe Experience Manager] 6.5.8.0包含自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。[!DNL Adobe Experience Manager] 6.5上安装了Service Pack。

[!DNL Adobe Experience Manager] 6.5.8.0中引入的主要功能和增强功能包括：

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 现在，使用[连接的资产功能](/help/assets/use-assets-across-connected-assets-instances.md)时，您可以查看使用该资产的所有[!DNL Sites]页面的列表。 资产的[!UICONTROL 属性]页面中提供了对资产的这些引用。 这允许管理员、营销人员和管理员全面了解资产使用情况，从而实现更好的跟踪、管理和品牌一致性。

* 删除网页中引用的资产时， [!DNL Experience Manager] [会显示警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)。 您可以强制删除引用的资产，或检查并修改资产[!DNL Properties]页面中显示的引用。 单击引用可打开本地和远程[!DNL Sites]页。

* 使用[!UICONTROL 名称]、[!UICONTROL 上次修改日期、]和[!UICONTROL 上次转出日期]属性对可供转出的Live Copy页面进行排序。

* 内置存储库(Apache Jackrabbit Oak)已更新为1.22.6。 <!-- TBD: Mention the version -->

有关[!DNL Experience Manager] 6.5.8.0中引入的功能和增强功能的完整列表，请参阅 [!DNL Adobe Experience Manager]  6.5 Service Pack 8](new-features-latest-service-pack.md)中的[新增功能。

以下是[!DNL Experience Manager] 6.5.8.0版中提供的修复列表。

### [!DNL Sites] {#sites-6580}

* 将页面移动到Blueprint后，链接的目标不会更新(NPR-35724)。
* 基于Tizen的播放器无法在某些浏览器上进行身份验证。 不支持samesite=none属性的浏览器出现问题(NPR-35589)。
* 已解锁的响应式容器不显示允许的组件(NPR-35565)。
* 创建新添加页面的Live Copy时，语言主控会为每个域创建两个副本(NPR-35545)。
* 当由于`org.apache.felix.scr.impl.ComponentRegistry`计时器导致多个线程被阻止时，SCR组件注册表中出现死锁。 因此，[!DNL Experience Manager]会在无限时间内停止响应(GRANITE-33125、FELIX-6252)。
* 在侧边栏中搜索特定资产时，结果中会包含一些未搜索的资产(NPR-35524)。
* 为Experience Manager实例启用SSL时，上下文路径将被删除(NPR-35477)。
* 创建列表时，将一些文本添加为第一个元素，将一个表添加为第二个元素，并在表内添加一个列表，父列表会扭曲(NPR-35465)。
* 如果对连续的列表项目使用不同的插件，则会向列表项目添加额外的<br>标记(NPR-35464)。
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
* 在[!DNL Experience Manager]中设置SSL时，上下文路径会自动删除(NPR-35294)。
* 单击“注销”选项后，包管理器不会注销用户(NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0修复了以 [!DNL Assets] 下问题，并提供了以下增强功能。

* 恢复资产的早期版本时，OSGi控制台中不会触发事件DamEvent.Type RESTORED(NPR-35789)。
* `IndexWriter.merge` 由于 `OutOfMemoryError` 智能标记功能创建大 `/oak:index/lucene` 和 `/oak:index/ntBaseLucene` 索引，因此会导致错误(NPR-35651)。
* 尝试保存名称中具有多字节字符的[!UICONTROL 资产贡献]类型文件夹时，会显示错误消息(NPR-35605)。
* 使用级联元数据子类型字段时，出现错误的“请填写此字段”错误(NPR-35643)。
* 在[!DNL Assets]用户界面上拖动现有资产并创建新版本后，元数据中的更改不会持久(NPR-34940)。
* 在级联菜单的元数据架构编辑器中创建规则时，[!UICONTROL 从属于]选项会重复使用相同的名称(NPR-35596)。
* 编辑[!UICONTROL 资产管理员搜索边栏]后，相似性搜索不起作用(NPR-35588)。
* 在文件夹中，如果通过单击[!UICONTROL Filter]在左边栏中打开资产搜索，则[!UICONTROL Status] > [!UICONTROL Checkout] > [!UICONTROL Checked out]中的过滤器将不起作用(NPR-35530)。
* 如果您尝试删除资产的所有智能标记并保存更改，则不会删除这些标记。 但是，用户界面会指示已保存更改(NPR-35519)。
* 用户无法在可排序文件夹的列表视图中重新排列或排序资产(NPR-35516)。
* 如果您编辑默认的元数据架构，资产[!UICONTROL 属性]页面中的“标记”字段将变为文本字段。 这项更改允许不了解的用户添加按需标记，并且这些标记将作为字符串存储在存储库中(NPR-35478)。
* 下载资产时，如果您提供的名称没有有效的电子邮件地址，则下载选项将不可用。 但是，如果选择了下载对话框中的其他选项，则会启用按钮，但不会发送电子邮件(NPR-35365)。
* 用户在编辑[!DNL Adobe InDesign]中的资产后无法签入资产，并收到有关缺少权限的错误(NPR-35341)。
* Handlebars JavaScript库已升级到v4.7.6(NPR-35333)。
* 当您从批量元数据编辑开始并取消选择项目时，元数据编辑器界面会停止按预期工作，直到仍选中单个项目为止(NPR-35144)。
* 从`assets.html`页面中单击全局导航时，无法打开正确的控制台(CQ-4312311)。
* [!DNL Assets] 对于具有RGB呈现版本的资产，不显示RGB呈现版本(CQ-4310190)。
* 菜单中的[!UICONTROL Relate]选项未正确显示在[!UICONTROL Properties]页面(CQ-4310188)中。
* 如果使用文档的文件类型过滤器搜索资产并创建智能收藏集，则在访问收藏集时不会应用该过滤器。 而是会在搜索中显示所有类型的资产(NPR-35759)。
* 您无法从[!DNL Assets]用户界面中拖动和添加Lightbox中的资产(NPR-35901)。
* 在解决命名冲突后创建现有资产的新版本时，会覆盖原始资产的元数据(CQ-4313594)。
* 当您使用搜索过滤器或谓词过滤资产搜索时，打开资产以查看或编辑资产，然后返回到搜索结果页面，则该过滤器不起作用。 所有搜索的资产都将列出为未过滤资产(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* 资产详细信息页面上启用了RESS图像预设的URL选项。 现在，在动态演绎版部分中选择RESS图像预设后，资产详细信息页面上会提供URL和RESS选项。 (CQ-4311241)
* 交互式媒体组件 — 如果用户具有具有选择性发布配置的[!DNL Experience Manager](CQ-4311054)，则交互式视频不起作用。
* 如果您跨文件夹移动资产，则通过API在[!DNL Experience Manager]和[!DNL Dynamic Media–Scene7]之间同步会非常慢(CQ-4310001)。
* 使用Omnisearch时，日志大小会显着增加(CQ-4309153)。
* 启用选择性同步并将资产复制（未移动）到同步文件夹中后，它不会按预期同步(CQ-4307122)。
* 对于自动发布到DM的已上传资产，状态不会在AEM上显示“已发布”。 此外，Dynamic Media发布状态列不显示正确的已发布状态(CQ-4306415)。
* 如果资产在[!DNL Experience Manager]上发布，并在激活时设置为发布到[!DNL Dynamic Media]，则`scene7FileStatus`元数据值不会按预期更新(CQ-4308269)。
* 编辑视频配置文件时，[!DNL Experience Manager]不显示为视频预设设置的高度和比特率值。 字段显示为空(CQ-4311828)。

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

* 对IMS租户ID和目标客户端代码使用不同的值时，[!DNL Experience Manager]无法与[!DNL Adobe Target]集成(NPR-35342)。

### 翻译项目{#translation-6580}

* 在[!DNL Experience Manager]中导出或导入翻译作业时出现问题(NPR-35259)。

### 营销活动 {#campaign-6580}

* 在触屏UI中使用现成模板创建促销活动页面，并打开页面属性对话框中的“电子邮件”选项卡时，主题和正文字段的个性化变量保持禁用状态(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* 在将页面结构添加到社区组时，痕迹导航中的[!UICONTROL 组]标题将更改为第一个[!UICONTROL 页面]的标题(NPR-35803)。
* 与审核者不同，标准社区成员无法访问和编辑任何草稿帖子(NPR-35339)。
* `DSRPReindexServlet`的访问控制和拒绝服务中断，导致社区站点停止运行，直到索引完成(NPR-35591)。
* 从[!UICONTROL Administrators]字段中删除[!UICONTROL 所有用户]实际上不会从后端删除这些用户(NPR-35592、NPR-35611)。
* 当输入的文本与部分匹配时，[!UICONTROL 撰写消息]组件不返回任何结果(NPR-35666)。

* 尝试通过选择&#x200B;**[!UICONTROL Add Tags]**&#x200B;将标记添加到新博客时，您可能会注意到一些性能影响和速度缓慢。 要提高性能，请安装[cqTagLucene-0.0.1.zip修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)。

### [!DNL Brand Portal] {#brandportal-6580}

* 向[!UICONTROL 资产贡献]类型文件夹添加成员时，用户界面中会显示[!UICONTROL 添加用户或组]标题，尽管仅支持Brand Portal活动用户，而不支持组(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。

**自适应表单**

* 将具有可重复行的表插入到在自适应表单中具有多个实例的可重复面板时，始终会将该表添加到面板的第一个实例(NPR-35635)。

* 在自适应表单中成功验证一次制表符集合后，再次将其显示到CAPTCHA组件时， [!DNL Experience Manager Forms]会显示`Provide Captcha phrase to proceed`错误消息(NPR-35539)。

**交互式通信**

* 提交翻译后的表单时，提交消息将以英语显示，且不会翻译成相应的语言(NPR-35808)。

* 在附加的XDP或文档片段中包含隐藏条件时，交互式通信无法加载(NPR-35745)。

**通信管理**

* 编辑信件时，包含条件的模块需要较长时间才能加载(NPR-35325)。

* 从左侧导航窗格中选择信件中未包含的资产，然后选择下一个资产时，不会从之前选择的资产中删除蓝色突出显示(NPR-35851)。

* 编辑信件中的文本字段时， [!DNL Experience Manager Forms]会显示`Text Edit Failed`错误消息(CQ-4313770)。

**工作流**

* 当您尝试在[!DNL Experience Manager Forms]移动设备应用程序上为iOS打开自适应表单时，应用程序会停止响应(CQ-4314825)。

* HTML工作区中的[!UICONTROL To-do]选项卡显示HTML字符(NPR-35298)。

**XMLFM**

* 使用输出服务生成XML文档时，某些XML文件(CQ-4311341、CQ-4313893)会出现`OutputServiceException`错误。

* 将上标属性应用于项目符号的第一个字符时，项目符号大小会变小(CQ-4306476)。

* 使用输出服务生成的PDF forms不包括边框(CQ-4312564)。

**Designer**

* 在[!DNL Experience Manager Forms] Designer中打开XDP文件时，将在与XDP文件(CQ-4309427、CQ-4310865)相同的文件夹中生成designer.log文件。

**HTML5 表单**

* 在[!DNL Safari] Web浏览器的[!DNL iOS 14.1 or 14.2]自适应表单中选中复选框时，不显示其他字段(NPR-35652)。

**Forms管理**

* 没有确认消息来指示XDP文件已成功批量上传到CRX存储库(NPR-35546)。

**文档安全**

* 在AdminUI中，针对[!UICONTROL 编辑策略]选项报告了多个问题(NPR-35747)。

有关安全更新的信息，请参阅[Experience Manager安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安装 6.5.8.0 {#install}

**设置要求和更多信息**

* Experience Manager6.5.8.0需要Experience Manager6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。
* 可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载Service Pack。
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装Experience Manager6.5.8.0。

>[!NOTE]
>
>Adobe不建议移除或卸载[!DNL Adobe Experience Manager] 6.5.8.0包。

### 安装Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5实例上安装Service Pack，请执行以下步骤：

1. 如果实例处于更新模式，请在安装前重新启动该实例（在从早期版本更新该实例时，即为此情况）。 Adobe还建议，如果实例的当前正常运行时间较高，则应重新启动。

1. 在安装之前，请拍摄[!DNL Experience Manager]实例的快照或新备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)下载Service Pack。

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅[Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常情况下，这会在[!DNL Safari]上发生，但是可能会间歇性地在任何浏览器上发生。

**自动安装**

在工作实例上自动安装Adobe Experience Manager 6.5.8.0的方法有两种：

A.当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 包会自动安装。

B.使用包管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安装嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下显示更新的版本字符串`Adobe Experience Manager (6.5.8.0)`。

1. 所有OSGi包均为OSGi控制台中的&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**(使用Web控制台：`/system/console/bundles`)。

1. OSGi包`org.apache.jackrabbit.oak-core`的版本为1.22.3或更高版本(使用Web控制台：`/system/console/bundles`)。

要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

### 安装Adobe Experience Manager Forms附加组件包{#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您没有使用Experience ManagerForms，请跳过。 在计划的[!DNL Experience Manager] Service Pack版本发布后一周，Experience ManagerForms中的修复将通过单独的附加组件包提供。

1. 确保您已安装Adobe Experience Manager Service Pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)中列出的相应 Forms 附加组件包。
1. 按照[安装Forms附加组件包](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中所述安装AEM Forms附加组件包。

>[!NOTE]
>
>AEM 6.5.8.0包含新版本的[AEM Forms兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)。 如果您使用的是旧版AEM Forms兼容包并更新到AEM 6.5.8.0，请在安装Forms附加组件包后安装该包的最新版本。

### 在JEE上安装Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。JEE上的Adobe Experience Manager Forms中的修复通过单独的安装程序提供。

有关在JEE上安装用于Experience ManagerForms的累积安装程序以及部署后配置的信息，请参阅[发行说明](jee-patch-installer-65.md)。

>[!NOTE]
>
>在JEE上安装用于Experience ManagerForms的累积安装程序后，安装最新的Forms附加组件包，从`crx-repository\install`文件夹中删除Forms附加组件包，然后重新启动服务器。

### UberJar {#uber-jar}

适用于Experience Manager6.5.8.0的UberJar在[Maven Central存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)中提供。

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目POM中包含以下依赖项：

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
>UberJar和其他相关对象在Maven中央存储库中可用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为`uber-jar-<version>.jar`。 因此，没有`classifier`作为`apis`值的`dependency`标记。

## 已弃用功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中标记为已弃用的特性和功能列表。在将来的版本中，这些功能最初被标记为已弃用，后来又被删除。 通常会提供替代选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | **[!UICONTROL AEM云服务选择加入]**&#x200B;屏幕已弃用。 随着Experience Manager6.5中更新了Experience Manager和Adobe Target集成，以支持Adobe Target Standard API(该API使用通过AdobeIMS和I/O进行身份验证)，以及Launch在检测Experience Manager页面以进行分析和个性化方面日益发挥的作用，选择加入向导在功能上已变得无关紧要。 | 通过相应的Experience Manager云服务配置系统连接、AdobeIMS身份验证和[!DNL Adobe I/O]集成。 |
| 连接器 | 适用于Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR Connector已在Experience Manager6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 如果您要将[!DNL Experience Manager]实例从6.5版升级到6.5.8.0版，则可以在`error.log`文件中查看`RRD4JReporter`异常。 重新启动实例以解决问题。

* 如果您在[!DNL Experience Manager] 6.5上安装[!DNL Experience Manager] 6.5 Service Pack 5或之前的Service Pack，则会删除资产自定义工作流模型（在`/var/workflow/models/dam`中创建）的运行时副本。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果在[!UICONTROL 文件夹元数据架构Forms编辑器]和[!UICONTROL 元数据架构Forms编辑器]中使用[!UICONTROL 定义规则]对话框编辑和创建级联规则时遇到问题，请联系Adobe客户关怀。 已创建和保存的规则可按预期运行。

* 如果层次结构中的文件夹在[!DNL Experience Manager Assets]中重命名，并且包含资产的嵌套文件夹已发布到[!DNL Brand Portal]，则在再次发布根文件夹之前，文件夹的标题不会在[!DNL Brand Portal]中更新。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 如果[!UICONTROL 连接的资产配置]向导在安装后返回404错误消息，请使用包管理器手动重新安装`cq-remotedam-client-ui-content`和`cq-remotedam-client-ui-components`包。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数（如SUM、MAX和MIN）时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

## 包含的{#osgi-bundles-and-content-packages-included} OSGi包和内容包

以下文本文档列出了[!DNL Experience Manager] 6.5.8.0中包含的OSGi包和内容包：

* [Experience Manager6.5.8.0中包含的OSGi包列表](assets/6580_bundles.txt)

* [Experience Manager6.5.8.0中包含的内容包列表](assets/6580_packages.txt)

## 受限网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅[如何联系Adobe客户关怀团队](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5发行说明](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 产品页面](https://www.adobe.com/cn/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
* [订阅 Adobe 产品更新早知道](https://www.adobe.com/subscription/priority-product-update.html)

