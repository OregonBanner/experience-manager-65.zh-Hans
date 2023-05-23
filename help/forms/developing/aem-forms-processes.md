---
title: 瞭解AEM Forms程式
seo-title: Understanding AEM Forms Processes
description: 瞭解AEM Forms程式
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

# 瞭解AEM Forms程式 {#understanding-aem-forms-processes}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

常見的使用案例是一組AEM Forms服務在單一檔案上運作。 您可以使用Workbench建立處理作業，將請求傳送至服務容器。 流程代表您正在自動化的業務流程。 如需建立處理作業的詳細資訊，請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

程式一旦啟動，就會變成服務，而且可以像其他服務一樣叫用。 標準服務（例如Encryption服務）與源自處理序的服務之間的一個差異，是後者有一個執行許多動作的作業。 相反地，標準服務有很多操作。 每個操作通常會執行一個動作，例如將原則套用至檔案或加密檔案。

程式可以是短期或長期。 短期程式是在從中叫用程式的相同執行緒上同步執行的操作。 短期作業與大多數程式設計語言中的標準行為類似，使用者端應用程式會呼叫方法並等待傳回值。

不過，在某些情況下，由於下列因素，流程無法同步完成：

* 一個程式可能需花費相當長的時間。
* 一個程式可以跨越組織邊界。
* 程式需要外部輸入才能完成。 例如，考慮將表單傳送給不在辦公室的經理的情況。 在此情況下，除非管理員返回並填寫表單，否則程式不會完成。

   這些型別的程式稱為長效程式。 系統會以非同步方式執行長期程式，讓系統在資源允許時互動，並追蹤及監控作業。 叫用長期處理程式時，AEM Forms會建立叫用識別碼值，作為追蹤長期處理程式狀態的記錄的一部分。 記錄儲存在AEM Forms資料庫中。 您可以在不再需要長期處理記錄時將其清除。

>[!NOTE]
>
>叫用短期程式時，AEM Forms不會建立記錄。

您可以使用叫用識別碼值來追蹤長效處理序的狀態。 例如，您可以使用處理序呼叫識別碼值來執行「處理序管理員」作業，例如終止執行中的處理序執行處理。

**短期程式範例**

下圖是名為的短期程式範例 *MyApplication/EncryptDocument*.

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要與討論如何呼叫此程式的程式碼範例一起遵循，請建立名為的程式 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

叫用這個短暫的處理程式時，會執行下列動作：

1. 取得未加密的PDF檔案，該檔案會作為輸入值傳遞至處理序。
1. 使用密碼加密PDF檔案。 此處理序的輸入引數名稱是 `inDoc` 而且資料型別為document。
1. 將密碼加密的PDF檔案儲存為PDF檔案至本機檔案系統。 此程式會傳回加密的PDF檔案作為輸出值。 此處理序的輸出引數名稱是 `outDoc` 而且資料型別為document。

   此程式會在從中叫用它的相同執行緒上同步完成。 此短期處理序的名稱為 `MyApplication/EncryptDocument`而且它的操作是 `invoke`.

   >[!NOTE]
   >
   >通常一個短暫的流程包含三個以上的動作。 您可以使用Workbench建立處理。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *使用AEM表單程式設計*&#x200B;說明以下以程式設計方式呼叫此短期程式的方法：

   * [使用AEM Forms Remoting傳遞不安全的檔案以叫用短暫的流程](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (使用Flex應用程式)
   * [使用叫用API叫用短期程式](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java叫用API）
   * [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （網站服務範例）
   * [使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （網站服務範例）
   * [使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （網站服務範例）
   * [透過HTTP使用BLOB資料叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （網站服務範例）
   * [使用DIME叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （網站服務範例）
   * [使用REST叫用MyApplication/EncryptDocument程式](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長效程式範例**

下圖是長期流程的範例。

當申請人提交貸款表單時，會呼叫此程式。 在貸款專員核准或拒絕貸款請求之前，該流程不會完成。 此長效處理序的名稱為 *FirstAppSolution/PreLoanProcess* 而且它的操作是 `invoke_Async`. 此程式必須以非同步方式叫用。 如需以程式設計方式叫用這個長效流程的相關資訊，請參閱 [叫用以人為中心的長期流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>您可以依照中指定的教學課程來建立此程式 [建立您的第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
