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

Adobe Dynamic Media Classic是一个托管解决方案，用于管理、增强、发布富媒体资产，并将其交付到Web、移动设备、电子邮件和连接到Internet的显示和打印。

要使用Dynamic Media Classic，您必须配置云配置，以便Dynamic Media Classic和Adobe Experience Manager资产可以相互交互。 本文档介绍了如何配置Experience Manager和Dynamic Media Classic。

有关在页面上使用所有Dynamic Media Classic组件以及使用视频的信息，请参阅 [使用Dynamic Media Classic](../assets/scene7.md).

>[!NOTE]
>
>* Dynamic Media Classic的DHTML查看器平台于2014年1月31日正式终止使用。 欲了解更多信息，请参见 [DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* 在配置Dynamic Media Classic以使用Experience Manager之前，请参阅 [最佳实践](#best-practices-for-integrating-scene-with-aem) 用于将Dynamic Media Classic与Experience Manager集成。
>* 如果您将Dynamic Media Classic与自定义代理配置一起使用，则必须同时配置HTTP客户端代理配置，因为Experience Manager的某些功能使用3.x API，而其他功能使用4.x API。 3.x配置有 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 和4.x配置了 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>


## Experience Manager/Dynamic Media Classic集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager用户可以在两种解决方案之间进行选择，以便与Dynamic Media一起使用。 您可以使用以下选项之一：

* 将Experience Manager实例与Dynamic Media Classic集成。
* 使用集成到Experience Manager中的Dynamic Media。

使用以下标准来确定要选择的解决方案：

* 您是 **现有** 资产驻留在Dynamic Media Classic中用于发布和交付的Dynamic Media Classic客户，但是您想要将这些资产与Sites (WCM)创作或Experience Manager Assets（或两者）集成？ 如果是这样的话，请使用 [Experience Manager/Dynamic Media Classic点对点集成](#aem-scene-point-to-point-integration) 本文档中有相关说明。

* 如果您是 **新** Experience Manager具有富媒体投放需求的客户，请选择 [Dynamic Media选项](#aem-dynamic-media). 如果您没有现有的S7帐户且系统中存储了许多资产，则此选项最有意义。

* 在某些情况下，请同时使用这两种解决方案。 此 [两用方案](/help/sites-administering/scene7.md#dual-use-scenario) 描述了该方案。

### Experience Manager/Dynamic Media Classic点对点集成 {#aem-scene-point-to-point-integration}

在此解决方案中使用资产时，需要执行以下操作之一：

* 将资源直接上传到Dynamic Media Classic，然后通过 **Dynamic Media Classic** 用于页面创作或的内容浏览器
* 上传到Experience Manager Assets，然后启用自动发布到Dynamic Media Classic；您可通过以下方式访问 **资产** 用于页面创作的内容浏览器

您用于此集成的组件位于 **Dynamic Media Classic** 中的组件区域 [设计模式](/help/sites-authoring/author-environment-tools.md#page-modes).

### Experience ManagerDynamic Media {#aem-dynamic-media}

Dynamic MediaExperience Manager是直接在Experience Manager平台中统一的Dynamic Media Classic功能。

在此解决方案中使用资产时，请遵循以下工作流程：

1. 将单个图像和视频资源直接上传到Experience Manager。
1. 直接在Experience Manager中对视频进行编码。
1. 直接在Experience Manager中构建基于图像的集。
1. 如果适用，请为图像或视频添加交互性。

您用于Dynamic Media的组件位于 **[!UICONTROL Dynamic Media]** 中的组件区域 [设计模式](/help/sites-authoring/author-environment-tools.md#page-modes). 它们包括：

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]** 组件是智能的 — 根据您添加的是图像还是视频，您拥有各种选项。 该组件支持图像预设、基于图像的查看器（如图像集、旋转集、混合媒体集和视频）。 此外，查看器可响应 — 屏幕大小根据屏幕大小自动更改。 所有查看者都是HTML5的查看者。

* **[!UICONTROL 交互式媒体]** - **[!UICONTROL 交互式媒体]** 组件用于轮播横幅、交互式图像和交互式视频等资产。 此类资源具有交互性，例如热点或图像映射。 此组件是智能的。 也就是说，根据您添加的是图像还是视频，您有各种不同的选项。 此外，查看器可响应 — 屏幕大小根据屏幕大小自动更改。 所有查看者都是HTML5的查看者。

### 两用方案 {#dual-use-scenario}

开箱即用后，您可以同时使用Dynamic Media和Dynamic Media Classic的Experience Manager集成功能。 以下用例表描述了何时打开和关闭某些区域。

要同时使用Dynamic Media和Dynamic Media Classic，请执行以下操作：

1. 配置 [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) 在Cloud Services中。
1. 按照用例的特定说明进行操作：

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
    <td><strong>从Assets自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>不熟悉Sites和Dynamic Media</td>
    <td>将资源上传到Experience Manager，并使用Experience ManagerDynamic Media组件在站点页面上创作资源</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>零售业中，以及初次接触网站和Dynamic Media</td>
    <td>将非产品资源上传到Experience Manager以进行管理和交付。 将产品资产上传到Dynamic Media Classic，并使用Experience Manager和组件中的Dynamic Media Classic内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>初次使用Assets和Dynamic Media</td>
    <td>将资源上传到Experience Manager Assets并使用从Dynamic Media发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>刚开始使用Dynamic Media和模板</td>
    <td>使用Dynamic Media进行成像和视频。 在Dynamic Media Classic中创作图像模板，并使用Dynamic Media Classic内容查找器在Sites页面中包含模板。</td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，并且是网站的新用户</td>
    <td>将资源上传到Dynamic Media Classic并使用Experience ManagerDynamic Media Classic内容浏览器在站点页面上搜索和创作资源</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，并且是Sites和Assets的新客户</td>
    <td>将资源上传到DAM并自动发布到Dynamic Media Classic以进行交付。 使用Experience ManagerDynamic Media Classic内容浏览器在站点页面上搜索和创作资源。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和不熟悉Assets</td>
    <td><p>将资源上传到Experience Manager并使用Dynamic Media生成演绎版以供下载/共享。 自动将Experience Manager资源发布到Dynamic Media Classic以进行交付。</p> <p><strong>重要提示：</strong> 发生重复处理，在Experience Manager中生成的演绎版不会同步到Dynamic Media Classic</p> </td>
    <td><p>开启</p> <p>（请参阅步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（请参阅步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. （可选；请参阅用例表） — 设置 [Dynamic Media云配置](/help/assets/config-dynamic.md) 和 [启用Dynamic Media服务器](/help/assets/config-dynamic.md).
1. （可选；请参阅用例表） — 如果选择启用从Assets自动上传到Dynamic Media Classic，则必须添加以下内容：

   1. 设置自动上传至Dynamic Media Classic。
   1. 添加 **Dynamic Media Classic上传** 执行所有Dynamic Media工作流步骤后的步骤 *在* **Dam更新资产** 工作流( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. （可选）在中按MIME类型限制Dynamic Media Classic资源上传 [https://&lt;server>：&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). 此列表中没有的资源MIME类型不会上传到Dynamic Media Classic服务器。
   1. （可选）在Dynamic Media Classic配置中设置视频。 您可以同时为Dynamic Media和Dynamic Media Classic或两者启用视频编码。 动态演绎版用于在Experience Manager实例中本地预览和播放，而Dynamic Media Classic视频演绎版则生成并存储在Dynamic Media Classic服务器上。 为Dynamic Media和Dynamic Media Classic设置视频编码服务时，请应用 [视频处理配置文件](/help/assets/video-profiles.md) 到Dynamic Media Classic资源文件夹。
   1. （可选） [在Dynamic Media Classic中配置安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### 限制 {#limitations}

当您同时启用Dynamic Media Classic和Dynamic Media时，存在以下限制：

* 通过选择资源并将其拖动到Experience Manager页面上的Dynamic Media Classic组件来手动上传到Dynamic Media Classic不起作用。
* 即使在Assets中编辑资产时，Experience Manager-Dynamic Media Classic同步的资产会自动更新到Dynamic Media Classic，但回滚操作不会触发新的上传。 因此，Dynamic Media Classic不会在回滚后立即获取最新版本。 解决方法是在回滚完成后再次编辑。
* 您是否需要将Dynamic Media用于一个用例，将Dynamic Media Classic集成用于另一个用例，以便Dynamic Media资源不会与Dynamic Media Classic系统交互？ 如果是这样的话，请不要将Dynamic Media Classic配置应用到Dynamic Media文件夹。 此外，请勿将Dynamic Media配置（处理配置文件）应用于Dynamic Media Classic文件夹。

## 将Dynamic Media Classic与Experience Manager集成的最佳实践 {#best-practices-for-integrating-scene-with-aem}

将Dynamic Media Classic与Experience Manager集成时，必须遵守以下方面的一些重要最佳实践：

* 测试推动您的集成
* 建议在某些情况下直接从Dynamic Media Classic上传资源

参见 [已知限制](#known-limitations-and-design-implications).

### 试用您的集成 {#test-driving-your-integration}

Adobe建议通过让根文件夹仅指向子文件夹而不是指向整个公司来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定一个没有太多资源的文件夹（例如，根文件夹通常有太多资源，可能会使系统崩溃）。

### 从Experience Manager Assets上传资源还是从Dynamic Media Classic上传资源 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用Assets（数字资源管理）功能或通过Dynamic Media Classic内容浏览器直接在Experience Manager中访问Dynamic Media Classic来上传资源。 您选择哪种方式取决于以下因素：

* 必须通过Dynamic Media Classic内容浏览器，直接从Dynamic Media Classic将Experience Manager Assets尚不支持的Dynamic Media Classic资源类型添加到Experience Manager网站。 例如，图像模板。
* 对于Experience Manager Assets和Dynamic Media Classic都支持的资源类型，如何上传它们取决于以下因素：

   * 当前资产所在的位置，以及
   * 在通用存储库中管理这些组件有多重要

假定资源已存在于Dynamic Media Classic中，在公共存储库中管理这些资源并不重要。 如果是这种情况，那么将资产导出到Experience Manager Assets只是为了将它们同步回Dynamic Media Classic以进行交付是不必要的往返测试。 Adobe建议您将资源保留在单个存储库中，并同步到Dynamic Media Classic以便仅进行交付。

## 配置Dynamic Media Classic集成 {#configuring-scene-integration}

您可以配置Experience Manager以将资源上传到Dynamic Media Classic。 可以将CQ目标文件夹中的资源（自动或手动）从Experience Manager上传到Dynamic Media Classic公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media Classic资源。 驻留在目标文件夹之外的数字资源只能在已启用Dynamic Media Classic配置的页面上的Dynamic Media Classic组件中使用。 此外，它们还被放在Dynamic Media Classic的按需文件夹中。 按需文件夹未与Experience Manager同步(但资产可在Dynamic Media Classic内容浏览器中发现)。

**要配置Dynamic Media Classic以与Experience Manager集成，请执行以下操作：**

1. [定义云配置](#creating-a-cloud-configuration-for-scene)  — 定义Dynamic Media Classic文件夹和Assets文件夹之间的映射。 即使您只想进行单向(Experience Manager Assets到Dynamic Media Classic)同步，也请完成此步骤。
1. [启用 **Adobe CQ s7dam Dam侦听器**](#enabling-the-adobe-cq-scene-dam-listener)  — 在中完成 [!UICONTROL osgi] 控制台。
1. 如果您希望Experience Manager Assets自动上传到Dynamic Media Classic，则必须打开该选项并将Dynamic Media Classic添加到 [!UICONTROL DAM更新资产] 工作流。 您还可以手动上传资产。
1. 将Dynamic Media Classic组件添加到Sidekick。 此功能允许用户在其Experience Manager页面上使用Dynamic Media Classic组件。
1. [将配置映射到Experience Manager中的页面](#enabling-scene-for-wcm)  — 查看您在Dynamic Media Classic中创建的任何视频预设时需要此步骤。 如果您必须从CQ目标文件夹外部执行资产发布到Dynamic Media Classic，也需要使用该字段。

本节介绍如何执行所有这些步骤，并列出重要限制。

### Dynamic Media Classic和Experience Manager Assets之间的同步的工作原理 {#how-synchronization-between-scene-and-aem-assets-works}

在设置Experience Manager Assets和Dynamic Media Classic同步时，请务必了解以下信息：

#### 从Experience Manager Assets上传到Dynamic Media Classic {#uploading-to-scene-from-aem-assets}

* Experience Manager中有一个指定的同步文件夹用于Dynamic Media Classic上传。
* 如果将数字资源放在指定的同步文件夹中，则可以自动上传到Dynamic Media Classic。
* Experience Manager中的文件夹和子文件夹结构在Dynamic Media Classic中进行复制。

>[!NOTE]
>
>Experience Manager在将所有元数据上传到Dynamic Media Classic之前将其嵌入为XMP，因此元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。

#### 已知限制和设计含义 {#known-limitations-and-design-implications}

在Experience Manager Assets和Dynamic Media Classic之间同步时，当前存在以下限制/设计影响：

<table>
 <tbody>
  <tr>
   <td><strong>限制/设计影响</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步（目标）文件夹</td>
   <td>在Dynamic Media Classic上传的Experience Manager中，每个公司只能有一个指定的文件夹。 如果您必须有权访问Dynamic Media Classic中的多个公司帐户，则可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果删除与资源同步的文件夹，则将删除所有Dynamic Media Classic远程资源，但保留文件夹。</td>
  </tr>
  <tr>
   <td>按需文件夹</td>
   <td>位于Target文件夹以外、手动上传到WCM中的Dynamic Media Classic的资产会自动放置在Dynamic Media Classic上的单独按需文件夹中。 您可以在Experience Manager的云配置中配置此文件夹。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集显示在Experience Manager中，但Experience Manager不支持它们。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media Classic中的eCatalogs生成的PDF将导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在Experience Manager和Dynamic Media Classic之间同步时，请确保刷新用户界面以查看更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果通过Dynamic Media Classic将视频上传到Experience Manager Assets进行编码，则视频缩略图和已编码视频可能需要一段时间才能在Experience Manager Assets中使用，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>目标子文件夹</td>
   <td><p>如果您在目标文件夹中使用子文件夹，请确保为每个资源使用唯一的名称（不考虑位置）。 此外，请确保将Dynamic Media Classic（在“设置”区域中）配置为不覆盖资源，而不考虑位置。</p> <p>否则，虽然会上传上传与Dynamic Media Classic目标子文件夹同名的资源，但会删除目标文件夹中的同名资源。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic服务器 {#configuring-scene-servers}

如果您在代理后运行Experience Manager或具有特殊的防火墙设置，则必须明确启用不同地区的主机。 服务器在内容中进行管理 `/etc/cloudservices/scene7/endpoints` 并且可以根据需要进行自定义。 选择一个URL，然后进行编辑以更改该URL（如有必要）。 在Experience Manager的早期版本中，这些值进行了硬编码。

如果您导航到 `/etc/cloudservices/scene7/endpoints.html`，您会看到列出的服务器（可以通过点按URL来编辑它们）：

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media Classic创建云配置 {#creating-a-cloud-configuration-for-scene}

云配置定义Dynamic Media Classic文件夹和Experience Manager Assets文件夹之间的映射。 必须将其配置为将Experience Manager Assets与Dynamic Media Classic同步。 有关更多信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定一个没有太多资源的文件夹。 例如，根文件夹通常包含太多资产。
>
>如果要测试集成，请将根文件夹仅指向子文件夹，而不是指向整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示一家Dynamic Media Classic公司的一名用户。 如果要访问其他Dynamic Media Classic公司或用户，则必须创建多个配置。

**要为Dynamic Media Classic创建云配置，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]** 以便访问Adobe Dynamic Media Classic。

1. 选择 **[!UICONTROL 立即配置]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在 **[!UICONTROL 标题]** 字段，并可选择在 **[!UICONTROL 名称]** 字段中，输入相应的信息。 选择&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >创建更多配置时， **[!UICONTROL 父配置]** 字段显示。
   >
   >Do **非** 更改父配置。 更改父配置可能会破坏集成。

1. 输入Dynamic Media Classic帐户的电子邮件地址、密码和区域，然后选择 **[!UICONTROL 连接到Dynamic Media Classic]**. 您已连接到Dynamic Media Classic服务器，并且对话框会展开并显示更多选项。

1. 输入 **[!UICONTROL 公司]** 名称和 **[!UICONTROL 根路径]**. 此信息是已发布的服务器名称以及您要指定的任何路径。 如果您不知道已发布的服务器名称，请在Dynamic Media Classic中转到 **[!UICONTROL 设置>应用程序设置]**)。

   >[!NOTE]
   >
   >Dynamic Media Classic根路径是Experience Manager连接到的Dynamic Media Classic文件夹。 可以将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media Classic文件夹的大小，导入根文件夹可能需要较长时间。 此外，Dynamic Media Classic数据可能会超过Experience Manager存储空间。 确保您正在导入正确的文件夹。 导入太多数据可能会导致系统停止。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 选择 **[!UICONTROL 确定]**. Experience Manager可保存您的配置。

>[!NOTE]
>
>如果您正在重新连接：
>
>* 在发布时重新连接到Dynamic Media Classic时，在发布或重新连接时重置密码不起作用（在创作实例上不是问题）。
>* 如果您修改了地区、公司名称等值，则必须重新连接到Dynamic Media Classic。 如果配置选项已被修改但未保存，则Experience Manager仍错误地指示配置有效。 确保重新连接。
>


### 启用Adobe CQ Dynamic Media Classic Dam侦听器 {#enabling-the-adobe-cq-scene-dam-listener}

启用Adobe CQ Dynamic Media Classic Dam侦听器，默认情况下该侦听器处于禁用状态。

**要启用Adobe CQ Dynamic Media Classic Dam侦听器，请执行以下操作：**

1. 选择 [!UICONTROL 工具] 图标，然后导航到 **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Web控制台中，导航到 **[!UICONTROL Adobe CQ Dynamic Media Classic Dam侦听器]** 并选择 **[!UICONTROL 已启用]** 复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 向Dynamic Media Classic上传工作流添加可配置超时 {#adding-configurable-timeout-to-scene-upload-workflow}

当Experience Manager实例配置为通过Dynamic Media Classic处理视频编码时，默认情况下，任何上传作业都有35分钟的超时时间。 要适应可能运行时间较长的视频编码作业，您可以配置此设置。

1. 导航到 **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在中根据需要更改数字 **[!UICONTROL 活动作业超时]** 字段。 任何非负数都可使用度量单位（以秒为单位）。 默认情况下，此数字设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资源最多可在几分钟内摄取（例如，图像）。 但在某些情况下（例如，较大的视频），超时值会增加到7200秒（两个小时），以适应较长的处理时间。 否则，此Dynamic Media Classic上载作业将标记为 **[!UICONTROL 上传失败]** 在JCR (Java™内容存储库)元数据中。

1. 选择&#x200B;**[!UICONTROL 保存]**。

### 从Experience Manager Assets自动上载 {#autouploading-from-aem-assets}

从Experience Manager6.3.2开始，对Experience Manager Assets进行了配置，以便上传的任何数字资源都更新到Dynamic Media Classic（如果资源位于CQ目标文件夹中）。

将资源添加到Experience Manager Assets后，该资源会自动上传并发布到Dynamic Media Classic。

>[!NOTE]
>
>从Experience Manager Assets自动上传到Dynamic Media Classic的最大文件大小为500 MB。

**要从Experience Manager Assets自动上载，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在Dynamic Media标题下的可用配置下，选择 **[!UICONTROL dms7 (Dynamic Media]**)。
1. 选择 **[!UICONTROL 高级]** 选项卡，选择 **[!UICONTROL 启用自动上传]** 复选框，然后选择 **[!UICONTROL 确定]**. 您现在必须配置DAM资产工作流以包含上传到Dynamic Media Classic的内容。

   >[!NOTE]
   >
   >参见 [配置推送到Dynamic Media Classic的资源状态（已发布/未发布）](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) 有关以未发布状态将资产推送到Dynamic Media Classic的信息。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回Experience Manager欢迎页面并选择 **[!UICONTROL 工作流]**. 双击 **DAM更新资产** 工作流，以使其打开。
1. 在sidekick中，导航到 **[!UICONTROL 工作流]** 组件，并选择 **[!UICONTROL Dynamic Media Classic]**. 拖动 **[!UICONTROL Dynamic Media Classic]** 到工作流并选择 **[!UICONTROL 保存]**. 添加到Experience Manager Assets目标文件夹中的资源会自动上传到Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动化后添加资源时，如果资源未放置在CQ目标文件夹中，则不会将其上传到Dynamic Media Classic。
   >* Experience Manager在将所有元数据上传到Dynamic Media Classic之前将其嵌入为XMP，因此元数据节点上的所有属性在Dynamic Media Classic as XMP中均可用。


### 配置推送到Dynamic Media Classic的资源状态（已发布/未发布） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果您要将资源从Experience Manager Assets推送到Dynamic Media Classic，则可以自动发布这些资源（默认行为），也可以将资源以未发布状态推送到Dynamic Media Classic。

如果要在上线前在暂存环境中测试资产，则可能不希望立即在Dynamic Media Classic上发布资产。 您可以将Experience Manager与Dynamic Media Classic的安全测试环境结合使用，以未发布状态将资产直接从Assets推送到Dynamic Media Classic。

Dynamic Media Classic资源仍可通过安全预览使用。 只有在Experience Manager中发布资源时，Dynamic Media Classic资源才会同时投入使用。

如果您要在将资源推送到Dynamic Media Classic时立即发布资源，则无需配置任何选项。 此功能是默认行为。

但是，如果您不希望推送到Dynamic Media Classic的资源自动发布，本节将介绍如何配置Experience Manager和Dynamic Media Classic以执行此操作。

#### 将资源推送到Dynamic Media Classic的先决条件已取消发布 {#prerequisites-to-push-assets-to-scene-unpublished}

在将资源推送到Dynamic Media Classic而不发布它们之前，您必须设置以下设置：

1. [使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). 在您的支持案例中，请求为您的Dynamic Media Classic帐户启用安全预览。
1. [为您的Dynamic Media Classic帐户设置安全预览](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

这些步骤与在Dynamic Media Classic中创建任何安全测试设置时要执行的步骤相同。

>[!NOTE]
>
>如果您的安装环境是UNIX® 64位操作系统，请参见 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) 关于您必须设置的其他配置选项。

#### 推送处于未发布状态的资产的已知限制  {#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在Experience Manager中发布并创建了后续版本，则会立即将该新版本实时发布到生产环境。 激活时发布仅适用于资产的初始发布。

>[!NOTE]
>
>如果要立即发布资产，最佳实践是保留 **[!UICONTROL 启用安全预览]** 设置为 **[!UICONTROL 立即]** 并使用 **[!UICONTROL 启用自动上传]** 功能。

### 将推送到Dynamic Media Classic的资产状态设置为未发布 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在Experience Manager中发布资源，则会自动将S7资源触发到生产/实时资源（资源不再处于安全预览/取消发布状态）。

**要将推送到Dynamic Media Classic的资产状态设置为未发布，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 选择 **[!UICONTROL 高级]** 选项卡。
1. 在 **[!UICONTROL 启用安全视图]** 下拉菜单，选择 **[!UICONTROL 根据AEM发布激活]** 将资产推送到Dynamic Media Classic而不发布。 (默认情况下，此值设置为 **[!UICONTROL 立即]**，立即发布Dynamic Media Classic资源。)

   参见 [Dynamic Media Classic文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) 有关在公开资产之前测试资产的更多信息。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 选择 **[!UICONTROL 确定]**.

启用“安全预览”意味着您的资产会推送到未发布的安全预览服务器。

查看是否 **[!UICONTROL 安全预览]** 启用，在Experience Manager中导航到页面上的Dynamic Media Classic组件。 选择&#x200B;**[!UICONTROL 编辑]**。资产的URL中列出了安全预览服务器。 在Experience Manager中发布后，文件引用中的服务器域将从预览URL更新为生产URL。

### 为WCM启用Dynamic Media Classic {#enabling-scene-for-wcm}

出于以下两个原因，需要为WCM启用Dynamic Media Classic：

* 它启用通用视频配置文件的下拉列表以进行页面创作。 如果没有此列表， **[!UICONTROL 通用视频预设]** 下拉列表为空，无法设置。
* 如果数字资源不在目标文件夹中，且您在页面属性中为该页面启用了Dynamic Media Classic，则可以将资源上传到Dynamic Media Classic。 然后将资源拖放到Dynamic Media Classic组件上。 应用常规继承规则（即子页面继承父页面的配置）。

与其他配置一样，为WCM启用Dynamic Media Classic时，将应用继承规则。 您可以在触控优化用户界面或经典用户界面中启用适用于WCM的Dynamic Media Classic。

#### 在触控优化用户界面中启用适用于WCM的Dynamic Media Classic {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. 选择Experience Manager图标并导航到 **[!UICONTROL 站点]**，则为网站的根页面（非特定语言）。

1. 在工具栏中，选择 [!UICONTROL 设置] 图标并选择 **[!UICONTROL 打开属性]**.

1. 选择 **[!UICONTROL Cloud Services]** 并选择 **[!UICONTROL 添加配置]** 并选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在 **[!UICONTROL Adobe Dynamic Media Classic]** 下拉列表，选择所需的配置并选择 **[!UICONTROL 确定]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   来自该Dynamic Media Classic配置的视频预设可用于与该页面及其子页面上的Dynamic Media Classic视频组件Experience Manager。

#### 在Classic用户界面中启用Dynamic Media Classic for WCM {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. 在Experience Manager中，选择 **[!UICONTROL 网站]** 和导航到网站的根页面（非特定语言）。

1. 在助手中，选择 **[!UICONTROL 页面]** 图标并选择 **[!UICONTROL 页面属性]**.

1. 选择 **[!UICONTROL Cloud Services]** > **[!UICONTROL 添加服务]** > **[!UICONTROL Dynamic Media Classic]**.
1. 在 **[!UICONTROL Adobe Dynamic Media Classic]** 下拉列表，选择所需的配置并选择 **[!UICONTROL 确定]**.

   来自该Dynamic Media Classic配置的视频预设可用于与该页面及其子页面上的Dynamic Media Classic视频组件Experience Manager。

### 配置默认配置 {#configuring-a-default-configuration}

如果您有多个Dynamic Media Classic配置，则可以指定其中一个配置作为Dynamic Media Classic内容浏览器的默认值。

在给定时刻，只能将一个Dynamic Media Classic配置标记为默认。 默认配置是默认显示在Dynamic Media Classic内容浏览器中的公司资源。

**配置默认配置：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择 **[!UICONTROL 编辑]**.

1. 在 **[!UICONTROL 常规]** 选项卡，选择 **[!UICONTROL 默认配置]** 复选框，以使其成为Dynamic Media Classic内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，请选择 **[!UICONTROL 默认配置]** 复选框不起作用。

### 配置临时文件夹 {#configuring-the-ad-hoc-folder}

您可以配置按需文件夹，当资产不在CQ目标文件夹中时，可在Dynamic Media Classic中将资产上传到该文件夹。 请参阅从CQ目标文件夹外部发布资产。

**要配置临时文件夹：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 选择 **[!UICONTROL Dynamic Media Classic]**.
1. 在Dynamic Media Classic中选择您的配置。
1. 要打开配置，请选择 **[!UICONTROL 编辑]**.

1. 选择 **[!UICONTROL 高级]** 选项卡。 在 **[!UICONTROL 临时文件夹]** 字段，则可以修改 **临时** 文件夹。 默认情况下，它是 **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用视频预设 {#configuring-universal-presets}

要为视频组件配置通用视频预设，请参阅 [视频](/help/assets/s7-video.md).

## 启用基于MIME类型的资产/Dynamic Media Classic上载作业参数支持 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用通过同步Digital Asset Manager/Dynamic Media Classic资源触发的可配置Dynamic Media Classic上传作业参数。

具体来说，您可以在Experience ManagerWeb控制台配置面板的OSGi (Open Service Gateway Initiative)区域中按MIME类型配置接受的文件格式。 然后，您可以自定义JCR (Java™内容存储库)中每个MIME类型使用的各个上载作业参数。

**要启用基于MIME类型的资产，请执行以下操作：**

1. 选择Experience Manager图标并导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在Adobe Experience Manager Web控制台的“配置”面板中， **[!UICONTROL osgi]** 菜单，选择 **[!UICONTROL 配置]**.
1. 在“名称”列下，查找并选择 **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME类型服务]** 以编辑配置。
1. 在MIME类型映射区域，选择任意加号(+)以添加MIME类型。

   参见 [支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types).

1. 在文本字段中，键入新的MIME类型名称。

   例如，您可以键入 `<file_extension>=<mime_type>` as in `EPS=application/postscript` 或 `PSD=image/vnd.adobe.photoshop`.

1. 在配置窗口的右下角，选择 **[!UICONTROL 保存]**.
1. 返回到Experience Manager，然后在左边栏中，选择 **[!UICONTROL CRXDE Lite]**.
1. 在“CRXDE Lite”页面的左边栏中，导航到 `/etc/cloudservices/scene7/<environment>` (替换 `<environment>` 实际名称)。
1. 展开 `<environment>` (替换 `<environment>` （实际名称）以显示 `mimeTypes` 节点。
1. 选择您刚刚添加的mimeType。

   例如， `mimeTypes > application_postscript` 或 `mimeTypes > image_vnd.adobe.photoshop`.

1. 在“CRXDE Lite”页面的右侧，选择 **[!UICONTROL 属性]** 选项卡。
1. 在中指定Dynamic Media Classic上载作业参数 **[!UICONTROL jobParam]** 值字段。

   例如， `psprocess="rasterize"&psresolution=120` .

   请参阅 [Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) 有关更多可以使用的上载作业参数，请参阅此处。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且希望将它们作为模板与图层提取一起处理，请在 **[!UICONTROL jobParam]** 值字段：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >确保PSD文件具有“图层”。 如果它严格是一个图像或带有蒙版的图像，则它作为图像处理，因为没有要处理的图层。

1. 在“CRXDE Lite”页面的左上角，选择 **[!UICONTROL 全部保存]**.

## Dynamic Media Classic与Experience Manager集成故障诊断 {#troubleshooting-scene-and-aem-integration}

如果您在将Experience Manager与Dynamic Media Classic集成时遇到问题，请参阅以下解决方案方案。

**如果向Dynamic Media Classic发布数字资源失败，请执行以下操作：**

* 检查您上传的资产是否位于 **[!UICONTROL CQ目标]** 文件夹(您在Dynamic Media Classic云配置中指定此文件夹)。
* 如果不是，则必须在中配置云配置 **[!UICONTROL 页面属性]** ，以允许上传至 **[!UICONTROL CQ即席]** 文件夹。

* 查看日志以了解任何信息。

**如果您的视频预设未显示：**

* 确保您已通过配置该页面的云配置 **[!UICONTROL 页面属性]**. 视频预设在Dynamic Media Classic视频组件中可用。

**如果您的视频资源未在Experience Manager中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media Classic视频组件与foundation视频组件不同。 参见 [Foundation视频组件与Dynamic Media Classic视频组件](/help/assets/s7-video.md).

**如果Experience Manager中的新资源或修改后的资源没有自动上传到Dynamic Media Classic：**

* 确保资产位于CQ目标文件夹中。 只有位于CQ目标文件夹中的资源才会自动更新(前提是您已将Experience Manager Assets配置为自动上传资源)。
* 确保您已将Cloud Services配置配置为启用自动上传，并且已更新并保存DAM资源工作流以包含Dynamic Media Classic上传。
* 将图像上传到Dynamic Media Classic目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资源的名称（无论位于何处）都是唯一的。 否则，主目标文件夹中的资产将被删除，并且仅保留子文件夹中的资产。
   * 在Dynamic Media Classic帐户的“设置”区域中更改Dynamic Media Classic覆盖资产的方式。 如果在子文件夹中使用同名的资源，请勿将Dynamic Media Classic设置为覆盖任何位置的资源。

**如果您删除的资源或文件夹未在Dynamic Media Classic和Experience Manager之间同步，请执行以下操作：**

* 在Experience Manager Assets中删除的资产和文件夹仍会显示在Dynamic Media Classic的同步文件夹中。 手动删除它们。

**如果视频上传失败：**

* 如果视频上传失败，并且您通过Dynamic Media Classic集成使用Experience Manager对视频进行编码，请参阅 [向Dynamic Media Classic上传工作流添加可配置超时](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 确保在Dynamic Media Classic中指定一个没有太多资源的文件夹。 例如，根文件夹通常包含太多资产。
>
>如果要测试集成，请将根文件夹仅指向子文件夹，而不是指向整个公司。
