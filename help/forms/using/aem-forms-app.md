---
title: AEM Forms应用程序
seo-title: AEM Forms应用程序
description: AEM Forms应用程序允许现场工作人员在其移动设备上使用自适应表单。
seo-description: AEM Forms应用程序允许现场工作人员在其移动设备上使用自适应表单。
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 2%

---

# AEM Forms应用程序简介{#aem-forms-app}

## 概述 {#overview}

AEM Forms应用程序支持根据您的服务器在移动设备上同步自适应表单、移动表单和表单集。 您可以在OSGi](/help/forms/using/aem-forms-workflow.md)上定义以[Forms为中心的工作流，或在JEE上定义以Forms为中心的工作流。 例如，您运营一家银行，并使用AEM Forms管理客户应用程序和通信。 您的客户填写表格并提交以供验证。 如果在移动设备上启用表单，则客户可以在AEM Forms应用程序中填写该表单。 您还可以通过在移动设备上启用验证表单来管理验证工作流。 您的现场工作人员可以向客户携带移动设备、验证详细信息并提交表单。 AEM Forms应用程序与AEM Forms服务器同步，并获取为移动设备启用的表单。 如果应用程序处于离线状态，则会将数据存储在本地。

客户可通过Software Distribution获取AEM Forms应用程序的源代码。 Software Distribution中的源代码包可用为：`adobe-aemfd-forms-app-src-pkg-<version>.zip`。

iOS、Android、Windows设备支持AEM Forms应用程序。 您可以从Google Play安装适用于Android的AEM Forms应用程序，从应用商店安装iOS，从Windows应用商店安装Windows。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-bagge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

要在iOS、Android或Windows设备上安装、自定义和分发应用程序，请参阅[自定义、构建和分发AEM Forms应用程序](#customize-build-distribute)。

## 前提条件 {#prerequisites}

AEM Forms应用程序需要AEM Forms服务器。 用户可以渲染您在AEM Forms中创建的表单
服务器，填写，另存为草稿，然后提交。 应用程序会连接到服务器并从中获取已启用的表单。 AEM Forms应用程序会与服务器同步，一旦表单加载到应用程序中，用户便可以离线工作。 如果应用程序处于脱机状态，则数据会保存在设备上，并且数据会在应用程序处于联机状态时与服务器同步。

### 使用AEM Forms工作流的AEM Forms应用程序{#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms工作流服务器，则可以在AEM Forms应用程序中将表单渲染为任务。 例如，您运行一家银行，客户填写应用程序以使用您的服务。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储为提交以供审阅。 管理员审核应用程序并将验证请求转发给字段工作器。 转发的应用程序会在您的现场工作人员应用程序中启用验证表单作为任务。 现场工作人员将移动设备携带给客户并验证详细信息。

### AEM Forms应用程序，在OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}上使用以Forms为中心的工作流

如果您有AEM Forms服务器，则可以将自适应表单渲染为AEM收件箱应用程序，并在AEM Forms应用程序中渲染任务。 例如，您运行一家银行，客户填写应用程序以使用您的服务。 该应用程序与一个自适应表单关联，该表单接受客户提供的信息并将其存储为提交以供审阅。 管理员审核任务并批准向现场工作人员发出的验证请求。 现场工作人员将移动设备携带给客户并验证详细信息。

### 独立表单或AEM Forms应用程序，带有没有AEM Forms工作流的服务器{#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

OSGi上的AEM Forms服务器未使用AEM Forms工作流，即是AEM Forms，或者是独立的移动设备表单或自适应表单。 AEM Forms应用程序可与您在[OSGi](/help/sites-deploying/configuring-osgi.md)上的AEM Forms实施配合使用。 Forms中提供了为AEM Forms应用程序启用和发布的功能。

表单将在您的应用程序上下载，并且可脱机使用。 例如，您运营着一家银行，客户在您的网站上填写应用程序。 该应用程序是一种自适应表单，可接受客户提供的信息并将其存储以供审阅。 管理员会审阅表单，并在AEM创作实例中创建验证表单。 管理员启用表单与AEM Forms应用程序同步并发布。 如果验证表单在AEM Forms应用程序中可用，则您的现场代理可以使用移动设备来验证客户的详细信息。 移动设备与服务器同步，并且验证表单已加载到应用程序中。 您的现场代理可以访问您的客户、验证详细信息、将数据保存为草稿或提交验证表。 每当应用程序处于联机状态时，表单都会与服务器同步。

要在AEM Forms应用程序中同步您的表单，请执行以下操作：

1. 在创作实例中，选择一个表单，然后单击&#x200B;**[!UICONTROL 查看属性]**。

1. 在属性页面中，单击&#x200B;**[!UICONTROL 高级]**。
1. 在高级下，启用选项：**[!UICONTROL 与AEM Forms App]**&#x200B;同步，然后点按&#x200B;**[!UICONTROL 保存]**。

发布表单后，应用程序将与服务器同步并获取表单。 要同步多个表单，请在创作实例中，在表单管理器中选择多个表单，然后点按&#x200B;**[!UICONTROL 与AEM Forms应用程序同步]**。

## 移动设备支持{#mobile-device-support}

请参阅[AEM Forms应用程序（以前称为Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms应用程序{#key-features-of-aem-forms-app}的主要功能

### AEM Forms应用程序与AEM Forms服务器{#aem-forms-app-with-aem-forms-servers}

您可以将您的应用程序与AEM Forms服务器同步，并可以在移动设备上处理表单。

使用AEM Forms Workflow Server，表单可以与Workbench进程和AEM Inbox应用程序中的起始点关联。 AEM收件箱应用程序可以有一个与其关联的自适应表单。 起点可以具有与其关联的自适应表单、HTML5表单或表单集。 起点可以作为任务提交，也可以将任务另存为草稿。 有关AEM收件箱应用程序与起点之间差异的更多信息，请参阅[OSGi和AEM Forms JEE工作流上以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

如果AEM Forms服务器没有AEM Forms工作流，则在AEM Forms应用程序中会呈现一个在应用程序中启用同步的表单。 Forms位于应用程序的Forms选项卡中，可以提交或另存为草稿。 应用程序支持自适应表单和移动设备表单。

1. **将任务或表单另存为草稿**

   另存为草稿选项保存任务或表单的快照，以及相关表单中已填充的数据和附加的文件。 草稿将保存到移动设备并与AEM Forms服务器同步，以供以后检索。

   请参阅[将任务或表单另存为草稿](/help/forms/using/save-as-draft.md)。

1. **将表单另存为模板**

   有时，当用户填写表单时，对几个字段的输入将保持不变。 对于此类情况，您可以在每个实例中填写要求相同值的字段，并将表单或草稿另存为模板。 现在，每次创建模板实例时，指定的字段都已填充模板中指定的值。 它有助于您节省填写表单所需的时间和精力。

   请参阅[将表单另存为模板](/help/forms/using/save-forms-and-start-points-as-templates.md)。

### 处理任务和表单{#working-with-tasks-and-forms}

您可以将应用程序与AEM Forms工作流服务器同步，并且可以在移动设备上处理任务和表单。

移动设备上的任务包含自适应表单、HTML5表单或表单集，并且还可以包含附件和[摘要URL](/help/forms/using/getting-task-variables-summary-url.md)。 默认情况下，分配给您的任务会放在&#x200B;**[!UICONTROL Tasks]**&#x200B;文件夹中。 处理任务时，您可以更改该任务并在AEM Forms服务器上保存任务的草稿副本。

移动设备上的表单可以是自适应表单或移动表单。 Forms在表单应用程序中启用了同步功能，该功能可在Forms文件夹中使用。 您可以在不使用AEM Forms工作流的情况下(OSGi上的AEM Forms)同步在AEM Forms服务器中启用的表单。

请参阅：

* [打开任务](/help/forms/using/open-task.md)
* [使用表单](/help/forms/using/working-with-form.md)

### 脱机工作{#working-offline}

您可以在脱机模式下处理移动设备。 即使没有网络连接，您也可以登录到应用程序，并且可以处理上次联机时与设备同步的所有表单。 有关如何同步表单的详细信息，请参阅[同步应用程序](/help/forms/using/sync-app.md)。 如果选择同步与表单关联的附件，则也可以在脱机模式下打开附件。 您可以在脱机模式下编辑表单、添加批注，以及提交或保存表单。 表单在您下次联机时与AEM Forms服务器同步。

有关详细信息，请参阅[在脱机模式下工作](/help/forms/using/work-offline-mode.md)。

### 添加注释{#adding-annotations}

您可以将以下附件添加到移动设备上的表单中

* **注释** — 可以使用“注释”功能在表单中添加手绘文字或文本注释。有关详细信息，请参阅[添加注释](/help/forms/using/add-attachments.md#adding-a-note)。

* **图片** - AEM Forms应用程序包含一项功能，该功能使用相机功能或移动设备的图库。使用照片附件，您可以添加具有关联表单的照片。 有关详细信息，请参阅[添加照片](/help/forms/using/add-attachments.md#adding-a-photograph)。

### 自动保存 {#autosave}

当用户在AEM Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免在应用程序因电池不足等情况关闭时丢失数据。

请参阅[在AEM Forms应用程序中使用自动保存](/help/forms/using/autosave-data-app.md)。

## AEM收件箱和AEM Forms应用程序功能之间的差异{#differences-between-aem-inbox-and-aem-forms-app-features}

启动以Forms为中心的工作流的两种主要方法是：使用[AEM Inbox](/help/forms/using/manage-applications-inbox.md)和AEM Forms应用程序。 但是，AEM收件箱和AEM Forms应用程序的功能有所不同。 AEM收件箱仅适用于[以Forms为中心的工作流](/help/forms/using/aem-forms-workflow.md)，而AEM Forms应用程序则适用于以Forms为中心的工作流以及流程管理。 有关AEM收件箱和AEM Forms应用程序功能之间差异的更多信息，请参阅[OSGi和AEM Forms JEE工作流上以表单为中心的AEM工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

## 支持的表单{#supported-forms}

AEM Forms应用程序中支持的表单类型：

### 自适应表单 {#adaptive-form}

AEM Forms应用程序支持动态适应用户输入的自适应表单。 还支持延迟加载的自适应表单。

### 移动设备表单{#mobile-form}

您可以在AEM Forms中为移动设备创建表单。 在可根据显示设备进行相应调整的移动设备中，移动表单会呈现为HTML表单。

### 表单集 {#formset}

使用表单集，可以将与服务或流程相关的多个表单分组，以自动执行业务流程并呈现给最终用户。 在这种情况下，用户可以将整个集合作为一个进行填充，而且无需存档、提交和跟踪单个表单或进程。

>[!NOTE]
>
>需要AEM Forms工作流(JEE上的AEM Forms)。

## AEM Forms应用程序的工作原理{#how-aem-forms-app-works}

AEM Forms应用程序为现场工作人员提供了一个移动设备解决方案，用于处理分配给他们的表单。 应用程序缓存来自服务器的完整数据，并通过将所有工作保存在本地来提供有效的用户体验。 磁盘中的数据通过及时的同步更新发送到服务器。

AEM Forms应用程序是一个基于PhoneGap 5.0的应用程序，在该应用程序中，Backbone模型可高效地通过视图显示存储在模型中的数据。 所有本机操作都通过PhoneGap插件执行。

## 自定义、构建和分发AEM Forms应用程序{#customize-build-distribute}

>[!NOTE]
>
>仅当您使用AEM Forms应用程序源代码来构建应用程序时才适用。

AEM Forms应用程序易于根据特定于组织的需求进行自定义。 应用程序的源代码与AEM Forms一起提供。 您可以更改源代码并构建您自己的移动员工解决方案。 您还可以使用自己的企业密钥对应用程序进行签名。

### 自定义 {#customize}

您可以自定义您的应用程序，以便：

**品牌策略**:在AEM Forms应用程序中更改应用程序图标、应用程序名称、启动图像和页面。您还可以更改文本，以将应用程序本地化为特定区域的本地化。 有关品牌化AEM Forms应用程序的更多信息，请参阅[品牌定制](/help/forms/using/branding-customization.md)。

**主题**:在AEM Forms应用程序用户界面中更改样式，如颜色、字体和间距。有关更多信息，请参阅[主题自定义](/help/forms/using/theme-customization.md)。

**手势**:在AEM Forms应用程序用户界面中更改手势，如向右轻扫和向左轻扫。有关更多信息，请参阅[手势自定义](/help/forms/using/gesture-customization.md)。

有关设置AEM Forms应用程序项目进行自定义的更多信息，请参阅：

* [为AEM Forms应用程序设置环境](/help/forms/using/setup-environment-mobile-workspace.md)
* [设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)
* [设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)

### 构建和分发{#build-and-distribute}

可以从`adobe-lc-mobileworkspace-src.zip`中提取AEM Forms应用程序的源代码，该代码作为Software Distribution上AEM Forms应用程序源包的一部分提供。

要获取AEM Forms应用程序源，请执行以下步骤：

1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分中：
   1. 从&#x200B;**[!UICONTROL Solution]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Forms]**。
   2. 选择包的版本和类型。 您还可以使用&#x200B;**[!UICONTROL 搜索下载]**&#x200B;选项来筛选结果。
1. 点按适用于您的操作系统的包名称，选择&#x200B;**[!UICONTROL 接受EULA条款]**，然后点按&#x200B;**[!UICONTROL 下载]**。
1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
1. 选择包并单击&#x200B;**[!UICONTROL Install]**。

**对于iOS**:

有关如何创建iOS应用程序(.ipa)的详细信息，请参阅[设置Xcode项目并构建iOS应用程序](/help/forms/using/setup-xcode-project-build-installer.md)。

有关如何使用配置文件对AEM Forms应用程序进行签名的详细信息，请参阅[iOS代码签名设置、过程和疑难解答](https://developer.apple.com/support/code-signing/)。

**对于Android**:

有关如何创建Android应用程序(.apk)的详细信息，请参阅[设置Eclipse项目并构建Android应用程序](/help/forms/using/setup-eclipse-project-build-installer.md)。

有关如何对AEM Forms应用程序进行签名的详细信息，请参阅[对您的应用程序进行签名](https://developer.android.com/tools/publishing/app-signing.html)。

**对于Windows**:

有关如何创建Windows应用程序(.appx)的详细信息，请参阅[设置Visual Studio项目并构建Windows应用程序](/help/forms/using/setup-visual-studio-project-build-installer.md)。

有关如何通过MDM分发应用程序的详细信息，请参阅[分发AEM Forms应用程序](/help/forms/using/distribute-mobile-workspace-app.md)。 通过MDM进行应用程序分发仅适用于iOS和Android。

## Recommendations将Mobile Workspace升级到AEM Forms应用程序{#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升级到最新版本的AEM Forms应用程序，请确保阅读以下内容：

* **如果您在Android上从Play Store安装了更早版本的应用程序，则**
可以直接从Play Store升级该应用程序。

* **如果使用源代码构建并安装了早期版本的应用程序（适用于iOS和Android）**:

   在安装新应用程序之前，请将所有数据与AEM Forms服务器同步。 同步数据后，请卸载应用程序的早期版本，然后安装新应用程序。
