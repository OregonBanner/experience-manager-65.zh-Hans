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

AEM提供了多个可用于创建工作流模型的流程步骤。 也可以为内置步骤未涵盖的任务添加自定义流程步骤(请参阅 [创建工作流模型](/help/sites-developing/workflows-models.md))。

## 进程特征 {#process-characteristics}

对于每个处理步骤，将描述以下特征。

### Java类或ECMA路径 {#java-class-or-ecma-path}

流程步骤由Java类或ECMAScript定义。

* 对于Java类进程，提供了完全限定的类名。
* 对于ECMAScript进程，提供了脚本的路径。

### 有效负荷 {#payload}

有效负载是工作流实例执行操作的实体。 有效负载由启动工作流实例的上下文隐式选择。

例如，如果将工作流应用于AEM页面 *P* 则 *P* 随着工作流的进行，会从一个步骤到另一个步骤传递，每个步骤均可选择性地执行以下操作 *P* 在某种程度上。

在大多数情况下，有效负载是存储库中的JCR节点(例如，AEM Page或Asset)。 JCR节点有效负载作为字符串(JCR路径或JCR标识符(UUID))传递。 在某些情况下，有效负载可以是JCR属性（作为JCR路径传递）、URL、二进制对象或通用Java对象。 对有效负载执行操作的各个流程步骤通常需要特定类型的有效负载，或根据有效负载类型采取不同的操作。 对于下面描述的每个进程，都会描述预期的有效负载类型（如果有）。

### 参数 {#arguments}

某些工作流进程接受管理员在设置工作流步骤时指定的参数。

参数将作为单个字符串输入到 **进程参数** 中的属性 **属性** 工作流编辑器的窗格。 对于下面描述的每个过程，参数字符串的格式都用简单的EBNF语法描述。 例如，以下指示参数字符串由一个或多个以逗号分隔的对组成，其中每对由一个名称（一个字符串）和一个值组成，以双冒号分隔：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 超时 {#timeout}

在此超时期限后，工作流步骤不再可操作。 某些工作流进程遵循超时，而其他工作流进程则不应用该超时并被忽略。

### 权限 {#permissions}

会话传递到 `WorkflowProcess` 由工作流进程服务的服务用户支持，该服务用户在存储库的根目录具有以下权限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果该权限集对您的权限不足， `WorkflowProcess` 因此，它必须使用具有所需权限的会话。

建议的方法是使用通过所需权限的子集创建的服务用户。

>[!CAUTION]
>
>如果您从AEM 6.2之前的版本升级，则可能需要更新实施。
>
>在以前的版本中，管理会话传递给 `WorkflowProcess` 实施后，和可以拥有对存储库的完全访问权限，而无需定义特定ACL。
>
>这些权限现在按如上所述进行定义([权限](#permissions))。 这是更新实施的推荐方法。
>
>当代码更改不可行时，还可以使用短期解决方案实现向后兼容性：
>
>* 使用Web控制台( `/system/console/configMgr` 找到 **AdobeGranite工作流配置服务**
>
>* 启用 **工作流进程旧模式**
>
>这将恢复到向提供管理会话的旧行为 `WorkflowProcess` 实施，并再次提供对整个存储库的无限制访问。

## 工作流控制流程 {#workflow-control-processes}

以下流程不会对内容执行任何操作。 它们用于控制工作流本身的行为。

### 绝对时间自动提前器（绝对时间自动提前器） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

此 `AbsoluteTimeAutoAdvancer` （绝对时间自动提前器）进程的行为与 **AutoAdvancer**，只是在给定时间和日期超时，而不是在给定时间长度后超时。

* **Java类**： `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **有效负荷**：无。
* **参数**：无。
* **超时**：达到设置的时间和日期时，流程超时。

### 自动提前器（自动提前器） {#autoadvancer-auto-advancer}

此 `AutoAdvancer` 流程会自动前进到工作流的下一步。 如果有多个可能的下一步（例如，如果存在OR拆分），则此进程将沿以下方向推进工作流 *默认路由*，如果已指定，则不会高级工作流。

* **Java类**： `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **有效负荷**：无。
* **参数**：无。
* **超时**：设置时间长度后进程超时。

### ProcessAssembler（进程汇编程序） {#processassembler-process-assembler}

此 `ProcessAssembler` 进程在单个工作流步骤中按顺序执行多个子进程。 要使用 `ProcessAssembler`，请在工作流中创建此类型的单个步骤，并设置其参数以指示要执行的子进程的名称和参数。

* **Java类**： `com.day.cq.workflow.impl.process.ProcessAssembler`

* **有效负荷**：DAM资产、AEM页面或无有效负载（取决于子流程的要求）。
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

* 从资源中提取元数据。
* 创建三个指定大小的缩略图。
* 假定资源最初既不是GIF也不是PNG(在这种情况下，不创建JPEG)，则从资源创建JPEG图像。
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
>您 ***必须*** 不更改 `/libs` 路径。
>
>这是因为 `/libs` 下次升级实例时将被覆盖（并且在应用修补程序或功能包时可能被覆盖）。

### 删除 {#delete}

给定路径下的项目被删除。

* **ECMAScript路径**： `/libs/workflow/scripts/delete.ecma`

* **有效负荷**： JCR路径
* **参数**：无
* **超时**：已忽略

### noop {#noop}

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

这是一个示例ECMAScript进程。

* **ECMAScript路径**： `/libs/workflow/scripts/sample.ecma`

* **有效负荷**：无
* **参数**：无
* **超时**：已忽略

### 锁定进程 {#lockprocess}

锁定工作流的负载。

* **Java类：** `com.day.cq.workflow.impl.process.LockProcess`

* **有效负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

该步骤在以下情况下不会生效：

* 有效负载已锁定
* 有效负载节点不包含jcr：content子节点

### Unlockprocess {#unlockprocess}

解锁工作流的负载。

* **Java类：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **有效负载：** JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：** 已忽略

该步骤在以下情况下不会生效：

* 有效负载已解锁
* 有效负载节点不包含jcr：content子节点

## 版本控制流程 {#versioning-processes}

以下进程执行与版本相关的任务。

### CreateVersionProcess {#createversionprocess}

创建工作流有效负载(AEM页面或DAM资源)的新版本。

* **Java类**： `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **有效负荷**：引用页面或DAM资源的JCR路径或UUID
* **参数**：无
* **超时**：已尊重
