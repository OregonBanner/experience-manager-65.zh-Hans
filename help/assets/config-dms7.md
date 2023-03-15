---
title: 配置Dynamic Media - Scene7模式
description: 了解如何配置Dynamic Media - Scene7模式。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: a8db862b4a90ee6679de44df9508caf75a4c3eec
workflow-type: tm+mt
source-wordcount: '6489'
ht-degree: 3%

---

# 配置Dynamic Media - Scene7模式{#configuring-dynamic-media-scene-mode}

如果您使用针对不同环境（如开发、暂存和生产）设置的Adobe Experience Manager，请为每个环境配置Dynamic MediaCloud Services。

## Dynamic Media - Scene7模式的架构图 {#architecture-diagram-of-dynamic-media-scene-mode}

以下架构图描述了Dynamic Media - Scene7模式的工作原理。

借助新架构，Experience Manager负责主要源资产，并与Dynamic Media同步，以进行资产处理和发布：

1. 将主源资产上传到Experience Manager后，会将其复制到Dynamic Media。 届时，Dynamic Media将处理所有资源处理和演绎版生成，例如视频编码和图像的动态变量。
(在Dynamic Media - Scene7模式下，默认上传文件大小为2 GB或更小。 要支持上传文件大小为2 GB，最大为15 GB，请参见 [（可选）配置Dynamic Media - Scene7模式以上传大于2 GB的资源](#optional-config-dms7-assets-larger-than-2gb).)
1. 在生成演绎版后，Experience Manager可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager实例)。
1. 在内容准备好发布并批准后，它会触发Dynamic Media服务将内容推送至交付服务器，并在CDN（内容交付网络）处缓存内容。

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
>* Akamai ChinaCDN（用于在中国实现最佳交付）


## 在Scene7模式下启用Dynamic Media {#enabling-dynamic-media-in-scene-mode}

[默认情况下，Dynamic Media 处于禁用状态。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)要利用Dynamic Media功能，您必须启用它。

>[!WARNING]
>
>Dynamic Media - Scene7模式适用于 *仅Experience Manager创作实例*. 因此，您必须配置 `runmode=dynamicmedia_scene7` 在Experience Manager创作实例上， *非* Experience Manager发布实例。

要启用Dynamic Media，请使用启动Experience Manager `dynamicmedia_scene7` 在终端窗口中输入以下命令，从命令行运行模式（使用的示例端口为4502）：

```shell {.line-numbers}
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5，零停机 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

将Experience ManagerDynamic Media从6.3升级到6.4或6.5现在包括零停机部署的功能。 要从以下位置迁移您的所有预设和配置： `/etc` 到 `/conf` 在CRXDE Lite中，确保运行以下curl命令。

>[!NOTE]
>
>如果在兼容模式下运行Experience Manager实例（即已安装兼容包），则无需运行这些命令。

对于所有升级（无论是否带有兼容包），您可以通过运行以下Linux® curl命令来复制最初随Dynamic Media一起提供的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

迁移从中创建的任何自定义查看器预设和配置 `/etc` 到 `/conf`，运行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 安装功能包18912以批量迁移资产 {#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是 *可选*.

通过Feature Pack 18912，您可以通过FTP批量摄取资源，或者在Experience Manager时将资源从Dynamic Media — 混合模式或Dynamic Media Classic迁移到Dynamic Media - Scene7模式。 可从以下位置获得： [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

参见 [安装功能包18912以批量迁移资产](/help/assets/bulk-ingest-migrate.md) 了解更多信息。

## 在Cloud Services中创建Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

<!-- **Before you configure Dynamic Media** - After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**To create a Dynamic Media Configuration in Cloud Services:** -->

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台，然后选择工具图标，然后转到 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media配置]**.
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择 **[!UICONTROL 全局]** (请勿选择左侧的文件夹图标 **[!UICONTROL 全局]**)，然后选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建Dynamic Media配置]** 页面，输入标题、Dynamic Media帐户电子邮件地址、密码，然后选择您所在的区域。 此信息通过在预配电子邮件中Adobe向您提供。 如果您没有收到电子邮件，请联系Adobe客户支持。

   选择 **[!UICONTROL 连接到Dynamic Media]**.

1. 在 **[!UICONTROL 更改密码]** 对话框，在 **[!UICONTROL 新密码]** 字段中，输入包含8-25个字符的新密码。 密码必须至少包含以下任一项：

   * 大写字母
   * 小写字母
   * 数字
   * 特殊字符： `# $ & . - _ : { }`

   此 **[!UICONTROL 当前密码]** 字段会刻意预填充并隐藏起来，以防交互。

   如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

1. 在 **[!UICONTROL 重复密码]** 字段，重新键入新密码，然后选择 **[!UICONTROL 完成]**.

   新密码会在您选择时保存 **[!UICONTROL 保存]** 右上角的 **[!UICONTROL 创建Dynamic Media配置]** 页面。

   如果您已选择 **[!UICONTROL 取消]** 在 **[!UICONTROL 更改密码]** 对话框，您仍然必须在保存新创建的Dynamic Media配置时输入新密码。

   另请参阅 [将密码更改为Dynamic Media](#change-dm-password).

1. 连接成功后，设置以下内容。 需要带星号(*)的标题：

   * **[!UICONTROL 公司]** - Dynamic Media帐户的名称。
      >[!IMPORTANT]
      一个Experience Manager实例仅支持Cloud Services中的一个Dynamic Media配置；请勿添加多个配置。 一个Experience Manager实例上的多个Dynamic Media配置是 _非_ 受Adobe支持或推荐。

      <!-- CQDOC-19579 and CQDOC-19612 -->

      另请参阅 [配置Dynamic Media公司别名帐户](/help/assets/dm-alias-account.md).

   * **[!UICONTROL 公司根文件夹路径]**

   * **[!UICONTROL 发布资产]**  — 您可以从以下三个选项中进行选择：
      * **[!UICONTROL 立即]** 这意味着在上传资产时，系统会摄取资产并立即提供URL/Embed。 发布资产无需用户干预。
      * **[!UICONTROL 激活时]** 这意味着在提供URL/嵌入链接之前，必须先显式发布资产。<br><!-- CQDOC-17478, Added March 9, 2021-->从Experience Manager6.5.8开始，Experience Manager发布实例反映准确的Dynamic Media元数据值，例如 `dam:scene7Domain` 和 `dam:scene7FileStatus` 在 **[!UICONTROL 激活时]** 仅发布模式。 要启用此功能，请安装Service Pack 8，然后重新启动Experience Manager。 转到Sling配置管理器。 查找配置 `Scene7ActivationJobConsumer Component` 或新建一个)。 选中复选框 **[!UICONTROL 在Dynamic Media发布后复制元数据]**，然后选择 **[!UICONTROL 保存]**.

         ![“在Dynamic Media发布后复制元数据”复选框](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 选择性发布]** 利用此选项，您可以控制在Dynamic Media中发布哪些文件夹。 它可让您使用智能裁切或动态呈现版本等功能，或确定哪些文件夹仅在Experience Manager中发布以供预览。 这些相同的资产是 *非* 在Dynamic Media中发布，以便在公共域中交付。<br>您可以在 **[!UICONTROL Dynamic Media云配置]** 或者，如果您愿意，可以选择在文件夹的 **[!UICONTROL 属性]**.<br>参见 [在Dynamic Media中使用“选择性发布”功能](/help/assets/selective-publishing.md).<br>如果您稍后更改此配置，或稍后在文件夹级别更改此配置，则这些更改只会影响您此后上传的新资产。 文件夹中现有资源的发布状态将保持不变，直到您从以下任一位置手动更改它们 **[!UICONTROL 快速发布]** 或 **[!UICONTROL 管理发布]** 对话框。
   * **[!UICONTROL 安全预览服务器]**  — 用于指定安全演绎版预览服务器的URL路径。 也就是说，在生成呈现版本之后，Experience Manager可以安全地访问和预览远程Dynamic Media呈现版本(不会将二进制文件发送回Experience Manager实例)。
除非您有特殊安排使用自己公司的服务器或特殊服务器，否则Adobe建议您保留指定的此设置。

   * **[!UICONTROL 同步所有内容]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->默认选中。 如果要有选择地在同步到Dynamic Media时包含或排除资源，请取消选择此选项。 取消选择此选项可以从以下两种Dynamic Media同步模式中进行选择：

   * **[!UICONTROL Dynamic Media 同步模式]**
      * **[!UICONTROL 默认启用]**  — 默认情况下，该配置将应用于所有文件夹，除非您专门将文件夹标记为排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL 默认禁用]**  — 除非您明确地将选定的文件夹标记为同步到Dynamic Media，否则该配置不会应用于任何文件夹。
要将选定的文件夹标记为同步到Dynamic Media，请选择一个资源文件夹，然后在工具栏上选择 **[!UICONTROL 属性]**. 在 **[!UICONTROL 详细信息]** 选项卡，在 **[!UICONTROL Dynamic Media同步模式]** 从以下三个选项中进行选择。 完成后，选择 **[!UICONTROL 保存]**. *请记住：如果选择，则以下三个选项不可用&#x200B;**[!UICONTROL 同步所有内容]**更早。* 另请参阅 [在Dynamic Media中使用文件夹级别的选择性发布](/help/assets/selective-publishing.md).
         * **[!UICONTROL 已继承]**  — 文件夹上没有显式同步值；相反，文件夹从其上级文件夹之一或云配置中的默认模式继承同步值。 继承的详细状态通过工具提示显示。
         * **[!UICONTROL 为子文件夹启用]**  — 包含此子树中的所有内容，以便同步到Dynamic Media。 文件夹特定的设置会覆盖云配置中的默认模式。
         * **[!UICONTROL 已为子文件夹禁用]**  — 从同步到Dynamic Media中排除此子树中的所有内容。

   >[!NOTE]
   Dynamic Media - Scene7模式不支持版本控制。 此外，仅当“编辑 Dynamic Media 配置”页面中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;时，并且直到首次激活资产时延迟激活才适用。
   激活资产后，任何更新都会立即实时发布到S7交付。

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 为了在发布Dynamic Media内容之前安全地预览该内容，Experience Manager作者使用基于令牌的验证，因此默认情况下，Experience Manager作者会预览Dynamic Media内容。 但是，您可以“允许列表”更多IP，以便让用户有权安全地预览内容。 要在Experience Manager中设置此操作，请参阅 [为图像服务器配置Dynamic Media发布设置 — “安全”选项卡](/help/assets/dm-publish-settings.md#security-tab).

如果您想进一步自定义配置，如启用ACL（访问控制列表）权限，您可以选择完成以下任务中的任何一项： [（可选）在Dynamic Media - Scene7模式下配置高级设置](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

您现在已完成基本配置；可以开始使用Dynamic Media - Scene7模式。

### 将密码更改为Dynamic Media {#change-dm-password}

Dynamic Media中的密码过期时间设置为自当前系统日期起100年。

密码必须至少包含以下任一项：

* 大写字母
* 小写字母
* 数字
* 特殊字符： `# $ & . - _ : { }`

如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

选择后会保存更改后的密码 **[!UICONTROL 保存]** 右上角的 **[!UICONTROL 编辑Dynamic Media配置]** 页面。

**要更改Dynamic Media的密码，请执行以下操作：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在控制台左侧，选择工具图标，然后转到 **[!UICONTROL Cloud Services] > [!UICONTROL Dynamic Media配置]**.
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择 **[!UICONTROL 全局]**. 不要选择左侧的文件夹图标 **[!UICONTROL 全局]**. 然后，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，紧接在 **[!UICONTROL 密码]** 字段，选择 **[!UICONTROL 更改密码]**.
1. 在 **[!UICONTROL 更改密码]** 对话框中，执行以下操作：

   * 在 **[!UICONTROL 新密码]** 字段中，输入新密码。

      此 **[!UICONTROL 当前密码]** 字段会刻意预填充并隐藏起来，以防交互。

   * 在 **[!UICONTROL 重复密码]** 字段，重新键入新密码，然后选择 **[!UICONTROL 完成]**.

1. 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 确定]**.

## （可选）在Dynamic Media - Scene7模式下配置高级设置 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

如果要进一步自定义Dynamic Media - Scene7模式的配置和设置，或优化其性能，您可以完成以下一项或多项操作 *可选* 任务：

* [（可选）在Dynamic Media - Scene7模式下启用ACL权限](#optional-enable-acl)

* [（可选）配置Dynamic Media - Scene7模式以上传大于2 GB的资源](#optional-config-dms7-assets-larger-than-2gb)

* [（可选）设置和配置Dynamic Media - Scene7模式设置](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（可选）调整Dynamic Media - Scene7模式的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（可选）筛选资源以进行复制](#optional-filtering-assets-for-replication)

### （可选）在Dynamic Media - Scene7模式下启用访问控制列表权限 {#optional-enable-acl}

当您在AEM上运行Dynamic Media - Scene7模式时，它当前会转发 `/is/image` 请求在不检查PlatformServerServlet上的ACL（访问控制列表）权限的情况下保护预览图像服务。 不过，你可以， *启用* acl权限。 这样做会转发授权的 `/is/image` 请求。 如果用户无权访问资产，则显示“403 — 禁止”错误。

**要在Dynamic Media - Scene7模式下启用ACL权限，请执行以下操作：**

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 此时将打开一个新的浏览器选项卡，并显示 **[!UICONTROL Adobe Experience Manager Web控制台配置]** 页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，滚动到名称 *Adobe CQ Scene7 Platform Server*.

1. 在名称的右侧，选择铅笔图标(**[!UICONTROL 编辑配置值]**)。

1. 在 **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** 页面中，选中以下两个设置的复选框：

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name`  — 启用时，此设置将缓存权限结果两分钟（默认）以保存。
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name`  — 启用后，此设置将在用户通过Dynamic Media Image Server预览资源时验证用户的访问权限。

   ![在Dynamic Media - Scene7模式下启用访问控制列表设置](/help/assets/assets-dm/acl.png)

1. 在页面的右下角附近，选择 **[!UICONTROL 保存]**.

### （可选）配置Dynamic Media - Scene7模式以上传大于2 GB的资源 {#optional-config-dms7-assets-larger-than-2gb}

在Dynamic Media - Scene7模式下，默认的资源上传文件大小为2 GB或更小。 但是，您可以选择配置大于2 GB和最大为15 GB的资产上传。

如果您打算使用此功能，请注意以下先决条件和要点：

* 您必须在Dynamic Media - Scene7模式下运行带有Service Pack 6.5.4.0或更高版本的Experience Manager6.5。
* 仅支持此大型上传功能 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 客户。
* 确保您的Experience Manager实例配置了Amazon S3或Microsoft® Azure Blob Storage。

   >[!NOTE]
   使用访问密钥和密钥配置Azure Blob存储，因为Blob存储配置中的AzureSas不支持此大型上传功能。

* Oak&#39;s [直接二进制访问下载](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) 已启用(Oak *直接二进制访问上传* 非必需)。

   要启用直接二进制访问下载，请设置属性 `presignedHttpDownloadURIExpirySeconds > 0` 在数据存储配置中。 该值应足够长，以便下载较大的二进制文件，并且可能重试。

* 不会上传大于15 GB的资产。 （大小限制在下面的步骤8中设置。）
* 当 **[!UICONTROL Dynamic Media重新处理]** 资源工作流在文件夹上触发，它重新处理已与Dynamic Media公司同步的任何大型资源。 但是，如果文件夹中尚未同步任何大型资产，则不会上传该资产。 因此，要同步Dynamic Media中的现有大型资源，您可以运行 **[!UICONTROL Dynamic Media重新处理]** 资产工作流对单个资产。

**要配置Dynamic Media - Scene7模式以上传大于2 GB的资源，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

1. 在CRXDE Lite窗口中，执行以下任一操作：

   * 在左边栏中，导航到以下路径：

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 将上面的路径复制并粘贴到工具栏下方的CRXDE Lite路径字段中，然后按 `Enter`.

1. 在左边栏中，右键单击 `fileupload`，然后从弹出式菜单中选择 **[!UICONTROL 覆盖节点]**.

   ![覆盖节点选项](/help/assets/assets-dm/uploadassets15gb_a.png)

1. 在“覆盖节点”对话框中，选择 **[!UICONTROL 匹配节点类型]** 复选框以启用（打开）该选项，然后选择 **[!UICONTROL 确定]**.

   ![“覆盖节点”对话框](/help/assets/assets-dm/uploadassets15gb_b.png)

1. 在“CRXDE Lite”窗口中，执行以下任一操作：

   * 在左边栏中，导航到以下覆盖节点路径：

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 将上面的路径复制并粘贴到工具栏下方的CRXDE Lite路径字段中，然后按 `Enter`.

1. 在 **[!UICONTROL 属性]** 选项卡，在 **[!UICONTROL 名称]** 列，查找 `sizeLimit`.
1. 右侧 `sizeLimit` 名称，在 **[!UICONTROL 值]** 列中，双击值字段。
1. 输入以字节为单位的相应值，以便将大小限制增加到所需的最大上载大小。 例如，要将上传资源大小限制增加到10 GB，请输入 `10737418240` 在值字段中。
您可以输入一个最大为15 GB的值(`2013265920` 字节)。 在这种情况下，不会上传大于15 GB的已上传资产。

   ![大小限制值](/help/assets/assets-dm/uploadassets15gb_c.png)

1. 在CRXDE Lite窗口的左上角附近，选择 **[!UICONTROL 全部保存]**.

   *现在，通过执行以下操作，为AdobeGranite工作流外部进程作业处理程序设置超时：*

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。
1. 执行以下操作之一：

   * 导航到以下URL路径：

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 将上面的路径复制并粘贴到浏览器的URL字段中。 确保替换了 `localhost:4502` 使用您自己的Experience Manager实例。

1. 在 **[!UICONTROL AdobeGranite工作流外部进程作业处理程序]** 对话框，在 **[!UICONTROL 最大超时]** 字段，将值设置为 `18000` 分钟（5小时）。 默认值为10800分钟（三个小时）。

   ![最大超时值](/help/assets/assets-dm/uploadassets15gb_d.png)

1. 在对话框的右下角，选择 **[!UICONTROL 保存]**.

   *现在，通过执行以下操作来设置Scene7直接二进制上传流程步骤的超时：*

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台。
1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“工作流模型”页面上，选择 **[!UICONTROL Dynamic Media编码视频]**.
1. 在工具栏上，选择 **[!UICONTROL 编辑]**.
1. 在工作流页面上，双击 **[!UICONTROL Scene7直接二进制上传]** 流程步骤。
1. 在 **[!UICONTROL 步骤属性]** 对话框，位于 **[!UICONTROL 公共]** 选项卡，在 **[!UICONTROL 高级设置]** 标题，在 **[!UICONTROL 超时]** 字段，输入值 `18000` 分钟（5小时）。 默认为 `3600` 分钟（1小时）。
1. 选择 **[!UICONTROL 确定]**.
1. 选择 **[!UICONTROL 同步]**.
1. 对重复步骤14-21 **[!UICONTROL DAM更新资产]** 工作流模型和 **[!UICONTROL Dynamic Media重新处理]** 工作流模型。

### （可选）设置和配置Dynamic Media - Scene7模式设置 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [为图像服务器配置Dynamic Media发布设置](/help/assets/dm-publish-settings.md)
* [配置Dynamic Media常规设置](/help/assets/dm-general-settings.md)
* [配置颜色管理](#configuring-color-management)
* [编辑所支持格式的MIME类型](#editing-mime-types-for-supported-formats)
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)
* [创建批次集预设以自动生成图像集和旋转集](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (在Dynamic Media Classic用户界面中完成)

#### 为图像服务器配置Dynamic Media发布设置 {#publishing-setup-for-image-server}

“Dynamic Media发布设置”页面可建立默认设置，以确定如何将资源从AdobeDynamic Media服务器传递到网站或应用程序。

参见 [为图像服务器配置Dynamic Media发布设置](/help/assets/dm-publish-settings.md).

#### 配置Dynamic Media常规设置 {#configuring-application-general-settings}

配置Dynamic Media **[!UICONTROL 发布服务器名称]** URL和 **[!UICONTROL 源服务器名称]** URL。 您还可以指定 **[!UICONTROL 上载到应用程序]** 设置和 **[!UICONTROL 默认上传选项]** 这些都基于您的特定用例。

参见 [配置Dynamic Media常规设置](/help/assets/dm-general-settings.md).

#### 配置颜色管理 {#configuring-color-management}

Dynamic Media色彩管理允许您对资源进行色彩校正。 通过颜色校正，摄取的资产可保留其色彩空间(RGB、CMYK、灰度)和嵌入的色彩配置文件。 请求动态演绎版时，使用CMYK、RGB或灰度输出将图像颜色校正到目标颜色空间中。

参见 [配置图像预设](/help/assets/managing-image-presets.md).

>[!NOTE]
默认情况下，当您选择时，系统会显示15个演绎版 **[!UICONTROL 演绎版]** 和15个查看器预设 **[!UICONTROL 查看器]** 在资产的“详细信息”视图中。 您可以提高此限制。参见 [增加显示的图像预设数量](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加显示的查看器预设数](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### 编辑所支持格式的MIME类型 {#editing-mime-types-for-supported-formats}

您可以定义Dynamic Media处理的资源类型，并自定义高级资源处理参数。 例如，您可以指定资源处理参数以执行以下操作：

* 将Adobe PDF转换为eCatalog资源。
* 将Adobe Photoshop文档(.platform)转换为PSD横幅模板资源以进行个性化。
* 栅格化Adobe Illustrator文件(.AI)或Adobe Photoshop封装PostScript®文件(.EPS)。
* [视频配置文件](/help/assets/video-profiles.md) 和 [成像配置文件](/help/assets/image-profiles.md) 分别用于定义视频和图像的处理。

请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

**要编辑所支持格式的MIME类型，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择mime类型。
1. 在“CRXDE Lite”页面的右侧，位于下部：

   * 双击 **[!UICONTROL 已启用]** 字段。 默认情况下，将启用所有资源mime类型(设置为 **[!UICONTROL true]**)，这意味着资产将同步到Dynamic Media以供处理。 如果要从处理中排除此资源mime类型，请将此设置更改为 **[!UICONTROL false]**.

   * 双击 **[!UICONTROL jobParam]** 以打开其关联的文本字段。 参见 [支持的Mime类型](/help/assets/assets-formats.md#supported-mime-types) 获取可用于给定mime类型的允许处理参数值列表。

1. 执行下列操作之一：

   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页的菜单栏上，选择 **[!UICONTROL 全部保存]**.

1. 在页面的左上角，选择 **[!UICONTROL CRXDE Lite]** 以返回Experience Manager。

#### 为不支持的格式添加MIME类型 {#adding-mime-types-for-unsupported-formats}

您可以为Experience Manager Assets中不支持的格式添加自定义MIME类型。 通过在之前移动MIME类型，确保Experience Manager不会删除您在CRXDE Lite中添加的任何新节点 `image_`. 此外，请确保将其启用值设置为 **[!UICONTROL false]**.

**为不支持的格式添加MIME类型：**

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 此时将打开一个新的浏览器选项卡，并显示 **[!UICONTROL Adobe Experience Manager Web控制台配置]** 页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名称的右侧，选择 **[!UICONTROL 编辑配置值]** （铅笔图标）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在 **Adobe CQ Scene7 Asset MIME类型服务** 页面上，选择任意加号图标&lt;+>。 在表格中选择加号以添加新mime类型的位置微不足道。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 类型 `DWG=image/vnd.dwg` 在刚刚添加的空文本字段中。

   示例 `DWG=image/vnd.dwg` 仅用于演示目的。 您在此处添加的MIME类型可以是任何其他不受支持的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，选择 **[!UICONTROL 保存]**.

   此时，您可以关闭已打开Adobe Experience Manager Web控制台配置页面的浏览器选项卡。

1. 返回到具有已打开的Experience Manager控制台的浏览器选项卡。
1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖动mime类型 `image_vnd.dwg` 然后把它直接放在上面 `image_` 在树中，如下面的屏幕快照所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 使用mime类型 `image_vnd.dwg` 仍被选中，从 **[!UICONTROL 属性]** 选项卡，在 **[!UICONTROL 已启用]** 行，在 **[!UICONTROL 值]** 列标题，双击值以打开 **[!UICONTROL 值]** 下拉列表。
1. 类型 `false` 在字段中(或选择 **[!UICONTROL false]** （从下拉列表中）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在“CRXDE Lite”页面的左上角附近，选择 **[!UICONTROL 全部保存]**.

#### 创建批次集预设以自动生成图像集和旋转集 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

在将资产上传到Dynamic Media时，可使用批次集预设自动创建图像集或旋转集。

首先，定义资产在一个集中的分组方式的命名约定。 然后，创建一个批次集预设，它是一个唯一命名的、自包含的指令集。 它必须定义如何使用与预设方法中定义的命名约定匹配的图像来构建集合。

上传文件时，Dynamic Media会自动创建一个文件集，其中包含与活动预设中定义的命名约定相匹配的所有文件。

##### 配置默认命名

创建用于任何批次集预设方法的默认命名约定。 在批次集预设定义中选择的默认命名惯例可能是您的公司批生成集所需的所有命名惯例。 将创建一个批次集预设，以使用您定义的默认命名约定。 如果公司定义的默认命名有例外，则可以为特定内容集创建所需数量的具有备用自定义命名约定的批次集预设。

虽然设置默认命名惯例并不是使用批次集预设功能所必需的，但最佳实践建议您使用默认命名惯例。 它允许您定义命名惯例的任意多个元素，以便将它们分组到一个集中，从而简化批次集的创建。

作为替代方法，您可以使用 **[!UICONTROL 查看代码]** 表单字段不可用。 在此视图中，您可以完全使用正则表达式创建命名约定定义。

两个元素可用于定义：“匹配”和“基本名称”。 这些字段允许您定义命名约定的所有元素，并标识约定的用于命名包含它们的集的部分。 公司的单个命名惯例通常对这些元素中的每一项使用一行或多行定义。 您可以为唯一定义使用任意数量的行，并将它们分组为不同的元素，例如对于“主图像”、“颜色”元素、“替代视图”元素和“样本”元素。

**要配置默认命名，请执行以下操作：**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   Adobe在配置时提供了您的凭据和登录详细信息。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏上，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批次集预设]** > **[!UICONTROL 默认命名]**.
1. 选择&#x200B;**[!UICONTROL 查看表单]**&#x200B;或&#x200B;**[!UICONTROL 查看代码]**，以指定要查看的方式并输入有关每个元素的信息。

   您可以选择 **[!UICONTROL 查看代码]** 选中此复选框可查看与表单选择一起构建的正则表达式值。 如果表单视图出于任何原因限制您，则可以输入或更改这些值以帮助定义命名约定的元素。 如果无法在表单视图中分析您的值，则表单字段将变为非活动状态。

   >[!NOTE]
   已停用的表单字段不会验证您的正则表达式是否正确。 您会看到为Result行后面的每个元素生成的正则表达式的结果。 完整的正则表达式将显示在页面底部。

1. 根据需要展开每个元素，然后输入要使用的命名约定。
1. 根据需要，执行以下任一操作：

   * 选择 **[!UICONTROL 添加]** 为元素添加其他命名约定。
   * 选择 **[!UICONTROL 移除]** 删除元素的命名约定。

1. 执行下列操作之一：

   * 选择 **[!UICONTROL 另存为]** 并键入预设的名称。
   * 选择 **[!UICONTROL 保存]** 如果您正在编辑现有预设。

##### 创建批次集预设

Dynamic Media使用批次集预设将资源组织成图像集（替代图像、颜色选项、360旋转）以便在查看器中显示。 批次集预设会自动与Dynamic Media中的资产上传流程一起运行。

您可以创建、编辑和管理批次集预设。 有两种形式的批次集预设定义：一种用于您可以设置的默认命名约定，另一种用于动态创建的自定义命名约定。

您可以使用表单字段方法定义批次集预设，也可以使用代码方法定义批次集预设，该方法允许您使用正则表达式。 与在默认命名中一样，您可以在表单视图中定义的同时选择查看代码，并使用正则表达式来构建定义。 或者，也可以取消选中任一视图，以独占使用其中一个。

**要创建批次集预设，请执行以下操作：**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   Adobe在配置时提供了您的凭据和登录详细信息。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏上，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批次集预设]** > **[!UICONTROL 批次集预设]**.

   **[!UICONTROL 查看表单]**&#x200B;如“详细信息”页面右上角设置的那样，是默认视图。

1. 在“预设列表”面板中，选择 **[!UICONTROL 添加]** 以激活屏幕右侧详细信息面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在“批次集类型”下拉菜单中，选择一个预设类型。
1. 执行下列操作之一：

   * 如果您使用之前在下设置的默认命名约定 **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批次集预设]** > **[!UICONTROL 默认命名]**，展开 **[!UICONTROL 资源命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 默认]**.

   * 要在设置预设时定义新的命名约定，请展开 **[!UICONTROL 资源命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 自定义]**.

1. 对于序列顺序，可定义在Dynamic Media中对集进行分组后图像的显示顺序。

   默认情况下，您的资产按字母数字排序。 但是，您可以使用逗号分隔的正则表达式列表来定义顺序。

1. 对于设置命名和创建约定，请为您在资产命名约定中定义的基本名称指定后缀或前缀。 此外，定义在Dynamic Media文件夹结构中创建集的位置。

   如果定义大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建一个“图像集”文件夹，并将生成的集放在此处。

1. 在详细信息面板中，选择 **[!UICONTROL 保存]**.
1. 选择 **[!UICONTROL 活动]** ，位于新预设名称旁边。

   激活预设可确保在将资产上传到Dynamic Media时，应用批次集预设以生成该集。

##### 创建批次集预设以自动生成2D旋转集

您可以使用批次集类型 **[!UICONTROL 多轴旋转集]** 创建一个方法以自动生成2D旋转集。 图像分组使用Row和Column正则表达式，以便图像资产在多维数组中的相应位置中正确对齐。 多轴旋转集中没有最小或最大行数或列数。

例如，假设您要创建一个名为的多轴旋转集 `spin-2dspin`. 您有一组旋转集图像，其中包含3行，每行12个图像。 这些图像的命名如下：

```xml {.line-numbers}
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

使用此信息，您可以按如下方式创建批集类型方法：

![chlimage_1-560](assets/chlimage_1-560.png)

旋转集的共享资源名称部分的分组将添加到 **[!UICONTROL 匹配]** 字段（高亮显示）。 资产名称中包含行和列的变量部分将分别添加到 **[!UICONTROL 行]** 和 **[!UICONTROL 列字段]** 。

上传和发布旋转集后，您可以激活&#x200B;**[!UICONTROL 上传作业选项]**&#x200B;对话框中&#x200B;**[!UICONTROL 批集预设]**&#x200B;下方 2D 旋转集方法的名称。

**要创建批次集预设以自动生成2D旋转集，请执行以下操作：**

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   Adobe在配置时提供了您的凭据和登录详细信息。 如果您没有此信息，请联系Adobe客户支持。

1. 在页面顶部附近的导航栏上，导航到 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 批次集预设]** > **[!UICONTROL 批次集预设]**.

   **[!UICONTROL 查看表单]**&#x200B;如“详细信息”页面右上角设置的那样，是默认视图。

1. 在“预设列表”面板中，选择 **[!UICONTROL 添加]** 以激活屏幕右侧详细信息面板中的定义字段。
1. 在“详细信息”面板的“预设名称”字段中，键入预设的名称。
1. 在“批集类型”下拉菜单中，选择&#x200B;**[!UICONTROL 资产集]**。
1. 在子类型下拉列表中，选择 **[!UICONTROL 多轴旋转集]**.
1. 展开 **[!UICONTROL 资源命名约定]**，然后在文件命名下拉列表中，选择 **[!UICONTROL 自定义]**.
1. 使用&#x200B;**[!UICONTROL 匹配]**&#x200B;和（可选）**[!UICONTROL 基本名称]**&#x200B;属性定义组成分组的图像资产命名的正则表达式。

   例如，您的文本Match正则表达式可能如下所示：

   `(w+)-w+-w+`

1. 展开 **[!UICONTROL 行列位置]**，然后定义图像资产在2D旋转集数组中的位置的名称格式。

   使用括号将文件名中的行或列位置括起来。

   例如，对于行正则表达式，它可能如下所示：

   `\w+-R([0-9]+)-\w+`

   或

   `\w+-(\d+)-\w+`

   对于列正则表达式，它可能如下所示：

   `\w+-\w+-C([0-9]+)`

   或

   `\w+-\w+-C(\d+)`

   以上示例仅供演示之用。 您可以根据需要创建任意的正则表达式。

   >[!NOTE]
   如果行和列的正则表达式组合无法确定资源在多维旋转集数组中的位置，则不会将资源添加到该集中。 还会记录错误。

1. 对于设置命名和创建约定，请为您在资产命名约定中定义的基本名称指定后缀或前缀。

   此外，定义在Dynamic Media Classic文件夹结构中创建旋转集的位置。

   如果定义大量集，请将这些集与包含资产本身的文件夹分开。 例如，创建旋转集文件夹以将生成的旋转集放在此处。

1. 在详细信息面板中，选择 **[!UICONTROL 保存]**.
1. 选择 **[!UICONTROL 活动]** ，位于新预设名称旁边。

   激活预设可确保在将资产上传到Dynamic Media时，应用批次集预设以生成该集。

### （可选）调整Dynamic Media - Scene7模式的性能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

为了保持Dynamic Media - Scene7模式平稳运行，Adobe建议采取以下同步性能/可扩展性微调提示：

* 更新预定义的作业参数以处理不同的文件格式。
* 更新预定义的Granite工作流（视频资产）队列工作线程。
* 更新预定义的Granite临时工作流（图像和非视频资产）队列工作线程。
* 正在更新与Dynamic Media Classic服务器的最大上传连接。

#### 更新预定义的作业参数以处理不同的文件格式

您可以调整作业参数，以便在上载文件时更快地处理。 例如，如果上传PSD文件，但不希望将它们作为模板处理，则可以将图层提取设置为false（关闭）。 在这种情况下，调谐的作业参数如下所示： `process=None&createTemplate=false`.

如果确实要启用模板创建，请使用以下参数： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议对PDF、PostScript®和PSD文件使用以下“优化”作业参数：

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| 文件类型 | 推荐的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新其中的任何参数，请按照中的步骤操作 [启用基于MIME类型的资产/Dynamic Media Classic上传作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### 更新Granite临时工作流队列 {#updating-the-granite-transient-workflow-queue}

Granite传输工作流队列用于 **[!UICONTROL DAM更新资产]** 工作流。 在Dynamic Media中，用于图像摄取和处理。

**要更新Granite临时工作流队列，请执行以下操作：**

1. 导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 和搜索 **队列： Granite临时工作流队列**.

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，将数字更改为所需的值。

   您可以增加 **[!UICONTROL 最大并行作业数]** 以充分支持将文件大量上传到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（例如内核数量的两倍）可能会对其他并发活动产生负面影响。 因此，请根据特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite工作流队列 {#updating-the-granite-workflow-queue}

Granite工作流队列用于非临时工作流。 在Dynamic Media中，它以前使用来处理视频 **[!UICONTROL Dynamic Media编码视频]** 工作流。

**要更新Granite工作流队列，请执行以下操作：**

1. 导航到 `https://<server>/system/console/configMgr` 和搜索 **队列： Granite工作流队列**.

   >[!NOTE]
   由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，将数字更改为所需的值。

   您可以增加最大并行作业数，以充分支持将文件大量上传到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（即初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（例如内核数量的两倍）可能会对其他并发活动产生负面影响。 因此，请根据特定用例测试和调整值。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新Dynamic Media Classic上传连接 {#updating-the-scene-upload-connection}

Scene7上传连接设置将Experience Manager资源同步到Dynamic Media Classic服务器。

**要更新Dynamic Media Classic上传连接，请执行以下操作：**

1. 导航至 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 连接数]** 字段和/或 **[!UICONTROL 活动作业超时]** 字段，根据需要更改数字。

   此 **[!UICONTROL 连接数]** 设置可控制Experience Manager到Dynamic Media上传所允许的最大HTTP连接数；通常，预定义值10个连接就足够了。

   此 **[!UICONTROL 活动作业超时]** 设置确定上传的Dynamic Media资源在投放服务器中发布的等待时间。 此值默认为2100秒或35分钟。

   对于大多数用例，设置2100就足够了。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### （可选）筛选资源以进行复制 {#optional-filtering-assets-for-replication}

在非Dynamic Media部署中，您复制 *所有* 资源（图像和视频）从Experience Manager创作环境转到Experience Manager发布节点。 此工作流是必要的，因为Experience Manager发布服务器也交付资源。

但是，在Dynamic Media部署中，由于资源是通过Cloud Service交付的，因此无需将这些相同的资源复制到Experience Manager发布节点。 这种“混合发布”工作流程避免了复制资产所需的额外存储成本和较长的处理时间。 其他内容（如网站页面）将继续从Experience Manager发布节点提供。

这些过滤器提供了一种方法，使您可以 *排除* 资源复制到该Experience Manager发布节点。

#### 使用默认资源筛选器进行复制 {#using-default-asset-filters-for-replication}

如果您将Dynamic Media用于图像处理、视频处理或两者，则可以使用Adobe按原样提供的默认筛选器。 默认情况下，以下过滤器处于活动状态：

|  | 过滤器 | Mime类型 | 演绎版 |
| --- | --- | --- | --- |
| Dynamic Media图像交付 | filter-image<br>筛选集 | 开头为 **image/**<br>&#x200B;包含 **应用程序/** 结束于 **设置**. | 开箱即用的“过滤器图像”（适用于单个图像资产，包括交互式图像）和“过滤器集”（适用于旋转集、图像集、混合媒体集和轮播集）将：<br>·从复制中排除原始图像和静态图像演绎版。 |
| Dynamic Media视频交付 | 滤镜 — 视频 | 开头为 **video/** | 现成的“过滤视频”将：<br>·从复制中排除原始视频和静态缩略图演绎版。 |

>[!NOTE]
过滤器适用于MIME类型，且不能特定于路径。

#### 自定义资源筛选器以进行复制 {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` 查看过滤器。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. 要定义过滤器的MIME类型，可以按如下方式找到MIME类型：

   在左边栏中，展开 `content > dam > <locate_your_asset> > jcr:content > metadata`，然后在表中，找到 `dc:format`.

   下图是资产路径的示例。 `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   请注意 `dc:format` （对于资产） `Fiji Red.jpg` 是 `image/jpeg`.

   要使此过滤器应用于所有图像（无论其格式如何），请将值设置为 `image/*` 位置 `*` 是一个正则表达式，应用于任何格式的所有图像。

   要使过滤器仅应用于文字JPEG的图像，请输入值 `image/jpeg`.

1. 定义要在复制中包含或排除的演绎版。

   可用于筛选以进行复制的字符包括：

   | 要使用的字符 | 它如何筛选资产以进行复制 |
   | --- | --- |
   | * | 通配符 |
   | + | 包括用于复制的资产 |
   | - | 从复制中排除资产 |

   导航到 `content/dam/<locate your asset>/jcr:content/renditions`。

   下图是资产的演绎版示例。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   如果您只想复制原始内容，则可以输入 `+original`.
