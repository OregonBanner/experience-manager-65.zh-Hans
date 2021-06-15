---
title: 用于处理元数据、图像和视频的配置文件
description: 配置文件是一组有关要应用于已上传到文件夹的资产的选项的规则。 指定要应用于您上传的视频资产的元数据配置文件和视频编码配置文件。 对于图像资产，您还可以指定要应用于图像资产的图像配置文件，以正确裁剪图像资产。
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
role: Business Practitioner, Administrator
feature: 工作流，资产管理，演绎版
exl-id: 3d9367ed-5a02-43aa-abd9-24fae457d4c5
source-git-commit: 4ad5237939289b5411a988424b2a3ecad15ca029
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 4%

---

# 用于处理元数据、图像和视频的配置文件{#profiles-for-processing-metadata-images-and-videos}

配置文件是用于将哪些选项应用于已上传到文件夹的资产的方法。 例如，您可以指定特定的元数据配置文件和视频编码配置文件，并将这些配置文件应用到您上传的视频资产。您还可以指定特定的图像配置文件，并将配置文件应用到图像资产，以便对图像资产进行适当的裁剪。

这些规则可以包括添加元数据、智能裁剪图像或创建视频编码配置文件。 在Adobe Experience Manager中，您可以创建三种类型的用户档案，以下链接详细介绍了这些用户档案：

* [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles)
* [图像配置文件](/help/assets/image-profiles.md)
* [视频配置文件](/help/assets/video-profiles.md)

您必须拥有管理员权限，才能创建、编辑和删除元数据、图像或视频配置文件。

创建元数据、图像或视频配置文件后，您需要将其分配给一个或多个文件夹，以用作新上传资产的目标。

有关在Experience Manager资产中使用配置文件的一个重要概念是，将配置文件分配给文件夹。 配置文件中包括元数据配置文件形式的设置，以及视频配置文件或图像配置文件。 这些设置会处理文件夹及其任何子文件夹的内容。 因此，您如何命名文件和文件夹、如何排列子文件夹以及如何处理这些文件夹中的文件，都会对配置文件处理这些资产的方式产生重大影响。
通过使用一致且适当的文件和文件夹命名策略以及良好的元数据实践，您可以充分利用数字资产收藏集，并确保使用正确的配置文件处理正确的文件。

>[!NOTE]
>
>从一个文件夹移动到另一个文件夹的资产不再重新处理。例如，假定您的文件夹1中分配了配置文件A，而文件夹2中分配了配置文件B。 如果将资产从文件夹1移动到文件夹2，则被移动的资产将保留其在文件夹1中的原始处理。
>
>即使在两个文件夹之间移动资产时，也是如此，因为这两个文件夹分配了相同的配置文件。

## 重新处理文件夹{#reprocessing-assets}中的资产

>[!NOTE]
>
>仅适用于Experience Manager6.4.6.0或更高版本中的&#x200B;*Dynamic Media - Scene7模式*。

您可以重新处理文件夹中的资产，该文件夹中已有您稍后更改的现有处理配置文件。

例如，假定您创建了图像配置文件并将其分配给文件夹。 您上传到文件夹的任何图像资产都会自动将图像配置文件应用到这些资产。 但是，之后您决定向用户档案添加新的智能裁剪比例。 现在，您只需运行&#x200B;*Scene7即可，而不必再次选择资产并将其重新上传到文件夹：重新处理资产*&#x200B;工作流。

您可以对首次处理失败的资产运行重新处理工作流。 因此，即使您未编辑处理配置文件或应用了处理配置文件，您仍然可以随时对资产文件夹运行重新处理工作流。

您可以（可选）从默认的50个资产（最多1000个资产）调整重新处理工作流的批大小。 运行&#x200B;_Scene7时：在文件夹上重新处理资产_&#x200B;工作流，会将资产分批分组，然后将其发送到Dynamic Media服务器进行处理。 处理后，整个批处理集中每个资产的元数据都会在Experience Manager时更新。 如果批次大小较大，则处理过程可能会延迟。 或者，如果批次大小过小，则可能会导致到Dynamic Media服务器的往返次数过多。

请参阅[调整重新处理工作流的批处理大小](#adjusting-load)。

>[!NOTE]
>
>如果您要将资产从Dynamic Media Classic批量迁移到Experience Manager，则必须在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
>
>必须在Dynamic Media服务器上禁用迁移发布代理，以便重新处理工作流按预期工作。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**要重新处理文件夹中的资产，请执行以下操作：**

1. 在Experience Manager中，从“资产”页面中，导航到一个资产文件夹，该文件夹中的资产分配了处理配置文件，您要对其应用&#x200B;**[!UICONTROL Scene7:重新处理资产]**&#x200B;工作流，

   如果文件夹已经分配了处理配置文件，则卡片视图中文件夹名称的正下方会显示配置文件的名称。

1. 选择文件夹。

   * 工作流会递归地考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个包含资产的子文件夹，则工作流会重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，您应避免在资产超过1000个的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中，单击&#x200B;**[!UICONTROL 时间轴]**。
1. 在页面左下角附近，在评论字段的右侧，单击加载图标(**^**)。

   ![重新处理资产工作流1](/help/assets/assets/reprocess-assets1.png)

1. 单击&#x200B;**[!UICONTROL 启动工作流]**。
1. 从&#x200B;**[!UICONTROL 启动工作流]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。
1. （可选）在&#x200B;**输入工作流**&#x200B;文本字段的标题中，输入工作流的名称。 如有必要，您可以使用名称引用工作流实例。

   ![重新处理资产2](/help/assets/assets/reprocess-assets2.png)

1. 单击&#x200B;**[!UICONTROL 开始]**，然后单击&#x200B;**[!UICONTROL 确认]**。

   要监控工作流或检查其进度，请从Experience Manager主控制台页面中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]**。 在工作流实例页面上，选择一个工作流。 在菜单栏上，单击&#x200B;**[!UICONTROL 打开历史记录]**。 您还可以从同一工作流实例页面中终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批处理大小{#adjusting-load}

（可选）重新处理工作流中的默认批大小为每个作业50个资产。 此最佳批处理大小受平均资产大小和运行重新处理的资产的MIME类型的约束。 值越高，表示您在一个重新处理作业中拥有许多文件。 因此，处理横幅会在Experience Manager资产上停留较长时间。 但是，如果平均文件大小较小（1 MB或更小），则Adobe建议您将值增加到100，但最多不超过1000。 如果文件平均大小较大（如数百MB），则Adobe建议您将批处理大小减少到10。

**（可选）要调整重新处理工作流的批大小，请执行以下操作：**

1. 在Experience Manager中，单击&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;以访问全局导航控制台，然后单击&#x200B;**[!UICONTROL 工具]**（锤子）图标> **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面的卡片视图或列表视图中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。

   ![工作流模型页面，其中包含Scene7:重新处理在卡片视图中选择的资产工作流](/help/assets/assets-dm/reprocess-assets7.png)

1. 在工具栏上，单击&#x200B;**[!UICONTROL 编辑]**。 新的浏览器选项卡会打开Scene7:重新处理资产工作流模型页面。
1. 在Scene7上：重新处理资产工作流页面右上角附近，单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以“解锁”工作流。
1. 在工作流中，选择Scene7批量上传组件以打开工具栏，然后单击工具栏中的&#x200B;**[!UICONTROL 配置]** 。

   ![Scene7批量上传组件](/help/assets/assets-dm/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7 — 步骤属性]**&#x200B;对话框中，设置以下内容：
   * 在&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**&#x200B;文本字段中，根据需要为作业输入新标题和描述。
   * 如果处理程序将前进到下一步，请选择&#x200B;**[!UICONTROL 处理程序Advance]**。
   * 在&#x200B;**[!UICONTROL Timeout]**&#x200B;字段中，输入外部进程超时（秒）。
   * 在&#x200B;**[!UICONTROL Period]**&#x200B;字段中，输入轮询间隔（秒）以测试外部进程的完成情况。
   * 在&#x200B;**[!UICONTROL 批处理字段]**&#x200B;中，输入在Dynamic Media服务器批处理上传作业中要处理的资产最大数量(50-1000)。
   * 如果希望在达到超时时提前，请选择&#x200B;**[!UICONTROL 超时时提前]**。 如果要在达到超时时继续进入收件箱，请取消选择。

   ![“属性”对话框](/help/assets/assets-dm/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7 — 步骤属性]**&#x200B;对话框的右上角，单击&#x200B;**[!UICONTROL 完成]**。

1. 位于Scene7的右上角：重新处理资产工作流模型页面，单击&#x200B;**[!UICONTROL 同步]**。 当您看到&#x200B;**[!UICONTROL Synced]**&#x200B;时，工作流运行时模型已成功同步，并可以重新处理文件夹中的资产。

   ![同步工作流模型](/help/assets/assets-dm/reprocess-assets1.png)

1. 关闭显示Scene7的浏览器选项卡：重新处理资产工作流模型。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
