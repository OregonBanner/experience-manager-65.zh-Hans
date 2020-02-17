---
title: 艰难的一天
seo-title: 艰难的一天
description: “艰难日”测试模拟在最坏情况下约1000位作者的日负载，同时执行所有操作。
seo-description: “艰难日”测试模拟在最坏情况下约1000位作者的日负载，同时执行所有操作。
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 艰难的一天{#tough-day}

## 艰难的一天2 {#what-is-tough-day}

“Tough Day 2”是一个应用程序，它允许您强调测试AEM实例的限制。 它可以随默认测试套件一起运行，也可以根据测试需求进行配置。 您可以观 [看此录制](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) ，以呈现应用程序。

## 如何经营艰难的一天2 {#how-to-run-tough-day}

从 [Adobe Repository下载Tough Day 2的最新版本](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)。 下载应用程序后，您可以通过提供参数来立即运行该应用 `host` 程序。 在以下示例中，AEM实例在本地运行，因此 `localhost` 使用该值：

```xml
java -jar toughday2.jar --host=localhost
```

添加参数后运行的默认套件名为 `toughday`。 它包含以下用例：

* 为其创建页面和Live Copy（包括转出）
* 获取主页
* 在querybuilder中运行查询
* 创建资产层次结构
* 删除资产

该套件包含15%的写入操作和85%的读取操作。

要运行套件测试，Tough Day 2将安装其默认内容包。 通过将参数设置为可以避 `installsamplecontent`免这种情 `false`况，但请记住，您还应更改要运行的测试的默认路径。 如果jar在运行时没有参数，则第2天将显示帮 [助信息](/help/sites-developing/tough-day.md#getting-help)。

通常，您可以通过以下模式使用应用程序：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>艰难的第2天没有清理步骤。 因此，建议在克隆的暂存实例上运行Tough Day 2，而不是在主生产实例上运行。 测试后应删除暂存实例。


### 获取帮助 {#getting-help}

Tough Day 2提供了各种帮助选项，可从命令行访问这些选项。 例如：

```xml
java -jar toughday2.jar --help_full
```

在下表中，您可以找到相关的帮助参数。

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>示例</strong></td>
  </tr>
  <tr>
   <td>--帮助</td>
   <td>打印全局信息，例如：可用的操作、预定义的套件、运行模式和全局参数。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>打印所有可用的发布者。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>打印测试类及其说明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>打印以上所有组件，以及测试、发布者和套件组件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>列出有关指定运行或发布模式的信息。</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>列出给定套件的所有测试及其各自的可配置属性。</td>
   <td><br /> java -jar toughday2.jar —help —suite=get=tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> 列出具有指定标记的所有项目。</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> 列出给定测试或发布者的所有可配置属性。</td>
   <td><p>java -jar toughday2.jar —help UploadPDFest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全局参数 {#global-parameters}

Tough Day 2提供全局参数，用于设置或更改测试环境。 这些包括目标主机、端口号、使用的协议、实例的用户和口令等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在以下列表中找到相关参数：

| **参数** | **描述** | **默认值** | **可能的值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安装或跳过默认的Tough Day 2内容包。 | true | true或false |
| `--protocol=<Val>` | 用于主机的协议。 | http | http或https |
| `--host=<Val>` | 目标主机名或IP。 |  |  |
| `--port=<Val>` | 主机的端口。 | 4502 |  |
| `--user=<Val>` | 实例的用户名。 | 管理员 |  |
| `--password=<Val>` | 给定用户的口令。 | 管理员 |  |
| `--duration=<Val>` | 测试的持续时间。 可以以(**s**)秒、(**m)分钟、(** h **)和(****** d)秒表示。 | 1d |  |
| `--timeout=<Val>` | 测试在中断并标记为失败之前将运行多长时间。 以秒为单位表示。 | 180 |  |
| `--suite=<Val>` | 该值可以是预定义测试套件的一个或一个列表（以逗号分隔）。 | 强势 |  |
| `--configfile=<Val>` | 目标yaml配置文件。 |  |  |
| `--contextpath=<Val>` | 实例的上下文路径。 |  |  |
| `--loglevel=<Val>` | Tough Day 2引擎的日志级别。 | 信息 | 全部，调试，信息，警告，错误，致命，关闭 |
| `--dryrun=<Val>` | 如果为true，则打印生成的配置，但不运行任何测试。 | false | true或false |

## 自定义 {#customizing}

可以通过两种方式实现自定义：命令行参数或yaml配置文件。 **配置文件通常用于大型自定义套件，并且它们将覆盖第2天的默认参数。 命令行参数将覆盖配置文件和默认参数。**

保存测试配置的唯一方法是以yaml格式复制它。 有关其他详细信息，请 [参阅此toughday.yaml配置](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) ，以及以下各节中的yaml配置示例。

### 添加新测试 {#adding-a-new-test}

如果不想使用默认套件，可 `toughday` 以使用参数添加您选择的测 `add` 试。 以下示例显示如何使用命 `CreateAssetTreeTest` 令行参数或yaml配置文件添加测试。

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

### 添加同一测试的多个实例 {#adding-multiple-instances-of-the-same-test}

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

如果需要更改一个或多个测试属性，可将该属性添加到命令行或主配置文件。 要查看所有可用的测试属性，请 `--help <TestClass/PublisherClass>` 将参数添加到命令行，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

请记住，yaml配置文件将覆盖第2天的默认参数，命令行参数将覆盖配置文件和默认值。

以下示例显示如何使用命令行 `template` 参数或 `CreatePageTreeTest` yaml配置文件来更改测试的属性。

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

### 使用预定义的测试套件 {#working-with-predefined-test-suites}

以下示例演示如何将测试添加到预定义的套件以及如何从预定义的套件重新配置和排除现有测试。

您可以使用该参数并指定目标预定义套件，将 `add` 新测试添加到预定义套件。

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

给定套件中的现有测试也可以使用 `config`* *参数进行重新配置。 请注意，您还必须指定测试的套件名称和实际名称（而非测试类名称）。 可以在测试类的属性中 `name` 找到测试名称。 有关如何查找测试属性的更多详细信息，请阅读更改 [测试属性部分](/help/sites-developing/tough-day.md#changing-the-test-properties) 。

在下面的示例中，（已命名）的默 `CreatePageTreeTest` 认资产标 `UploadAsset`题将更改为“NewAsset”。

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

此外，您还可以使用参数从默认配置中删除预定义套件或发布者的测 `exclude` 试。 请注意，您还必须指定测试的套件名称和实际名称(而非测试C `lass` 名称)。 可以在测试类的属性中 `name` 找到测试名称。 在以下示例中， `CreatePageTreeTest` (已命 `UploadAsset`名)测试从toughday套件中删除。

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

Tough Day 2可以在以下模式之一中运行：正 **常和****恒定负载**。

正常 **运行模** 式有两个参数：

* `concurrency` -并发表示第2天为执行测试而创建的线程数。 在这些线程上，将执行测试，直到持续时间已用完或不再执行测试为止。

* `waittime` -同一线程上两个连续测试执行之间的等待时间。 该值必须以毫秒表示。

以下示例说明如何使用命令行添加参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

或者，使用yaml配置文件：

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

恒 **定负载运行模式** ，通过生成恒定数目的开始测试执行而不是恒定数目的线程，与正常运行模式不同。 可以使用同名的运行模式参数来设置负载。

### 测试选择 {#test-selection}

对于两种运行模式，测试选择过程相同，其步骤如下：所有测试都有 `weight` 一个属性，它决定了在线程中执行的可能性。 例如，如果我们有两项测试，一项重量为5，另一项重量为10，则执行后者的可能性是前者的两倍。

此外，测试可以具有一 `count` 个属性，该属性将执行次数限制为给定数量。 通过此数字后，将不再执行测试。 所有已运行的测试实例将按照配置完成运行。 以下示例演示如何在命令行中或使用yaml配置文件添加这些参数。

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
>由于并行执行，实际测试运行数将不完全等于参数中配置的数 `count` 量。 期望与运行线程数成比例的偏差(由控 `concurrency parameter`制)。

### 练习 {#dry-run}

练习将解析所有给定输入（命令行参数或配置文件），将其与默认值合并，然后输出结果。 它不执行任何测试。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 输出 {#output}

Tough Day 2输出测试指标和日志。 有关更多详细信息，请阅读以下部分。

### 测试指标 {#test-metrics}

艰难的第2天目前报告9个可评估的测试指标。 具有 ***符号的度量仅在成功运行** 后才会报告：

| **名称** | **描述** |
|---|---|
| 时间戳 | 上次完成测试运行的时间戳。 |
| 已通过 | 成功运行的数量。 |
| 失败 | 失败的运行数。 |
| 最小* | 测试执行的最短持续时间。 |
| 最大* | 测试执行的最长持续时间。 |
| 中等* | 计算所有测试执行的中值持续时间。 |
| 平均* | 计算所有测试执行的平均持续时间。 |
| StdDev* | 标准差。 |
| 90p* | 90百分点。 |
| 99p* | 99个百分点。 |
| 99.9p* | 99.9百分点。 |
| 实际吞吐量* | 运行数除以已用执行时间。 |

这些度量是在发布者的帮助下编写的，发布者可以随参 `add` 数一起添加（与添加测试类似）。 目前，有两种选择：

* **CSVPublisher** —— 输出为CSV文件。
* **ConsolePublisher** —— 输出显示在控制台中。

默认情况下，两个发布者均处于启用状态。

此外，还有两种报告度量的模式：

* 简 **单发布模式** -报告从执行开始到发布点的结果。
* 间隔 **发布模式** -在给定的时间范围内报告结果。 可以使用间隔发布模式参数设 **置时间** 范围。

以下示例演示如何在命令行 `intervals` 或使用yaml配置文件配置参数。

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

### 记录 {#logging}

Tough Day 2在运行Tough Day 2的同一目录中创建日志文件夹。 此文件夹包含两种类型的日志：

* **toughday.log**:包含与应用程序状态、调试信息和全局消息相关的消息。
* **toughday_&lt;testname>.log**:与指定测试相关的消息。

日志不会被覆盖，后续运行会将消息附加到现有日志中。 日志有多个级别，有关详细信息，请参阅 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`。

#### 示例使用 {#example-usage}

#### 已知问题 {#known-issues}

[获取文件](assets/toughday-6_1.jar)
