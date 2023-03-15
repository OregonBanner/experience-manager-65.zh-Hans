---
title: 复制
seo-title: Replication
description: 了解如何在AEM中配置和监视复制代理。
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 5%

---

# 复制{#replication}

复制代理是Adobe Experience Manager (AEM)的核心，因为该机制可用于：

* [发布（激活）](/help/sites-authoring/publishing-pages.md#activatingcontent) 内容从创作环境到发布环境。
* 明确刷新Dispatcher缓存中的内容。
* 将用户输入（例如，表单输入）从发布环境返回到创作环境（在创作环境控制下）。

请求为 [已排队](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) 到相应的代理以进行处理。

>[!NOTE]
>
>用户数据（用户、用户组和用户配置文件）不会在创作实例和发布实例之间复制。
>
>对于多个发布实例，用户数据在以下情况下是Sling分发的： [用户同步](/help/sites-administering/sync.md) 已启用。

## 从创作复制到发布 {#replicating-from-author-to-publish}

向发布实例或Dispatcher的复制分几个步骤进行：

* 作者请求发布（激活）某些内容；这可以由手动请求或预配置的自动触发器启动。
* 该请求将传递到相应的默认复制代理；一个环境可以具有多个默认代理，这些代理将始终被选择用于此类操作。
* 复制代理将内容“打包”并放置在复制队列中。
* 在网站选项卡中， [彩色状态指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) 为单个页面设置。
* 内容会从队列中提升，并使用配置的协议传输到发布环境；通常这是HTTP。
* 发布环境中的servlet接收请求并发布接收到的内容；默认servlet为 `https://localhost:4503/bin/receive`.

* 可以配置多个创作和发布环境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 从发布复制到作者 {#replicating-from-publish-to-author}

某些功能允许用户在发布实例上输入数据。

在某些情况下，需要一种称为反向复制的复制类型，将此数据返回到创作环境，之后再从创作环境分发到其他发布环境。 出于安全考虑，必须严格控制从发布到创作环境的任何流量。

反向复制在引用创作环境的发布环境中使用代理。 此代理将数据放入发件箱。 此发件箱与创作环境中的复制侦听器匹配。 监听器轮询发件箱以收集输入的任何数据，然后根据需要进行分发。 这可确保创作环境控制所有流量。

在其他情况下，例如对于Communities功能（例如，论坛、博客、评论和评论），在发布环境中输入的用户生成内容(UGC)量很难使用复制功能在AEM实例之间有效同步。

AEM [Communities](/help/communities/overview.md) 从不对UGC使用复制。 相反，Communities的部署需要用于UGC的公用存储(请参阅 [社区内容存储](/help/communities/working-with-srp.md))。

### 复制 — 开箱即用 {#replication-out-of-the-box}

AEM的标准安装中包含的we-retail网站可用于说明复制。

要遵循此示例并使用默认复制代理，您需要 [安装AEM](/help/sites-deploying/deploy.md) 替换为：

* 端口上的创作环境 `4502`
* 端口上的发布环境 `4503`

>[!NOTE]
>
>默认为已启用 :
>
>* 作者代理：默认代理（发布）
>
>默认情况下有效禁用(自AEM 6.1起)：
>
>* 创作代理：反向复制代理(publish_reverse)
>* 发布代理：反向复制（发件箱）
>
>要检查代理或队列的状态，请使用 **工具** 控制台。
>参见 [监视复制代理](#monitoring-your-replication-agents).

#### 复制（创作到发布） {#replication-author-to-publish}

1. 导航到创作环境上的支持页面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 编辑页面以添加一些新文本。
1. **激活页面** 以发布更改。
1. 在发布环境中打开支持页面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 您现在可以看到您对作者输入的更改。

此复制操作由以下人员从创作环境执行：

* **默认代理（发布）**
此代理将内容复制到默认发布实例。
可从创作环境的“工具”控制台访问此项（配置和日志）的详细信息；或：

   `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 复制代理 — 开箱即用 {#replication-agents-out-of-the-box}

标准AEM安装中提供了以下代理：

* [默认代理](#replication-author-to-publish)
用于从创作复制到发布。

* Dispatcher刷新用于管理Dispatcher缓存。 参见 [使创作环境中的Dispatcher缓存失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) 和 [使发布实例中的Dispatcher缓存失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) 了解更多信息。

* [反向复制](#reverse-replication-publish-to-author)
用于从发布复制到作者。 反向复制不用于Communities功能，例如论坛、博客和评论。 由于未启用发件箱，因此该功能实际上已被禁用。 使用反向复制需要自定义配置。

* 静态代理这是一个“将节点的静态表示存储在文件系统中的代理”。
例如，使用默认设置时，内容页面和DAM资产存储在 `/tmp`，作为HTML或相应的资源格式。 请参阅 `Settings` 和 `Rules` 选项卡进行配置。
这是请求的，以便当直接从应用程序服务器请求页面时，可以看到内容。 这是一个专用代理，（可能）在大多数情况下不需要它。

## 复制代理 — 配置参数 {#replication-agents-configuration-parameters}

从“工具”控制台配置复制代理时，对话框中提供了四个选项卡：

### 设置 {#settings}

* **名称**

   复制代理的唯一名称。

* **描述**

   此复制代理将提供的用途的说明。

* **启用**

   指示复制代理当前是否已启用。

   当代理处于 **已启用** 队列将显示为：

   * **活动** 处理项目时。
   * **空闲** 队列为空时。
   * **已阻止** 当项目在队列中，但无法进行处理时；例如，当接收队列被禁用时。

* **序列化类型**

   序列化的类型：

   * **默认**：设置是否自动选择代理。
   * **Dispatcher刷新**：如果要使用代理刷新Dispatcher缓存，请选择此选项。

* **重试延迟**

   如果遇到问题，两次重试之间的延迟（等待时间，以毫秒为单位）。

   默认: `60000`

* **代理用户 ID**

   根据环境，代理将使用此用户帐户来：

   * 从创作环境收集内容并将其打包
   * 在发布环境中创建和编写内容

   将此字段留空将使用系统用户帐户(在sling中定义为管理员用户的帐户；默认情况下，这是 `admin`)。

   >[!CAUTION]
   >
   >对于创作环境中的代理，此帐户为 *必须* 对要复制的所有路径具有读取访问权限。

   >[!CAUTION]
   >
   >对于发布环境中的代理，此帐户为 *必须* 具有复制内容所需的创建/写入权限。

   >[!NOTE]
   >
   >这可用作选择复制特定内容的机制。

* **日志级别**

   指定日志消息使用的详细级别。

   * `Error`：仅记录错误
   * `Info`：将记录错误、警告和其他信息性消息
   * `Debug`：将在消息中使用高级别的详细信息，主要用于调试目的

   默认: `Info`

* **使用反转复制**

   指示此代理是否将用于反向复制；将用户输入从发布环境返回到创作环境。

* **别名更新**

   选择此选项可启用对Dispatcher的别名或虚名路径失效请求。 另请参阅 [配置Dispatcher刷新代理](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### 传输 {#transport}

* **URI**

   这会指定目标位置的接收servlet。 特别是，您可以在此处指定目标实例的主机名（或别名）和上下文路径。

   例如：

   * 默认代理可以复制到 `https://localhost:4503/bin/receive`
   * Dispatcher Flush代理可能会复制到 `https://localhost:8000/dispatcher/invalidate.cache`

   此处指定的协议（HTTP或HTTPS）将确定传输方法。

   对于Dispatcher Flush代理，仅当您使用基于路径的虚拟主机条目来区分场时，才使用URI属性，您可以使用此字段来定位要使其失效的场。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用 URL `/path1/invalidate.cache` 定位第一个场，使用 `/path2/invalidate.cache` 定位第二个场。

* **用户**

   用于访问目标的帐户的用户名。

* **密码**

   用于访问目标的帐户的密码。

* **NTLM 域**

   NTML身份验证的域。

* **NTLM 主机**

   用于NTML身份验证的主机。

* **启用宽松 SSL**

   如果希望接受自认证SSL证书，则启用。

* **允许过期的证书**

   如果希望接受过期的SSL证书，则启用。

#### 代理 {#proxy}

仅在需要代理时才需要以下设置：

* **代理主机**

   用于传输的代理的主机名。

* **代理端口**

   代理的端口。

* **代理用户**

   要使用的帐户的用户名。

* **代理密码**

   要使用的帐户的密码。

* **代理 NTLM 域**

   代理NTLM域。

* **代理·NTLM 主机**

   代理NTLM域。

#### 扩展 {#extended}

* **接口**

   您可以在此处定义要绑定的套接字接口。

   这会设置创建连接时要使用的本地地址。 如果未设置，将使用默认地址。 这对于指定要在多宿主系统或群集系统上使用的接口非常有用。

* **HTTP 方法**

   要使用的HTTP方法。

   对于Dispatcher Flush代理，这几乎总是GET，不应更改(POST是另一个可能的值)。

* **HTTP 头**

   它们用于Dispatcher Flush代理，并指定必须刷新的元素。

   对于Dispatcher Flush代理，不需要更改三个标准条目：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   在刷新句柄或路径时，会酌情使用这些参数来指示要使用的操作。 子参数是动态的：

   * `{action}` 表示复制操作

   * `{path}` 指示路径

   与请求相关的路径/操作将替换它们，因此无需“硬编码”：

   >[!NOTE]
   >
   >如果您在推荐的默认上下文以外的其他上下文中安装了AEM，则需要在HTTP标头中注册该上下文。 例如：
   >`CQ-Handle:/<*yourContext*>{path}`

* **关闭连接**

   启用可在每次请求后关闭连接。

* **连接超时**

   尝试建立连接时应用的超时（以毫秒为单位）。

* **套接字超时**

   建立连接后等待流量时应用的超时（以毫秒为单位）。

* **协议版本**

   协议的版本；例如 `1.0` 适用于HTTP/1.0的。

#### 触发器 {#triggers}

这些设置用于定义自动复制的触发器：

* **忽略默认值**

   如果选中，代理将从默认复制中排除；这意味着如果内容作者发出复制操作，将不使用该代理。

* **修改**

   在此，修改页面时将自动触发此代理的复制。 这主要用于Dispatcher Flush代理，但也用于反向复制。

* **在分发时**

   如果选中，代理将在修改时自动复制标记为分发的任何内容。

* **已达到开启/关闭时间**

   当为页面定义的时间或间隔发生时，这将触发自动复制（根据需要激活或取消激活页面）。 这主要用于Dispatcher Flush代理。

* **接收时**

   如果选中，代理将在收到复制事件时进行链式复制。

* **无状态更新**

   选中后，代理将不会强制复制状态更新。

* **无版本控制**

   选中后，代理将不会强制对已激活的页面进行版本控制。

## 配置复制代理 {#configuring-your-replication-agents}

有关使用MSSL将复制代理连接到发布实例的信息，请参阅 [使用双向SSL进行复制](/help/sites-deploying/mssl-replication.md).

### 从创作环境配置复制代理 {#configuring-your-replication-agents-from-the-author-environment}

在创作环境的Tools选项卡中，您可以配置驻留在任一创作环境中的复制代理(**作者代理**)或发布环境(**发布时的代理**)。 以下过程说明了为创作环境配置Agent，但可用于两者。

>[!NOTE]
>
>当Dispatcher处理创作或发布实例的HTTP请求时，来自复制代理的HTTP请求必须包含PATH标头。 除了以下过程外，还必须将PATH标头添加到客户端标头的Dispatcher列表中。 (请参阅 [/clientheaders（客户端标头）](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

1. 访问 **工具** AEM选项卡。
1. 单击 **复制** （左窗格以打开文件夹）。
1. 双击 **作者代理** （左窗格或右窗格）。
1. 单击相应的代理名称（一个链接）以显示有关该代理的详细信息。
1. 单击 **编辑** 要打开“配置”对话框，请执行以下操作：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值应足以用于默认安装。 如果您进行了更改，请单击 **确定** 以保存它们(请参阅 [复制代理 — 配置参数](#replication-agents-configuration-parameters) 了解各个参数的更多详细信息)。

>[!NOTE]
>
>AEM的标准安装指定 `admin` 作为默认复制代理中传输凭据的用户。
>
>这应该更改为站点特定的复制用户帐户，该帐户具有复制所需路径的权限。

### 配置反向复制 {#configuring-reverse-replication}

反向复制用于将发布实例上生成的用户内容取回创作实例。 这通常用于调查表和登记表等功能。

出于安全原因，大多数网络拓扑都不允许连接 *起始日期* “非军事区”(将外部服务公开给不受信任的网络（如Internet）的子网络)。

由于发布环境通常位于DMZ中，因此要将内容返回创作环境，必须从创作实例启动连接。 此操作可通过以下方式完成：

* 一个 *发件箱* 在放置内容的发布环境中。
* 创作环境中的代理（发布），定期轮询发件箱以获取新内容。

>[!NOTE]
>
>对于AEM [Communities](/help/communities/overview.md)，复制不适用于发布实例上用户生成的内容。 参见 [社区内容存储](/help/communities/working-with-srp.md).

为此，您需要：

**创作环境中的反向复制代理** 它充当活动组件，从发布环境中的发件箱中收集信息：

如果要使用反向复制，请确保已激活此代理。

![chlimage_1-23](assets/chlimage_1-23.png)

**发布环境中的反向复制代理（发件箱）** 这是被动元素，因为它充当“发件箱”。 用户输入放置在此处，代理从此处在创作环境中收集用户输入。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 为多个发布实例配置复制 {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>仅复制内容 — 不复制用户数据（用户、用户组和用户配置文件）。
>
>要在多个发布实例之间同步用户数据，请启用 [用户同步](/help/sites-administering/sync.md).

在安装时，已配置默认代理以将内容复制到本地主机的端口4503上运行的发布实例。

要为其他发布实例配置内容复制，您需要创建和配置新的复制代理：

1. 打开 **工具** AEM选项卡。
1. 选择 **复制**，则 **作者代理** （在左侧面板中）。
1. 选择 **新建……**.
1. 设置 **标题** 和 **名称**，然后选择 **复制代理**.
1. 单击 **创建** 以创建新代理。
1. 双击新代理项目以打开配置面板。
1. 单击 **编辑** - **代理设置** 随即会打开对话框 —  **序列化类型** 已定义为默认，必须保持此状态。

   * 在 **设置** 选项卡：

      * 激活 **已启用**.
      * 输入&#x200B;**说明**.
      * 设置 **重试延迟** 到 `60000`.

      * 保留 **序列化类型** 作为 `Default`.
   * 在 **传输** 选项卡：

      * 输入新发布实例所需的URI；例如，
         `https://localhost:4504/bin/receive`。

      * 输入用于复制的站点特定用户帐户。
      * 您可以根据需要配置其他参数。


1. 单击 **确定** 以保存设置。

然后，您可以通过更新、发布创作环境中的页面来测试操作。

更新将显示在如上配置的所有发布实例上。

如果您遇到任何问题，可以检查创作实例上的日志。 根据所需的详细程度，您还可以设置 **日志级别** 到 `Debug` 使用 **代理设置** 对话框（如上所述）。

>[!NOTE]
>
>这可以结合使用 [代理用户ID](#agentuserid) 以选择不同的内容以复制到各个发布环境。 对于每个发布环境：
>
>1. 配置复制代理以复制到该发布环境。
>1. 配置用户帐户；具有读取将复制到该特定发布环境的内容所需的访问权限。
>1. 将用户帐户分配为 **代理用户ID** 用于复制代理。

>


### 配置Dispatcher刷新代理 {#configuring-a-dispatcher-flush-agent}

默认代理包含在安装中。 但是，仍需要某些配置，如果您定义新代理，同样需要这些配置：

1. 打开 **工具** AEM选项卡。
1. 单击 **部署**.
1. 选择 **复制** 然后 **发布时的代理**.
1. 双击 **Dispatcher刷新** 打开概述的项目。
1. 单击 **编辑** - **代理设置** 此时将打开对话框：

   * 在 **设置** 选项卡：

      * 激活 **已启用**.
      * 输入&#x200B;**说明**.
      * 保留 **序列化类型** 作为 `Dispatcher Flush`，或者在创建新代理时进行此设置。

      * （可选）选择 **别名更新** 启用对Dispatcher的别名或虚名路径失效请求。
   * 在 **传输** 选项卡：

      * 输入新发布实例所需的URI；例如，
         `https://localhost:80/dispatcher/invalidate.cache`。

      * 输入用于复制的站点特定用户帐户。
      * 您可以根据需要配置其他参数。

   对于Dispatcher Flush代理，仅当您使用基于路径的虚拟主机条目来区分场时，才使用URI属性，您可以使用此字段来定位要使其失效的场。 例如，场 #1 的虚拟主机为 `www.mysite.com/path1/*`，场 #2 的虚拟主机为 `www.mysite.com/path2/*`。您可以使用 URL `/path1/invalidate.cache` 定位第一个场，使用 `/path2/invalidate.cache` 定位第二个场。

   >[!NOTE]
   >
   >如果您在推荐的默认上下文以外的其他上下文中安装了AEM，则需要配置 [HTTP标头](#extended) 在 **扩展** 选项卡。

1. 单击&#x200B;**确定**&#x200B;以保存更改。
1. 返回到 **工具** 选项卡，从此处您可以 **激活** 此 **Dispatcher刷新** 代理(**发布时的代理**)。

此 **Dispatcher刷新** 复制代理在创作上非活动。 您可以使用等效的URI在发布环境中访问同一页面；例如， `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### 控制对复制代理的访问 {#controlling-access-to-replication-agents}

对用于配置复制代理的页面的访问可通过对的用户和/或组页面权限进行控制 `etc/replication` 节点。

>[!NOTE]
>
>设置此类权限不会影响用户复制内容（例如，从网站控制台或Sidekick选项）。 复制框架在复制页面时，不使用当前用户的“用户会话”来访问复制代理。

### 从CRXDE Lite配置复制代理 {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>仅支持在中创建复制代理 `/etc/replication` 存储库位置。 要正确处理关联的ACL ，需要此项。 在树的其他位置创建复制代理可能会导致未经授权的访问。

可以使用CRXDE Lite配置复制代理的各种参数。

如果您导航到 `/etc/replication` 您可以看到以下三个节点：

* `agents.author`
* `agents.publish`
* `treeactivation`

两个 `agents` 保存有关相应环境的配置信息，并且仅在该环境运行时处于活动状态。 例如， `agents.publish` 将仅在发布环境中使用。 以下屏幕截图显示了创作环境中的发布代理(随AEM WCM提供)：

![chlimage_1-24](assets/chlimage_1-24.png)

## 监视复制代理 {#monitoring-your-replication-agents}

监视复制代理：

1. 访问 **工具** AEM选项卡。
1. 单击&#x200B;**复制**。
1. 双击相应环境（左窗格或右窗格）的代理链接；例如 **作者代理**.

   生成的窗口将显示创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（一个链接）以显示有关该代理的详细信息：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   在此编辑器中，您可以：

   * 查看代理是否已启用。
   * 查看任何复制的目标。
   * 查看复制队列当前是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **刷新** 或 **清除** 更新队列条目的显示；这有助于查看进入和离开队列的项目。

   * **查看日志** 用于访问复制代理执行的任何操作的日志。
   * **测试连接** 到目标实例。
   * **强制重试** 在任何队列项目上（如果需要）。

   >[!CAUTION]
   >
   >请不要在发布实例上对“反向复制发件箱”使用“测试连接”链接。
   >
   >
   >如果为Outbox队列执行复制测试，则任何早于测试复制的项目都将通过每次反向复制重新处理。
   >
   >
   >如果此类项目已存在于队列中，则可通过以下XPath JCR查询找到它们，应将其删除。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批量复制 {#batch-replication}

批量复制不会复制单个页面或资产，而是等待触发这两个页面或资产的第一个阈值（基于时间或大小）。

然后，它将所有复制项目打包到一个包中，然后将该包作为单个文件复制到发布服务器。

发布者将解压缩所有项目，保存它们并向作者报告。

### 配置批量复制 {#configuring-batch-replication}

1. 转到 `http://serveraddress:serverport/siteadmin`
1. 按 **[!UICONTROL 工具]** 图标（位于屏幕的上方）
1. 从左侧导航栏转到 **[!UICONTROL 复制 — 创作上的代理]** 并双击 **[!UICONTROL 默认代理]**.
   * 您还可以直接转到，访问默认的发布复制代理。 `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. 按 **[!UICONTROL 编辑]** 按钮进行复制。
1. 在以下窗口中，转到 **[!UICONTROL 批次]** 选项卡：
   ![批量复制](assets/batchreplication.png)
1. 配置代理。

### 参数 {#parameters}

* `[!UICONTROL Enable Batch Mode]`  — 启用或禁用批量复制模式
* `[!UICONTROL Max Wait Time]`  — 启动批处理请求之前的最长等待时间（以秒为单位）。 默认值为2秒。
* `[!UICONTROL Trigger Size]`  — 在此大小限制时启动批量复制

## 其他资源 {#additional-resources}

有关疑难解答的详细信息，您可以阅读 [复制疑难解答](/help/sites-deploying/troubleshoot-rep.md) 页面。
