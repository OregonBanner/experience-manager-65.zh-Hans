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
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# 工作流进程引用{#workflow-process-reference}

AEM提供了几个可用于创建工作流模型的流程步骤。 也可以为内置步骤未涵盖的任务添加自定义流程步骤（请参阅[创建工作流模型](/help/sites-developing/workflows-models.md)）。

## 进程特性{#process-characteristics}

对于每个过程步骤，描述了以下特征。

### Java类或ECMA路径{#java-class-or-ecma-path}

进程步骤由Java类或ECMAScript定义。

* 对于Java类进程，提供完全限定的类名称。
* 对于ECMAScript处理脚本的路径。

### 有效负荷 {#payload}

有效负荷是工作流实例对其起作用的实体。 有效负荷由启动工作流实例的上下文隐式选择。

例如，如果工作流应用于AEM页&#x200B;*P*，则随着工作流的推进，会逐步传递&#x200B;*P*，每个步骤都可以选择以某种方式作用在&#x200B;*P*&#x200B;上。

在最常见的情况下，有效负荷是存储库中的JCR节点(例如AEM页面或资产)。 JCR节点有效负荷作为JCR路径或JCR标识符(UUID)的字符串传递。 在某些情况下，有效负荷可以是JCR属性（作为JCR路径传递）、URL、二进制对象或通用Java对象。 对有效负荷起作用的单个进程步骤通常预期某种类型的有效负荷，或根据有效负荷类型采取不同的操作。 对于下面描述的每个过程，将说明预期的有效负荷类型（如果有）。

### 参数 {#arguments}

某些工作流进程接受管理员在设置工作流步骤时指定的参数。

在工作流编辑器的&#x200B;**属性**&#x200B;窗格中，参数作为单个字符串输入在“进程参数”**属性中。**&#x200B;对于下面描述的每个过程，参数字符串的格式以简单的EBNF语法进行描述。 例如，以下指示参数字符串由一个或多个逗号分隔的对组成，其中每对都由名称（即字符串）和值(以多次冒号分隔)组成：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 超时 {#timeout}

在此超时期后，工作流步骤不再可操作。 某些工作流进程会遵守超时，而其他工作流进程则不适用并会被忽略。

### 权限 {#permissions}

传递给`WorkflowProcess`的会话由工作流进程服务的服务用户支持，该服务在存储库的根位置具有以下权限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果该权限集不足于您的`WorkflowProcess`实现，则必须使用具有所需权限的会话。

为此，建议的方法是使用使用所需权限子集（但最少）创建的服务用户。

>[!CAUTION]
>
>如果从AEM 6.2之前的版本升级，则可能需要更新实施。
>
>在以前的版本中，管理员会话被传递到`WorkflowProcess`实现，然后可以拥有对存储库的完全访问权，而无需定义特定ACL。
>
>权限现在定义为以上（[权限](#permissions)）。 同样，更新实现的推荐方法也是如此。
>
>当代码更改不可行时，还提供短期解决方案用于向后兼容：
>
>* 使用Web控制台(`/system/console/configMgr`找到&#x200B;**AdobeGranite工作流配置服务**
   >
   >
* 启用&#x200B;**工作流进程传统模式**
>
>
这将恢复为向`WorkflowProcess`实施提供管理会话的旧行为，并再次提供对整个存储库的无限制访问。

## 工作流控制进程{#workflow-control-processes}

以下进程不对内容执行任何操作。 它们用于控制工作流本身的行为。

### AbsoluteTimeAutoAdvancer（绝对时间自动提前器）{#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（绝对时间自动提前器）进程对&#x200B;**AutoAdvancer**&#x200B;的行为相同，只是它在给定时间和日期超时，而不是在给定时间长度后超时。

* **Java类**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **有效负荷**:没有。
* **参数**:没有。
* **超时**:到达设置的时间和日期时，进程超时。

### AutoAdvancer（自动提前器）{#autoadvancer-auto-advancer}

`AutoAdvancer`进程会自动将工作流前进到下一步。 如果有多个可能的下一步（例如，如果存在OR拆分），则此进程将沿&#x200B;*默认路由*&#x200B;推进工作流，如果已指定，则不会进行工作流高级。

* **Java类**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **有效负荷**:没有。
* **参数**:没有。
* **超时**:在设定的时间长度后，处理超时。

### ProcessAssembler(Process Assembler){#processassembler-process-assembler}

`ProcessAssembler`进程在一个工作流步骤中按顺序执行多个子进程。 要使用`ProcessAssembler`，请在工作流中创建此类型的单个步骤，并设置其参数以指示要执行的子进程的名称和参数。

* **Java类**:  `com.day.cq.workflow.impl.process.ProcessAssembler`

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

* **超时**:受人尊重。

例如：

* 从资产中提取元数据。
* 创建三个指定大小的三个缩略图。
* 根据资产创建JPEG图像，假定资产最初既不是GIF也不是PNG（在这种情况下，不会创建JPEG）。
* 设置资产的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本进程{#basic-processes}

以下过程执行简单的任务或作为示例。

>[!CAUTION]
>
>您&#x200B;***必须***&#x200B;不要更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（应用修补程序或功能包时，可能会被覆盖）。

### 删除 {#delete}

将删除给定路径上的项。

* **ECMAScript路径**:  `/libs/workflow/scripts/delete.ecma`

* **有效负荷**:JCR路径
* **参数**:无
* **超时**:已忽略

### noop {#noop}

这是空进程。 它不执行任何操作，但会记录调试消息。

* **ECMAScript路径**:  `/libs/workflow/scripts/noop.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### rule-false {#rule-false}

这是一个在`check()`方法上返回`false`的空进程。

* **ECMAScript路径**:  `/libs/workflow/scripts/rule-false.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### 示例{#sample}

这是一个示例ECMAScript进程。

* **ECMAScript路径**:  `/libs/workflow/scripts/sample.ecma`

* **有效负荷**:无
* **参数**:无
* **超时**:已忽略

### urlcaller {#urlcaller}

这是一个调用给定URL的简单工作流程。 通常，URL将是对执行简单任务的JSP（或其他Servlet等效项）的引用。 此过程仅应在开发和演示时使用，而不应在生产环境中使用。 参数指定URL、登录名和口令。

* **ECMAScript路径**:  `/libs/workflow/scripts/urlcaller.ecma`

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

* **Java类：** `com.day.cq.workflow.impl.process.LockProcess`

* **有效负** 荷：JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：已忽** 略

该步骤在下列情况下并无影响：

* 负载已锁定
* 有效负荷节点不包含jcr:content子节点

### UnlockProcess {#unlockprocess}

解锁工作流的有效负荷。

* **Java类：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **有效负** 荷：JCR_PATH和JCR_UUID
* **参数：** 无
* **超时：已忽** 略

该步骤在下列情况下并无影响：

* 有效负荷已解锁
* 有效负荷节点不包含jcr:content子节点

## 版本控制进程{#versioning-processes}

以下过程执行与版本相关的任务。

### CreateVersionProcess {#createversionprocess}

创建工作流有效负荷的新版本(AEM页面或DAM资产)。

* **Java类**:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **有效负荷**:引用页面或DAM资产的JCR路径或UUID
* **参数**:无
* **超时**:受尊重

