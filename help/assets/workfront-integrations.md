---
title: '[!DNL Experience Manager Assets] 集成 [!DNL Adobe Workfront]'
description: 集成简介 [!DNL Assets] 和 [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] 集成 [!DNL Adobe Workfront] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Workfront] 是一个工作管理应用程序，它帮助您集中在一处管理工作的整个生命周期。集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 通过将工作与数字资产管理本质地联系在一起，让组织可以提高内容的快速性和上市时间。 在Workfront中管理其工作的范围内，用户可以访问所需的文档和图像。

的 [!DNL Workfront for Experience Manager enhanced connector] 通过端到端工作流支持增强的业务流程，并提供个性化的端到端客户体验和中央存储。 Adobe提供标准连接器和增强的连接器，以集成这两个解决方案。 请参阅下面支持的功能以进行比较，并参阅 [的新增功能 [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] 使贵组织能够：

* 在Workfront中自动创建链接的Experience Manager文件夹，并根据WorkfrontPortfolio、项目和项目来组织文件夹。
* 将Workfront项目元数据与链接的Experience Manager文件夹同步。
* Experience Manager元数据会随新版本而更新。
* 使用Workfront工作流根据可配置条件设置Experience Manager对象状态。
* 将资产发布到Experience Manager发布环境或Brand Portal。

查看平台支持和 [enhanced connector先决条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署和配置时没有经过认证的合作伙伴或 [!DNL Adobe Professional Services]，则Adobe不支持此功能。
>
>* Adobe可发布 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强的连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请导航到 `digital.hoodoo` 组在 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans).
>
>* 请参阅 [Workfront的Experience Manager Assets增强连接器合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参阅 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 比较 [!DNL Assets] 和 [!DNL Workfront] {#feature-parity-matrix}

以下是通过不同类型集成之间提供的功能的详细信息 [!DNL Assets] 和 [!DNL Workfront].

| 专题 | 描述 | [!DNL Workfront] 和 [!DNL Assets Essentials] *无连接器(OOTB)* | [!DNL Workfront for Experience Manager enhanced connector] *需要连接器* | Workfront和 [!DNL Experience Manager as a Cloud Service] *无连接器(OOTB)* |
|----|----|----|-----|-----|
| 部署方法 | 适用于 [!DNL Assets] 服务。 | Assets Essentials | Adobe Managed Services，内部部署 | 云服务 |
| **常规** |
| 从发送数字文件 [!DNL Workfront] to [!DNL Assets] | WF文档的最新版本可以上传到AEM Assets，该版本将作为文档的新版本链接。 | ✓ | ✓ | ✓ |
| 手动将AEM文件夹关联到Workfront对象 | 现有的AEM文件夹可以作为Workfront文件夹进行链接，其子资产则作为新的Workfront文档进行链接。 | ✓ | ✓ | ✓ |
| 链接 [!DNL Assets] 到Workfront对象 | AEM中的现有资产可以链接到新的Workfront文档或作为现有文档的新版本。 | ✓ | ✓ | ✓ |
| 添加到链接文件夹的资产会自动发送到AEM | 如果文档被添加到链接的文件夹，则关联的资产会自动作为新资产上传到AEM Assets。 | ✓ | ✓ | ✓ |
| 从Workfront中下载链接的AEM Assets | 在Workfront中链接资产后，用户可以下载资产的字节。 | ✓ | ✓ | ✓ |
| 在Workfront中搜索AEM Assets | Workfront中的AEM Assets选择器允许对资产进行全文搜索。 | ✓ | ✓ | ✓ |
| 在Workfront中搜索AEM文件夹 | Workfront中的AEM Assets选择器允许对文件夹进行全文搜索。 | ✓ | ✓ | ✓ |
| 在Workfront中查看和导航AEM文件夹层次结构 | Workfront中的AEM Assets选择器允许浏览受用户在AEM中设置的关联访问控制和权限所限制的AEM Assets层次结构。 | ✓ | ✓ | ✓ |
| 在AEM时间轴中跟踪资产版本 | 在Workfront和AEM之间维护文档版本历史记录。 | ✓ | ✓ | ✓ |
| 在Workfront中取消资产与AEM Assets的关联 | 可以从关联的Workfront文档中取消链接来自AEM的现有链接资产。 这不会删除AEM内的原始资产。 | ✓ | ✓ | ✓ |
| 将新版本化的资产从Workfront添加到AEM Assets | 在Workfront中的文档中添加新添加的版本后，用户可以将新版本发送到AEM以替换现有版本。 | ✓ | ✓ | ✓ |
| 将用户直接单击到AEM时，Workfront中链接的资产 | 系统会将用户定向到AEM，以从Workfront中预览链接的资产。 | ✓ | ✓ | 即将推出 |
| 在Workfront中自动创建链接的AEM文件夹 | 使用项目状态在Workfront中自动创建链接的AEM文件夹。 根据“WorkfrontPortfolio”、“程序”和“项目”自动配置AEM文件夹。 | 否 | ✓ | 否 |
| 直接从Workfront导航到AEM存储库 | 允许用户导航到在Workfront中配置的可用AEM存储库。 | ✓ | 否 | ✓ |
| 在Workfront中创建链接的AEM文件夹 | 使用“文档”选项卡中的选项在Workfront中手动创建链接的AEM文件夹。 | ✓ | 否 | ✓ |
| 评论同步 | 自动同步资产的注释 [!DNL Workfront] to [!DNL Assets] | 否 | ✓ | 否 |
| 支持连接到单个AEM环境的多个Workfront环境 | 来自多个Workfront环境的用户可以连接到单个AEM环境。 | ✓ | 否 | ✓ |
| 支持多个AEM环境连接到单个Workfront环境 | 单个Workfront环境中的用户可以在多个AEM环境之间发送或链接资产。 | ✓ | ✓ | ✓ |
| **元数据** |
| 将Workfront资产元数据映射到AEM Assets | Workfront对象和自定义表单属性可以映射到AEM资产元数据属性。 值将在初始上载/链接时推送。 | ✓ | ✓ | ✓ |
| 在Workfront中自动创建文档自定义Forms | 使用AEM工作流将自定义表单附加到Workfront文档、任务和问题。 | 否 | ✓ | 否 |
| AEM Assets与Workfront元数据的双向自动更新 | 自动更新AEM Assets和Workfront之间的元数据。 资产最初必须从Workfront推送到AEM，并且Workfront资产元数据必须映射到AEM资产，才能正确进行双向元数据更新。 | 否 | ✓ | 否 |
| Workfront中用于将元数据映射到AEM的实时视图 | 在“Workfront文档详细信息”和“文档摘要”面板中查看已更新映射到AEM的元数据。 | ✓ | 否 | ✓ |
| 将更新的Workfront元数据实时推送到AEM | 自动将映射的Workfront元数据更新到AEM，而无需重新推送资产或资产的新版本。 | ✓ | 否 | ✓ |
| 将Workfront元数据映射到AEM Assets文件夹 | 将Workfront项目元数据与关联的AEM文件夹同步。 | 否 | ✓ | ✓ |
| AEM元数据更新了新版本 | 可以在AEM中进行配置，以确定Workfront中新版本化的资产是否还会推送对其元数据所做的任何更改。 | 否 | ✓ | 否 |
| 在更改Workfront中的自定义Forms时自动更新AEM元数据 | AEM允许您订阅Workfront中文档表单的更新。 因此，对Workfront文档自定义表单元数据的任何更新都会修改映射的AEM元数据字段的值。 | 否 | ✓ | 否 |
| **工作流（现成）** |
| 在链接的资产上创建新校样版本 | 在Workfront中关联资产时，可以自动生成校样。 | 否 | 自定义 | 否 |
| 在Workfront对象上设置状态 | 使用AEM工作流设置基于Workfront对象状态的可配置条件 | 否 | ✓ | 即将推出 |
| 将资产发布到AEM发布环境或Brand Portal | 为Workfront用户提供相应选项，以将链接的资产自动发布到AEM发布环境或Brand Portal。 | 否 | ✓ | 即将推出 |
