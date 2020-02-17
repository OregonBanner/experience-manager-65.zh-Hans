---
title: 运行模式
seo-title: 运行模式
description: 了解如何使用运行模式调整AEM实例以用于特定用途。
seo-description: 了解如何使用运行模式调整AEM实例以用于特定用途。
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 运行模式{#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发、内部网或其他内容。

您可以：

* [为每个运行模式定义配置参数的集合](#defining-configuration-properties-for-a-run-mode)。

   基本的配置参数集将应用于所有运行模式，然后您可以根据特定环境的目的调整其他设置。 这些功能会根据需要应用。

* [定义要为特定模式安装的其他捆绑包](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有设置和定义都存储在一个存储库中，并通过设置“运行模式” **来激活**。

## 安装运行模式 {#installation-run-modes}

安装（或固定）运行模式在安装时使用，然后在实例的整个生命周期中对其进行修复，这些模式无法更改。

现成提供安装运行模式：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

这是两对互斥的运行模式；例如，您可以：

* 同时定 `author` 义或 `publish`（而非同时定义两者）

* 组合 `author` 使用 `samplecontent` 或(但 `nosamplecontent` 不同于两者)

>[!CAUTION]
>
>当使用上述运行模式之一（作者、发布、示例内容、nosamplecontent）时，安装时使用的值定义该安装的整个生命周期 *的运行模式* 。
>
>对于这些运行模式，您 *在安装* 后无法更改它们。

## 自定义运行模式 {#customized-run-modes}

您还可以创建自己的自定义运行模式。 可以将这些组合起来，以涵盖以下场景：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 根据需要。..

也可以在每次启动时选择自定义的运行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

这些模式允许您控制示例内容的使用。 在构建快速入门之前定义示例内容，其中可以包括包、配置等：

* 运行 `samplecontent` 模式将安装此内容（默认模式）。

* 此模 `nosamplecontent` 式将不会安装示例内容。

nosamplecontent运行模式设计用于生产安装。

## 为运行模式定义配置属性 {#defining-configuration-properties-for-a-run-mode}

配置属性的值集合（用于特定运行模式）可保存在存储库中。

运行模式由文件夹名称的后缀指示。 这允许您将所有配置作为存储在一个存储库中。 例如：

* `config`

   适用于所有运行模式

* `config.author`

   用于创作运行模式

* `config.publish`

   用于发布运行模式

* `config.<run-mode>`

   用于适用的运行模式；例如，config

有关在 [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 这些文件夹中定义单个配置节点以及为多种运行模式组合创建配置的更多详细信息，请参阅存储库中的OSGi配置。

>[!NOTE]
>
>对 [于安装运行模式](#installation-run-modes) （例如作者），安装后无法更改运行模式。 但是，对单个配置属性所做的更改将在重新启动后生效。

## 定义要为运行模式安装的其他捆绑包 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

还可以指定应为特定运行模式安装的其他捆绑包。 对于这些定义，安装文件夹用于保存包。 同样，运行模式由前缀表示：

* `install.author`
* `install.publish`

这些文件夹的类型 `nt:folder` 是，应包含相应的捆绑包。

## 以特定运行模式启动CQ {#starting-cq-with-a-specific-run-mode}

如果您为多种运行模式定义了配置，则需要定义启动时要使用的配置。 有多种方法可指定要使用的运行模式；决议的顺序是：

1. [ `sling.properties` 文件](#using-the-sling-properties-file)
1. [ `-r` 选项](#using-the-r-option)
1. [系统属性(`-D`)](#using-a-system-property-in-the-start-script)

1. [文件名检测](#filename-detection-renaming-the-jar-file)

当您使用应用程序服务器时，还 [可以在web.xml中定义运行模式](#defining-the-run-mode-in-web-xml-with-application-server)。

### 使用sling.properties文件 {#using-the-sling-properties-file}

文 `sling.properties` 件可用于定义所需的运行模式：

1. 编辑配置文件：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下属性；以下示例适用于作者：

   `sling.run.modes=author`

### 使用-r选项 {#using-the-r-option}

启动快速启动时，可使用选项 `-r` 激活自定义运行模式。 例如，使用以下命令启动运行模式设置为dev的AEM实例。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在启动脚本中使用系统属性 {#using-a-system-property-in-the-start-script}

启动脚本中的系统属性可用于指定运行模式。

* 例如，使用以下方法将实例作为位于美国的生产发布实例启动：

   `-Dsling.run.modes=publish,prod,us`

### 文件名检测——重命名jar文件 {#filename-detection-renaming-the-jar-file}

可以在安装前重命名安装jar文件来激活以下两种安装运行模式：

* 发布
* 作者

jar文件必须使用命名约定：

`cq5-<run-mode>-p<port-number>`

例如，通过命名 `publish` jar文件来设置运行模式：

`cq5-publish-p4503`

### 在web.xml中定义运行模式（使用Application Server） {#defining-the-run-mode-in-web-xml-with-application-server}

在使用应用程序服务器时，您还可以配置以下属性：

`sling.run.modes`

在文件中：

`WEB-INF/web.xml`

它位于AEM文件中， `war` 应在部署前进行更新。

有关更 [多详细信息，请参阅使用应用程序服务器安装AEM](/help/sites-deploying/application-server-install.md) 。
