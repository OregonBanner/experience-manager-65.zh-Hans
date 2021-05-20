---
title: 交易报表概述
seo-title: 交易报表概述
description: 保留提交的所有表单、交互式通信渲染、转换为一种格式的文档，等等
seo-description: 保留提交的所有表单、交互式通信渲染、转换为一种格式的文档，等等
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 事务报表概述{#transaction-reports-overview}

## 简介 {#introduction}

利用AEM Forms中的事务报表，可统计自AEM Forms部署中指定日期以来发生的所有事务。 其目标是提供有关产品使用情况的信息，并帮助业务利益相关方了解其数字处理量。 交易示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印版或Web版的再现
* 将文档从一种文件格式转换为另一种文件格式

有关被视为交易的详细信息，请参阅[计费API](../../forms/using/transaction-reports-billable-apis.md)。

默认情况下，事务记录处于禁用状态。 您可以从AEM Web控制台中[启用事务记录](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports)。 您可以查看有关创作、处理或发布实例的事务报表。 查看所有交易汇总的作者或处理实例的交易报表。 查看发布实例上的事务报表，了解仅在运行报表的发布实例上发生的所有事务的计数。

请勿在同一AEM实例上创作内容（创建自适应表单、交互式通信、主题和其他创作活动）和处理文档（使用工作流、文档服务和其他处理活动）。 对于用于创作内容的AEM Forms服务器，请禁用交易记录。 为用于处理文档的AEM Forms服务器启用事务记录。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

事务在指定时段（刷新缓冲时间+反向复制时间）内保留在缓冲区中。 默认情况下，交易计数大约需要90秒才能反映在交易报表中。

诸如提交PDF表单、使用代理UI预览交互式通信或使用非标准表单提交方法之类的操作不会计为交易。 AEM Forms提供了用于记录此类交易的API。 从自定义实施中调用API以记录交易。

## 支持的拓扑{#supported-topology}

交易报表仅在OSGi环境的AEM Forms上可用。 它支持创作发布、创作处理发布以及仅处理拓扑。 例如，请参阅[AEM Forms](../../forms/using/transaction-reports-overview.md)的架构和部署拓扑。

事务计数会从发布实例反向复制到创作实例或处理实例。 下面显示了一个指示性的作者发布拓扑：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms事务报表不支持仅包含发布实例的拓扑。

### 使用事务报表{#guidelines-for-using-transaction-reports}的准则

* 禁用所有创作实例的事务报表，因为创作实例的报表包括在创作活动期间注册的事务。
* 在创作实例上启用&#x200B;**仅显示发布事务**&#x200B;选项，以查看所有发布实例的累积事务。 您还可以仅查看每个发布实例的事务报表，以查看该特定发布实例的实际事务报表。
* 请勿使用创作实例来运行工作流和处理文档。
* 在使用事务报告之前，如果您具有包含发布服务器的主题，请确保为所有发布实例启用了反向复制。
* 事务数据会从发布实例反向复制到仅对应的创作或处理实例。 创作或处理实例无法进一步将数据复制到其他实例。 例如，如果您具有创作处理 — 发布拓扑，则聚合事务数据将仅复制到处理实例。

## 相关文章{#related-articles}

* [查看和了解交易报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [交易报表计费API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实施的交易](/help/forms/using/record-transaction-custom-implementation.md)
