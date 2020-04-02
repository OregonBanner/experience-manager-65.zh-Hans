---
title: 用户同步
seo-title: 用户同步
description: 了解AEM中的用户同步。
seo-description: 了解AEM中的用户同步。
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
translation-type: tm+mt
source-git-commit: c9edac158bc6a00637f8be5aac70a2a249e11d59

---


# 用户同步{#user-synchronization}

## 简介 {#introduction}

当部署是发 [布场时](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，成员需要能够登录并查看其任何发布节点上的数据。

在发布环境中创建的用户和用户组（用户数据）在创作环境中不需要。

在创作环境中创建的大多数用户数据都打算保留在创作环境中，而不会被复制到发布实例中。

在一个发布实例上进行的注册和修改需要与其他发布实例同步，以便它们能够访问相同的用户数据。

自AEM 6.1起，启用用户同步后，用户数据将自动在群中的发布实例之间同步，而不是在作者身上创建。

## Sling分发 {#sling-distribution}

用户数据及其 [ACL](/help/sites-administering/security.md)，存储在 [Oak Core中，即Oak JCR下的层，并使用](/help/sites-deploying/platform.md)Oak API [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)。 由于更新不频繁，因此使用 [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (Sling Distribution)将用户数据与其他发布实例同步是合理的。

与传统复制相比，使用Sling分发进行用户同步的好处有：

* *用户*、用 *户用户档案和在发* 布时创建的用户组 ** ，不会在创作时创建

* Sling分发在jcr事件中设置属性，使得可以在发布端事件监听器中执行操作，而无需考虑无限的复制循环
* Sling分发仅将用户数据发送到非源发布实例，从而消除不必要的流量
* [在用户](/help/sites-administering/security.md) 节点中设置的ACL包含在同步中

>[!NOTE]
>
>如果需要会话，建议使用SSO解决方案或使用粘性会话，并在客户切换到其他发布者时让其登录。

>[!CAUTION]
>
>即使启用了 ***用户同步*** ，也不支持管理员组的同步。 相反，“导入差异”失败将记录在错误日志中。
>
>因此，当部署是发布场时，如果将用户添加到***administrators** group或从中删除用户，则必须对每个发布实例手动进行修改。

## 启用用户同步 {#enable-user-sync}

>[!NOTE]
>
>默认情况下，用户同步为 `disabled`。
>
>启用用户同步涉及修改 *现有* OSGi配置。
>
>不应因启用用户同步而添加新配置。

用户同步依赖于创作环境来管理用户数据分发，即使用户数据不是由作者创建的。 许多（但并非全部）配置都发生在创作环境中，每个步骤都清楚地标识是在创作还是发布时执行。

以下是启用用户同步所必需的步骤，后面是“疑难解 [答](#troubleshooting) ”部分：

### 前提条件 {#prerequisites}

1. 如果用户和用户组已在一个发布者上创建，则建议在配置和启用用户同步 [之前](#manually-syncing-users-and-user-groups) ，手动将用户数据同步到所有发布者。

启用用户同步后，只同步新创建的用户和用户组。

1. 确保已安装最新代码：

* [AEM平台更新](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1.Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

**启用用户同步**

* **在作者**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位 `Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）验证 `name`: **`socialpubsync`**

      * 选中复选 `Enabled` 框
      * select `Save`


![](assets/chlimage_1-20.png)

### 2.创建授权用户 {#createauthuser}

**配置权**&#x200B;限此授权用户将在步骤3中用于配置创作时的Sling分发。

* **在每个发布实例上**

   * 使用管理员权限登录
   * 访问安 [全控制台](/help/sites-administering/security.md)

      * 例如， [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * 创建新用户

      * for example, `usersync-admin`
   * 将此用户添加到用 **`administrators`** 户组
   * [将此用户的ACL添加到/home](#howtoaddacl)

      * `Allow jcr:all` 限制 `rep:glob=*/activities/*`



>[!CAUTION]
>
>必须创建新用户。
>
>* 分配的默认用户为 **`admin`**。
>* 不使用 `communities-user-admin user.`
>



#### 如何添加ACL {#addacls}

* 访问CRXDE Lite

   * 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 选择节 `/home` 点
* 在右侧窗格中，选择选 `Access Control` 项卡
* 选择 `+` 按钮以添加ACL条目

   * **主要**:搜索 *为用户同步创建的用户*
   * **类型**: `Allow`
   * **权限**: `jcr:all`
   * **限制** rep:glob: `*/activities/*`
   * 选择确 **定**

* 选择 **全部保存**

![](assets/chlimage_1-21.png)

另请参阅

* [访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 疑难排解部 [分在响应处理过程中修改操作异常](#modify-operation-exception-during-response-processing)。

### 3.Apache Sling Distribution Transport Credentials —— 基于用户凭据的DistributionTransportSecretProvider {#adobegraniteencpasswrd}

**配置权限**

在所有发布实例上创建了授权用户**`administrators`**用户组的成员后，必须在创作时将该授权用户标识为具有从创作同步用户数据到发布的权限。

* **在作者**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位 `Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider`
   * 选择要打开进行编辑的现有配置（铅笔图标）验证 `property name`: **`socialpubsync-publishUser`**

   * 在步骤2中将用户名和密码设置为在 [发布时创建](#createauthuser) 的授权用户。

      * for example, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4.Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

**启用用户同步**

* **发布时**:

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 定位 `Apache Sling Distribution Agent - Queue Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）验证 `Name`: `socialpubsync-reverse`

      * 选中复选 `Enabled` 框
      * select `Save`
   * **重复**



![](assets/chlimage_1-23.png)

### 5.Adobe Social Sync - Diff Observer Factory {#diffobserver}

**启用组同步**

* **在每个发布实例上**:

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 定位 **`Adobe Social Sync - Diff Observer Factory`**

      * 选择要打开进行编辑的现有配置（铅笔图标）

         验证 `agent name`: `socialpubsync-reverse`

      * 选中复选 `Enabled` 框
      * select `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6.Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（可选）修改轮询间隔**

默认情况下，作者每30秒对更改进行轮询一次。 要更改此间隔：

* **在作者**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位 `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）

         * 验证 `Name`: `socialpubsync-scheduled-trigger`
      * 设置为 `Interval in Seconds` 所需的间隔
      * select `Save`



![](assets/chlimage_1-24.png)

## 为多个发布实例配置 {#configure-for-multiple-publish-instances}

默认配置是针对单个发布实例。 由于启用用户同步的原因是同步多个发布实例（如发布群），因此需要将其他发布实例添加到同步代理工厂。

### 7.Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**添加发布实例：**

* **在作者**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位 `Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）验证 `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **导出器端**&#x200B;点每个发布者应有一个导出器端点。 例如，如果有2个发布者，localhost:4503和4504，则应有2个条目：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **导入程序端**&#x200B;点每个发布者应有一个导入程序端点。 例如，如果有2个发布者，localhost:4503和4504，则应有2个条目：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8.AEM Communities用户同步监听器 {#aem-communities-user-sync-listener}

**（可选）同步其他JCR节点**

如果希望在多个发布实例之间同步自定义数据，则：

* **在每个发布实例上**:

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * for example, `https://localhost:4503/system/console/configMgr`
   * 定位 `AEM Communities User Sync Listener`
   * 选择要打开进行编辑的现有配置（铅笔图标）验证 `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **节点类**型这是要同步的节点类型的列表。 除sling:Folder之外的任何节点类型都需要在此列出（sling:folder需要单独处理）。
要同步的节点类型的默认列表:

   * rep：用户
   * nt:unstructured
   * nt:resource

* **可忽略**属性这是在检测到任何更改时将忽略的属性列表。 对这些属性所做的更改可能会作为其他更改的副作用而同步（因为同步始终在节点级别），但对这些属性所做的更改本身不会触发同步。
要忽略的默认属性：

   * cq:lastModified

* **可忽略节**点在同步过程中将完全忽略的子路径。 这些子路径下的任何内容将随时同步。
要忽略的默认节点：

   * .tokens
   * 系统

* **分布式文件**夹大多数sling：文件夹会被忽略，因为不需要同步。 此处列出了少数例外。
要同步的默认文件夹

   * 细分／评分
   * 社交／关系
   * 活动

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在两个或多个发布实例之间匹配，则用户组同步将失败。

如果Sling ID与发布群中多个发布实例的Sling ID相同，则用户组将不会同步。

要验证所有Sling ID值是否不同，请在每个发布实例上：

1. 浏览至 `http://<host>:<port>/system/console/status-slingsettings`
1. 检查 **Sling ID的值**

![](assets/chlimage_1-27.png)

如果发布实例的Sling ID与任何其他发布实例的Sling ID匹配，则：

1. 停止一个具有匹配Sling ID的发布实例
1. crx-quickstart/launchpad/felix目录中

   * 搜索并删除名为sling.id.file的文 *件*

      * 例如，在Linux系统上：
         `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系统上：
         `use windows explorer and search for *sling.id.file*`

1. 开始发布实例

   * 启动时，将为其分配一个新的Sling ID

1. 验证 **Sling ID现在是唯一** ,

重复这些步骤，直到所有发布实例都具有唯一的Sling ID。

## Vault Package Builder Factory {#vault-package-builder-factory}

为了使更新正确同步，必须修改Vault包构建器以便用户同步：

* 在每个AEM发布实例上
* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 查找 `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 选择编辑图标
* 添加两个 `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 策略处理：

   * 要用新节点覆盖现有rep:policy节点，请添加第三个包过滤器：

      * `/home/users|+.*/rep:policy`
   * 要防止策略被分发，请设置

      * `Acl Handling:` `IGNORE`


![Vault Package Builder Factory](assets/vault-package-builder-factory.png)

## 当…… {#what-happens-when}

### 用户在发布时自注册或编辑用户档案 {#user-self-registers-or-edits-profile-on-publish}

根据设计，在发布环境（自注册）中创建的用户和用户档案不会显示在创作环境中。

当拓扑为发布群 [，且用户同步已正确配置时，*user *和](/help/sites-deploying/recommended-deploys.md#tarmk-farm)** user用户档案将使用Sling分发在发布群中同步。

### 用户或用户组是使用安全控制台创建的 {#users-or-user-groups-are-created-using-security-console}

根据设计，在发布环境中创建的用户数据不显示在创作环境中，反之亦然。

当使用 [](/help/sites-administering/security.md) 用户管理和安全控制台在发布环境中添加新用户时，用户同步会将新用户及其组成员关系与其他发布实例同步（如果需要）。 用户同步还将同步通过安全控制台创建的用户组。

## 疑难解答 {#troubleshooting}

### 如何使用户同步脱机 {#how-to-take-user-sync-offline}

要使用户同步脱机，要删除发 [布者](#how-to-remove-a-publisher) ，或 [手动同步数据](#manually-syncing-users-and-user-groups)，分发队列必须为空而安静。

要检查分发队列的状态，请执行以下操作：

* 作者：

   * 使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 查找 `/var/sling/distribution/packages`

         * 使用模式命名的文件夹节点 `distrpackage_*`
   * 使用 [包管理器](/help/sites-administering/package-manager.md)

      * 查找待定包（尚未安装）

         * 以图案命名 `socialpubsync-vlt*`
         * created by `communities-user-admin`


当分发队列为空时，禁用用户同步：

* 在作者

   * *取消选中* `Enabled` Apache [Sling Distribution Agent - Sync Agents Factory的复选框](#apache-sling-distribution-agent-sync-agents-factory)

完成任务后，要重新启用用户同步：

* 在作者

   * 选中Apache `Enabled` Sling Distribution Agent - Sync Agents Factory [的复选框](#apache-sling-distribution-agent-sync-agents-factory)

### 使用同步诊断 {#user-sync-diagnostics}

用户同步诊断是一种检查配置并尝试识别任何问题的工具。

在创作时，只需通过工具、操作、诊断、用户同 **步诊断从主控制台中导航。**

只需进入“用户同步诊断”控制台，就会显示结果。

这是未启用用户同步时显示的内容：

![](assets/chlimage_1-28.png)

#### 如何为发布者运行诊断 {#how-to-run-diagnostics-for-publishers}

当从创作环境运行诊断程序时，通过／失败结果将包含一个 [INFO] （信息）部分，其中显示已配置发布实例的列表以进行确认。

该列表包含每个发布实例的URL，该实例将为该实例运行诊断。 url参数 `syncUser` 将附加到诊断URL中，其值设置为在步骤2中创 *建的授权同步* 用户 [](#createauthuser)。

**注意**:在启动URL之前，授权 *的同步用户* ，必须已登录到该发布实例。

![](assets/chlimage_1-29.png)

### 配置添加错误 {#configuration-improperly-added}

当用户同步失败时，最常见的问题是添加了其他配 *置*。 相反，应编辑*现有*默认配 *置*。

以下是已编辑的默认配置在Web控制台中的显示方式的视图。 如果出现多个实例，则应删除添加的配置。

#### （作者）一个Apache Sling Distribution Agent - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### （作者）一个Apache Sling Distribution Transport Credentials —— 基于用户凭据的DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### （发布）一个Apache Sling Distribution Agent —— 队列代理工厂 {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### （发布）一个Adobe Social Sync —— 差异观察器工厂 {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### （作者）一个Apache Sling分发触发器——计划触发器工厂 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### 在响应处理过程中修改操作异常 {#modify-operation-exception-during-response-processing}

如果日志中显示以下内容：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然后验证第 [2节。 正确遵循了“创建授权用户](#createauthuser) ”。

本节介绍如何创建在所有发布实例上存在的授权用户，并在创作的“机密提供者”OSGi配置中识别这些用户。 默认情况下，用户为 `admin`。

授权用户应成为用户组的成员， **`administrators`** 并且不应更改该用户组的权限。

授权用户应对所有发布实例明确具有以下权限和限制：

| **路径** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */活动/* |
| /home/users | X | */活动/* |
| /home/groups | X | */活动/* |

作为用户组的成员， `administrators` 授权用户应对所有发布实例具有以下权限：

| **路径** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 用户组同步失败 {#user-group-sync-failed}

如果Sling ID在两个或多个发布实例之间匹配，则用户组同步将失败。

请参阅第 [9节。 唯一Sling ID](#unique-sling-id)

### 手动同步用户和用户组 {#manually-syncing-users-and-user-groups}

* 在发布者上，其中存在用户和用户组：

   * [如果启用，则禁用用户同步](#how-to-take-user-sync-offline)
   * [创建包](/help/sites-administering/package-manager.md#creating-a-new-package) : `/home`

      * 编辑包时

         * 过滤器选项卡：添加过滤器：根路径： `/home`
         * 高级选项卡：交流处理： `Overwrite`
   * [导出包](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* 在其他发布实例上：

   * [导入包](/help/sites-administering/package-manager.md#installing-packages)

要配置或启用用户同步，请转到步骤1:Apache [Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

### 当发布者变得不可用时 {#when-a-publisher-becomes-unavailable}

当发布实例不可用时，如果它将来恢复联机状态，则不应删除它。 更改将排队等待发布者，一旦它重新联机，将处理更改。

如果发布实例永远不会恢复联机状态（如果它永久处于脱机状态），则必须删除它，因为队列累积将导致作者环境中明显的磁盘空间使用。

当发布者关闭时，创作日志将具有与以下内容类似的例外：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何删除发布者 {#how-to-remove-a-publisher}

要从 [Apache Sling Distribution Agent - Sync Agents Factory中删除发布者](#apache-sling-distribution-agent-sync-agents-factory)，分发队列必须为空且安静。

* 作者：

   * [使用户脱机同步](#how-to-take-user-sync-offline)
   * 按照 [步骤7](#apache-sling-distribution-agent-sync-agents-factory) ，从两个服务器列表中删除发布者：

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * 重新启用用户同步

      * 选中Apache `Enabled` Sling Distribution Agent - Sync Agents Factory [的复选框](#apache-sling-distribution-agent-sync-agents-factory)
