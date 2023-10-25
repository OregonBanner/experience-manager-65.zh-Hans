---
title: 工作流过程参考
description: 有关Adobe Experience Manager中的工作流，请参阅此流程参考。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 1%

---

# 工作流过程参考{#workflow-process-reference}

AEM提供了多个可用于创建工作流模型的流程步骤。 也可以为内置步骤未涵盖的任务添加自定义流程步骤(请参阅 [创建工作流模型](/help/sites-developing/workflows-models.md))。

## 流程特征 {#process-characteristics}

对于每个工艺步骤，描述了以下特征。

### Java™类或ECMA路径 {#java-class-or-ecma-path}

进程步骤由Java™类或ECMAScript定义。

* 对于Java™类进程，提供了完全限定的类名。
* 对于ECMAScript进程，提供脚本的路径。

### 有效负荷 {#payload}

有效负载是工作流实例执行操作的实体。 有效负载由启动工作流实例的上下文隐式选择。

例如，如果将工作流应用于AEM页面 *P* 则 *P* 随着工作流的进行，会逐个传递，每个步骤均会选择性地执行以下操作 *P* 以某种方式。

在大多数情况下，有效负载是存储库中的JCR节点(例如，AEM页面或Asset)。 JCR节点有效负载作为字符串(JCR路径或JCR标识符(UUID))传递。 有时，有效负载可以是JCR属性（作为JCR路径传递）、URL、二进制对象或通用Java™对象。 对有效负载执行操作的各个流程步骤通常需要特定类型的有效负载，或根据有效负载类型执行不同的操作。 对于下面描述的每个进程，将介绍预期的有效负载类型（如果有）。

### 参数 {#arguments}

某些工作流进程接受管理员在设置工作流步骤时指定的参数。

参数将作为单个字符串输入到 **进程参数** 中的属性 **属性** 工作流编辑器的窗格。 对于下面描述的每个过程，参数字符串的格式都用简单的EBNF语法描述。 例如，下面指示参数字符串由一个或多个逗号分隔对组成，其中每对由名称（即字符串）和值组成，并以双冒号分隔：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 超时 {#timeout}

在此超时时段后，工作流步骤不再可操作。 某些工作流进程遵循超时，而其他工作流进程则不应用超时并将其忽略。

### 权限 {#permissions}

会话传递到 `WorkflowProcess` 由工作流进程服务的服务用户支持，该服务用户在存储库的根目录具有以下权限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果这组权限不足以满足 `WorkflowProcess` 实施，则必须使用具有所需权限的会话。

为此，建议的方法是使用创建的具有所需权限的子集的服务用户。

>[!CAUTION]
>
>如果您是从AEM 6.2之前的版本升级，则可能需要更新实施。
>
>在以前的版本中，管理员会话传递给 `WorkflowProcess` 实施后，即可完全访问存储库，而无需定义特定ACL。
>
>权限现在如上定义([权限](#permissions))。 这是更新实施的推荐方法。
>
>当代码更改不可行时，还可以使用短期解决方案实现向后兼容性：
>
>* 使用Web控制台( `/system/console/configMgr` 找到 **AdobeGranite工作流配置服务**
>
>* 启用 **工作流进程旧模式**
>
>这将还原为向提供管理会话的旧行为 `WorkflowProcess` 实施，并再次提供对整个存储库的无限制访问。

## 工作流控制流程 {#workflow-control-processes}

以下流程不会对内容执行任何操作。 它们用于控制工作流本身的行为。

### AbsoluteTimeAutoAdvancer（绝对时间自动提前器） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

此 `AbsoluteTimeAutoAdvancer` (Absolute Time Auto Advancer)进程的行为与 **自动提前器**，只是在给定时间和日期超时，而不是在给定时间长度后超时。

* **Java™类**： `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **有效负荷**：无。
* **参数**：无。
* **超时**：达到设置的时间和日期时，流程会超时。

### 自动提前器（自动提前器） {#autoadvancer-auto-advancer}

此 `AutoAdvancer` 流程会自动前进到工作流的下一步。 如果有多个可能的下一步（例如，如果存在OR拆分），则此进程将沿以下方向推进工作流 *默认路由*，如果已指定，则不会高级工作流。

* **Java™类**： `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **有效负荷**：无。
* **参数**：无。
* **超时**：设置时间长度后进程超时。

### ProcessAssembler（进程汇编程序） {#processassembler-process-assembler}

此 `ProcessAssembler` 进程在单个工作流步骤中按顺序执行多个子进程。 要使用 `ProcessAssembler`，请在工作流中创建此类型的单个步骤，并设置其参数以指示要执行的子进程的名称和参数。

* **Java™类**： `com.day.cq.workflow.impl.process.ProcessAssembler`

* **有效负荷**：DAM资源、AEM页面或无有效负载（取决于子流程的要求）。
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

* **超时**：已尊重。

例如：

* 从资源提取元数据。
* 创建三种指定大小的缩略图。
* 假设资源最初不是GIF或PNG(在这种情况下，不会创建JPEG)，则从资源创建JPEG图像。
* 设置资源的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

以下进程执行简单任务或作为示例。

>[!CAUTION]
>
>请勿更改 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（应用修补程序或功能包时可能会被覆盖）。

### 删除 {#delete}

给定路径下的项目被删除。

* **ECMAScript路径**： `/libs/workflow/scripts/delete.ecma`

* **有效负荷**： JCR路径
* **参数**：无
* **超时**：已忽略

### 空位 {#noop}

这是空进程。 它不执行任何操作，但会记录调试消息。

* **ECMAScript路径**： `/libs/workflow/scripts/noop.ecma`

* **有效负荷**：无
* **参数**：无
* **超时**：已忽略

### rule-false {#rule-false}

这是一个返回的null进程 `false` 在 `check()` 方法。

* **ECMAScript路径**： `/libs/workflow/scripts/rule-false.ecma`

* **有效负荷**：无
* **参数**：无
* **超时**：已忽略

### 示例 {#sample}

这是ECMAScript进程的一个示例。

* **ECMAScript路径**： `/libs/workflow/scripts/sample.ecma`

* **有效负荷**：无
* **参数**：无
* **超时**：已忽略

### 锁定进程 {#lockprocess}

锁定工作流的负载。

* **Java™类：** `com.day.cq.workflow.impl.process.LockProcess`

* **有效负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

在下列情况下，该步骤不生效：

* 有效负载已锁定
* 有效负载节点不包含jcr：content子节点

### Unlockprocess {#unlockprocess}

解锁工作流的负载。

* **Java™类：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **有效负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

在下列情况下，该步骤不生效：

* 有效负载已解锁
* 有效负载节点不包含jcr：content子节点

## 版本控制流程 {#versioning-processes}

以下进程执行与版本相关的任务。

### CreateVersionProcess {#createversionprocess}

创建工作流有效负载的版本(AEM页面或DAM资源)。

* **Java™类**： `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **有效负荷**：引用页面或DAM资源的JCR路径或UUID
* **参数**：无
* **超时**：已尊重
