---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作方法和详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 1077aeabacb1dbb489dbc7222c45da0a35b8cf16
workflow-type: tm+mt
source-wordcount: '3777'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2023年5月25日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包括的内容 [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0包括自2019年4月首次推出6.5以来发布的新功能、客户请求的关键增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) 日期 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的一些主要功能和改进如下：

* **搜索体验增强** - 您现在可以对搜索结果中显示的资源快速执行以下操作：
   * 创建工作流
   * 创建一个版本
   * 关联或取消关联资源

  您无需导航到资源的位置并查看其属性即可执行这些操作。
* **Dynamic Media _快照_**- 体验测试图像或 Dynamic Media URL，以查看不同图像修改器的输出，以及针对文件大小（使用 WebP 和 AVIF 交付）、网络带宽和设备像素比率的智能成像优化。请参阅 [Dynamic Media 快照。](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)
* **使用Dynamic Media进行DASH流**  — 为Dynamic Media视频交付中的自适应流推出了新协议(DASH - Dynamic Adaptive Streaming over HTTP)支持（已启用CMAF）。 现在向所有地区提供， [通过支持票证启用](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Experience Manager Sites和内容片段与Assets新一代Dynamic Media的集成** -Experience Manager Assetsas a Cloud Service的新一代Dynamic Media的用户现在可以通过Experience Manager Sites 6.5的内部部署或Managed Services实例，使用这些云托管资源进行创作和交付。

**AEM Forms**

* **[AEM 页面编辑器中的自适应表单](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**：您现在可以使用 AEM 页面编辑器快速创建多个表单并将其添加到您的 Sites 页面。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：
   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件来创建自适应表单。
   * 在AEM Sites编辑器中使用“自适应Forms向导”，以便您可以独立于任何Sites页面创建表单，同时让您能够在多个页面中重用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。
* **[Experience Manager Forms中的reCAPTCHA Enterprise支持](/help/forms/using/captcha-adaptive-forms.md)**：在Experience Manager Forms中增加了对reCAPTCHA Enterprise的支持，针对欺诈性活动和垃圾邮件提供了增强的保护，此外还有现有的Google reCAPTCHA v2支持。
* **[通过Experience Manager Forms支持面向政府的Adobe Acrobat Sign](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**：AEM Forms现在与面向政府的Adobe Acrobat Sign集成（符合FedRAMP）。 这种集成通过为政府关联帐户（政府部门和机构）提交自适应表单，为电子签名提供了高级的合规性和安全性。 与面向政府的Adobe Acrobat Sign集成使Adobe的合作伙伴和政府客户能够在Adaptive Forms中使用电子签名处理一些任务最关键和最敏感的业务线。 这一额外的安全层确保所有电子签名完全符合FedRAMP Moderate合规性，从而让Adobe的政府客户高枕无忧。
* **[启用Salesforce与Experience Manager Forms的集成以便进行数据交换](/help/forms/using/oauth2-client-credentials-flow-for-server-to-server-integration.md)**：使用OAuth 2.0客户端凭据流配置Experience Manager Forms与Salesforce应用程序之间的集成。 此功能实现了应用程序的安全且直接的身份验证和授权，并允许无缝通信而无需用户参与。
* **工作流引擎的优化和增强功能**：通过最大限度地减少工作流实例的数量来提高工作流引擎的性能。 除此之外 `COMPLETED` 和 `RUNNING` 状态值，工作流还支持三个新的状态值： `ABORTED`， `SUSPENDED`、和 `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* 如果同时发布40个以上的PDF， [!DNL Experience Manager] 停止响应并在一段时间内不可用。 (ASSETS-21789)
* 如果您以测试用户身份登录，则在单击某个资产的属性时，您将看不到与某个特定资产相关的资产。 (ASSETS-21648)
* 使用编辑资源时 `Desktop Actions`，如果您尝试一次签入五个以上的资产， `Limit Reached` 将显示错误并签出选定的资产。 (ASSETS-21121)
* 无法按收藏集中的名称对资源排序。 (ASSETS-20924)
* 无法在图像格式类型的资产上设置维度。 (ASSETS-20835)
* 共享链接时，“搜索/添加电子邮件地址”字段上的工具提示文本及其背景不显示相应的对比度。 (ASSETS-17347)
* 展开时 `Notifications`时，由于段落间距，文本无法正常显示。 (ASSETS-17345)
* 在收藏集中复制资产时， `Public Collection` 复选框未正确显示。 (ASSETS-17343)
* 元素在没有角色的情况下使用ARIA属性。 (ASSETS-17325，ASSETS-17323)
* 展开时链接不是描述性的 `Notifications`. (ASSETS-17283)
* 导航并展开 [!DNL Smart Crop] 按钮时，内容看起来像列表一样，但未标记为未排序列表。 因此，屏幕阅读器无法识别无序列表并将其阅读为纯文本。 (ASSETS-17247)
* 此 `Sort By` 标签不与其相应的下拉列表关联。 因此，屏幕阅读器无法识别下拉选项。 (ASSETS-17239)
* 当您尝试使用添加用户时，无法使用键盘Tab键或箭头键向前或向后移动 `Add user` 组合框。 (ASSETS-17233)
* 屏幕阅读器无法正确传达工作流步骤的信息(ASSETS-17285)。
* 当您导航到 `Saved Searches` 下拉框中，名称和角色均没有任何分配的标签。 (ASSETS-17329)
* 当您导航时 `Collection` 并将光标悬停在文本上 *成员*，则文本不会显示为已标记。 因此，屏幕阅读器无法识别标题文本并将其阅读为纯文本。 (ASSETS-17245)
* 无法访问 `View Settings` 选项，使用键盘上的向下或向上滚动键。 (ASSETS-17257)
* 无法为使用搜索筛选器找到的多个选定资产触发工作流。 (ASSETS-7689)
* 从搜索结果中选择资产（或多个资产）时，“相关”或“取消相关”选项不可见。 但是，该选项可用，否则。 (ASSETS-7679)
* 搜索过滤器面板在登录后仅打开一次，如果您退出搜索页面并重新运行搜索，则不会打开。 (ASSETS-7671)
* 共享链接时，电子邮件组合框不显示适当的对比度。 (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* 当Dynamic Media云配置已存在时，与Dynamic Media的连接已断开。 (ASSETS-23057)
* 提高了浏览包含大量Dynamic Media视频的文件夹时的性能，解决了在文件夹信息卡视图上加载失败的问题。 (ASSETS-23016)
* 从中删除预览令牌 `error.log` 用于从安全测试服务器请求安全内容。 (ASSETS-22685)
* PDF缩略图渲染添加阴影。 升级了Gibson lib版本4.0.1680232194，以解决PDF缩略图渲染问题。 (ASSETS-22585)
* Dynamic Media混合模式现在与New Relic Agent版本8.0.1 (ASSETS-22578)兼容。
* 现在，在Experience Manager上预览Dynamic Media文件时，会考虑Experience ManagerACL（访问控制列表）。 (ASSETS-21628)
* 当用户尝试使用向下箭头键或Tab键导航时，屏幕阅读器不会导航到隐藏元素。 (ASSETS-5617)
* 图像配置文件用户界面限制使用相同名称、相同维度或两者的智能裁剪。 (ASSETS-16997)
* 图像配置文件用户界面上的智能裁剪的默认宽度和高度现在设置为50像素。 (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* 已移动的标记是垃圾收集的，但仍由下的产品引用。 `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* 更新到AEM 6.5.15.0 Service Pack后，HTML5表单在具有IE兼容模式的Edge浏览器中无法正常运行或正确加载。 (FORMS-8526、FORMS-8523)
* 当用户应用AEM 6.5.16.0 Service Pack时，规则编辑器无法打开。 (FORMS-8290)
* 对数字框组件应用最大位数验证时，该操作将失败。 (FORMS-7938)
* 创建交互式通信语句时，PDF中的图表组件未正确生成。 (FORMS-7827、FORMS-8297)
* Java™垃圾收藏集无法清除Experience Manager Forms OSGi服务器上的旧生成栈。 (FORMS-8207)
* 当用户升级到Experience Manager6.5.16.0 Service Pack时，提交后缺少CRX元数据属性。 (FORMS-8205)
* 当用户禁用自适应表单中的日期选取器组件时，它仍可编辑。 (FORMS-7804)
* 在Experience Manager6.5.16.0 Forms Service Pack中，当用户尝试编辑策略集协调员时，Manager Document Publisher始终保持未选中状态。 (FORMS-7775、FORMS-8599)
* 当用户升级到Experience Manager6.5.16.0 Service Pack时，处理必须翻译的字符串的“GuideNode.externalize”方法停止工作。 (FORMS-7709)
* 在 `Assign task` 步骤，当用户选择“发送通知电子邮件”并调用工作流时，文本未正确显示在收到的电子邮件中。 接收问号而不是接收的电子邮件中的文本。 (FORMS-7675)
* 记录文档正在部分本地化。 (FORMS-7674、FORMS-7573)
* 用户无法编辑策略集，即使分配了特定权限也是如此。 (FORMS-7665)
* 当用户在 `forms-users` 组尝试创建表单，Experience Manager Forms实例崩溃。 (FORMS-7629)
* 当用户单击自适应表单上的“重置”、“保存”或“提交”按钮时，屏幕上不显示任何消息。 (FORMS-7524)
* 为了提高Experience Manager6.5.16.0 Service Pack上PDFG转换的性能，可以配置休眠间隔。 (FORMS-6752)
* 切换选项保持不变，但字段的可见性会更改，即使用户稍微拖动光标也是如此。 (FORMS-6728)
* 当用户升级到Experience Manager6.5.15.0 Service Pack时，重定向在Internet Explorer中呈现自适应表单时停止工作。 (FORMS-6725)
* 对于由Experience Manager设计者创建的PDF表单中的所有背景对象，PAC 2021工具会返回以下错误 `Path object not tagged`. (FORMS-6707)
* 当用户在收件箱中应用过滤器时，会抛出 `NullPointerException` 错误。 (FORMS-6706)
* 当用户导入包含引用片段的模板(.tds)文件时，Experience Manager设计器崩溃。 (FORMS-6702)
* 如果用户在Experience Manager Forms Designer 6.5中使用“输出”服务创建静态PDF，则会出现以下错误 `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* 当用户创建简单工作流并添加简单变量时， `set variable mapping` 出现错误。 (FORMS-5819)
* 当用户尝试使用输出服务生成PDF时，即使它标记为 `PDF/A-1a`，合规性检查，使用`Preflight` 服务失败。 (LC-3920837)
* 安装Experience Manager6.5.16.0 Service Pack后，Experience Manager设计器无法打开。 (LC-3921000)
* 当用户添加复选框和单选按钮时，未根据PDF标准生成Tag树的结构。 (LC-3920838)
* 如果用户通过输出服务使用字体的嵌入和子设置来生成静态PDF，则生成的PDF仅包含嵌入的字体。 (LC-3920963)
* 希伯来文本以RTL格式显示不正确。 (LC-3919632)
* 当用户升级到JBoss® Turnkey服务器上的Experience Manager6.5.16.0 Service Pack时，签名服务无法调用。 遇到的错误是： `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* 升级到Experience Manager6.5.14.0 Service Pack后，Workbench无法处理CRX节点从一个位置移动到另一个位置的操作。 错误发生于 `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* 当用户更新到Experience Manager6.5.16.0 Service Pack时， `Usage Rights` 无法应用。 (FORMS-7892)
* 当用户尝试生成PDF文档时，PDF/A-1b验证失败。 (FORMS-7615)
* 当用户单击 `Configure` 的选项 `Form Container` 组件时，浏览器将变得无响应。 (FORMS-7605)
* 当用户更新到Experience Manager Forms 6.5.16.0 Service Pack并尝试更改 `LicenseType` 到 `Production`时，更改不会反映出来。 (FORMS-7594)
* 当用户尝试使用包含以下PDF的LCA进程时 `Chinese Full Width Characters`，出现问题 `ValidateForm` 进程。 (FORMS-7464)
* 在Experience Manager Forms Designer中，XMLFM为基于XDP的模板生成具有不同纸张大小的ZPL输出，例如信纸、A4和A5。 (FORMS-7898)

## 集成{#integrations-6517}

* 将Adobe Target IMS配置转换为旧版云配置中的用户凭据时， `connectedWhen` 属性不会更改。 此问题使得所有调用都像配置仍基于IMS一样运行。 (CQ-4352810)
* 添加 `modifyProperties` 权限 `fd-cloudservice` Adobe Sign配置的系统用户。 (FORMS-6164)
* 通过与Adobe Target集成的Experience Manager，在创建AB测试活动时，它不会将与其关联的受众同步到Target。 (NPR-40085)

## Oak{#oak-6517}

从Service Pack 13及更高版本开始，影响持久性缓存的以下错误日志开始出现：

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

## Platform{#platform-6517}

* 在Experience ManagerTag Management用户界面(/aem/tags/)中，命名空间和标记按其创建顺序显示。 但是，当存在许多命名空间和标记时，查看和管理它们的功能会比较困难。 此问题是因为它们不能以任何其他方式排序。 (NPR-39620)
* 需要Google关闭版本更新，因为缩小作业无法用于某些客户端库。 (NPR-40043)

## [!DNL Sites]{#sites-6517}

* LinkCheckerTransformer中的性能下降。 (SITES-11661)
* 页面的语言副本未按预期更新。 (SITES-11191)
* 打开非营销活动页面调用 `targeteditor.html` 不必要的。 删除 `targeteditor` 必要时调用。 (SITES-12469)
* 无法为带有批注的页面创建活动副本。 (SITES-12154)
* 页面转出在Experience Manager6.5.16中不起作用。 (SITES-12008)
* 内存不足；由于以下原因，垃圾收集活动频繁 `NotificationManagerImpl`. `NotificationManager` 捆绑包升级到Experience Manager6.5。 (SITES-11440)
* 修复了阻止Service Pack 17的WCM IT测试。 (SITES-13089)
* 在servlet上检索站点引用失败。 (SITES-10901)

### [!DNL Sites]  — 管理员用户界面{#sites-adminui-6517}

* 无法关闭缩略图图像选择器的预览窗口。 (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* 用于连接到Polaris服务对象（URL、凭据、回调等）的配置。 (SITES-12149)
* 使用情况 `SemanticDataType.REFERENCE` 应支持“Remote-Asset-IDs”。 (SITES-12127)
* 将Polaris资产选择器集成到内容片段编辑器中。 (SITES-12125)
* 访问元数据服务端点需要必需的http标头。 (SITES-13068)
* GraphQL 6.5的实施与Cloud Service（主要）不尽相同；已确定的问题已得到修复。 (SITES-13096)
* GraphQL分页/排序和混合筛选应在Experience Manager6.5/AMS上可用。 (SITES-9154)

### [!DNL Sites] - 核心组件{#sites-core-components-6517}

* 属性 `cq-msm-lockable` Foundation页面组件中的重定向值错误。 (SITES-10904)
* 远程资产选取器始终重定向到IMS暂存环境。 (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* 在导出到Adobe Target时，在体验片段中选择外部化器配置会导致发送错误的外部化URL。 (SITES-12402)
* 删除非包含性条款；应用包含性条款准则。 (SITES-11244)

### [!DNL Sites] - 页面编辑器{#sites-pageeditor-6517}

* Experience Manager内容查找器侧边栏中的轮播集未显示任何缩略图。 (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` 为虚拟路径提供时会占用大量CPU，从而导致拒绝服务。 (NPR-40338)

## 翻译项目{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* 用户未配置非必填字段时不会创建语言副本。 (NPR-40036)

## 用户界面{#ui-6517}

* “页面属性”中的“取消”按钮处于不活动状态；它应该会将您转到“站点管理员”用户界面。 (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## 工作流{#workflow-6517}

* 工作流控制台更改。 (NPR-40502)
* `SegmentNotfound errors` 在生产创作实例的日志中，由类中未关闭的资源解析程序导致 `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* 已关闭的未关闭 `ResourceResolver` 记录异常。 (ASSETS-22495)
* Experience Manager创作在PSD/PDF大量内容时崩溃 `DocumentAncestors` 元数据属性已上传。 (ASSETS-22966)
* 类中的会话泄漏 `InboxSharingCache` 替换为 `user-reader-service`. (CQ-4352513)
* 当“工作流发起者参与者选择器”步骤列出参与者步骤的用户和组时，将显示不完整的用户和组列表。 当一个组同时也是另一个组的成员，则会发生此问题。 (NPR-40055)
* 增强了工作流清除功能。 (NPR-40459)

## 安装 [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0需要 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以获取详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上获取Service Pack下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 使用包管理器对其中一个Author实例执行6.5.17.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.17.0程序包。 因此，在安装该包之前，您应该创建 `crx-repository` 以防你必须把它倒回去。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装服务包 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。

1. 从以下位置下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，将现有连接器替换为安装文件夹中提供的新二进制文件，然后重新启动实例。 参见 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack期间，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题出现在以下位置 [!DNL Safari] 浏览器，但可能间歇性地在任何浏览器上出现。

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL Experience Manager] 6.5.17.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.17.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.17.0)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.15或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装此Service Pack的说明，请参阅 [Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装 [GraphQL索引包1.1.1的Experience Manager内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

这样做可让您根据它们实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

UberJar用于 [!DNL Experience Manager] 6.5.17.0可从以下网站获取： [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件在Maven中央存储库而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，替换为 `apis` 作为值，用于 `dependency` 标记之前。

## 已弃用功能{#removed-deprecated-features}

以下为标记为已弃用的特性和功能的列表 [!DNL Experience Manager] 6.5.7.0。这些功能最初标记为已弃用，但以后会在以后的版本中删除。 提供了替代选项。

查看是否在部署中使用某个功能或功能。 此外，计划更改实施以使用替代选项。

| 区域 | 专题 | 替换 |
|---|---|---|
| 集成 | 屏幕 **[!UICONTROL Experience Manager Cloud Services选择加入]** 已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成更新于 [!DNL Experience Manager] 6.5.该集成支持Adobe Target标准API。 该API通过Adobe IMS进行身份验证，并且 [!DNL Adobe I/O Runtime]. 它支持AdobeLaunch在检测方面发挥越来越大的作用 [!DNL Experience Manager] 页面进行分析和个性化时，选择加入向导在功能上无关紧要。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O Runtime] 通过各自的集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 用于Microsoft®SharePoint 2010和Microsoft®SharePoint 2013的AdobeJCR连接器已弃用 [!DNL Experience Manager] 6.5. | 不适用 |

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* 将可能已使用内容模型的自定义API名称的GraphQL查询更新为改用内容模型的默认名称。

* GraphQL查询可以使用 `damAssetLucene` 索引而非 `fragments` 索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  要更正此问题， `damAssetLucene` 必须配置为包含以下两个属性：

   * `contentFragment`
   * `model`

  更改索引定义后，需要重新索引(`reindex` = `true`)。

  执行这些步骤后，GraphQL查询应该可以更快地执行。

* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1]， [!DNL Microsoft® Windows Server 2019] 不支持的全包安装 [!DNL Experience Manager Forms 6.5.10.0].

* 如果您升级 [!DNL Experience Manager] 从6.5.0 - 6.5.4到Java™ 11上最新Service Pack的实例，请参见 `RRD4JReporter` 中的例外 `error.log` 文件。 要停止异常，请重新启动您的实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在以下位置重命名层次结构中的文件夹： [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题不会在中更新 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户选择在自适应表单中首次配置字段时，保存配置的选项未显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 安装过程中可能会显示以下错误和警告消息 [!DNL Experience Manager] 6.5.x.x：
   * “当在中配置Adobe Target集成时 [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance中未找到维护窗口。
   * 当使用SUM、MAX和MIN等聚合函数时，Adaptive Form服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance未找到维护窗口。
   * 通过Shoppable Banner查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题，因为后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 在JBoss® 7.1.4平台上，当用户安装Experience Manager6.5.16.0或更高版本Service Pack时， `adobe-livecycle-jboss.ear` 部署失败。
* WebLogic JEE服务器不支持高于1.8.0_281的JDK版本。
* 从AEM 6.5.15开始，Rhino JavaScript引擎由 ```org.apache.servicemix.bundles.rhino``` 捆绑包具有新的提升行为。 使用严格模式(```use strict;```)必须正确声明其变量，否则它们将不会执行，而是会引发运行时错误。

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了中包含的OSGi包和内容包 [!DNL Experience Manager] 6.5.17.0： <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.17.0中包含的OSGi包列表](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.17.0中包含的内容包列表](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)
