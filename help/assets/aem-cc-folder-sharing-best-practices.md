---
title: AEM到Creative cloud文件夹，共享最佳实践
description: 配置Adobe Experience Manager(AEM)，以允许AEM资产中的用户与Adobe Creative Cloud(CC)用户交换文件夹。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# AEM到Creative cloud文件夹，共享最佳实践 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>已弃用“AEM到Creative cloud文件夹共享”功能。 Adobe强烈建议使用 [Adobe Asset Link或](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) AEM桌面应用程序 [](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)等更新的功能。 了解有关 [AEM和Creative cloud集成最佳实践的更多信息](/help/assets/aem-cc-integration-best-practices.md)。

可以将Adobe Experience Manager(AEM)配置为允许AEM资产中的用户与Adobe Creative cloud应用程序的用户共享文件夹，以便在Adobe Creative Cloud Assets服务中将它们作为共享文件夹提供。 此功能可用于在创意团队和AEM资产用户之间交换文件，尤其是当创意用户无权访问AEM资产实例（他们不在企业网络中）时。

此类集成可用于以下用例，尤其是与没有直接访问AEM资产的用户一起使用时：

* AEM Assets用户与Adobe Creative Cloud files用户共享一组特定资产（例如，为新营销活动进行设计而制作的创意简介和一组获准资产）
* AEM Assets用户将收到Adobe Creative cloud应用程序用户创建的新文件。

>[!NOTE]
>
>在阅读本文档之前，您可以查看整体 [AEM和Creative cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md) ，以获得主题的更高级别概述。

## 概述 {#overview}

AEM到Creative cloud文件夹的共享依赖于AEM资产和Creative cloud帐户之间的文件夹和文件的服务器端共享。 在桌面上使用Creative cloud桌面应用程序的创意专业人士还可以使用Adobe CreativeSync技术将共享文件夹直接放到其磁盘上。

下图提供了集成的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

集成包括以下元素：

* **AEM Assets服务器** （部署在企业网络中）（托管服务或内部部署）:此处启动文件夹共享。
* **Adobe Marketing Cloud Assets核心服务**:充当AEM和Creative cloud存储服务之间的中介。 使用集成的公司的管理员需要在Marketing cloud组织和AEM资产实例之间建立信任关系。 他们还定 [义了已批准的Creative cloud协作者列表](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html),AEM资产用户可以共享文件夹以提高安全性。

* **Creative Cloud Assets web服务** （存储和Creative Cloud Files Web UI）:这是特定Creative cloud应用程序用户（与其共享了AEM资产文件夹）能够接受邀请并查看其Creative cloud帐户存储中的文件夹的位置。
* **Creative cloud桌面应用程序**:（可选）允许通过与Creative Cloud Assets存储同步，从创意用户的桌面直接访问共享文件夹／文件。

## 特性和限制 {#characteristics-and-limitations}

* **** 更改的单向传播：文件更改仅向一个方向传播——从最初创建（上传）资产的系统（AEM或Creative Cloud Assets）传播。 该集成不提供两个系统之间的完全自动化的双向同步。
* **版本控制:**

   * 仅当文件源自AEM并在AEM中更新时，AEM才会在更新时创建资产的版本。
   * Creative Cloud Assets提供其自己的版 [本控制功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) ，该功能针对在创作品更新（基本上，将更新存储最多10天）

* **** 空间限制：交换的文件大小和数量受创意用户特定 [Creative Cloud Assets配额限制](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) （取决于订阅级别），最大文件大小限制为5 GB。 此外，组织在Adobe Marketing Cloud Assets核心服务中的资产配额也限制了空间。

* **** 空间要求：共享文件夹中的文件还需要先物理存储在AEM中，然后再存储在Creative cloud帐户中，并在Marketing Cloud Assets核心服务中缓存副本。
* **** 网络和带宽：共享文件夹中的文件和所有更新都需要通过网络在系统之间传输。 您应确保仅共享相关文件和更新。
* **文件夹类型**:在Adobe Marketing cloud中共享时， `sling:OrderedFolder`不支持共享类型的“资产”文件夹。 如果要共享文件夹，则在AEM资产中创建文件夹时，请勿选择“已排序”选项。

## Best practices {#best-practices}

将AEM用于Creative cloud文件夹共享的最佳实践包括：

* **** 卷注意事项：应使用AEM/Creative cloud文件夹共享来共享较少数量的文件，例如，与特定营销活动或活动相关的文件。 要共享较大的资产集（与组织中所有已批准的资产一样），请使用其他分发方法（例如，AEM Assets Brand Portal）或AEM桌面应用程序。

* **** 避免共享深层次：共享以递归方式工作，不允许选择性取消共享。 通常，只有没有子文件夹或层次结构非常浅的文件夹（如1个子文件夹级别）才应考虑共享。
* **** 单向共享的单独文件夹：应使用单独的文件夹将最终资产从AEM资产共享到Creative cloud文件，以及将创意就绪型资产从Creative cloud文件共享回AEM资产。 除了这些文件夹的良好命名规范外，它还为AEM Assets和Creative cloud用户创建了一个更易于理解的工作环境。
* **** 避免在共享文件夹中创建WIP:不应将共享文件夹用于进行中的作品——在Creative Cloud文件中使用单独的文件夹来执行需要频繁更改文件的工作。
* **** 在共享文件夹之外开始新工作：新设计（创意文件）应在Creative Cloud文件中的单独WIP文件夹中启动，当它们准备好与AEM资产用户共享时，应将其移动或保存到共享文件夹。
* **** 简化共享结构：要设置更易于管理的操作，请考虑简化共享结构。 与所有创意用户共享不同，AEM资产文件夹应仅与团队代表共享，如创意总监或团队经理。 创意部门的经理将收到最终资产，决定工作分配，然后让设计人员在自己的Creative cloud帐户中处理WIP资产。 他们可以使用Creative cloud协作功能来协调工作，最后选择准备好共享回AEM资产的资产并将其放入其可随时使用创意的共享文件夹。

下图说明了一个用于根据AEM资产中的现有最终资产创建新设计的示例配置。

![chlimage_1-180](assets/chlimage_1-407.png)
