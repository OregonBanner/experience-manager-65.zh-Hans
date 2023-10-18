---
title: Communities用户同步
description: 了解用户同步在Adobe Experience Manager Communities中的工作方式。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '2471'
ht-degree: 2%

---

# Communities用户同步 {#communities-user-synchronization}

## 简介 {#introduction}

在Adobe Experience Manager (AEM) Communities中，从发布环境（取决于配置的权限）中， *网站访客* 可能会变成 *成员*，创建 *用户组*，并编辑其 *成员配置文件* .

*用户数据* 引用 *用户*， *用户配置文件*、和 *用户组*.

*成员* 请参阅 *用户* 在发布环境中注册的用户，而不是在创作环境中注册的用户。

有关用户数据的更多信息，请访问 [管理用户和用户组](/help/communities/users.md).

## 在发布场中同步用户 {#synchronizing-users-across-a-publish-farm}

根据设计，在发布环境中创建的用户数据不会显示在创作环境中。

在创作环境中创建的大多数用户数据旨在保留在创作环境中，不会同步也不会复制到发布实例。

当 [拓扑](/help/communities/topologies.md) 是 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，对一个发布实例所做的注册和修改必须与其他发布实例同步。 成员必须能够登录并在任何发布节点上查看其数据。

启用用户同步后，将在场中的发布实例之间自动同步用户数据。

### 用户同步设置说明 {#user-sync-setup-instructions}

有关如何启用发布场间同步的分步详细说明，请参阅 [用户同步](/help/sites-administering/sync.md).

## 后台用户同步 {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt包**

  它是zip文件，其中包含对发布服务器进行的所有更改，必须在发布服务器上进行分发。 对发布者所做的更改将生成由更改事件侦听器选取的事件。 这将创建一个包含所有更改的vlt包。

* **分发包**

  它包含Sling的分发信息。 这是有关必须在何处分发内容以及最后分发内容的时间的信息。

## 当……发生时 {#what-happens-when}

### 从社区站点控制台发布站点 {#publish-site-from-communities-sites-console}

在作者中，当从发布社区站点时 [社区站点控制台](/help/communities/sites-console.md)，效果为 [复制](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) 关联的页面和Sling分发动态创建的社区用户组，包括其成员资格。

### 发布时创建或编辑用户配置文件 {#user-is-created-or-edits-profile-on-publish}

根据设计，在发布环境中创建的用户和配置文件（例如通过自助注册、社交登录、LDAP身份验证）不会显示在创作环境中。

当拓扑为 [发布场](/help/communities/topologies.md) 和用户同步已正确配置， *用户* 和 *用户配置文件* 使用Sling分发跨发布场同步。

### 发布时创建新社区组 {#new-community-group-is-created-on-publish}

虽然社区组创建是从发布实例启动的，但实际上会在“创作”实例上发生，从而产生新的站点页面和新用户组。

作为此过程的一部分，新站点页面将复制到所有发布实例。 动态创建的社区用户组及其成员资格将分发到所有Publish实例。

### 用户或用户组是使用安全控制台创建的 {#users-or-user-groups-are-created-using-security-console}

根据设计，在发布环境中创建的用户数据不会显示在创作环境中，反之亦然。

当 [用户管理和安全性](/help/sites-administering/security.md) console用于在发布环境中添加新用户，如有必要，用户同步会将新用户及其组成员资格同步到其他发布实例。 用户同步还会同步通过安全控制台创建的用户组。

### 用户发布时发布内容 {#user-posts-content-on-publish}

对于用户生成的内容(UGC)，在发布实例上输入的数据可通过 [配置的SRP](/help/communities/srp-config.md).

## 最佳实践 {#bestpractices}

默认情况下，用户同步为 **已禁用**. 启用用户同步涉及修改 *现有* osgi配置。 启用用户同步后，不应添加任何新配置。

用户同步依赖于作者环境来管理用户数据分发，即使用户数据不是基于作者创建的。

**前提条件**

1. 如果已在一个发布服务器上创建了用户和用户组，则建议执行以下操作 [手动同步](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) 配置并启用用户同步之前，将用户数据发送到所有发布者。

   启用用户同步后，将仅同步新创建的用户和组。

1. 确保安装了最新的代码：

   * [AEM平台更新](https://helpx.adobe.com/cn/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

需要以下配置才能在AEM Communities上启用用户同步。 确保这些配置正确无误，以防止sling内容分发失败。

### Apache Sling分发代理 — 同步代理工厂 {#apache-sling-distribution-agent-sync-agents-factory}

此配置获取要在发布者之间同步的内容。 该配置位于创作实例上。 作者必须跟踪所有存在的发布者以及在何处同步所有信息。

配置中的默认值适用于单个发布实例。 由于用户同步对于同步多个发布实例很有用（例如对于发布场），因此需要向配置中添加其他发布实例。

**内容如何同步？**

创作实例ping发布服务器的导出程序终结点。 每当在特定发布者(n)上创建用户或更新用户时，作者都会从其导出程序端点获取内容，并且 [推送内容](/help/communities/sync.md#main-pars-image-1413756164) 其他发布者（n-1，不同于从中获取内容的发布者）。

要配置Apache Sling同步代理配置，请执行以下操作：

1. 使用管理员权限登录到AEM创作实例。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 定位 **Apache Sling分发代理 — 同步代理工厂**.

   * 选择要打开进行编辑的现有配置（铅笔图标）。

     验证名称： **socialpubsync。**

   * 选中&#x200B;**启用**&#x200B;复选框。
   * 选择 **使用多个队列。**
   * 指定 **导出程序端点** 和 **导入程序终端** （您可以添加更多导出程序和导入程序端点）。

     这些端点定义从何处获取内容以及要将内容推送到何处。 作者从指定的导出程序终结点获取内容，并将内容推送到发布者（而不是从中获取内容的发布者）。

   ![sync-agent-fact](assets/sync-agent-fact.png)

### AdobeGranite分发 — 加密的密码传输密钥提供程序 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它使作者能够识别具有将用户数据从作者同步到发布的权限的授权用户。

此 [已创建授权用户](/help/sites-administering/sync.md#createauthuser) 在所有发布实例上，帮助发布者与作者连接并在作者上配置Sling分发。 此授权用户拥有所有必需的 [ACL](/help/sites-administering/sync.md#howtoaddacl).

每当要在发布服务器上安装数据或从发布服务器上获取数据时，作者都将使用此配置中设置的凭据（用户名和密码）与发布者连接。

要使用授权用户连接作者与发布者，请执行以下操作：

1. 使用管理员权限登录到AEM创作实例。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 定位 **AdobeGranite分发 — 加密的密码传输密钥提供程序。**
1. 选择要打开进行编辑的现有配置（铅笔图标）。

   验证属性 **socialpubsync** - **publishUser。**

1. 将用户名和密码设置为 [授权用户](/help/sites-administering/sync.md#createauthorizeduser).

   例如， **usersync — 管理员**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling分发代理 — 队列代理工厂 {#apache-sling-distribution-agent-queue-agents-factory}

此配置用于配置要在发布者之间同步的数据。 在指定的路径中创建/更新数据时 **允许的根**，则会激活“var/community/distribution/diff”，并且创建的复制程序会从发布服务器获取数据并将其安装到其他发布服务器。

要配置要同步的数据（节点路径）：

1. 使用发布实例上的管理员权限登录。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 定位 **Apache Sling分发代理 — 队列代理工厂**.
1. 选择要打开进行编辑的现有配置（铅笔图标）。

   验证名称： **socialpubsync -reverse**

1. 选择 **已启用** 复选框，然后保存。
1. 指定要复制的节点路径 **允许的根**.
1. 重复执行每个 **发布** 实例。

   ![queue-agents-fact](assets/queue-agents-fact.png)

### AdobeGranite分发 — 观察者工厂差异 {#adobe-granite-distribution-diff-observer-factory}

此配置跨发布者同步组成员资格。
如果更改一个发布器中组的成员资格时没有更新其在其他发布器上的成员资格，请确保 **ref ：members** 已添加至 **查找的属性名称**.

要确保成员同步，请执行以下操作：

1. 使用发布实例上的管理员权限登录。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 定位 **AdobeGranite分发 — 观察者工厂差异**.
1. 选择要打开进行编辑的现有配置（铅笔图标）。

   验证 **代理名称： socialpubsync -reverse**.

1. 选中&#x200B;**启用**&#x200B;复选框。
1. 指定 **rep：members** 作为中的propertyName的说明 **查找的属性名称**，并保存。

   ![差异](assets/diff-obs.png)

### Apache Sling Distribution Trigger — 计划触发器工厂 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

通过此配置，可配置轮询间隔（在此间隔后，发布者将进行试通，作者将提取更改）以跨发布者同步更改。

作者每30秒轮询发布者（默认）。 如果文件夹中存在任何包 `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`，然后它会获取这些包并将它们安装在其他发布者上。

更改轮询间隔：

1. 使用管理员权限登录到AEM创作实例。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 定位 **Apache Sling Distribution Trigger — 计划触发器工厂**

   * 选择要打开进行编辑的现有配置（铅笔图标）。

     验证 **socialpubsync -scheduled-trigger**

   * 将“时间间隔（秒）”设置为所需的时间间隔，然后保存。

   ![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities用户同步侦听器 {#aem-communities-user-sync-listener}

对于在Sling分发中订阅和所关注内容不一致的问题，检查中是否包括以下属性 **AEM Communities用户同步侦听器** 已设置配置：

* 节点类型
* 可忽略的属性
* 可忽略的节点
* 分布式文件夹

同步订阅、关注和通知

在每个AEM发布实例上：

1. 使用管理员权限登录。
1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 定位 **AEM Communities用户同步侦听器**.
1. 选择要打开以进行编辑的现有配置（铅笔图标）

   验证名称： **socialpubsync -scheduled-trigger**

1. 设置以下内容 **节点类型**：

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   此属性中指定的节点类型会同步，并且通知信息（遵循的博客和配置）会在不同的发布者之间同步。

1. 添加要在其中同步的所有文件夹 **分布式文件夹**. 例如，

   `segments/scoring`

   `social/relationships`

   `activities`

1. 设置 **ignorablenodes** 至：

   `.tokens`

   `system`

   `rep:cache` （由于我们使用粘性会话，因此不需要将此节点同步到不同的发布者）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 唯一Sling ID {#unique-sling-id}

AEM创作实例使用Sling ID来识别数据的来源以及它需要（或不需要）将包发送回的发布者。

确保发布场中的所有发布者都有一个唯一的Sling ID。 如果发布场中的多个发布实例的Sling ID相同，则用户同步失败。 因为作者不知道从何处获取包以及在何处安装包。

要确保发布场中发布者的唯一Sling ID，请在每个发布实例上：

1. 浏览至 [https://_host：port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. 检查值 **Sling ID**.

   ![slingid](assets/slingid.png)

   如果发布实例的Sling ID与任何其他发布实例的Sling ID匹配，则：

1. 停止具有匹配Sling ID的其中一个发布实例。
1. 在 `crx-quickstart/launchpad/felix` 目录，搜索并删除名为的文件 *sling.id.file.*

   例如，在Linux系统上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系统上：

   使用Windows资源管理器并搜索 `sling.id.file`

1. 启动发布实例。 启动时，会为其分配一个新的Sling ID。
1. 验证 **Sling ID** 现在是唯一的。

重复这些步骤，直到所有发布实例都具有唯一的Sling ID。

### Vault Package Builder工厂 {#vault-package-builder-factory}

要使更新正确同步，必须修改Vault包生成器以进行用户同步。
在 `/home/users`， a `*/rep:cache` 节点已创建。 它是一种缓存，用来发现如果我们查询一个节点的主体名称，那么这个缓存可以直接使用。

在以下情况下，可以停止用户同步： `rep :cache` 节点在发布者之间同步。

要确保更新在发布者之间正确同步，请在每个AEM Publish实例上：

1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 找到 **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   生成器名称：socialpubsync-vlt。

1. 选择编辑图标。
1. 添加两个包节点筛选器：
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 策略处理
   * 要使用新节点覆盖现有rep ：policy节点，请添加第三个包过滤器： `/home/users|+.*/rep:policy`
   * 要防止策略被分发，请设置： `Acl Handling: IGNORE`

   ![Vault包生成器工厂](assets/vault-package-builder-factory.png)

## AEM Communities中的Sling分发疑难解答 {#troubleshoot-sling-distribution-in-aem-communities}

如果Sling分发失败，请尝试以下调试步骤：

1. **检查 [未正确添加配置](/help/sites-administering/sync.md#improperconfig)**

   确保未添加或编辑多个配置，而是应编辑现有的默认配置。
1. **检查配置**

   确保所有 [配置](/help/communities/sync.md#bestpractices) 在您的AEM创作实例中进行适当设置，如中所述 [最佳实践](/help/communities/sync.md#main-pars-header-863110628).

1. **检查授权用户权限**

   如果软件包安装不正确，请检查 [授权用户](/help/sites-administering/sync.md#createauthuser) 在第一个发布实例中创建的，具有正确的ACL。

   要验证此内容，而不是 [已创建授权用户](/help/sites-administering/sync.md#createauthuser) 更改 [AdobeGranite分发 — 加密的密码传输密钥提供程序](/help/sites-administering/sync.md#adobegraniteencpasswrd) 在创作实例上配置为使用管理员用户凭据。 现在，请尝试重新安装包。 如果用户同步使用管理员凭据时工作正常，则意味着创建的发布用户没有适当的ACL。

1. **检查Diff Observer Factory配置**

   如果仅特定节点未在发布场之间同步（例如，组成员未同步），请确保 [AdobeGranite分发 — 观察者工厂差异](/help/sites-administering/sync.md#diffobserver) 配置已启用，并且 **rep：成员** 在中设置 **查找的属性名称**.

1. **检查AEM Communities用户同步侦听器配置。** 如果创建的用户已同步，但订阅和以下订阅不起作用，请确保AEM Communities用户同步侦听器配置具有：

   * 节点类型 — 设置为 **rep：User， nt：unstructured**， **nt：resource**， **rep：ACL**， **sling：Folder**、和 **sling：OrderedFolder**.
   * 可忽略的节点 — 设置为 **.tokens**， **系统**、和 **rep ：cache**.
   * 分布式文件夹 — 设置为要分发的文件夹。

1. **检查在发布实例上创建用户时生成的日志**

   如果正确设置了上述配置，但用户同步无法正常工作，请检查创建用户时生成的日志。

   检查日志的顺序是否相同，如下所示：

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

要进行调试：

1. 禁用用户同步：
1. 在AEM创作实例上，使用管理员权限登录。

   1. 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 查找配置 **Apache Sling分发代理 — 同步代理工厂**.
   1. 取消选择 **已启用** 复选框。

      在禁用创作实例（导出器和导入器）端点上的用户同步时，将禁用该实例，并且创作实例是静态的。 此 **vlt** 作者不会ping或获取包。

      现在，如果在发布实例上创建用户，则 **vlt** 包创建于 */var/sling/distribution/packages/ socialpubsync - vlt /data* 节点。 并且作者是否将这些包推送到其他服务。 您可以下载并提取此数据，以检查将所有属性推送到其他服务的情况。

1. 转到发布者，并在发布者上创建用户。 因此，会创建事件。
1. 查看 [日志的顺序](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) 在用户创建时创建。
1. 检查是否 **vlt** 包创建于 **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. 现在，在AEM Author实例上启用用户同步。
1. 在发布服务器上，更改中的导出程序或导入程序端点 **Apache Sling分发代理 — 同步代理工厂**.
我们可以下载并提取包数据，以检查哪些属性已推送到其他发布者，以及哪些数据丢失。
