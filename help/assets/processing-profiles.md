---
title: 用于处理元数据、图像和视频的配置文件
description: 配置文件包含一组规则，这些规则围绕要应用于上传到文件夹的资产的选项。 指定要应用于您上传的视频资产的元数据配置文件和视频编码配置文件。 对于图像资产，您还可以指定要应用到图像资产的图像配置文件，以便正确裁剪它们。
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 用于处理元数据、图像和视频的配置文件{#profiles-for-processing-metadata-images-and-videos}

配置文件是一种菜谱，用于将哪些选项应用到上传到文件夹的资产。 例如，您可以指定特定的元数据配置文件和视频编码配置文件，并将这些配置文件应用到您上传的视频资产。您还可以指定特定的图像配置文件，并将配置文件应用到图像资产，以便对图像资产进行适当的裁剪。

这些规则可以包括添加元数据、智能裁剪图像或创建视频编码配置文件。 在AEM中，您可以创建三种类型的配置文件，这些配置文件将在以下链接中详细介绍：

* [元数据配置文件](/help/assets/metadata-profiles.md)
* [图像配置文件](/help/assets/image-profiles.md)
* [视频配置文件](/help/assets/video-profiles.md)

您必须拥有管理员权限才能创建、编辑和删除元数据、图像或视频配置文件。

在创建元数据、图像或视频配置文件后，您可以将其分配到一个或多个文件夹，以用作新上传资产的目标。

关于在AEM资产中使用配置文件的一个重要概念是，配置文件被分配到文件夹。 配置文件中包含元数据配置文件形式的设置，以及视频配置文件或图像配置文件。 这些设置将处理文件夹的内容及其任何子文件夹。 因此，您如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件都会对配置文件处理这些资产的方式产生重大影响。
通过使用一致、适当的文件和文件夹命名策略，以及良好的元数据实践，您可以充分利用数字资产集合，并确保通过正确的配置文件处理正确的文件。

>[!NOTE]
>
>从一个文件夹移动到另一个文件夹的资产不再重新处理。例如，假设您的文件夹1分配了配置文件A，而文件夹2分配了配置文件B。 如果将资产从文件夹1移到文件夹2，则移动的资产将保留其从文件夹1的原始处理。
>
>即使在分配了相同配置文件的两个文件夹之间移动资产，情况也是如此。

## 重新处理文件夹中的资产 {#reprocessing-assets}

>[!NOTE]
>
>仅适用于 ** AEM 6.4.6.0或更高版本中的Dynamic Media - Scene7模式。

您可以重新处理文件夹中的资产，该文件夹中已有您稍后更改的现有处理配置文件。

例如，假定您创建了图像配置文件并将其分配到文件夹。 您上传到该文件夹的任何图像资产都会自动将图像配置文件应用到资产。 但是，稍后您决定向配置文件添加新的智能裁剪比例。 现在，您只需运行 *Scene7，而不必再再次选择资产并将其重新上传到文件夹：重新处理资产* 工作流。

您可以对首次处理失败的资产运行重新处理工作流。 因此，即使您尚未编辑处理配置文件或应用了处理配置文件，您仍然可以随时对资产文件夹运行重新处理工作流。

您可以选择调整重新处理工作流的批大小（默认值为50个资产，最多为1000个资产）。 运行 _Scene7时：在文件夹上重新处理_ “资产”工作流，资产会分批分组在一起，然后发送到Dynamic Media服务器进行处理。 在进行处理后，整个批集中每个资产的元数据会在AEM上更新。 如果批量很大，您可能会遇到处理延迟。 或者，如果批量太小，则可能导致过多的往返到Dynamic Media服务器。

请参 [阅调整重新处理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果要将资产从Dynamic Media Classic批量迁移到AEM，则必须在Dynamic media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
迁移发布代理必须在Dynamic media服务器上禁用，以便重新处理工作流按预期工作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**要重新处理文件夹中的资产，请执行以下操作**:
1. 在AEM中，从“资产”页面，导航到一个资产文件夹，该文件夹已为其分配了处理配置文件，并且您要为其应用 **Scene7:重新处理资产** ,

   如果文件夹已经分配了处理配置文件，则卡片视图中的文件夹名称正下方会显示配置文件的名称。

1. 选择文件夹。

   * 该工作流会定期考虑选定文件夹中的所有文件。
   * 如果一个或多个子文件夹在主选定文件夹中包含资产，则该工作流将重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，您应避免在资产超过1000个的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中，单击时间 **[!UICONTROL 轴]**。
1. 在页面左下角附近的“评论”字段的右侧，单击“插入”图标( **^** )。

   ![重新处理资产工作流1](/help/assets/assets/reprocess-assets1.png)

1. 单击“ **[!UICONTROL 启动工作流]**”。
1. 从“开 **[!UICONTROL 始工作流]** ”下拉列表中，选择 **[!UICONTROL Scene7:重新处理资产]**。
1. （可选）在“输 **入工作流的标题** ”文本字段中，输入工作流的名称。 如有必要，可以使用名称引用工作流实例。

   ![重新处理资产2](/help/assets/assets/reprocess-assets2.png)

1. 单击“ **[!UICONTROL 开始]**”，然后单击“ **[!UICONTROL 确认”]**。

   要监视工作流或检查其进度，请在AEM主控制台页面中，单击工具>工 **[!UICONTROL 作流]**。 在“工作流实例”页面上，选择一个工作流。 在菜单栏上，单击“打 **[!UICONTROL 开历史记录”]**。 您还可以从同一“工作流实例”页面终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批大小 {#adjusting-load}

（可选）重新处理工作流中的默认批大小为每个作业50个资产。 此最佳批量大小受运行重新处理的资产的平均资产大小和MIME类型的约束。 值越高，意味着您在一个重新处理作业中将拥有许多文件。 因此，处理横幅在AEM资产上停留的时间较长。 但是，如果平均文件大小为1 MB或更小- adobe建议您将该值增加到几百，但不要超过1000。 如果文件的平均大小是数百兆字节，Adobe建议您将批处理大小降低至10。

**（可选）要调整重新处理工作流的批大小**

1. 在Experience Manager中，点按 **[!UICONTROL Adobe Experience Manager]** ，以访问全局导航控制台，然后点按工具 **[!UICONTROL （锤子）图标>工作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面的卡片视图或列表视图中，选择 **[!UICONTROL Scene7:重新处理资产]**。

   ![“工作流模型”页面：在卡片视图中选择的重新处理资产工作流](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具栏上，单击“编 **[!UICONTROL 辑”]**。 新的浏览器选项卡会打开Scene7:重新处理资产工作流模型页面。
1. 在Scene7上：重新处理资产工作流页面，在右上角附近，点按编 **[!UICONTROL 辑]** ，以“解锁”工作流。
1. 在工作流中，选择Scene7批上传组件以打开工具栏，然后点按工具栏 **[!UICONTROL 上的配置]** 。

   ![Scene7批量上传组件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在“批 **[!UICONTROL 量上传到Scene7-步骤属性”对话框中]** ，设置以下各项：
   * 在“标 **[!UICONTROL 题]** ”和“说 **** 明”文本字段中，根据需要为作业输入新标题和说明。
   * 如果处 **[!UICONTROL 理程序将前进到下一步]** ，请选择“处理程序前进”。
   * 在“超 **[!UICONTROL 时]** ”字段中，输入外部进程超时（秒）。
   * 在“ **[!UICONTROL 期间]** ”字段中，输入轮询间隔（秒）以测试外部进程是否完成。
   * 在“批 **[!UICONTROL 处理”字段]**，输入要在Dynamic Media服务器批处理上传作业中处理的资产最大数量(50-1000)。
   * 如果 **[!UICONTROL 要在到达超时时前进]** ，请选择超时前进。 如果要在到达超时时继续进入收件箱，请取消选择。
   ![属性对话框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在“批量上传到Scene7 —— 步 **[!UICONTROL 骤属性”对话框的右上角]** ，点按 **[!UICONTROL 完成]**。

1. 在Scene7的右上角：重新处理资产工作流模型页面，点按 **[!UICONTROL 同步]**。 当您看到“已 **[!UICONTROL 同步]**”时，工作流运行时模型已成功同步并且可以重新处理文件夹中的资产。

   ![同步工作流模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 关闭显示Scene7的浏览器选项卡：重新处理资产工作流模型。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
