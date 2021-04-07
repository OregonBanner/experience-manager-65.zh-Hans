---
title: 配置 Dynamic Media — Scene7 模式
description: 了解如何配置Dynamic Media - Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: 配置，Scene7模式
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '6154'
ht-degree: 5%

---

# 配置 Dynamic Media — Scene7 模式{#configuring-dynamic-media-scene-mode}

如果您使用为不同环境（如开发、升级和生产）设置的Adobe Experience Manager，请为这些环境中的每个配置Dynamic MediaCloud Services。

## Dynamic Media的架构图 — Scene7模式{#architecture-diagram-of-dynamic-media-scene-mode}

以下架构图描述了Dynamic Media - Scene7模式的工作原理。

借助新的架构，Experience Manager负责主源资源并与Dynamic Media同步以处理和发布资源：

1. 将主源资产上传到Experience Manager后，该资产将复制到Dynamic Media。 此时，Dynamic Media将处理所有资产处理和再现生成，如图像的视频编码和动态变体。<!-- (In Dynamic Media - Scene7 mode, be aware that you can only upload assets whose file sizes are 2 GB or less.) Jira ticket CQ-4286561 fixed this issue. DM-S7 NOW SUPPORTS THE UPLOAD OF ASSETS LARGER THAN 2 GB. -->
1. 生成演绎版后，Experience Manager可以安全访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager实例)。
1. 在内容准备好发布和批准后，它会触发Dynamic Media服务，将内容推送到投放服务器并缓存CDN(内容投放网络)中的内容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>以下功能列表要求您使用与Adobe Experience Manager - Dynamic Media捆绑的现成CDN。 这些功能不支持任何其他自定义CDN。
>
>* [智能图像处理](/help/assets/imaging-faq.md)
>* [缓存失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [热链接保护](/help/assets/hotlink-protection.md)
>* [HTTP/2 内容交付](/help/assets/http2.md)
>* 在CDN级别重定向URL
>* Akamai ChinaCDN(在中国实现最佳投放)


## 在Scene7模式{#enabling-dynamic-media-in-scene-mode}中启用Dynamic Media

[默认情况下，Dynamic Media 处于禁用状态。](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)要利用Dynamic Media功能，您必须启用它。

>[!NOTE]
>
>Dynamic Media - Scene7模式仅用于Experience Manager作者实例。 因此，必须在Experience Manager Author实例&#x200B;**&#x200B;上配置`runmode=dynamicmedia_scene7` ，而不是Experience Manager Publish实例。

要启用Dynamic Media，您必须在终端窗口中输入以下内容，从命令行使用`dynamicmedia_scene7`运行模式开始Experience Manager（示例端口为4502）：

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5零停机时间{#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

将Experience Manager Dynamic Media从6.3升级到6.4或6.5现在包括零停机时间部署的能力。 要将所有预设和配置从`/etc`迁移到CRXDE Lite中的`/conf`，请确保运行以下curl命令。

>[!NOTE]
>
>如果您在兼容模式下运行Experience Manager实例（即已安装兼容性打包），则无需运行这些命令。

对于所有具有或没有兼容性包的升级，您都可以通过运行以下Linux® curl命令复制Dynamic Media最初附带的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要将您从`/etc`创建的任何自定义查看器预设和配置迁移到`/conf`，请运行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安装功能包18912以批量迁移{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是&#x200B;*可选*。

功能包18912允许您通过FTP批量摄取资源，或将资源从Dynamic Media — 混合模式或Dynamic Media Classic迁移到Dynamic Media - Scene7模式(Experience Manager)。 可从[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)获取。

有关详细信息，请参阅[安装功能包18912以进行批量资源迁移](/help/assets/bulk-ingest-migrate.md)。

## 在Cloud Services{#configuring-dynamic-media-cloud-services}中创建Dynamic Media配置

**配置Dynamic Media**  — 在收到包含Dynamic Media凭据的供应电子邮件后，必须打开Dynamic Media Classic桌 [面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户以更改密码。供应电子邮件中提供的密码是系统生成的，并且仅用于临时密码。 请务必更新密码，以便设置Dynamic MediaCloud Service时使用正确的凭据。

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**在Cloud Services中创建Dynamic Media配置**

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按工具图标，然后点按&#x200B;**[!UICONTROL Cloud Services> Dynamic Media配置]**。
1. 在 Dynamic Media 配置浏览器页面的左侧窗格中，点按&#x200B;**[!UICONTROL 全局]**（请勿点按或选择&#x200B;**[!UICONTROL 全局]**&#x200B;左侧的文件夹图标），然后点按&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;页面中，输入标题、Dynamic Media帐户电子邮件地址和密码，然后选择您的区域。 此信息是通过供应电子邮件中的Adobe提供给您的。 如果您未收到该电子邮件，请与Adobe客户服务联系。

   点按&#x200B;**[!UICONTROL 连接到Dynamic Media]**。

   >[!NOTE]
   在您收到包含Dynamic Media凭据的供应电子邮件后，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户以更改密码。 供应电子邮件中提供的密码是系统生成的，并且仅用于临时密码。 请务必更新密码，以便设置Dynamic MediaCloud Service时使用正确的凭据。

1. 连接成功时，请设置以下内容。 带有星号(*)的标题为必填项：

   * **[!UICONTROL 公司]** -Dynamic Media帐户的名称。您有多个Dynamic Media帐户。 例如，您可能具有不同的子品牌、部门、阶段或生产环境。

   * **[!UICONTROL 公司根文件夹路径]**

   * **[!UICONTROL 发布资产]**  — 您可以从以下三个选项中进行选择：
      * **[!UICONTROL 即]** 时意味着上传资产时，系统会立即收录资产并提供URL/Embed。发布资产不需要用户干预。
      * **[!UICONTROL 激]** 活后，即在提供URL/嵌入链接之前，您必须先显式发布资产。<br><!-- CQDOC-17478, Added March 9, 2021-->从Experience Manager 6.5.8开始，Experience Manager Publish实例反映的是Dynamic Media元数据值准确无误，如仅在“激活 `dam:scene7Domain` 时” `dam:scene7FileStatus` 和“ **[!UICONTROL 激活]** 时”发布模式中。要启用此功能，请安装Service Pack 8，然后重新启动Experience Manager。 转至Sling Config Manager。 查找`Scene7ActivationJobConsumer Component`的配置或创建新配置)。 选中复选框&#x200B;**[!UICONTROL 在Dynamic Media发布]**&#x200B;后复制元数据，然后点按&#x200B;**[!UICONTROL 保存]**。

         ![“在Dynamic Media发布后复制元数据”复选框](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 选择]** 性发布此选项可让您控制在Dynamic Media中发布的文件夹。它允许您使用智能裁剪或动态演绎版等功能，或确定仅在Experience Manager中发布哪些文件夹以进行预览。 这些相同的资产&#x200B;*不*&#x200B;已发布到Dynamic Media，以便在公共域中进行投放。<br>您可以在Dynamic Media云配置中 **[!UICONTROL 在此]** 处设置此选项，或者，如果您愿意，也可以选择在文件夹属性中的文件夹级别设置 **[!UICONTROL 此选项]**。<br>请参阅[使用 Dynamic Media 中的“选择性发布”功能。](/help/assets/selective-publishing.md)<br>如果您稍后更改此配置，或稍后在文件夹级别更改它，则这些更改仅影响您从该点向前上传的新资产。在您从&#x200B;**[!UICONTROL 快速发布]**&#x200B;或&#x200B;**[!UICONTROL 管理发布]**&#x200B;对话框手动更改文件夹中现有资产的发布状态之前，这些资产将保持原样。
   * **[!UICONTROL 安全预览服务器]**  — 允许您指定指向安全再现预览服务器的URL路径。也就是说，在生成再现后，Experience Manager可以安全访问和预览远程Dynamic Media再现(不会将二进制文件发送回Experience Manager实例)。
除非您有特殊安排来使用您自己的公司服务器或特殊服务器，否则Adobe建议您按指定的方式保留此设置。

   * **[!UICONTROL 同步所有内容]**  — 默 <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->认为选中。如果您希望在同步到Dynamic Media时有选择地包括或排除资源，请取消选择此选项。 取消选择此选项后，您可以从以下两种Dynamic Media同步模式中进行选择：

   * **[!UICONTROL Dynamic Media 同步模式]**
      * **[!UICONTROL 默认情况下启用]**  — 默认情况下，配置将应用于所有文件夹，除非您专门为排除标记文件夹。  <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 默认情况下禁用]**  — 在显式标记选定的文件夹以同步到Dynamic Media之前，此配置不会应用于任何文件夹。要将选定的文件夹标记为同步到Dynamic Media，请选择一个资产文件夹，然后在工具栏中点按&#x200B;**[!UICONTROL 属性]**。 在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉列表中，从以下三个选项中进行选择。 完成后，点按&#x200B;**[!UICONTROL 保存]**。 *记住：如果您选择了“同步所有内容”，则这三个&#x200B;**选项将**不可用。* 另请参 [阅在Dynamic Media的文件夹级别使用选择性发布。](/help/assets/selective-publishing.md)
         * **[!UICONTROL 继承]**  — 文件夹中没有显式同步值；相反，该文件夹会从其父文件夹之一或云配置中的默认模式继承同步值。通过工具提示显示继承的节目的详细状态。
         * **[!UICONTROL 为子文件夹启用]**  — 包括此子树中的所有内容以同步到Dynamic Media。特定于文件夹的设置将覆盖云配置中的默认模式。
         * **[!UICONTROL 对子文件夹禁用]**  — 将此子树中的所有内容从同步到Dynamic Media中排除。

   >[!NOTE]
   DMS7中不支持版本控制。 此外，仅当“编辑 Dynamic Media 配置”页面中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;时，并且直到首次激活资产时延迟激活才适用。
   激活资产后，所有更新都会立即实时发布到S7投放。

1. 点按&#x200B;**[!UICONTROL 保存]**。
1. 要在发布Dynamic Media内容之前安全地预览该内容，允许列表您必须“”Experience Manager作者实例以连接到Dynamic Media:

   * 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。 您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与技术支持联系。

   * 在页面右上角附近的导航栏上，点按&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。

   * 在“图像服务器发布”页面的“发布上下文”下拉列表中，选择&#x200B;**[!UICONTROL 测试图像服务]**。
   * 对于“客户端地址筛选器”，点按&#x200B;**[!UICONTROL 添加]**。
   * 要启用（打开）地址，请选中该复选框。 输入Experience Manager作者实例的IP地址（不是调度程序IP）。
   * 点按&#x200B;**[!UICONTROL 保存]**。

现在您已完成基本配置；您已准备好使用Dynamic Media - Scene7模式。

如果要进一步自定义配置，您可以选择在Dynamic Media - Scene7模式](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)中配置高级设置下完成任何任务。[

## （可选）在Dynamic Media - Scene7模式{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}中配置高级设置

如果要进一步自定义Dynamic Media - Scene7模式的配置和设置，或优化其性能，您可以完成以下一个或多个&#x200B;*可选*&#x200B;任务:

* [（可选）Dynamic Media - Scene7模式设置和配置](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（可选）调整Dynamic Media - Scene7模式的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（可选）筛选要复制的资产](#optional-filtering-assets-for-replication)

### （可选）Dynamic Media的设置和配置 — Scene7模式设置{#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

当您处于运行模式`dynamicmedia_scene7`时，请使用Dynamic Media Classic用户界面更改您的Dynamic Media设置。

上述某些任务要求您打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

设置和配置任务包括：

* [为图像服务器发布设置](#publishing-setup-for-image-server)
* [配置应用程序常规设置](#configuring-application-general-settings)
* [配置色彩管理](#configuring-color-management)
* [编辑支持的格式的MIME类型](#editing-mime-types-for-supported-formats)
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)
* [创建批集预设以自动生成图像集和旋转集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### 发布图像服务器{#publishing-setup-for-image-server}的设置

默认情况下，“发布设置”设置会确定如何从Dynamic Media传送资产。 如果未指定任何设置，则Dynamic Media会根据发布设置中定义的默认设置传送资产。 例如，传送不包含分辨率属性的图像的请求将生成具有“默认对象分辨率”设置的图像。

配置发布设置：在Dynamic Media Classic中，点按&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。

“图像服务器”屏幕会为传送图像建立默认设置。 有关每个设置的说明，请参阅UI屏幕。

* **[!UICONTROL 请求属性]**  — 这些设置对可以从服务器传送的图像施加限制。
* **[!UICONTROL 默认请求属性]**  — 这些设置与图像的默认外观有关。
* **[!UICONTROL 常用缩览图属性]**  — 这些设置与缩览图图像的默认外观有关。
* **[!UICONTROL 目录字段的默认值]** — 这些设置与图像的分辨率和默认缩略图类型有关。
* **[!UICONTROL 色彩管理属性]**  — 这些设置决定使用哪些ICC色彩用户档案。
* **[!UICONTROL 兼容性属性]**  — 通过此设置，文本图层中的前导和尾部段落可以像在版本3.6中一样处理，以实现向后兼容。
* **[!UICONTROL 本地化支持]**  — 这些设置允许您管理多个区域设置属性。它还允许您指定区域设置映射字符串，以便定义要在查看器中支持各种工具提示的语言。 有关设置&#x200B;**[本地化支持]**&#x200B;的详细信息，请参阅[设置资产本地化时的注意事项](https://help.adobe.com/en_US/scene7/using/WS997f1dc4cb0179f034e07dc31412799d19a-8000.html)。

#### 配置应用程序常规设置{#configuring-application-general-settings}

要打开“应用程序常规设置”页，请在Dynamic Media Classic全局导航栏中，点按&#x200B;**[!UICONTROL 设置>应用程序设置>常规设置]**。

**[!UICONTROL 服务器]**  — 在帐户设置时，Dynamic Media会自动为您的公司提供分配的服务器。这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。 除非Adobe客户关怀部门明确指示，否则不要更改任何服务器名称。

**[!UICONTROL 覆盖图像]** - Dynamic Media不允许两个文件具有相同的名称。每个项目的URL ID（文件名减去扩展名）必须唯一。 这些选项指定如何上传替换资产：是替换原始图像，还是变成重复。 重复资产使用“–1”重命名（例如，chair.tif更名为chair-1.tif）。 这些选项影响上传到与原始文件夹不同的文件夹的资产，或文件扩展名与原始文件夹不同的资产（如JPG、TIF或PNG）。

* **[!UICONTROL 在当前文件夹中覆盖，基本图像名称/扩展名相同]**  — 此选项是最严格的替换规则。它要求您将替换图像上传到与原始图像相同的文件夹，并且替换图像的文件扩展名与原始图像的扩展名相同。 如果这些要求未得到满足，则会创建重复。

>[!NOTE]
要保持与Experience Manager的一致性，请始终选择以下设置：**在当前文件夹中覆盖，基本图像名称/扩展名相同**

* **[!UICONTROL 在任何文件夹中覆盖相同的基本资源名称/扩展名]**  — 要求替换图像的文件扩展名与原始图像相同（例如，chair.jpg必须替换chair.jpg，而不是chair.tif）。但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新后的图像驻留在新文件夹中；在文件的原始位置找不到文件
* **[!UICONTROL 在任意文件夹中覆盖相同的基本资产名称，而不管其扩展名]**  — 此选项是最包容的替换规则。您可以将替换图像上传到与原始图像不同的文件夹，以其他文件扩展名上传文件，并替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将驻留在其上传到的新文件夹中。

**[!UICONTROL 默认颜色用户档案]**  — 有关其 [他信](#configuring-color-management) 息，请参阅配置颜色管理。

>[!NOTE]
默认情况下，当您选择&#x200B;**[!UICONTROL 呈现]**&#x200B;时，系统会显示 15 种呈现形式，当您在资产的详细信息视图中选择&#x200B;**[!UICONTROL 查看器]**&#x200B;时，系统会显示 15 个查看器预设。您可以提高此限制。请参阅[增加显示](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)或[的图像预设数量增加显示](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)的查看器预设数量。


#### 配置色彩管理{#configuring-color-management}

Dynamic Media色彩管理可让您对资产进行色彩校正。 借助颜色校正，摄取的资源可保留其色彩空间（RGB、CMYK、灰色）和嵌入的颜色用户档案。 当您请求动态再现时，图像颜色会使用CMYK、RGB或灰色输出校正到目标色彩空间。 请参阅[配置图像预设](/help/assets/managing-image-presets.md)。

要配置默认颜色属性，以便在请求图像时启用颜色校正：

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后使用在设置过程中提供的凭据登录到您的帐户。
1. 导航到&#x200B;**[!UICONTROL 设置>应用程序设置]**。
1. 展开&#x200B;**[!UICONTROL 发布设置]**&#x200B;区域，然后选择&#x200B;**[!UICONTROL 图像服务器]**。设置发布实例的默认设置时，将&#x200B;**[!UICONTROL 发布上下文]**&#x200B;设置为&#x200B;**[!UICONTROL 图像提供]**。
1. 滚动到要更改的属性。 例如，**[!UICONTROL 色彩管理属性]**&#x200B;区域中的属性。

   可以设置以下颜色校正属性：

   * **[!UICONTROL CMYK默认色彩空间]**  — 默认CMYK颜色用户档案的名称
   * **[!UICONTROL 灰度默认色彩空间]**  — 默认灰色用户档案的名称
   * **[!UICONTROL RGB默认色彩空间]**  — 默认RGB色彩用户档案的名称
   * **[!UICONTROL 颜色转换渲染方法]**  — 指定渲染方法。可接受的值为：**[!UICONTROL 可感知]**、**[!UICONTROL 相对测温]**、**[!UICONTROL 饱和度]**、**[!UICONTROL 绝对测温]**。 Adobe建议将&#x200B;**[!UICONTROL relative]**&#x200B;作为默认值。

1. 点按&#x200B;**[!UICONTROL 保存]**。

例如，可以将 **[!UICONTROL RGB 默认色彩空间]**&#x200B;设置为 *sRGB*，将 **[!UICONTROL CMYK 默认色彩空间]**&#x200B;设置为 *WebCoated*。

这样做将执行以下操作：

* 启用RGB和CMYK图像的颜色校正。
* 假定没有颜色用户档案的RGB图像位于&#x200B;*sRGB*&#x200B;色彩空间中。
* 假定没有颜色用户档案的CMYK图像位于&#x200B;*WebCoated*&#x200B;色彩空间中。
* 返回RGB输出的动态演绎版，在&#x200B;*sRGB*&#x200B;色彩空间中返回它。
* 返回CMYK输出的动态演绎版，在&#x200B;*WebCoated*&#x200B;色彩空间中返回它。

#### 编辑支持的格式{#editing-mime-types-for-supported-formats}的MIME类型

您可以定义Dynamic Media要处理的资产类型，并自定义高级资产处理参数。 例如，您可以指定资产处理参数以执行以下操作：

* 将Adobe PDF转换为eCatalog资源。
* 将Adobe Photoshop文档(.PSD)转换为横幅模板资产以进行个性化。
* 栅格化Adobe Illustrator文件(.AI)或Adobe Photoshop封装PostScript®文件(.EPS)。
* [视频](/help/assets/video-profiles.md) 概要 [和](/help/assets/image-profiles.md) 图像概要文件可用于定义视频和图像的处理。

请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

**要编辑支持的格式的MIME类型，请执行以下操作：**

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite]**。
1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择MIME类型。
1. 在CRXDE Lite页面的右侧，在下半部分：

   * 多次 — 单击&#x200B;**[!UICONTROL enabled]**&#x200B;字段。 默认情况下，所有资产MIME类型都处于启用状态（设置为&#x200B;**[!UICONTROL true]**），这意味着资产将同步到Dynamic Media进行处理。 如果您希望不处理此资产mime类型，请将此设置更改为&#x200B;**[!UICONTROL false]**。

   * 多次点按&#x200B;**[!UICONTROL jobParam]**&#x200B;可打开其关联的文本字段。 有关可用于给定mime类型的允许处理参数值的列表，请参阅[支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 执行下列操作之一：

   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页面的菜单栏上，点按&#x200B;**[!UICONTROL 保存全部]**。

1. 在页面的左上角，点按&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回Experience Manager。

#### 为不支持的格式{#adding-mime-types-for-unsupported-formats}添加MIME类型

您可以为Experience Manager资产中不支持的格式添加自定义MIME类型。 通过将MIME类型移到`image_`之前，确保您在CRXDE Lite中添加的任何新节点不会被Experience Manager删除。 另外，请确保其启用值设置为&#x200B;**[!UICONTROL false]**。

**要为不支持的格式添加MIME类型，请执行以下操作：**

1. 在Experience Manager中，点按&#x200B;**[!UICONTROL 工具>操作> Web控制台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的浏览器选项卡会打开到&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名称的右侧，点按&#x200B;**[!UICONTROL 编辑配置值]**（铅笔图标）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7资产MIME类型服务**&#x200B;页面上，点按任意加号图标&lt;+>。 在表中点按加号以添加新MIME类型的位置很小。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 在刚刚添加的空文本字段中键入`DWG=image/vnd.dwg`。

   示例`DWG=image/vnd.dwg`仅供说明之用。 您在此处添加的MIME类型可以是任何其他不支持的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，点按&#x200B;**[!UICONTROL 保存]**。

   此时，您可以关闭具有打开的Adobe Experience Manager Web Console“配置”页的浏览器选项卡。

1. 返回到具有打开的Experience Manager控制台的浏览器选项卡。
1. 从Experience Manager，点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖动mime类型`image_vnd.dwg`并将其直接放在树中`image_`的上方，如下面的屏幕截图所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 在&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡的&#x200B;**[!UICONTROL enabled]**&#x200B;行&#x200B;**[!UICONTROL 值]**&#x200B;列标题下，在MIME类型`image_vnd.dwg`中，多次点按值以打开&#x200B;**[!UICONTROL 值]**&#x200B;下拉列表。
1. 在字段中键入`false`(或从下拉列表中选择&#x200B;**[!UICONTROL false]**)。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite页面的左上角附近，点按&#x200B;**[!UICONTROL 全部保存]**。

#### 创建批集预设以自动生成图像集和旋转集{#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

在资产上传到Dynamic Media时，使用批量集预设自动创建图像集或旋转集。

首先，定义资产在集中的分组方式的命名约定。 然后，创建一个批集预设，它是一组唯一命名的、自包含的指令集。 它必须定义如何使用与预设菜谱中定义的命名约定匹配的图像构建集合。

在上传文件时，Dynamic Media会自动创建一个集，其中包含与活动预设中定义的命名约定相匹配的所有文件。

**配置默认命名**

创建用于任何批集预设处方的默认命名约定。 在批集预设定义中选择的默认命名约定可能是公司批量生成集所需的全部。 将创建批集预设，以使用您定义的默认命名约定。 在公司定义的默认命名有例外情况时，您可以创建具有特定内容集所需的替代自定义命名约定的任意批集预设。

虽然使用批量集预设功能不需要设置默认命名约定，但最佳实践是建议您使用默认命名约定。 它允许您定义要分组到一个集中的命名约定的任意多个元素，以便简化批量集创建。

作为替代方法，您可以使用没有可用表单字段的&#x200B;**[!UICONTROL 视图代码]**。 在此视图中，您完全使用常规表达式创建命名约定定义。

两个元素可用于定义：“匹配”和“基名”。 这些字段允许您定义命名约定的所有元素，并标识用于命名包含这些元素的集合的约定部分。 公司的单个命名约定通常对这些元素中的每一个使用一行或多行定义。 您可以使用任意多行进行唯一定义，并将它们分组为不同的元素，如主图像、颜色元素、替代视图元素和色板元素。

**配置默认命名：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与技术支持联系。

1. 在页面顶部附近的导航栏上，点按&#x200B;**[!UICONTROL 设置>应用程序设置>批量集预设>默认命名]**。
1. 选择&#x200B;**[!UICONTROL 查看表单]**&#x200B;或&#x200B;**[!UICONTROL 查看代码]**，以指定要查看的方式并输入有关每个元素的信息。

   您可以选中&#x200B;**[!UICONTROL 视图代码]**&#x200B;复选框，以在表单选择旁边视图常规表达式值构建。 如果表单视图因任何原因限制您，您可以输入或更改这些值以帮助定义命名约定的元素。 如果无法在表单视图中分析您的值，则表单字段将变为非活动状态。

   >[!NOTE]
   取消激活的表单域不会验证您的常规表达式是否正确。 您将看到在结果行之后为每个元素构建的常规表达式的结果。 完整的常规表达式显示在页面底部。

1. 根据需要展开每个元素并输入要使用的命名约定。
1. 根据需要，执行以下任一操作：

   * 点按&#x200B;**[!UICONTROL 添加]**&#x200B;可为元素添加另一个命名约定。
   * 点按&#x200B;**[!UICONTROL 删除]**&#x200B;可删除元素的命名约定。

1. 执行下列操作之一：

   * 点按&#x200B;**[!UICONTROL 另存为]**&#x200B;并键入预设的名称。
   * 如果您正在编辑现有预设，请点按&#x200B;**[!UICONTROL 保存]**。

**创建批集预设**

Dynamic Media使用批量集预设将资产组织为一组图像（替代图像、颜色选项、360旋转），以便在查看器中显示。 批量集预设会在Dynamic Media中与资产上传流程一起自动运行。

您可以创建、编辑和管理批集预设。 有两种形式的批集预设定义：一个用于可设置的默认命名约定，另一个用于动态创建的自定义命名约定。

您可以使用表单字段方法定义批集预设或代码方法(通过代码方法可使用常规表达式)。 与默认命名一样，您可以在表单视图中定义的同时选择视图代码，并使用常规表达式构建定义。 或者，您也可以取消选中“视图”以使用其中一个或另一个专用。

**要创建批集预设，请执行以下操作：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与技术支持联系。

1. 在页面顶部附近的导航栏上，点按&#x200B;**[!UICONTROL 设置>应用程序设置>批集预设>批集预设]**。

   **[!UICONTROL 视图表]**&#x200B;单（如“详细信息”页面右上角所设置）是默认视图。

1. 在“预设”列表面板中，点按&#x200B;**[!UICONTROL 添加]**&#x200B;以激活屏幕右侧“详细信息”面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在批集类型下拉菜单中，选择预设类型。
1. 执行下列操作之一：

   * 如果您使用的是之前在&#x200B;**[!UICONTROL 应用程序设置>批集预设>默认命名]**&#x200B;下设置的默认命名约定，请展开&#x200B;**[!UICONTROL 资产命名约定]**，然后在文件命名下拉列表中，点按&#x200B;**[!UICONTROL 默认]**。

   * 要在设置预设时定义新的命名约定，请展开&#x200B;**[!UICONTROL 资产命名约定]**，然后在“文件命名”下拉列表中，点按&#x200B;**[!UICONTROL 自定义]**。

1. 对于“序列”顺序，定义在Dynamic Media中对图像集进行分组后图像的显示顺序。

   默认情况下，资产按字母数字顺序排列。 但是，您可以使用逗号分隔的常规表达式列表来定义顺序。

1. 对于“设置命名和创建约定”，请指定在“资产命名约定”中定义的基名的后缀或前缀。 此外，定义在Dynamic Media文件夹结构中创建集的位置。

   如果您定义了大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建一个“图像集”文件夹，然后将生成的集放在此处。

1. 在“详细信息”面板中，点按&#x200B;**[!UICONTROL 保存]**。
1. 点按新预设名称旁的&#x200B;**[!UICONTROL 活动]**。

   激活预设可确保在您将资产上传到Dynamic Media时，批集预设会应用于生成该集。

**创建批集预设以自动生成2D旋转集**

您可以使用批集类型&#x200B;**[!UICONTROL 多轴旋转集]**&#x200B;创建可自动生成2D旋转集的方法。 图像分组使用行和列规则表达式，以便图像资产在多维数组中的相应位置正确对齐。 在多轴旋转集中，不存在必须具有的最小或最大行数或列数。

例如，假设要创建名为`spin-2dspin`的多轴旋转集。 您有一组包含三行的旋转集图像，每行12幅图像。 图像的名称如下：

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

通过此信息，您可以按如下方式创建批集类型菜谱：

![chlimage_1-560](assets/chlimage_1-560.png)

旋转集的共享资产名称部分的分组将添加到&#x200B;**匹配**&#x200B;字段（高亮显示）。 资产名称中包含行和列的变量部分将分别添加到 **行** 和 **列字段** 。

上传和发布旋转集后，您可以激活&#x200B;**上传作业选项**&#x200B;对话框中&#x200B;**批集预设**&#x200B;下方 2D 旋转集方法的名称。

**要创建批集预设以自动生成2D旋转集，请执行以下操作：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与技术支持联系。

1. 在页面顶部附近的导航栏上，点按&#x200B;**[!UICONTROL 设置] > [!UICONTROL 应用程序设置] > [!UICONTROL 批集预设] > [!UICONTROL 批集预设]**。

   **[!UICONTROL 视图表]**&#x200B;单（如“详细信息”页面右上角所设置）是默认视图。

1. 在“预设”列表面板中，点按&#x200B;**[!UICONTROL 添加]**&#x200B;以激活屏幕右侧“详细信息”面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在“批集类型”下拉菜单中，选择&#x200B;**[!UICONTROL 资产集]**。
1. 在“子类型”下拉列表中，选择&#x200B;**[!UICONTROL 多轴旋转集]**。
1. 展开&#x200B;**[!UICONTROL 资产命名约定]**，然后在“文件命名”下拉列表中，点按&#x200B;**[!UICONTROL 自定义]**。
1. 使用&#x200B;**[!UICONTROL 匹配]**&#x200B;和（可选）**[!UICONTROL 基本名称]**&#x200B;属性定义组成分组的图像资产命名的正则表达式。

   例如，您的文本“匹配”常规表达式可能如下所示：

   `(w+)-w+-w+`

1. 展开&#x200B;**[!UICONTROL 行列位置]**，然后为2D旋转集数组中的图像资产的位置定义名称格式。

   使用括号将行或列位置置于文件名中。

   例如，对于行常规表达式，它可以如下所示：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   对于列常规表达式，它可以如下所示：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   上述范例仅供说明。 您可以创建常规表达式，但是您希望创建的内容适合您的需求。

   >[!NOTE]
   如果行和列常规表达式的组合无法确定资产在多维旋转集数组中的位置，则不会将资产添加到该集。 还会记录错误。

1. 对于“设置命名和创建约定”，请指定在“资产命名约定”中定义的基名的后缀或前缀。

   此外，定义旋转集在Dynamic Media经典文件夹结构中的创建位置。

   如果您定义了大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建一个旋转集文件夹，将生成的集放在此处。

1. 在“详细信息”面板中，点按&#x200B;**[!UICONTROL 保存]**。
1. 点按新预设名称旁的&#x200B;**[!UICONTROL 活动]**。

   激活预设可确保在您将资产上传到Dynamic Media时，批集预设会应用于生成该集。

### （可选）调整Dynamic Media - Scene7模式{#optional-tuning-the-performance-of-dynamic-media-scene-mode}的性能

为了保持Dynamic Media - Scene7模式平稳运行，Adobe建议使用以下同步性能/可伸缩性微调提示：

* 更新预定义的作业参数以处理不同的文件格式。
* 更新预定义的Granite工作流（视频资产）队列工作线程。
* 更新预定义的Granite临时工作流（图像和非视频资产）队列工作线程。
* 更新到Dynamic Media Classic服务器的最大上载连接数。

#### 更新预定义的作业参数以处理不同的文件格式

您可以调整作业参数，以便在上传文件时加快处理速度。 例如，如果您上传PSD文件，但不想将它们作为模板进行处理，则可以将图层提取设置为false（关闭）。 在这种情况下，调整的作业参数如下所示：`process=None&createTemplate=false`。

如果确实要打开模板创建，请使用以下参数：`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议对PDF、PostScript®和PSD文件使用以下“调整”作业参数：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 文件类型 | 建议的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新任何这些参数，请按照[启用基于MIME类型的资产/Dynamic Media经典上传作业参数support](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)中的步骤操作。

#### 更新Granite临时工作流队列{#updating-the-granite-transient-workflow-queue}

Granite Transit工作流队列用于&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。 在Dynamic Media中，它用于图像摄取和处理。

**要更新Granite临时工作流队列，请执行以下操作：**

1. 导航到[https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr)并搜索&#x200B;**队列：Granite临时工作流队列**。

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将数字更改为所需值。

   您可以增加&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;以充分支持将文件重新上载到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用大值。 但是，请注意，使用大值（如核心数的2倍）可能会对其他并发活动产生负面影响。 因此，请根据您的特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流队列{#updating-the-granite-workflow-queue}

Granite工作流队列用于非临时工作流。 在Dynamic Media中，它用于使用&#x200B;**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流处理视频。

**要更新Granite工作流队列，请执行以下操作：**

1. 导航到`https://<server>/system/console/configMgr`并搜索&#x200B;**队列：Granite工作流队列**。

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将数字更改为所需值。

   您可以增加“最大并行作业数”，以充分支持将文件大量上传到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用大值。 但是，请注意，使用大值（如核心数的2倍）可能会对其他并发活动产生负面影响。 因此，请根据您的特定用例测试和调整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上载连接{#updating-the-scene-upload-connection}

Scene7上传连接设置将Experience Manager资源同步到Dynamic Media Classic服务器。

**要更新Dynamic Media Classic上传连接，请执行以下操作：**

1. 导航至 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 连接数]**&#x200B;字段和/或&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段中，根据需要更改数字。

   **[!UICONTROL 连接数]**&#x200B;设置控制允许Experience ManagerDynamic Media上载的HTTP连接的最大数量；通常，十个连接的预定义值就足够了。

   **[!UICONTROL 活动作业超时]**&#x200B;设置决定了在投放服务器中发布已上传Dynamic Media资产的等待时间。 默认情况下，此值为2100秒或35分钟。

   对于大多数用例，设置2100就足够了。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存]**。

### （可选）筛选用于复制的资产{#optional-filtering-assets-for-replication}

在非Dynamic Media部署中，您将&#x200B;*所有*&#x200B;资产（图像和视频）从Experience Manager作者环境复制到Experience Manager发布节点。 此工作流是必需的，因为Experience Manager发布服务器也会传送资产。

但是，在Dynamic Media部署中，由于资产是通过Cloud Service交付的，因此无需将这些相同的资产复制到Experience Manager发布节点。 这种“混合发布”工作流可避免复制资源时需要额外的存储成本和更长的处理时间。 其他内容（如“网站”页面）将继续从“Experience Manager”发布节点提供。

这些过滤器为您提供了一种方法，使您能够排除&#x200B;*资产，使其无法复制到Experience Manager发布节点。*

#### 使用默认资产过滤器进行复制{#using-default-asset-filters-for-replication}

如果您使用Dynamic Media进行成像或视频，或者同时使用这两种方法，则可以使用Adobe按原样提供的默认过滤器。 默认情况下，以下过滤器处于活动状态：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>筛选器</strong></td>
   <td><strong>MIME类型</strong></td>
   <td><strong>演绎版</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media图像投放</td>
   <td><p>滤镜图像</p> <p>过滤器集</p> <p> </p> </td>
   <td><p>具有<strong>image/</strong>的开始</p> <p>包含<strong>application/</strong>，以<strong>set</strong>结尾。</p> </td>
   <td>现成的“滤镜图像”（适用于单个图像资产，包括交互式图像）和“滤镜集”（适用于旋转集、图像集、混合媒体集和旋转集）将：
    <ul>
     <li>从复制原始图像和静态图像演绎版中排除。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media视频投放</td>
   <td>filter-video</td>
   <td>开始具有<strong>video/</strong></td>
   <td>现成的“filter-video”将：
    <ul>
     <li>从复制中排除原始视频和静态缩略图再现。<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
过滤器应用于MIME类型，不能特定于路径。

#### 自定义用于复制{#customizing-asset-filters-for-replication}的资产过滤器

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite]**。
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/publish/jcr:content/damRenditionFilters`以查看过滤器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 要定义筛选器的MIME类型，可以按如下方式查找Mime类型：

   在左边栏中，展开`content > dam > <locate_your_asset> > jcr:content > metadata`，然后在表中找到`dc:format`。

   下图是资产到`dc:format`的路径示例。

   ![chlimage_1-18](assets/chlimage_1-3.png)

   请注意，资产`Fiji Red.jpg`的`dc:format`是`image/jpeg`。

   要使此滤镜应用于所有图像（无论其格式如何），请将该值设置为`image/*`，其中`*`是应用于任何格式的所有图像的常规表达式。

   要使滤镜仅应用于JPEG类型的图像，请输入值`image/jpeg`。

1. 定义要包括或从复制中排除的演绎版。

   可用于筛选复制的字符包括：

<table>
 <tbody>
  <tr>
   <td><strong>要使用的字符</strong></td>
   <td><strong>如何过滤器资产进行复制</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>通配符</td>
  </tr>
  <tr>
   <td>+</td>
   <td>包括用于复制的资产。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>从复制中排除资产。</td>
  </tr>
 </tbody>
</table>

导航至 `content/dam/<locate your asset>/jcr:content/renditions`.

下图是资产的演绎版示例。

![chlimage_1-4](assets/chlimage_1-4.png)

如果只想复制原件，则输入`+original`。
