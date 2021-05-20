---
title: 记录自定义实施的交易
seo-title: 记录自定义实施的交易
description: 使用TransactionRecorder API记录未自动入帐为事务的操作
seo-description: 使用TransactionRecorder API记录未自动入帐为事务的操作
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 记录自定义实施的事务{#record-a-transaction-for-custom-implementations}

使用TransactionRecorder API记录未自动入帐为事务的操作

您可以使用自定义代码提交PDF表单、向最终用户发送代理UI预览URL以预览交互式通信，或使用自定义方法提交表单，而不是使用AEM Forms提供的提交方法。 之前提到的所有AEM Forms API操作和自定义实施均不会计为交易。 AEM Forms提供了一个API [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)，用于记录此类操作（如交易）。

要记录事务，请编写[标准sling servlet](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html)并从客户端调用Servlet以记录事务。 您可以使用AJAX或任何其他标准方法调用Servlet。

## 服务器端代码{#sample-server-sided-code}示例

您可以使用以下示例代码从JAVA类中使用自定义OSGi包运行TransactionRecorder API。

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## 示例客户端代码{#sample-client-side-code}

您可以使用以下示例代码调用具有`TransactionRecorder` API的Servlet。

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 相关文章{#related-articles}

* [交易报表概述](/help/forms/using/transaction-reports-overview.md)
* [查看和了解交易报表](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [交易报表计费API](/help/forms/using/transaction-reports-billable-apis.md)
