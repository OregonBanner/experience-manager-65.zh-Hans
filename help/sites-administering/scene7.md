---
title: 将Adobe Experience Manager与Dynamic Media Classic集成
description: 了解如何将Adobe Experience Manager与Dynamic Media Classic集成。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '5484'
ht-degree: 1%

---

# 将Adobe Experience Manager与Dynamic Media Classic集成 {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic是一个托管解决方案，用于管理、增强、发布富媒体资产并将其交付到Web、移动设备、电子邮件以及连接Internet的显示屏和打印设备。

要使用Dynamic Media Classic，您必须配置云配置，以便Dynamic Media Classic和Adobe Experience Manager Assets能够彼此进行交互。 本文档介绍如何配置Experience Manager和Dynamic Media Classic。

有关在页面上使用所有Dynamic Media Classic组件和处理视频的信息，请参阅 [使用Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* Dynamic Media Classic的DHTML查看器平台于2014年1月31日正式终止使用。 有关更多信息，请参阅 [DHTML查看器生命周期终止常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* 在将Dynamic Media Classic配置为使用Experience Manager之前，请参阅 [最佳实践](#best-practices-for-integrating-scene-with-aem) 用于将Dynamic Media Classic与Experience Manager集成。
>* 如果您将Dynamic Media Classic与自定义代理配置一起使用，则必须同时配置两个HTTP客户端代理配置，因为Experience Manager的某些功能使用3.x API，而其他功能使用4.x API。 3.x的配置 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 和4.x的配置 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>


## Experience Manager/Dynamic Media Classic集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager用户可以在两个解决方案之间进行选择，以与Dynamic Media配合使用。 您可以使用以下任一方法：

* 将您的Experience Manager实例与Dynamic Media Classic集成。
* 使用集成到Experience Manager中的Dynamic Media。

使用以下标准确定要选择的解决方案：

* 你是 **现有** Dynamic Media Classic客户的资产位于Dynamic Media Classic中以供发布和交付，但您希望将这些资产与Sites(WCM)创作或Experience Manager Assets或两者集成？ 如果是，请使用 [Experience Manager/Dynamic Media Classic点对点集成](#aem-scene-point-to-point-integration) 如本文档所述。

* 如果您是 **新建** Experience Manager具有富媒体交付需求的客户，请选择 [Dynamic Media选项](#aem-dynamic-media). 如果您没有现有的S7帐户，并且该系统中存储了许多资产，则此选项最有意义。

* 在某些情况下，请同时使用这两种解决方案。 的 [双用方案](/help/sites-administering/scene7.md#dual-use-scenario) 描述此方案。

### Experience Manager/Dynamic Media Classic点对点集成 {#aem-scene-point-to-point-integration}

在此解决方案中处理资产时，您需要执行以下操作之一：

* 将资产直接上传到Dynamic Media Classic，然后通过 **Dynamic Media Classic** 用于页面创作的内容浏览器或
* 上传到Experience Manager Assets，然后启用自动发布到Dynamic Media Classic;通过 **资产** 页面创作内容浏览器

您用于此集成的组件可在 **Dynamic Media Classic** 组件区域 [设计模式](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience ManagerDynamic Media {#aem-dynamic-media}

Experience ManagerDynamic Media是直接在Experience Manager平台内统一Dynamic Media Classic功能。

在此解决方案中处理资产时，您需要遵循以下工作流程：

1. 将单个图像和视频资产直接上传到Experience Manager。
1. 直接在Experience Manager中对视频进行编码。
1. 直接在Experience Manager中构建基于图像的集。
1. 如果适用，为图像或视频添加交互性。

您用于Dynamic Media的组件位于 **[!UICONTROL Dynamic Media]** 组件区域 [设计模式](/help/sites-authoring/author-environment-tools.md#page-modes). 包括以下内容：

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]** 组件是智能的 — 根据您添加的是图像还是视频，您可以选择各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

* **[!UICONTROL 交互式媒体]** - **[!UICONTROL 交互式媒体]** 组件适用于轮播横幅、交互式图像和交互式视频等资产。 这些资产具有交互性，例如热点或图像映射。 此组件是智能的。 也就是说，根据您添加的是图像还是视频，您可以选择各种不同的选项。 此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

### 两用方案 {#dual-use-scenario}

开箱即用，您可以同时使用Dynamic Media和Dynamic Media Classic的Experience Manager集成功能。 下表说明了何时打开和关闭某些区域。

要同时使用Dynamic Media和Dynamic Media Classic，请执行以下操作：

1. 配置 [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) Cloud Services。
1. 按照特定于您的用例的具体说明操作：

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic集成</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>如果您……</strong></td>
    <td><strong>用例工作流</strong></td>
    <td><strong>成像/视频</strong></td>
    <td><strong>动态媒体组件</strong></td>
    <td><strong>S7内容浏览器和组件</strong></td>
    <td><strong>从资产自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>站点和Dynamic Media的新增功能</td>
    <td>将资产上传到Experience Manager，然后使用Experience ManagerDynamic Media组件在站点页面上创作资产</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>在零售领域，新增了站点和Dynamic Media</td>
    <td>将非产品资产上传到Experience Manager，以便进行管理和交付。 将产品资产上传到Dynamic Media Classic，并在Experience Manager和组件中使用Dynamic Media Classic内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>资产和Dynamic Media的新增功能</td>
    <td>将资产上传到Experience Manager Assets，并使用Dynamic Media中发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>Dynamic Media和模板的新增功能</td>
    <td>使用Dynamic Media进行成像和视频处理。 在Dynamic Media Classic中创作图像模板，并使用Dynamic Media Classic内容查找器在站点页面中包含模板。</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，是Sites的新用户</td>
    <td>将资产上传到Dynamic Media Classic，然后使用Experience ManagerDynamic Media Classic内容浏览器在站点页面上搜索和创作资产</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，是站点和资产的新用户</td>
    <td>将资产上传到DAM并自动发布到Dynamic Media Classic以进行交付。 使用Experience ManagerDynamic Media Classic内容浏览器在站点页面上搜索和创作资产。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和新资产客户</td>
    <td><p>将资产上传到Experience Manager，然后使用Dynamic Media生成要下载/共享的演绎版。 自动将Experience Manager资产发布到Dynamic Media Classic以进行交付。</p> <p><strong>重要信息：</strong> 在Experience Manager中生成的处理和演绎版出现重复时，未同步到Dynamic Media Classic</p> </td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可选；请参阅用例表) — 设置 [Dynamic Media云配置](/help/assets/config-dynamic.md) 和 [启用Dynamic Media服务器](/help/assets/config-dynamic.md).
1. (可选；请参阅用例表) — 如果您选择启用“从资产自动上传到Dynamic Media Classic”，则必须添加以下内容：

   1. 设置自动上传到Dynamic Media Classic。
   1. 添加 **Dynamic Media Classic上传** 步骤(完成所有Dynamic Media工作流步骤) *在* **Dam更新资产** 工作流( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. （可选）按MIME类型在 [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). 此列表中未包含的资产MIME类型不会上传到Dynamic Media Classic服务器。
   1. （可选）在Dynamic Media Classic配置中设置视频。 您可以同时为Dynamic Media和Dynamic Media Classic启用视频编码。 动态演绎版用于在Experience Manager实例中在本地预览和播放，而Dynamic Media Classic视频演绎版则在Dynamic Media Classic服务器上生成和存储。 为Dynamic Media和Dynamic Media Classic设置视频编码服务时，请应用 [视频处理配置文件](/help/assets/video-profiles.md) 到Dynamic Media Classic资产文件夹。
   1. （可选） [在Dynamic Media Classic中配置安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### 限制 {#limitations}

同时启用Dynamic Media Classic和Dynamic Media后，存在以下限制：

* 无法通过选择资产并将其拖动到Dynamic Media Classic页面上的Dynamic Media Classic组件来手动上传到Experience Manager。
* 即使在Assets中编辑Experience Manager时，Dynamic Media Classic同步的资产会自动更新到Dynamic Media Classic，回滚操作也不会触发新的上传。 因此，Dynamic Media Classic在回滚后不会立即获取最新版本。 解决方法是在回滚完成后再次进行编辑。
* 您是否有必要将Dynamic Media用于一个用例，将Dynamic Media Classic集成用于另一个用例，以便Dynamic Media资产不会与Dynamic Media Classic系统进行交互？ 如果是，请不要将Dynamic Media Classic配置应用到Dynamic Media文件夹。 另外，请勿将Dynamic Media配置（处理配置文件）应用到Dynamic Media Classic文件夹。

## 将Dynamic Media Classic与Experience Manager集成的最佳实践 {#best-practices-for-integrating-scene-with-aem}

在将Dynamic Media Classic与Experience Manager集成时，必须遵循以下方面的一些重要最佳实践：

* 测试集成
* 在某些情况下，建议直接从Dynamic Media Classic上传资产

请参阅 [已知限制](#known-limitations-and-design-implications).

### 测试集成 {#test-driving-your-integration}

Adobe建议您通过让根文件夹仅指向子文件夹而不是整个公司来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要较长时间，才能在Experience Manager中显示。 确保您在Dynamic Media Classic中指定的文件夹的资产不太多（例如，根文件夹的资产通常过多，并且可能会导致系统崩溃）。

### 从Experience Manager Assets与从Dynamic Media Classic上传资产 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用资产（数字资产管理）功能上传资产，或通过直接通过Dynamic Media Classic内容浏览器以Experience Manager方式访问Dynamic Media Classic来上传资产。 您选择哪个因素取决于以下因素：

* Dynamic Media Classic尚不支持的Experience Manager Assets资产类型必须通过Dynamic Media Classic内容浏览器，直接从Dynamic Media Classic添加到Experience Manager网站。 例如，图像模板。
* 对于Experience Manager Assets和Dynamic Media Classic都支持的资产类型，如何上传取决于以下信息：

   * 当前资产所在的位置和
   * 在通用存储库中管理它们的重要性

假定资产已在Dynamic Media Classic中，并且在通用存储库中管理它们并不重要。 如果是这种情况，则不必进行往返测试，只需将资产导出到Experience Manager Assets，并仅将其同步回Dynamic Media Classic以便交付。 Adobe建议您将资产保留在单个存储库中，并同步到Dynamic Media Classic以仅进行交付。

## 配置Dynamic Media Classic集成 {#configuring-scene-integration}

您可以配置Experience Manager以将资产上传到Dynamic Media Classic。 从CQ目标文件夹中的资产可以（自动或手动）从Experience Manager上传到Dynamic Media Classic公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media Classic资产。 位于目标文件夹以外的数字资产只能在已启用Dynamic Media Classic配置的页面上的Dynamic Media Classic组件中使用。 此外，它们还放在Dynamic Media Classic的按需文件夹中。 按需文件夹未与Experience Manager同步(但Dynamic Media Classic内容浏览器中会发现资产)。

**要配置Dynamic Media Classic以与Experience Manager集成，请执行以下操作：**

1. [定义云配置](#creating-a-cloud-configuration-for-scene)  — 定义Dynamic Media Classic文件夹和Assets文件夹之间的映射。 即使您只想要单向(Experience Manager Assets到Dynamic Media Classic)同步，也可以完成此步骤。
1. [启用 **Adobe CQ s7dam Dam侦听器**](#enabling-the-adobe-cq-scene-dam-listener)  — 在 [!UICONTROL OSGi] 控制台。
1. 如果您希望Experience Manager Assets自动上传到Dynamic Media Classic，则必须打开该选项，并将Dynamic Media Classic添加到 [!UICONTROL DAM更新资产] 工作流。 您还可以手动上传资产。
1. 将Dynamic Media Classic组件添加到Sidekick。 此功能允许用户在其Experience Manager页面上使用Dynamic Media Classic组件。
1. [将配置映射到Experience Manager中的页面](#enabling-scene-for-wcm)  — 查看您在Dynamic Media Classic中创建的任何视频预设时，需要执行此步骤。 如果您必须从CQ目标文件夹外部将资产发布到Dynamic Media Classic，则还需要此参数。

本节介绍如何执行所有这些步骤，并列出重要限制。

### Dynamic Media Classic与Experience Manager Assets之间的同步工作原理 {#how-synchronization-between-scene-and-aem-assets-works}

在设置Experience Manager Assets和Dynamic Media Classic同步时，请务必了解以下内容：

#### 从Experience Manager Assets上传到Dynamic Media Classic {#uploading-to-scene-from-aem-assets}

* Experience Manager中有一个指定的同步文件夹，用于Dynamic Media Classic上传。
* 如果将数字资产放置在指定的同步文件夹中，则可以自动上传到Dynamic Media Classic。
* Experience Manager中的文件夹和子文件夹结构将复制到Dynamic Media Classic中。

>[!NOTE]
>
>Experience Manager在将所有元数据上传到Dynamic Media Classic之前，会将其嵌入为XMP，因此该元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。

#### 已知限制和设计含义 {#known-limitations-and-design-implications}

通过在Experience Manager Assets和Dynamic Media Classic之间进行同步，当前存在以下限制/设计含义：

<table>
 <tbody>
  <tr>
   <td><strong>限制/设计含义</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步（目标）文件夹</td>
   <td>您在Dynamic Media Classic上传的Experience Manager中，每个公司只能有一个指定的文件夹。 如果您必须有权访问Dynamic Media Classic中的多个公司帐户，则可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果删除具有资产的已同步文件夹，则所有Dynamic Media Classic远程资产都将被删除，但该文件夹仍会保留。</td>
  </tr>
  <tr>
   <td>按需文件夹</td>
   <td>在WCM中手动上传到Dynamic Media Classic的目标文件夹以外的资产会自动放置在Dynamic Media Classic上的单独按需文件夹中。 您可以在云配置中以Experience Manager配置此文件夹。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集在Experience Manager中显示，但在Experience Manager中不受支持。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media Classic中的eCatalogs生成的PDF会导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在Experience Manager和Dynamic Media Classic之间同步时，请务必刷新用户界面以查看更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果将视频上传到Experience Manager Assets以通过Dynamic Media Classic进行编码，则Experience Manager Assets中可能需要一些时间来提供视频缩略图和编码视频，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>Target子文件夹</td>
   <td><p>如果您在目标文件夹中使用子文件夹，请确保为每个资产使用唯一的名称（无论位置如何）。 此外，请确保将Dynamic Media Classic（在“设置”区域）配置为不会覆盖资产，而不考虑其位置。</p> <p>否则，将会上传具有相同名称且已上传到Dynamic Media Classic目标子文件夹的资产，但会删除目标文件夹中同名的资产。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic服务器 {#configuring-scene-servers}

如果在代理后运行Experience Manager或具有特殊的防火墙设置，则必须明确启用不同区域的主机。 服务器在 `/etc/cloudservices/scene7/endpoints` 和可根据需要进行自定义。 选择一个URL，然后进行编辑以根据需要更改该URL。 在早期版本的Experience Manager中，这些值进行了硬编码。

如果您导航到 `/etc/cloudservices/scene7/endpoints.html`，则会看到列出的服务器（并可以通过点按URL来编辑它们）：

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media Classic创建云配置 {#creating-a-cloud-configuration-for-scene}

云配置定义了Dynamic Media Classic文件夹和Experience Manager Assets文件夹之间的映射。 必须将其配置为将Experience Manager Assets与Dynamic Media Classic同步。 有关更多信息，请参阅同步的工作原理。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要较长时间，才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定的资产不太多的文件夹。 例如，根文件夹的资产通常过多。
>
>如果要测试集成，请让根文件夹仅指向子文件夹，而不是整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示Dynamic Media Classic公司的一个用户。 如果要访问其他Dynamic Media Classic公司或用户，则必须创建多个配置。

**为Dynamic Media Classic创建云配置：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]** 这样您就可以访问Adobe Dynamic Media Classic。

1. 选择 **[!UICONTROL 立即配置]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在 **[!UICONTROL 标题]** 字段中，或者在 **[!UICONTROL 名称]** 字段，输入相应的信息。 选择&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >创建更多配置时， **[!UICONTROL 父配置]** 字段。
   >
   >做 **not** 更改父配置。 更改父配置可能会破坏集成。

1. 输入Dynamic Media Classic帐户的电子邮件地址、密码和区域，然后选择 **[!UICONTROL 连接到Dynamic Media Classic]**. 您已连接到Dynamic Media Classic服务器，此时对话框将展开，显示更多选项。

1. 输入 **[!UICONTROL 公司]** 名称和 **[!UICONTROL 根路径]**. 此信息是已发布的服务器名称以及您要指定的任何路径。 如果您不知道已发布的服务器名称，请在Dynamic Media Classic中，转到 **[!UICONTROL 设置>应用程序设置]**)。

   >[!NOTE]
   >
   >Dynamic Media Classic根路径是连接到的Dynamic Media Classic文件夹Experience Manager。 可以将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media Classic文件夹的大小，导入根文件夹可能会花费较长时间。 此外，Dynamic Media Classic数据可能会超出Experience Manager存储。 确保导入正确的文件夹。 导入过多数据可能会停止您的系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 选择 **[!UICONTROL 确定]**. Experience Manager保存您的配置。

>[!NOTE]
>
>如果要重新连接：
>
>* 在发布时重新连接到Dynamic Media Classic时，在发布时重置密码或重新连接时无法正常工作（在创作实例中不存在问题）。
>* 如果修改地区、公司名称等值，则必须重新连接到Dynamic Media Classic。 如果配置选项已修改但未保存，则Experience Manager仍会错误地指示配置有效。 确保重新连接。
>


### 启用Adobe CQ Dynamic Media Classic Dam侦听器 {#enabling-the-adobe-cq-scene-dam-listener}

启用Adobe CQ Dynamic Media Classic Dam侦听器，默认情况下处于禁用状态。

**要启用Adobe CQ Dynamic Media Classic Dam侦听器，请执行以下操作：**

1. 选择 [!UICONTROL 工具] 图标，然后导航到 **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Web控制台中，导航到 **[!UICONTROL Adobe CQ Dynamic Media Classic Dam侦听器]** ，然后选择 **[!UICONTROL 已启用]** 复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 向Dynamic Media Classic上传工作流添加可配置的超时 {#adding-configurable-timeout-to-scene-upload-workflow}

如果将Experience Manager实例配置为通过Dynamic Media Classic处理视频编码，则默认情况下，任何上传作业都会有35分钟的超时。 要适应可能运行时间较长的视频编码作业，您可以配置此设置。

1. 导航到 **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 根据需要，在 **[!UICONTROL 活动作业超时]** 字段。 以秒为单位接受任何非负数。 默认情况下，此数字设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资产最多会在几分钟内摄取（例如，图像）。 但在某些情况下（例如，视频较大），将超时值增加到7200秒（2小时），以适应较长的处理时间。 否则，此Dynamic Media Classic上传作业将标记为 **[!UICONTROL 上载失败]** (在JCR(Java™内容存储库)元数据中)。

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 来自Experience Manager Assets的奥图普洛德 {#autouploading-from-aem-assets}

从Experience Manager6.3.2开始，系统会配置Experience Manager Assets，以便如果资产位于CQ目标文件夹中，则任何上传的数字资产都会更新到Dynamic Media Classic。

将资产添加到Experience Manager Assets后，会自动将其上传并发布到Dynamic Media Classic。

>[!NOTE]
>
>从Experience Manager Assets自动上传到Dynamic Media Classic的最大文件大小为500 MB。

**要从Experience Manager Assets下载自动上传，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在Dynamic Media标题的可用配置下，选择 **[!UICONTROL dms7(Dynamic Media)]**)。
1. 选择 **[!UICONTROL 高级]** 选项卡，选择 **[!UICONTROL 启用自动上传]** 复选框，然后选择 **[!UICONTROL 确定]**. 现在，您必须配置DAM资产工作流，以包含上传到Dynamic Media Classic。

   >[!NOTE]
   >
   >请参阅 [配置推送到Dynamic Media Classic的资产的状态（已发布/未发布）](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) 以了解有关将资产推送到未发布状态的Dynamic Media Classic的信息。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回Experience Manager欢迎页面，然后选择 **[!UICONTROL 工作流]**. 双击 **DAM更新资产** 工作流，以便打开。
1. 在Sidekick中，导航到 **[!UICONTROL 工作流]** 组件，然后选择 **[!UICONTROL Dynamic Media Classic]**. 拖动 **[!UICONTROL Dynamic Media Classic]** ，然后选择 **[!UICONTROL 保存]**. 目标文件夹中添加到Experience Manager Assets的资产会自动上传到Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动化后添加资产时，如果资产未放入CQ目标文件夹，则它们不会上传到Dynamic Media Classic。
   >* Experience Manager在将所有元数据上传到Dynamic Media Classic之前，会将其嵌入为XMP，因此该元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。


### 配置推送到Dynamic Media Classic的资产的状态（已发布/未发布） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果您将资产从Experience Manager Assets推送到Dynamic Media Classic，则可以自动发布资产（默认行为）或将资产推送到未发布状态的Dynamic Media Classic。

如果要在上线之前在暂存环境中测试资产，则可能不希望立即在Dynamic Media Classic上发布资产。 您可以将Experience Manager与Dynamic Media Classic的安全测试环境结合使用，以将资产直接从资产推送到处于未发布状态的Dynamic Media Classic。

Dynamic Media Classic资产仍可通过安全预览使用。 只有在Experience Manager中发布资产时，Dynamic Media Classic资产才会在生产环境中上线。

如果要在将资产推送到Dynamic Media Classic时立即发布资产，则无需配置任何选项。 此功能是默认行为。

但是，如果您不希望将资产推送到Dynamic Media Classic以自动发布，则此部分将介绍如何配置Experience Manager和Dynamic Media Classic以执行此功能。

#### 将资产推送到未发布的Dynamic Media Classic的先决条件 {#prerequisites-to-push-assets-to-scene-unpublished}

在不发布资产的情况下将资产推送到Dynamic Media Classic之前，您必须先设置以下内容：

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). 在您的支持案例中，请为您的Dynamic Media Classic帐户请求启用安全预览。
1. [为Dynamic Media Classic帐户设置安全预览](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

这些步骤与在Dynamic Media Classic中创建任何安全测试设置时所遵循的步骤相同。

>[!NOTE]
>
>如果您的安装环境是UNIX® 64位操作系统，请参阅 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) 关于其他配置选项，您必须设置。

#### 将资产推送到未发布状态的已知限制  {#known-limitations-for-pushing-assets-in-unpublished-state}

如果使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在Experience Manager中发布，并且创建了后续版本，则该新版本会立即实时发布到生产环境。 激活时发布仅适用于资产的初始发布。

>[!NOTE]
>
>如果您想要立即发布资产，最佳实践是 **[!UICONTROL 启用安全预览]** 设置为 **[!UICONTROL 立即]** 并使用 **[!UICONTROL 启用自动上传]** 功能。

### 将推送到Dynamic Media Classic的资产状态设置为未发布 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在Experience Manager中发布资产，则会自动将S7资产触发到生产/活动资产（资产不再处于安全预览/取消发布状态）。

**要将推送到Dynamic Media Classic的资产状态设置为未发布，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 选择 **[!UICONTROL 高级]** 选项卡。
1. 在 **[!UICONTROL 启用安全视图]** 下拉菜单，选择 **[!UICONTROL 激活AEM发布时]** 将资产推送到Dynamic Media Classic而不发布。 (默认情况下，此值设置为 **[!UICONTROL 立即]**，立即发布Dynamic Media Classic资产。)

   请参阅 [Dynamic Media Classic文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) ，以了解有关在公开资产之前测试资产的更多信息。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 选择 **[!UICONTROL 确定]**.

启用“安全预览”表示资产会被推送到未发布的安全预览服务器。

查看 **[!UICONTROL 安全预览]** 启用后，在Experience Manager中导航到页面上的Dynamic Media Classic组件。 选择&#x200B;**[!UICONTROL 编辑]**。资产的URL中列出了安全预览服务器。 在Experience Manager中发布后，文件引用中的服务器域将从预览URL更新为生产URL。

### 为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm}

需要为WCM启用Dynamic Media Classic，原因有二：

* 它为页面创作启用了通用视频配置文件的下拉列表。 如果没有这个列表， **[!UICONTROL 通用视频预设]** 下拉列表为空，无法设置。
* 如果某个数字资产不在目标文件夹中，则在页面属性中为该页面启用Dynamic Media Classic时，您可以将该资产上传到Dynamic Media Classic。 然后，将资产拖放到Dynamic Media Classic组件上。 适用常规继承规则（即子页面从父页面继承配置）。

为WCM启用Dynamic Media Classic时，与其他配置一样，会应用继承规则。 您可以在触屏优化或经典用户界面中为WCM启用Dynamic Media Classic。

#### 在触屏优化用户界面中为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. 选择Experience Manager图标并导航到 **[!UICONTROL 站点]**，则是网站的根页面（不特定于语言）。

1. 在工具栏中，选择 [!UICONTROL 设置] 图标，选择 **[!UICONTROL 打开属性]**.

1. 选择 **[!UICONTROL Cloud Services]** 选择 **[!UICONTROL 添加配置]** 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在 **[!UICONTROL Adobe Dynamic Media Classic]** 下拉列表中，选择所需的配置，然后选择 **[!UICONTROL 确定]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   该Dynamic Media Classic配置中的视频预设可用于与该页面和子页面上的Dynamic Media Classic视频组件Experience Manager。

#### 在经典用户界面中为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. 在Experience Manager中，选择 **[!UICONTROL 网站]** 并导航到网站的根页面（不特定于语言）。

1. 在Sidekick中，选择 **[!UICONTROL 页面]** 图标，选择 **[!UICONTROL 页面属性]**.

1. 选择 **[!UICONTROL Cloud Services]** > **[!UICONTROL 添加服务]** > **[!UICONTROL Dynamic Media Classic]**.
1. 在 **[!UICONTROL Adobe Dynamic Media Classic]** 下拉列表中，选择所需的配置，然后选择 **[!UICONTROL 确定]**.

   该Dynamic Media Classic配置中的视频预设可用于与该页面和子页面上的Dynamic Media Classic视频组件Experience Manager。

### 配置默认配置 {#configuring-a-default-configuration}

如果您有多个Dynamic Media Classic配置，则可以指定其中一个配置作为Dynamic Media Classic内容浏览器的默认配置。

在给定时间，只能将一个Dynamic Media Classic配置标记为默认配置。 默认配置是默认在Dynamic Media Classic内容浏览器中显示的公司资产。

**要配置默认配置，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择 **[!UICONTROL 编辑]**.

1. 在 **[!UICONTROL 常规]** 选项卡，选择 **[!UICONTROL 默认配置]** 复选框，使其成为在Dynamic Media Classic内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，请选择 **[!UICONTROL 默认配置]** 复选框无效。

### 配置临时文件夹 {#configuring-the-ad-hoc-folder}

当资产不在CQ目标文件夹中时，您可以配置在Dynamic Media Classic中将资产上传到的按需文件夹。 请参阅从CQ目标文件夹外部发布资产。

**要配置临时文件夹，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择 **[!UICONTROL 编辑]**.

1. 选择 **[!UICONTROL 高级]** 选项卡。 在 **[!UICONTROL 临时文件夹]** 字段，您可以修改 **临时** 文件夹。 默认情况下， **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用视频预设 {#configuring-universal-presets}

要为视频组件配置通用视频预设，请参阅 [视频](/help/assets/s7-video.md).

## 启用基于MIME类型的Assets/Dynamic Media Classic上传作业参数支持 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用可配置的Dynamic Media Classic上传作业参数，这些作业参数是由Digital Asset Manager/Dynamic Media Classic资产同步触发的。

具体而言，您可以在“Experience ManagerWeb控制台配置”面板的OSGi（打开服务网关方案）区域中按MIME类型配置已接受的文件格式。 然后，您可以自定义在JCR(Java™内容存储库)中用于每个MIME类型的单个上传作业参数。

**要启用基于MIME类型的资产，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Adobe Experience Manager Web控制台配置面板中， **[!UICONTROL OSGi]** 菜单，选择 **[!UICONTROL 配置]**.
1. 在“名称”列下，查找并选择 **[!UICONTROL Adobe CQ Dynamic Media Classic资产MIME类型服务]** 以编辑配置。
1. 在Mime类型映射区域中，选择任意加号(+)以添加MIME类型。

   请参阅 [支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types).

1. 在文本字段中，键入新的MIME类型名称。

   例如，您需要键入 `<file_extension>=<mime_type>` as in `EPS=application/postscript` 或 `PSD=image/vnd.adobe.photoshop`.

1. 在配置窗口的右下角，选择 **[!UICONTROL 保存]**.
1. 返回到Experience Manager，然后在左边栏中选择 **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite页面的左边栏中，导航到 `/etc/cloudservices/scene7/<environment>` （替换） `<environment>` )。
1. 展开 `<environment>` （替换） `<environment>` )以显示 `mimeTypes` 节点。
1. 选择您刚才添加的mimeType。

   例如， `mimeTypes > application_postscript` 或 `mimeTypes > image_vnd.adobe.photoshop`.

1. 在CRXDE Lite页面的右侧，选择 **[!UICONTROL 属性]** 选项卡。
1. 在 **[!UICONTROL jobParam]** 值字段。

   例如：`psprocess="rasterize"&psresolution=120`。

   请参阅 [Adobe Dynamic Media Classic图像生产系统API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) 要获取更多上传作业参数，您可以使用。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且要将它们作为带有层提取的模板进行处理，请在 **[!UICONTROL jobParam]** 值字段：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >确保您的PSD文件具有“层”。 如果图像是严格意义上的一个图像或带有蒙版的图像，则会将其作为图像进行处理，因为没有要处理的图层。

1. 在CRXDE Lite页面的左上角，选择 **[!UICONTROL 全部保存]**.

## Dynamic Media Classic与Experience Manager集成故障诊断 {#troubleshooting-scene-and-aem-integration}

如果您在将Experience Manager与Dynamic Media Classic集成时遇到问题，请参阅以下解决方案情景。

**如果将数字资产发布到Dynamic Media Classic失败：**

* 检查您上传的资产是否位于 **[!UICONTROL CQ目标]** 文件夹(您可以在Dynamic Media Classic云配置中指定此文件夹)。
* 如果不是，则必须在 **[!UICONTROL 页面属性]** ，以便允许将上传到 **[!UICONTROL CQ临时]** 文件夹。

* 检查日志以了解任何信息。

**如果您的视频预设未显示：**

* 确保您已通过 **[!UICONTROL 页面属性]**. 视频预设在Dynamic Media Classic视频组件中可用。

**如果您的视频资产未在Experience Manager中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media Classic视频组件与基础视频组件不同。 请参阅 [基础视频组件与Dynamic Media Classic视频组件](/help/assets/s7-video.md).

**如果Experience Manager中的新资产或已修改资产不会自动上传到Dynamic Media Classic:**

* 确保资产位于CQ目标文件夹中。 只会自动更新CQ目标文件夹中的资产(前提是您将Experience Manager Assets配置为自动上传资产)。
* 确保您已将Cloud Services配置配置为启用自动上传，并且您已更新并保存DAM资产工作流，以包含Dynamic Media Classic上传。
* 将图像上传到Dynamic Media Classic目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资产的名称（无论位置如何）都是唯一的。 否则，将删除主目标文件夹中的资产，并且只保留子文件夹中的资产。
   * 更改Dynamic Media Classic覆盖Dynamic Media Classic帐户“设置”区域中资产的方式。 如果您在子文件夹中使用具有相同名称的资产，则无论您在何处使用，都不要将Dynamic Media Classic设置为覆盖资产。

**如果已删除的资产或文件夹未在Dynamic Media Classic和Experience Manager之间同步：**

* 在Experience Manager Assets中删除的资产和文件夹仍会显示在Dynamic Media Classic的同步文件夹中。 手动删除它们。

**如果视频上传失败：**

* 如果您的视频上传失败，并且您正在使用Experience Manager通过Dynamic Media Classic集成对视频进行编码，请参阅 [向Dynamic Media Classic上传工作流添加可配置的超时](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资产可能需要较长时间，才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定的资产不太多的文件夹。 例如，根文件夹的资产通常过多。
>
>如果要测试集成，请让根文件夹仅指向子文件夹，而不是整个公司。
