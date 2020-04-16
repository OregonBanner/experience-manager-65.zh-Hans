---
title: 了解AEM Forms流程
seo-title: 了解AEM Forms流程
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 了解AEM Forms流程 {#understanding-aem-forms-processes}

一个常见用例是针对一组AEM Forms服务在单个文档上操作。 您可以通过使用Workbench创建流程，将请求发送到服务容器。 流程代表您正在自动处理的业务流程。 有关创建进程的信息，请参 [阅使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

一旦过程被激活，它就会成为服务，并且可以像其他服务一样被调用。 标准服务（如加密服务）和源自进程的服务之间的一个区别是后者有一个执行许多操作的操作。 相反，标准服务具有许多操作。 每个操作通常执行一个操作，例如将策略应用于文档或加密文档。

过程可以是短期的，也可以是长期的。 短时进程是同步执行的操作以及从中调用它的同一执行线程。 短期操作与大多数编程语言中的标准行为类似，在这些语言中，客户端应用程序调用方法并等待返回值。

但是，在某些情况下，由于以下因素，进程无法同步完成：

* 一个过程可以跨越大量时间。
* 一个流程可以跨越组织界限。
* 进程需要外部输入才能完成。 例如，考虑将表单发送给不在办公室的经理的情况。 在这种情况下，只有经理返回并填写表单后，该过程才会完成。

   这些类型的进程称为长期进程。 以异步方式执行长期进程，允许系统在资源允许的情况下进行交互，并允许跟踪和监视操作。 当调用长期进程时，AEM Forms会创建一个调用标识符值，作为跟踪长期进程状态的记录的一部分。 记录存储在AEM Forms数据库中。 您可以在不再需要长期流程记录时清除这些记录。

>[!NOTE]
>
>在调用短时间进程时，AEM Forms不会创建记录。

使用调用标识符值，您可以跟踪长寿命进程的状态。 例如，您可以使用进程调用标识符值来执行进程管理器操作，如终止正在运行的进程实例。

**短时过程示例**

下图是一个名为MyApplication/EncryptDocument的短时 *间进程示例*。

>[!NOTE]
>
>此过程不基于现有的AEM Forms流程。 要跟踪讨论如何调用此进程的代码示例，请使用Workbench创建一个名 `MyApplication/EncryptDocument` 为的进程。 (请参 [阅使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此短期进程时，它将执行以下操作：

1. 获取作为输入值传递给流程的无担保PDF文档。
1. 使用密码加密PDF文档。 此进程的输入参数名称为， `inDoc` 数据类型为文档。
1. 将密码加密的PDF文档另存为PDF文件到本地文件系统。 此过程将加密的PDF文档返回为输出值。 此进程的输出参数的名称是， `outDoc` 数据类型是文档。

   此进程在从中调用它的同一执行线程上同步完成。 这个短期过程的名称是， `MyApplication/EncryptDocument`其操作是 `invoke`。

   >[!NOTE]
   >
   >通常，短期流程由三个以上的操作组成。 您可以使用Workbench创建流程。 (请参 [阅使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

   *使用AEM格式进*&#x200B;行编程介绍了以下方法，通过这些方法，您可以有计划地调用此短期流程：

   * [通过使用AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) （使用Flex应用程序）通过传递不安全的文档来调用短时过程
   * [使用调用API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java调用API）调用短期进程
   * [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服务示例）
   * [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服务示例）
   * [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服务示例）
   * [通过HTTP使用BLOB数据调用AEM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) Forms（Web服务示例）
   * [使用DIME调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服务示例）
   * [使用REST调用MyApplication/EncryptDocument进程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**长寿命过程示例**

下图是一个长期进程的示例。

申请人提交贷款表时会调用此过程。 在贷款官员批准或拒绝贷款申请之前，该程序尚未完成。 此长期流程的名称为 *FirstAppSolution/PreLoanProcess* ，其操作为 `invoke_Async`。 必须异步调用此进程。 有关以编程方式调用此长寿命进程的信息，请 [参阅调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>可以按照创建您的第一个AEM Forms应用程序中指 [定的教程创建此过程](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。