---
title: 查看和了解事务处理报表
seo-title: 查看和了解事务处理报表
description: 使用交易报告对产品使用情况做出明智决策并重新平衡硬件和软件方面的投资。
seo-description: 使用交易报告对产品使用情况做出明智决策并重新平衡硬件和软件方面的投资。
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# 查看和了解事务处理报表{#viewing-and-understanding-transaction-reports}

交易报表允许您捕获和跟踪已提交的表单、已处理文档和已渲染文档的数量。 跟踪这些交易的目标是对产品使用情况做出明智决策，并重新平衡硬件和软件投资。 有关详细信息，请参 [阅AEM Forms Transaction Reports概述](../../forms/using/transaction-reports-overview.md)。

## 设置事务处理报告 {#setting-up-transaction-reports}

事务报表功能可作为AEM表单加载项包的一部分提供。 有关在所有作者实例和发布实例上安装加载项包的信息，请参 [阅安装和配置AEM表单](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安装AEM Forms Add-on包后，请执行以下操作：

* 在所有发布实例上启用反向复制
* 启用事务报表
* 提供查看事务报告的权限
* （可选）配置事务处理刷新期间和出货箱 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms事务报表不支持仅包含发布实例的拓扑。
>* 在使用事务报告之前，请确保对所有发布实例启用反向复制。
>* 事务数据从发布实例反向复制到仅对应的作者或处理实例。 作者或处理实例无法进一步将数据复制到另一个实例。
>



### 在所有发布实例上启用反向复制 {#enable-reverse-replication-on-all-the-publish-instances}

事务报表使用反向复制来合并从发布实例到作者实例的事务计数。 在所有发布实例上设置反向复制。 有关设置反向复制的详细说明，请参 [阅复制](/help/sites-deploying/replication.md)。

### 启用事务报表 {#enable-transaction-reports}

默认情况下，事务报表处于禁用状态。 您可以从AEM Web Console中启用报告。 要在AEM Forms环境中启用事务报表，请对所有作者和发布实例执行以下步骤：

1. 以管理员身份登录到AEM实例。 转到工 **具** >操 **作** > **Web控制台**。
1. 找到并打开 **Forms Transaction Reporting服务** 。
1. 选中“记录事务处理”复选框。 单击&#x200B;**保存**。

   对所有作者实例和发布实例重复第1-3步。

### 提供查看事务报告的权限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator组的成员才能查看事务报告。 要允许用户查看事务报告，请使用户成为fd-administrator组的成员。 有关使用户成为AEM组的成员的说明，请参阅用 [户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### （可选）配置事务处理刷新期间和出货箱 {#optional-configure-transaction-flush-period-and-outboxes}

事务在被存储到存储库之前在内存中缓存。 默认情况下，缓存期（事务刷新期）设置为60秒。 请执行以下步骤以更改默认缓存期：

1. 以管理员身份登录以创作实例。 转到工 **具** >操 **作** > **Web控制台**。
1. 找到并打开表 **单事务存储库存储提供程序** 。
1. 在“事务处理刷新期间”字 **段中指定秒数** 。 单击&#x200B;**保存**。

反向复制会将事务数据复制到作者实例的默认外框。 您可以将事务数据放入自定义外框中。 执行以下步骤以指定自定义输出框：

1. 以管理员身份登录以创作实例。 转到工 **具** >操 **作** > **Web控制台**。
1. 找到并打开表 **单事务存储库存储提供程序** 。
1. 在“发件箱”字段中指定自定义发件 **箱的名** 称。 单击&#x200B;**保存**。将在所有作者实例上创建具有指定名称的发件箱。

## 查看事务处理报告 {#viewing-the-transaction-report}

您可以查看有关作者实例或发布实例的事务报告。 作者实例的事务报表提供在配置的作者实例和发布实例上发生的所有事务的汇总总和。 发布实例上的事务报表提供仅在基础发布实例上发生的事务计数。 执行以下步骤查看报告：

1. 登录到AEM Forms服务器，网址为 `https://[hostname]:[port]`。
1. 导航到工 **具** >表 **单**>查看事务报表&#x200B;****。

## 了解报告 {#understanding-the-report}

AEM Forms显示自配置日期起的事务处理报表，如下面的摘要报表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用“ **将日期重置为今天** ”选项重置事务记录。 将日期重置为今天时，将丢失所有以前的交易记录。 在创作实例上重置日期时，所做的更改不会影响发布实例上的事务报表，反之也不会影响发布实例上的事务报表。
* 使用仅 **显示发布实例的事务** ，查看仅在配置的发布实例或发布农场上发生的所有事务。
* 使用类别：“已 **处理的文档**”、“已 **呈现的文档**”和“已 **提交的表单** ”，以查看相应的事务处理。 有关这些类别中入账的事务处理类型，请参阅“可 [开单事务处理报表”API](../../forms/using/transaction-reports-billable-apis.md)。

## 查看事务报告日志 {#view-transaction-reporting-logs}

事务报告会将报告中显示的所有信息和一些其他信息放在日志中。 日志中提供的信息对高级用户很有帮助。 例如，日志将事务划分为多个粒度类别，与报表中显示的三个统一类别相比。 日志位于/crx-quickstart/logs/aem-forms-transaction.log。

## 相关文章 {#related-articles}

* [事务处理报告概述](../../forms/using/transaction-reports-overview.md)
* [事务处理报告可开单API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实现的事务](/help/forms/using/record-transaction-custom-implementation.md)

