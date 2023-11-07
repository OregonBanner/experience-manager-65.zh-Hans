---
title: 艰难的一天
description: Tough Day测试模拟了在所有操作同时进行的最坏情况下约1000位作者的日常负载。
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 2%

---

# 艰难的一天{#tough-day}

## 第2天是多么艰难 {#what-is-tough-day}

“Touch Day 2”是一个应用程序，可用于对AEM实例的限制进行压力测试。 它可以直接与默认测试套件一起运行，也可以根据测试需要进行配置。 你可以看 [此录制](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) 以展示应用程序。

>[!CAUTION]
>
>“第2天很艰难”需要使用Java™ 8。

## 如何应对艰难的第2天 {#how-to-run-tough-day}

从以下网站下载最新版本的“Tough Day 2（棘手第2天）”： [Adobe存储库](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). 下载应用程序后，您可以通过提供 `host` 参数。 在以下示例中，AEM实例在本地运行，因此 `localhost` 值中使用了：

```xml
java -jar toughday2.jar --host=localhost
```

添加参数后运行的默认套件名为 `toughday`. 它包含以下用例：

* 为其创建页面和活动副本（包括转出）
* 获取主页
* 在querybuilder中运行查询
* 创建资源层次结构
* 删除资源

该套件包含15%的写入操作和85%的读取操作。

要运行包测试，Tough Day 2将安装其默认内容包。 可以通过设置 `installsamplecontent`参数至 `false`，但请记住，您还应该更改要运行的测试的默认路径。 如果在没有参数的情况下运行jar，则“Tough Day 2”（严格第2天）将显示 [帮助信息](/help/sites-developing/tough-day.md#getting-help).

通常，您可以按照以下模式使用该应用程序：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
第2天非常艰难，没有清理步骤。 因此，建议在克隆的暂存实例上而不是在主生产实例上运行第2天非常困难。 应在测试后删除暂存实例。
>

### 获取帮助 {#getting-help}

Tough Day 2提供了多种帮助选项，可从命令行访问。 例如：

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
   <td>打印出所有可用的发布者。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>打印测试类及其说明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>打印以上所有内容，以及测试、发布器和套件组件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>列出有关指定的运行或发布模式的信息。</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>列出给定包的所有测试及其各自的可配置属性。</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> 列出具有指定标记的所有项目。</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td> — 帮助 &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 列出给定测试或发布者的所有可配置属性。</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar — 帮助CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全局参数 {#global-parameters}

Tough Day 2提供了用于设置或更改测试环境的全局参数。 这些资源包括目标主机、端口号、使用的协议、实例的用户和密码等等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在下面的列表中找到相关参数：

| **参数** | **描述** | **默认值** | **可能值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安装或跳过默认的“第2天困难”内容包。 | true | true或false |
| `--protocol=<Val>` | 用于主机的协议。 | http | http或https |
| `--host=<Val>` | 要定位的主机名或IP。 |  |  |
| `--port=<Val>` | 主机的端口。 | 4502 |  |
| `--user=<Val>` | 实例的用户名。 | 管理员 |  |
| `--password=<Val>` | 给定用户的密码。 | 管理员 |  |
| `--duration=<Val>` | 测试的持续时间。 可以表达为(**s**)秒，(**m**)分钟，(**h**)我们的和(**d**)天。 | 1d |  |
| `--timeout=<Val>` | 测试将运行多长时间，才会被中断并标记为失败。 以秒为单位表示。 | 180 |  |
| `--suite=<Val>` | 该值可以是预定义测试包中的一个或列表（以逗号分隔）。 | toughday |  |
| `--configfile=<Val>` | 目标yaml配置文件。 |  |  |
| `--contextpath=<Val>` | 实例的上下文路径。 |  |  |
| `--loglevel=<Val>` | Tough Day 2引擎的日志级别。 | 信息 | 全部，调试，信息，警告，错误，致命，关闭 |
| `--dryrun=<Val>` | 如果为true，则打印生成的配置并且不运行任何测试。 | false | true或false |

## 自定义 {#customizing}

可通过两种方式实现自定义：命令行参数或yaml配置文件。 **配置文件用于大型自定义套件，它们会覆盖Tough Day 2默认参数。 命令行参数会覆盖配置文件和缺省参数。**

保存测试配置的唯一方法是以yaml格式复制它。

### 添加新测试 {#adding-a-new-test}

如果您不想使用默认 `toughday` 套件，您可以通过使用 `add` 参数。 以下示例显示如何添加 `CreateAssetTreeTest` 使用命令行参数或yaml配置文件进行测试。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

通过使用yaml配置文件：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 添加同一测试的多个实例  {#adding-multiple-instances-of-the-same-test}

您还可以添加和运行同一测试的多个实例，但每个实例必须具有唯一的名称。 以下示例说明如何使用命令行参数或yaml配置文件添加同一测试的两个实例。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

通过使用yaml配置文件：

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

如果需要更改一个或多个测试属性，可将该属性添加到命令行或yaml配置文件中。 要查看所有可用的测试属性，请添加 `--help <TestClass/PublisherClass>` 命令行参数，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

请记住， yaml配置文件将覆盖Touch Day 2默认参数，而命令行参数将覆盖配置文件和默认值。

以下示例显示如何更改 `template` 的属性 `CreatePageTreeTest` 使用命令行参数或yaml配置文件进行测试。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

通过使用yaml配置文件：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 使用预定义的测试包 {#working-with-predefined-test-suites}

以下示例显示如何向预定义套件添加测试，以及如何重新配置和从预定义套件中排除现有测试。

您可以使用向预定义套件添加新测试 `add` 参数和指定目标预定义套件。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

通过使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

还可以使用重新配置给定套件中的现有测试。 `config`* *参数。 您还必须指定套件名称和测试的实际名称（而不是测试类名称）。 您可以在以下位置找到测试名称 `name` Test类的属性。 有关如何查找测试属性的详细信息，请参阅 [更改测试属性](/help/sites-developing/tough-day.md#changing-the-test-properties) 部分。

在以下示例中，的默认资产标题 `CreatePageTreeTest` (已命名 `UploadAsset`)被更改为“NewAsset”。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

通过使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

此外，您还可以通过使用，将测试从默认配置中删除预定义套件或发布者的测试 `exclude` 参数。 您还必须指定套件名称和测试的实际名称（而不是测试C） `lass` 名称)。 您可以在以下位置找到测试名称 `name` 测试类的属性。 在以下示例中， `CreatePageTreeTest` (已命名 `UploadAsset`)从toughday套件中删除测试。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

通过使用yaml配置文件：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 运行模式 {#run-modes}

“第2天非常艰难”可以使用以下模式之一运行： **普通** 和 **恒定载荷**.

此 **普通** 运行模式有两个参数：

* `concurrency` - concurrency表示“第2天”将为测试执行创建的线程数。 在这些线程上，将执行测试，直到持续时间耗尽或没有其他要执行的测试为止。

* `waittime`  — 同一线程上两次连续测试执行之间的等待时间。 该值必须以毫秒为单位表示。

以下示例说明如何使用命令行添加参数：

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

此 **恒定载荷** 运行模式与正常运行模式不同，它生成的是固定数量的已启动测试执行，而不是固定数量的线程。 可以使用同名的运行模式参数来设置载荷。

### 测试选择 {#test-selection}

两种运行模式的测试选择过程相同，如下所示：所有测试都有 `weight` 属性，确定线程中执行的可能性。 例如，如果您有两个测试，一个权重为5，另一个权重为10，则后者比前者执行的可能性高两倍。

此外，测试可以具有 `count` 属性，用于将执行次数限制为给定数字。 通过此数字后，将不会再执行测试。 所有已运行的测试实例都将按配置完成运行。 以下示例说明如何在命令行或使用yaml配置文件添加这些参数。

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
由于并行执行，测试运行的实际数量不会完全等于 `count` 参数。 期望偏差与正在运行的线程数成比例(由 `concurrency parameter`)。

### 练习 {#dry-run}

试运行将解析所有给定的输入（命令行参数或配置文件），将其与默认值合并，然后输出结果。 它不会执行任何测试。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 输出 {#output}

“第2天”比较困难，会输出测试指标和日志。 有关详细信息，请阅读以下部分。

### 测试指标 {#test-metrics}

“第2天非常艰难”当前报告了9个您可以评估的测试指标。 包含的量度 **&#42;** 符号仅在成功运行后报告：

| **名称** | **描述** |
|---|---|
| 时间戳 | 上次完成的测试运行的时间戳。 |
| 已通过 | 成功运行的次数。 |
| 失败 | 失败的运行数。 |
| 最小&#42; | 测试执行的最短持续时间。 |
| Max&#42; | 测试执行的最长持续时间。 |
| 中等&#42; | 计算的所有测试执行的中位持续时间。 |
| 平均&#42; | 计算的所有测试执行的平均持续时间。 |
| 标准开发&#42; | 标准偏差。 |
| 90p&#42; | 百分之90。 |
| 99p&#42; | 99%。 |
| 99.9p&#42; | 99.9%。 |
| 实际吞吐量&#42; | 运行次数除以经过的执行时间。 |

这些量度是在发布者的帮助下编写的，发布者可以使用 `add` 参数（与添加测试类似）。 目前，有两个选项：

* **CSVPublisher**  — 输出为CSV文件。
* **控制台发布者**  — 控制台中将显示输出。

默认情况下，这两个发布者均处于启用状态。

此外，还有两种报告量度的模式：

* 此 **简单** 发布模式 — 报告从执行开始到发布时的结果。
* 此 **间隔** 发布模式 — 报告给定时间范围内的结果。 您可以使用以下方式设置时间范围 **间隔** 发布模式参数。

以下示例说明如何配置 `intervals` 命令行中的参数或使用yaml配置文件中的参数。

通过使用命令行参数：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

通过使用yaml配置文件：

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 日志记录 {#logging}

“Tough Day 2”会在您运行“Tough Day 2”的同一目录中创建一个日志文件夹。 此文件夹包含两种类型的日志：

* **toughday.log**：包含与应用程序状态、调试信息和全局消息相关的消息。
* **toughday_&lt;testname>.log**：与指定测试相关的消息。

不会覆盖日志，后续运行会将消息附加到现有日志。 日志包含多个级别，有关详细信息，请参阅 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
