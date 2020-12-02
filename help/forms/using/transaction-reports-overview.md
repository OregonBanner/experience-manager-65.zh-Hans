---
title: 事务处理报表概览
seo-title: 事务处理报表概览
description: 记住所有提交的表单、呈现的交互式通信、转换为一种格式的文档，以及更多
seo-description: 记住所有提交的表单、呈现的交互式通信、转换为一种格式的文档，以及更多
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---


# 事务报表概述{#transaction-reports-overview}

## 简介 {#introduction}

在AEM Forms，事务报表允许您对自指定日期以来在AEM Forms部署时发生的所有事务进行计数。 其目标是提供有关产品使用情况的信息，并帮助业务相关人员了解其数字处理量。 事务处理的示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印版或Web版的再现
* 将文档从一种文件格式转换为另一种格式

有关被视为事务的详细信息，请参阅[可计费API](../../forms/using/transaction-reports-billable-apis.md)。

默认情况下，事务记录处于禁用状态。 您可以从AEM Web Console[启用事务记录](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports)。 您可以视图有关作者、处理或发布实例的事务报表。 视图事务处理报告所有事务处理的合计的作者或处理实例。 视图事务处理报告发布实例中仅在运行报告的发布实例上发生的所有事务处理的计数。

请勿在同一文档实例上创作内容(创建自适应表单、交互式通信、主题和其他创作活动)和处理AEM(使用工作流、文档服务和其他处理活动)。 对于用于创作内容的AEM Forms服务器，请禁用事务记录。 为用于处理文档的AEM Forms服务器启用事务记录。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

在指定的时间段内，事务将保留在缓冲区中（刷新缓冲时间+反向复制时间）。 默认情况下，事务计数大约需要90秒才能反映在事务报表中。

诸如提交PDF表单、使用代理UI预览交互式通信或使用非标准表单提交方法等操作不作为事务处理入账。 AEM Forms提供API记录此类交易。 从您的自定义实现调用API以记录事务。

## 支持的拓扑{#supported-topology}

事务报表仅在OSGi环境的AEM Forms上可用。 它支持作者发布、作者处理发布和仅处理拓扑。 例如，请参见[AEM Forms](../../forms/using/transaction-reports-overview.md)的架构和部署拓扑。

事务计数从发布实例反向复制到作者实例或处理实例。 指示性的作者发布拓扑如下所示：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms事务报表不支持仅包含发布实例的拓扑。

### 使用事务报表{#guidelines-for-using-transaction-reports}的准则

* 禁用所有作者实例的事务报表，因为作者实例的报表包括在创作活动中注册的事务。
* 在作者实例上启用&#x200B;**仅显示发布事务**&#x200B;选项，以视图所有发布实例的累积事务。 您还可以视图每个发布实例上的事务报表，以便仅针对该特定发布实例上的实际事务。
* 请勿使用作者实例运行工作流和处理文档。
* 在使用事务报告之前，如果您具有发布服务器的主题，请确保对所有发布实例启用反向复制。
* 事务数据从发布实例反向复制到仅对应的作者或处理实例。 作者或处理实例无法进一步将数据复制到另一个实例。 例如，如果您具有作者处理——发布拓扑，则聚合事务数据仅复制到处理实例。

## 相关文章{#related-articles}

* [查看和了解事务处理报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [事务处理报表可计费API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实现的事务](/help/forms/using/record-transaction-custom-implementation.md)

