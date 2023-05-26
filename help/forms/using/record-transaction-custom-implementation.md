---
title: 记录自定义实施的交易
seo-title: Record a transaction for custom implementations
description: 使用TransactionRecorder API自动记录未作为事务入帐的操作
seo-description: Use the TransactionRecorder API to record actions which are not accounted as transactions automatically
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 记录自定义实施的交易 {#record-a-transaction-for-custom-implementations}

使用TransactionRecorder API自动记录未作为事务入帐的操作

您可以使用自定义代码提交PDF表单，或将代理UI预览URL发送给最终用户以预览交互式通信。 或者，您也可以使用自定义方法提交表单，而不是使用AEM Forms提供的提交方法。 前面提到的AEM Forms API的所有操作和自定义实施都不会计为交易。 AEM Forms提供API、 [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)，将此类操作记录为事务处理。

要记录事务处理，请编写 [标准sling servlet](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) 并从客户端调用servlet以记录事务。 您可以使用AJAX或任何其他标准方法调用servlet。

## 服务器端代码示例 {#sample-server-sided-code}

您可以使用以下示例代码通过自定义OSGi捆绑包从Java™类运行TransactionRecorder API。

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

## 示例客户端代码 {#sample-client-side-code}

您可以使用以下示例代码调用具有以下特性的servlet： `TransactionRecorder`API。

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

## 相关文章 {#related-articles}

* [事务处理报表概览](/help/forms/using/transaction-reports-overview.md)
* [查看和了解事务处理报表](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [交易报告可记帐API](/help/forms/using/transaction-reports-billable-apis.md)
