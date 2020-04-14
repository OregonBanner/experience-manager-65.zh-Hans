---
title: 在 Adobe Experience Manager Sites 创作工作流程中，使用连接的资产共享 DAM 资产
description: 在另一个 Experience Manager Site 部署中创建网页时，使用远程 Adobe Experience Manager Assets 部署中的可用资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 04fef21d6027dcfcb6a67a1121e0d1570926db41

---


# 在 AEM Sites 中，使用连接的资产共享 DAM 资产 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。部分原因可能是在地理上分散但需要相互协同工作的现有部署，或是因并购而导致的需要由父公司统一管理的异构基础架构。

AEM Sites 提供了创建网页的功能，AEM Assets 是为网站提供所需资产的数字资产管理 (DAM) 系统。AEM 现在可通过集成 AEM Sites 和 AEM Assets 来支持上述用例。

## 连接的资产概述 {#overview-of-connected-assets}

在“页面编辑器”中编辑页面时，作者可以从其他 AEM Assets 部署中无缝搜索、浏览和嵌入资产。为此，AEM 管理员需要将 AEM Sites 的本地部署与 AEM Assets 的其他（远程）部署进行一次性集成。

对于 Sites 作者，远程资产将以只读本地资产方式提供。该功能可支持一次无缝搜索和使用多个远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于 Adobe Experience Manager 部署类型，需要满足如下所示的支持标准。AEM 6.5资产可作为云服务与AEM一起使用。 有关详细信息，请参 [阅AEM中作为云服务的“已连接资产”功能](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | AEM Sites 云服务 | AMS 上的 AEM 6.5 Sites | 内部部署的 AEM 6.5 Sites |
   |---|---|---|---|
   | **AEM Assets 云服务** | 支持 | 支持 | 支持 |
   | **AMS 上的 AEM 6.5 Assets** | 支持 | 支持 | 支持 |
   | **内部部署的 AEM 6.5 Assets** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者可以在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索到的资产。文档可添加到 `Download` 组件中，图像可添加到 `Image` 组件中。此外，作者还可以在任何自定义 AEM 组件（对默认 `Download` 或 `Image` 组件的扩展）中添加远程资产。支持的格式的列表包括：

* **图像格式**:连接的资产支持图像组 [件支持的图](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html) 像格式。 不支持 Dynamic Media 图像。
* **文档格式**：请参阅[连接的资产支持的文档格式](assets-formats.md#supported-document-formats)。

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。对于作者创建的网页的用例，使用本地范围。对于托管所需资产的 DAM 部署，使用远程范围。Sites 作者会获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 要求 |
|---|---|---|---|---|
| AEM Sites 管理员 | 本地 | AEM 管理员 | `admin` | 设置 AEM，配置与远程 Assets 部署的集成。 |
| DAM 用户 | 本地 | 作者 | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| AEM Sites 作者 | 本地 | 作者（拥有对远程 DAM 的读取访问权限，以及对本地 Sites 的创作访问权限） | `ksaner` | 最终用户是使用此集成提高内容速度的 Sites 作者。作者搜索并浏览远程 DAM 中的资产有两种方式：使用内容查找器；使用本地网页中所需的图像。使用的 DAM 用户的 `ksaner` 凭据。 |
| AEM Assets 管理员 | 远程 | AEM 管理员 | 远程 AEM 上的 `admin` | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | 作者 | 远程 AEM 上的 `ksaner` | 远程 AEM 部署上的作者角色。使用内容查找器搜索并浏览“连接的资产”中的资产。 |
| DAM 分发人员（技术用户） | 远程 | 软件包生成器与 Sites 作者 | 远程 AEM 上的 `ksaner` | AEM 本地服务器（而非 Sites 作者角色）代表 Sites 作者，使用远程部署上存在的用户来获取远程资产。此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

## 在 Sites 与 Assets 部署之间配置连接 {#configure-a-connection-between-sites-and-assets-deployments}

AEM 管理员可以创建此集成。创建后，使用该集成所需的权限是通过在 Sites 部署和 DAM 部署中定义的用户组来建立。

要配置连接的资产与本地 Sites 连接，请执行以下步骤。

1. 访问现有 AEM Sites 部署，或使用以下命令创建一个部署：

   1. 在 JAR 文件的文件夹中，在终端上执行以下命令以创建 AEM 服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，AEM 服务器成功启动。将此 AEM Sites 部署视为用于网页创作的本地计算机，例如 `https://[local_sites]:4502`。

1. 确保 AEM Sites 部署和 AMS 上的 AEM Assets 部署中，存在具有本地范围的用户和角色。在 Assets 部署上创建技术用户，并将其添加到[涉及的用户和组](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)中所述的用户组。

1. 访问本地 AEM Sites 部署：`https://[local_sites]:4502`。单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. AEM Assets 位置为 `https://[assets_servername_ams]:[port]`。
   1. DAM 分发人员（技术用户）的凭据。
   1. 在&#x200B;**[!UICONTROL 装入点]**&#x200B;字段中，输入 AEM 获取资产的本地 AEM 路径。例如，`remoteassets` 文件夹。
   1. 根据您的网络，调整&#x200B;**[!UICONTROL 原始二进制传输优化阈值]**&#x200B;的值。大于此阈值的资产演绎版，将异步传输。
   1. 如果您使用数据存储来存储您的资产，且数据存储是两个 AEM 部署之间的公用存储，请选择&#x200B;**[!UICONTROL 与连接的资产共享数据存储]**。在这种情况下，阈值限制并不重要，因为实际的资产二进制文件驻留在数据存储上并且不会传输。
      ![连接的资产的典型配置](assets/connected-assets-typical-config.png)
   *图：连接的资产的典型配置*

1. 由于已经处理资产且已获取资产演绎版，因此请禁用工作流程启动器。在本地 (AEM Sites) 部署中调整启动器配置，以排除从其中获取远程资产的 `connectedassets` 文件夹。

   1. 在 AEM Sites 部署中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**。

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在“属性”向导中，将&#x200B;**[!UICONTROL 路径]**&#x200B;字段更改为以下映射来更新其正则表达式，以便排除 **[!UICONTROL connectedassets]** 装入点。
   | 之前 | 之后 |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >在作者获取资产时，将会获取该资产在远程 AEM 部署中可用的所有演绎版。如果要为获取的资产创建更多演绎版，请跳过此配置步骤。The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. 在远程 AEM Assets 的 CORS 配置上，将 AEM Sites 实例添加为&#x200B;**[!UICONTROL 允许的源]**&#x200B;之一。

   1. 使用管理员凭据登录。搜索“跨源”。访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 运营]** > **[!UICONTROL Web 控制台]**。

   1. 要为 AEM Sites 实例创建 CORS 配置，请单击 **[!UICONTROL Adobe Granite 跨源资源共享策略]**&#x200B;旁边的 ![aem_assets_add_icon](assets/aem_assets_add_icon.png) 图标。

   1. 在&#x200B;**[!UICONTROL 允许的源]**&#x200B;字段中，输入本地 Sites 的 URL，即 `https://[local_sites]:[port]`。保存配置。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器来连接到 DAM 实例。作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程 DAM，请准备好管理员提供的 DAM 用户凭据。

在一个网页中，作者既可以使用本地 DAM 上可用的资产，也可以使用远程 DAM 实例上可用的资产。使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

只会获取远程资产的那些标记，这些标记具有与同一分类层次结构完全相同的对应标记，该分类层次结构在本地Sites实例中可用。 任何其他标记都将被丢弃。因为 AEM 提供全文搜索功能，因此作者可以使用远程 AEM 部署中存在的所有标记来搜索远程资产。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 通过从 AEM 工作区访问 **[!UICONTROL Assets]** > **[!UICONTROL 文件]**，导航到远程部署中的 Assets UI。或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在 Sites 实例上，在右上角的配置文件激活器中单击&#x200B;**[!UICONTROL 模拟为]**。提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开“资产”选项卡，然后单击&#x200B;**[!UICONTROL 登录到连接的资产]**。
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户拥有这两个 AEM 部署的创作权限。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   获取的资产在本地 AEM Sites 部署上是只读的。您仍可以使用 AEM Sites 组件提供的选项来编辑获取的资产。通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项*

1. 如果异步获取资产且获取任务失败，会通知站点作者。在创作过程中甚至是创作后，作者可以在[异步作业](/help/assets/asynchronous-jobs.md)用户界面中，查看关于获取任务和错误的详细信息。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的资产异步获取的通知*

1. 发布页面时，AEM 会显示页面中使用的资产的完整列表。请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请查看[异步作业](/help/assets/asynchronous-jobs.md)用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，页面也会发布。使用该远程资产的组件发布为空。AEM 通知区域会显示在异步作业页面中出现错误的通知。

>[!CAUTION]
>
>获取的远程资产一经在网页中使用后，有权访问存储所获取资产的本地文件夹的任何人都可以搜索和使用这些已获取的资产（上述演示中的 `connectedassets`）。此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

## 限制 {#limitations}

**权限与资产管理**

* 本地资产与远程部署中的原始资产不同步。在 DAM 部署上所具有的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。AEM 组件对资产进行无损编辑。不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。不支持 Dynamic Media 资产、内容片段和体验片段。
* 不获取元数据架构。
* 所有 Sites 作者都拥有对获取的副本的读取权限，即便他们无权访问远程 DAM 部署。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 无法在页面属性用户界面上将远程资产用作页 [!UICONTROL 面缩略图] 。 可以通过单击选择图像，在缩略图的“页 [!UICONTROL 面属性] ”用户界面中设 [!UICONTROL 置网页的缩] 略图 。

**设置和许可**

* 支持 AMS 上的 AEM Assets 部署。
* AEM Sites 一次可以连接到一个 AEM Assets 存储库。
* AEM Assets 的许可证用作远程存储库。
* AEM Sites 的一个或多个许可证用作本地创作部署。

**使用**

* 唯一支持的功能是：在本地页面上搜索并拖动远程资产，来创作内容。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过将远程资产从[!UICONTROL 内容查找器]拖到[!UICONTROL 页面编辑器]来重新尝试获取资产。
* 可以对获取的资产执行无损的简单编辑以及 AEM `Image` 组件支持的编辑。资产是只读的。

## 故障诊断问题 {#troubleshoot}

对于常见错误情景，请按照以下步骤进行故障诊断：

* 如果无法从内容查找器中搜索远程资产，请重新检查并确保拥有所需的角色和权限。
* 从远程 DAM 获取的资产，可能会因为以下原因无法发布到网页上：该资产不存在于远程 DAM 上；缺乏相应的获取该资产的权限；网络故障。确保资产没有从远程 DAM 中删除，或者权限没有发生变化；确保满足适当的先决条件；重新尝试将资产添加到页面并重新发布。检查[异步作业列表](/help/assets/asynchronous-jobs.md)，查看是否发生了资产获取错误。
