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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# 了解AEM Forms进程{#understanding-aem-forms-processes}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

一个常见用例是一组AEM Forms服务在单个文档上运行。 您可以通过使用Workbench创建流程，将请求发送到服务容器。 流程代表您要自动处理的业务流程。 有关创建进程的信息，请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

激活某个进程后，该进程将变为一个服务，可以像调用其他服务一样调用它。 标准服务（如加密服务）与源自进程的服务之间的一个区别是，后者有一个操作，可执行多个操作。 相反，标准服务有许多操作。 每个操作通常执行一个操作，如将策略应用于文档或加密文档。

过程可以是短命的，也可以是长命的。 短时进程是同步执行的操作，并在调用该进程的同一执行线程上执行。 短期操作与大多数编程语言中的标准行为类似，在这些语言中，客户端应用程序调用方法并等待返回值。

但是，有时由于以下因素无法同步完成进程：

* 一个过程可以跨越大量时间。
* 一个过程可以跨越组织边界。
* 进程需要外部输入才能完成。 例如，考虑将表单发送给不在办公室的经理的情况。 在这种情况下，只有经理返回并填写表单后，该过程才会完成。

   这些类型的进程称为长寿命进程。 以异步方式执行长期处理，允许系统在资源允许的情况下进行交互，并允许跟踪和监视操作。 调用长寿命进程时，AEM Forms会创建一个调用标识符值，作为跟踪长寿命进程状态的记录的一部分。 记录存储在AEM Forms数据库中。 您可以在长期流程记录不再需要时清除它们。

>[!NOTE]
>
>AEM Forms在调用短时间进程时不创建记录。

使用调用标识符值，您可以跟踪长寿命进程的状态。 例如，您可以使用进程调用标识符值来执行进程管理器操作，如终止正在运行的进程实例。

**短时过程示例**

下图是名为&#x200B;*MyApplication/EncryptDocument*&#x200B;的短期进程的示例。

>[!NOTE]
>
>此过程不基于现有的AEM Forms进程。 要与讨论如何调用此进程的代码示例一起，请使用Workbench创建一个名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

调用此短期进程时，将执行以下操作：

1. 获取作为输入值传递给流程的不安全PDF文档。
1. 使用密码加密PDF文档。 此进程的输入参数名称为`inDoc`，数据类型为文档。
1. 将密码加密的PDF文档另存为PDF文件保存到本地文件系统。 此过程将加密的PDF文档返回为输出值。 此进程的输出参数名称为`outDoc`，数据类型为文档。

   此进程在调用该进程的同一执行线程上同步完成。 此短期进程的名称为`MyApplication/EncryptDocument`，其操作为`invoke`。

   >[!NOTE]
   >
   >通常，短期的过程包含三个以上的操作。 您可以使用Workbench创建流程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

   *使用AEM表*&#x200B;单进行编程介绍以下方法，您可以通过这些方法以编程方式调用此短时过程：

   * [使用AEM Forms Remoting(使用Flex应用程序)通过传递不安全的文档](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) ，调用短时的进程
   * [使用调用API(Java调用API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) )调用短时进程
   * [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服务示例）
   * [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服务示例）
   * [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服务示例）
   * [通过HTTP使用BLOB数据调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服务示例）
   * [使用DIME调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服务示例）
   * [使用REST调用MyApplication/EncryptDocument进程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**长寿命的过程示例**

下图是一个长期进程的示例。

申请人提交贷款表时将调用此过程。 在贷款官员批准或拒绝贷款请求之前，该程序不会完成。 此长期进程的名称为&#x200B;*FirstAppSolution/PreLoanProcess*，其操作为`invoke_Async`。 必须异步调用此进程。 有关以编程方式调用此长寿命进程的信息，请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>可以按照[创建您的第一个AEM Forms应用程序](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)中指定的教程创建此过程。