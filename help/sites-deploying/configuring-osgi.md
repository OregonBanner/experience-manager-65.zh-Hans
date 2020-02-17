---
title: 配置OSGi
seo-title: 配置OSGi
description: OSGi是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。 它用于控制AEM的复合捆绑包及其配置。 本文详细介绍了如何管理此类包的配置设置。
seo-description: OSGi是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。 它用于控制AEM的复合捆绑包及其配置。 本文详细介绍了如何管理此类包的配置设置。
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置OSGi{#configuring-osgi}

[OSGi是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。](https://www.osgi.org/) 它用于控制AEM的复合捆绑包及其配置。

OSGi“提&#x200B;*供了标准化的基元，这些基元允许从小的、可重用的和协作的组件构建应用程序。 这些组件可以组成一个应用程序并部署*”。

这样，由于可以单独停止、安装和启动捆绑套件，因此可以轻松管理它们。 互依关系将自动处理。 每个OSGi组件(请参 [阅OSGi规范](https://www.osgi.org/Specifications/HomePage))都包含在各种包之一中。

您可以通过以下任一方式管理此类包的配置设置：

* 使用 [Adobe CQ web控制台](#osgi-configuration-with-the-web-console)
* 使用配 [置文件](#osgi-configuration-with-configuration-files)
* 配置 [存储库中的内 `sling:OsgiConfig`容节点()](#osgi-configuration-in-the-repository)

尽管存在细微差异，但这两种方法都可以使用，主要与“运行模 [式”相关](/help/sites-deploying/configure-runmodes.md):

* [Adobe CQ web控制台](#osgi-configuration-with-the-web-console)

   * Web控制台是OSGi配置的标准界面。 它提供了用于编辑各种属性的UI，在该UI中，可以从预定义的列表中选择可能的值。

      因此，这是最简单的方法。

   * 使用Web控制台进行的任何配置都将立即应用并适用于当前实例，而不管当前运行模式或对运行模式的任何后续更改。

* [配置文件](#osgi-configuration-with-configuration-files)

   * 包含Web控制台中定义的设置。
   * 可以包含在内容包中，以用于其他实例。

* [存储库中的内容节点(sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * 这需要使用CRXDE lite进行手动配置。
   * 根据节点的命名约 `sling:OsgiConfig` 定，您可以将配置绑定到特定的运 [行模式](/help/sites-deploying/configure-runmodes.md)。 您甚至可以在同一存储库中保存多个运行模式的配置。
   * 将立即应用任何适当的配置（取决于运行模式）。

无论您使用哪种方法，所有这些配置方法：

* 确保复制或复制存储库内容会重新创建相同的配置。
* 允许您将配置检出到FileVault或Subversion;用于安全或更新。
* 可以保存在包中，以便在设置其他实例时使用。
* 允许您使用脚本执行配置转出以传播配置详细信息。

>[!NOTE]
>
>某些重要设置的详细信息列在“ [OSGi配置设置”下。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web控制台进行OSGi配置 {#osgi-configuration-with-the-web-console}

AEM中 [的Web控制台](/help/sites-deploying/web-console.md) ，为配置捆绑包提供了标准化界面。 “配 **置** ”选项卡用于配置OSGi包，因此是配置AEM系统参数的基础机制。

所做的任何更改将立即应用于相关OSGi配置，无需重新启动。

>[!NOTE]
>
>在Web控制台中所做的更改会作为配置文件保存在存储库 [中](#osgi-configuration-with-configuration-files)。 这些组件可以包含在内容包中，以便在进一步安装中重复使用。

>[!NOTE]
>
>在Web控制台上，提及默认设置的任何说明都与Sling默认值相关。
>
>Adobe Experience manager具有自己的默认值，因此默认设置可能与控制台中记录的默认值不同。

要使用Web控制台更新配置，请执行以下操作：

1. 通过以 **下任一方式** ，访问Web控制台的“配置”选项卡：

   * 从“工具”->“操作”菜单上的链 **接打开Web控制台** 。 登录控制台后，您可以使用以下下拉菜单：

      **OSGi >**

   * 直接URL;例如：

      `http://localhost:4502/system/console/configMgr`
   此时将显示一个列表。

1. 通过以下任一方式选择要配置的捆绑包：

   * 单击该包 **的编辑** 图标
   * 单击包 **的名称** 。

1. 此时将打开一个对话框。您可以在此根据需要进行编辑；例如，将“日志 **级别** ”设置为 `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新将作为配置文件保存在 [存储库中](#osgi-configuration-with-configuration-files)。 要在之后找到这些标识（例如，包含在内容包中以用于另一个实例），您应记下永久标识( `PID`)。

1. 单击&#x200B;**保存**。

   您所做的更改会立即应用于正在运行的系统的相关OSGi配置，无需重新启动。

   >[!NOTE]
   >
   >您现在可以找到 [相关的配置文件](#osgi-configuration-with-configuration-files);例如，包含在内容包中以用于另一个实例。

## OSGi配置与配置文件 {#osgi-configuration-with-configuration-files}

使用Web控制台进行的配置更改会作为配置文件()保留在存储库中，该配置文件位于： `.config`

`/apps`

这些组件可以包含在内容包中，并可在其他实例上重新使用。

>[!NOTE]
>
>配置文件的格式非常具体——有关完整的详细信 [息，请参阅Sling Apache文档](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 。
>
>因此，建议通过在Web控制台中进行实际更改来创建和维护配置文件。

Web控制台不显示已保存更改的存储库位置，但可以轻松找到这些更改：

1. 通过在Web控制台中 [进行初始更改来创建配置文件](#osgi-configuration-with-the-web-console)。
1. 打开CRXDE Lite。
1. **在“工**&#x200B;具&#x200B;**”菜单中，选**&#x200B;择查询…….
1. 提交 **Type** 查询 `SQL` ，以搜索已更新的配置的PID。

   例如， **Apache Felix OSGi管理控制台具有** :

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此SQL查询可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 此时将显示配置文件节点。

   对于上述示例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以打开此文件来查看更改，但为避免键入错误，建议使用控制台进行实际更改。

1. 您现在可以构建包含此节点的内容包，并根据需要在其他实例上使用。

## 存储库中的OSGi配置 {#osgi-configuration-in-the-repository}

除了使用Web控制台，您还可以在存储库中定义配置详细信息。 这使您能够轻松配置不同的运行模式。

这些配置是通过在存储库中 `sling:OsgiConfig` 创建节点以供系统引用来实现的。 这些节点镜像OSGi配置，并为它们形成用户界面。 要更新配置数据，请更新节点属性。

如果修改存储库中的配置数据，则更改将立即应用于相关OSGi配置，就像是使用Web控制台进行了更改一样，并会进行相应的验证和一致性检查。 这也适用于将配置从复制到的操 `/libs/` 作 `/apps/`。

由于同一配置参数可以位于多个位置，因此系统：

* 搜索类型的所有节点 `sling:OsgiConfig`
* 根据服务名称过滤
* 根据运行模式过滤

>[!NOTE]
>
>另请阅 [读如何仅为特定实例定义基于存储库的配置](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)。

### 将新配置添加到存储库 {#adding-a-new-configuration-to-the-repository}

#### 您需要了解的内容 {#what-you-need-to-know}

要向存储库添加新配置，您需要了解以下内容：

1. 服 **务的永久标识** (PID)。

   在Web控 **制台中** ，引用“配置”字段。 该名称在包名称后方的括号中显示(或在页面 **底部的“配置信息** ”中显示)。

   例如，创建一个节点 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 以配置 **AEM WCM版本管理器**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是否需要 [特定运行模](/help/sites-deploying/configure-runmodes.md) 式。 创建文件夹：

   * `config` -适用于所有运行模式
   * `config.author` -适用于创作环境
   * `config.publish` -对于发布环境
   * `config.<run-mode>` -视情况而定

1. 是否需要 **配置****或工厂配置** 。
1. 要配置的各个参数；包括需要重新创建的任何现有参数定义。

   在Web控制台中引用单个参数字段。 每个参数的名称以括号显示。

   例如，创建属性
   `versionmanager.createVersionOnActivation` 配置激 **活时创建版本**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 中是否已存在配置 `/libs`? 要列出实例中的所有配置，请使用CRXDE **Lite中的Query** 工具提交以下SQL查询：

   `select * from sling:OsgiConfig`

   如果是，则可以将此配置复制到新位 ` /apps/<yourProject>/`置，然后在新位置进行自定义。

#### 在存储库中创建配置 {#creating-the-configuration-in-the-repository}

要将新配置实际添加到存储库，请执行以下操作：

1. 使用CRXDE Lite导航到：

   ` /apps/<yourProject>`

1. 如果尚未存在，请创建文 `config` 件夹( `sling:Folder`):

   * `config` -适用于所有运行模式
   * `config.<run-mode>` -特定于特定运行模式

1. 在此文件夹下，创建一个节点：

   * 类型: `sling:OsgiConfig`
   * 名称：持久身份(PID);

      例如，AEM WCM版本管理器使用 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >在名称后附加工厂配 `-<identifier>` 置时。
   >
   >如下所示： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >如果 `<identifier>` 被您（必须）输入用来标识实例的自由文本替换（您不能忽略此信息）;例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 对于要配置的每个参数，在此节点上创建一个属性：

   * 名称：Web控制台中所示的参数名称；该名称显示在字段描述末尾的括号中。 例如，供使 `Create Version on Activation` 用 `versionmanager.createVersionOnActivation`
   * 类型：视情况而定。
   * 值：根据需要。
   您只需为要配置的参数创建属性，其他参数仍将采用AEM设置的默认值。

1. 保存所有更改。

   通过重新启动服务更新节点后，更改会立即应用（与在Web控制台中所做的更改一样）。

>[!CAUTION]
>
>不得更改路径中的任 `/libs` 何内容。

>[!CAUTION]
>
>配置的完整路径必须正确，才能在启动时读取。

## 配置详细信息 {#configuration-details}

### 启动时的分辨率顺序 {#resolution-order-at-startup}

使用以下优先顺序：

1. 存储库节点位于 `/apps/*/config...`.with type或property `sling:OsgiConfig` files下。

1. 类型为“”的存储库 `sling:OsgiConfig` 节点 `/libs/*/config...`。 （现成定义）。

1. 来自 `.config` 的任何文 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`件。 在本地文件系统上。

这意味着中的通用配置可 `/libs` 以由中的项目特定配置遮罩 `/apps`。

### 运行时的分辨率顺序 {#resolution-order-at-runtime}

在系统运行时所做的配置更改会触发使用修改后的配置的重新加载。

然后，将应用以下优先级顺序：

1. 在Web控制台中修改配置将立即生效，因为它在运行时优先。
1. 在中修改配置 `/apps` 将立即生效。
1. 在中修改配 `/libs` 置将立即生效，除非中的配置遮罩 `/apps`。

### 多种运行模式的分辨率 {#resolution-of-multiple-run-modes}

对于运行模式特定的配置，可以组合多个运行模式。 例如，您可以使用以下样式创建配置文件夹：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有运行模式都与启动时定义的运行模式匹配，则将应用此类文件夹中的配置。

例如，如果实例是以运行模式启动的，则 `author,dev,emea`将应用中和中的配置节点，而不应用中和中的配置 `/apps/*/config.emea`节 `/apps/*/config.author.dev/``/apps/*/config.author.emea.dev/``/apps/*/config.author.asean/``/config/author.dev.emea.noldap/` 点则不会应用。

如果同一PID的多个配置适用，则应用具有最大匹配运行模式数的配置。

例如，如果实例是以运行模式启动的 `author,dev,emea`，并且同时 `/apps/*/config.author/` 定义 `/apps/*/config.emea.author/` 了配置`com.day.cq.wcm.core.impl.VersionManagerImpl`，则将应用中的 `/apps/*/config.emea.author/` 配置。

此规则的粒度为PID级别。
不能为同一PID定义某些属性，而为 `/apps/*/config.author/` 同一PID定义更 `/apps/*/config.emea.author/` 多特定的属性。
对于整个PID，具有最大匹配运行模式的配置是有效的。

### 标准配置 {#standard-configurations}

以下列表显示了存储库中可用配置（在标准安装中）的一小部分选择：

* 作者- AEM WCM过滤器：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 发布- AEM WCM过滤器：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 发布- AEM WCM页面统计：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>由于这些配置位于 `/libs` 其中，因此不能直接编辑，而是在自定义之前将其复制到您的应用程序区 `/apps`域()。

要列出实例中的所有配置节点，请使用CRXDE **** Lite中的查询功能提交以下SQL查询：

`select * from sling:OsgiConfig`

### 配置持久性 {#configuration-persistence}

* 如果通过Web控制台更改配置，则（通常）会将其写入存储库(位于：

   `/apps/{somewhere}`

   * 默认情 `{somewhere}` 况下， `system/config` 将配置写入

      `/apps/system/config`

   * 但是，如果您编辑的配置最初来自存储库中的其他位置：例如：

      /libs/foo/config/someconfig

      然后将更新后的配置写入原始位置；例如：

      `/apps/foo/config/someconfig`

* 由更改的设置将保 `admin` 存在以下文 `*.config` 件中：

   ```
      /crx-quickstart/launchpad/config
   ```

   * 这是OSGi配置管理员的专用数据区域，它包含由指定的所有配置详细信息，而 `admin`不管这些配置是如何进入系统的。
   * 这是一个实施详细信息，您绝不能直接编辑此目录。
   * 但是，了解这些配置文件的位置是有用的，以便可以为备份和／或多次安装获取副本：

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling客户端存储库

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>您不得 ***在*** :
>
>`/crx-quickstart/launchpad/config`

