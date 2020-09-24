---
title: 理解AEM Forms进程
seo-title: 理解AEM Forms进程
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---


# 理解AEM Forms进程 {#understanding-aem-forms-processes}

一个常见用例是在单一文档上运行一组AEM Forms服务。 您可以使用工作台创建流程，将请求发送到服务容器。 流程代表您要实现自动化的业务流程。 有关创建流程的信息，请参 [阅使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

一旦某个进程被激活，它就变成一个服务，可以像其他服务一样被调用。 标准服务（如加密服务）和源自进程的服务之间的一个区别是后者有一个操作，它执行许多操作。 相反，标准服务具有许多操作。 每个操作通常执行一个操作，如将策略应用于文档或加密文档。

过程可以是短期的，也可以是长期的。 短时进程是同步执行的操作，从中调用它的同一执行线程。 短时操作与大多数编程语言中的标准行为类似，在这些语言中，客户端应用程序调用方法并等待返回值。

但是，存在以下情况：由于以下因素，进程无法同步完成：

* 一个过程可以跨越大量时间。
* 流程可以跨越组织界限。
* 进程需要外部输入才能完成。 例如，考虑将表单发送给不在办公室的经理的情况。 在这种情况下，只有经理返回并填写表单后，该过程才会完成。

   这些类型的过程称为长寿命过程。 异步执行长寿命进程，允许系统作为资源允许进行交互，并允许跟踪和监视操作。 当调用长寿命进程时，AEM Forms将创建调用标识符值作为跟踪长寿命进程状态的记录的一部分。 记录存储在AEM Forms数据库中。 您可以在不再需要长期处理记录时清除它们。

>[!NOTE]
>
>AEM Forms在调用短期进程时不会创建记录。

使用调用标识符值，您可以跟踪长寿命进程的状态。 例如，您可以使用进程调用标识符值执行进程管理器操作，如终止正在运行的进程实例。

**短寿命过程示例**

下图是名为MyApplication/EncryptDocument的短时 *进程示例*。

>[!NOTE]
>
>这一进程不是基于AEM Forms现有进程。 要跟随讨论如何调用此流程的代码示例，请使用Workbench创建一个名为 `MyApplication/EncryptDocument` 的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此短时进程时，它将执行以下操作：

1. 获取作为输入值传递到流程的不安全PDF文档。
1. 用密码加密PDF文档。 此进程的输入参数的名称为， `inDoc` 数据类型为文档。
1. 将密码加密的PDF文档另存为PDF文件保存到本地文件系统。 此过程将返回加密的PDF文档作为输出值。 此进程的输出参数名称为， `outDoc` 数据类型为文档。

   此进程在从中调用它的同一执行线程上同步完成。 这个短期过程的名称是， `MyApplication/EncryptDocument`其操作是 `invoke`。

   >[!NOTE]
   >
   >通常，短期流程包含三个以上的操作。 您可以使用Workbench创建流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

   *使用AEM表*&#x200B;格进行编程介绍以下方法，通过这些方法，您可以以编程方式调用此短期流程：

   * [使用AEM Forms·远程处理(使用Flex应用程序)通过不安全的文档](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) ，调用短时过程。
   * [使用调用API(Java调用API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) )调用短时进程
   * [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服务示例）
   * [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服务示例）
   * [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服务示例）
   * [通过HTTP使用BLOB数据调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服务示例）
   * [使用DIME调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服务示例）
   * [使用REST调用MyApplication/EncryptDocument进程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**长寿命过程实例**

下图是一个长寿命过程的示例。

申请人提交贷款表时将调用此流程。 在贷款官员批准或拒绝贷款请求之前，该过程不会完成。 此长期流程的名称为 *FirstAppSolution/PreLoanProcess* ，其操作为 `invoke_Async`。 必须异步调用此进程。 有关以编程方式调用此长寿命进程的信息，请 [参阅调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>可以按照创建您的第一个AEM Forms应用程序中 [指定的教程创建此过程](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。