---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找发行信息、新增功能、安装操作方法，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
source-git-commit: ea90bd913b437a564fb50e01af7719510fa22e74
workflow-type: tm+mt
source-wordcount: '2692'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2023年2月23日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包含的内容 [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0包括自2019年4月6.5版首次发布以来发布的新增功能、客户请求的关键增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Media的一个关键改进是：

启动了新协议DASH（通过HTTP的动态自适应流）支持，以在Dynamic Media视频交付中实现自适应比特率流传输（使用CMAF） [常用媒体应用程序格式] 启用)。

* 自适应流播放(DASH/HLS)可确保最终用户更好地观看视频。
* DASH是自适应视频流传输的国际标准协议，在业界得到广泛采用。
* 现在在北美提供（将通过支持票证启用），即将在亚太和欧洲 — 中东 — 非洲推出。

请参阅 [在您的帐户上启用短划线](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* 连接的资产：为远程DAM上的图像启用智能裁剪选项、将图像上传到文件夹，并将文件夹同步到本地站点时，该文件夹不会在本地Sites部署中打开。 (NPR-39912)
* 按名称对收藏集进行排序时，列表视图无法正常工作(ASSETS-19401)
* 将大型媒体文件(JPEG)上传到收藏集后，Experience Manager停止响应。 (ASSETS-19387)
* 在内容树窗格中，显示的资产名称不正确，因为资产的位置未正确呈现。 (ASSETS-18870)
* 使用链接共享收藏集时，URL中的数据在卡片视图和列表视图的混洗之间不匹配。 (ASSETS-18758)
* 对文件夹类型使用过滤器执行全局搜索时，搜索结果不一致。 (ASSETS-18227)
* 的 `dam:size` 属性在XMP写回后未更新，这会导致从返回错误信息 `/platform/path/to/asset.jpg;resource=metadata` API。 (ASSETS-17631)
* 所有Experience Manager实例上的资源解析程序未关闭。 (ASSETS-16904)
* 即使为您分配了 `create` 和 `modify` 权限。 (ASSETS-15956)
* 的 `move` 将资产从一个点移动到另一个点时，会随机禁用按钮。 (ASSETS-14889)
* 屏幕阅读器无法识别标题，因为文本不是在标题标记中定义的，而是常规文本。 (ASSETS-6924)
* 图像下的替换文本不是强制的，但图像下显示的文本会重复，并带有 `Type` 属性。 (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* 表单元素不包含标签。 使用屏幕阅读器（如NVDA和JAWS）时，无法正确发布表单标签信息。 (CQ-4344078)
* 当 `Escape` 键在键盘上使用。 (CQ-4344077)
* 在提供无效输入后为内联错误建议显示的信息图标（字母“i”）无法使用键盘访问。 (CQ-4344076)
* `getManifestURI` 由于JCR属性被读取为，因此返回null `toString` 而不是 `getString`. (ASSETS-18674)
* SmartCrop视频组件行为不正确。 组件正在执行播放，而不是流播放，并且VTT调用失败，导致404错误。 (ASSETS-18468)
* 选择 **[!UICONTROL 属性]** 在资产的“查看器”页面上，会导致空指针异常。 (ASSETS-18420)
* [!DNL Experience Manager] DASH流的用户界面更改，包括以下内容：
   * 在视频配置文件编辑器中具有可见的CMAF（通用媒体应用程序格式）字段。
   * 通过视频上传过程发送CMAF标记。
   * 选项 **[!UICONTROL 自动]**, **[!UICONTROL hls]**&#x200B;和 **[!UICONTROL 短划线]** 现在在查看器预设编辑器的“播放”下拉列表中可用 **[!UICONTROL 行为]** 选项卡。
(ASSETS-17428)
* 在导航中，当您选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]** > **[!UICONTROL 创建]** > **[!UICONTROL 轮播集]**，则图像图标与“幻灯片1”文本字符串重叠。 (ASSETS-18578)
* 将再次发布未发布的资产。 (ASSETS-16428)
* Experience Manager作者因加载问题而停止工作，提示创建合成警报。 (ASSETS-15937)
* 在Dynamic Media的“常规设置”页面中，显示一条未翻译的错误消息 `Failed to fetch data` 中。 (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 主要功能 {#forms-features-6516}

* [无头自适应Forms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 使您的开发人员能够创建、发布和管理可通过API访问和交互的交互式表单，而不是通过传统的图形用户界面。

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一组24个符合BEM规范的开源组件，这些组件基于Adobe Experience Manager WCM核心组件构建。 这些组件是开源的，使开发人员能够轻松自定义和扩展这些组件，以满足其组织的特定需求。 任何具备定制技能的人 [WCM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) 可以轻松自定义和设置这些组件的样式。

* OSGi上的Reader扩展服务现在提供了单独的选项，用于在PDF上启用导入和导出使用权限以在Adobe Acrobat Reader中导入或导出数据。 (NPR-39909)

### [!DNL Forms] 修复 {#forms-fixes-6516}

* 使用“分配任务**”步骤为分配的任务发送通知时，会发送两封电子邮件，而不是一封给分配的个人。 (NPR-40078)
* 当用户隐藏表标题时，会导致取消设置以前设置的列宽，并且所有列都保持相同的宽度。 (NPR-40063)
* 如果您将管理员用户的默认密码从 `admin`，执行 `Prepare Adobe Experience Manager Server For DSC deployment` 检查AEM Forms JEE Service Pack失败。 (NPR-40062)、(NPR-39387)
* 输出服务和汇编程序服务API无法将PDF表单转换为PDF/A。(NPR-39990)
* 汇编程序服务无法将PDF转换为PDF/A。当用户将PDF转换为PDF/A时，会出现以下错误： `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* 当GuideSubmitServlet API调用的服务器端验证失败时，不会在发送给客户端的响应中返回错误。 (NPR-39925)
* 在Windows服务器上升级到AEM 6.5.15.0 Service Pack后，用户会遇到多条错误消息，并且电子邮件服务无法正常运行。(NPR-39919)
* 升级到AEM 6.5.14.0并使用importData服务将PDF与XML合并时，会出现以下错误： `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* 用户安装时 **文档安全办公室** 扩展中，会出现以下问题：
   * Microsoft® Excel频繁崩溃。
   * 在打开安全文档时， **文件安全办公室** 未在计算机上检测到安装扩展。 指示用户下载并安装安全扩展。 (NPR-39768)
* 用户升级到AEM 6.5.15.0 Service Pack后，无法进行PostScript到Pdf的转换。 (NPR-39765)、(NPR-39764)
* 当用户在打开自适应表单后尝试打开导览屏幕时，会失败，出现空指针异常：`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:”` (NPR-39654)
* 在Windows中，当用户启用高对比度黑色设置时，HTML5 Forms内容在浏览器中以HTML预览形式呈现时将不清晰。 (NPR-39018)

## 集成 {#integrations-6516}

* 从Experience Manager6.5中删除AdobeSearch&amp;Promote代码和依赖项。AdobeSearch&amp;Promote已于2022年9月终止服务。 请参阅 [AdobeSearch&amp;Promote服务终止公告](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* 当前 `cq-wcm-core` 艺工厂版本没有POM。 (SITES-10983)
* 转出预览操作不应列出要创建的页面。 (SITES-10355、CQ-4266213)
* 在MSM分离后转出会重新创建分离的页面。 (SITES-9841)
* 创建启动项是超时；用户必须在加载屏幕上等待多分钟，然后请求才会超时。 (SITES-9051)
* 转出页面用户界面显示不存在的父页面路径。 您可以转出包含成功消息的页面，但由于父页面从未转出，因此不会转出子页面。 (SITES-8621)

### [!DNL Sites] - 核心组件 {#sites-core-components-6516}

* 将链接处理集中到电子邮件页面上，这样便不再需要模型自定义。 (SITES-9002)

### [!DNL Sites]  — 管理员用户界面 {#sites-adminui-6516}

* CSV导出不会导出选定页面下的所有页面。 (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* 无法打印内容片段的JSON。 原因是在打开内容片段的预览页面时无法生成GraphQL查询。 (SITES-8619)
* 重新打开内容片段模型编辑器时，所有 **[!UICONTROL 日期和时间]** 字段默认使用“日期和时间”类型。 (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 即使模板列在允许的模板下，您也无法将体验片段移动到其他文件夹。 (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - 页面编辑器 {#sites-pageeditor-6516}

* 更新了SITES-8464中对资源解析程序进行改进的依赖项，在该过程中，在创作模式下进行页面渲染会创建大量 `TemplatedResourceImpl` 对象。 (SITES-9350)


## Sling {#sling-6516}

* Experience Manager在启动时死锁。 (NPR-39832)
* 当Experience Manager的版本存储中存在许多虚路径时，Experience Manager无法启动。 (NPR-38955)


## 翻译项目 {#translation-6516}

* 在 `MicrosoftTranslationServiceImpl`，查询字符串参数 `Category` 不正确。 (NPR-39828)
* 创建翻译项目时，会显示错误 *主控页面资源不存在*;将不会创建翻译项目。 (NPR-39762)
* 无法在使用人工翻译连接器的翻译项目上设置到期日期。 (NPR-39593)

## 用户界面 {#ui-6516}

* 更改为较小分辨率时，不显示DatePicker，并且AM/PM选择不显示或可见更改。 (NPR-39948)
* 使用缩小js（JavaScript的最小化）时，它不会因解析错误而处理缩小。 (NPR-39650)
* 标记字段(`/libs/cq/gui/components/coral/common/form/tagfield`)与时间轴冲突。 (CQ-4350751)


## WCM {#wcm-6516}

* 转出预览操作不应列出要创建的页面。 (CQ-4266213, SITES-10355)

## 工作流 {#workflow-6516}

* 从中手动删除可编辑的工作流模型 `/conf` 将延迟运行时模型实例保留为不可编辑的模型。 (CQ-4349365)


## 安装 [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0要求 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以了解详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 6.5.16.0，在其中一个使用包管理器的创作实例上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.16.0包。 因此，在安装该包之前，您应该先创建 `crx-repository` 以防你需要把它卷回去。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。

1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能会间歇性地在任何浏览器上发生。

**自动安装**

可以使用两种不同的方法自动安装 [!DNL Experience Manager] 6.5.16.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹。 包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.16.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.16.0)` 在 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.14或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

有关在AEM Forms上安装Service Pack的说明，请参阅 [AEM Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安装用于GraphQL内容片段的Experience Manager索引包 {#install-aem-graphql-index-add-on-package}

使用GraphQL的客户应安装 [AEM内容片段(包含GraphQL索引包1.0.5)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip). 这样，用户就可以根据实际使用的功能添加所需的索引定义。

>[!NOTE]
>
>每个实例只能安装一次此包；无需随每个Service Pack重新安装它。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.16.0在 [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.16.0中，UberJar版本(6.5.15.0)与上一版本相同。


要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象可在Maven中央存储库中使用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，使用 `apis` 作为值，对于 `dependency` 标记。

## 已弃用功能 {#removed-deprecated-features}

以下是标记为已弃用的特性和功能列表 [!DNL Experience Manager] 6.5.7.0。功能在最初被标记为已弃用，之后在将来的版本中被删除。 提供了备用选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 专题 | 替换 |
|---|---|---|
| 集成 | 的 **[!UICONTROL AEM云服务选择加入]** 屏幕已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成在 [!DNL Experience Manager] 6.5.此集成支持Adobe Target Standard API。 API使用Adobe IMS和 [!DNL Adobe I/O Runtime]. 它支持AdobeLaunch在工具方面日益发挥的作用 [!DNL Experience Manager] 页面，则选择加入向导在功能上与此无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O Runtime] 集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR连接器已在 [!DNL Experience Manager] 6.5。 | 不适用 |

## 已知问题 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 请将您的GraphQL查询（可能已使用内容模型的自定义API名称）更新为改用内容模型的默认名称。

* GraphQL查询可以使用 `damAssetLucene` 而不是索引 `fragments` 索引。 这可能会导致GraphQL查询失败，或执行时间过长。

   为了纠正问题， `damAssetLucene` 必须配置以包含以下两个属性：

   * `contentFragment`
   * `model`

   在索引定义发生更改后，需要重新编入索引(`reindex` = `true`)。

   完成这些步骤后，GraphQL查询应该会执行得更快。

* 作为 [!DNL Microsoft®® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您升级 [!DNL Experience Manager] 从6.5.0 - 6.5.4到Java™ 11上最新的Service Pack的实例，您会看到 `RRD4JReporter` 例外 `error.log` 文件。 要停止例外，请重新启动实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装 [!DNL Experience Manager] 6.5.x.x:
   * “配置Adobe Target集成时， [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target时，会导致创建错误的选件类型。 Target会创建多个类型为“HTML”/源“Adobe Experience Manager Classic”的选件，而不是“体验片段”/源“Adobe Target Classic”的选件类型。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance中未找到维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance中未找到维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

* 在尝试移动/删除/发布内容片段或站点/页面时，当获取内容片段引用时会出现问题，因为后台查询失败；即，该功能不起作用。
要确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* 在AEM Forms中，POP3协议不适用于Microsoft® Office 365的电子邮件端点。
* 在JBoss® 7.1.4平台上，当用户安装AEM 6.5.16.0 Service Pack时， `adobe-livecycle-jboss.ear` 部署失败。

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.16.0中包含的OSGi包列表](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.16.0中包含的内容包列表](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是Adobe，并且需要访问，请联系您的客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

