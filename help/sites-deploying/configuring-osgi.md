---
title: 配置OSGi
seo-title: Configuring OSGi
description: OSGi是Adobe Experience Manager (AEM)技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。 本文详细介绍了如何管理此类捆绑包的配置设置。
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# 配置OSGi{#configuring-osgi}

[osgi](https://www.osgi.org/) 是Adobe Experience Manager (AEM)技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。

OSGi ”*提供标准化的基元，允许使用小型、可重用和协作组件构建应用程序。 这些组件可以组合为一个应用程序并进行部署*“。

这样可以轻松地管理捆绑包，因为它们可以单独停止、安装和启动。 系统会自动处理相互依赖关系。 每个OSGi组件(请参见 [OSGi规范](https://docs.osgi.org/specification/))包含在多个捆绑包中的一个。

您可以通过以下任一方式管理此类捆绑包的配置设置：

* 使用 [Adobe CQ Web控制台](#osgi-configuration-with-the-web-console)
* 使用 [配置文件](#osgi-configuration-with-configuration-files)
* 配置 [content-nodes ( `sling:OsgiConfig`)](#osgi-configuration-in-the-repository)

虽然存在一些细微差异，但可以使用任一方法，主要与 [运行模式](/help/sites-deploying/configure-runmodes.md)：

* [Adobe CQ Web控制台](#osgi-configuration-with-the-web-console)

   * Web控制台是OSGi配置的标准界面。 它提供了一个用于编辑各种属性的UI，在其中可以从预定义列表中选择可能的值。

     因此，这是最简单的方法。

   * 使用Web控制台所做的任何配置都将立即应用并适用于当前实例，不论当前运行模式如何，也不论后续是否对运行模式进行了任何更改。

* [配置文件](#osgi-configuration-with-configuration-files)

   * 包含在Web控制台中定义的设置。
   * 可以包含在内容包中，以供在其他实例中使用。

* [存储库中的content-nodes (sling：osgiConfig)](#osgi-configuration-in-the-repository)

   * 需要使用CRXDE Lite进行手动配置。
   * 由于 `sling:OsgiConfig` 节点，您可以将配置绑定到特定 [运行模式](/help/sites-deploying/configure-runmodes.md). 您甚至可以在同一存储库中保存多个运行模式的配置。
   * 任何适当的配置都会立即应用（取决于运行模式）。

无论您使用哪种方法，所有这些配置方法都可以：

* 确保复制或复制存储库内容会重新创建相同的配置。
* 允许您将配置签出到FileVault或Subversion；用于安全或进一步更新。
* 可以保存在包中，以便在设置其他实例时使用。
* 允许您使用脚本执行配置转出以传播配置详细信息。

>[!NOTE]
>
>某些重要设置的详细信息列在 [OSGi配置。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web控制台进行OSGi配置 {#osgi-configuration-with-the-web-console}

此 [Web控制台](/help/sites-deploying/web-console.md) AEM中提供了用于配置捆绑包的标准化界面。 此 **配置** tab用于配置OSGi捆绑包，因此是用于配置AEM系统参数的底层机制。

所做的任何更改将立即应用于相关的OSGi配置，无需重新启动。

>[!NOTE]
>
>在Web控制台中所做的更改在存储库中保存为 [配置文件](#osgi-configuration-with-configuration-files). 这些文件可以包含在内容包中，以供在后续安装中重复使用。

>[!NOTE]
>
>在Web控制台上，任何提及默认设置的描述都与Sling默认设置相关。
>
>Adobe Experience Manager有自己的默认值，因此设置的默认值可能与控制台中记录的默认值不同。

要使用Web控制台更新配置，请执行以下操作：

1. 访问 **配置** Web控制台的选项卡，方法是：

   * 通过上的链接打开Web控制台 **工具 — >操作** 菜单。 登录到控制台后，您可以使用以下下拉菜单：

     **OSGi >**

   * 直接URL；例如：

     `http://localhost:4502/system/console/configMgr`

   此时将显示一个列表。

1. 选择要通过以下任一方式配置的包：

   * 单击 **编辑** 该捆绑包的图标
   * 单击 **名称** 捆绑

1. 随即会打开一个对话框。 您可以在此根据需要进行编辑。 例如，设置 **日志级别** 到 `INFO`：

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新在存储库中保存为 [配置文件](#osgi-configuration-with-configuration-files). 例如，要在以后查找这些文件以包含在内容包中以供在其他实例上使用，请记下永久标识( `PID`)。

1. 单击&#x200B;**保存**。

   您的更改将立即应用于正在运行的系统的相关OSGi配置，无需重新启动。

   >[!NOTE]
   >
   >您现在可以找到相关的 [配置文件](#osgi-configuration-with-configuration-files). 例如，包含在内容包中以供在另一个实例上使用。

## 包含配置文件的OSGi配置 {#osgi-configuration-with-configuration-files}

使用Web控制台所做的配置更改将作为配置文件保留在存储库中( `.config`)，位于：

`/apps`

这些文件可以包含在内容包中并在其他实例上重用。

>[!NOTE]
>
>配置文件的格式是特定的 — 请参阅Sling Apache文档以了解以下内容：
>* 的完整详细信息 [Apache Sling配置模型和Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* 教程和示例 [在Sling中获取资源和属性](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>因此，建议通过在Web控制台中进行实际更改来创建和维护配置文件。

Web控制台不显示存储库中已保存更改的位置，但可以轻松地找到它们：

1. 通过以下方式创建配置文件 [在Web控制台中进行初始更改](#osgi-configuration-with-the-web-console).
1. 打开 CRXDE Lite。
1. 在 **工具** 菜单，选择 **查询……** .
1. 要搜索已更新配置的PID，请提交 **类型** `SQL`.

   例如， **Apache Felix OSGi管理控制台** 具有永久标识(PID)：

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此，SQL查询可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 此时将显示配置文件节点。

   对于以上示例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以打开此文件以查看更改，但为避免键入错误，建议使用控制台进行实际更改。

1. 您现在可以生成包含此节点的内容包，并根据需要在其他实例中使用。

## 存储库中的OSGi配置 {#osgi-configuration-in-the-repository}

除了使用Web控制台之外，您还可以在存储库中定义配置详细信息。 这样，您就可以轻松配置不同的运行模式。

这些配置是通过创建 `sling:OsgiConfig` 供系统引用的存储库中的节点。 这些节点镜像了OSGi配置，并为它们形成了用户界面。 要更新配置数据，请更新节点属性。

如果修改存储库中的配置数据，更改将立即应用于相关的OSGi配置。 就好像更改是使用Web控制台进行的，进行了适当的验证和一致性检查。 此工作流还适用于从复制配置的操作 `/libs/` 到 `/apps/`.

由于同一个配置参数位于多个位置，因此系统：

* 搜索类型为的所有节点 `sling:OsgiConfig`
* 根据服务名称过滤
* 根据运行模式进行筛选

>[!NOTE]
>
>另请阅读 [如何仅为特定实例定义基于存储库的配置](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=zh-Hans).

### 向存储库添加新配置 {#adding-a-new-configuration-to-the-repository}

#### 您需要了解的信息 {#what-you-need-to-know}

要将配置添加到存储库，您必须知道以下内容：

1. 此 **永久身份** 服务的(PID)。

   参考 **配置** 字段。 该名称显示在包名称后面的括号中(或在 **配置信息** （向页面底部发送）。

   例如，创建一个节点 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 配置 **AEM WCM版本管理器**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是特定的 [运行模式](/help/sites-deploying/configure-runmodes.md) 必需？ 创建文件夹：

   * `config`  — 适用于所有运行模式
   * `config.author`  — 对于创作环境
   * `config.publish`  — 对于发布环境
   * `config.<run-mode>` - 酌情

1. 是 **配置** 或 **工厂配置** 是否必需？
1. 要配置的单个参数，包括必须重新创建的任何现有参数定义。

   引用Web控制台中的各个参数字段。 每个参数的名称都显示在括号中。

   例如，创建一个资产
   `versionmanager.createVersionOnActivation` 配置 **激活时创建版本**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 中是否存在配置 `/libs`？ 要列出实例中的所有配置，请使用 **查询** CRXDE Lite中用于提交以下SQL查询的工具：

   `select * from sling:OsgiConfig`

   如果是这样的话，此配置可以复制到 ` /apps/<yourProject>/`，然后在新位置自定义。

#### 在存储库中创建配置 {#creating-the-configuration-in-the-repository}

要向存储库中实际添加新配置，请执行以下操作：

1. 使用CRXDE Lite可导航至：

   ` /apps/<yourProject>`

1. 如果不存在，请创建 `config` 文件夹( `sling:Folder`)：

   * `config`  — 适用于所有运行模式
   * `config.<run-mode>`  — 特定于特定运行模式

1. 在此文件夹下创建节点：

   * 类型：`sling:OsgiConfig`
   * 名称：永久标识(PID)；

     例如，对于AEM WCM版本管理器，请使用 `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >在附加工厂配置时 `-<identifier>` 到名称。
   >
   >如下所示： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >位置 `<identifier>` 替换为（必须）输入以标识实例的自由文本（不能忽略此信息）；例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 对于要配置的每个参数，在此节点上创建一个属性：

   * 名称：在Web控制台中显示的参数名称；该名称显示在字段描述末尾的括号中。 例如，对于 `Create Version on Activation` 使用 `versionmanager.createVersionOnActivation`
   * 类型：根据需要。
   * 值：根据需要。

   您只需为要配置的参数创建属性，其他参数仍采用AEM设置的默认值。

1. 保存所有更改。

   当通过重新启动服务来更新节点时，将应用更改（与Web控制台中所做的更改一样）。

>[!CAUTION]
>
>请勿更改 `/libs` 路径。

>[!CAUTION]
>
>配置的完整路径必须正确，才能在启动时读取。

## 配置详细信息 {#configuration-details}

### 启动时的解决顺序 {#resolution-order-at-startup}

使用以下优先顺序：

1. 下的存储库节点 `/apps/*/config...`.与类型一起使用 `sling:OsgiConfig` 或属性文件。

1. 具有类型的存储库节点 `sling:OsgiConfig` 下 `/libs/*/config...`. （开箱即用的定义）。

1. 任何 `.config` 文件来源 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. 在本地文件系统上。

中的常规配置 `/libs` 可以被中的项目特定配置掩盖 `/apps`.

### 运行时解决顺序 {#resolution-order-at-runtime}

系统运行时所做的配置更改会触发使用修改后的配置重新加载。

则以下优先级顺序适用：

1. 在Web控制台中修改配置会立即生效，因为它在运行时具有优先权。
1. 在中修改配置 `/apps` 会立即生效
1. 在中修改配置 `/libs` 立即生效，除非在中配置将其掩盖 `/apps`.

### 多种运行模式的分辨率 {#resolution-of-multiple-run-modes}

对于特定于运行模式的配置，可以组合多个运行模式。 例如，您可以按照以下样式创建配置文件夹：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有运行模式与启动时定义的运行模式匹配，则应用此类文件夹中的配置。

例如，如果使用运行模式启动实例 `author,dev,emea`，配置中的节点 `/apps/*/config.emea`， `/apps/*/config.author.dev/`、和 `/apps/*/config.author.emea.dev/` ，而配置节点 `/apps/*/config.author.asean/` 和 `/config/author.dev.emea.noldap/` 不应用。

如果同一PID有多个配置适用，则应用匹配运行模式数最多的配置。

例如，如果使用运行模式启动实例 `author,dev,emea`，并且两者 `/apps/*/config.author/` 和 `/apps/*/config.emea.author/` 定义配置
`com.day.cq.wcm.core.impl.VersionManagerImpl`，中的配置 `/apps/*/config.emea.author/` 中所有规则都适用的URL的区域。

此规则的粒度处于PID级别。
不能在中为同一PID定义某些属性 `/apps/*/config.author/` 以及中更具体的部分 `/apps/*/config.emea.author/` 相同的PID。
匹配运行模式数最高的配置对整个PID有效。

### 标准配置 {#standard-configurations}

以下列表显示了存储库中可用配置的一小部分（在标准安装中）：

* 作者 — AEM WCM过滤器：

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 发布 — AEM WCM过滤器：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 发布 — AEM WCM页面统计信息：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>因为这些配置驻留在 `/libs` 不能直接编辑它们，而是将其复制到您的应用程序区域( `/apps`)。

要列出实例中的所有配置节点，请使用 **查询** CRXDE Lite中用于提交以下SQL查询的功能：

`select * from sling:OsgiConfig`

### 配置持久性 {#configuration-persistence}

* 如果通过Web控制台更改配置，则它（通常）会写入存储库的以下位置：

  `/apps/{somewhere}`

   * 默认情况下 `{somewhere}` 是 `system/config` 因此将配置写入

     `/apps/system/config`

   * 但是，如果您编辑的配置最初来自存储库中的其他位置，例如：

     /libs/foo/config/someconfig

     然后将更新的配置写入原始位置下；例如：

     `/apps/foo/config/someconfig`

* 由更改的设置 `admin` 保存在 `*.config` 文件位于：

  ```
     /crx-quickstart/launchpad/config
  ```

   * 此区域是OSGi配置管理员的私有数据，保存了指定的所有配置详细信息 `admin`，而不管他们如何进入系统。
   * 此区域是一个实施详细信息，您绝不能直接编辑此目录。
   * 但是，知道这些配置文件的位置很有用，这样就可以获取副本进行备份，或者执行多个安装，或者同时执行两者：

      * Apache Felix OSGi管理控制台

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling客户端存储库

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>切勿编辑以下文件夹或文件：
>
>`/crx-quickstart/launchpad/config`
