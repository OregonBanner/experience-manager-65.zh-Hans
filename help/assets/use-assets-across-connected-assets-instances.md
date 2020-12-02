---
title: 在 中，使用连接的资产共享 DAM 资产 [!DNL Sites]
description: 使用远程 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 部署中可用的资源。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f0d91a32caa4d3b862d852028e3bc5547aeb8015
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 41%

---


# 在 中，使用连接的资产共享 DAM 资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。一个原因可以是地理上分散的现有部署，这些部署需要协同工作。 另一个原因可能是收购导致了父公司希望共同使用的异质基础结构。

用户可以在[!DNL Experience Manager Sites]中创建网页。 [!DNL Experience Manager Assets] 是数字资产管理(DAM)系统，它为网站提供所需的资产。[!DNL Experience Manager] 现在通过集成和支持上述用 [!DNL Sites] 例 [!DNL Assets]。

## 连接的资产概述 {#overview-of-connected-assets}

在[!UICONTROL 页面编辑器]中编辑页面作为目标目标时，作者可以从充当资产源的不同[!DNL Assets]部署中无缝搜索、浏览和嵌入资产。 管理员创建具有[!DNL Sites]功能的[!DNL Experience Manager]部署与具有[!DNL Assets]功能的[!DNL Experience Manager]的另一个部署的一次性集成。

对于[!DNL Sites]作者，远程资产可以作为只读本地资产。 该功能可支持一次无缝搜索和使用多个远程资产。要在一次性的[!DNL Sites]部署中提供许多远程资产，请考虑批量迁移这些资产。 请参阅[Experience Manager资产迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 用户是每个部署中相应用户组的一部分。
* 对于[!DNL Adobe Experience Manager]部署类型，符合支持的标准之一。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 以 [!DNL Experience Manager] 作为Cloud Service。有关此功能在[!DNL Experience Manager as a Cloud Service]中的工作方式的详细信息，请参阅[以Experience Manager形式作为Cloud Service的连接资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)。

   |  | [!DNL Sites] 作为Cloud Service | [!DNL Experience Manager] 6.5  [!DNL Sites] on AMS. | [!DNL Experience Manager] 6.5内 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]作为Cloud Service** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] on AMS.** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5内 [!DNL Assets] 部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索的资产。 文档添加到`Download`组件，图像添加到`Image`组件。 作者还可以在扩展默认`Download`或`Image`组件的任何自定义[!DNL Experience Manager]组件中添加远程资源。 支持的格式有：

* **图像格式**:图像组件支 [持](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 的格式。[!DNL Dynamic Media] 不支持图像。
* **文档格式**:查看支 [持的文档格式](assets-formats.md#supported-document-formats)。

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。本地范围用于作者创建网页的用例。 对于托管所需资产的 DAM 部署，使用远程范围。[!DNL Sites]作者获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 要求 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | [!DNL Experience Manager] `administrators` | `admin` | 设置[!DNL Experience Manager]并配置与远程[!DNL Assets]部署的集成。 |
| DAM 用户 | 本地 | `Authors` | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | `Authors` (在远程DAM上具有读访问权，在本地具有作者访问权 [!DNL Sites]) | `ksaner` | 最终用户是[!DNL Sites]作者，他们使用此集成来提高其内容速度。 作者使用[!UICONTROL 内容查找器]在远程DAM中搜索和浏览资产，并在本地网页中使用所需的图像。 使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | [!DNL Experience Manager] `administrators` | `admin` 在远程  [!DNL Experience Manager] | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | `Authors` | `ksaner` 在远程  [!DNL Experience Manager] | 远程[!DNL Experience Manager]部署上的作者角色。 使用[!UICONTROL 内容查找器]在已连接资产中搜索和浏览资产。 |
| DAM 分发人员（技术用户） | 远程 | [!DNL Sites] `Authors` | `ksaner` 在远程  [!DNL Experience Manager] | [!DNL Experience Manager]本地服务器（不是[!DNL Sites]作者角色）使用此远程部署用户代表[!DNL Sites]作者获取远程资产。 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

## 配置[!DNL Sites]和[!DNL Assets]部署{#configure-a-connection-between-sites-and-assets-deployments}之间的连接

[!DNL Experience Manager]管理员可以创建此集成。 创建后，用户组将建立使用该应用程序所需的权限。 用户组在[!DNL Sites]部署和DAM部署中定义。

要配置已连接资产和本地[!DNL Sites]连接，请执行以下步骤：

1. 访问现有[!DNL Sites]部署或使用以下命令创建部署：

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建每个[!DNL Experience Manager]服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，[!DNL Experience Manager]服务器开始成功。 将此[!DNL Sites]部署视为用于网页创作的本地计算机，例如`https://[local_sites]:4502`。

1. 确保在[!DNL Sites]部署和AMS的[!DNL Assets]部署中存在具有本地范围的用户和角色。 在[!DNL Assets]部署中创建一个技术用户，并将其添加到[用户和涉及的组](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)中提到的用户组。

1. 访问`https://[local_sites]:4502`的本地[!DNL Sites]部署。 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. [!DNL Assets] 位置为 `https://[assets_servername_ams]:[port]`。
   1. DAM 分发人员（技术用户）的凭据。
   1. 在&#x200B;**[!UICONTROL 装载点]**&#x200B;字段中，输入[!DNL Experience Manager]获取资产的本地[!DNL Experience Manager]路径。 例如，`remoteassets` 文件夹。
   1. 根据您的网络，调整&#x200B;**[!UICONTROL 原始二进制传输优化阈值]**&#x200B;的值。大于此阈值的资产演绎版，将异步传输。
   1. 如果您使用数据存储来存储您的资产，且数据存储是两个 部署之间的公用存储，请选择&#x200B;**[!UICONTROL 与连接的资产共享数据存储]**。在这种情况下，阈值限制并不重要，因为实际的资产二进制文件驻留在数据存储上并且不会传输。

   ![连接的资产的典型配置](assets/connected-assets-typical-config.png)

   *图：连接的资产的典型配置.*

1. 由于已经处理资产且已获取资产演绎版，因此请禁用工作流程启动器。调整本地([!DNL Sites])部署上的启动器配置，以排除从中获取远程资源的`connectedassets`文件夹。

   1. 在[!DNL Sites]部署中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 启动器]**。

   1. 搜索工作流为 **[!UICONTROL DAM 更新资产]**&#x200B;和 **[!UICONTROL DAM 元数据写回]**&#x200B;的启动器。

   1. 选择工作流启动器，然后单击操作栏上的&#x200B;**[!UICONTROL 属性]**。

   1. 在[!UICONTROL 属性]向导中，将&#x200B;**[!UICONTROL 路径]**&#x200B;字段更改为以下映射，以更新其常规表达式以排除挂载点&#x200B;**[!UICONTROL 已连接资产]**。

   | 之前 | 之后 |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >在作者获取资产时，将会获取该资产在远程 部署中可用的所有演绎版。如果要为获取的资产创建更多演绎版，请跳过此配置步骤。将触发[!UICONTROL  DAM更新资产]工作流并创建更多演绎版。 这些演绎版仅在本地[!DNL Sites]部署中可用，在远程DAM部署中则不可用。

1. 将[!DNL Sites]部署添加为远程[!DNL Assets'] CORS配置上的&#x200B;**[!UICONTROL 允许的来源]**&#x200B;之一。

   1. 使用管理员凭据登录。 搜索 `Cross-Origin`. 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 运营]** > **[!UICONTROL Web 控制台]**。

   1. 要为[!DNL Sites]部署创建CORS配置，请单击&#x200B;**[!UICONTROL AdobeGranite跨来源资源共享策略]**&#x200B;旁边的“资产添加”选项![“添加”图标](assets/do-not-localize/assets_add_icon.png)。

   1. 在字段&#x200B;**[!UICONTROL 允许的来源]**&#x200B;中，输入本地[!DNL Sites]的URL，即`https://[local_sites]:[port]`。 保存配置。

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器连接到DAM部署。 作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程 DAM，请准备好管理员提供的 DAM 用户凭据。

作者可以在单个网页中使用本地DAM和远程DAM部署上的可用资产。 使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

只会获取远程资产的那些标记，这些标记具有与同一分类层次结构完全相同的对应标记，该分类层次结构在本地[!DNL Sites]部署中可用。 任何其他标记都将被丢弃。作者可以使用远程[!DNL Experience Manager]部署中显示的所有标记搜索远程资产，因为它会优惠全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 通过从[!DNL Experience Manager]工作区访问&#x200B;**[!UICONTROL 资产]** > **[!UICONTROL 文件]**，导航到远程部署上的[!DNL Assets]接口。 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在[!DNL Sites]部署中，在右上角的用户档案激活器中，单击“模拟为&#x200B;]**”。**[!UICONTROL &#x200B;提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开[!UICONTROL 资产]选项卡，然后单击&#x200B;**[!UICONTROL 登录到已连接的资产]**。
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户对[!DNL Experience Manager]部署具有创作权限。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   在本地[!DNL Sites]部署中，获取的资源是只读的。 您仍可以使用[!DNL Sites]组件提供的选项来编辑获取的资产。 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项.*

1. 如果异步获取资产且获取任务失败，会通知站点作者。在创作过程中甚至是创作后，作者可以在[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面中，查看关于获取任务和错误的详细信息。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. 发布页面时，[!DNL Experience Manager]将显示页面上使用的资产的完整列表。 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请查看[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，页面也会发布。使用该远程资产的组件发布为空。[!DNL Experience Manager]通知区域显示异步作业页中显示的错误通知。

>[!CAUTION]
>
>在网页中使用后，获取的远程资源便可以被具有访问本地文件夹权限的用户搜索和使用。 获取的资源存储在本地文件夹中（上面的遍历中的`connectedassets`）。 此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

## 限制和最佳实践{#tips-and-limitations}

* 要了解资产使用情况，请对[!DNL Sites]实例配置[资产分析](/help/assets/asset-insights.md)功能。

### 权限和资产管理{#permissions-and-managing-assets}

* 本地资产与远程部署中的原始资产不同步。在 DAM 部署上所具有的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。[!DNL Experience Manager] 组件对资产进行无损编辑。不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Dynamic Media]不支持 资产、内容片段和体验片段。
* [!DNL Experience Manager] 不提取元数据模式。这意味着可能无法显示所有获取的元数据。 如果模式单独更新，则显示所有属性。
* 所有[!DNL Sites]作者都对获取的副本具有读取权限，即使作者无法访问远程DAM部署。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 无法在[!UICONTROL 页面属性]用户界面上将远程资产用作页面缩略图。 可以通过单击[!UICONTROL 选择图像]，在[!UICONTROL 缩略图]的[!UICONTROL 用户界面中设置网页的缩略图。]

### 设置和许可 {#setup-licensing}

* [!DNL Assets] 支持在 [!DNL Adobe Managed Services] 上部署。
* [!DNL Sites] 一次可以连接到 [!DNL Assets] 单个存储库。
* [!DNL Assets]的许可证用作远程存储库。
* [!DNL Sites]的一个或多个许可证用作本地创作部署。

### 使用 {#usage}

* 创作时，用户可以搜索远程资产并在本地页面上拖动这些资产。 不支持任何其他功能。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过将远程资产从[!UICONTROL 内容查找器]拖动到[!UICONTROL 页面编辑器]来重新尝试。
* 可以对获取的资产执行无损的简单编辑以及 `Image` 组件支持的编辑。资产是只读的。
* 重新提取资产的唯一方法是将其拖动到页面上。 没有API支持或其他方法可重新获取资产以进行更新。
* 如果资产从DAM中停止使用，则这些资产将继续在[!DNL Sites]页面上使用。

## 故障诊断问题 {#troubleshoot}

要排除常见错误方案的故障，请执行以下步骤：

* 如果无法从[!UICONTROL 内容查找器]搜索远程资产，请确保所需的角色和权限已到位。
* 由于一个或多个原因，从远程dam获取的资产可能无法发布到网页上。 它在远程服务器上不存在，缺少相应的权限来获取它，或者网络故障可能是原因。 确保资产未从远程DAM中删除。 确保拥有适当的权限，并满足先决条件。 重试将资产添加到页面并重新发布。 检查[异步作业列表](/help/sites-administering/asynchronous-jobs.md)，查看是否发生了资产获取错误。
* 如果无法从本地[!DNL Sites]部署访问远程DAM部署，请确保允许跨站点Cookie。 如果跨站点Cookie被阻止，则[!DNL Experience Manager]的两个部署可能无法进行身份验证。 例如，在Incognito模式下，[!DNL Google Chrome]可能会阻止第三方cookie。 要允许[!DNL Chrome]浏览器中的cookie，请单击地址栏中的“眼睛”图标，导航到“站点不工作”>“阻止”，选择“远程DAM URL”，并允许登录令牌cookie。 或者，请参阅有关如何启用第三方cookies](https://support.google.com/chrome/answer/95647)的帮助。[

   ![Chrome中的Incognito模式下的Cookie错误](assets/chrome-cookies-incognito-dialog.png)
