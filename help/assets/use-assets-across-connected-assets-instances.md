---
title: 在 中，使用连接的资产共享 DAM 资产 [!DNL Sites]
description: 使用远程设备上可用的资产 [!DNL Adobe Experience Manager Assets] 在另一个页面上创建网页时进行部署 [!DNL Adobe Experience Manager Sites] 部署。
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
source-git-commit: cd7800546ec4ebc950c5ebca4d7c80779cb2632c
workflow-type: tm+mt
source-wordcount: '3877'
ht-degree: 18%

---

# 在 中，使用连接的资产共享 DAM 资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | 本文 |


在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。一个原因可能是地理上分散的现有部署需要协同工作。 另一个原因可能是收购导致不同的基础架构，包括不同 [!DNL Experience Manager] 版本，父公司希望结合使用的版本。

“连接的资产”功能通过集成支持上述用例 [!DNL Experience Manager Sites] 和 [!DNL Experience Manager Assets]. 用户可以在 [!DNL Sites] 从单独的 [!DNL Assets] 部署。

>[!NOTE]
>
>仅当您需要在单独的Sites部署中使用远程DAM部署中可用的资产来创作网页时，才配置连接的资产。

## 连接的资产概述 {#overview-of-connected-assets}

在中编辑页面时 [!UICONTROL 页面编辑器] 作为target目标，作者可以从其他位置无缝搜索、浏览和嵌入资产 [!DNL Assets] 用作资产源的部署。 管理员可创建部署的一次性集成 [!DNL Experience Manager] with [!DNL Sites] 能力与另一部署 [!DNL Experience Manager] with [!DNL Assets] 功能。 网站作者还可以通过连接的资产在其网站网页中使用Dynamic Media图像，并利用Dynamic Media功能，如智能裁剪和图像预设。

对于 [!DNL Sites] 作者，远程资产可用作只读本地资产。 该功能支持在站点编辑器上无缝搜索和访问远程资产。 对于可能需要在站点上提供完整资产语料库的任何其他用例，请考虑批量迁移资产，而不是使用连接的资产。 请参阅 [Experience Manager Assets迁移指南](/help/assets/assets-migration-guide.md).

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于 [!DNL Adobe Experience Manager] 部署类型中，满足支持的标准之一。 [!DNL Experience Manager] 6.5 [!DNL Assets] 与 [!DNL Experience Manager] as a Cloud Service。 有关此功能在中的工作方式的更多信息 [!DNL Experience Manager] as a [!DNL Cloud Service]，请参阅 [Experience Manageras a Cloud Service中的连接资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] 在AMS上 | [!DNL Experience Manager] 6.5 [!DNL Sites] 内部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] 在AMS上** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] 内部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中拖动搜索到的资产。 文档将添加到 `Download` 组件和图像 `Image` 组件。 作者还可以在任何自定义中添加远程资产 [!DNL Experience Manager] 扩展默认值的组件 `Download` 或 `Image` 组件。 支持的格式包括：

* **图像格式**:格式 [图像组件](assets-formats.md#supported-raster-image-formats) 支持。
* **文档格式**:请参阅 [支持的文档格式](assets-formats.md#supported-document-formats).

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。作者创建网页的用例使用本地范围。 对于托管所需资产的 DAM 部署，使用远程范围。的 [!DNL Sites] 作者会获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 描述 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | [!DNL Experience Manager] `administrators` | `admin` | 设置 [!DNL Experience Manager] 和配置与远程设备的集成 [!DNL Assets] 部署。 |
| DAM 用户 | 本地 | `Authors` | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | <ul><li>`Authors` (具有对远程DAM的读取访问权限，以及对本地的创作访问权限 [!DNL Sites]) </li> <li>`dam-users` 本地 [!DNL Sites]</li></ul> | `ksaner` | 最终用户包括 [!DNL Sites] 使用此集成提高内容速度的作者。 作者使用 [!UICONTROL 内容查找器] 以及在本地网页中使用所需的图像。 使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | [!DNL Experience Manager] `administrators` | `admin` 远程 [!DNL Experience Manager] | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | `Authors` | `ksaner` 远程 [!DNL Experience Manager] | 远程上的创作角色 [!DNL Experience Manager] 部署。 使用 [!UICONTROL 内容查找器]. |
| DAM 分发人员（技术用户） | 远程 | [!DNL Sites] `Authors` | `ksaner` 远程 [!DNL Experience Manager] | 远程部署中存在的用户由 [!DNL Experience Manager] 本地服务器(不是 [!DNL Sites] 作者角色)，以代表获取远程资产 [!DNL Sites] 作者。 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

### 连接的资产架构 {#connected-assets-architecture}

Experience Manager允许您将远程DAM部署作为源连接到多个Experience Manager [!DNL Sites] 部署。 但是，您可以 [!DNL Sites] 部署时，只能使用一个远程DAM部署。

评估要连接到远程DAM部署的最佳Sites实例数。 Adobe建议以增量方式将Sites实例连接到部署，并测试远程DAM上的性能没有影响，因为每个连接的Sites实例都会贡献到远程DAM上的数据流量。

下图说明了支持的情景：

![连接的资产架构](assets/connected-assets-architecture.png)

下图说明了不支持的方案：

![连接的资产架构](assets/connected-assets-architecture-unsupported.png)

## 在 [!DNL Sites] 和 [!DNL Assets] 部署 {#configure-a-connection-between-sites-and-assets-deployments}

安 [!DNL Experience Manager] 管理员可以创建此集成。 创建后，使用该组件所需的权限会通过用户组建立。 用户组在 [!DNL Sites] 部署和DAM部署中。

配置连接的资产和本地资产 [!DNL Sites] 连接，请执行以下步骤：

1. 访问现有 [!DNL Sites] 使用以下命令部署或创建部署：

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建每个 [!DNL Experience Manager] 服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后， [!DNL Experience Manager] 服务器成功启动。 请考虑 [!DNL Sites] 部署为用于网页创作的本地计算机，例如 `https://[local_sites]:4502`.

1. 确保上存在具有适当范围的用户和角色 [!DNL Sites] 部署和 [!DNL Assets] 在AMS上部署 在上创建技术用户 [!DNL Assets] 部署并添加到 [涉及的用户和组](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. 访问本地 [!DNL Sites] 部署 `https://[local_sites]:4502`. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. A **[!UICONTROL 标题]** 的次数。
   1. **[!UICONTROL 远程DAM URL]** 是 [!DNL Assets] 格式中的位置 `https://[assets_servername]:[port]`.
   1. DAM 分发人员（技术用户）的凭据。
   1. 在 **[!UICONTROL 山角]** 字段，输入本地 [!DNL Experience Manager] 路径位置 [!DNL Experience Manager] 会获取资产。 例如，`remoteassets` 文件夹。从DAM获取的资产会存储在 [!DNL Sites] 部署。
   1. **[!UICONTROL 本地站点URL]** 是 [!DNL Sites] 部署。 [!DNL Assets] 部署使用此值维护对此获取的数字资产的引用 [!DNL Sites] 部署。
   1. 凭据 [!DNL Sites] 技术用户。
   1. 的值 **[!UICONTROL 原始二进制传输优化阈值]** 字段会指定原始资产（包括演绎版）是否同步传输。 可以轻松获取文件大小较小的资产，而文件大小相对较大的资产最好异步同步。 此值取决于您的网络功能。
   1. 选择 **[!UICONTROL 与连接的资产共享数据存储]**，则当您使用数据存储来存储您的资产，并且数据存储在两个部署之间共享时。 在这种情况下，阈值限制无关紧要，因为数据存储上有实际的资产二进制文件，并且不会传输。

   ![连接的资产功能的典型配置](assets/connected-assets-typical-config.png)

   *图：连接的资产功能的典型配置。*

1. 上的现有数字资产 [!DNL Assets] 部署已得到处理，并且演绎版已生成。 使用此功能可获取这些演绎版，因此无需重新生成演绎版。 禁用工作流启动器，以阻止重新生成演绎版。 在[!DNL Sites])部署以排除 `connectedassets` 文件夹（将在此文件夹中获取资产）。

   1. 开 [!DNL Sites] 部署，单击 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**.

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在 [!UICONTROL 属性] 向导，请更改 **[!UICONTROL 路径]** 字段作为以下映射来更新其正则表达式以排除装入点 **[!UICONTROL connectedassets]**.

   | 之前 | 之后 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >在作者获取资产时，将会获取该资产在远程 部署中可用的所有演绎版。如果要为获取的资产创建更多演绎版，请跳过此配置步骤。的 [!UICONTROL DAM更新资产] 工作流会被触发并创建更多演绎版。 这些演绎版仅在本地 [!DNL Sites] 部署，而不是远程DAM部署中。

1. 添加 [!DNL Sites] 部署作为上CORS配置中允许的源 [!DNL Assets] 部署。 有关更多信息，请参阅 [了解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. 配置 [同一站点Cookie支持](/help/sites-administering/same-site-cookie-support.md).

您可以检查配置的 [!DNL Sites] 部署和 [!DNL Assets] 部署。

![已配置连接的资产的连接测试 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*图：已配置连接的资产的连接测试 [!DNL Sites].*

## 使用Dynamic Media资产 {#dynamic-media-assets}


通过连接的资产，您可以使用由 [!DNL Dynamic Media] 从站点页面上的远程DAM部署，并利用Dynamic Media功能，如智能裁剪和图像预设。

使用 [!DNL Dynamic Media] 与连接的资产：

1. 配置 [!DNL Dynamic Media] 在启用了同步模式的远程DAM部署中。
1. 配置 [连接的资产](#configure-a-connection-between-sites-and-assets-deployments).
1. 配置 [!DNL Dynamic Media] 在与远程DAM中配置的公司名称相同的Sites实例上。 Sites部署必须具有Dynamic Media帐户的只读访问权限才能处理连接的资产。 因此，请确保在Sites实例上的Dynamic Media配置中禁用同步模式。

>[!CAUTION]
>
>具有连接的资产和 [!DNL Dynamic Media] 配置，您不能使用 [!DNL Dynamic Media] 以处理 [!DNL Sites] 部署。

## 配置 [!DNL Dynamic Media] {#configure-dynamic-media}

配置 [!DNL Dynamic Media] on [!DNL Assets] 和 [!DNL Sites] 部署：

1. 启用和配置 [!DNL Dynamic Media] 作为远程的全局配置 [!DNL Assets] 作者部署。 要配置Dynamic Media，请参阅 [配置Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).
在远程 [!DNL Assets] 部署，在 [!UICONTROL Dynamic Media同步模式]，选择 **[!UICONTROL 默认启用]**.

1. 按照 [在站点和资产部署之间配置连接](#configure-a-connection-between-sites-and-assets-deployments). 此外，选择 **[!UICONTROL 获取Dynamic Media连接的资产的原始呈现版本]** 选项。

1. 配置 [!DNL Dynamic Media] 本地 [!DNL Sites] 远程 [!DNL Assets] 部署。 按照 [配置 [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * 在所有配置中使用相同的公司名称。
   * 在本地 [!DNL Sites]，在 [!UICONTROL Dynamic Media同步模式]，选择 **[!UICONTROL 默认情况下处于禁用状态]**. 的 [!DNL Sites] 部署必须具有对 [!DNL Dynamic Media] 帐户。
   * 在本地 [!DNL Sites]，在 **[!UICONTROL 发布资产]** 选项，选择 **[!UICONTROL 选择性发布]**. 不选择 **[!UICONTROL 同步所有内容]**.

1. 启用 [[!DNL Dynamic Media] 在图像核心组件中支持](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). 此功能会启用默认 [图像组件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) 显示 [!DNL Dynamic Media] 图像 [!DNL Dynamic Media] 作者在本地网页上使用图像 [!DNL Sites] 部署。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器连接到DAM部署。 作者可以浏览、搜索以及拖动组件中的远程资产。要对远程DAM进行身份验证，请准备好管理员提供的凭据（如果有）。

作者可以在单个网页中使用本地DAM和远程DAM部署中可用的资产。 使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

只会获取远程资产的那些标记，这些标记具有与本地分类层次结构完全对应的标记 [!DNL Sites] 部署。 任何其他标记都将被丢弃。作者可以使用远程资产上存在的所有标记来搜索远程资产 [!DNL Experience Manager] 部署，因为它提供全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 导航到 [!DNL Assets] 通过访问 **[!UICONTROL 资产]** > **[!UICONTROL 文件]** 从 [!DNL Experience Manager] 工作区。 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在 [!DNL Sites] 部署时，在右上角的配置文件激活器中，单击 **[!UICONTROL 模拟为]**. 提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开 [!UICONTROL 资产] 选项卡（远程内容查找器），然后单击 **[!UICONTROL 登录到连接的资产]**.
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户对 [!DNL Experience Manager] 部署。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   获取的资产在本地是只读的 [!DNL Sites] 部署。 您仍可以使用 [!DNL Sites] 用于编辑获取的资产的组件。 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项.*

1. 如果异步获取资产的原始资产，并且获取任务失败，则会通知网站作者。 在创作时甚至在创作后，作者可以在 [异步作业](/help/sites-administering/asynchronous-jobs.md) 用户界面。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. 发布页面时， [!DNL Experience Manager] 显示页面上使用的资产的完整列表。 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请参阅 [异步作业](/help/sites-administering/asynchronous-jobs.md) 用户界面。

   >[!NOTE]
   >
   >即使未完全获取一个或多个远程资产，页面也会发布。 的 [!DNL Experience Manager] “通知”区域显示在异步作业页面中显示错误通知。

>[!CAUTION]
>
>获取的远程资产一经在网页中使用后，有权访问本地文件夹的任何人都可以搜索和使用这些已获取的资产。 获取的资产存储在本地文件夹(`connectedassets` )。 此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

### 检查跨网页的资产使用情况 {#asset-usage-references}

[!DNL Experience Manager] 允许DAM用户检查对资产的所有引用。 它有助于了解和管理资产在远程中的使用情况 [!DNL Sites] 和复合资产。 上网页的许多作者 [!DNL Experience Manager Sites] 部署可以在远程上使用资产 [!DNL Assets] 在不同的网页中。 为了简化资产管理，并且不会导致引用损坏，DAM用户必须检查本地和远程网页中资产的使用情况。 的 [!UICONTROL 引用] 选项卡 [!UICONTROL 属性] 页面列出了资产的本地和远程引用。

查看和管理 [!DNL Assets] 部署中，请执行以下步骤：

1. 在中选择资产 [!DNL Assets] 控制台并单击 **[!UICONTROL 属性]** 中。
1. 单击 **[!UICONTROL 引用]** 选项卡。 请参阅 **[!UICONTROL 本地引用]** 资产于 [!DNL Assets] 部署。 参见**[!UICONTROL 远程引用] 用于 [!DNL Sites] 部署中使用连接的资产功能获取资产。

   ![资产属性页面中的远程引用](assets/connected-assets-remote-reference.png)

1. 的引用 [!DNL Sites] 页面显示每个本地引用的总计数 [!DNL Sites]. 查找所有引用并显示引用总数可能需要一些时间。
1. 引用列表是交互式的，DAM用户可以单击引用以打开引用页面。 如果由于某些原因无法获取远程引用，则会显示通知，告知用户失败。
1. 用户可以移动或删除资产。 移动或删除资产时，所有选定资产/文件夹的引用总数会显示在警告对话框中。 删除尚未检索引用的资产时，会显示一个警告对话框。

   ![强制删除警告](assets/delete-referenced-asset.png)

### 管理远程DAM中资产的更新 {#manage-updates-in-remote-dam}

之后 [配置连接](#configure-a-connection-between-sites-and-assets-deployments) 在远程DAM和 [!DNL Sites] 部署时，远程DAM上的资产可在 [!DNL Sites] 部署。 然后，您可以对远程DAM资产或文件夹执行更新、删除、重命名和移动操作。 更新（如果延迟）会在 [!DNL Sites] 部署。 此外，如果远程DAM上的资产在本地 [!DNL Experience Manager Sites] 页面上，远程DAM上的资产更新将显示在 [!DNL Sites] 页面。

将资产从一个位置移动到另一个位置时，请确保 [调整参照](/help/assets/manage-assets.md) 以便资产显示在 [!DNL Sites] 页面。 如果您将资产移动到无法从本地访问的位置， [!DNL Sites] 部署时，资产无法在Sites部署中显示。

您还可以更新远程DAM上资产的元数据属性，并且更改可在本地使用 [!DNL Sites] 部署。

[!DNL Sites] 作者可以在 [!DNL Sites] 部署后，再重新发布更改，以使其在 [!DNL Experience Manager] 发布实例。

[!DNL Experience Manager] 在 `Remote Assets Content Finder` 阻止网站作者在 [!DNL Sites] 页面。 如果您在 [!DNL Sites] 页面上显示的资产失败 [!DNL Experience Manager] 发布实例。

>[!NOTE]
>
>对远程DAM中资产的更新可用于 [!DNL Sites] 仅在远程DAM和 [!DNL Sites] 部署已开启 [!DNL Experience Manager].

## 常见问题解答 {#frequently-asked-questions}

+++**如果您需要使用 [!DNL Sites] 部署？**

在这种情况下，无需配置“连接的资产”。 您可以在 [!DNL Sites] 部署。

+++

+++**您何时需要配置“连接的资产”功能？**

仅当您需要使用 [!DNL Sites] 部署。

+++

+++**能否连接多个 [!DNL Sites] 部署到远程DAM部署中的任何步骤？**

是，您可以连接多个 [!DNL Sites] 部署到远程DAM部署。 有关更多信息，请参阅 [连接的资产架构](#connected-assets-architecture).

+++

+++**您可以连接多少个远程DAM部署 [!DNL Sites] 是否在配置连接的资产后进行部署？**

您可以将一个远程DAM部署连接到 [!DNL Sites] 配置连接的资产后进行部署。 有关更多信息，请参阅 [连接的资产架构](#connected-assets-architecture).

+++

+++**能否从 [!DNL Sites] 是否在配置连接的资产后进行部署？**

配置连接的资产后， [!DNL Dynamic Media] 资产可用于 [!DNL Sites] 以只读模式部署。 因此，您无法使用 [!DNL Dynamic Media] 处理 [!DNL Sites] 部署。 有关更多信息，请参阅 [在Sites与Dynamic Media部署之间配置连接](#dynamic-media-assets).

+++

+++**能否在 [!DNL Sites] 是否在配置连接的资产后进行部署？**

是，您可以在 [!DNL Sites] 配置连接的资产后进行部署。

+++

+++**能否在 [!DNL Sites] 是否在配置连接的资产后进行部署？**

不能，您不能在 [!DNL Sites] 配置连接的资产后进行部署。

+++

+++**能否在上的远程DAM部署中使用Dynamic Media资产 [!DNL Sites] 是否在配置连接的资产后进行部署？**

能，您可以在 [!DNL Sites] 配置连接的资产后进行部署。 有关更多信息，请参阅 [在Sites与Dynamic Media部署之间配置连接](#dynamic-media-assets).

+++

+++**配置连接的资产后，能否对远程DAM资产或文件夹执行更新、删除、重命名和移动操作？**

是，在配置连接的资产后，您可以对远程DAM资产或文件夹执行更新、删除、重命名和移动操作。 相关更新会在 Sites 部署中自动提供，但会有一些延迟。有关更多信息，请参阅 [管理远程DAM中资产的更新](#handling-updates-to-remote-assets).

+++

+++**配置连接的资产后，您可以在 [!DNL Sites] 部署，并在远程DAM部署中使用？**

您可以将资产添加到 [!DNL Sites] 但是，无法将这些资产用于远程DAM部署。

+++

## 限制和最佳实践 {#tip-and-limitations}

* 要深入了解资产使用情况，请配置 [资产分析](/help/assets/asset-insights.md) 功能 [!DNL Sites] 实例。

### 权限和资产管理 {#permissions-and-managing-assets}

* 本地资产是只读副本。[!DNL Experience Manager] 组件对资产进行无损编辑。不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Content Fragments] 和 [!DNL Experience Fragments] 不受支持。
* [!DNL Experience Manager] 不会获取元数据架构。 这意味着可能无法显示所有获取的元数据。 如果架构在 [!DNL Sites] 部署后，将显示所有元数据属性。
* 全部 [!DNL Sites] 即使作者无法访问远程DAM部署，作者仍对获取的副本具有读取权限。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 无法在 [!UICONTROL 页面属性] 用户界面。 您可以在 [!UICONTROL 页面属性] 用户界面 [!UICONTROL 缩略图] 单击 [!UICONTROL 选择图像].

### 设置和许可 {#setup-licensing}

* [!DNL Assets] 部署 [!DNL Adobe Managed Services] 支持。
* [!DNL Sites] 可以连接到单个 [!DNL Assets] 一次部署。
* 许可证 [!DNL Assets] 需要远程存储库。
* 一个或多个 [!DNL Sites] 需要本地创作部署。

### 用途 {#usage}

* 用户在创作时，可以搜索远程资产并将这些资产拖动到本地页面上。 不支持其他功能。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过从 [!UICONTROL 内容查找器] to [!UICONTROL 页面编辑器].
* 可以对获取的资产执行无损的简单编辑以及 `Image` 组件支持的编辑。资产是只读的。
* 重新获取资产的唯一方法是将资产拖动到页面上。 不支持API或其他方法来重新获取资产以更新资产。
* 如果资产从DAM中停用，则这些资产将继续在上使用 [!DNL Sites] 页面。
* 异步获取资产的远程引用条目。 引用和总计数不是实时的，如果站点作者在DAM用户查看引用时使用资产，则可能会有一些差异。 DAM用户可以刷新页面，然后在几分钟内重试，以获取总计数。

## 故障诊断问题 {#troubleshoot}

要对常见错误进行故障诊断，请执行以下步骤：

* 如果您无法从 [!UICONTROL 内容查找器]，然后确保拥有所需的角色和权限。

* 从远程DAM获取的资产可能由于一个或多个原因无法发布在网页上。 它不存在于远程服务器上，缺少获取它的适当权限，或者网络故障可能是原因。 确保资产未从远程DAM中删除。 确保拥有适当的权限并满足先决条件。 重试将资产添加到页面并重新发布。 检查[异步作业列表](/help/sites-administering/asynchronous-jobs.md)，查看是否发生了资产获取错误。

* 如果您无法从本地访问远程DAM部署 [!DNL Sites] 部署，确保允许跨站点Cookie，并 [同一站点Cookie支持](/help/sites-administering/same-site-cookie-support.md) 已配置。 如果阻止跨站点Cookie的部署， [!DNL Experience Manager] 可能无法验证。 例如， [!DNL Google Chrome] 隐身模式下可能会阻止第三方Cookie。 允许在 [!DNL Chrome] 浏览器，单击地址栏中的“眼睛”图标，导航到 **网站不工作** > **已阻止**，选择远程DAM URL，并允许登录令牌Cookie。 或者，请参阅 [如何启用第三方Cookie](https://support.google.com/chrome/answer/95647).

   ![Chrome浏览器中的“隐身”模式出现Cookie错误](assets/chrome-cookies-incognito-dialog.png)

* 如果您无法从Experience Manager Sitesas a Cloud ServiceSites部署访问Adobe Managed Services远程DAM部署，请更新 `aem_author.vhost` 文件，可在 `"/etc/httpd/conf.d/available_vhosts`，以便远程DAM在Dispatcher配置中包含以下标头：

   ```xml
   Header Set Access-Control-Allow-Origin <Local Sites instance host>
   Header Set Access-Control-Allow-Credentials true
   ```

* 如果未检索到远程引用并导致出现错误消息，请检查是否 [!DNL Sites] 部署可用，并检查网络连接问题。 稍后重试以检查。 [!DNL Assets] 部署尝试两次与建立连接 [!DNL Sites] 部署，然后报告失败。

   ![检索资产远程引用失败](assets/reference-report-failure.png)



