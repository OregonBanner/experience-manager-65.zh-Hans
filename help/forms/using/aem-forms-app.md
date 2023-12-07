---
title: AEM Forms应用程序
description: AEM Forms应用程序使您的字段工作人员能够在其移动设备上使用自适应表单。
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 0%

---

# AEM Forms应用程序简介 {#aem-forms-app}

## 概述 {#overview}

AEM Forms应用程序支持根据您的服务器，在移动设备上同步自适应表单、移动表单和表单集。 您可以定义以下工作流 [OSGi上以Forms为中心的工作流](/help/forms/using/aem-forms-workflow.md) 或JEE上的Forms工作流。 例如，您经营一家银行公司，并使用AEM Forms管理客户应用程序和通信。 您的客户填写并提交表单以进行验证。 如果您在移动设备上启用表单，则客户可以在AEM Forms应用程序中填写表单。 您还可以通过在移动设备上启用验证表单来管理验证工作流。 您的现场工作人员可以向客户携带移动设备、验证详细信息并提交表单。 AEM Forms应用程序与AEM Forms服务器同步，并获取为移动设备启用的表单。 如果应用程序处于离线状态，则会将数据存储在本地。

客户可以通过Software Distribution获取AEM Forms应用程序的源代码。 Software Distribution中的源代码包如下所示： `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

iOS、Android和Windows设备支持AEM Forms应用程序。 您可以从Google Play安装适用于Android的AEM Forms应用程序，从App Store安装iOS，并从Windows应用商店安装Windows。

    [ ！[google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ！[app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ！[microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

要在iOS、Android或Windows设备上安装、自定义和分发应用程序，请参阅 [自定义、构建和分发AEM Forms应用程序](#customize-build-distribute).

## 前提条件 {#prerequisites}

AEM Forms应用程序需要AEM Forms服务器。 用户可以渲染您在AEM Forms服务器中创建的表单、填写表单、另存为草稿并提交表单。 应用程序会连接到服务器并从其中获取启用的表单。 AEM Forms应用程序与服务器同步，一旦表单加载到应用程序中，用户就可以脱机工作。 如果应用程序处于离线状态，则数据会保存在设备上，并在应用程序处于在线状态时与服务器同步。

### 带服务器的AEM Forms应用程序使用AEM Forms工作流程 {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms工作流服务器，则可以在AEM Forms应用程序中将表单渲染为任务。 例如，您经营一家银行公司，客户填写申请表以使用您的服务。 应用程序是一个自适应表单，它接受来自客户的信息，并将其存储为提交以供审核。 管理员审查申请并将验证请求转发给现场工作人员。 转发的申请会在您的现场工作人员应用程序中启用验证表单作为任务。 您的现场工作人员将移动设备带给您的客户并验证详细信息。

### 在OSGi上使用以Forms为中心的工作流的服务器的AEM Forms应用程序 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您拥有AEM Forms服务器，则可以在AEM Forms应用程序中将自适应表单渲染为AEM收件箱应用程序以及任务。 例如，您经营一家银行公司，客户填写申请表以使用您的服务。 该应用程序与自适应表单相关联，该表单接受来自客户的信息，并将其存储为提交以供审核。 管理员审阅任务并批准现场工作人员的验证请求。 您的现场工作人员将移动设备带给您的客户并验证详细信息。

### 独立表单或AEM Forms应用程序(带服务器，无AEM Forms工作流程) {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms Workflow的AEM Forms服务器是OSGi上的AEM Forms，或者是独立的移动表单或自适应表单。 AEM Forms应用程序与您的AEM Forms实施配合使用，位于 [osgi](/help/sites-deploying/configuring-osgi.md). 您为AEM Forms应用程序启用和发布的Forms在应用程序中可用。

这些表单将在您的应用程序中下载，并可供离线使用。 例如，您正在运行一家银行公司，客户在您的网站上填写申请。 应用程序是一个自适应表单，它接受来自客户的信息并将其存储以供审查。 管理员查看表单，并在AEM创作实例中创建验证表单。 管理员可以启用表单与AEM Forms应用程序的同步功能，并将其发布。 如果AEM Forms应用程序中提供了验证表单，则您的字段代理可以使用移动设备来验证客户的详细信息。 移动设备将与服务器同步，并且验证表单会加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据另存为草稿或提交验证表单。 只要应用程序处于联机状态，该表单就会与服务器同步。

要在AEM Forms应用程序中同步表单，请执行以下操作：

1. 在创作实例中，选择一个表单，然后单击 **[!UICONTROL 查看属性]**.

1. 在属性页面中，单击 **[!UICONTROL 高级]**.
1. 在“高级”下，启用选项： **[!UICONTROL 与AEM Forms应用程序同步]** 并选择 **[!UICONTROL 保存]**.

发布表单后，应用程序将与服务器同步并获取表单。 要同步多个表单，请在创作实例中选择表单管理器中的多个表单，然后选择 **[!UICONTROL 与AEM Forms应用程序同步]**.

## 移动设备支持 {#mobile-device-support}

请参阅 [AEM Forms应用程序（以前称为移动工作区）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms应用程序的主要功能 {#key-features-of-aem-forms-app}

### AEM Forms应用程序与AEM Forms服务器 {#aem-forms-app-with-aem-forms-servers}

您可以将应用程序与AEM Forms服务器同步，并可以在移动设备上处理表单。

使用AEM Forms Workflow Server时，可以将表单与Workbench进程和AEM收件箱应用程序中的起点关联。 AEM收件箱应用程序可以具有与其关联的自适应表单。 起点可以具有自适应表单、HTML5表单或与其关联的表单集。 起点可以作为任务提交，也可以将任务另存为草稿。 有关AEM收件箱应用程序与起点之间差异的更多信息，请参阅 [OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md).

借助不具有AEM Forms工作流的AEM Forms服务器，应用程序中启用同步的表单将在AEM Forms应用程序中渲染。 Forms在应用程序的Forms选项卡中可用，可以提交或另存为草稿。 应用程序支持自适应表单和移动表单。

1. **将任务或表单另存为草稿**

   另存为草稿选项保存任务或表单的快照，以及相关表单中填写的数据和附加的文件。 草稿将保存到移动设备并与AEM Forms服务器同步，以供日后检索。

   请参阅 [将任务或表单另存为草稿](/help/forms/using/save-as-draft.md).

1. **将表单另存为模板**

   有时，当用户填写表单时，对几个字段的输入将保持不变。 对于这种情况，您可以填写每个实例中需要相同值的字段，并将表单或草稿另存为模板。 现在，每次创建模板的实例时，指定的字段都已填充了模板中指定的值。 这有助于节省填写表单所需的时间和精力。

   请参阅 [将表单另存为模板](/help/forms/using/save-forms-and-start-points-as-templates.md).

### 处理任务和表单 {#working-with-tasks-and-forms}

您可以将应用程序与AEM Forms Workflow Server同步，并可以在移动设备上处理任务和表单。

移动设备上的任务包含自适应表单、HTML5表单或表单集，并且还可以包含附件和 [摘要URL](/help/forms/using/getting-task-variables-summary-url.md). 默认情况下，分配给您的任务放在 **[!UICONTROL 任务]** 文件夹。 处理任务时，您可以更改任务并在AEM Forms服务器上保存任务的草稿副本。

移动设备上的表单可以是自适应表单或移动设备表单。 Forms文件夹中提供了在表单应用程序中启用同步的Forms。 您可以同步在AEM Forms服务器中启用的表单，而无需使用AEM Forms工作流程(OSGi上的AEM Forms)。

请参阅：

* [打开任务](/help/forms/using/open-task.md)
* [使用表单](/help/forms/using/working-with-form.md)

### 脱机工作 {#working-offline}

您可以在脱机模式下使用移动设备。 即使没有网络连接，您也可以登录到该应用程序，并可以使用上次联机时与设备同步的所有表单。 有关如何同步表单的详细信息，请参阅 [同步应用程序](/help/forms/using/sync-app.md). 如果选择同步与表单关联的附件，则也可以在脱机模式下打开附件。 您可以在脱机模式下编辑表单、添加批注以及提交或保存表单。 该表单将在您下次联机时与AEM Forms服务器同步。

有关详细信息，请参阅 [在脱机模式下工作](/help/forms/using/work-offline-mode.md).

### 添加注释 {#adding-annotations}

您可以将以下附件添加到移动设备上的表单中

* **注释** — 可以使用“注释”功能在表单中添加手绘涂鸦或文本注释。 有关详细信息，请参阅 [添加注释](/help/forms/using/add-attachments.md#adding-a-note).

* **图片**- AEM Forms应用程序包含的一项功能使用了摄像头的功能或移动设备的图片库。 使用照片附件，可以添加带有相关表单的照片。 有关详细信息，请参阅 [添加照片](/help/forms/using/add-attachments.md#adding-a-photograph).

### 自动保存 {#autosave}

当用户在AEM Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免因电池电量不足等情况而关闭应用程序时的数据丢失。

请参阅 [在AEM Forms应用程序中使用自动保存](/help/forms/using/autosave-data-app.md).

## AEM收件箱和AEM Forms应用程序功能之间的差异 {#differences-between-aem-inbox-and-aem-forms-app-features}

启动以Forms为中心的工作流的两种主要方法是 [AEM收件箱](/help/forms/using/manage-applications-inbox.md) 和AEM Forms应用程序。 但是，AEM收件箱和AEM Forms应用程序的功能有所不同。 AEM收件箱仅适用于 [以Forms为中心的工作流](/help/forms/using/aem-forms-workflow.md) 而AEM Forms应用程序可同时使用以Forms为中心的工作流和流程管理。 有关AEM收件箱与AEM Forms应用程序功能之间差异的更多信息，请参阅 [OSGi和AEM Forms JEE工作流中以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md).

## 支持的表单 {#supported-forms}

AEM Forms应用程序中支持的表单类型：

### 自适应表单 {#adaptive-form}

AEM Forms应用程序支持可动态适应用户输入的自适应表单。 还支持延迟加载的自适应表单。

### 移动设备表单 {#mobile-form}

您可以在AEM Forms中为移动设备创建表单。 移动设备表单在根据显示设备调整的移动设备中呈现为HTML表单。

### 表单集 {#formset}

使用表单集，可以分组与服务或流程相关的多个表单以自动化业务流程并向最终用户呈现。 在这样的场景中，用户可以作为一个整体填写整个集合，而无需文件、提交和跟踪单个表单或进程。

>[!NOTE]
>
>需要AEM Forms工作流程(JEE上的AEM Forms)。

## AEM Forms应用程序的工作原理 {#how-aem-forms-app-works}

AEM Forms应用程序为现场工作人员处理分配给他们的表单提供移动解决方案。 该应用程序从服务器缓存完整数据，并通过将所有工作保存在本地来提供高效的用户体验。 来自磁盘的数据通过及时的同步更新发送到服务器。

AEM Forms应用程序是基于PhoneGap 5.0的应用程序，其中骨干模型可高效用于通过视图呈现存储在模型中的数据。 所有本机操作均通过PhoneGap插件执行。

## 自定义、构建和分发AEM Forms应用程序 {#customize-build-distribute}

>[!NOTE]
>
>仅适用于使用AEM Forms应用程序源代码构建应用程序的情况。

AEM Forms应用程序可轻松根据组织的特定需求进行自定义。 该应用程序的源代码与AEM Forms一起提供。 您可以更改源代码并构建自己的移动工作人员解决方案。 您还可以使用自己的企业密钥对应用程序进行签名。

### 自定义 {#customize}

您可以针对以下项目自定义您的应用程序：

**品牌化**：更改AEM Forms应用程序中的应用程序图标、应用程序名称、启动图像和页面。 您还可以更改文本以将应用程序本地化到特定区域。 有关品牌化AEM Forms应用程序的更多信息，请参阅 [品牌化自定义](/help/forms/using/branding-customization.md).

**主题**：在AEM Forms应用程序用户界面中更改样式，如颜色、字体和间距。 有关更多信息，请参阅 [主题自定义](/help/forms/using/theme-customization.md).

**手势**：更改手势，例如在AEM Forms应用程序用户界面中向右轻扫和向左轻扫。 有关更多信息，请参阅 [手势自定义](/help/forms/using/gesture-customization.md).

有关设置AEM Forms应用程序项目以进行自定义的更多信息，请参阅：

* [为AEM Forms应用程序设置环境](/help/forms/using/setup-environment-mobile-workspace.md)
* [设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)
* [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)

### 构建和分发 {#build-and-distribute}

AEM Forms应用程序的源代码可从提取 `adobe-lc-mobileworkspace-src.zip` 可作为Software Distribution上的AEM Forms应用程序源包的一部分获取。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 选择 **[!UICONTROL Adobe Experience Manager]** 在标题菜单中可用。
1. 在 **[!UICONTROL 过滤器]** 部分：
   1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
   2. 选择包的版本和类型。 您也可以使用 **[!UICONTROL 搜索下载]** 用于筛选结果的选项。
1. 选择适用于您的操作系统的包名称，然后选择 **[!UICONTROL 接受EULA条款]**，并选择 **[!UICONTROL 下载]**.
1. 打开 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  并单击 **[!UICONTROL 上传包]** 以上传包。
1. 选择包并单击 **[!UICONTROL 安装]**.

**适用于iOS的**：

有关如何创建iOS应用程序(.ipa)的详细信息，请参阅 [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md).

有关如何使用配置配置文件签署AEM Forms应用程序的详细信息，请参阅 [iOS代码签名设置、流程和疑难解答](https://developer.apple.com/support/code-signing/).

**适用于Android**：

有关如何创建Android应用程序(.apk)的详细信息，请参阅 [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md).

有关如何签署AEM Forms应用程序的详细信息，请参阅 [对应用程序进行签名](https://developer.android.com/tools/publishing/app-signing.html).

**对于Windows**：

有关如何创建Windows应用程序(.appx)的详细信息，请参阅 [设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md).

有关如何通过MDM分发应用程序的详细信息，请参阅 [分发AEM Forms应用程序](/help/forms/using/distribute-mobile-workspace-app.md). 通过MDM分发的应用程序仅适用于iOS和Android。

## Recommendations将移动工作区升级到AEM Forms应用程序 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升级到最新版本的AEM Forms应用程序，请确保您已阅读以下几点：

* **如果您从Android上的Play Store安装了应用程序的早期版本**
您可以直接从Play Store升级应用程序。

* **如果使用源代码构建和安装应用程序的早期版本(适用于iOS和Android)**：

  在安装新应用程序之前，请将所有数据与AEM Forms服务器同步。 数据同步后，卸载旧版应用程序，然后安装新应用程序。
