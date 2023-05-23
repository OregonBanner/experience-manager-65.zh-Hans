---
title: 在AEM Forms工作區中整合第三方應用程式
seo-title: Integrating third-party applications in AEM Forms workspace
description: 在AEM Forms工作區中整合協力廠商應用程式，例如通訊管理。
seo-description: How-to integrate third-party apps like Correspondence Management in AEM Forms workspace.
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# 在AEM Forms工作區中整合第三方應用程式{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作區支援管理表單與檔案的任務指派與完成活動。 這些表單和檔案可以是XDP Forms、Flex®表單或已棄用的XDP、PDF、HTML或Flex格式轉譯指南。

這些功能會進一步增強。 AEM Forms現在支援與協力廠商應用程式共同作業，這些應用程式支援與AEM Forms工作區類似的功能。 此功能的共同部分是任務指派和後續核准的工作流程。 AEM Forms為AEM Forms企業使用者提供單一統一的體驗，以便透過AEM Forms工作區處理受支援應用程式的所有此類任務指派或核准。

例如，我們將「通訊管理」視為與AEM Forms工作區整合的候選範例。 Correspondence Management具有「信件」的概念，可以轉譯並允許動作。

## 建立對應管理資產 {#create-correspondence-management-assets}

首先，建立在AEM Forms工作區中轉譯的範例「通訊管理」範本。 如需詳細資訊，請參閱 [建立字母範本](../../forms/using/create-letter.md).

存取「通訊管理」範本的URL以驗證「通訊管理」範本是否可以成功呈現。 URL的模式類似於 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

位置 `encodedLetterId` 是URL編碼的字母識別碼。 在Workbench中定義工作區工作的轉譯流程時，請指定相同的字母ID。

## 建立任務以在AEM Workspace中呈現和提交信件 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

在執行這些步驟之前，請確定您是以下群組的成員：

* cm-agent-users
* 工作區使用者

如需詳細資訊，請參閱 [新增和設定使用者](/help/forms/using/admin-help/adding-configuring-users.md).

使用以下步驟來建立任務，以便在AEM Workspace中轉譯和提交信件：

1. 啟動Workbench。 以管理員身分登入localhost。
1. 按一下「檔案」>「新增」>「應用程式」。 在「應用程式名稱」欄位中，輸入 `CMDemoSample` 然後按一下[完成]。
1. 選取 `CMDemoSample/1.0` 並按一下右鍵 `NewProcess`. 在名稱欄位中，輸入 `CMRenderer` 然後按一下[完成]。
1. 拖曳起點活動選擇器並加以設定：

   1. 在簡報資料中，選取使用CRX資產。

      ![useacrxasset](assets/useacrxasset.png)

   1. 瀏覽資產。 在「選取表單資產」對話方塊中，「字母」索引標籤會列出伺服器上的所有字母。

      ![字母索引標籤](assets/letter_tab_new.png)

   1. 選取適當的字母並按一下 **確定**.

1. 按一下「管理動作設定檔」。 「管理動作設定檔」對話方塊隨即顯示。 請確定已正確選取轉譯程式和提交程式。
1. 若要使用資料XML檔案開啟信件，請在「準備資料程式」中瀏覽並選取適當的資料檔案。
1. 单击确定。
1. 定義起始點輸出和工作附件的變數。 定義的變數將包含「起始點輸出」和「工作附件」資料。
1. （可選）若要在工作流程中新增其他使用者，請拖曳活動選擇器、設定活動選擇器並將其指派給使用者。 撰寫自訂包裝函式（以下提供範例）或下載並安裝DSC （以下提供）以擷取Letter範本、起點輸出和工作附件。

   自訂包裝函式的範例如下：

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [取得檔案](assets/dscsample.zip)
下載DSC：以上附加的DSCSample.zip檔案中提供範例DSC。 下載並解壓縮DSCSample.zip檔案。 在使用DSC服務之前，您必須先設定它。 如需詳細資訊，請參閱 [設定DSC服務](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   在「定義活動」對話方塊中，選取適當的活動（例如getLetterInstanceInfo），然後按一下 **確定**.

1. 部署應用程式。 如果出現提示，請入庫並儲存資產。
1. 在https://&#39;登入AEM表單工作區[伺服器]：[連線埠]&#39;/lc/content/ws.
1. 開啟您新增的工作CMRenderer。 「通訊管理」信函隨即出現。

   ![cminworkspace](assets/cminworkspace.png)

1. 填寫所需資料並提交信件。 視窗關閉。 在此程式中，任務會指派給步驟9中工作流程中所指定的使用者。

   >[!NOTE]
   >
   >填妥信函中的所有必要變數後，才會啟用「提交」按鈕。
