---
title: 以AEM Forms形式监视文件夹
seo-title: 以AEM Forms形式监视文件夹
description: 管理员可以将文件夹置于监视中，并在文件置于监视的文件夹中时开始工作流、服务或脚本操作。
seo-description: 管理员可以将文件夹置于监视中，并在文件置于监视的文件夹中时开始工作流、服务或脚本操作。
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '7153'
ht-degree: 0%

---


# 以AEM Forms形式监视文件夹{#watched-folder-in-aem-forms}

管理员可以配置网络文件夹（称为“监视文件夹”），当用户将文件（如PDF文件）放在“监视文件夹”中时，会启动预先配置的工作流、服务或脚本操作以处理添加的文件。 服务执行指定操作后，会将结果文件保存到指定的输出文件夹中。 有关工作流、服务和脚本的详细信息，请参 [阅各种文件处理方法](#variousmethodsforprocessingfiles)。

## 创建监视文件夹 {#create-a-watched-folder}

您可以使用以下方法之一在文件系统上创建监视文件夹：

* 配置“监视文件夹”配置节点的属性时，在folderPath属性中键入父目录的完整路径，并附加要创建的监视文件夹的名称，如下例所示： `C:/MyPDFs/MyWatchedFolder`
The 
`MyWatchedFolder`文件夹不存在，AEM Forms会尝试在指定的路径中创建文件夹。

* 在配置监视文件夹端点之前在文件系统上创建一个文件夹，然后在folderPath属性中提供完整路径。 有关folderPath属性的详细信息，请参阅 [监视文件夹属性](#watchedfolderproperties)。

>[!NOTE]
>
>在群集环境中，用作监视文件夹的文件夹必须在文件系统或网络上具有辅助、可写和共享功能。 群集的每个应用程序服务器实例都必须有权访问同一共享文件夹。 在Windows上，在所有服务器上创建一个映射的网络驱动器，并在folderPath属性中指定映射的网络驱动器的路径。

## 创建监视文件夹配置节点 {#create-watched-folder-configuration-node}

要配置监视文件夹，请创建监视文件夹配置节点。 执行以下步骤以创建配置节点：

1. 以管理员身份登录到CRX-DE lite并导航到/etc/fd/watchfolder/config文件夹。

1. 创建类型的节点 `nt:unstructured`。 例如，watchedfolder

   >[!NOTE]
   >
   >“监视文件夹”节点名称不能包含空格和特殊字符。

1. 向节点添加以下属性：

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   有关受支持属性的完整列表，请参 [阅监视文件夹属性](#watchedfolderproperties)。

1. 单击“ **全部保存**”。 创建节点并保存属性后。 、、 `input`、 `result`和文 `failure`件 `preserve`夹是在属性中指定的路径 `stage``folderPath` 创建的。

   扫描作业开始以定义的时间间隔扫描监视的文件夹。

## 监视文件夹属性 {#watchedfolderproperties}

您可以为监视文件夹配置以下属性。

* **folderPath（字符串）**: 要在定义的时间间隔内扫描的文件夹的路径。 对于群集环境，文件夹必须位于与所有具有对服务器完全访问权限的服务器共享的位置。 它是强制属性。
* **inputProcessorType（字符串）**: 要开始的进程类型。 您可以指定工作流、脚本或服务。 它是强制属性。
* **inputProcessorId（字符串）**: inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 它是强制属性。 以下列表详细列出了inputProcessorType属性的所有可能值以及inputProcessorType属性的相应必需项：

   * 对于工作流，指定要执行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * 对于脚本，指定要执行的脚本的JCR路径。 例如，/etc/fd/watchfolder/test/testScript.ecma
   * 对于服务，指定用于查找OSGi服务的筛选器。 服务注册为com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的实现。

* **runModes（字符串）**: 允许运行模式的逗号分隔列表，用于执行工作流。 以下是几个示例：

   * 作者

   * 发布

   * 作者，发布

   * 发布，创作

>[!NOTE]
>
>如果承载监视文件夹的服务器没有任何指定的运行模式，则无论服务器上的运行模式如何，监视文件夹都始终激活。

* **outputFilePattern（字符串）**: 输出文件的模式。 可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称如工作流中所述。 如果指定了文件模式，则输出文件具有文件模式中所述的名称。 [文件和文件夹模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) ，还可以为输出文件指定目录结构。 它是强制属性。

* **stageFileExpirationDuration（长，默认-1）**: 在已被拾取用于处理的输入文件／文件夹之前等待的秒数应视为已超时并标记为失败。 仅当此属性的值为正数时，此过期机制才激活。

>[!NOTE]
>
>即使当输入使用此机制被标记为已超时时，它仍可能在后台处理，但只是比预期花费更多时间。 如果在超时机制启动之前消耗了输入内容，则处理甚至可能在以后继续完成，并将输出转储到结果文件夹中。 如果超时之前未消耗内容，则以后尝试消耗内容时处理很可能会出错，并且对于同一输入，此错误也会记录在失败文件夹中。 另一方面，如果由于间歇性作业／工作流失火（这是失效机制要解决的情况）而未激活对输入的处理，那么当然，这两种可能性都不会发生。 因此，对于因超时而标记为失败的失败文件夹中的任何条目(查找“文件在相当长时间后未处理，标记为失败！”格式的消息 在失败日志中)，建议扫描结果文件夹（以及针对同一输入扫描失败文件夹本身以查找另一个条目），以检查之前描述的任何可能性是否实际发生。

* **deleteExpiredStageFileOnlyWhenThrotled（布尔值，默认为true）:** 到期机制是否应仅在监视文件夹被限制时激活。 该机制对于节流的监视文件夹更相关，因为在未处理状态中徘徊的少量文件（由于间歇性作业／工作流失火）在启用节流时有可能阻塞整个批的处理。 如果此属性保持为true（默认），则过期机制将不激活未限制的监视文件夹。 如果属性保留为false，则只要stageFileExpirationDuration属性是正数，机制将始终激活。

* **pollInterval（长）**: 扫描监视文件夹以进行输入的时间间隔（秒）。 除非启用“限制”设置，否则轮询间隔应比处理平均作业的时间长； 否则，系统可能会过载。 默认值为 5。有关其他信息，请参阅批量大小说明。 轮询间隔的值必须大于或等于1。
* **excludeFilePattern（字符串）**: 分号(;)分隔的模式列表，监视文件夹使用这些模式确定要扫描和拾取的文件和文件夹。 不扫描任何具有此模式的文件或文件夹进行处理。 当输入是包含多个文件的文件夹时，此设置很有用。 文件夹的内容可以复制到名称由监视文件夹选取的文件夹中。 这样，监视文件夹在将文件夹完全复制到输入文件夹之前，便无法拾取要处理的文件夹。 默认值为null。
您可以使用文 [件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 来排除：

   * 具有特定文件扩展名的文件； 例如，*.dat、*.xml、.pdf、*。*
   * 具有特定名称的文件； 例如，data*将排除名为data1、data2等的文件和文件夹。
   * 名称和扩展名中具有复合表达式的文件，如以下示例所示：

      * 数据[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;
      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx]毫[米][Ll]

有关文件模式的详细信息，请参 [阅关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

* **includeFilePattern（字符串）**: 分号(;)分隔的模式列表，监视文件夹使用这些模式确定要扫描和拾取的文件夹和文件。 例如，如果输入IncludeFilePattern*，则会选取与输入匹配的所有文件和文件夹*。 这包括名为input1、input2等的文件和文件夹。 默认值为*，表示所有文件和文件夹。 您可以使用文件模式包括：

   * 具有特定文件扩展名的文件； 例如，*.dat、*.xml、.pdf、*。*
   * 具有特定名称的文件； 例如，数据。*将包括名为data1、data2等的文件和文件夹。

* 名称和扩展名中具有复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;

      * *.[dD][Aa]&#39;port&#39;
      * *.[Xx]毫[米][Ll]

有关文件模式的详细信息，请参 [阅关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime（长）**: 在创建文件夹或文件后扫描文件之前等待的时间（以毫秒为单位）。 例如，如果等待时间为3,600,000毫秒（1小时），且文件是在一分钟前创建的，则此文件将在59分钟或更长时间后被拾取。 默认值为 0。此设置有助于确保将文件或文件夹完全复制到输入文件夹。 例如，如果要处理大型文件，而下载该文件需要10分钟，请将等待时间设置为10*60*1000毫秒。 如果文件未达到10分钟，则阻止监视文件夹扫描文件。
* **purgeDuration（长）**: 当结果文件夹中的文件和文件夹早于此值时，将清除这些文件和文件夹。 此值以天数计。 此设置有助于确保结果文件夹不变为完整文件夹。 值为-1天表示从不删除结果文件夹。 默认值为-1。
* **resultFolderName（字符串）**: 保存的结果存储在的文件夹。 如果结果未显示在此文件夹中，请检查失败文件夹。 只读文件不会处理，并保存在失败文件夹中。 此值可以是具有以下文件模式的绝对路径或相对路径：

   * %F =文件名前缀
   * %E =文件扩展名
   * %Y =年（已满）
   * %y =年（最后两位）
   * %M =月
   * %D =月日
   * %d =年
   * %H =小时（24小时钟）
   * %h =小时（12小时钟）
   * %m =分钟
   * %s =秒
   * %l =毫秒
   * %R =随机数（介于0和9之间）
   * %P =进程或作业ID

   例如，如果2009年7月17日晚上8点，并且您指定C:/Test/WF0/failure/%Y/%M/%D/%H/，则结果文件夹为C:/Test/WF0/failure/2009/07/17/20

   如果路径不是绝对的，而是相对的，则在“监视文件夹”中创建该文件夹。 默认值为result/%Y/%M/%D/，它是监视文件夹内的Result文件夹。 有关文件模式的详细信息，请参 [阅关于文件模式](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)。

>[!NOTE]
>
>结果文件夹的大小越小，“监视文件夹”的效果就越好。 例如，如果监视文件夹的估计负载是每小时1000个文件，请尝试类似result/%Y%M%D%H的模式，以便每小时创建一个新的子文件夹。 如果负载较小（例如，每天1000个文件），您可以使用类似result/%Y%M%D的模式。

* **failureFolderName（字符串）**: 保存失败文件的文件夹。 此位置始终与监视文件夹相关。 可以使用文件模式，如结果文件夹中所述。 只读文件不会处理，并保存在失败文件夹中。 默认值为failure/%Y/%M/%D/。
* **preserveFolderName（字符串）:** 文件在成功处理后的存储位置。 路径可以是绝对路径、相对路径或空目录路径。 可以使用文件模式，如结果文件夹中所述。 默认值为preseve/%Y/%M/%D/。
* **batchSize（长）**: 每次扫描要拾取的文件或文件夹数。 用于防止系统过载； 一次扫描过多文件可能会导致崩溃。 默认值为 2。

   “投票间隔”和“批处理大小”设置决定“监视文件夹”在每次扫描中拾取的文件数。 监视文件夹使用石英线程池扫描输入文件夹。 线程池与其他服务共享。 如果扫描间隔较小，线程会经常扫描输入文件夹。 如果文件经常被放入“监视文件夹”，则扫描间隔应保持较小。 如果文件不常被删除，请使用更大的扫描间隔，以便其他服务可以使用线程。

   如果丢弃的文件量很大，请使批处理大小变大。 例如，如果监视文件夹端点启动的服务每分钟可处理700个文件，并且用户以相同的速率将文件放入输入文件夹，则将“批处理大小”设置为350，将“投票间隔”设置为30秒即可帮助监视文件夹执行，而不必频繁扫描监视文件夹。

   将文件放入“监视文件夹”后，将列表输入中的文件，如果每秒都进行扫描，则会降低性能。 增加扫描间隔可以提高性能。 如果正在删除的文件量较小，请相应地调整“批处理大小”和“轮询间隔”。 例如，如果每秒丢弃10个文件，请尝试将pollInterval设置为1秒，将批处理大小设置为10

* **throttleOn（布尔值）**: 选择此选项后，将限制AEM Forms在任何给定时间处理的监视文件夹作业数。 最大作业数由“批大小”值确定。 默认值为true。 (请参 [阅关于限](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p)制。)

* **overwriteDuplicateFilename(Boolean)**: 设置为“True”时，结果文件夹和保留文件夹中的文件将被覆盖。 设置为“False”时，名称将使用带数字索引后缀的文件和文件夹。 默认值为False。
* **preserveOnFailure（布尔值）**: 在无法对服务执行操作的情况下保留输入文件。 默认值为true。
* **inputFilePattern（字符串）**: 指定监视文件夹的输入文件的模式。 创建允许列表文件。
* **asynch（布尔值）**: 将调用类型标识为异步或同步。 默认值为true（异步）。 文件处理是一种资源消耗任务，将异步标志的值保持为真以防止阻塞扫描作业的主线程。 在群集环境中，务必使标志保持为true，以便为在可用服务器上处理的文件实现负载平衡。 如果标志为false，则扫描作业将尝试按顺序对其自己的线程中的每个顶级文件／文件夹执行处理。 如果没有特定原因（如单服务器设置上基于工作流的处理），请勿将标记设置为false。

>[!NOTE]
>
>根据设计，工作流是异步的。 即使将值设置为false,工作流也会以异步模式启动。

* **enabled（布尔值）**: 取消激活和激活监视文件夹的扫描。 设置为“启用”为“true”,开始扫描“监视的文件夹”。 默认值为true。
* **payloadMapperFilter:** 将文件夹配置为监视文件夹后，将在监视文件夹内创建文件夹结构。 该结构具有用于提供输入、接收输出（结果）、为故障保存数据、为长寿命进程保存数据以及为不同阶段保存数据的文件夹。 监视文件夹的文件夹结构可用作以表单为中心的工作流的有效负荷。 有效负荷映射器允许您定义有效负荷的结构，该结构使用监视文件夹进行输入、输出和处理。 例如，如果使用默认映射器，它将“监视文件夹”的内容与 [payload]\input和 [payload]\output文件夹映射。 提供两种现成的有效负荷映射器实现。 如果您没有 [自定义实](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)施，请使用现成的实施之一：

   * **默认映射器：** 使用默认的有效负荷映射器，将已监视文件夹的输入和输出内容保留在有效负荷中单独的输入和输出文件夹中。 此外，在工作流的有效负荷路径中，使 [用有效]/输入/ [和有效]/输出路径，检索并保存内容。

   * **基于文件的简单有效负荷映射器：** 使用基于简单文件的有效负荷映射器将输入和输出内容直接保留在有效负荷文件夹中。 它不会创建任何额外的层次结构，如默认映射器。

### 自定义配置参数 {#custom-configuration-parameters}

除了上面列出的“监视文件夹”配置属性外，您还可以指定自定义配置参数。 自定义参数将传递到文件处理代码。 它使代码能够根据参数的值更改其行为。 要指定参数，请执行以下操作：

1. 登录到CRXDE-Lite并导航到“监视文件夹”配置节点。
1. 添加属性参数。&lt;property_name>添加到“监视文件夹”配置节点。 该属性的类型只能是Boolean、Date、Decimal、多次、Long和String。 您可以指定单值和多值属性。

>[!NOTE]
>
>如果属性的多次类型为“”，则在此类属性的值中指定小数点。 对于所有属性，其中数据类型为多次，且值中未指定小数点，类型将转换为长。

这些属性作为Map&lt;String, Object>类型的不可变映射传递到处理代码。 处理代码可以是ECMAScript、Workflow或服务。 为属性提供的值在映射中以键值对的形式可用。 键是属性的名称，值是属性的值。 有关自定义配置参数的详细信息，请参阅下图：

![具有必需属性、几个可选属性和几个配置参数的监视文件夹配置节点示例](assets/custom-configuration-parameters.png)

具有必需属性、几个可选属性和几个配置参数的监视文件夹配置节点示例。

#### 工作流程的可变变量 {#mutable-variables-for-workflows}

可以为基于工作流的文件处理方法创建可变变量。 这些变量用作在工作流的各个步骤之间流动的容器。 要创建此类变量，请执行以下操作：

1. 登录到CRXDE-Lite并导航到“监视文件夹”配置节点。

1. 添加属性workflow.var。&lt;variable_name>添加到“监视文件夹”配置节点。

   该属性的类型只能是Boolean、Date、Decimal、多次、Long和String。 还支持多值属性。 对于多值属性，工作流步骤的可用值是指定类型的数组。

   >[!NOTE]
   >
   >如果属性的多次类型为“”，则在此类属性的值中指定小数点。 对于所有属性，其中数据类型为多次，且值中未指定小数点，类型将转换为长。

>[!NOTE]
>
>JCR规范要求属性具有默认值。 默认值适用于工作流中要处理的步骤。 因此，请指定适当的默认值。

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 处理文件的各种方法 {#variousmethodsforprocessingfiles}

您可以开始工作流、服务或脚本，以处理监视文件夹中的文档位置。

### 使用服务处理监视文件夹的文件   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

服务是接口的自定义实 `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 现。 它已在OSGi中注册，并且还注册了一些自定义属性。 实现的自定义属性使其独一无二，并有助于识别实现。

#### ContentProcessor接口的自定义实现 {#custom-implementation-of-the-contentprocessor-interface}

自定义实现接受处理上下文（com.adobe.aemfd.watchfolder.service.api.ProcessorContext类型的对象），从上下文中读取输入文档和配置参数，处理输入，并将输出添加回上下文。 ProcessorContext具有以下API:

* **getWatchFolderId**: 返回已监视文件夹的ID。
* **getInputMap**: 返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getConfigParameters**: 返回Map类型的不可变映射。 映射包含监视文件夹的配置参数。

* **setResult**: ContentProcessor实现使用API将输出文档写入结果文件夹。 可为setResult API提供输出文件的名称。 API可能会根据指定的输出文件夹／文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称如工作流中所述。 如果指定了文件模式，则输出文件具有文件模式中所述的名称。

例如，以下代码是具有custom foo=bar属性的ContentProcessor接口的自定义实现。

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

配置 [监视文件夹时](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)，如果将inputProcessorId属性指定为(foo=bar)，将inputProcessorType属性指定为服务，则上述服务（自定义实现）将用于处理监视文件夹的输入文件。

以下示例也是ContentProcessor接口的自定义实现。 在示例中，服务接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹。 结果文件夹的物理路径在“监视文件夹” [配置节点中配置](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)。

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

### 使用脚本处理监视文件夹的文件 {#using-scripts-to-process-files-of-a-watched-folder}

脚本是写入到“监视文件夹”中的文档的ECMAScript自定义代码。 脚本表示为JCR节点。 除了标准ECMAScript变量（日志、sling等）之外，脚本还包含一个变量processorContext。 该变量的类型为ProcessorContext。 ProcessorContext具有以下API:

* **getWatchFolderId**: 返回已监视文件夹的ID。
* **getInputMap**: 返回映射类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* **getConfigParameters**: 返回Map类型的不可变映射。 映射包含监视文件夹的配置参数。
* **setResult**: ContentProcessor实现使用API将输出文档写入结果文件夹。 可为setResult API提供输出文件的名称。 API可能会根据指定的输出文件夹／文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称如工作流中所述。 如果指定了文件模式，则输出文件具有文件模式中所述的名称。

以下代码是一个ECMAScript示例。 它接受输入文件，将文件复制到临时位置，并返回包含文件内容的文档对象。 文档对象的内容将保存到结果文件夹。 结果文件夹的物理路径在“监视文件夹” [配置节点中配置](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p)。

>[!NOTE]
>
>输出文件夹和文件名前缀取决于“监视文件夹”配置参数。

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 脚本的位置和安全注意事项 {#location-of-scripts-and-security-considerations}

默认情况下，会提供一个容器文件夹(/etc/fd/watchfolder/scripts)，客户可以在其中放置脚本，而观察文件夹框架使用的默认服务用户具有从此位置读取脚本所需的权限。

如果您计划将脚本放在自定义位置，则默认服务用户可能没有对自定义位置的读取权限。 对于这种情况，请执行以下步骤以为自定义位置提供必要的权限：

1. 以编程方式或通过控制台https://&#39;[服务器]:[port]&#39;/crx/explorer创建系统用户。 您还可以使用现有系统用户。 与这里的系统用户而不是普通用户一起工作非常重要。
1. 在存储脚本的自定义位置为新创建或现有系统用户提供读取权限。 您可以有多个自定义位置。 为所有自定义位置提供至少读取权限。
1. 在Felix配置控制台(/system/console/configMgr)中，找到监视文件夹的服务用户映射。 此映射类似于“映射： adobe-aemds-core-watch-folder=...”
1. 单击映射。 对于条目“adobe-aemds-core-watch-folder:scripts=fd-service”，将fd-service更改为自定义系统用户的ID。 单击保存。

现在，您可以使用已配置的自定义位置来保存脚本。

### 使用工作流处理监视文件夹的文件 {#using-a-workflow-to-process-files-of-a-watched-folder}

工作流使您能够自动Experience Manager活动。 工作流由一系列按特定顺序执行的步骤组成。 每个步骤都会执行不同的活动，如激活页面或发送电子邮件。 工作流可以与存储库中的资产、用户帐户和Experience Manager服务进行交互。 因此，工作流可以协调复杂。

* 在创建工作流之前，请考虑以下几点：
* 步骤的输出必须可用于所有后续步骤。
这些步骤必须能够更新（甚至删除）由前些步骤生成的现有输出。
* 可变变量用于在步骤之间流动自定义动态数据。

执行以下步骤以使用工作流处理文件：

1. 创建接口的 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 实现。 它类似于为服务创建的实现。

   >[!NOTE]
   >
   >您可以完全在ECMAScript中创建完整的实现。

1. 在工作流的步骤中，找到com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService类型的OSGi服务，并使用以下参数调用该服务的execute()方法。

   * WorkflowContextProcessor界面的自定义实现
   * workItem
   * workflowSession
   * 元数据

如果使用Java编程语言实现工作流，则AEM工作流引擎为workItem、workflowSession和元数据变量提供值。 这些变量作为参数传递给自定义WorkflowProcess实现的execute()方法。

如果使用ECMAScript实现工作流，则AEM工作流引擎为graniteWorkItem、graniteWorkflowSession和元数据变量提供值。 这些变量作为参数传递给WorkflowContextService.execute()方法。

processWorkflowContext()的参数是com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext类型的对象。 WorkflowContext界面具有以下API，以便于执行上述工作流特定的注意事项：

* getWorkItem: 返回WorkItem变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getWorkflowSession: 返回WorkflowSession变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getMetadata: 返回元数据变量的值。 变量将传递到WorkflowContextService.execute()方法。
* getCommittedVariables: 返回表示由前一步骤设置的变量的只读对象映射。 如果在以前的任何步骤中未修改变量，则会返回配置监视文件夹时指定的默认值。
* getCommittedResults: 返回只读文档图。 该映射表示由前些步骤生成的输出文件。
* setVariable: WorkflowContextProcessor实现使用变量来操作表示在步骤之间流动的自定义动态数据的变量。 变量的名称和类型与配置监视文件夹期间指定的变 [量的名称相同](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)。 要更改变量的值，请使用非null值调用setVariable API。 要删除变量，请调用值为null的setVariable()。

还提供以下ProcessorContext API:

* getWatchFolderId: 返回已监视文件夹的ID。
* getInputMap: 返回Map&lt;String,文档>类型的映射。 映射的键是输入文件的文件名和包含文件内容的文档对象。 使用getinputMap API读取输入文件。
* getConfigParameters: 返回Map&lt;String, Object>类型的不可变映射。 映射包含监视文件夹的配置参数。
* setResult: ContentProcessor实现使用API将输出文档写入结果文件夹。 可为setResult API提供输出文件的名称。 API可能会根据指定的输出文件夹／文件模式选择使用或忽略提供的文件。 如果指定了文件夹模式，则输出文件的名称如工作流中所述。 如果指定了文件模式，则输出文件具有文件模式中所述的名称

在工作流中使用setResult API时的考虑事项：

* 要添加对整个工作流输出有贡献的新输出文档，请调用setResult API，其文件名在之前的任何步骤中尚未用作输出文件名。
* 要更新由上一步生成的输出，请调用setResult API，其文件名已由上一步使用。
* 要删除由上一步生成的输出，请调用setResult，其文件名已被上一步使用，而空值为内容。

>[!NOTE]
>
>在任何其他情况中调用内容为null的setResult API将导致错误。

以下示例作为工作流步骤实现。 在示例中，ECMAscript使用变量stepCount跟踪当前工作流实例中调用步骤的次数。
输出文件夹的名称是当前步骤编号、原始文件名和在outPrefix参数中指定的前缀的组合。

ECMAScript获取工作流上下文服务的参考并创建WorkflowContextProcessor接口的实现。 WorkflowContextProcessor实现接受输入文件，将文件复制到临时位置，并返回表示复制文件的文档。 根据布尔变量purgePrevious的值，当前步骤将删除上次由当前工作流实例中启动该步骤时的同一步骤生成的输出。 最后，调用wfSvc.execute方法执行WorkflowContextProcessor实现。 输出文档的内容将保存到结果文件夹中“监视文件夹”配置节点中提到的物理路径。

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

### 创建有效负荷映射器过滤器以将已监视文件夹的结构映射到工作流的有效负荷 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

在创建监视的文件夹时，它会在被监视的文件夹中创建文件夹结构。 文件夹结构具有阶段、结果、保留、输入和失败文件夹。 文件夹结构可用作工作流的输入有效负荷，并接受工作流的输出。 它还可以列表故障点（如果有）。

如果有效负荷的结构与监视文件夹的结构不同，您可以编写自定义脚本将监视文件夹的结构映射到有效负荷。 这种脚本称为负载映射器过滤器。 现成AEM Forms提供有效负荷映射器过滤器，以将已监视文件夹的结构映射到有效负荷。

#### 创建自定义有效负荷映射器过滤器 {#creating-a-custom-payload-mapper-filter}

1. 下 [载Adobe Client SDK](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aemfd/aemfd-client-sdk/6.3.0/aemfd-client-sdk-6.3.0.jar)。
1. 在基于Maven的项目的构建路径中设置客户端SDK。 要开始，您可以在自己选择的IDE中下载并打开以下基于主机的项目。
1. 编辑示例包中可用的有效负荷映射器过滤器代码，以满足您的要求。
1. 使用maven创建自定义有效负荷映射器过滤器的捆绑。
1. 使 [用AEM包控制台](https://localhost:4502/system/console/bundles) ，安装该包。

   现在，自定义“负载映射器”过滤器列在AEM监视文件夹UI中。 您可以将其用于工作流。

   以下示例代码为相对于有效负荷保存的文件实现了一个基于文件的简单映射器。 您可以使用它开始。

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

## 用户如何与监视文件夹交互 {#how-users-interact-with-a-watched-folder}

对于监视文件夹端点，用户可以通过将输入文件或文件夹从桌面复制或拖动到监视文件夹，来开始文件处理操作。 文件按到达顺序处理。

对于监视文件夹端点，如果作业只需要一个输入文件，则用户可以将该文件复制到监视文件夹的根目录中。

如果作业包含多个输入文件，则用户必须在监视文件夹层次结构之外创建一个包含所有必需文件的文件夹。 此新文件夹应包括输入文件（如果进程需要，还可选择包含DDX文件）。 作业文件夹构建完成后，用户将其复制到监视文件夹的输入文件夹中。

>[!NOTE]
>
>确保应用程序服务器已删除对监视文件夹中文件的访问权限。 如果AEM Forms在扫描文件后无法从输入文件夹删除文件，则关联的进程将无限期地启动。

## 有关监视文件夹的其他信息 {#additional-information-about-the-watched-folders}

### 关于限制 {#about-throttling}

当为监视文件夹端点启用限制时，它会限制在任何给定时间处理的监视文件夹作业数。 最大作业数由批量大小值确定，也可在监视文件夹端点中进行配置。 达到限制限制后，不会轮询“监视文件夹”输入目录中的传入文档。 该文档也会保留在输入目录中，直到完成其他“已监视文件夹”作业并再次尝试投票。 对于同步处理，在单次轮询中处理的所有作业都计入限制，即使这些作业在单个线程中连续处理也是如此。

>[!NOTE]
>
>限制不随群集扩展。 启用限制后，群集作为一个整体将不会在任何给定时间处理超过批量大小中指定的作业数。 此限制在群集范围内，并非特定于群集中的每个节点。 例如，如果“批处理大小”为2，则只有一个节点处理两个作业时，才能达到限制限制，并且在完成其中一个作业之前，其他节点都不会轮询输入目录。

#### 限制的工作原理 {#how-throttling-works}

监视文件夹在每个pollInterval扫描输入文件夹，选取批量大小中指定的文件数，并为每个文件调用目标服务。 例如，如果批处理大小为4，则在每次扫描时，监视文件夹会选取四个文件，创建四个调用请求并调用目标服务。 在完成这些请求之前，如果调用了“监视文件夹”，则再次开始4个作业，而不管以前4个作业是否完成。

限制可防止监视文件夹在以前的作业未完成时调用新作业。 监视文件夹检测正在进行的作业，并根据批处理大小减正在进行的作业处理新作业。 例如，在第二次调用中，如果完成的作业数仅为3，而一个作业仍在进行，则“监视文件夹”仅再调用3个作业。

* “监视文件夹”依赖舞台文件夹中存在的文件数来确定正在进行的作业数。 如果文件在舞台文件夹中仍未处理，“监视文件夹”将不再调用任何其他作业。 例如，如果批量大小为4，并且停止了3个作业，则“监视文件夹”在后续调用中只调用一个作业。 存在多种情况，这些情况会导致文件在阶段文件夹中保持未处理状态。 安装作业后，管理员可以终止“进程管理”管理页面上的进程，以便“监视文件夹”将文件移出舞台文件夹。
* 如果AEM Forms服务器在“监视文件夹”调用作业之前关闭，则管理员可以将文件移出舞台文件夹。 有关信息，请参 [阅故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。
* 如果AEM Forms服务器正在运行，但当作业管理器服务回调时监视文件夹未运行(在服务未按顺序开始时发生)，则管理员可以将文件移出舞台文件夹。 有关信息，请参 [阅故障点和恢复](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p)。

### 故障点和恢复故障点和恢复 {#failure-points-and-recoveryfailure-points-and-recovery}

在每个投票事件下，“监视文件夹”锁定输入文件夹，将与包含文件模式匹配的文件移动到舞台文件夹，然后解锁输入文件夹。 需要锁定，这样两个线程就不会选取同一组文件并处理它们两次。 发生这种情况的几率会随着pollInterval和大批量而增加。 将文件移到舞台文件夹后，将解锁输入文件夹，以便其他线程可以扫描文件夹。 此步骤有助于提供高吞吐量，因为在一个线程处理文件时，其他线程可以进行扫描。

将文件移到舞台文件夹后，将为每个文件创建调用请求并调用目标服务。 有时监视文件夹无法恢复舞台文件夹中的文件：

* 如果服务器在监视文件夹创建调用请求之前关闭，则舞台文件夹中的文件仍保留在舞台文件夹中，并且无法恢复。

* 如果监视文件夹已成功为舞台文件夹中的每个文件创建调用请求，且服务器崩溃，则基于调用类型有两种行为：

   * **同步**: 如果“监视文件夹”配置为同步调用服务，则舞台文件夹中的所有文件在舞台文件夹中仍未处理。
   * **异步**: 在这种情况下，监视文件夹依赖于作业管理器服务。 如果作业管理器服务回调监视文件夹，则根据调用结果将舞台文件夹中的文件移动到保留或失败文件夹。 如果作业管理器服务不回叫监视文件夹，则这些文件在阶段文件夹中将保持未处理状态。 当作业管理器回叫时，监视文件夹未运行时，会发生这种情况。

#### 恢复舞台文件夹中未处理的源文件 {#recover-unprocessed-source-files-in-the-stage-folder}

当监视文件夹无法处理舞台文件夹中的源文件时，您可以恢复未处理的文件。

1. 重新启动应用程序服务器或节点。

1. 停止监视文件夹处理新的输入文件。 如果跳过此步骤，将更难确定舞台文件夹中哪些文件未处理。 要阻止监视文件夹处理新的输入文件，请执行下列任务之一：

   * 将“监视文件夹”的includeFilePattern属性更改为与任何新输入文件不匹配的内容（例如，输入NOMATCH）。
   * 暂停创建新输入文件的进程。

   等待AEM Forms恢复并处理所有文件。 大多数文件都应该恢复，并且所有新的输入文件都应正确处理。 等待监视文件夹恢复和处理文件的时间长短取决于要调用的操作长度和要恢复的文件数。

1. 确定无法处理哪些文件。 如果您等了适当的时间并完成了上一步，并且舞台文件夹中仍保留未处理的文件，请转到下一步。

   >[!NOTE]
   >
   >您可以查看舞台目录中文件的日期和时间戳。 根据文件数和正常处理时间，您可以确定哪些文件的版本足够旧，以便被视为卡住。

1. 将未处理的文件从舞台目录复制到输入目录。

1. 如果您阻止监视文件夹在步骤2中处理新的输入文件，请将“包括文件模式”更改为其以前的值，或重新启用您禁用的进程。

### 将监视的文件夹链在一起 {#chain-watched-folders-together}

监视文件夹可以链接在一起，这样一个监视文件夹的结果文档就是下一个监视文件夹的输入文档。 每个监视文件夹都可以调用不同的服务。 通过以这种方式配置监视文件夹，可以调用多个服务。 例如，一个监视文件夹可以将PDF文件转换为Adobe PostScript®，另一个监视文件夹可以将PostScript文件转换为PDF/A格式。 为此，只需将第一个端点定义的监视文件夹的结果文件夹设置为指向第二个端点定义的监视文件夹的输入文件夹。

第一次转换的输出将转到\path\result。 第二个转换的输入为\path\result，第二个转换的输出将转到\path\result\result （或在“结果文件夹”框中为第二个转换定义的目录）。

### 文件和文件夹模式 {#file-and-folder-patterns}

管理员可以指定可调用服务的文件类型。 可以为每个监视文件夹建立多个文件模式。 文件模式可以是以下文件属性之一：

* 具有特定文件扩展名的文件； 例如，*.dat、*.xml、.pdf、*。*
* 具有特定名称的文件； 例如，数据。*
* 名称和扩展名中具有复合表达式的文件，如以下示例所示：

   * 数据[0-9][0-9][0-9]。[dD][aA]&#39;port&#39;
   * *.[dD][Aa]&#39;port&#39;
   * *.[Xx]毫[米][Ll]

* 管理员可以定义输出文件夹的文件模式，以在其中存储结果。 对于输出文件夹（结果、保留和失败），管理员可以指定以下任意文件模式：
* %Y =年（已满）
* %y =年（最后两位）
* %M =月，
* %D =月日，
* %d =年份日，
* %h =小时，
* %m =分钟，
* %s =秒，
* %R = 0-9之间的随机数
* %J =作业名称

例如，结果文件夹的路径可能为C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d。

输出参数映射还可以指定其他模式，如：

* %F =源文件名
* %E =源文件扩展名

如果输出参数映射模式以“File.separator”（即路径分隔符）结尾，则会创建一个文件夹，并将内容复制到该文件夹中。 如果模式不以“File.separator”结尾，则内容（结果文件或文件夹）将使用该名称创建。

## 将PDF生成器与监视的文件夹一起使用 {#using-pdf-generator-with-a-watched-folder}

您可以配置监视文件夹以启动工作流、服务或脚本以处理输入文件。 在下一节中，我们将配置一个监视文件夹以启动ECMAScript。 ECMAScript将使用PDF Generator将Microsoft Word(.docx)文档转换为PDF文档。

请执行以下步骤，使用PDF生成器配置监视的文件夹：

1. [创建ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [创建工作流](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [配置监视文件夹](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### 创建ECMAScript {#create-an-ecmascript}

ECMAScript将使用PDF Generator的createPDF API将Microsoft Word(.docx)文档转换为PDF文档。 请执行以下步骤以创建脚本：

1. 在浏览器窗口中打开CRXDE lite。 URL为https://&#39;[server]:[port]&#39;/crx/de。

1. 导航到/etc/workflow/scripts并创建一个名为PDFG的文件夹。

1. 在PDFG文件夹中，创建一个名为pdfg-openOffice-sample.ecma的文件，并将以下代码添加到该文件：

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

1. 保存并关闭文件。

### 创建工作流 {#create-a-workflow}

1. 在浏览器窗口中打开AEM工作流UI。
https://[servername]:&#39;port&#39;/workflow

1. 在“模型”视图中，单击“ **新建**”。 在“新建工作流”对话框中，指 **定“标**&#x200B;题”，然后 **单击“确定”**。

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 选择新创建的工作流，然后单击“ **编辑**”。 该工作流将在新窗口中打开。

1. 删除默认工作流步骤。 将流程步骤从Sidekick拖放到工作流。

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 右键单击“处理步骤”，然后选择“ **编辑**”。 出现“Step Properties（步骤属性）”窗口。

1. 在“进程”选项卡中，选择ECMAScript。 例如，在“创建ECMAScript”中创建的pdfg-openOffice-sample. [ecma脚本](#p-create-an-ecmascript-p)。 启用“处 **理程序高级** ”选项并单 **击“确定”**。

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 配置监视文件夹 {#configure-the-watched-folder}

1. 在浏览器窗口中打开CRXDE lite。 https://&#39;[服]务[器]:port&#39;/crx/de/

1. 导航到/etc/fd/watchfolder/config/文件夹，创建nt:unstructured类型的节点。

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 向节点添加以下属性：

   * folderPath（字符串）: 要在定义的时间间隔内扫描的文件夹的路径。 该文件夹必须位于共享位置，所有服务器都具有对服务器的完全访问权限。
inputProcessorType（字符串）: 要开始的进程类型。 在本教程中，指定工作流。

   * inputProcessorId（字符串）: inputProcessorId属性的行为基于为inputProcessorType属性指定的值。 在此示例中，inputProcessorType属性的值为workflow。 因此，对于inputProcessorId属性，指定PDFG工作流的以下路径： /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern（字符串）: 输出文件的模式。 可以指定文件夹或文件模式。 如果指定了文件夹模式，则输出文件的名称如工作流中所述。 如果指定了文件模式，则输出文件具有文件模式中所述的名称。
   除了上述必选属性之外，“监视文件夹”还支持一些可选属性。 有关可选属性的完整列表和说明，请参阅 [监视文件夹属性](#watchedfolderproperties)。

