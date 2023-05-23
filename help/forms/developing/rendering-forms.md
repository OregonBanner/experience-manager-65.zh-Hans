---
title: 轉譯Forms
seo-title: Rendering Forms
description: 使用Forms服務建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可以開發單一表單設計，Forms服務會在各種瀏覽器環境中以PDF、SWF或HTML呈現。
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 轉譯Forms {#rendering-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於Forms服務**

Forms服務可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者可以開發單一表單設計，Forms服務會在各種瀏覽器環境中以PDF、SWF或HTML呈現。

當一般使用者請求表單時，使用者端應用程式會將請求傳送至Forms服務，該服務會以適當格式傳回表單。 Forms服務一收到要求，就會將資料與表單設計合併，然後以所需格式傳送表單。 表單服務輸出是互動式表單，通常是PDF檔案。 互動式表單可讓使用者填寫表單上的欄位。

根據使用者端應用程式的型別，您可以將表單寫入使用者端網頁瀏覽器，或將表單儲存為PDF檔案。 網頁型應用程式可將表單寫入網頁瀏覽器。 案頭應用程式可將表單儲存為PDF檔案。 為了示範如何寫出至網頁瀏覽器和PDF檔案，快速入門位於 *轉譯Forms* 區段的組織方式如下：

* Java API強型別（SOAP模式）範例為Java servlet。
* Web服務(Java Base64)範例是Java servlet。
* Web服務(MTOM)範例是主控台應用程式（並非所有快速啟動都有MTOM範例）。

>[!NOTE]
>
>如需有關建立使用Java Servlet來呼叫Forms服務的Web應用程式的資訊，請參閱 [建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md).

您可以使用下列兩種方式之一，將表單設計（XDP檔案）或PDF檔案傳遞到Forms服務：

* 您可以使用URL值來參考表單設計。 此方法涉及使用 `URLSpec` 物件。 內容根目錄會使用傳遞至Forms服務 `URLSpec` 物件的 `setContentRootURI` 方法。 表單設計名稱( `formQuery`)以個別引數傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。 (大部分快速入門位於 *轉譯Forms* 部分請使用此方法。)
* 您可以傳遞 `com.adobe.idp.Document` 包含表單設計給Forms服務的檔案。 兩個命名的新方法 `renderPDFForm2` 和 `renderHTMLForm2` 接受 `com.adobe.idp.Document` 包含表單設計的物件。 (請參閱 [將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

您可以使用Forms服務完成這些工作：

* 演算互動式PDF forms。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* 在使用者端轉譯表單。 (請參閱 [在使用者端轉譯Forms](/help/forms/developing/rendering-forms-client.md).)
* 根據片段轉譯表單。 (請參閱 [根據片段轉譯Forms](/help/forms/developing/rendering-forms-based-fragments.md).)
* 轉譯啟用許可權的表單。 (請參閱 [轉譯啟用許可權的Forms](/help/forms/developing/rendering-rights-enabled-forms.md).)
* 將表單轉譯為HTML。 (請參閱 [將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md).)
* 使用自訂CSS檔案呈現HTMLForms ([使用自訂CSS檔案轉譯HTMLForms](/help/forms/developing/rendering-html-forms-using-custom.md).)
* 處理提交的表單。 (請參閱 [處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md).)
* 使用已提交的XML資料建立PDF檔案。 (請參閱 [使用已提交的XML資料建立PDF檔案](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* 預先填入表單。 (請參閱 [使用可流動版面預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* 傳遞檔案。 (請參閱 [將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)
* 計算表單資料。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md).)
* 最佳化應用程式。 (請參閱 [最佳化Forms服務的效能](/help/forms/developing/optimizing-performance-forms-service.md).)
