---
title: 扩展工作流功能
seo-title: Extending Workflow Functionality
description: 了解如何扩展Adobe Experience Manager的工作流功能。
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '3589'
ht-degree: 2%

---

# 扩展工作流功能{#extending-workflow-functionality}

本主题介绍如何为工作流开发自定义步骤组件，以及如何以编程方式与工作流交互。

创建自定义工作流步骤涉及以下活动：

* 开发工作流步骤组件。
* 将步骤功能作为OSGi服务或ECMA脚本实施。

您还可以 [通过程序和脚本与工作流交互](/help/sites-developing/workflows-program-interaction.md).

## 工作流步骤组件 — 基础知识 {#workflow-step-components-the-basics}

工作流步骤组件在创建工作流模型时定义步骤的外观和行为：

* 工作流Sidekick中的类别和步骤名称。
* 工作流模型中步骤的外观。
* 用于配置组件属性的编辑对话框。
* 运行时执行的服务或脚本。

与 [所有组件](/help/sites-developing/components.md)，工作流步骤组件继承自为指定的组件 `sling:resourceSuperType` 属性。 下图显示了 `cq:component` 构成所有工作流步骤组件基础的节点。 该图还包含 **流程步骤**， **参与者步骤**、和 **动态参与者步骤** 组件，因为这些组件是开发自定义步骤组件最常见（也是最基本）的起点。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>您 ***必须*** 不会更改中的任何内容 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>建议用于配置和其他更改的方法是：
>
>1. 重新创建所需项目(即，它存在于 `/libs` 下 `/apps`
>2. 在中进行任何更改 `/apps`

此 `/libs/cq/workflow/components/model/step` component是 **流程步骤**， **参与者步骤**、和 **动态参与者步骤**，它们将继承以下项：

* `step.jsp`

  此 `step.jsp` 脚本在添加到模型时呈现步骤组件的标题。

  ![wf-22-1](assets/wf-22-1.png)

* [cq：dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

  包含以下选项卡的对话框：

   * **公共**：用于编辑标题和描述。
   * **高级**：用于编辑电子邮件通知属性。

  ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

  >[!NOTE]
  >
  >当步骤组件的“编辑”对话框的选项卡与此默认外观不匹配时，步骤组件已定义了脚本、节点属性或对话框选项卡，这些选项卡将覆盖这些继承的选项卡。

### ECMA脚本 {#ecma-scripts}

以下对象在ECMA脚本中可用（取决于步骤类型）：

* [工作项](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) 工作项
* [Workflowsession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [Workflowdata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`：包含进程参数的数组。

* `sling`：访问其他osgi服务。
* `jcrSession`

### 元数据映射 {#metadatamaps}

您可以使用工作流元数据来保留在工作流生命周期期间所需的信息。 工作流步骤的常见要求是保留数据以供将来在工作流中使用，或者检索保留的数据。

有三种类型的MetaDataMap对象 — for `Workflow`， `WorkflowData` 和 `WorkItem` 对象。 它们都具有相同的预期用途 — 存储元数据。

工作项具有自己的元数据映射，该元数据映射只能在该工作项（例如，步骤）运行时使用。

两者 `Workflow` 和 `WorkflowData` 元数据映射在整个工作流中共享。 对于这些情况，建议仅使用 `WorkflowData` 元数据映射。

## 创建自定义工作流步骤组件 {#creating-custom-workflow-step-components}

工作流步骤组件可以是 [创建方式与任何其他组件相同](/help/sites-developing/components.md).

要从（现有）基本步骤组件之一继承，请将以下属性添加到 `cq:Component` 节点：

* 名称：`sling:resourceSuperType`
* 类型：`String`
* 值：解析为基本组件的以下路径之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步骤实例的默认标题和说明 {#specifying-the-default-title-and-description-for-step-instances}

使用以下过程指定 **标题** 和 **描述** 字段位于 **公共** 选项卡。

>[!NOTE]
>
>当满足以下两个要求时，字段值将显示在步骤实例上：
>
>* 步骤的“编辑”对话框将标题和描述存储在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 个位置
>
>  当“编辑”对话框使用 `/libs/cq/flow/components/step/step` 组件实现。
>
>* 步骤组件或组件的上级不会覆盖 `step.jsp` 编写脚本以便 `/libs/cq/flow/components/step/step` 组件实现。

1. 在 `cq:Component` 节点，添加以下节点：

   * 名称：`cq:editConfig`
   * 类型：`cq:EditConfig`

   >[!NOTE]
   >
   >有关cq：editConfig节点的更多信息，请参见 [配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在 `cq:EditConfig` 节点，添加以下节点：

   * 名称：`cq:formParameters`
   * 类型：`nt:unstructured`

1. 添加 `String` 以下名称的属性更改为 `cq:formParameters` 节点：

   * `jcr:title`：此值填充 **标题** 字段 **公共** 选项卡。
   * `jcr:description`：此值填充 **描述** 字段 **公共** 选项卡。

### 在工作流元数据中保存属性值 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>请参阅 [保留和访问数据](#persisting-and-accessing-data). 特别是，有关在运行时访问属性的信息，请参见 [在运行时访问对话框属性值](#accessing-dialog-property-values-at-runtime).

的名称属性 `cq:Widget` items指定存储构件值的JCR节点。 当小组件出现在工作流步骤组件的对话框中时，将值存储在 `./metaData` 节点，该值将添加到工作流中 `MetaDataMap`.

例如，对话框中的文本字段是 `cq:Widget` 具有以下属性的节点：

| 名称 | 类型 | 价值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

在此文本字段中指定的值将添加到工作流实例的 ` [MetaDataMap](#metadatamaps)` 对象，并与 `subject` 键。

>[!NOTE]
>
>当键为 `PROCESS_ARGS`，此值可在ECMA脚本实施中通过 `args` 变量。 在本例中，name属性的值为 `./metaData/PROCESS_ARGS.`

### 覆盖步骤实施 {#overriding-the-step-implementation}

通过每个基本步骤组件，工作流模型开发人员可在设计时配置以下关键功能：

* 流程步骤：要在运行时执行的服务或ECMA脚本。
* 参与者步骤：为已生成的工作项分配了用户的标识。
* 动态参与者步骤：选择已分配工作项的用户ID的服务或ECMA脚本。

要集中特定工作流场景中使用的组件，请在设计中配置关键功能，并移除模型开发人员更改该组件的功能。

1. 在cq：component节点下，添加以下节点：

   * 名称：`cq:editConfig`
   * 类型：`cq:EditConfig`

   有关cq：editConfig节点的更多信息，请参见 [配置组件的编辑行为](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在cq：EditConfig节点下，添加以下节点：

   * 名称：`cq:formParameters`
   * 类型：`nt:unstructured`

1. 添加 `String` 属性到 `cq:formParameters` 节点。 组件超类型确定属性的名称：

   * 流程步骤: `PROCESS`
   * 参与者步骤: `PARTICIPANT`
   * 动态参与者步骤: `DYNAMIC_PARTICIPANT`

1. 指定属性的值：

   * `PROCESS`：ECMA脚本的路径或实施步骤行为的服务的PID。
   * `PARTICIPANT`：分配了工作项的用户的ID。
   * `DYNAMIC_PARTICIPANT`：ECMA脚本的路径或选择用户分配工作项的服务的PID。

1. 要移除模型开发人员更改属性值的功能，请覆盖组件超类型的对话框。

### 将Forms和对话框添加到参与者步骤 {#adding-forms-and-dialogs-to-participant-steps}

自定义您的参与者步骤组件，以提供可在以下位置找到的功能： [表单参与者步骤](/help/sites-developing/workflows-step-ref.md#form-participant-step) 和 [对话框参与者步骤](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) 组件：

* 当用户打开生成的工作项时，向其展示表单。
* 当用户完成生成的工作项时，向其显示自定义对话框。

在新组件上执行以下过程(请参见 [创建自定义工作流步骤组件](#creating-custom-workflow-step-components))：

1. 在 `cq:Component` 节点，添加以下节点：

   * 名称：`cq:editConfig`
   * 类型：`cq:EditConfig`

   有关cq：editConfig节点的更多信息，请参见 [配置组件的编辑行为](/help/sites-developing/components-basics.md#edit-behavior).

1. 在cq：EditConfig节点下，添加以下节点：

   * 名称：`cq:formParameters`
   * 类型：`nt:unstructured`

1. 要在用户打开工作项时显示表单，请将以下属性添加到 `cq:formParameters` 节点：

   * 名称：`FORM_PATH`
   * 类型：`String`
   * 值：解析为表单的路径

1. 要在用户完成工作项时显示自定义对话框，请将以下属性添加到 `cq:formParameters` 节点

   * 名称：`DIALOG_PATH`
   * 类型：`String`
   * 值：解析为对话框的路径

### 配置工作流步骤运行时行为 {#configuring-the-workflow-step-runtime-behavior}

在 `cq:Component` 节点，添加 `cq:EditConfig` 节点。 在该处下添加 `nt:unstructured` 节点(必须命名 `cq:formParameters`)并添加到该节点中，添加以下属性：

* 名称：`PROCESS_AUTO_ADVANCE`

   * 类型：`Boolean`
   * 价值:

      * 当设置为 `true` 工作流将运行此步骤并继续 — 这是默认设置，也是推荐的
      * 时间 `false`，工作流将运行并停止；这需要额外的处理，因此 `true` 推荐

* 名称：`DO_NOTIFY`

   * 类型：`Boolean`
   * 值：指示是否应为用户参与步骤发送电子邮件通知（并假定邮件服务器配置正确）

## 保留和访问数据 {#persisting-and-accessing-data}

### 保留数据以供后续工作流步骤使用 {#persisting-data-for-subsequent-workflow-steps}

您可以使用工作流元数据来保留在工作流生命周期期间以及各个步骤之间所需的信息。 工作流步骤的常见要求是保留数据以供将来使用，或者从先前的步骤中检索保留的数据。

工作流元数据存储在中 [`MetaDataMap`](#metadatamaps) 对象。 Java API提供 [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) 用于返回 [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) 提供相应内容的对象 `MetaDataMap` 对象。 此 `WorkflowData` `MetaDataMap` 对象可用于步骤组件的OSGi服务或ECMA脚本。

#### Java {#java}

的execute方法 `WorkflowProcess` 实施传递给 `WorkItem` 对象。 使用此对象获取 `WorkflowData` 当前工作流实例的对象。 以下示例将项目添加到工作流 `MetaDataMap` 对象，然后记录每个项目。 （“mykey”、“我的步骤值”）项目可用于工作流中的后续步骤。

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

此 `graniteWorkItem` 变量是当前的ECMA脚本表示形式 `WorkItem` Java对象。 因此，您可以使用 `graniteWorkItem` 变量以获取工作流元数据。 以下ECMA脚本可用于实施 **流程步骤** 将项目添加到工作流 `MetaDataMap` 对象，然后记录每个项目。 这些项目随后可用于工作流中的后续步骤。

>[!NOTE]
>
>此 `metaData` 步骤脚本立即可用的变量是步骤的元数据。 步骤元数据与工作流元数据不同。

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

### 在运行时访问对话框属性值 {#accessing-dialog-property-values-at-runtime}

此 `MetaDataMap` 工作流实例对象可用于在工作流整个生命周期中存储和检索数据。 对于工作流步骤组件实施， `MetaDataMap` 在运行时检索组件属性值时特别有用。

>[!NOTE]
>
>有关配置组件对话框以将属性存储为工作流元数据的信息，请参阅 [在工作流元数据中保存属性值](#saving-property-values-in-workflow-metadata).

工作流 `MetaDataMap` 可用于Java和ECMA脚本流程实施：

* 在WorkflowProcess接口的Java实现中， `args` 参数为 `MetaDataMap` 工作流对象。

* 在ECMA脚本实施中，值可通过使用 `args` 和 `metadata` 变量。

### 示例：检索流程步骤组件的参数 {#example-retrieving-the-arguments-of-the-process-step-component}

的编辑对话框 **流程步骤** 组件包括 **参数** 属性。 的值 **参数** 属性存储在工作流元数据中，并与 `PROCESS_ARGS` 键。

在下图中， **参数** 属性为 `argument1, argument2`：

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java代码是 `execute` 方法 `WorkflowProcess` 实现。 方法将值记录在 `args` `MetaDataMap` 与 `PROCESS_ARGS` 键。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

当使用此Java实施的流程步骤执行时，日志包含以下条目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 脚本 {#ecma-script-1}

以下ECMA脚本将用作 **流程步骤**. 它会记录参数的数量和参数值：

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
>本节介绍如何使用参数完成流程步骤。 该信息也适用于动态参与者选择器。

>[!NOTE]
>有关在工作流元数据中存储组件属性的另一个示例，请参阅示例：创建记录器工作流步骤。 此示例的特征是一个将元数据值与PROCESS_ARGS以外的键关联的对话框。

### 脚本和进程参数 {#scripts-and-process-arguments}

在脚本中的 **流程步骤** 组件，参数可通过 `args` 对象。

创建自定义步骤组件时，对象 `metaData` 在脚本中可用。 此对象仅限于单个字符串参数。

## 开发流程步骤实施 {#developing-process-step-implementations}

当在工作流进程中启动流程步骤时，这些步骤将向OSGi服务发送请求或执行ECMA脚本。 开发服务或ECMA脚本，以执行工作流所需的操作。

>[!NOTE]
>
>有关将Process Step组件与服务或脚本关联的信息，请参见 [流程步骤](/help/sites-developing/workflows-step-ref.md#process-step) 或 [覆盖步骤实施](#overriding-the-step-implementation).

### 使用Java类实施流程步骤 {#implementing-a-process-step-with-a-java-class}

将流程步骤定义为OSGI服务组件（Java捆绑包）：

1. 创建该捆绑包并将其部署到OSGI容器中。 请参阅有关使用创建捆绑包的文档 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 或 [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >OSGI组件需要实施 `WorkflowProcess` 与其的接口 `execute()` 方法。 请参阅下面的示例代码。

   >[!NOTE]
   >
   >需要将包名称添加到 `<*Private-Package*>` 的部分 `maven-bundle-plugin` 配置。

1. 添加SCR属性 `process.label`  并根据需要设置值。 这将是使用通用部件时列出的流程步骤的名称 **流程步骤** 组件。 请参阅以下示例。
1. 在 **模型** 编辑器中，使用通用规则将流程步骤添加到工作流中 **流程步骤** 组件。
1. 在的“编辑”对话框中， **流程步骤**)，转到 **进程** 选项卡并选择流程实施。
1. 如果在代码中使用参数，请设置 **进程参数**. 例如：false。
1. 保存步骤和工作流模型（模型编辑器的左上角）的更改。

Java方法（分别用于实现可执行的Java方法的类）注册为OSGI服务，从而使您可以在运行时随时添加方法。

以下OSGI组件添加属性 `approved` 到页面内容节点（当有效负荷为页面时）：

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
>如果流程连续失败三次，则会将项目置于工作流管理员的“收件箱”中。

### 使用ECMAScript {#using-ecmascript}

ECMA脚本使脚本开发人员能够实施流程步骤。 脚本位于JCR存储库中，并从此处执行。

下表列出了可立即用于处理脚本的变量，提供了对工作流Java API对象的访问权限。

| Java类 | 脚本变量名称 | 描述 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 当前步骤实例。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 当前步骤实例的工作流会话。 |
| `String[]` （包含进程参数） | `args` | 步骤参数。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 当前步骤实例的元数据。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供对Sling运行时环境的访问权限。 |

以下示例脚本演示了如何访问表示工作流有效负载的JCR节点。 此 `graniteWorkflowSession` 变量被调整为JCR会话变量，该变量用于从有效负荷路径获取节点。

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

以下脚本检查有效负载是否为图像( `.png` 文件)，从中创建黑白图像，并将其另存为同级节点。

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

1. 创建脚本(例如，使用CRXDE Lite)并将其保存在下面的存储库中 `//apps/workflow/scripts/`
1. 要指定用于在脚本中标识脚本的标题，请执行以下操作 **流程步骤** 编辑对话框，请将以下属性添加到 `jcr:content` 脚本的节点：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 显示在“编辑”对话框中的名称。 |

1. 编辑 **流程步骤** 并指定要使用的脚本。

## 开发参与者选择器 {#developing-participant-choosers}

您可以开发参与者选择器 **动态参与者步骤** 组件。

当 **动态参与者步骤** 组件在工作流期间启动，该步骤需要确定可将生成的工作项分配到的参与者。 要执行此操作，请执行以下步骤：

* 向OSGi服务发送请求
* 执行ECMA脚本以选择参与者

您可以开发服务或ECMA脚本，以根据工作流的要求选择参与者。

>[!NOTE]
>
>有关关联 **动态参与者步骤** 包含服务或脚本的组件，请参见 [动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 或 [覆盖步骤实施](#persisting-and-accessing-data).

### 使用Java类开发参与者选择器 {#developing-a-participant-chooser-using-a-java-class}

要将参与者步骤定义为OSGI服务组件（Java类），请执行以下操作：

1. OSGI组件需要实施 `ParticipantStepChooser` 与其的接口 `getParticipant()` 方法。 请参阅下面的示例代码。

   创建该捆绑包并将其部署到OSGI容器中。

1. 添加SCR属性 `chooser.label` 并根据需要设置值。 这将为参与者选择器列出的名称，使用 **动态参与者步骤** 组件。 请参阅示例：

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

1. 在 **模型** 编辑者，使用通用规则将动态参与者步骤添加到工作流中 **动态参与者步骤** 组件。
1. 在“编辑”对话框中，选择 **参与者选择器** 选项卡，然后选择您的选择器实施。
1. 如果您在代码中使用参数，请将 **进程参数**. 对于此示例： `/content/we-retail/de`.
1. 保存步骤和工作流模型的更改。

### 使用ECMA脚本开发参与者选择器 {#developing-a-participant-chooser-using-an-ecma-script}

您可以创建一个ECMA脚本，该脚本用于选择分配了工作项的用户。 **参与者步骤** 生成。 脚本必须包含一个名为的函数 `getParticipant` 它不需要任何参数，并且返回 `String` 包含用户或组的ID。

脚本位于JCR存储库中，并从此处执行。

下表列出了允许您立即访问脚本中的工作流Java对象的变量。

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

1. 创建脚本(例如，使用CRXDE Lite)并将其保存在下面的存储库中 `//apps/workflow/scripts`
1. 要指定用于在脚本中标识脚本的标题，请执行以下操作 **流程步骤** 编辑对话框，请将以下属性添加到 `jcr:content` 脚本的节点：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 显示在“编辑”对话框中的名称。 |

1. 编辑 [动态参与者步骤](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 并指定要使用的脚本。

## 处理工作流包 {#handling-workflow-packages}

[工作流包](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 可传递给工作流进行处理。 工作流包包含对资源（如页面和资产）的引用。

>[!NOTE]
>
>以下工作流流程步骤接受工作流包以进行批量页面激活：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>

您可以开发工作流步骤以获取资源包资源并对其进行处理。 以下成员属于 `com.day.cq.workflow.collection` 包提供对工作流包的访问：

* `ResourceCollection`：工作流包类。
* `ResourceCollectionUtil`：用于检索Resource收藏集对象。
* `ResourceCollectionManager`：创建和检索收藏集。 实施部署为OSGi服务。

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

## 示例：创建自定义步骤 {#example-creating-a-custom-step}

开始创建自己的自定义步骤的一个简单方法是从以下位置复制现有步骤：

`/libs/cq/workflow/components/model`

### 创建基本步骤 {#creating-the-basic-step}

1. 在/apps下重新创建路径；例如：

   `/apps/cq/workflow/components/model`

   新文件夹的类型为 `nt:folder`：

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

1. 然后将复制的步骤放置到/apps文件夹中；例如，如下所示：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是我们的示例自定义步骤的结果：

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >因为在标准UI中，卡片上不显示标题而非详细信息， `details.jsp` 不需要使用，因为这对于经典UI编辑器来说是必需的。

1. 将以下属性应用于节点：

   `/apps/cq/workflow/components/model/myCustomStep`

   **感兴趣的物业：**

   * `sling:resourceSuperType`

     必须继承自现有步骤。

     在本例中，我们继承了位于的基本步骤 `cq/workflow/components/model/step`，但您可以使用其他超级类型，例如 `participant`， `process`，等等。

   * `jcr:title`

     在步骤浏览器（工作流模型编辑器的左侧面板）中列出组件时显示的标题。

   * `cq:icon`

     用于指定 [Coral图标](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 完成步骤。

   * `componentGroup`

     必须为以下任一项：

      * 协作工作流
      * DAM 工作流
      * 表单工作流
      * 项目
      * WCM 工作流
      * 工作流

   ![wf-35](assets/wf-35.png)

1. 您现在可以打开工作流模型进行编辑。 在步骤中，您可以对浏览器进行筛选以查看 **我的自定义步骤**：

   ![wf-36](assets/wf-36.png)

   拖动 **我的自定义步骤** 在模型上，显示信息卡：

   ![wf-37](assets/wf-37.png)

   如果否 `cq:icon` 已经为步骤定义了，然后使用标题的前两个字母呈现默认图标。 例如：

   ![wf-38](assets/wf-38.png)

#### 定义步骤配置对话框 {#defining-the-step-configure-dialog}

之后 [创建基本步骤](#creating-the-basic-step)，定义步骤 **配置** 对话框，如下所示：

1. 配置节点上的属性 `cq:editConfig` 如下所示：

   **感兴趣的物业：**

   * `cq:inherit`

     当设置为 `true`，则步骤组件将继承您在中指定的步骤的属性 `sling:resourceSuperType`.

   * `cq:disableTargeting`

     根据需要设置。

   ![wf-39](assets/wf-39.png)

1. 配置节点上的属性 `cq:formsParameter` 如下所示：

   **感兴趣的物业：**

   * `jcr:title`

     在模型图中的步骤卡片上设置默认标题，在 **标题** 字段 **我的自定义 — 步骤属性** 配置对话框。

   * 您还可以定义自己的自定义属性。

   ![wf-40](assets/wf-40.png)

1. 配置节点上的属性 `cq:listeners`.

   此 `cq:listener` 节点及其属性允许您在启用了触屏的UI模型编辑器中设置对事件做出反应的事件处理程序；例如，将步骤拖动到模型页面或编辑步骤属性。

   **感兴趣的物业：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此配置对于编辑器的正常运行至关重要。 在大多数情况下，不得更改此配置。

   但是，设置 `cq:inherit` 为true(在 `cq:editConfig` 节点，请参阅上文)允许您继承此配置，而无需将其明确包含在步骤定义中。 如果未实施继承，则您需要添加具有以下属性和值的此节点。

   在此示例中，继承已激活，因此我们可以删除 `cq:listeners` 节点和步骤仍可正常运行。

   ![wf-41](assets/wf-41.png)

1. 您现在可以将步骤的实例添加到工作流模型中。 当您 **配置** 在步骤中，您将看到以下对话框：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此示例中使用的示例标记 {#sample-markup-used-in-this-example}

自定义步骤的标记在 `.content.xml` 组件根节点的。 示例 `.content.xml` 用于此示例：

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

此 `_cq_editConfig.xml` 此示例中使用的示例：

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

此 `_cq_dialog/.content.xml` 此示例中使用的示例：

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
>请注意对话框定义中的常用节点和进程节点。 这些变量继承自我们用作自定义步骤的超类型的流程步骤：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>经典UI模型编辑器对话框仍可与标准的触屏UI编辑器一起使用。
>
>尽管AEM已 [现代化工具](/help/sites-developing/modernization-tools.md) 如果要将经典UI步骤对话框升级到标准UI对话框。 转换后，仍可针对某些情况对对话框进行一些手动改进。
>
>* 如果升级后的对话框为空，您可以在以下位置查看对话框： `/libs` 其功能与如何提供解决方案的示例类似。 例如：
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  您不得修改中的任何内容 `/libs`，只需将它们用作示例。 如果要使用任何现有步骤，请将其复制到 `/apps` 并在那里修改它们。
