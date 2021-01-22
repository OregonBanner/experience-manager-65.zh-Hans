---
title: 与Dynamic Media经典集成
description: 了解如何将Adobe Experience Manager与Dynamic Media经典相集成。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '5452'
ht-degree: 1%

---


# 与Dynamic Media经典{#integrating-with-dynamic-media-classic-scene}集成

AdobeDynamic Media经典是用于管理、增强、发布和将富媒体资产交付到Web、移动、电子邮件以及连接Internet的显示屏和印刷品的托管解决方案。

要使用Dynamic Media经典，您需要配置云配置，以便Dynamic Media经典和AEM Assets能够相互交互。 本文档介绍如何配置AEM和Dynamic Media经典。

有关在页面上使用所有Dynamic Media经典组件和处理视频的信息，请参阅[使用Dynamic Media经典](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media经典的DHTML查看器平台于2014年1月31日正式停止使用。 有关详细信息，请参阅[DHTML查看器生命周期结束常见问题解答](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在将Dynamic Media经典配置为与AEM结合使用之前，请参阅[将Dynamic Media经典与AEM集成的最佳实践](#best-practices-for-integrating-scene-with-aem)。
>* 如果您正在将Dynamic Media经典与自定义代理配置结合使用，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些则使用4.x API。 3.x配置有[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient),4.x配置有[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)。

>



## AEM/Dynamic Media经典集成与Dynamic Media{#aem-scene-integration-versus-dynamic-media}

AEM用户可以选择两种解决方案来使用dynamic media:将AEM实例与Dynamic Media经典集成，或使用集成到AEM的Dynamic Media解决方案。

使用以下条件确定要选择的解决方案：

* 如果您是&#x200B;**现有** Dynamic Media经典客户，其富媒体资产驻留在Dynamic Media经典中进行发布和投放，但您希望将这些资产与站点(WCM)创作和／或AEM Assets集成以进行管理，请使用本文档中所述的[AEM/Dynamic Media经典点对点集成](#aem-scene-point-to-point-integration)。

* 如果您是&#x200B;**新** AEM客户，具有富媒体投放需求，请选择[Dynamic Media选项](#aem-dynamic-media)。 如果您没有现有的S7帐户，并且该系统中存储了许多资产，则此选项最有意义。

* 在某些情况下，您可能希望同时使用这两种解决方案。 [双用方案](/help/sites-administering/scene7.md#dual-use-scenario)描述了该方案。

### AEM/Dynamic Media经典点对点集成{#aem-scene-point-to-point-integration}

在此解决方案中处理资产时，您需要执行下列操作之一：

* 将资产直接上传到Dynamic Media经典，然后通过&#x200B;**Dynamic Media经典**&#x200B;内容浏览器访问，以进行页面创作或
* 上传到AEM Assets，然后启用自动发布到Dynamic Media经典；可通过&#x200B;**资产**&#x200B;内容浏览器进行页面创作

您用于此集成的组件位于[设计模式的&#x200B;**Dynamic Media经典**&#x200B;组件区域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEMDynamic Media{#aem-dynamic-media}

AEMDynamic Media直接在AEM平台内统一了Dynamic Media经典功能。

在此解决方案中处理资产时，您可以遵循以下工作流：

1. 将单个图像和视频资产直接上传到AEM。
1. 在AEM内直接对视频进行编码。
1. 直接在AEM内构建基于图像的集。
1. 如果适用，为图像或视频添加交互性。

您用于Dynamic Media的组件位于[设计模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件区域。 包括：

* **[!UICONTROL Dynamic Media]** -动 **[!UICONTROL 态]** 媒体组件是智能的——根据您添加的是图像还是视频，您有各种选项。该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

* **[!UICONTROL 交互式媒体]** -交 **[!UICONTROL 互]** 式媒体组件适用于在热点或图像地图等资源上具有交互性的资源，如传送横幅、交互式图像和交互式视频。此组件是智能的——根据您添加的是图像还是视频，您有各种选项。 此外，查看器是响应式的 - 其屏幕大小可根据设备屏幕大小自动进行更改。所有查看器都是 HTML5 查看器。

### 双用途方案{#dual-use-scenario}

开箱即用，您可以同时使用Dynamic Media和Dynamic Media经典集成的AEM功能。 下面的使用案例表描述了在打开和关闭某些区域时的情况。

要同时使用Dynamic Media和Dynamic Media经典：

1. 在云服务中配置[Dynamic Media经典](#creating-a-cloud-configuration-for-scene)。
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
    <td>站点和Dynamic Media</td>
    <td>将资产上传到AEM并使用AEMDynamic Media组件在站点页面上创作资产</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>零售业，对Sites和Dynamic Media不熟悉</td>
    <td>将非产品资产上传至AEM以进行管理和投放。 将产品资产上传到Dynamic Media经典，使用AEM和组件中的Dynamic Media经典内容浏览器在站点上创作产品详细信息页面。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>资产新手和Dynamic Media</td>
    <td>将资产上传到AEM Assets，并使用Dynamic Media发布的URL/嵌入代码</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>Dynamic Media与模板</td>
    <td>使用Dynamic Media进行成像和视频。 在Dynamic Media经典中创作图像模板，并使用Dynamic Media经典内容查找器将模板包含在站点页面中。</td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">开启</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有的Dynamic Media经典客户，不熟悉站点</td>
    <td>将资产上传到Dynamic Media经典，并使用AEMDynamic Media经典内容浏览器在站点页面上搜索和创作资产</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td>关闭</td>
    </tr>
    <tr>
    <td>现有的Dynamic Media经典客户，熟悉站点和资产</td>
    <td>将资产上传到DAM并自动发布到Dynamic Media经典以供投放。 使用AEMDynamic Media经典内容浏览器在站点页面上搜索和创作资产。</td>
    <td>关闭</td>
    <td>关闭</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">开启</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    <tr>
    <td>现有Dynamic Media经典客户和新资产</td>
    <td><p>将资产上传到AEM，然后使用Dynamic Media生成再现以供下载／共享。 自动将AEM资产发布到Dynamic Media经典以进行投放。</p> <p><strong>重要：在</strong> AEM中生成的重复处理和再现将不会同步到Dynamic Media经典</p> </td>
    <td><p>开启</p> <p>（见步骤3）</p> </td>
    <td>关闭</td>
    <td>关闭</td>
    <td><p><a href="#configuringautouploadingfromaemassets">开启</a></p> <p>（见步骤4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可选；请参阅用例表)-设置[Dynamic Media云配置](/help/assets/config-dynamic.md)和[启用Dynamic Media服务器](/help/assets/config-dynamic.md)。
1. (可选；请参阅用例表)-如果您选择启用从资产自动上传到Dynamic Media经典，则需要添加以下内容：

   1. 设置自动上传到Dynamic Media经典。
   1. 在&#x200B;***Dam更新资产**工作流(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)末尾的所有Dynamic Media工作流步骤*&#x200B;之后添加&#x200B;**Dynamic Media经典上传**&#x200B;步骤
   1. （可选）按[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7资产MimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)中的MIME类型限制Dynamic Media经典资产上传。 此列表中未包含的资产MIME类型将不会上传到Dynamic Media经典服务器。
   1. （可选）在Dynamic Media经典配置中设置视频。 您可以同时为Dynamic Media和Dynamic Media经典启用视频编码。 动态演绎版用于在AEM实例中本地预览和回放，而Dynamic Media经典视频演绎版则生成并存储在Dynamic Media经典服务器上。 在为Dynamic Media和Dynamic Media经典设置视频编码服务时，将[视频处理用户档案](/help/assets/video-profiles.md)应用到Dynamic Media经典资源文件夹。
   1. （可选）[在Dynamic Media经典](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)中配置安全预览。

#### 限制 {#limitations}

启用Dynamic Media经典和Dynamic Media后，有以下限制：

* 通过选择资产并将其拖动到AEM页面上的Dynamic Media经典组件，手动上传到该经典。
* 即使AEM-Dynamic Media经典同步的资产在资产中编辑时会自动更新到Dynamic Media经典，但回滚操作不会触发新的上传，因此Dynamic Media经典在回滚后不会立即获得最新版本。 解决方法是在回滚完成后再次编辑。
* 如果您需要将Dynamic Media用于一个用例，将Dynamic Media经典集成用于另一个用例，以便Dynamic Media资源不与Dynamic Media经典系统交互，则请勿将Dynamic Media经典配置应用于Dynamic Media文件夹，或将Dynamic Media配置(处理用户档案)应用于Dynamic Media经典文件夹。

## 集成Dynamic Media经典与AEM {#best-practices-for-integrating-scene-with-aem}的最佳实践

在将Dynamic Media经典与AEM集成时，需要在以下方面遵循一些重要的最佳实践：

* 测试驱动集成
* 对于某些情况，建议直接从Dynamic Media经典上传资产

请参阅[已知限制](#known-limitations-and-design-implications)。

### 测试集成{#test-driving-your-integration}

Adobe建议您通过让根文件夹仅指向子文件夹而不是整个公司来测试集成。

>[!CAUTION]
>
>从现有的Dynamic Media经典公司帐户导入资源可能需要很长时间才能在AEM中显示。 请确保在Dynamic Media经典中指定的文件夹中的资源不太多（例如，根文件夹通常包含的资源过多，并且可能会导致系统崩溃）。

### 从AEM Assets上传资产与从Dynamic Media经典{#uploading-assets-from-aem-assets-versus-from-scene}上传资产

您可以通过使用资产（数字资产管理）功能，或通过直接通过Dynamic Media经典内容浏览器在AEM中访问Dynamic Media经典来上传资产。 您选择哪个取决于以下因素：

* Dynamic Media尚不支持的经典资产类型必须通过Dynamic Media经典内容浏览器（例如图像模板）从Dynamic Media经典直接添加到AEM网站。
* 对于AEM Assets和Dynamic Media经典都支持的资产类型，确定如何上传取决于以下各项：

   * 资产现在的位置，以及
   * 在通用存储库中管理它们的重要性

如果资产已在Dynamic Media经典中，而在通用存储库中管理资产并不重要，则仅将资产导出到AEM Assets以将其同步回Dynamic Media经典进行投放将是不必要的往返操作。 否则，最好将资产保留在单个存储库中，并仅同步到Dynamic Media经典以供投放。

## 配置Dynamic Media经典集成{#configuring-scene-integration}

您可以配置AEM以将资产上传到Dynamic Media经典。 可以从CQ目标文件夹中将资产（自动或手动）从AEM上传到Dynamic Media经典公司帐户。

>[!NOTE]
>
>Adobe建议您仅使用指定的目标文件夹来导入Dynamic Media经典资产。 驻留在目标文件夹以外的数字资产只能在启用了Dynamic Media经典配置的页面上的Dynamic Media经典组件中使用。 此外，它们还位于Dynamic Media经典中的临时文件夹中。 临时文件夹未与AEM同步(但资源可在Dynamic Media经典内容浏览器中发现)。

要将Dynamic Media经典配置为与AEM集成，您需要完成以下步骤：

1. [定义云配置](#creating-a-cloud-configuration-for-scene) -定义Dynamic Media经典文件夹与资产文件夹之间的映射。即使您只想单向(AEM Assets到Dynamic Media经典)同步，您也需要完成此步骤。
1. [启用 **Adobe CQ的s7dam Dam监听器**](#enabling-the-adobe-cq-scene-dam-listener) -在OSGiconsole中  完成。
1. 如果希望AEM资产自动上传到Dynamic Media经典，您需要打开此选项，并将Dynamic Media经典添加到[!UICONTROL DAM更新资产]工作流。 您还可以手动上传资产。
1. 将Dynamic Media经典组件添加到Sidekick。 这允许用户在其AEM页面上使用Dynamic Media经典组件。
1. [将配置映射到AEM中的页面](#enabling-scene-for-wcm) -需要此步骤来视图您在Dynamic Media经典中创建的任何视频预设。如果您需要将资产从CQ目标文件夹外部发布到Dynamic Media经典，则此操作也是必需的。

本节介绍如何执行所有这些步骤和列表重要限制。

### Dynamic Media经典与AEM Assets的同步如何工作{#how-synchronization-between-scene-and-aem-assets-works}

在设置AEM Assets和Dynamic Media经典同步时，请务必了解以下内容：

#### 从AEM Assets上传到Dynamic Media经典{#uploading-to-scene-from-aem-assets}

* AEM中存在一个指定的同步文件夹，用于Dynamic Media经典上传。
* 如果数字资产放在指定的同步文件夹中，则上传到Dynamic Media经典可以自动完成。
* AEM中的文件夹和子文件夹结构将在Dynamic Media经典中复制。

>[!NOTE]
>
>AEM在将元数据上传到Dynamic Media经典之前将其嵌入到XMP中，因此，在Dynamic Media经典中，元数据节点上的所有属性都以XMP的形式提供。

#### 已知限制和设计含义{#known-limitations-and-design-implications}

在AEM Assets和Dynamic Media经典之间进行同步后，目前存在以下限制／设计含义：

<table>
 <tbody>
  <tr>
   <td><strong>限制／设计含义</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>一个指定的同步(目标)文件夹</td>
   <td>对于Dynamic Media经典上传，在AEM中，每个公司只能有一个指定的文件夹。 如果您需要访问Dynamic Media经典中的多个公司帐户，可以创建多个配置。</td>
  </tr>
  <tr>
   <td>文件夹结构</td>
   <td>如果删除与资产同步的文件夹，则所有Dynamic Media经典远程资产都将被删除，但该文件夹仍会保留。</td>
  </tr>
  <tr>
   <td>临时文件夹</td>
   <td>在WCM中手动上传到Dynamic Media经典的目标文件夹外的资产将自动放在Dynamic Media经典上的单独点对点文件夹中。 您可以在AEM的云配置中进行配置。</td>
  </tr>
  <tr>
   <td>混合媒体</td>
   <td>混合媒体集显示在AEM中，但AEM中不支持它们。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>从Dynamic Media经典中的电子目录生成的PDF导入到CQ目标文件夹。</td>
  </tr>
  <tr>
   <td>UI刷新</td>
   <td>在AEM和Dynamic Media经典之间同步时，请务必刷新用户界面以视图更改。 </td>
  </tr>
  <tr>
   <td>视频缩略图</td>
   <td>如果将视频上传到AEM Assets以通过Dynamic Media经典进行编码，则视频缩略图和编码视频可能需要一些时间才能在AEM Assets发布，具体取决于视频处理时间。</td>
  </tr>
  <tr>
   <td>目标子文件夹</td>
   <td><p>如果您正在目标文件夹中使用子文件夹，请确保对每个资产使用唯一的名称（无论位置如何），或者配置Dynamic Media经典（在“设置”区域），不覆盖任何位置的资产。</p> <p>否则，上传到Dynamic Media经典目标子文件夹的同名资产会被上传，但目标文件夹中同名的资产会被删除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media经典服务器{#configuring-scene-servers}

如果在代理后运行AEM或具有特殊的防火墙设置，则可能需要显式启用不同区域的主机。 服务器在`/etc/cloudservices/scene7/endpoints`中的内容中进行管理，并可以根据需要进行自定义。 点按一个URL，然后根据需要进行编辑以更改该URL。 在AEM的早期版本中，这些值是硬编码的。

如果导航到`/etc/cloudservices/scene7/endpoints.html`，您将看到列出的服务器（并可以通过单击URL来编辑它们）:

![chlimage_1-296](assets/chlimage_1-296.png)

### 为Dynamic Media经典{#creating-a-cloud-configuration-for-scene}创建云配置

云配置定义Dynamic Media经典文件夹与AEM Assets文件夹之间的映射。 它需要配置为将AEM Assets与Dynamic Media经典同步。 有关详细信息，请参阅同步的工作方式。

>[!CAUTION]
>
>从现有的Dynamic Media经典公司帐户导入资源可能需要很长时间才能在AEM中显示。 确保在Dynamic Media经典中指定的文件夹不包含太多资产（例如，根文件夹通常包含过多资产）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

>[!NOTE]
>
>您可以有多个配置：一个云配置表示Dynamic Media经典公司的一个用户。 如果要访问其他Dynamic Media经典公司或用户，您需要创建多个配置。

要将AEM配置为能够将资产发布到Dynamic Media经典，请执行以下操作：

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**&#x200B;以访问AdobeDynamic Media经典。

1. 点按&#x200B;**[!UICONTROL 立即配置。]**

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中，或者在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，输入相应的信息。 点按&#x200B;**[!UICONTROL 创建。]**

   >[!NOTE]
   >
   >创建其他配置时，将显示&#x200B;**[!UICONTROL 父配置]**&#x200B;字段。
   >
   >**不**&#x200B;更改父配置。 更改父配置可能会中断集成。

1. 输入您的Dynamic Media经典帐户的电子邮件地址、密码和区域，然后点按&#x200B;**[!UICONTROL 连接到Dynamic Media经典。]** 您已连接到Dynamic Media经典服务器，对话框将扩展，显示更多选项。

1. 输入&#x200B;**[!UICONTROL 公司]**&#x200B;名称和&#x200B;**[!UICONTROL 根路径]**(这是已发布的服务器名称以及要指定的任何路径；如果您不知道已发布的服务器名称，请在“Dynamic Media经典”中，转至&#x200B;**[!UICONTROL 设置>应用程序设置。]**)

   >[!NOTE]
   >
   >Dynamic Media经典根路径是AEM连接到的Dynamic Media经典文件夹。 可以将其缩小到特定文件夹。

   >[!CAUTION]
   >
   >根据Dynamic Media经典文件夹的大小，导入根文件夹可能需要很长时间。 此外，Dynamic Media经典数据可能超过AEM存储。 确保导入的文件夹正确。 导入过多数据可能会停止系统。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 单击&#x200B;**[!UICONTROL 确定。]** AEM保存您的配置。

>[!NOTE]
>
>如果您正在重新连接：
>
>* 在发布时重新连接到Dynamic Media经典时，可能需要在发布时重置密码，或重新连接将无法工作。 这不是创作实例的问题。
>* 如果修改区域、公司名称等值，则必须重新连接到Dynamic Media经典。 如果配置选项已修改但未保存，AEM仍错误地指示配置有效。 确保重新连接。

>



### 启用Adobe CQDynamic Media经典Dam监听器{#enabling-the-adobe-cq-scene-dam-listener}

必须启用Adobe CQDynamic Media经典Dam监听器，默认情况下禁用它。

要启用它，请执行以下操作：

1. 点按[!UICONTROL 工具]图标，然后导航到&#x200B;**[!UICONTROL 操作> Web控制台。]** Web控制台将打开。
1. 导航到&#x200B;**[!UICONTROL Adobe CQDynamic Media经典Dam监听器]**&#x200B;并选中&#x200B;**[!UICONTROL 已启用]**&#x200B;复选框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 点按&#x200B;**[!UICONTROL 保存。]**

### 向Dynamic Media经典上传工作流{#adding-configurable-timeout-to-scene-upload-workflow}添加可配置超时

默认情况下，当AEM实例配置为通过Dynamic Media经典处理视频编码时，任何上传作业都会出现35分钟超时。 要适应可能运行时间较长的视频编码作业，可以配置此设置：

1. 导航到&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段中根据需要更改数字。 以秒为单位接受任何非负数。 默认情况下，此值设置为2100。

   >[!NOTE]
   >
   >最佳实践：大多数资源最多只需几分钟即可摄取（例如，图像）。 但在某些情况下（例如，视频较大），超时值应增加到7200秒（2小时）以适应较长的处理时间。 否则，此Dynamic Media经典上传作业在JCR元数据中标记为&#x200B;**[!UICONTROL UploadFailed]**。

1. 点按&#x200B;**[!UICONTROL 保存。]**

### 从AEM Assets偷渡{#autouploading-from-aem-assets}

从AEM 6.3.2开始，现在已为您配置AEM Assets，这样，如果资产位于CQ目标文件夹中，您上传到数字资产管理器的任何数字资产都将自动更新至Dynamic Media经典。

将资产添加到AEM Assets后，会自动上传并发布到Dynamic Media经典。

>[!NOTE]
>
>从AEM Assets自动上传到Dynamic Media经典的最大文件大小为500 MB。

从AEM Assets配置自动绘图：

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，然后在Dynamic Media标题下的可用配置下，点按&#x200B;**[!UICONTROL dms7(Dynamic Media]**)
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，选中&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;复选框，然后点按&#x200B;**[!UICONTROL 确定。]** 您现在需要配置DAM资产工作流，以包括上传到Dynamic Media经典。

   >[!NOTE]
   >
   >请参阅[配置推送到Dynamic Media经典](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)的资产的状态（已发布／未发布），以了解有关将资产推送到未发布状态的Dynamic Media经典的信息。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 导航回AEM欢迎页面，然后点按&#x200B;**[!UICONTROL 工作流。]** 多次单击 **DAM更新资** 产流以打开它。
1. 在Sidekick中，导航到&#x200B;**[!UICONTROL Workflow]**&#x200B;组件，然后选择&#x200B;**[!UICONTROL Dynamic Media经典。]** 将 **[!UICONTROL Dynamic Media]** 类拖到工作流中，然后点 **[!UICONTROL 按保存。]** 添加到“AEM Assets”文件夹中的资产将自动上传到“Dynamic Media经典”。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自动添加资产后，如果资产未放在CQ目标文件夹中，则不会将其上传到Dynamic Media经典。
   >* AEM在将元数据上传到Dynamic Media经典之前将其嵌入到XMP中，因此，在Dynamic Media经典中，元数据节点上的所有属性都以XMP的形式提供。


### 配置推送到Dynamic Media经典{#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}的资产的状态（已发布／未发布）

如果要将资产从AEM Assets推送到Dynamic Media经典，您可以自动发布资产（默认行为）或将资产推送到未发布状态的Dynamic Media经典。

如果要在上线前在分阶段环境测试资产，您可能不想立即在Dynamic Media经典上发布资产。 您可以将AEM与Dynamic Media经典的安全测试环境结合使用，将资产直接从资产推送到处于未发布状态的Dynamic Media经典。

Dynamic Media经典资产仍可通过安全预览获得。 只有在AEM中发布资产后，Dynamic Media经典资产才能在生产中投入使用。

如果要在将资产推送到Dynamic Media经典时立即发布资产，则无需配置任何选项。 这是默认行为。

但是，如果您不希望将资产推送到Dynamic Media经典以自动发布，本节将介绍如何配置AEM和Dynamic Media经典。

#### 将资产推送到未发布的Dynamic Media经典{#prerequisites-to-push-assets-to-scene-unpublished}的先决条件

在将资产推送到Dynamic Media经典而不发布之前，您必须设置以下各项：

1. [使用Admin Console创建支持案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 在您的支持情况下，请求为您的Dynamic Media经典帐户启用安全预览。
1. 按照[为您的Dynamic Media经典帐户设置安全预览的说明操作。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

这些步骤与在Dynamic Media经典中创建任何安全测试设置的步骤相同。

>[!NOTE]
>
>如果您的安装环境是Unix 64位操作系统，请参阅[https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)，了解需要设置的其他配置选项。

#### 将资产推入未发布状态的已知限制{#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，请注意以下限制：

* 不支持版本控制。
* 如果资产已在AEM中发布并且创建了后续版本，则新版本将立即实时发布到生产。 仅在激活时发布适用于资产的初始发布。

>[!NOTE]
>
>如果要立即发布资产，最佳实践是将&#x200B;**[!UICONTROL 启用安全预览]**&#x200B;设置为&#x200B;**[!UICONTROL 立即]**&#x200B;并使用&#x200B;**[!UICONTROL 启用自动上传]**&#x200B;功能。

### 将推送到Dynamic Media经典的资源状态设置为未发布{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果用户在AEM中发布资产，则会自动将S7资产触发到生产／实时资产(资产将不再处于安全预览/取消发布状态)。

将推送到Dynamic Media经典的资产状态设置为未发布：

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media经典]**，然后在Dynamic Media经典中选择您的配置。
1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 启用安全视图]**&#x200B;下拉菜单中，选择&#x200B;**[!UICONTROL 在AEM发布激活]**&#x200B;上，将资产推送到Dynamic Media经典而不进行发布。 (默认情况下，此值设置为&#x200B;**[!UICONTROL Immedialy]**，其中Dynamic Media经典资产会立即发布。)

   有关在资产公开前测试资产的详细信息，请参阅[Dynamic Media经典文档](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 点按&#x200B;**[!UICONTROL 确定。]**

启用安全视图意味着您的资产将推送到未发布的安全预览服务器。

您可以通过导航到AEM中页面上的Dynamic Media经典组件并点按&#x200B;**[!UICONTROL 编辑来选中此选项。]** 资产的URL中将列出安全预览服务器。在AEM中发布后，文件引用中的服务器域将从预览URL更新到生产URL。

### 为WCM启用Dynamic Media经典{#enabling-scene-for-wcm}

需要为WCM启用Dynamic Media经典，原因有二：

* 启用用于页面创作的通用视频用户档案的下拉列表。 如果没有此选项，则&#x200B;**[!UICONTROL 通用视频预设]**&#x200B;下拉框为空，无法设置。
* 如果数字资产不在目标文件夹中，则您可以在页面属性中为该页面启用Dynamic Media经典，然后将资产拖放到Dynamic Media经典组件上，即可将资产上传到Dynamic Media经典。 普通继承规则适用（这意味着子页面将从父页面继承配置）。

为WCM启用Dynamic Media经典时，请注意，与其他配置一样，继承规则也适用。 您可以在触屏优化或经典用户界面中为WCM启用Dynamic Media经典。

#### 在触屏优化用户界面{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}中为WCM启用Dynamic Media经典

要在触屏优化UI中为WCM启用Dynamic Media经典：

1. 点按AEM图标，然后导航到&#x200B;**[!UICONTROL 站点]**，然后导航到网站的根页面（不是特定语言）。

1. 在工具栏中，选择[!UICONTROL 设置]图标，然后点按&#x200B;**[!UICONTROL 打开属性。]**

1. 点按&#x200B;**[!UICONTROL Cloud Services]**，然后点按&#x200B;**[!UICONTROL 添加配置]**&#x200B;并选择&#x200B;**[!UICONTROL Dynamic Media经典。]**
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media经典]**&#x200B;下拉列表中，选择所需的配置并点按&#x200B;**[!UICONTROL 确定。]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   基于Dynamic Media经典配置的视频预设可在AEM中与该页面和子页面上的Dynamic Media经典视频组件一起使用。

#### 在经典用户界面{#enabling-scene-for-wcm-in-the-classic-user-interface}中为WCM启用Dynamic Media经典

要在经典UI中为WCM启用Dynamic Media经典：

1. 在AEM中，点按&#x200B;**[!UICONTROL 网站]**&#x200B;并导航到网站的根页面（非特定语言）。

1. 在Sidekick中，点按&#x200B;**[!UICONTROL 页面]**&#x200B;图标，然后点按&#x200B;**[!UICONTROL 页面属性。]**

1. 点按&#x200B;**[!UICONTROL Cloud Services>添加服务>Dynamic Media经典。]**
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media经典]**&#x200B;下拉列表中，选择所需的配置并点按&#x200B;**[!UICONTROL 确定。]**

   基于Dynamic Media经典配置的视频预设可在AEM中与该页面和子页面上的Dynamic Media经典视频组件一起使用。

### 配置默认配置{#configuring-a-default-configuration}

如果您有多个Dynamic Media经典配置，则可以指定其中一个配置作为Dynamic Media经典内容浏览器的默认配置。

在给定时刻，只能将一个Dynamic Media经典配置标记为默认。 默认配置是默认在Dynamic Media经典内容浏览器中显示的公司资产。

配置默认配置：

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media经典]**，然后在Dynamic Media经典中选择您的配置。
1. 点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开配置。

1. 在&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，选中&#x200B;**[!UICONTROL 默认配置]**&#x200B;复选框，使其成为在Dynamic Media经典内容浏览器中显示的默认公司和根路径。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一个配置，则选中&#x200B;**[!UICONTROL 默认配置]**&#x200B;复选框将不起作用。

### 配置临时文件夹{#configuring-the-ad-hoc-folder}

当资产不在CQ目标文件夹中时，您可以配置资产上传到Dynamic Media经典中的文件夹。 请参阅从CQ目标文件夹外部发布资产。

配置临时文件夹：

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 部署>Cloud Services]**，点按&#x200B;**[!UICONTROL Dynamic Media经典]**，然后在Dynamic Media经典中选择您的配置。
1. 点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开配置。

1. 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 临时文件夹]**&#x200B;字段中，可以修改&#x200B;**临时**&#x200B;文件夹。 默认情况下，它为&#x200B;**name_of_the_公司/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用预设{#configuring-universal-presets}

要为视频组件配置通用预设，请参阅[视频](/help/assets/s7-video.md)。

## 启用基于MIME类型的资产/Dynamic Media经典上传作业参数支持{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以启用可配置的Dynamic Media经典上传作业参数，这些参数由数字资产管理器/Dynamic Media经典资产的同步触发。

具体而言，在AEM Web Console“配置”面板的OSGi（Open Service Gateway活动）区域按MIME类型配置接受的文件格式。 然后，您可以自定义单个上传作业参数，这些参数用于JCR（Java内容存储库）中的每个MIME类型。

**要启用基于MIME类型的资产，请执行以下操作：**

1. 点按AEM图标并导航到&#x200B;**[!UICONTROL 工具>操作> Web控制台。]**
1. 在“Adobe Experience ManagerWeb控制台配置”面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;菜单上，点按&#x200B;**[!UICONTROL 配置。]**
1. 在“名称”列下，找到并点按&#x200B;**[!UICONTROL Adobe CQDynamic Media经典资产MIME类型服务]**&#x200B;以编辑配置。
1. 在“Mime类型映射”区域，点按任何加号(+)以添加MIME类型。

   请参阅[支持的MIME类型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文本字段中，键入新的MIME类型名称。

   例如，您应键入`<file_extension>=<mime_type>` ，如`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`所示。

1. 在配置窗口的右下角，点按&#x200B;**[!UICONTROL 保存。]**
1. 返回AEM，在左边栏中点按CRXDE Lite。
1. 在CRXDE Lite页的左边栏中，导航到`/etc/cloudservices/scene7/<environment>`（用`<environment>`替换实际名称）。
1. 展开`<environment>`（用`<environment>`替换实际名称）以显示`mimeTypes`节点。
1. 点按刚刚添加的mimeType。

   例如，`mimeTypes > application_postscript`或`mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite页的右侧，点按&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中指定Dynamic Media经典上传作业参数。

   例如，`psprocess="rasterize"&psresolution=120`。

   有关可使用的其他上传作业参数，请参阅[AdobeDynamic Media经典图像生产系统API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)。

   >[!NOTE]
   >
   >如果要上传PSD文件，并且要将其作为具有图层提取的模板进行处理，请在&#x200B;**[!UICONTROL jobParam]**&#x200B;值字段中输入以下内容：
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >确保您的PSD文件具有“图层”。 如果它只是一幅图像或带有遮罩的图像，则它将作为图像处理，因为没有要处理的图层。

1. 在CRXDE Lite页的左上角，点按&#x200B;**[!UICONTROL 全部保存。]**

## Dynamic Media经典和AEM集成故障排除{#troubleshooting-scene-and-aem-integration}

如果您在将AEM与Dynamic Media经典集成时遇到问题，请参阅以下解决方案情景。

**如果您的数字资产发布到Dynamic Media经典版失败：**

* 检查您尝试上传的资产是否位于&#x200B;**[!UICONTROL CQ目标]**&#x200B;文件夹中(您应在Dynamic Media经典云配置中指定此文件夹)。
* 否则，您需要在该页面的&#x200B;**[!UICONTROL 页面属性]**&#x200B;中配置云配置，以允许上传到&#x200B;**[!UICONTROL CQ adhoc]**&#x200B;文件夹。

* 检查日志中是否有任何信息。

**如果视频预设未显示：**

* 确保已通过&#x200B;**[!UICONTROL 页面属性配置该页面的云配置。]** 视频预设在Dynamic Media经典视频组件中可用。

**如果您的视频资源不在AEM中播放：**

* 确保您使用了正确的视频组件。 Dynamic Media经典视频组件与基础视频组件不同。 请参阅[基础视频组件与Dynamic Media经典视频组件](/help/assets/s7-video.md)。

**如果AEM中的新资产或已修改的资产不会自动上传到Dynamic Media经典：**

* 确保资产位于CQ目标文件夹中。 只有CQ目标文件夹中的资产才会自动更新(前提是您已将AEM Assets配置为自动上传资产)。
* 确保您已将Cloud Services配置配置为启用自动上传，并且已更新并保存DAM资产工作流以包括Dynamic Media经典上传。
* 将图像上传到Dynamic Media经典目标文件夹的子文件夹时，请确保执行以下操作之一：

   * 确保所有资产的名称（不管位置如何）都是唯一的。 否则，主目标文件夹中的资产将被删除，并且只保留子文件夹中的资产。
   * 更改Dynamic Media经典如何覆盖Dynamic Media经典帐户的“设置”区域中的资产。 如果在子文件夹中使用名称相同的资源，请勿设置“Dynamic Media经典”来覆盖资源，而不考虑位置。

**如果已删除的资产或文件夹未在Dynamic Media经典与AEM之间同步：**

* 在AEM Assets删除的资产和文件夹仍显示在Dynamic Media经典的同步文件夹中。 必须手动删除它们。

**如果视频上传失败**

* 如果视频上传失败，并且您正在使用AEM通过Dynamic Media经典集成对视频进行编码，请参阅[向Dynamic Media经典上传工作流添加可配置超时](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>从现有的Dynamic Media经典公司帐户导入资源可能需要很长时间才能在AEM中显示。 确保在Dynamic Media经典中指定的文件夹不包含太多资产（例如，根文件夹通常包含过多资产）。
>
>如果要测试集成，您可能希望根文件夹仅指向子文件夹，而不是指向整个公司。

