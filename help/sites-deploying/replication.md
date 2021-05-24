---
title: 复制
seo-title: 复制
description: 了解如何在AEM中配置和监视复制代理。
seo-description: 了解如何在AEM中配置和监视复制代理。
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: 配置
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3444'
ht-degree: 3%

---

# 复制{#replication}

复制代理是Adobe Experience Manager(AEM)的核心，作为用于：

* [将](/help/sites-authoring/publishing-pages.md#activatingcontent) 内容从创作发布（激活）到发布环境。
* 显式刷新Dispatcher缓存中的内容。
* 将用户输入（例如，表单输入）从发布环境返回到创作环境（在创作环境的控制下）。

请求将[排队](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler)到相应的代理进行处理。

>[!NOTE]
>
>用户数据（用户、用户组和用户配置文件）不会在创作实例和发布实例之间复制。
>
>对于多个发布实例，在启用[用户同步](/help/sites-administering/sync.md)时，将分发用户数据。

## 从创作复制到发布{#replicating-from-author-to-publish}

复制到发布实例或调度程序的过程分为以下步骤：

* 作者要求发布（激活）某些内容；可以通过手动请求或预配置的自动触发器来启动此操作。
* 请求将传递到相应的默认复制代理；一个环境可以具有多个默认代理，这些默认代理将始终为此类操作选择。
* 复制代理将“打包”内容并将其置于复制队列中。
* 在“网站”选项卡中，为各个页面设置[彩色状态指示器](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus)。
* 内容会从队列中提取并使用配置的协议传输到发布环境；通常为HTTP。
* 发布环境中的servlet接收请求并发布接收的内容；默认的servlet为`https://localhost:4503/bin/receive`。

* 可以配置多个创作和发布环境。

![chlimage_1-21](assets/chlimage_1-21.png)

### 从发布复制到创作{#replicating-from-publish-to-author}

某些功能允许用户在发布实例上输入数据。

在某些情况下，需要一种称为反向复制的复制类型，才能将此数据返回到创作环境，从中将其重新分发到其他发布环境。 出于安全考虑，必须严格控制从发布到创作环境的任何流量。

反向复制使用发布环境中引用创作环境的代理。 此代理将数据放入发件箱中。 此发件箱与创作环境中的复制侦听器匹配。 听众轮询发件箱以收集输入的任何数据，然后根据需要分发。 这可确保创作环境控制所有流量。

在其他情况下，例如对于“社区”功能（例如，论坛、博客、评论和评论），使用复制在发布环境中输入的用户生成内容(UGC)量很难在AEM实例之间高效同步。

AEM [Communities](/help/communities/overview.md)从不对UGC使用复制。 Communities的部署需要UGC的公共存储（请参阅[Community Content Storage](/help/communities/working-with-srp.md)）。

### 复制 — 开箱即用{#replication-out-of-the-box}

标准安装的AEM中包含的we-retail网站可用于说明复制。

要遵循此示例并使用默认的复制代理，您需要[安装AEM](/help/sites-deploying/deploy.md)并执行以下操作：

* 端口`4502`上的创作环境
* 端口`4503`上的发布环境

>[!NOTE]
>
>默认为已启用 :
>
>* 作者代理：默认代理（发布）
>
>
默认情况下会实际禁用(自AEM 6.1起):
>
>* 作者代理：反向复制代理(publish_reverse)
>* 发布代理：反向复制（发件箱）

>
>
要检查代理或队列的状态，请使用&#x200B;**工具**控制台。
>请参阅[监视复制代理](#monitoring-your-replication-agents)。

#### 复制（创作到发布）{#replication-author-to-publish}

1. 导航到创作环境中的支持页面。
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. 编辑页面以添加一些新文本。
1. **激活** 页面以发布更改。
1. 在发布环境中打开支持页面：
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. 现在，您可以查看在创作中输入的更改。

此复制操作是从创作环境中通过执行以下操作进行的：

* **默认代理（发布）**
此代理将内容复制到默认的发布实例。有关此（配置和日志）的详细信息，可从创作环境的“工具”控制台访问；或：

   `https://localhost:4502/etc/replication/agents.author/publish.html`。

#### 复制代理 — 开箱即用{#replication-agents-out-of-the-box}

标准AEM安装中提供以下代理：

* [默认](#replication-author-to-publish)
AgentUsed用于从创作复制到发布。

* 调度程序刷新
用于管理调度程序缓存。 有关更多信息，请参阅[从创作环境中使Dispatcher缓存失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment)和[从发布实例中使Dispatcher缓存失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)。

* [反向](#reverse-replication-publish-to-author)
复制：用于从发布复制到创作。社区功能（如论坛、博客和评论）不使用反向复制。 由于未启用发件箱，因此会有效地禁用该功能。 使用反向复制需要自定义配置。

* 静态代理
这是一个“将节点的静态表示存储到文件系统中的代理”。
例如，使用默认设置时，内容页面和dam资产会以HTML或相应的资产格式存储在`/tmp`下。 有关配置，请参阅`Settings`和`Rules`选项卡。
请求执行此操作，以便当直接从应用程序服务器请求页面时，可以看到内容。 这是一个专门的代理，在大多数情况下（可能）不是必需的。

## 复制代理 — 配置参数{#replication-agents-configuration-parameters}

从“工具”控制台配置复制代理时，对话框中有四个选项卡：

### 设置 {#settings}

* **名称**

   复制代理的唯一名称。

* **描述**

   此复制代理的用途描述。

* **启用**

   指示复制代理当前是否已启用。

   当代理为&#x200B;**enabled**&#x200B;时，队列将显示为：

   * **** 处理项目时处于活动状态。
   * **** 队列为空时。
   * **** 当项目在队列中但无法处理时，阻止；例如，当接收队列被禁用时。

* **序列化类型**

   序列化的类型：

   * **默认**:如果要自动选择代理，则进行设置。
   * **调度程序刷新**:如果要使用代理刷新调度程序缓存，请选择此选项。

* **重试延迟**

   如果遇到问题，则两次重试之间的延迟(等待时间（以毫秒为单位）。

   默认: `60000`

* **代理用户 ID**

   根据环境，代理将使用此用户帐户执行以下操作：

   * 从创作环境中收集和打包内容
   * 在发布环境中创建和写入内容

   将此字段留空，以使用系统用户帐户(sling中定义的帐户为管理员用户；默认情况下，此值为`admin`)。

   >[!CAUTION]
   >
   >对于创作环境中的代理，此帐户&#x200B;*必须*&#x200B;具有对要复制的所有路径的读取访问权限。

   >[!CAUTION]
   >
   >对于发布环境中的代理，此帐户&#x200B;*必须*&#x200B;具有复制内容所需的创建/写入权限。

   >[!NOTE]
   >
   >这可用作选择特定内容进行复制的机制。

* **日志级别**

   指定用于日志消息的详细级别。

   * `Error`:只记录错误
   * `Info`:将记录错误、警告和其他信息性消息
   * `Debug`:将在消息中使用高级详细信息，主要用于调试目的

   默认: `Info`

* **使用反转复制**

   指示此代理是否用于反向复制；返回从发布到创作环境中的用户输入。

* **别名更新**

   选择此选项可向Dispatcher启用别名或虚路径失效请求。 另请参阅[配置调度程序刷新代理](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent)。

#### 传输 {#transport}

* **URI**

   这会指定目标位置的接收Servlet。 特别是，您可以在此处指定目标实例的主机名（或别名）和上下文路径。

   例如：

   * 默认代理可以复制到`https://localhost:4503/bin/receive`
   * 调度程序刷新代理可以复制到`https://localhost:8000/dispatcher/invalidate.cache`

   此处指定的协议（HTTP或HTTPS）将确定传输方法。

   对于调度程序刷新代理，仅当使用基于路径的虚拟主机条目来区分场时，才使用URI属性，使用此字段来定位要失效的场。 例如，场#1的虚拟主机为`www.mysite.com/path1/*`，场#2的虚拟主机为`www.mysite.com/path2/*`。 您可以使用`/path1/invalidate.cache`的URL来定位第一个场，使用`/path2/invalidate.cache`来定位第二个场。

* **用户**

   用于访问目标的帐户的用户名。

* **密码**

   用于访问目标的帐户的密码。

* **NTLM 域**

   用于NTML身份验证的域。

* **NTLM 主机**

   用于NTML身份验证的主机。

* **启用宽松 SSL**

   如果希望接受自认证的SSL证书，请启用。

* **允许过期的证书**

   如果希望接受过期的SSL证书，则启用。

#### 代理 {#proxy}

仅当需要代理时，才需要以下设置：

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

   在此，您可以定义要绑定到的套接字接口。

   这会设置创建连接时使用的本地地址。 如果未设置此设置，则将使用默认地址。 这对于指定要在多宿主或群集系统上使用的接口非常有用。

* **HTTP 方法**

   要使用的HTTP方法。

   对于调度程序刷新代理，这几乎总是GET，不应更改(POST将是另一个可能的值)。

* **HTTP 头**

   这些参数用于调度程序刷新代理，并指定必须刷新的元素。

   对于调度程序刷新代理，三个标准条目不应需要更改：

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   根据需要，使用这些参数来指示刷新手柄或路径时要使用的操作。 子参数是动态的：

   * `{action}` 表示复制操作

   * `{path}` 指示路径

   它们将被与请求相关的路径/操作替换，因此不需要“硬编码”：

   >[!NOTE]
   >
   >如果您在推荐的默认上下文以外的上下文中安装了AEM，则需要在HTTP标头中注册该上下文。 例如：
   >`CQ-Handle:/<*yourContext*>{path}`

* **关闭连接**

   在每个请求后启用以关闭连接。

* **连接超时**

   尝试建立连接时应用的超时（以毫秒为单位）。

* **套接字超时**

   在建立连接后等待流量时应用的超时（以毫秒为单位）。

* **协议版本**

   协议版本；例如，`1.0`表示HTTP/1.0。

#### 触发器 {#triggers}

以下设置用于定义用于自动复制的触发器：

* **忽略默认值**

   如果选中，则代理将从默认复制中排除；这意味着如果内容作者发出复制操作，则不会使用此插件。

* **修改**

   此处，将在修改页面时自动触发此代理的复制。 它主要用于调度程序刷新代理，但也用于反向复制。

* **在分发时**

   如果选中，则代理将在修改时自动复制标记为分发的任何内容。

* **已实现开/关时间**

   当发生为页面定义的在线或离线时间时，这将触发自动复制（根据需要激活或停用页面）。 它主要用于调度程序刷新代理。

* **接收时**

   如果选中此选项，则代理将在收到复制事件时链式复制。

* **无状态更新**

   选中此选项后，代理将不会强制更新复制状态。

* **无版本控制**

   选中此选项后，代理将不会强制对已激活的页面进行版本控制。

## 配置复制代理{#configuring-your-replication-agents}

有关使用MSSL将复制代理连接到发布实例的信息，请参阅[使用互相SSL复制](/help/sites-deploying/mssl-replication.md)。

### 从创作环境{#configuring-your-replication-agents-from-the-author-environment}配置复制代理

在创作环境的“工具”选项卡中，您可以配置位于创作环境（**创作代理**）或发布环境（**发布代理**）中的复制代理。 以下过程说明了创作环境的代理配置，但可用于这两者。

>[!NOTE]
>
>当调度程序处理创作或发布实例的HTTP请求时，来自复制代理的HTTP请求必须包含PATH标头。 除了以下过程之外，您还必须将PATH标头添加到客户端标头的调度程序列表中。 (请参阅[/clientheaders（客户端标头）](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)。 [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. 访问AEM中的&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**复制**（左窗格可打开文件夹）。
1. 双击&#x200B;**创作代理**（左窗格或右窗格）。
1. 单击相应的代理名称（即链接）可显示有关该代理的详细信息。
1. 单击&#x200B;**编辑**&#x200B;以打开配置对话框：

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 提供的值应足以用于默认安装。 如果进行更改，请单击&#x200B;**确定**&#x200B;以保存它们（有关各个参数的更多详细信息，请参阅[复制代理 — 配置参数](#replication-agents-configuration-parameters)）。

>[!NOTE]
>
>标准安装的AEM将`admin`指定为默认复制代理内传输凭据的用户。
>
>应将此帐户更改为具有复制所需路径权限的特定于站点的复制用户帐户。

### 配置反向复制{#configuring-reverse-replication}

反向复制用于将发布实例上生成的用户内容返回到创作实例。 这通常用于调查和注册表单等功能。

出于安全原因，大多数网络拓扑不允许从&#x200B;*到“非军事区”（一个子网络，将外部服务公开给不受信任的网络，如Internet）的连接*。

由于发布环境通常位于DMZ中，因此要将内容返回到创作环境，必须从创作实例启动连接。 这可通过以下方式完成：

* 在放置内容的发布环境中显示&#x200B;*发件箱*。
* 创作环境中的代理（发布），该环境会定期轮询发件箱以获取新内容。

>[!NOTE]
>
>对于AEM [Communities](/help/communities/overview.md)，发布实例上的用户生成内容不使用复制。 请参阅[社区内容存储](/help/communities/working-with-srp.md)。

为此，您需要：

**创作环境中的反向复制代** 理充当活动组件，从发布环境的发件箱中收集信息：

如果要使用反向复制，请确保激活此代理。

![chlimage_1-23](assets/chlimage_1-23.png)

**发布环境中的反向复制代理（发件箱）** 这是被动元素，因为它充当“发件箱”。用户输入将放置在此处，作者环境中的代理从中收集用户输入。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### 为多个发布实例{#configuring-replication-for-multiple-publish-instances}配置复制

>[!NOTE]
>
>仅复制内容 — 不复制用户数据（用户、用户组和用户配置文件）。
>
>要同步多个发布实例中的用户数据，请启用[用户同步](/help/sites-administering/sync.md)。

安装后，已配置默认代理，以将内容复制到本地主机端口4503上运行的发布实例。

要为其他发布实例配置内容复制，您需要创建并配置一个新的复制代理：

1. 在AEM中打开&#x200B;**工具**&#x200B;选项卡。
1. 选择&#x200B;**复制**，然后在左侧面板中选择&#x200B;**创作代理**。
1. 选择&#x200B;**新建……**。
1. 设置&#x200B;**标题**&#x200B;和&#x200B;**名称**，然后选择&#x200B;**复制代理**。
1. 单击&#x200B;**创建**&#x200B;以创建新代理。
1. 双击新代理项以打开配置面板。
1. 单击&#x200B;**编辑** — 将打开&#x200B;**代理设置**&#x200B;对话框 — **序列化类型**&#x200B;已定义为默认值，必须保留该值。

   * 在&#x200B;**Settings**&#x200B;选项卡中：

      * 激活&#x200B;**Enabled**。
      * 输入&#x200B;**说明**.
      * 将&#x200B;**Retry Delay**&#x200B;设置为`60000`。

      * 将&#x200B;**序列化类型**&#x200B;保留为`Default`。
   * 在&#x200B;**传输**&#x200B;选项卡中：

      * 输入新发布实例所需的URI;例如，
         `https://localhost:4504/bin/receive`。

      * 输入用于复制的特定于站点的用户帐户。
      * 您可以根据需要配置其他参数。


1. 单击&#x200B;**确定**&#x200B;以保存设置。

然后，您可以通过在创作环境中更新并发布页面来测试操作。

这些更新将显示在已配置为上述内容的所有发布实例上。

如果您遇到任何问题，可以检查创作实例上的日志。 根据所需的详细级别，您还可以使用上面的&#x200B;**代理设置**&#x200B;对话框将&#x200B;**日志级别**&#x200B;设置为`Debug`。

>[!NOTE]
>
>这可以与使用[代理用户ID](#agentuserid)选择不同内容以复制到单个发布环境结合使用。 对于每个发布环境：
>
>1. 配置复制代理以复制到该发布环境。
>1. 配置用户帐户；具有读取将被复制到该特定发布环境的内容所需的访问权限。
>1. 将用户帐户分配为复制代理的&#x200B;**代理用户ID**。

>



### 配置调度程序刷新代理{#configuring-a-dispatcher-flush-agent}

安装中包含默认代理。 但是，如果您要定义新代理，则仍需要某些配置，这同样适用：

1. 在AEM中打开&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**Deployment**。
1. 选择&#x200B;**复制**，然后选择&#x200B;**发布的代理**。
1. 双击&#x200B;**调度程序刷新**&#x200B;项目以打开概述。
1. 单击&#x200B;**编辑** — 将打开&#x200B;**代理设置**&#x200B;对话框：

   * 在&#x200B;**Settings**&#x200B;选项卡中：

      * 激活&#x200B;**Enabled**。
      * 输入&#x200B;**说明**.
      * 将&#x200B;**序列化类型**&#x200B;保留为`Dispatcher Flush`，或者在创建新代理时将其设置为。

      * （可选）选择&#x200B;**别名更新**&#x200B;以启用对Dispatcher的别名或虚路径失效请求。
   * 在&#x200B;**传输**&#x200B;选项卡中：

      * 输入新发布实例所需的URI;例如，
         `https://localhost:80/dispatcher/invalidate.cache`。

      * 输入用于复制的特定于站点的用户帐户。
      * 您可以根据需要配置其他参数。

   对于调度程序刷新代理，仅当使用基于路径的虚拟主机条目来区分场时，才使用URI属性，使用此字段来定位要失效的场。 例如，场#1的虚拟主机为`www.mysite.com/path1/*`，场#2的虚拟主机为`www.mysite.com/path2/*`。 您可以使用`/path1/invalidate.cache`的URL来定位第一个场，使用`/path2/invalidate.cache`来定位第二个场。

   >[!NOTE]
   >
   >如果您在建议的默认上下文以外的上下文中安装了AEM，则需要在&#x200B;**Extended**&#x200B;选项卡中配置[HTTP标头](#extended)。

1. 单击&#x200B;**确定**&#x200B;以保存更改。
1. 返回到&#x200B;**工具**&#x200B;选项卡，从此处可以&#x200B;**激活****调度程序刷新**&#x200B;代理（**发布时的代理**）。

**Dispatcher Flush**&#x200B;复制代理在创作时不活动。 您可以使用等效的URI在发布环境中访问同一页面；例如，`https://localhost:4503/etc/replication/agents.publish/flush.html`。

### 控制对复制代理的访问{#controlling-access-to-replication-agents}

使用`etc/replication`节点上的用户和/或组页面权限，可以控制对用于配置复制代理的页面的访问。

>[!NOTE]
>
>设置此类权限将不会影响复制内容的用户（例如，从“网站”控制台或Sidekick选项）。 复制框架在复制页面时不使用当前用户的“用户会话”访问复制代理。

### 从CRXDE Lite{#configuring-your-replication-agents-from-crxde-lite}配置复制代理

>[!NOTE]
>
>仅在`/etc/replication`存储库位置支持创建复制代理。 要正确处理关联的ACL，需要这样做。 在树的其他位置创建复制代理可能会导致未经授权的访问。

可以使用CRXDE Lite配置复制代理的各种参数。

如果导航到`/etc/replication`，您可以看到以下三个节点：

* `agents.author`
* `agents.publish`
* `treeactivation`

两个`agents`保存有关相应环境的配置信息，并且仅在该环境运行时才处于活动状态。 例如， `agents.publish`将仅在发布环境中使用。 以下屏幕截图显示了创作环境中的发布代理，该代理随AEM WCM一起提供：

![chlimage_1-24](assets/chlimage_1-24.png)

## 监视复制代理{#monitoring-your-replication-agents}

要监视复制代理，请执行以下操作：

1. 访问AEM中的&#x200B;**工具**&#x200B;选项卡。
1. 单击&#x200B;**复制**。
1. 双击相应环境（左窗格或右窗格）的代理链接；例如，作者&#x200B;**上的代理。**

   生成的窗口显示了创作环境的所有复制代理的概述，包括其目标和状态。

1. 单击相应的代理名称（即链接）可显示有关该代理的详细信息：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   在此对话框中，您可以：

   * 查看是否启用了代理。
   * 查看任何复制的目标。
   * 查看复制队列当前是否处于活动状态（已启用）。
   * 查看队列中是否有任何项目。
   * **** 刷新或 **** 清除以更新队列条目的显示；这有助于您查看进入队列和离开队列的项目。

   * **查** 看日志以访问复制代理执行的任何操作的日志。
   * **测试** 与目标实例的连接。
   * **根据** 需要强制重试任何队列项。

   >[!CAUTION]
   >
   >请勿在发布实例上对反向复制发件箱使用“测试连接”链接。
   >
   >
   >如果对发件箱队列执行复制测试，则所有早于测试复制的项目都将通过每次反向复制进行重新处理。
   >
   >
   >如果此类项目已存在于队列中，则可通过以下XPath JCR查询找到它们，并应将其删除。
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## 批量复制{#batch-replication}

批量复制不会复制单个页面或资产，而是会等待触发两个页面或资产的第一个阈值（基于时间或大小）。

然后，将所有复制项打包到一个包中，然后将该包作为单个文件复制到发布者。

出版商将解包所有项目，保存它们并向作者报告。

### 配置批量复制{#configuring-batch-replication}

1. 转到 `http://serveraddress:serverport/siteadmin`
1. 按屏幕上方的&#x200B;**[!UICONTROL 工具]**&#x200B;图标
1. 从左侧导航边栏中，转到&#x200B;**[!UICONTROL 复制 — 作者上的代理]** ，然后双击&#x200B;**[!UICONTROL 默认代理]**。
   * 您还可以直接转到`http://serveraddress:serverport/etc/replication/agents.author/publish.html`以访问默认的发布复制代理
1. 按复制队列上方的&#x200B;**[!UICONTROL 编辑]**&#x200B;按钮。
1. 在以下窗口中，转到&#x200B;**[!UICONTROL 批]**选项卡：
   ![批量复制](assets/batchreplication.png)
1. 配置代理。

### 参数 {#parameters}

* `[!UICONTROL Enable Batch Mode]`  — 启用或禁用批处理复制模式
* `[!UICONTROL Max Wait Time]`  — 在启动批处理请求之前的最长等待时间（以秒为单位）。默认为2秒。
* `[!UICONTROL Trigger Size]`  — 在此大小限制时启动批量复制

## 其他资源 {#additional-resources}

有关疑难解答的详细信息，请阅读[复制疑难解答](/help/sites-deploying/troubleshoot-rep.md)页面。
