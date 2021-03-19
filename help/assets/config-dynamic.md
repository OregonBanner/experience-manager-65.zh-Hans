---
title: 配置Dynamic Media — 混合模式
description: 了解如何配置Dynamic Media — 混合模式。
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: 业务从业者，管理员
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '7843'
ht-degree: 1%

---


# 配置Dynamic Media — 混合模式{#configuring-dynamic-media-hybrid-mode}

Dynamic Media-Hybrid必须启用并配置以供使用。 根据您的用例，Dynamic Media具有多个[支持的配置](#supported-dynamic-media-configurations)。

>[!NOTE]
>
>如果您打算在Scene7运行模式下配置和运行Dynamic Media，请参阅[配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。
>
>如果您打算在混合运行模式下配置和运行Dynamic Media，请按照本页中的说明操作。

了解有关在Dynamic Media中使用[video](/help/assets/video.md)的更多信息。

>[!NOTE]
>
>如果您使用为不同环境(如用于开发、升级和实时生产的Cloud Services)设置的Adobe Experience Manager，请为每个环境配置Dynamic Media。

>[!NOTE]
>
>如果您对Dynamic Media配置有任何问题，请查看特定于Dynamic Media的日志文件。 启用Dynamic Media时，会自动安装这些文件：
>
>* `s7access.log`
>* `ImageServing.log`

>
>
[监视和维护您的Experience Manager实例](/help/sites-deploying/monitoring-and-maintaining.md)中有相关说明。

混合出版和投放是Adobe Experience Manager之外的Dynamic Media的一个核心功能。 混合发布允许您从云而不是从Dynamic Media发布节点提供Experience Manager资产，如图像、集和视频。

其他内容(如Dynamic Media查看器、站点页面和静态内容)继续从Experience Manager发布节点提供。

如果您是Dynamic Media的客户，则需要使用混合投放作为所有Dynamic Media内容的投放机制。

## 视频{#hybrid-publishing-architecture-for-videos}的混合发布架构

![chlimage_1-506](assets/chlimage_1-428.png)

## 图像{#hybrid-publishing-architecture-for-images}的混合发布架构

![chlimage_1-507](assets/chlimage_1-507.png)

## 支持的Dynamic Media配置{#supported-dynamic-media-configurations}

后面的配置任务引用了以下术语：

| **术语** | **Dynamic Media已启用** | **描述** |
|---|---|---|
| Experience Manager作者节点 | 绿色圆形中的白色复选标记 | 您部署到内部部署或通过Managed Services部署的作者节点。 |
| Experience Manager发布节点 | 红方的白色X。 | 您部署到内部部署或通过Managed Services部署的发布节点。 |
| 图像服务发布节点 | 绿色圆形中的白色复选标记。 | 您在由Adobe管理的数据中心上运行的发布节点。 引用图像服务URL。 |

您可以选择仅为成像、视频或成像和视频实施Dynamic Media。 要确定为特定方案配置Dynamic Media的步骤，请参阅下表。

<table>
 <tbody>
  <tr>
   <td><strong>方案</strong></td>
   <td ><strong>工作原理</strong></td>
   <td><strong>配置步骤</strong></td>
  </tr>
  <tr>
   <td>在制作中仅提供图像</td>
   <td>图像通过Adobe全球数据中心中的服务器交付，然后由CDN缓存，以实现可扩展的性能和全球范围。</td>
   <td>
    <ol>
     <li>在Experience Manager<strong>author</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>。</li>
     <li>在<a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services</a>中配置映像。</li>
     <li><a href="#configuring-image-replication">配置映像复制</a>。</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产过滤器进行复制</a>。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media Image Server设置</a>。</li>
     <li><a href="#delivering-assets">交付资产</a>。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>在预制作（开发、QE、舞台等）中仅提供图像。</td>
   <td>图像通过Experience Manager发布节点传送。 在此方案中，由于流量很小，因此无需将图像传送到Adobe的数据中心。 它还允许在生产启动前安全预览内容。</td>
   <td>
    <ol>
     <li>在Experience Manager<strong>author</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>。</li>
     <li>在Experience Manager<strong>publish</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li>为非生产图像设置<a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">资产过滤器</a>。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media Image Server设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在任何环境（制作、开发、QE、舞台等）中只提供视频</td>
   <td>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 视频海报图像（播放开始前显示的视频缩略图）由Experience Manager发布实例提供。</td>
   <td>
    <ol>
     <li>在Experience Manager<strong>author</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>。</li>
     <li>在Experience Manager<strong>publish</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>（发布实例提供视频海报图像并提供视频回放的元数据）。</li>
     <li>在<a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services中配置视频。</a></li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li>为仅视频</a>设置<a href="#setting-up-asset-filters-for-video-only-deployments">资产过滤器。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>在制作中提供图像和视频</td>
   <td><p>视频由CDN交付和缓存，以实现可扩展的性能和全球范围。 图像和视频海报图像通过Adobe全球数据中心中的服务器交付，然后由CDN缓存，以实现可扩展的性能和全球范围。</p> <p>请参阅前几节，在预制作中设置图像或视频。 </p> </td>
   <td>
    <ol>
     <li>在Experience Manager<strong>author</strong>节点上，<a href="#enabling-dynamic-media">启用Dynamic Media</a>。</li>
     <li>在<a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services中配置视频。</a></li>
     <li>在<a href="#configuring-dynamic-media-cloud-services">Dynamic MediaCloud Services中配置映像。</a></li>
     <li><a href="#configuring-image-replication">配置映像复制</a>。</li>
     <li><a href="#replicating-catalog-settings">复制目录设置</a>。</li>
     <li><a href="#replicating-viewer-presets">复制查看器预设</a>。</li>
     <li><a href="#using-default-asset-filters-for-replication">使用默认资产过滤器进行复制。</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">配置Dynamic Media Image Server设置。</a></li>
     <li><a href="#delivering-assets">交付资产。</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## 启用Dynamic Media {#enabling-dynamic-media}

[默认情况下，Dynamic Media 处于禁用状态。](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)要利用Dynamic Media功能，必须像使用`dynamicmedia`运行模式一样使用`publish`运行模式来启用Dynamic Media。 在启用之前，请确保查看[技术要求。](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on)

>[!NOTE]
>
>通过运行模式启用Dynamic Media将替换Experience Manager 6.1和Experience Manager 6.0中的功能，在这两个版本中，您通过将`dynamicMediaEnabled`标志设置为&#x200B;**[!UICONTROL true来启用Dynamic Media。]** 此标志在Experience Manager 6.2和更高版本中没有功能。此外，您无需重新启动快速启动即可启用Dynamic Media。

通过启用Dynamic Media,Dynamic Media功能可在用户界面中使用，并且每个上传的图像资产都会收到一个&#x200B;*cqdam.pyramid.tiff*&#x200B;再现，用于快速投放动态图像演绎版。 这些PTIFF具有以下显着优势：

* 只能管理单个主源图像并动态生成无限演绎版，而无需任何其他存储。
* 能够使用交互式可视化，如缩放、平移和旋转。

如果要在Experience Manager中使用Dynamic Media Classic，请不要启用Dynamic Media，除非您使用的是[特定方案](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)。 除非您通过运行模式启用Dynamic Media，否则Dynamic Media将被禁用。

要启用Dynamic Media，必须从命令行或快速启动文件名中启用Dynamic Media运行模式。

**启用Dynamic Media**

1. 在命令行上，启动快速启动时，请执行以下操作：

   * 在启动jar文件时，将`-r dynamicmedia`添加到命令行末尾。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   如果要发布到s7投放，则还必须包含以下trustStore参数：

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. 请求`https://localhost:4502/is/image`，并确保图像服务器现在正在运行。

   >[!NOTE]
   >
   >要解决Dynamic Media的问题，请参阅`crx-quickstart/logs/`目录中的以下日志：
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer日志提供用于分析内部ImageServer进程行为的统计信息和分析信息。

   图像服务器日志文件名示例：`ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access日志记录通过`/is/image`和`/is/content`向Dynamic Media发出的每个请求。

   这些日志仅在启用Dynamic Media时使用。 它们不包含在从`system/console/status-Bundlelist`页面生成的&#x200B;**下载完整**&#x200B;包中；如果您遇到Dynamic Media问题，在致电客户支持时，将这两个日志附加到该问题。

### 如果将Experience Manager安装到其他端口或上下文路径…… {#if-you-installed-aem-to-a-different-port-or-context-path}

如果要将[Experience Manager部署到应用程序服务器](/help/sites-deploying/application-server-install.md)并启用了Dynamic Media，则必须在外部化器中配置&#x200B;**self**&#x200B;域。 否则，资产的缩略图生成无法正常用于Dynamic Media资产。

此外，如果在其他端口或上下文路径上运行快速启动，则还必须更改&#x200B;**self**&#x200B;域。

启用Dynamic Media后，将使用Dynamic Media生成图像资产的静态缩略图演绎版。 要使缩览图生成正常工作，Experience Manager必须对自身执行URL请求，并且必须同时知道端口号和上下文路径。

Experience Manager:

* [externalizer](/help/sites-developing/externalizer.md)中的&#x200B;**self**&#x200B;域用于检索端口号和上下文路径。
* 如果未配置&#x200B;**self**&#x200B;域，则从Jetty HTTP服务检索端口号和上下文路径。

在Experience Manager QuickStart WAR部署中，无法派生端口号和上下文路径，因此必须配置&#x200B;**self**&#x200B;域。 有关如何配置&#x200B;**self**&#x200B;域，请参见[externalizer documentation](/help/sites-developing/externalizer.md)。

>[!NOTE]
在[Experience Manager快速启动独立部署](/help/sites-deploying/deploy.md)中，通常不需要配置&#x200B;**自**&#x200B;域，因为可以自动配置端口号和上下文路径。 但是，如果所有网络接口都关闭，则必须配置&#x200B;**self**&#x200B;域。

## 禁用Dynamic Media {#disabling-dynamic-media}

Dynamic Media在默认情况下未启用。 但是，如果您以前启用了Dynamic Media，则可以稍后将其关闭。

要在启用Dynamic Media后禁用它，请删除`-r dynamicmedia`运行模式标志。

**在启用Dynamic Media后禁用它**

1. 在命令行上，启动快速启动时，可以执行以下任一操作：

   * 启动jar文件时，不要向命令行添加`-r dynamicmedia`。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. 请求`https://localhost:4502/is/image`。 您会收到一条消息，指示Dynamic Media已禁用。

   >[!NOTE]
   禁用Dynamic Media运行模式后，将自动跳过生成`cqdam.pyramid.tiff`再现的工作流步骤。 它还会禁用动态再现支持和其他Dynamic Media功能。
   另请注意，在配置Dynamic Media服务器后，当禁用了Experience Manager运行模式时，在此运行模式下上传的所有资产现在都无效。

## （可选）将Dynamic Media预设和配置从6.3迁移到6.5零停机时间{#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

如果要将Experience Manager Dynamic Media从6.3升级到6.5（现在包括零停机时间部署功能），则必须运行以下curl命令。 该命令将您的所有预设和配置从`/etc`迁移到`/conf`的CRXDE Lite中。

>[!NOTE]
如果您在兼容模式下运行Experience Manager实例（即安装了兼容包），则无需运行这些命令。

对于所有具有或没有兼容性包的升级，您都可以通过运行以下Linux® curl命令复制Dynamic Media最初附带的默认现成查看器预设：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

要将您从`/etc`创建的任何自定义查看器预设和配置迁移到`/conf`，请运行以下Linux® curl命令：

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 配置图像复制 {#configuring-image-replication}

Dynamic Media图像投放的工作方式是：从Experience Manager作者中发布图像资产（包括视频缩略图），并将其复制到Adobe的点播复制服务（复制服务URL）。 资产随后会通过按需图像投放服务（图像服务URL）交付。

执行以下操作：

1. [设置身份验证](#setting-up-authentication)。
1. [配置复制代理](#configuring-the-replication-agent)。

Dynamic Media Agent将发布Replication Agent资产，如图像、视频元数据，并将这些资产集合到托管Adobe的Image Service。 默认情况下，未启用复制代理。

配置复制代理后，必须[验证并测试是否已成功设置](#validating-the-replication-agent-for-dynamic-media)。 本节介绍这些过程。

>[!NOTE]
创建PTIFF的默认内存限制在所有工作流中为3 GB。 例如，您可以处理一个需要3 GB内存的映像，而其他工作流则暂停，或者可以并行处理10个映像，每个映像需要300 MB内存。
存储器限制是可配置的，并且适合系统资源可用性和正在处理的图像内容的类型。 如果您拥有许多大型资源并且系统上有足够的内存，您可以增加此限制以确保并行处理图像。
要求超过最大内存限制的图像将被拒绝。
要更改创建PTIFF的内存限制，请导航到&#x200B;**[!UICONTROL “工具”>“操作”>“Web控制台”>“Adobe CQ Scene7 PTiffManager]**”并更改&#x200B;**[!UICONTROL maxMemory]**&#x200B;值。

### 设置身份验证{#setting-up-authentication}

在创作时设置复制身份验证，以便将映像复制到Dynamic Media映像投放服务。 您首先获得一个KeyStore，然后将其保存在&#x200B;**[!UICONTROL dynamic-media-replication]**&#x200B;用户下并进行配置。 在设置过程中，您的公司管理员收到了一封包含KeyStore文件和必需凭据的欢迎电子邮件。 如果您未收到此信息，请与Adobe客户关怀联系。

**设置身份验证**

1. 如果您尚未拥有KeyStore文件和密码，请与Adobe客户服务部联系。 此信息是设置的必要部分。 它会关联到您帐户的密钥。
1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>安全>用户。]**
1. 在“用户管理”页面上，导航到&#x200B;**[!UICONTROL dynamic-media-replication]**&#x200B;用户，然后点按打开。

   ![dm复制](assets/dm-replication.png)

1. 在“Edit User Settings For dynamic-media-replication”（编辑用户设置）页中，点按&#x200B;**[!UICONTROL Keystore]**&#x200B;选项卡，然后单击&#x200B;**[!UICONTROL Create KeyStore。]**

   ![dm复制密钥库](assets/dm-replication-keystore.png)

1. 在&#x200B;**[!UICONTROL 设置KeyStore访问密码]**&#x200B;对话框中输入密码并确认密码。

   >[!NOTE]
   记住密码，因为以后配置复制代理时必须再次输入密码。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. 在&#x200B;**[!UICONTROL 编辑User Settings For dynamic-media-replication]**&#x200B;页面上，展开&#x200B;**从KeyStore文件**&#x200B;添加私钥区域并添加以下内容（请参阅下面的图像）：

   * 在&#x200B;**[!UICONTROL 新建别名]**&#x200B;字段中，输入要在复制配置中稍后使用的别名的名称。 例如，您可以使用`replication`作为别名。
   * 点按&#x200B;**[!UICONTROL KeyStore文件。]** 导航到Adobe提供给您的KeyStore文件，选择它，然后点按打 **[!UICONTROL 开。]**
   * 在&#x200B;**[!UICONTROL KeyStore File Password]**&#x200B;字段中，输入KeyStore File密码。 此密码是您在步骤5中创建的KeyStore密码，**不**，但是是KeyStore文件密码Adobe在设置过程中发送给您的欢迎电子邮件中提供的。 如果您未收到KeyStore文件密码，请与Adobe客户服务部门联系。
   * 在&#x200B;**[!UICONTROL 私钥密码]**&#x200B;字段中，输入私钥密码（可以是上一步中提供的相同私钥密码）。 Adobe在设置过程中向您发送的欢迎电子邮件中提供私钥密码。 如果您未收到私钥密码，请与Adobe客户关怀联系。
   * 在&#x200B;**[!UICONTROL 私钥别名]**&#x200B;字段中，输入私钥别名。 例如，`*companyname*-alias`。 Adobe在设置过程中向您发送的欢迎电子邮件中提供私钥别名。 如果您未收到私钥别名，请与Adobe客户关怀联系。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 点按&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以将更改保存到此用户。

   接下来，您必须[配置复制代理。](#configuring-the-replication-agent)

### 配置复制代理 {#configuring-the-replication-agent}

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>部署>复制>作者代理。]**
1. 在创作页面上的代理中，点按&#x200B;**[!UICONTROL Dynamic Media混合映像复制(s7投放)。]**
1. 点按&#x200B;**[!UICONTROL 编辑。]**
1. 点按&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡，然后输入以下内容：

   * **[!UICONTROL 已启用]**  — 选中此复选框可启用复制代理。
   * **[!UICONTROL 区域]**  — 设置为相应区域：北美、欧洲或亚洲
   * **[!UICONTROL 租户ID]**  — 此值是发布到复制服务的公司/租户的名称。此值是Adobe在设置过程中在向您发送的欢迎电子邮件中提供的租户ID。 如果您未收到此信息，请与Adobe客户关怀联系。
   * **[!UICONTROL 密钥存储别名]**  — 此值与在设置身份验证中生成密钥时设置的**新别名**值 [相同](#setting-up-authentication);例如，  `replication`（请参阅[设置身份验证](#setting-up-authentication)中的步骤7。）
   * **[!UICONTROL Key Store Password]**  — 点按创建KeyStore时创建的 **[!UICONTROL KeyStore密码。]** Adobe不提供此密码。请参阅[设置身份验证](#setting-up-authentication)的步骤5。

   下图显示了包含示例数据的复制代理：

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 点按&#x200B;**[!UICONTROL 确定。]**

### 验证Dynamic Media {#validating-the-replication-agent-for-dynamic-media}的复制代理

要验证Dynamic Media的复制代理，请执行以下操作：

点按&#x200B;**[!UICONTROL 测试连接。]** 输出示例如下：

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
您还可以通过执行下列操作之一进行检查：
* 检查复制日志，以确保已复制资产。
* 发布图像。 点按图像，在下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**，然后选择查看器预设。 单击&#x200B;**[!UICONTROL URL]**。 要验证是否可以看到图像，请在浏览器中复制并粘贴URL路径。



### 身份验证疑难解答 {#troubleshooting-authentication}

在设置身份验证时，您可能会遇到以下一些问题，这些问题与他们的解决方案一起。 在检查这些问题之前，请确保已设置复制。

#### 问题：包含消息的HTTP状态代码401 — 需要授权{#problem-http-status-code-with-message-authorization-required}

此问题可能是由于`dynamic-media-replication`用户未能设置KeyStore而引起的。

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

**解决方案**:检查是 `KeyStore` 否将保存 **到Dynamic-** Media-Replicationuser并提供了正确的密码。

#### 问题：无法解密密钥 — 无法解密数据{#problem-could-not-decrypt-key-could-not-decrypt-data}

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

**解决方案**:检查密码。在复制代理中保存的密码与用于创建密钥库的密码不同。

#### 问题：InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

此问题是由Experience Manager作者实例中的配置错误引起的。 作者上的Java™进程未获得正确的`javax.net.ssl.trustStore`。 在复制日志中可以看到以下错误：

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

**解决方案**:确保Experience Manager作者上的Java™进程将系统属性设 `-Djavax.net.ssl.trustStore=` 置为有效的truststore。

#### 问题：KeyStore未设置或未初始化{#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

此问题可能由热修复或覆盖Dynamic-Media用户或Keystore节点的功能包引起。

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
1. 在“用户管理”页面上，导航到`dynamic-media-replication`用户，然后点按以打开。
1. 单击&#x200B;**[!UICONTROL KeyStore]**&#x200B;选项卡。 如果出现&#x200B;**[!UICONTROL 创建KeyStore]**&#x200B;按钮，则必须重做之前[设置身份验证](#setting-up-authentication)下的步骤。
1. 如果必须重做KeyStore设置，则还必须重新执行[配置复制代理](/help/assets/config-dynamic.md#configuring-the-replication-agent)。

   重新配置s7投放复制代理。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 点按&#x200B;**[!UICONTROL 测试连接]**&#x200B;以验证配置是否有效。

#### 问题：Publish Agent使用SSL而不是OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

此问题可能由热修复或未正确安装或覆盖设置的功能包引起。

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

1. 在Experience Manager中，单击&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite。]**

   `localhost:4502/crx/de/index.jsp`

1. 导航到s7投放 Replication Agent节点。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 将此设置添加到复制代理（值设置为&#x200B;**[!UICONTROL True]**&#x200B;的布尔值）：

   `enableOauth=true`

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 全部保存。]**

### 正在测试配置{#testing-your-configuration}

Adobe建议您对配置执行端到端测试。

在开始此测试之前，请确保您已经执行了以下操作：

* 添加的图像预设。
* 在Cloud Services下配置&#x200B;**[!UICONTROL Dynamic Media配置（6.3之前）]**。 此测试需要图像服务URL

**测试配置**

1. 上传图像资产。 （在资产中，点按&#x200B;**[!UICONTROL 创建>文件]**&#x200B;并选择文件。）
1. 等待工作流完成。
1. 发布图像资产。 （选择资产，然后点按&#x200B;**[!UICONTROL 快速发布。]**）
1. 打开图像并点按&#x200B;**[!UICONTROL 演绎版，导航到该图像的演绎版。]**

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 选择任意动态演绎版。
1. 要获取此资产的URL，请单击&#x200B;**[!UICONTROL URL]**。
1. 导航到选定的URL并检查图像的行为是否按预期方式显示。

测试已交付资产的另一种方法是将req=exists附加到您的URL。

## 配置Dynamic MediaCloud Services{#configuring-dynamic-media-cloud-services}

Dynamic MediaCloud Service支持混合发布和投放图像和视频、视频分析和视频编码等。

在配置中，必须输入注册ID、视频服务URL、图像服务URL、复制服务URL和设置身份验证。 此信息已通过电子邮件发送给您，这是帐户设置过程的一部分。 如果您未收到此信息，请与Adobe Experience Manager管理员或Adobe客户服务部门联系以获取该信息。

>[!NOTE]
在设置Dynamic MediaCloud Services之前，请确保已设置发布实例。 配置Dynamic MediaCloud Services之前，还必须设置复制。

配置Dynamic MediaCloud Services:

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>Cloud Services> Dynamic Media配置(Pre-6.3)。]**
1. 在“Dynamic Media配置浏览器”页面的左窗格中，选择&#x200B;**[!UICONTROL global]**，然后点按&#x200B;**[!UICONTROL 创建。]**
1. 在&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;对话框的标题字段中，键入标题。
1. 如果要配置Dynamic Media的视频，

   * 在&#x200B;**[!UICONTROL 注册ID]**&#x200B;字段中，键入注册ID。
   * 在&#x200B;**[!UICONTROL 视频服务URL]**&#x200B;字段中，输入Dynamic Media网关的视频服务URL。

1. 如果要配置Dynamic Media以进行映像，请在&#x200B;**[!UICONTROL 图像服务URL]**&#x200B;字段中输入Dynamic Media网关的图像服务URL。
1. 点按&#x200B;**[!UICONTROL 保存]**&#x200B;以返回Dynamic Media配置浏览器页。
1. 要访问全局导航控制台，请点按Experience Manager徽标。

## 配置视频报告{#configuring-video-reporting}

您可以使用Dynamic Media Hybrid在多个Experience Manager安装中配置视频报告。

**何时使用：** 在配置Dynamic Media配置（6.3之前版本）时，开始提供包括视频报告在内的许多功能。该配置在区域Analytics公司中创建报表包。 如果配置多个“作者”节点，则为每个节点分别创建一个单独的报表包。 因此，报告数据在安装之间不一致。 此外，如果每个作者节点引用同一混合发布服务器，则上次作者安装会更改所有视频报告的目标报表包。 此问题使Analytics系统的报表包过多。

**开始：通过** 完成以下三个任务配置视频报告。

1. 在第一个“作者”节点上配置Dynamic Media配置（6.3之前版本）后，创建一个Video Analytics预设包。 此初始任务很重要，因为它允许新配置继续使用同一报表包。
1. 将Video Analytics预设包安装到配置Dynamic Media配置（6.3之前）之前的任何&#x200B;***新***&#x200B;作者节点&#x200B;***。***
1. 验证并调试包安装。

### 在配置第一个作者节点{#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}后创建视频分析预设包

完成此任务后，您将有一个包文件，其中包含“视频分析”预设。 这些预设包含报表包、跟踪服务器、跟踪命名空间和Marketing Cloud组织ID（如果可用）。

1. 如果尚未配置Dynamic Media配置（6.3之前版本），请配置。
1. （可选）视图并复制报表包ID（您必须有权访问JCR）。 虽然不需要使用报表包ID，但它使验证更加容易。
1. 使用包管理器创建包。
1. 编辑包以包含过滤器。

   Experience Manager:`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 构建包。
1. 下载或共享视频分析预设包，以便能够与后续的新作者节点共享。

### 在配置更多作者节点{#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}之前，请安装视频分析预设包

请确保在配置Dynamic Media配置（6.3之前）***之前完成此任务***。 否则，将创建另一个未使用的报表包。 此外，即使视频报告继续正确工作，数据收集也未得到优化。

确保可从第一个作者节点访问视频分析预设包（位于新的作者节点上）。

1. 将您之前创建的视频分析预设包上传到包管理器。
1. 安装Video Analytics预设包。
1. 配置Dynamic Media配置（6.3之前版本）。

### 验证和调试包安装{#verifying-and-debugging-the-package-installation}

1. 执行下列任一操作以验证并调试包安装（如有必要）：

   * **通过JCRT检查“视频分析”预设，**
通过JCR检查“视频分析”预设，您必须有权访问CRXDE Lite。

      Experience Manager — 在CRXDE Lite中，导航到`/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`

      如`https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`中所示

      如果您无权访问“作者”节点上的CRXDE Lite，则可以通过发布服务器检查预设。

   * **通过图像服务器检查视频分析预设**

      您可以通过发出图像服务器req=userdata请求直接验证视频分析预设。
例如，要在“作者”节点上查看Analytics预设，您可以发出以下请求：

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      要验证发布服务器上的预设，您可以向发布服务器发出类似的直接请求。 “作者”和“发布”节点上的响应相同。 响应如下所示：

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **通过Experience Manager中的视频报告工具检查视频分析预设**
点按 **[!UICONTROL 工具>资产>视频报告]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      如果您看到以下错误消息，则报表包可用，但未填充。 在系统收集任何数据之前，在新安装中出现此错误是正确的，也是需要的。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   要生成报告数据，请上传并发布一个视频。 使用&#x200B;**[!UICONTROL 复制URL]**&#x200B;并至少运行一次视频。

   从Video Viewer的使用情况中填充报告数据可能需要12小时。

   如果出现错误且报表包设置不正确，将显示以下警报。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   如果在配置Dynamic Media配置（6.3以前版本）服务之前运行了视频报告，则还会显示此错误。

### 视频报告配置{#troubleshooting-the-video-reporting-configuration}疑难解答

* 在安装过程中，有时与Analytics API服务器的连接会超时。 安装重试连接20次，但仍然失败。 出现这种情况时，日志文件会记录多个错误。 搜索 `SiteCatalystReportService`.
* 不首先安装Analytics Preset包会导致创建新报表包。
* 从Experience Manager 6.3升级到Experience Manager 6.4或Experience Manager 6.4.1，然后配置Dynamic Media配置（6.3之前版本），仍会创建报表包。 此问题已知并将针对Experience Manager 6.4.2进行修复。

### 关于视频分析预设{#about-the-video-analytics-preset}

“视频分析”预设（有时也称为分析预设）存储在Dynamic Media中的查看器预设旁边。 它基本上与查看器预设相同，但包含用于配置AppMeasurement和视频心率报告的信息。

预设的属性如下所示：

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (旧版Experience Manager中不存在)

Experience Manager 6.4和更高版本将此预设保存在`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## 正在复制目录设置{#replicating-catalog-settings}

通过JCR发布您自己的默认目录设置，作为设置过程的一部分。 要复制目录设置：

1. 在“终端”窗口中，运行以下命令：

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. 在Experience Manager中，导航到CRXDE Lite中的以下位置（需要管理员权限）：

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 点按&#x200B;**[!UICONTROL 复制]**&#x200B;选项卡。
1. 点按&#x200B;**[!UICONTROL 复制。]**

## 复制查看器预设{#replicating-viewer-presets}

要传送带有查看器预设的&#x200B;*资产，您必须复制/发布*&#x200B;查看器预设。 (必须激活&#x200B;*和*所有查看器预设，才能获取资产的URL或嵌入代码。
有关详细信息，请参阅[发布查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

>[!NOTE]
默认情况下，当您选择&#x200B;**[!UICONTROL 演绎版]**&#x200B;时，系统会显示各种演绎版；当您在资产的详细信息视图中选择&#x200B;**[!UICONTROL 查看器]**&#x200B;时，系统会显示各种查看器预设。 您可以增加或减少所看到的数量。 请参阅[增加显示](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)或[的图像预设数量增加显示](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)的查看器预设数量。

## 筛选复制{#filtering-assets-for-replication}的资产

在非Dynamic Media部署中，您将&#x200B;*所有*&#x200B;资产（图像和视频）从Experience Manager作者环境复制到Experience Manager发布节点。 此工作流是必需的，因为Experience Manager发布服务器也会传送资产。

但是，在Dynamic Media部署中，由于资产是通过云传送的，因此无需将这些相同的资产复制到Experience Manager发布节点。 这种“混合发布”工作流可避免复制资源时需要额外的存储成本和更长的处理时间。 其他内容(如Dynamic Media查看器、站点页面和静态内容)继续从Experience Manager发布节点提供。

除复制资产外，还复制以下非资产：

* Dynamic Media投放配置：`/conf/global/settings/dam/dm/imageserver/jcr:content`
* 图像预设: `/conf/global/settings/dam/dm/presets/macros`
* 查看器预设: `/conf/global/settings/dam/dm/presets/viewer`

这些过滤器为您提供了一种方法，使您能够排除&#x200B;*资产，使其无法复制到Experience Manager发布节点。*

### 使用默认资产过滤器进行复制{#using-default-asset-filters-for-replication}

如果您在生产&#x200B;**或**(2)成像和视频中使用Dynamic Media用于(1)成像，则可以使用Adobe按原样提供的默认过滤器。 默认情况下，以下过滤器处于活动状态：

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
   <td><p>具有<strong>image/</strong>的开始</p> <p>包含<strong>application/</strong>，以<strong>set</strong>结尾。</p> </td>
   <td>现成的“滤镜图像”（适用于单个图像资产，包括交互式图像）和“滤镜集”（适用于旋转集、图像集、混合媒体集和旋转集）将：
    <ul>
     <li>包括PTIFF图像和用于复制的元数据（任何以<strong>cqdam</strong>开头的再现）。</li>
     <li>从复制原始图像和静态图像演绎版中排除。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media视频投放</td>
   <td>filter-video</td>
   <td>开始具有<strong>video/</strong></td>
   <td>现成的“filter-video”将：
    <ul>
     <li>包含用于复制的代理视频演绎版、视频缩略图/海报图像、元数据（在父视频演绎版和视频演绎版中都有）（任何以<strong>cqdam</strong>开头的演绎版）。</li>
     <li>从复制原始视频和静态缩略图再现中排除。<br /> <br /> <strong>注意：</strong> 代理视频演绎版不包含二进制文件，而只是节点属性。因此，不会影响发布者存储库大小。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic(Scene7)集成</td>
   <td><p>滤镜图像</p> <p>过滤器集</p> <p>filter-video</p> </td>
   <td><p>具有<strong>image/</strong>的开始</p> <p>包含<strong>application/</strong>，以<strong>set</strong>结尾。</p> <p>开始具有<strong>video/</strong></p> </td>
   <td><p>您配置传输URI以指向您的Experience Manager发布服务器，而不是Adobe Dynamic Media云复制服务URL。 通过设置此过滤器，Dynamic Media Classic可以传送资产，而不是传送Experience Manager发布实例。</p> <p>现成的“filter-images”、“filter-sets”和“filter-video”将：</p>
    <ul>
     <li>包括PTIFF图像、代理视频演绎版和用于复制的元数据。 但是，由于JCR中不存在这些应用程序，因此对于运行Experience Manager的用户 — Dynamic Media Classic集成，IT无效。</li>
     <li>从复制中排除原始图像、静态图像演绎版、原始视频和静态缩略图演绎版。 相反，Dynamic Media Classic提供图像和视频资产。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
过滤器应用于MIME类型，不能特定于路径。

### 为仅视频部署设置资产过滤器{#setting-up-asset-filters-for-video-only-deployments}

如果您使用Dynamic Media仅用于视频，请按照以下步骤设置要复制的资产过滤器:

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>部署>复制>作者代理。]**
1. 在创作页面上的代理中，点按&#x200B;**[!UICONTROL 默认代理（发布）。]**
1. 点按&#x200B;**[!UICONTROL 编辑。]**
1. 在&#x200B;**[!UICONTROL 代理设置]**&#x200B;对话框的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，选中&#x200B;**[!UICONTROL 已启用]**&#x200B;以打开代理。
1. 点按&#x200B;**[!UICONTROL 确定。]**
1. 在Experience Manager中，点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite。]**
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. 找到&#x200B;**[!UICONTROL filter-video]**，右键单击它并选择&#x200B;**[!UICONTROL 复制。]**
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/publish`
1. 找到&#x200B;**[!UICONTROL jcr:content]**，右键单击它并选择&#x200B;**[!UICONTROL 粘贴。]**

这些步骤设置Experience Manager发布实例，以传送播放所需的视频海报图像和视频元数据，而视频本身则由Dynamic MediaCloud Service传送。 过滤器还会从复制中排除发布实例中不需要的原始视频和静态缩略图再现。

### 设置用于非生产部署中映像的资产过滤器{#setting-up-asset-filters-for-imaging-in-non-production-deployments}

如果您在非生产部署中使用Dynamic Media进行映像，请按照以下步骤设置要复制的资产过滤器:

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>部署>复制>作者代理。]**
1. 在创作页面上的代理中，点按&#x200B;**[!UICONTROL 默认代理（发布）。]**
1. 点按&#x200B;**[!UICONTROL 编辑。]**
1. 在&#x200B;**[!UICONTROL 代理设置]**&#x200B;对话框的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，选中&#x200B;**[!UICONTROL 已启用]**&#x200B;以打开代理。
1. 点按&#x200B;**[!UICONTROL 确定。]**
1. 在Experience Manager中，点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite。]**
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. 找到&#x200B;**[!UICONTROL filter-images]**，右键单击它并选择&#x200B;**[!UICONTROL 复制。]**
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/publish`
1. 找到&#x200B;**[!UICONTROL jcr:content]**，右键单击它并选择&#x200B;**[!UICONTROL 创建>创建节点。]** 输入类 `damRenditionFilters` 型名 `nt:unstructured`称。
1. 找到`damRenditionFilters`，右键单击它并选择&#x200B;**[!UICONTROL 粘贴。]**

这些步骤设置Experience Manager发布实例，以将图像传送到非生产环境。 过滤器还会从复制中排除原始映像和静态演绎版，这在发布实例中是不需要的。

>[!NOTE]
如果作者中有许多不同的过滤器，则每个代理需要为其分配一个不同的用户。 花岗岩代码强制采用每用户一个滤镜模型。 对于每个过滤器设置，始终有不同的用户。
您是否在服务器上使用多个过滤器？ 例如，一个用于要发布的复制的过滤器，另一个用于s7投放的过滤器。 如果是，则必须确保在&#x200B;**jcr:content**&#x200B;节点中为这两个过滤器分配了不同的&#x200B;**userId**。 请参阅下图：

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 自定义复制{#customizing-asset-filters-for-replication}的资产过滤器

（可选）要自定义资产过滤器以进行复制，请执行以下操作：

1. 在Experience Manager中，点按Experience Manager徽标以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite。]**
1. 在左侧文件夹树中，导航到`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`以查看过滤器。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 要定义筛选器的MIME类型，可以按如下方式查找Mime类型：

   在左边栏中，展开`content > dam > <locate_your_asset> >  jcr:content > metadata`，然后在表中找到&#x200B;**[!UICONTROL dc:format.]**

   下图是资产到dc:format的路径示例。

   ![chlimage_1-512](assets/chlimage_1-512.png)

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

下图是资产的演绎版示例。

![chlimage_1-513](assets/chlimage_1-4.png)

使用上面的示例，如果您只想复制PTIFF（金字塔TIFF），则应输入`+cqdam,*`，其中包括与`cqdam`开始的所有演绎版。 在示例中，该再现为`cqdam.pyramid.tiff`。

如果只想复制原件，则输入`+original`。

## 配置Dynamic Media Image Server设置{#configuring-dynamic-media-image-server-settings}

配置Dynamic Media Image Server涉及编辑Adobe CQ Scene7 ImageServer捆绑和Adobe CQ Scene7 PlatformServer捆绑。

>[!NOTE]
Dynamic Media启用后即可开箱运行[。 ](#enabling-dynamic-media)但是，您可以选择通过配置Dynamic Media Image Server来优化安装，以满足特定规范或要求。

**先决条件**: *在* 配置Dynamic Media Image Server之前，请确保您的Windows®虚拟机包括Microsoft® Visual C++库的安装。运行Dynamic Media Image Server时必须使用这些库。 您可以[在此处](https://www.microsoft.com/en-us/download/details.aspx?id=14632)下载Microsoft® Visual C++ 2010 Redistributable Package(x64)。

要配置Dynamic Media Image Server设置：

1. 在Experience Manager的左上角，点按&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具>操作> Web控制台。]**
1. 在Adobe Experience Manager Web控制台的“配置”页上，点按&#x200B;**[!UICONTROL OSGi > Configuration]**&#x200B;以列表Experience Manager中当前运行的所有捆绑包。

   Dynamic Media投放服务器位于列表中的以下名称下：

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 在捆绑包的列表中，点按Adobe CQ Scene7 ImageServer右侧的编辑图标。
1. 在Adobe CQ Scene7 ImageServer对话框中，设置以下配置值：

   >[!NOTE]
   通常，无需更改默认值。 但是，如果确实更改了默认值，则必须重新启动包才能使更改生效。

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
   <td>用于与ImageServer进程通信的端口号。 默认情况下，会自动检测空闲端口。</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>允许或禁止对ImageServer进程的远程访问。 如果为false，则图像服务器仅侦听localhost。</p> <p>指向localhost的默认外部设定器设置必须指定特定VM实例的实际域或IP地址。 原因是localhost指向VM的父系统。</p> <p>VM的域或IP地址必须有一个主机文件条目，以便它能够解析自身。</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16兆帕</td>
   <td>渲染的最大大小（以百万像素为单位）。</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16 MB</td>
   <td>传递的最大消息大小(MB)。</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>超时值，指图像服务器等待JCR响应范围内的拼贴请求的时间（以秒为单位）。</td>
  </tr>
  <tr>
   <td>WorkerThreads</td>
   <td>10</td>
   <td>工作线程数。</td>
  </tr>
 </tbody>
</table>

1. 点按&#x200B;**[!UICONTROL 保存。]**
1. 在捆绑包的列表中，点按Adobe CQ Scene7 PlatformServer右侧的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在Adobe CQ Scene7 PlatformServer对话框中，设置以下默认值选项：

   >[!NOTE]
   Dynamic Media Image Server使用其自己的磁盘缓存缓存响应。 无法使用Experience Manager HTTP缓存和调度程序缓存来自Dynamic Media Image Server的响应。

   | **属性** | **默认值** | **描述** |
   |---|---|---|
   | 已启用缓存 | 已选中 | 是否启用响应缓存 |
   | 缓存根 | 缓存 | 指向响应缓存文件夹的一个或多个路径。 相对路径针对内部s7imaging bundle文件夹进行解析。 |
   | 缓存最大大小 | 200000000 | 响应缓存的最大大小（以字节为单位）。 |
   | 缓存最大条目数 | 100000 | 缓存中允许的最大条目数。 |

### 默认清单设置{#default-manifest-settings}

默认清单允许您配置用于生成Dynamic Media投放响应的默认值。 您可以微调质量（JPEG质量、分辨率、重新取样模式）、缓存（过期），并防止渲染过大的图像(defaultpix、defaultthumpix、maxpix)。

默认清单配置的位置来自&#x200B;**[!UICONTROL Adobe CQ Scene7 PlatformServer]**&#x200B;包的&#x200B;**[!UICONTROL 目录根]**&#x200B;默认值。 默认情况下，此值位于&#x200B;**[!UICONTROL “工具”>“常规”>“CRXDE Lite]**”中的以下路径：

`/conf/global/settings/dam/dm/imageserver/`

![在CRXDE Lite中配置图像服务器](assets/configimageservercrxdelite.png)

您可以通过输入新值来更改属性的值，如下表中所述。

更改完默认清单后，请点按页面左上角的&#x200B;**[!UICONTROL 全部保存]**。

请确保点按&#x200B;**[!UICONTROL 访问控制]**&#x200B;选项卡（“属性”选项卡右侧），然后将每个用户和动态媒体复制用户的访问控制权限设置为`jcr:read`。

![在CRXDE Lite中配置图像服务器并设置“访问控制”选项卡](assets/configimageservercrxdeliteaccesscontroltab.png)

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
   <td><p>默认背景颜色。 用于填充不含实际图像数据的回复图像任何区域的RGB值。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api">BkgColor</a>。</p> </td>
  </tr>
  <tr>
   <td>defaultpix</td>
   <td>三十万零三百</td>
   <td><p>默认视图大小。 如果请求未使用wid=、hei=或scl=显式指定视图大小，则服务器将限制返回图像不大于此宽度和高度。</p> <p>指定为两个整数，0或更大，用逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值设置为0，以保持它们不受约束。 不适用于嵌套/嵌入的请求。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api">DefaultPix</a>。</p> <p>但是，您通常使用查看器预设或图像预设来传送资产。 Defaultpix仅适用于未使用查看器预设或图像预设的资产。</p> </td>
  </tr>
  <tr>
   <td>defaulthumbpix</td>
   <td>十万零一百</td>
   <td><p>默认缩略图大小。 Useded而不是attribute::DefaultPix for thumbnail requests(req=tmb)。</p> <p>服务器将限制返回图像不大于此宽度和高度。 如果缩略图请求(req=tmb)未显式指定大小且未使用“wid=”、“hei=”或“scl=”显式指定视图大小，则此操作为true。</p> <p>指定为两个整数，0或更大，用逗号分隔。 宽度和高度（以像素为单位）。 可以将任一或两个值设置为0，以保持它们不受约束。 </p> <p>不适用于嵌套/嵌入的请求。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api">DefaultThumbPix</a>。 </p> </td>
  </tr>
  <tr>
   <td>过期</td>
   <td>36000000</td>
   <td><p>默认客户端缓存的活动时间。 提供默认的过期时间间隔，以防特定目录记录不包含有效的目录：:Expiration值。</p> <p>实数，0或更大。 自生成回复数据后，到期为止的毫秒数。 设置为0可始终立即使回复图像过期，这会有效地禁用客户端缓存。 默认情况下，此值设置为10小时，这意味着如果发布了新图像，则旧图像离开用户缓存需要10小时。 如果您需要更早清除缓存，请与客户服务部门联系。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html">Expiration</a>。</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>默认JPEG编码属性。 指定JPEG回复图像的默认属性。</p> <p>整数数字和标志，以逗号分隔。 第一个值在1.100范围内，并定义质量。 第二个值可以是0（对于正常行为），也可以是1（用于禁用JPEG编码器采用的RGB色度缩减采样）。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api">JpegQuality</a>。</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>20万2千</td>
   <td><p>回复图像大小限制。 返回到客户端的最大回复图像宽度和高度。</p> <p>如果请求导致返回图像的宽度或高度大于属性：:MaxPix，则服务器会返回错误。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=en#image-serving-api">MaxPix</a>。</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>默认重新取样模式。 指定用于缩放图像数据的默认重新取样属性和插值属性。</p> <p>在请求中未指定resMode=时使用。</p> <p>允许的值包括BILIN、BICUB或SHARP2。</p> <p>枚举。 对于bilin，设置为2；对于bicub，设置为3；对于sharp2插值模式，设置为4。 使用sharp2可获得最佳效果。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api">ResMode</a>。</p> </td>
  </tr>
  <tr>
   <td>分辨率</td>
   <td>72</td>
   <td><p>默认对象分辨率。 提供默认对象分辨率，以防特定目录记录不包含有效的目录：:Resolution值。</p> <p>实数，大于0。 通常以每英寸像素数表示，但也可以以其他单位表示，如每米像素数。</p> <p>另请参阅图像服务API中的<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api">分辨率</a>。</p> </td>
  </tr>
  <tr>
   <td>thumbnaitime</td>
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>这些值表示视频播放时间的快照，并传递给<a href="https://www.encoding.com/">encoding.com</a>。 有关详细信息，请参阅<a href="/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode">关于视频缩略图</a>。</td>
  </tr>
 </tbody>
</table>

## 配置Dynamic Media色彩管理{#configuring-dynamic-media-color-management}

Dynamic Media色彩管理允许您为预览对资源进行颜色校正。

借助颜色校正，摄取的资源在生成的金字塔TIFF再现中保留其色彩空间（RGB、CMYK、灰色）和嵌入的用户档案。 当您请求动态再现时，图像颜色会校正到目标色彩空间中。 可以在JCR的Dynamic Media发布设置中配置输出颜色用户档案。

Adobe色彩管理使用ICC（国际色彩联盟）用户档案,ICC定义的一种格式。

您可以配置Dynamic Media色彩管理，并使用CMYK、RGB或灰色输出配置图像预设。 请参阅[配置图像预设](/help/assets/managing-image-presets.md)。

高级用例可以使用手动配置`icc=`修饰符来显式选择输出颜色用户档案:

* `icc` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
只有安装了软件分发的[功能包12445](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445)时，才能使用标准的Adobe颜色用户档案集。 所有功能包和服务包均在[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)提供。 功能包12445提供Adobe颜色用户档案。


### 安装功能包12445 {#installing-feature-pack}

要使用Dynamic Media色彩管理功能，请安装功能包12445。

**安装功能包12445**

1. 导航到[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)并下载`cq-6.3.0-featurepack-12445`。

   有关在[!DNL Adobe Experience Manager]中使用包的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。

1. 安装功能包。

### 配置默认颜色用户档案{#configuring-the-default-color-profiles}

安装功能包后，配置适当的默认颜色用户档案，以在请求RGB或CMYK图像数据时启用颜色校正。

**配置默认颜色用户档案**

1. 在&#x200B;**[!UICONTROL “工具”>“常规”>“CRXDE Lite”]**&#x200B;中，导航到包含默认Adobe Color用户档案的`/conf/global/settings/dam/dm/imageserver/jcr:content`。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 通过滚动到&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡底部来添加颜色校正属性。 手动输入属性名称、类型和值，如下表中所述。 输入这些值后，点按&#x200B;**[!UICONTROL 添加]**，然后点按&#x200B;**[!UICONTROL 保存全部]**&#x200B;以保存您的值。

   颜色校正属性在&#x200B;**颜色校正属性**&#x200B;表中有介绍。 可指定给颜色校正属性的值位于&#x200B;**颜色用户档案**&#x200B;表中。

   例如，在&#x200B;**[!UICONTROL 名称]**&#x200B;中，添加`iccprofilecmyk`，选择&#x200B;**[!UICONTROL 类型]** `String`，并将`WebCoated`添加为&#x200B;**[!UICONTROL 值。]** 然后，点 **** 按添加，再 **[!UICONTROL 点]** 按保存全部以保存您的值。

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
   <td>默认RGB颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilemyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认CMYK颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">iccprofilegray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>默认灰色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesercrgb</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的RGB图像的默认RGB颜色用户档案的名称</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrccmyk</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的CMYK图像的默认CMYK颜色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>字符串</td>
   <td>&lt;empty&gt;</td>
   <td>用于未嵌入颜色用户档案的CMYK图像的默认灰色用户档案的名称。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpoint补偿</a></td>
   <td>布尔型</td>
   <td>True</td>
   <td>指定是否在颜色校正期间执行黑场补偿。 Adobe建议此设置处于打开状态。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">iccdither</a></td>
   <td>布尔型</td>
   <td>False</td>
   <td>指定是否在颜色校正期间执行仿色。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">iccrenderintent</a></td>
   <td>字符串</td>
   <td>相对</td>
   <td><p>指定渲染方法。 可接受的值为：<strong>可感知、相对、饱和、绝对。 </strong><i></i>Adobe建议 <strong>将 </strong><i></i>相对值作为默认值。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
属性名称区分大小写，且必须全部为小写。

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
   <td>Coated GRACoL 2006(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>颜色匹配RGB</td>
  </tr>
  <tr>
   <td>欧洲ISOC</td>
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
   <td>JapanColorSpeable</td>
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
   <td>新闻纸SNAP2007</td>
   <td>CMYK</td>
   <td>美国新闻纸（2007年快照）</td>
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
   <td>PS5默认</td>
   <td>CMYK</td>
   <td>Photoshop 5默认CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>美国Sheetfed Coated v2</td>
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
   <td>美国Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGalytRGB</td>
   <td>RGB</td>
   <td>宽色域RGB</td>
  </tr>
 </tbody>
</table>

1. 点按&#x200B;**[!UICONTROL 保存全部。]**

例如，您可以将&#x200B;**[!UICONTROL iccprofilergb]**&#x200B;设置为`sRGB`，将&#x200B;**[!UICONTROL iccprofilecmyk]**&#x200B;设置为&#x200B;**[!UICONTROL WebCoated。]**

这样做将执行以下操作：

* 启用RGB和CMYK图像的颜色校正。
* 假定没有颜色用户档案的RGB图像位于&#x200B;*sRGB*&#x200B;色彩空间中。
* 假定没有颜色用户档案的CMYK图像位于&#x200B;*WebCoated*&#x200B;色彩空间中。
* 返回RGB输出的动态演绎版，在*sRGB *色彩空间中返回它。
* 返回CMYK输出的动态演绎版，在&#x200B;*WebCoated*&#x200B;色彩空间中返回它。

## 传送资产 {#delivering-assets}

完成上述所有任务后，会通过图像或视频服务提供激活的Dynamic Media资产。 在Experience Manager中，此功能显示在&#x200B;**[!UICONTROL 复制图像URL]**、**[!UICONTROL 复制查看器URL]**、**[!UICONTROL 嵌入查看器代码]**&#x200B;和WCM中。

请参阅[传送Dynamic Media资产](/help/assets/delivering-dynamic-media-assets.md)。

<table>
 <tbody>
  <tr>
   <td><strong>当你……</strong></td>
   <td><strong>结果</strong></td>
  </tr>
  <tr>
   <td>复制图像URL</td>
   <td><p>"复制URL"对话框显示与以下内容类似的URL（URL仅用于演示目的）：</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>其中<code>IMAGESERVICEPUBLISHNODE</code>指的是图像服务URL。</p> <p>另请参阅<a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>。</p> </td>
  </tr>
  <tr>
   <td>复制查看器URL</td>
   <td><p>"复制URL"对话框显示与以下内容类似的URL（URL仅用于演示目的）：</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>其中<code>PUBLISHNODE</code>指常规Experience Manager发布节点，<code>IMAGESERVICEPUBLISHNODE</code>指图像服务URL。</p> <p>另请参阅<a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>。</p> </td>
  </tr>
  <tr>
   <td>复制查看器的嵌入代码</td>
   <td><p>“复制嵌入代码”对话框显示与以下内容类似的代码片段（代码示例仅用于演示目的）：</p> <p><code class="code">&lt;style type="text/css"&gt;
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
       &lt;/script&gt;</code></p> <p>其中<code>PUBLISHNODE</code>指常规Experience Manager发布节点，<code>IMAGESERVICEPUBLISHNODE</code>指图像服务URL。</p> <p>另请参阅<a href="/help/assets/delivering-dynamic-media-assets.md">传送Dynamic Media资产</a>。</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media和交互式媒体组件{#wcm-dynamic-media-and-interactive-media-components}

引用Dynamic Media和交互式媒体组件的WCM页面引用投放服务。
