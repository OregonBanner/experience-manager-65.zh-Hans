---
title: 交易报表概述
seo-title: Transaction Reports Overview
description: 记录已提交的所有表单、已渲染的交互式通信、已转换为另一种格式的文档及其他内容的计数
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 交易报表概述{#transaction-reports-overview}

## 简介 {#introduction}

通过AEM Forms中的交易报表，您可以对自AEM Forms部署中的指定日期以来发生的所有交易进行计数。 目标是提供有关产品使用情况的信息，并帮助业务利益相关者了解他们的数字处理量。 事务示例包括：

* 提交自适应表单、HTML5表单或表单集
* 交互式通信的打印或Web版本的演绎版
* 文档从一种文件格式转换为另一种文件格式

有关什么是事务的详细信息，请参见 [可记帐API](../../forms/using/transaction-reports-billable-apis.md).

默认情况下，事务记录处于禁用状态。 您可以 [启用事务记录](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 从AEM Web控制台。 您可以查看有关创作、处理或发布实例的事务报表。 查看有关所有事务汇总的创作或处理实例的事务报表。 查看发布实例上的事务报告，了解仅在该报告运行所在的发布实例上发生的所有事务的计数。

请勿在同一AEM实例上创作内容（创建自适应表单、交互式通信、主题和其他创作活动）和处理文档（使用工作流、文档服务和其他处理活动）。 对于用于创作内容的AEM Forms服务器，请保持禁用事务录制。 为用于处理文档的AEM Forms服务器保持启用事务记录。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

事务在缓冲区中保留指定的时间段（刷新缓冲区时间+反向复制时间）。 默认情况下，事务计数大约需要90秒才能反映在事务报表中。

提交PDF表单、使用代理UI预览交互式通信或使用非标准表单提交方法等操作不计为交易。 AEM Forms提供了一个API来记录此类交易。 从自定义实施中调用API以记录交易。

## 支持的拓扑 {#supported-topology}

事务报表仅在OSGi环境上的AEM Forms上可用。 它支持author-publish 、 author-processing-publish ，并且仅支持处理拓扑。 有关拓扑，请参阅 [AEM Forms的架构和部署拓扑](../../forms/using/transaction-reports-overview.md).

事务计数将从发布实例反向复制到创作实例或处理实例。 下面显示了指示性的作者 — 发布拓扑：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms事务报表不支持仅包含发布实例的拓扑。

### 使用交易报告的准则 {#guidelines-for-using-transaction-reports}

* 禁用所有创作实例上的事务报表，因为创作实例上的报表包含在创作活动期间注册的事务。
* 启用 **仅显示发布中的事务** 创作实例上的选项，用于查看所有发布实例的累积事务。 您还可以查看每个发布实例上的事务报告，了解仅特定发布实例上的实际事务。
* 请勿使用创作实例来运行工作流和处理文档。
* 在使用事务报表之前，如果您拥有发布服务器的拓扑，请确保为所有发布实例启用反向复制。
* 事务数据将从发布实例反向复制到仅相应的创作或处理实例。 创作或处理实例无法进一步将数据复制到另一个实例。 例如，如果您有author-processing-publish拓扑，则聚合的事务数据将仅复制到处理实例。

## 相关文章 {#related-articles}

* [查看和了解事务处理报表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [交易报告可记帐API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实施的交易](/help/forms/using/record-transaction-custom-implementation.md)
