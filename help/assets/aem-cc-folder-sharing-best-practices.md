---
title: 文件夹共享到 [!DNL Adobe Creative Cloud] 最佳实践
description: 配置 [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 以与Adobe Creative Cloud(CC)用户交换文件夹。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18e62f8fb46de20e1668b2dcdcedf68fe4622b50
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 到文 [!DNL Adobe Creative Cloud] 件夹共享  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager]到[!DNL Creative Cloud]文件夹共享功能已弃用。 Adobe强烈建议使用较新的功能，如[Adobe资产链接](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)或[Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 了解有关[Experience Manager和Creative Cloud集成最佳实践的更多信息](/help/assets/aem-cc-integration-best-practices.md)。

[!DNL Adobe Experience Manager] 可以配置为允许中的用户与 [!DNL Assets] 应用程序的用户共享文件 [!DNL Adobe Creative Cloud] 夹，以便他们在“资产”服务中可以作为共 [!DNL Adobe Creative Cloud] 享文件夹。该功能可用于在创意团队和[!DNL Assets]用户之间交换文件，尤其是当创意用户无权访问[!DNL Assets]部署时（他们不在企业网络上）。

此类集成可用于以下用例，特别是与没有直接访问[!DNL Assets]权限的用户合作时：

* [!DNL Assets] 用户与文件用户共享一组特定数字资 [!DNL Adobe Creative Cloud] 产(例如，为新的营销活动设计作品的创意简介和一组获准资产)。
* [!DNL Assets] 用户将收到由应用程序用户创 [!DNL Adobe Creative Cloud] 建的新文件。

>[!NOTE]
>
>在阅读此文档之前，您可以查看整体[Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)，了解集成的概述。

## 概述 {#overview}

[!DNL Experience Manager] 到文 [!DNL Creative Cloud] 件夹共享依赖于与帐户之间的文件夹和文件 [!DNL Assets] 的服 [!DNL Creative Cloud] 务器端。在桌面上使用[!DNL Creative Cloud]桌面应用程序的创意专业人士还可以使用[!DNL Adobe CreativeSync]技术在其磁盘上直接提供共享文件夹。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

该集成包含以下元素：

* **[!DNL Experience Manager Assets]** 部署在企业网络（托管服务或内部部署）中：在此处启动文件夹共享。
* **[!DNL Adobe Marketing Cloud Assets]核心服务**:充当与存储服务之 [!DNL Experience Manager] 间 [!DNL Creative Cloud] 的中介。使用集成的组织的管理员需要在Marketing Cloud组织与[!DNL Assets]部署之间建立信任关系。 他们还[定义了已批准的Creative Cloud协作者](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)的列表,[!DNL Assets]用户也可以共享文件夹，以增强安全性。

* **[!DNL Creative Cloud]资产Web服务** (存储和 [!DNL Creative Cloud] 文件Web UI):这是特定Creative Cloud应用程序用户能够接受邀 [!DNL Assets] 请并在其Creative Cloud帐户存储中查看该文件夹的位置。
* **Creative Cloud桌面应用程序**:（可选）允许通过与资产存储同步从创意用户的桌面直接访问共享文件夹/ [!DNL Creative Cloud] 文件。

## 特性和限制{#characteristics-and-limitations}

* **更改的单向传播：文** 件更改仅向一个方向传播 — 从最初创建(上[!DNL Experience Manager] 传 [!DNL Creative Cloud Assets])资产的系统（或）。该集成不提供两个系统之间完全自动的双向同步。
* **版本控制:**

   * [!DNL Experience Manager] 如果文件源于并在更新时更新，则仅在更新时创 [!DNL Experience Manager] 建资产的版本。
   * [!DNL Creative Cloud] Assets提供其自己的版 [本](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 控制功能，该功能针对“进行中的工作”更新（基本上，将更新存储最多10天）

* **空间限制：** 交换的文件大小和数量受特定Creative Cloud资 [产配额](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) (取决于订阅级别)的限制，最大文件大小限制为5 GB。此外，组织在Adobe Marketing Cloud Assets核心服务中拥有的资产配额也限制了空间。

* **空间要求：** 共享文件夹中的文件还需要物理存储在 [!DNL Experience Manager] 内，然 [!DNL Creative Cloud] 后存储在帐户中，核心服务中有缓 [!DNL Marketing Cloud Assets] 存副本。
* **网络和带宽：** 共享文件夹中的文件和所有更新需要通过网络在系统之间传输。您应确保仅共享相关文件和更新。
* **文件夹类型**:在中 [!DNL Assets] 共享的上 `sling:OrderedFolder`下文中不支持共享类型的文件夹 [!DNL Adobe Marketing Cloud]。如果要共享文件夹，请在[!DNL Assets]中创建文件夹时，不要选择[!UICONTROL “已排序]”选项。

## 最佳实践{#best-practices}

将[!DNL Experience Manager]用于[!DNL Creative Cloud]文件夹共享的最佳实践包括：

* **卷注意事** [!DNL Experience Manager] 项： [!DNL Creative Cloud] 应使用“文件夹共享”来共享较少数量的文件，例如，与特定活动或活动相关的文件。要共享较大的资产集（与组织中所有已批准的资产一样），请使用其他分发方法（例如[!DNL Assets Brand Portal]）或[!DNL Experience Manager]桌面应用程序。
* **避免共享深层次结构：** 共享以递归方式工作，不允许选择性取消共享。通常，只有没有子文件夹或层次结构非常浅的文件夹（如1个子文件夹级别）才应考虑共享。
* **单向共享应使用单独的文** 件夹：应使用单独的文件夹，将最终的资 [!DNL Assets] 产 [!DNL Creative Cloud] 从文件共享到文件，并将创意就绪型资源从文件共享 [!DNL Creative Cloud] 回 [!DNL Assets]到文件。除了为这些文件夹创建良好的命名约定外，它还为[!DNL Assets]和[!DNL Creative Cloud]用户创建了易于理解的工作环境。
* **在共享文件夹中避免** WIP：不应将共享文件夹用于进行中工作 — 在Creative Cloud文件中使用单独的文件夹来执行需要频繁更改文件的工作。
* **开始共享文件夹外的新** 工作：新设计（创作文件）应在Creative Cloud文件中的单独WIP文件夹中启动，当它们准备好与用户共享时，应将 [!DNL Assets] 它们移动或保存到共享文件夹。
* **简化共享结构：** 要实现更易于管理的操作设置，请考虑简化共享结构。应仅与团队代表共享[!DNL Assets]文件夹，而不是与所有创意用户共享，如创意总监或团队经理。 创意部门的经理将接收最终资产，决定工作分配，然后让设计人员在自己的Creative Cloud帐户中处理WIP资产。 他们可以使用Creative Cloud协作功能来协调工作，最后选择准备好共享回[!DNL Assets]的资源并将其放入其可供创意使用的共享文件夹。

下图说明了一个用于根据[!DNL Assets]的现有最终资产创建新设计的示例配置。

![chlimage_1-180](assets/chlimage_1-407.png)
