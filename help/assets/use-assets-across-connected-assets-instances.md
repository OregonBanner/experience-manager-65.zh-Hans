---
title: 使用“已连接资产”在[!DNL Adobe Experience Manager Sites]创作工作流程中共享DAM资产。
description: 在另一个Experience Manager Site部署中创建网页时，使用远程[!DNL Adobe Experience Manager Assets]部署中可用的资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 在 中，使用连接的资产共享 DAM 资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。部分原因可能是在地理上分散但需要相互协同工作的现有部署，或是因并购而导致的需要由父公司统一管理的异构基础架构。

[!DNL Adobe Experience Manager Sites] 提供了创建网页的功能， 是为网站提供所需资产的数字资产管理 (DAM) 系统。[!DNL Adobe Experience Manager Assets][!DNL Experience Manager] 现在通过集成和支持上述用 [!DNL Experience Manager Sites] 例 [!DNL Experience Manager Assets]。

## 连接的资产概述 {#overview-of-connected-assets}

When editing pages in Page Editor, the authors can seamlessly search, browse, and embed assets from a different [!DNL Experience Manager Assets] deployment. To do an [!DNL Experience Manager] administrator do a one-time integration of a local deployment of [!DNL Experience Manager Sites] with a different (remote) deployment of [!DNL Experience Manager Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. 该功能可支持一次无缝搜索和使用多个远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参 [阅Experience Manager资产迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于 Adobe Experience Manager 部署类型，需要满足如下所示的支持标准。[!DNL Experience Manager] 6.5可 [!DNL Assets] 以作为 [!DNL Experience Manager] 云服务使用。 有关详细信息，请参 [阅Experience Manager中作为云服务的“连接资产”功能](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Experience Manager Sites] 作为云服务 | AMS上的Experience Manager 6.5 [!DNL Sites] | Experience Manager 6.5内 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]作为云服务&#x200B;** | 支持 | 支持 | 支持 |
   | **AMS上的Experience Manager 6.5[!DNL Assets]** | 支持 | 支持 | 支持 |
   | **Experience Manager 6.5内[!DNL Assets]部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者可以在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索到的资产。文档可添加到 `Download` 组件中，图像可添加到 `Image` 组件中。Authors can also add the remote assets in any custom Experience Manager component that extends the default `Download` or `Image` components. 支持的格式的列表包括：

* **图像格式**:连接的资产支持图像组 [件支持的图](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html) 像格式。 [!DNL Dynamic Media] 不支持图像。
* **文档格式**：请参阅[连接的资产支持的文档格式](assets-formats.md#supported-document-formats)。

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。对于作者创建的网页的用例，使用本地范围。对于托管所需资产的 DAM 部署，使用远程范围。The [!DNL Sites] author fetches these remote assets.

| 角色 | 范围 | 用户组 | 演示中的用户名 | 要求 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | Experience Manager管理员 | `admin` | Set up Experience Manager, configure integration with the remote [!DNL Assets] deployment. |
| DAM 用户 | 本地 | 作者 | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | Author (with read access on the remote DAM and author access on local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. 作者搜索并浏览远程 DAM 中的资产有两种方式：使用内容查找器；使用本地网页中所需的图像。使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | Experience Manager管理员 | `admin` 在远程Experience Manager上 | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | 作者 | `ksaner` 在远程Experience Manager上 | 在远程Experience Manager部署上的创作角色。 使用内容查找器搜索并浏览“连接的资产”中的资产。 |
| DAM 分发人员（技术用户） | 远程 | 软件包生成器与 Sites 作者 | `ksaner` 在远程Experience Manager上 | This user present on the remote deployment is used by Experience Manager local server (not the Site author role) to fetch the remote assets, on behalf of [!DNL Sites] author. 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

Experience Manager管理员可以创建此集成。 Once created, the permissions required to use it are established via user groups that are defined on the [!DNL Sites] deployment and on the DAM deployment.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps.

1. Access an existing [!DNL Experience Manager Sites] deployment or create a deployment using the following command:

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建每个Experience Manager服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，Experience Manager服务器成功开始。 Consider this [!DNL Experience Manager Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the Experience Manager Sites deployment and on the [!DNL Experience Manager Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Experience Manager Sites] deployment at `https://[local_sites]:4502`. 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. [!DNL Experience Manager Assets] 位置 `https://[assets_servername_ams]:[port]`。
   1. DAM 分发人员（技术用户）的凭据。
   1. In **[!UICONTROL Mount Point]** field, enter the local Experience Manager path where Experience Manager fetches the assets. 例如，`remoteassets` 文件夹。
   1. 根据您的网络，调整&#x200B;**[!UICONTROL 原始二进制传输优化阈值]**&#x200B;的值。大于此阈值的资产演绎版，将异步传输。
   1. Select **[!UICONTROL Datastore Shared with Connected Assets]**, if you use a datastore to store your assets and the Datastore is the common storage between both Experience Manager deployments. 在这种情况下，阈值限制并不重要，因为实际的资产二进制文件驻留在数据存储上并且不会传输。
      ![连接的资产的典型配置](assets/connected-assets-typical-config.png)
   *图：连接的资产的典型配置.*

1. 由于已经处理资产且已获取资产演绎版，因此请禁用工作流程启动器。Adjust the launcher configurations on the local ([!DNL Experience Manager Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Experience Manager Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在“属性”向导中，将&#x200B;**[!UICONTROL 路径]**&#x200B;字段更改为以下映射来更新其正则表达式，以便排除 **[!UICONTROL connectedassets]** 装入点。
   | 之前 | 之后 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >当作者提取资产时，将获取远程Experience Manager部署中可用的所有再现。 如果要为获取的资产创建更多演绎版，请跳过此配置步骤。The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Experience Manager Sites] instance as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Experience Manager Assets] CORS configuration.

   1. 使用管理员凭据登录。搜索 `Cross-Origin`. 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 运营]** > **[!UICONTROL Web 控制台]**。

   1. To create a CORS configuration for [!DNL Experience Manager Sites] instance, click ![aem_assets_add_icon](assets/aem_assets_add_icon.png) icon next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. 保存配置。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器来连接到 DAM 实例。作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程 DAM，请准备好管理员提供的 DAM 用户凭据。

在一个网页中，作者既可以使用本地 DAM 上可用的资产，也可以使用远程 DAM 实例上可用的资产。使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

Only those tags of remote assets are fetched that have an exact corresponding tag along with the same taxonomy hierarchy, available on the local [!DNL Sites] instance. 任何其他标记都将被丢弃。作者可以使用远程Experience Manager部署中显示的所有标记搜索远程资产，因为Experience Manager会优惠全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. Navigate to the [!DNL Assets] user interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. On the [!DNL Sites] instance, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. 提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   The fetched assets are read-only on the local [!DNL Experience Manager Sites] deployment. You can still use the options provided by your [!DNL Experience Manager Sites] components to edit the fetched asset. 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项.*

1. 如果异步获取资产且获取任务失败，会通知站点作者。在创作过程中甚至是创作后，作者可以在[异步作业](/help/assets/asynchronous-jobs.md)用户界面中，查看关于获取任务和错误的详细信息。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used in the page. 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请查看[异步作业](/help/assets/asynchronous-jobs.md)用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，页面也会发布。使用该远程资产的组件发布为空。The [!DNL Experience Manager] notification area displays notification for errors that show in async jobs page.

>[!CAUTION]
>
>获取的远程资产一经在网页中使用后，有权访问存储所获取资产的本地文件夹的任何人都可以搜索和使用这些已获取的资产（上述演示中的 `connectedassets`）。此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

## 限制 {#limitations}

**权限与资产管理**

* 本地资产与远程部署中的原始资产不同步。在 DAM 部署上所具有的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。Experience Manager组件可对资产进行无损编辑。 不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Dynamic Media]不支持 资产、内容片段和体验片段。
* 不获取元数据架构。
* All [!DNL Sites] authors have read permissions on the fetched copies, even if they do not have access to the remote DAM deployment.
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 无法在页面属性用户界面上将远程资产用作页 [!UICONTROL 面缩略图] 。 可以通过单击选择图像，在缩略图的“页 [!UICONTROL 面属性] ”用户界面中设 [!UICONTROL 置网页] 的缩略图 。

**设置和许可**

* [!DNL Experience Manager Assets] 支持在AMS上部署。
* [!DNL Experience Manager Sites] 一次可以连接到 [!DNL Experience Manager Assets] 单个存储库。
* A license of [!DNL Experience Manager Assets] working as remote repository.
* One or more licenses of [!DNL Experience Manager Sites] working as local authoring deployment.

**使用**

* 唯一支持的功能是：在本地页面上搜索并拖动远程资产，来创作内容。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过将远程资产从[!UICONTROL 内容查找器]拖到[!UICONTROL 页面编辑器]来重新尝试获取资产。
* 可以对获取的资产执行无损的简单编辑以及 [!DNL Experience Manager] 组件支持的编辑。`Image`资产是只读的。

## 故障诊断问题 {#troubleshoot}

对于常见错误情景，请按照以下步骤进行故障诊断：

* 如果无法从内容查找器中搜索远程资产，请重新检查并确保拥有所需的角色和权限。
* 从远程 DAM 获取的资产，可能会因为以下原因无法发布到网页上：该资产不存在于远程 DAM 上；缺乏相应的获取该资产的权限；网络故障。确保资产没有从远程 DAM 中删除，或者权限没有发生变化；确保满足适当的先决条件；重新尝试将资产添加到页面并重新发布。检查[异步作业列表](/help/assets/asynchronous-jobs.md)，查看是否发生了资产获取错误。
