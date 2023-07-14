---
title: 文件夹共享到 [!DNL Adobe Creative Cloud] 最佳实践
description: 配置 [!DNL Adobe Experience Manager] 允许用户进入 [!DNL Experience Manager Assets] 以与Adobe Creative Cloud用户交换文件夹。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 到 [!DNL Adobe Creative Cloud] 文件夹共享 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>此 [!DNL Experience Manager] 到 [!DNL Creative Cloud] 已弃用文件夹共享功能。 Adobe建议使用较新的功能，例如 [Adobe资源链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 或 [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). 了解详情，请参阅 [Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] 可配置为允许用户进入 [!DNL Assets] 要与的用户共享文件夹，请执行以下操作 [!DNL Adobe Creative Cloud] 应用程序，因此它们可用作中的共享文件夹 [!DNL Adobe Creative Cloud] assets服务。 该功能可用于在创意团队和团队之间交换文件 [!DNL Assets] 用户，尤其是创意用户无权访问 [!DNL Assets] 部署（它们不在企业网络上）。

此类型的集成可用于以下用例，尤其是当使用无法直接访问的用户时 [!DNL Assets]：

* [!DNL Assets] 用户与的用户共享一组特定的数字资产 [!DNL Adobe Creative Cloud] 文件（例如，创意简介和一组批准用于新营销活动的设计资产）。
* [!DNL Assets] 用户会收到由创建的新文件 [!DNL Adobe Creative Cloud] 应用程序用户。

>[!NOTE]
>
>在阅读本文档之前，您可以查看整个 [Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md) 以了解集成的概述。

## 概述 {#overview}

[!DNL Experience Manager] 到 [!DNL Creative Cloud] 文件夹共享依赖于在服务器端之间共享文件夹和文件 [!DNL Assets] 和 [!DNL Creative Cloud] 帐户。 使用 [!DNL Creative Cloud] 桌面应用程序也可以使用直接在磁盘上提供共享文件夹 [!DNL Adobe CreativeSync] 技术。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

该集成包含以下元素：

* **[!DNL Experience Manager Assets]** 在企业网络(Managed Services或内部部署)中部署：在此处启动文件夹共享。
* **[!DNL Adobe Experience Cloud Assets]核心服务**：充当以下两者之间的中介： [!DNL Experience Manager] 和 [!DNL Creative Cloud] 存储服务。 使用集成的组织管理员必须在Experience Cloud组织与 [!DNL Assets] 部署。 他们还 [定义已批准的Creative Cloud协作者列表](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html)，即 [!DNL Assets] 为了增加安全性，用户也可以共享文件夹。

* **[!DNL Creative Cloud]Assets Web服务** (存储和 [!DNL Creative Cloud] 文件(Web UI)：这是特定Creative Cloud应用程序用户(这些用户具有 [!DNL Assets] 文件夹已共享，将能够接受邀请并在其Creative Cloud帐户存储中看到该文件夹。
* **Creative Cloud桌面应用程序**：（可选）允许通过与同步，从创意用户的桌面直接访问共享文件夹/文件 [!DNL Creative Cloud] 资产存储。

## 特点和限制 {#characteristics-and-limitations}

* **更改的单向传播：** 文件更改仅在一个方向上传播 — 从系统([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])，资产最初创建（上传）的位置。 该集成不提供两个系统之间的完全自动化的双向同步。
* **版本控制:**

   * [!DNL Experience Manager] 仅当文件源自以下位置时，才会在更新时创建资源的版本 [!DNL Experience Manager] 并在该处进行了更新。
   * [!DNL Creative Cloud] Assets提供自己的 [版本控制功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 此更新旨在进行中的工作更新（基本上，可将更新存储最多10天）

* **空间限制：** 交换的文件的大小和卷受特定的 [Creative Cloud资源配额](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 对于创意用户（取决于订阅级别），最大文件大小限制为5 GB。 空间还受到组织在Adobe Experience Cloud Assets核心服务中拥有的资源配额的限制。

* **空间要求：** 共享文件夹中的文件还必须实际存储在 [!DNL Experience Manager] 然后在 [!DNL Creative Cloud] 帐户，具有缓存的副本 [!DNL Experience Cloud Assets] 核心服务。
* **网络和带宽：** 必须通过网络在系统之间传输共享文件夹中的文件和所有更新。 确保仅共享相关文件和更新。
* **文件夹类型**：共享 [!DNL Assets] 类型的文件夹 `sling:OrderedFolder`中的共享上下文中不支持 [!DNL Adobe Experience Cloud]. 如果要共享文件夹，请在中创建该文件夹时 [!DNL Assets]，请勿选择 [!UICONTROL 已排序] 选项。

## 最佳实践 {#best-practices}

使用的最佳实践 [!DNL Experience Manager] 到 [!DNL Creative Cloud] 文件夹共享包括：

* **卷注意事项：** [!DNL Experience Manager] 和 [!DNL Creative Cloud] 文件夹共享可用于共享较少数量的文件，例如，与特定营销策划或活动相关的文件。 要共享更大的资产集（如组织中的所有已批准资产），请使用其他分配方法(例如， [!DNL Assets Brand Portal])或 [!DNL Experience Manager] 桌面应用程序。
* **避免共享深层层次结构：** 共享以递归方式工作，不允许选择性取消共享。 通常，只应考虑共享没有子文件夹或层次结构较浅的文件夹（如一个子文件夹级别）。
* **用于单向共享的单独文件夹：** 应使用单独的文件夹从共享最终资源 [!DNL Assets] 到 [!DNL Creative Cloud] 文件，并用于从共享创意就绪的资产 [!DNL Creative Cloud] 文件到 [!DNL Assets]. 再加上这些文件夹的良好命名约定，它为创建更易于理解的工作环境 [!DNL Assets] 和 [!DNL Creative Cloud] 用户都一样。
* **避免在共享文件夹中使用WIP：** 共享文件夹不能用于进行中的工作 — 在Creative Cloud文件中使用单独的文件夹来执行需要经常更改文件的工作。
* **在共享文件夹之外开始新工作：** 新设计（创意文件）应在Creative Cloud文件中的单独WIP文件夹中启动，并且当它们可以共享时 [!DNL Assets] 用户时，应将他们移动或保存到共享文件夹。
* **简化共享结构：** 要获得更易于管理的操作设置，请考虑简化共享结构。 与其与所有创意用户共享， [!DNL Assets] 文件夹应仅与团队代表共享，例如创意总监或团队经理。 创意方面的经理将接收最终资产，决定工作分配，然后让设计人员在其自己的Creative Cloud帐户中工作。 他们可以使用Creative Cloud协作功能来协调工作，最后选择并放置要共享回的资源 [!DNL Assets] 放入其创意就绪的共享文件夹。

下图说明了用于根据中的现有最终资源创建设计的示例配置 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
