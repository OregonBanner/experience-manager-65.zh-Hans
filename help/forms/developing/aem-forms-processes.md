---
title: 了解AEM Forms流程
seo-title: Understanding AEM Forms Processes
description: 了解AEM Forms流程
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 了解AEM Forms流程 {#understanding-aem-forms-processes}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

一个常见用例是一组AEM Forms服务在单个文档上运行。 您可以使用Workbench创建流程来向服务容器发送请求。 流程表示您正在自动化的业务流程。 有关创建进程的信息，请参见 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

一旦激活了某个进程，它就会变成一个服务，而且可以像其他服务一样被调用。 标准服务（如加密服务）与源自进程的服务之间的一个区别在于，后者具有一个执行多项操作的操作。 相比之下，标准服务具有许多操作。 每个操作通常执行一项操作，例如将策略应用到文档或加密文档。

进程可以是短期的，也可以是长期的。 短期进程是在从中调用它的同一执行线程上同步执行的操作。 短期操作与大多数编程语言中的标准行为类似，大多数情况下，客户端应用程序会调用方法并等待返回值。

但是，在某些情况下，由于以下因素，进程无法同步完成：

* 一个过程可能持续相当长的时间。
* 一个过程可以跨越组织边界。
* 进程需要外部输入才能完成。 例如，考虑将表单发送给不在办公室的经理的情况。 在这种情况下，只有在经理返回并填写表单后该过程才会完成。

   这些类型的进程称为长期进程。 长期进程是异步执行的，允许系统在资源允许时进行交互，并允许跟踪和监视操作。 在调用长期进程时，AEM Forms会创建一个调用标识符值，作为跟踪长期进程状态的记录的一部分。 该记录存储在AEM Forms数据库中。 您可以在不再需要长期进程记录时清除这些记录。

>[!NOTE]
>
>在调用短期进程时，AEM Forms不会创建记录。

使用调用标识符值，您可以跟踪长生命周期进程的状态。 例如，可以使用进程调用标识符值执行Process Manager操作，如终止正在运行的进程实例。

**短期进程示例**

下图是名为的短暂进程的示例 *MyApplication/EncryptDocument*.

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循以下说明如何调用此进程的代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此短暂的进程时，它将执行以下操作：

1. 获取作为输入值传递给进程的非安全PDF文档。
1. 使用密码加密PDF文档。 此进程的输入参数的名称为 `inDoc` 并且数据类型是文档。
1. 将密码加密的PDF文件作为PDF文件保存到本地文件系统。 此进程将加密的PDF文档作为输出值返回。 此进程的输出参数的名称为 `outDoc` 并且数据类型是文档。

   此进程在从中调用它的同一执行线程上同步完成。 此短暂进程的名称是 `MyApplication/EncryptDocument`它的操作是 `invoke`.

   >[!NOTE]
   >
   >通常，一个短暂的过程包含三个以上的操作。 您可以使用Workbench创建流程。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *使用AEM表单编程*&#x200B;描述了您可以通过以下方式以编程方式调用此短暂的进程：

   * [通过使用AEM Forms Remoting传递不安全的文档来调用短暂的进程](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (使用Flex应用程序)
   * [使用调用API调用短暂的进程](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java调用API）
   * [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服务示例）
   * [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服务示例）
   * [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服务示例）
   * [通过HTTP使用BLOB数据调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服务示例）
   * [使用DIME调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服务示例）
   * [使用REST调用MyApplication/EncryptDocument进程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**长期流程示例**

下图是一个长期过程的示例。

当申请人提交贷款表单时，将调用此流程。 该过程要等到贷款官员批准或拒绝贷款请求后才能完成。 此长期进程的名称为 *FirstAppSolution/PreLoanProcess* 它的操作是 `invoke_Async`. 必须异步调用此进程。 有关以编程方式调用此长期进程的信息，请参见 [调用以人为中心的长期进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>可以按照中指定的教程来创建此流程 [创建您的第一个AEM Forms应用程序](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
