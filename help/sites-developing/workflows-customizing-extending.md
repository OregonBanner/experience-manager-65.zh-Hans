---
title: 扩展工作流功能
seo-title: 扩展工作流功能
description: 扩展工作流功能
seo-description: 'null'
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '3587'
ht-degree: 1%

---


# 扩展工作流功能{#extending-workflow-functionality}

本主题介绍如何为工作流开发自定义步骤组件，以及如何与工作流进行有序交互。

创建自定义工作流步骤涉及以下活动:

* 开发工作流步骤组件。
* 将步骤功能作为OSGi服务或ECMA脚本实现。

您还可以[与项目和脚本中的工作流进行交互](/help/sites-developing/workflows-program-interaction.md)。

## 工作流步骤组件 — 基础知识{#workflow-step-components-the-basics}

工作流步骤组件定义创建工作流模型时步骤的外观和行为：

* 工作流Sidekick中的类别和步骤名称。
* 工作流模型中步骤的外观。
* 用于配置组件属性的编辑对话框。
* 在运行时执行的服务或脚本。

与[所有组件](/help/sites-developing/components.md)一样，工作流步骤组件继承自为`sling:resourceSuperType`属性指定的组件。 下图显示了构成所有工作流步骤组件基础的`cq:component`节点的层次结构。 该图还包括&#x200B;**处理步骤**、**参与者步骤**&#x200B;和&#x200B;**动态参与者步骤**&#x200B;组件，因为它们是开发自定义步骤组件的最常见（和基本）起点。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>***必须***&#x200B;不更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，将覆盖`/libs`的内容（当应用修补程序或功能包时，很可能会覆盖）。
>
>对配置和其他更改的建议方法是：
>
>1. 重新创建所需项(即，它存在于`/apps`下的`/libs`中
>2. 在`/apps`中进行任何更改


`/libs/cq/workflow/components/model/step`组件是&#x200B;**流程步骤**、**参与者步骤**&#x200B;和&#x200B;**动态参与者步骤**&#x200B;的最近共同祖先，它们都继承了以下项目：

* `step.jsp`

   `step.jsp`脚本在将步骤组件添加到模型时呈现其标题。

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   包含以下选项卡的对话框：

   * **常见**:。
   * **高级**:用于编辑电子邮件通知属性。

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >当步骤组件的编辑对话框的选项卡与此默认外观不匹配时，该步骤组件已定义了覆盖这些继承选项卡的脚本、节点属性或对话框选项卡。

### ECMA脚本{#ecma-scripts}

ECMA脚本中提供以下对象（取决于步骤类型）：

* [WorkItemwork ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) Item
* [WorkflowSessionworkflow ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) Session
* [WorkflowDataworkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) 
* `args`:数组。

* `sling`:访问其他osgi服务。
* `jcrSession`

### MetaDataMaps {#metadatamaps}

您可以使用工作流元数据来保留工作流生命周期中所需的信息。 工作流步骤的一个常见要求是保留数据以供将来在工作流中使用，或检索保留的数据。

有三种类型的MetaDataMap对象 — 用于`Workflow`、`WorkflowData`和`WorkItem`对象。 它们都有相同的目标 — 存储元数据。

WorkItem有其自己的MetaDataMap，只能在该工作项（例如步骤）运行时使用。

`Workflow`和`WorkflowData`元数据映射均在整个工作流中共享。 对于这些情况，建议仅使用`WorkflowData`元数据映射。

## 创建自定义工作流步骤组件{#creating-custom-workflow-step-components}

工作流步骤组件可以以与任何其他组件](/help/sites-developing/components.md)相同的方式创建。[

要继承某个（现有）基本步骤组件，请向`cq:Component`节点添加以下属性：

* 名称: `sling:resourceSuperType`
* 类型: `String`
* 值：解析为基本组件的以下路径之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步骤实例{#specifying-the-default-title-and-description-for-step-instances}的默认标题和说明

使用以下过程为&#x200B;**Common**&#x200B;选项卡上的&#x200B;**Title**&#x200B;和&#x200B;**Description**&#x200B;字段指定默认值。

>[!NOTE]
>
>当满足以下两个要求时，该字段值将显示在步骤实例中：
>
>* 该步骤的编辑对话框将标题和说明存储在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 位置

>
>  
当编辑对话框使用`/libs/cq/flow/components/step/step`组件实现的“常用”选项卡时，满足此要求。
>
>* 步骤组件或组件的祖代不会覆盖`/libs/cq/flow/components/step/step`组件实现的`step.jsp`脚本。


1. 在`cq:Component`节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   >[!NOTE]
   >
   >有关cq:editConfig节点的详细信息，请参阅[配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在`cq:EditConfig`节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 将以下名称的`String`属性添加到`cq:formParameters`节点：

   * `jcr:title`:该值将填充“公 **** 用”选项卡的“字 **** 幕”字段。
   * `jcr:description`:该值将填充“公 **** 用”(Common)选项卡的“ **** 描述”(Description)字段。

### 在工作流元数据{#saving-property-values-in-workflow-metadata}中保存属性值

>[!NOTE]
>
>请参阅[保持和访问数据](#persisting-and-accessing-data)。 特别是，有关在运行时访问属性值的信息，请参见[在Runtime](#accessing-dialog-property-values-at-runtime)访问对话框属性值。

`cq:Widget`项的name属性指定存储Widget值的JCR节点。 当工作流步骤组件对话框中的构件将值存储在`./metaData`节点下时，该值将添加到工作流`MetaDataMap`。

例如，对话框中的文本字段是具有以下属性的`cq:Widget`节点：

| 名称 | 类型 | 值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

在此文本字段中指定的值将添加到工作流实例的` [MetaDataMap](#metadatamaps)`对象中，并与`subject`键关联。

>[!NOTE]
>
>当密钥为`PROCESS_ARGS`时，该值可通过`args`变量在ECMA脚本实现中随时使用。 在这种情况下，name属性的值为`./metaData/PROCESS_ARGS.`

### 覆盖步骤实现{#overriding-the-step-implementation}

每个基本步骤组件使工作流模型开发人员能够在设计时配置以下主要功能：

* 处理步骤：要在运行时执行的服务或ECMA脚本。
* 参与者步骤：为生成的工作项分配的用户的ID。
* 动态参与者步骤：选择为工作项分配的用户ID的服务或ECMA脚本。

要将组件集中在特定工作流方案中使用，请在设计中配置关键功能，并删除模型开发人员更改它的功能。

1. 在cq:component节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   有关cq:editConfig节点的详细信息，请参阅[配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在cq:EditConfig节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 向`cq:formParameters`节点添加`String`属性。 组件super类型确定属性的名称：

   * 进程步骤: `PROCESS`
   * 参与者步骤: `PARTICIPANT`
   * 动态参与者步骤: `DYNAMIC_PARTICIPANT`

1. 指定属性的值：

   * `PROCESS`:实现步骤行为的服务的ECMA脚本或PID的路径。
   * `PARTICIPANT`:为工作项分配的用户的ID。
   * `DYNAMIC_PARTICIPANT`:ECMA脚本的路径或选择用户分配工作项的服务的PID。

1. 要删除模型开发人员更改属性值的功能，请覆盖组件super类型的对话框。

### 将Forms和对话框添加到参加者步骤{#adding-forms-and-dialogs-to-participant-steps}

自定义您的参与者步骤组件，以提供[表单参与者步骤](/help/sites-developing/workflows-step-ref.md#form-participant-step)和[对话参与者步骤](/help/sites-developing/workflows-step-ref.md#dialog-participant-step)组件中提供的功能：

* 在用户打开生成的工作项时向其演示表单。
* 在用户完成生成的工作项时向用户显示自定义对话框。

对新组件执行以下过程（请参阅[创建自定义工作流步骤组件](#creating-custom-workflow-step-components)）：

1. 在`cq:Component`节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   有关cq:editConfig节点的详细信息，请参阅[配置组件的编辑行为](/help/sites-developing/components-basics.md#edit-behavior)。

1. 在cq:EditConfig节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 要在用户打开工作项时显示表单，请向`cq:formParameters`节点添加以下属性：

   * 名称: `FORM_PATH`
   * 类型: `String`
   * 值：解析到表单的路径

1. 要在用户完成工作项时显示自定义对话框，请向`cq:formParameters`节点添加以下属性

   * 名称: `DIALOG_PATH`
   * 类型: `String`
   * 值：解析到对话框的路径

### 配置工作流步骤运行时行为{#configuring-the-workflow-step-runtime-behavior}

在`cq:Component`节点下，添加`cq:EditConfig`节点。 在下面添加一个`nt:unstructured`节点（必须命名为`cq:formParameters`），并在该节点中添加以下属性：

* 名称: `PROCESS_AUTO_ADVANCE`

   * 类型: `Boolean`
   * 值:

      * 当设置为`true`时，工作流将运行该步骤并继续 — 这是默认值，也建议
      * 当`false`时，工作流将运行并停止；这需要额外处理，因此建议`true`

* 名称: `DO_NOTIFY`

   * 类型: `Boolean`
   * 值：指示是否应针对用户参与步骤发送电子邮件通知（并假定邮件服务器已正确配置）

## 保持和访问数据{#persisting-and-accessing-data}

### 后续工作流步骤{#persisting-data-for-subsequent-workflow-steps}的数据保持

您可以使用工作流元数据来保留工作流生命周期中所需的信息以及步骤之间的信息。 工作流步骤的一个常见要求是保留数据以供将来使用，或从先前步骤中检索保留的数据。

工作流元数据存储在[`MetaDataMap`](#metadatamaps)对象中。 Java API提供[`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)方法以返回提供相应`MetaDataMap`对象的[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html)对象。 此`WorkflowData` `MetaDataMap`对象可用于步骤组件的OSGi服务或ECMA脚本。

#### Java {#java}

将`WorkflowProcess`实现的执行方法传递给`WorkItem`对象。 使用此对象可获得当前工作流实例的`WorkflowData`对象。 下面的示例向工作流`MetaDataMap`对象中添加一个项，然后记录每个项。 (“mykey”、“My Step Value”)项可用于工作流中的后续步骤。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### ECMA 脚本 {#ecma-script}

`graniteWorkItem`变量是当前`WorkItem` Java对象的ECMA脚本表示形式。 因此，您可以使用`graniteWorkItem`变量来获取工作流元数据。 以下ECMA脚本可用于实现&#x200B;**处理步骤**，以向工作流`MetaDataMap`对象添加项，然后记录每个项。 然后，这些项目便可以用于工作流中的后续步骤。

>[!NOTE]
>
>步骤脚本直接可用的`metaData`变量是步骤的元数据。 步骤元数据与工作流元数据不同。

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### 在运行时{#accessing-dialog-property-values-at-runtime}访问对话框属性值

工作流实例的`MetaDataMap`对象对于在整个工作流生命周期中存储和检索数据很有用。 对于工作流步骤组件实现，`MetaDataMap`对于在运行时检索组件属性值尤为有用。

>[!NOTE]
>
>有关配置组件对话框以将属性存储为工作流元数据的信息，请参阅[在工作流元数据中保存属性值](#saving-property-values-in-workflow-metadata)。

工作流`MetaDataMap`可用于Java和ECMA脚本进程实现：

* 在WorkflowProcess接口的Java实现中，`args`参数是工作流的`MetaDataMap`对象。

* 在ECMA脚本实现中，该值可使用`args`和`metadata`变量。

### 示例：检索进程步骤组件{#example-retrieving-the-arguments-of-the-process-step-component}的参数

**处理步骤**&#x200B;组件的编辑对话框包含&#x200B;**参数**&#x200B;属性。 **Arguments**&#x200B;属性的值存储在工作流元数据中，并与`PROCESS_ARGS`键关联。

在下图中，**Arguments**&#x200B;属性的值为`argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java代码是`WorkflowProcess`实现的`execute`方法。 该方法在`args` `MetaDataMap`中记录与`PROCESS_ARGS`键关联的值。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

当执行使用此Java实现的进程步骤时，日志包含以下条目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 脚本 {#ecma-script-1}

以下ECMA脚本用作&#x200B;**进程步骤**&#x200B;的进程。 它记录参数数和参数值：

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>本节介绍如何使用流程步骤的参数。 该信息也适用于动态参加者选择器。

>[!NOTE]
>有关在工作流元数据中存储组件属性的另一个示例，请参阅示例：创建记录器工作流步骤。 此示例包含一个将元数据值与PROCESS_ARGS以外的键关联的对话框。

### 脚本和进程参数{#scripts-and-process-arguments}

在&#x200B;**进程步骤**&#x200B;组件的脚本中，参数可通过`args`对象使用。

创建自定义步骤组件时，对象`metaData`在脚本中可用。 此对象仅限于单个字符串参数。

## 开发进程步骤实现{#developing-process-step-implementations}

当在工作流的过程中启动进程步骤时，这些步骤向OSGi服务发送请求或执行ECMA脚本。 开发执行工作流所需操作的服务或ECMA脚本。

>[!NOTE]
>
>有关将您的进程步骤组件与服务或脚本关联的信息，请参阅[进程步骤](/help/sites-developing/workflows-step-ref.md#process-step)或[覆盖步骤实现](#overriding-the-step-implementation)。

### 使用Java类{#implementing-a-process-step-with-a-java-class}实现进程步骤

要将进程步骤定义为OSGI服务组件（Java包）：

1. 创建捆绑包并将其部署到OSGI容器。 请参阅有关创建包的文档，包含[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)或[Eclipse](/help/sites-developing/howto-projects-eclipse.md)。

   >[!NOTE]
   >
   >OSGI组件需要使用其`execute()`方法实现`WorkflowProcess`接口。 请参阅下面的示例代码。

   >[!NOTE]
   >
   >需要将包名称添加到`maven-bundle-plugin`配置的`<*Private-Package*>`部分。

1. 添加SCR属性`process.label`并根据需要设置值。 这将是使用通用&#x200B;**进程步骤**&#x200B;组件时列出的进程步骤的名称。 请参阅以下示例。
1. 在&#x200B;**模型**&#x200B;编辑器中，使用通用&#x200B;**流程步骤**&#x200B;组件将流程步骤添加到工作流中。
1. 在编辑对话框（位于&#x200B;**处理步骤**）中，转到&#x200B;**处理**&#x200B;选项卡并选择您的进程实现。
1. 如果在代码中使用参数，请设置&#x200B;**进程参数**。 例如：错误。
1. 保存对步骤和工作流模型（模型编辑器的左上角）所做的更改。

Java方法分别将实现可执行Java方法的类注册为OSGI服务，使您能够在运行时随时添加方法。

当有效负荷为页面时，以下OSGI组件会将属性`approved`添加到页面内容节点：

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>如果流程在一行中失败三次，则会将项目放在工作流管理员的收件箱中。

### 使用ECMAScript {#using-ecmascript}

ECMA脚本使脚本开发人员能够实施进程步骤。 脚本位于JCR存储库中，并从中执行。

下表列表了可立即用于处理脚本的变量，提供对工作流Java API对象的访问。

| Java类 | 脚本变量名 | 描述 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 当前步骤实例。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 当前步骤实例的工作流会话。 |
| `String[]` （包含进程参数） | `args` | 步骤参数。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 当前步骤实例的元数据。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供对Sling运行时环境的访问。 |

以下示例脚本演示如何访问表示工作流有效负荷的JCR节点。 `graniteWorkflowSession`变量适用于JCR会话变量，该会话变量用于从有效负荷路径获得节点。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

以下脚本检查有效负荷是否为图像（`.png`文件），从中创建黑白图像，并将其另存为同级节点。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

要使用脚本：

1. 创建脚本(例如，使用CRXDE Lite)并将其保存在`/apps/myapp/workflow/scripts`下的存储库中
1. 要指定在&#x200B;**处理步骤**&#x200B;编辑对话框中标识脚本的标题，请将以下属性添加到脚本的`jcr:content`节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在编辑对话框中显示的名称。 |

1. 编辑&#x200B;**处理步骤**&#x200B;实例并指定要使用的脚本。

## 开发参与者选择器{#developing-participant-choosers}

您可以为&#x200B;**动态参与者步骤**&#x200B;组件开发参与者选择器。

在工作流期间启动&#x200B;**动态参与者步骤**&#x200B;组件时，该步骤需要确定可以将生成的工作项分配到的参与者。 要执行此操作，请执行以下任一步骤：

* 向OSGi服务发送请求
* 执行ECMA脚本以选择参加者

您可以开发服务或ECMA脚本，该脚本根据工作流的要求选择参加者。

>[!NOTE]
>
>有关将&#x200B;**动态参与者步骤**&#x200B;组件与服务或脚本关联的信息，请参阅[动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step)或[覆盖步骤实现](#persisting-and-accessing-data)。

### 使用Java类{#developing-a-participant-chooser-using-a-java-class}开发参与者选择器

要将参与者步骤定义为OSGI服务组件（Java类），请执行以下操作：

1. OSGI组件需要使用其`getParticipant()`方法实现`ParticipantStepChooser`接口。 请参阅下面的示例代码。

   创建捆绑包并将其部署到OSGI容器。

1. 添加SCR属性`chooser.label`并根据需要设置值。 这将是使用&#x200B;**动态参与者步骤**&#x200B;组件列出参与者选择器的名称。 请参阅示例：

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. 在&#x200B;**模型**&#x200B;编辑器中，使用通用&#x200B;**动态参与者步骤**&#x200B;组件将动态参与者步骤添加到工作流。
1. 在编辑对话框中，选择&#x200B;**参加者选择器**&#x200B;选项卡，然后选择选择器实现。
1. 如果在代码中使用参数，请设置&#x200B;**进程参数**。 对于此示例：`/content/we-retail/de`。
1. 保存步骤和工作流模型的更改。

### 使用ECMA脚本{#developing-a-participant-chooser-using-an-ecma-script}开发参加者选择器

您可以创建一个ECMA脚本，该脚本将选择分配了&#x200B;**参与者步骤**&#x200B;生成的工作项的用户。 脚本必须包含一个名为`getParticipant`的函数，该函数不需要参数，并返回一个包含用户或组ID的`String`。

脚本位于JCR存储库中，并从中执行。

下表列表了变量，这些变量提供对脚本中工作流Java对象的即时访问。

| Java类 | 脚本变量名 |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` （包含进程参数） | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. 创建脚本(例如，使用CRXDE Lite)并将其保存在`/apps/myapp/workflow/scripts`下的存储库中
1. 要指定在&#x200B;**处理步骤**&#x200B;编辑对话框中标识脚本的标题，请将以下属性添加到脚本的`jcr:content`节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在编辑对话框中显示的名称。 |

1. 编辑[动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step)实例并指定要使用的脚本。

## 处理工作流包{#handling-workflow-packages}

[工作流](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 包可以传递到工作流进行处理。工作流包包含对页面和资产等资源的引用。

>[!NOTE]
>
>以下工作流流程步骤接受批量页面激活的工作流包：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)

>



您可以开发工作流步骤，以获取包资源并对其进行处理。 `com.day.cq.workflow.collection`包的以下成员提供对工作流包的访问：

* `ResourceCollection`:工作流包类。
* `ResourceCollectionUtil`:用于检索ResourceCollection对象。
* `ResourceCollectionManager`:创建和检索集合。将实现部署为OSGi服务。

下面的Java类示例演示如何获取包资源：

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## 示例：创建自定义步骤{#example-creating-a-custom-step}

开始创建您自己的自定义步骤的简单方法是从以下位置复制现有步骤：

`/libs/cq/workflow/components/model`

### 创建基本步骤{#creating-the-basic-step}

1. 在/apps下重新创建路径；例如：

   `/apps/cq/workflow/components/model`

   新文件夹的类型为`nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >此步骤不适用于经典UI模型编辑器。

1. 然后，将复制的步骤放在/apps文件夹中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是自定义步骤示例的结果：

   ![wf-36](assets/wf-34.png)

   >[!CAUTION]
   >
   >由于在标准UI中，卡上不显示仅标题而非详细信息，因此与经典UI编辑器一样，不需要`details.jsp`。

1. 将以下属性应用于节点：

   `/apps/cq/workflow/components/model/myCustomStep`

   **权益物业：**

   * `sling:resourceSuperType`

      必须继承现有步骤。

      在此示例中，我们继承了位于`cq/workflow/components/model/step`的基本步骤，但您可以使用其他超类型，如`participant`、`process`等。

   * `jcr:title`

      是在步骤浏览器（工作流模型编辑器的左侧面板）中列出组件时显示的标题。

   * `cq:icon`

      用于为步骤指定[珊瑚图标](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html)。

   * `componentGroup`

      必须为以下项之一：

      * 协作工作流
      * DAM 工作流
      * 表单工作流
      * 项目
      * WCM 工作流
      * 工作流

   ![wf-35](assets/wf-35.png)

1. 您现在可以打开工作流模型进行编辑。 在步骤浏览器中，您可以进行筛选，以查看&#x200B;**我的自定义步骤**:

   ![wf-36](assets/wf-36.png)

   将&#x200B;**我的自定义步骤**&#x200B;拖动到模型上会显示卡：

   ![wf-37](assets/wf-37.png)

   如果尚未为该步骤定义`cq:icon`，则使用标题的前两个字母显示默认图标。 例如：

   ![wf-38](assets/wf-38.png)

#### 定义步骤配置对话框{#defining-the-step-configure-dialog}

在[创建基本步骤](#creating-the-basic-step)之后，按如下方式定义步骤&#x200B;**配置**&#x200B;对话框：

1. 在节点`cq:editConfig`上配置以下属性：

   **权益物业：**

   * `cq:inherit`

      设置为`true`时，您的步骤组件将继承您在`sling:resourceSuperType`中指定的步骤的属性。

   * `cq:disableTargeting`

      根据需要设置。
   ![wf-39](assets/wf-39.png)

1. 在节点`cq:formsParameter`上配置以下属性：

   **权益物业：**

   * `jcr:title`

      在模型映射中和&#x200B;**我的自定义 — 步骤属性**&#x200B;配置对话框的&#x200B;**标题**&#x200B;字段中设置步骤卡上的默认标题。

   * 您还可以定义自己的自定义属性。

   ![wf-40](assets/wf-40.png)

1. 在节点`cq:listeners`上配置属性。

   `cq:listener`节点及其属性允许您设置事件处理函数，这些处理函数在触屏优化UI模型编辑器中对事件做出响应；例如，将步骤拖动到模型页面或编辑步骤属性。

   **利息物业：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此配置对于编辑器的正常运行至关重要。 在大多数情况下，此配置不得更改。

   但是，将`cq:inherit`设置为true（在`cq:editConfig`节点上，请参阅上面的内容）允许您继承此配置，无需将其显式包含在步骤定义中。 如果没有继承，则您需要添加此节点，其中包含以下属性和值。

   在此示例中，已激活继承，因此我们可以删除`cq:listeners`节点，并且该步骤仍可正常工作。

   ![wf-41](assets/wf-41.png)

1. 您现在可以将步骤的实例添加到工作流模型。 当您&#x200B;**配置**&#x200B;时，您将看到以下对话框：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此示例{#sample-markup-used-in-this-example}中使用的标记示例

自定义步骤的标记在组件根节点的`.content.xml`中表示。 此示例使用的示例`.content.xml`:

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

此示例中使用的`_cq_editConfig.xml`示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

此示例中使用的`_cq_dialog/.content.xml`示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>注意对话框定义中的公用节点和进程节点。 这些属性继承自我们用作自定义步骤超类型的流程步骤：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>经典UI模型编辑器对话框仍可与标准的触屏优化UI编辑器一起使用。
>
>如果要将经典UI步骤对话框升级到标准UI对话框，则AEM具有[现代化工具](/help/sites-developing/modernization-tools.md)。 转换后，某些情况下仍可对对话框进行手动改进。
>
>* 如果升级的对话框为空，您可以查看`/libs`中的对话框，这些对话框的功能与如何提供解决方案的示例类似。 例如：
   >
   >
* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`

>
>  
您不得修改`/libs`中的任何内容，只需将它们用作示例。 如果要利用任何现有步骤，请将它们复制到`/apps`并在此处修改它们。
