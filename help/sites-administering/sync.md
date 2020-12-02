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
source-git-commit: 8ed7409740cdd3e45fad006dc6e470a06acc60fe
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 2%

---


# 用户同步{#user-synchronization}

## 简介 {#introduction}

当部署为[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)时，成员需要能够登录并查看其任何发布节点上的数据。

在发布环境中创建的用户和用户组（用户数据）在创作环境中不是必需的。

在创作环境中创建的大多数用户数据都打算保留在创作环境中，而不是复制到发布实例。

在一个发布实例上进行的注册和修改需要与其他发布实例同步，以便它们能够访问同一用户数据。

从AEM 6.1开始，启用用户同步后，用户数据将自动在场中的发布实例间同步，而不是在作者身上创建。

## Sling分发{#sling-distribution}

用户数据及其[ACL](/help/sites-administering/security.md)存储在[Oak Core](/help/sites-deploying/platform.md)中，即Oak JCR下的层，并使用[Oak API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)进行访问。 如果更新不频繁，则使用[Sling内容分发](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md)（Sling分发）将用户数据与其他发布实例同步是合理的。

与传统复制相比，使用Sling分发进行用户同步的好处有：

* *用户*、用 *户概* 要文件和 *在发布* 时创建的用户组不是在作者上创建的

* Sling分发在jcr事件中设置属性，使得可以在发布端事件监听器中执行操作，而无需考虑无限的复制循环
* Sling分发仅将用户数据发送到非源发布实例，消除了不必要的流量
* [同](/help/sites-administering/security.md) 步中包含用户节点中的ACLset

>[!NOTE]
>
>如果需要会话，建议使用SSO解决方案，或使用粘性会话，并在客户切换到其他发布者时让其登录。

>[!CAUTION]
>
>不支持&#x200B;***administrators***&#x200B;组的同步，即使启用了用户同步。 相反，“导入差异”失败将记录在错误日志中。
>
>因此，当部署是发布场时，如果用户被添加到***administrators**&#x200B;组或从中删除，则必须在每个发布实例上手动进行修改。

## 启用用户同步{#enable-user-sync}

>[!NOTE]
>
>默认情况下，用户同步为`disabled`。
>
>启用用户同步涉及修改&#x200B;*现有* OSGi配置。
>
>不应因启用用户同步而添加新配置。

用户同步依赖于作者环境来管理用户数据分发，即使用户数据不是在作者身上创建的。 许多（但并非全部）配置都发生在创作环境中，每个步骤都清楚地标识是在创作还是发布时执行。

以下是启用用户同步所需的步骤，后面是[疑难解答](#troubleshooting)部分：

### 前提条件 {#prerequisites}

1. 如果用户和用户组已在一个发布者上创建，建议在配置和启用用户同步之前，[手动将用户数据同步](#manually-syncing-users-and-user-groups)到所有发布者。

启用用户同步后，仅新创建的用户和用户组会进行同步。

1. 确保已安装最新代码：

* [AEM平台更新](https://helpx.adobe.com/cn/experience-manager/kb/aem62-available-hotfixes.html)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent —— 同步代理工厂{#apache-sling-distribution-agent-sync-agents-factory}

**启用用户同步**

* **在作者**

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位`Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）
验证`name`:**`socialpubsync`**

      * 选中`Enabled`复选框
      * 选择`Save`


![](assets/chlimage_1-20.png)

### 2.创建授权用户{#createauthuser}

**配置**
权限此授权用户将在步骤3中用于配置创作时的Sling分发。

* **在每个发布实例上**

   * 以管理员权限登录
   * 访问[安全控制台](/help/sites-administering/security.md)

      * 例如[https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * 创建新用户

      * 例如`usersync-admin`
   * 将此用户添加到&#x200B;**`administrators`**&#x200B;用户组
   * [将此用户的ACL添加到/home](#howtoaddacl)

      * `Allow jcr:all` 限制  `rep:glob=*/activities/*`



>[!CAUTION]
>
>必须创建新用户。
>
>* 分配的默认用户为&#x200B;**`admin`**。
>* 不使用`communities-user-admin user.`

>



#### 如何添加ACL {#addacls}

* 访问CRXDE Lite

   * 例如[https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 选择`/home`节点
* 在右窗格中，选择`Access Control`选项卡
* 选择`+`按钮以添加ACL项

   * **主要**: *搜索为用户同步创建的用户*
   * **类型**: `Allow`
   * **特权**:  `jcr:all`
   * **限** 制代表：glob:  `*/activities/*`
   * 选择&#x200B;**确定**

* 选择&#x200B;**全部保存**

![](assets/chlimage_1-21.png)

另请参阅

* [访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 疑难解答部分[在响应处理过程中修改操作异常](#modify-operation-exception-during-response-processing)。

### 3.AdobeGranite分发——加密密码传输机密提供程序{#adobegraniteencpasswrd}

**配置权限**

在所有发布实例上创建了授权用户**`administrators`**用户组的成员后，必须在作者身上将该授权用户识别为具有从作者同步用户数据到发布的权限。

* **在作者**

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位`com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * 选择要打开进行编辑的现有配置（铅笔图标）
验证`property name`:**`socialpubsync-publishUser`**

   * 在步骤2中将用户名和密码设置为在发布时创建的[授权用户](#createauthuser)

      * 例如`usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent —— 队列代理工厂{#apache-sling-distribution-agent-queue-agents-factory}

**启用用户同步**

* **在发布**:

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 定位`Apache Sling Distribution Agent - Queue Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）
验证`Name`:`socialpubsync-reverse`

      * 选中`Enabled`复选框
      * 选择`Save`
   * **重复**



![](assets/chlimage_1-23.png)

### 5.Adobe Social同步——差异观察器工厂{#diffobserver}

**启用组同步**

* **在每个发布实例上**:

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 定位&#x200B;**`Adobe Social Sync - Diff Observer Factory`**

      * 选择要打开进行编辑的现有配置（铅笔图标）

         验证 `agent name`: `socialpubsync-reverse`

      * 选中`Enabled`复选框
      * 选择`Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling分发触发器——计划触发器工厂{#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（可选）修改轮询间隔**

默认情况下，作者每30秒对更改进行轮询一次。 要更改此间隔：

* **在作者**

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位`Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）

         * 验证 `Name`: `socialpubsync-scheduled-trigger`
      * 将`Interval in Seconds`设置为所需的间隔
      * 选择`Save`



![](assets/chlimage_1-24.png)

## 为多个发布实例配置{#configure-for-multiple-publish-instances}

默认配置用于单个发布实例。 由于启用用户同步的原因是同步多个发布实例（如发布场），因此需要将其他发布实例添加到同步代理工厂。

### 7. Apache Sling Distribution Agent —— 同步代理工厂{#apache-sling-distribution-agent-sync-agents-factory-1}

**添加发布实例：**

* **在作者**

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 定位`Apache Sling Distribution Agent - Sync Agents Factory`

      * 选择要打开进行编辑的现有配置（铅笔图标）
验证`Name`:`socialpubsync`


![](assets/chlimage_1-25.png)

* **导出**
器端点每个发布者应有一个导出器端点。例如，如果有2个发布者，localhost:4503和4504，则应有2个条目：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **导入**
程序端点每个发布者应有一个导入程序端点。例如，如果有2个发布者，localhost:4503和4504，则应有2个条目：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 选择`Save`

### 8.AEM Communities用户同步监听器{#aem-communities-user-sync-listener}

**（可选）同步其他JCR节点**

如果有自定义数据需要在多个发布实例之间同步，则：

* **在每个发布实例上**:

   * 以管理员权限登录
   * 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如`https://localhost:4503/system/console/configMgr`
   * 定位`AEM Communities User Sync Listener`
   * 选择要打开进行编辑的现有配置（铅笔图标）
验证`Name`:`socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **节点**
类型这是要同步的节点类型的列表。除sling:Folder以外的任何节点类型都需要在此列出（sling:folder是单独处理的）。
要同步的节点类型的默认列表:

   * rep：用户
   * nt:unstructured
   * nt：资源

* **可忽**
略属性这是在检测到任何更改时将忽略的属性列表。对这些属性所做的更改可能会作为其他更改的副作用进行同步（因为同步始终处于节点级别），但对这些属性所做的更改本身不会触发同步。
要忽略的默认属性：

   * cq:lastModified

* **可忽略**
的节点在同步过程中将完全忽略的子路径。这些子路径下的任何内容将随时同步。
要忽略的默认节点：

   * .tokens
   * 系统

* **分布**
式文件夹大多数sling：文件夹被忽略，因为不需要同步。此处列出了少数例外。
要同步的默认文件夹

   * 细分／评分
   * 社交／关系
   * 活动

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在两个或多个发布实例之间匹配，则用户组同步将失败。

如果发布场中多个发布实例的Sling ID相同，则用户组将不会同步。

要验证所有Sling ID值是否不同，请在每个发布实例上：

1. 浏览至`http://<host>:<port>/system/console/status-slingsettings`
1. 检查&#x200B;**Sling ID**&#x200B;的值

![](assets/chlimage_1-27.png)

如果发布实例的Sling ID与任何其他发布实例的Sling ID匹配，则：

1. 停止具有匹配Sling ID的发布实例之一
1. 在crx-quickstart/launchpad/felix目录中

   * 搜索并删除名为&#x200B;*sling.id.file*&#x200B;的文件

      * 例如，在Linux系统上：
         `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系统上：
         `use windows explorer and search for *sling.id.file*`

1. 开始发布实例

   * 启动时，将为其分配一个新的Sling ID

1. 验证&#x200B;**Sling ID**&#x200B;现在是唯一的

重复这些步骤，直到所有发布实例都具有唯一的Sling ID。

## Vault Package Builder工厂{#vault-package-builder-factory}

为了使更新正确同步，必须修改用于用户同步的保险存储包生成器：

* 在每个AEM发布实例上
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 选择编辑图标
* 添加两个`Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 策略处理：

   * 要用新节点覆盖现有rep:policy节点，请添加第三个包过滤器：

      * `/home/users|+.*/rep:policy`
   * 要防止策略被分发，请设置

      * `Acl Handling:` `IGNORE`


![保管库包生成器工厂](assets/vault-package-builder-factory.png)

## 当…… {#what-happens-when}时会发生什么情况

### 发布{#user-self-registers-or-edits-profile-on-publish}时用户自注册或编辑用户档案

根据设计，在发布环境（自注册）中创建的用户和用户档案不会显示在创作环境中。

当拓扑为[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)且用户同步已正确配置时，使用Sling分发在发布场上同步*user *和&#x200B;*用户用户档案*。

### 用户或用户组是使用安全控制台{#users-or-user-groups-are-created-using-security-console}创建的

根据设计，在发布环境中创建的用户数据不会显示在创作环境中，反之亦然。

当使用[用户管理和安全](/help/sites-administering/security.md)控制台在发布环境中添加新用户时，用户同步将根据需要将新用户及其组成员关系同步到其他发布实例。 用户同步还将同步通过安全控制台创建的用户组。

## 疑难解答 {#troubleshooting}

### 如何使用户同步脱机{#how-to-take-user-sync-offline}

要使用户同步脱机，[要删除发布者](#how-to-remove-a-publisher)或[手动同步数据](#manually-syncing-users-and-user-groups)，分发队列必须为空且安静。

要检查分发队列的状态，请执行以下操作：

* 作者：

   * 使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 在`/var/sling/distribution/packages`中查找条目

         * 使用模式`distrpackage_*`命名的文件夹节点
   * 使用[包管理器](/help/sites-administering/package-manager.md)

      * 查找挂起的包（尚未安装）

         * 以模式`socialpubsync-vlt*`命名
         * 由`communities-user-admin`创建


当分发队列为空时，禁用用户同步：

* 在作者

   * *取消选中[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框

完成任务后，要重新启用用户同步：

* 在作者

   * 选中[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框

### 使用同步诊断 {#user-sync-diagnostics}

用户同步诊断是检查配置并尝试识别任何问题的工具。

在创作时，只需通过&#x200B;**工具、操作、诊断、用户同步诊断从主控制台导航。**

只需输入“用户同步诊断”控制台，即会显示结果。

这是未启用用户同步时显示的内容：

![](assets/chlimage_1-28.png)

#### 如何为发布者运行诊断{#how-to-run-diagnostics-for-publishers}

当从作者环境运行诊断时，通过／失败结果将包括[INFO]部分，显示已配置发布实例的列表以进行确认。

该列表中包含每个发布实例的URL，该实例将运行该实例的诊断。 url参数`syncUser`被附加到诊断URL中，其值设置为在[步骤2](#createauthuser)中创建的&#x200B;*授权同步用户*。

**注意**:在启动URL之前，授 *权的* sync用户必须已登录到该发布实例。

![](assets/chlimage_1-29.png)

### 配置添加不正确{#configuration-improperly-added}

当用户同步失败时，最常见的问题是额外的配置是&#x200B;*added*。 相反，*现有的*default配置应该已编辑&#x200B;**。

以下是编辑后默认配置在Web控制台中的显示方式视图。 如果出现多个实例，则应删除添加的配置。

#### (author)一个Apache Sling Distribution Agent —— 同步代理工厂{#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### （作者）一个Apache Sling Distribution Transport Credentials —— 基于用户凭据的DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### （发布）一个Apache Sling Distribution Agent —— 队列代理工厂{#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### （发布）一个Adobe Social同步——比较观察器工厂{#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (author)一个Apache Sling分发触发器——计划触发器工厂{#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### 在响应处理{#modify-operation-exception-during-response-processing}期间修改操作异常

如果日志中显示以下内容：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然后验证部分[2。 正确遵循“创建授权用户](#createauthuser)”。

本节介绍如何创建在所有发布实例上存在的授权用户，并在作者的“机密提供者”OSGi配置中识别这些用户。 默认情况下，用户为`admin`。

授权用户应成为&#x200B;**`administrators`**&#x200B;用户组的成员，该用户组的权限不应更改。

授权用户应对所有发布实例明确具有以下权限和限制：

| **路径** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */活动/* |
| /home/users | X | */活动/* |
| /home/groups | X | */活动/* |

作为`administrators`组的成员，授权用户应对所有发布实例具有以下权限：

| **路径** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 用户组同步失败{#user-group-sync-failed}

如果Sling ID在两个或多个发布实例之间匹配，则用户组同步将失败。

请参见第[9节。 唯一Sling ID](#unique-sling-id)

### 手动同步用户和用户组{#manually-syncing-users-and-user-groups}

* 在存在用户和用户组的发布者上：

   * [如果启用，则禁用用户同步](#how-to-take-user-sync-offline)
   * [创建](/help/sites-administering/package-manager.md#creating-a-new-package) 包  `/home`

      * 编辑包时

         * 过滤器选项卡：添加过滤器：根路径：`/home`
         * 高级选项卡：交流处理：`Overwrite`
   * [导出包](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* 在其他发布实例上：

   * [导入包](/help/sites-administering/package-manager.md#installing-packages)

要配置或启用用户同步，请转至步骤1:[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)

### 当发布者变为不可用时{#when-a-publisher-becomes-unavailable}

当发布实例不可用时，如果它将来恢复联机状态，则不应删除它。 更改将排队等待发布者，一旦它重新联机，将处理更改。

如果发布实例永远不会恢复联机状态，如果它永久脱机，则必须删除它，因为队列累积将导致作者环境中出现明显的磁盘空间使用。

当发布者关闭时，创作日志将具有与以下内容类似的异常：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何删除发布者{#how-to-remove-a-publisher}

要从[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)中删除发布者，分发队列必须为空且安静。

* 作者：

   * [使用户脱机同步](#how-to-take-user-sync-offline)
   * 按照[步骤7](#apache-sling-distribution-agent-sync-agents-factory)从两个服务器列表中删除发布者：

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * 重新启用用户同步

      * 选中[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`复选框
