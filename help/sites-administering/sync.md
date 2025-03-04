---
title: 用户同步
description: 了解AEM中用户同步的内部工作原理。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 5%

---


# 用户同步{#user-synchronization}

## 简介 {#introduction}

当部署是 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，成员必须能够登录并在任何发布节点上查看其数据。

创作环境中不需要在发布环境中创建的用户和用户组（用户数据）。

在创作环境中创建的大多数用户数据都会保留在创作环境中，而不会复制到Publish实例。

对一个发布实例所做的注册和修改必须与其他发布实例同步，它们才能访问相同的用户数据。

从AEM 6.1开始，当用户同步启用时，用户数据将自动在场中的Publish实例之间同步，并且不会在author上创建。

## Sling分发 {#sling-distribution}

用户数据及其 [ACL](/help/sites-administering/security.md)，存储在中 [Oak Core](/help/sites-deploying/platform.md)，位于Oak JCR下方的层，可通过访问 [Oak API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). 对于不常见的更新，可以使用将用户数据与其他发布实例同步 [Sling内容分发](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md) （Sling分发）。

与传统复制相比，使用Sling分发的用户同步具有以下优势：

* *用户*， *用户配置文件*、和 *用户组* 在发布时创建的内容不是在创作时创建的

* Sling分发可设置jcr事件中的属性，从而能够在发布端事件侦听器内执行操作，而无需考虑无限复制循环
* Sling Distribution仅将用户数据发送到非源发布实例，从而消除不必要的流量
* [ACL](/help/sites-administering/security.md) 在同步中包括用户节点中的设置

>[!NOTE]
>
>如果需要会话，建议使用SSO解决方案或使用粘性会话，并且在客户切换到另一个发布实例时让他们登录。

>[!CAUTION]
>
>同步 **管理员** 不支持组，即使启用了用户同步也是如此。 相反，错误日志中会记录“导入差异”失败。
>
>因此，当部署是发布场时，如果将用户添加到或从中删除， **管理员** 组，必须在每个发布实例上手动进行修改。

## 启用用户同步 {#enable-user-sync}

>[!NOTE]
>
>默认情况下，用户同步为 `disabled`.
>
>启用用户同步涉及修改 *现有* osgi配置。
>
>启用用户同步后，不应添加任何新配置。

用户同步依赖作者环境管理用户数据分发，即使未在作者上创建用户数据也是如此。 大部分配置（但不是全部）发生在创作环境中，每个步骤都清楚地标识是对“创作”还是“发布”执行。

以下是启用用户同步所需的步骤，随后是 [疑难解答](#troubleshooting) 部分：

### 前提条件 {#prerequisites}

1. 如果已在一个发布实例上创建用户和用户组，则建议执行以下操作 [手动同步](#manually-syncing-users-and-user-groups) 将用户数据发送到所有发布实例，然后再配置并启用用户同步。

启用用户同步后，将仅同步新创建的用户和组。

1. 确保安装了最新的代码：

* [AEM平台更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling分发代理 — 同步代理工厂 {#apache-sling-distribution-agent-sync-agents-factory}

**启用用户同步**

* **在作者上**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 定位 `Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择现有配置以便打开它进行编辑（铅笔图标）验证 `name`： **`socialpubsync`**

      * 选择 `Enabled` 复选框
      * 选择 `Save`

![Apache Sling分发代理](assets/chlimage_1-20.png)

### 2.创建授权用户 {#createauthuser}

**配置权限**

在步骤3中使用授权用户在Author上配置Sling分发。

* **在每个发布实例上**

   * 使用管理员权限登录
   * 访问 [安全控制台](/help/sites-administering/security.md)

      * 例如， [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * 创建用户

      * 例如， `usersync-admin`

   * 将此用户添加到 **`administrators`** 用户组
   * [将此用户的ACL添加到/home](#howtoaddacl)

      * `Allow jcr:all` 具有限制 `rep:glob=*/activities/*`

>[!CAUTION]
>
>必须创建新用户。
>
>* 分配的默认用户为 **`admin`**.
>* 不使用 `communities-user-admin user.`
>

#### 如何添加ACL {#addacls}

* 访问CRXDE Lite

   * 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 选择 `/home` 节点
* 在右窗格中，选择 `Access Control` 选项卡
* 要添加ACL项，请选择 `+` 按钮

   * **主体**： *搜索为用户同步创建的用户*
   * **类型**：`Allow`
   * **权限**： `jcr:all`
   * **限制** rep:glob: `*/activities/*`
   * 选择 **确定**

* 选择 **全部保存**

![添加ACL窗口](assets/chlimage_1-21.png)

另请参阅

* [访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* “疑难解答”部分 [处理响应期间修改操作异常](#modify-operation-exception-during-response-processing).

### 3. Granite分发Adobe — 加密的密码传输密钥提供程序 {#adobegraniteencpasswrd}

**配置权限**

一旦授权用户成为 **`administrators`** 用户组是在所有Publish实例中创建的，在Author上必须将授权用户标识为具有将用户数据从Author同步到Publish的权限。

* **在作者上**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 定位 `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * 要打开进行编辑，请选择现有配置（铅笔图标）验证 `property name`： **`socialpubsync-publishUser`**

   * 将用户名和密码设置为 [授权用户](#createauthuser) 在第2步发布时创建

      * 例如， `usersync-admin`

![加密的密码传输密钥提供程序](assets/chlimage_1-22.png)

### 4. Apache Sling分发代理 — 队列代理工厂 {#apache-sling-distribution-agent-queue-agents-factory}

**启用用户同步**

* **在每个发布实例上**：

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 定位 `Apache Sling Distribution Agent - Queue Agents Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）验证 `Name`： `socialpubsync-reverse`

      * 选择 `Enabled` 复选框
      * 选择 `Save`

   * **repeat** 适用于每个发布实例

![队列代理工厂](assets/chlimage_1-23.png)

### 5. Adobe Social同步 — 观察者工厂差异 {#diffobserver}

**启用组同步**

* **在每个发布实例上**：

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 定位 **`Adobe Social Sync - Diff Observer Factory`**

      * 要打开进行编辑，请选择现有配置（铅笔图标）

        验证 `agent name`: `socialpubsync-reverse`

      * 选择 `Enabled` 复选框
      * 选择 `Save`

![比较观察程序工厂](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger — 计划触发器工厂 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（可选）修改轮询间隔**

默认情况下，作者每30秒轮询一次更改。 更改此间隔：

* **在作者上**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 定位 `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）

         * 验证 `Name`: `socialpubsync-scheduled-trigger`

      * 设置 `Interval in Seconds` 到所需的间隔
      * 选择 `Save`

![计划触发器工厂](assets/chlimage_1-24.png)

## 为多个发布实例配置 {#configure-for-multiple-publish-instances}

默认配置是适用于单个发布实例。 由于启用用户同步的原因是同步多个发布实例，例如对于发布场，必须将其他发布实例添加到同步代理工厂。

### 7. Apache Sling分发代理 — 同步代理工厂 {#apache-sling-distribution-agent-sync-agents-factory-1}

**添加发布实例：**

* **在作者上**

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 定位 `Apache Sling Distribution Agent - Sync Agents Factory`

      * 要打开进行编辑，请选择现有配置（铅笔图标）验证 `Name`： `socialpubsync`

![同步代理工厂](assets/chlimage_1-25.png)

* **导出程序端点**
每个发布实例都应该有一个导出器端点。 例如，如果有2个Publish实例localhost：4503和4504，则应该有两个条目：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **导入程序终端**
每个发布实例都应该有一个导入程序端点。 例如，如果有2个Publish实例localhost：4503和4504，则应该有两个条目：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 选择 `Save`

### 8. AEM Communities用户同步侦听器 {#aem-communities-user-sync-listener}

**（可选）同步其他JCR节点**

如果有要在多个发布实例之间同步的自定义数据，则：

* **在每个发布实例上**：

   * 使用管理员权限登录
   * 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， `https://localhost:4503/system/console/configMgr`

   * 定位 `AEM Communities User Sync Listener`
   * 要打开进行编辑，请选择现有配置（铅笔图标）验证 `Name`： `socialpubsync-scheduled-trigger`

![AEM Communities用户同步侦听器](assets/chlimage_1-26.png)

* **节点类型**
这是已同步的节点类型的列表。 必须在此处列出sling：Folder以外的任何节点类型（sling：folder单独处理）。
要同步的节点类型的默认列表：

   * rep：User
   * nt:unstructured
   * nt：resource

* **可忽略的属性**
这是如果检测到任何更改将被忽略的属性的列表。 对这些属性的更改可能会作为其他更改的副作用而同步（因为同步始终在节点级别），但是对这些属性的更改本身不会触发同步。
要忽略的默认属性：

   * cq:lastModified

* **可忽略的节点**
同步期间被忽略的子路径。 这些子路径下的任何内容都不会随时同步。
要忽略的默认节点：

   * .tokens
   * system

* **分布式文件夹**
大多数sling：Folders被忽略，因为不需要同步。 这里列出了少数例外。
要同步的默认文件夹

   * 区段/得分
   * 社交/关系
   * 活动

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在两个或更多发布实例之间匹配，则用户组同步失败。

如果发布场中的多个发布实例的Sling ID相同，则用户组不会同步。

要验证所有Sling ID值是否不同，请在每个发布实例上：

1. 浏览至 `http://<host>:<port>/system/console/status-slingsettings`
1. 检查值 **Sling ID**

![检查Sling ID的值](assets/chlimage_1-27.png)

如果发布实例的Sling ID与任何其他发布实例的Sling ID匹配，则：

1. 停止具有匹配Sling ID的其中一个发布实例
1. 在crx-quickstart/launchpad/felix目录中

   * 搜索并删除名为的文件 *sling.id.file*

      * 例如，在Linux®系统上：
        `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系统上：
        `use windows explorer and search for *sling.id.file*`

1. 启动发布实例

   * 启动时，会为其分配一个新的Sling ID

1. 验证 **Sling ID** 现在是唯一的

重复这些步骤，直到所有发布实例都具有唯一的Sling ID。

## Vault Package Builder工厂 {#vault-package-builder-factory}

要使更新正确同步，必须修改用于用户同步的Vault包生成器：

* 在每个AEM发布实例上
* 访问 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到 `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 选择编辑图标
* 添加两个 `Package Node Filters`：

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 策略处理：

   * 要使用新节点覆盖现有rep：policy节点，请添加第三个包过滤器：

      * `/home/users|+.*/rep:policy`

   * 要防止策略被分发，请设置

      * `Acl Handling:` `IGNORE`

![Vault Package Builder工厂](assets/vault-package-builder-factory.png)

## 当……发生时 {#what-happens-when}

### 发布时用户自行注册或编辑配置文件 {#user-self-registers-or-edits-profile-on-publish}

根据设计，在发布环境（自注册）中创建的用户和配置文件不会显示在创作环境中。

当拓扑为 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm) 和用户同步已正确配置， *用户* 和 *用户配置文件* 使用Sling分发跨发布场同步。

### 用户或用户组是使用安全控制台创建的 {#users-or-user-groups-are-created-using-security-console}

根据设计，在发布环境中创建的用户数据不会出现在创作环境中，反之亦然。

当 [用户管理和安全性](/help/sites-administering/security.md) console用于在发布环境中添加新用户，如有必要，用户同步会将新用户及其组成员资格同步到其他发布实例。 用户同步还会同步通过安全控制台创建的用户组。

## 疑难解答 {#troubleshooting}

### 如何让用户同步脱机 {#how-to-take-user-sync-offline}

要将用户同步脱机，请转到 [删除发布实例](#how-to-remove-a-publish-instance) 或 [手动同步数据](#manually-syncing-users-and-user-groups)，分发队列必须为空且安静。

检查分发队列的状态：

* 对于作者：

   * 使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 在中查找条目 `/var/sling/distribution/packages`

         * 使用模式命名的文件夹节点 `distrpackage_*`

   * 使用 [包管理器](/help/sites-administering/package-manager.md)

      * 查找挂起的包（尚未安装）

         * 使用模式命名 `socialpubsync-vlt*`
         * 创建者 `communities-user-admin`

当分发队列为空时，禁用用户同步：

* 在作者上

   * *取消选中*the `Enabled` 复选框 [Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)

完成任务后，要重新启用用户同步，请执行以下操作：

* 在作者上

   * 查看 `Enabled` 复选框 [Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)

### 使用同步诊断 {#user-sync-diagnostics}

用户同步诊断是一种检查配置并尝试识别任何问题的工具。

在作者中，只需从主控制台导航到 **工具、操作、诊断、用户同步诊断。**

只需进入“User Sync Diagnostics（用户同步诊断）”控制台即可显示结果。

这是未启用用户同步时显示的内容：

![未启用用户同步诊断的警告](assets/chlimage_1-28.png)

#### 如何为发布实例运行诊断 {#how-to-run-diagnostics-for-publish-instances}

从创作环境运行诊断时，通过/失败结果包括 [信息] 部分显示已配置的发布实例列表以进行确认。

列表中包括运行该实例诊断的每个发布实例的URL。 url参数 `syncUser` 会附加到诊断URL中，其值设置为 *授权同步用户* 创建于 [步骤2](#createauthuser).

**注意**：在启动URL之前， *授权同步用户* 必须已登录到发布实例。

![发布实例的诊断](assets/chlimage_1-29.png)

### 未正确添加配置 {#configuration-improperly-added}

当用户同步失败时，最常见的问题是额外的配置是 *已添加*. 相反，*existing *default配置应该是 *已编辑*.

以下是有关已编辑的默认配置应如何显示在Web控制台中的视图。 如果出现多个实例，则应删除添加的配置。

#### （作者）一个Apache Sling分发代理 — 同步代理工厂 {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-30.png)

#### （作者）一个Apache Sling分发传输凭据 — 基于用户凭据的DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-31.png)

#### （发布）一个Apache Sling分发代理 — 队列代理工厂 {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-32.png)

#### （发布）一个Adobe Social同步 — 观察者工厂差异 {#publish-one-adobe-social-sync-diff-observer-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-33.png)

#### （作者）一个Apache Sling Distribution Trigger — 计划触发器工厂 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![已编辑，Web控制台中的默认配置视图](assets/chlimage_1-34.png)

### 处理响应期间修改操作异常 {#modify-operation-exception-during-response-processing}

如果日志中显示以下内容：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然后验证部分 [2. 创建授权用户](#createauthuser) 被恰如其分地跟踪了。

本节介绍如何创建存在于所有Publish实例上的授权用户，以及在作者的“机密提供程序”OSGi配置中标识这些用户。 默认情况下，用户为 `admin`.

授权用户应成为 **`administrators`** 不应更改该组的用户组和权限。

授权用户对所有Publish实例应明确具有以下权限和限制：

| **path** | **jcr：all** | **rep：glob** |
|---|---|---|
| /home | X | &#42;/活动/&#42; |
| /home/users | X | &#42;/活动/&#42; |
| /home/groups | X | &#42;/活动/&#42; |

作为 `administrators` 组，授权用户应对所有Publish实例具有以下权限：

| **path** | **jcr：all** | **jcr：read** | **rep：write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 用户组同步失败 {#user-group-sync-failed}

如果Sling ID在两个或更多发布实例之间匹配，则用户组同步失败。

请参阅部分 [9. 唯一Sling ID](#unique-sling-id)

### 手动同步用户和用户组 {#manually-syncing-users-and-user-groups}

* 在存在用户和用户组的发布实例上：

   * [如果启用，则禁用用户同步](#how-to-take-user-sync-offline)
   * [创建资源包](/help/sites-administering/package-manager.md#creating-a-new-package) 之 `/home`

      * 编辑包时

         * 筛选器选项卡：添加筛选器：根路径： `/home`
         * 高级选项卡：AC处理： `Overwrite`

   * [导出资源包](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* 在其他Publish实例上：

   * [导入资源包](/help/sites-administering/package-manager.md#installing-packages)

要配置或启用用户同步，请转到步骤1： [Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)

### 当发布实例变得不可用时 {#when-a-publish-instance-becomes-unavailable}

当发布实例变得不可用时，如果它将来重新联机，则不应删除该实例。 更改将排队等候发布实例，当它重新联机时，将处理更改。

如果发布实例从不重新联机，如果它永久脱机，则必须将其删除，因为队列累积会导致在创作环境中显着占用磁盘空间。

当发布实例关闭时，创作日志会出现与以下内容类似的异常：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何删除发布实例 {#how-to-remove-a-publish-instance}

要从删除发布实例 [Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)，分发队列必须为空且安静。

* 对于作者：

   * [使用户同步脱机](#how-to-take-user-sync-offline)
   * 关注 [步骤7](#apache-sling-distribution-agent-sync-agents-factory) 要从两个服务器列表中删除发布实例，请执行以下操作：

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * 重新启用用户同步

      * 查看 `Enabled` 复选框 [Apache Sling分发代理 — 同步代理工厂](#apache-sling-distribution-agent-sync-agents-factory)
