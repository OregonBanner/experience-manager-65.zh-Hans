---
title: 文件夹共享到 [!DNL Adobe Creative Cloud] 最佳实践
description: 配置 [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 以与Adobe Creative Cloud(CC)用户交换文件夹。
contentOwner: AG
role: User, Admin
feature: 协作
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 到文 [!DNL Adobe Creative Cloud] 件夹共享 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager]到[!DNL Creative Cloud]的文件夹共享功能已弃用。 Adobe强烈建议使用较新的功能，如[Adobe资产链接](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)或[Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 在[Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)中了解更多信息。

[!DNL Adobe Experience Manager] 中的用户可以与应用 [!DNL Assets] 程序的用户共享文件夹，以 [!DNL Adobe Creative Cloud] 便他们在资产服务中可以作为共享 [!DNL Adobe Creative Cloud] 文件夹。该功能可用于在创意团队和[!DNL Assets]用户之间交换文件，尤其是当创意用户无权访问[!DNL Assets]部署时（他们不在企业网络上）。

此类集成可用于以下用例，特别是在与没有直接访问[!DNL Assets]的用户合作时：

* [!DNL Assets] 用户与文件用户共享一组特定的数 [!DNL Adobe Creative Cloud] 字资产（例如，创作摘要和一组用于新营销活动的设计作品的已批准资产）。
* [!DNL Assets] 用户将收到由应用程序用户创建 [!DNL Adobe Creative Cloud] 的新文件。

>[!NOTE]
>
>在阅读本文档之前，您可以查看整体[Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)以了解集成的概述。

## 概述 {#overview}

[!DNL Experience Manager] 文件夹 [!DNL Creative Cloud] 共享依赖于和帐户之间在服务器端共享文件夹和 [!DNL Assets] 文 [!DNL Creative Cloud] 件。在桌面上使用[!DNL Creative Cloud]桌面应用程序的创意专业人士，还可以使用[!DNL Adobe CreativeSync]技术，在其磁盘上直接提供共享文件夹。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

该集成包含以下元素：

* **[!DNL Experience Manager Assets]** 部署在企业网络（托管服务或内部部署）中：在此处启动文件夹共享。
* **[!DNL Adobe Marketing Cloud Assets]核心服务**:在和存储服务之 [!DNL Experience Manager] 间 [!DNL Creative Cloud] 充当中介。使用集成的组织的管理员需要在Marketing Cloud组织与[!DNL Assets]部署之间建立信任关系。 它们还[定义了已批准的Creative Cloud协作者](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)的列表，[!DNL Assets]用户也可以共享文件夹，以提高安全性。

* **[!DNL Creative Cloud]资产Web服务** (存储和 [!DNL Creative Cloud] 文件Web UI):在这里，与之共享文件夹的特定Creative Cloud [!DNL Assets] 应用程序用户将能够接受邀请并在其Creative Cloud帐户存储中查看该文件夹。
* **Creative Cloud桌面应用程序**:（可选）允许通过与Assets存储同步，从创意用户的桌面直接访问共享文件夹/ [!DNL Creative Cloud] 文件。

## 特征和限制 {#characteristics-and-limitations}

* **更改的单向传播：** 文件更改仅沿一个方向传播 — 从最初创建（上传）资产的系统([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])传播。该集成不会在两个系统之间提供完全自动的双向同步。
* **版本控制:**

   * [!DNL Experience Manager] 仅当文件源于，并且在该处进行更新时，才会在更 [!DNL Experience Manager] 新时创建资产版本。
   * [!DNL Creative Cloud] Assets提供了自己的版 [本控](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 制功能，该功能可针对进行中的更新（基本上，可将更新存储长达10天）

* **空间限制：** 交换的文件大小和卷数受创意用户 [的特](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 定Creative Cloud资产配额（取决于订阅级别）和最大文件大小限制为5 GB。此外，组织在Adobe Marketing Cloud Assets核心服务中的资产配额也会限制空间。

* **空间要求：** 共享文件夹中的文件还需要先物理存储在中， [!DNL Experience Manager] 然后 [!DNL Creative Cloud] 再存储在帐户中，并在核心服务中缓存 [!DNL Marketing Cloud Assets] 一个副本。
* **网络和带宽：** 共享文件夹中的文件和所有更新需要通过网络在系统之间传输。您应确保仅共享相关文件和更新。
* **文件夹类型**:在中 [!DNL Assets] 共享的上 `sling:OrderedFolder`下文中不支持共享类型的文 [!DNL Adobe Marketing Cloud]件夹。如果要共享文件夹，请在[!DNL Assets]中创建文件夹时，请勿选择[!UICONTROL 已排序]选项。

## 最佳实践 {#best-practices}

利用[!DNL Experience Manager]到[!DNL Creative Cloud]文件夹共享的最佳实践包括：

* **卷注意事项：** [!DNL Experience Manager] 和“ [!DNL Creative Cloud] 文件夹共享”应用于共享较少数量的文件，例如，与特定营销活动或活动相关的文件。要共享较大的资产集（与组织中所有已批准的资产一样），请使用其他分发方法（例如[!DNL Assets Brand Portal]）或[!DNL Experience Manager]桌面应用程序。
* **避免共享深层次：** 按递归方式共享，不允许选择性取消共享。通常，只应考虑共享没有子文件夹或层次结构非常浅（如1个子文件夹级别）的文件夹。
* **单向共享的单独文件夹：** 应使用单独的文件夹将最终资产从共享到 [!DNL Assets] 文 [!DNL Creative Cloud] 件，以及将创意就绪资产从文件共享回 [!DNL Creative Cloud]  [!DNL Assets]文件。除了为这些文件夹制定了良好的命名规范外，它还为[!DNL Assets]和[!DNL Creative Cloud]用户创建了一个更易于理解的工作环境。
* **避免在共享文件夹中出现WIP:** 共享文件夹不应用于进行中的工作 — 在Creative Cloud文件中使用单独的文件夹来执行需要频繁更改文件的工作。
* **在共享文件夹之外开始新工作：** 应在“Creative Cloud文件”的单独WIP文件夹中启动新设计（创作文件），当它们准备好与用户共享时，应将它们移 [!DNL Assets] 动或保存到共享文件夹。
* **简化共享结构：** 要实现更易于管理的操作设置，请考虑简化共享结构。应仅与团队代表共享[!DNL Assets]文件夹，而不是与所有创意用户共享，如创意总监或团队经理。 创意方面的经理将接收最终资产，决定工作分配，然后让设计人员在自己的Creative Cloud帐户中处理WIP资产。 他们可以使用Creative Cloud协作功能来协调工作，最后选择已准备好共享到[!DNL Assets]的资产并将其放入其可供创作的共享文件夹。

下图说明了一个示例配置，用于根据[!DNL Assets]中的现有最终资产创建新设计。

![chlimage_1-180](assets/chlimage_1-407.png)
