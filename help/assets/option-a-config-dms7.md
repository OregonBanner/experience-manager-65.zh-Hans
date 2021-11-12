---
title: 选项A — 配置Dynamic Media - Scene7模式
description: 了解如何配置Dynamic Media - Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: bfa41deb156ffd0adb8138c11548912bc954f084
workflow-type: tm+mt
source-wordcount: '11558'
ht-degree: 4%

---

# 选项A — 配置Dynamic Media - Scene7模式{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>选项A — 我写的两个新主题将被删除。 但是，在删除这些主题之前，其所有内容都已移到此主题中，并移到了我已讨论常规设置和发布设置的各个区域。

如果您使用为开发、暂存和生产等不同环境设置的Adobe Experience Manager，则请为每个环境配置Dynamic MediaCloud Services。

## Dynamic Media - Scene7模式的架构图 {#architecture-diagram-of-dynamic-media-scene-mode}

**里克：保持原样**

以下架构图介绍了Dynamic Media - Scene7模式的工作方式。

使用新架构时，Experience Manager负责主源资产以及与Dynamic Media的同步，以便进行资产处理和发布：

1. 将主源资产上传到Experience Manager后，该资产会复制到Dynamic Media。 此时，Dynamic Media将处理所有资产处理和演绎版生成，如图像的视频编码和动态变体。
(在Dynamic Media - Scene7模式下，默认上传文件大小为2 GB或更小。 要启用上传文件大小为2 GB至15 GB的功能，请参阅 [（可选）配置Dynamic Media - Scene7模式，以上传大于2 GB的资产](#optional-config-dms7-assets-larger-than-2gb).)
1. 生成演绎版后，Experience Manager可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager实例)。
1. 在内容准备好发布和批准后，它将触发Dynamic Media服务，以将内容推送到分发服务器，并在CDN（内容分发网络）处缓存内容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>以下功能列表要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN。 这些功能不支持任何其他自定义CDN。
>
>* [智能图像处理](/help/assets/imaging-faq.md)
>* [缓存失效](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [热链接保护](/help/assets/hotlink-protection.md)
>* [HTTP/2 内容交付](/help/assets/http2.md)
>* CDN级别的URL重定向
>* Akamai ChinaCDN（在中国实现最佳交付）


## 在Scene7模式下启用Dynamic Media {#enabling-dynamic-media-in-scene-mode}

**里克：保持原样**

[默认情况下，Dynamic Media 处于禁用状态。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)要利用Dynamic Media功能，您必须启用它。

>[!WARNING]
>
>Dynamic Media - Scene7模式适用于 *仅Experience Manager创作实例*. 因此，您必须配置 `runmode=dynamicmedia_scene7` 在Experience Manager创作实例上， *not* Experience Manager发布实例。

要启用Dynamic Media，您必须使用 `dynamicmedia_scene7` 通过在终端窗口中输入以下命令行来运行模式（使用的示例端口为4502）：

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5，零停机时间 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**里克：保持原样**

现在，将Experience ManagerDynamic Media从6.3升级到6.4或6.5中，即可实现零停机时间部署。 要从 `/etc` to `/conf` 在CRXDE Lite中，确保运行以下curl命令。

>[!NOTE]
>
>如果您在兼容性模式下运行Experience Manager实例（即，已安装兼容包），则无需运行这些命令。

无论是否具有兼容包，您都可以对所有升级，通过运行以下Linux® curl命令，复制Dynamic Media最初附带的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要迁移您通过 `/etc` to `/conf`，运行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安装用于批量资产迁移的功能包18912 {#installing-feature-pack-for-bulk-asset-migration}

**里克：保持原样**

功能包18912的安装是 *可选*.

功能包18912允许您通过FTP批量摄取资产，或在Experience Manager中将资产从Dynamic Media — 混合模式或Dynamic Media Classic迁移到Dynamic Media - Scene7模式。 可从 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

请参阅 [安装用于批量资产迁移的功能包18912](/help/assets/bulk-ingest-migrate.md) 以了解更多信息。

## 在Cloud Services中创建Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

**里克：保持原样**

**在配置Dynamic Media之前**  — 收到包含Dynamic Media凭据的配置电子邮件后，必须打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户以更改密码。 预配电子邮件中提供的密码是系统生成的，并且仅准备为临时密码。 请务必更新密码，以便使用正确的凭据设置Dynamic MediaCloud Service。

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**要在Cloud Services中创建Dynamic Media配置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台，然后选择工具图标，然后转到 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media配置]**.
1. 在Dynamic Media配置浏览器页面的左窗格中，选择 **[!UICONTROL 全球]** (请勿选择 **[!UICONTROL 全球]**)，然后选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建Dynamic Media配置]** 页面，输入标题、Dynamic Media帐户电子邮件地址、密码，然后选择您所在的区域。 此信息通过配置电子邮件中的Adobe提供给您。 如果您未收到电子邮件，请联系Adobe客户支持。

   选择 **[!UICONTROL 连接到Dynamic Media]**.

   >[!NOTE]
   **里克：保持原样??** 在收到包含Dynamic Media凭据的配置电子邮件后，打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户以更改密码。 预配电子邮件中提供的密码是系统生成的，并且仅准备为临时密码。 请务必更新密码，以便使用正确的凭据设置Dynamic MediaCloud Service。

1. 连接成功后，请设置以下内容。 带星号(*)的标题是必填项：

   * **[!UICONTROL 公司]** -Dynamic Media帐户的名称。 您有多个Dynamic Media帐户。 例如，您可以具有不同的子品牌、部门、暂存或生产环境。

   * **[!UICONTROL 公司根文件夹路径]**

   * **[!UICONTROL 发布资产]**  — 您可以从以下三个选项中进行选择：
      * **[!UICONTROL 立即]** 是指上传资产后，系统会摄取资产并立即提供URL/嵌入。 发布资产无需用户干预。
      * **[!UICONTROL 激活时]** 表示在提供URL/嵌入链接之前，必须先明确发布资产。<br><!-- CQDOC-17478, Added March 9, 2021-->从Experience Manager6.5.8开始，Experience Manager发布实例可反映准确的Dynamic Media元数据值，例如 `dam:scene7Domain` 和 `dam:scene7FileStatus` in **[!UICONTROL 激活时]** 仅发布模式。 要启用此功能，请安装Service Pack 8，然后重新启动Experience Manager。 转到Sling配置管理器。 查找的配置 `Scene7ActivationJobConsumer Component` 或创建新受众)。 选中复选框 **[!UICONTROL 在Dynamic Media发布后复制元数据]**，然后选择 **[!UICONTROL 保存]**.

         ![“在Dynamic Media发布后复制元数据”复选框](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 选择性发布]** 利用此选项，可控制在Dynamic Media中发布的文件夹。 它允许您使用智能裁剪或动态演绎版等功能，或确定哪些文件夹在Experience Manager中仅发布以进行预览。 这些资产是 *not* 发布在Dynamic Media中，以在公共域中交付。<br>您可以在 **[!UICONTROL Dynamic Media云配置]** 或者，如果您愿意，也可以选择在文件夹的 **[!UICONTROL 属性]**.<br>请参阅 [在Dynamic Media中使用“选择性发布”功能](/help/assets/selective-publishing.md).<br>如果您稍后更改此配置，或稍后在文件夹级别更改此配置，则这些更改仅会影响您从此时上传的新资产。 文件夹中现有资产的发布状态将保持原样，直到您手动从以下任一 **[!UICONTROL 快速发布]** 或 **[!UICONTROL 管理发布]** 对话框。
   * **[!UICONTROL 安全预览服务器]**  — 用于指定安全演绎版预览服务器的URL路径。 也就是说，在生成演绎版后，Experience Manager可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager实例)。
除非您有使用自己公司服务器或特殊服务器的特殊安排，否则Adobe建议您按指定的方式保留此设置。

   * **[!UICONTROL 同步所有内容]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->默认选中。 如果要在同步到Dynamic Media时有选择地包含或排除资产，请取消选择此选项。 取消选中此选项允许您从以下两种Dynamic Media同步模式中进行选择：

   * **[!UICONTROL Dynamic Media 同步模式]**
      * **[!UICONTROL 默认启用]**  — 默认情况下，配置将应用于所有文件夹，除非您专门标记文件夹以进行排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 默认情况下处于禁用状态]**  — 在您明确标记要同步到Dynamic Media的选定文件夹之前，不会将配置应用于任何文件夹。
要将选定的文件夹标记为同步到Dynamic Media，请选择一个资产文件夹，然后在工具栏中，选择 **[!UICONTROL 属性]**. 在 **[!UICONTROL 详细信息]** 选项卡 **[!UICONTROL Dynamic Media同步模式]** 下拉列表中，从以下三个选项中进行选择。 完成后，选择 **[!UICONTROL 保存]**. *请记住：如果您选择&#x200B;**[!UICONTROL 同步所有内容]**早期。* 另请参阅 [在Dynamic Media的文件夹级别使用“选择性发布”](/help/assets/selective-publishing.md).
         * **[!UICONTROL 继承]**  — 文件夹上没有明确的同步值；相反，文件夹会从其上级文件夹之一继承同步值，或继承云配置中的默认模式。 通过工具提示，显示继承的节目的详细状态。
         * **[!UICONTROL 为子文件夹启用]**  — 包含此子树中要同步到Dynamic Media的所有内容。 特定于文件夹的设置会覆盖云配置中的默认模式。
         * **[!UICONTROL 子文件夹已禁用]**  — 将此子树中的所有内容从同步到Dynamic Media。

   >[!NOTE]
   DMS7中不支持版本控制。 此外，仅当“编辑 Dynamic Media 配置”页面中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;时，并且直到首次激活资产时延迟激活才适用。
   激活资产后，任何更新都会立即实时发布到S7交付。

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 要在发布Dynamic Media内容之前安全预览内容，您必须“”允许列表Experience Manager创作实例才能连接到Dynamic Media:

   * **里克：链接到新的发布设置主题** 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。 您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系Adobe客户支持。

   * 在页面右上方的导航栏上，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**.

   * 在图像服务器发布页面的发布上下文下拉列表中，选择 **[!UICONTROL 测试图像提供]**.
   * 对于客户端地址筛选器，选择 **[!UICONTROL 添加]**.
   * 要启用（打开）地址，请选中复选框。 输入Experience Manager创作实例的IP地址（而非Dispatcher IP）。
   * 选择&#x200B;**[!UICONTROL 保存]**。

您现在已完成基本配置；您已准备好使用Dynamic Media - Scene7模式。

如果要进一步自定义配置，可以选择完成 [（可选）在Dynamic Media - Scene7模式下配置高级设置](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## （可选）在Dynamic Media - Scene7模式下配置高级设置 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

**里克：保持原样**

如果要进一步自定义Dynamic Media - Scene7模式的配置和设置，或优化其性能，可以完成以下一个或多个操作 *可选* 任务：

* [（可选）配置Dynamic Media - Scene7模式，以上传大于2 GB的资产](#optional-config-dms7-assets-larger-than-2gb)

* [（可选）Dynamic Media - Scene7模式设置的设置和配置](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（可选）调整Dynamic Media - Scene7模式的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（可选）筛选用于复制的资产](#optional-filtering-assets-for-replication)

### （可选）配置Dynamic Media - Scene7模式，以上传大于2 GB的资产 {#optional-config-dms7-assets-larger-than-2gb}

**里克：保持原样**

在Dynamic Media - Scene7模式下，默认资产上传文件大小为2 GB或更小。 但是，您可以选择配置大于2 GB和高于15 GB的资产上传。

如果您打算使用此功能，请注意以下先决条件和要点：

* 您必须在Dynamic Media - Scene7模式下运行带有Service Pack 6.5.4.0或更高版本的Experience Manager6.5。
* 仅支持此大型上传功能 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 客户。
* 确保已使用Amazon S3或Microsoft® Azure Blob Storage配置Experience Manager实例。

   >[!NOTE]
   使用访问密钥和密钥配置Azure Blob Storage，因为Blob存储配置中的AzureSas不支持此大上传功能。

* Oak&#39;s [直接二进制访问下载](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) 已启用(Oak的 *直接二进制访问上传* 不是必需的)。

   要启用直接二进制访问下载，请设置属性 `presignedHttpDownloadURIExpirySeconds > 0` 在数据存储配置中。 值应足够长，可下载较大的二进制文件，并可能重试。

* 大于15 GB的资产不会上传。 （大小限制在下面的步骤8中设置。）
* 当 **[!UICONTROL Dynamic Media重新处理]** 资产工作流在文件夹上触发，它会重新处理已与Dynamic Media公司同步的任何大型资产。 但是，如果文件夹中尚未同步任何大型资产，则不会上传资产。 因此，要同步Dynamic Media中的现有大资产，您可以运行 **[!UICONTROL Dynamic Media重新处理]** 单个资产上的资产工作流。

**要配置Dynamic Media - Scene7模式，以上传大于2 GB的资产，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

1. 在“CRXDE Lite”窗口中，执行以下任一操作：

   * 在左边栏中，导航到以下路径：

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 将上面的路径复制并粘贴到工具栏下方的CRXDE Lite路径字段中，然后按 `Enter`.

1. 在左边栏中，右键单击 `fileupload`，然后从弹出菜单中选择 **[!UICONTROL 覆盖节点]**.

   ![“覆盖节点”选项](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 在“覆盖节点”对话框中，选择 **[!UICONTROL 匹配节点类型]** 选中框以启用（打开）选项，然后选择 **[!UICONTROL 确定]**.

   ![“覆盖节点”对话框](/help/assets/assets-dm/uploadassets15gb_b.png)

1. 在“CRXDE Lite”窗口中，执行以下任一操作：

   * 在左边栏中，导航到以下覆盖节点路径：

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 将上面的路径复制并粘贴到工具栏下方的CRXDE Lite路径字段中，然后按 `Enter`.

1. 在 **[!UICONTROL 属性]** 选项卡 **[!UICONTROL 名称]** 列，查找 `sizeLimit`.
1. 在 `sizeLimit` 名称，在 **[!UICONTROL 值]** 列中，双击值字段。
1. 输入相应的字节值，以便将大小限制增加到所需的最大上载大小。 例如，要将上传资产大小限制增加到10 GB，请输入 `10737418240` （在值字段中）。
您可以输入一个最大为15 GB(`2013265920` 字节)。 在这种情况下，不会上传大于15 GB的已上传资产。


   ![大小限制值](/help/assets/assets-dm/uploadassets15gb_c.png)

1. 在CRXDE Lite窗口的左上角附近，选择 **[!UICONTROL 全部保存]**.

   *现在，通过执行以下操作，为AdobeGranite工作流外部进程作业处理程序设置超时：*

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。
1. 执行以下操作之一：

   * 导航到以下URL路径：

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 将上述路径复制并粘贴到浏览器的URL字段中。 请务必将 `localhost:4502` 使用您自己的Experience Manager实例。

1. 在 **[!UICONTROL AdobeGranite工作流外部进程作业处理程序]** 对话框中 **[!UICONTROL 最大超时]** 字段，将值设置为 `18000` 分钟（五小时）。 默认为10800分钟（三小时）。

   ![最大超时值](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 在对话框的右下角，选择 **[!UICONTROL 保存]**.

   *现在，通过执行以下操作，为Scene7直接二进制上传过程步骤设置超时：*

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。
1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在工作流模型页面上，选择 **[!UICONTROL Dynamic Media编码视频]**.
1. 在工具栏中，选择 **[!UICONTROL 编辑]**.
1. 在工作流页面上，双击 **[!UICONTROL Scene7直接二进制上传]** 处理步骤。
1. 在 **[!UICONTROL 步骤属性]** 对话框下 **[!UICONTROL 常用]** 选项卡 **[!UICONTROL 高级设置]** 标题 **[!UICONTROL 超时]** 字段，输入值 `18000` 分钟（五小时）。 默认值为 `3600` 分钟（1小时）。
1. 选择 **[!UICONTROL 确定]**.
1. 选择 **[!UICONTROL 同步]**.
1. 对 **[!UICONTROL DAM更新资产]** 工作流模型和 **[!UICONTROL Dynamic Media重新处理]** 工作流模型。

### （可选）配置Dynamic Media发布设置 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**里克：此处添加了新发布设置主题中的整个内容**

>[!IMPORTANT]
Dynamic Media发布设置仅在以下情况下可用：
* 您在Scene7模式下运行Dynamic Media。
* 您拥有 *现有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5中或在Experience Manageras a Cloud Service中。
* 您是具有管理员权限的Experience Manager系统管理员。


“Dynamic Media发布设置”页面设置决定了默认情况下如何将资产从Dynamic Media服务器Adobe到网站或应用程序。 如果未指定任何设置，AdobeDynamic Media服务器将根据“发布设置”页面上的默认设置来传送资产。 例如，如果请求传送的图像不包含分辨率属性，则会生成一个图像，其中图像服务器页面上具有默认对象分辨率设置。

管理员可以更改“图像服务器”、“图像渲染器”和“晕影”页面上的默认设置，以建立用于从服务器传送资产的默认设置。

>[!NOTE]
Dynamic Media发布设置适用于经验丰富的网站开发人员和程序员。 Adobe建议更改其中任何默认发布设置的用户熟悉AdobeDynamic Media、HTTP协议标准和惯例以及基本成像技术。

**要配置Dynamic Media发布设置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面中，设置图像服务器 — 发布上下文，然后使用五个选项卡配置默认的发布设置。

   * [图像服务器](#image-server)
   * [安全性](#security-tab) 选项卡
   * [目录管理](#catalog-management-tab) 选项卡
   * [请求属性](#request-attributes-tab) 选项卡
   * [常见缩略图属性](#common-thumbnail-attributes-tab) 选项卡
   * [色彩管理属性](#color-management-attributes-tab) 选项卡

   ![Dynamic Media发布设置页面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media发布设置页面，其中&#x200B;**[!UICONTROL 请求属性]**选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

#### 图像服务器 {#image-server}

“图像服务器”页为从图像服务器传送图像建立了默认设置。 有五个类别提供了设置

| 发布上下文 | 描述 |
| --- | --- |
| 图像服务 | 指定发布设置的上下文。 |
| 提供测试图像 | 指定用于测试发布设置的上下文。<br>请参阅 [在将资产公开之前对其进行测试](#test-assets-before-making-public). |

#### “安全”选项卡 {#security-tab}

**[!UICONTROL 客户端地址]**  — 用于指定一个或多个IP地址或IP地址范围。 指定后，对此图像目录的请求将被拒绝，这些请求源自位于未列出IP地址的客户端。 此规则同时适用于图像和已渲染图像的交付。

#### “目录管理”选项卡 {#catalog-management-tab}

**[!UICONTROL 规则集定义文件路径]**  — 指定包含图像目录的规则集定义的文件。

另请参阅 [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 参数。

#### “请求属性”选项卡 {#request-attributes-tab}

这些设置与图像的默认外观有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 回复图像大小限制]** | 必填.<br>指定返回给客户端的最大回复图像宽度和高度。 如果请求导致返回图像的宽度或高度或两者都大于此设置，则服务器会返回错误。<br>另请参阅 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 参数。 |
| **[!UICONTROL 请求混淆模式]** | 如果希望将base64编码应用于有效请求，则启用。<br>另请参阅 [请求模糊处理](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 参数。 |
| **[!UICONTROL 请求锁定模式]** | 如果您希望请求中包含简单的哈希锁定，则启用。<br>另请参阅 [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 参数。 |
| **[!UICONTROL 默认请求属性]** |  |
| **[!UICONTROL 默认图像文件后缀]** | 必填.<br>默认数据文件扩展名，如果路径不包含文件后缀，则附加到目录路径和掩码路径字段值中。<br>另请参阅 [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 参数。 |
| **[!UICONTROL 默认字体名称]** | 指定在文本层请求未提供字体时使用的字体。 If specified, it must be a valid font name value in the font map of this image catalog or in the font map of the default catalog.<br>另请参阅 [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 参数。 |
| **[!UICONTROL 默认图像]** | 提供默认图像以返回，以响应未找到请求图像的请求。<br>另请参阅 [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 参数。 |
| **[!UICONTROL 默认图像模式]** | 启用滑块框（右侧的滑块）后， **[!UICONTROL 默认图像]** 使用默认图像替换源图像中每个缺失的图层，并照常返回复合。 禁用滑块框（左侧的滑块）后，默认图像会替换整个复合图像，即使缺少的图像只是多个图层中的一个图层。<br>另请参阅 [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 参数。 |
| **[!UICONTROL 默认视图大小]** | 必填.<br>如果请求未明确使用指定视图大小，则服务器将限制返回图像不得大于此宽度和高度 `wid=`, `hei=`或 `scl=`.<br>另请参阅 [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 参数。 |
| **[!UICONTROL 默认缩略图大小]** | 必填.<br>使用而不是属性 **[!UICONTROL 默认视图大小]** 对于缩略图请求(`req=tmb`)。 如果缩略图请求(`req=tmb`)未明确使用 `wid=`, `hei=`或 `scl=`.<br>另请参阅 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 参数。 |
| **[!UICONTROL 默认背景颜色]** | 指定用于填充不包含实际图像数据的回复图像任何区域的RGB值。<br>另请参阅 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 参数。 |
| **[!UICONTROL JPEG 编码属性]** |  |
| **[!UICONTROL 质量]** | 指定JPEG回复图像的默认属性。 的 **[!UICONTROL 质量]** 字段，其定义范围为1 - 100。<br>另请参阅 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 参数。 |
| **[!UICONTROL 色度降采样]** | 启用或禁用JPEG编码器采用的以色度进行缩减采样。 |
| **[!UICONTROL 默认重新取样模式]** | 指定用于缩放图像数据的默认重新取样属性和插值属性。在 `resMode` 未在请求中指定。<br>另请参阅 [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 参数。 |

#### “常用缩略图属性”选项卡 {#common-thumbnail-attributes-tab}

这些设置与缩略图图像的默认外观和对齐方式有关。

| 设置 | 描述 |
| --- | --- |
| **[!UICONTROL 缩略图的默认背景颜色]** | 指定用于填充不包含实际图像数据的输出缩略图图像区域的RGB值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]** 或 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 参数。 |
| **[!UICONTROL 水平对齐]** | 在由指定的回复图像矩形中指定缩略图的水平对齐方式 `wid=` 和 `hei=` 值。<br>仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]**.<br>有三个水平对齐可供选择： **[!UICONTROL 居中对齐]**, **[!UICONTROL 左对齐]**&#x200B;和 **[!UICONTROL 右对齐]**.<br>另请参阅 [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 参数。 |
| **[!UICONTROL 垂直对齐]** | 在由指定的回复图像矩形中指定缩略图图像的垂直对齐方式 `wid=` 和 `hei=` 值。 仅用于缩略图请求(`req=tmb`)和时间 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 拟合]**.<br>有三个垂直对齐方式可供选择： **[!UICONTROL 顶部对齐方式]**, **[!UICONTROL 居中对齐]**&#x200B;和 **[!UICONTROL 底部对齐方式]**.<br>另请参阅 [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 参数。 |
| **[!UICONTROL 默认缓存生存时间]** | 提供默认的有效期时间间隔（以小时为单位），以防特定的目录记录不包含有效的目录有效期值。设置为 `-1` 标记为永不过期。 <br>另请参阅 [过期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 参数。 |
| **[!UICONTROL 默认缩略图类型]** | 为缩略图类型提供默认值，以防特定目录记录不包含有效的目录ThumbType值。 仅用于缩略图请求(`req=tmb`)。<br>有三种缩略图类型可供选择： **[!UICONTROL 裁切]**, **[!UICONTROL 拟合]**&#x200B;和 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 参数。 |
| **[!UICONTROL 默认缩略图分辨率]** | 为缩略图对象分辨率提供默认值，以防特定目录记录不包含有效的目录ThumbRes值。 仅用于缩略图请求(`req=tmb`)和 **[!UICONTROL 默认缩略图类型]** 设置设置为 **[!UICONTROL 纹理]**.<br>另请参阅 [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 参数。 |

#### “色彩管理属性”选项卡 {#color-management-attributes-tab}

这些设置决定了图像使用的ICC颜色配置文件。

**颜色转换渲染意图**
颜色转换呈现意图允许覆盖工作配置文件的默认呈现意图以确定如何调整源颜色。 在以下情况下使用：

1. 默认的ICC配置文件之一是颜色转换的目标色彩空间。
1. 输出设备（打印机或显示器）的特征是此配置文件。
1. 而且，指定的渲染意图对此配置文件有效。

不同的渲染意图使用不同的规则来确定如何调整源颜色。

例如，您可以将 **[!UICONTROL RGB默认色彩空间]** to **[!UICONTROL sRGB]**&#x200B;和 **[!UICONTROL CMYK默认色彩空间]** to **[!UICONTROL WebCoated]**.

这样做可以执行以下操作：

* 为RGB和CMYK图像启用颜色校正。
* 没有颜色配置文件的RGB图像假定位于 *sRGB* 色彩空间。
* 假定没有颜色配置文件的CMYK图像位于 *WebCoated* 色彩空间。
* 返回RGB输出的动态演绎版，将其返回 *sRGB* 色彩空间。
* 返回CMYK输出的动态呈现，将其返回 *WebCoated* 色彩空间。

另请参阅 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 参数。

>[!NOTE]
通常，最好对所选颜色设置使用默认渲染意图，该设置已通过Adobe测试，符合行业标准。 例如，如果您为北美或欧洲选择颜色设置，则默认颜色转换呈现意图为 **[!UICONTROL 相对色度]**. 如果为“日本”选择颜色设置，则默认颜色转换呈现意图为 **[!UICONTROL 知觉]**.

| 设置 | 特征 |
| --- | --- |
| **[!UICONTROL CMYK默认色彩空间]** | 指定要用作CMYK数据工作配置文件的ICC颜色配置文件的名称。 如果 **[!UICONTROL 未指定]** 选中后，当涉及CMYK源图像时，将禁用此图像目录的色彩管理。 所有CMYK工作空间都依赖于设备，这意味着它们基于实际的油墨和纸张组合。 CMYK工作空间Adobe供应基于标准商业印刷条件。<br> 另请参阅 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 参数。 |
| **[!UICONTROL 灰阶默认色彩空间]** | 指定ICC颜色配置文件的名称，以用作灰度数据的工作配置文件。 如果 **[!UICONTROL 未指定]** 选中后，当涉及灰度源图像时，将禁用此图像目录的颜色管理。<br>另请参阅 [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 参数。 |
| **[!UICONTROL RGB默认色彩空间]** | 指定ICC颜色配置文件的名称，以用作RGB数据的工作配置文件。 如果 **[!UICONTROL 未指定]** 已选择，则在涉及RGB源图像时，将禁用此图像目录的颜色管理。 总的来说，最好选择 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而不是特定设备的配置文件（如监视器配置文件）。 **[!UICONTROL sRGB]** 在为web或移动设备准备图像时，建议使用此参数，因为它定义了用于查看web上图像的标准显示器的颜色空间。 **[!UICONTROL sRGB]** 在处理来自消费者级别的数码相机的图像时，也是一个不错的选择，因为大多数这些相机都使用sRGB作为其默认颜色空间。<br>另请参阅 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 参数。 |
| **[!UICONTROL 颜色转换渲染意图]** | **[!UICONTROL 知觉]**  — 旨在保持颜色之间的视觉关系，使人眼认为它是自然的，即使颜色价值本身可能会改变。 此意图适用于具有大量色域外颜色的照片图像。 此设置是日本印刷行业的标准渲染意图。 |
|  | **[!UICONTROL 相对比色]**  — 将源颜色空间的极端高亮与目标颜色空间的极端高亮进行比较，并相应地移动所有颜色。 色域外颜色被移动到目标色彩空间中最接近的可再现颜色。 相对比色在图像中保留的原始颜色多于“感知”。 此设置是在北美和欧洲打印的标准渲染意图。 |
|  | **[!UICONTROL 饱和度]**  — 尝试在图像中生成生动的颜色，但牺牲了颜色的准确性。 此渲染意图适用于图形或图表等商业图形，其中明亮的饱和颜色比颜色之间的确切关系更为重要。 |
|  | **[!UICONTROL 绝对比色]**  — 保留位于目标色域内的颜色不变。 超出色域的颜色会被剪切。 不会将颜色缩放到目标白点。 此目的旨在以保持颜色之间关系为代价来保持颜色准确性，并且适于校样以模拟特定设备的输出。 此意图可用于预览纸张颜色对打印颜色的影响。 |

### 在将资产公开之前对其进行测试 {#test-assets-before-making-public}

安全测试可帮助您定义安全测试环境，并基于一组可配置的IP地址和范围构建强大的企业对企业解决方案。 此功能允许您将AdobeDynamic Media部署与内容管理和业务系统的架构相匹配。

通过安全测试，您可以预览包含未发布内容的网站的暂存版本。

如果需要，请创建暂存环境，而不是公开提供资产，原因如下：

* 在公共启动之前预览网站（暂存网站）。
* 提供需要受限访问的资产，例如在B2B Web应用程序中显示价格的eCatalog。
* 将防火墙后的资产用作产品信息管理系统、客户服务应用程序、培训站点等的一部分。

>[!NOTE]
安全测试不影响对Adobe Dynamic Media Classic的访问。 Adobe Dynamic Media Classic安全性保持一致，需要通常的凭据才能访问Adobe Dynamic Media Classic和相关web服务。

#### 安全测试的工作原理 {#how-test-assets-works}

大多数公司都在防火墙的后面运行互联网。 通过某些路由（通常通过有限范围的公共IP地址）可以访问Internet。

从您的公司网络中，您可以使用诸如 [https://www.whatismyip.com](https://www.whatismyip.com/) 或向您的公司IT组织请求此信息。

通过安全测试，AdobeDynamic Media为暂存环境或内部应用程序建立专用的图像服务器。 对此服务器的任何请求都会检查源IP地址。 如果传入的请求不在批准的IP地址列表中，则返回失败响应。 AdobeDynamic Media公司管理员为其公司的安全测试环境配置已批准的IP地址列表。

由于必须确认原始请求的位置，因此安全测试服务的流量不会通过内容分发网络(如公共Dynamic Media图像服务器流量)路由。 与公共的Dynamic Media图像服务器相比，对安全测试服务的请求的滞后时间略高。

未发布的资产可立即从安全测试服务中获取，而无需发布。 这样，您就可以在将资产发布到其面向公众的图像服务器之前，运行预览。

>[!NOTE]
安全测试服务使用配置了内部发布上下文的目录服务器。 因此，如果您的公司配置为发布到安全测试，则AdobeDynamic Media中任何上传的资产都会立即在安全测试服务上可用。 无论资产是否标记为上传后发布，此功能都为true。

安全测试服务当前支持以下资产类型和功能：

* 图像.
* 小插图（渲染服务器请求）。
* 呈现服务器请求（支持，但必须由客户明确请求）。
* 集，包括图像集、eCatalog、渲染集和媒体集。
* 标准AdobeDynamic Media富媒体查看器。
* AdobeDynamic Media OnDemand JSP页。
* 静态内容，如PDF文件和逐步提供的视频。
* HTTP视频流。
* 渐进式视频流。

The following asset types and functionalities are currently not supported:

* Adobe Dynamic Media Classic信息或eCatalog搜索
* RTMP video streaming
* Web-to-print
* UGC（用户生成的内容）服务

>[!IMPORTANT]
对AdobeDynamic Media中新的或现有UGC矢量图像资产的支持于2021年9月30日终止。

#### 测试安全测试服务 {#test-secure-testing-service}

要确保安全测试服务按预期工作，请执行以下操作：

##### 准备帐户

1. 请联系Adobe客户关怀团队，要求他们在您的帐户中启用安全测试。
1. 在Adobe Experience Manager中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media发布设置]**.
1. 在“图像服务器”页面上的 **[!UICONTROL 发布上下文]** 下拉列表中，选择 **[!UICONTROL 测试图像提供]**.
1. 选择 **[!UICONTROL 安全性]** 选项卡。
1. 对于 **[!UICONTROL 客户端地址]** 过滤器，选择 **[!UICONTROL 添加]**.
1. 在 **[!UICONTROL IP地址]** 字段，键入IP地址。
1. 在 **[!UICONTROL 蒙版]** 字段中，键入网络掩码。

   >[!NOTE]
   如果添加多个IP地址和网络掩码，则它实际上允许 *全部* IP地址进行资产调用，所有这些IP地址都会显示。

1. 执行下列操作之一：

   * 要添加更多IP地址，请重复前三步。
   * 继续下一步。

1. 在“图像服务器”页面的右上角，选择 **[!UICONTROL 保存]**.
1. 将所需的图像上传到您的AdobeDynamic Media帐户。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 确保某些图像被标记为要发布，而其他图像被取消标记，然后提交发布作业。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 通过转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在 **[!UICONTROL 服务器]** 页面，在 **[!UICONTROL 已发布的服务器名称]**.

如果服务器名称缺失或指向服务器的URL不起作用，请联系Adobe关怀。

##### 准备网站变体

您需要链接已发布和未发布资产的网站的两个变体：

* 公共版本 — 使用传统的AdobeDynamic Media URL语法来关联资产。
* 测试版本 — 使用相同语法但具有安全测试网站名称的资产链接。

##### 运行测试

执行以下测试：

1. 检查资产在公司网络中是否可见。

   在由先前定义的IP地址范围标识的公司网络中，网站的暂存版本显示所有图像，无论是否标记为发布。 因此，在预览批准或产品发布之前，您无需意外地使图像可用，即可进行测试。

   确认网站的公共版本显示的资产与以前使用AdobeDynamic Media时一样。

1. 从公司网络外部，验证未发布的资产（即未标记为发布）是否受到第三方访问的保护。

   从外部访问您的网络（例如从家庭计算机或通过4G/5G连接），然后验证网站的公共版本是否显示所有已发布的资产，但不显示任何未发布内容。

   确认暂存版本不显示任何资产，因为您正从未批准的IP地址访问安全测试服务。

### 配置Dynamic Media常规设置 {#configuring-application-general-settings}

>[!IMPORTANT]
Dynamic Media常规设置仅在以下情况下可用：
* 您在Scene7模式下运行Dynamic Media。
* 您拥有 *现有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)在Adobe Experience Manager 6.5中或在Experience Manageras a Cloud Service中。
* 您是具有管理员权限的Experience Manager系统管理员。


在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

另请参阅 [测试安全测试服务](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**要配置Dynamic Media常规设置，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到 **[!UICONTROL 资产]** > **[!UICONTROL Dynamic Media常规设置]**.
1. 在“服务器”页面中，将 **[!UICONTROL 已发布的服务器名称]** 和 **[!UICONTROL 源服务器名称]**，然后使用五个选项卡来配置默认的发布设置。

   * [服务器](#server-general-setting)
   * [上载到应用程序](#upload-to-application)
   * [图像编辑](#image-editing-tab) 选项卡
   * [PostScript](#postscript-tab) 选项卡
   * [Photoshop](#photoshop-tab) 选项卡
   * [PDF](#pdf-tab) 选项卡
   * [Illustrator](#illustrator-tab) 选项卡

   ![Dynamic Media“常规设置”页面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media“常规设置”页面，其中&#x200B;**[!UICONTROL 图像编辑]**选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 保存]**.

#### 服务器 {#server-general-setting}

在创建帐户时，AdobeDynamic Media会自动为您的公司提供分配的服务器。 这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。

| 选项 | 描述 |
| --- | --- |
| **[!UICONTROL 已发布的服务器名称]** | 必填.<br>此服务器是实时CDN（内容交付网络）服务器，用于特定于您帐户的所有系统生成URL调用。 请勿更改此服务器名称，除非Adobe技术支持部门指示您更改此名称。 名称必须使用 `https://` 在路径中。 |
| **[!UICONTROL 原始服务器名称]** | 必填.<br>此服务器仅用于质量保证测试。 除非Adobe技术支持部门指示您更改此服务器名称，否则请勿更改此服务器名称。 |

#### 上载到应用程序 {#upload-to-application}

* **[!UICONTROL 覆盖图像]**

   AdobeDynamic Media不允许两个文件具有相同的名称。 每个项目的AdobeDynamic Media ID（图像名称减去文件扩展名）必须唯一。 因为这条规则， **[!UICONTROL 上传到应用程序]** 包含覆盖。 此选项的确切效果取决于您选择的指定的覆盖图像选项。 以下选项指定了如何上传替换图像：是替换原始图像，还是变为重复图像。 重复图像将重命名为 `-1`. 例如， `chair.tif` 已重命名 `chair-1.tif`. 这些选项会影响上传到与原始文件夹不同的文件夹的图像，或文件扩展名与原始文件不同的图像，例如JPG、TIF或PNG。

   | “覆盖图像”选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 在当前文件夹内，使用相同的基本名称/扩展名进行覆盖]** | 默认.<br>此选项是最严格的替换规则。 它要求您将替换图像上传到与原始图像相同的文件夹，并且替换图像的文件扩展名与原始图像相同。 如果不满足这些要求，则会创建重复项。 |
   | **[!UICONTROL 在当前文件夹内，使用相同的基本名称（不论扩展名是什么）进行覆盖]** | 要求您将替换图像上传到与原始图像相同的文件夹，但文件扩展名可能与原始图像不同。 例如， chair.tif将取代chair.jpg。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称和扩展名进行覆盖]** | 要求替换图像的文件扩展名与原始图像相同（例如，chair.jpg必须替换chair.jpg，而不是chair.tif）。 但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新后的图像位于新文件夹中；在文件的原始位置中无法再找到该文件。 |
   | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称（不论扩展名是什么）进行覆盖]** | 此选项是包含最广的替换规则。 您可以将替换图像上传到与原始图像不同的文件夹，上传文件扩展名不同的文件，然后替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将位于上传到的新文件夹中。 |

* **[!UICONTROL 保留裁切]**

   控制对任何现有手动裁剪定义的保留。

   另请参阅 `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 和 [重新处理AssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)，均在《Dynamic Media查看器参考指南》中。

#### 默认上传选项 {#default-upload-options}

##### “图像编辑”选项卡 {#image-editing-tab}

此滤镜允许您对最终缩减采样图像微调锐化滤镜效果。 它有助于您控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。

“USM锐化”效果使用的选项与Photoshop的“USM锐化”滤镜的选项相同。 与名称所暗示的相反，USM锐化是一种锐化滤镜。

| 钝化蒙版选项 | 描述 |
| --- | --- |
| **[!UICONTROL 数量]** | 必填.<br>控制应用于边缘像素的对比度量。<br>把它看作效果的强度。 在AdobeDynamic Media中，“钝化蒙版”的量值与在Adobe Photoshop中的量值之间的主要区别是，Photoshop的量范围在1%到500%之间。 而在AdobeDynamic Media中，值范围是 `0.0` to `5.0`. AdobeDynamic Media中的值为5.0大致相当于Photoshop中的500%;值0.9等于90%，依此类推。 |
| **[!UICONTROL 半径]** | 必填.<br>控制效果的半径。<br>值范围为 `0` to `250`. 该效果在图像中的所有像素上运行，并在所有方向上从所有像素辐射出来。 半径以像素为单位进行测量。 例如，要对2000 x 2000像素图像和500 x 500像素图像获得类似的锐化效果，应在2000 x 2000像素图像上设置两个像素的半径。 然后，在500 x 500像素图像上设置一个像素的半径值。 像素数较多的图像会使用较大的值。 |
| **[!UICONTROL 阈值]** | 必填.<br>阈值是在应用“USM锐化”滤镜时忽略的对比度范围。 此效果很重要，因此在使用此滤镜时，图像不会引入“杂色”。 值范围为 `0` - `255`，灰度图像中的亮度步骤数。 `0`=黑色， `128`=50%灰色和 `255`=white。<br>阈值 `12` 忽略细微的变化是肤色亮度以避免添加杂色，但仍会为对比区域添加边缘对比度，如睫毛与皮肤相遇的地方。<br>如果您有某人的脸部照片，则USM锐化会影响图像的禁忌部分。 例如，睫毛和皮肤会聚以创建明显的对比度区域，以及平滑的皮肤本身。 即使最平滑的皮肤也表现出亮度值的细微变化。 如果不使用阈值，滤镜会突出皮肤像素中的这些细微更改。 反过来，产生噪声和不期望的效果，同时增加睫毛的对比度，增强锐度。<br>为避免出现此问题，引入了一个阈值，用于告知滤镜忽略不会显着更改对比度的像素，如平滑的皮肤。<br>在前面显示的拉链图中，请注意拉链旁边的纹理。 由于阈值过低，无法抑制噪声，出现图像噪声。 |
| **[!UICONTROL 单色]** | 选择以使图像亮度（强度）钝化。<br>取消选择以单独对每个颜色组件进行锐化。 |

另请参阅 [在AdobeDynamic Media和图像服务器上锐化图像](/help/assets/assets/sharpening_images.pdf).

##### “PostScript”选项卡 {#postscript-tab}

您可以栅格化Adobe PostScript®文件、维护透明背景、选择分辨率和选择色彩空间。

您可以在Adobe PostScript®(EPS)AdobeDynamic Media中使用。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传PostScript(EPS)图像文件时，可以采用各种方式设置它们的格式。 您可以栅格化文件、维护透明背景、选择分辨率和选择色彩空间。

| PostScript选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”(Rasterize)将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |

##### Photoshop选项卡 {#photoshop-tab}

您可以从Adobe® Photoshop®文件创建模板、维护图层、指定图层的命名方式、提取文本，以及指定图像如何定位到模板中。

| Photoshop选项 | 描述 |
| --- | --- |
| **[!UICONTROL 保持层]** | 将PSD中的层（如果有）拆分为单个资产。 资产层与PSD保持关联。 可通过在“详细信息视图”中打开PSD文件并选择层面板来查看它们。 请参阅查看和编辑PSD文件中的图层。 |
| **[!UICONTROL 创建模板]** | 从PSD文件的层创建模板。 |
| **[!UICONTROL 提取文本]** | 提取文本，以便用户在查看器中搜索文本。 |
| **[!UICONTROL 将图层扩展至背景大小]** | 将撕裂图像层的大小扩展到背景层的大小。 |
| **[!UICONTROL 图层命名]** | 将撕裂图像层的大小扩展到背景层的大小。<br>· **[!UICONTROL 层名称]**  — 将图像命名为PSD文件中图层名称之后的图像。 例如，原始PSD文件中名为“价格标签”的层将变为名为“价格标签”的图像。 但是，如果PSD文件中的层名称是默认的Photoshop层名称（背景、层1、层2等），则图像将以其在PSD文件中的层编号命名。 <br>· **[!UICONTROL Photoshop和图层编号]**  — 在PSD文件中将图像命名为图层编号之后，而忽略原始图层名称。 图像以Photoshop文件名和附加的图层编号命名。 例如，文件的第二层，名为 `Spring Ad.psd` 已命名 `Spring Ad_2` 即使它在Photoshop中具有非默认名称。<br>· **[!UICONTROL Photoshop和层名称]**  — 在PSD文件后面命名图像，后跟层名或层号。 如果PSD文件中的层名称是默认的Photoshop层名称，则使用层编号。 例如，名为 `Price Tag` 在名为的PSD文件中 `SpringAd` 已命名 `Spring Ad_Price Tag`. 将调用缺省名称为Layer 2的层 `Spring Ad_2`. |
| **[!UICONTROL 锚点]** | 指定如何在模板中锚定图像，这些模板是从PSD文件生成的分层组合生成的。 默认情况下，锚点为中心。 无论替换图像的长宽比如何，中心锚点都允许替换图像最好地填充相同的空间。 引用模板和使用参数替换时，具有不同方面的图像会替换此图像，因此，当引用模板和使用参数替换时，会有效地占用相同的空间。 如果您的应用程序需要替换图像来填充模板中分配的空间，请更改为其他设置。 |

##### PDF选项卡 {#pdf-tab}

您可以选择将文件栅格化、提取搜索词和链接、设置分辨率并选择色彩空间。

| PDF选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | · **[!UICONTROL 无]**  — 未完成PDF处理。<br>· **[!UICONTROL 缩略图]**  — 拆分PDF文件中的每个页面，并将其转换为缩略图。<br> · **[!UICONTROL 光栅化]**  — 拆开PDF文件中的页面，并将矢量图形转换为位图图像。 要创建eCatalog，请选择此选项。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 无]**  — 未从PDF中提取搜索词或链接。<br>· **[!UICONTROL 搜索词]**  — 从PDF文件中提取搜索词，以便在eCatalog查看器中按关键字搜索文件。<br>· **[!UICONTROL 链接]**  — 从PDF文件中提取链接，并将其转换为在eCatalog查看器中使用的图像映射。<br>· **[!UICONTROL 搜索词和链接]**  — 提取搜索词和链接，以在eCatalog查看器中使用。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认为 150。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 维护PDF文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |

##### Illustrator选项卡 {#illustrator-tab}

您可以栅格化Adobe Illustrator®文件、维护透明背景、选择分辨率和选择色彩空间。

您可以在AdobeDynamic Media中使用Adobe® Illustrator®(AI)文件。 AdobeDynamic Media提供了用于在上传这些文件时配置这些文件的命令。

上传Illustrator(AI)图像文件时，可以采用各种方式设置它们的格式。 您可以栅格化文件、维护透明背景、选择分辨率和选择色彩空间。 在上传屏幕上的上传屏幕上，“上传作业选项”框中的“PostScript选项”和“Illustrator选项”下提供了用于设置PostScript和Illustrator文件格式的选项。


| Illustrator选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”(Rasterize)将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]**  — 保留文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]**  — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]**  — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]**  — 转换为灰度色彩空间。 |


**[!UICONTROL 默认颜色配置文件]**  — 请参阅 [配置色彩管理](#configuring-color-management) 以了解其他信息。

>[!NOTE]
默认情况下，当您选择&#x200B;**[!UICONTROL 呈现]**&#x200B;时，系统会显示 15 种呈现形式，当您在资产的详细信息视图中选择&#x200B;**[!UICONTROL 查看器]**&#x200B;时，系统会显示 15 个查看器预设。您可以提高此限制。请参阅 [增加显示的图像预设数](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加显示的查看器预设数](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### （可选）其他配置任务

可选的设置和配置任务包括：

* [编辑支持的格式的MIME类型](#editing-mime-types-for-supported-formats) **里克：留下？**
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats) **里克：留下？**
* [创建批集预设以自动生成图像集和旋转集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **里克：留下？**

* **[!UICONTROL 兼容性属性]** - **里克：还需要吗？ 是经典的** 为了向后兼容，此设置允许文本层中的前导和尾随段落与版本3.6中的段落一样进行处理。
* **[!UICONTROL 本地化支持]** - **里克：还需要吗？ 是经典的** 这些设置允许您管理多个区域设置属性。 它还允许您指定区域设置映射字符串，以便定义要在查看器中支持各种工具提示的语言。 有关设置的更多信息 **[本地化支持]**，请参阅 [设置资产本地化时的注意事项](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### 编辑支持的格式的MIME类型 {#editing-mime-types-for-supported-formats}

**里克：保持原样??**

您可以定义Dynamic Media处理的资产类型，并自定义高级资产处理参数。 例如，您可以指定资产处理参数以执行以下操作：

* 将Adobe PDF转换为eCatalog资产。
* 将Adobe Photoshop文档(.PSD)转换为横幅模板资产以进行个性化。
* 将Adobe Illustrator文件(.AI)或Adobe Photoshop封装的PostScript®文件(.EPS)栅格化。
* [视频配置文件](/help/assets/video-profiles.md) 和 [成像配置文件](/help/assets/image-profiles.md) 可以分别用于定义视频和图像的处理。

请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

**要编辑支持格式的MIME类型，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择mime类型。
1. 在CRXDE Lite页面的右侧，在下部：

   * 双击 **[!UICONTROL 已启用]** 字段。 默认情况下，所有资产mime类型均启用(设置为 **[!UICONTROL true]**)，这表示资产将同步到Dynamic Media进行处理。 如果要排除此资产mime类型，请将此设置更改为 **[!UICONTROL false]**.

   * 双击 **[!UICONTROL jobParam]** 打开其关联的文本字段。 请参阅 [支持的Mime类型](/help/assets/assets-formats.md#supported-mime-types) 有关允许的处理参数值列表，可用于给定mime类型。

1. 执行下列操作之一：

   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页面的菜单栏上，选择 **[!UICONTROL 全部保存]**.

1. 在页面的左上角，选择 **[!UICONTROL CRXDE Lite]** 返回Experience Manager。

#### 为不支持的格式添加MIME类型 {#adding-mime-types-for-unsupported-formats}

**里克：保持原样??**

您可以为Experience Manager Assets中不支持的格式添加自定义MIME类型。 通过在CRXDE Lite前移动MIME类型，确保Experience Manager不会删除您添加的任何新节点 `image_`. 此外，请确保将其启用值设置为 **[!UICONTROL false]**.

**要为不支持的格式添加MIME类型，请执行以下操作：**

1. 从Experience Manager，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 将打开一个新的浏览器选项卡，该选项卡将显示 **[!UICONTROL Adobe Experience Manager Web控制台配置]** 页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名称的右侧，选择 **[!UICONTROL 编辑配置值]** （铅笔图标）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在 **Adobe CQ Scene7资产MIME类型服务** ，请选择任意加号图标&lt;+>。 在表格中选择加号以添加新mime类型的位置很琐碎。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 类型 `DWG=image/vnd.dwg` 的空文本字段中。

   示例 `DWG=image/vnd.dwg` 仅用于演示目的。 您在此处添加的MIME类型可以是任何其他不支持的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，选择 **[!UICONTROL 保存]**.

   此时，您可以关闭已打开Adobe Experience Manager Web Console配置页面的浏览器选项卡。

1. 返回到具有打开的Experience Manager控制台的浏览器选项卡。
1. 从Experience Manager，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖动mime类型 `image_vnd.dwg` 直接放在上面 `image_` 在树中，如以下屏幕截图所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 具有mime类型 `image_vnd.dwg` 仍选定， **[!UICONTROL 属性]** 选项卡 **[!UICONTROL 已启用]** 行，在 **[!UICONTROL 值]** 列标题中，双击值以打开 **[!UICONTROL 值]** 下拉列表。
1. 类型 `false` (或选择 **[!UICONTROL false]** )。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite页面的左上角附近，选择 **[!UICONTROL 全部保存]**.

#### 创建批集预设以自动生成图像集和旋转集 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

**里克：保持原样??**

在将资产上传到Dynamic Media时，使用批集预设自动创建图像集或旋转集。

首先，定义资产在一组中分组的命名约定。 然后，创建一个批集预设，该预设是一组唯一命名的自包含说明。 它必须定义如何使用与预设方法中定义的命名约定相匹配的图像来构建集。

上传文件时，Dynamic Media会自动创建一个文件集，其中包含与活动预设中定义的命名约定相匹配的所有文件。

##### 配置默认命名

创建默认命名约定，以在任何批集预设方法中使用该命名约定。 在批量集预设定义中选择的默认命名约定可能是贵公司批量生成集所需的全部命名约定。 将创建批集预设，以使用您定义的默认命名约定。 如果公司定义的默认命名存在例外，您可以为特定内容集创建任意数量的批量集预设，并使用所需的替代自定义命名约定。

虽然使用批量集预设功能不需要设置默认的命名约定，但最佳实践建议您使用默认的命名约定。 它允许您定义要分组到一组中的命名约定中的任意多个元素，以便简化批量集创建过程。

作为替代方法，您可以使用 **[!UICONTROL 查看代码]** 没有可用的表单字段。 在此视图中，您可以完全使用正则表达式创建命名约定定义。

有两个元素可用于定义：“匹配”和“基本名称”。 利用这些字段，可定义命名约定的所有元素，并标识用于命名包含这些元素的集合的约定部分。 公司的单个命名约定通常对其中每个元素使用一行或多行定义。 您可以为唯一定义使用任意多行的线条，并将它们分组为不同的元素，如“主图像”、“颜色”元素、“替代视图”元素和“色板”元素。

**要配置默认命名，请执行以下操作：**

**里克：保持原样??**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏中，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批集预设]** > **[!UICONTROL 默认命名]**.
1. 选择&#x200B;**[!UICONTROL 查看表单]**&#x200B;或&#x200B;**[!UICONTROL 查看代码]**，以指定要查看的方式并输入有关每个元素的信息。

   您可以选择 **[!UICONTROL 查看代码]** 复选框，以查看生成的正则表达式值与表单选项的旁边。 如果表单视图因任何原因限制您，则您可以输入或更改这些值以帮助定义命名约定的元素。 如果无法在表单视图中分析您的值，则表单字段将变为不活动。

   >[!NOTE]
   取消激活的表单字段不会验证正则表达式是否正确。 您会看到在结果行之后为每个元素构建的正则表达式的结果。 完整的正则表达式显示在页面底部。

1. 根据需要展开每个元素，然后输入要使用的命名约定。
1. 根据需要，执行以下任一操作：

   * 选择 **[!UICONTROL 添加]** 为元素添加其他命名约定。
   * 选择 **[!UICONTROL 删除]** 删除元素的命名约定。

1. 执行下列操作之一：

   * 选择 **[!UICONTROL 另存为]** 并键入预设的名称。
   * 选择 **[!UICONTROL 保存]** 编辑现有预设时，才会显示该预设。

##### 创建批集预设

Dynamic Media使用批量集预设将资产组织为一组图像（替代图像、颜色选项、360旋转），以便在查看器中显示。 批集预设会随Dynamic Media中的资产上传流程自动运行。

您可以创建、编辑和管理批集预设。 有两种形式的批集预设定义：一个用于您可以设置的默认命名约定，另一个用于您随时创建的自定义命名约定。

您可以使用表单字段方法定义批集预设，也可以使用代码方法来使用正则表达式。 与默认命名一样，您可以在表单视图中定义的同时选择查看代码，并使用正则表达式来构建定义。 或者，您也可以取消选中任一视图以独占使用其中一个视图。

**要创建批集预设，请执行以下操作：**

**里克：保持原样??**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏中，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批集预设]** > **[!UICONTROL 批集预设]**.

   **[!UICONTROL 查看表单]**，如“详细信息”页面右上角设置的，则是默认视图。

1. 在“预设列表”面板中，选择 **[!UICONTROL 添加]** 激活屏幕右侧“详细信息”面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在“批集类型”下拉菜单中，选择预设类型。
1. 执行下列操作之一：

   * 如果您使用的是之前在 **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批集预设]** > **[!UICONTROL 默认命名]**，展开 **[!UICONTROL 资产命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 默认]**.

   * 要在设置预设时定义新的命名约定，请展开 **[!UICONTROL 资产命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 自定义]**.

1. 对于“序列”顺序，定义在图像集分组到Dynamic Media后图像的显示顺序。

   默认情况下，您的资产按字母数字顺序排序。 但是，您可以使用逗号分隔的正则表达式列表来定义顺序。

1. 对于设置命名和创建约定，请为您在资产命名约定中定义的基本名称指定后缀或前缀。 此外，定义在Dynamic Media文件夹结构中创建集的位置。

   如果您定义大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建一个“图像集”文件夹，并将生成的集放置在此处。

1. 在“详细信息”面板中，选择 **[!UICONTROL 保存]**.
1. 选择 **[!UICONTROL 活动]** 新预设名称旁边。

   激活预设可确保在您将资产上传到Dynamic Media时，会应用批量集预设来生成资产集。

##### 创建批集预设以自动生成2D旋转集

您可以使用批集类型 **[!UICONTROL 多轴旋转集]** 创建可自动生成2D旋转集的方法。 图像分组使用行和列正则表达式，以便图像资产在多维数组中的相应位置中正确对齐。 在多轴旋转集中，没有必须具有的最小或最大行数或列数。

例如，假定要创建一个名为 `spin-2dspin`. 您有一组包含三行的旋转集图像，每行12个图像。 这些图像的名称如下所示：

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

根据此信息，可以按如下方式创建批集类型方法：

![chlimage_1-560](assets/chlimage_1-560.png)

旋转集的共享资产名称部分的分组将添加到 **[!UICONTROL 匹配]** 字段（高亮显示）。 资产名称中包含行和列的变量部分将分别添加到 **[!UICONTROL 行]** 和 **[!UICONTROL 列字段]** 。

上传和发布旋转集后，您可以激活&#x200B;**[!UICONTROL 上传作业选项]**&#x200B;对话框中&#x200B;**[!UICONTROL 批集预设]**&#x200B;下方 2D 旋转集方法的名称。

**要创建批量集预设以自动生成2D旋转集，请执行以下操作：**

**里克：保持原样??**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏中，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批集预设]** > **[!UICONTROL 批集预设]**.

   **[!UICONTROL 查看表单]**，如“详细信息”页面右上角设置的，则是默认视图。

1. 在“预设列表”面板中，选择 **[!UICONTROL 添加]** 激活屏幕右侧“详细信息”面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在“批集类型”下拉菜单中，选择&#x200B;**[!UICONTROL 资产集]**。
1. 在子类型下拉列表中，选择 **[!UICONTROL 多轴旋转集]**.
1. 展开 **[!UICONTROL 资产命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 自定义]**.
1. 使用&#x200B;**[!UICONTROL 匹配]**&#x200B;和（可选）**[!UICONTROL 基本名称]**&#x200B;属性定义组成分组的图像资产命名的正则表达式。

   例如，您的文字“匹配”正则表达式可能如下所示：

   `(w+)-w+-w+`

1. 展开 **[!UICONTROL 行列位置]**，然后为图像资产在2D旋转集数组中的位置定义名称格式。

   使用圆括号将行或列在文件名中的位置括起来。

   例如，对于行正则表达式，它可能如下所示：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   对于列正则表达式，它可能如下所示：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   上述示例仅供演示之用。 您可以根据需要创建正则表达式。

   >[!NOTE]
   如果行和列正则表达式的组合无法确定资产在多维旋转集数组中的位置，则不会将资产添加到该集。 还记录错误。

1. 对于设置命名和创建约定，请为您在资产命名约定中定义的基本名称指定后缀或前缀。

   此外，定义在Dynamic Media Classic文件夹结构中创建旋转集的位置。

   如果您定义大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建一个旋转集文件夹，将生成的集放在此处。

1. 在“详细信息”面板中，选择 **[!UICONTROL 保存]**.
1. 选择 **[!UICONTROL 活动]** 新预设名称旁边。

   激活预设可确保在您将资产上传到Dynamic Media时，会应用批量集预设来生成资产集。

### （可选）调整Dynamic Media - Scene7模式的性能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

**里克：保持原样??**

为保持Dynamic Media - Scene7模式顺利运行，Adobe建议使用以下同步性能/可伸缩性微调提示：

* 更新预定义的作业参数，以处理不同的文件格式。
* 更新预定义的Granite工作流（视频资产）队列工作线程。
* 更新预定义的Granite临时工作流（图像和非视频资产）队列工作线程。
* 更新与Dynamic Media Classic服务器的最大上传连接数。

#### 更新预定义的作业参数，以处理不同的文件格式

**里克：保持原样??**

您可以在上传文件时调整作业参数以加快处理速度。 例如，如果您上传PSD文件，但不希望将它们作为模板进行处理，则可以将层提取设置为false(off)。 在这种情况下，调整的作业参数如下所示： `process=None&createTemplate=false`.

如果确实要打开模板创建，请使用以下参数： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议对PDF、PostScript®和PSD文件使用以下“已调整”的作业参数：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 文件类型 | 推荐的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新其中的任何参数，请按照 [启用基于MIME类型的Assets/Dynamic Media Classic上传作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### 更新Granite临时工作流队列 {#updating-the-granite-transient-workflow-queue}

**里克：保持原样??**

Granite传输工作流队列用于 **[!UICONTROL DAM更新资产]** 工作流。 在Dynamic Media中，它用于图像摄取和处理。

**要更新Granite临时工作流队列，请执行以下操作：**

1. 导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 和搜索 **队列：Granite Transient工作流队列**.

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，请将数字更改为所需的值。

   您可以 **[!UICONTROL 最大并行作业数]** 以充分支持将文件重量上传到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（如内核数的两倍）可能会对其他并发活动产生负面影响。 因此，请根据您的特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流队列 {#updating-the-granite-workflow-queue}

**里克：保持原样??**

Granite工作流队列用于非临时工作流。 在Dynamic Media中，它使用 **[!UICONTROL Dynamic Media编码视频]** 工作流。

**要更新Granite工作流队列，请执行以下操作：**

1. 导航到 `https://<server>/system/console/configMgr` 和搜索 **队列：Granite工作流队列**.

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，请将数字更改为所需的值。

   您可以增加最大并行作业数，以充分支持将文件重新上载到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（如内核数的两倍）可能会对其他并发活动产生负面影响。 因此，请根据您的特定用例测试和调整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上传连接 {#updating-the-scene-upload-connection}

**里克：保持原样??**

Scene7上传连接设置可将Experience Manager资产同步到Dynamic Media Classic服务器。

**要更新Dynamic Media Classic上传连接，请执行以下操作：**

1. 导航至 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 连接数]** 字段和/或 **[!UICONTROL 活动作业超时]** 字段，请根据需要更改数字。

   的 **[!UICONTROL 连接数]** 设置控制允许Experience Manager到Dynamic Media上传的HTTP连接的最大数量；通常，十个连接的预定义值就足够了。

   的 **[!UICONTROL 活动作业超时]** 设置可确定在交付服务器中发布已上传的Dynamic Media资产的等待时间。 默认情况下，此值为2100秒或35分钟。

   对于大多数用例，设置2100便已足够。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### （可选）筛选用于复制的资产 {#optional-filtering-assets-for-replication}

**里克：保持原样**

在非Dynamic Media部署中，您会复制 *全部* 资产（图像和视频）从Experience Manager创作环境到Experience Manager发布节点。 此工作流是必需的，因为Experience Manager发布服务器也会交付资产。

但是，在Dynamic Media部署中，由于资产是通过Cloud Service交付的，因此无需复制这些资产来Experience Manager发布节点。 这种“混合发布”工作流可避免复制资产所需的额外存储成本和较长的处理时间。 其他内容（如网站页面）将继续从Experience Manager发布节点提供。

这些过滤器为您提供了一种 *排除* 资产复制到Experience Manager发布节点。

#### 使用默认资产筛选器进行复制 {#using-default-asset-filters-for-replication}

**里克：保持原样**

如果您使用Dynamic Media进行成像或视频，或者同时使用视频或视频，则可以按原样使用Adobe提供的默认过滤器。 默认情况下，以下过滤器处于活动状态：

|  | 筛选器 | Mime类型 | 演绎版 |
| --- | --- | --- | --- |
| Dynamic Media图像交付 | 过滤图像<br>筛选集 | 开始于 **图像/**<br>&#x200B;包含 **应用程序/** 结尾为 **set**. | 现成的“滤镜图像”（适用于单个图像资产，包括交互式图像）和“滤镜集”（适用于旋转集、图像集、混合媒体集和轮播集）将：<br>·从复制中排除原始图像和静态图像呈现。 |
| Dynamic Media视频交付 | filter-video | 开始于 **video/** | 现成的“过滤视频”将：<br>·从复制中排除原始视频和静态缩略图呈现。 |

>[!NOTE]
过滤器应用于MIME类型，并且不能特定于路径。

#### 自定义用于复制的资产筛选器 {#customizing-asset-filters-for-replication}

**里克：保持原样**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` 以查看过滤器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 要为过滤器定义Mime类型，可以按如下方式找到Mime类型：

   在左边栏中，展开 `content > dam > <locate_your_asset> > jcr:content > metadata`，然后在表中找到 `dc:format`.

   下图是资产路径的示例 `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   请注意， `dc:format` （对于资产） `Fiji Red.jpg` is `image/jpeg`.

   要使此过滤器应用于所有图像（无论其格式如何），请将值设置为 `image/*` where `*` 是应用于任何格式的所有图像的正则表达式。

   要使过滤器仅应用于JPEG类型的图像，请输入值 `image/jpeg`.

1. 定义要在复制中包含或排除的演绎版。

   可用于筛选复制字符的字符包括：

   | 要使用的字符 | 如何筛选用于复制的资产 |
   | --- | --- |
   | * | 通配符 |
   | + | 包括用于复制的资产 |
   | - | 从复制中排除资产 |

   导航到 `content/dam/<locate your asset>/jcr:content/renditions`。

   下图是资产演绎版的示例。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   如果您只想复制原件，则可以输入 `+original`.
