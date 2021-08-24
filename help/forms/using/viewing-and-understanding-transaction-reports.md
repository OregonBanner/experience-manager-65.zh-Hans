---
title: 查看和了解交易报表
seo-title: 查看和了解交易报表
description: 使用事务报表对产品使用情况做出明智决策，并重新平衡硬件和软件方面的投资。
seo-description: 使用事务报表对产品使用情况做出明智决策，并重新平衡硬件和软件方面的投资。
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# 查看和了解交易报表{#viewing-and-understanding-transaction-reports}

利用交易报表，可捕获和跟踪已提交的表单、已处理文档和已渲染文档的数量。 跟踪这些交易的目标是对产品使用情况做出明智决策，并重新平衡对硬件和软件的投资。 有关更多信息，请参阅[AEM Forms事务报表概述](../../forms/using/transaction-reports-overview.md)。

## 设置事务报表  {#setting-up-transaction-reports}

交易报表功能作为AEM Forms附加组件包的一部分提供。 有关在所有创作实例和发布实例上安装附加组件包的信息，请参阅[安装和配置AEM表单](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安装AEM Forms附加组件包后，请执行以下操作：

* 在所有发布实例上启用反向复制
* 启用事务报表
* 提供查看交易报表的权限
* （可选）配置事务刷新时段和发件箱[](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms事务报表不支持仅包含发布实例的拓扑。
>* 在使用事务报告之前，请确保为所有发布实例启用了反向复制。
>* 事务数据会从发布实例反向复制到仅对应的创作或处理实例。 创作或处理实例无法进一步将数据复制到其他实例。

>



### 在所有发布实例上启用反向复制 {#enable-reverse-replication-on-all-the-publish-instances}

事务报表使用反向复制来整合从发布实例到创作实例的事务计数。 在所有发布实例上设置反向复制。 有关设置反向复制的详细说明，请参阅[replication](/help/sites-deploying/replication.md)。

### 启用事务报表 {#enable-transaction-reports}

默认情况下，交易报表处于禁用状态。 您可以从AEM Web Console中启用报表。 要在AEM Forms环境中启用事务报表，请对所有创作实例和发布实例执行以下步骤：

1. 以管理员身份登录AEM实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms Transaction Reporting**&#x200B;服务。
1. 选中“记录事务处理”复选框。 单击&#x200B;**保存**。

   对所有创作实例和发布实例重复步骤1-3。

### 提供查看交易报表的权限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator组的成员才能查看事务报表。 要允许用户查看事务报表，请使用户成为fd-administrator组的成员。 有关将用户设为AEM组成员的说明，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### （可选）配置事务刷新时段和发件箱 {#optional-configure-transaction-flush-period-and-outboxes}

事务在存储到存储库中之前，会先缓存在内存中。 按照此过程可确保不会频繁写入存储库。 默认情况下，缓存时段（事务刷新时段）设置为60秒。 您可以更改默认期限以适合您的环境。 执行以下步骤以更改默认缓存期：

1. 以管理员身份登录创作实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务存储库存储提供程序**&#x200B;服务。
1. 在&#x200B;**事务刷新时段**&#x200B;字段中指定秒数。 单击&#x200B;**保存**。

反向复制将事务数据复制到创作实例的默认发件箱。 您可以将交易数据放入自定义发件箱中。 执行以下步骤以指定自定义发件箱：

1. 以管理员身份登录创作实例。 转到&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务存储库存储提供程序**&#x200B;服务。
1. 在&#x200B;**发件箱**&#x200B;字段中指定自定义发件箱的名称。 单击&#x200B;**保存**。将在所有创作实例上创建具有指定名称的发件箱。

## 查看交易报表 {#viewing-the-transaction-report}

您可以查看有关创作或发布实例的事务报表。 关于创作实例的事务报表提供了在配置的创作实例和发布实例中发生的所有事务的汇总。 发布实例上的事务报表提供了仅在基础发布实例上发生的事务计数。 执行以下步骤以查看报表：

1. 登录到位于`https://[hostname]:'port'`的AEM Forms服务器。
1. 导航到&#x200B;**工具** > **Forms**>**查看事务报表**。

## 了解报表 {#understanding-the-report}

AEM Forms显示自配置日期以来的交易报表，如以下摘要报表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用&#x200B;**将日期重置为今天**&#x200B;选项重置事务记录。 将日期重置为今天时，所有以前的交易记录都将丢失。 在创作实例上重置日期时，所做的更改不会影响发布实例上的事务报表，反之也不会影响发布实例上的事务报表。
* 使用&#x200B;**仅显示发布实例的事务**&#x200B;可查看仅在配置的发布实例或发布场上发生的所有事务。
* 使用类别：**已处理的文档**、**已呈现的文档**&#x200B;和&#x200B;**Forms Submitted**&#x200B;以查看相应事务。 有关这些类别中入帐的事务处理类型，请参阅[计费事务处理报表API](../../forms/using/transaction-reports-billable-apis.md)。

## 查看事务报告日志 {#view-transaction-reporting-logs}

事务报表会将报告中显示的所有信息以及一些其他信息置于日志中。 日志中提供的信息对高级用户很有帮助。 例如，日志将事务划分为多个粒度类别，而不是报表中显示的三个合并类别。 日志位于`/crx-repository/logs/`目录的`error.log`文件中。 即使您未从AEM Web Console中启用事务报表，日志也可用。

## 相关文章 {#related-articles}

* [交易报表概述](../../forms/using/transaction-reports-overview.md)
* [交易报表计费API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实施的交易](/help/forms/using/record-transaction-custom-implementation.md)
