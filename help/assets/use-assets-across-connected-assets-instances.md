---
title: 使用“连接的资产”在中共享DAM资产 [!DNL Sites]
description: 使用远程上可用的资源 [!DNL Adobe Experience Manager Assets] 在另一个网站上创建网页时的部署 [!DNL Adobe Experience Manager Sites] 部署。
contentOwner: AK
mini-toc-levels: 2
role: User, Admin, Leader
feature: Connected Assets,User and Groups
exl-id: 4ceb49d8-b619-42b1-81e7-c3e83d4e6e62
hide: true
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '3908'
ht-degree: 15%

---

# 使用“连接的资产”在中共享DAM资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html?lang=en) |
| AEM 6.5 | 本文 |


在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。一个原因可能是地理上分散但需要协同工作的现有部署。 另一个原因可能是收购导致基础架构的异构性，包括不同的 [!DNL Experience Manager] 版本，即母公司希望一起使用的版本。

“连接的资产”功能通过集成支持上述用例 [!DNL Experience Manager Sites] 和 [!DNL Experience Manager Assets]. 用户可以在以下位置创建网页： [!DNL Sites] 使用来自单独设备的数字资产 [!DNL Assets] 部署。

>[!NOTE]
>
>只有在您需要使用远程DAM部署中的可用资产（位于单独的Sites部署中）来创作网页时，才能配置“连接的资产” 。

## 连接的资产概述 {#overview-of-connected-assets}

在中编辑页面时 [!UICONTROL 页面编辑器] 作为目标位置，作者可以无缝地搜索、浏览和嵌入其他位置的资产 [!DNL Assets] 充当资源源的部署。 管理员创建部署的一次性集成 [!DNL Experience Manager] 替换为 [!DNL Sites] 功能的另一个部署 [!DNL Experience Manager] 替换为 [!DNL Assets] 功能。 站点作者还可以通过Connected Assets在其站点的网页中使用Dynamic Media图像，并使用Dynamic Media功能，如智能裁切和图像预设。

对于 [!DNL Sites] 此外，远程资产将以只读本地资产形式提供。 该功能支持在站点编辑器中无缝搜索和访问远程资产。 对于可能要求在站点上提供完整资产语料的任何其他用例，请考虑批量迁移资产，而不是使用“连接的资产”。 请参阅 [Experience Manager Assets迁移指南](/help/assets/assets-migration-guide.md).

### 先决条件和支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对象 [!DNL Adobe Experience Manager] 部署类型时，将满足一个受支持的标准。 [!DNL Experience Manager] 6.5 [!DNL Assets] 适用于 [!DNL Experience Manager] as a Cloud Service。 有关此功能在中如何工作的更多信息 [!DNL Experience Manager] as a [!DNL Cloud Service]，请参见 [Experience Manageras a Cloud Service中的“连接的资源”](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] 在AMS上 | [!DNL Experience Manager] 6.5 [!DNL Sites] 内部部署 |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | 支持 | 支持 | 支持 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 在AMS上** | 支持 | 支持 | 支持 |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] 内部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中拖动搜索到的资产。 文档将添加到 `Download` 组件和图像到 `Image` 组件。 作者还可以在任何自定义中添加远程资产 [!DNL Experience Manager] 扩展缺省值的组件 `Download` 或 `Image` 组件。 支持的格式包括：

* **图像格式**：使用的格式 [图像组件](assets-formats.md#supported-raster-image-formats) 支持。
* **文档格式**：请参阅 [支持的文档格式](assets-formats.md#supported-document-formats).

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。对于作者创建网页的用例，使用本地范围。 对于托管所需资产的 DAM 部署，使用远程范围。此 [!DNL Sites] 作者获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 描述 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | [!DNL Experience Manager] `administrators` | `admin` | 设置 [!DNL Experience Manager] 并配置与远程设备的集成 [!DNL Assets] 部署。 |
| DAM 用户 | 本地 | `Authors` | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | <ul><li>`Authors` （对远程DAM具有读取访问权限，对本地具有创作访问权限） [!DNL Sites]) </li> <li>`dam-users` 本地 [!DNL Sites]</li></ul> | `ksaner` | 最终用户是 [!DNL Sites] 使用此集成提高内容速度的作者。 作者使用在远程DAM中搜索和浏览资产 [!UICONTROL 内容查找器] 并在本地网页中使用所需的图像。 使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | [!DNL Experience Manager] `administrators` | `admin` 远程 [!DNL Experience Manager] | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | `Authors` | `ksaner` 远程 [!DNL Experience Manager] | 远程设备上的作者角色 [!DNL Experience Manager] 部署。 在“连接的资产”中，使用搜索并浏览资产 [!UICONTROL 内容查找器]. |
| DAM 分发人员（技术用户） | 远程 | [!DNL Sites] `Authors` | `ksaner` 远程 [!DNL Experience Manager] | 远程部署上存在的此用户由使用 [!DNL Experience Manager] 本地服务器(不是 [!DNL Sites] 创作角色)以代表获取远程资产 [!DNL Sites] 作者。 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

### 连接的资产体系结构 {#connected-assets-architecture}

通过Experience Manager，您可以将远程DAM部署作为源连接到多个Experience Manager [!DNL Sites] 部署。 但是，您可以连接 [!DNL Sites] 只有一个远程DAM部署的部署。

评估连接到远程DAM部署的最佳站点实例数量。 Adobe建议将Sites实例增量连接到部署，并测试远程DAM上的性能不会受到影响，因为每个连接的Sites实例都会贡献远程DAM上的数据流量。

下图说明了支持的场景：

![连接的资产体系结构](assets/connected-assets-architecture.png)

下图说明了不支持的方案：

![连接的资产体系结构](assets/connected-assets-architecture-unsupported.png)

## 配置之间的连接 [!DNL Sites] 和 [!DNL Assets] 部署 {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] 管理员可以创建此集成。 创建后，使用该集成所需的权限是通过用户组建立的。 用户组定义在 [!DNL Sites] 部署和DAM部署。

配置“连接的资产”和本地 [!DNL Sites] 连接，请按照以下步骤操作：

1. 访问现有 [!DNL Sites] 部署或使用以下命令创建部署：

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建 [!DNL Experience Manager] 服务器。
      `java -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后， [!DNL Experience Manager] 服务器启动成功。 考虑一下 [!DNL Sites] 将部署为用于网页创作的本地计算机，例如 `https://[local_sites]:4502`.

1. 确保上存在具有适当范围的用户和角色 [!DNL Sites] 部署和 [!DNL Assets] 在AMS上部署。 创建技术用户 [!DNL Assets] 部署和添加到中所述的用户组 [涉及的用户和组](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. 访问本地 [!DNL Sites] 部署位置 `https://[local_sites]:4502`. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. A **[!UICONTROL 标题]** 配置中。
   1. **[!UICONTROL 远程DAM URL]** 是的URL [!DNL Assets] 格式中的位置 `https://[assets_servername]:[port]`.
   1. DAM 分发人员（技术用户）的凭据。
   1. 在 **[!UICONTROL 装入点]** 字段，输入本地 [!DNL Experience Manager] 路径： [!DNL Experience Manager] 获取资源。 例如， `remoteassets` 文件夹。 从DAM获取的资产存储在 [!DNL Sites] 部署。
   1. **[!UICONTROL 本地站点URL]** 是的位置 [!DNL Sites] 部署。 [!DNL Assets] 部署使用此值维护对此获取的数字资产的引用 [!DNL Sites] 部署。
   1. 凭据 [!DNL Sites] 技术用户。
   1. 的值 **[!UICONTROL 原始二进制传输优化阈值]** 字段指定是否同步传输原始资源（包括演绎版）。 文件大小较小的资产可以轻松获取，而文件大小相对较大的资产最好进行异步同步。 该值取决于您的网络功能。
   1. 选择 **[!UICONTROL 与“连接的资产”共享数据存储]**，如果您使用数据存储来存储资产，并且数据存储在这两个部署之间共享。 在这种情况下，阈值限制并不重要，因为实际的资产二进制文件在数据存储上可用并且不会传输。

   ![“连接的资产”功能的典型配置](assets/connected-assets-typical-config.png)

   *图：连接的资产功能的典型配置。*

1. 上的现有数字资产 [!DNL Assets] 已处理部署并生成演绎版。 使用此功能获取这些演绎版，因此无需重新生成演绎版。 禁用工作流启动器以防止重新生成节目。 调整上的启动器配置([!DNL Sites])部署，以排除 `connectedassets` 文件夹（在此文件夹中获取资产）。

   1. 开启 [!DNL Sites] 部署，单击 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**.

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在 [!UICONTROL 属性] 向导，更改 **[!UICONTROL 路径]** 字段作为以下映射来更新其正则表达式以排除装入点 **[!UICONTROL connectedassets]**.

   | 之前 | 之后 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >在作者获取资产时，将会获取远程部署中可用的所有演绎版。 如果要为获取的资产创建更多演绎版，请跳过此配置步骤。此 [!UICONTROL DAM更新资产] 触发工作流并创建更多演绎版。 这些演绎版仅在本地可用 [!DNL Sites] 而不是在远程DAM部署中。

1. 添加 [!DNL Sites] 在上的CORS配置中作为允许的源部署 [!DNL Assets] 部署。 有关更多信息，请参阅 [了解CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. 配置 [相同网站Cookie支持](/help/sites-administering/same-site-cookie-support.md).

您可以检查已配置服务器之间的连接， [!DNL Sites] 部署和 [!DNL Assets] 部署。

![已配置“连接的资产”的连接测试 [!DNL Sites]](assets/connected-assets-multiple-config.png)
*图：已配置的连接的资产的连接测试 [!DNL Sites].*

## 使用Dynamic Media资源 {#dynamic-media-assets}


通过“连接的资产”，您可以使用由以下对象处理的图像资产： [!DNL Dynamic Media] 从Sites页面上的远程DAM部署，并使用Dynamic Media功能，如智能裁切和图像预设。

使用 [!DNL Dynamic Media] 连接的资产：

1. 配置 [!DNL Dynamic Media] 在启用了同步模式的远程DAM部署上。
1. 配置 [连接的资产](#configure-a-connection-between-sites-and-assets-deployments).
1. 配置 [!DNL Dynamic Media] 与在远程DAM上配置的公司名称相同的Sites实例上。 Sites部署必须对Dynamic Media帐户具有只读访问权限，才能使用连接的资源。 因此，请确保在站点实例的Dynamic Media配置中禁用同步模式。

>[!CAUTION]
>
>与Connected Assets [!DNL Dynamic Media] 配置，无法使用 [!DNL Dynamic Media] ，以处理本地资产在 [!DNL Sites] 部署。

## 配置 [!DNL Dynamic Media] {#configure-dynamic-media}

配置 [!DNL Dynamic Media] 日期 [!DNL Assets] 和 [!DNL Sites] 部署：

1. 启用和配置 [!DNL Dynamic Media] 作为远程服务器上的全局配置 [!DNL Assets] 作者部署。 要配置Dynamic Media，请参阅 [配置Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).
远程 [!DNL Assets] 部署，位于 [!UICONTROL Dynamic Media同步模式]，选择 **[!UICONTROL 默认启用]**.

1. 按照中的说明创建“连接的资产”配置 [配置站点和资源部署之间的连接](#configure-a-connection-between-sites-and-assets-deployments). 此外，选择 **[!UICONTROL 获取Dynamic Media连接的资源的原始演绎版]** 选项。

1. 配置 [!DNL Dynamic Media] 本地 [!DNL Sites] 和远程 [!DNL Assets] 部署。 按照说明进行操作，以 [配置 [!DNL Dynamic Media]](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services).

   * 在所有配置中使用相同的公司名称。
   * 在本地 [!DNL Sites]，在 [!UICONTROL Dynamic Media同步模式]，选择 **[!UICONTROL 默认禁用]**. 此 [!DNL Sites] 部署必须具有对的只读访问权限 [!DNL Dynamic Media] 帐户。
   * 在本地 [!DNL Sites]，在 **[!UICONTROL 发布资产]** 选项，选择 **[!UICONTROL 选择性发布]**. 不选择 **[!UICONTROL 同步所有内容]**.

1. 启用 [[!DNL Dynamic Media] 图像核心组件中的支持](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). 此功能启用默认值 [图像组件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) 显示 [!DNL Dynamic Media] 图像时间 [!DNL Dynamic Media] 图像由作者在本地的网页中使用 [!DNL Sites] 部署。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器连接到DAM部署。 作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程DAM，请准备好管理员提供的凭据（如果有）。

作者可以在单个网页中使用本地DAM和远程DAM部署上可用的资产。 使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

仅获取那些具有完全对应的标记以及本地可用的相同分类层次结构的远程资产标记 [!DNL Sites] 部署。 任何其他标记都将被丢弃。作者可以使用远程位置上的所有标记来搜索远程资产 [!DNL Experience Manager] 部署，因为它提供全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 导航至 [!DNL Assets] 通过访问远程部署上的接口 **[!UICONTROL 资产]** > **[!UICONTROL 文件]** 从 [!DNL Experience Manager] 工作区。 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在 [!DNL Sites] 部署，在右上角的配置文件激活器中，单击 **[!UICONTROL 模拟为]**. 提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开 [!UICONTROL 资产] 选项卡（远程内容查找器）并单击 **[!UICONTROL 登录到“连接的资产”]**.
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户具有对两者的创作权限 [!DNL Experience Manager] 部署。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   获取的资产在本地是只读的 [!DNL Sites] 部署。 您仍然可以使用由贵机构提供的选项， [!DNL Sites] 组件以编辑获取的资产。 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程DAM上搜索资产时，筛选文档类型和图像的选项。*

1. 如果异步获取资产的原始资产且获取任务失败，会通知站点作者。 在创作过程中甚至创作后，作者都可以在中查看有关获取任务和错误的详细信息 [异步作业](/help/sites-administering/asynchronous-jobs.md) 用户界面。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. 发布页面时， [!DNL Experience Manager] 显示页面上使用的资源的完整列表。 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请参阅 [异步作业](/help/sites-administering/asynchronous-jobs.md) 用户界面。

   >[!NOTE]
   >
   >即使未完全获取一个或多个远程资产，页面也会发布。 此 [!DNL Experience Manager] 通知区域显示通知，指出异步作业页面中显示的错误。

>[!CAUTION]
>
>获取的远程资产一经在网页中使用后，有权访问本地文件夹的任何人都可以搜索和使用这些资产。 获取的资产存储在本地文件夹中(`connectedassets` 上述演示中)。 此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

### 检查跨网页的资源使用 {#asset-usage-references}

[!DNL Experience Manager] 允许DAM用户检查对资产的所有引用。 它有助于了解和管理远程资产的使用情况 [!DNL Sites] 在复合资产中。 上的许多网页作者 [!DNL Experience Manager Sites] 部署可以使用远程设备上的资产 [!DNL Assets] 在不同的网页中。 要简化资产管理且不会导致引用损坏，DAM用户务必要检查本地和远程网页上资源的使用情况。 此 [!UICONTROL 引用] 选项卡中的资产 [!UICONTROL 属性] 页面列出了资产的本地和远程引用。

要查看和管理 [!DNL Assets] 部署，请按照以下步骤操作：

1. 在中选择资源 [!DNL Assets] 控制台并单击 **[!UICONTROL 属性]** 工具栏中。
1. 单击 **[!UICONTROL 引用]** 选项卡。 请参阅 **[!UICONTROL 本地引用]** 以在上使用资产 [!DNL Assets] 部署。 参见**[!UICONTROL 远程引用] 于以下位置使用资产： [!DNL Sites] 部署：使用“连接的资产”功能获取资产。

   ![资产“属性”页面中的远程引用](assets/connected-assets-remote-reference.png)

1. 的引用 [!DNL Sites] 页面显示每个本地的引用总数 [!DNL Sites]. 查找所有引用并显示引用总数可能需要一些时间。
1. 引用列表是交互式的，DAM用户可以单击引用以打开引用页面。 如果由于某个原因无法获取远程引用，则会显示通知以告知用户该故障。
1. 用户可以移动或删除资源。 移动或删除资源时，所有选定资源/文件夹的引用总数都会显示在警告对话框中。 删除尚未检索其引用的资产时，会显示警告对话框。

   ![强制删除警告](assets/delete-referenced-asset.png)

### 管理远程DAM中资产的更新 {#manage-updates-in-remote-dam}

之后 [配置连接](#configure-a-connection-between-sites-and-assets-deployments) 远程DAM与之间 [!DNL Sites] 在部署中，远程DAM上的资产在以下位置提供： [!DNL Sites] 部署。 然后，您可以对远程DAM资源或文件夹执行更新、删除、重命名和移动操作。 更新会在()上自动提供，但会有一些延迟。 [!DNL Sites] 部署。 此外，如果在本地使用远程DAM上的资产， [!DNL Experience Manager Sites] 页面上，对远程DAM上资产的更新将显示在 [!DNL Sites] 页面。

在将资产从一个位置移动到另一个位置时，请确保 [调整引用](/help/assets/manage-assets.md) 以便该资产显示在 [!DNL Sites] 页面。 如果将资产移动到无法从本地访问的位置 [!DNL Sites] 部署，则资产无法在Sites部署中显示。

您还可以更新远程DAM上资产的元数据属性，所做的更改可在本地使用 [!DNL Sites] 部署。

[!DNL Sites] 作者可以在以下位置预览可用更新： [!DNL Sites] 部署，然后重新发布更改以使其在 [!DNL Experience Manager] 发布实例。

[!DNL Experience Manager] 在中显示资源的过期状态可视指示器 `Remote Assets Content Finder` 阻止网站作者在网站上使用资产 [!DNL Sites] 页面。 如果您对使用状态为已到期的资产 [!DNL Sites] 页面上，该资产无法显示在 [!DNL Experience Manager] 发布实例。

## 常见问题解答 {#frequently-asked-questions}

+++**如果您需要使用上可用的资源，您应配置“连接的资源”？ [!DNL Sites] 部署？**

在这种情况下，无需配置“连接的资产”。 您可以使用上的可用资产 [!DNL Sites] 部署。

+++

+++**何时需要配置“连接的资产”功能？**

只有在您需要使用上的远程DAM部署中可用的资产时，才需配置“连接的资产”功能 [!DNL Sites] 部署。

+++

+++**您是否可以连接多个 [!DNL Sites] 在配置“连接的资产”之后部署到远程DAM部署？**

是，您可以连接多个 [!DNL Sites] 在配置“连接的资产”之后部署到远程DAM部署。 有关更多信息，请参阅 [连接的资产体系结构](#connected-assets-architecture).

+++

+++**您可以连接到多少远程DAM部署 [!DNL Sites] 配置“连接的资产”后的部署？**

您可以将一个远程DAM部署连接到 [!DNL Sites] 配置“连接的资产”后的部署。 有关更多信息，请参阅 [连接的资产体系结构](#connected-assets-architecture).

+++

+++**能否使用来自您的Dynamic Media资源？ [!DNL Sites] 配置“连接的资产”后的部署？**

配置“连接的资产”后， [!DNL Dynamic Media] 资源位于 [!DNL Sites] 以只读模式部署。 因此，您无法使用 [!DNL Dynamic Media] 在中处理资产 [!DNL Sites] 部署。 有关更多信息，请参阅 [在Sites和Dynamic Media部署之间配置连接](#dynamic-media-assets).

+++

+++**您是否可以在上的远程DAM部署中使用图像和文档格式类型的资产 [!DNL Sites] 配置“连接的资产”后的部署？**

是，您可以从上的远程DAM部署中使用图像和文档格式类型的资产 [!DNL Sites] 配置“连接的资产”后的部署。

+++

+++**您能否在上使用来自远程DAM部署的内容片段和视频资产？ [!DNL Sites] 配置“连接的资产”后的部署？**

不能，您无法在上使用来自远程DAM部署的内容片段和视频资产。 [!DNL Sites] 配置“连接的资产”后的部署。

+++

+++**您能否在上使用来自远程DAM部署的Dynamic Media资源？ [!DNL Sites] 配置“连接的资产”后的部署？**

是，您可以从上的远程DAM部署配置并使用Dynamic Media图像资产 [!DNL Sites] 配置“连接的资产”后的部署。 有关更多信息，请参阅 [在Sites和Dynamic Media部署之间配置连接](#dynamic-media-assets).

+++

+++**配置“连接的资产”后，能否对远程DAM资产或文件夹执行更新、删除、重命名和移动操作？**

是，在配置“连接的资产”后，您可以对远程DAM资产或文件夹执行更新、删除、重命名和移动操作。 更新会在Sites部署中自动提供，但会有一些延迟。 有关更多信息，请参阅 [管理远程DAM中资产的更新](#handling-updates-to-remote-assets).

+++

+++**配置“连接的资产”后，您能否在 [!DNL Sites] 部署并在远程DAM部署中可用？**

您可以将资源添加到 [!DNL Sites] 但是，部署这些资产无法用于远程DAM部署。

+++

## 限制和最佳实践 {#tip-and-limitations}

* 要获取有关资产使用情况的见解，请配置 [资产分析](/help/assets/asset-insights.md) 上的功能 [!DNL Sites] 实例。

* 您不能将远程资产拖动到 [图像组件“配置”对话框](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=en#configure-dialog). 但是，您可以直接将远程资产拖到Sites页面上的图像组件，而无需单击 **[!UICONTROL 配置]**.

### 权限和资产管理 {#permissions-and-managing-assets}

* 本地资产是只读副本。[!DNL Experience Manager] 组件对资产进行无损编辑。 不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Content Fragments] 和 [!DNL Experience Fragments] 不受支持。
* [!DNL Experience Manager] 不获取元数据架构。 这意味着可能无法显示所有获取的元数据。 如果架构单独更新，在 [!DNL Sites] 部署，则会显示所有元数据属性。
* 全部 [!DNL Sites] 作者对获取的副本具有读取权限，即使作者无法访问远程DAM部署也是如此。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 不能将远程资产用作上的页面缩略图 [!UICONTROL 页面属性] 用户界面。 您可以在中设置网页的缩略图 [!UICONTROL 页面属性] 的用户界面 [!UICONTROL 缩略图] 通过单击 [!UICONTROL 选择图像].

### 设置和许可 {#setup-licensing}

* [!DNL Assets] 部署于 [!DNL Adobe Managed Services] 受支持。
* [!DNL Sites] 可以连接到单个 [!DNL Assets] 一次部署。
* 的许可证 [!DNL Assets] 必须使用远程存储库。
* 的一个或多个许可证 [!DNL Sites] 需要使用本地创作部署。

### 用途 {#usage}

* 用户可以在创作时搜索远程资产并将这些资产拖动到本地页面上。 不支持其他功能。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过从拖动远程资产来重新尝试 [!UICONTROL 内容查找器] 到 [!UICONTROL 页面编辑器].
* 无损的简单编辑以及通过支持的编辑 `Image` 组件，可以对获取的资产执行。 资产是只读的。
* 重新获取资产的唯一方法是将其拖动到页面上。 没有API支持或其他方法可重新获取资产以对其进行更新。
* 如果从DAM中停用资产，则在上继续使用这些资产 [!DNL Sites] 页数。
* 资产的远程引用条目是异步获取的。 引用和总计数不是实时的，并且如果Sites作者在DAM用户查看引用时使用资产，则可能会有一些差异。 DAM用户可以刷新页面，并在几分钟后重试以获取总计数。

## 问题疑难解答 {#troubleshoot}

要排除常见错误，请执行以下步骤：

* 如果您无法从以下位置搜索远程资产： [!UICONTROL 内容查找器]，然后确保具备所需的角色和权限。

* 出于一个或多个原因，从远程DAM获取的资产可能不会发布到网页上。 它不存在于远程服务器上，缺少获取它的相应权限，或者可能是网络故障所致。 确保资产没有从远程DAM中删除。 确保具有适当的权限并且满足先决条件。 重试将资产添加到页面并重新发布。 检查[异步作业列表](/help/sites-administering/asynchronous-jobs.md)，查看是否发生了资产获取错误。

* 如果您无法从本地访问远程DAM部署 [!DNL Sites] 部署，确保允许跨站点Cookie，并且 [相同网站Cookie支持](/help/sites-administering/same-site-cookie-support.md) 已配置。 如果跨站点Cookie被阻止，则部署 [!DNL Experience Manager] 不能进行身份验证。 例如， [!DNL Google Chrome] 可能会阻止第三方Cookie。 允许Cookie [!DNL Chrome] 浏览器，单击地址栏中的“眼睛”图标，导航至 **站点无法正常工作** > **已阻止**，选择远程DAM URL，并允许使用登录令牌Cookie。 或者，请参阅 [如何启用第三方Cookie](https://support.google.com/chrome/answer/95647).

  ![无痕模式下Chrome浏览器中的Cookie错误](assets/chrome-cookies-incognito-dialog.png)

* 如果您无法从Managed Servicesas a Cloud Service站点部署访问AdobeExperience Manager Sites远程DAM部署，请更新 `aem_author.vhost` 文件，位于 `"/etc/httpd/conf.d/available_vhosts`，以便远程DAM在Dispatcher配置中包含以下标头：

  ```xml
  Header Set Access-Control-Allow-Origin <Local Sites instance host>
  Header Set Access-Control-Allow-Credentials true
  ```

* 如果未检索远程引用并导致错误消息，请检查 [!DNL Sites] 部署可用，并检查网络连接问题。 请稍后重试以检查。 [!DNL Assets] 部署尝试两次与建立连接 [!DNL Sites] 部署，然后报告故障。

  ![无法检索资产远程引用](assets/reference-report-failure.png)

* 如果未将Cookie从Sites服务器发送到Google Chrome中的Assets服务器，则这是因为Assets连接不是通过HTTPS进行的。 如果您没有在Assets实例上使用HTTPS，则 `SameSite=None` 在使用资产服务器进行身份验证后，无法将标头添加到响应中。

