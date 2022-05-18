---
title: 工作流过程参考
seo-title: Workflow Process Reference
description: 工作流过程参考
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: cf3b739fd774bc860d9906b9884d22fd532fd5dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# 工作流过程参考{#workflow-process-reference}

AEM提供了几个可用于创建工作流模型的流程步骤。 对于内置步骤未涵盖的任务，还可以添加自定义流程步骤(请参阅 [创建工作流模型](/help/sites-developing/workflows-models.md))。

## 过程特性 {#process-characteristics}

对于每个过程步骤，描述了以下特征。

### Java类或ECMA路径 {#java-class-or-ecma-path}

流程步骤由Java类或ECMAScript定义。

* 对于Java类进程，提供完全限定的类名称。
* 对于ECMAScript，会提供脚本的路径。

### 有效负荷 {#payload}

有效负载是工作流实例对其执行操作的实体。 有效负载由启动工作流实例的上下文隐式选择。

例如，如果将工作流应用于AEM页面 *P* then *P* 会随着工作流的进行逐步传递，每个步骤都可以选择在执行时执行 *P* 在某种程度上。

在最常见的情况下，有效负载是存储库中的JCR节点(例如，AEM页面或资产)。 JCR节点有效负载作为JCR路径或JCR标识符(UUID)的字符串传递。 在某些情况下，有效负载可能是JCR属性（作为JCR路径传递）、URL、二进制对象或通用Java对象。 对有效负载采取行动的单个进程步骤通常期望有特定类型的有效负载，或根据有效负载类型采取不同的行动。 对于下面描述的每个流程，都描述了预期的有效负载类型（如果有）。

### 参数 {#arguments}

某些工作流会处理接受管理员在设置工作流步骤时指定的参数。

参数在 **进程参数** 属性 **属性** 工作流编辑器窗格。 对于下面描述的每个过程，参数字符串的格式以简单的EBNF语法进行描述。 例如，以下表示参数字符串由一个或多个以逗号分隔的对组成，其中每对都由名称（即字符串）和值（用双冒号分隔）组成：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 超时 {#timeout}

在此超时时间段后，工作流步骤不再可操作。 某些工作流进程会遵守超时，而对于其他工作流进程，则不会应用超时，因此会被忽略。

### 权限 {#permissions}

传递给的会话 `WorkflowProcess` 由服务用户为工作流进程服务提供支持，该服务在存储库的根下具有以下权限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果这组权限不足以满足您的 `WorkflowProcess` 实施，则必须使用具有所需权限的会话。

要实现此目的，建议使用创建的具有所需权限子集的必要（但最小）服务用户。

>[!CAUTION]
>
>如果您从AEM 6.2之前的版本升级，则可能需要更新实施。
>
>在以前的版本中，管理员会话被传递到 `WorkflowProcess` 实施和之后可以拥有对存储库的完全访问权限，而无需定义特定的ACL。
>
>权限现在定义如下([权限](#permissions))。 与更新实施的推荐方法相同。
>
>当代码更改不可行时，还会出于向后兼容性目的提供短期解决方案：
>
>* 使用Web控制台( `/system/console/configMgr` 找到 **AdobeGranite工作流配置服务**
>
>* 启用 **工作流进程旧版模式**
>
>这将还原为向提供管理员会话的旧行为 `WorkflowProcess` 实施，并再次提供对整个存储库的无限制访问。

## 工作流控制流程 {#workflow-control-processes}

以下进程不会对内容执行任何操作。 它们用于控制工作流本身的行为。

### AbsoluteTimeAutoAdvancer（绝对时间自动提前器） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

的 `AbsoluteTimeAutoAdvancer` （绝对时间自动提前器）进程的行为与 **AutoAdvancer**，但是它会在给定的时间和日期超时，而不是在给定的时长后超时。

* **Java类**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **负载**:无。
* **参数**:无。
* **超时**:达到设置的时间和日期后，处理超时。

### AutoAdvancer(Auto Advancer) {#autoadvancer-auto-advancer}

的 `AutoAdvancer` 进程会自动将工作流推进到下一步。 如果有多个可能的下一步（例如，如果存在OR拆分），则此流程将沿 *默认路线*，如果已指定，则不会高级工作流。

* **Java类**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **负载**:无。
* **参数**:无。
* **超时**:在设置的时长后，处理超时。

### ProcessAssembler（进程汇编程序） {#processassembler-process-assembler}

的 `ProcessAssembler` 进程在单个工作流步骤中按顺序执行多个子进程。 使用 `ProcessAssembler`，在工作流中创建此类型的单个步骤，并设置其参数以指示要执行的子进程的名称和参数。

* **Java类**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **负载**:DAM资产、AEM页面或无有效负载（取决于子流程的要求）。
* **参数**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **超时**:尊重。

例如：

* 从资产中提取元数据。
* 创建三个指定大小的缩略图。
* 从资产创建JPEG图像，假定资产最初既不是GIF也不是PNG(在这种情况下，不会创建JPEG)。
* 设置资产的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

以下流程执行简单任务或作为示例。

>[!CAUTION]
>
>您 ***必须*** 不会更改 `/libs` 路径。
>
>这是因为 `/libs` 在下次升级实例时被覆盖（在应用修补程序或功能包时可能会被覆盖）。

### 删除 {#delete}

将删除给定路径上的项目。

* **ECMAScript路径**: `/libs/workflow/scripts/delete.ecma`

* **负载**:JCR路径
* **参数**:无
* **超时**:已忽略

### noop {#noop}

这是空进程。 它不执行任何操作，但会记录调试消息。

* **ECMAScript路径**: `/libs/workflow/scripts/noop.ecma`

* **负载**:无
* **参数**:无
* **超时**:已忽略

### rule-false {#rule-false}

这是一个返回的空进程 `false` 在 `check()` 方法。

* **ECMAScript路径**: `/libs/workflow/scripts/rule-false.ecma`

* **负载**:无
* **参数**:无
* **超时**:已忽略

### 样本 {#sample}

这是ECMAScript过程示例。

* **ECMAScript路径**: `/libs/workflow/scripts/sample.ecma`

* **负载**:无
* **参数**:无
* **超时**:已忽略

### LockProcess {#lockprocess}

锁定工作流的有效负载。

* **Java类：** `com.day.cq.workflow.impl.process.LockProcess`

* **负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

该步骤在下列情况下无效：

* 负载已锁定
* 有效负荷节点不包含jcr:content子节点

### UnlockProcess {#unlockprocess}

解锁工作流的有效负载。

* **Java类：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

该步骤在下列情况下无效：

* 有效负载已解锁
* 有效负荷节点不包含jcr:content子节点

## 版本控制流程 {#versioning-processes}

以下进程将执行与版本相关的任务。

### CreateVersionProcess {#createversionprocess}

创建工作流有效负载的新版本(AEM页面或DAM资产)。

* **Java类**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **负载**:引用页面或DAM资产的JCR路径或UUID
* **参数**:无
* **超时**:受尊重
