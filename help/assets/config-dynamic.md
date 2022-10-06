---
title: 配置Dynamic Media — 混合模式
description: 了解如何配置Dynamic Media — 混合模式。
mini-toc-levels: 3
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '7792'
ht-degree: 2%

---

# 配置Dynamic Media — 混合模式 {#configuring-dynamic-media-hybrid-mode}

Dynamic Media-Hybrid必须启用并配置以供使用。 根据您的用例，Dynamic Media具有 [受支持的配置](#supported-dynamic-media-configurations).

>[!NOTE]
>
>如果您打算在Scene7运行模式下配置和运行Dynamic Media，请参阅 [配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md).
>
>如果您打算在混合运行模式下配置和运行Dynamic Media，请按照本页中的说明操作。

了解有关使用的更多信息 [视频](/help/assets/video.md) 在Dynamic Media。

>[!NOTE]
>
>如果您使用为不同环境（如开发、暂存和实时生产环境）设置的Adobe Experience Manager，请为每个环境配置Dynamic MediaCloud Services。

>[!NOTE]
>
>如果您的Dynamic Media配置有问题，请查看特定于Dynamic Media的日志文件。 在启用Dynamic Media时，将自动安装这些文件：
>
>* `s7access.log`
>* `ImageServing.log`
>
>它们记录在 [监控和维护Experience Manager实例](/help/sites-deploying/monitoring-and-maintaining.md).

混合发布和交付是Dynamic Media新增的Adobe Experience Manager的核心功能。 混合发布允许您从云而不是Experience Manager发布节点交付Dynamic Media资产，例如图像、集和视频。

其他内容(如Dynamic Media查看器、网站页面和静态内容)将继续从Experience Manager发布节点提供。

如果您是Dynamic Media客户，则需要使用混合投放作为所有Dynamic Media内容的投放机制。

## 视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 图像的混合发布架构 {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## 支持的Dynamic Media配置 {#supported-dynamic-media-configurations}

以下配置任务引用了以下术语：

| **术语** | **Dynamic Media已启用** | **描述** |
|---|---|---|
| Experience Manager创作节点 | 绿色圆圈中的白色复选标记 | 您部署到内部部署或通过Managed Services的创作节点。 |
| Experience Manager发布节点 | 红方的白色“X”。 | 您部署到内部部署或通过Managed Services的发布节点。 |
| 图像服务发布节点 | 绿色圆圈中的白色复选标记。 | 您在由Adobe管理的数据中心上运行的发布节点。 指图像服务URL。 |

您可以选择仅为成像、视频或成像和视频实施Dynamic Media。 要确定为特定方案配置Dynamic Media的步骤，请参阅下表。

<table>
 <tbody>
  <tr>
   <td><strong>方案</strong></td>
   <td ><strong>工作原理</strong></td>
   <td><strong>配置步骤</strong></td>
  </tr>
  <tr>
   <td>在生产中仅提供图像</td>
   <td>图像通过Adobe全球数据中心的服务器交付，然后由CDN缓存，以实现可扩展的性能和全球覆盖范围。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a>.</li>
     <li>在中配置映像 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services</a>.</li>
     <li><a href="#configuring-image-replication">配置图像复制</a>.</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>.</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产筛选器进行复制</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置</a>.</li>
     <li><a href="#delivering-assets">交付资产</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>仅在预生产（开发、QE、暂存等）中提供图像。</td>
   <td>图像通过Experience Manager发布节点交付。 在这种情况下，由于流量很小，因此无需将图像交付到Adobe的数据中心。 它允许在生产启动之前安全预览内容。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a>.</li>
     <li>Experience Manager <strong>发布</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>.</li>
     <li>设置 <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">非生产图像的资产筛选器</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在任何环境（生产、开发、QE、暂存等）中仅提供视频</td>
   <td>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 视频海报图像（在开始播放之前显示的视频缩略图）由Experience Manager发布实例交付。</td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a>.</li>
     <li>在Experience Manager上 <strong>发布</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a> （发布实例提供视频海报图像，并提供视频播放的元数据）。</li>
     <li>在中配置视频 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>.</li>
     <li>设置 <a href="#setting-up-asset-filters-for-video-only-deployments">纯视频资产筛选器</a>.</li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在生产中提供图像和视频</td>
   <td><p>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 图像和视频海报图像通过Adobe全球数据中心的服务器提供，然后由CDN缓存，以实现可扩展的性能和全球覆盖范围。</p> <p>请参阅前面的章节，以在预制作中设置图像或视频。 </p> </td>
   <td>
    <ol>
     <li>在Experience Manager上 <strong>作者</strong> 节点， <a href="#enabling-dynamic-media">启用Dynamic Media</a>.</li>
     <li>在中配置视频 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li>在中配置映像 <a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services。</a></li>
     <li><a href="#configuring-image-replication">配置图像复制</a>.</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>.</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产过滤器进行复制。</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 启用Dynamic Media {#enabling-dynamic-media}

[默认情况下，Dynamic Media 处于禁用状态。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)要利用Dynamic Media功能，您必须使用 `dynamicmedia` 运行模式，例如， `publish` 运行模式。 在启用之前，请确保查看 [技术要求](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>通过运行模式启用Dynamic Media取代了Experience Manager6.1和Experience Manager6.0中的功能，您可以在该版本中通过将 `dynamicMediaEnabled` 标记为 **[!UICONTROL true]**. 此标记在Experience Manager6.2及更高版本中不起作用。 此外，您还无需重新启动快速启动即可启用Dynamic Media。

启用Dynamic Media后，UI中即提供了Dynamic Media功能，并且每个上传的图像资产都会收到 *cqdam.pyramid.tiff* 用于快速交付动态图像演绎版的演绎版。 这些PTIFF具有以下显着优势：

* 能够仅管理单个主源图像，并即时生成无限演绎版，而无需任何额外存储。
* 能够使用交互式可视化图表，如缩放、平移和旋转。

如果要在Experience Manager中使用Dynamic Media Classic，请勿启用Dynamic Media，除非您使用 [特定方案](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media被禁用，除非您通过运行模式启用Dynamic Media。

要启用Dynamic Media，必须通过命令行或快速启动文件名启用Dynamic Media运行模式。

**要启用Dynamic Media，请执行以下操作：**

1. 在命令行中，启动快速启动时，请执行以下操作：

   * 添加 `-r dynamicmedia` 到命令行的末尾。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   如果您要发布到s7delivery，则还必须包含以下trustStore参数：

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. 请求 `https://localhost:4502/is/image` 并确保图像服务器当前正在运行。

   >[!NOTE]
   >
   >要解决Dynamic Media的问题，请在 `crx-quickstart/logs/` 目录：
   >
   >* ImageServer -&lt;portid>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer日志提供用于分析内部ImageServer进程行为的统计和分析信息。

   图像服务器日志文件名的示例： `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access日志记录通过向Dynamic Media发出的每个请求 `/is/image` 和 `/is/content`.

   这些日志仅在启用Dynamic Media时才使用。 它们未包含在 **下载完整版** 从生成的包 `system/console/status-Bundlelist` 页面；在致电客户支持(如果遇到Dynamic Media问题)时，将这两个日志附加到问题。

### 如果已将Experience Manager安装到其他端口或上下文路径…… {#if-you-installed-aem-to-a-different-port-or-context-path}

如果要部署 [Experience Manager到应用程序服务器](/help/sites-deploying/application-server-install.md) 启用Dynamic Media后，您必须配置 **自域** 中。 否则，资产的缩略图生成操作无法正常用于Dynamic Media资产。

此外，如果您在其他端口或上下文路径上运行快速启动，则还必须更改 **自域**.

启用Dynamic Media后，图像资产的静态缩略图呈现将使用Dynamic Media生成。 为了使缩略图生成功能在Dynamic Media中正常工作，Experience Manager必须对其自身执行URL请求，并且必须知道端口号和上下文路径。

在Experience Manager中：

* 的 **自域** 在 [外部器](/help/sites-developing/externalizer.md) 用于检索端口号和上下文路径。
* 如果否 **自域** 已配置，则会从Jetty HTTP服务中检索端口号和上下文路径。

在Experience ManagerQuickStart WAR部署中，无法派生端口号和上下文路径，因此您必须配置 **自域**. 请参阅 [外部器文档](/help/sites-developing/externalizer.md) 关于如何配置 **自域**.

>[!NOTE]
在 [Experience Manager快速入门独立部署](/help/sites-deploying/deploy.md), a **自域** 通常不需要配置，因为端口号和上下文路径可以自动配置。 但是，如果所有网络接口都关闭，则必须配置 **自域**.

## 禁用Dynamic Media  {#disabling-dynamic-media}

Dynamic Media默认未启用。 但是，如果您之前已启用Dynamic Media，则可以稍后将其关闭。

要在启用Dynamic Media后将其禁用，请删除 `-r dynamicmedia` 运行模式标志。

**禁用Dynamic Media:**

1. 在命令行中，启动快速启动时，可以执行以下任一操作：

   * 不添加 `-r dynamicmedia` 到命令行。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. 请求 `https://localhost:4502/is/image`. 您收到一条消息，指出Dynamic Media已禁用。

   >[!NOTE]
   禁用Dynamic Media运行模式后，用于生成 `cqdam.pyramid.tiff` 会自动跳过演绎版。 它还会禁用动态呈现版本支持和其他Dynamic Media功能。
   另请注意，在配置Dynamic MediaExperience Manager服务器后，如果禁用了Analytics运行模式，则之前在该运行模式下上传的所有资产现在都无效。

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5，零停机时间 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

如果您要将Experience Manager- Dynamic Media从6.3升级到6.5（现在包括零停机时间部署的功能），则必须运行以下curl命令。 该命令会从 `/etc` to `/conf` CRXDE Lite。

>[!NOTE]
如果您在兼容模式下运行Experience Manager实例（即，您已安装兼容包），则无需运行这些命令。

无论是否具有兼容包，您都可以对所有升级，通过运行以下Linux® curl命令，复制Dynamic Media最初附带的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要迁移您通过 `/etc` to `/conf`，运行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 配置图像复制 {#configuring-image-replication}

Dynamic Media图像交付的工作方式是：将图像资产（包括视频缩略图）从“Experience Manager作者”中发布，并将其复制到Adobe的按需复制服务（复制服务URL）。 然后，资产会通过按需图像交付服务（图像服务URL）来交付。

执行以下操作：

1. [设置身份验证](#setting-up-authentication).
1. [配置复制代理](#configuring-the-replication-agent).

复制代理将Dynamic Media资产（如图像、视频元数据）和集发布到Adobe托管的图像服务。 默认情况下，复制代理未启用。

配置复制代理后，您必须 [验证并测试是否已成功设置](#validating-the-replication-agent-for-dynamic-media). 本节将介绍这些步骤。

>[!NOTE]
创建PTIFF的默认内存限制为跨所有工作流的3 GB。 例如，您可以在其他工作流暂停时处理一个需要3 GB内存的映像，也可以并行处理10个每个需要300 MB内存的映像。
内存限制是可配置的，并适合系统资源可用性和正在处理的图像内容类型。 如果您拥有许多大型资产，并且系统上具有足够的内存，则可以提高此限制以确保并行处理图像。
超过最大内存限制的映像将被拒绝。
要更改创建PTIFF的内存限制，请导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** > **[!UICONTROL Adobe CQ Scene7 PtifManager]** 然后改变 **[!UICONTROL maxMemory]** 值。

### 设置身份验证 {#setting-up-authentication}

在作者上设置复制身份验证，以便将图像复制到Dynamic Media图像交付服务。 首先获取KeyStore，然后将其保存在 **[!UICONTROL dynamic-media-replication]** 并对其进行配置。 在配置过程中，公司管理员收到了一封欢迎电子邮件，其中包含KeyStore文件和必要的凭据。 如果您未收到此信息，请联系Adobe客户支持。

**要设置身份验证，请执行以下操作：**

1. 如果您还没有KeyStore文件和密码，请联系Adobe客户支持，以获取该文件和密码。 此信息是配置的必要部分。 它会将密钥关联到您的帐户。

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**.

1. 在“用户管理”页面上，导航到 **[!UICONTROL dynamic-media-replication]** 用户，然后选择以打开。

   ![dm复制](assets/dm-replication.png)

1. 在Dynamic-media-replication的编辑用户设置页面中，选择 **[!UICONTROL 密钥库]** 选项卡，然后选择 **[!UICONTROL 创建KeyStore]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. 输入密码，并在 **[!UICONTROL 设置KeyStore访问密码]** 对话框。

   >[!NOTE]
   记住密码，因为以后配置复制代理时必须再次输入密码。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. 在 **[!UICONTROL 编辑Dynamic-Media复制的用户设置]** 页面，展开 **从KeyStore文件添加私钥** 区域并添加以下内容（请参阅下面的图像）：

   * 在 **[!UICONTROL 新别名]** 字段，输入要在复制配置中稍后使用的别名的名称。 例如，您可以使用 `replication` 作为别名。
   * 选择 **[!UICONTROL KeyStore文件]**. 导航到按Adobe提供给您的KeyStore文件，选择它，然后选择 **[!UICONTROL 打开]**.
   * 在 **[!UICONTROL KeyStore文件密码]** 字段，输入KeyStore文件密码。 此密码为 **not** 您在步骤5中创建的KeyStore密码，但是该密码是在配置期间发送给您的欢迎电子邮件中提供的KeyStore文件密码Adobe。 如果您未收到KeyStore文件密码，请联系Adobe客户支持。
   * 在 **[!UICONTROL 私钥密码]** 字段，输入私钥密码（可以是上一步中提供的相同私钥密码）。 Adobe在预配期间向您发送的欢迎电子邮件中提供私钥密码。 如果您未收到私钥密码，请联系Adobe客户支持。
   * 在 **[!UICONTROL 私钥别名]** 字段，输入私钥别名。 例如：`*companyname*-alias`。Adobe在配置期间向您发送的欢迎电子邮件中提供私钥别名。 如果您未收到私钥别名，请联系Adobe客户支持。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 选择 **[!UICONTROL 保存并关闭]** 以保存对此用户所做的更改。

   接下来，你必须 [配置复制代理](#configuring-the-replication-agent).

### 配置复制代理 {#configuring-the-replication-agent}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**.
1. 在创作代理页面上，选择 **[!UICONTROL Dynamic Media混合图像复制(s7delivery)]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 选择 **[!UICONTROL 设置]** ，然后输入以下内容：

   * **[!UICONTROL 已启用]**  — 选中此复选框可启用复制代理。
   * **[!UICONTROL 地区]**  — 设置到适当区域：北美洲、欧洲或亚洲
   * **[!UICONTROL 租户ID]**  — 此值是发布到复制服务的公司/租户的名称。 此值是Adobe在配置期间发送给您的欢迎电子邮件中提供的租户ID。 如果您未收到此信息，请联系Adobe客户支持。
   * **[!UICONTROL 密钥存储别名]**  — 此值与 **新别名** 值 [设置身份验证](#setting-up-authentication);例如， `replication`. (请参阅 [设置身份验证](#setting-up-authentication).)
   * **[!UICONTROL 密钥存储密码]**  — 点按时创建的KeyStore密码 **[!UICONTROL 创建KeyStore]**. Adobe不提供此密码。 请参阅步骤5（共） [设置身份验证](#setting-up-authentication).

   下图显示了包含示例数据的复制代理：

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 选择 **[!UICONTROL 确定]**.

### 验证Dynamic Media的复制代理 {#validating-the-replication-agent-for-dynamic-media}

要验证Dynamic Media的复制代理，请执行以下操作：

选择 **[!UICONTROL 测试连接]**. 输出示例如下：

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
您还可以通过执行以下操作之一来检查：
* 检查复制日志，以确保资产已复制。
* 发布图像。 选择图像并选择 **[!UICONTROL 查看器]** 在下拉菜单中，选择查看器预设。 选择 **[!UICONTROL URL]**. 要验证是否可以看到图像，请复制URL路径并将其粘贴到浏览器中。
>


### 身份验证疑难解答 {#troubleshooting-authentication}

在设置身份验证时，您可能会在其解决方案中遇到以下问题。 在检查这些问题之前，请确保已设置复制。

#### 问题：包含消息的HTTP状态代码401 — 需要授权 {#problem-http-status-code-with-message-authorization-required}

此问题可能是由于未能为 `dynamic-media-replication` 用户。

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**解决方案：**
检查 `KeyStore` 保存到 **dynamic-media-replication** 用户，并提供了正确的密码。

#### 问题：无法解密密钥 — 无法解密数据 {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**解决方案：**
检查密码。 复制代理中保存的密码与用于创建密钥库的密码不同。

#### 问题：InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

此问题是由Experience Manager创作实例中的配置错误引起的。 作者的Java™进程未获得正确的 `javax.net.ssl.trustStore`. 您会在复制日志中看到以下错误：

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

或者错误日志：

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**解决方案：**
确保Experience Manager作者上的Java™进程具有系统属性 `-Djavax.net.ssl.trustStore=` 设置为有效的truststore。

#### 问题：KeyStore未设置或未初始化 {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

此问题可能是由热修复或覆盖dynamic-media-user或keystore节点的功能包所致。

复制日志示例：

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**解决方案:**

1. 导航到“用户管理”页面：
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. 在“用户管理”页面上，导航到 `dynamic-media-replication` 用户，然后选择以打开。
1. 选择 **[!UICONTROL KeyStore]** 选项卡。 如果 **[!UICONTROL 创建KeyStore]** 按钮，则必须重做 [设置身份验证](#setting-up-authentication) 早期。
1. 如果必须重做KeyStore设置，则必须执行 [配置复制代理](/help/assets/config-dynamic.md#configuring-the-replication-agent) 同样，也是。

   重新配置s7delivery复制代理。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 选择 **[!UICONTROL 测试连接]** 以便您验证配置是否有效。

#### 问题：发布代理使用SSL而不是OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

此问题可能是由于修补程序或功能包未正确安装或覆盖设置所致。

复制日志示例：

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**解决方案:**

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. 导航到s7delivery复制代理节点。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 将此设置添加到复制代理（值设置为的布尔值） **[!UICONTROL True]**):

   `enableOauth=true`

1. 在页面的左上角附近，选择 **[!UICONTROL 全部保存]**.

### 测试配置 {#testing-your-configuration}

Adobe建议您对配置进行端到端测试。

在开始此测试之前，请确保您已经执行了以下操作：

* 添加了图像预设。
* 配置 **[!UICONTROL Dynamic Media配置（6.3之前）]** Cloud Services。 此测试需要图像服务URL

**要测试您的配置，请执行以下操作：**

1. 上传图像资产。 (在资产中，导航到 **[!UICONTROL 创建]** > **[!UICONTROL 文件]** 并选择文件。)
1. 等待工作流完成。
1. 发布图像资产。 (选择资产，然后选择 **[!UICONTROL 快速发布]**.)
1. 通过打开图像并点按，导航到该图像的演绎版 **[!UICONTROL 演绎版]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 选择任何动态演绎版。
1. 要获取此资产的URL，请选择 **[!UICONTROL URL]**.
1. 导航到选定的URL并检查图像是否按预期运行。

测试已交付资产的另一种方法是，在URL后附加req=exists。

## 配置Dynamic MediaCloud Services {#configuring-dynamic-media-cloud-services}

Dynamic MediaCloud Service支持混合发布和交付图像、视频、视频分析和视频编码等内容。

在配置中，您必须输入注册ID、视频服务URL、图像服务URL、复制服务URL并设置身份验证。 此信息已在帐户配置过程中通过电子邮件发送给您。 如果您未收到此信息，请联系Adobe Experience Manager管理员或Adobe客户支持以获取该信息。

>[!NOTE]
在设置Dynamic MediaCloud Services之前，请确保设置了您的发布实例。 在配置Dynamic MediaCloud Services之前，您还必须设置复制。

**要配置Dynamic MediaCloud Services:**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media配置（6.3之前版本）]**.
1. 在Dynamic Media配置浏览器页面的左窗格中，选择 **[!UICONTROL 全球]**，然后选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建Dynamic Media配置]** 对话框的标题字段中，键入标题。
1. 如果要为视频配置Dynamic Media,

   * 在 **[!UICONTROL 注册ID]** 字段中，键入您的注册ID。
   * 在 **[!UICONTROL 视频服务URL]** 字段中，输入Dynamic Media网关的视频服务URL。

1. 如果要配置Dynamic Media以进行成像，请在 **[!UICONTROL 图像服务URL]** 字段中，输入Dynamic Media网关的图像服务URL。
1. 选择 **[!UICONTROL 保存]** 返回到Dynamic Media配置浏览器页面。
1. 要访问全局导航控制台，请选择Experience Manager徽标。

## 配置视频报告 {#configuring-video-reporting}

您可以使用Dynamic Media Hybrid在多个Experience Manager安装中配置视频报告。

**何时使用：** 在配置Dynamic Media配置（6.3之前版本）时，开始提供包括视频报告在内的多项功能。 该配置会在区域Analytics公司中创建一个报表包。 如果配置多个“创作”节点，则需为每个节点创建一个单独的报表包。 因此，各安装中的报表数据不一致。 此外，如果每个作者节点引用同一混合发布服务器，则上次作者安装会更改所有视频报告的目标报表包。 此问题会在报表包过多的Analytics系统上过载。

**入门：** 完成以下三项任务以配置视频报告。

1. 在第一个“创作”节点上配置Dynamic Media配置（6.3之前）后，创建Video Analytics预设包。 此初始任务很重要，因为它允许新配置继续使用同一报表包。
1. 将Video Analytics预设包安装到任何 ***新建*** 创作节点 ***之前*** 您可以配置Dynamic Media配置（6.3之前）。
1. 验证并调试包安装。

### 在配置第一个创作节点后创建Video Analytics预设包 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

完成此任务后，您将拥有一个包含Video Analytics预设的包文件。 这些预设包含报表包、跟踪服务器、跟踪命名空间和Experience Cloud组织ID（如果可用）。

1. 如果尚未配置，请配置Dynamic Media配置（6.3之前版本）。
1. （可选）查看并复制报表包ID（您必须有权访问JCR）。 虽然不需要具有报表包ID，但它可以更轻松地进行验证。
1. 使用包管理器创建包。
1. 编辑包以包含过滤器。

   在Experience Manager中： `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 构建包。
1. 下载或共享Video Analytics预设包，以便能够与后续的新创作节点共享该预设包。

### 在配置更多创作节点之前，请安装Video Analytics预设包 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

确保您已完成此任务 ***之前*** 您可以配置Dynamic Media配置（6.3之前）。 如果未能这样做，则会创建另一个未使用的报表包。 此外，即使视频报告继续正常运行，数据收集也未得到优化。

确保新的“创作”节点上可以访问第一个创作节点中的Video Analytics预设包。

1. 将您之前创建的Video Analytics预设包上传到包管理器。
1. 安装Video Analytics预设包。
1. 配置Dynamic Media配置（6.3之前版本）。

### 验证和调试包安装 {#verifying-and-debugging-the-package-installation}

1. 执行以下任一操作以验证并（如有必要）调试包安装：

   * **通过JCR检查Video Analytics预设**
要通过JCR检查Video Analytics预设，您必须有权访问CRXDE Lite。

      Experience Manager — 在CRXDE Lite中，导航到 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

      与 `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      如果您无权访问“创作”节点上的CRXDE Lite，则可以通过发布服务器检查预设。

   * **通过图像服务器检查Video Analytics预设**

      您可以通过发出图像服务器req=userdata请求来直接验证Video Analytics预设。
例如，要在“创作”节点上查看Analytics预设，您可以提出以下请求：

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      要在发布服务器上验证预设，您可以向发布服务器发出类似的直接请求。 创作和发布节点上的响应是相同的。 响应类似于以下内容：

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **通过视频报告工具在Experience Manager中检查Video Analytics预设**
导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频报告]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      如果您看到以下错误消息，则报表包可用，但未填充。 在系统收集任何数据之前，在新安装中，此错误是正确的（也是必需的）。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   要生成报表数据，请上传并发布一个视频。 使用 **[!UICONTROL 复制URL]** 并至少运行一次视频。

   使用视频查看器填充报表数据可能需要长达12小时。

   如果出现错误且报表包设置不正确，则会显示以下警报。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   如果在配置Dynamic Media配置（6.3之前）服务之前运行视频报告，则也会显示此错误。

### 视频报告配置故障诊断 {#troubleshooting-the-video-reporting-configuration}

* 在安装过程中，有时与Analytics API服务器的连接会超时。 安装会重试连接20次，但仍会失败。 出现这种情况时，日志文件会记录多个错误。 搜索 `SiteCatalystReportService`.
* 如果不先安装Analytics预设包，则可能会创建新的报表包。
* 从Experience Manager6.3升级到Experience Manager6.4或Experience Manager6.4.1，然后配置Dynamic Media配置（6.3之前），仍会创建报表包。 此问题已知并将在Experience Manager6.4.2中修复。

### 关于Video Analytics预设 {#about-the-video-analytics-preset}

Video Analytics预设（有时简称为Analytics预设）存储在Dynamic Media中的查看器预设旁边。 它基本上与查看器预设相同，但包含用于配置AppMeasurement和视频心率报告的信息。

预设的属性如下所示：

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (旧版Experience Manager中不存在)

Experience Manager6.4及更高版本将此预设保存在 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## 复制目录设置 {#replicating-catalog-settings}

在设置过程中，通过JCR发布您自己的默认目录设置。 要复制目录设置，请执行以下操作：

1. 在“终端”窗口中，运行以下命令：

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. 在Experience Manager中，导航到CRXDE Lite中的以下位置（需要管理员权限）：

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 选择 **[!UICONTROL 复制]** 选项卡。
1. 选择 **[!UICONTROL 复制]**.

## 复制查看器预设 {#replicating-viewer-presets}

交付 *具有查看器预设的资产，则必须复制/发布* 查看器预设。 (必须激活所有查看器预设 *和* 已复制，以获取资产的URL或嵌入代码。
请参阅 [发布查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) 以了解更多信息。

>[!NOTE]
默认情况下，当您选择 **[!UICONTROL 演绎版]** 当您选择 **[!UICONTROL 查看器]** 的详细信息视图。 您可以增加或减少可见的数量。 请参阅 [增加显示的图像预设数](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 或 [增加显示的查看器预设数](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## 筛选要复制的资产 {#filtering-assets-for-replication}

在非Dynamic Media部署中，您会复制 *全部* 资产（图像和视频）从Experience Manager创作环境到Experience Manager发布节点。 此工作流是必需的，因为Experience Manager发布服务器也会交付资产。

但是，在Dynamic Media部署中，由于资产是通过云传送的，因此无需复制这些资产来Experience Manager发布节点。 这种“混合发布”工作流可避免复制资产所需的额外存储成本和较长的处理时间。 其他内容(如Dynamic Media查看器、网站页面和静态内容)将继续从Experience Manager发布节点提供。

除复制资产外，还复制以下非资产：

* Dynamic Media交付配置： `/conf/global/settings/dam/dm/imageserver/jcr:content`
* 图像预设: `/conf/global/settings/dam/dm/presets/macros`
* 查看器预设: `/conf/global/settings/dam/dm/presets/viewer`

这些过滤器为您提供了一种 *排除* 资产复制到Experience Manager发布节点。

### 使用默认资产筛选器进行复制 {#using-default-asset-filters-for-replication}

如果您在生产中使用Dynamic Media进行(1)成像 *或* (2)成像和视频，则可以使用Adobe按原样提供的默认过滤器。 默认情况下，以下过滤器处于活动状态：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>过滤器</strong></td>
   <td><strong>Mime类型</strong></td>
   <td><strong>演绎版</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media图像交付</td>
   <td><p>过滤图像</p> <p>筛选集</p> <p> </p> </td>
   <td><p>开始于 <strong>图像/</strong></p> <p>包含 <strong>application/</strong> 结尾为 <strong>set</strong>.</p> </td>
   <td>现成的“滤镜图像”（适用于单个图像资产，包括交互式图像）和“滤镜集”（适用于旋转集、图像集、混合媒体集和轮播集）将：
    <ul>
     <li>包含PTIFF图像和元数据以进行复制(以 <strong>cqdam</strong>)。</li>
     <li>从复制中排除原始图像和静态图像演绎版。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media视频交付</td>
   <td>filter-video</td>
   <td>开始于 <strong>video/</strong></td>
   <td>现成的“filter-video”将：
    <ul>
     <li>包含用于复制的代理视频演绎版、视频缩略图/海报图像、元数据（在父视频演绎版和视频演绎版中均有）(以 <strong>cqdam</strong>)。</li>
     <li>从复制中排除原始视频和静态缩略图演绎版。<br /> <br /> <strong>注意：</strong> 代理视频演绎版不包含二进制文件，而只是节点属性。 因此，对发布者存储库大小没有影响。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic(Scene7)集成</td>
   <td><p>过滤图像</p> <p>筛选集</p> <p>filter-video</p> </td>
   <td><p>开始于 <strong>图像/</strong></p> <p>包含 <strong>application/</strong> 结尾为 <strong>set</strong>.</p> <p>开始于 <strong>video/</strong></p> </td>
   <td><p>您将传输URI配置为指向您的Experience Manager发布服务器，而不是AdobeDynamic Media云复制服务URL。 通过设置此过滤器，Dynamic Media Classic可以交付资产，而不是Experience Manager发布实例。</p> <p>现成的“filter-images”、“filter-sets”和“filter-video”将：</p>
    <ul>
     <li>包括PTIFF图像、代理视频演绎版和用于复制的元数据。 但是，由于JCR中不存在这些运行Experience Manager(即Dynamic Media Classic集成)的JCR中，因此IT会无效执行任何操作。</li>
     <li>从复制中排除原始图像、静态图像呈现、原始视频和静态缩略图呈现。 相反，Dynamic Media Classic会提供图像和视频资产。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
过滤器应用于MIME类型，并且不能特定于路径。

### 为纯视频部署设置资产过滤器 {#setting-up-asset-filters-for-video-only-deployments}

如果您使用Dynamic Media进行纯视频，请按照以下步骤设置资产过滤器以进行复制：

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**.
1. 在创作代理页面上，选择 **[!UICONTROL 默认代理（发布）]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL 代理设置]** 对话框中 **[!UICONTROL 设置]** 选项卡，勾选 **[!UICONTROL 已启用]** 来开探员。
1. 选择 **[!UICONTROL 确定]**.
1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. 定位 **[!UICONTROL filter-video]**，右键单击它，然后选择 **[!UICONTROL 复制]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish`
1. 定位 `jcr:content`，右键单击它，然后选择 **[!UICONTROL 粘贴]**.

这些步骤设置Experience Manager发布实例以交付播放所需的视频海报图像和视频元数据，而视频本身则由Dynamic MediaCloud Service交付。 过滤器还从复制中排除了发布实例中不需要的原始视频和静态缩略图演绎版。

### 在非生产部署中设置用于成像的资产过滤器 {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

如果您在非生产部署中使用Dynamic Media进行成像，请按照以下步骤设置资产过滤器以进行复制：

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**.
1. 在创作代理页面上，选择 **[!UICONTROL 默认代理（发布）]**.
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL 代理设置]** 对话框中 **[!UICONTROL 设置]** 选项卡，勾选 **[!UICONTROL 已启用]** 来开探员。
1. 选择 **[!UICONTROL 确定]**.
1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. 定位 **[!UICONTROL 过滤图像]**，右键单击它，然后选择 **[!UICONTROL 复制]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish`
1. 定位 `jcr:content`，右键单击该页面，然后转到 **[!UICONTROL 创建]** > **[!UICONTROL 创建节点]**. 输入名称 `damRenditionFilters` 类型 `nt:unstructured`.
1. 定位 `damRenditionFilters`，右键单击它，然后选择 **[!UICONTROL 粘贴]**.

这些步骤设置Experience Manager发布实例，以将图像交付到非生产环境。 过滤器还会从复制中排除原始图像和静态演绎版，这在发布实例中是不需要的。

>[!NOTE]
如果作者中有许多不同的过滤器，则每个代理需要为其分配一个不同的用户。 Granite代码强制按用户使用一个过滤器模型。 对于每个过滤器设置，始终具有不同的用户。
您是否在服务器上使用多个过滤器？ 例如，一个用于要发布的复制的过滤器，另一个用于s7delivery的过滤器。 如果是，则必须确保这两个过滤器具有不同的 **userId** 在 `jcr:content` 节点。 请参阅下图：

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 自定义用于复制的资产过滤器（可选） {#customizing-asset-filters-for-replication}

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` 以查看过滤器。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 要为过滤器定义Mime类型，可以按如下方式找到Mime类型：

   在左边栏中，展开 `content > dam > <locate_your_asset> >  jcr:content > metadata` 然后在表格中，找到 `dc:format`.

   下图是资产路径的示例 `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   请注意， `dc:format` （对于资产） `Fiji Red.jpg` is `image/jpeg`.

   要使此过滤器应用于所有图像（无论其格式如何），请将值设置为 `image/*` where `*` 是应用于任何格式的所有图像的正则表达式。

   要使过滤器仅应用于JPEG类型的图像，请输入值 `image/jpeg`.

1. 定义要在复制中包含或排除的演绎版。

   可用于筛选复制字符的字符包括：

   | 要使用的字符 | 如何筛选用于复制的资产 |
   | --- | --- |
   | `*` | 通配符 |
   | `+` | 包括用于复制的资产 |
   | `-` | 从复制中排除资产 |

   导航到 `content/dam/<locate your asset>/jcr:content/renditions`。

   下图是资产演绎版的示例。

   ![chlimage_1-513](assets/chlimage_1-4.png)

   使用上例，如果您只想复制PTIFF(金字塔TIFF)，则可以输入 `+cqdam,*` 包括以 `cqdam`. 在示例中，该演绎版为 `cqdam.pyramid.tiff`.

   如果您只想复制原件，则可以输入 `+original`.

## 配置Dynamic Media图像服务器设置 {#configuring-dynamic-media-image-server-settings}

配置Dynamic Media图像服务器涉及编辑Adobe CQ Scene7 ImageServer包和Adobe CQ Scene7 PlatformServer包。

>[!NOTE]
Dynamic Media开箱即用 [启用后](#enabling-dynamic-media). 但是，您可以选择通过配置Dynamic Media Image Server以满足特定规范或要求来微调安装。

**先决条件** - *之前* 您配置Dynamic Media Image Server，确保您的Windows® VM包含Microsoft® Visual C++库的安装。 运行Dynamic Media Image Server时需要这些库。 您可以 [在此处下载Microsoft® Visual C++ 2010 Redistributable Package(x64)](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

要配置Dynamic Media图像服务器设置，请执行以下操作：

1. 在Experience Manager的左上角，选择 **[!UICONTROL Adobe Experience Manager]** 要访问全局导航控制台，请导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Adobe Experience Manager Web控制台配置页面上，转到 **[!UICONTROL OSGi]** > **[!UICONTROL 配置]** 列出当前在Experience Manager中运行的所有包。

   Dynamic Media交付服务器位于列表中的以下名称下：

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 在包列表中，在Adobe CQ Scene7 ImageServer右侧，选择 **[!UICONTROL 编辑]** 图标。
1. 在Adobe CQ Scene7 ImageServer对话框中，设置以下配置值：

   >[!NOTE]
   通常，无需更改默认值。 但是，如果确实更改了默认值，则必须重新启动包才能使更改生效。

   | 属性 | 默认值 | 描述 |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | 用于与ImageServer进程通信的端口号。 默认情况下，会自动检测空闲端口。 |
   | `AllowRemoteAccess.name` | *`empty`* | 允许或禁止远程访问ImageServer进程。 如果为false，则图像服务器仅监听本地主机。<br> 指向本地主机的默认外部器设置必须指定特定VM实例的实际域或IP地址。 原因是本地主机指向虚拟机的父系统。<br>VM的域或IP地址必须具有主机文件条目，以便它能够解析自身。 |
   | `MaxRenderRgnPixels` | 16兆帕 | 呈现的最大大小（以百万像素为单位）。 |
   | `MaxMessageSize` | 16 MB | 已传送的最大消息大小(MB)。 |
   | `RandomAccessUrlTimeout` | 20 | 超时值，指图像服务器等待JCR响应范围内的拼贴请求的时长（以秒为单位）。 |
   | `WorkerThreads` | 10 | 工作线程数。 |

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 在包列表中，在Adobe CQ Scene7 PlatformServer右侧，选择 **[!UICONTROL 编辑]** 图标。
1. 在Adobe CQ Scene7 PlatformServer对话框中，设置以下默认值选项：

   >[!NOTE]
   Dynamic Media Image Server使用其自己的磁盘缓存来缓存响应。 Experience ManagerHTTP缓存和Dispatcher不能用于缓存来自Dynamic Media Image Server的响应。

   | 属性 | 默认值 | 描述 |
   |---|---|---|
   | 已启用缓存 | 已选中 | 是否启用响应缓存 |
   | 缓存根 | cache | 响应缓存文件夹的一个或多个路径。 相对路径针对内部s7成像包文件夹进行解析。 |
   | 缓存最大大小 | 200000000 | 响应缓存的最大大小（以字节为单位）。 |
   | 缓存最大条目数 | 100000 | 缓存中允许的最大条目数。 |

### 默认清单设置 {#default-manifest-settings}

默认清单允许您配置用于生成Dynamic Media投放响应的默认清单。 您可以微调质量(JPEG质量、分辨率、重新取样模式)、缓存（过期），并阻止渲染太大的图像(defaultpix、defaultthumbpix、maxpix)。

默认清单配置的位置取自 **[!UICONTROL 目录根]** 默认值为 **[!UICONTROL Adobe CQ Scene7 PlatformServer]** 捆绑。 默认情况下，此值位于 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![在CRXDE Lite中配置图像服务器](assets/configimageservercrxdelite.png)

您可以通过输入新值来更改属性的值（如下表所述）。

更改完默认清单后，在页面的左上角选择 **[!UICONTROL 全部保存]**.

确保选择 **[!UICONTROL 访问控制]** 选项卡（位于“属性”选项卡的右侧），然后将访问控制权限设置为 `jcr:read` 适用于所有用户和dynamic-media-replication用户。

![在CRXDE Lite中配置图像服务器并设置访问控制选项卡](assets/configimageservercrxdeliteaccesscontroltab.png)

清单设置表及其默认值：

| 属性 | 默认值 | 描述 |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | 默认背景颜色. RGB值，用于填充回复图像中不包含实际图像数据的任何区域。 另请参阅 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) 在图像提供API中。 |
| `defaultpix` | `300,300` | 默认视图大小. 如果请求未使用wid=、hei=或scl=明确指定视图大小，则服务器将限制返回图像不大于此宽度和高度。<br>指定为两个整数数字，0或更大，用逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值都设置为0，以保持它们不受约束。 不适用于嵌套/嵌入的请求。<br>另请参阅 [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) 在图像提供API中。<br>但是，通常情况下，您会使用查看器预设或图像预设来交付资产。 Defaultpix仅适用于未使用查看器预设或图像预设的资产。 |
| `defaultthumbpix` | `100,100` | 默认缩略图大小. 对缩略图请求(`req=tmb`)。<br>服务器将限制返回图像不得大于此宽度和高度。 如果出现缩略图请求(`req=tmb`)未明确指定大小，并且未明确使用指定视图大小 `wid=`, `hei=`或 `scl=`.<br>指定为两个整数数字，0或更大，用逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值都设置为0，以保持它们不受约束。<br>不适用于嵌套/嵌入的请求。<br>另请参阅 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) 在图像提供API中。 |
| `expiration` | `36000000` | 默认的客户端缓存生存时间。 提供默认过期时间间隔，以防特定目录记录不包含有效的目录：：过期值。<br>实数，0或更大。 自生成回复数据后到期的毫秒数。 设置为0时，将始终立即使回复图像过期，这会有效地禁用客户端缓存。 默认情况下，此值设置为10小时，这意味着如果发布了新图像，则旧图像需要10小时才能离开用户的缓存。 如果您需要更快清除缓存，请联系客户支持。<br>另请参阅 [过期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 在图像提供API中。 |
| `jpegquality` | `80` | 默认JPEG编码属性。 指定JPEG回复图像的默认属性。<br>整数和标记，以逗号分隔。 第一个值在1.100范围内，用于定义质量。 对于正常行为，第二个值可以为0，或者为1，以禁用JPEG编码器使用的RGB色度下采样。<br>另请参阅 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) 在图像提供API中。 |
| `maxpix` | `2000,2000` | 回复图像大小限制. 返回到客户端的最大回复图像宽度和高度。<br>如果请求导致返回图像的宽度或高度大于属性：:MaxPix，则服务器会返回错误。<br>另请参阅 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) 在图像提供API中。 |
| `resmode` | `SHARP2` | 默认重新取样模式. 指定用于缩放图像数据的默认重新取样属性和插值属性。<br>在 `resMode=` 未在请求中指定。<br>允许的值包括 `BILIN`, `BICUB`或 `SHARP2`.<br>枚举。 对于，设置为2 `bilin`, 3表示 `bicub`或4 `sharp2` 插值模式。 使用 `sharp2` 以获得最佳结果。<br>另请参阅 [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) 在图像提供API中。 |
| `resolution` | `72` | 默认对象分辨率。 提供默认对象分辨率，以防特定目录记录不包含有效的目录：:Resolution值。<br>实数，大于0。 通常以每英寸像素数表示，但也可以以其他单位表示，如每米像素数。<br>另请参阅 [分辨率](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api) 在图像提供API中。 |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | 这些值表示视频播放时间的快照，并被传递到 [encoding.com](https://www.encoding.com/). 请参阅 [关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) 以了解更多信息。 |

## 配置Dynamic Media色彩管理 {#configuring-dynamic-media-color-management}

Dynamic Media色彩管理允许您对资产进行颜色校正以进行预览。

通过颜色校正，摄取的资产会在生成的金字塔TIFF呈现版本中保留其色彩空间(RGB、CMYK、灰色)和嵌入的颜色配置文件。 当您请求动态呈现时，图像颜色会校正到目标颜色空间中。 您可以在JCR的Dynamic Media发布设置中配置输出颜色配置文件。

Adobe的色彩管理使用ICC（国际色彩联盟）配置文件，ICC定义了该配置文件的格式。

您可以配置Dynamic Media色彩管理，并使用CMYK、RGB或灰度输出配置图像预设。 请参阅 [配置图像预设](/help/assets/managing-image-presets.md).

高级用例可使用手动配置 `icc=` 用于明确选择输出颜色配置文件的修饰符：

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
Adobe的标准颜色配置文件集仅在您具有 [Software Distribution的功能包12445](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) 已安装。 所有功能包和Service Pack均可在 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 功能包12445提供Adobe的颜色配置文件。


### 安装功能包12445 {#installing-feature-pack}

要使用Dynamic Media色彩管理功能，请安装功能包12445。

**要安装功能包12445，请执行以下操作：**

1. 导航到 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 下载 `cq-6.3.0-featurepack-12445`.

   请参阅 [如何使用包](/help/sites-administering/package-manager.md) 有关在 [!DNL Adobe Experience Manager].

1. 安装功能包。

### 配置默认颜色配置文件 {#configuring-the-default-color-profiles}

安装功能包后，配置适当的默认颜色配置文件，以在请求RGB或CMYK图像数据时启用颜色校正。

**要配置默认颜色配置文件，请执行以下操作：**

1. 在 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**，导航到 `/conf/global/settings/dam/dm/imageserver/jcr:content` 其中包含默认的Adobe Color Profiles。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 通过滚动到 **[!UICONTROL 属性]** 选项卡。 手动输入属性名称、类型和值，下表对此进行了说明。 输入值后，选择 **[!UICONTROL 添加]** 然后 **[!UICONTROL 全部保存]** 保存值。

   颜色校正属性在 **颜色校正属性** 表。 可分配给颜色校正属性的值位于 **颜色配置文件** 表。

   例如， **[!UICONTROL 名称]**，添加 `iccprofilecmyk`，选择 **[!UICONTROL 类型]** `String`，然后添加 `WebCoated` as a **[!UICONTROL 值]**. 然后选择 **[!UICONTROL 添加]** 然后 **[!UICONTROL 全部保存]** 保存值。

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **颜色校正属性表**

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>默认</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">iccprofilergb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认RGB颜色配置文件的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">icprofilecmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认CMYK颜色配置文件的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认灰色配置文件的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilescrgb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认RGB颜色配置文件的名称，该配置文件用于没有嵌入颜色配置文件的RGB图像</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">icprofilesccmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于没有嵌入颜色配置文件的CMYK图像的默认CMYK颜色配置文件的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgrey</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于没有嵌入颜色配置文件的CMYK图像的默认灰色配置文件的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensation</a></td>
   <td>布尔型</td>
   <td>True</td>
   <td>指定是否在颜色校正期间执行黑点补偿。 Adobe建议此设置为打开。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">icdither</a></td>
   <td>布尔型</td>
   <td>False</td>
   <td>指定是否在颜色校正期间进行抖动。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">icrenderintent</a></td>
   <td>字符串</td>
   <td>相对</td>
   <td><p>指定渲染意图。 可接受的值包括： <strong>持久、相对、饱和度、绝对。 </strong><i></i>Adobe建议 <strong>相对 </strong><i></i>作为默认设置。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
属性名称区分大小写，且必须全部为小写。

**颜色配置文件表**

安装了以下颜色配置文件：

<table>
 <tbody>
  <tr>
   <th><p>名称</p> </th>
   <th><p>颜色空间</p> </th>
   <th><p>描述</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB（1998年）</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>AppleRGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIERGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>涂层FOGRA27(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>涂层FOGRA39(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>涂层GRACoL 2006(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatchRGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>欧洲ISO涂层FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Coated v2欧元级</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>欧元级无涂层v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>日本颜色2001涂层</td>
  </tr>
  <tr>
   <td>JapanColorJeappe</td>
   <td>CMYK</td>
   <td>日本彩色2002报纸</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>日本颜色2001无涂层</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>日本Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated（广告）</td>
  </tr>
  <tr>
   <td>新闻纸SNAP2007</td>
   <td>CMYK</td>
   <td>美国新闻纸（2007年快照）</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC（1953年）</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhotoRGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4默认CMYK</td>
  </tr>
  <tr>
   <td>PS5默认</td>
   <td>CMYK</td>
   <td>Photoshop 5默认CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>美国钣金涂层v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoated</td>
   <td>CMYK</td>
   <td>美国平板纸未涂层v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>UncoatedFogra29</td>
   <td>CMYK</td>
   <td>无涂层FOGRA29(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>美国涂层网络(SWOP)v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Web版SWOP 2006三级纸</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Web版SWOP 2006五级纸</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>美国Web Uncoated v2</td>
  </tr>
  <tr>
   <td>宽色域RGB</td>
   <td>RGB</td>
   <td>宽色域RGB</td>
  </tr>
 </tbody>
</table>

1. 选择 **[!UICONTROL 全部保存]**.

例如，您可以将 **[!UICONTROL iccprofilergb]** to `sRGB`和 **[!UICONTROL icprofilecmyk]** to **[!UICONTROL WebCoated]**.

这样做可以执行以下操作：

* 为RGB和CMYK图像启用颜色校正。
* 没有颜色配置文件的RGB图像假定位于 *sRGB* 色彩空间。
* 假定没有颜色配置文件的CMYK图像位于 *WebCoated* 色彩空间。
* 可返回RGB输出的动态演绎版，以*sRGB *色彩空间的形式返回。
* 返回CMYK输出的动态呈现，将其返回 *WebCoated* 色彩空间。

## 传送资产 {#delivering-assets}

完成上述所有任务后，图像或视频服务中会提供已激活的Dynamic Media资产。 在Experience Manager中，此功能显示在 **[!UICONTROL 复制图像URL]**, **[!UICONTROL 复制查看器URL]**, **[!UICONTROL 嵌入查看器代码]**、和。

请参阅 [传送Dynamic Media资产](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>当你……</strong></td>
   <td><strong>结果</strong></td>
  </tr>
  <tr>
   <td>复制图像URL</td>
   <td><p>“复制URL”对话框显示一个与以下类似的URL（URL仅用于演示目的）：</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>其中 <code>IMAGESERVICEPUBLISHNODE</code> 是指图像服务URL。</p> <p>另请参阅 <a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>.</p> </td>
  </tr>
  <tr>
   <td>复制查看器URL</td>
   <td><p>“复制URL”对话框显示一个与以下内容类似的URL（URL仅用于演示目的）：</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>其中 <code>PUBLISHNODE</code> 是指常规Experience Manager发布节点和 <code>IMAGESERVICEPUBLISHNODE</code> 是指图像服务URL。</p> <p>另请参阅 <a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>.</p> </td>
  </tr>
  <tr>
   <td>复制查看器的嵌入代码</td>
   <td><p>“复制嵌入代码”对话框显示一个与以下内容类似的代码片段（代码示例仅用于演示目的）：</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>其中 <code>PUBLISHNODE</code> 是指常规Experience Manager发布节点和 <code>IMAGESERVICEPUBLISHNODE</code> 是指图像服务URL。</p> <p>另请参阅 <a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media和交互式媒体组件 {#wcm-dynamic-media-and-interactive-media-components}

引用Dynamic Media和交互式媒体组件的WCM页面引用交付服务。
