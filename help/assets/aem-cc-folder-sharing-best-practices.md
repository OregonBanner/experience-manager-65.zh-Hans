---
title: Adobe Experience Manager到Adobe Creative Cloud文件夹，共享最佳实践
description: 配置Adobe Experience Manager，允许Experience Manager资产中的用户与Adobe Creative Cloud(CC)用户交换文件夹。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---


# Adobe Experience Manager到Adobe Creative Cloud文件夹共享 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>已弃用Experience Manager到Creative Cloud文件夹共享功能。 Adobe强烈建议使用Adobe Asset Link或 [Experience Manager桌面应用](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)[程序等新功能](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)。 了解有关Experience Manager [和Creative Cloud集成最佳实践的更多信息](/help/assets/aem-cc-integration-best-practices.md)。

Adobe Experience Manager可以配置为允许资产中的用户与Adobe Creative Cloud应用程序的用户共享文件夹，这样，在Adobe Creative Cloud Assets服务中，这些用户便可以作为共享文件夹。 该功能可用于在创意团队和资产用户之间交换文件，尤其是当创意用户无权访问资产部署时（他们不在企业网络上）。

此类集成可用于以下用例，尤其是与没有直接访问资产权限的用户合作时：

* 资产用户与Adobe Creative Cloud文件的用户共享一组特定资产(例如，为新的营销活动进行设计工作而提供的创意简介和一组获准资产)
* 资产用户会收到由Adobe Creative Cloud应用程序用户创建的新文件。

>[!NOTE]
>
>在阅读此文档之前，您可以查看整 [体Experience Manager和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md) ，以获得主题的更高级概述。

## 概述 {#overview}

Experience Manager到Creative Cloud文件夹共享依赖于资产和Creative Cloud帐户之间的文件夹和文件的服务器端共享。 在桌面上使用Creative Cloud桌面应用程序的创意专业人士还可以使用Adobe CreativeSync技术直接在其磁盘上提供共享文件夹。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

集成包括以下元素：

* **Experience Manager资产** （托管服务或内部部署）在企业网络中部署的服务器： 此处启动文件夹共享。
* **Adobe Marketing Cloud资产核心服务**: 充当Experience Manager和Creative Cloud存储服务之间的中介。 使用集成的公司管理员需要在Marketing Cloud组织和资产部署之间建立信任关系。 它们还定 [义了经过批准的Creative Cloud协作者的列表](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)，资产用户也可以共享文件夹以提高安全性。

* **Creative Cloud Assets Web服务** (存储和Creative Cloud文件Web UI): 在这里，已与其共享Assets文件夹的特定Creative Cloud应用程序用户可以接受邀请并在其Creative Cloud帐户存储中查看该文件夹。
* **Creative Cloud桌面应用程序**: （可选）允许通过与Creative Cloud资产存储同步，从创意用户的桌面直接访问共享文件夹／文件。

## 特点和限制 {#characteristics-and-limitations}

* **更改的单向传播：** 文件更改仅从最初创建（上传）资产的系统(Experience Manager或Creative Cloud资产)单向传播。 该集成不提供两个系统之间的完全自动化的双向同步。
* **版本控制:**

   * Experience Manager仅在文件源于Experience Manager且在更新时创建资产版本。
   * Creative Cloud Assets提供其自己的 [版本控制功](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 能，该功能针对进行中的更新（基本上，将更新存储最多10天）

* **空间限制：** 交换的文件大小和数量受特定Creative Cloud Assets [配额(取决于订阅级别](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) )和最大文件大小限制(5 GB)的限制。 此外，Adobe Marketing Cloud资产核心服务中的资产配额也会限制空间。

* **空间要求：** 共享文件夹中的文件还需要先以Experience Manager存储，再以Creative Cloud帐户存储，并在Marketing Cloud Assets核心服务中缓存副本。
* **网络和带宽：** 共享文件夹中的文件和所有更新需要通过网络在系统之间传输。 您应确保仅共享相关文件和更新。
* **文件夹类型**: 共享类型的“资产” `sling:OrderedFolder`文件夹在Adobe Marketing Cloud中不受支持。 如果要共享文件夹，则在资产中创建文件夹时，请勿选择“已排序”选项。

## Best practices {#best-practices}

将Experience Manager用于Creative Cloud文件夹共享的最佳实践包括：

* **卷注意事项：** Experience Manager/Creative Cloud文件夹共享应用于共享较少数量的文件，例如，与特定活动或活动相关的文件。 要共享较大的资产集（与组织中所有已批准的资产一样），请使用其他分发方法（例如，资产品牌门户）或Experience Manager桌面应用程序。

* **避免共享深层层次：** 共享功能可循环使用，不允许选择性取消共享。 通常，仅应考虑使用没有子文件夹或层次结构非常浅的文件夹（如1个子文件夹级别）进行共享。
* **为单向共享单独使用文件夹：** 应使用单独的文件夹将最终资产从资产共享到Creative Cloud文件，以及将创意就绪型资产从Creative Cloud文件共享回资产。 它结合这些文件夹的良好命名规范，为Assets和Creative Cloud用户创建了一个更易于理解的工作环境。
* **避免在共享文件夹中出现WIP:** 共享文件夹不应用于进行中的工作——在Creative Cloud文件中使用单独的文件夹执行需要频繁更改文件的工作。
* **开始共享文件夹外的新工作：** 新设计（创意文件）应在Creative Cloud文件中的单独WIP文件夹中启动，当它们准备好与资产用户共享时，应将其移动或保存到共享文件夹中。
* **简化共享结构：** 要实现更易于管理的操作设置，请考虑简化共享结构。 资产文件夹应仅与团队代表共享，而不是与所有创意用户共享，如创意总监或团队经理。 创意方面的经理将接收最终资产，决定工作分配，然后让设计人员在自己的Creative Cloud帐户中处理WIP资产。 他们可以使用Creative Cloud协作功能来协调工作，最后选择并放回准备共享到资产的资产到他们的创意就绪共享文件夹。

下图说明了一个根据资产中现有最终资产创建新设计的示例配置。

![chlimage_1-180](assets/chlimage_1-407.png)
