---
title: 了解AEM Forms流程
seo-title: 了解AEM Forms流程
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
source-wordcount: '807'
ht-degree: 0%

---

# 了解AEM Forms进程{#understanding-aem-forms-processes}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

一个常见用例是，一组AEM Forms服务要在单个文档上运行。 您可以通过使用Workbench创建流程，将请求发送到服务容器。 流程表示您正在实现自动化的业务流程。 有关创建流程的信息，请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

一旦某个进程被激活，它就会成为一项服务，可以像其他服务一样被调用。 标准服务（如加密服务）与源自进程的服务之间的一个区别是，后者有一个操作可执行许多操作。 相比之下，标准服务有许多操作。 每个操作通常执行一个操作，例如将策略应用于文档或对文档进行加密。

流程可以是短期的，也可以是长期的。 短期进程是同步执行的操作，在从中调用该进程的同一执行线程上执行。 短期操作与大多数编程语言中的标准行为类似，在这些语言中，客户端应用程序调用方法并等待返回值。

但是，在某些情况下，由于以下因素，无法同步完成进程：

* 流程可以跨越大量时间。
* 流程可以跨组织边界。
* 进程需要外部输入才能完成。 例如，假设某个表单被发送到不在办公室的经理。 在这种情况下，在管理器返回并填写表单之前，该过程不会完成。

   这些类型的进程称为长寿命进程。 可以异步执行长时间的过程，允许系统在资源允许的情况下进行交互，并允许跟踪和监视操作。 在调用长寿命进程时，AEM Forms会创建一个调用标识符值作为跟踪长寿命进程状态的记录的一部分。 记录存储在AEM Forms数据库中。 您可以在不再需要长期处理记录时清除这些记录。

>[!NOTE]
>
>AEM Forms在调用短期流程时不会创建记录。

使用调用标识符值，可以跟踪长生命周期进程的状态。 例如，您可以使用进程调用标识符值执行进程管理器操作，如终止正在运行的进程实例。

**短暂的流程示例**

下图是名为&#x200B;*MyApplication/EncryptDocument*&#x200B;的短暂进程的示例。

>[!NOTE]
>
>此过程不基于现有的AEM Forms进程。 要遵循讨论如何调用此过程的代码示例，请使用Workbench创建一个名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

在调用此短暂的进程时，它会执行以下操作：

1. 获取作为输入值传递给流程的不安全PDF文档。
1. 使用密码加密PDF文档。 此进程的输入参数名称为`inDoc`，数据类型为文档。
1. 将密码加密的PDF文档另存为PDF文件，保存到本地文件系统中。 此过程会将加密的PDF文档作为输出值返回。 此进程的输出参数名称为`outDoc`，数据类型为document。

   此过程在从中调用该进程的同一执行线程上同步完成。 此短暂进程的名称为`MyApplication/EncryptDocument`，其操作为`invoke`。

   >[!NOTE]
   >
   >通常，短期流程包含三个以上的操作。 您可以使用Workbench创建流程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

   *使用AEM表*&#x200B;单进行编程介绍了以下方法，您可以通过这些方法以编程方式调用此短暂的流程：

   * [使用AEM Forms Remoting(使用Flex应用程序)通过传递不安全的文档来调用](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) 短暂的进程
   * [使用调用API（Java调用API）调用短时](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) 的进程
   * [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服务示例）
   * [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服务示例）
   * [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服务示例）
   * [通过HTTP使用BLOB数据调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服务示例）
   * [使用DIME调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服务示例）
   * [使用REST调用MyApplication/EncryptDocument进程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**长期处理示例**

下图是一个长期使用的过程的示例。

申请人提交贷款表时，将调用此流程。 在贷款官员批准或拒绝贷款请求之前，该过程无法完成。 此长生命周期进程的名称为&#x200B;*FirstAppSolution/PreLoanProcess*，其操作为`invoke_Async`。 必须异步调用此进程。 有关以编程方式调用此长寿命进程的信息，请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>此过程可按照[创建您的第一个AEM Forms应用程序](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)中指定的教程进行创建。
