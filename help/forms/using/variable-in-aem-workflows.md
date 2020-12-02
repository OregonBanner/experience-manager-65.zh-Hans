---
title: AEM Forms工作流变量
seo-title: AEM Forms工作流变量
description: 创建变量，为变量设置值，并在AEM Forms工作流步骤中使用它。
seo-description: 创建变量，为变量设置值，并在AEM Forms工作流步骤中使用它。
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
translation-type: tm+mt
source-git-commit: 252dac988c8256cf99ee8487feb937d5345ed797
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 1%

---


# AEM Forms工作流中的变量{#variables-in-aem-forms-workflows}

工作流模型中的变量是根据其数据类型存储值的一种方法。 然后，您可以在任何工作流步骤中使用变量的名称来检索存储在变量中的值。 您还可以使用变量名称定义表达式，以便进行路由决策。

在AEM工作流模型中，您可以：

* [根据](../../forms/using/variable-in-aem-workflows.md#create-a-variable) 要存储在数据类型中的信息类型创建数据类型的变量。
* [使用设置变量工](../../forms/using/variable-in-aem-workflows.md#set-a-variable) 作流步骤设置变量值。
* [在所有AEM Forms](../../forms/using/variable-in-aem-workflows.md#use-a-variable) 工作流步骤中使用变量来检索存储的值，在“或”拆分和跳转步骤中使用变量来定义路由表达式。

以下视频演示了如何在AEM工作流模型中创建、设置和使用变量：

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

变量是现有[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)接口的扩展。 可以在ECMAScript中使用[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)访问使用变量保存的元数据。

## 创建变量{#create-a-variable}

可使用工作流模型Sidekick中的“变量”部分创建变量。 AEM工作流变量支持以下数据类型：

* **基本数据类型**:长、多次、布尔、日期和字符串
* **复杂数据类型**: [文档](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html) [、](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html)XML [、](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)JSON和表单数据模型实例。

>[!NOTE]
>
>工作流仅支持ISO8601格式的日期类型变量。

您需要[AEM Forms加载项包](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)来文档和表单数据模型数据类型。  使用ArrayList数据类型创建变量集合。 可以为所有简单和复杂的数据类型创建ArrayList变量。 例如，创建一个ArrayList变量，并选择String作为子类型，以使用该变量存储多个字符串值。

执行以下步骤以创建变量：

1. 在AEM实例上，导航到工具![](/help/forms/using/assets/hammer.png) >工作流>模型。
1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;并指定工作流模型的标题和可选名称。 选择模型，然后点按&#x200B;**[!UICONTROL 编辑]**。
1. 点按工作流模型的Sidekick中可用的变量图标，然后点按&#x200B;**[!UICONTROL 添加变量]**。

   ![添加变量](assets/variables_add_variable_new.png)

1. 在添加变量对话框中，指定名称并选择变量类型。
1. 从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择数据类型并指定以下值：

   * 基本数据类型——为变量指定可选默认值。
   * JSON或XML —— 指定可选的JSON或XML模式路径。 在将此模式中可用的属性映射和存储到另一个变量时，系统验证模式路径。
   * 表单数据模型——指定表单数据模型路径。
   * ArrayList —— 指定集合的子类型。

1. 指定变量的可选描述，然后点按![done_icon](assets/done_icon.png)以保存更改。 变量将显示在左窗格的可用列表中。

在创建变量时，请考虑以下实践：

* 创建工作流所需的任意数量的变量。 但是，为了节省数据库资源，请尽可能使用所需的最少变量数，并重用变量。
* 变量区分大小写。 确保在工作流中使用相同的大小写引用变量。
* 避免在变量名称中使用特殊字符

## 设置变量{#set-a-variable}

您可以使用设置变量步骤来设置变量的值并定义值的设置顺序。 变量的设置顺序是变量映射在设置变量步骤中的列出顺序。

对变量值所做的更改只影响发生更改的进程的实例。 例如，当启动工作流并更改变量数据时，更改仅影响该工作流的实例。 这些更改不会影响以前启动或随后启动的工作流的其他实例。

根据变量的数据类型，您可以使用以下选项设置变量的值：

* **文本：** 当您知道要指定的确切值时，请使用此选项。

* **表达式:** 当根据表达式计算要使用的值时，请使用此选项。表达式是在提供的表达式编辑器中创建的。

* **JSON点表示法：** 使用此选项从JSON或FDM类型变量检索值。
* **XPATH:** 使用该选项从XML类型变量检索值。

* **相对于有效负** 荷：当要保存到变量的值在相对于有效负荷的路径上可用时，请使用此选项。

* **绝对路径：** 当要保存到变量的值在绝对路径上可用时，请使用此选项。

您还可以使用JSON DOT表示法或XPATH表示法更新JSON或XML类型变量的特定元素。

### 添加变量{#add-mapping-between-variables}之间的映射

执行以下步骤以添加变量之间的映射：

1. 在工作流编辑页面上，点按工作流模型Sidekick中可用的步骤图标。
1. 将&#x200B;**设置变量**&#x200B;步骤拖放到工作流编辑器中，点按该步骤并选择![configure_icon](assets/configure_icon.png)（配置）。
1. 在“设置变量”对话框中，选择“映射”**[!UICONTROL “映射”]**>“添加映射”]**。**[!UICONTROL 
1. 在&#x200B;**映射变量**&#x200B;部分，选择要存储数据的变量，选择映射模式，并指定要存储在变量中的值。 映射模式因变量类型而异。
1. 映射更多变量，实现有意义的表达式。 点按![done_icon](assets/done_icon.png)以保存更改。

### 示例1:查询XML变量，为字符串变量{#example-query-an-xml-variable-to-set-value-for-a-string-variable}设置值

选择XML类型的变量以存储XML文件。 查询XML变量，为XML文件中可用的属性设置字符串变量的值。 使用&#x200B;**为XML变量**&#x200B;字段指定XPATH，以定义要存储在字符串变量中的属性。

在此示例中，选择&#x200B;**formdata** XML变量以存储&#x200B;**cc-app.xml**&#x200B;文件。 查询&#x200B;**formdata**&#x200B;变量以设置&#x200B;**emailaddress**&#x200B;字符串变量的值，以存储&#x200B;**cc-app.xml**&#x200B;文件中可用的&#x200B;**emailAddress**&#x200B;属性的值。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "设置变量值")

### 示例2:使用表达式存储基于其他变量{#example2}的值

使用表达式计算变量的和并将结果存储在变量中。

在此示例中，使用表达式编辑器定义一个表达式来计算&#x200B;**assetscost**&#x200B;和&#x200B;**balanceamount**&#x200B;变量的和，并将结果存储在&#x200B;**totalvalue**&#x200B;变量中。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用表达式编辑器{#use-expression-editor}

您还使用表达式计算运行时变量的值。 变量提供表达式编辑器来定义表达式。

使用表达式编辑器可以：

* 使用其他工作流变量、数字或数学表达式设置变量值。
* 在数学表达式中使用工作流变量、字符串、数字或表达式
* 添加条件以设置变量值。
* 在条件之间添加运算符。

![表达式编辑器](assets/variables_expression_editor_new.png)

它基于具有以下更改的自适应表单规则编辑器。 变量中的规则编辑器：

* 不支持功能。
* 不提供视图规则摘要的UI
* 没有代码编辑器。
* 不支持启用和禁用对象的值。
* 不支持对象的设置属性。
* 不支持调用Web服务。

有关详细信息，请参阅[自适应表单规则编辑器](../../forms/using/rule-editor.md)。

## 使用变量{#use-a-variable}

您可以使用变量来检索输入和输出或保存步骤的结果。 工作流编辑器提供两种类型的工作流步骤：

* 支持变量的工作流步骤
* 不支持变量的工作流步骤

### 支持变量{#workflow-steps-with-support-for-variables}的工作流步骤

“转至”步骤、“或拆分”步骤和所有AEM Forms工作流步骤都支持变量。

#### OR拆分步骤{#or-split-step}

“或拆分”(OR Split)在工作流中创建拆分，之后只有一个分支处于活动状态。 此步骤允许您将条件处理路径引入工作流。 您可以根据需要向每个分支添加工作流步骤。

您可以使用规则定义、ECMA脚本或外部脚本为分支定义路由表达式。

您可以使用变量来定义路由表达式，使用表达式编辑器。 有关对“或拆分”步骤使用路由表达式的详细信息，请参阅[“或拆分”步骤](/help/sites-developing/workflows-step-ref.md#or-split)。

在此示例中，在定义路由表达式之前，请使用[示例2](../../forms/using/variable-in-aem-workflows.md#example2)设置&#x200B;**totalvalue**&#x200B;变量的值。 如果&#x200B;**totalvalue**&#x200B;变量的值大于50000，则分支1处于活动状态。 同样，如果&#x200B;**totalvalue**&#x200B;变量的值小于50000，则可以定义使分支2处于活动状态的规则。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同样，选择外部脚本路径或为路由表达式指定ECMA脚本以评估活动分支。 点按&#x200B;**[!UICONTROL 重命名分支]**&#x200B;以指定分支的替代名称。

有关更多示例，请参阅[创建工作流模型](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)。

#### 转到步骤{#go-to-step}

**跳转步骤**&#x200B;允许您根据路由表达式的结果指定要执行的工作流模型中的下一步。

与“或拆分”步骤类似，您可以使用规则定义、ECMA脚本或外部脚本为“跳转”步骤定义路由表达式。

您可以使用变量来定义路由表达式，使用表达式编辑器。 有关对Goto步骤使用路由表达式的详细信息，请参阅[Goto步骤](/help/sites-developing/workflows-step-ref.md#goto-step)。

![跳转规则](assets/variables_goto_rule1_new.png)

在此示例中，如果&#x200B;**actiontaked**&#x200B;变量的值等于&#x200B;**需要更多信息**，则跳转步骤将指定审核信用卡应用程序作为下一步。

有关在跳转步骤中使用规则定义的更多示例，请参阅[模拟For循环](/help/sites-developing/workflows-step-ref.md#simulateforloop)。

#### Forms以工作流为中心的工作流步骤{#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流程步骤都支持变量。 有关详细信息，请参阅OSGi](../../forms/using/aem-forms-workflow-step-reference.md)上以Forms为中心的工作流。[

### 不支持变量{#workflow-steps-without-support-for-variables}的工作流步骤

您可以使用[ MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)接口访问工作流步骤中不支持变量的变量。

#### 检索变量值{#retrieve-the-variable-value}

在ECMA脚本中使用以下API，根据数据类型检索现有变量的值：

| 可变数据类型 | API |
|---|---|
| 基元(长、多次、布尔、日期和字符串) | workItem.getWorkflowData()。getMetaDataMap()。get(variableName, type) |
| 文档 | Packages.com.adobe.aemfd.docmanager.文档doc = workItem.getWorkflowData()。getMetaDataMap()。get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.文档.class); |
| XML | Packages.org.w3c.dom.文档xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.org.w3c.dom.文档.class); |
| 表单数据模型 | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.com.google.gson.JsonObject.class); |

对于文档和表单数据模型变量数据类型，您需要[AEM Forms加载项包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

**示例**

使用以下API检索字符串数据类型的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新变量值{#update-the-variable-value}

在ECMA脚本中使用以下API更新变量的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**示例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

将&#x200B;**salary**&#x200B;变量的值更新为50000。

### 设置变量以调用工作流{#apiinvokeworkflow}

您可以使用API设置变量并传递它们以调用工作流实例。

[workflowSession.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) startWorkflow使用模型、wfData和metaData作为参数。使用MetaDataMap为变量设置值。

在此API中，使用metaData.put(variableName, value)将&#x200B;**variableName**&#x200B;变量设置为&#x200B;**value**;

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**示例**

将&#x200B;**doc**&#x200B;文档对象初始化为路径(“a/b/c”)，并将&#x200B;**docVar**&#x200B;变量的值设置为文档对象中存储的路径。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 编辑变量{#edit-a-variable}

1. 在编辑工作流页面上，点按工作流模型Sidekick中的可用变量图标。 左窗格中的“变量”部分显示所有现有变量。
1. 点按要编辑的变量名称旁边的![edit](assets/edit.png)（编辑）图标。
1. 编辑变量信息，然后点按![done_icon](assets/done_icon.png)以保存更改。 不能编辑变量的&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 类型]**&#x200B;字段。

## 删除变量{#delete-a-variable}

在删除变量之前，请从工作流中删除变量的所有引用。 确保该变量未在工作流中使用。

执行以下步骤以删除变量：

1. 在编辑工作流页面上，点按工作流模型Sidekick中的可用变量图标。 左窗格中的“变量”部分显示所有现有变量。
1. 点按要删除的变量名称旁边的删除图标。
1. 点按![done_icon](assets/done_icon.png)以确认和删除变量。

## 引用 {#references}

有关在AEM Forms工作流步骤中使用变量的更多示例，请参阅AEM工作流](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html)中的[变量。
