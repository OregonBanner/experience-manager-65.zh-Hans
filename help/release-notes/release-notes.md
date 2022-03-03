---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5发行说明，其中概述了发行信息、新增功能、安装方式和详细的更改列表。”'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: b1e38323fbbb268de76067eb85596119b44221c2
workflow-type: tm+mt
source-wordcount: '2662'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.12.0 |
| 类型 | Service Pack 版本 |
| 日期 | 2022 年 2 月 24 日 |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## 中包含的内容 [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.12.0包括自2019年4月6.5版发布以来发布的新功能、客户请求的关键增强功能以及性能、稳定性和安全性改进。 Service Pack安装在 [!DNL Adobe Experience Manager] 6.5。

中引入的主要功能和增强功能 [!DNL Adobe Experience Manager] 6.5.12.0是：

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行更新、删除、重命名和移动操作。更新（会出现一些延迟）将在站点部署中自动提供(NPR-37816)。

* 默认情况下，现在可以将Live Copy源推送到多个Live Copy，而无需Blueprint配置(CQ-4259951)。
* 正在进行的异步操作的状态现在显示在用户界面中，以帮助防止用户意外触发同一路径上的多个异步操作(NPR-37611)。
* 为Analytics 2.0 API提供了基于IMS的身份验证支持(CQ-4285474、NPR-37803、NPR-37701、NPR-37702、NPR-37703)。
* 对JSON选件类型体验片段的API支持(NPR-37796)。
* 现在为IMS中的删除选件（体验片段API）提供了选件请求(NPR-37668)。
* 内置存储库(Apache Jackrabbit Oak)仍保持为1.22.9。

以下是 [!DNL Experience Manager] 6.5.12.0版本。

### [!DNL Sites] {#sites-65120}

中修复了以下问题 [!DNL Sites]:

* 内容片段的布局属性会被损坏，因为基本和高级选项卡左侧没有边距(SITES-4484)。
* 关闭在不同站点页面上引用的内容片段上的横幅的选项不起作用。 此横幅会告知用户内容片段是在一个或多个页面上引用的(SITES-4173)。
* 复选框在“还原继承”对话框中未对齐(SITES-3514)。
* we-retail和wknd站点上的模板页面已损坏，因为组件不加载且结构选项不可用，因为pageinfo.json servlet在LaunchManagerImpl.getLaunchStream(SITES-3489)上卡住。
* 从创作环境到发布环境的用户节点发布不起作用(NPR-38005)。
* 尝试使用已编辑的模板创建体验片段时，不会显示对初始页面属性所做的编辑(NPR-37962)。
* Experience Manager上的页面移动操作缓慢(NPR-37961)。
* 体验片段翻译不会更新对语言副本路径的引用(NPR-37953)。
* 没有复制权限的用户即使未激活页面，也无法删除或移动页面(NPR-37936)。
* 服务器上观察到随机org.apache.felix.metatype错误(NPR-37935)。
* 站点管理员接触用户界面中的引用无法正确显示传入链接(NPR-37934)。
* 在翻译作业中选择页面时，无法使用用于添加新页面或资产的启动路径(NPR-37912)。
* 提升启动项时，在体验片段中添加的列表组件中的引用页面不会更新到目标页面(NPR-37886)。
* 创作环境存在用户界面问题，例如“编辑模式”页面标题未居中，并且在策略编辑器中允许选择组件：“组”复选框占用容器的整个宽度，因此标签将呈现在下一行中(NPR-37878)。
* [平台] commons-httpclient的metatype.xml文件中的xmlns:metatype的版本号为“http://www.osgi.org/xmlns/metatype/v1.0.0”，而不是“http://www.osgi.org/xmlns/metatype/v1.2.0”(NPR-37865)。
* 尝试访问页面时，发现错误并且页面无法移动(NPR-37864)。
* [富文本编辑器] 在富文本编辑器中将图像作为列表项添加时，图像未在经典用户界面中呈现(NPR-37835)。
* 在对话框中使用标记字段时，作者能够应用配置的根路径以外的标记(NPR-37834)。
* 多字段在布局容器中无法正确呈现，并且会出错(NPR-37811)。
* 在移动布局中无法尝试在页面编辑器中调整组件布局大小(NPR-37805)。
* 体验片段翻译不会更新对语言副本路径的循环引用(NPR-37745)。
* 在页面属性中使用cq-msm-lockable富文本字段不会禁用转出页面时的字段，并且作者可以修改该字段(NPR-37714)。
* 激活体验片段时，发布者会向Dispatcher发送许多激活请求(NPR-37707)。
* 拓扑更改时，用于资产处理的Sling作业会重置，从而导致拓扑更改时正在进行的作业被忽略(NPR-37706)。
* 使用MacOS导出网站和资产URL的用户不会将引号、叉号和短划线导出到CSV(NPR-37698)。
* 运行react SPA页面时，SPA页面模板中的布局容器无法注册模板策略中定义的自定义CSS类(NPR-37697)。
* 当用户在容器中具有背景的体验片段上选择定位时，背景图像不可见(NPR-37662)。
* 体验片段上的翻译作业无法翻译该体验片段上的所有组件(NPR-37660)。
* 翻译体验片段和包含体验片段的页面时，不会更新体验片段链接中的启动路径(NPR-37659)。
* 上传文件时，文件上传小组件不显示文件名，并且保存了对话框(NPR-37634)。
* 如果移动包含资产的文件夹，则资产的计划激活（发布）不会在计划时间触发(NPR-37621)。
* [平台] 外部链接检查器功能板无法在 [!DNL Adobe Experience Manager] WCM(NPR-37614)。
* 在编辑器中编辑标记时，如果标记名称中使用大写字母，则内容片段编辑器无法正常工作(NPR-37601)。
* 经典用户界面编辑器在触屏用户界面的比较视图中未显示为标记(NPR-37588)。
* 在将体验片段添加到翻译作业时记录间歇性500错误(NPR-37587)。
* 即使在禁用的日期选取器上，作者也能够选择和使用日期选取器日期(NPR-37583)。
* [基础] 在触屏用户界面的组件对话框结构中，作者无法在数字字段资源类型中输入一些小数值(NPR-37059)。
* 安装以前的Service Pack时，会删除libs文件夹中的路径(NPR-36815)。
* [商务] 停用根文件夹不会更改中子产品的停用状态 [!DNL Experience Manager Commerce] 控制台；此外，在用户界面中错误地显示停用时根文件夹的子文件夹计数(CQ-4338261)。
* [本地化工作流程] 列自定义和品牌自定义的内容未在“管理控制”对话框中本地化 — 在 [!DNL Adobe Experience Manager] 收件箱(CQ-4334864)。
* [社区] 群组成员的表中的内容不可点击(CQ-4334404)。
* [Oak] 冷待同步进程不工作且正在记录错误(CQ-4333868)。
* [Platform Foundation UI] [!DNL Experience Manager] 当用户选择 [!DNL Adobe Experience Manager] 图标(CQ-4317409)。

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

中修复了以下问题 [!DNL Assets]:

* 添加资产或文件夹(包含 `single quote` 名称中)，引用路径失败，并导致异常(NPR-37712)。
* 向资产添加水印时，水印始终以黑色显示，与用户定义的颜色无关(NPR-37720)。
* 使用连接的资产时，即使非管理员用户被限制访问DAM存储库，该用户仍能够搜索资产(NPR-37644)。
* 使用批量编辑更新资产元数据时，不会保存应用于下拉字段的更改，并将其重置为默认值(NPR-37345)。
* 删除文件夹的时间过长，这会影响整体性能(NPR-37107)。
* 在元数据架构中应用规则时，用户无法查看下拉菜单的完整值 `Field Value` 和 `Field Choices` 值大于文本框(CQ-4338074)。
* 升级到版本6.5.10.0后，资产属性页面会反映不必要的HTML渲染消息(CQ-4336994)。
* 在中对资产进行排序 `List View` 无效工作(CQ-4335298)。
* 使用共享链接共享资产时，会将资产下载到不同的文件夹中(CQ-4335000)。
* 验证 [!DNL Experience Manager] `Inbox` 设置， `Share` 和 `Out of office` 选项卡反映未翻译的内容(CQ-4334858)。

* 以下修复与资产属性中的级联元数据相关。
   * 强制下拉列表反映了多值字段中每个选择的多个错误消息(NPR-37859)。
   * 对于从属的不可编辑字段，只会保存最后选择的父字段(NPR-37858)。
   * 从属下拉列表（多值字段）间歇性地反映选定父下拉列表的默认值(NPR-37791)。


### [!DNL Dynamic Media] {#dynamic-media-65120}

中修复了以下问题 [!DNL Dynamic Media]:

* 包含 `renditions` 文件夹名称中的不同步 `Dynamic Media` (CQ-4338428)。
* 在中创建图像预设时 `tiff` 格式，但会创建预设，但格式会更改为 `jpeg` (CQ-4335985)。
* 修改 `Progressive JPEG Scan` 值时，下拉菜单值始终将重置为 `auto`(CQ-4335971)。
* 对于 `mxf` 资产属性页面上的视频(CQ-4335499)。
* 重新处理视频资产时，将从发布服务器取消发布AVS（自适应视频集）和视频演绎版(CQ-4335461)。
* 生成的PDF缩略图与实际PDF的第一页不同。 缩略图中缺少图像的某些部分(CQ-4315554)。
* 如果 `companyName` 和 `companyRoot` 不同(CQ-4339896)。

### 工作流 {#workflows-65120}

* 如果对收件箱项目应用过滤器，则滚动操作无法按预期工作(CQ-4333594)。


### [!DNL Forms] {#forms-65120}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] 在计划的 [!DNL Experience Manager] Service Pack 发行日期后一周发布附加组件包。


<!--

**Adaptive Forms**

* Accessibility – When you set the `Wizard` layout for a panel in an adaptive form, the navigation buttons do not have Aria labels and role (NPR-37613).

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* Differences in the value of the `Switch` component on the user interface and in the backend (NPR-37268).

* When you use the keyboard keys to navigate to the `Submit` option and press the `Enter` key, you can submit the adaptive form multiple times (CQ-4333993).

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Document Services**

* An error displays while using the Assembler service (NPR-37606):

  ```TXT
    500 Internal Server Error
  ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

  ```TXT
    com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
  ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**HTML5 Forms**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Letters**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Forms Workflow**

* In case of embedded container workflow, you get multiple workflow completion emails even after selecting the `Notify on Complete of Container Workflow` option (NPR-37280).

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

**Issues fixed in AEM Forms 6.5.11.1**

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (JEE Only) Critical security vulnerabilities (CVE-2021-44228 and CVE-2021-45046) reported for Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.

-->


有关安全更新的信息，请参阅 [[!DNL Experience Manager] 安全公告页面](https://helpx.adobe.com/security/products/experience-manager.html).

## 安装 6.5.12.0 {#install}

**设置要求和更多信息**

* Experience Manager6.5.12.0需要Experience Manager6.5。请参阅 [升级文档](/help/sites-deploying/upgrade.md) 以了解详细说明。
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装Experience Manager6.5.12.0。

>[!NOTE]
>
>Adobe不建议删除或卸载 [!DNL Adobe Experience Manager] 6.5.12.0包。

### 安装Service Pack {#install-service-pack}

在 [!DNL Adobe Experience Manager] 6.5实例，请执行以下步骤：

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 Adobe建议，如果实例的当前正常运行时间较高，则重新启动。

1. 在安装之前，请拍摄快照或对 [!DNL Experience Manager] 实例。

1. 从下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. 打开包管理器，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包并单击 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack时，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 请等待与卸载更新程序包相关的特定日志，然后才能确保安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能会间歇性地在任何浏览器上发生。

**自动安装**

有两种方法可自动安装 [!DNL Experience Manager] 6.5.12.0在工作实例上：

A.将包裹放入 `../crx-quickstart/install` 文件夹。 包会自动安装。

B.使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0不支持Bootstrap安装。

**验证安装**

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.12.0)` 在 [!UICONTROL 已安装的产品].

1. 所有OSGi包都 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.3或更高版本(使用Web控制台： `/system/console/bundles`)。

要了解经认证可与此版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

适用于Experience Manager6.5.12.0的UberJar可在 [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
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
| 集成 | 的 **[!UICONTROL AEM云服务选择加入]** 屏幕已弃用，因为 [!DNL Experience Manager] 和 [!DNL Adobe Target] Experience Manager6.5中更新了集成。该集成支持Adobe Target Standard API。 该API使用通过Adobe IMS进行身份验证，并且 [!DNL Adobe I/O] 并支持Launch在仪器上发挥越来越大的Adobe作用 [!DNL Experience Manager] 页面，则选择加入向导在功能上与此无关。 | 配置系统连接、Adobe IMS身份验证和 [!DNL Adobe I/O] 集成 [!DNL Experience Manager] 云服务。 |
| 连接器 | 适用于Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR Connector已在Experience Manager6.5中弃用。 | 不适用 |

## 已知问题 {#known-issues}

* 安装AEM 6.5 Service Pack 12并尝试下载状态ZIP文件时，Experience Manager会下载损坏的文件。

   要避免出现此问题，请在AEM实例上下载并安装以下两个项目 **之前** 下载状态ZIP文件：

   * 以下 [修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip)

   * the [AEM Sites SEO索引包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.4.zip)

* 作为 [!DNL Microsoft Windows Server 2019] 不支持 [!DNL MySQL 5.7] 和 [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] 不支持的turnkey安装 [!DNL AEM Forms 6.5.10.0].

* 如果您要升级 [!DNL Experience Manager] 实例从6.5版到6.5.10.0版，您可以查看 `RRD4JReporter` 例外 `error.log` 文件。 要解决此问题，请重新启动实例。

* 如果安装 [!DNL Experience Manager] 6.5 Service Pack 10或上的先前Service Pack [!DNL Experience Manager] 6.5，资产自定义工作流模型的运行时副本(在 `/var/workflow/models/dam`)。
要检索运行时副本，Adobe建议使用HTTP API将自定义工作流模型的设计时间副本与其运行时副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 用户可以在 [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题在 [!DNL Brand Portal] 直到重新发布根文件夹。

* 当用户首次选择在自适应表单中配置字段时，用于保存配置的选项不会显示在属性浏览器中。 选择在同一编辑器中配置自适应表单的其他一些字段可解决此问题。

* 在安装Experience Manager6.5.x.x期间，可能会显示以下错误和警告消息：
   * “当使用Target Standard API（IMS身份验证）在Experience Manager中配置Adobe Target集成时，将体验片段导出到Target会导致创建错误的选件类型。 而不是“体验片段”/源“Adobe Experience Manager”类型，Target 会创建若干个“HTML”/源“Adobe Target Classic”类型的选件。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 使用聚合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在 granite/operations/maintenance 中未发现维护窗口。
   * 通过购物横幅查看器预览资产时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待注册更改完成取消注册时超时。

* 在尝试移动/删除/发布内容片段或站点/页面时，当获取内容片段引用时会出现问题，因为后台查询失败；即，该功能不起作用。
要确保操作正确，您需要将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 包含的OSGi包和内容包 {#osgi-bundles-and-content-packages-included}

以下文本文档列出了 [!DNL Experience Manager] 6.5.12.0:

* [Experience Manager6.5.12.0中包含的OSGi包列表](assets/65120_bundles.txt)

* [Experience Manager6.5.12.0中包含的内容包列表](assets/65120_packages.txt)

## 受限网站 {#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/)
* 请参阅 [如何联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅 Adobe 产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)

