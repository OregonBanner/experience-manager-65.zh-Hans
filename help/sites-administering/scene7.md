---
title: 与Dynamic Media Classic集成
description: 了解如何将Adobe Experience Manager与Dynamic Media Classic集成。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: d700510efb340598a7931647164e22d574884569
workflow-type: tm+mt
source-wordcount: '5517'
ht-degree: 1%

---


# 与Dynamic Media Classic {#integrating-with-dynamic-media-classic-scene}集成

Adobe Dynamic Media Classic是一个托管解决方案，用于管理、增强、发布富媒体资产并将富媒体资产交付到Web、移动设备、电子邮件和连接Internet的显示屏和印刷品。

要使用Dynamic Media Classic，您必须配置云配置，以便Dynamic Media Classic和Adobe Experience Manager资产能够相互交互。 本文档介绍如何配置Experience Manager和Dynamic Media Classic。

有关在页面上使用所有Dynamic Media Classic组件和处理视频的信息，请参阅[使用Dynamic Media Classic](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media Classic的DHTML查看器平台于2014年1月31日正式停止使用。 有关详细信息，请参阅[DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在配置Dynamic Media Classic以与Experience Manager结合使用之前，请参阅[将Dynamic Media Classic与Experience Manager集成的最佳实践](#best-practices-for-integrating-scene-with-aem)。
>* 如果将Dynamic Media Classic与自定义代理配置一起使用，则必须同时配置HTTP客户端代理配置，因为Experience Manager的某些功能使用3.x API，而其他功能使用4.x API。 3.x配置有[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient),4.x配置有[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)。

>



## Experience Manager/Dynamic Media Classic集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager用户可以在两种解决方案之间进行选择以与Dynamic Media结合使用。 您可以使用以下选项之一：

* 将您的Experience Manager实例与Dynamic Media Classic集成。
* 使用集成到Experience Manager中的Dynamic Media。

使用以下标准确定要选择的解决方案：

* 如果您是&#x200B;**现有** Dynamic Media Classic客户，其富媒体资源驻留在Dynamic Media Classic中用于发布和投放，但您希望将这些资源与站点(WCM)创作和/或Experience Manager资产集成以进行管理，请使用本文档中描述的[Experience Manager/Dynamic Media Classic点对点集成](#aem-scene-point-to-point-integration)。

* 如果您是&#x200B;**新** Experience Manager客户，且有富媒体投放需求，请选择[Dynamic Media选项](#aem-dynamic-media)。 如果您没有现有的S7帐户，并且该系统中存储了许多资源，则此选项最有意义。

* 在某些情况下，请同时使用这两种解决方案。 [双用方案](/help/sites-administering/scene7.md#dual-use-scenario)描述了该方案。

### Experience Manager/Dynamic Media Classic点对点集成{#aem-scene-point-to-point-integration}

在此解决方案中处理资产时，您需要执行以下操作之一：

* 将资源直接上传到Dynamic Media Classic，然后通过&#x200B;**Dynamic Media Classic**&#x200B;内容浏览器访问，以进行页面创作或
* 上传到Experience Manager资产，然后启用自动发布到Dynamic Media Classic;可通过&#x200B;**资产**&#x200B;内容浏览器进行页面创作

您用于此集成的组件位于[设计模式的&#x200B;**Dynamic Media Classic**&#x200B;组件区域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### Experience Manager Dynamic Media {#aem-dynamic-media}

Experience Manager Dynamic Media是Dynamic Media Classic功能在Experience Manager平台内直接统一的。

在此解决方案中处理资产时，您可以遵循以下工作流：

1. 将单个图像和视频资产直接上传到Experience Manager。
1. 在Experience Manager中直接对视频进行编码。
1. 直接在Experience Manager中构建基于图像的集。
1. 如果适用，为图像或视频添加交互性。

您用于Dynamic Media的组件位于[设计模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件区域。 它们包括：

* **[!UICONTROL Dynamic Media]**  — 动 **[!UICONTROL 态]** 媒体组件是智能的 — 根据您添加的是图像还是视频，您有各种选项。该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

* **[!UICONTROL 交互式媒体]**  — 交 **[!UICONTROL 互]** 式媒体组件用于资源，如传送横幅、交互式图像和交互式视频。此类资产在热点或图像地图中具有交互性。 此组件是智能的。 也就是说，根据您添加的是图像还是视频，您有各种选项。 此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

### 双用方案{#dual-use-scenario}

开箱即用，您可以同时使用Dynamic Media和Dynamic Media Classic的Experience Manager集成功能。 下表说明了在打开和关闭某些区域时的使用案例。

要同时使用Dynamic Media和Dynamic Media Classic:

1. 在Cloud Services中配置[Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)。
1. 请按照您的使用案例中特别具体的说明操作：

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
    <td><strong>图像/视频</strong></td>
    <td><strong>动态媒体组件</strong></td>
    <td><strong>S7内容浏览器和组件</strong></td>
    <td><strong>从资产自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>站点和Dynamic Media的新功能</td>
    <td>将资产上传到Experience Manager，然后使用Experience Manager Dynamic Media组件在站点页面上创作资产</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>在零售业，以及新到的站点和Dynamic Media</td>
    <td>将非产品资产上传到Experience Manager，以便进行管理和投放。 将产品资产上传到Dynamic Media Classic，然后使用Experience Manager和组件中的Dynamic Media Classic内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>资产和Dynamic Media</td>
    <td>将资产上传到Experience Manager资产，并使用Dynamic Media中发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>Dynamic Media和模板的新功能</td>
    <td>使用Dynamic Media进行成像和视频。 在Dynamic Media Classic中创作图像模板，并使用Dynamic Media Classic内容查找器将模板包含在“站点”页面中。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，不熟悉Sites</td>
    <td>将资产上传到Dynamic Media Classic并使用Experience Manager Dynamic Media Classic内容浏览器在站点页面上搜索和创作资产</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户，是站点和资产的新客户</td>
    <td>将资产上传到DAM并自动发布到Dynamic Media Classic以进行投放。 使用Experience Manager Dynamic Media Classic内容浏览器在站点页面上搜索和创作资产。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media Classic客户和新资产</td>
    <td><p>将资产上传到Experience Manager，然后使用Dynamic Media生成要下载/共享的演绎版。 自动将Experience Manager资源发布到Dynamic Media Classic以进行投放。</p> <p><strong>重要：在</strong> Experience Manager中生成的重复处理和演绎版未同步到Dynamic Media Classic</p> </td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可选；请参阅用例表) — 设置[Dynamic Media云配置](/help/assets/config-dynamic.md)和[启用Dynamic Media服务器](/help/assets/config-dynamic.md)。
1. (可选；请参阅用例表) — 如果您选择启用从资产自动上传到Dynamic Media经典，则必须添加以下内容：

   1. 设置自动上传到Dynamic Media Classic。
   1. 在&#x200B;***Dam更新资产**工作流(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)末尾的所有Dynamic Media工作流步骤*&#x200B;之后添加&#x200B;**Dynamic Media Classic upload**&#x200B;步骤
   1. （可选）按[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)中的MIME类型限制Dynamic Media经典资产上传。 此列表中未包含的资产MIME类型不会上传到Dynamic Media Classic服务器。
   1. （可选）在Dynamic Media Classic配置中设置视频。 您可以同时为Dynamic Media和Dynamic Media Classic启用视频编码。 动态演绎版用于在Experience Manager实例中本地预览和回放，而Dynamic Media Classic视频演绎版则生成并存储在Dynamic Media Classic服务器上。 在为Dynamic Media和Dynamic Media Classic设置视频编码服务时，将[视频处理用户档案](/help/assets/video-profiles.md)应用到Dynamic Media Classic资源文件夹。
   1. （可选）[在Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)中配置安全预览。

#### 限制 {#limitations}

启用Dynamic Media Classic和Dynamic Media后，有以下限制：

* 通过选择资产并将其拖动到Dynamic Media Classic组件(位于Experience Manager页面上)来手动上传到Dynamic Media Classic不起作用。
* 即使Experience Manager-Dynamic Media经典同步的资产在资产中进行编辑时会自动更新到Dynamic Media经典，回滚操作也不会触发新的上传。 因此，Dynamic Media Classic在回滚后不会立即获得最新版本。 解决方法是在回滚完成后再次编辑。
* 如果您必须将Dynamic Media用于一个用例，将Dynamic Media Classic集成用于另一个用例，以便Dynamic Media资源不会与Dynamic Media Classic系统交互，则请勿将Dynamic Media Classic配置应用到Dynamic Media文件夹。 此外，请勿将Dynamic Media配置(处理用户档案)应用到Dynamic Media Classic文件夹。

## 将Dynamic Media Classic与Experience Manager {#best-practices-for-integrating-scene-with-aem}集成的最佳实践

在将Dynamic Media Classic与Experience Manager集成时，必须在以下方面遵循一些重要的最佳实践：

* 测试驱动集成
* 对于某些情况，建议直接从Dynamic Media Classic上传资产

请参见[已知限制](#known-limitations-and-design-implications)。

### 测试集成{#test-driving-your-integration}

Adobe建议您通过让根文件夹仅指向子文件夹而不是整个公司来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 请确保在Dynamic Media Classic中指定一个资源不太多的文件夹（例如，根文件夹通常包含的资源太多，可能会导致系统崩溃）。

### 从Experience Manager资产上传资产与从Dynamic Media Classic {#uploading-assets-from-aem-assets-versus-from-scene}上传资产

您可以通过使用资产（数字资产管理）功能或通过Dynamic Media Classic内容浏览器直接以Experience Manager形式访问Dynamic Media Classic来上传资产。 您选择哪个取决于以下因素：

* Dynamic Media Classic资产尚不支持的Experience Manager经典资源类型必须通过Dynamic Media Classic内容浏览器直接从Dynamic Media Classic添加到Experience Manager网站。 例如，图像模板。
* 对于Experience Manager Assets和Dynamic Media Classic都支持的资产类型，确定如何上传取决于以下各项：

   * 当前资产所在的位置，
   * 在通用存储库中管理它们的重要性

如果资产已在Dynamic Media Classic中，并且在通用存储库中管理这些资产并不重要，则将这些资产导出到Experience Manager资产时，仅将其同步回Dynamic Media Classic进行投放是不必要的往返操作。 否则，最好将资产保留在单个存储库中并同步到Dynamic Media Classic以仅用于投放。

## 配置Dynamic Media Classic集成{#configuring-scene-integration}

您可以配置Experience Manager以将资产上传到Dynamic Media Classic。 可以从CQ目标文件夹将资产从Experience Manager上传（自动或手动）到Dynamic Media Classic公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media经典资产。 驻留在目标文件夹以外的数字资产只能用于启用Dynamic Media Classic配置的页面上的Dynamic Media Classic组件。 此外，它们还位于Dynamic Media Classic中的临时文件夹中。 临时文件夹未与Experience Manager同步(但资源可在Dynamic Media Classic内容浏览器中显示)。

要配置Dynamic Media Classic以与Experience Manager集成，您必须完成以下步骤：

1. [定义云配置](#creating-a-cloud-configuration-for-scene)  — 定义Dynamic Media Classic文件夹与Assets文件夹之间的映射。即使您只想单向(将资产Experience Manager到Dynamic Media Classic)同步，也可以完成此步骤。
1. [启用 **Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener)  — 在OSGiconsole中完  成。
1. 如果您希望Experience Manager资产自动上传到Dynamic Media Classic，则必须打开该选项，并将Dynamic Media Classic添加到[!UICONTROL DAM更新资产]工作流。 您还可以手动上传资产。
1. 将Dynamic Media经典组件添加到Sidekick。 此功能允许用户在其Experience Manager页面上使用Dynamic Media Classic组件。
1. [将配置映射到Experience Manager中的页面](#enabling-scene-for-wcm)  — 需要此步骤才能视图在Dynamic Media Classic中创建的任何视频预设。如果必须将资产从CQ目标文件夹外部发布到Dynamic Media Classic，则需要执行此操作。

本节介绍如何执行所有这些步骤和列表重要限制。

### Dynamic Media Classic和Experience Manager Assets之间的同步工作方式{#how-synchronization-between-scene-and-aem-assets-works}

在设置Experience Manager资产和Dynamic Media Classic同步时，请务必了解以下内容：

#### 从Dynamic Media资产{#uploading-to-scene-from-aem-assets}上载到Experience Manager Classic

* Dynamic Media Classic上载的Experience Manager中有一个指定的同步文件夹。
* 如果数字资产放在指定的同步文件夹中，则上传到Dynamic Media Classic的内容可以自动完成。
* Experience Manager中的文件夹和子文件夹结构将在Dynamic Media Classic中复制。

>[!NOTE]
>
>Experience Manager在将所有元数据上传到Dynamic Media Classic之前将其嵌入为XMP，因此，在Dynamic Media Classic XMP中，元数据节点上的所有属性都可用。

#### 已知限制和设计含义{#known-limitations-and-design-implications}

在Experience Manager资产和Dynamic Media Classic之间进行同步后，当前存在以下限制/设计含义：

<table>
 <tbody>
  <tr>
   <td><strong>限制/设计含义</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步(目标)文件夹</td>
   <td>对于Dynamic Media Classic上传，在Experience Manager中，每个公司只能有一个指定的文件夹。 如果您必须在Dynamic Media Classic中访问多个公司帐户，则可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果您删除包含资产的已同步文件夹，则所有Dynamic Media Classic远程资产都会被删除，但该文件夹仍会保留。</td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>位于WCM中手动上传到Dynamic Media Classic的目标文件夹外的资产将自动放置在Dynamic Media Classic上的单独的临时文件夹中。 您可以在Experience Manager的云配置中配置此文件夹。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集以Experience Manager显示，但在Experience Manager中不受支持。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media Classic中的eCatalogs生成的PDF导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在Experience Manager和Dynamic Media Classic之间同步时，请务必刷新用户界面以视图更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果将视频上传到Experience Manager资产以通过Dynamic Media Classic进行编码，则视频缩略图和编码视频可能需要一些时间才能在Experience Manager资产中使用，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>目标子文件夹</td>
   <td><p>如果您在目标文件夹中使用子文件夹，请确保对每个资产使用唯一的名称（无论位置如何），或者配置Dynamic Media Classic（在“设置”区域）以不覆盖资产，而不覆盖任何位置。</p> <p>否则，上传到Dynamic Media Classic目标子文件夹的同名资产会被上传，但目标文件夹中同名的资产会被删除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic服务器{#configuring-scene-servers}

如果在代理后运行Experience Manager或具有特殊的防火墙设置，则必须显式启用不同区域的主机。 服务器在`/etc/cloudservices/scene7/endpoints`中的内容中进行管理，并可以根据需要进行自定义。 点按一个URL，然后进行编辑以根据需要更改该URL。 在以前版本的Experience Manager中，这些值是硬编码的。

如果导航到`/etc/cloudservices/scene7/endpoints.html`，您会看到列出的服务器（并可通过点击URL编辑它们）：

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}创建云配置

云配置定义了Dynamic Media Classic文件夹与Experience Manager Assets文件夹之间的映射。 必须将其配置为将Experience Manager资产与Dynamic Media Classic同步。 有关详细信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 请确保在Dynamic Media Classic中指定一个资源不太多的文件夹。 例如，根文件夹通常包含的资源过多。
>
>如果要测试集成，请让根文件夹仅指向子文件夹，而不是整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示Dynamic Media Classic公司的一个用户。 如果要访问其他Dynamic Media Classic公司或用户，必须创建多个配置。

要配置Experience Manager以能够将资产发布到Dynamic Media Classic，请执行以下操作：

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**&#x200B;以访问Adobe Dynamic Media Classic。

1. 点按&#x200B;**[!UICONTROL 立即配置]**。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中，或者在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，输入相应的信息。 点按&#x200B;**[!UICONTROL 创建]**。

   >[!NOTE]
   >
   >创建更多配置时，将显示&#x200B;**[!UICONTROL 父配置]**&#x200B;字段。
   >
   >**不**&#x200B;更改父配置。 更改父配置可能会中断集成。

1. 输入Dynamic Media Classic帐户的电子邮件地址、密码和区域，然后点按&#x200B;**[!UICONTROL 连接到Dynamic Media Classic]**。 您已连接到Dynamic Media Classic服务器，该对话框将扩展为更多选项。

1. 输入&#x200B;**[!UICONTROL 公司]**&#x200B;名称和&#x200B;**[!UICONTROL 根路径]**。 此信息是已发布的服务器名称以及要指定的任何路径。 如果您不知道已发布的服务器名称，请在Dynamic Media Classic中，转至&#x200B;**[!UICONTROL 设置>应用程序设置]**)。

   >[!NOTE]
   >
   >Dynamic Media Classic根路径是Experience Manager连接到的Dynamic Media Classic文件夹路径。 可以将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media Classic文件夹的大小，导入根文件夹可能需要很长时间。 此外，Dynamic Media Classic数据可能超过Experience Manager存储。 请确保导入的文件夹正确。 导入过多数据可能会停止系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 单击&#x200B;**[!UICONTROL 确定]**。Experience Manager保存您的配置。

>[!NOTE]
>
>如果要重新连接：
>
>* 在发布时重新连接到Dynamic Media Classic时，在发布时重置口令或重新连接时无法正常工作（创作实例上不存在问题）。
>* 如果您修改了区域、公司名称等值，则必须重新连接到Dynamic Media Classic。 如果已修改但未保存配置选项，Experience Manager仍错误地指示配置有效。 请务必重新连接。

>



### 启用Adobe CQ Dynamic Media Classic Dam侦听器{#enabling-the-adobe-cq-scene-dam-listener}

启用Adobe CQ Dynamic Media Classic Dam侦听器，默认情况下处于禁用状态。

要启用Adobe CQ Dynamic Media Classic Dam侦听器：

1. 点按[!UICONTROL 工具]图标，然后导航到&#x200B;**[!UICONTROL 操作> Web Console]**。 Web控制台将打开。
1. 导航到&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Dam监听器]**&#x200B;并选中&#x200B;**[!UICONTROL 已启用]**&#x200B;复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 点按&#x200B;**[!UICONTROL 保存]**。

### 向Dynamic Media Classic上载工作流{#adding-configurable-timeout-to-scene-upload-workflow}添加可配置的超时

当Experience Manager实例配置为通过Dynamic Media Classic处理视频编码时，默认情况下，任何上传作业都会有35分钟超时。 要容纳可能运行时间较长的视频编码作业，可以配置此设置：

1. 导航到&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段中根据需要更改数字。 以秒为单位接受任何非负数。 默认情况下，此数字设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资源最多只需几分钟即可摄取（例如，图像）。 但在某些情况下（例如，视频较大），将超时值增加到7200秒（2小时）以适应较长的处理时间。 否则，此Dynamic Media经典上传作业在JCR元数据中标记为&#x200B;**[!UICONTROL UploadFailed]**。

1. 点按&#x200B;**[!UICONTROL 保存]**。

### 从Experience Manager资产{#autouploading-from-aem-assets}进行部署

从Experience Manager 6.3.2开始，系统会配置Experience Manager资产，以便上传到资产管理器的任何数字资产在资产位于CQ目标文件夹中时，都会更新到Dynamic Media Classic。

当资产添加到Experience Manager资产时，会自动上传并发布到Dynamic Media Classic。

>[!NOTE]
>
>从Experience Manager资产自动上传到Dynamic Media Classic的最大文件大小为500 MB。

要从Experience Manager资产配置自动部署，请执行以下操作：

1. 点按Experience Manager图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，然后在Dynamic Media标题的可用配置下点按&#x200B;**[!UICONTROL dms7(Dynamic Media]**)
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，选中&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;复选框，然后点按&#x200B;**[!UICONTROL 确定]**。 您现在必须配置DAM资产工作流，以包括上传到Dynamic Media Classic。

   >[!NOTE]
   >
   >有关将资产推送到Dynamic Media Classic处于未发布状态的信息，请参阅[配置推送到Dynamic Media Classic的资产的状态（已发布/未发布）。](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回Experience Manager欢迎页面，然后点按&#x200B;**[!UICONTROL 工作流]**。 多次单击&#x200B;**DAM更新资产**&#x200B;工作流以打开它。
1. 在Sidekick中，导航到&#x200B;**[!UICONTROL Workflow]**&#x200B;组件，然后选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。 将&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;拖动到工作流，然后点按&#x200B;**[!UICONTROL 保存]**。 添加到Experience Manager文件夹中的目标资产的资产会自动上传到Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动化后添加资产时，如果资产未放在CQ目标文件夹中，则不会将其上传到Dynamic Media Classic。
   >* Experience Manager在将所有元数据上传到Dynamic Media Classic之前将其嵌入为XMP，因此，在Dynamic Media Classic XMP中，元数据节点上的所有属性都可用。


### 配置推送到Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}的资产的状态（已发布/未发布）

如果您要将资产从Experience Manager资产推送到Dynamic Media Classic，则可以自动发布资产（默认行为）或将资产推送到未发布状态的Dynamic Media Classic。

如果您要在上线前在暂存环境中测试资产，则可能不想立即在Dynamic Media Classic上发布资产。 您可以将Experience Manager与Dynamic Media Classic的安全测试环境结合使用，将资产直接从资产推送到处于未发布状态的Dynamic Media Classic。

Dynamic Media Classic资源仍可通过安全预览使用。 仅当在Experience Manager中发布资产时，Dynamic Media Classic资产才会在生产中实时显示。

如果要在将资产推送到Dynamic Media Classic时立即发布资产，则无需配置任何选项。 此功能是默认行为。

但是，如果您不希望将资产推送到Dynamic Media Classic以自动发布，本节将介绍如何配置Experience Manager和Dynamic Media Classic以执行此功能。

#### 将资产推送到未发布的Dynamic Media Classic {#prerequisites-to-push-assets-to-scene-unpublished}的先决条件

在将资产推送到Dynamic Media Classic而不发布之前，您必须设置以下各项：

1. [使用Admin Console创建支持案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 在您的支持案例中，请求为您的Dynamic Media Classic帐户启用安全预览。
1. 按照[设置Dynamic Media Classic帐户的安全预览的说明操作。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

这些步骤与在Dynamic Media Classic中创建任何安全测试设置时所遵循的步骤相同。

>[!NOTE]
>
>如果您的安装环境是UNIX® 64位操作系统，请参阅https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)，了解您必须设置的其他配置选项。[

#### 将资产推入未发布状态的已知限制{#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在Experience Manager中发布，并且创建了后续版本，则新版本将立即实时发布到生产。 只有在激活时发布才能与资产的初始发布一起使用。

>[!NOTE]
>
>如果您想立即发布资产，最佳实践是将&#x200B;**[!UICONTROL 启用安全预览]**&#x200B;设置为&#x200B;**[!UICONTROL 立即]**，然后使用&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;功能。

### 将推送到Dynamic Media Classic的资产的状态设置为未发布{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户以Experience Manager形式发布资产，则会自动将S7资产触发到生产/实时资产(该资产不再处于安全预览/未发布状态)。

要将推送到Dynamic Media Classic的资产状态设置为未发布，请执行以下操作：

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 启用安全视图]**&#x200B;下拉菜单中，选择&#x200B;**[!UICONTROL 在AEM发布激活]**&#x200B;上，将资产推送到Dynamic Media Classic而不进行发布。 (默认情况下，此值设置为&#x200B;**[!UICONTROL Immedialed]**，其中Dynamic Media Classic资产会立即发布。)

   有关在将资产公开之前测试资产的详细信息，请参阅[Dynamic Media Classic文档](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 点按&#x200B;**[!UICONTROL 确定]**。

启用安全预览意味着您的资产会被推送到未发布的安全预览服务器。

要查看是否启用了安全预览，请在Experience Manager中的页面上导航到Dynamic Media Classic组件。 点按&#x200B;**[!UICONTROL 编辑]**。 资产的URL中列出了安全预览服务器。 在Experience Manager中发布后，文件引用中的服务器域将从预览URL更新到生产URL。

### 为WCM {#enabling-scene-for-wcm}启用Dynamic Media Classic

需要为WCM启用Dynamic Media Classic，原因有二：

* 它支持通用用户档案的下拉列表，用于页面创作。 如果没有此列表,**[!UICONTROL 通用视频预设]**&#x200B;下拉框为空，无法设置。
* 如果数字资产不在目标文件夹中，则您可以在页面属性中为该页面启用Dynamic Media Classic，则可以将该资产上传到Dynamic Media Classic。 然后，将资产拖放到Dynamic Media Classic组件上。 普通继承规则适用（即子页面从父页面继承配置）。

与其他配置一样，为WCM启用Dynamic Media Classic时，将应用继承规则。 您可以在触屏优化用户界面或经典用户界面中为WCM启用Dynamic Media Classic。

#### 在触屏优化用户界面{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}中为WCM启用Dynamic Media Classic

要在触屏优化UI中为WCM启用Dynamic Media Classic:

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL Sites]**，然后导航到网站的根页面（不是特定于语言）。

1. 在工具栏中，选择[!UICONTROL settings]图标，然后点按&#x200B;**[!UICONTROL 打开属性]**。

1. 点按&#x200B;**[!UICONTROL Cloud Services]**，然后点按&#x200B;**[!UICONTROL 添加配置]**&#x200B;并选择&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media Classic]**&#x200B;下拉列表中，选择所需的配置，然后点按&#x200B;**[!UICONTROL 确定]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   通过Dynamic Media Classic配置创建的Experience Manager预设可用于该页面和子页面上的Dynamic Media Classic视频组件。

#### 在经典用户界面{#enabling-scene-for-wcm-in-the-classic-user-interface}中为WCM启用Dynamic Media Classic

要在经典UI中为WCM启用Dynamic Media Classic，请执行以下操作：

1. 在Experience Manager中，点按&#x200B;**[!UICONTROL 网站]**&#x200B;并导航到网站的根页面（不是特定语言）。

1. 在Sidekick中，点按&#x200B;**[!UICONTROL 页面]**&#x200B;图标，然后点按&#x200B;**[!UICONTROL 页面属性]**。

1. 点按&#x200B;**[!UICONTROL Cloud Services>添加服务> Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media Classic]**&#x200B;下拉列表中，选择所需的配置，然后点按&#x200B;**[!UICONTROL 确定]**。

   通过Dynamic Media Classic配置创建的Experience Manager预设可用于该页面和子页面上的Dynamic Media Classic视频组件。

### 配置默认配置{#configuring-a-default-configuration}

如果您有多个Dynamic Media Classic配置，则可以将其中一个配置指定为Dynamic Media Classic内容浏览器的默认配置。

在给定时刻，只能将一个Dynamic Media经典配置标记为默认配置。 默认配置是默认在Dynamic Media经典内容浏览器中显示的公司资产。

配置默认配置：

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 要打开配置，请点按&#x200B;**[!UICONTROL 编辑]**。

1. 在&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，选中&#x200B;**[!UICONTROL 默认配置]**&#x200B;复选框，使其成为Dynamic Media Classic内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，则选中“默认配置”**[!UICONTROL 复选框不起作用。]**

### 配置Ad-hoc文件夹{#configuring-the-ad-hoc-folder}

当资产不在CQ目标文件夹中时，您可以配置资产上传到的文件夹。 请参阅从CQ目标文件夹外部发布资产。

要配置临时文件夹，请执行以下操作：

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media Classic]**，然后在Dynamic Media Classic中选择配置。
1. 要打开配置，请点按&#x200B;**[!UICONTROL 编辑]**。

1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 临时文件夹]**&#x200B;字段中，可以修改&#x200B;**临时**&#x200B;文件夹。 默认情况下，它为&#x200B;**name_of_the_公司/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用预设{#configuring-universal-presets}

要为视频组件配置通用预设，请参阅[视频](/help/assets/s7-video.md)。

## 启用基于MIME类型的资产/Dynamic Media Classic上传作业参数支持{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用可配置的Dynamic Media Classic上传作业参数，这些参数是通过同步数字资产管理器/Dynamic Media Classic资产触发的。

具体而言，在“Experience ManagerWeb控制台配置”面板的OSGi（Open Service Gateway活动）区域中，按MIME类型配置接受的文件格式。 然后，您可以自定义单个上传作业参数，这些参数用于JCR(Java™内容存储库)中的每个MIME类型。

**要启用基于MIME类型的资产，请执行以下操作：**

1. 点按Experience Manager图标，然后导航到&#x200B;**[!UICONTROL 工具>操作> Web Console]**。
1. 在Adobe Experience Manager Web控制台的“配置”面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;菜单上，点按&#x200B;**[!UICONTROL 配置]**。
1. 在“名称”列下，找到并点按&#x200B;**[!UICONTROL Adobe CQ Dynamic Media经典资产MIME类型服务]**&#x200B;以编辑配置。
1. 在Mime类型映射区域中，点按任意加号(+)以添加MIME类型。

   请参阅[支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文本字段中，键入新的MIME类型名称。

   例如，您应键入`<file_extension>=<mime_type>` ，如`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`中所示。

1. 在配置窗口的右下角，点按&#x200B;**[!UICONTROL 保存]**。
1. 返回Experience Manager，在左边栏中点按CRXDE Lite。
1. 在CRXDE Lite页面的左边栏中，导航到`/etc/cloudservices/scene7/<environment>`（用`<environment>`替换实际名称）。
1. 展开`<environment>`（用`<environment>`替换实际名称）以显示`mimeTypes`节点。
1. 点按刚刚添加的mimeType。

   例如，`mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite页面的右侧，点按&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中指定Dynamic Media Classic上载作业参数。

   例如，`psprocess="rasterize"&psresolution=120`。

   有关可使用的更多上传作业参数，请参阅[AdobeDynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)。

   >[!NOTE]
   >
   >如果您正在上传PSD文件，并且要将其作为具有图层提取的模板进行处理，请在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中输入以下内容：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >确保PSD文件包含“图层”。 如果它只是一幅图像或带有蒙版的图像，则会作为图像进行处理，因为没有要处理的图层。

1. 在CRXDE Lite页面的左上角，点按&#x200B;**[!UICONTROL 全部保存]**。

## Dynamic Media Classic和Experience Manager集成疑难解答{#troubleshooting-scene-and-aem-integration}

如果您在将Experience Manager与Dynamic Media Classic集成时遇到问题，请参阅以下解决方案方案。

**如果发布到Dynamic Media Classic的数字资产失败：**

* 检查您上传的资产是否位于&#x200B;**[!UICONTROL CQ 目标]**&#x200B;文件夹中(您在Dynamic Media Classic云配置中指定此文件夹)。
* 否则，必须在&#x200B;**[!UICONTROL 页面属性]**&#x200B;中配置该页面的云配置，以允许上传到&#x200B;**[!UICONTROL CQ ad hoc]**&#x200B;文件夹。

* 检查日志中是否有任何信息。

**如果未显示视频预设：**

* 请确保您已通过&#x200B;**[!UICONTROL 页面属性]**&#x200B;配置了该页面的云配置。 Dynamic Media经典视频组件中提供了视频预设。

**如果您的视频资源不以Experience Manager播放：**

* 确保您使用了正确的视频组件。 Dynamic Media经典视频组件与基础视频组件不同。 请参阅[基础视频组件与Dynamic Media经典视频组件](/help/assets/s7-video.md)。

**如果Experience Manager中的新资产或已修改的资产不会自动上传到Dynamic Media Classic:**

* 确保资产位于CQ目标文件夹中。 只有CQ目标文件夹中的资产才会自动更新(前提是您已将Experience Manager资产配置为自动上传资产)。
* 确保您已将Cloud Services配置配置为启用自动上传，并且您已更新并保存DAM资产工作流以包括Dynamic Media Classic上传。
* 将图像上传到Dynamic Media Classic目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资产的名称（无论位置如何）都是唯一的。 否则，主目标文件夹中的资产将被删除，并且只保留子文件夹中的资产。
   * 更改Dynamic Media Classic在Dynamic Media Classic帐户的“设置”区域覆盖资产的方式。 如果您在子文件夹中使用同名的资源，则不要设置Dynamic Media Classic覆盖资源，而不考虑其位置。

**如果已删除的资产或文件夹未在Dynamic Media Classic和Experience Manager之间同步：**

* 在Experience Manager Assets中删除的资产和文件夹仍会显示在Dynamic Media Classic的同步文件夹中。 手动删除。

**如果视频上传失败**

* 如果您的视频上传失败，并且您正在使用Experience Manager通过Dynamic Media Classic集成对视频进行编码，请参阅[向Dynamic Media Classic Upload工作流添加可配置的超时](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>从现有Dynamic Media Classic公司帐户导入资源可能需要很长时间才能在Experience Manager中显示。 请确保在Dynamic Media Classic中指定一个资源不太多的文件夹。 例如，根文件夹通常包含的资源过多。
>
>如果要测试集成，请让根文件夹仅指向子文件夹，而不是整个公司。

