---
title: Web 控制台
seo-title: Web 控制台
description: 了解如何使用AEM web控制台。
seo-description: 了解如何使用AEM web控制台。
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Web 控制台{#web-console}

AEM中的Web控制台基于 [Apache Felix web管理控制台](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html)。 Apache Felix是为实施OSGi R4服务平台而进行的社区工作，该平台包括OSGi框架和标准服务。

>[!NOTE]
>
>在Web控制台上，提及默认设置的任何说明都与Sling默认值相关。
>
>AEM有其自己的默认值，因此默认设置可能与控制台中记录的默认值不同。

Web控制台提供一系列用于维护OSGi包的选项卡，包括：

* [配置](#configuration):用于配置OSGi包，因此它是用于配置AEM系统参数的基础机制
* [捆绑](#bundles):用于安装捆绑包
* [组件](#components):用于控制AEM所需组件的状态

所做的任何更改将立即应用于正在运行的系统。 无需重新启动。

控制台可从访问 `../system/console`;例如：

`http://localhost:4502/system/console/components`

## 配置 {#configuration}

“配 **置** ”选项卡用于配置OSGi包，因此是配置AEM系统参数的基础机制。

>[!NOTE]
>
>有关 [更多详细信息，请参阅Web控制台的OSGi配置](/help/sites-deploying/configuring-osgi.md) 。

“配 **置** ”选项卡可通过以下任一方式访问：

* 下拉菜单：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/configMgr`

此时将显示配置列表：

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

此屏幕上的下拉列表提供两种类型的配置：

* **配置**&#x200B;允许您更新现有配置。 它们具有永久标识(PID)，可以是：

   * AEM的标准和集成；如果删除这些值，则这些值将返回到默认设置。
   * 根据工厂配置创建的实例；这些实例由用户创建，删除操作将删除该实例。

* **工厂配**&#x200B;置允许您创建所需功能对象的实例。

   此标识将分配一个永久标识，然后列在配置下拉列表中。

从列表中选择任何条目将显示与该配置相关的参数：

![chlimage_1-21](assets/chlimage_1-21a.png)

然后，您可以根据需要更新参数，并：

* **保存**

   保存所做的更改。

   对于工厂配置，这将创建一个具有永久标识的新实例。 新实例随后将列在配置下。

* **重置**

   将屏幕上显示的参数重置为上次保存的参数。

* **删除**

   删除当前配置。 如果为标准，则参数将返回到默认设置。 如果从工厂配置创建，则特定实例将被删除。

* **解除绑定**

   从包中取消绑定当前配置。

* **取消**

   取消当前所做的任何更改。

## 捆绑 {#bundles}

“包 **”选项卡** ，用于安装AEM所需的OSGi包。 该选项卡可通过以下任一方法访问：

* 下拉菜单：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/bundles`

将显示包列表：

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

使用此选项卡，您可以：

* **安装或更新**

   您可以 **通过浏览** ，查找包含捆绑的文件，并指定它是否应立即开始 **，以及开始** 级别 ****。

* **重新加载**

   刷新显示的列表。

* **刷新包**

   这将检查所有包的引用，并根据需要刷新。

   例如，在更新后，由于先前的引用，旧版本和新版本可能仍在运行。 此选项将检查并移动对新版本的所有引用，从而允许停止旧版本。

* **开始**

   根据指定的开始级别启动捆绑。

* **停止**

   停止捆绑。

* **卸载**

   从系统中卸载捆绑包。

* **查看状态**

   该列表指定了捆绑的当前状态；单击特定捆绑包的名称，并显示更多信息。

>[!NOTE]
>
>更新 **后** ，建议执行刷新 **包**。

## 组件 {#components}

在“ **组件** ”选项卡中，您可以启用和／或禁用各种组件。 可通过以下任一方式访问它：

* 下拉菜单：

   **主要 >**

* URL;例如：

   `http://localhost:4502/system/console/components`

此时将显示组件列表。 可以使用各种图标来启用、禁用或（在适当时）打开特定组件的配置详细信息。

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

单击特定组件的名称将显示有关其状态的更多信息。 您还可以在此启用、禁用或重新加载组件。

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>启用或禁用组件时，组件仅在AEM/CRX重新启动之前才适用。
>
>在组件描述符中定义开始状态，该描述符在开发过程中生成并在包创建时存储在包中。

