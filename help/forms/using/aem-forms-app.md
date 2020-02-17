---
title: AEM Forms应用程序
seo-title: AEM Forms应用程序
description: AEM Forms应用程序使现场工作人员能够在他们的移动设备上使用自适应表单。
seo-description: AEM Forms应用程序使现场工作人员能够在他们的移动设备上使用自适应表单。
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Introduction to AEM Forms app {#aem-forms-app}

## 概述 {#overview}

AEM Forms应用程序支持在移动设备上基于服务器同步自适应表单、移动表单和表单集。 您可以在OSGi上定义以表 [单为中心的工作流](/help/forms/using/aem-forms-workflow.md) ，或在JEE [上定义表单工作流](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application)。 例如，您运行了一家银行，并使用AEM Forms管理客户应用程序和通信。 客户填写表单并提交以进行验证。 如果在移动设备上启用表单，则客户可以在AEM Forms应用程序中填写表单。 您还可以通过在移动设备上启用验证表单来管理验证工作流。 您的现场工作人员可以将移动设备运送给客户、验证详细信息并提交表单。 AEM Forms应用程序与AEM Forms服务器同步，并获取为移动设备启用的表单。 如果应用程序处于脱机状态，则它将数据存储在本地。

AEM Forms应用程序的源代码可通过包共享方式提供给客户。 包共享中的源代码包可用于： `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

iOS、Android和Windows设备支持AEM Forms应用程序。 您可以从Google Play、App Store和Windows应用商店中安装适用于Android的AEM Forms应用程序。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

要在iOS、Android或Windows设备上安装、自定义和分发应用程序，请参阅自 [定义、构建和分发AEM Forms应用程序](#customize-build-distribute)。

## 前提条件 {#prerequisites}

AEM Forms应用程序需要AEM Forms服务器。 用户可以渲染您在AEM Forms服务器中创建的表单、填写表单、另存为草稿并提交它们。 应用程序连接到服务器并从中获取已启用的表单。 AEM Forms应用程序与服务器同步，一旦表单加载到应用程序中，用户就可以脱机工作。 如果应用程序处于脱机状态，则数据会保存在设备上，并且当应用程序处于联机状态时，数据会与服务器同步。

### AEM Forms应用程序（带有使用AEM Forms Workflow的服务器） {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms Workflow服务器，则可以在AEM Forms应用程序中将表单渲染为任务。 例如，您经营一家银行，客户填写应用程序以使用您的服务。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储为供审阅的提交。 管理员会审阅应用程序并将验证请求转发给字段工作器。 转发的应用程序将现场工作者应用程序中的验证表单作为任务启用。 现场工作人员将移动设备运送给客户并验证详细信息。

### AEM Forms应用程序，服务器使用OSGi上以表单为中心的工作流 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您有AEM Forms服务器，则可以将自适应表单渲染为AEM收件箱应用程序，并在AEM Forms应用程序中渲染任务。 例如，您经营一家银行，客户填写应用程序以使用您的服务。 该应用程序与自适应表单关联，该表单接受客户提供的信息并将其存储为供审阅的提交。 管理员会检查任务并批准向现场工作者发出的验证请求。 现场工作人员将移动设备运送给客户并验证详细信息。

### 独立表单或AEM Forms应用程序（带有不带AEM Forms Workflow的服务器） {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms workflow的AEM Forms服务器是OSGi上的AEM Forms，或是独立的移动表单或自适应表单。 AEM Forms应用程序可与OSGi上的AEM Forms实施 [配合使用](/help/sites-deploying/configuring-osgi.md)。 您为AEM Forms应用程序启用和发布的表单在您的应用程序中可用。

表单将下载到您的应用程序中，并且可脱机使用。 例如，您正在运营一家银行，而客户在您的网站上填写了一个应用程序。 该应用程序是一种自适应表单，可接受客户提供的信息并存储以供审阅。 管理员会审阅表单，并在AEM作者实例中创建验证表单。 管理员启用表单与AEM Forms应用程序的同步，并发布它。 如果验证表单在AEM Forms应用程序中可用，则您的现场代理可以使用移动设备验证客户的详细信息。 移动设备与服务器同步，验证表单加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据保存为草稿或提交验证表单。 只要应用程序处于联机状态，表单就会与服务器同步。

要在AEM Forms应用程序中同步表单，请执行以下操作：

1. 在创作实例中，选择一个表单，然后单击“查 **[!UICONTROL 看属性”]**。

1. 在属性页面中，单击高 **[!UICONTROL 级]**。
1. 在“高级”下，启用选项：与 **[!UICONTROL AEM Forms应用程序同步]** ，然后点 **[!UICONTROL 按保存]**。

发布表单后，应用程序将与服务器同步并获取表单。 要同步多个表单，请在创作实例中，在表单管理器中选择多个表单，然后点按与AEM **[!UICONTROL 表单应用程序同步]**。

## 移动设备支持 {#mobile-device-support}

请参 [阅AEM Forms应用程序（以前称为Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms应用程序的主要功能 {#key-features-of-aem-forms-app}

### 带有AEM Forms服务器的AEM Forms应用程序 {#aem-forms-app-with-aem-forms-servers}

您可以将应用程序与AEM Forms服务器同步，并可以在移动设备上处理表单。

借助AEM Forms Workflow服务器，表单可以与工作台进程和AEM收件箱应用程序中的起点关联。 AEM收件箱应用程序可以有一个与其关联的自适应表单。 起点可以具有与其关联的自适应表单、HTML5表单或表单集。 起始点可以作为任务提交，或者任务可以另存为草稿。 有关AEM收件箱应用程序与起点之间差异的更多信息，请参阅OSGi和AEM Forms JEE工作流上以表单为中心的AEM工作流的操作和功能 [](/help/forms/using/capabilities-osgi-jee-workflows.md)。

在AEM Forms服务器不带AEM Forms工作流的情况下，在AEM Forms应用程序中将呈现一个在应用程序中启用同步的表单。 表单位于应用程序的“表单”选项卡中，可提交或另存为草稿。 应用程序支持自适应表单和移动表单。

1. **将任务或表单另存为草稿**

   另存为草稿选项会保存任务或表单的快照以及已填写的数据以及关联表单中附加的文件。 草稿将保存到移动设备，并与AEM Forms服务器同步以供以后检索。

   请参 [阅将任务或表单另存为草稿](/help/forms/using/save-as-draft.md)。

1. **将表单另存为模板**

   有时，当用户填写表单时，对几个字段的输入将保持不变。 对于此类情况，您可以在每个实例中填写要求相同值的字段，并将表单或草稿另存为模板。 现在，每次创建模板实例时，指定的字段都已填充了模板中指定的值。 它可以帮助您节省填写表单所需的时间和精力。

   请参阅 [将表单另存为模板](/help/forms/using/save-forms-and-start-points-as-templates.md)。

### 处理任务和表单 {#working-with-tasks-and-forms}

您可以将应用程序与AEM Forms Workflow服务器同步，并可在移动设备上处理任务和表单。

移动设备上的任务包含自适应表单、HTML5表单或表单集，并且还可以包含附件和摘 [要URL](/help/forms/using/getting-task-variables-summary-url.md)。 默认情况下，分配给您的任务将放在“任务”文 **[!UICONTROL 件夹]** 中。 处理任务时，您可以更改任务并在AEM Forms服务器上保存任务的草稿副本。

移动设备上的表单可以是自适应表单或移动表单。 表单文件夹中提供了在表单应用程序中启用同步的表单。 您可以同步在AEM Forms服务器中启用的表单，而无需AEM Forms工作流（OSGi上的AEM Forms）。

请参阅：

* [打开任务](/help/forms/using/open-task.md)
* [使用表单](/help/forms/using/working-with-form.md)

### 脱机工作 {#working-offline}

您可以在脱机模式下使用移动设备。 即使没有网络连接，您也可以登录到应用程序，并且可以处理上次联机时与设备同步的所有表单。 有关如何同步表单的详细信息，请参阅同 [步应用程序](/help/forms/using/sync-app.md)。 如果选择同步与表单关联的附件，则还可以在脱机模式下打开附件。 您可以在脱机模式下编辑表单、添加批注以及提交或保存表单。 下次联机时，表单将与AEM Forms服务器同步。

有关详细信息，请 [参阅在脱机模式下工作](/help/forms/using/work-offline-mode.md)。

### Adding annotations {#adding-annotations}

您可以在移动设备上向表单中添加以下附件

* **附注**-您可以使用“附注”功能在表单中添加手绘或文本附注。 有关详细信息，请 [参阅添加备注](/help/forms/using/add-attachments.md#adding-a-note)。

* **图片**- AEM Forms应用程序包含一个功能，可使用相机功能或移动设备的画廊。 使用照片附件，您可以添加具有关联表单的照片。 有关详细信息，请 [参阅添加照片](/help/forms/using/add-attachments.md#adding-a-photograph)。

### 自动保存 {#autosave}

当用户在AEM Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免因电池电量不足等情况导致应用程序关闭时的数据丢失。

请参 [阅在AEM Forms应用程序中使用自动保存](/help/forms/using/autosave-data-app.md)。

## AEM收件箱与AEM Forms应用程序功能之间的区别 {#differences-between-aem-inbox-and-aem-forms-app-features}

启动以表单为中心的工作流程的两种主要方法是使用 [AEM收件箱](/help/forms/using/manage-applications-inbox.md) 和AEM Forms应用程序。 但是，AEM收件箱和AEM Forms应用程序的功能不同。 AEM收件箱只能与以表 [单为中心的工作流一起使用](/help/forms/using/aem-forms-workflow.md) ，而AEM Forms应用程序既可以与以表单为中心的工作流一起使用，又可以与流程管理一起使用。 有关AEM收件箱与AEM Forms应用程序功能之间差异的更多信息，请参阅OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能 [](/help/forms/using/capabilities-osgi-jee-workflows.md)。

## 支持的表单 {#supported-forms}

AEM Forms应用程序中支持的表单类型：

### 自适应表单 {#adaptive-form}

AEM Forms应用程序支持动态适应用户输入的自适应表单。 还支持延迟加载的自适应表单。

### 移动表单 {#mobile-form}

您可以在AEM Forms中为移动设备创建表单。 移动表单在移动设备中呈现为HTML表单，这些表单根据显示设备进行调整。

### 表单集 {#formset}

使用表单集，可以将与服务或流程相关的多个表单分组以自动处理业务流程并呈现给最终用户。 在这种情况下，用户可以将整个集合作为一部分进行填写，而无需对单个表单或进程进行归档、提交和跟踪。

>[!NOTE]
>
>需要AEM Forms Workflow（JEE上的AEM Forms）。

## AEM Forms应用程序的工作方式 {#how-aem-forms-app-works}

AEM Forms应用程序为现场工作人员提供了一个移动解决方案，以便处理分配给他们的表单。 应用程序缓存来自服务器的完整数据，并通过将所有工作保存在本地来提供有效的用户体验。 磁盘中的数据通过及时的同步更新发送到服务器。

AEM Forms应用程序是基于PhoneGap 5.0的应用程序，在该应用程序中，Backbone模型可高效地通过视图呈现存储在模型中的数据。 所有本机操作都通过PhoneGap插件执行。

## 自定义、构建和分发AEM Forms应用程序 {#customize-build-distribute}

>[!NOTE]
>
>仅适用于使用AEM Forms应用程序源代码构建应用程序。

AEM Forms应用程序可轻松自定义，以满足特定于组织的需求。 应用程序的源代码随AEM Forms一起提供。 您可以更改源代码并构建自己的移动员工解决方案。 您还可以使用您自己的企业密钥对应用程序进行签名。

### 自定义 {#customize}

您可以为以下对象自定义应用程序：

**品牌**:在AEM Forms应用程序中更改应用程序图标、应用程序名称、启动图像和页面。 您还可以更改文本以本地化特定区域的应用程序。 有关AEM Forms应用程序品牌化的更多信息，请参阅品牌 [自定义](/help/forms/using/branding-customization.md)。

**主题**:在AEM Forms应用程序用户界面中更改颜色、字体和间距等样式。 有关详细信息，请参阅 [主题自定义](/help/forms/using/theme-customization.md)。

**手势**:在AEM Forms应用程序用户界面中更改手势，如右轻扫和左轻扫。 有关详细信息，请参阅手 [势自定义](/help/forms/using/gesture-customization.md)。

有关设置AEM Forms应用程序项目以进行自定义的详细信息，请参阅：

* [为AEM Forms应用程序设置环境](/help/forms/using/setup-environment-mobile-workspace.md)
* [设置Visual studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)
* [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)

### 构建和分发 {#build-and-distribute}

AEM Forms应用程序的源代码可从adobe-lc-mobileworkspace-src.zip中提取，该代码可作为包共享上AEM Forms应用程序源包的一部分提供。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 导航到包共享

   URL: `https://<server>:<port>/crx/packageshare`.

1. 下载源包。 下载包时，它会添加到AEM Forms包管理器中。
1. 下载完毕后，导航到： `https://<server>:<port>/crx/packmgr/index.jsp`并安装 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 要下载包，请在您的浏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 览器中打开。

   源包将下载到您的设备上。

**对于iOS**:

有关如何创建iOS应用程序(.ipa)的详细信息，请参 [阅设置Xcode项目和构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)。

有关如何使用供应配置文件对AEM Forms应用程序进行签名的详细信息，请参阅 [iOS代码签名设置、进程和疑难解答](https://developer.apple.com/support/code-signing/)。

**对于Android**:

有关如何创建Android应用程序(.apk)的详细信息，请参 [阅设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

有关如何对AEM Forms应用程序进行签名的详细信息，请参阅对应 [用程序进行签名](https://developer.android.com/tools/publishing/app-signing.html)。

**对于Windows**:

有关如何创建Windows应用程序(.appx)的详细信息，请参阅 [设置Visual studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)。

有关如何通过MDM分发应用程序的详细信息，请参 [阅分发AEM Forms应用程序](/help/forms/using/distribute-mobile-workspace-app.md)。 通过MDM分发的应用程序仅适用于iOS和Android。

## 将Mobile Workspace升级到AEM Forms应用程序的建议 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升级到AEM Forms应用程序的最新版本，请确保阅读以下要点：

* **如果您从Android上的play store安装了该应用程序的早期版本**，则可以直接从play store升级该应用程序。

* **如果应用程序的早期版本是使用源代码构建和安装的（适用于iOS和Android）**:

   在安装新应用程序之前，请将所有数据与AEM Forms服务器同步。 同步数据后，请卸载应用程序的早期版本，然后安装新应用程序。

