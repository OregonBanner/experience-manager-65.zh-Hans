---
title: 运行模式
seo-title: Run Modes
description: 了解如何使用运行模式根据特定目的调整AEM实例。
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: 7d91fbdaae7ade27e9d6bf42bbcd5b16d3f6e358
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 运行模式{#run-modes}

运行模式允许您针对特定目的调整AEM实例；例如，创作或发布、测试、开发、内联网或其他目的。

您可以：

* [为每个运行模式定义配置参数集合](#defining-configuration-properties-for-a-run-mode).

   基本配置参数集适用于所有运行模式，然后您可以根据特定环境的目的调整其他配置集。 根据需要应用这些规则。

* [定义要为特定模式安装的其他包](#defining-additional-bundles-to-be-installed-for-a-run-mode).

所有设置和定义都存储在一个存储库中，并通过设置 **运行模式**.

## 安装运行模式 {#installation-run-modes}

安装（或固定）运行模式在安装时使用，然后在实例的整个生命周期内固定，这些模式无法更改。

提供开箱即用的安装运行模式：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

它们是两对互斥的运行模式；例如，您可以：

* 定义 `author` 或 `publish`，而不是同时执行两者

* 合并 `author` 具有任一 `samplecontent` 或 `nosamplecontent` （但不是两者）

>[!CAUTION]
>
>使用上述运行模式之一(author、publish、samplecontent、nosamplecontent)时，安装时使用的值定义 *整个生命周期* 那个装置的。
>
>对于这些运行模式 *无法* 安装后更改它们。

## 自定义运行模式 {#customized-run-modes}

您还可以创建自己的自定义运行模式。 这些组件可以组合起来以涵盖以下场景：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 根据需要。..

每次启动时也可以选择定制的运行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

这些模式允许您控制示例内容的使用。 示例内容是在构建快速入门之前定义的，可以包含包、配置等：

* 此 `samplecontent` 运行模式将安装此内容（默认模式）。

* 此 `nosamplecontent` 模式将不会安装示例内容。

nosamplecontent运行模式专为生产安装而设计。

## 定义运行模式的配置属性 {#defining-configuration-properties-for-a-run-mode}

用于特定运行模式的配置属性值集合可以保存在存储库中。

运行模式由文件夹名称上的后缀表示。 这样，您可以将所有配置作为存储在一个存储库中。 例如：

* `config`

   适用于所有运行模式

* `config.author`

   用于作者运行模式

* `config.publish`

   用于发布运行模式

* `config.<run-mode>`

   用于适用的运行模式；例如，配置

参见 [存储库中的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 有关定义这些文件夹中的各个配置节点以及为多个运行模式的组合创建配置的更多详细信息。

>[!NOTE]
>
>对象 [安装运行模式](#installation-run-modes) 安装后无法更改运行模式（例如，作者）。 但是，对单个配置属性的更改将在重新启动后生效。

## 定义要为运行模式安装的其他包 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

还可以指定应该为特定运行模式安装的其他包。 对于这些定义，使用安装文件夹来保存捆绑包。 运行模式同样由前缀表示：

* `install.author`
* `install.publish`

这些文件夹的类型为 `nt:folder` 和应包含相应的捆绑包。

## 使用特定运行模式启动CQ {#starting-cq-with-a-specific-run-mode}

如果您为多个运行模式定义了配置，则需要定义要在启动时使用的配置。 有多种方法可指定要使用的运行模式；分辨率的顺序为：

1. [系统属性(](#using-a-system-property-in-the-start-script)
1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [文件名检测](#filename-detection-renaming-the-jar-file)

在使用应用程序服务器时，您还可以 [在web.xml中定义运行模式](#defining-the-run-mode-in-web-xml-with-application-server).

### 使用sling.properties文件 {#using-the-sling-properties-file}

此 `sling.properties` 文件可用于定义所需的运行模式：

1. 编辑配置文件：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下属性；以下示例适用于作者：

   `sling.run.modes=author`

### 使用 — r选项 {#using-the-r-option}

可以使用激活自定义运行模式 `-r` 选项。 例如，使用以下命令启动运行模式设置为dev的AEM实例。”

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在启动脚本中使用系统属性 {#using-a-system-property-in-the-start-script}

启动脚本中的系统属性可用于指定运行模式。

* 例如，使用以下内容将实例作为位于美国的生产发布实例启动：

   `-Dsling.run.modes=publish,prod,us`

### 文件名检测 — 重命名jar文件 {#filename-detection-renaming-the-jar-file}

通过在安装之前重命名安装jar文件，可以激活以下两种安装运行模式：

* 发布
* 作者

jar文件必须使用命名约定：

`cq5-<run-mode>-p<port-number>`

例如，设置 `publish` 通过命名jar文件运行模式：

`cq5-publish-p4503`

### 在web.xml中定义运行模式（使用应用程序服务器） {#defining-the-run-mode-in-web-xml-with-application-server}

在使用应用程序服务器时，还可以配置属性：

`sling.run.modes`

在文件中：

`WEB-INF/web.xml`

这在AEM中 `war` 文件，应在部署之前更新。

参见 [在应用程序服务器中安装AEM](/help/sites-deploying/application-server-install.md) 了解更多详细信息。
