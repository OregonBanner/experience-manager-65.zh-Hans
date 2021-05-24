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
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3587'
ht-degree: 1%

---

# 扩展工作流功能{#extending-workflow-functionality}

本主题介绍如何为工作流开发自定义步骤组件，以及如何以编程方式与工作流交互。

创建自定义工作流步骤涉及以下活动：

* 开发工作流步骤组件。
* 作为OSGi服务或ECMA脚本实施步骤功能。

您还可以通过程序和脚本](/help/sites-developing/workflows-program-interaction.md)与工作流进行交互。[

## 工作流步骤组件 — 基础知识{#workflow-step-components-the-basics}

工作流步骤组件定义创建工作流模型时步骤的外观和行为：

* 工作流Sidekick中的类别和步骤名称。
* 工作流模型中步骤的外观。
* 用于配置组件属性的编辑对话框。
* 运行时执行的服务或脚本。

与[所有组件](/help/sites-developing/components.md)一样，工作流步骤组件继承自为`sling:resourceSuperType`属性指定的组件。 下图显示了构成所有工作流步骤组件基础的`cq:component`节点的层次结构。 该图还包括&#x200B;**流程步骤**、**参与者步骤**&#x200B;和&#x200B;**动态参与者步骤**&#x200B;组件，因为它们是开发自定义步骤组件的最常见（和基本）起点。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>***必须***&#x200B;不更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 在`/apps`下重新创建所需项目（即，它存在于`/libs`中）
>2. 在`/apps`中进行任何更改


`/libs/cq/workflow/components/model/step`组件是&#x200B;**流程步骤**、**参与者步骤**&#x200B;和&#x200B;**动态参与者步骤**&#x200B;的最接近的共同上级，所有这些组件都继承以下项目：

* `step.jsp`

   `step.jsp`脚本在将步骤组件添加到模型时会呈现该组件的标题。

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   具有以下选项卡的对话框：

   * **常见**:，以编辑标题和描述。
   * **高级**:，以编辑电子邮件通知属性。

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >当步骤组件的编辑对话框的选项卡与此默认外观不匹配时，步骤组件会定义覆盖这些继承选项卡的脚本、节点属性或对话框选项卡。

### ECMA脚本{#ecma-scripts}

ECMA脚本中提供了以下对象（取决于步骤类型）：

* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) WorkItemworkItem
* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) WorkflowSessionworkflowSession
* [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) WorkflowDataworkflowData
* `args`:数组。

* `sling`:以访问其他osgi服务。
* `jcrSession`

### MetaDataMaps {#metadatamaps}

您可以使用工作流元数据保留在工作流生命周期内所需的信息。 工作流步骤的常见要求是保留数据以供将来在工作流中使用，或检索保留的数据。

有三种类型的MetaDataMap对象 — 用于`Workflow`、`WorkflowData`和`WorkItem`对象。 它们具有相同的预期用途 — 存储元数据。

WorkItem具有其自己的MetaDataMap，该MetaDataMap只能在该工作项（例如步骤）运行时使用。

`Workflow`和`WorkflowData`元数据映射在整个工作流中共享。 对于这些情况，建议仅使用`WorkflowData`元数据映射。

## 创建自定义工作流步骤组件{#creating-custom-workflow-step-components}

工作流步骤组件可以以与任何其他组件](/help/sites-developing/components.md)相同的方式创建。[

要从其中一个（现有）基本步骤组件继承，请将以下属性添加到`cq:Component`节点：

* 名称: `sling:resourceSuperType`
* 类型: `String`
* 值：解析为基本组件的以下路径之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步骤实例{#specifying-the-default-title-and-description-for-step-instances}的默认标题和描述

使用以下过程为&#x200B;**Common**&#x200B;选项卡上的&#x200B;**Title**&#x200B;和&#x200B;**Description**&#x200B;字段指定默认值。

>[!NOTE]
>
>当满足以下两个要求时，该字段值将显示在步骤实例中：
>
>* 该步骤的编辑对话框将标题和描述存储在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 位置

>
>  
当编辑对话框使用`/libs/cq/flow/components/step/step`组件实施的“常用”选项卡时，即满足此要求。
>
>* 组件的步骤组件或上级组件不会覆盖`/libs/cq/flow/components/step/step`组件实施的`step.jsp`脚本。


1. 在`cq:Component`节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   >[!NOTE]
   >
   >有关cq:editConfig节点的更多信息，请参阅[配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在`cq:EditConfig`节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 将以下名称的`String`属性添加到`cq:formParameters`节点：

   * `jcr:title`:该值将填充“公 **** 用”选项卡的“标 **** 题”字段。
   * `jcr:description`:该值将填充“ **** 常用”选项卡的“描 **** 述”字段。

### 在工作流元数据{#saving-property-values-in-workflow-metadata}中保存属性值

>[!NOTE]
>
>请参阅[保留并访问数据](#persisting-and-accessing-data)。 特别是，有关在运行时访问属性值的信息，请参阅[在运行时访问对话框属性值](#accessing-dialog-property-values-at-runtime)。

`cq:Widget`项的name属性指定用于存储小组件值的JCR节点。 当工作流步骤组件对话框中的小组件在`./metaData`节点下存储值时，该值会添加到工作流`MetaDataMap`中。

例如，对话框中的文本字段是`cq:Widget`节点，其属性如下：

| 名称 | 类型 | 值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

此文本字段中指定的值将添加到工作流实例的` [MetaDataMap](#metadatamaps)`对象中，并与`subject`键相关联。

>[!NOTE]
>
>当键为`PROCESS_ARGS`时，该值可在ECMA脚本实施中通过`args`变量随时使用。 在这种情况下，name属性的值为`./metaData/PROCESS_ARGS.`

### 覆盖步骤实施{#overriding-the-step-implementation}

每个基本步骤组件都允许工作流模型开发人员在设计时配置以下主要功能：

* 流程步骤：要在运行时执行的服务或ECMA脚本。
* 参与者步骤：为生成的工作项分配的用户ID。
* 动态参与者步骤：用于选择为工作项分配的用户ID的服务或ECMA脚本。

要将组件集中在特定工作流场景中使用，请在设计中配置关键功能，并移除模型开发人员更改组件的功能。

1. 在cq:component节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   有关cq:editConfig节点的更多信息，请参阅[配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在cq:EditConfig节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 向`cq:formParameters`节点添加`String`属性。 组件超级类型确定属性的名称：

   * 进程步骤: `PROCESS`
   * 参与者步骤: `PARTICIPANT`
   * 动态参与者步骤: `DYNAMIC_PARTICIPANT`

1. 指定属性的值：

   * `PROCESS`:ECMA脚本或实施步骤行为的服务PID的路径。
   * `PARTICIPANT`:为工作项分配的用户ID。
   * `DYNAMIC_PARTICIPANT`:ECMA脚本的路径或选择用户分配工作项的服务的PID。

1. 要删除模型开发人员更改属性值的功能，请覆盖组件超类型的对话框。

### 将Forms和对话框添加到参与者步骤{#adding-forms-and-dialogs-to-participant-steps}

自定义您的参与者步骤组件，以提供[表单参与者步骤](/help/sites-developing/workflows-step-ref.md#form-participant-step)和[对话框参与者步骤](/help/sites-developing/workflows-step-ref.md#dialog-participant-step)组件中的功能：

* 在用户打开生成的工作项时向用户展示表单。
* 在用户完成生成的工作项时，向用户显示自定义对话框。

对新组件执行以下过程（请参阅[创建自定义工作流步骤组件](#creating-custom-workflow-step-components)）：

1. 在`cq:Component`节点下，添加以下节点：

   * 名称: `cq:editConfig`
   * 类型: `cq:EditConfig`

   有关cq:editConfig节点的更多信息，请参阅[配置组件的编辑行为](/help/sites-developing/components-basics.md#edit-behavior)。

1. 在cq:EditConfig节点下，添加以下节点：

   * 名称: `cq:formParameters`
   * 类型: `nt:unstructured`

1. 要在用户打开工作项时显示表单，请将以下属性添加到`cq:formParameters`节点：

   * 名称: `FORM_PATH`
   * 类型: `String`
   * 值：解析到表单的路径

1. 要在用户完成工作项时显示自定义对话框，请将以下属性添加到`cq:formParameters`节点

   * 名称: `DIALOG_PATH`
   * 类型: `String`
   * 值：解析到对话框的路径

### 配置工作流步骤运行时行为{#configuring-the-workflow-step-runtime-behavior}

在`cq:Component`节点下，添加`cq:EditConfig`节点。 在添加`nt:unstructured`节点（必须命名为`cq:formParameters`）的下面，向该节点添加以下属性：

* 名称: `PROCESS_AUTO_ADVANCE`

   * 类型: `Boolean`
   * 值:

      * 当设置为`true`时，工作流将运行该步骤并继续 — 这是默认设置，也建议
      * `false`时，工作流将运行并停止；这需要额外的处理，因此建议使用`true`

* 名称: `DO_NOTIFY`

   * 类型: `Boolean`
   * 值：指示是否应为用户参与步骤发送电子邮件通知（并假定邮件服务器已正确配置）

## 保留并访问数据{#persisting-and-accessing-data}

### 保留后续工作流步骤{#persisting-data-for-subsequent-workflow-steps}的数据

您可以使用工作流元数据在工作流生命周期内以及各个步骤之间保留所需的信息。 工作流步骤的常见要求是保留数据以供将来使用，或从先前步骤中检索保留的数据。

工作流元数据存储在[`MetaDataMap`](#metadatamaps)对象中。 Java API提供了[`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)方法，以返回提供相应`MetaDataMap`对象的[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html)对象。 此`WorkflowData` `MetaDataMap`对象可用于步骤组件的OSGi服务或ECMA脚本。

#### Java {#java}

`WorkflowProcess`实现的执行方法将传递到`WorkItem`对象。 使用此对象获取当前工作流实例的`WorkflowData`对象。 以下示例将项目添加到工作流`MetaDataMap`对象，然后记录每个项目。 (“mykey”、“My Step Value”)项目可用于工作流中的后续步骤。

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

`graniteWorkItem`变量是当前`WorkItem` Java对象的ECMA脚本表示形式。 因此，您可以使用`graniteWorkItem`变量获取工作流元数据。 以下ECMA脚本可用于实施&#x200B;**流程步骤**&#x200B;以向工作流`MetaDataMap`对象添加项目，然后记录每个项目。 这些项目随后可用于工作流中的后续步骤。

>[!NOTE]
>
>步骤脚本可立即使用的`metaData`变量是步骤的元数据。 步骤元数据与工作流元数据不同。

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

### 在运行时访问对话框属性值{#accessing-dialog-property-values-at-runtime}

工作流实例的`MetaDataMap`对象可用于在整个工作流生命周期中存储和检索数据。 对于工作流步骤组件实施，`MetaDataMap`对于在运行时检索组件属性值特别有用。

>[!NOTE]
>
>有关将组件对话框配置为将属性存储为工作流元数据的信息，请参阅[在工作流元数据中保存属性值](#saving-property-values-in-workflow-metadata)。

工作流`MetaDataMap`可用于Java和ECMA脚本进程实施：

* 在WorkflowProcess界面的Java实现中，`args`参数是工作流的`MetaDataMap`对象。

* 在ECMA脚本实施中，值可使用`args`和`metadata`变量。

### 示例：检索流程步骤组件的参数{#example-retrieving-the-arguments-of-the-process-step-component}

**进程步骤**&#x200B;组件的编辑对话框包含&#x200B;**参数**&#x200B;属性。 **Arguments**&#x200B;属性的值存储在工作流元数据中，并与`PROCESS_ARGS`键相关联。

在下图中，**Arguments**&#x200B;属性的值为`argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java代码是`WorkflowProcess`实施的`execute`方法。 方法会在`args` `MetaDataMap`中记录与`PROCESS_ARGS`键值关联的值。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

当执行使用此Java实施的流程步骤时，日志包含以下条目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 脚本 {#ecma-script-1}

以下ECMA脚本用作&#x200B;**流程步骤**&#x200B;的流程。 它记录参数数和参数值：

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
>本节介绍如何使用用于流程步骤的参数。 该信息也适用于动态参与者选择器。

>[!NOTE]
>有关在工作流元数据中存储组件属性的另一个示例，请参阅示例：创建记录器工作流步骤。 此示例提供了一个对话框，用于将元数据值与PROCESS_ARGS以外的键值关联。

### 脚本和进程参数{#scripts-and-process-arguments}

在&#x200B;**处理步骤**&#x200B;组件的脚本中，参数可通过`args`对象使用。

创建自定义步骤组件时，对象`metaData`在脚本中可用。 此对象仅限于单个字符串参数。

## 开发流程步骤实施{#developing-process-step-implementations}

在工作流过程中启动进程步骤时，这些步骤会向OSGi服务发送请求或执行ECMA脚本。 开发服务或ECMA脚本，以执行工作流所需的操作。

>[!NOTE]
>
>有关将流程步骤组件与服务或脚本关联的信息，请参阅[流程步骤](/help/sites-developing/workflows-step-ref.md#process-step)或[覆盖步骤实施](#overriding-the-step-implementation)。

### 使用Java类{#implementing-a-process-step-with-a-java-class}实施进程步骤

要将流程步骤定义为OSGi服务组件（Java包），请执行以下操作：

1. 创建包并将其部署到OSGI容器中。 请参阅有关使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)或[Eclipse](/help/sites-developing/howto-projects-eclipse.md)创建包的文档。

   >[!NOTE]
   >
   >OSGi组件需要使用其`execute()`方法实现`WorkflowProcess`接口。 请参阅下面的示例代码。

   >[!NOTE]
   >
   >需要将包名称添加到`maven-bundle-plugin`配置的`<*Private-Package*>`部分。

1. 添加SCR属性`process.label`并根据需要设置值。 这将是使用通用的&#x200B;**流程步骤**&#x200B;组件时，流程步骤所列的名称。 请参阅以下示例。
1. 在&#x200B;**模型**&#x200B;编辑器中，使用通用的&#x200B;**流程步骤**&#x200B;组件将流程步骤添加到工作流中。
1. 在编辑对话框（**流程步骤**&#x200B;的）中，转到&#x200B;**流程**&#x200B;选项卡，然后选择您的流程实施。
1. 如果在代码中使用参数，请设置&#x200B;**进程参数**。 例如：false。
1. 保存步骤和工作流模型（模型编辑器的左上角）的更改。

Java方法，分别将实现可执行Java方法的类注册为OSGI服务，这样您就可以在运行时随时添加方法。

当有效负载为页面时，以下OSGI组件会将属性`approved`添加到页面内容节点：

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
>如果流程一行中失败三次，则会将一个项目置于工作流管理员的收件箱中。

### 使用ECMAScript {#using-ecmascript}

ECMA脚本使脚本开发人员能够实施流程步骤。 脚本位于JCR存储库中，并从中执行。

下表列出了可立即用于处理脚本的变量，以便提供对工作流Java API对象的访问。

| Java类 | 脚本变量名称 | 描述 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 当前步骤实例。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 当前步骤实例的工作流会话。 |
| `String[]` （包含进程参数） | `args` | 步骤参数。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 当前步骤实例的元数据。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供对Sling运行时环境的访问。 |

以下示例脚本演示如何访问表示工作流有效负载的JCR节点。 `graniteWorkflowSession`变量适用于JCR会话变量，该变量用于从有效负载路径获取节点。

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

以下脚本检查有效负载是否为图像（`.png`文件），从中创建黑白图像，并将其另存为同级节点。

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

要使用脚本，请执行以下操作：

1. 创建脚本(例如CRXDE Lite)并将其保存在`/apps/myapp/workflow/scripts`下的存储库中
1. 要在&#x200B;**流程步骤**&#x200B;编辑对话框中指定标识脚本的标题，请将以下属性添加到脚本的`jcr:content`节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在编辑对话框中显示的名称。 |

1. 编辑&#x200B;**Process Step**&#x200B;实例，并指定要使用的脚本。

## 开发参与者选择器{#developing-participant-choosers}

您可以为&#x200B;**动态参与者步骤**&#x200B;组件开发参与者选择器。

当在工作流中启动&#x200B;**动态参与者步骤**&#x200B;组件时，该步骤需要确定可将生成的工作项分配到的参与者。 要执行此步骤，请执行以下操作之一：

* 向OSGi服务发送请求
* 执行ECMA脚本以选择参与者

您可以开发一个服务或ECMA脚本，该脚本将根据工作流的要求选择参与者。

>[!NOTE]
>
>有关将&#x200B;**动态参与者步骤**&#x200B;组件与服务或脚本关联的信息，请参阅[动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step)或[覆盖步骤实施](#persisting-and-accessing-data)。

### 使用Java类{#developing-a-participant-chooser-using-a-java-class}开发参与者选择器

要将参与者步骤定义为OSGi服务组件（Java类），请执行以下操作：

1. OSGi组件需要使用其`getParticipant()`方法实现`ParticipantStepChooser`接口。 请参阅下面的示例代码。

   创建包并将其部署到OSGI容器中。

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

1. 在&#x200B;**模型**&#x200B;编辑器中，使用通用的&#x200B;**动态参与者步骤**&#x200B;组件将动态参与者步骤添加到工作流中。
1. 在编辑对话框中，选择&#x200B;**参与者选择器**&#x200B;选项卡，然后选择您的选择器实施。
1. 如果在代码中使用参数设置&#x200B;**Process Arguments**。 对于此示例：`/content/we-retail/de`。
1. 保存步骤和工作流模型的更改。

### 使用ECMA脚本{#developing-a-participant-chooser-using-an-ecma-script}开发参与者选择器

您可以创建一个ECMA脚本，以选择为分配了&#x200B;**参与者步骤**&#x200B;所生成的工作项的用户。 脚本必须包含一个名为`getParticipant`的函数，该函数不需要参数，并返回一个`String`，该函数包含用户或组的ID。

脚本位于JCR存储库中，并从中执行。

下表列出了变量，这些变量可让您立即访问脚本中的工作流Java对象。

| Java类 | 脚本变量名称 |
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

1. 创建脚本(例如CRXDE Lite)并将其保存在`/apps/myapp/workflow/scripts`下的存储库中
1. 要在&#x200B;**流程步骤**&#x200B;编辑对话框中指定标识脚本的标题，请将以下属性添加到脚本的`jcr:content`节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在编辑对话框中显示的名称。 |

1. 编辑[动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step)实例并指定要使用的脚本。

## 处理工作流包{#handling-workflow-packages}

[可以](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 将工作流包传递到工作流进行处理。工作流包包含对页面和资产等资源的引用。

>[!NOTE]
>
>以下工作流流程步骤接受用于批量页面激活的工作流包：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)

>



您可以开发工作流步骤，以获取资源包并对其进行处理。 `com.day.cq.workflow.collection`包的以下成员提供对工作流包的访问：

* `ResourceCollection`:工作流包类。
* `ResourceCollectionUtil`:用于检索ResourceCollection对象。
* `ResourceCollectionManager`:创建并检索收藏集。实施将部署为OSGi服务。

以下示例Java类演示了如何获取包资源：

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

开始创建您自己的自定义步骤的一种简单方法是，从以下位置复制现有步骤：

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

1. 然后，将复制的步骤放入/apps文件夹中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是我们示例自定义步骤的结果：

   ![wf-36](assets/wf-34.png)

   >[!CAUTION]
   >
   >由于在标准UI中，卡片上不显示仅标题而非详细信息，因此不需要`details.jsp`，因为经典UI编辑器需要。

1. 将以下属性应用到节点：

   `/apps/cq/workflow/components/model/myCustomStep`

   **权益物业：**

   * `sling:resourceSuperType`

      必须继承现有步骤。

      在本例中，我们将继承位于`cq/workflow/components/model/step`的基本步骤，但您可以使用其他超类型，如`participant`、`process`等。

   * `jcr:title`

      是在步骤浏览器中列出组件时显示的标题（工作流模型编辑器的左侧面板）。

   * `cq:icon`

      用于为步骤指定[Coral图标](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html)。

   * `componentGroup`

      必须是以下任一值：

      * 协作工作流
      * DAM 工作流
      * 表单工作流
      * 项目
      * WCM 工作流
      * 工作流

   ![wf-35](assets/wf-35.png)

1. 您现在可以打开工作流模型进行编辑。 在步骤浏览器中，您可以进行筛选以查看&#x200B;**我的自定义步骤**:

   ![wf-36](assets/wf-36.png)

   将&#x200B;**My Custom Step**&#x200B;拖动到模型上时，会显示卡：

   ![wf-37](assets/wf-37.png)

   如果尚未为步骤定义`cq:icon`，则使用标题的前两个字母呈现默认图标。 例如：

   ![wf-38](assets/wf-38.png)

#### 定义步骤配置对话框{#defining-the-step-configure-dialog}

在[创建基本步骤](#creating-the-basic-step)之后，按如下方式定义步骤&#x200B;**配置**&#x200B;对话框：

1. 按如下方式配置节点`cq:editConfig`上的属性：

   **权益物业：**

   * `cq:inherit`

      当设置为`true`时，您的步骤组件将继承您在`sling:resourceSuperType`中指定的步骤的属性。

   * `cq:disableTargeting`

      设置为必需。
   ![wf-39](assets/wf-39.png)

1. 按如下方式配置节点`cq:formsParameter`上的属性：

   **权益物业：**

   * `jcr:title`

      在模型映射的步骤卡片和&#x200B;**My Custom - Step Properties**&#x200B;配置对话框的&#x200B;**Title**&#x200B;字段中设置默认标题。

   * 您还可以定义自己的自定义属性。

   ![wf-40](assets/wf-40.png)

1. 在节点`cq:listeners`上配置属性。

   `cq:listener`节点及其属性允许您在触屏优化UI模型编辑器中设置事件响应事件处理程序；例如，将步骤拖动到模型页面或编辑步骤属性。

   **权益物业：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此配置对于编辑器的正常运行至关重要。 在大多数情况下，此配置不得更改。

   但是，将`cq:inherit`设置为true（在`cq:editConfig`节点上，请参阅上文）允许您继承此配置，而无需在步骤定义中显式包含此配置。 如果没有就地继承，则无需添加具有以下属性和值的此节点。

   在此示例中，已激活继承，因此我们可以删除`cq:listeners`节点，并且该步骤仍可以正常运行。

   ![wf-41](assets/wf-41.png)

1. 您现在可以将步骤的实例添加到工作流模型中。 在&#x200B;**配置**&#x200B;步骤时，您将看到对话框：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此示例{#sample-markup-used-in-this-example}中使用的示例标记

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
>请注意对话框定义中的公共节点和进程节点。 这些值继承自用作自定义步骤超类型的流程步骤：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>经典UI模型编辑器对话框仍可以与标准触屏UI编辑器配合使用。
>
>如果要将经典UI步骤对话框升级到标准UI对话框，则AEM具有[现代化工具](/help/sites-developing/modernization-tools.md)。 在转换后，对于某些情况，仍可对对话框进行一些手动改进。
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
您不得修改`/libs`中的任何内容，只需以它们为示例即可。 如果要利用任何现有步骤，请将它们复制到`/apps`，然后在此处对其进行修改。
