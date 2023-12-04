---
title: 创建或配置观察文件夹
description: 了解如何创建或删除watched文件夹，或修改现有watched文件夹的属性。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---

# 创建或配置观察文件夹 {#create-or-configure-a-watched-folder}

管理员可以配置网络文件夹，称为 *观察文件夹*，以便当用户将文件(如PDF文件)放置在watched文件夹中时，将启动预配置的操作并操作该文件。 执行指定的操作后，该操作会将修改的文件保存在指定的输出文件夹中。 有关管理watched文件夹的详细信息，请参见 [管理帮助](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

可以使用watched文件夹用户界面执行以下操作：

* 创建观察文件夹
* 修改现有观察文件夹的属性
* 删除观察文件夹

## 创建观察文件夹 {#create-a-watched-folder}

在配置watched文件夹之前，请确保：

* Watched文件夹是AEM表单的高级功能。 它需要AEM Forms附加组件包才能正常运行。 确保已安装并配置适当的AEM Forms附加组件包。
* 您可以在共享存储或本地存储中创建观察文件夹。 确保配置为运行watched文件夹的AEM forms用户对watched文件夹具有读写权限。
* 您可以使用服务、工作流或脚本来自动执行监视文件夹的操作。 确保相应的服务、工作流或脚本已创建并准备运行。 有关创建服务、工作流和脚本的信息，请参见 [处理文件的各种方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* 观察文件夹具有各种属性，请参见 [观察文件夹属性](watched-folder-in-aem-forms.md#watchedfolderproperties).

执行以下步骤可创建watched文件夹：

1. 选择 **Adobe Experience Manager** 图标（位于屏幕左上角）。
1. 选择 **工具** > **Forms** > **配置观察文件夹。** 将显示已配置的观察文件夹的列表。
1. 选择 **新建**. 此时将显示创建watched文件夹所需的字段列表：

   * **名称**：标识观察文件夹。 名称只能使用字母数字字符。
   * **路径**：指定watched文件夹位置。 在群集环境中，此设置必须指向共享网络文件夹，在群集的不同节点上运行AEM的每个用户都可以访问该文件夹。
   * **处理文件，使用**：要启动的进程类型。 您可以指定工作流、脚本或服务。
   * **服务名称/脚本路径/工作流路径**：字段的行为基于为指定的值 **处理文件，使用** 字段。 您可以指定以下值：

      * 对于工作流，请指定要执行的工作流模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：content/model
      * 对于脚本，指定要执行的脚本的JCR路径。 例如， /etc/watchfolder/test/testScript.ecma
      * 对于服务，指定用于查找OSGi服务的过滤器。 该服务已注册为com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的实现。 例如，以下代码是具有custom (foo=bar)属性的ContentProcessor界面的自定义实施。

   >[!NOTE]
   >
   >如果您已选择 **服务** 对于 **处理文件，使用** 字段，Service Name(inputProcessorType)字段的值必须括在括号中。 例如， (foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **输出文件模式**：指定观察文件夹用于确定输出文件和文件夹的名称和位置的用分号(；)分隔的模式列表。 有关文件模式的详细信息，请参见 [关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. 选择 **高级**. 高级选项卡包含更多字段。 这些字段中的大多数都包含默认值。

   * **有效负载映射器过滤器：** 创建watched文件夹时，会在被监视的文件夹内创建一个文件夹结构。 文件夹结构具有阶段、结果、保留、输入和失败文件夹。 文件夹结构可用作工作流的输入有效负荷并接受工作流的输出。 它还可以列出故障点（如果有）。 有效负荷的结构不同于观察文件夹的结构。 您可以编写自定义脚本以将观察文件夹的结构映射到有效负载。 此类脚本称为有效负荷映射器过滤器。 提供了两种现成的有效负载映射器实施。 如果您没有 [自定义实施](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，请使用以下现成的实施之一：

      * **默认映射器：** 使用默认有效负荷映射器将watched文件夹的输入和输出内容保留在有效负荷的单独输入和输出文件夹中。
      * **基于文件的简单有效负载映射器：** 使用基于简单文件的有效负荷映射器，将输入和输出内容直接保留在有效负荷文件夹中。 它不会创建任何额外的层次结构，如默认映射器。

   * **运行模式**：指定工作流执行所允许的运行模式列表（以逗号分隔）。
   * **每隔以下时间超时暂存文件**：指定已选取进行处理的输入文件/文件夹被视为已超时并标记为失败之前等待的秒数。 仅当此属性的值为正数时，超时机制才会激活。
   * **调整时删除已超时暂存文件**：如果启用，则 **每隔以下时间超时暂存文件** 仅当打开监视文件夹的限制时，机制才会激活。
   * **每隔以下时间扫描输入文件夹：** 以秒为单位指定时间间隔，用于扫描观察文件夹中的输入。 除非启用“限制”设置，否则“轮询间隔”应大于处理平均作业的时间；否则，系统可能会过载。 间隔的值必须大于或等于1。
   * **排除文件模式**：指定以分号(；)分隔的模式列表，观察文件夹将使用该列表来确定要扫描和选取的文件和文件夹。 不会扫描任何具有指定模式的文件或文件夹以进行处理。 有关文件模式的详细信息，请参见 [关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **包含文件模式**：指定以分号(；)分隔的模式列表，观察文件夹将使用该列表确定要扫描和选取的文件夹和文件。 例如，如果“包含文件模式”是input&amp;ast；，则选取与input&amp;ast；匹配的所有文件和文件夹。 默认值为&amp;ast；，表示所有文件和文件夹。 有关文件模式的详细信息，请参见 [关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **等待时间：** 指定在创建文件夹或文件后等待扫描的时间（以毫秒为单位）。 例如，如果等待时间为3,600,000毫秒（1小时），文件是在一分钟前创建的，则将在59分钟或更长时间后提取此文件。 默认值为 0。

     此设置对于确保文件或文件夹的所有内容都复制到输入文件夹非常有用。 例如，如果处理的文件很大，且下载文件需要10分钟，则将等待时间设置为10&amp;ast；60 &amp;ast；1000毫秒。 此间隔可防止观察文件夹在文件未满十分钟时扫描文件。

   * **删除早于以下时间的结果：** 指定删除早于指定值的文件和文件夹之前等待的时间（天数）。 此设置有助于确保结果文件夹不会变满。 值为–1天表示从不删除结果文件夹。 默认值为 -1。
   * **结果文件夹名称：** 指定要存储结果的文件夹的名称。 如果结果未出现在此文件夹中，请检查失败文件夹。 只读文件不会被处理，并保存在失败文件夹中。 可以将绝对路径或相对路径用于以下文件模式：

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
      * 例如，如果在2009年7月17日晚上8点，并且您指定C：/Test/WF0/failure/%Y/%M/%D/%H/，则结果文件夹为C：/Test/WF0/failure/2009/07/17/20。
      * 如果路径不是绝对路径而是相对路径，则会在观察文件夹内创建文件夹。 默认值为result/%Y/%M/%D/，它是watched文件夹内的Result文件夹。 有关文件模式的详细信息，请参见 [关于文件模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **失败文件夹名称：** 指定保存失败文件的文件夹。 此位置始终相对于观察文件夹。 您可以使用文件模式，如“结果文件夹”中所述。
   * **保留文件夹名称：** 指定成功扫描和提取后存储文件的文件夹。 路径可以是绝对、相对或空目录。 您可以使用文件模式，如“结果文件夹”中所述。 默认值为preserve/%Y/%M/%D/。
   * **批次大小：** 指定每次扫描要提取的文件或文件夹数。 它可防止系统过载；一次扫描太多文件可能会导致崩溃。 默认值为 2。

     如果扫描间隔很小，则线程会经常扫描输入文件夹。 如果文件经常被放入观察文件夹，则应该保持较小的扫描间隔。 如果文件不经常被丢弃，请使用较大的扫描间隔，以便其他服务可以使用线程。

   * **调整日期：** 启用此选项后，它会限制AEM Forms在任何给定时间处理的观察文件夹作业数。 “批次大小”值确定最大作业数。 有关更多信息，请参阅 [节流](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **用相似名称覆盖现有文件**：设置为True时，将覆盖结果文件夹和保留文件夹中的文件。 当设置为False时，使用具有数字索引后缀的文件和文件夹作为名称。 默认值为False。
   * **失败时保留文件：** 当设置为True时，如果失败，则保留输入文件。 默认值为true。
   * **包含文件模式：** 指定以分号(；)分隔的模式列表，观察文件夹使用该列表来确定要扫描和选取的文件夹和文件。 例如，如果输入“包括文件模式”，则会选取与输入匹配的所有文件和文件夹。 有关更多信息，请参阅 [管理帮助](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **异步调用观察文件夹：** 将调用类型标识为异步或同步。 默认值为asynchronous。 建议对长生命周期进程使用异步，对瞬态或短生命周期进程使用同步。
   * **启用Watched文件夹：** 启用此选项后，将启用监视文件夹。 默认值为True。

## 修改现有观察文件夹的属性 {#modify-properties-of-an-existing-watched-folder}

除了更改watched文件夹名称外，您还可以修改现有watched文件夹的所有属性。 执行以下步骤来修改现有watched文件夹的属性：

1. 选择 **Adobe Experience Manager** 图标（位于屏幕左上角）。
1. 选择 **工具** > **Forms** > **配置观察文件夹。** 将显示已配置的观察文件夹的列表。
1. 在Watched Folder屏幕的左侧，选择watchfolder并选择 **编辑。** 此时将显示创建watched文件夹所需的字段列表。 中列出的字段 **基本** 选项卡是必填项。 高级选项卡包含更多字段。 这些字段中的大多数都包含默认值。 您可以根据需要修改这些属性。
1. 修改属性后，选择 **更新**. 将保存修改后的属性。
