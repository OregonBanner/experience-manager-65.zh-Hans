---
title: 运行模式
seo-title: 运行模式
description: 了解如何使用运行模式调整AEM实例以用于特定目的。
seo-description: 了解如何使用运行模式调整AEM实例以用于特定目的。
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: 配置
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 运行模式{#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发、内部网或其他。

您可以：

* [为每个运行模式定义配置参数的集合](#defining-configuration-properties-for-a-run-mode)。

   所有运行模式都应用一组基本的配置参数，然后您可以根据特定环境的目的调整其他集。 这些值将根据需要应用。

* [定义要为特定模式安装的其他包](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有设置和定义都存储在一个存储库中，并通过设置&#x200B;**运行模式**&#x200B;来激活。

## 安装运行模式{#installation-run-modes}

安装时使用安装（或固定）运行模式，然后在实例的整个生命周期内对其进行修复，这些模式将无法更改。

提供了现成的安装运行模式：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

这是两对相互排斥的运行模式；例如，您可以：

* 定义`author`或`publish`，但不能同时定义两者

* 将`author`与`samplecontent`或`nosamplecontent`组合（但不能同时与二者组合）

>[!CAUTION]
>
>使用上述运行模式之一（创作、发布、samplecontent、nosamplecontent）时，安装时使用的值定义该安装&#x200B;*整个生命周期*&#x200B;的运行模式。
>
>对于这些运行模式，*在安装后不能*&#x200B;更改它们。

## 自定义运行模式{#customized-run-modes}

您还可以创建自己的自定义运行模式。 这些选项可以组合在一起，以涵盖以下场景：

* `author` + `development`

* `publish` +  `test`

* `publish` +  `test` +  `golive`

* `publish` +  `intranet`

* （根据需要）。..

每次启动时也可以选择自定义运行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

利用这些模式，可控制示例内容的使用。 在构建快速入门之前定义示例内容，该内容可以包含包、配置等：

* `samplecontent`运行模式将安装此内容（默认模式）。

* `nosamplecontent`模式将不安装示例内容。

nosamplecontent运行模式专为生产安装而设计。

## 为运行模式{#defining-configuration-properties-for-a-run-mode}定义配置属性

配置属性的值集合（用于特定运行模式）可以保存在存储库中。

运行模式在文件夹名称上由后缀表示。 这样，您可以将所有配置作为存储在一个存储库中。 例如：

* `config`

   适用于所有运行模式

* `config.author`

   用于创作运行模式

* `config.publish`

   用于发布运行模式

* `config.<run-mode>`

   用于适用的运行模式；例如，config

有关定义这些文件夹中的各个配置节点以及为多个运行模式组合创建配置的更多详细信息，请参阅存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[OSGi配置。

>[!NOTE]
>
>对于[安装运行模式](#installation-run-modes)（例如作者），安装后无法更改运行模式。 但是，对单个配置属性所做的更改将在重新启动后生效。

## 定义要为运行模式{#defining-additional-bundles-to-be-installed-for-a-run-mode}安装的其他包

还可以指定应为特定运行模式安装的其他包。 对于这些定义，使用安装文件夹来保存包。 运行模式同样由前缀表示：

* `install.author`
* `install.publish`

这些文件夹的类型为`nt:folder`，应包含相应的包。

## 以特定运行模式{#starting-cq-with-a-specific-run-mode}启动CQ

如果您为多个运行模式定义了配置，则需要定义启动时要使用的配置。 可通过多种方法来指定要使用的运行模式；决议的顺序是：

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [系统属性(](#using-a-system-property-in-the-start-script)

1. [文件名检测](#filename-detection-renaming-the-jar-file)

使用应用程序服务器时，还可以[在web.xml](#defining-the-run-mode-in-web-xml-with-application-server)中定义运行模式。

### 使用sling.properties文件{#using-the-sling-properties-file}

`sling.properties`文件可用于定义所需的运行模式：

1. 编辑配置文件：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下属性；以下示例供作者使用：

   `sling.run.modes=author`

### 使用 — r选项{#using-the-r-option}

启动快速启动时，可以使用`-r`选项激活自定义运行模式。 例如，使用以下命令启动运行模式设置为dev的AEM实例。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在启动脚本{#using-a-system-property-in-the-start-script}中使用系统属性

启动脚本中的系统属性可用于指定运行模式。

* 例如，使用以下方法将一个实例作为位于美国的生产发布实例启动：

   `-Dsling.run.modes=publish,prod,us`

### 文件名检测 — 重命名jar文件{#filename-detection-renaming-the-jar-file}

可通过在安装前重命名安装jar文件来激活以下两种安装运行模式：

* 发布
* 作者

jar文件必须使用命名约定：

`cq5-<run-mode>-p<port-number>`

例如，通过命名jar文件来设置`publish`运行模式：

`cq5-publish-p4503`

### 在web.xml中定义运行模式（使用Application Server）{#defining-the-run-mode-in-web-xml-with-application-server}

使用应用程序服务器时，您还可以配置属性：

`sling.run.modes`

在文件中：

`WEB-INF/web.xml`

此文件位于AEM `war`文件中，应在部署之前进行更新。

有关更多详细信息，请参阅[将AEM与应用程序服务器一起安装](/help/sites-deploying/application-server-install.md) 。
