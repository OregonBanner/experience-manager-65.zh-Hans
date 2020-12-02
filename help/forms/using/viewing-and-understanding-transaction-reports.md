---
title: 查看和了解事务处理报表
seo-title: 查看和了解事务处理报表
description: 使用事务报表对产品使用情况做出明智决策并重新平衡硬件和软件投资。
seo-description: 使用事务报表对产品使用情况做出明智决策并重新平衡硬件和软件投资。
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 4ee3b99a3f0a5d37441eee76c3ec747afcf2e32e
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---


# 查看和了解事务报表{#viewing-and-understanding-transaction-reports}

事务报表允许您捕获和跟踪已提交表单、已处理文档和呈现文档的数量。 跟踪这些交易的目标是对产品使用情况做出明智决策，并重新平衡硬件和软件投资。 有关详细信息，请参阅[AEM Forms事务报告概述](../../forms/using/transaction-reports-overview.md)。

## 设置事务报告{#setting-up-transaction-reports}

事务报表功能是AEM forms add-on包的一部分。 有关在所有作者实例和发布实例上安装加载项包的信息，请参阅[安装和配置AEM forms](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安装AEM forms加载项包后，请执行以下操作：

* 在所有发布实例上启用反向复制
* 启用事务报表
* 提供视图事务报表的权限
* （可选）配置事务处理刷新周期和出货箱[](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms事务报表不支持仅包含发布实例的拓扑。
>* 在使用事务报告之前，请确保对所有发布实例启用反向复制。
>* 事务数据从发布实例反向复制到仅对应的作者或处理实例。 作者或处理实例无法进一步将数据复制到另一个实例。

>



### 对所有发布实例{#enable-reverse-replication-on-all-the-publish-instances}启用反向复制

事务报表使用反向复制来合并从发布实例到作者实例的事务计数。 在所有发布实例上设置反向复制。 有关设置反向复制的详细说明，请参见[replication](/help/sites-deploying/replication.md)。

### 启用事务报表{#enable-transaction-reports}

默认情况下，事务报表处于禁用状态。 您可以从AEM Web Console启用报告。 要在AEM Forms环境中启用事务报表，请对所有作者和发布实例执行以下步骤：

1. 以管理员身份登录到AEM实例。 转至&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务报告**&#x200B;服务。
1. 选中记录事务复选框。 单击&#x200B;**保存**。

   对所有作者实例和发布实例重复步骤1-3。

### 提供视图事务报告{#provide-rights-to-view-a-transaction-report}的权限

只有fd-administrator组的成员才能视图事务报表。 要允许用户视图事务报表，请使用户成为fd-administrator组的成员。 有关使用户成为AEM组成员的说明，请参阅[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### （可选）配置事务处理刷新周期和出货箱{#optional-configure-transaction-flush-period-and-outboxes}

事务在存储到存储库之前在内存中缓存。 默认情况下，缓存期间（事务刷新期间）设置为60秒。 请执行以下步骤以更改默认缓存期：

1. 以管理员身份登录以创作实例。 转至&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务库存储提供程序**&#x200B;服务。
1. 在&#x200B;**事务刷新周期**&#x200B;字段中指定秒数。 单击&#x200B;**保存**。

反向复制将事务数据复制到作者实例的默认输出框。 您可以将事务数据放在自定义输出框中。 请执行以下步骤以指定自定义输出框：

1. 以管理员身份登录以创作实例。 转至&#x200B;**工具** > **操作** > **Web控制台**。
1. 找到并打开&#x200B;**Forms事务库存储提供程序**&#x200B;服务。
1. 在&#x200B;**发件箱**&#x200B;字段中指定自定义发件箱的名称。 单击&#x200B;**保存**。将在所有作者实例上创建具有指定名称的输出框。

## 查看事务报告{#viewing-the-transaction-report}

您可以视图创作或发布实例的事务报表。 创作实例上的事务报表提供在已配置的作者实例和发布实例上发生的所有事务的汇总。 发布实例上的事务报表提供仅在基础发布实例上发生的事务计数。 执行以下步骤来视图报表：

1. 登录到位于`https://[hostname]:'port'`的AEM Forms服务器。
1. 导航到&#x200B;**工具** > **Forms**>**视图事务报表**。

## 了解报告{#understanding-the-report}

AEM Forms显示自配置日期起的事务处理报表，如以下摘要报表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用&#x200B;**将日期重置为今天**&#x200B;选项重置事务记录。 将日期重置为今天时，将丢失所有以前的交易记录。 在创作实例上重置日期时，所做的更改不会影响发布实例上的事务报表，反之也不会影响该事务报表。
* 使用&#x200B;**仅显示发布实例的事务**&#x200B;可视图仅在配置的发布实例或发布场上发生的所有事务。
* 使用类别:**已处理文档**、**已呈现文档**&#x200B;和&#x200B;**Forms已提交到视图相应事务。**&#x200B;有关这些类别中记录的事务处理类型，请参阅[可开单事务处理报表API](../../forms/using/transaction-reports-billable-apis.md)。

## 视图事务报告日志{#view-transaction-reporting-logs}

事务报告将报告中显示的所有信息和日志中的其他一些信息放在一起。 日志中提供的信息对高级用户很有帮助。 例如，日志将事务划分为多个粒度类别，而报告中显示的三个统一类别则不同。 日志位于`/crx-repository/logs/`目录的`error.log`文件中。 日志可用，即使您未从AEM Web Console启用事务报表也是如此。

## 相关文章{#related-articles}

* [事务处理报表概览](../../forms/using/transaction-reports-overview.md)
* [事务处理报表可计费API](../../forms/using/transaction-reports-billable-apis.md)
* [记录自定义实现的事务](/help/forms/using/record-transaction-custom-implementation.md)

