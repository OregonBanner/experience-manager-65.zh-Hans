---
title: 文件夹共享到 [!DNL Adobe Creative Cloud] 最佳实践
description: 配置 [!DNL Adobe Experience Manager] 允许用户在 [!DNL Experience Manager Assets] 与Adobe Creative Cloud用户交换文件夹。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] to [!DNL Adobe Creative Cloud] 文件夹共享 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>的 [!DNL Experience Manager] to [!DNL Creative Cloud] 已弃用文件夹共享功能。 Adobe强烈建议使用较新的功能，例如 [Adobe资产链接](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 或 [Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). 在 [Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] 可以配置为允许用户在 [!DNL Assets] 与的用户共享文件夹 [!DNL Adobe Creative Cloud] ，因此它们可用作共享文件夹 [!DNL Adobe Creative Cloud] 资产服务。 该功能可用于在创意团队和 [!DNL Assets] 用户，尤其是当创意用户无权访问 [!DNL Assets] 部署（它们不在企业网络上）。

此类集成可在以下用例中使用，尤其是在与没有直接访问权限的用户合作时 [!DNL Assets]:

* [!DNL Assets] 用户与 [!DNL Adobe Creative Cloud] 文件（例如，为新营销活动设计的创作摘要和一组已批准的资产）。
* [!DNL Assets] 用户将收到由 [!DNL Adobe Creative Cloud] 应用程序用户。

>[!NOTE]
>
>在阅读本文档之前，您可以查看 [Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md) 以了解集成的概述。

## 概述 {#overview}

[!DNL Experience Manager] to [!DNL Creative Cloud] 文件夹共享依赖于在服务器端在 [!DNL Assets] 和 [!DNL Creative Cloud] 帐户。 使用 [!DNL Creative Cloud] 桌面应用程序，则还可以使用 [!DNL Adobe CreativeSync] 技术。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

该集成包含以下元素：

* **[!DNL Experience Manager Assets]** 部署在企业网络（托管服务或内部部署）中：在此处启动文件夹共享。
* **[!DNL Adobe Marketing Cloud Assets]核心服务**:在 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 存储服务。 使用集成的组织的管理员需要在Marketing Cloud组织和 [!DNL Assets] 部署。 此外， [定义已批准的Creative Cloud协作者列表](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), [!DNL Assets] 用户也可以共享文件夹，以提高安全性。

* **[!DNL Creative Cloud]资产Web服务** (存储和 [!DNL Creative Cloud] 文件web UI):这是特定Creative Cloud应用程序用户(与 [!DNL Assets] 文件夹已共享，将能够接受邀请并在其Creative Cloud帐户存储中查看该文件夹。
* **Creative Cloud桌面应用程序**:（可选）允许通过与同步，从创意用户的桌面直接访问共享文件夹/文件 [!DNL Creative Cloud] 资产存储。

## 特征和限制 {#characteristics-and-limitations}

* **更改的单向传播：** 文件更改仅沿一个方向传播 — 从系统([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])，即最初创建（上传）资产的位置。 该集成不会在两个系统之间提供完全自动的双向同步。
* **版本控制:**

   * [!DNL Experience Manager] 仅当文件源于 [!DNL Experience Manager] 和已更新。
   * [!DNL Creative Cloud] 资产自行提供 [版本控制功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 定位在进行中的更新（基本上，可将更新存储长达10天）

* **空间限制：** 交换的文件的大小和数量受特定 [Creative Cloud资产配额](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 对于创意用户（取决于订阅级别），最大文件大小限制为5 GB。 此外，组织在Adobe Marketing Cloud Assets核心服务中的资产配额也会限制空间。

* **空间要求：** 共享文件夹中的文件还需要在 [!DNL Experience Manager] 然后在 [!DNL Creative Cloud] 帐户，已缓存副本 [!DNL Marketing Cloud Assets] 核心服务。
* **网络和带宽：** 共享文件夹中的文件和所有更新需要通过网络在系统之间传输。 您应确保仅共享相关文件和更新。
* **文件夹类型**:共享 [!DNL Assets] 类型的文件夹 `sling:OrderedFolder`，在共享的上下文中不受支持 [!DNL Adobe Marketing Cloud]. 如果要共享文件夹，请在 [!DNL Assets]，请勿选择 [!UICONTROL 已排序] 选项。

## 最佳实践 {#best-practices}

利用 [!DNL Experience Manager] to [!DNL Creative Cloud] 文件夹共享包括：

* **卷注意事项：** [!DNL Experience Manager] 和 [!DNL Creative Cloud] 文件夹共享应用于共享较少数量的文件，例如，与特定营销活动或活动相关的文件。 要共享较大的资产集（与组织中所有已批准的资产一样），请使用其他分配方法(例如， [!DNL Assets Brand Portal])或 [!DNL Experience Manager] 桌面应用程序。
* **避免共享深层次：** 按照递归方式进行共享，不允许选择性取消共享。 通常，只应考虑共享没有子文件夹或层次结构非常浅（如1个子文件夹级别）的文件夹。
* **单向共享的单独文件夹：** 应使用单独的文件夹共享最终的资产 [!DNL Assets] to [!DNL Creative Cloud] 文件，以及用于从共享创意就绪资产 [!DNL Creative Cloud] 文件到 [!DNL Assets]. 除了为这些文件夹提供良好的命名规范外，它还为 [!DNL Assets] 和 [!DNL Creative Cloud] 用户相似。
* **避免在共享文件夹中出现WIP:** 不应将共享文件夹用于进行中的工作 — 在Creative Cloud文件中使用单独的文件夹来执行需要频繁更改文件的工作。
* **在共享文件夹之外开始新工作：** 新设计（创作文件）应在“Creative Cloud文件”的单独WIP文件夹中启动，并在它们准备好与共享时启动 [!DNL Assets] 用户，则应将他们移动或保存到共享文件夹。
* **简化共享结构：** 要建立更易于管理的操作集，请考虑简化共享结构。 与其与所有创意用户共享， [!DNL Assets] 文件夹应仅与团队代表共享，如创意总监或团队经理。 创意方面的经理将接收最终资产，决定工作分配，然后让设计人员在自己的Creative Cloud帐户中处理WIP资产。 他们可以使用Creative Cloud协作功能来协调工作，最后选择并放置已准备好共享的资产回到 [!DNL Assets] 到其可供创意使用的共享文件夹中。

下图展示了一个示例配置，用于根据 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
