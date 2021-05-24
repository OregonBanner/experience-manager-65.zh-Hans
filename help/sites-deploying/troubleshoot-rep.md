---
title: 复制故障诊断
seo-title: 复制故障诊断
description: 本文提供了有关如何解决复制问题的信息。
seo-description: 本文提供了有关如何解决复制问题的信息。
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: 配置
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# 复制疑难解答{#troubleshooting-replication}

本页提供了有关如何解决复制问题的信息。

## 问题 {#problem}

复制（非反向复制）因某些原因而失败。

## 分辨率 {#resolution}

复制失败的原因有多种。 本文解释了在分析这些问题时可能采取的方法。

**单击激活按钮时，复制是否会完全触发？如果为NOT，则执行以下操作：**

1. 转到/crx/explorer并以管理员身份登录。
1. 打开“内容资源管理器”
1. 查看节点/bin/replicate或/bin/replicate.json是否存在。 如果节点存在，则删除该节点并保存。

**复制是否在复制代理队列中排队？**

请转到/etc/replication/agents.author.html ，然后单击要检查的复制代理，以检查此内容。

**如果一个代理队列或几个代理队列卡住：**

1. 队列是否显示&#x200B;**blocked**&#x200B;状态？ 如果是，则发布实例未运行或完全无响应？ 检查发布实例以查看其错误（即检查日志，并查看是否存在OutOfMemory错误或其他问题）。 然后，如果速度通常比较慢，请提取线程转储并分析它们。
1. 队列状态是否显示&#x200B;**队列处于活动状态 — # pending**? 基本上，复制作业可能卡在套接字读取中，等待发布实例或调度程序做出响应。 这可能意味着发布实例或调度程序处于高负载状态或卡在锁中。 从创作中获取线程转储，并在此例中发布。

   * 在线程转储分析器中打开创作线程转储，检查复制代理的sling事件作业是否在套接字读取中卡住。
   * 在线程转储分析器中打开发布中的线程转储，分析可能导致发布实例未做出响应的原因。 您应会看到名称中带有POST/bin/receive的线程，该线程是从作者处接收复制的线程。

**如果所有代理队列都卡住**

1. 由于存储库损坏或其他问题，某段内容可能无法在/var/replication/data下序列化。 检查logs/error.log中的相关错误。 要清除错误的复制项，请执行以下操作：

   1. 转到https://&lt;host>:&lt;port>/crx/de ，以管理员用户身份登录。
   1. 单击顶部菜单中的“工具”。
   1. 单击放大镜按钮。
   1. 选择“XPath”作为“Type”。
   1. 在“查询”框中，输入@slingevent:created的查询/jcr:root/var/eventing/jobs//element(*,slingevent:Job)顺序
   1. 单击“搜索”
   1. 在结果中，排名最前的项目是最新的sling事件作业。 单击每个复制器，然后找到与队列顶部显示的内容相匹配的卡住复制器。

1. sling事件框架作业队列可能出错。 尝试在/system/console中重新启动org.apache.sling.event包。
1. 可能是作业处理已完全关闭。 您可以在Felix控制台的Sling事件选项卡中查看该设置。 检查它是否显示 — Apache Sling事件（作业处理已禁用！）

   * 如果为“是”，则在Felix控制台的“配置”选项卡下检查Apache Sling作业事件处理程序。 可能是未选中“作业处理已启用”复选框。 如果选中该复选框，但仍显示“作业处理已禁用”，则请检查/apps/system/config下是否存在任何正在禁用作业处理的叠加。 尝试为jobmanager.enabled创建一个布尔值为true的osgi:config节点，然后重新检查激活是否开始以及队列中没有更多作业。

1. DefaultJobManager配置也可能处于不一致状态。 当某人通过OSGiconsole手动修改“Apache Sling作业事件处理程序”配置（例如，禁用并重新启用“已启用作业处理”属性并保存配置）时，可能会发生这种情况。

   * 此时，存储在crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config的DefaultJobManager配置将进入不一致状态。 即使“Apache Sling作业事件处理程序”属性显示“已启用作业处理”处于选中状态，当您导航到Sling事件选项卡时，仍会显示消息 — JOB PROCESSING IS DISABLED ，并且复制不起作用。
   * 要解决此问题，您需要导航到OSGi控制台的“配置”页面并删除“Apache Sling作业事件处理程序”配置。 然后，重新启动群集的主控节点，以使配置恢复到一致状态。 这应该可以修复该问题，并且复制将重新开始工作。

**创建replication.log**

有时，将所有复制日志记录设置为在调试级别的单独日志文件中，会非常有用。 要执行此操作：

1. 转到https://host:port/system/console/configMgr并以管理员身份登录。
1. 找到Apache Sling日志记录器工厂，然后单击工厂配置右侧的&#x200B;**+**&#x200B;按钮以创建实例。 这将创建新的日志记录记录器。
1. 设置如下配置：

   * 日志级别：调试
   * 日志文件路径：logs/replication.log
   * 类别：com.day.cq.replication

1. 如果您怀疑问题与sling事件/作业有任何关系，则还可以在categories:org.apache.sling.event下添加此Java包

## 暂停复制代理队列{#pausing-replication-agent-queue}

有时，可能适合暂停复制队列以减少创作系统的负载，而不禁用它。 目前，只有临时配置无效端口的黑客攻击才能做到这一点。 从5.4开始，您可以在复制代理队列中看到暂停按钮，它存在一些限制

1. 状态不会持久，这意味着如果重新启动服务器或复制包被循环使用，它将返回到运行状态。
1. 暂停的空闲时间较短（在没有其他线程复制的活动后1小时，OOB空闲），并且不会超过更长时间。 因为Sling中有避免空闲线程的功能。 基本上，检查作业队列线程是否已被使用较长时间，如果这样，它就会启动清理周期。 由于清理周期，它会停止线程，因此暂停的设置会丢失。 由于保留了作业，因此会启动一个新线程来处理没有暂停配置详细信息的队列。 由于此队列变为运行状态。

## 用户激活{#page-permissions-are-not-replicated-on-user-activation}时未复制页面权限

页面权限不会复制，因为它们存储在授予访问权限的节点下，而不是与用户一起存储。

一般情况下，页面权限不应从作者复制到发布，而且默认情况下不应复制。 这是因为这两个环境中的访问权限应该不同。 因此，建议在发布时与作者分开配置ACL。

## 在将命名空间信息从创作复制到发布{#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}时，复制队列被阻止

在某些情况下，在尝试将命名空间信息从创作实例复制到发布实例时，复制队列会被阻止。 发生此情况的原因是复制用户没有`jcr:namespaceManagement`权限。 要避免出现此问题，请确保：

* 复制用户（如[Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)选项卡>User下配置）也存在于Publish实例中。
* 用户在安装内容的路径上具有读写权限。
* 用户在存储库级别具有`jcr:namespaceManagement`权限。 您可以按如下方式授予权限：

1. 以管理员身份登录到CRX/DE(`https://localhost:4502/crx/de/index.jsp`)。
1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 选择&#x200B;**Repository**。
1. 单击&#x200B;**Add Entry**（加号图标）。
1. 输入用户的名称。
1. 从权限列表中选择`jcr:namespaceManagement`。
1. 单击确定。
