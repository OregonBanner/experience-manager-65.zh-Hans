---
title: AEM Forms中的Watched文件夹
description: 管理员可以将文件夹置于监视状态，并在文件置于监视的文件夹中时启动工作流、服务或脚本操作。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '7143'
ht-degree: 0%

---

# AEM Forms中的Watched文件夹{#watched-folder-in-aem-forms}

管理员可以配置网络文件夹（称为Watched文件夹），以便当用户将文件(如PDF文件)放入Watched文件夹时，可以启动预先配置的工作流、服务或脚本操作来处理添加的文件。 服务执行指定的操作后，将结果文件保存在指定的输出文件夹中。 有关工作流、服务和脚本的更多信息，请参阅 [处理文件的各种方法](#variousmethodsforprocessingfiles).

## 创建观察文件夹 {#create-a-watched-folder}

可以使用以下方法之一在文件系统上创建Watched文件夹：

* 在配置Watched Folder配置节点的属性时，在folderPath属性中键入父目录的完整路径，并附加要创建的Watched文件夹的名称，如以下示例所示： `C:/MyPDFs/MyWatchedFolder`
此 `MyWatchedFolder`文件夹不存在，AEM Forms会尝试在指定路径创建文件夹。

* 在配置Watched Folder端点之前，在文件系统上创建文件夹，然后在folderPath属性中提供完整路径。 有关folderPath属性的详细信息，请参见 [观察文件夹属性](#watchedfolderproperties).

>[!NOTE]
>
>在群集环境中，用作观察文件夹的文件夹必须在文件系统或网络上可访问、可写和共享。 群集的每个应用程序服务器实例都必须具有对同一共享文件夹的访问权限。 在Windows上，在所有服务器上创建一个映射的网络驱动器，并在folderPath属性中指定映射的网络驱动器的路径。

## 创建观察文件夹配置节点 {#create-watched-folder-configuration-node}

要配置Watched文件夹，请创建Watched文件夹配置节点。 执行以下步骤以创建配置节点：

1. 以管理员身份登录到CRX-DE Lite并导航到/etc/fd/watchfolder/config文件夹。

1. 创建节点类型 `nt:unstructured`. 例如， watchedfolder

   >[!NOTE]
   >
   >观察文件夹节点名称不能包含空格和特殊字符。

1. 将以下属性添加到节点：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   有关支持的属性的完整列表，请参阅 [观察文件夹属性](#watchedfolderproperties).

1. 单击&#x200B;**全部保存**。创建节点并保存属性后。 此 `input`， `result`， `failure`， `preserve`、和 `stage`文件夹是在指定的路径创建的 `folderPath` 属性。

   扫描作业以定义的时间间隔开始扫描观察文件夹。

## 观察文件夹属性 {#watchedfolderproperties}

您可以为Watched文件夹配置以下属性。

* **folderPath （字符串）**：在定义的时间间隔内扫描的文件夹的路径。 对于群集环境，文件夹必须位于共享位置，且所有服务器均具有服务器的完全访问权限。 它是必需属性。
* **inputProcessorType（字符串）**：要启动的进程类型。 您可以指定工作流、脚本或服务。 它是必需属性。
* **inputProcessorId（字符串）**：inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 它是必需属性。 以下列表详细列出了inputProcessorType属性的所有可能值以及inputProcessorType属性的相应先决条件：

   * 对于工作流，请指定要执行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：content/model
   * 对于脚本，请指定要执行的脚本的JCR路径。 例如， /etc/fd/watchfolder/test/testScript.ecma
   * 对于服务，指定用于查找OSGi服务的过滤器。 该服务已注册为com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的实现。

* **runModes（字符串）**：工作流执行所允许的运行模式列表（以逗号分隔）。 一些示例包括：

   * 作者

   * 发布

   * 作者，发布

   * 发布，作者

>[!NOTE]
>
>如果托管Watched文件夹的服务器没有指定的任何运行模式，则Watched文件夹始终激活，而不管服务器上的运行模式如何。

* **outputFilePattern（字符串）**：输出文件的模式。 您可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。 [文件和文件夹模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 还可以指定输出文件的目录结构。 它是必需属性。

* **stageFileExpirationDuration（长，默认为–1）**：已选取进行处理的输入文件/文件夹应被视为已超时并标记为失败之前等待的秒数。 仅当此属性的值为正数时，此到期机制才会激活。

>[!NOTE]
>
>即使使用此机制将输入标记为已超时，它仍可能在后台处理，但只是花费的时间比预期要长。 如果在超时机制被引入之前消耗了输入内容，则处理甚至可能稍后继续完成，并将输出转储到结果文件夹中。 如果在超时之前未使用内容，则在稍后尝试使用内容时，处理很有可能出错，并且此错误也将记录到同一输入的失败文件夹中。 另一方面，如果由于间歇性工作/工作流误发（到期机制旨在解决这种情况）而从未激活对输入的处理，则这两种情况都不会发生。 因此，对于失败文件夹中由于超时而被标记为失败的任何条目(查找窗体“文件在很长时间后未处理，标记为失败！”的消息。 在失败日志中)，建议扫描结果文件夹（以及失败文件夹本身，以查找相同输入的其他条目），以检查先前描述的任何事件是否实际发生。

* **deleteExpiredStageFileOnlyWhenThrottled （Boolean，默认为true）：** 是否应在限制监视文件夹时激活到期机制。 由于以未处理状态延迟的少量文件（由于间歇性作业/工作流错误触发）可能会在启用限制时阻塞整个批次的处理，因此该机制与受限制的监视文件夹更相关。 如果此属性保持为true（默认值），将不会为不受限制的监视文件夹激活到期机制。 如果属性保留为false，则只要stageFileExpirationDuration属性为正数，机制将始终激活。

* **pollInterval （长）**：扫描观察文件夹以进行输入的间隔（以秒为单位）。 除非启用“限制”设置，否则“轮询间隔”应大于处理平均作业的时间；否则，系统可能会过载。 默认值为 5。有关其他信息，请参阅批量大小的说明。 轮询间隔的值必须大于或等于1。
* **excludeFilePattern（字符串）**：分号(；)分隔的模式列表，观察文件夹使用该列表来确定要扫描和选取的文件和文件夹。 不会扫描任何具有此模式的文件或文件夹以进行处理。 当输入是具有多个文件的文件夹时，此设置很有用。 文件夹的内容可以复制到一个名称由Watched文件夹选取的文件夹中。 这样可防止Watched文件夹在将该文件夹完全复制到输入文件夹之前拾取要处理的文件夹。 默认值为null。
您可以使用 [文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 要排除，请执行以下操作：

   * 具有特定文件扩展名的文件；例如， &#42;.dat， &#42;.xml、.pdf、 &#42;.&#42;
   * 具有特定名称的文件；例如，数据&#42; 将排除名为data1、data2等的文件和文件夹。
   * 名称和扩展名中包含复合表达式的文件，如以下示例所示：

      * 数据[0-9][0-9][0-9].[分日][aA]&#39;端口&#39;
      * &#42;。[分日][Aa]&#39;端口&#39;
      * &#42;。[Xx][Mm][Ll]

有关文件模式的详细信息，请参见 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern（字符串）**：分号(；)分隔的模式列表，Watched文件夹使用该模式来确定要扫描和选取的文件夹和文件。 例如，如果输入了IncludeFilePattern&#42;，与输入匹配的所有文件和文件夹&#42; 被接走了。 这包括名为input1、input2等的文件和文件夹。 默认值为 &#42; 和指示所有文件和文件夹。 您可以使用文件模式来包括：

   * 具有特定文件扩展名的文件；例如， &#42;.dat， &#42;.xml、.pdf、 &#42;.&#42;
   * 具有特定名称的文件；例如，数据。&#42; 将包括名为data1、data2等的文件和文件夹。

* 名称和扩展名中包含复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9].[分日][aA]&#39;端口&#39;

      * &#42;。[分日][Aa]&#39;端口&#39;
      * &#42;。[Xx][Mm][Ll]

有关文件模式的详细信息，请参见 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime（长）**：文件夹或文件创建后等待扫描的时间，以毫秒为单位。 例如，如果等待时间为3,600,000毫秒（1小时），文件是在一分钟前创建的，则将在59分钟或更长时间后提取此文件。 默认值为 0。此设置对于确保将文件或文件夹完全复制到输入文件夹非常有用。 例如，如果您要处理大文件，并且下载该文件需要10分钟，则将等待时间设置为10&#42;60 &#42;1000毫秒。 这样可防止Watched Folder在文件未满十分钟时扫描文件。
* **purgeDuration（长）**：当结果文件夹中的文件和文件夹早于此值时会将其清除。 此值以天为单位。 此设置有助于确保结果文件夹不会变满。 值为–1天表示从不删除结果文件夹。 默认值为–1。
* **resultFolderName（字符串）**：存储所保存结果的文件夹。 如果结果未出现在此文件夹中，请检查失败文件夹。 只读文件不会被处理，并保存在失败文件夹中。 此值可以是具有以下文件模式的绝对路径或相对路径：

   * %F =文件名前缀
   * %E =文件扩展名
   * %Y =年（完整）
   * %y =年（最后两位数）
   * %M =月
   * %D =日期
   * %d =年中的日
   * %H =小时（24小时制）
   * %h =小时（12小时制）
   * %m =分钟
   * %s =秒
   * %l =毫秒
   * %R =随机数（介于0-9之间）
   * %P =进程或作业标识

  例如，如果在2009年7月17日晚上8点，并且您指定C：/Test/WF0/failure/%Y/%M/%D/%H/，则结果文件夹为C：/Test/WF0/failure/2009/07/17/20

  如果路径不是绝对路径而是相对路径，则在Watched文件夹内创建该文件夹。 默认值为result/%Y/%M/%D/，它是Watched文件夹内的Result文件夹。 有关文件模式的详细信息，请参见 [关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>结果文件夹的大小越小，“观察文件夹”的性能越好。 例如，如果监视文件夹的预计负载为每小时1000个文件，请尝试使用result/%Y%M%D%H之类的模式，以便每小时创建一个新的子文件夹。 如果负载较小（例如，每天1000个文件），则可以使用诸如result/%Y%M%D之类的模式。

* **failureFolderName（字符串）**：保存失败文件的文件夹。 此位置始终相对于Watched文件夹。 您可以使用文件模式，如“结果文件夹”中所述。 只读文件不会被处理，并保存在失败文件夹中。 默认值为失败/%Y/%M/%D/。
* **preserveFolderName（字符串）：** 成功处理文件后存储文件的位置。 路径可以是绝对、相对或空目录路径。 您可以使用文件模式，如“结果文件夹”中所述。 默认值为preserve/%Y/%M/%D/。
* **batchSize (Long)**：每次扫描要提取的文件或文件夹数。 用于防止系统过载；一次扫描太多文件可能会导致崩溃。 默认值为 2。

  “轮询间隔”和“批处理大小”设置可确定Watched Folder在每次扫描中选取的文件数。 观察文件夹使用Quartz线程池扫描输入文件夹。 线程池与其他服务共享。 如果扫描间隔很小，则线程会经常扫描输入文件夹。 如果文件经常被放入Watched文件夹，则应该保持较小的扫描间隔。 如果文件不经常被丢弃，请使用较大的扫描间隔，以便其他服务可以使用线程。

  如果正在删除大量文件，请使批次大小变大。 例如，如果Watched Folder端点启动的服务每分钟可以处理700个文件，并且用户以相同的速率将文件放入输入文件夹，则将“批处理大小”设置为350，将“轮询间隔”设置为30秒，将有助于提高Watched Folder的性能，而不会太频繁地扫描Watched Folder的成本。

  当文件被放入Watched文件夹时，它会列出输入中的文件，如果每秒都进行扫描，则可能会降低性能。 增加扫描间隔可以提高性能。 如果正在删除的文件量很小，请相应地调整批处理大小和轮询间隔。 例如，如果每秒丢弃10个文件，请尝试将pollInterval设置为1秒，并将Batch Size设置为10

* **throttleOn（布尔值）**：选中此选项后，它会限制AEM Forms在任何给定时间处理的观察文件夹作业数。 最大作业数由“批次大小”值决定。 默认值为true。 (请参阅 [关于限制](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename（布尔值）**：设置为True时，将覆盖结果文件夹和保留文件夹中的文件。 当设置为False时，使用具有数字索引后缀的文件和文件夹作为名称。 默认值为False。
* **preserveOnFailure（布尔值）**：如果对服务运行操作失败，则保留输入文件。 默认值为true。
* **inputFilePattern（字符串）**：指定Watched文件夹的输入文件模式。 创建文件的允许列表。
* **异步（布尔值）**：将调用类型标识为异步或同步。 默认值为true（异步）。 文件处理是一项消耗资源的任务，将异步标志的值保持为true可防止阻塞扫描作业的主线程。 在群集环境中，保持标记为true对于启用跨可用服务器处理的文件的负载平衡至关重要。 如果标志为false，则扫描作业将尝试在其自己的线程中依次对每个顶级文件/文件夹执行处理。 如果没有特定原因（例如，在单服务器设置上基于工作流的处理），请勿将标志设置为false。

>[!NOTE]
>
>工作流在设计上是异步的。 即使将该值设置为false，工作流也会以异步模式启动。

* **已启用（布尔值）**：停用并激活对Watched文件夹的扫描。 将enabled设置为true ，以开始扫描Watched文件夹。 默认值为true。
* **payloadMapperFilter：** 当文件夹配置为watched文件夹时，将在watched文件夹内创建一个文件夹结构。 该结构具有文件夹，用于提供输入、接收输出（结果）、保存故障数据、保存长期流程的数据以及保存各个阶段的数据。 观察文件夹的文件夹结构可用作以Forms为中心的工作流的负载。 有效负荷映射器允许您定义有效负荷的结构，该有效负荷使用观察文件夹进行输入、输出和处理。 例如，如果使用默认映射器，它将监视文件夹的内容映射为 [有效负荷]\输入和 [有效负荷]\output文件夹 提供了两种现成的有效负载映射器实施。 如果您没有 [自定义实施](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，请使用以下现成的实施之一：

   * **默认映射器：** 使用默认有效负荷映射器将watched文件夹的输入和输出内容保留在有效负荷的单独输入和输出文件夹中。 此外，在工作流的有效负荷路径中，使用 [有效负荷]/input/和 [有效负荷]/output路径以检索和保存内容。

   * **基于文件的简单有效负载映射器：** 使用基于简单文件的有效负荷映射器，将输入和输出内容直接保留在有效负荷文件夹中。 它不会创建任何额外的层次结构，如默认映射器。

### 自定义配置参数 {#custom-configuration-parameters}

除了上面列出的观察文件夹配置属性外，您还可以指定自定义配置参数。 自定义参数将传递到文件处理代码。 它允许代码根据参数的值更改其行为。 要指定参数，请执行以下操作：

1. 登录到CRXDE-Lite并导航到“观察文件夹”配置节点。
1. 添加属性参数。&lt;property_name> 到“观察文件夹”配置节点。 属性的类型只能为Boolean、Date、Decimal、Double、Long和String。 您可以指定单值和多值属性。

>[!NOTE]
>
>如果属性的数据类型是Double，则在此类属性的值中指定小数点。 对于所有属性（其中数据类型为Double且在值中未指定小数点），类型将转换为Long。

这些属性作为Map类型的不可变映射传递&lt;string object=&quot;&quot;> 到处理代码中。 处理代码可以是ECMAScript、工作流或服务。 为属性提供的值在映射中作为键值对提供。 键是属性的名称，值是属性的值。 有关自定义配置参数的更多信息，请参阅以下图像：

![具有强制属性、一些可选属性和一些配置参数的监视文件夹配置节点示例](assets/custom-configuration-parameters.png)

具有强制属性、一些可选属性和一些配置参数的监视文件夹配置节点示例。

#### 工作流程的可变变量 {#mutable-variables-for-workflows}

您可以为基于工作流的文件处理方法创建可变变量。 这些变量用作工作流各个步骤之间流的数据的容器。 要创建此类变量，请执行以下操作：

1. 登录到CRXDE-Lite并导航到“观察文件夹”配置节点。

1. 添加属性workflow.var。&lt;variable_name> 到“观察文件夹”配置节点。

   属性的类型只能为Boolean、Date、Decimal、Double、Long和String。 还支持多值属性。 对于多值属性，工作流步骤可用的值是指定类型的数组。

   >[!NOTE]
   >
   >如果属性的数据类型是Double，则在此类属性的值中指定小数点。 对于所有属性（其中数据类型为Double且在值中未指定小数点），类型将转换为Long。

>[!NOTE]
>
>JCR规范规定了属性的默认值。 默认值可用于工作流的步骤以进行处理。 因此，请指定正确的默认值。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 处理文件的各种方法 {#variousmethodsforprocessingfiles}

您可以启动工作流、服务或脚本以处理监视文件夹中的文档位置。

### 使用服务处理观察文件夹的文件   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服务是以下内容的自定义实施 `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 界面。 它向OSGi注册以及一些自定义属性。 实施的自定义属性使其具有唯一性，并有助于识别实施。

#### ContentProcessor界面的自定义实施 {#custom-implementation-of-the-contentprocessor-interface}

自定义实施接受处理上下文（com.adobe.aemfd.watchfolder.service.api.ProcessorContext类型的对象），从上下文读取输入文档和配置参数，处理输入，并将输出添加回上下文。 ProcessorContext具有以下API：

* **getWatchFolderId**：返回观察文件夹的ID。
* **getInputMap**：返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getconfigparameters**：返回映射类型的不可变映射。 映射包含观察文件夹的配置参数。

* **setResult**：ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供一个名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。

例如，以下代码是使用自定义foo=bar属性的ContentProcessor界面的自定义实施。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

同时 [配置观察文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)，如果将inputProcessorId属性指定为(foo=bar)，将inputProcessorType属性指定为Service ，则使用上述服务（自定义实施）处理Watched文件夹的输入文件。

以下示例也是ContentProcessor界面的自定义实现。 在示例中，服务接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹中。 结果文件夹的物理路径配置于 [观察文件夹配置节点](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### 使用脚本处理观察文件夹的文件 {#using-scripts-to-process-files-of-a-watched-folder}

脚本是写入的ECMAScript投诉自定义代码，用于处理放置在Watched文件夹中的文档。 脚本表示为JCR节点。 除了标准ECMAScript变量（log、sling等）之外，脚本还具有变量processorContext。 变量的类型为ProcessorContext。 ProcessorContext具有以下API：

* **getWatchFolderId**：返回观察文件夹的ID。
* **getInputMap**：返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getconfigparameters**：返回映射类型的不可变映射。 映射包含观察文件夹的配置参数。
* **setResult**：ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供一个名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。

以下代码是一个示例ECMAScript。 它接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹中。 结果文件夹的物理路径配置于 [观察文件夹配置节点](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>输出文件夹和文件名前缀是根据Watched Folder配置参数确定的。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 脚本的位置和安全注意事项 {#location-of-scripts-and-security-considerations}

默认情况下，提供了一个容器文件夹(/etc/fd/watchfolder/scripts)，客户可以在其中放置其脚本，并且watch-folder框架使用的默认service-user具有从该位置读取脚本的必要权限。

如果您计划将脚本放置在自定义位置，则默认服务用户可能没有对自定义位置的读取权限。 对于这种情况，请执行以下步骤以提供对自定义位置的必要权限：

1. 以编程方式或通过控制台https://&#39;创建系统用户[服务器]：[端口]&#39;/crx/explorer. 您也可以使用现有系统用户。 请务必在此处与系统用户而非正常用户合作。
1. 在存储脚本的自定义位置向新创建的或现有的系统用户提供读取权限。 您可以有多个自定义位置。 至少向所有自定义位置提供读取权限。
1. 在Felix配置控制台(/system/console/configMgr)中，找到监视文件夹的服务用户映射。 此映射类似于“映射： adobe-aemds-core-watch-folder=...”。
1. 单击映射。 对于“adobe-aemds-core-watch-folder：scripts=fd-service”条目，请将fd-service更改为自定义系统用户的ID。 单击保存。

现在，您可以使用配置的自定义位置来保存脚本。

### 使用工作流处理观察文件夹的文件 {#using-a-workflow-to-process-files-of-a-watched-folder}

通过工作流，您可以自动执行Experience Manager活动。 工作流包含一系列按特定顺序执行的步骤。 每个步骤都会执行不同的活动，例如激活页面或发送电子邮件。 工作流可与存储库中的资源、用户帐户和Experience Manager服务进行交互。 因此，工作流可以协调复杂。

* 在创建工作流之前，请考虑以下几点：
* 步骤的输出必须可用于所有后续步骤。
这些步骤必须能够更新（甚至删除）由先前步骤生成的现有输出。
* 可变变量用于在步骤之间传输自定义动态数据。

执行以下步骤以使用工作流处理文件：

1. 创建实施 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 界面。 它类似于为服务创建的实施。

   >[!NOTE]
   >
   >您可以在ECMAScript中完全创建完整的实施。

1. 在工作流的一个步骤中，找到com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService类型的OSGi服务，并使用以下参数调用该服务的execute()方法。

   * WorkflowContextProcessor界面的自定义实施
   * 工作项
   * workflowSession
   * 元数据

如果使用Java编程语言实施工作流，则AEM工作流引擎会为workItem、workflowSession和元数据变量提供值。 这些变量将作为参数传递给自定义WorkflowProcess实施的execute()方法。

如果使用ECMAScript实施工作流，则AEM工作流引擎会为graniteWorkItem、graniteWorkflowSession和元数据变量提供值。 这些变量作为参数传递到WorkflowContextService.execute()方法。

processWorkflowContext()的参数是com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext类型的对象。 WorkflowContext接口具有以下API，以便于执行上述特定于工作流的注意事项：

* getWorkItem：返回WorkItem变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getWorkflowSession：返回WorkflowSession变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getMetadata：返回元数据变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getCommittedVariables：返回表示由先前步骤设置的变量的只读对象映射。 如果变量未在前面的任何步骤中修改，则会返回在配置Watched文件夹时指定的默认值。
* getCommittedResults：返回只读文档映射。 该映射表示通过上述步骤生成的输出文件。
* setVariable： WorkflowContextProcessor实施使用变量来操作变量，这些变量表示在步骤之间流动的自定义动态数据。 变量的名称和类型与期间指定的变量的名称相同。 [配置观察文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). 要更改变量的值，请使用非null值调用setVariable API。 要删除变量，请使用null值调用setVariable()。

以下ProcessorContext API也可用：

* getWatchFolderId：返回观察文件夹的ID。
* getInputMap：返回映射类型的映射&lt;string document=&quot;&quot;>. 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* getConfigParameters：返回类型为Map的不可变映射&lt;string object=&quot;&quot;>. 映射包含观察文件夹的配置参数。
* setResult： ContentProcessor实施使用API将输出文档写入结果文件夹。 您可以为setResult API的输出文件提供一个名称。 API可能会根据指定的输出文件夹/文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述

setResult API在工作流中使用的注意事项：

* 要添加有助于整体工作流输出的新输出文档，请使用任何先前步骤均未用作输出文件名的文件名来调用setResult API。
* 要更新上一步骤生成的输出，请使用上一步已使用的文件名调用setResult API。
* 要删除上一步骤生成的输出，请调用setResult，其文件名已由上一步骤使用，内容为null。

>[!NOTE]
>
>在任何其他情况下调用包含null内容的setResult API都将导致错误。

以下示例作为工作流步骤实施。 在此示例中，ECMAscript使用变量stepCount跟踪当前工作流实例中调用步骤的次数。
输出文件夹的名称是当前步骤编号、原始文件名和outPrefix参数中指定的前缀的组合。

ECMAScript获取工作流上下文服务的引用，并创建WorkflowContextProcessor接口的实现。 WorkflowContextProcessor实现接受输入文件，将文件复制到临时位置，并返回表示所复制文件的文档。 根据布尔变量purgePrevious的值，当前步骤将删除当前工作流实例中启动该步骤时，由同一步骤上次生成的输出。 最后，调用wfSvc.execute方法以执行WorkflowContextProcessor实现。 输出文档的内容将保存到Watched Folder配置节点中提到的物理路径上的结果文件夹中。

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### 创建有效负荷映射器过滤器以将watched文件夹的结构映射到工作流的有效负荷 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

创建watched文件夹时，会在被监视的文件夹内创建一个文件夹结构。 文件夹结构具有阶段、结果、保留、输入和失败文件夹。 文件夹结构可用作工作流的输入有效负荷并接受工作流的输出。 它还可以列出故障点（如果有）。

如果有效负荷的结构与观察文件夹的结构不同，您可以编写自定义脚本以将观察文件夹的结构映射到有效负荷。 此类脚本称为有效负荷映射器过滤器。 AEM Forms开箱即用地提供有效负荷映射器过滤器，以将观察文件夹的结构映射到有效负荷。

#### 创建自定义有效负载映射器过滤器 {#creating-a-custom-payload-mapper-filter}

1. 下载 [Adobe客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. 在基于maven的项目的构建路径中设置客户端SDK。 要开始配置，您可以在所选的IDE中下载并打开以下基于maven的项目。
1. 编辑示例包中可用的有效负载映射器过滤器代码以满足您的要求。
1. 使用maven创建自定义有效负载映射器过滤器的捆绑包。
1. 使用 [AEM包控制台](https://localhost:4502/system/console/bundles) 以安装捆绑包。

   现在，AEM Watched文件夹UI中列出了自定义有效负载映射器筛选器。 您可以将其用于工作流。

   以下示例代码为相对于有效负荷保存的文件实施一个简单的基于文件的映射器。 你可以用它开始。

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## 用户如何与Watched文件夹交互 {#how-users-interact-with-a-watched-folder}

对于Watched Folder端点，用户可以通过将输入文件或文件夹从其桌面复制或拖到Watched Folder来开始文件处理操作。 文件按到达顺序处理。

对于观察文件夹端点，如果作业只需要一个输入文件，则用户可以将该文件复制到Watched文件夹的根目录。

如果作业包含多个输入文件，则用户必须在Watched Folder层次结构之外创建一个包含所有必需文件的文件夹。 此新文件夹应包含输入文件（如果进程需要，还可以选择包含DDX文件）。 创建作业文件夹后，用户将其复制到Watched文件夹的输入文件夹中。

>[!NOTE]
>
>确保应用程序服务器已删除对Watched文件夹中文件的访问权限。 如果AEM Forms在扫描文件后无法从输入文件夹中删除这些文件，则关联的进程将无限期启动。

## 有关观察文件夹的其他信息 {#additional-information-about-the-watched-folders}

### 关于限制 {#about-throttling}

为监视文件夹端点启用限制时，它会限制在任何给定时间处理的监视文件夹作业的数量。 最大作业数由批处理大小值决定，该值也可以在Watched文件夹端点中配置。 当达到限制限制时，将不轮询观察文件夹输入目录中的传入文档。 文档还保留在输入目录中，直到完成其他观察文件夹作业并再次尝试轮询为止。 对于同步处理，单个轮询中处理的所有作业都将计入限制值，即使这些作业在单个线程中连续处理。

>[!NOTE]
>
>限制无法随群集扩展。 启用限制后，群集作为一个整体不会在任何给定时间处理超过批量大小中指定的作业数。 此限制在群集范围之内，并非特定于群集中的每个节点。 例如，当批处理大小为2时，单个节点处理两个作业即可达到限制限制，并且在一个作业完成之前，没有其他节点会轮询输入目录。

#### 限制的工作方式 {#how-throttling-works}

观察文件夹在每个pollInterval扫描输入文件夹，选取在“批处理大小”中指定的文件数，并为每个文件调用目标服务。 例如，如果Batch Size为4，则每次扫描时，Watched Folder会选取四个文件，创建四个调用请求，然后调用目标服务。 在完成这些请求之前，如果调用Watched Folder，则无论前四个作业是否完成，它都会再次启动四个作业。

限制功能可防止Watched文件夹在前面的作业未完成时调用新作业。 观察文件夹检测正在进行的作业，并根据批处理大小减去正在进行的作业来处理新作业。 例如，在第二次调用中，如果完成的作业数只有三个，并且一个作业仍在进行中，则Watched Folder将仅调用另外三个作业。

* 观察文件夹依赖于暂存文件夹中的文件数，以确定正在进行多少个作业。 如果文件在stage文件夹中保持未处理状态，Watched Folder将不再调用任何作业。 例如，如果批处理大小为4个且已停止三个作业，则Watched文件夹在后续调用中仅调用一个作业。 有多个情况可能会导致文件在stage文件夹中保持未处理状态。 当作业停止时，管理员可以在“进程管理”管理页面上终止进程，以便Watched Folder将文件移出stage文件夹。
* 如果AEM Forms服务器在Watched Folder调用作业之前关闭，管理员可以将文件移出stage文件夹。 有关信息，请参阅 [故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* 如果AEM Forms服务器正在运行，但在作业管理器服务回调时观察文件夹未运行（当服务未按顺序启动时会发生回调），则管理员可以将文件移出暂存文件夹。 有关信息，请参阅 [故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### 故障点和恢复故障点和恢复 {#failure-points-and-recoveryfailure-points-and-recovery}

在每个轮询事件中， Watched Folder锁定输入文件夹，将匹配包含文件模式的文件移到stage文件夹，然后解除锁定输入文件夹。 需要锁定，这样两个线程就不会拾取同一组文件并对其进行两次处理。 如果轮询间隔较小且批次较大，则发生此情况的机会会增加。 将文件移到stage文件夹后，输入文件夹将被解锁，以便其他线程可以扫描该文件夹。 此步骤有助于提供高吞吐量，因为其他线程可以在一个线程处理文件时进行扫描。

将文件移到stage文件夹后，将为每个文件创建调用请求，并调用目标服务。 在Watched Folder无法恢复stage文件夹中的文件的情况下：

* 如果服务器在Watched Folder创建调用请求之前关闭，则舞台文件夹中的文件将保留在stage文件夹中，并且不会恢复。

* 如果Watched Folder已成功为stage文件夹中的每个文件创建调用请求，并且服务器崩溃，则根据调用类型有两种行为：

   * **同步**：如果观察文件夹配置为同步调用服务，则stage文件夹中的所有文件在stage文件夹中保持未处理状态。
   * **异步**：在这种情况下， Watched文件夹依赖作业管理器服务。 如果作业管理器服务回调Watched文件夹，则根据调用的结果，会将暂存文件夹中的文件移到preserve或failure文件夹。 如果作业管理器服务没有回调“观察文件夹”，则文件在stage文件夹中将保持未处理状态。 当作业管理器回拨时，Watched文件夹未运行，会发生这种情况。

#### 恢复暂存文件夹中未处理的源文件 {#recover-unprocessed-source-files-in-the-stage-folder}

当观察文件夹无法处理暂存文件夹中的源文件时，您可以恢复未处理的文件。

1. 重新启动应用程序服务器或节点。

1. 停止Watched文件夹处理新输入文件。 如果跳过此步骤，将更难确定哪些文件在stage文件夹中未处理。 要阻止Watched Folder处理新的输入文件，请执行以下任务之一：

   * 将Watched文件夹的includeFilePattern属性更改为与任何新输入文件都不匹配的属性（例如，输入NOMATCH）。
   * 暂停正在创建新输入文件的进程。

   等待AEM Forms恢复并处理所有文件。 大多数文件应恢复，任何新输入文件都应正确处理。 您等待观察文件夹恢复和处理文件的时间长短将取决于要调用的操作的长度和要恢复的文件数。

1. 确定无法处理哪些文件。 如果等待了适当的时间并且已完成上一步，并且暂存文件夹中仍存在未处理的文件，请转到下一步。

   >[!NOTE]
   >
   >您可以在暂存目录中查看文件的日期和时间戳。 根据文件数和正常处理时间，您可以确定哪些文件的年龄足以被视为卡住。

1. 将未处理的文件从stage目录复制到输入目录。

1. 如果在步骤2中阻止Watched Folder处理新的输入文件，请将“Include File Pattern”（包含文件模式）更改为先前的值，或者重新启用已禁用的进程。

### 将Watched文件夹链接在一起 {#chain-watched-folders-together}

监视文件夹可以链接在一起，因此一个Watched文件夹的结果文档是下一个Watched文件夹的输入文档。 每个Watched文件夹都可以调用不同的服务。 通过以这种方式配置Watched文件夹，可以调用多个服务。 例如，一个Watched文件夹可以将PDF文件转换为Adobe PostScript®，另一个Watched文件夹可以将PostScript文件转换为PDF/A格式。 要执行此操作，只需将您第一个端点定义的Watched文件夹的结果文件夹设置为指向您第二个端点定义的Watched文件夹的输入文件夹。

第一次转换的输出将转到\path\result。 第二次转换的输入是\path\result，第二次转换的输出将转到\path\result\result （或您在第二次转换的结果文件夹框中定义的目录）。

### 文件和文件夹模式 {#file-and-folder-patterns}

管理员可以指定可以调用服务的文件类型。 可以为每个Watched文件夹建立多个文件模式。 文件模式可以是以下文件属性之一：

* 具有特定文件扩展名的文件；例如， &#42;.dat， &#42;.xml、.pdf、 &#42;.&#42;
* 具有特定名称的文件；例如，数据。&#42;
* 名称和扩展名中包含复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9].[分日][aA]&#39;端口&#39;
   * &#42;。[分日][Aa]&#39;端口&#39;
   * &#42;。[Xx][Mm][Ll]

* 管理员可以定义用于存储结果的输出文件夹的文件模式。 对于输出文件夹（“结果”、“保留”和“失败”），管理员可以指定以下任何文件模式：
* %Y =年（完整）
* %y =年（最后两位数）
* %M =月，
* %D =日期，
* %d =一年中的第几天，
* %h =小时，
* %m =分钟，
* %s =秒，
* %R =介于0-9之间的随机数
* %J =作业名称

例如，结果文件夹的路径可能是C:\Adobe\AdobeLiveCycleES4\BarcodedForms\%y\%m\%d。

输出参数映射还可以指定其他模式，例如：

* %F =源文件名
* %E =源文件扩展名

如果输出参数映射模式以“File.separator”（路径分隔符）结尾，则会创建一个文件夹，并将内容复制到该文件夹中。 如果模式不以“File.separator”结尾，则会使用该名称创建内容（结果文件或文件夹）。

## 将PDF Generator与Watched文件夹一起使用 {#using-pdf-generator-with-a-watched-folder}

您可以配置Watched文件夹以启动工作流、服务或脚本来处理输入文件。 在以下部分中，我们将配置Watched文件夹以启动ECMAScript。 ECMAScript将使用PDF Generator将Microsoft Word (.docx)文档转换为PDF文档。

执行以下步骤来使用PDF Generator配置Watched文件夹：

1. [创建ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [创建工作流](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [配置观察文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 创建ECMAScript {#create-an-ecmascript}

ECMAScript将使用PDF Generator的createPDF API将Microsoft Word (.docx)文档转换为PDF文档。 执行以下步骤以创建脚本：

1. 在浏览器窗口中打开CRXDE Lite。 URL为https://&#39;[服务器]：[端口]&#39;/crx/de.

1. 导航到/etc/workflow/scripts并创建一个名为PDFG的文件夹。

1. 在PDFG文件夹中，创建一个名为pdfg-openOffice-sample.ecma的文件，并将以下代码添加到该文件中：

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. 保存并关闭该文件。

### 创建工作流 {#create-a-workflow}

1. 在浏览器窗口中打开AEM Workflow UI。
   <https://[servername>]：&#39;端口&#39;/工作流

1. 在“模型”视图中，单击 **新建**. 在新增工作流对话框中，指定 **标题**，然后单击 **确定**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 选择新创建的工作流，然后单击 **编辑**. 工作流将在新窗口中打开。

1. 删除默认工作流步骤。 将流程步骤从Sidekick拖放到工作流。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 右键单击流程步骤并选择 **编辑**. 出现“Step Properties（步骤属性）”窗口。

1. 在“流程”选项卡中，选择ECMAScript。 例如，在中创建的pdfg-openOffice-sample.ecma脚本 [创建ECMAScript](#p-create-an-ecmascript-p). 启用 **处理程序前进** 选项并单击 **确定**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 配置观察文件夹 {#configure-the-watched-folder}

1. 在浏览器窗口中打开CRXDE Lite。 https://&#39;[服务器]：[端口]&#39;/crx/de/

1. 导航到/etc/fd/watchfolder/config/文件夹，并创建类型为nt：unstructured的节点。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 将以下属性添加到节点：

   * folderPath （字符串）：在定义的时间间隔内扫描的文件夹的路径。 文件夹必须位于共享位置，且所有服务器均具有服务器的完全访问权限。
inputProcessorType （字符串）：要启动的进程的类型。 在本教程中，指定工作流。

   * inputProcessorId （字符串）： inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 在此示例中，inputProcessorType属性的值为workflow。 因此，对于inputProcessorId属性，请指定PDFG工作流的以下路径：/etc/workflow/models/pdfg/jcr：content/model

   * outputFilePattern （字符串）：输出文件的模式。 您可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称将如工作流中所述。 如果指定了文件模式，则输出文件的名称如文件模式中所述。

   除了上述强制属性外，Watched文件夹还支持一些可选属性。 有关可选属性的完整列表和说明，请参阅 [观察文件夹属性](#watchedfolderproperties).

## 已知问题 {#watched-folder-known-issues}

在JEE上启动AEM 6.5 Forms时，文件会在JBoss完全启动之前开始处理，并且文件无法处理。 要避免此情况，请在启动JBoss之前，清除所有Watched文件夹。
