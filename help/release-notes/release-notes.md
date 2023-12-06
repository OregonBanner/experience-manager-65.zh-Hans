---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作说明以及的详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '3552'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2023年11月30日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包括的内容 [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0包括自2019年4月首次推出6.5以来发布的新功能、关键客户请求的增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) 日期 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

**主要功能和增强功能**

此版本中的某些主要功能和增强功能包括：

* 允许站点页面编辑器/图像组件用户从远程AssetsCloud Service引用资源。 (SITES-13448和SITES-13433)
* AEM现在支持服务器端排序，从而加快列表视图中的项目导航速度。 项目节点在显示在界面中之前根据用户选择的列排序。

**已弃用功能**

* 已弃用AEM中的ActiveMQ。 ActiveMQ用于两个AEM Publish实例之间的通信。 Adobe建议客户现在使用负载平衡器。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 19中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### 辅助功能{#sites-accessibility-6519}

* 在AEM Sites页面上，当您百分之百放大页面时，链接 **[!UICONTROL 语言复制]** 和 **[!UICONTROL CSV报表]** 在引用边栏中消失。 (SITES-11011)

#### 管理员用户界面{#sites-adminui-6519}

* AEM Screens渠道 **[!UICONTROL 预览]** 功能在功能板上不起作用或无法显示。 (SITES-15730)
* 在页面移动操作期间，如果用户界面无法显示引用，但指出这些引用已自动重新发布，则它们会 *非* 已重新发布。 (SITES-16435)
* 在带有Service Pack 16或17的AEM 6.5中，当在启用了“工作流”列的网站的列表视图中时，无法根据该列中的项目对列表进行排序。 不执行排序。 (SITES-15385)
* 对于重定向页面模板，重定向字段已设置为必填字段。 但是，在以下两种情况下，必填字段的验证既无法应用，也无法工作：当创建的页面没有强制重定向值时；无法创建重定向页面。 使用键盘快捷键导航时，验证不起作用，并且当字段标记为无效时，验证无法继续。 (SITES-15903)
* 部分 **传入链接** 未包括在 **引用** 面板。 例如，该面板显示 **传入链接(6)** 但实际上有9个链接传入。 (SITES-14816)

#### 经典 UI{#sites-classicui-6519}

* 在SITES-15827中安装修补程序后，单词之间有空格的对话框标题将被替换为 `" "`. 换行符也被删除。 (SITES-16089)
* 已编码的对话框标题现在会导致对标题进行双重编码。 (SITES-15841)
* 将AEM服务器从Service Pack 6.5.16更新到6.5.17会导致对经典UI对话框标题进行双重编码。 (SITES-15634)

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* 内容片段编辑器中会显示一条内部服务器错误消息。 (SITES-13550)
* 更新 `org.json` 通过NPR-41291方式生成的库导致中的数据错误转换 `DefaultDataTypeConverter` 的 `cfm-impl` 捆绑。 数据类型转换必须更加灵活。 (SITES-16473)
* 获取错误弹出消息“由于内容不兼容，此内容片段版本无法与当前版本进行比较。” 内容片段应当具有可比性，但事实并非如此。 (SITES-16317)
* 已将资源选择器JS URL从
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
到
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068)
* 将新的Polaris元数据API响应模式适用于CFM-Polaris集成。 (SITES-15166)
* 应列出引用所选内容片段的所有内容片段。 相反，内容片段引用面板中的资产引用显示0（零）引用。 (SITES-15036)

#### 核心后端{#sites-core-backend-6519}

* 改进 `StyleImpl`. (SITES-15164)
* 改进WCM管道的release/650分支，以便能够为其模块运行集成测试。 (SITES-12938)

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Campaign集成{#sites-campaign-integration-6519}

* 在签名组件上(`/apps/fpl/components/campaign/signature`)，链接Externalizer无法正常工作。 如果删除了图像标记上方的HTML评论，则域未附加到图像源。 此问题仅存在于生产环境中的签名组件中，而不存在于暂存环境中。 (SITES-16120)

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### 基础组件（旧版）{#sites-foundation-components-legacy-6519}

* Adobe Experience Manager (AEM) Sites Search组件损坏了用户界面。 (SITES-15087)

#### GraphQL Query Editor{#sites-graphql-query-editor-6519}

* 当查询数量较多时（例如，超过25个），GraphQL编辑器用户界面不允许您滚动浏览所有持久查询。 (SITES-16008)
* GraphQL编辑器未保存持久查询的发布状态。 GraphQL编辑器中会显示取消发布按钮，但不显示指示已发布持久查询的图标。 刷新页面会显示持久查询甚至未发布。 (SITES-15858)

#### 启动项{#sites-launches-6519}

* 存储库中的更改无法保存，原因是 `Oak0001` 在编辑多个页面或创作内容时发生冲突。 在此类事件中执行重试是正常的，但不会发生这种情况。 (SITES-14840)

#### MSM — 活动副本{#sites-msm-live-copies-6519}

* MSM转出按钮在触控图形用户界面中不起作用。 (SITES-16991)
* 创建Live Copy或转出体验片段时，体验片段内的链接引用未更新。 (SITES-15460)

#### 页面编辑器{#sites-pageeditor-6519}

* 在Forms >主题中，如果在主题编辑器中打开主题并进行一些更改并保存，然后单击预览，则会显示加载图标，但不会加载实际预览。 (SITES-17164)
* 在资产类型筛选器上选择多个文档文件类型在页面控制台上不起作用。 即使某个特定文件类型的结果可用，也找不到任何结果。 因此，作者无法过滤多个文档。 他们必须使用多种文档类型，并且必须逐个进行筛选。 (SITES-14047)
* 从AEM 6.5.17和AEM 6.5.18升级实例后，在页面编辑器中（如果已选择） **[!UICONTROL 发布页面]**，您会被重定向到不存在的URL。 用户应被重定向到“发布”向导。 (SITES-15856)
* 在操作系统剪贴板粘贴过程中从AEM剪贴板进行冗余复制。 (SITES-15704)
* 在资产中，选择 **[!UICONTROL 文档]**，然后在 **[!UICONTROL Filtertype]**，选择 **[!UICONTROL Microsoft® Word]** 或 **[!UICONTROL Microsoft® Excel]** 即使存在这两种类型的文件，也不显示任何结果。 (SITES-14837)

### [!DNL Assets]{#assets-6519}

* 创建或保存公共文件夹时，会在管理员功能板中创建三个组。 (ASSETS-26700)
* 无法区分将资源发布到Experience Manager或Brand Portal。 (NPR-41320)
* 在搜索面板中，当您选中复选框并取消选中任何一个复选框时，所有复选框都将被取消选中。 (ASSETS-26377)

#### [!DNL Dynamic Media]{#assets-dm-6519}

* 将资源上传到AEM后， `update_asset` 工作流已触发。 该工作流永远不会完成。 查看工作流实例，工作流会完成到产品上传步骤。 下一步是Scene7批量上传。 用户可以从Dynamic Media Classic应用程序中看到资源位于Scene7中。 (ASSETS-30443)
* 自定义Servlet（API端点）返回错误的Dynamic Media (Scene7)文件名。 删除资产并将其替换为同名资产时，会发生这种情况。 自定义servlet将返回旧的Dynamic Media (Scene7)文件名，而“jcr”API调用将返回正确的文件名。 (ASSETS-29476)
* 即使在文件夹级别关闭同步后，日志也会显示“Scene7 ReplicateOnModifyListener”的触发器。 此 `ReplicateOnModifyListener/Worker` 应跳过对非Dynamic Media文件夹资源和内容片段的处理。 (ASSETS-26705)
* 如果焦点在高对比度黑白模式下的下拉元素（仅限内容、视图、更多选项）中不可见，则视力缺佳的人会受到影响。 (ASSETS-25759)
* 如果页面上文本的光度对比度小于4.5:1，则视力缺佳的人会受到影响。 (ASSETS-25756)
* 屏幕阅读器在提交数据后不提供所显示弹出消息的旁白。 (ASSETS-25755)
* 使用地标/区域快捷键导航时，屏幕阅读器无法识别页面中的地标(Dynamic Media；创建视频编码配置文件) `D/R`. (ASSETS-25752)
* 使用地标/区域快捷键导航时，屏幕阅读器无法识别页面中的多个地标(Dynamic Media；创建交互式视频) `D/R`. (ASSETS-25750)
* 屏幕阅读器（NVDA/JAWS/讲述人）无法识别中的里程碑 **编辑资源** 使用快捷键导航时显示的页面 `D/R`. (ASSETS-25744)
* 用户收到空/假异步作业消息，但连接的资产已成功发布。 (ASSETS-29342)

### [!DNL Forms]{#forms-6519}

中的修复 [!DNL Experience Manager] Forms在计划的一周后通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack发行日期。 在本例中，AEM 6.5.19.0 Forms附加组件包版本计划于2023年11月30日星期四发布。 发布后，此部分中将添加一系列Forms修复和增强功能。

* 添加访问控制列表 `fd-cloudservice` 用户能够读取或更新下的Microsoft®配置 `cloudconfigs/microsoftoffice`. (FORMS-11142)

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

### Foundation{#foundation-6519}

* 在语言根级别创建语言副本不会调整页面中的路径。 如果创建了语言副本（不是针对语言根，而是针对其下方的页面），则路径正确更改。 (NPR-41364)
* “相对日期显示”工具提示只能通过按键盘上的Esc键关闭。 当用户选择用户界面的任何部分时，工具提示都应关闭。 (NPR-41394)
* 未本地化的字符串 `Something went wrong while adding the private key.` 在中添加错误的私钥文件时 **编辑用户** > **密钥库**. (NPR-41366)
* AEM 6.5环境中的Microsoft®SharePoint和Microsoft®一个驱动器需要图标。 (NPR-41354)
* 未本地化的“用户ID/密码不匹配”。 字符串输入 **安全性** > **用户** > **创建** 对话框。 (NPR-41245)
* 弹出框代码和事件处理程序加载两次，破坏了用户创建的基于Coral3的用户界面。 (NPR-41171)
* 在AEM Sites控制台中使用“全选”后，取消选择无法正常工作。 (NPR-41304)

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### 集成{#integrations-6519}

* AEM电子邮件营销活动中的短信链接未正确写入；它们包含HTML锚点元素。 (NPR-41211)
* 在帐户配置屏幕上使用的措辞不应使用新的凭据类型。 (NPR-41210)
* 正在将Analytics报表导入计划程序从 `ManagedPollConfig` 去吊索乔布斯。 将两个不同的分析框架与不同的报表包附加到两个不同的站点时， `ManagedPollConfig` 只能轮询其中一项。 (NPR-41209)
* 将该值重置为默认值后，以前选择的时间范围按钮将保持启用状态。 在AEM的内容洞察功能板中，默认情况下，时间范围设置为周，并将内容洞察显示为每周数据。 现在，如果用户选择其他时间范围选项，例如小时、日、月和年，数据会根据所选值而变化。 但是，如果重置了值，则默认情况下，可见的时间范围为周，但仍会选中之前选择的时间范围选项。 (NPR-41246)

#### Oak{#oak-6519}

* 在异步索引延迟的情况下，用于限制写入AEM速率的反向端口实用程序。 (NPR-40985)

#### Platform{#foundation-platform-6519}

* 包含方括号的QueryBuilder查询被错误地转换为xpath 。 (NPR-41298)

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### 翻译项目{#foundation-translation-6519}

* 在创建页面“A”的语言副本时，它应自动创建引用的页面、体验片段、内容片段和资产的语言副本。 此外，新路径下新创建的页面“A”的语言副本应将其引用更新为页面、体验片段、内容片段和资产的各自新创建的语言副本。 (NPR-41076)

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### 工作流{#foundation-workflow-6519}

* 无法完成收件箱中的任务。 尝试完成任务并选择操作时，下拉菜单中只显示“未定义”值。 这意味着用户无法应用AEM 6.5.18 Service Pack。 (NPR-41402和NPR-41473)
* 无法完成收件箱中的任务。 尝试完成zip文件、资源报表、移动（成功或失败）或资源到期的任务时，下拉列表中没有值（仅限“未定义”）。 (NPR-41305)
* 当用户选择时 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** >实例，选择正在运行的工作流，然后选择 **[!UICONTROL 查看有效负荷]**，这将导致出现500错误页面。 (NPR-41325)

## 安装 [!DNL Experience Manager] 6.5.19.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0需要 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以获取详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上获取Service Pack下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 6.5.19.0适用于使用包管理器的某个Author实例。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.19.0程序包。 因此，在安装该包之前，您应该创建 `crx-repository` 万一你一定要把它退回。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装服务包 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。

1. 从以下位置下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack期间，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能间歇性地在任何浏览器上出现。

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL Experience Manager] 6.5.19.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.19.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.19.0)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.17或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装服务包的说明，请参阅 [Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装 [GraphQL索引包1.1.1的Experience Manager内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

UberJar用于 [!DNL Experience Manager] 6.5.19.0可从以下网站获取： [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件可在Maven中央存储库而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，替换为 `apis` 作为值，用于 `dependency` 标记之前。

## 已弃用和已删除的功能{#removed-deprecated-features}

请参阅 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md/).

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **与Oak相关**
在Service Pack 13及更高版本中，已开始出现以下错误日志，这会影响持久性缓存：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或者

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  要解决此异常，请执行以下操作：

   1. 从删除以下两个文件夹 `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 安装Service Pack，或重新启动Experience Manageras a Cloud Service。
的新文件夹 `cache` 和 `diff-cache` 自动创建，并且您不再遇到与相关的异常 `mvstore` 在 `error.log`.

* 更新可能已为内容模型使用自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询可能使用 `damAssetLucene` 索引而非 `fragments` 索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  要更正此问题， `damAssetLucene` 必须配置为在以下位置包含以下两个属性： `/indexRules/dam:Asset/properties`：

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  更改索引定义后，需要重新索引(`reindex` = `true`)。

  执行这些步骤后，GraphQL查询的执行速度应该会更快。

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题，因为后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您升级您的 [!DNL Experience Manager] 从6.5.0 - 6.5.4到Java™ 11上最新Service Pack的实例，请参见 `RRD4JReporter` 中的例外 `error.log` 文件。 要停止例外，请重新启动您的实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在以下位置重命名层级中的文件夹： [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题不会在中更新 [!DNL Brand Portal] 直到重新发布根文件夹。

* 安装期间可能会显示以下错误和警告消息 [!DNL Experience Manager] 6.5.x.x：
   * “当在中配置Adobe Target集成时 [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型为“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance中未找到维护窗口。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance中未找到维护窗口。
   * 通过可购物横幅查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，Rhino JavaScript引擎由 ```org.apache.servicemix.bundles.rhino``` 捆绑有新的提升行为。 使用严格模式(```use strict;```)必须正确声明其变量，否则它们不会运行，而是会引发运行时错误。

### AEM Forms的已知问题

#### 支持的平台

* WebLogic JEE服务器不支持高于1.8.0_281的JDK版本。 (FORMS-8498、CQDOC-20383)
* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支持的全包安装 [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20不支持在JEE安装程序上安装AEM Forms。 在JEE安装程序上安装AEM Forms仅支持JDK 11.0.19或更早版本。 (FORMS-10659)

#### 安装

* 在JBoss® 7.1.4平台上，当用户安装Experience Manager6.5.16.0或更高版本的Service Pack时， `adobe-livecycle-jboss.ear` 部署失败。 (CQ-4351522和CQDOC-20159)
* 升级到Windows Server 2022上的AEM Forms 6.5.18.0 JBoss® Turnkey完整安装程序环境后，使用Java™ 11编译输出客户端应用程序代码时，可能会出现以下编译错误：

  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  ```

  要解决此问题，请执行以下步骤：
   1. 导航到 `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` 和unzip `adobe-output-client.jar` 以提取 `Manifest.mf` 文件。
   1. 更新 `Manifest.mf` 通过删除条目生成文件 `${clover.jar.name}` 从class-path属性中。

      >[!NOTE]
      >
      > 您还可以使用就地编辑工具（例如7-zip）来更新 `Manifest.mf` 文件。

   1. 保存更新的 `Manifest.mf` 在 `adobe-output-client.jar` 存档。
   1. 保存修改的内容 `adobe-output-client.jar` 文件并重新运行安装程序。 (CQDOC-20878)
* 安装AEM Service Pack 6.5.19.0完整安装程序后，EAR部署在使用JBoss® Turnkey的JEE上失败。
要解决此问题，请找到 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` 文件和更新 `Adobe_Adobe_JAVA_HOME` 到 `Adobe_JAVA_HOME` 所有出现的次数。 (CQDOC-20803)

#### 安装servlet片段(AEM Service Pack 6.5.14.0或更低版本)

* 如果您要升级到AEM Service Pack 6.5.15.0或更高版本，并且AEM实例在Tomcat 8.5.88上运行，则必须安装servlet片段 *早于* 请继续安装Service Pack 6.5.15.0或更高版本。
* 必须为所有应用程序服务器(在JBoss® EAP 7.4.0上运行的除外)安装servlet片段。

**安装servlet片段：**

1. 下载servlet片段，从 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. 启动应用程序服务器。
1. 等待日志稳定并检查捆绑包状态。
1. 打开Web控制台包。 默认URL为 `http://[Server]:[Port]/system/console/bundles`.
1. 选择 **[!UICONTROL 安装]** 或 **[!UICONTROL 更新]**.
1. 选择下载的片段
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. 选择 **[!UICONTROL 安装]** 或 **[!UICONTROL 更新]**.
1. 等待应用程序服务器稳定下来。
1. 停止应用程序服务器。

#### 自适应表单

* 发布自适应表单时，其所有依赖项（包括策略）都会重新发布，即使尚未对它们进行任何修改也是如此。 (FORMS-10454)
* 当用户选择在自适应表单中首次配置字段时，属性浏览器中不显示保存配置的选项。 选择在同一编辑器中配置自适应表单的某些其他字段可解决此问题。
* 在自适应表单的指南容器中设置重定向URL后，内联签名将停止工作。 (FORMS-10493)要解决此问题，请下载并安装 [适用于6.5.18.0的修补程序](/help/release-notes/aem-forms-hotfix.md).
* 所有记录文档(DoR)模板均无法发布。 仅发布基于区域设置的英文DoR模板及其关联的基于Forms的DoR模板。 (FORMS-10535)要解决此问题，请下载并安装 [适用于6.5.18.0的修补程序](/help/release-notes/aem-forms-hotfix.md).


#### 交互式通信

* 升级到AEM Service Pack 18后，无法在编辑模式下打开包含大型内联图像的交互式通信。 (FORMS-10578)要解决此问题，请安装 [适用于6.5.18.0的修补程序](/help/release-notes/aem-forms-hotfix.md).

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了中包含的OSGi包和内容包 [!DNL Experience Manager] 6.5.19.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.19.0中包含的OSGi包列表](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.19.0中包含的内容包列表](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅Adobe产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)
