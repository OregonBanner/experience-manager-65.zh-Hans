---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: 集成简介 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 468a8d96153c67232524eea6f180c9ceb364d60a
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] 集成 [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] 是一个工作管理应用程序，可帮助您在一个位置管理工作的整个生命周期。 集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 通过将工作与数字资产管理本质地联系在一起，让组织可以提高内容的快速性和上市时间。 在Workfront中管理其工作的上下文中，用户可以访问所需的文档和图像。

Adobe提供了两个不同的连接器来集成两个解决方案。 这些连接器在以下两个位置之间实现了复杂的企业自动化、配置和可扩展的工作流 [!DNL Assets] 和 [!DNL Workfront]. 此外， [!DNL Assets Essentials] 可作为新 [!DNL Workfront] 客户可以单独购买。 要了解更多信息，请参阅 [[!DNL Workfront] and [!DNL Assets Essentials] 集成](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/integration.html).

[!DNL Workfront for Experience Manage enhanced connector] 使贵组织能够：

* 轻松协作。 创意团队可以少担心一件事。 现在，完成工作后，他们只需单击按钮，即可将其发送到AEM Assets
* 在每一步都丰富资产。 在资产生命周期的每个阶段收集新数据。 从构思到交付，您的组织可以捕获关键量度，以便对未来资产开发做出更明智的业务决策。
* 引用现有资产。 轻松地在生产中查找和重复使用现有资产，并将其作为参考项目添加到新项目中。
* 同步所有元数据。 通过尽可能简化添加过程来增强元数据。 通过连接器，元数据在Workfront和AEM Assets之间双向同步
* 利用 [!DNL Experience Manager Assets] 数字管理功能。 直接在您喜爱的内容中访问所有数字资产 [!DNL Creative Cloud] 应用程序。 支持AI的智能标记和裁剪、搜索工具、通过动态交付 [!DNL Dynamic Media]，以及更多。

请参阅平台支持和其他 [enhanced connector先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署和配置时没有经过认证的合作伙伴或 [!DNL Adobe Professional Services]，则Adobe不支持此功能。
>
>Adobe可发布 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 这使得该连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。

## 比较 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是通过不同类型集成之间提供的功能的详细信息 [!DNL Assets] 和 [!DNL Workfront].

| 功能 | 描述 | [!DNL Workfront] 和 [!DNL Assets Essentials] | [!DNL Workfront] 表示 [!DNL Experience Manager] 连接器 | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| 部署方法 | 适用于 [!DNL Assets] 服务。 | Assets Essentials | Cloud Service, Adobe Managed Services，内部部署 | Cloud Service, Adobe Managed Services，内部部署 |
| 从发送数字文件 [!DNL Workfront] to [!DNL Assets] | WF文档的最新版本可以上传到AEM Assets，该版本将作为文档的新版本链接。 | ✓ | ✓ | ✓ |
| 手动将AEM文件夹关联到Workfront对象 | 现有的AEM文件夹可以作为Workfront文件夹进行链接，其子资产则作为新的Workfront文档进行链接。 | ✓ | ✓ | ✓ |
| 链接 [!DNL Assets] 到Workfront对象 | AEM中的现有资产可以链接到新的Workfront文档或作为现有文档的新版本。 | ✓ | ✓ | ✓ |
| 添加到链接文件夹的资产会自动发送到AEM | 如果文档被添加到链接的文件夹，则关联的资产会自动作为新资产上传到AEM Assets。 | ✓ | ✓ | ✓ |
| 从Workfront中下载链接的AEM Assets | 在Workfront中链接资产后，用户可以下载资产的字节。 | ✓ | ✓ | ✓ |
| 在Workfront中搜索AEM Assets | Workfront中的AEM Assets选择器允许对资产进行全文搜索。 | ✓ | ✓ | ✓ |
| 在Workfront中查看和导航AEM文件夹层次结构 | Workfront中的AEM Assets选择器允许浏览受用户在AEM中设置的关联访问控制和权限所限制的AEM Assets层次结构。 | ✓ | ✓ | ✓ |
| 在Workfront中取消资产与AEM Assets的关联 | 可以从关联的Workfront文档中取消链接来自AEM的现有链接资产。 这不会删除AEM内的原始资产。 | ✓ | ✓ | ✓ |
| 将新版本化的资产从Workfront添加到AEM Assets | 在Workfront中的文档中添加新添加的版本后，用户可以将新版本发送到AEM以替换现有版本。 | ✓ | ✓ | ✓ |
| 将用户直接单击到AEM时，Workfront中链接的资产 | 系统会将用户定向到AEM，以从Workfront中预览链接的资产。 | ✓ | ✓ | 自定义 |
| 在Workfront中自动创建链接的AEM文件夹 | 使用对象状态在Workfront中自动创建链接的AEM文件夹。 根据WorkfrontPortfolio、项目和项目自动组织AEM文件夹。 | 否 | 否 | ✓ |
| 评论同步 | 自动同步资产的注释 [!DNL Workfront] to [!DNL Assets] | 否 | ✓ | ✓ |
| 将Workfront资产元数据映射到AEM Assets | Workfront对象和自定义表单属性可以映射到AEM资产元数据属性。 值将在初始上载/链接时推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自动创建文档自定义Forms | 使用AEM工作流将自定义表单附加到Workfront文档、任务和问题。 | 否 | 手动添加自定义表单，然后自动同步可正常工作 | ✓ |
| AEM Assets与Workfront元数据的双向自动更新 | 自动更新AEM Assets和Workfront之间的元数据。 | 否 | ✓ | ✓ |
| 将Workfront元数据映射到AEM Assets文件夹 | 将Workfront项目元数据与关联的AEM文件夹同步。 | 否 | 否 | ✓ |
| AEM元数据更新了新版本 | 可以在AEM中进行配置，以确定Workfront中新版本化的资产是否还会推送对其元数据所做的任何更改。 | 否 | 否 | ✓ |
| 在更改Workfront中的自定义Forms时自动更新AEM元数据 | Workfront的配置，以便将指定的AEM资产元数据属性映射到文档自定义表单。 当初始链接资产或更新资产时，这些元数据属性的值会复制到相应的Workfront文档自定义表单字段。 必须谨慎防止从AEM所做的更改发送回AEM，就像它是源自Workfront的更改一样。 | 否 | ✓ | ✓ |
| 在链接的资产上创建新校样版本 | 在Workfront中关联资产时，可以自动生成校样。 | 否 | ✓ | 自定义 |
| 在Workfront对象上设置状态 | 使用AEM工作流设置基于Workfront对象状态的可配置条件 | 否 | 否 | ✓ |
| 将资产发布到AEM发布环境或Brand Portal | 为Workfront用户提供相应选项，以将链接的资产自动发布到AEM发布环境或Brand Portal。 | 否 | 否 | ✓ |
