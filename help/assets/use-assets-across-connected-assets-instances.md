---
title: 在 中，使用连接的资产共享 DAM 资产 [!DNL Sites]
description: 使用远程 [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] 部署上的可用资源。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d17749cb8e923848f8f81360c03b9afba7989ae2
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 29%

---


# 在 中，使用连接的资产共享 DAM 资产 [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和用于创建这些网站的数字资产可能驻留在不同的部署中。一个原因可以是在地理上分散了需要协同工作的现有部署。 另一个原因可能是收购导致了父公司希望共同使用的异质基础结构。

用户可以在[!DNL Experience Manager Sites]中创建网页。 [!DNL Experience Manager Assets] 是数字资产管理(DAM)系统，可为网站提供所需的资产。[!DNL Experience Manager] 现在，通过集成和支持上述用 [!DNL Sites] 例 [!DNL Assets]。

## 连接的资产概述 {#overview-of-connected-assets}

当在[!UICONTROL 页面编辑器]中编辑页面作为目标目标时，作者可以无缝地搜索、浏览和嵌入作为资源源的不同[!DNL Assets]部署中的资产。 管理员创建具有[!DNL Sites]功能的[!DNL Experience Manager]部署与具有[!DNL Assets]功能的[!DNL Experience Manager]的另一个部署的一次性集成。

对于[!DNL Sites]作者，远程资源可用作只读本地资源。 该功能可支持一次无缝搜索和使用多个远程资产。要在一次部署[!DNL Sites]中提供许多远程资源，请考虑批量迁移这些资源。 请参阅[Experience Manager资产迁移指南](/help/assets/assets-migration-guide.md)。

### 先决条件与支持的部署 {#prerequisites}

在使用或配置此功能之前，请确保：

* 这些用户是每个部署中相应用户组的一部分。
* 对于[!DNL Adobe Experience Manager]部署类型，符合支持的标准之一。 [!DNL Experience Manager] 6.5可 [!DNL Assets] 作 [!DNL Experience Manager] 为Cloud Service。有关此功能在[!DNL Experience Manager]中作为[!DNL Cloud Service]的工作方式的详细信息，请参阅 [!DNL Experience Manager] 中的[作为 [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)的“已连接资产”。

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5  [!DNL Sites] on AMS | [!DNL Experience Manager] 6.5内 [!DNL Sites] 部部署 |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]a[!DNL Cloud Service]** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5  [!DNL Assets] on AMS** | 支持 | 支持 | 支持 |
   | **[!DNL Experience Manager]6.5内 [!DNL Assets] 部部署** | 不支持 | 不支持 | 不支持 |

### 支持的文件格式 {#mimetypes}

作者在内容查找器中搜索图像和以下类型的文档，并在页面编辑器中使用搜索的资产。 文档会添加到`Download`组件，图像会添加到`Image`组件。 作者还可以在扩展默认`Download`或`Image`组件的任何自定义[!DNL Experience Manager]组件中添加远程资源。 支持的格式有：

* **图像格式**:图像组件支 [持](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 的格式。[!DNL Dynamic Media] 不支持图像。
* **文档格式**:请参阅支 [持的文档格式](assets-formats.md#supported-document-formats)。

### 涉及的用户和组 {#users-and-groups-involved}

下面介绍了配置和使用该功能所涉及的各种角色，及其相应的用户组。本地范围用于作者创建网页的用例。 对于托管所需资产的 DAM 部署，使用远程范围。[!DNL Sites]作者会获取这些远程资产。

| 角色 | 范围 | 用户组 | 演示中的用户名 | 要求 |
|---|---|---|---|---|
| [!DNL Sites] 管理员 | 本地 | [!DNL Experience Manager] `administrators` | `admin` | 设置[!DNL Experience Manager]并配置与远程[!DNL Assets]部署的集成。 |
| DAM 用户 | 本地 | `Authors` | `ksaner` | 用于查看和复制在 `/content/DAM/connectedassets/` 上获取的资产。 |
| [!DNL Sites] 作者 | 本地 | <ul><li>`Authors` (在远程DAM上具有读访问权，在本地具有作者访问 [!DNL Sites]权) </li> <li>`dam-users` 在本地  [!DNL Sites]</li></ul> | `ksaner` | 最终用户是[!DNL Sites]作者，他们使用此集成来提高其内容速度。 作者使用[!UICONTROL 内容查找器]并在本地网页中使用所需的图像在远程DAM中搜索和浏览资产。 使用的 DAM 用户的 `ksaner` 凭据。 |
| [!DNL Assets] 管理员 | 远程 | [!DNL Experience Manager] `administrators` | `admin` 远程  [!DNL Experience Manager] | 配置跨源资源共享 (CORS)。 |
| DAM 用户 | 远程 | `Authors` | `ksaner` 远程  [!DNL Experience Manager] | 远程[!DNL Experience Manager]部署上的作者角色。 使用[!UICONTROL 内容查找器]在已连接资产中搜索和浏览资产。 |
| DAM 分发人员（技术用户） | 远程 | [!DNL Sites] `Authors` | `ksaner` 远程  [!DNL Experience Manager] | [!DNL Experience Manager]本地服务器（而非[!DNL Sites]作者角色）会代表[!DNL Sites]作者使用此远程部署用户获取远程资源。 此角色与上述两个 `ksaner` 角色不同，它属于另一个不同的用户组。 |

## 配置[!DNL Sites]和[!DNL Assets]部署{#configure-a-connection-between-sites-and-assets-deployments}之间的连接

[!DNL Experience Manager]管理员可以创建此集成。 创建后，用户组将建立使用该应用程序所需的权限。 用户组在[!DNL Sites]部署和DAM部署中定义。

要配置已连接资产和本地[!DNL Sites]连接，请执行以下步骤：

1. 访问现有的[!DNL Sites]部署或使用以下命令创建部署：

   1. 在JAR文件的文件夹中，在终端上执行以下命令以创建每个[!DNL Experience Manager]服务器。
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. 几分钟后，[!DNL Experience Manager]服务器开始成功。 将此[!DNL Sites]部署视为用于网页创作的本地计算机，例如`https://[local_sites]:4502`。

1. 确保在[!DNL Sites]部署和AMS的[!DNL Assets]部署中存在具有适当范围的用户和角色。 在[!DNL Assets]部署中创建一个技术用户，并将其添加到[中提到的用户和涉及的](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved)组。

1. 访问`https://[local_sites]:4502`的本地[!DNL Sites]部署。 单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 连接的资产配置]**，并提供以下值：

   1. 配置的&#x200B;**[!UICONTROL 标题]**。
   1. **[!UICONTROL 远程]** DAM URL是格式 [!DNL Assets] 中位置的URL  `https://[assets_servername]:[port]`。
   1. DAM 分发人员（技术用户）的凭据。
   1. 在&#x200B;**[!UICONTROL 装载点]**&#x200B;字段中，输入[!DNL Experience Manager]获取资产的本地[!DNL Experience Manager]路径。 例如，`remoteassets` 文件夹。从DAM获取的资产存储在[!DNL Sites]部署的此文件夹中。
   1. **[!UICONTROL 本地站]** 点URL是部署的 [!DNL Sites] 位置。[!DNL Assets] 部署使用此值来维护对此部署获取的数字资产的 [!DNL Sites] 引用。
   1. [!DNL Sites]技术用户的凭据。
   1. **[!UICONTROL 原始二进制传输优化阈值]**&#x200B;字段的值指定是否同步传输原始资产（包括演绎版）。 可以轻松获取文件大小较小的资产，而文件大小相对较大的资产最好异步同步。 价值取决于您的网络功能。
   1. 如果您使用数据存储来存储您的资产，且数据存储是两个 部署之间的公用存储，请选择&#x200B;**[!UICONTROL 与连接的资产共享数据存储]**。在这种情况下，阈值限制并不重要，因为实际的资产二进制文件在数据存储上可用，并且不会传输。

   ![连接资产功能的典型配置](assets/connected-assets-typical-config.png)

   *图：连接资产功能的典型配置。*

1. 已处理[!DNL Assets]部署中的现有数字资产并生成演绎版。 这些演绎版是使用此功能获取的，因此无需重新生成演绎版。 禁用工作流启动器以阻止再生再现。 在([!DNL Sites])部署中调整启动程序配置，以排除`connectedassets`文件夹（将在此文件夹中获取资产）。

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
   >在作者获取资产时，将会获取该资产在远程 部署中可用的所有演绎版。如果要为获取的资产创建更多演绎版，请跳过此配置步骤。将触发[!UICONTROL  DAM更新资产]工作流，并创建更多演绎版。 这些再现仅在本地[!DNL Sites]部署中可用，而在远程DAM部署中不可用。

1. 将[!DNL Sites]部署添加为[!DNL Assets]部署上的CORS配置中允许的来源。

   1. 使用管理员凭据登录。 搜索 `Cross-Origin`. 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 运营]** > **[!UICONTROL Web 控制台]**。

   1. 要为[!DNL Sites]部署创建CORS配置，请单击&#x200B;**[!UICONTROL AdobeGranite跨来源资源共享策略]**&#x200B;旁边的“资产添加”选项![“添加图标](assets/do-not-localize/assets_add_icon.png)”。

   1. 在字段&#x200B;**[!UICONTROL 允许的来源]**&#x200B;中，输入本地[!DNL Sites]的URL，即`https://[local_sites]:[port]`。 保存配置。

您可以检查已配置的[!DNL Sites]部署与[!DNL Assets]部署之间的连接。

![已配置已连接资产的连接测试  [!DNL Sites]](assets/connected-assets-multiple-config.png)

## 使用远程资产 {#use-remote-assets}

网站作者使用内容查找器连接到DAM部署。 作者可以浏览、搜索以及拖动组件中的远程资产。要验证远程 DAM，请准备好管理员提供的 DAM 用户凭据。

作者可以在单个网页中使用本地DAM和远程DAM部署上的可用资产。 使用内容查找器，可在搜索本地 DAM 与搜索远程 DAM 之间切换。

只会获取远程资产的那些标记，这些标记具有与同一分类层次结构完全对应的标记，该分类层次结构在本地[!DNL Sites]部署中可用。 任何其他标记都将被丢弃。作者可以使用远程[!DNL Experience Manager]部署中显示的所有标记搜索远程资产，因为它会优惠全文搜索。

### 使用说明演示 {#walk-through-of-usage}

使用上述设置尝试创作体验，以了解该功能是如何运作的。使用您在远程 DAM 部署中选择的文档或图像。

1. 通过从[!DNL Experience Manager]工作区访问&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Files]**，导航到远程部署上的[!DNL Assets]接口。 或者，也可以在浏览器中访问 `https://[assets_servername_ams]:[port]/assets.html/content/dam`。上传您选择的资产。
1. 在[!DNL Sites]部署中，在右上角的用户档案激活器中，单击&#x200B;**[!UICONTROL 模拟为]**。 提供 `ksaner` 作为用户名，选择提供的选项，然后单击&#x200B;**[!UICONTROL 确定]**。
1. 打开 We.Retail 网页：**[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL us]** > **[!UICONTROL en]**。编辑页面。或者，也可以在浏览器中访问 `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` 以编辑页面。

   单击页面左上角的&#x200B;**[!UICONTROL 切换侧面板]**。

1. 打开[!UICONTROL 资产]选项卡，然后单击&#x200B;**[!UICONTROL 登录到已连接的资产]**。
1. 提供凭据 -- `ksaner` 作为用户名，`password` 作为密码。此用户对[!DNL Experience Manager]部署都具有创作权限。
1. 搜索您添加到 DAM 的资产。远程资产会显示在左侧面板中。筛选图像或文档，并进一步筛选支持的文档类型。拖动 `Image` 组件上的图像和 `Download` 组件上的文档。

   在本地[!DNL Sites]部署中，获取的资源是只读的。 您仍然可以使用[!DNL Sites]组件提供的选项来编辑获取的资产。 通过组件进行的编辑是无损的。

   ![在远程 DAM 上搜索资产时，筛选文档类型和图像的选项](assets/filetypes_filter_connected_assets.png)

   *图：在远程 DAM 上搜索资产时，筛选文档类型和图像的选项.*

1. 如果异步获取资产且获取任务失败，会通知站点作者。在创作时，甚至在创作之后，作者可以在[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面中查看有关提取任务和错误的详细信息。

   ![关于在后台进行的异步获取资产的通知。](assets/assets_async_transfer_fails.png)

   *图：关于在后台进行的异步获取资产的通知。*

1. 发布页面时，[!DNL Experience Manager]会显示页面上使用的资产的完整列表。 请确保在发布时成功获取了远程资产。要检查每个获取的资产的状态，请参阅[异步作业](/help/sites-administering/asynchronous-jobs.md)用户界面。

   >[!NOTE]
   >
   >即使未获取一个或多个远程资产，页面也会发布。使用该远程资产的组件发布为空。[!DNL Experience Manager]通知区域显示在异步作业页中显示错误的通知。

>[!CAUTION]
>
>在网页中使用后，获取的远程资源便可以被具有访问本地文件夹权限的用户搜索和使用。 获取的资源存储在本地文件夹中（上面的浏览中的`connectedassets`）。 此外，还可通过[!UICONTROL 内容查找器]，搜索和查看本地存储库中的资产。

获取的资产可用作任何其他本地资产，但关联的元数据无法编辑。

### 检查跨网页{#asset-usage-references}使用资产的情况

[!DNL Experience Manager] 允许DAM用户检查对资产的所有引用。它有助于了解和管理远程[!DNL Sites]和复合资产中资产的使用情况。 [!DNL Experience Manager Sites]部署中的许多网页作者都可以在不同网页中使用远程[!DNL Assets]上的资源。 要简化资产管理，而不是导致引用损坏，DAM用户必须检查本地和远程网页中资产的使用情况。 资产的[!UICONTROL 属性]页面中的[!UICONTROL 引用]选项卡列表了资产的本地和远程引用。

要视图和管理[!DNL Assets]部署上的引用，请执行以下步骤：

1. 在[!DNL Assets]控制台中选择资产，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。
1. 单击&#x200B;**[!UICONTROL 引用]**&#x200B;选项卡。 有关在[!DNL Assets]部署中使用资产的信息，请参阅&#x200B;**[!UICONTROL 本地引用]**。 请参阅**[!UICONTROL 远程引用]，以在[!DNL Sites]部署中使用“已连接资产”功能获取资产时使用资产。

   ![资产属性中的远程引用](assets/connected-assets-remote-reference.png)

1. [!DNL Sites]页的引用显示每个本地[!DNL Sites]的引用总数。 查找所有引用并显示引用的总数可能需要一些时间。
1. 引用的列表是交互式的，DAM用户可以单击引用以打开引用页面。 如果由于某种原因无法获取远程引用，则显示通知，通知用户失败。
1. 用户可以移动或删除资产。 移动或删除资产时，所有选定资产/文件夹的引用总数会显示在警告对话框中。 删除尚未显示引用的资产时，将显示警告对话框。

   ![强制删除警告](assets/delete-referenced-asset.png)

## 限制和最佳实践{#tip-and-limitations}

* 要获得有关资产使用情况的洞察，请在[!DNL Sites]实例上配置[资产分析](/help/assets/asset-insights.md)功能。

### 权限和资产管理{#permissions-and-managing-assets}

* 本地资产与远程部署中的原始资产不同步。在 DAM 部署上所具有的任何编辑、删除或撤销权限均不会传播到下游。
* 本地资产是只读副本。[!DNL Experience Manager] 组件对资产进行无损编辑。不允许进行其他编辑。
* 本地获取的资产只能用于创作。不能应用资产更新工作流，也不能编辑元数据。
* 仅支持图像和列出的文档格式。[!DNL Dynamic Media]不支持 资产、内容片段和体验片段。
* [!DNL Experience Manager] 不会获取元数据模式。这意味着可能无法显示获取的所有元数据。 如果单独更新模式，则显示所有属性。
* 所有[!DNL Sites]作者都对获取的副本具有读取权限，即使作者无法访问远程DAM部署。
* 没有支持自定义集成的 API。
* 该功能支持无缝搜索和使用远程资产。为了能够在本地部署中一次使用许多远程资产，请考虑批量迁移这些资产。请参阅 [Assets 迁移指南](assets-migration-guide.md)。
* 无法在[!UICONTROL 页面属性]用户界面上将远程资产用作页面缩略图。 单击[!UICONTROL 选择图像]可在[!UICONTROL 缩略图]的[!UICONTROL 页面属性]用户界面中设置网页的缩略图。

### 设置和许可 {#setup-licensing}

* [!DNL Assets] 支持在 [!DNL Adobe Managed Services] 上部署。
* [!DNL Sites] 一次可以连接到 [!DNL Assets] 单个存储库。
* [!DNL Assets]作为远程存储库工作的许可证。
* [!DNL Sites]的一个或多个许可证用作本地创作部署。

### 使用 {#usage}

* 在创作时，用户可以搜索远程资产并在本地页面上拖动这些资产。 不支持其他功能。
* 获取操作会在 5 秒后超时。作者在获取资产时可能会遇到问题，比如，网络问题。作者可以通过将远程资产从[!UICONTROL Content Finder]拖动到[!UICONTROL 页面编辑器]来重新尝试。
* 可以对获取的资产执行无损的简单编辑以及 `Image` 组件支持的编辑。资产是只读的。
* 重新提取资产的唯一方法是将其拖动到页面上。 没有API支持或其他方法可重新获取资源以进行更新。
* 如果资产从DAM中停止使用，则这些资产将继续在[!DNL Sites]页面上使用。
* 资产的远程引用条目以异步方式获取。 引用和总计数不是实时的，如果在DAM用户查看引用时站点作者使用资产，则可能会有一些差异。 DAM用户可以刷新页面，并在几分钟后重试以获取总计数。

## 故障诊断问题 {#troubleshoot}

要排除常见错误，请执行以下步骤：

* 如果您无法从[!UICONTROL 内容查找器]中搜索远程资产，请确保所需的角色和权限都到位。
* 由于一个或多个原因，从远程大坝获取的资产可能无法发布到网页上。 它不存在于远程服务器上，缺少相应的获取权限，或者网络故障可能是原因。 确保未从远程DAM中删除资产。 请确保适当的权限到位并满足先决条件。 重试将资产添加到页面并重新发布。 检查[异步作业列表](/help/sites-administering/asynchronous-jobs.md)，查看是否发生了资产获取错误。
* 如果无法从本地[!DNL Sites]部署访问远程DAM部署，请确保允许跨站点Cookie。 如果跨站点Cookie被阻止，则[!DNL Experience Manager]的两个部署可能无法进行身份验证。 例如，在Incognito模式下，[!DNL Google Chrome]可能会阻止第三方Cookie。 要允许[!DNL Chrome]浏览器中的Cookie，请单击地址栏中的“眼睛”图标，导航到“站点不工作”>“阻止”，选择“远程DAM URL”，然后允许登录令牌Cookie。 或者，请参阅有关[如何启用第三方Cookie的帮助](https://support.google.com/chrome/answer/95647)。

   ![Chrome中的Cookie错误](assets/chrome-cookies-incognito-dialog.png)

* 如果未检索远程引用并导致错误消息，请检查站点部署是否可用，并检查网络连接问题。 稍后重试以进行检查。 [!DNL Assets] 部署尝试两次建立与部署的 [!DNL Sites] 连接，然后报告失败。

![重试资产远程引用失败](assets/reference-report-failure.png)
