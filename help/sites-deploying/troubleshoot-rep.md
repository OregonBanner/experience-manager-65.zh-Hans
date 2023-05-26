---
title: 复制疑难解答
seo-title: Troubleshooting Replication
description: 本文介绍如何解决复制问题。
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# 复制疑难解答{#troubleshooting-replication}

本页提供了有关如何解决复制问题的信息。

## 问题 {#problem}

由于某种原因，复制（非反向复制）失败。

## 解决方法 {#resolution}

复制失败的原因有很多。 本文解释了分析这些问题时可能需要采用的方法。

**单击“激活”按钮后是否还会触发复制？ 如果为NOT，则执行以下操作：**

1. 转到/crx/explorer并以管理员身份登录。
1. 打开“内容资源管理器”
1. 查看节点/bin/replicate或/bin/replicate.json是否存在。 如果节点存在，则删除它并保存。

**复制是否在复制代理队列中排队？**

转到/etc/replication/agents.author.html进行检查，然后单击要检查的复制代理。

**如果一个代理队列或几个代理队列卡住：**

1. 队列是否显示 **已阻止** 状态？ 如果是这样，那么发布实例是否未运行或完全无响应？ 检查发布实例以查看其错误（即，检查日志，并查看是否存在OutOfMemory错误或某些其他问题）。 然后，如果速度通常较慢，则进行线程转储并分析它们。
1. 是否显示队列状态 **队列处于活动状态 — #个待处理**？ 基本上，复制作业可能会卡在套接字读取中，等待发布实例或Dispatcher响应。 这可能意味着发布实例或Dispatcher处于高负载下或卡在锁中。 在本例中，从作者处进行线程转储并发布。

   * 在线程转储分析器中打开来自作者的线程转储，检查它是否显示复制代理的sling事件作业卡在socketRead中。
   * 在线程转储分析器中从发布中打开线程转储，分析可能导致发布实例不响应的原因。 您应该会看到其名称中包含POST/bin/receive的线程，即从author接收复制的线程。

**如果所有代理队列都卡住**

1. 可能由于存储库损坏或某些其他问题，无法在/var/replication/data下序列化特定内容。 查看logs/error.log以了解相关错误。 要清除错误的复制项目，请执行以下操作：

   1. 转到https://&lt;host>：&lt;port>/crx/de并以管理员用户身份登录。
   1. 单击顶部菜单中的“工具”。
   1. 单击“放大镜”按钮。
   1. 选择“XPath”作为“类型”。
   1. 在“查询”框中，输入此查询/jcr：root/var/eventing/jobs//element(&#42;，slingevent：Job)按@slingevent：created排序
   1. 单击“搜索”
   1. 在结果中，排名最前的项目是最新的Sling事件作业。 单击每个复制并查找与队列顶部显示的内容匹配的停滞复制。

1. sling事件框架作业队列可能出错。 尝试在/system/console中重新启动org.apache.sling.event捆绑包。
1. 可能是作业处理已完全关闭。 您可以在Sling事件选项卡的Felix控制台下检查这一点。 检查是否显示 — Apache Sling事件（作业处理已禁用！）

   * 如果为“是”，请检查Felix控制台的“配置”选项卡下的“Apache Sling作业事件处理程序”。 可能未选中“作业处理已启用”复选框。 如果选中了此复选框，但仍显示“作业处理已禁用”，则检查/apps/system/config下是否存在正在禁用作业处理的覆盖。 尝试为jobmanager.enabled创建一个osgi：config节点，其布尔值为true，并重新检查激活是否开始以及队列中是否没有更多作业。

1. DefaultJobManager配置也可能处于不一致状态。 当有人通过OSGiconsole手动修改“Apache Sling作业事件处理程序”配置（例如，禁用并重新启用“作业处理已启用”属性并保存配置）时，可能会发生此情况。

   * 此时，存储在crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config中的DefaultJobManager配置进入不一致状态。 即使“Apache Sling Job Event Handler”属性显示“作业处理已启用”处于选中状态，当导航到“Sling事件”选项卡时，它会显示消息 — JOB PROCESSING IS DISABLED ，并且复制不起作用。
   * 要解决此问题，需要导航到OSGi控制台的配置页面并删除“Apache Sling作业事件处理程序”配置。 然后，重新启动群集的主控节点，使配置返回到一致状态。 这应该可以修复此问题，并且复制将重新开始工作。

**创建replication.log**

有时，在DEBUG级别将所有复制日志记录添加到单独的日志文件中会非常有用。 要执行此操作：

1. 前往https://host:port/system/console/configMgr并以管理员身份登录。
1. 找到Apache Sling日志记录器工厂，并通过单击 **+** 按钮。 这将创建一个新的日志记录器。
1. 设置配置，如下所示：

   * 日志级别： DEBUG
   * 日志文件路径： logs/replication.log
   * 类别： com.day.cq.replication

1. 如果您怀疑该问题与Sling事件/作业以任何方式相关，则还可以将此Java包添加到类别：org.apache.sling.event下

## 暂停复制代理队列  {#pausing-replication-agent-queue}

有时，暂停复制队列以减轻创作系统的负载而不禁用它可能是合适的。 目前，这只能通过暂时配置无效端口的黑客攻击来实现。 从5.4开始，您可以在复制代理队列中看到暂停按钮，该按钮有一些限制

1. 该状态不会持续存在，这意味着如果重新启动服务器或复制捆绑包被回收，它将恢复到运行状态。
1. 暂停空闲的时间较短（在没有通过其他线程复制的活动后为1小时），而不是较长时间。 因为Sling中有一个避免空闲线程的功能。 基本上，检查作业队列线程是否已经长时间未使用，如果是，它会启动清理周期。 由于清理周期，它会停止线程，因此暂停的设置丢失。 由于作业是持久的，因此它会启动一个新线程来处理没有已暂停配置详细信息的队列。 由于此队列变为运行状态。

## 用户激活时不会复制页面权限 {#page-permissions-are-not-replicated-on-user-activation}

不会复制页面权限，因为它们存储在授予访问权限的节点下，而不是与用户一起。

通常，页面权限不应从作者复制到发布，默认情况下也不应复制。 这是因为在这两个环境中，访问权限应该不同。 因此，建议在发布时与作者分开配置ACL。

## 将命名空间信息从创作复制到发布时阻止复制队列 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

在某些情况下，当尝试将命名空间信息从创作实例复制到发布实例时，复制队列会被阻止。 发生此情况是因为复制用户没有 `jcr:namespaceManagement` 特权。 要避免出现此问题，请确保：

* 复制用户(在 [传输](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) 选项卡>用户)也存在于发布实例中。
* 用户在安装内容的路径上拥有读写权限。
* 用户具有 `jcr:namespaceManagement` 存储库级别的权限。 您可以按如下方式授予权限：

1. 登录到CRX/DE ( `https://localhost:4502/crx/de/index.jsp`)作为管理员。
1. 单击 **访问控制** 选项卡。
1. 选择 **存储库**.
1. 单击 **添加条目** （加号图标）。
1. 输入用户的名称。
1. 选择 `jcr:namespaceManagement` 从权限列表中。
1. 单击确定。
