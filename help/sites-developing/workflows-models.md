---
title: 创建工作流模型
seo-title: 创建工作流模型
description: 您可以创建工作流模型来定义用户启动工作流时执行的一系列步骤。
seo-description: 您可以创建工作流模型来定义用户启动工作流时执行的一系列步骤。
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 创建工作流模型{#creating-workflow-models}

>[!CAUTION]
>
>有关经典UI的使用，请参阅 [AEM 6.3文档以供参考](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) 。

您可以创建一 [个工作流模型](/help/sites-developing/workflows.md#model) ，以定义用户启动工作流时执行的一系列步骤。 您还可以定义模型属性，如工作流是临时的还是使用多个资源。

用户启动工作流时，会启动一个实例；这是相应的运行时模型，在您同步更 [改时](#sync-your-workflow-generate-a-runtime-model) 创建。

## 创建新工作流 {#creating-a-new-workflow}

首次创建新的工作流模型时，它包含：

* 步骤、流 **动开始****和流结束**。
这些组件表示工作流的开始和结束。 这些步骤是必需的，无法编辑／删除。
* 名为“步 **骤** 1”的参加 **者步骤示例**。
此步骤配置为将工作项分配给工作流启动器。 编辑或删除此步骤，并根据需要添加步骤。

要使用编辑器创建新工作流，请执行以下操作：

1. 打开“工 **作流模型** ”控制台；通过 **工具**、工 **作流**、 **模型** ，或者，例如： [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Select **Create**, then **Create Model**.
1. 此时将 **出现“添加工作流模型** ”(Add Workflow Model)对话框。 在选择完 **成之前** ，输入标题 **和名称** （可选） ****。
1. 新模型将列在“工作流模 **型”控制台中** 。
1. 选择新的工作流，然后使用 [**编辑&#x200B;**，打开它进行配置](#editinganexistingworkflow):   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>如果以编程方式（使用crx包）创建模型，则还可以在以下位置创建子文件夹：
>
>`/var/workflow/models`

>For example, `/var/workflow/models/prototypes`
>然后，该文件夹可用于管 [理对该文件夹中模型的访问](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)。

## 编辑工作流 {#editing-a-workflow}

您可以编辑任何现有的工作流模型以：

* [定义步骤](#addingasteptoamodel-) 及其参 [数](#configuring-a-workflow-step)
* 配置工作流属性 [，包括](#configuring-workflow-stages-that-show-workflow-progress)阶段 [,](#creatingatransientworkflow-) 无论工作流是临时的 [，还是使用多个资源](#configuring-a-workflow-for-multi-resource-support)

编辑 [**默认和／或旧版&#x200B;**（开箱即用）工作流程还有一个额外步骤，以确保在进行更改之前](#editing-a-default-or-legacy-workflow-for-the-first-time)[](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)获得安全副本。

对工作流的更新完成后，必须使用 **Sync****生成运行时模型**。 有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

### 同步工作流——生成运行时模型 {#sync-your-workflow-generate-a-runtime-model}

**Sync** （在编辑器工具栏中）生成一个运 [行时模型](/help/sites-developing/workflows.md#runtime-model)。 运行时模型是用户启动工作流时实际使用的模型。 如果不同步 **更改** ，则更改在运行时将不可用。

当您（或任何其他用户）对工作流进行任何更改时，您必须使用 **Sync** ，以生成运行时模型，即使单个对话框（例如，对于步骤）具有自己的保存选项时也是如此。

当更改与运行时（已保存）模型同步时， **将显示** “同步”。

某些步骤包含必填字段和／或内置验证。 当这些条件不满足时，当您尝试同步模型时，将显示 **错误** 。 例如，当尚未为“参加者”步骤定义任何参 **加者** :

![wf-21](assets/wf-21.png)

### 首次编辑默认或旧版工作流 {#editing-a-default-or-legacy-workflow-for-the-first-time}

打开默认和/ [或旧版模型进行编辑时](/help/sites-developing/workflows.md#workflow-types) :

* 步骤浏览器不可用（左侧）。
* 工具栏( **右侧** )中提供了“编辑”操作。
* 最初，模型及其属性以只读模式显示为：
   * 默认工作流位于 `/libs`
   * 旧版工作流位于选择 `/etc`编辑 **中** :
* 将工作流的副本 `/conf`
* 使步骤浏览器可用
* 使您能够进行更改

>[!NOTE]
有关更 [多信息，请参阅工作流模型的位置](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) 。

![wf-22](assets/wf-22.png)

### 向模型添加步骤 {#adding-a-step-to-a-model}

您需要向模型中添加步骤以表示要执行的活动——每个步骤都执行特定的活动。 标准AEM实例中提供了一系列步骤组件。

编辑模型时，可用步骤显示在“步骤”(Steps)浏览器的各 **组中**。 例如：

![wf-10](assets/wf-10.png)

>[!NOTE]
有关随AEM一起安装的主要步骤组件的信息，请参阅工作 [流步骤参考](/help/sites-developing/workflows-step-ref.md)。

要向工作流模型中添加步骤，请执行以下操作：

1. 打开现有的工作流模型进行编辑。 从“工作 **流模型** ”控制台中，选择所需的模型，然后选择“编 **辑”**。
1. 打开步骤浏览器；使用 **“切换侧面板**”（位于顶部工具栏的最左侧）。 在此对话框中，您可以：

   * **针对特定步骤进行筛选** 。
   * 使用下拉选择器将选择限制为特定步骤组。
   * 选择“显示说明”图 ![标wf-stepinfo-icon](assets/wf-stepinfo-icon.png) ，以显示有关相应步骤的更多详细信息。
   ![wf-02](assets/wf-02.png)

1. 将相应的步骤拖动到模型中的所需位置。

   例如，参加 **者步骤**。

   添加到流后，您可以配 [置该步骤](#configuring-a-workflow-step)。

   ![wf-03](assets/wf-03.png)

1. 根据需要添加任意多个步骤或其他更新。

   在运行时，按步骤在模型中的显示顺序执行步骤。 添加步骤组件后，可以将它们拖动到模型中的其他位置。

   您还可以复制、剪切、粘贴、分组或删除现有步骤；与页面编辑 [器一样。](/help/sites-authoring/editing-content.md)

   还可以使用工具栏选项折叠／展开拆分步骤： ![wf-collapse展开工具栏图标](assets/wf-collapseexpand-toolbar-icon.png)

1. 使用 **Sync** （编辑器工具栏）确认更改以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

### 配置工作流步骤 {#configuring-a-workflow-step}

您可以 **使用** “步骤属性”对话框配置和自定义工作流 **步骤的行为** 。

1. 要打开步骤 **的“步骤属性** ”对话框，请执行以下任一操作：

   * 单击／点按工作流模型中的**步骤，然后从组件 **工具栏中选择** “配置”。

   * 双击该步骤。
   >[!NOTE]
   有关随AEM一起安装的主要步骤组件的信息，请参阅工作 [流步骤参考](/help/sites-developing/workflows-step-ref.md)。

1. 根据需 **要配置步骤** “属性”;可用的属性取决于步骤类型，也可能有多个可用的选项卡。 例如，新工作流中 **的默认参加者步骤**，显示为 `Step 1`:

   ![wf-11](assets/wf-11.png)

1. 用勾号确认更新。
1. 使用 **Sync** （编辑器工具栏）确认更改以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

### 创建临时工作流 {#creating-a-transient-workflow}

在创建新模型时， [或通过编辑现有模型](/help/sites-developing/workflows.md#transient-workflows) ，可以创建“临时”工作流模型：

1. 打开工作流模型进行 [编辑](#editinganexistingworkflow)。
1. 从工 **具栏中选择工作流模型** “属性”。
1. 在对话框中，激活 **临时工作流** （或根据需要取消激活）:

   ![wf-07](assets/wf-07.png)

1. 使用保存并关闭 **确认更改**;后跟 **Sync** （编辑器工具栏）以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

>[!NOTE]
在临时模式下运行工作 [流时](/help/sites-developing/workflows.md#transient-workflows) ,AEM不会存储任何工作流历史记录。 因此， [时间轴](/help/sites-authoring/basic-handling.md#timeline) 不显示与该工作流相关的任何信息。 [](/help/sites-authoring/basic-handling.md#timeline)

## 使工作流模型在触屏UI中可用 {#classic2touchui}

如果在经典UI中存在但在触屏UI的时间线边栏的选择弹出菜单中缺少工作流模型，请按照配置使其可用。 以下步骤说明了如何使用称为“请求激活”和“请 **[!UICONTROL 求取消激活]** ”的AEM **[!UICONTROL 资产工作流模型]**。

1. 确认该型号在触屏优化UI中不可用。 使用路径访问 `/assets.html/content/dam` 资产。 选择资产。 在左 **[!UICONTROL 边栏中]** ，打开时间轴。 单击 **[!UICONTROL 启动工作流]** ，并注意弹出 **[!UICONTROL 列表中不存在Request for Activation]** and **** Request for Acactivation模型。
1. 单击“ **[!UICONTROL 工具”>“常规”>“标记]**”。 选择 **[!UICONTROL 工作流]**。
1. 单击“ **[!UICONTROL 创建”>“创建标记]**”。 将标 **[!UICONTROL 题设置]**`DAM` 为，将名 **[!UICONTROL 称设置为]**`dam`。 单击 **[!UICONTROL 提交]**。

   ![在工作流模型中创建标签](assets/workflow_create_tag.png)

1. 单击“ **[!UICONTROL 工具”(Tools)>“工作流”(Workflow)>“模型”(Models]**)。 选择 **[!UICONTROL 请求激活]** (或请 **[!UICONTROL 求取消激活]**)。 单击&#x200B;**[!UICONTROL 编辑]**。
1. 在Sidekick中，转到“页面 **[!UICONTROL ”选项]** 卡。 Open **[!UICONTROL Page Properties]**.
1. 添加 `Workflow : DAM` 到“ **[!UICONTROL 标记／关键字]** ”字段。 单击&#x200B;**[!UICONTROL 确定]**。单击&#x200B;**[!UICONTROL 保存]**。

   ![编辑模型的页面属性](assets/workflow_model_edit_activation1.png)

### 为多资源支持配置工作流 {#configuring-a-workflow-for-multi-resource-support}

在创建新模型或编辑现有模 [型时](/help/sites-developing/workflows.md#multi-resource-support) ，可以为“多资源支持”配置工作流模型：

1. 打开工作流模型进行 [编辑](#editinganexistingworkflow)。
1. 从工 **具栏中选择工作流模型** “属性”。

1. 在对话框中，激活 **多资源支持** （或根据需要取消激活）:

   ![wf-08](assets/wf-08.png)

1. 使用保存并关闭 **确认更改**;后跟 **Sync** （编辑器工具栏）以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

### 配置工作流阶段（显示工作流进度） {#configuring-workflow-stages-that-show-workflow-progress}

[工作流阶段](/help/sites-developing/workflows.md#workflow-stages) ，有助于在处理任务时可视化工作流的进度。

>[!CAUTION]
如果在页面属性中定义了工作流阶段 ****，但不用于任何工作流步骤，则进度栏将不显示任何进度（无论当前工作流步骤如何）。

可用阶段在工作流模型中定义；可更新现有工作流模型以包含舞台定义。 您可以为工作流模型定义任意数量的阶段。

要为工作流 **定义阶段** ，请执行以下操作：

1. 打开工作流模型进行编辑。
1. 从工 **具栏中选择工作流模型** “属性”。 然后打开“ **阶段** ”选项卡。
1. 添加（并定位）您所需的 **阶段**。 您可以为工作流模型定义任意数量的阶段。

   例如：

   ![wf-08-1](assets/wf-08-1.png)

1. 单击 **保存并关闭** ，以保存属性。
1. 为工作流模型中的每个步骤分配一个舞台。 例如：

   ![wf-09](assets/wf-09.png)

   可以将舞台分配给多个步骤。 例如：

   | **步骤** | **暂存** |
   |---|---|
   | 步骤 1 | 创建 |
   | 步骤 2 | 创建 |
   | 步骤 3 | 审核 |
   | 步骤 4 | 批准 |
   | 步骤 5 | 批准 |
   | 步骤 6 | 完成 |

1. 使用 **Sync** （编辑器工具栏）确认更改以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

## 导出包中的工作流模型 {#exporting-a-workflow-model-in-a-package}

要导出包中的工作流模型，请执行以下操作：

1. 使用包管理器创建新 [包](/help/sites-administering/package-manager.md#package-manager):

   1. 通过工具、部署、包导 **航到包****管****理器**。

   1. 单击“ **创建包”**。
   1. 根据需 **要指定包名称**，以及任何其他详细信息。
   1. 单击&#x200B;**确定**。

1. 单击 **新包工具栏上的** “编辑”。

1. Open the **Filters** tab.

1. 选择 **添加过滤器** ，并指定工作流模型设计的路 *径*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   单击&#x200B;**完成**。

1. 选择 **添加过滤器** ，并指定运行时工作流模 *型的路径* :

   `/var/workflow/models/<*your-model-name*>`

   单击&#x200B;**完成**。

1. 为模型使用的任何自定义脚本添加其他过滤器。
1. 单击 **保存** ，以确认您的过滤器定义。
1. 从包定 **义的工具栏中** ，选择“构建”。
1. 从包工 **具栏中** ，选择“下载”。

## 使用工作流处理表单提交 {#using-workflows-to-process-form-submissions}

您可以配置一个表单，以便由选定的工作流进行处理。 当用户提交表单时，将创建一个新的工作流实例，其中表单提交的数据作为有效负荷。

要配置要与表单一起使用的工作流，请执行以下操作：

1. 创建新页面并打开它进行编辑。
1. Add a **Form** component to the page.
1. **配置** “ **表单开始** ”组件（显示在页面中）。
1. 使用 **启动工作流** ，从以下可用工作流中选择所需的工作流：

   ![wf-12](assets/wf-12.png)

1. 使用勾号确认新表单配置。

## 测试工作流 {#testing-workflows}

在测试工作流以使用各种有效负荷类型时，这是一个好做法；包括不同于其开发的类型。 例如，如果您打算处理资产的工作流，请通过将页面设置为有效负荷来测试它，并确保它不会引发错误。

例如，按如下方式测试新工作流：

1. [从控制台启动您的工作流模型](/help/sites-administering/workflows-starting.md) 。
1. 定义有 **效负荷** ，并确认。

1. 根据需要执行操作，以便继续工作流。
1. 在工作流运行时监视日志文件。

您还可以将AEM配置为在日 **志文件中显示** DEBUG消息。 请参 [阅记录](/help/sites-deploying/configure-logging.md) ，了解详细信息，开发完成后，将“日志级别 **”设置回“信** 息” ****。

## 示例 {#examples}

### 示例：创建一个（简单）工作流以接受或拒绝发布请求 {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

为了说明创建工作流的一些可能性，以下示例创建了工作流的变 `Publish Example` 体。

1. [创建新的工作流模型](#creating-a-new-workflow)。

   新工作流将包含：

   * **流程开始**
   * `Step 1`
   * **流程结束**

1. 删 `Step 1` 除（因为此示例的步骤类型错误）:

   * 单击该步骤，然后从组件工 **具栏中** ，选择删除。 确认该操作。

1. 从步骤浏 **览器的“工作流** ”选择中，将“参与者步骤 **”拖动到工作流上，并将它放在“流开始”和“流结束** ”之 ********&#x200B;间。
1. 要打开属性对话框，请执行以下操作之一：

   * 单击参加者步骤，然后从组件工 **具栏中** 选择配置。
   * 双击参加者步骤。

1. 在“公 **用** ”选项卡 `Validate Content` 中，输入“标 **题** ”和“说 **明”**。
1. 打开“用 **户／组”选项卡** :

   * Activate **Notify user via email**.
   * 为“ `Administrator` 用 `admin`户／组”字 **段选择(** )。
   >[!NOTE]
   对于要发送的电子邮件， [需要配置邮件服务和用户帐户详细信息](/help/sites-administering/notification.md)。

1. 用勾号确认更新。

   您将返回到工作流模型的概述，在此参加者步骤将重命名为 `Validate Content`。

1. 将“或 **拆分** ”拖到工作流上，并将其放在“流结束” `Validate Content` 和“ **流结束”之间**。
1. 打开或 **拆分** ，进行配置。
1. 配置:

   * **常见**:指定拆分名称。
   * **分支1**:选择 **默认路由**。

   * **分支2**:确保 **未选择默认路由** 。

1. 确认对 **OR拆分的更新**。
1. 将“参 **加者步骤** ”拖到左侧分支，打开属性，指定以下值，然后确认更改：

   * **标题**: `Reject Publish Request`

   * **用户／用户组**:例如， `projects-administrators`

   * **通过电子邮件通知用户**:激活后，通过电子邮件通知用户。

1. 将处理 **步骤拖到右侧分支** ，打开属性，指定以下值，然后确认更改：

   * **标题**: `Publish Page as Requested`

   * **流程**:选择 `Activate Page`。 此过程将选定页面发布到发布者实例。

1. 单击 **同步** （编辑器工具栏）以生成运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

   您的新工作流模型将如下：

   ![wf-13](assets/wf-13.png)

1. 将此工作流应用于您的页面，以便当用户移动到“完成 **** 验证内容 **”步骤时，他们可以选择要按请求发布页面** ，还是 ********“发布请求拒绝”。

   ![chlimage_1-72](assets/chlimage_1-72.png)

### 示例：使用ECMA脚本为OR拆分定义规则 {#defineruleecmascript}

**“或者拆分** ”步骤允许您将条件处理路径引入工作流。

要定义OR规则，请按如下步骤继续：

1. 创建两个脚本并将它们保存到存储库中，例如：

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   脚本必须有一个返 [回 `check()`](#function-check) 布尔值的函数。

1. 编辑工作流，并将“ **OR拆分** ”(OR Split)添加到模型。
1. 编辑OR拆分 **的分支** 1的 **属性**:

   * 将“值”(Value)设 **置为** ，将其定义为“默 **认路由** ”(Default Route) `true`。

   * 作 **为规则**，设置脚本的路径。 例如：
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   您可以根据需要切换分支顺序。

1. 编辑OR拆分的 **Branch 2** 的 **属性**。

   * 作为 **规则**，将路径设置为其他脚本。 例如：
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 在每个分支中设置各个步骤的属性。 确保已 **设置用户／组** 。
1. 单击 **同步** （编辑器工具栏），将更改保留到运行时模型。

   有关详细 [信息，请参阅同步您的工作流](#sync-your-workflow-generate-a-runtime-model) 。

#### Function Check() {#function-check}

>[!NOTE]
请参 [阅使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。

如果节点位于 `true` 以下位置，则以下示例脚 `JCR_PATH` 本将返回 `/content/we-retail/us/en`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### 示例：自定义的激活请求 {#example-customized-request-for-activation}

您可以自定义任何现成的工作流。 要进行自定义行为，请叠加相应工作流的详细信息。

例如， **请求激活**。 此工作流用于在 **Sites** 中发布页面，并在内容作者没有相应的复制权限时自动触发。 有关更 [多详细信息，请参阅自定义页面创作——自定义激活请求工作流](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) 。
