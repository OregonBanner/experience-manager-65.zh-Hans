---
title: 工作流进程参考
seo-title: 工作流进程参考
description: 'null'
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 工作流进程参考{#workflow-process-reference}

AEM提供了几个可用于创建工作流模型的流程步骤。 也可以为内置步骤未涵盖的任务添加自定义流程步骤(请参阅创 [建工作流模型](/help/sites-developing/workflows-models.md))。

## 进程特性 {#process-characteristics}

对于每个过程步骤，描述了以下特性。

### Java类或ECMA路径 {#java-class-or-ecma-path}

进程步骤由Java类或ECMAScript定义。

* 对于Java类进程，提供完全限定的类名称。
* 对于ECMAScript处理，将提供指向脚本的路径。

### 有效负荷 {#payload}

有效负荷是工作流实例对其起作用的实体。 有效负荷由启动工作流实例的上下文隐式选择。

例如，如果将工作流应用于AEM页面 *P* ，则随着工作流的前进，P *将逐步传递，每个步骤可选地以某种方式对* P ** 执行操作。

在最常见的情况下，有效负荷是存储库中的JCR节点（例如，AEM页面或资产）。 JCR节点有效负荷作为JCR路径或JCR标识符(UUID)的字符串传递。 在某些情况下，有效负荷可能是JCR属性（作为JCR路径传递）、URL、二进制对象或通用Java对象。 对有效负荷起作用的单个进程步骤通常期望某种类型的有效负荷，或根据有效负荷类型采取不同的操作。 对于下面描述的每个进程，将说明期望的有效负荷类型（如果有）。

### 参数 {#arguments}

某些工作流进程接受管理员在设置工作流步骤时指定的参数。

参数在工作流编辑器的“属性”窗格 **的“进程参数** ”属性中 **以单个字符串的形式输入** 。 对于下面描述的每个过程，参数字符串的格式在简单的EBNF语法中进行了说明。 例如，下面指示参数字符串由一个或多个逗号分隔的对组成，其中每对都由一个名称（即字符串）和一个由双冒号分隔的值组成：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 超时 {#timeout}

在此超时期后，工作流步骤不再可操作。 某些工作流进程会遵守超时，而其他工作流进程则不会应用并被忽略。

### 权限 {#permissions}

传递给会话的会 `WorkflowProcess` 话由工作流进程服务的服务用户备份，该服务在存储库的根位置具有以下权限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果这组权限不足以实现您的 `WorkflowProcess` 实现，则它必须使用具有所需权限的会话。

为此，建议的方法是使用创建的服务用户所需权限子集，但权限子集最少。

>[!CAUTION]
>
>如果您是从AEM 6.2之前的版本升级，则可能需要更新您的实施。
>
>在以前的版本中，管理员会话被传递到实 `WorkflowProcess` 施中，然后可以拥有对存储库的完全访问权限，而无需定义特定ACL。
>
>权限现在定义为上述(权[限](#permissions))。 同样，更新实现的推荐方法也是如此。
>
>当代码更改不可行时，短期解决方案也可用于向后兼容性目的：
>
>* 使用Web控制台( `/system/console/configMgr` 找到 **Adobe Granite Workflow Configuration Service**
   >
   >
* 启用工作 **流进程传统模式**
>
>
这将恢复为向实施提供管理员会话的旧行为， `WorkflowProcess` 并再次提供对整个存储库的无限制访问。

## 工作流控制进程 {#workflow-control-processes}

以下进程不对内容执行任何操作。 它们用于控制工作流本身的行为。

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

“ `AbsoluteTimeAutoAdvancer` 绝对时间自动提前器”(Absolute Time Auto Advancer)进程与 **** AutoAdvancer的行为相同，只是它在给定时间和日期超时，而不是在给定时间长度后超时。

* **Java类**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **有效负荷**:没有。
* **参数**:没有。
* **超时**:到达设置的时间和日期后的进程超时。

### AutoAdvancer(Auto Advancer) {#autoadvancer-auto-advancer}

该过 `AutoAdvancer` 程会自动将工作流前进到下一步。 如果有多个可能的下一步（例如，如果有OR拆分），则此进程将沿着默认路径推进工作流 *，如果已指定该步骤*，否则将不进行工作流。

* **Java类**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **有效负荷**:没有。
* **参数**:没有。
* **超时**:在设定的时间长度后，处理超时。

### ProcessAssembler（进程汇编器） {#processassembler-process-assembler}

该过 `ProcessAssembler` 程在一个工作流步骤中顺序地执行多个子进程。 要使用该 `ProcessAssembler`功能，请在工作流中创建一个此类型的步骤，并设置其参数以指示要执行的子进程的名称和参数。

* **Java类**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **有效负荷**:DAM资产、AEM页面或无有效负荷（取决于子流程的要求）。
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

* **超时**:受尊敬。

例如：

* 从资产中提取元数据。
* 创建三个指定大小的缩览图。
* 根据资产创建JPEG图像，假定资产最初既不是GIF也不是PNG（在这种情况下，不会创建JPEG）。
* 设置资产的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

以下过程执行简单任务或作为示例。

>[!CAUTION]
>
>您 ***不得*** 更改路径中的任 `/libs` 何内容。
>
>这是因为下次升级实 `/libs` 例时，将覆盖其内容（应用修补程序或功能包时，可能会覆盖该内容）。

### 删除 {#delete}

将删除给定路径上的项目。

* **ECMAScript路径**: `/libs/workflow/scripts/delete.ecma`

* **有效负荷**:JCR路径
* **参数**:无
* **超时**:已忽略

### noop {#noop}

这是空进程。 它不执行任何操作，但会记录调试消息。

* **ECMAScript路径**: `/libs/workflow/scripts/noop.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### 规则假 {#rule-false}

这是一个在方法上返回 `false` 的空进 `check()` 程。

* **ECMAScript路径**: `/libs/workflow/scripts/rule-false.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### sample {#sample}

这是一个ECMAScript进程示例。

* **ECMAScript路径**: `/libs/workflow/scripts/sample.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### urlcaller {#urlcaller}

这是一个调用给定URL的简单工作流程。 通常，URL将是对执行简单任务的JSP（或其他Servlet等效项）的引用。 此过程仅应在开发和演示过程中使用，而不应在生产环境中使用。 参数指定URL、登录名和口令。

* **ECMAScript路径**: `/libs/workflow/scripts/urlcaller.ecma`

* **有效负荷**:无
* **参数**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例如：`http://localhost:4502/my.jsp, mylogin, mypassword`

* **超时**:已忽略

### LockProcess {#lockprocess}

锁定工作流的有效负荷。

* **** Java类： `com.day.cq.workflow.impl.process.LockProcess`

* **** 有效负荷：JCR_PATH和JCR_UUID
* **** 参数：无
* **** 超时：已忽略

该步骤在下列情况下无效：

* 有效负荷已锁定
* 有效负荷节点不包含jcr:content子节点

### UnlockProcess {#unlockprocess}

解锁工作流的有效负荷。

* **** Java类： `com.day.cq.workflow.impl.process.UnlockProcess`

* **** 有效负荷：JCR_PATH和JCR_UUID
* **** 参数：无
* **** 超时：已忽略

该步骤在下列情况下无效：

* 有效负荷已解锁
* 有效负荷节点不包含jcr:content子节点

## 版本控制流程 {#versioning-processes}

以下过程执行与版本相关的任务。

### CreateVersionProcess {#createversionprocess}

创建工作流有效负荷的新版本（AEM页面或DAM资产）。

* **Java类**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **有效负荷**:引用页面或DAM资产的JCR路径或UUID
* **参数**:无
* **超时**:受尊重

