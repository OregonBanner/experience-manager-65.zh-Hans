---
title: 与Dynamic Media经典集成(Scene7)
seo-title: 与Dynamic Media经典集成(Scene7)
description: 了解如何将AEM与Dynamic Media经典相集成。
seo-description: 了解如何将AEM与Dynamic Media经典相集成。
uuid: b014d643-1cc1-47f3-a79c-7f6f9e45637a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: f55e68c3-3309-4400-bef9-fd3afa6e2b5f
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '5474'
ht-degree: 1%

---


# 与Dynamic Media经典集成(Scene7){#integrating-with-dynamic-media-classic-scene}

[AdobeDynamic MediaClassic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 是一款托管解决方案，用于管理、增强、发布富媒体资产并将富媒体资产交付到Web、移动、电子邮件以及连接Internet的显示屏和印刷品。

要使用Dynamic Media经典，您需要配置云配置，以便Dynamic Media经典和AEM Assets能够相互交互。 本文档介绍如何配置AEM和Dynamic Media经典。

有关在页面上使用所有Dynamic Media经典组件和处理视频的信息，请参 [阅使用Dynamic Media经典](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic MediaClassic的DHTML查看器平台于2014年1月31日正式停止使用。 有关详细信息，请 [参阅DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在配置Dynamic Media经典以与AEM结合使用之前，请参 [阅将Dynamic Media经](#best-practices-for-integrating-scene-with-aem) 典与AEM集成的最佳实践。
>* 如果您使用Dynamic Media经典和自定义代理配置，则需要同时配置HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他功能则使用4.x API。 3.x配置有http://localhost:4502/system/console/configMgr/com.day.commons.httpclient [](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) ,4.x配置有 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)。

>



## AEM/Dynamic Media经典集成与Dynamic Media {#aem-scene-integration-versus-dynamic-media}

AEM用户可以选择两种解决方案来使用Dynamic Media: 将其AEM实例与Dynamic Media经典集成，或使用集成到AEM中的Dynamic Media解决方案。

使用以下条件确定要选择的解决方案：

* 如果您是现有 **Dynamic Media** Classic客户，其富媒体资产驻留在Dynamic MediaClassic中进行发布和投放，但您希望将这些资产与站点(WCM)创作和／或AEM Assets集成以进行管理，请使用本文档中介绍的 [](#aem-scene-point-to-point-integration) AEM/Dynamic Media经典点对点集成。

* 如果您是具有 **富媒体投放** 需求的新AEM客户，请选择“ [Dynamic Media”选项](#aem-dynamic-media)。 如果您没有现有的S7帐户，并且该系统中存储了许多资产，则此选项最有意义。

* 在某些情况下，您可能希望同时使用这两种解决方案。 两 [用方案描述](/help/sites-administering/scene7.md#dual-use-scenario) 该方案。

### AEM/Dynamic Media经典点对点集成 {#aem-scene-point-to-point-integration}

在此解决方案中处理资产时，您需要执行下列操作之一：

* 将资产直接上传到Dynamic Media经典，然后通过Dynamic Media经典内 **容浏览器** (用于创作页面或
* 上传到AEM Assets，然后启用自动发布到Dynamic Media经典； 您可以通过资 **产内容** 浏览器访问以进行页面创作

您用于此集成的组件位于“设计”模 **式的Dynamic Media** “经典”组 [件区域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEMDynamic Media {#aem-dynamic-media}

AEMDynamic Media是直接在AEM平台中统一Dynamic Media经典功能。

在此解决方案中处理资产时，您可以遵循以下工作流：

1. 将单个图像和视频资产直接上传到AEM。
1. 在AEM中直接对视频进行编码。
1. 直接在AEM中构建基于图像的集。
1. 如果适用，为图像或视频添加交互性。

您用于Dynamic Media的组件位于“设计” **[!UICONTROL 模式]** 的“Dynamic Media [”组件](/help/sites-authoring/author-environment-tools.md#page-modes)区域中。 包括：

* **[!UICONTROL Dynamic Media]****[!UICONTROL -]** Dynamic Media组件是智能的，具体取决于您是添加图像还是添加视频，您有各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

* **[!UICONTROL 交互式媒体]** -交互 **[!UICONTROL 式媒体组件适用于在热点或图像地图等资源上具有交互性的资源]** ，如传送横幅、交互式图像和交互式视频。 此组件是智能的——根据您添加的是图像还是视频，您有各种选项。 此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

### 双用途方案 {#dual-use-scenario}

开箱即用，您可以同时使用AEM的Dynamic Media和Dynamic Media经典集成功能。 下面的使用案例表描述了在打开和关闭某些区域时的情况。

要同时使用Dynamic Media和Dynamic Media经典：

1. 在云 [服务中配](#creating-a-cloud-configuration-for-scene) 置Dynamic Media经典。
1. 按照您的用例特有的说明操作：

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media经典集成</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>如果你……</strong></td>
    <td><strong>用例工作流</strong></td>
    <td><strong>成像／视频</strong></td>
    <td><strong>动态媒体组件</strong></td>
    <td><strong>S7内容浏览器和组件</strong></td>
    <td><strong>从资产自动上传到S7</strong></td>
    </tr>
    <tr>
    <td>站点和Dynamic Media新手</td>
    <td>将资产上传到AEM并使用AEMDynamic Media组件在站点页面上创作资产</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>在零售业中，对站点和Dynamic Media不熟悉</td>
    <td>将非产品资产上传到AEM以进行管理和投放。 将产品资产上传到Dynamic Media经典，并在AEM和组件中使用Dynamic Media经典内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>资产和Dynamic Media新增功能</td>
    <td>将资产上传到AEM Assets，并使用Dynamic Media中发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>Dynamic Media和模板新功能</td>
    <td>使用Dynamic Media进行成像和视频。 在Dynamic Media经典中创作图像模板，并使用Dynamic Media经典内容查找器将模板包含在站点页面中。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media经典客户，不熟悉站点</td>
    <td>将资产上传到Dynamic Media经典，然后使用AEMDynamic Media经典内容浏览器在站点页面上搜索和创作资产</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有Dynamic Media经典客户，不熟悉站点和资产</td>
    <td>将资产上传到DAM并自动发布到Dynamic Media经典以供投放。 使用AEMDynamic Media经典内容浏览器在站点页面上搜索和创作资产。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media经典客户和新资产</td>
    <td><p>将资产上传到AEM，然后使用Dynamic Media生成要下载／共享的演绎版。 自动将AEM资产发布到Dynamic Media经典以供投放。</p> <p><strong>重要：</strong> 在AEM中生成的重复处理和再现将不会同步到Dynamic Media经典</p> </td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可选； 请参阅用例表)-设置 [Dynamic Media云配置](/help/assets/config-dynamic.md)[并启用Dynamic Media服务器](/help/assets/config-dynamic.md)。
1. (可选； 请参阅用例表)-如果您选择启用从资产自动上传到Dynamic Media经典，则需要添加以下内容：

   1. 设置自动上传到Dynamic Media经典。
   1. 在Dam更新 **资产工作流结束时** ，在所有Dynamic Media工作流步骤之 *后添加Dynamic Media经* 典上 **** 传步骤( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. （可选）按https://&lt;server>:&lt;port> [/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl中的MIME类型限制Dynamic Media经典资产上传](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)。 此列表中未包含的资产MIME类型将不会上传到Dynamic Media经典服务器。
   1. （可选）以Dynamic Media经典配置设置视频。 您可以同时为Dynamic Media和Dynamic Media经典启用视频编码。 动态演绎版用于在AEM实例中本地预览和回放，而Dynamic Media经典视频演绎版则生成并存储在Dynamic Media经典服务器上。 在为Dynamic Media和Dynamic Media经典设置视频编码服务时，将视频处 [理用户档案应用到Dynamic Media](/help/assets/video-profiles.md) 经典资产文件夹。
   1. （可选）在 [Dynamic Media经典中配置安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 限制 {#limitations}

启用Dynamic Media经典和Dynamic Media后，有以下限制：

* 在AEM页面上选择资产并将其拖动到Dynamic Media经典组件，手动上传到Dynamic Media经典组件不起作用。
* 即使在资产中编辑资产时，AEMDynamic Media经典同步的资产会自动更新为Dynamic Media经典，但回滚操作不会触发新的上传，因此Dynamic Media经典在回滚后不会立即获得最新版本。 解决方法是在回滚完成后再次编辑。
* 如果您需要将Dynamic Media用于一个用例，将Dynamic Media经典集成用于另一个用例，以便Dynamic Media资产不会与Dynamic Media经典系统交互，那么请勿将Dynamic Media经典配置应用到Dynamic Media文件夹，或将Dynamic Media配置(处理用户档案)应用到Dynamic Media经典文件夹。

## 将Dynamic Media经典与AEM集成的最佳实践 {#best-practices-for-integrating-scene-with-aem}

在将Dynamic Media经典与AEM集成时，需要在以下方面遵循一些重要的最佳实践：

* 测试驱动集成
* 对于某些情况，建议直接从Dynamic Media经典上传资产

请参 [阅已知限制](#known-limitations-and-design-implications)。

### 测试驱动集成 {#test-driving-your-integration}

Adobe建议您通过让根文件夹仅指向子文件夹而非整个公司来测试集成。

>[!CAUTION]
>
>从现有Dynamic Media经典公司帐户导入资产可能需要很长时间才能在AEM中显示。 请确保在Dynamic Media经典中指定一个资产不过多的文件夹（例如，根文件夹通常拥有的资产过多，并且可能会导致系统崩溃）。

### 从AEM Assets上传资产与从Dynamic Media经典上传资产 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以通过使用资产（数字资产管理）功能，或通过Dynamic Media经典内容浏览器直接在AEM中访问Dynamic Media经典来上传资产。 您选择哪个取决于以下因素：

* Dynamic MediaAEM Assets尚不支持的经典资产类型必须通过Dynamic Media经典内容浏览器（例如图像模板）直接从Dynamic Media经典添加到AEM网站。
* 对于AEM Assets和Dynamic Media经典都支持的资产类型，确定如何上传资产取决于以下各项：

   * 资产现在的位置，以及
   * 在通用存储库中管理它们的重要性

如果资产已在Dynamic Media经典中，而在通用存储库中管理资产并不重要，则仅将资产导出到AEM Assets以将其同步回Dynamic Media经典进行投放将是不必要的往返操作。 否则，最好将资产保留在单个存储库中，并仅同步到Dynamic Media经典以供投放。

## 配置Dynamic Media经典集成 {#configuring-scene-integration}

您可以配置AEM以将资产上传到Dynamic Media经典。 可以从CQ目标文件夹将资产（自动或手动）从AEM上传到Dynamic Media经典公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media经典资产。 驻留在目标文件夹以外的数字资产只能用于启用Dynamic Media经典配置的页面上的Dynamic Media经典组件。 此外，它们还位于Dynamic Media经典中的临时文件夹中。 临时文件夹未与AEM同步(但资产可在Dynamic Media经典内容浏览器中显示)。

要将Dynamic Media经典配置为与AEM集成，您需要完成以下步骤：

1. [定义云配置](#creating-a-cloud-configuration-for-scene) -定义Dynamic Media经典文件夹与资产文件夹之间的映射。 即使您只想单向(AEM Assets到Dynamic Media经典)同步，也需要完成此步骤。
1. [启用 **Adobe CQ s7dam Dam监听器&#x200B;**](#enabling-the-adobe-cq-scene-dam-listener)-在OSGi控[!UICONTROL 制台中]完成。
1. 如果您希望AEM资产自动上传到Dynamic Media经典，您需要打开此选项，并将Dynamic Media经典添加到DAM更 [!UICONTROL 新资产工作流] 。 您还可以手动上传资产。
1. 将Dynamic Media经典组件添加到Sidekick。 这允许用户在其AEM页面上使用Dynamic Media经典组件。
1. [将配置映射到AEM中的页面](#enabling-scene-for-wcm) -此步骤是视图您在Dynamic Media经典中创建的任何视频预设所必需的。 如果您需要将资产从CQ目标文件夹外部发布到Dynamic Media经典，则此操作也是必需的。

本节介绍如何执行所有这些步骤和列表重要限制。

### Dynamic Media经典与AEM Assets之间的同步如何工作 {#how-synchronization-between-scene-and-aem-assets-works}

在设置AEM Assets和Dynamic Media经典同步时，请务必了解以下内容：

#### 从Dynamic Media上传到AEM Assets经典 {#uploading-to-scene-from-aem-assets}

* AEM中存在一个指定的同步文件夹，用于Dynamic Media经典上传。
* 如果数字资产放在指定的同步文件夹中，则上传到Dynamic Media经典版本可以自动完成。
* AEM中的文件夹和子文件夹结构将复制到Dynamic Media经典中。

>[!NOTE]
>
>在将所有元数据上传到Dynamic Media经典之前，AEM会将其嵌入为XMP，因此在Dynamic Media经典中，元数据节点上的所有属性都可以作为XMP使用。

#### 已知限制和设计含义 {#known-limitations-and-design-implications}

在AEM Assets和Dynamic Media经典之间进行同步时，当前存在以下限制／设计含义：

<table>
 <tbody>
  <tr>
   <td><strong>限制／设计含义</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步(目标)文件夹</td>
   <td>在AEM中，对于Dynamic Media经典上传，每个公司只能有一个指定的文件夹。 如果您需要访问Dynamic Media经典中的多个公司帐户，可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果删除的是与资产同步的文件夹，则所有Dynamic Media经典远程资产都将被删除，但该文件夹仍然存在。</td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>在WCM中手动上传到目标经典的Dynamic Media文件夹外的资产将自动放在Dynamic Media经典上的单独点对点文件夹中。 您可以在AEM的云配置中配置此项。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集显示在AEM中，但AEM不支持它们。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media经典中的电子目录生成的PDF导入到CQ目标文件夹中。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在AEM和Dynamic Media经典之间同步时，请确保刷新用户界面以视图更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果将视频上传到AEM Assets以通过Dynamic Media经典进行编码，则视频缩略图和编码视频可能需要一些时间才能在AEM Assets中可用，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>Target子文件夹</td>
   <td><p>如果您正在目标文件夹中使用子文件夹，请确保对每个资产使用唯一的名称（无论位置如何），或者配置Dynamic Media经典（在“设置”区域）以不覆盖任何位置的资产。</p> <p>否则，上传到Dynamic Media经典目标子文件夹的同名资产会被上传，但目标文件夹中同名的资产会被删除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media经典服务器 {#configuring-scene-servers}

如果您在代理后运行AEM或具有特殊的防火墙设置，则可能需要显式启用不同区域的主机。 服务器在内容中进行管 `/etc/cloudservices/scene7/endpoints` 理，并可以根据需要进行自定义。 点按一个URL，然后根据需要进行编辑以更改该URL。 在AEM的早期版本中，这些值是硬编码的。

如果导航到， `/etc/cloudservices/scene7/endpoints.html`您会看到列出的服务器（并可通过单击URL来编辑它们）:

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media经典创建云配置 {#creating-a-cloud-configuration-for-scene}

云配置定义Dynamic Media经典文件夹与AEM Assets文件夹之间的映射。 它需要配置为将AEM Assets与Dynamic Media经典同步。 有关详细信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有Dynamic Media经典公司帐户导入资产可能需要很长时间才能在AEM中显示。 请确保在Dynamic Media经典中指定一个资产不太多的文件夹（例如，根文件夹通常包含的资产过多）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

>[!NOTE]
>
>您可以有多个配置： 一个云配置表示Dynamic Media经典公司的一个用户。 如果要访问其他Dynamic Media经典公司或用户，您需要创建多个配置。

要将AEM配置为能够将资产发布到Dynamic Media经典，请执行以下操作：

1. 点按AEM图标，然后导航到 **[!UICONTROL 部署>Cloud Service]** ，以访问AdobeDynamic Media经典。

1. 点按 **[!UICONTROL 立即配置。]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在“标 **[!UICONTROL 题]** ”字段中，或（可选） **[!UICONTROL 在“名称]** ”字段中输入相应的信息。 Tap **[!UICONTROL Create.]**

   >[!NOTE]
   >
   >创建其他配置时，将显 **[!UICONTROL 示父配置]** 字段。
   >
   >请 **勿更** 改父配置。 更改父配置可能会中断集成。

1. 输入Dynamic Media经典帐户的电子邮件地址、密码和区域，然后点按连 **[!UICONTROL 接到Dynamic Media经典。]** 您已连接到Dynamic Media经典服务器，对话框会扩展，显示更多选项。

1. 输入 **[!UICONTROL 公司]** 名 **[!UICONTROL 称和根路径]** (这是已发布的服务器名称以及要指定的任何路径； 如果您不知道已发布的服务器名称，请在Dynamic Media经典中，转 **[!UICONTROL 到设置>应用程序设置]**。)

   >[!NOTE]
   >
   >Dynamic Media经典根路径是AEM连接的Dynamic Media经典文件夹。 可以将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media经典文件夹的大小，导入根文件夹可能需要很长时间。 此外，Dynamic Media经典数据可能超过AEM存储。 确保导入的文件夹正确。 导入过多数据可能会停止系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 单击&#x200B;**[!UICONTROL 确定。]** AEM会保存您的配置。

>[!NOTE]
>
>如果您正在重新连接：
>
>* 在发布时重新连接到Dynamic Media经典时，可能需要在发布时重置口令，或重新连接将无法工作。 这不是创作实例的问题。
>* 如果修改区域、公司名称等值，则必须重新连接到Dynamic Media经典。 如果配置选项已修改但未保存，AEM仍错误地指示配置有效。 确保重新连接。

>



### 启用Adobe CQDynamic Media经典Dam监听器 {#enabling-the-adobe-cq-scene-dam-listener}

您必须启用Adobe CQDynamic Media经典Dam监听器，默认情况下禁用它。

要启用它，请执行以下操作：

1. 点按工 [!UICONTROL 具图] 标，然后导航到 **[!UICONTROL 操作> Web Console。]** Web控制台将打开。
1. 导航到 **[!UICONTROL Adobe CQDynamic MediaClassic Dam监听器]** ，然后选 **[!UICONTROL 中“启]** 用”复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. Tap  **[!UICONTROL Save.]**

### 为Dynamic Media经典上传工作流添加可配置超时 {#adding-configurable-timeout-to-scene-upload-workflow}

当AEM实例配置为通过Dynamic Media经典(Scene7)处理视频编码时，默认情况下，任何上传作业都会出现35分钟超时。 要适应可能运行时间较长的视频编码作业，可以配置此设置：

1. 导航到 **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在活动作业超时字段中根 **[!UICONTROL 据需要更改]** 数。 以秒为单位接受任何非负数。 默认情况下，此值设置为2100。

   >[!NOTE]
   >
   >最佳实践： 大多数资源最多只需几分钟即可摄取（例如，图像）。 但在某些情况下（例如，视频较大），超时值应增加到7200秒（2小时）以适应较长的处理时间。 否则，此Dynamic Media经典上传作业在JCR元 **[!UICONTROL 数据中]** 被标记为UploadFailed。

1. Tap **[!UICONTROL Save.]**

### 来自AEM Assets的自动绘图 {#autouploading-from-aem-assets}

从AEM 6.3.2开始，现在为您配置了AEM Assets，这样，如果资产位于CQ目标文件夹中，您上传到数字资产管理器的任何数字资产都将自动更新至Dynamic Media经典。

当资产添加到AEM Assets时，它会自动上传并发布到Dynamic Media经典。

>[!NOTE]
>
>从AEM Assets自动上传到Dynamic Media经典的最大文件大小为500 MB。

要从AEM Assets配置自动部署，请执行以下操作：

1. 点按AEM图标并导航到 **[!UICONTROL 部署>Cloud Service]** ，然后在Dynamic Media标题下的可用配置下，点 **[!UICONTROL 按dms7(Dynamic Media]**)
1. 点按高 **[!UICONTROL 级]** 选项卡，选 **[!UICONTROL 择启用自动上传]** 复选框，然后点 **[!UICONTROL 按确定。]** 您现在需要配置DAM资产工作流，以包括上传到Dynamic Media经典。

   >[!NOTE]
   >
   >有 [关将资产推送到未发布状态的Dynamic Media经典的信息](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) ，请参阅配置推送到Dynamic Media经典的资产的状态（已发布／未发布）。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回AEM欢迎页面，然后点按 **[!UICONTROL 工作流。]** 多次，单击 **DAM更新资产工作流** ，以将其打开。
1. 在Sidekick中，导航到工作流 **[!UICONTROL 组件]** ，然后选择 **[!UICONTROL Dynamic Media经典。]** 将Dynamic Media **[!UICONTROL 经典]** 拖到工作流中，然后点 **[!UICONTROL 按保存。]** 添加到AEM Assets文件夹中的目标的资产将自动上传到Dynamic Media经典。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动添加资产时，如果资产未放在CQ目标文件夹中，则不会将其上传到Dynamic Media经典。
   >* 在将所有元数据上传到Dynamic Media经典之前，AEM会将其嵌入为XMP，因此在Dynamic Media经典中，元数据节点上的所有属性都可以作为XMP使用。


### 配置推送到Dynamic Media经典的资产的状态（已发布／未发布） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果要将资产从AEM Assets推送到Dynamic Media经典，则可以自动发布资产（默认行为），也可以将资产推送到未发布状态的Dynamic Media经典。

如果要在上线前在分阶段Dynamic Media中测试资产，则可能不想立即在环境经典上发布资产。 您可以将AEM与Dynamic Media经典的安全测试环境结合使用，将资产直接从资产推送到未发布状态的Dynamic Media经典。

Dynamic Media经典资产仍可通过安全预览使用。 仅当资产在AEM中发布时，Dynamic Media经典资产才会在生产中投入使用。

如果要在将资产推送到Dynamic Media经典时立即发布资产，则无需配置任何选项。 这是默认行为。

但是，如果您不希望将资产推送到Dynamic Media经典以自动发布，本节将介绍如何配置AEM和Dynamic Media经典以实现此操作。

#### 将资产推送到Dynamic Media经典未发布的先决条件 {#prerequisites-to-push-assets-to-scene-unpublished}

在将资产推送到Dynamic Media经典而不发布之前，您必须设置以下各项：

1. 联系Dynamic Media经典客户关怀(s7support@adobe.com)，为您的Dynamic Media经典帐户启用安全预览。
1. 按照说明为 [Dynamic Media经典帐户设置安全预览。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

这些步骤与在Dynamic Media经典中创建任何安全测试设置的步骤相同。

>[!NOTE]
>
>如果您的安装环境是Unix 64位操作系统，请参 [阅https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) ，了解需要设置的其他配置选项。

#### 将资产推入未发布状态的已知限制  {#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在AEM中发布，且已创建后续版本，则新版本将立即实时发布到生产。 仅在激活时发布适用于资产的初始发布。

>[!NOTE]
>
>如果要立即发布资产，最佳实践是将“启用安 **[!UICONTROL 全预览]** ”设置 **[!UICONTROL 为“立即]** ”，然 **[!UICONTROL 后使用“启用自动上传]** ”功能。

### 将推送到Dynamic Media经典的资产的状态设置为未发布 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在AEM中发布资产，则会自动将S7资产触发到生产／实时资产(该资产将不再处于安全预览/取消发布状态)。

要将推送到Dynamic Media经典的资产的状态设置为未发布，请执行以下操作：

1. 点按AEM图标，导航到 **[!UICONTROL 部署>Cloud Service]**，点 **[!UICONTROL 按Dynamic Media经]**&#x200B;典，然后在Dynamic Media经典中选择您的配置。
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在启 **[!UICONTROL 用安全视图]** 下拉菜单中，选 **[!UICONTROL 择在AEM Publish激活]** 时将资产推送到Dynamic Media经典，而不进行发布。 (默认情况下，此值设置为“立即 **[!UICONTROL ”]**,Dynamic Media经典资产会立即发布。)

   有关在 [公开资产前测试资产](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) ，请参阅Dynamic Media经典文档。

   ![chlimage_1-382](assets/chlimage_1-302.png)

1. 点按 **[!UICONTROL 确定。]**

启用安全视图意味着您的资产将推送到未发布的安全预览服务器。

您可以通过导航到AEM中页面上的Dynamic Media经典组件并点按编辑来选中 **[!UICONTROL 此选项。]** 资产的URL中将列出安全预览服务器。 在AEM中发布后，文件引用中的服务器域将从预览URL更新到生产URL。

### 为WCM启用Dynamic Media经典 {#enabling-scene-for-wcm}

需要为WCM启用Dynamic Media经典，原因有二：

* 启用用于页面创作的通用视频用户档案的下拉列表。 如果没有此选项， **[!UICONTROL 则“通用视频]** 预设”下拉框为空，无法设置。
* 如果数字资产不在目标文件夹中，则您可以在页面属性中为该页面启用Dynamic Media经典，然后将资产拖放到Dynamic Media经典组件上，即可将资产上传到Dynamic Media经典。 普通继承规则适用（这意味着子页面将从父页面继承配置）。

在为WCM启用Dynamic Media经典时，请注意，与其他配置一样，继承规则也适用。 您可以在触屏优化或经典用户界面中为WCM启用Dynamic Media经典。

#### 在触屏优化用户界面中为WCM启用Dynamic Media经典 {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

要在触屏优化UI中为WCM启用Dynamic Media经典：

1. 点按AEM图标，然后导 **[!UICONTROL 航到]** “站点”，然后导航到网站的根页面（不是特定于语言的页面）。

1. 在工具栏中，选择设置 [!UICONTROL 图标] ，然后点 **[!UICONTROL 按打开属性。]**

1. 点按 **[!UICONTROL Cloud Service]** ，然后点 **[!UICONTROL 按添加配置]** ，然后选择 **[!UICONTROL Dynamic Media经典。]**
1. 在Adobe **[!UICONTROL Dynamic Media经典]** 列表下拉框中，选择所需的配置并点按 **[!UICONTROL 确定。]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   基于Dynamic Media经典配置的视频预设可在AEM中与该页面和子页面上的Dynamic Media经典视频组件一起使用。

#### 在经典用户界面中为WCM启用Dynamic Media经典 {#enabling-scene-for-wcm-in-the-classic-user-interface}

要在经典UI中为WCM启用Dynamic Media经典：

1. 在AEM中，点 **[!UICONTROL 按网站]** ，然后导航到网站的根页面（不是特定于语言的页面）。

1. In the sidekick, tap the **[!UICONTROL Page]** icon and tap **[!UICONTROL Page Properties.]**

1. 点按 **[!UICONTROL Cloud Service>添加服务>Dynamic Media经典。]**
1. 在Adobe **[!UICONTROL Dynamic Media经典]** 列表下拉框中，选择所需的配置并点按 **[!UICONTROL 确定。]**

   基于Dynamic Media经典配置的视频预设可在AEM中与该页面和子页面上的Dynamic Media经典视频组件一起使用。

### 配置默认配置 {#configuring-a-default-configuration}

如果您有多个Dynamic Media经典配置，您可以将其中一个指定为Dynamic Media经典内容浏览器的默认配置。

在给定时刻，只能将一个Dynamic Media经典配置标记为默认。 默认配置是默认在公司经典内容浏览器中显示的Dynamic Media资产。

配置默认配置：

1. 点按AEM图标，导航到 **[!UICONTROL 部署>Cloud Service]**，点 **[!UICONTROL 按Dynamic Media经]**&#x200B;典，然后在Dynamic Media经典中选择您的配置。
1. 点按 **[!UICONTROL 编辑]** ，打开配置。

1. 在“常 **[!UICONTROL 规]** ”选项卡中，选 **[!UICONTROL 择“默认配置]** ”复选框，使其成为Dynamic Media经典内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，则选中“默 **[!UICONTROL 认配置]** ”复选框不起作用。

### 配置点对点文件夹 {#configuring-the-ad-hoc-folder}

当资产不在CQDynamic Media文件夹中时，您可以配置资产上传到的文件夹。 请参阅从CQ目标文件夹外部发布资产。

配置临时文件夹：

1. 点按AEM图标，导航到 **[!UICONTROL 部署>Cloud Service]**，点 **[!UICONTROL 按Dynamic Media经]**&#x200B;典，然后在Dynamic Media经典中选择您的配置。
1. 点按 **[!UICONTROL 编辑]** ，打开配置。

1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在临 **[!UICONTROL 时文件夹字段中]** ，您可以修改 **临时文件夹** 。 默认情况下，它 **是name_of_the_公司/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用预设 {#configuring-universal-presets}

要为视频组件配置通用预设，请参阅 [视频](/help/assets/s7-video.md)。

## 支持基于MIME类型的资产/Dynamic Media经典上传作业参数 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用可配置的Dynamic Media经典上传作业参数，这些参数是通过同步数字资产管理器/Dynamic Media经典资产来触发的。

具体而言，您可以在AEM Web Console“配置”面板的OSGi（Open Service Gateway活动）区域按MIME类型配置接受的文件格式。 然后，您可以自定义单个上传作业参数，这些参数用于JCR（Java内容存储库）中的每个MIME类型。

**要启用基于MIME类型的资产，请执行以下操作：**

1. Tap the AEM icon and navigate to **[!UICONTROL Tools > Operations > Web Console.]**
1. 在“Adobe Experience ManagerWeb控制台配置”面板的“OSGi **[!UICONTROL ”菜单]** ，点按 **[!UICONTROL 配置。]**
1. 在“名称”列下，查找并点 **[!UICONTROL 按Adobe CQDynamic Media经典资产MIME类型服务]** ，以编辑配置。
1. 在“Mime类型映射”区域，点按任何加号(+)以添加MIME类型。

   请参 [阅支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文本字段中，键入新的MIME类型名称。

   例如，您应键入 `<file_extension>=<mime_type>` 作为 `EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`。

1. 在配置窗口的右下角，点按保 **[!UICONTROL 存。]**
1. 返回AEM，在左边栏中点按CRXDE Lite。
1. 在CRXDE Lite页面的左边栏中，导航到 `/etc/cloudservices/scene7/<environment>` (替 `<environment>` 代实际名称)。
1. 展开 `<environment>` (替 `<environment>` 换实际名称)以显示节 `mimeTypes` 点。
1. 点按刚刚添加的mimeType。

   For example, `mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`.

1. 在CRXDE Lite页面的右侧，点按属性选 **[!UICONTROL 项卡]** 。
1. 在jobParam值字段中指定Dynamic Media经典上 **[!UICONTROL 传作业]** 参数。

   For example, `psprocess="rasterize"&psresolution=120` .

   有关可 [以使用的其他上传作业参数](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/) ，请参阅AdobeDynamic Media经典图像生产系统API。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且要将其作为具有图层提取的模板进行处理，请在jobParam值字 **[!UICONTROL 段中]** 输入以下内容：
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >确保您的PSD文件具有“图层”。 如果它只是一幅图像或带有遮罩的图像，则它将作为图像处理，因为没有要处理的图层。

1. 在CRXDE Lite页面的左上角，点按全部 **[!UICONTROL 保存。]**

## Dynamic Media经典和AEM集成疑难解答 {#troubleshooting-scene-and-aem-integration}

如果您在将AEM与Dynamic Media经典集成时遇到问题，请参阅以下解决方案。

**如果向Dynamic Media经典发布数字资产失败：**

* 检查您尝试上传的资产是否在CQ **[!UICONTROL 目标文件夹]** (您可以在Dynamic Media经典云配置中指定此文件夹)。
* 否则，您需要在该页面的页面属性中配 **[!UICONTROL 置云配置]** ，以允许上传到 **[!UICONTROL CQ临时文件夹]** 。

* 检查日志中是否有任何信息。

**如果视频预设未显示：**

* 请确保您已通过页面属性配置了该页 **[!UICONTROL 面的云配置。]** Dynamic Media经典视频组件中提供了视频预设。

**如果您的视频资产不在AEM中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media经典视频组件与基础视频组件不同。 请参 [阅基础视频组件与Dynamic Media经典视频组件](/help/assets/s7-video.md)。

**如果AEM中的新资产或已修改资产不会自动上传到Dynamic Media经典：**

* 确保资产位于CQ目标文件夹中。 只有CQ目标文件夹中的资产才会自动更新(前提是您已配置AEM Assets以自动上传资产)。
* 确保您已将Cloud Service配置配置为启用自动上传，并且您已更新并保存DAM资产工作流以包括Dynamic Media经典上传。
* 将图像上传到Dynamic Media经典目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资产的名称（不管位置如何）都是唯一的。 否则，主目标文件夹中的资产将被删除，并且只保留子文件夹中的资产。
   * 更改Dynamic Media经典如何覆盖Dynamic Media经典帐户的“设置”区域中的资产。 如果在子文件夹中使用名称相同的资源，则不要设置“Dynamic Media经典”来覆盖资源，而不考虑位置。

**如果已删除的资产或文件夹未在Dynamic Media经典和AEM之间同步：**

* 在AEM Assets中删除的资产和文件夹仍会显示在Dynamic Media经典的同步文件夹中。 必须手动删除它们。

**如果视频上传失败**

* 如果您的视频上传失败，并且您正在使用AEM通过Dynamic Media经典集成对视频进行编码，请参 [阅为Dynamic Media经典上传工作流添加可配置超时](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>从现有Dynamic Media经典公司帐户导入资产可能需要很长时间才能在AEM中显示。 请确保在Dynamic Media经典中指定一个资产不太多的文件夹（例如，根文件夹通常包含的资产过多）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

