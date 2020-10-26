---
title: 创意项目和 PIM 集成
seo-title: 创意项目和 PIM 集成
description: 创意项目简化了整个照片拍摄工作流，包括生成照片拍摄请求、上传照片拍摄、协作处理照片拍摄以及打包已批准的资产
seo-description: 创意项目简化了整个照片拍摄工作流，包括生成照片拍摄请求、上传照片拍摄、协作处理照片拍摄以及打包已批准的资产
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '3013'
ht-degree: 68%

---


# 创意项目和 PIM 集成{#creative-project-and-pim-integration}

如果您是营销人员或创意专业人士，您可以使用Adobe Experience Manager(AEM)的创意项目工具管理您组织内与电子商务相关的产品摄影和相关的创意流程。

特别是，您可以使用“创意项目”来简化照片拍摄工作流中的以下任务：

* 生成照片拍摄请求
* 上传照片拍摄
* 协作处理照片拍摄
* 打包已批准的资产

>[!NOTE]
>
>请参阅[项目用户角色](/help/sites-authoring/projects.md#user-roles-in-a-project)，了解如何将用户角色和工作流分配给特定类型的用户。

## 了解产品照片拍摄工作流  {#exploring-product-photo-shoot-workflows}

创意项目提供了各种项目模板，可满足多种项目需求。**产品照片拍摄项目**&#x200B;模板可立即使用。此模板包含多个照片拍摄工作流，允许您发起并管理产品照片拍摄请求。它还包含一系列任务，使您能够通过相应的审核和批准流程获取产品的数字图像。

此模板包含以下工作流：

* **产品照片拍摄（商务集成）工作流**：此工作流利用与产品信息管理 (PIM) 系统的商务集成，自动为选定的产品（层次结构）生成拍摄列表。完成此工作流后，您可以查看资产元数据中包含的产品数据。
* **产品照片拍摄工作流**：通过此工作流，您可以自己提供拍摄列表，而无需依赖商务集成。此工作流会将上传的图像映射到项目资产文件夹中的 CSV 文件。

>[!NOTE]
>
>在产品照片拍摄工作流的“上传拍摄列表”任务中上传的 CSV 文件的文件名应当为 shotlist.csv。

## 创建产品照片拍摄项目 {#create-a-product-photo-shoot-project}

1. In the **Projects** console, tap/click **Create** and then choose **Create Project** from the list.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. 在&#x200B;**创建项目**&#x200B;页面中，选择照片拍摄项目模板，然后点按/单击&#x200B;**下一步**。

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. 输入项目详细信息，包括标题、描述和到期日期。添加用户，并为其分配不同的角色。您还可以为项目添加缩略图。

   ![chlimage_1-134](assets/chlimage_1-134a.png)

1. 点按/单击&#x200B;**创建**。此时会显示一条确认消息，通知您项目已创建。
1. Tap/click **Done** to return to the **Projects** console. Alternatively, tap/click **Open** to view the assets within the photoshoot project.

## 开始在产品照片拍摄项目中工作 {#starting-work-in-a-product-photo-shoot-project}

要发起照片拍摄请求，请点按或单击某个项目，然后在项目详细信息页面中点按/单击&#x200B;**添加工作**，以启动某个工作流。

![chlimage_1-135](assets/chlimage_1-135a.png)

产品照片拍摄项目包含以下现成的工作流：

* 产品照片拍摄（商务集成）工作流
* 产品照片拍摄工作流

使用产品照片拍摄（商务集成）工作流可将图像资产与 AEM 中的产品进行映射。此工作流利用商务集成将已批准的图像关联到以下位置的现有产品数据：*/etc/commerce*。

产品照片拍摄（商务集成）工作流包含以下任务:

* 创建拍摄列表
* 上传照片拍摄
* 修饰照片拍摄
* 审核和批准
* “移到生产”任务

如果 AEM 中没有产品信息，请使用产品照片拍摄工作流，根据您通过 CSV 文件上传的产品详细信息，将图像资产与产品进行映射。CSV 文件必须包含基本的产品信息，例如产品 ID、类别和描述。此工作流会获取产品的已批准资产。

此工作流包含以下任务：

* 上传拍摄列表
* 上传照片拍摄
* 修饰照片拍摄
* 审核和批准
* “移到生产”任务

您可以使用工作流配置选项来自定义此工作流。

两个工作流都包含将产品与其已批准的资产进行关联的步骤。每个工作流均包含以下步骤：

* 工作流配置：介绍用于自定义工作流的选项
* 启动项目工作流：说明如何启动产品照片拍摄
* 工作流任务详细信息：提供工作流中可用任务的详细信息

## 跟踪项目进度 {#tracking-project-progress}

您可以通过监测项目中的活动/已完成任务来跟踪项目进度。

可使用以下工具来监测项目进度：

* **任务卡**

* **任务列表**

任务卡描绘了项目的整体进度。 仅当项目具有任何相关任务时，任务卡才会在项目详细信息页面中显示。任务卡会根据已完成任务的数量来显示项目的当前完成状态。任务卡不包含以后的任务。

任务卡提供了以下详细信息：

* 活动任务的百分比
* 已完成任务的百分比

![chlimage_1-136](assets/chlimage_1-136a.png)

任务列表提供了项目中当前处于活动状态的工作流任务的详细信息。要显示该列表，请点按/单击任务卡。任务列表还显示了元数据，例如开始日期、到期日期、被分派人、优先级和任务的状态。

![chlimage_1-137](assets/chlimage_1-137a.png)

## 工作流配置 {#workflow-configuration}

此任务涉及根据用户的角色为用户分配工作流步骤。

要配置&#x200B;**产品照片拍摄**&#x200B;工作流，请执行以下操作：

1. Navigate to **Tools** > **Workflows**, and then tap the **Models** tile to open the **Workflow Models** page.
1. Select the **Product Photo Shoot** workflow, and the tap the **Edit** icon from the toolbar to open it in edit mode.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

1. In the **Product Photo Shoot Workflow** page, open a project task. 例如，打开&#x200B;**上传拍摄列表**&#x200B;任务。

   ![chlimage_1-139](assets/chlimage_1-139a.png)

1. 单击&#x200B;**任务**&#x200B;选项卡，以配置以下各项：

   * 任务的名称
   * 接收任务的默认用户（角色）
   * 任务的默认优先级（在用户的任务列表中显示）
   * 任务描述（在被分派人打开任务时显示）
   * 任务到期日期（根据任务的开始时间计算）

1. 单击&#x200B;**确定**，以保存配置设置。

   同样，您也可以为&#x200B;**产品照片拍摄**&#x200B;工作流配置以下任务：

   * 上传照片拍摄
   * 修饰照片拍摄
   * 照片拍摄审核
   * 移到生产

   Perform a similar procedure to configure the tasks in the **Product Photo Shoot (Commerce Integration) workflow**.

此部分介绍如何将产品信息管理与创意项目进行集成。

## 启动项目工作流 {#starting-a-project-workflow}

1. Navigate to a Product Photo Shoot project, and tap/click the **Add Work** icon on the **Workflows** card.
1. 选择&#x200B;**产品照片拍摄（商务集成）**&#x200B;工作流卡片，以启动产品照片拍摄（商务集成）工作流。If the product information isn&#39;t available under /etc/commerce, select the **Product Photo Shoot** workflow and start the Product Photo Shoot workflow.

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. 点按/单击&#x200B;**下一步**，以在项目中启动该工作流。
1. 在下一个页面上输入工作流详细信息。

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   单击&#x200B;**提交**，以启动照片拍摄工作流。随即会显示照片拍摄项目的项目详细信息页面。

   ![chlimage_1-142](assets/chlimage_1-142a.png)

### 工作流任务详细信息 {#workflow-tasks-details}

照片拍摄工作流包含若干任务。每项任务会根据为该任务定义的配置分配到相应的用户组。

#### 创建拍摄列表任务 {#create-shot-list-task}

**创建拍摄列表**&#x200B;任务允许项目所有者选择需要图像的产品。系统会根据用户选择的选项，生成包含基本产品信息的 CSV 文件。

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the task item in the workflow.

   ![chlimage_1-143](assets/chlimage_1-143a.png)

1. Select the **Create Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. 查看任务详细信息，然后点按/单击&#x200B;**创建拍摄列表**&#x200B;按钮。

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. 选择存在产品数据但没有关联图像的产品。

   ![chlimage_1-146](assets/chlimage_1-146a.png)

1. Tap/click the **Add To Shotlist** icon to create a CSV file that contains a list of all such products. 此时会显示一条消息，确认已为选定的产品创建拍摄列表。单击&#x200B;**关闭**&#x200B;以完成此工作流。
1. 创建拍摄列表后，会显示&#x200B;**查看拍摄列表**&#x200B;链接。To add more products to the shot list, tap/click **Add to Shot List**. 在这种情况下，数据会附加到最初创建的拍摄列表。

   ![chlimage_1-147](assets/chlimage_1-147a.png)

1. 点按/单击&#x200B;**查看拍摄列表**，以查看新的拍摄列表。

   ![chlimage_1-148](assets/chlimage_1-148a.png)

   要编辑现有数据或添加新数据，请从工具栏中点按/单击&#x200B;**编辑**。Only the **Product **and **Description** fields are editable.

   ![chlimage_1-149](assets/chlimage_1-149a.png)

   After you update the file, tap/click **Save** on toolbar to save the file.

1. After adding the products, tap/click the **Complete** icon on the **Create Shot List **task details page to mark the task as completed. 您可以添加可选注释。

   任务完成后，项目中会发生以下更改：

   * 在与工作流标题同名的文件夹中创建与产品层次结构对应的资产。
   * 可使用“资产”控制台来编辑资产的元数据，即使摄影师还未提供图像。
   * 创建一个照片拍摄文件夹，用于存储摄影师提供的图像。该照片拍摄文件夹中包含一些子文件夹，分别对应拍摄列表中的各个产品条目。

   在产品照片拍摄（无商务集成）工作流中，上传拍摄列表是首要任务。点按/单击&#x200B;**上传拍摄列表**&#x200B;可上传 **shotlist.csv** 文件。该 CSV 文件应包含产品 ID。其他字段为选填字段。您可以使用这些信息将资产映射到产品。

### “上传拍摄列表”任务 {#upload-shot-list-task}

这是产品照片拍摄工作流中的一个任务。如果 AEM 中没有可用的产品信息，则需要执行此任务。在这种情况下，您需要通过 CSV 文件上传需要图像资产的产品列表。根据CSV文件中的详细信息，您可以将图像资产与产品进行映射。

使用上述操作过程中项目卡片下的&#x200B;**查看拍摄列表**&#x200B;链接，可下载 CSV 示例文件。查看示例文件，可了解 CSV 文件中的常见内容。

产品列表或 CSV 文件可能包含多个字段，例如&#x200B;**类别、产品、ID、描述**&#x200B;和&#x200B;**路径**。**ID** 字段为必填字段，其中包含产品 ID。其他字段为选填字段。

产品可能属于某个特定类别。CSV 文件中的&#x200B;**类别**&#x200B;列下方可能会列出产品类别。**产品**&#x200B;字段包含产品名称。在&#x200B;**描述**&#x200B;字段中，可输入产品描述或说明，以供摄影师参考。

>[!NOTE]
>
>The name of images to be uploaded should start with &quot;**&lt;ProductId>_&quot;** where Product ID is referenced from the **Id** field in the *shotlist.csv* file. For example, for a product in the shot list with **Id 397122**, you can upload files with names **397122_highcontrast.jpg**, **397122_lowlight.png**, and so on.

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the list of tasks in the workflow.
1. Select the **Upload Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-150](assets/chlimage_1-150a.png)

1. Review the task details and then tap/click the **Upload Shot List** button.

   ![chlimage_1-151](assets/chlimage_1-151a.png)

1. Tap/click the **Upload Shot List** button to upload the CSV file with filename shotlist.csv. 工作流会将此文件识别为用于为下一任务提取产品数据的源文件。
1. 以正确的格式上传包含产品信息的 CSV 文件。The **View Uploaded Assets** link appears under the card after the CSV file is uploaded.

   ![chlimage_1-152](assets/chlimage_1-152a.png)

   Click the **Complete** icon to complete the task.

1. Tap/click the **Complete** icon to complete the task.

### “上传照片拍摄”任务{#upload-photo-shoot-task}

If you are an Editor, you can upload shots for the products listed in the **shotlist.csv** file that is created or uploaded in the previous task.

The name of images to be uploaded should begin with **&quot;&lt;productId>_&quot;** where Product ID is referenced from the **Id** field in the **shotlist.csv** file. 例如，对于拍摄列表中 **ID 为 397122** 的产品，您可以上传具有以下名称的文件：**397122_highcontrast.jpg**、**397122_lowlight.png**，等等。

您可以直接上传图像，也可以上传包含图像的 ZIP 文件。系统会根据图像的名称，将图像放置到&#x200B;**照片拍摄**&#x200B;文件夹中的相应产品文件夹内。

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Upload Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-153](assets/chlimage_1-153a.png)

1. Tap/click **Upload Photo Shoot** and upload the photo shoot images.
1. 点按/单击工具栏中的&#x200B;**完成**&#x200B;图标以完成任务。

### “修饰照片拍摄”任务 {#retouch-photo-shoot-task}

如果您拥有编辑权限，则可以执行“修饰照片拍摄”任务，以对上传到“照片拍摄”文件夹的图像进行编辑。

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Retouch Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-154](assets/chlimage_1-154a.png)

1. Tap/click the **View Uploaded Assets** link in the **Retouch Photo Shoot** page to browse the uploaded images.

   ![chlimage_1-155](assets/chlimage_1-155a.png)

   如有必要，可使用 Adobe Creative Cloud 应用程序来编辑图像。

   ![chlimage_1-156](assets/chlimage_1-156a.png)

1. 点按/单击工具栏中的&#x200B;**完成**&#x200B;图标以完成任务。

### “审核和批准”任务{#review-and-approve-task}

在此任务中，您需要审核摄影师上传的照片拍摄图像，并将图像标记为已批准使用。

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Review &amp; Approve** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-157](assets/chlimage_1-157a.png)

1. In the **Review &amp; Approve** page, assign the review task to role, for example Reviewers, and then tap/click **Review **to start reviewing the uploaded product images.

   ![chlimage_1-158](assets/chlimage_1-158a.png)

1. 选择产品图像，然后点按/单击工具栏中的“批准”图标，以将图像标记为已批准。

   ![chlimage_1-159](assets/chlimage_1-159a.png)

   批准图像后，图像上方会显示指示已批准的横幅。

   >[!NOTE]
   您可能会遗漏一些产品，而没有为其批准任何图像。稍后，您可以重新访问此任务，并在完成操作后将其标记为完成。

1. 点按/单击&#x200B;**完成**。已批准的图像会与之前创建的空资产进行关联。

您可以使用资产 UI 导航到项目资产，并验证已批准的图像。

点按/单击下一个级别，可按照产品数据的层次结构来查看产品。

创意项目会将已批准的资产与引用的产品进行关联。资产元数据会使用 AEM 资产元数据部分资产属性下的&#x200B;**产品数据**&#x200B;选项卡中的产品引用和基本信息进行更新。

>[!NOTE]
在产品照片拍摄工作流（无商务集成）中，已批准的图像与产品之间没有任何关联。

### “移到生产”任务 {#move-to-production-task}

此任务是将已批准的资产移到生产就绪文件夹，以使其变为可用。

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Move to Production** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-160](assets/chlimage_1-160a.png)

1. 要在将照片拍摄的已批准资产移到生产就绪文件夹之前查看这些资产，请在&#x200B;**移到生产**&#x200B;任务页面上单击项目缩略图下方的&#x200B;**查看已批准的资产**&#x200B;链接。

   ![chlimage_1-161](assets/chlimage_1-161a.png)

1. Enter the path of the production-ready folder in the **Move To** field.

   ![chlimage_1-162](assets/chlimage_1-162a.png)

   Tap/click **Move to Production**. 关闭确认消息。资产随即会移到指定的路径，并且系统会根据文件夹层次结构自动为每个产品的已批准资产创建旋转集。

1. 点按/单击工具栏中的&#x200B;**完成**&#x200B;图标。最后一个步骤标记为完成后，工作流即已完成。

## 查看 DAM 资产元数据 {#viewing-dam-asset-metadata}

批准资产后，资产会关联到相应的产品。现在，已批准资产的[“属性”页面](/help/assets/manage-assets.md#editing-properties)包含额外的&#x200B;**产品数据**（关联的产品信息）选项卡。此选项卡显示了产品详细信息、SKU 编号以及与资产关联的其他产品相关详细信息。点按/单击&#x200B;**编辑**&#x200B;图标，可更新资产属性。产品相关信息保持为只读状态。

点按/单击出现的链接，可导航到与资产关联的产品控制台中的相应产品详细信息页面。

## 自定义项目照片拍摄工作流 {#customizing-the-project-photo-shoot-workflows}

您可以根据需要自定义项目照片拍摄工作流。这是一项基于角色的可选任务，执行此任务可设置项目中的变量值。随后，您可以使用配置的值来做出决策。

1. Click/tap the AEM logo, and then navigate to **Tools** > **Workflow** > **Models** to open the Workflow Models page.
1. 选择&#x200B;**产品照片拍摄（商务集成）**&#x200B;工作流或&#x200B;**产品照片拍摄**&#x200B;工作流，然后单击/点按工具栏中的&#x200B;**编辑**，以在编辑模式下打开工作流。
1. 在 Sidekick 中打开&#x200B;**项目**&#x200B;任务，然后将&#x200B;**创建基于角色的项目任务**&#x200B;步骤拖动到工作流。

   ![chlimage_1-163](assets/chlimage_1-163a.png)

1. Open the **Role Based Task** step.
1. 在&#x200B;**任务**&#x200B;选项卡中，提供任务的名称，此名称将显示在&#x200B;**任务**&#x200B;列表中。您还可以将任务分配给角色、设置默认优先级、提供说明并指定任务到期的时间。

   ![chlimage_1-164](assets/chlimage_1-164a.png)

1. 在&#x200B;**路由**&#x200B;选项卡中，为任务指定操作。要添加多个操作，请点按／单击**添加项目**链接。

   ![chlimage_1-165](assets/chlimage_1-165a.png)

1. After adding the options click **OK** to add the changes to the step.

   >[!NOTE]
   Tapping/clicking **OK** does not save the changes in the workflow. To save changes in the workflow, tap/click **Save**.

1. Open the **Workflow** tasks from side kick, and add a **Goto** task.
1. 打开&#x200B;**跳转**&#x200B;任务，然后点按/单击&#x200B;**过程**&#x200B;选项卡。
1. 在&#x200B;**脚本**&#x200B;框中指定以下代码：

```
   function check() {

   if (workflowData.getMetaDataMap().get("lastTaskAction","") == "Reject All") {

   return true

   }

   // set copywriter user in metadata

   var previousId = workflowData.getMetaDataMap().get("lastTaskCompletedBy", "");

   workflowData.getMetaDataMap().put("copywriter", previousId);

   return false;

   }
```

>[!NOTE]
For details around scripting in workflow steps, see [Defining a Rule for an OR Split](/help/sites-developing/workflows-models.md).

![chlimage_1-166](assets/chlimage_1-166a.png)

1. Tap/click **OK**.

1. Tap/click **Save** to save the workflow.

   ![chlimage_1-167](assets/chlimage_1-167a.png)

1. A new Project owner acceptance task now comes up after the [Move to Production task](#move-to-production-task) is completed and is assigned to the owner.

   所有者角色中的用户可以完成此任务，并从注释弹出框的列表中（从在工作流步骤配置中添加的操作列表中）选择一个操作。

   ![chlimage_1-168](assets/chlimage_1-168a.png)

   选择相应的选项，然后单击&#x200B;**完成**&#x200B;以在工作流中运行&#x200B;**跳转步骤**。

>[!NOTE]
When you start a server, the Project task list servlet caches the mappings between task types and URLs defined under `/libs/cq/core/content/projects/tasktypes`. You can then perform the usual overlay and add custom task types by placing them under `/apps/cq/core/content/projects/tasktypes`.

