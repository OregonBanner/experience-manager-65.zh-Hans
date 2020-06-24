---
title: 配置Dynamic Media-混合模式
description: 了解如何配置Dynamic Media-混合模式。
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
translation-type: tm+mt
source-git-commit: 7e9dcebc654e63e171e2baacfe53081f58676f8d
workflow-type: tm+mt
source-wordcount: '7951'
ht-degree: 1%

---


# 配置Dynamic Media-混合模式{#configuring-dynamic-media-hybrid-mode}

Dynamic Media-混合需要启用并配置以供使用。 根据您的用例，Dynamic Media具有多种受 [支持的配置](#supported-dynamic-media-configurations)。

>[!NOTE]
>
>如果要在Scene7运行模式下配置和运行Dynamic Media，请参 [阅配置Dynamic Media- Scene7模式](/help/assets/config-dms7.md)。
>
>如果要在混合运行模式下配置和运行Dynamic Media，请按照本页中的说明操作。

进一步了解如何在 [Dynamic Media](/help/assets/video.md) 中使用视频。

>[!NOTE]
>
>如果您使用为不同环境设置的Adobe Experience Manager，例如一个用于开发，一个用于暂存，另一个用于实时生产，您需要为这些环境中的每个配置Dynamic MediaCloud Service。

>[!NOTE]
>
>如果您的Dynamic Media配置有问题，一个重要的查找位置是特定于Dynamic Media的日志文件。 在启用Dynamic Media时，这些组件会自动安装：
>
>* `s7access.log`
>* `ImageServing.log`

>
>
它们在监视 [和维护AEM实例中有说明](/help/sites-deploying/monitoring-and-maintaining.md)。

混合出版和投放是Adobe Experience Manager之外的Dynamic Media的核心功能。 混合发布允许您从云而不是AEM发布节点传送Dynamic Media资产，如图像、集和视频。

AEM发布节点将继续提供Dynamic Media查看器、站点页面和静态内容等其他内容。

如果您是Dynamic Media的客户，则必须使用混合投放作为所有Dynamic Media内容的投放机制。

## 用于视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 图像的混合出版架构 {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## 支持的Dynamic Media配置 {#supported-dynamic-media-configurations}

遵循的配置任务引用了以下术语：

| **术语** | **Dynamic Media已启用** | **描述** |
|---|---|---|
| AEM作者节点 | 绿色圆圈中的白色复选标记 | 您部署到内部部署或通过Managed Services部署的作者节点。 |
| AEM发布节点 | 红方的白色“X”。 | 您部署到内部部署或通过Managed Services部署的发布节点。 |
| 图像服务发布节点 | 绿色圆圈中的白色复选标记。 | 您在由Adobe管理的数据中心上运行的发布节点。 引用图像服务URL。 |

您可以选择仅针对成像、仅针对视频或针对成像和视频实施Dynamic Media。 要确定为特定方案配置Dynamic Media的步骤，请参阅下表。

<table>
 <tbody>
  <tr>
   <td><strong>方案</strong></td>
   <td ><strong>工作原理</strong></td>
   <td><strong>配置步骤</strong></td>
  </tr>
  <tr>
   <td>在制作中仅提供图像</td>
   <td>图像通过Adobe全球数据中心的服务器交付，然后由CDN缓存，以实现可扩展的性能和全球范围。</td>
   <td>
    <ol>
     <li>在AEM作者 <strong>节点上</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a>。</li>
     <li>在Dynamic Media <a href="#configuring-dynamic-media-cloud-services">Cloud Service中配置映像</a>。</li>
     <li><a href="#configuring-image-replication">配置映像复制</a>。</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产过滤器进行复制</a>。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置</a>。</li>
     <li><a href="#delivering-assets">交付资产</a>。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>在预制作（开发、量化宽松、舞台等）中仅提供图像。</td>
   <td>图像通过AEM发布节点交付。 在这种情况下，由于流量很小，因此无需将图像传送到Adobe的数据中心。 另一个好处是，这允许在生产启动之前安全预览内容</td>
   <td>
    <ol>
     <li>在AEM作者 <strong>节点上</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a>。</li>
     <li>在AEM发 <strong>布节点上</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li>为非生 <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">产图像设置资产筛选器</a>。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在任何环境（生产、开发、QE、舞台等）中只提供视频</td>
   <td>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 视频海报图像（在播放开始前显示的视频缩略图）将由AEM发布实例提供。</td>
   <td>
    <ol>
     <li>在AEM作者 <strong>节点上</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a>。</li>
     <li>在AEM发 <strong>布节点</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a> （发布实例提供视频海报图像并提供视频回放的元数据）。</li>
     <li>在Dynamic Media <a href="#configuring-dynamic-media-cloud-services">Cloud Service中配置视频。</a></li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li>为仅视 <a href="#setting-up-asset-filters-for-video-only-deployments">频设置资产筛选器</a>。</li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在制作中提供图像和视频</td>
   <td><p>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 图像和视频海报图像通过Adobe全球数据中心的服务器交付，然后由CDN缓存，以实现可扩展的性能和全球范围。</p> <p>请参阅前面几节，在预制作中设置图像或视频。 </p> </td>
   <td>
    <ol>
     <li>在AEM作者 <strong>节点上</strong> ，启 <a href="#enabling-dynamic-media">用Dynamic Media</a>。</li>
     <li>在Dynamic Media <a href="#configuring-dynamic-media-cloud-services">Cloud Service中配置视频。</a></li>
     <li>在Dynamic MediaCloud Service <a href="#configuring-dynamic-media-cloud-services">中配置映像。</a></li>
     <li><a href="#configuring-image-replication">配置映像复制</a>。</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产过滤器进行复制。</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media图像服务器设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 启用Dynamic Media {#enabling-dynamic-media}

[默认情况](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) 下，Dynamic Media处于禁用状态。 要利用Dynamic Media功能，您需要像运行模式一样 `dynamicmedia` 使用运行模式来启用 `publish` Dynamic Media。 在启用之前，请确保查看技 [术要求。](/help/sites-deploying/technical-requirements.md#dynamicmediaaddonprerequisites)

>[!NOTE]
>
>通过运行模式启用Dynamic Media将替换AEM 6.1和AEM 6.0中的功能，您可以通过将标志设置为true来启用 `dynamicMediaEnabled` Dynamic Media **[!UICONTROL 的功能。]** 此标志在AEM 6.2和更高版本中没有功能。 此外，您无需重新启动快速启动即可启用Dynamic Media。

通过启用Dynamic Media,Dynamic Media功能将在UI中可用，并且每个上传的图像资产都会收到 *cqdam.pyramid.tiff* 再现，该再现用于动态图像再现的快速投放。 这些PTIFF具有显着优势，包括(1)仅管理单个主源图像并动态生成无限再现而无需任何附加存储，以及(2)使用交互式可视化（如缩放、平移、旋转等）的能力。

如果要在AEM中使用Dynamic Media经典(Scene7)，则不应启用Dynamic Media，除非您使用的是特 [定方案](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)。 Dynamic Media被禁用，除非您通过runmode启用dynamic media。

要启用Dynamic Media，必须从命令行或快速启动文件名中启用Dynamic Media运行模式。

**启用Dynamic Media**

1. 在命令行上，启动快速启动时，请执行以下操作：

   * 在 `-r dynamicmedia` 启动jar文件时添加到命令行末尾。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   如果要发布到s7投放，则还需要包含以下trustStore参数：

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. 请 `https://localhost:4502/is/image` 求并确保图像服务器正在运行。

   >[!NOTE]
   >
   >要对Dynamic Media问题进行疑难解答，请参阅目录中的以下 `crx-quickstart/logs/` 日志：
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer日志提供用于分析内部ImageServer进程行为的统计和分析信息。

   图像服务器日志文件名的示例： `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access日志记录通过和向Dynamic Media发出的每个 `/is/image` 请求 `/is/content`。

   仅当启用Dynamic Media时，才使用这些日志。 它们不包含在从页 **面生成** 的下载完整 `system/console/status-Bundlelist` 包中； 如果您遇到Dynamic Media问题，请在致电客户支持时，将这两个日志附加到该问题。

### 如果将AEM安装到其他端口或上下文路径…… {#if-you-installed-aem-to-a-different-port-or-context-path}

如果要将AEM部 [署到应用程序服务器](/help/sites-deploying/application-server-install.md) ，并启用Dynamic Media **，则需要在externalizer中配置** self domain。 否则，Dynamic Media资产的资产缩略图生成将无法正常工作。

此外，如果在其他端口或上下文路径上运行快速启动，则还必须更改 **自定义** 域。

启用Dynamic Media后，将使用Dynamic Media生成图像资产的静态缩略图演绎版。 为了使缩略图生成能够正常用于Dynamic Media,AEM必须对其自身执行URL请求，并且必须知道端口号和上下文路径。

在AEM中：

* 外 **部器** 中的自 [我域](/help/sites-developing/externalizer.md) 用于检索端口号和上下文路径。
* 如果未 **配置** 自域，则从Jetty HTTP服务检索端口号和上下文路径。

在AEM QuickStart WAR部署中，无法派生端口号和上下文路径，因此必须配置 **自定义** 域。 请参 [阅](/help/sites-developing/externalizer.md) externalizer文档，了解如何 **配置** self域。

>[!NOTE]
在AEM [快速启动独立部署中](/help/sites-deploying/deploy.md)，自 **身域通常不需要配置** ，因为可以自动配置端口号和上下文路径。 但是，如果所有网络接口都关闭，则需要配置 **自身** 域。

## 禁用Dynamic Media  {#disabling-dynamic-media}

默认情况下，Dynamic Media未启用。 但是，如果您以前启用了Dynamic Media，您可能希望稍后将其关闭。

要在启用Dynamic Media后禁用它，请删除运行 `-r dynamicmedia` 模式标志。

**在启用Dynamic Media后禁用**

1. 在命令行上，启动快速启动时，可以执行下列操作之一：

   * 启动jar文 `-r dynamicmedia` 件时，不要添加到命令行。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Request `https://localhost:4502/is/image`. 您会收到一条消息，指示Dynamic Media已禁用。

   >[!NOTE]
   禁用Dynamic Media运行模式后，将自动跳过生成再现 `cqdam.pyramid.tiff` 的工作流步骤。 这也会禁用动态再现支持和其他Dynamic Media功能。
   另请注意，在配置AEM服务器后，当Dynamic Media运行模式被禁用时，在该运行模式下上传的所有资产现在都无效。

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5零停机时间 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

如果您要将AEMDynamic Media从6.3升级到6.5（现在包括零停机时间部署的功能），您需要运行以下curl命令，以将所有预设和配置从CRXDE Lite迁 `/etc` 移到 `/conf` CRXDE Lite。

**注意**: 如果您在兼容模式下运行AEM实例（即，您已安装兼容包），则无需运行这些命令。

对于所有具有或没有兼容性包的升级，您都可以通过运行以下Linux curl命令复制Dynamic Media最初附带的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要将您创建的任何自定义查看器预设和配置从迁移 `/etc` 到 `/conf`，请运行以下Linux curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 配置映像复制 {#configuring-image-replication}

Dynamic Media图像投放的工作方式是：将图像资产（包括视频缩略图）从AEM Author发布并复制到Adobe的点播复制服务（复制服务URL）。 然后，资产会通过按需图像投放服务（图像服务URL）交付。

您必须执行以下操作：

1. [设置身份验证](#setting-up-authentication)。
1. [配置复制代理](#configuring-the-replication-agent)。

复制代理将发布Dynamic Media资产（如图像、视频元数据）并将其集合到由Adobe托管的图像服务。 默认情况下，复制代理未启用。

配置复制代理后，您需要验 [证并测试它是否已成功设置](#validating-the-replication-agent-for-dynamic-media)。 本节介绍这些过程。

>[!NOTE]
创建PTIFF的默认内存限制为所有工作流的3 GB。 例如，您可以处理一个需要3 GB内存的图像，而其他工作流则暂停；或者，您可以并行处理10个图像，每个图像需要300 MB内存。
内存限制是可配置的，并且应符合系统资源可用性和正在处理的图像内容类型。 如果您拥有许多超大资源并且系统内存充足，您可以增加此限制以确保并行处理图像。
需要超过最大内存限制的图像将被拒绝。
要更改创建PTIFF的内存限制，请导航到“工 **[!UICONTROL 具”>“操作”>“Web控制台”>“Adobe CQ Scene7 PTiffManager]** ”，然后更 **[!UICONTROL 改maxMemory]** 值。

### 设置身份验证 {#setting-up-authentication}

您需要在创作时设置复制身份验证，才能将映像复制到Dynamic Media映像投放服务。 为此，请获取一个KeyStore，然后将其保存在 **[!UICONTROL Dynamic-media-replication用户下]** ，并进行配置。 在设置过程中，您的公司管理员应已收到一封包含KeyStore文件和必需凭据的欢迎电子邮件。 如果您未收到此信息，请联系客户服务。

**设置身份验证**

1. 如果您尚未提供KeyStore文件和密码，请与客户服务部联系。 这是配置的一部分，它将密钥关联到您的帐户。
1. In AEM, tap the AEM logo to access the global navigation console, then tap **[!UICONTROL Tools > Security > Users.]**
1. 在“用户管理”页上，导航到 **[!UICONTROL dynamic-media-replication用户]** ，然后点按以打开。

   ![dm复制](assets/dm-replication.png)

1. 在“Edit User Settings For dynamic-media-replication”（编辑动态媒体复制的用户设置）页中，点 **[!UICONTROL 击Keystore]** （密钥库）选项卡，然 **[!UICONTROL 后单击Create KeyStore。]**

   ![dm复制密钥库](assets/dm-replication-keystore.png)

1. 在“设置密钥存储访问密码”对 **[!UICONTROL 话框中输入密码并]** 确认密码。

   >[!NOTE]
   请记住您输入的密码。 以后配置复制代理时，您需要再次输入它。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. 在“编 **[!UICONTROL 辑User Settings For dynamic-media]** -replication”页面上 **，展开“从KeyStore** 添加私钥”文件区域，并添加以下内容（请参阅下面的图像）:

   * 在“ **[!UICONTROL 新别名]** ”字段中，输入稍后在复制配置中使用的别名名称； 例如 `replication`,
   * 点按 **[!UICONTROL 密钥存储文件。]** 导航到Adobe提供给您的KeyStore文件，将其选中，然后点按打 **[!UICONTROL 开。]**
   * 在“KeyStore **[!UICONTROL 文件口令]** ”字段中，输入KeyStore文件口令。 这不是 **您在步骤** 5中创建的KeyStore密码，而是Adobe在配置过程中向您发送的欢迎电子邮件中提供的KeyStore文件密码。 如果您未收到KeyStore文件密码，请与Adobe客户服务部门联系。
   * 在“ **[!UICONTROL 私钥密码]** ”字段中，输入私钥密码（可能与上一步中提供的私钥密码相同）。 在设置过程中，Adobe会在向您发送的欢迎电子邮件中提供私钥密码。 如果您未收到私钥密码，请与Adobe客户服务联系。
   * 在私钥 **[!UICONTROL 别名字段中]** ，输入私钥别名。 For example, `*companyname*-alias`. 在设置过程中，Adobe在向您发送的欢迎电子邮件中提供私钥别名。 如果您未收到私钥别名，请与Adobe客户服务联系。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 点按 **[!UICONTROL 保存并关闭]** ，以保存对此用户所做的更改。

   接下来，您需 [要配置复制代理。](#configuring-the-replication-agent)

### 配置复制代理 {#configuring-the-replication-agent}

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点按工 **[!UICONTROL 具>部署>复制>创作代理。]**
1. 在创作页面上的代理中，点 **[!UICONTROL 按Dynamic Media混合图像复制(s7投放)。]**
1. 点按 **[!UICONTROL 编辑。]**
1. 点按设 **[!UICONTROL 置]** 选项卡，然后输入以下内容：

   * **[!UICONTROL 启用]** -选中此复选框可启用复制代理。
   * **[!UICONTROL 区域]** -设置为相应的区域： 北美、欧洲或亚洲
   * **[!UICONTROL 租户ID]** —— 此值是发布到复制服务的公司/租户的名称。 此值是Adobe在设置过程中在向您发送的欢迎电子邮件中提供的租户ID。 如果您未收到此信息，请与Adobe客户服务部门联系。
   * **[!UICONTROL 密钥存储别名]** -此值与在设置身份验证中生成密钥时设置的**新别名** [值相同](#setting-up-authentication); 例如 `replication`, (请参阅设置身 [份验证中的步骤](#setting-up-authentication)7。)
   * **[!UICONTROL 密钥存储密码]** -这是您在点击创建密钥存储时创建的 **[!UICONTROL KeyStore密码。]** Adobe不提供此密码。 请参阅设置身 [份验证的第5步](#setting-up-authentication)。

   下图显示了具有示例数据的复制代理：

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 点按 **[!UICONTROL 确定。]**

### 验证Dynamic Media的复制代理 {#validating-the-replication-agent-for-dynamic-media}

要验证Dynamic Media的复制代理，请执行以下操作：

点按 **[!UICONTROL 测试连接。]** 输出示例如下：

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
您还可以通过执行下列操作之一来检查：
* 检查复制日志，确保资产已复制。
* 发布图像。 点按图像，然后在下 **[!UICONTROL 拉菜]** 单中选择查看器。 然后选择一个查看器预设，单击URL，在浏览器中复制／粘贴该URL，以验证您是否可以看到该图像。



### 身份验证疑难解答 {#troubleshooting-authentication}

在设置身份验证时，您可能会遇到以下一些问题，这些问题与他们的解决方案一起使用。 在检查这些复制之前，请确保已设置复制。

#### 问题： HTTP状态代码401（带有消息）-需要授权 {#problem-http-status-code-with-message-authorization-required}

此问题可能是由于用户未能设置KeyStore而引 `dynamic-media-replication` 起的。

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

**解决方案**: 检查是否 `KeyStore` 已保存 **到Dynamic Media Replication用户** ，并且提供了正确的密码。

#### 问题： 无法解密密钥——无法解密数据 {#problem-could-not-decrypt-key-could-not-decrypt-data}

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

**解决方案**: 检查密码。 复制代理中保存的密码与用于创建密钥库的密码不同。

#### 问题： InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

此问题是由AEM Author实例中的配置错误引起的。 作者上的java进程未获得正确的结果 `javax.net.ssl.trustStore`。 复制日志中显示此错误：

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

或错误日志：

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**解决方案**: 确保AEM Author上的java进程将系统属性设 `-Djavax.net.ssl.trustStore=` 置为有效的信任存储。

#### 问题： KeyStore未设置或未初始化 {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

此问题可能由热修复或覆盖Dynamic Media用户或密钥库节点的功能包引起。

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

**解决方案**：

1. 导航到“用户管理”页：
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. 在“用户管理”页面上，导航到 `dynamic-media-replication` 该用户，然后点按以打开。
1. Click the **[!UICONTROL KeyStore]** tab. 如果显 **[!UICONTROL 示“创建密钥]** ”按钮 [，则需要重做之前设置身份验证](#setting-up-authentication) 下的步骤。
1. 如果必须重做KeyStore设置，则可能还需要 [再次配置复制代理](/help/assets/config-dynamic.md#configuring-the-replication-agent) 。

   重新配置s7投放复制代理。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 点按 **[!UICONTROL 测试连接]** ，以验证配置是否有效。

#### 问题： 发布代理使用SSL而不是OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

此问题可能是由于修补程序或功能包安装不正确或覆盖设置所致。

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

**解决方案：**

1. In AEM, click **[!UICONTROL Tools > General > CRXDE Lite.]**

   `localhost:4502/crx/de/index.jsp`

1. 导航到s7投放复制代理节点。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 将此设置添加到复制代理(值设置为True的布尔 **[!UICONTROL 值]**):

   `enableOauth=true`

1. Near the upper-left corner of the page, tap **[!UICONTROL Save All.]**

### 测试配置 {#testing-your-configuration}

Adobe建议您对配置执行端对端测试。

在开始此测试之前，请确保您已经执行了以下操作：

* 添加的图像预设。
* 在 **[!UICONTROL Dynamic Media下配置Cloud Service配置(6.3之前]** )。 此测试需要图像服务URL

**测试配置**

1. 上传图像资产。 (在资产中，点按 **[!UICONTROL 创建>文件]** ，然后选择文件。)
1. 等待工作流完成。
1. 发布图像资产。 (选择资产，然后点 **[!UICONTROL 按快速发布。]**)
1. 通过打开图像并点按演绎版，导航到该图像的演绎 **[!UICONTROL 版。]**

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 选择任何动态演绎版。
1. 单 **[!UICONTROL 击]** URL可获取此资产的URL。
1. 导航到所选URL并检查图像的行为是否按预期方式显示。

测试已交付资产的另一种方法是将req=exists附加到您的URL。

## Configuring Dynamic Media Cloud Services {#configuring-dynamic-media-cloud-services}

Dynamic Media云服务提供云服务支持，例如混合发布和图像和视频投放、视频分析和视频编码等。

在配置中，您需要输入注册ID、视频服务URL、图像服务URL、复制服务URL并设置身份验证。 您应该已经在帐户设置过程中收到了所有这些信息。 如果您未收到此信息，请与Adobe Experience Manager管理员或Adobe技术支持联系以获取该信息。

>[!NOTE]
在设置Dynamic Media云服务之前，请确保设置发布实例。 在配置Dynamic Media云服务之前，还必须设置复制。

要配置Dynamic Media云服务，请执行以下操作：

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点 **[!UICONTROL 按工具>Cloud Service>Dynamic Media配置（6.3之前版本）。]**
1. 在“Dynamic Media配置浏览器”页面的左窗格中，选择全 **[!UICONTROL 局]**，然后点按 **[!UICONTROL 创建。]**
1. 在“创 **[!UICONTROL 建Dynamic Media配置]** ”对话框的“标题”字段中，键入标题。
1. 如果要为视频配置Dynamic Media,

   * 在“注 **[!UICONTROL 册ID]** ”字段中，键入注册ID。
   * 在“视 **[!UICONTROL 频服务URL ]**”字段中，输入Dynamic Media网关的视频服务URL。

1. 如果要配置Dynamic Media以进行成像，请在 **[!UICONTROL 图像服务URL]** 字段中，输入Dynamic Media网关的图像服务URL。
1. 点按 **[!UICONTROL 保存]** ，返回“Dynamic Media配置浏览器”页。
1. 点按AEM徽标以访问全局导航控制台。

## 配置视频报告 {#configuring-video-reporting}

您可以使用报告混合在AEM的多个安装中配置视频Dynamic Media。

**何时使用：** 在配置Dynamic Media配置（6.3之前版本）时，将启动包括视频报告在内的众多功能。 该配置在区域Analytics公司中创建报表包。 如果配置多个作者节点，则为每个节点创建一个单独的报表包。 因此，报告数据在安装之间不一致。 此外，如果每个作者节点引用同一混合发布服务器，则上次作者安装会更改所有视频报告的目标报表包。 此问题使Analytics系统的报表包过多。

**开始：** 通过完成以下三个报告配置视频任务。

1. 在第一个作者节点上配置Dynamic Media配置（6.3之前版本）后，创建一个视频Analytics预设包。 此初始任务很重要，因为它允许新配置继续使用同一报表包。
1. 在配置“Analytics配置”(6.3 ***之前*** ，请先将“视频 ***Dynamic Media*** ”预设包安装到任何新的“作者”节点。
1. 验证并调试包安装。

### 在配置第一个作者节点后创建视频Analytics预设包 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

完成此任务后，您将有一个包文件，其中包含视频Analytics预设。 这些预设包含报表包、跟踪服务器、跟踪命名空间和Marketing Cloud组织ID（如果可用）。

1. 如果尚未配置Dynamic Media配置（6.3之前）。
1. （可选）视图并复制报表包ID（您必须有权访问JCR）。 虽然不需要使用报表包ID，但它使验证更简单。
1. 使用包管理器创建包。
1. 编辑包以包含过滤器。

   在AEM中： `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 构建包。
1. 下载或共享视频Analytics预设包，以便与后续新的作者节点共享。

### 在配置其他作者节点之前安装视频Analytics预设包 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

请确保在配置任务配 ***置*** （6.3之前）之前完成此Dynamic Media。 否则，将创建另一个未使用的报表包。 此外，即使视频报告仍能正常工作，数据收集也未得到优化。

确保可在新的“作者”节点上访问来自第一个“作者”节点的视频Analytics预设包。

1. 将您创建的视频Analytics预设包上传到包管理器。
1. 安装视频Analytics预设包。
1. 配置Dynamic Media配置（6.3之前版本）。

### 验证和调试包安装 {#verifying-and-debugging-the-package-installation}

1. 执行下列任一操作以验证并（如有必要）调试包安装：

   * **通过JCR检查视频Analytics预设**&#x200B;要通过JCR检查视频Analytics预设，您必须具有对CRXDE Lite的访问权限。

      AEM —— 在CRXDE Lite中，导航到 `/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`

      就是 `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      如果您无权访问“作者”节点上的CRXDE Lite，则可以通过发布服务器检查预设。

   * **通过图像服务器检查视频Analytics预设**

      您可以通过发出图像服务器req=userdata请求直接验证视频Analytics预设。
例如，要在“作者”节点上查看“Analytics”预设，您可以发出以下请求：

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      要验证发布服务器上的预设，您可以向发布服务器发出类似的直接请求。 “作者”和“发布”节点上的响应相同。 响应类似于：**

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **通过AEM中的视频Analytics工具检查视频报告预设**，点 **[!UICONTROL 按工具>资产>视频报告]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      如果看到以下错误消息，则报表包可用，但未填充。 在系统收集任何数据之前，在新安装中出现此错误是正确的，并且是需要的。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   要生成报告数据，请上传并发布一个视频。 使 **[!UICONTROL 用复制]** URL并至少运行视频一次。

   请注意，从视频查看器的使用情况填充报告数据可能需要12小时。

   如果出现错误且报告包设置不正确，将显示以下警报。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   如果在配置报告配置（6.3以前版本）服务之前运行视频Dynamic Media，则还会显示此错误。

### 视频报告配置疑难解答 {#troubleshooting-the-video-reporting-configuration}

* 在安装过程中，有时与AnalyticsAPI服务器的连接会超时。 安装重试连接20次，但仍然失败。 出现这种情况时，日志文件会记录多个错误。 搜索 `SiteCatalystReportService`.
* 不首先安装Analytics预设包可能会创建新报表包。
* 从AEM 6.3升级到AEM 6.4或AEM 6.4.1，然后配置Dynamic Media配置（6.3之前），仍会创建报表包。 此问题已知并将在AEM 6.4.2中修复。

### 关于视频Analytics预设 {#about-the-video-analytics-preset}

视频Analytics预设（有时也称为分析预设）存储在查看器预设的Dynamic Media中。 它基本上与查看器预设相同，但包含用于配置AppMeasurement和视频心跳报告的信息。

预设的属性如下所示：

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` （旧版AEM中不存在）

AEM 6.4及更高版本将此预设保存在 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## 复制目录设置 {#replicating-catalog-settings}

您必须通过JCR在安装过程中发布自己的默认目录设置。 要复制目录设置：

1. 在“终端”窗口中，运行以下内容：

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. 在AEM中，导航到CRXDE Lite中的以下位置（需要管理员权限）:

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Tap the **[!UICONTROL Replication]** tab.
1. 点按 **[!UICONTROL 复制。]**

## 复制查看器预设 {#replicating-viewer-presets}

要传送带 *有查看器预设的资产，您必须复制／发布该查看器* 预设。 (All viewer presets must be activated *and* replicated to obtain the URL or embed code for an asset.
有关详 [细信息，请参阅](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) “发布查看器预设”。

>[!NOTE]
By default, the system shows a variety of renditions when you select **[!UICONTROL Renditions]** and a variety of viewer presets when you select **[!UICONTROL Viewers]** in the asset&#39;s detail view. 您可以增加或减少所看到的数量。 See [Increasing the number of image presets that display](/help/assets/managing-image-presets.md#increasingthenumberofimagepresetsthatdisplay) or [Increasing the number of viewer presets that display](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## 筛选要复制的资产 {#filtering-assets-for-replication}

在非Dynamic Media部署中，您可 *以将* 所有资产（包括图像和视频）从AEM作者环境复制到AEM发布节点。 此工作流是必需的，因为AEM发布服务器也会传送资产。

但是，在Dynamic Media部署中，由于资产是通过云传送的，因此无需将这些资产复制到AEM发布节点。 这种“混合发布”工作流程可避免复制资产的额外存储成本和更长的处理时间。 AEM发布节点继续提供Dynamic Media查看器、站点页面和静态内容等其他内容。

除复制资产外，还复制以下非资产：

* Dynamic Media投放配置： `/conf/global/settings/dam/dm/imageserver/jcr:content`
* 图像预设: `/conf/global/settings/dam/dm/presets/macros`
* 查看器预设: `/conf/global/settings/dam/dm/presets/viewer`

这些过滤器为您提供了一种方 *法* ，可以排除资产被复制到AEM发布节点。

### 使用默认资产过滤器进行复制 {#using-default-asset-filters-for-replication}

如果您使用的Dynamic Media是(1)在生产中进 **行成像** ，或(2)在成像和视频中进行成像，则您可以使用我们按原样提供的默认过滤器。 默认情况下，以下过滤器处于活动状态：

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>筛选器</strong></td>
   <td><strong>Mime 类型</strong></td>
   <td><strong>演绎版</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media图像投放</td>
   <td><p>滤镜图像</p> <p>过滤器集</p> <p> </p> </td>
   <td><p>开始 <strong>/图像</strong></p> <p>包 <strong>含应用</strong> 程序／以 <strong>集结尾</strong>。</p> </td>
   <td>现成的“滤镜图像”（适用于单个图像资产，包括交互式图像）和“滤镜集”（适用于旋转集、图像集、混合媒体集和旋转集）将：
    <ul>
     <li>包括PTIFF图像和用于复制的元数据(以cqdam开头的任 <strong>何再</strong>现)。</li>
     <li>从复制中排除原始图像和静态图像演绎版。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media视频投放</td>
   <td>过滤视频</td>
   <td>开始 <strong>视频/</strong></td>
   <td>现成的“过滤器——视频”将：
    <ul>
     <li>包括用于复制的代理视频演绎版、视频缩略图／海报图像、元数据（父视频和视频演绎版中均有）(以cqdam开头的 <strong>任何演</strong>绎版)。</li>
     <li>从复制中排除原始视频和静态缩略图再现。<br /> <br /> <strong>注意：</strong> 代理视频演绎版不包含二进制文件，而只是节点属性。 因此，不会影响发布者存储库大小。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media经典(Scene7)集成</td>
   <td><p>滤镜图像</p> <p>过滤器集</p> <p>过滤视频</p> </td>
   <td><p>开始 <strong>/图像</strong></p> <p>包 <strong>含应用</strong> 程序／以 <strong>集结尾</strong>。</p> <p>开始 <strong>视频/</strong></p> </td>
   <td><p>您配置传输URI以指向您的AEM发布服务器，而不是AdobeDynamic Media云复制服务URL。 设置此过滤器将允许Dynamic Media经典传送资产，而不是AEM发布实例。</p> <p>现成的“filter-images”、“filter-sets”和“filter-video”将：</p>
    <ul>
     <li>包括PTIFF图像、代理视频演绎版和用于复制的元数据。 但是，由于JCR中不存在这些AEM -Dynamic Media经典集成，因此JCR有效无效。</li>
     <li>从复制中排除原始图像、静态图像演绎版、原始视频和静态缩略图演绎版。 相反，Dynamic Media经典将提供图像和视频资产。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
过滤器应用于mime类型，不能特定于路径。

### 为纯视频部署设置资产过滤器 {#setting-up-asset-filters-for-video-only-deployments}

如果您正在将Dynamic Media用于仅视频，请按照以下步骤设置要复制的资产过滤器:

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点按工 **[!UICONTROL 具>部署>复制>创作代理。]**
1. 在作者页面上的代理中，点 **[!UICONTROL 按默认代理（发布）。]**
1. 点按 **[!UICONTROL 编辑。]**
1. 在“代 **[!UICONTROL 理设置]** ”对话框的“设 **[!UICONTROL 置]** ”选项卡中，选 **[!UICONTROL 中“启用]** ”以打开代理。
1. 点按 **[!UICONTROL 确定。]**
1. In AEM, tap **[!UICONTROL Tools > General > CRXDE Lite.]**
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. 找到 **[!UICONTROL filter-video]**，右键单击它并选择“复 **[!UICONTROL 制”。]**
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish`
1. 找到 **[!UICONTROL jcr:content]**，右键单击它并选择“粘 **[!UICONTROL 贴”。]**

这将设置AEM发布实例以传送视频海报图像以及回放所需的视频元数据，而视频本身则由Dynamic Media云服务传送。 过滤器还将从复制中排除原始视频和静态缩略图再现，这在发布实例中是不需要的。

### 在非生产部署中为映像设置资产过滤器 {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

如果您在非生产部署中使用映像Dynamic Media，请按照以下步骤设置要复制的资产过滤器:

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点按工 **[!UICONTROL 具>部署>复制>创作代理。]**
1. 在作者页面上的代理中，点 **[!UICONTROL 按默认代理（发布）。]**
1. 点按 **[!UICONTROL 编辑。]**
1. 在“代 **[!UICONTROL 理设置]** ”对话框的“设 **[!UICONTROL 置]** ”选项卡中，选 **[!UICONTROL 中“启用]** ”以打开代理。
1. 点按 **[!UICONTROL 确定。]**
1. In AEM, tap **[!UICONTROL Tools > General > CRXDE Lite.]**
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. 找 **[!UICONTROL 到滤镜图像]**，右键单击它并选择“复 **[!UICONTROL 制”。]**
1. 在左侧文件夹树中，导航到 `/etc/replication/agents.author/publish`
1. 找 **[!UICONTROL 到jcr:content]**，右键单击它并选择“创建” **[!UICONTROL >“创建节点”。]** 输入类 `damRenditionFilters` 型名 `nt:unstructured`称。
1. 找到 `damRenditionFilters`它，右键单击它并选择“粘 **[!UICONTROL 贴”。]**

这将设置AEM发布实例，以将图像传送到非生产环境。 过滤器还将从复制中排除原始图像和静态演绎版，这是发布实例不需要的。

>[!NOTE]
如果作者中有许多不同的过滤器，则每个代理都需要分配给它一个不同的用户。 花岗岩代码强制实施每用户一个过滤器模型。 对于设置的每个过滤器，始终有不同的用户。
如果您在服务器上使用多个过滤器——例如，一个用于复制的过滤器要发布，另一个用于s7投放的过滤器——则需要确保这两个过滤器在jcr:content节点中为它们分 **配了不同** 的userId **** 。 请参阅下图：

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 自定义用于复制的资产过滤器 {#customizing-asset-filters-for-replication}

（可选）要自定义资产过滤器以进行复制，请执行以下操作：

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点 **[!UICONTROL 按工具>常规> CRXDE Lite。]**
1. 在左侧文件夹树中，导 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` 航以查看过滤器。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 要定义筛选器的MIME类型，可以按如下方式查找Mime类型：

   在左边栏中，展 `content > dam > <locate_your_asset> >  jcr:content > metadata` 开，然后在表中找到 **[!UICONTROL dc:format。]**

   下图是资产到dc:format的路径示例。

   ![chlimage_1-512](assets/chlimage_1-512.png)

   请注意， `dc:format` 资产的 `Fiji Red.jpg` 属性 `image/jpeg`是

   要使此滤镜应用于所有图像（无论其格式如何），请将值设 `image/*` 置 `*` 为应用于任何格式的所有图像的常规表达式。

   要使滤镜仅应用于JPEG类型的图像，请输入值 `image/jpeg`。

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
   <td>通配符<br /> </td>
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

下图是资产演绎版的示例。

![chlimage_1-513](assets/chlimage_1-4.png)

使用上面的示例，如果您只想复制PTIFF（金字塔TIFF），则您应输入其 `+cqdam,*` 中包含开始的所有演绎版 `cqdam`。 在示例中，该再现为 `cqdam.pyramid.tiff`。

如果您只想复制原件，则输入 `+original`。

## 配置Dynamic Media图像服务器设置 {#configuring-dynamic-media-image-server-settings}

配置Dynamic Media图像服务器涉及编辑Adobe CQ Scene7 ImageServer捆绑和Adobe CQ Scene7 PlatformServer捆绑。

>[!NOTE]
Dynamic Media在启用后即 [可使用](#enabling-dynamic-media)。 但是，您可以选择通过配置Dynamic Media图像服务器来优化安装，以满足某些规范或要求。

**入门项目**: *在配* 置Dynamic Media映像服务器之前，请确保Windows虚拟机包括Microsoft Visual C++库的安装。 运行Dynamic Media图像服务器时必须使用这些库。 您可 [以在此处下载Microsoft Visual C++ 2010 Redistributable Package(x64)](https://www.microsoft.com/en-us/download/details.aspx?id=14632)。

要配置Dynamic Media图像服务器设置，请执行以下操作：

1. 在AEM的左上角，点按 **[!UICONTROL Adobe Experience Manager]** 以访问全局导航控制台，然后点 **[!UICONTROL 按工具>操作> Web Console。]**
1. 在“Adobe Experience ManagerWeb控制台配置”页上，点 **[!UICONTROL 按OSGi > Configuration]** ，以列表AEM中当前运行的所有捆绑包。

   Dynamic Media投放服务器位于列表中的以下名称下：

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 在捆绑包的列表中，点按Adobe CQ Scene7 ImageServer右侧的编辑图标。
1. 在Adobe CQ Scene7 ImageServer对话框中，设置以下配置值：

   >[!NOTE]
   在大多数情况下，无需更改默认值。 但是，如果确实更改了默认值，则必须重新启动捆绑，以使更改生效。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>默认值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>TcpPort.name</td>
   <td><code><em>empty</em></code></td>
   <td>用于与ImageServer进程通信的端口号。 默认情况下，会自动检测到空闲端口。</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>允许或禁止对ImageServer进程进行远程访问。 如果为false，则图像服务器仅监听localhost。</p> <p>指向本地主机的默认外部设定器设置需要指定特定VM实例的实际域或IP地址。 原因是localhost可能指向VM的父系统。</p> <p>VM的域或IP地址可能需要有主机文件条目，以便它能够解析自身。</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16兆帕</td>
   <td>渲染的最大大小（百万像素）。</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16 MB</td>
   <td>传递的最大消息大小(MB)。</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>超时值，指ImageServer等待JCR响应范围内的拼贴请求的时间（秒）。</td>
  </tr>
  <tr>
   <td>WorkerThreads</td>
   <td>10</td>
   <td>工作线程数。</td>
  </tr>
 </tbody>
</table>

1. Tap **[!UICONTROL Save.]**
1. 在捆绑包的列表中，点按Adobe CQ Scene7 PlatformServer右侧的编辑 **[!UICONTROL 图标]** 。
1. 在Adobe CQ Scene7 PlatformServer对话框中，设置以下默认值选项：

   >[!NOTE]
   Dynamic Media图像服务器使用其自己的磁盘缓存缓存响应。 AEM HTTP缓存和Dispacher不能用于缓存来自Dynamic Media图像服务器的响应。

   | **属性** | **默认值** | **描述** |
   |---|---|---|
   | 已启用缓存 | 已选中 | 是否启用响应缓存。 |
   | 缓存根 | 高速缓存 | 响应缓存文件夹的一个或多个路径。 相对路径针对内部s7imaging bundle文件夹进行解析。 |
   | 高速缓存最大大小 | 200000000 | 响应缓存的最大大小（字节）。 |
   | 缓存最大条目数 | 100000 | 缓存中允许的最大条目数。 |

### 默认清单设置 {#default-manifest-settings}

默认清单允许您配置用于生成Dynamic Media投放响应的默认值。 您可以微调质量（JPEG质量、分辨率、重新取样模式）、缓存（过期），并防止渲染过大的图像(defaultpix、defaultthumbpix、maxpix)。

默认清单配置的位置来自 **[!UICONTROL Adobe CQ]** Scene7 PlatformServer包 **[!UICONTROL 的目录根默认值]** 。 默认情况下，此值位于“工具”>“常规”>“CRXDE Lite” **[!UICONTROL 中的以下路径中]**:

`/conf/global/settings/dam/dm/imageserver/`

![configimageservercrxdelite](assets/configimageservercrxdelite.png)

您可以通过输入新值来更改属性的值，如下表中所述。

完成对默认清单的更改后，点按页面左上角的全 **[!UICONTROL 部保存。]**

请确保点按 **[!UICONTROL 访问控制]** 选项卡（“属性”选项卡右侧），然后为所有人和动态媒体 `jcr:read` 复制用户设置访问控制权限。

![configimageservercrxdeliteaccesscontroltab](assets/configimageservercrxdeliteaccesscontroltab.png)

清单设置表及其默认值：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>默认值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>bkgcolor</td>
   <td>FFFFFF</td>
   <td><p>默认背景颜色。 用于填充返回图像中不包含实际图像数据的任何区域的RGB值。</p> <p>另请参 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_bkgcolor.html">阅图像</a> 服务API中的BkgColor。</p> </td>
  </tr>
  <tr>
   <td>defaultpix</td>
   <td>300,300</td>
   <td><p>默认视图大小。 如果请求未使用wid=、hei=或scl=显式指定视图大小，则服务器将限制返回图像不大于此宽度和高度。</p> <p>指定为两个整数，0或更大，以逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值设置为0以保持它们不受约束。 不适用于嵌套／嵌入的请求。</p> <p>另请 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_defaultpix.html">参阅</a> Image Serving API中的DefaultPix。</p> <p>但是，您通常使用查看器预设或图像预设来传送资产。 Defaultpix仅适用于未使用查看器预设或图像预设的资产。</p> </td>
  </tr>
  <tr>
   <td>defaulthumbpix</td>
   <td>100,100</td>
   <td><p>默认缩略图大小。 用于缩略图请求(req=tmb)，而非属性：:DefaultPix。</p> <p>如果缩略图请求(req=tmb)未明确指定大小，则服务器将限制返回图像不大于此宽度和高度，而不使用wid=、hei=或scl=显式指定视图大小。</p> <p>指定为两个整数，0或更大，以逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值设置为0以保持它们不受约束。 </p> <p>不适用于嵌套／嵌入的请求。</p> <p>另请参 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_defaultthumbpix.html">阅图像</a> 服务API中的DefaultThumbPix。 </p> </td>
  </tr>
  <tr>
   <td>过期</td>
   <td>36000000</td>
   <td><p>默认客户端的存储时间。 提供默认的过期时间间隔，以防特定目录记录不包含有效的目录：:Expiration值。</p> <p>实数，0或更大。 自生成回复数据后，到期的毫秒数。 设置为0以始终立即使回复图像过期，这会有效地禁用客户端缓存。 默认情况下，此值设置为10小时，这意味着如果发布了新图像，则旧图像离开用户缓存需要10小时。 如果您需要更早清除缓存，请与客户关怀联系。</p> <p>另请参 <a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html">阅</a> “图像服务API”中的“过期”。</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>默认JPEG编码属性。 指定JPEG回复图像的默认属性。</p> <p>整数数和标记，以逗号分隔。 第一个值在1.100范围内，它定义质量。 对于正常行为，第二个值可为0，或者为1以禁用JPEG编码器通常采用的RGB色度缩减采样。</p> <p>另请参 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_jpegquality.html">阅</a> Image Serving API中的JpegQuality。</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>2000,2000</td>
   <td><p>回复图像大小限制。 返回给客户端的最大返回图像宽度和高度。</p> <p>如果请求导致返回图像的宽度或高度大于属性：:MaxPix，则服务器返回错误。</p> <p>另请 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_maxpix.html">参阅</a> “图像服务API”中的MaxPix。</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>默认重新取样模式。 指定用于缩放图像数据的默认重新取样属性和插值属性。</p> <p>在请求中未指定resMode=时使用。</p> <p>允许的值包括BILIN、BICUB或SHARP2。</p> <p>枚举。 对于bilin，设置为2；对于bicub，设置为3；对于sharp2插值模式，设置为4。 使用sharp2可获得最佳效果。</p> <p>另请参 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_is_cat_resmode.html">阅图</a> 像服务API中的ResMode。</p> </td>
  </tr>
  <tr>
   <td>分辨率</td>
   <td>72</td>
   <td><p>默认对象分辨率。 提供默认对象分辨率，以防特定目录记录不包含有效的目录：:Resolution值。</p> <p>实数，大于0。 通常以每英寸的像素数表示，但也可以以其他单位表示，如每米的像素数。</p> <p>另请参 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_resolution.html">阅图</a> 像服务API中的分辨率。</p> </td>
  </tr>
  <tr>
   <td>thumbnaitime</td>
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>这些值表示视频播放时间的快照，并传 <a href="https://encoding.com/">递给encoding.com</a>。 有关 <a href="/help/assets/video.md#aboutvideothumbnails">详细信息</a> ，请参阅“关于视频缩略图”。</td>
  </tr>
 </tbody>
</table>

## 配置Dynamic Media颜色管理 {#configuring-dynamic-media-color-management}

通过Dynamic Media颜色管理，您可以为预览对资产进行颜色校正。

借助颜色校正，摄取的资源在生成的金字塔TIFF再现中保留其色彩空间（RGB、CMYK、灰色）和嵌入的色彩用户档案。 当您请求动态再现时，图像颜色会校正到目标色彩空间中。 在JCR的Dynamic Media发布设置中配置输出颜色用户档案。

Adobe颜色管理使用ICC用户档案，这是国际颜色协会(ICC)定义的格式。

您可以配置Dynamic Media颜色管理，并使用CMYK、RGB或灰度输出配置图像预设。 See [Configuring Image Presets](/help/assets/managing-image-presets.md).

高级用例可使用手动配置修 `icc=` 饰符显式选择输出颜色用户档案:

* `icc` - [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` - [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
只有在安装了“包共享”中的功 [能包12445或“软件分发](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) ”中 [的功能包12445时，Adobe颜色用户档案](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) 标准集才可用。 所有功能包和服务包均可通过包 [共享和软件](https://www.adobeaemcloud.com/content/packageshare.html)[分发获得](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 功能包12445提供Adobe颜色用户档案。

### 安装功能包12445 {#installing-feature-pack}

您必须安装功能包12445才能使用动态媒体色彩管理功能。

**安装功能包12445**

1. 导航到“ [包共享](https://www.adobeaemcloud.com/content/packageshare.html) ”或“ [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) ”，然后下载 `cq-6.3.0-featurepack-12445`。

   有关 [在AEM中使用包共享](/help/sites-administering/package-manager.md) 和包的更多信息，请参阅如何使用包。

1. 安装功能包。

### 配置默认颜色用户档案 {#configuring-the-default-color-profiles}

安装功能包后，您需要配置适当的默认颜色用户档案，以在请求RGB或CMYK图像数据时启用颜色校正。

**配置默认颜色用户档案**

1. 在“ **[!UICONTROL 工具”>“常规”>]** CRXDE Lite `/conf/global/settings/dam/dm/imageserver/jcr:content` 中，导航到包含默认Adobe Color用户档案。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 通过滚动到“属性”选项卡的底部并手 **[!UICONTROL 动输入]** 属性名称、类型和值来添加颜色校正属性，这些内容在下表中有介绍。 输入值后，点按添 **[!UICONTROL 加]** ，然 **[!UICONTROL 后点按全]** 部保存，以保存值。

   颜色校正属性在颜色校 **正属性表中进行** 说明。 可指定给颜色校正属性的值在“颜色 **用户档案** ”表中。

   例如，在“名 **[!UICONTROL 称]**”中， `iccprofilecmyk`添加 **[!UICONTROL ，选择]** 类型 `String`，然 `WebCoated` 后添加 **[!UICONTROL 为值。]** 然后点按 **[!UICONTROL 添加]** ，然后 **[!UICONTROL 点按全]** 部保存，以保存您的值。

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
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">iccprofilergb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认RGB颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilemyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认CMYK颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认灰色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofireservercrgb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的RGB图像的默认RGB颜色用户档案的名称</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrcmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的CMYK图像的默认CMYK颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的CMYK图像的默认灰色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpoint补偿</a></td>
   <td>布尔型</td>
   <td>True</td>
   <td>指定是否应在颜色校正期间执行黑点补偿。 Adobe建议启用此选项。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">icdhiter</a></td>
   <td>布尔型</td>
   <td>False</td>
   <td>指定是否应在颜色校正期间进行仿色。</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderintent</a></td>
   <td>字符串</td>
   <td>相对</td>
   <td><p>指定渲染方法。 可接受的值为： <strong>感知、相对、饱和度、绝对。 </strong><i></i>Adobe建议 <strong>将 </strong><i></i>相对值作为默认值。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
属性名称区分大小写，并且必须全部为小写。

**颜色用户档案表**

安装了以下颜色用户档案:

<table>
 <tbody>
  <tr>
   <th><p>名称</p> </th>
   <th><p>色彩空间</p> </th>
   <th><p>描述</p> </th>
  </tr>
  <tr>
   <td>AdobeRGB</td>
   <td>RGB</td>
   <td>Adobe RGB(1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>Coated FOGRA27(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Coated FOGRA39(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>涂层GRACoL 2006(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>颜色匹配RGB</td>
  </tr>
  <tr>
   <td>EuropeISOCopated</td>
   <td>CMYK</td>
   <td>欧洲ISO涂层FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euroscale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>Euroscale Uncoated v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Coated</td>
  </tr>
  <tr>
   <td>JapanColorSpeaper</td>
   <td>CMYK</td>
   <td>Japan Color 2002报纸</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Uncoated</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated(Ad)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>美国新闻纸(SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC(1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4默认CMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>Photoshop 5默认CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>美国平板电脑涂层v2</td>
  </tr>
  <tr>
   <td>平板纸未涂层</td>
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
   <td>非涂层FOGRA29(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>U.S. Web Coated(SWOP)v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006 3级纸</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006五级纸</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGamyRGB</td>
   <td>RGB</td>
   <td>宽色域RGB</td>
  </tr>
 </tbody>
</table>

1. 点按 **[!UICONTROL 全部保存。]**

例如，可以将iccprofilergb设 **[!UICONTROL 置为]** ，将iccprofile `sRGB`cmyk设 **[!UICONTROL 置为WebCoated]****[!UICONTROL 。]**

这样做将执行以下操作：

* 启用RGB和CMYK图像的颜色校正。
* 将假定没有颜色用户档案的RGB图像在sRGB *颜色空* 间中。
* 将假定没有颜色用户档案的CMYK图像在WebCoated颜色 *空间中* 。
* 返回RGB输出的动态演绎版将在*sRGB *色彩空间中返回它。
* 返回CMYK输出的动态演绎版将在WebCoated颜色空 *间中* 返回它。

## 传送资产 {#delivering-assets}

完成上述所有任务后，会从图像或视频服务中提供已激活的Dynamic Media资产。 在AEM中，此功能显示在“复 **[!UICONTROL 制图像URL]**”、“ **[!UICONTROL 复制查看器URL]**”、“ **[!UICONTROL 嵌入查看器代码]**”和“WCM”中。

See [Delivering Dynamic Media Assets](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>当你……</strong></td>
   <td><strong>结果</strong></td>
  </tr>
  <tr>
   <td>复制图像URL</td>
   <td><p>“复制URL”对话框显示与以下内容类似的URL（URL仅供演示之用）:</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>其中 <code>IMAGESERVICEPUBLISHNODE</code> 指的是图像服务URL。</p> <p>See also <a href="/help/assets/delivering-dynamic-media-assets.md">Delivering Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>复制查看器URL</td>
   <td><p>“复制URL”对话框显示与以下内容类似的URL（URL仅供演示之用）:</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>其 <code>PUBLISHNODE</code> 中指常规AEM发布节点 <code>IMAGESERVICEPUBLISHNODE</code> 和图像服务URL。</p> <p>See also <a href="/help/assets/delivering-dynamic-media-assets.md">Delivering Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>复制查看器的嵌入代码</td>
   <td><p>“复制嵌入代码”对话框显示与以下内容类似的代码片断（代码范例仅用于演示目的）:</p> <p><code class="code">&lt;style type="text/css"&gt;
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
       &lt;/script&gt;</code></p> <p>其 <code>PUBLISHNODE</code> 中指常规AEM发布节点 <code>IMAGESERVICEPUBLISHNODE</code> 和图像服务URL。</p> <p>See also <a href="/help/assets/delivering-dynamic-media-assets.md">Delivering Dynamic Media Assets</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCMDynamic Media和交互式媒体组件 {#wcm-dynamic-media-and-interactive-media-components}

引用Dynamic Media和交互式媒体组件的WCM页面引用投放服务。
