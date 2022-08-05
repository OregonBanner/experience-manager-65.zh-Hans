---
title: 艰难的一天
description: Tough Day测试在最坏情况下模拟大约1000位作者的每日负载，所有操作同时进行。
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: 1b92b973209fdbd2509b1c644c1064a1e9224a9e
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 2%

---

# 艰难的一天{#tough-day}

## 艰难的第2天 {#what-is-tough-day}

“Tough Day 2”是一个应用程序，它允许您压力测试AEM实例的限制。 它可以随默认测试包一起开箱即用，也可以根据您的测试需求对其进行配置。 您可以观看 [这个录音](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) 以呈现应用程序。

>[!CAUTION]
>
>艰难的第2天需要Java 8。

## 如何跑艰难的第2天 {#how-to-run-tough-day}

从 [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). 下载应用程序后，您可以通过提供 `host` 参数。 在以下示例中，AEM实例在本地运行，因此 `localhost` 值：

```xml
java -jar toughday2.jar --host=localhost
```

添加参数后运行的默认包名为 `toughday`. 它包含以下用例：

* 为其创建页面和Live Copy（包括转出）
* 获取主页
* 在querybuilder中运行查询
* 创建资产层次结构
* 删除资产

包中包含15%的写入操作和85%的读取操作。

要运行包测试， Tough Day 2将安装其默认内容包。 通过设置 `installsamplecontent`参数 `false`，但请记住，您还应更改要运行的测试的默认路径。 如果在没有参数的情况下运行该jar，则Tough Day 2会显示 [帮助信息](/help/sites-developing/tough-day.md#getting-help).

通常，您可以通过以下模式使用应用程序：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>艰难的第2天没有清理步骤。 因此，建议在克隆暂存实例上运行Tough Day 2，而不是在主生产实例上运行。 测试后应删除暂存实例。

### 获取帮助 {#getting-help}

艰难的第2天提供了从命令行访问的各种帮助选项。 例如：

```xml
java -jar toughday2.jar --help_full
```

在下表中，您可以找到相关帮助参数。

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>示例</strong></td>
  </tr>
  <tr>
   <td>--帮助</td>
   <td>打印全局信息，例如：可用的操作、预定义的包、运行模式和全局参数。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>打印所有可用的发布器。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>打印测试类及其说明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>打印上述所有组件，以及测试、发布者和包组件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>列出有关指定运行或发布模式的信息。</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>列出给定套件的所有测试及其各自的可配置属性。</td>
   <td><br /> java -jar toughday2.jar —help —suite=gettests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> 列出具有指定标记的所有项目。</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td> — 帮助 &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 列出给定测试或发布者的所有可配置属性。</td>
   <td><p>java -jar toughday2.jar — 帮助上载PDFTest</p> <p>java -jar toughday2.jar — 帮助CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全局参数 {#global-parameters}

艰难的第2天提供了全局参数，用于设置或更改测试环境。 这包括目标主机、端口号、使用的协议、实例的用户和密码等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在以下列表中找到相关参数：

| **参数** | **描述** | **默认值** | **可能值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安装或跳过默认的Tough Day 2内容包。 | true | true或false |
| `--protocol=<Val>` | 主机使用的协议。 | http | http或https |
| `--host=<Val>` | 要定位的主机名或IP。 |  |  |
| `--port=<Val>` | 主机的端口。 | 4502 |  |
| `--user=<Val>` | 实例的用户名。 | 管理员 |  |
| `--password=<Val>` | 给定用户的密码。 | 管理员 |  |
| `--duration=<Val>` | 测试的持续时间。 可以以(**s**)秒，(**m**)分钟，(**h**)和(**d**)ays。 | 1d |  |
| `--timeout=<Val>` | 测试在中断并标记为失败之前将运行多长时间。 以秒为单位。 | 180 |  |
| `--suite=<Val>` | 该值可以是预定义测试包的一个或列表（以逗号分隔）。 | toughday |  |
| `--configfile=<Val>` | 目标yaml配置文件。 |  |  |
| `--contextpath=<Val>` | 实例的上下文路径。 |  |  |
| `--loglevel=<Val>` | Tough Day 2引擎的日志级别。 | 信息 | 全部，调试，信息，警告，错误，致命，关闭 |
| `--dryrun=<Val>` | 如果为true，则打印生成的配置，并且不运行任何测试。 | false | true或false |

## 自定义 {#customizing}

可通过两种方式实现定制：命令行参数或yaml配置文件。 **配置文件通常用于大型自定义包，并将覆盖第2天的严格默认参数。 命令行参数覆盖配置文件和缺省参数。**

保存测试配置的唯一方法是以yaml格式复制该配置。

### 添加新测试 {#adding-a-new-test}

如果您不想使用默认 `toughday` 包中，您可以使用 `add` 参数。 以下示例显示如何将 `CreateAssetTreeTest` 使用命令行参数或yaml配置文件进行测试。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

使用yaml配置文件：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 添加同一测试的多个实例  {#adding-multiple-instances-of-the-same-test}

您还可以添加和运行同一测试的多个实例，但每个实例必须具有唯一的名称。 以下示例显示如何使用命令行参数或yaml配置文件添加同一测试的两个实例。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

使用yaml配置文件：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### 更改测试属性 {#changing-the-test-properties}

如果需要更改一个或多个测试属性，可将该属性添加到命令行或yaml配置文件中。 要查看所有可用的测试属性，请将 `--help <TestClass/PublisherClass>` 命令行参数，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

请记住，yaml配置文件将覆盖Tough Day 2默认参数，命令行参数将覆盖配置文件和默认参数。

以下示例显示如何更改 `template` 属性 `CreatePageTreeTest` 使用命令行参数或yaml配置文件进行测试。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

使用yaml配置文件：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 使用预定义测试包 {#working-with-predefined-test-suites}

以下示例显示如何向预定义包添加测试，以及如何从预定义包重新配置和排除现有测试。

您可以使用 `add` 参数和指定目标预定义包。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

给定包中的现有测试也可以使用 `config`* *参数。 请注意，您还必须指定测试的包名称和实际名称（而非测试类名称）。 您可以在 `name` 测试类的属性。 有关如何查找测试属性的更多详细信息，请阅读 [更改测试属性](/help/sites-developing/tough-day.md#changing-the-test-properties) 中。

在以下示例中， `CreatePageTreeTest` (已命名 `UploadAsset`)更改为“NewAsset”。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

此外，您还可以通过使用 `exclude` 参数。 请注意，您还必须指定测试的包名称和实际名称（而非测试C） `lass` 名称)。 您可以在 `name` 测试类的属性。 在以下示例中， `CreatePageTreeTest` (已命名 `UploadAsset`)测试。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 运行模式 {#run-modes}

艰难的第2天可以在以下模式之一中运行： **正常** 和 **恒定负载**.

的 **正常** 运行模式具有两个参数：

* `concurrency`  — 并发表示Tough第2天为测试执行创建的线程数。 在这些线程上，将执行测试，直到持续时间耗尽或不再执行测试为止。

* `waittime`  — 在同一线程上连续执行两次测试之间的等待时间。 值必须以毫秒为单位表示。

以下示例显示如何使用命令行添加参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

或者使用yaml配置文件：

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

的 **恒定负载** 运行模式与正常运行模式不同，它生成的是启动测试执行的常量数，而不是线程的常量数。 可以使用具有相同名称的运行模式参数来设置负载。

### 测试选择 {#test-selection}

两种运行模式的测试选择过程相同，其方式如下：所有测试都 `weight` 属性，该属性确定线程中执行的可能性。 例如，如果我们有两个测试，一个测试的权重为5，另一个测试的权重为10，则执行后者的可能性是前者的两倍。

此外，测试可以 `count` 属性，该属性将执行次数限制为给定数量。 在传递此数字后，将不再执行测试。 所有已运行的测试实例都将按照配置的方式完成运行。 以下示例显示如何在命令行中或使用yaml配置文件添加这些参数。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

或

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>由于并行执行，实际测试运行次数将不会与 `count` 参数。 期望与运行线程数成正比的偏差(由 `concurrency parameter`)。

### 练习 {#dry-run}

练习将解析所有给定输入（命令行参数或配置文件），并将其与默认值合并，然后输出结果。 它不执行任何测试。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 输出 {#output}

Tough Day 2可输出测试量度和日志。 有关更多详细信息，请阅读以下章节。

### 测试量度 {#test-metrics}

艰难的第2天当前报告了9个可评估的测试量度。 量度 **&#42;** 符号仅在成功运行后才报告：

| **名称** | **描述** |
|---|---|
| 时间戳 | 上次完成测试运行的时间戳。 |
| 已通过 | 成功运行的次数。 |
| 失败 | 失败的运行数。 |
| 最小&#42; | 测试执行的最短持续时间。 |
| 最大&#42; | 测试执行的最长持续时间。 |
| 中等&#42; | 计算所有测试执行的中间持续时间。 |
| 平均&#42; | 计算所有测试执行的平均持续时间。 |
| StdDev&#42; | 标准偏差。 |
| 90p&#42; | 第90个百分位数。 |
| 99便士&#42; | 第99个百分位数。 |
| 99.9便士&#42; | 第99.9个百分位数。 |
| 实际吞吐量&#42; | 运行次数除以已用执行时间。 |

这些量度是在发布者的帮助下编写的，发布者可以在 `add` 参数（与添加测试类似）。 目前有两个选项：

* **CSVPublisher**  — 输出为CSV文件。
* **ConsolePublisher**  — 输出显示在控制台中。

默认情况下，两个发布者均处于启用状态。

此外，还有两种报告量度的模式：

* 的 **简单** 发布模式 — 报告从执行开始到发布点的结果。
* 的 **间隔** 发布模式 — 报告给定时间范围内的结果。 您可以使用 **间隔** 发布模式参数。

以下示例显示如何配置 `intervals` 参数（在命令行中或使用yaml配置文件）。

使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

使用yaml配置文件：

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 日志记录 {#logging}

Tough Day 2会在运行Tough Day 2的同一目录中创建日志文件夹。 此文件夹包含两种类型的日志：

* **toughday.log**:包含与应用程序状态、调试信息和全局消息相关的消息。
* **toughday_&lt;testname>.log**:与指定测试相关的消息。

日志不会被覆盖，后续运行会将消息附加到现有日志。 日志具有多个级别，有关详细信息，请参阅 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
