---
title: 在 中，使用连接的资产共享 DAM 资产 [!DNL Sites]
description: 使用远程 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 部署中可用的资产。
contentOwner: AG
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: 3e4e9ab8b3940f539228bccf759dcade03a8b015
workflow-type: tm+mt
source-wordcount: '2967'
ht-degree: 26%

---

# 在 中，使用连接的资产共享 DAM 资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。一个原因可能是地理上分散的现有部署需要协同工作。 另一个原因可能是收购导致了母公司希望结合使用的不同基础架构，包括不同的[!DNL Experience Manager]版本。

“连接的资产”功能通过集成[!DNL Experience Manager Sites]和[!DNL Experience Manager Assets]支持上述用例。 用户可以在[!DNL Sites]中创建网页，这些网页将使用单独的[!DNL Assets]部署中的数字资产。

## 连接的资产概述 {#overview-of-connected-assets}

在[!UICONTROL 页面编辑器]中编辑页面作为目标目标时，作者可以从其他充当资产源的[!DNL Assets]部署中无缝搜索、浏览和嵌入资产。 管理员将具有[!DNL Sites]功能的[!DNL Experience Manager]部署与具有[!DNL Assets]功能的[!DNL Experience Manager]的另一部署创建一次性集成。 网站作者还可以通过连接的资产在其网站网页中使用Dynamic Media图像，并利用Dynamic Media功能，如智能裁剪和图像预设。

对于[!DNL Sites]作者，远程资产可用作只读本地资产。 该功能可支持一次无缝搜索和使用多个远程资产。要在[!DNL Sites]部署中一次性使用许多远程资产，请考虑批量迁移这些资产。 请参阅[Experience Manager资产迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于[!DNL Adobe Experience Manager]部署类型，满足支持的一个条件。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 与 [!DNL Experience Manager] 作为Cloud Service。有关此功能如何在[!DNL Experience Manager]中作为[!DNL Cloud Service]使用的更多信息，请参阅 [!DNL Experience Manager] 中的[连接的资产(a [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html))。

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] AMS上的 [!DNL Sites] 6.5 | [!DNL Experience Manager] 6.5内 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]AMS上的 [!DNL Assets] 6.5** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5内 [!DNL Assets] 部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索到的资产。 文档会添加到`Download`组件，图像会添加到`Image`组件。 此外，作者还会在任何自定义[!DNL Experience Manager]组件中添加远程资产，这些组件扩展了默认`Download`或`Image`组件。 支持的格式包括：

* **图像格式**:图像组件支 [持](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html) 的格式。
* **文档格式**:请参阅支 [持的文档格式](assets-formats.md#supported-document-formats)。

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。作者创建网页的用例使用本地范围。 对于托管所需资产的 DAM 部署，使用远程范围。[!DNL Sites]作者会获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 要求 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | [!DNL Experience Manager] `administrators` | `admin` | 设置[!DNL Experience Manager]并配置与远程[!DNL Assets]部署的集成。 |
| DAM 用户 | 本地 | `Authors` | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | <ul><li>`Authors` (具有对远程DAM的读取访问权限，以及对本地的创作访问 [!DNL Sites]权限) </li> <li>`dam-users` 本地  [!DNL Sites]</li></ul> | `ksaner` | 最终用户是[!DNL Sites]作者，他们使用此集成来提高内容速度。 作者使用[!UICONTROL 内容查找器]和使用本地网页中所需的图像来搜索和浏览远程DAM中的资产。 使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | [!DNL Experience Manager] `administrators` | `admin` 远程  [!DNL Experience Manager] | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | `Authors` | `ksaner` 远程  [!DNL Experience Manager] | 远程[!DNL Experience Manager]部署上的创作角色。 使用[!UICONTROL 内容查找器]搜索和浏览“连接的资产”中的资产。 |
| DAM 分发人员（技术用户） | 远程 | [!DNL Sites] `Authors` | `ksaner` 远程  [!DNL Experience Manager] | [!DNL Experience Manager]本地服务器（而非[!DNL Sites]作者角色）代表[!DNL Sites]作者，使用远程部署上存在的用户来获取远程资产。 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

## 在[!DNL Sites]部署和[!DNL Assets]部署之间配置连接 {#configure-a-connection-between-sites-and-assets-deployments}

[!DNL Experience Manager]管理员可以创建此集成。 创建后，使用该组件所需的权限会通过用户组建立。 用户组在[!DNL Sites]部署和DAM部署中定义。

要配置连接的资产和本地[!DNL Sites]连接，请执行以下步骤：

1. 访问现有的[!DNL Sites]部署或使用以下命令创建部署：

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建每个[!DNL Experience Manager]服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，[!DNL Experience Manager]服务器成功启动。 将此[!DNL Sites]部署视为用于网页创作的本地计算机，例如`https://[local_sites]:4502`。

1. 确保在AMS的[!DNL Sites]部署和[!DNL Assets]部署中存在具有适当范围的用户和角色。 在[!DNL Assets]部署中创建技术用户，并将其添加到[涉及的用户和组中所述的用户组。](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)

1. 在`https://[local_sites]:4502`访问本地[!DNL Sites]部署。 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. 配置的&#x200B;**[!UICONTROL 标题]**。
   1. **[!UICONTROL 远程]** DAM URL是格式 [!DNL Assets] 中位置的URL  `https://[assets_servername]:[port]`。
   1. DAM 分发人员（技术用户）的凭据。
   1. 在&#x200B;**[!UICONTROL 装入点]**&#x200B;字段中，输入[!DNL Experience Manager]获取资产的本地[!DNL Experience Manager]路径。 例如，`remoteassets` 文件夹。从DAM获取的资产将存储在[!DNL Sites]部署的此文件夹中。
   1. **[!UICONTROL 本地]** 站点URL是部署的位 [!DNL Sites] 置。[!DNL Assets] 部署使用此值维护对此部署获取的数字资产的 [!DNL Sites] 引用。
   1. [!DNL Sites]技术用户的凭据。
   1. **[!UICONTROL 原始二进制传输优化阈值]**&#x200B;字段的值指定原始资产（包括演绎版）是否同步传输。 可以轻松获取文件大小较小的资产，而文件大小相对较大的资产最好异步同步。 此值取决于您的网络功能。
   1. 如果您使用数据存储来存储您的资产，且数据存储是两个 部署之间的公用存储，请选择&#x200B;**[!UICONTROL 与连接的资产共享数据存储]**。在这种情况下，阈值限制无关紧要，因为数据存储上有实际的资产二进制文件，并且不会传输。

   ![连接的资产功能的典型配置](assets/connected-assets-typical-config.png)

   *图：连接的资产功能的典型配置。*

1. 已处理[!DNL Assets]部署中的现有数字资产，并生成演绎版。 使用此功能可获取这些演绎版，因此无需重新生成演绎版。 禁用工作流启动器，以阻止重新生成演绎版。 在([!DNL Sites])部署中调整启动器配置，以排除`connectedassets`文件夹（此文件夹中会获取资产）。

   1. 在[!DNL Sites]部署中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**。

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在[!UICONTROL 属性]向导中，将&#x200B;**[!UICONTROL 路径]**&#x200B;字段更改为以下映射，以更新其正则表达式，以排除装入点&#x200B;**[!UICONTROL connectedassets]**。

   | 之前 | 之后 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >在作者获取资产时，将会获取该资产在远程 部署中可用的所有演绎版。如果要为获取的资产创建更多演绎版，请跳过此配置步骤。将触发[!UICONTROL DAM更新资产]工作流并创建更多演绎版。 这些演绎版仅在本地[!DNL Sites]部署中可用，而在远程DAM部署中则不可用。

1. 在[!DNL Assets]部署的CORS配置中，将[!DNL Sites]部署添加为允许的源。 有关更多信息，请参阅[了解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)。

1. 配置[同一站点Cookie支持](/help/sites-administering/same-site-cookie-support.md)。

您可以检查已配置的[!DNL Sites]部署与[!DNL Assets]部署之间的连接。

![已连接资产的连接测试配 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*置图：已配置连接资产的连接测 [!DNL Sites]试。*

### 配置Dynamic Media资产的连接{#sites-dynamic-media-connected-assets}

您可以在[!DNL Sites]部署和[!DNL Dynamic Media]部署之间配置连接，以允许网页作者在其网页中使用[!DNL Dynamic Media]图像。 在创作网页时，使用远程资产和远程[!DNL Dynamic Media]部署的体验保持不变。

要为Dynamic Media部署配置“连接的资产”功能，请执行以下步骤：

1. 在远程[!DNL Assets]作者部署上启用[!DNL Dynamic Media]并将其配置为全局配置。 要配置Dynamic Media，请参阅[配置Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)。<br/>
在远程 [!DNL Assets] 部署中，在 [!UICONTROL Dynamic Media同步模式]下，选 **[!UICONTROL 择默认启用]**。

1. 创建连接的资产配置，如[配置站点与资产部署之间的连接](#configure-a-connection-between-sites-and-assets-deployments)中所述。 此外，选择&#x200B;**[!UICONTROL 为Dynamic Media连接的资产获取原始呈现版本]**&#x200B;选项。

1. 在本地[!DNL Sites]和远程[!DNL Assets]部署上配置[!DNL Dynamic Media]。 按照[configure [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services)的说明操作。

   * 在所有配置中使用相同的公司名称。
   * 在本地[!DNL Sites]上的[!UICONTROL Dynamic Media同步模式]中，选择&#x200B;**[!UICONTROL 默认情况下禁用]**。 [!DNL Sites]部署只需要对[!DNL Dynamic Media]帐户进行只读访问。
   * 在本地[!DNL Sites]的&#x200B;**[!UICONTROL 发布资产]**&#x200B;选项中，选择&#x200B;**[!UICONTROL 选择性发布]**。 请勿选择&#x200B;**[!UICONTROL 同步所有内容]**。

1. 在图像核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media)中启用[[!DNL Dynamic Media] 支持。 当作者在本地[!DNL Sites]部署的网页中使用[!DNL Dynamic Media]图像时，此功能允许默认的[图像组件](https://www.aemcomponents.dev/content/core-components-examples/library/page-authoring/image.html)显示[!DNL Dynamic Media]图像。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器连接到DAM部署。 作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程 DAM，请准备好管理员提供的 DAM 用户凭据。

作者可以在单个网页中使用本地DAM和远程DAM部署中可用的资产。 使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

只会获取那些具有与本地[!DNL Sites]部署中可用的相同分类层次结构完全对应的标记的远程资产标记。 任何其他标记都将被丢弃。作者可以使用远程[!DNL Experience Manager]部署中存在的所有标记来搜索远程资产，因为它提供了全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 通过从[!DNL Experience Manager]工作区访问&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**，导航到远程部署上的[!DNL Assets]接口。 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在[!DNL Sites]部署中，在右上角的配置文件激活器中，单击&#x200B;**[!UICONTROL 模拟为]**。 提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开[!UICONTROL Assets]选项卡，然后单击&#x200B;**[!UICONTROL 登录到连接的资产]**。
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户对两个[!DNL Experience Manager]部署都具有创作权限。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   获取的资产在本地[!DNL Sites]部署上为只读。 您仍可以使用[!DNL Sites]组件提供的选项来编辑获取的资产。 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项.*

1. 如果异步获取资产且获取任务失败，会通知站点作者。在创作过程中甚至在创作后，作者可以在[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面中查看有关获取任务和错误的详细信息。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. 发布页面时， [!DNL Experience Manager]会显示页面上使用的资产的完整列表。 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请参阅[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，页面也会发布。使用该远程资产的组件发布为空。[!DNL Experience Manager]通知区域显示异步作业页面中显示错误的通知。

>[!CAUTION]
>
>获取的远程资产一经在网页中使用后，有权访问本地文件夹的任何人都可以搜索和使用这些已获取的资产。 获取的资产存储在本地文件夹中（上述演练的`connectedassets`）。 此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

### 检查跨网页的资产使用情况 {#asset-usage-references}

[!DNL Experience Manager] 允许DAM用户检查对资产的所有引用。它有助于了解和管理远程[!DNL Sites]和复合资产中资产的使用情况。 [!DNL Experience Manager Sites]部署中的许多网页作者可以在不同网页中的远程[!DNL Assets]上使用资产。 为了简化资产管理，并且不会导致引用损坏，DAM用户必须检查本地和远程网页中资产的使用情况。 资产的[!UICONTROL 属性]页面中的[!UICONTROL 引用]选项卡列出了资产的本地和远程引用。

要查看和管理[!DNL Assets]部署上的引用，请执行以下步骤：

1. 在[!DNL Assets]控制台中选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]** 。
1. 单击&#x200B;**[!UICONTROL 引用]**&#x200B;选项卡。 有关在[!DNL Assets]部署中使用资产的信息，请参阅&#x200B;**[!UICONTROL 本地引用]**。 请参阅**[!UICONTROL 远程引用]，以了解在[!DNL Sites]部署中使用“连接的资产”功能获取资产的资产的用法。

   ![资产属性页面中的远程引用](assets/connected-assets-remote-reference.png)

1. [!DNL Sites]页面的引用显示每个本地[!DNL Sites]的引用总数。 查找所有引用并显示引用总数可能需要一些时间。
1. 引用列表是交互式的，DAM用户可以单击引用以打开引用页面。 如果由于某些原因无法获取远程引用，则会显示通知，告知用户失败。
1. 用户可以移动或删除资产。 移动或删除资产时，所有选定资产/文件夹的引用总数会显示在警告对话框中。 删除尚未显示引用的资产时，会显示一个警告对话框。

   ![强制删除警告](assets/delete-referenced-asset.png)

## 限制和最佳实践 {#tip-and-limitations}

* 要深入了解资产使用情况，请在[!DNL Sites]实例上配置[资产分析](/help/assets/asset-insights.md)功能。

### 权限和资产管理 {#permissions-and-managing-assets}

* 本地资产与远程部署中的原始资产不同步。在 DAM 部署上所具有的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。[!DNL Experience Manager] 组件对资产进行无损编辑。不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Content Fragments] 和 [!DNL Experience Fragments] 不受支持。
* [!DNL Experience Manager] 不会获取元数据架构。这意味着可能无法显示所有获取的元数据。 如果在[!DNL Sites]部署中单独更新了架构，则会显示所有元数据属性。
* 所有[!DNL Sites]作者都对获取的副本具有读取权限，即使作者无法访问远程DAM部署。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 在[!UICONTROL 页面属性]用户界面上，不能将远程资产用作页面缩略图。 通过单击[!UICONTROL 选择图像]，可以在[!UICONTROL 缩略图]的用户界面中，在[!UICONTROL 页面属性]中设置网页的缩略图。

### 设置和许可 {#setup-licensing}

* [!DNL Assets] 支持在 [!DNL Adobe Managed Services] 上部署。
* [!DNL Sites] 一次可以连接 [!DNL Assets] 到单个存储库。
* [!DNL Assets]的许可证需要用作远程存储库。
* 需要[!DNL Sites]的一个或多个许可证用作本地创作部署。

### 使用 {#usage}

* 用户在创作时，可以搜索远程资产并将这些资产拖动到本地页面上。 不支持其他功能。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过将远程资产从[!UICONTROL 内容查找器]拖到[!UICONTROL 页面编辑器]来重新尝试获取资产。
* 可以对获取的资产执行无损的简单编辑以及 `Image` 组件支持的编辑。资产是只读的。
* 重新获取资产的唯一方法是将资产拖动到页面上。 不支持API或其他方法来重新获取资产以更新资产。
* 如果资产从DAM中停用，则这些资产将继续在[!DNL Sites]页面上使用。
* 异步获取资产的远程引用条目。 引用和总计数不是实时的，如果站点作者在DAM用户查看引用时使用资产，则可能会有一些差异。 DAM用户可以刷新页面，然后在几分钟内重试，以获取总计数。

## 故障诊断问题 {#troubleshoot}

要对常见错误进行故障诊断，请执行以下步骤：

* 如果您无法从[!UICONTROL 内容查找器]搜索远程资产，请确保拥有所需的角色和权限。

* 从远程DAM获取的资产可能由于一个或多个原因无法发布在网页上。 它不存在于远程服务器上，缺少获取它的适当权限，或者网络故障可能是原因。 确保资产未从远程DAM中删除。 确保拥有适当的权限并满足先决条件。 重试将资产添加到页面并重新发布。 检查[异步作业列表](/help/sites-administering/asynchronous-jobs.md)，查看是否发生了资产获取错误。

* 如果您无法从本地[!DNL Sites]部署访问远程DAM部署，请确保允许跨站点Cookie，并配置了[同一站点Cookie支持](/help/sites-administering/same-site-cookie-support.md)。 如果阻止跨站点Cookie，则[!DNL Experience Manager]的部署可能无法进行身份验证。 例如，在“隐身”模式下，[!DNL Google Chrome]可能会阻止第三方Cookie。 要允许[!DNL Chrome]浏览器中的Cookie，请单击地址栏中的“眼睛”图标，导航到&#x200B;**站点不工作** > **阻止的**，选择远程DAM URL并允许登录令牌Cookie。 或者，请参阅[如何启用第三方Cookie](https://support.google.com/chrome/answer/95647)。

   ![Chrome浏览器中的“隐身”模式出现Cookie错误](assets/chrome-cookies-incognito-dialog.png)

* 如果未检索到远程引用并导致出现错误消息，请检查[!DNL Sites]部署是否可用，并检查网络连接问题。 稍后重试以检查。 [!DNL Assets] 部署尝试两次建立与部署的 [!DNL Sites] 连接，然后报告失败。

   ![检索资产远程引用失败](assets/reference-report-failure.png)



