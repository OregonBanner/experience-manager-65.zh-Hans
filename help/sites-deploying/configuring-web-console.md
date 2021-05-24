---
title: Web 控制台
seo-title: Web 控制台
description: 了解如何在AEM中使用Web控制台。
seo-description: 了解如何在AEM中使用Web控制台。
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Web 控制台{#web-console}

AEM中的Web控制台基于[Apache Felix Web管理控制台](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html)。 Apache Felix是为实施OSGi R4服务平台（包括OSGi框架和标准服务）而做出的社区努力。

>[!NOTE]
>
>在Web控制台中，任何提及默认设置的描述都与Sling默认值相关。
>
>AEM有其自己的默认值，因此默认设置可能与控制台中记录的默认值不同。

Web控制台提供了一系列用于维护OSGi包的选项卡，包括：

* [配置](#configuration):用于配置OSGi包，因此是配置AEM系统参数的基础机制
* [包](#bundles):用于安装包
* [组件](#components):用于控制AEM所需组件的状态

所做的任何更改都会立即应用于正在运行的系统。 无需重新启动。

可以从`../system/console`访问控制台；例如：

`http://localhost:4502/system/console/components`

## 配置 {#configuration}

**Configuration**&#x200B;选项卡用于配置OSGi包，因此是配置AEM系统参数的基础机制。

>[!NOTE]
>
>有关更多详细信息，请参阅使用Web控制台进行的[OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 。

**Configuration**&#x200B;选项卡可通过以下任一方式访问：

* 下拉菜单：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/configMgr`

将显示配置列表：

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

此屏幕上的下拉列表提供了两种类型的配置：

* **配置**

   用于更新现有配置。 它们具有永久标识(PID)，可以是：

   * 标准及AEM的完整性；如果删除了这些值，则需要使用这些值，这些值将返回默认设置。
   * 从工厂配置创建的实例；这些实例由用户创建，删除后将删除该实例。

* **工厂配置**

   用于创建所需功能对象的实例。

   这将分配一个永久标识，然后列在配置下拉列表中。

从列表中选择任何条目将显示与该配置相关的参数：

![chlimage_1-61](assets/chlimage_1-61.png)

然后，您可以根据需要更新参数，并：

* **保存**

   保存所做的更改。

   对于工厂配置，这将创建一个具有永久标识的新实例。 然后，新实例将列在Configurations下。

* **重置**

   将屏幕上显示的参数重置为最后保存的参数。

* **删除**

   删除当前配置。 如果为标准，则参数将返回到默认设置。 如果从工厂配置创建，则会删除特定实例。

* **取消绑定**

   从包中取消绑定当前配置。

* **取消**

   取消任何当前更改。

## 包 {#bundles}

**Bundles**&#x200B;选项卡是安装AEM所需的OSGi包的机制。 可通过以下任一方法访问选项卡：

* 下拉菜单：

   **OSGi >**

* URL;例如：

   `http://localhost:4502/system/console/bundles`

将显示包列表：

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

使用此选项卡，您可以：

* **安装或更新**

   您可以&#x200B;**浏览**&#x200B;以查找包含包的文件，并指定它是否应立即启动&#x200B;****，在该启动级别&#x200B;**。**

* **重新加载**

   刷新显示的列表。

* **刷新包**

   这将检查所有包的引用，并根据需要刷新。

   例如，在更新后，由于以前的引用，旧版本和新版本可能仍在运行。 此选项将检查并移动对新版本的所有引用，从而允许停止旧版本。

* **开始**

   根据指定的开始级别启动包。

* **停止**

   停止捆绑。

* **卸载**

   从系统中卸载包。

* **查看状态**

   该列表指定包的当前状态；单击包含显示更多信息的特定包的名称。

>[!NOTE]
>
>在&#x200B;**Update**&#x200B;之后，建议执行&#x200B;**刷新包**。

## 组件 {#components}

**组件**&#x200B;选项卡允许您启用和/或禁用各种组件。 它可通过以下任一方式访问：

* 下拉菜单：

   **主要 >**

* URL;例如：

   `http://localhost:4502/system/console/components`

将显示组件列表。 您可以使用各种图标来启用、禁用或（适用时）打开特定组件的配置详细信息。

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

单击特定组件的名称将显示有关其状态的更多信息。 在此，您还可以启用、禁用或重新加载组件。

![chlimage_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>启用或禁用组件后，只有在AEM/CRX重新启动之前，组件才会应用。
>
>在组件描述符内定义开始状态，该描述符在开发期间生成，并在包创建时存储在包中。
