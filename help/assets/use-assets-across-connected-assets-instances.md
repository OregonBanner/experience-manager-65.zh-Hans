---
title: 在Adobe Experience Manager Sites创作工作流程中使用连接的资产共享DAM资产
description: 在另一个Experience Manager Site部署中创建网页时，使用远程Adobe Experience Manager Assets部署中可用的资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 04789dc662bc935277f392aefde4146f1a79f747

---


# 使用连接的资产在AEM Sites中共享DAM资产 {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，创建网站所需的基础结构可以分发。 有时，用于创建这些网站的网站创建功能和数字资产可能驻留在不同部署中。 一些原因可能是地理上分散的部署，需要协同工作；并购导致母公司希望整合的异质基础设施；增长导致资产管理需要专门的实例。

AEM Sites 提供了创建网页的功能，AEM Assets 是为网站提供所需资产的数字资产管理 (DAM) 系统。AEM 现在可通过集成 AEM Sites 和 AEM Assets 来支持上述用例。

## 已连接资产概述 {#overview-of-connected-assets}

在页面编辑器中编辑页面时，作者可以从其他AEM资产部署中无缝搜索、浏览和嵌入资产。 要执行AEM管理员操作，请将AEM Sites的本地部署与AEM Assets的其他（远程）部署进行一次性集成。

对于站点作者，远程资源可以作为只读本地资源。 该功能支持一次无缝搜索和使用几个远程资产。 要使许多远程资产可以一次性用于本地部署，请考虑批量迁移这些资产。 请参阅 [资产迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件和支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于Adobe Experience Manager的部署类型，符合支持的标准之一。 AEM 6.5资产可作为云服务与AEM一起使用。 有关详细信息，请参 [阅AEM中作为云服务的“已连接资产”功能](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | AEM Sites 云服务 | AMS上的AEM 6.5站点 | AEM 6.5站点内部部署 |
   |---|---|---|---|
   | **AEM Assets 云服务** | 受支持 | 受支持 | 受支持 |
   | **AMS上的AEM 6.5资产** | 受支持 | 受支持 | 受支持 |
   | **AEM 6.5资产内部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者可以在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索到的资产。 文档可以添加到组件 `Download` 中，图像可以添加到组件 `Image` 中。 作者还可以在扩展默认或组件的任何自定义AEM组件中添加远 `Download` 程资 `Image` 产。 支持的格式列表包括：

* **图像格式**:连接的资产支持图像组 [件支持的图](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/image.html) 像格式。 不支持Dynamic Media图像。
* **文档格式**:请参阅 [连接的资产支持的文档格式](assets-formats.md#supported-document-formats)。

### Users and groups involved {#users-and-groups-involved}

配置和使用该功能所涉及的各种角色及其相应的用户组如下所述。 本地范围用于作者创建网页的用例。 远程范围用于托管所需资产的DAM部署。 站点作者会获取这些远程资产。

| 角色 | 范围 | 用户组 | 遍历中的用户名 | 要求 |
|----------------------------------|--------|------------------------------------------------------------------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM Sites Administrator | 本地 | AEM管理员 | `admin` | 设置AEM，配置与远程资产部署的集成。 |
| DAM用户 | 本地 | 创作 | `ksaner` | 用于查看和复制在上获取的资产 `/content/DAM/connectedassets/`。 |
| AEM Sites作者 | 本地 | 创作（在远程DAM上具有读访问权限，在本地站点上具有创作访问权限） | `ksaner` | 最终用户是使用此集成提高内容速度的站点作者。 作者使用内容查找器在远程DAM中搜索和浏览资产，并在本地网页中使用所需的图像。 使用 `ksaner` DAM用户的凭据。 |
| AEM Assets管理员 | 远程 | AEM Administrator | `admin` 在远程AEM上 | 配置跨源资源共享(CORS)。 |
| DAM用户 | 远程 | 创作 | `ksaner` 在远程AEM上 | 远程AEM部署上的创作角色。 使用内容查找器在已连接资产中搜索和浏览资产。 |
| DAM分销商（技术用户） | 远程 | 包构建器和站点作者 | `ksaner` 在远程AEM上 | AEM本地服务器（而非站点作者角色）会代表站点作者使用此远程部署用户获取远程资产。 此角色与上述两个角色不同， `ksaner` 它属于其他用户组。 |

## 在站点和资产部署之间配置连接 {#configure-a-connection-between-sites-and-assets-deployments}

AEM管理员可以创建此集成。 创建后，使用它所需的权限会通过在站点部署和DAM部署中定义的用户组来建立。

要配置已连接的资产和本地站点连接，请执行以下步骤。

1. 访问现有AEM Sites部署或使用以下命令创建部署：

   1. 在JAR文件的文件夹中，对终端执行以下命令以创建每个AEM服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，AEM服务器成功启动。 将此AEM Sites部署视为用于网页创作的本地计算机，例如 `https://[local_sites]:4502`。

1. 确保在AEM Sites部署和AMS上的AEM Assets部署中存在具有本地范围的用户和角色。 创建有关资产部署的技术用户，并将其添加到相关用户和用户 [组中提到的用户组](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)。

1. 访问本地AEM Sites部署，网址为 `https://[local_sites]:4502`。 单击 **[!UICONTROL 工具]** >资 **[!UICONTROL 产]** > **[!UICONTROL 连接的资产配置]** ，并提供以下值：

   1. AEM Assets位置为 `https://[assets_servername_ams]:[port]`。
   1. DAM分销商（技术用户）的凭据。
   1. 在装 **[!UICONTROL 载点字段]** ，输入AEM获取资产的本地AEM路径。 例如， `remoteassets` folder。

   1. 根据您的网络调 **[!UICONTROL 整原始二进制传输优化阈值]** 。 大小大于此阈值的资产演绎版将异步传输。
   1. 如果 ****&#x200B;您使用数据存储来存储您的资产，而数据存储是两个AEM部署之间的公用存储，请选择与已连接资产共享的数据存储。 在这种情况下，阈值限制并不重要，因为实际的资产二进制文件驻留在数据存储上并且不会传输。
   ![已连接资产的典型配置](assets/connected-assets-typical-config.png)

   *图：已连接资产的典型配置*

1. 由于资产已经处理且已获取演绎版，请禁用工作流启动器。 在本地(AEM Sites)部署中调整启动器配置，以排除 `connectedassets` 从中获取远程资产的文件夹。

   1. 在AEM Sites部署中，单击工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流]** >启 **[!UICONTROL 动器]**。

   1. 使用工作流作为 **[!UICONTROL DAM更新资产和]** DAM元数 **[!UICONTROL 据写回搜索启动程序]**。

   1. 选择工作流启动器，然后单 **[!UICONTROL 击操作栏]** 上的“属性”。

   1. 在“属性”向导中，将“路 **[!UICONTROL 径]** ”字段更改为以下映射，以更新其正则表达式以排除已连接的挂 **[!UICONTROL 载点资产]**。
   | 显示之前状态 | 发生 |
   |---|---|
   | /content/dam(/(?!/subassets)。)*/)再现／原始 | /content/dam(/(?!/subassets)(?!connectedassets)。)*/)再现／原始 |
   | /content/dam(/.*/)再现／原始 | /content/dam(/((?!connectedassets)。)*/)再现／原始 |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets)。)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >在作者提取资产时，将获取远程AEM部署中可用的所有演绎版。 如果要为获取的资产创建更多演绎版，请跳过此配置步骤。 DAM更新资产工作流会被触发并创建更多演绎版。 这些演绎版仅在本地站点部署中可用，而在远程DAM部署中则不可用。

1. 将AEM Sites实例添加为远程AEM资 **[!UICONTROL 产的]** CORS配置上允许的源实例之一。

   1. 使用管理员凭据登录。 搜索跨源。 访问 **[!UICONTROL 工具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]**。

   1. 要为AEM Sites实例创建CORS配置，请单击 ![Adobe Granite跨源资源共享策略旁边的](assets/aem_assets_add_icon.png) aem_assets_add_icon **[!UICONTROL 图标]**。

   1. 在“允 **[!UICONTROL 许的来源]**”字段中，输入本地站点的URL，即 `https://[local_sites]:[port]`。 保存配置。

## 使用远程资源 {#use-remote-assets}

网站作者使用内容查找器连接到DAM实例。 作者可以浏览、搜索和拖动组件中的远程资产。 要验证到远程DAM，请准备好管理员提供的DAM用户凭据。

作者可以在单个网页中使用本地DAM和远程DAM实例上的可用资源。 使用内容查找器可在搜索本地DAM或搜索远程DAM之间切换。

只会获取远程资产的那些标记，这些标记具有与本地站点实例相同的分类层次结构，并且具有相同的对应标记。 任何其他标记将被丢弃。 作者可以使用远程AEM部署中提供的所有标记搜索远程资产，因为AEM提供了全文搜索。

### 使用说明 {#walk-through-of-usage}

使用上述设置尝试创作体验以了解功能的工作方式。 在远程DAM部署中使用您选择的文档或图像。

1. 通过从AEM工作区访问“资产” **[!UICONTROL >“文件”，导航到远程部]** 署中的“资 **[!UICONTROL 产]** ”UI。 或者，也可以在 `https://[assets_servername_ams]:[port]/assets.html/content/dam` 浏览器中访问。 上传您选择的资产。
1. 在“站点”实例的右上角的配置文件激活程序中，单击“模拟 **[!UICONTROL 为”]**。 提供 `ksaner` 为用户名，选择提供的选项，然后单击“确 **[!UICONTROL 定”]**。
1. 打开We.Retail网站页面，网址为 **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **** en.Retail。 编辑页面。 或者，也可 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以在浏览器中访问以编辑页面。

   单击 **[!UICONTROL 页面左上角的]** “切换侧面板”。

1. 打开“资产”选项卡，然后单 **[!UICONTROL 击“登录到已连接的资产”]**。
1. 提供凭据- `ksaner` 作为用户名和 `password` 口令。 此用户对两个AEM部署都具有创作权限。
1. 搜索您添加到DAM的资产。 远程资源显示在左侧面板中。 对图像或文档进行过滤，并进一步对支持的文档类型进行过滤。 拖动组件上的图 `Image` 像和组件上的文档 `Download` 。

   获取的资产在本地AEM Sites部署上是只读的。 您仍可以使用AEM站点组件提供的选项来编辑获取的资产。 按组件进行编辑是无损的。

   ![在远程DAM上搜索资产时筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程DAM上搜索资产时筛选文档类型和图像的选项*

1. 如果异步获取资产并且任何获取任务失败，则会通知站点作者。 在创作时，甚至在创作之后，作者可以在异步作业用户界面中查看有关提取任务和错误 [的详细信](/help/assets/asynchronous-jobs.md) 息。

   ![关于在后台进行的资产异步获取的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的资产异步获取的通知。*

1. 发布页面时，AEM会显示页面中使用的资产的完整列表。 确保在发布时成功获取远程资产。 要检查每个获取的资产的状态，请参阅异 [步作业](/help/assets/asynchronous-jobs.md) 用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，也会发布页面。 使用远程资产的组件已发布为空。 AEM通知区域显示有关在异步作业页面中显示的错误的通知。

>[!CAUTION]
>
>在网页中使用获取的远程资源后，任何有权访问存储获取的资源的本地文件夹的人（在上面的浏览中）都可以搜索和使用获取的`connectedassets` 远程资源。 资产也可通过内容查找器搜索并在本地存储库中 [!UICONTROL 显示]。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑除外。

## 限制 {#limitations}

**权限和管理资产**

* 本地资产与远程部署中的原始资产不同步。 对DAM部署的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。 AEM组件对资产进行无损编辑。 不允许进行其他编辑。
* 本地获取的资源仅可用于创作目的。 无法应用资产更新工作流，也无法编辑元数据。
* 仅支持图像和列出的文档格式。 不支持Dynamic Media资产、内容片段和体验片段。
* 未获取元数据架构。
* 所有站点作者都对获取的副本具有读取权限，即使他们无权访问远程DAM部署。
* 无API支持自定义集成。
* 该功能支持无缝搜索和使用远程资源。 要一次性在本地部署中提供许多远程资产，请考虑迁移这些资产。 请参阅 [资产迁移指南](assets-migration-guide.md)。
* 无法在页面属性用户界面上将远程资产用作页 [!UICONTROL 面缩略图] 。 可以通过单击选择图像，在缩略图的“页 [!UICONTROL 面属性] ”用户界面中设 [!UICONTROL 置网页] 的缩略图 。

**设置和许可**

* 支持在AMS上部署AEM资产。
* AEM Sites可以一次连接到单个AEM资产存储库。
* AEM Assets作为远程存储库使用的许可证。
* 作为本地创作部署的AEM Sites的一个或多个许可证。

**使用情况**

* 只支持搜索远程资产并将远程资产拖动到本地页面上以创作内容的功能。
* 5秒后提取操作超时。 作者在获取资产时可能遇到问题，如是否存在网络问题。 作者可以通过将远程资产从内容查找器拖到页 [!UICONTROL 面编辑器] ，重 [!UICONTROL 新尝试]。
* 可以对获取的资产执行无损的简单编辑以及AEM `Image` 组件支持的编辑。 资产为只读。

## 问题疑难解答 {#troubleshoot}

请按照以下步骤对常见错误情景进行疑难解答：

* 如果无法从内容查找器中搜索远程资产，请重新检查并确保所需的角色和权限到位。
* 由于以下原因，从远程dam获取的资产可能无法发布到网页上：它不存在于远程设备上；缺乏相应的权限来获取它；网络故障。 确保资产不会从远程DAM中删除，或者权限不会更改；确保满足适当的先决条件；重试将资产添加到页面并重新发布。 检查异 [步作业列表](/help/assets/asynchronous-jobs.md) ，以查找资产获取错误。
