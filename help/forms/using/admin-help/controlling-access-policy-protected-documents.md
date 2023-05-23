---
title: 控制對受原則保護檔案的存取
seo-title: Controlling access to policy-protected documents
description: 瞭解如何檢視、管理及控制受原則保護檔案的存取權。
seo-description: See how you can view, manage and control the access to your policy-protected documents.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2169'
ht-degree: 0%

---

# 控制對受原則保護檔案的存取 {#controlling-access-to-policy-protected-documents}

您可以控制收件者使用受原則保護檔案的方式，無論受原則保護檔案的分佈範圍有多廣。

您可以在「檔案」頁面執行下列工作：

* 搜尋並檢視受原則保護檔案的詳細資訊。 您可以檢視檔名稱、發行者名稱、原則名稱和套用原則的日期的相關資訊。 如果刪除了保護檔案的原則，您也可以在原則名稱下看到已刪除的原則ID。 使用者可以檢視和管理自己受原則保護的檔案。 管理員可以檢視和管理所有受原則保護的檔案。
* 變更套用至檔案之原則的詳細資訊。 使用者可以編輯他們自己的原則，管理員可以編輯共用和個人原則，原則集專員可以編輯他們有權執行的原則集中的共用原則。 您可以直接從「檔案詳細資訊」頁面存取與檔案相關聯的原則。
* 撤銷並恢復受原則保護檔案的存取權。 管理員可以撤銷和恢復任何檔案的存取權。 原則組協調員（有權管理檔案的人）可以從其原則組撤銷和恢復對使用共用原則的受原則保護檔案的存取權。 如果使用者建立了保護檔案的原則，或該原則是允許此功能的共用原則，則使用者可以撤銷對其受原則保護檔案的存取權。
* 切換套用至檔案的原則。 將原則套用至檔案的使用者，可以在建立原則或該原則是啟用此功能的共用原則時切換原則。 原則組專員可以從其原則組切換原則。 管理員可以切換套用至任何檔案的原則。

當檔案受原則保護，而您撤銷存取許可權或切換套用的原則時，變更將生效，如下所示：

* 如果檔案線上上，除非使用者已開啟檔案，否則會立即套用變更。 在這種情況下，使用者必須關閉檔案，變更才會生效。
* 如果收件者離線使用檔案（例如在筆記型電腦上），則變更會在下次收件者透過開啟任何受原則保護的檔案與Document Security同步時生效。

## 檢視檔案的相關資訊 {#view-information-about-a-document}

對於「檔案」頁面上列出的每個檔案，您可以看到檔名稱、發行者名稱、原則名稱和檔案受保護日期。 如果保護檔案的原則已刪除，則原則ID會列在「原則名稱」下。

您也可以在「檔案詳細資訊」頁面上檢視有關特定檔案的更多詳細資訊（如下所述）：

>[!NOTE]
>
>您必須使用[檔案詳細資訊]頁面上的[原則名稱]連結，才能存取在Microsoft Outlook中為附加至電子郵件訊息之檔案的收件者自動產生的原則。 這些原則不會出現在原則頁面上。

**檔名稱：** 所選檔案的名稱。

**檔案ID：** 當原則套用至檔案時，Document Security指派的唯一識別碼。 document security使用此編號來追蹤檔案。

**檔案狀態：** 檔案的狀態（例如，有效或已撤銷）。

**發行者：** 將原則附加至檔案的使用者名稱。

**原則名稱：** 用來保護檔案的原則名稱。 您可以按一下名稱以開啟原則。 您必須使用此連結來存取Acrobat為Outlook中附加至電子郵件訊息之檔案的收件者產生的原則。 這些原則不會顯示在「原則」頁面上。

**原則型別：** 套用至檔案的原則型別。

**發佈日期：** 將原則套用至檔案的日期。

**相關反複專案：** 如果檔案具有相關版序，則此專案也會出現在清單中。 按一下連結可檢視檔案的相關版序清單。

使用者可以檢視有關其受保護檔案的資訊。 管理員可檢視任何使用者已受原則保護之檔案的相關資訊。 原則組專員可以檢視受原則保護的檔案相關資訊，而不受其原則組的影響。

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。 「檔案詳細資訊」頁面隨即開啟，顯示有關檔案的詳細資訊。 此頁面也提供撤銷檔案存取權、切換原則以及檢視與此檔案相關之事件的選項。

## 檢視檔案的相關版序 {#view-related-iterations-for-a-document}

如果啟用了追蹤相關版序，您可以追蹤不同使用者已儲存的檔案版本。 只有特定應用程式支援此功能，例如PTC Pro/ENGINEER Wildfire。

當多位使用者共同作業並儲存同一份檔案的不同版本時，此功能會很有用。 document security可以追蹤各種版序；因此，您可以輕鬆檢視不同版本的檔案資訊。

如果啟用此功能，您可以從「檔案」頁面檢視檔案的相關版序。

1. 檢視檔案的「檔案詳細資訊」頁面。 (請參閱 [檢視檔案的相關資訊](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. 按一下「檢視相關版序」。 只有在啟用特徵時，才可使用選項。 相關版序清單隨即顯示。 對於每個版序，您可以檢視下列資訊：

   * **反複專案：** 檔案名稱。 它可能與原始檔案名稱不同，並且會在結尾附加一個版本號碼。
   * **發行者：** 原始檔案的發行者。
   * **建立者：** 儲存反複專案的使用者。
   * **建立日期：** 儲存反複專案的日期和時間。
   * **原則：** 保護反複專案的原則。 不同的反複專案可能受不同的原則保護。

1. 若要顯示該版序的「檔案詳細資訊」頁面，請按一下版序的檔案名稱。

## 撤銷和恢復對檔案的存取權 {#revoking-and-reinstating-access-to-documents}

您可以撤銷並恢復受原則保護檔案的存取權：

**使用者：** 可以撤銷或恢復使用個人原則或共用原則（套用原則的使用者可針對這些共用原則啟用撤銷功能）保護之檔案的存取權。 無法撤銷檔案存取權或切換原則的使用者需要聯絡管理員。

**管理員：** 可以撤銷或恢復任何受原則保護檔案的存取許可權，包括受個人或共用原則保護的檔案。 如果管理員撤銷對受共用原則保護之檔案的存取權，則只有管理員可以恢復該檔案的存取許可權。

**原則集協調員：** 可以撤銷或恢復其原則集所保護之檔案的存取許可權。

當您撤銷或恢復檔案存取許可權時，變更會在以下時間生效：

* 如果檔案線上上並已關閉，則下次收件者透過開啟受原則保護的檔案與Document Security同步時，變更會生效。
* 如果檔案線上上且已開啟，則變更會在收件者關閉檔案時生效。
* 如果檔案離線（使用時沒有網際網路連線，例如在筆記型電腦上），則變更會在收件者下次與Document Security同步時生效。

**撤銷受原則保護檔案的存取權**

1. 在Document Security頁面上，按一下「檔案」。
1. 選取適當檔案旁的核取方塊，然後按一下撤銷。 您可以一次撤銷多個檔案的存取權。
1. 選取要在檔案撤銷後向嘗試開啟檔案的使用者顯示的訊息：

   * **一般訊息：** 指出作者已撤銷檔案
   * **檔案已終止：** 指出作者已終止檔案
   * **檔案已修訂**：指出作者已修訂檔案

1. （可選）如果有較新版本的檔案可用，請輸入URL並按一下測試以驗證URL。
1. 按一下「確定」，然後再次按一下「確定」以返回「檔案」頁面。

**恢復檔案存取許可權**

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下取消撤銷，然後按一下確定。

## 切換套用至檔案的原則 {#switch-a-policy-that-is-applied-to-a-document}

使用者、原則組專員和管理員可以切換套用至受原則保護檔案的原則（您一次只能套用一個原則至檔案）。 如果使用者已建立原則，或該原則是已啟用此功能之共用原則，則使用者可以切換套用至他們自己的受原則保護檔案的原則。 否則，管理員或原則設定協調者必須切換原則。 管理員可以為任何使用者的受原則保護檔案切換原則。 原則組專員可以從其原則組切換原則。

當您切換原則時，新原則會依下列方式強制執行：

* 如果檔案線上上並已關閉，則下次收件者透過線上上開啟任何受原則保護的檔案來與Document Security同步時，變更會生效。
* 如果檔案線上上且已開啟，則變更會在使用者關閉檔案時生效。
* 如果檔案離線（使用中時沒有使用中的網際網路或網路連線，例如在筆記型電腦上），則下次使用者透過線上開啟受原則保護的檔案與Document Security同步時，會套用變更。

>[!NOTE]
>
>若要允許匿名存取目前沒有此存取權的受原則保護檔案，請移除使用者端應用程式中的現有原則，然後套用允許匿名存取的原則。 如果您切換原則，使用者仍然必須登入才能存取檔案。

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下「切換原則」。 最多會顯示100個原則的清單。
1. 如果未顯示您想要的原則，請從[尋找]清單中選取[原則名稱]或[原則ID]，輸入名稱或ID，然後按一下[尋找]。
1. 按一下清單中的新原則。
1. 按一下「切換原則」，然後按一下「確定」返回「檔案」頁面。

## 搜尋檔案 {#search-for-a-document}

您可以使用日期範圍條件與清單中可用的搜尋條件組合，在「檔案」頁面上搜尋檔案。 這些條件包括檔名稱、原則名稱或所有檔案。

只有管理員可以使用其他搜尋選項：

**檔案ID：** 當套用原則時，Document Security指派給檔案的唯一ID號。

**檔名稱：** 檔名稱。

**發行者名稱：** 將原則附加至檔案的使用者名稱。 您可以從所有網域或指定的網域中選取使用者。

**原則ID：** 附加到檔案的原則的ID號。

**原則名稱：** 附加至檔案的原則名稱。

**所有檔案：** 所有受管理員和使用者保護的檔案。 使用「所有檔案」選項進行搜尋可能會傳回一長串檔案。

1. 在Document Security頁面上，按一下「檔案」。
1. 在「尋找」清單中，選取所需的搜尋條件。

   您可以將條件指定為檔案ID、檔名稱、發行者名稱、原則ID、原則名稱或所有檔案。

   如果您指定發行者名稱，請按一下[通訊錄]圖示，並指定您要搜尋使用者的網域，然後按一下[確定]返回[檔案]搜尋頁面。

1. （選用）在日期清單中，選取日期範圍選項。 如果您選取「自訂日期」，請在出現的方塊中以yyyy/mm/dd格式輸入日期，或使用日期選擇器指定日期範圍：

   * 按一下行事曆以開啟日期選擇器。
   * 使用箭頭來尋找年份和月份。
   * 在行事曆上按一下當月某日。
   * 按一下「確定」以關閉「日期選擇器」。

1. 按一下「尋找」。

## 排序檔案清單 {#sort-the-document-list}

您可以依欄標題來排序檔案清單。 欄標題旁的三角形圖示表示目前使用哪一欄來排序。 向上指向三角形表示遞增順序，向下指向三角形表示遞減順序。

1. 在Document Security頁面上，按一下「檔案」。
1. 按一下適當的欄標題。
1. 若要變更排序順序，請再次按一下欄。

## 新增封面頁至受原則保護的檔案 {#add-cover-page-to-policy-protected-documents}

在大部分非Adobe PDF檢視器的情況下，如果您開啟受Document Security保護的檔案，第一頁會顯示為空白頁面，或者應用程式會在未開啟檔案的情況下中止。

您可以使用頁面0 （包裝函式檔案）支援，讓非Adobe PDF檢視器開啟受保護的檔案並在檔案中顯示封面頁。

>[!NOTE]
>
>在Adobe Reader/Acrobat或行動Reader中檢視此類檔案（包含頁面0）時，受保護檔案會依預設開啟。

**若要將封面頁新增至受原則保護的檔案**

在Workbench中使用下列處理：

**含封面頁的Protect檔案：** 使用指定的原則保護PDF檔案，並將封面頁新增至檔案

**擷取受保護檔案：** 從含有封面頁的PDF檔案中擷取受原則保護的PDF檔案

使用下列Document Security API：

**protectDocumentWithCoverPage：** 使用指定的原則保護指定PDF，並傳回附有封面頁和受保護檔案作為附件的檔案
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument：** 擷取受保護的檔案，它是封面頁所在檔案的附件。 可以使用protectDocumentWithCoverPage方法建立具有封面頁的檔案
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
