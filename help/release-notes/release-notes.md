---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找发行信息、新增功能、安装操作方法，以及 [!DNL Adobe Experience Manager] 6.5。
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 966a3ea6b8cb9b42e21f8e3eb3fee1c7ca93cf51
workflow-type: tm+mt
source-wordcount: '2603'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2022 年 8 月 25 日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包含的内容 [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0包括自2019年4月6.5版首次发布以来发布的新增功能、客户请求的关键增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) on [!DNL Experience Manager] 6.5。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* 无法添加或查看PDF文件的标记。 (NPR-38452)
* 配置连接的资产、保存配置、重新打开配置页面并测试已保存的配置时，测试连接会失败。 (NPR-38507)
* 无法将具有数字用户ID的用户添加到收藏集。 (NPR-38538)
* Experience Manager无法处理在创作实例上安装的FFmpeg。 (NPR-38568)
* PDF处理失败，具有 `NoClassDefFoundError` 错误消息。 (NPR-38741)
* 为创建资产报表时，自定义列下的添加按钮无法正确显示 `de_DE` 区域设置。 (ASSETS-10641)
* 当您将重复资产上传到数字资产管理存储库，并且Experience Manager检测到并提供了删除重复资产的选项时，原始资产也会从存储库中删除。 (ASSETS-10826)
* 在多字段中指定特殊字符时，Experience Manager无法正确保存文件夹元数据。 (ASSETS-10721)
* 在单击 **[!UICONTROL 保存并关闭]** 两次。 (ASSETS-12040)
* 屏幕阅读器仅会朗读 `Relate` 按钮。 但是， `Relate` 按钮还包含一个子菜单，可以展开和折叠。 (ASSETS-6938)
* 必需的ARIA（可访问的富互联网应用程序）属性 `aria-expanded` 表示 `role="combo box"` 缺少。 (ASSETS-6928)
* 在“卡片”视图的主文件导航区域中，文本内容 **[!UICONTROL 排序依据]** 相对于其背景颜色，至少没有4.5:1的对比度。 (ASSETS-6926)
* Experience Manager无法识别 **[!UICONTROL 选择工作流模型]** 下拉列表作为创建工作流模型时的必填字段。 (ASSETS-6871)

>[!NOTE]
>
>自2022年9月1日起，新的Experience Manager Assets内部部署客户将无法使用智能内容服务。 对已启用此功能的现有内部部署和Adobe Managed Services客户没有影响。

### [!DNL Dynamic Media] {#dynamic-media-6514}

* 在Experience Manager中为Dynamic Media Classic用户添加对密码重置的支持。 (ASSETS-10298)
* 为具有透明背景的图像生成的智能裁剪具有白色背景。 (ASSETS-13148)
* Dynamic Media不会为EPS文件生成缩略图。 (ASSETS-10959)
* 由于缺少上传参数，资产无法上传到Dynamic Media帐户。 (ASSETS-13165)
* 允许将名称超过127个字符的资产上传到Dynamic Media。 (ASSETS-9991)
* 在Experience Manager6.5.14.0上启用适用于Dynamic Media查看器的JavaScript ES6(ECMAScript 6)。 (NPR-38393)
* 在Dynamic Media中配置选项 **[!UICONTROL 常规设置]** 和 **[!UICONTROL 发布设置]** 非管理员用户不应访问。 (ASSETS-8628)
* Dynamic Media **[!UICONTROL 常规设置]** 页面未正确显示已配置的上载参数。 (ASSETS-10245)
* Experience Manager用户界面不显示任何失败消息，以防集创建/更新失败。 (ASSETS-10264)
* 无法将保存的策略应用于可编辑模板的其中一个容器，以便添加Dynamic Media组件。 (ASSETS-11044)
* 对作业句柄错误的资产运行Dynamic Media重新处理资产工作流后，资产未上传到Dynamic Media帐户。 (ASSETS-12084, ASSETS-9877)
* 屏幕阅读器用户受 `title` 属性未提供 `<frame>` 和 `<iframe>` 在 **[!UICONTROL 搜索类型]** 对话框。 (ASSETS-5483)
* 在屏幕阅读器中，相关且有意义 `alt=` 值应当为下面存在的多个图像提供 **[!UICONTROL 资产]** 标题。 (ASSETS-5644)
* 屏幕阅读器未读取 **[!UICONTROL 静音]** 和 **[!UICONTROL 取消静音]** 按钮。 (ASSETS-10169)

## 商务 {#commerce-6514}

* 商务产品未使用列标题进行排序，并且它使用 _远程_ 排序模式；而是应使用带有的列标题对商务产品进行排序 _本地_ 排序模式。 (CQ-4343750、NPR-38498)



## [!DNL Forms] {#forms-6514}

>[!NOTE]
>
> 的修复 [!DNL Experience Manager] Forms在计划后一周通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack版本。

## 集成 {#integrations-6514}

* 启用JavaScript ES6（ECMAScript6模式或更高模式）编译支持，以缩小 `/libs/cq/analytics/widgets.js` 库。 (NPR-38433)
* 启用JavaScript ES6（ESMAScript6模式或更高模式）编译支持，以缩小 `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` 库。 (NPR-38435)
* 中的内容越多 `/content/campaigns`，则调用的时间越长 `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`)会在您打开页面编辑器时使用。 (NPR-38663)

## 平台 {#platform-6514}

* 无法登录到包管理器来部署更新。 (NPR-38646)
* 在资产标记选取器用户界面中，标记按创建顺序显示。 但是，当标记数量很多时，查看和管理标记会比较困难，因为无法对标记进行排序。 (CQ-4344279)
* 当用户被管理员或任何其他人模拟为使用 **[!UICONTROL 模拟为]** 字段。 (CQ-4345288)
* 在智能收藏集中，使用保存的搜索进行筛选时，会显示所有资产。 (CQ-4345326)
* 显示的选定资产计数不正确 **[!UICONTROL 添加到收藏集]** when **[!UICONTROL 全选]** 中。 (CQ-4345424)
* 使用 **[!UICONTROL 模拟为]** 字段。 (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* 将Experience Manager从6.5.12.0升级到6.5.13.0时发生意外路径删除。 (NPR-38532)

### 辅助功能 {#access-6514}

* 在Experience Manager Sites中，当您将 **[!UICONTROL 切换显示格式并调整显示设置]** 按钮，然后选择 **[!UICONTROL 列表视图]**, **[!UICONTROL 拖放]** 按钮缺少可访问的名称。 (SITES-2863、NPR-38760)
* 屏幕阅读器必须读出可访问的名称，例如 `Show description for Archive` 或 `Show description for mini shopping cart`. 但是，当前可访问的名称将宣布为 `Info Circle button show description` 表示 _全部_ 工具提示信息按钮。 (SITES-3104)
* 改进了中没有inlineEditing或dropTarget功能的组件的撤消 `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 样式系统下拉列表可能位于页面顶部，而不是组件的上下文内容(对于使用 `cq:editConfig` “afteredit:REFRESH_PAGE”。 (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* 文本组件在添加到嵌套布局容器时未对齐。 (NPR-38193)
* 当组件没有样式系统配置时，会显示空样式选项卡。 现在，当没有配置时，选项卡处于隐藏状态。 (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* 资产 `useLegacyResponsiveBehaviour` 仅在经过身份验证后才可正常工作。 (NPR-37996)
* 将jquery-ui升级到最新版本会导致编辑器损坏。 (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* 首次加载内容片段时，内容片段枚举字段验证会出现问题。 (SITES-7140)
* 需要在内容片段编辑器的富文本编辑器中添加Campaign个性化字段。 (NPR-38526)
* 在内容片段编辑器中通过调度程序创建或编辑新内容片段时，不会保存内容片段模型。 此外，内容片段编辑器未关闭，并且浏览器日志中会显示错误。 (NPR-38691)
* 永久查询验证错误。 (NPR-38523)
* 在“内容片段”对话框的 **[!UICONTROL 属性]**, **[!UICONTROL 内容片段]** 字段不会保留“选择”弹出窗口中的保存路径。 (NPR-38632)
* 创建内容片段模型并添加下拉类型的枚举字段时，将正确验证 _`is required`_失败。 (NPR-38237)

### 核心组件 {#sites-corecomponents-6514}

* 新的页面电子邮件组件在编辑时不应强制您进入经典用户界面 `/etc`. (NPR-38648)

### 页面编辑器 {#sites-pageeditor-6514}

* 用户无法将组件调整到所需的列数。 (NPR-38688)

### 模板编辑器 {#sites-templateeditor-6514}

* 缺少 **[!UICONTROL 删除]** 和 **[!UICONTROL 剪切]** 可编辑模板中的菜单栏 `cq:actions` 属性已自定义。 (NPR-38521)
* 如果组件包含其他组件，则无法删除模板结构中的组件，因为 **[!UICONTROL 删除]** 按钮。 (NPR-38585)

## Sling {#sling-6514}

* 由于模块中内存泄漏，生产上的打开文件数量有所增加 `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`，版本1.0.20。 (NPR-38288)
* 在Experience Manager中，从 **[!UICONTROL 操作]** > **[!UICONTROL 诊断]**，则在选择 **[!UICONTROL 下载状态ZIP]** > **[!UICONTROL 下载]**. (NPR-38514)

## 翻译项目 {#translation-6514}

* 当 `isDeep` 属性设置为 `false`. (NPR-38531)

## 用户界面 {#ui-6514}

* 使用 **[!UICONTROL 全选]** > **[!UICONTROL 快速发布]**，则Experience Manager不会发布所有资产或显示中将发布的资产数量 **[!UICONTROL 卡片]** 查看或查看 **[!UICONTROL 列表]** 中。 (NPR-38546)
* 显示的选定资产计数不正确 **[!UICONTROL 添加到收藏集]** in **[!UICONTROL 全选]** 案例。 (NPR-38633)
* 仍可以将禁用的用户添加到收藏集和项目。 (NPR-38651)
* 在不保存搜索表单的情况下删除过滤器会创建错误。 (NPR-38698)
* 用户的会话无法获取 `ModifiableValueMap` 群组实例，以建立直接群组成员资格。 (NPR-38710)

## 工作流 {#workflow-6514}

* 启用JavaScript ES6（ESMAScript6模式或更高模式）编译支持，以缩小 `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` 库。 (NPR-38304)
* 运行工作流并完成流程步骤后，会多次重复同一注释。 (NPR-38364)

## 安装 [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0要求 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以了解详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 6.5.14.0，在其中一个使用包管理器的创作实例上。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe不建议删除或卸载 [!DNL Experience Manager] 6.5.14.0包。 <!-- UPDATE FOR EACH NEW RELEASE -->

### 在上安装Service Pack [!DNL Experience Manager] 6.5 {#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。

1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能会间歇性地在任何浏览器上发生。

**自动安装**

可以使用两种不同的方法自动安装 [!DNL Experience Manager] 6.5.14.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹。 包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.14.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.14.0)` 在 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.12或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- NPR-38747 -->

### 安装 [!DNL Experience Manager] Forms附加组件包 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您没有使用 [!DNL Experience Manager] Forms。

的修复 [!DNL Experience Manager] Forms在计划后一周通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack版本。

1. 确保您已安装 [!DNL Experience Manager] Service Pack。
1. 下载适用于您的操作系统的 [AEM Forms 发行版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)中列出的相应 Forms 附加组件包。
1. 按照 [安装AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. 如果您在Experience Manager6.5 Forms中使用字母，请安装 [最新的AEMFD兼容包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### 安装 [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在 JEE 上使用 AEM Forms，请跳过。的修复 [!DNL Experience Manager] JEE上的Forms通过单独的安装程序交付。

有关为 [!DNL Experience Manager] Forms（在JEE上）和部署后配置中，请参阅 [发行说明](jee-patch-installer-65.md).

>[!NOTE]
>
>安装的累积安装程序之后 [!DNL Experience Manager] Forms，安装最新的Forms附加组件包，从 `crx-repository\install` 文件夹，然后重新启动服务器。

### UberJar {#uber-jar}

UberJar [!DNL Experience Manager] 6.5.13.0在 [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>在Experience Manager6.5.14.0中，请注意UberJar版本(6.5.13.0)与上一版本相同。

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相关对象可在Maven中央存储库中使用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，使用 `apis` 作为值，对于 `dependency` 标记。

## 已弃用功能 {#removed-deprecated-features}

以下是标记为已弃用的特性和功能列表 [!DNL Experience Manager] 6.5.7.0。功能在最初被标记为已弃用，之后在将来的版本中被删除。 提供了备用选项。

查看您在部署中是否使用了功能。 此外，还计划更改实施以使用替代选项。

| 区域 | 功能 | 替换 |
|---|---|---|
| 集成 | 的 **[!UICONTROL AEM云服务选择加入]** 屏幕已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] 集成在 [!DNL Experience Manager] 6.5.此集成支持Adobe Target Standard API。 API使用Adobe IMS和 [!DNL Adobe I/O Runtime]. 它支持AdobeLaunch在工具方面日益发挥的作用 [!DNL Experience Manager] 页面，则选择加入向导在功能上与此无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O Runtime] 集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR连接器已在 [!DNL Experience Manager] 6.5。 | 不适用 |

## 已知问题 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [AEM包含GraphQL索引包1.0.3的内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* 作为 [!DNL Microsoft® Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 10或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装 [!DNL Experience Manager] 6.5.x.x:
   * “配置Adobe Target集成时， [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target时，会导致创建错误的选件类型。 Target会创建多个类型为“HTML”/源“Adobe Experience Manager Classic”的选件，而不是“体验片段”/源“Adobe Target Classic”的选件类型。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
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

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager6.5.14.0中包含的OSGi包列表](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.14.0中包含的内容包列表](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

