---
title: 字母和互動式通訊的後處理
seo-title: Post Processing of Letters
description: 「通訊管理」中的信件後處理可讓您建立AEM和Forms後處理（例如列印和電子郵件），並將其與您的信件整合。
seo-description: Post Processing of Letters in Correspondence Management lets you create AEM and Forms post processes, such as print and email, and integrate them with your letters.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 字母和互動式通訊的後處理{#post-processing-of-letters-and-interactive-communications}

## 後處理 {#post-processing}

代理程式可以關聯並執行信函和互動式通訊的後處理工作流程。 可以在Letter範本的「屬性」檢視中選取要執行的後續程式。 您可以設定後續程式，以電子郵件、列印、傳真或封存最終信件。

![後處理](assets/ppoverview.png)

若要將後置處理程式與信件或互動式通訊建立關聯，您必須先設定後置處理程式。 提交的信件上可執行兩種型別的工作流程：

1. **Forms Workflow：** 這些是AEM Forms on JEE流程管理工作流程。 設定說明 [Forms Workflow](#formsworkflow).

1. **AEM工作流程：** AEM工作流程也可用作為已提交信函的張貼程式。 設定說明 [AEM工作流程](../../forms/using/aem-forms-workflow.md).

## 表单工作流 {#formsworkflow}

1. 在AEM中，使用下列URL開啟伺服器的Adobe Experience Manager Web主控台設定： `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![設定管理員](assets/2configmanager-1.png)

1. 在此頁面上，找到AEM Forms使用者端SDK設定，然後按一下以展開它。
1. 在伺服器URL中，輸入JEE伺服器上AEM Forms的名稱、登入詳細資訊，然後按一下 **儲存**.

   ![輸入LiveCycle伺服器的名稱](assets/1cofigmanager.png)

1. 指定使用者名稱和密碼。
1. 確定已將sun.util.calendar新增至還原序列化防火牆設定。

   移至[還原序列化防火牆設定]，然後在[允許清單的套件首碼類別]下方，新增sun.util.calendar。

1. 現在您的伺服器已完成對應，並且建立信件時，AEM使用者介面中提供AEM Forms on JEE中的發佈程式。

   ![建立信件畫面，並列出後續程式](assets/0configmanager.png)

1. 若要驗證程式/服務，請復製程式名稱，然後返回「Adobe Experience Manager Web主控台組態」頁面> 「AEM Forms使用者端SDK組態」 ，並將程式新增為新服務。

   例如，如果信函的「屬性」頁面中的下拉式清單將流程名稱顯示為Forms Workflow-> ValidCCPostProcess/SaveXML，請將「服務名稱」新增為 `ValidCCPostProcess/SaveXML`.

1. 若要在JEE工作流程中使用AEM Forms進行後續處理，請設定必要的引數和輸出。 引數的預設值如下所示。

   前往Adobe Experience Manager Web Console設定頁面> **[!UICONTROL 通訊管理設定]** 並設定下列引數：

   1. **inPDFDoc (PDF檔案引數)：** PDF檔案作為輸入。 此輸入包含轉譯字母作為輸入。 指示的引數名稱是可設定的。 可以從設定的「通訊管理」設定中進行設定。
   1. **inXMLDoc （XML資料引數）：** XML檔案作為輸入。 此輸入包含使用者以XML格式輸入的資料。
   1. **inXDPDoc （XDP檔案引數）：** XML檔案作為輸入。 此輸入包含基礎配置(XDP)。
   1. **inAttachmentDocs （附件檔案引數）：** 清單輸入引數。 此輸入包含作為輸入的所有附件。
   1. **redirectURL （重新導向URL輸出）：** 指出要重新導向之URL的輸出型別。

   您的表單工作流程必須有PDF的檔案引數或XML資料引數作為輸入，且名稱與 **[!UICONTROL 通訊管理設定]**. 這是處理程式列在「後續處理程式」下拉式清單中的必要專案。

## 發佈執行個體上的設定 {#settings-on-the-publish-instance}

1. 登入 `https://localhost:publishport/aem/forms`.
1. 導覽至 **[!UICONTROL 字母]** 以檢視發佈執行個體上可用的已發佈信件。
1. 設定AEM DS設定。 另請參閱 [正在設定AEM DS設定](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>使用Forms或AEM工作流程時，從發佈伺服器提交任何內容之前，必須先設定DS設定服務。 否則，表單提交將會失敗。

## 字母例項擷取 {#letter-instances-retrieval}

您可以使用LetterInstanceService中定義的下列API進一步操作儲存的信件例項，例如擷取信件例項和刪除信件例項。

<table>
 <tbody>
  <tr>
   <td><strong>伺服器端API</strong></td>
   <td><strong>作業名稱</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><p>公開LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>擲回ICCException； </p> </td>
   <td>getLetterInstance</td>
   <td>擷取指定的字母例項 </td>
  </tr>
  <tr>
   <td>公用void deleteLetterInstance(String letterInstanceId)擲回ICCException； </td>
   <td>deleteLetterInstance </td>
   <td>已刪除指定的字母例項 </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)擲回ICCException； </td>
   <td>getAllLetterInstances </td>
   <td>此API會根據輸入查詢引數擷取信件例項。 若要擷取所有信件例項，可將查詢引數傳遞為null。<br /> </td>
  </tr>
  <tr>
   <td>公用布林值letterInstanceExists(String letterInstanceName)擲回ICCException； </td>
   <td>letterInstanceExists </td>
   <td>檢查指定的名稱是否存在LetterInstance </td>
  </tr>
 </tbody>
</table>

## 建立後處理與字母的關聯 {#associating-a-post-process-with-a-letter}

在CCR使用者介面中，完成下列步驟，將後處理與信函產生關聯：

1. 將滑鼠指標暫留在信函上並點選 **檢視屬性**.
1. 选择&#x200B;**编辑**。
1. 在「基本屬性」中，使用「後處理」下拉式清單，選取要與信函關聯的後處理。 下拉式清單中會列出AEM和Forms相關的發佈程式。
1. 點選 **儲存**.
1. 使用後處理設定信函後，發佈信函，並選擇性地在發佈執行個體上指定AEM DS設定服務中的處理URL。 這樣可確保後處理會在處理執行個體上執行。

## 重新載入草稿字母例項  {#reloaddraft}

草稿信件例項可以使用以下URL在使用者介面中重新載入：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstanceID：已提交信件例項的唯一ID。

如需儲存草稿信函的詳細資訊，請參閱 [儲存草稿並提交信件例項](../../forms/using/create-correspondence.md#savingdrafts).
