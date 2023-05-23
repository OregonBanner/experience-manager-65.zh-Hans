---
title: 使用批次API產生多個互動式通訊
description: 使用批次API產生多個互動式通訊
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 1%

---

# 使用批次API產生多個互動式通訊 {#use-batch-api-to-generate-multiple-ic}

您可以使用批次API從範本產生多個互動式通訊。 範本是沒有任何資料的互動式通訊。 Batch API會將資料與範本結合，以產生互動式通訊。 此API適用於大量生產互動式通訊。 例如，電話帳單、多個客戶的信用卡對帳單。

批次API接受JSON格式和表單資料模型中的記錄（資料）。 產生的互動式通訊數量等於在設定的表單資料模型中輸入JSON檔案中指定的記錄。 您可以使用API來產生列印和網頁輸出。 PRINT選項會產生PDF檔案，而WEB選項會為每個個別記錄產生JSON格式的資料。

## 使用批次API {#using-the-batch-api}

您可以將批次API與Watched資料夾搭配使用，或作為獨立的Rest API使用。 您可以為產生的互動式通訊設定範本、輸出型別(HTML、列印或兩者)、地區設定、預填服務和名稱，以使用批次API。

您可以將記錄與互動式通訊範本結合，以產生互動式通訊。 批次API可以直接從JSON檔案或透過表單資料模型存取的外部資料來源讀取記錄（互動式通訊範本的資料）。 您可以將每個記錄儲存在單獨的JSON檔案中，也可以建立JSON陣列以將所有記錄儲存在單個檔案中。

**JSON檔案中的單一記錄**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON檔案中有多個記錄**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### 搭配Watched資料夾使用批次API {#using-the-batch-api-watched-folders}

為了讓您輕鬆體驗API，AEM Forms提供開箱即用且設定為使用批次API的Watched資料夾服務。 您可以透過AEM Forms UI存取此服務，以產生多種互動式通訊。 您也可以根據需求建立自訂服務。 您可以使用下列方法搭配Watched資料夾使用批次API：

* 指定JSON檔案格式的輸入資料（記錄），以產生互動式通訊
* 使用儲存在外部資料來源中並透過表單資料模型存取的輸入資料（記錄）來產生互動式通訊

#### 指定JSON檔案格式的輸入資料記錄，以產生互動式通訊 {#specify-input-data-in-JSON-file-format}

您可以將記錄與互動式通訊範本結合，以產生互動式通訊。 您可以為每個記錄建立個別的JSON檔案，或建立JSON陣列以將所有記錄儲存在單一檔案中：

若要從JSON檔案中儲存的記錄建立互動式通訊：

1. 建立 [Watched資料夾](/help/forms/using/creating-configure-watched-folder.md) 並將其設定為使用Batch API：
   1. 登入AEM Forms作者執行個體。
   1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定Watched資料夾]**. 點選 **[!UICONTROL 新增]**.
   1. 指定 **[!UICONTROL 名稱]** 和實體 **[!UICONTROL 路徑]** 檔案夾的。 例如：`c:\batchprocessing`。
   1. 選取 **[!UICONTROL 服務]** 中的選項 **[!UICONTROL 處理檔案，使用]** 欄位。
   1. 選取 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 中的服務 **[!UICONTROL 服務名稱]** 欄位。
   1. 指定 **[!UICONTROL 輸出檔案模式]**. 例如，%F/ [圖樣](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定Watched資料夾可以在Watched資料夾\input資料夾的子資料夾中找到輸入檔案。
1. 設定進階引數：
   1. 開啟 **[!UICONTROL 進階]** 標籤並新增下列自訂屬性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | 範本路徑 | 字符串 | 指定要使用的互動式通訊範本路徑。 例如，/content/dam/formsanddocuments/testsample/mediumic。 這是強制屬性。 |
      | recordpath | 字符串 | recordPath欄位的值有助於設定互動式通訊的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果您指定/employee/Id，id欄位的值會變成對應互動式通訊的名稱。 預設值是隨機的 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | 布尔值 | 將值設為False。 您可以使用usePrefillService引數來預先填入互動式通訊，其中資料是從針對對應互動式通訊而設定的預先填入服務中擷取。 當usePrefillService設為true時，輸入JSON資料（每個記錄）會視為FDM引數。 預設值為false。 |
      | batchType | 字符串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定輸出互動式通訊的地區設定。 現成服務不會使用地區設定選項，但您可以建立自訂服務以產生本地化的互動式通訊。 預設值為en_US |

   1. 點選 **[!UICONTROL 建立]** 已建立watched資料夾。
1. 使用watched資料夾產生互動式通訊：
   1. 開啟Watched資料夾。 導覽至輸入資料夾。
   1. 在輸入資料夾中建立資料夾，並將JSON檔案放在新建立的資料夾中。
   1. 等候Watched資料夾處理檔案。 處理開始時，輸入檔案和包含該檔案的子資料夾會移至暫存資料夾。
   1. 開啟輸出資料夾以檢視輸出：
      * 當您在Watched資料夾組態中指定PRINT選項時，會產生互動式通訊的PDF輸出。
      * 當您在Watched資料夾設定中指定WEB選項時，會針對每筆記錄產生一個JSON檔案。 您可以使用JSON檔案來 [預先填入Web範本](#web-template).
      * 當您同時指定PRINT和WEB選項時，會針對每筆記錄同時產生PDF檔案和JSON檔案。

#### 使用儲存在外部資料來源中並透過表單資料模型存取的輸入資料，以產生互動式通訊 {#use-fdm-as-data-source}

您可以將儲存在外部資料來源中的資料（記錄）與互動式通訊範本結合，以產生互動式通訊。 當您建立互動式通訊時，可以透過表單資料模型(FDM)將其連線到外部資料來源以存取資料。 您可以設定Watched Folders批次處理服務，以使用相同的表單資料模型從外部資料來源擷取資料。 至 [從儲存在外部資料來源中的記錄建立互動式通訊](/help/forms/using/work-with-form-data-model.md)：

1. 設定範本的表單資料模型：
   1. 開啟與互動式通訊範本相關聯的表單資料模型。
   1. 選取您的頂層模型物件，然後點選「編輯屬性」。
   1. 從「編輯屬性」窗格下的「讀取服務」欄位中選取擷取或取得服務。
   1. 點選讀取服務引數的鉛筆圖示，以將引數繫結至要求屬性，並指定繫結值。 它會將服務引數繫結到指定的繫結屬性或常值中，該值會作為引數傳遞給服務，以從資料來源擷取與指定值相關聯的詳細資訊。

      <br>
        在此範例中，id引數會採用使用者設定檔的id屬性值，並將其當做引數傳給讀取服務。 它會從指定ID的員工資料模型物件讀取並傳回關聯屬性的值。 因此，如果您在表單的id欄位中指定00250，則讀取服務將讀取具有員工id00250員工的詳細資訊。
        <br>

      ![設定請求屬性](assets/request-attribute.png)

   1. 儲存屬性和表單資料模型。
1. 設定請求屬性的值：
   1. 在您的檔案系統上建立.json檔案，並開啟它以進行編輯。
   1. 建立JSON陣列並指定主要屬性，以從表單資料模型擷取資料。 例如，下列JSON會要求FDM傳送id為27126或27127的記錄資料：

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. 儲存並關閉檔案。

1. 建立 [Watched資料夾](/help/forms/using/creating-configure-watched-folder.md) 並將其設定為使用批次API服務：
   1. 登入AEM Forms作者執行個體。
   1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 設定Watched資料夾]**. 點選 **[!UICONTROL 新增]**.
   1. 指定 **[!UICONTROL 名稱]** 和實體 **[!UICONTROL 路徑]** 檔案夾的。 例如：`c:\batchprocessing`。
   1. 選取 **[!UICONTROL 服務]** 中的選項 **[!UICONTROL 處理檔案，使用]** 欄位。
   1. 選取 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 中的服務 **[!UICONTROL 服務名稱]** 欄位。
   1. 指定 **[!UICONTROL 輸出檔案模式]**. 例如，%F/ [圖樣](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定Watched資料夾可以在Watched資料夾\input資料夾的子資料夾中找到輸入檔案。
1. 設定進階引數：
   1. 開啟 **[!UICONTROL 進階]** 標籤並新增下列自訂屬性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | 範本路徑 | 字符串 | 指定要使用的互動式通訊範本路徑。 例如，/content/dam/formsanddocuments/testsample/mediumic。 這是強制屬性。 |
      | recordpath | 字符串 | recordPath欄位的值有助於設定互動式通訊的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果您指定/employee/Id，id欄位的值會變成對應互動式通訊的名稱。 預設值是隨機的 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | 布尔值 | 將值設定為True。 預設值為false。  當值設定為true時，批次API會從已設定的表單資料模型中讀取資料，並將其填入互動式通訊。 當usePrefillService設為true時，輸入JSON資料（每個記錄）會視為FDM引數。 |
      | batchType | 字符串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定輸出互動式通訊的地區設定。 現成服務不會使用地區設定選項，但您可以建立自訂服務以產生本地化的互動式通訊。 預設值為en_US。 |

   1. 點選 **[!UICONTROL 建立]** 已建立watched資料夾。
1. 使用watched資料夾產生互動式通訊：
   1. 開啟Watched資料夾。 導覽至輸入資料夾。
   1. 在輸入資料夾中建立資料夾。 將在步驟2中建立的JSON檔案置於新建立的資料夾中。
   1. 等候Watched資料夾處理檔案。 處理開始時，輸入檔案和包含該檔案的子資料夾會移至暫存資料夾。
   1. 開啟輸出資料夾以檢視輸出：
      * 當您在Watched資料夾組態中指定PRINT選項時，會產生互動式通訊的PDF輸出。
      * 當您在Watched資料夾設定中指定WEB選項時，會針對每筆記錄產生一個JSON檔案。 您可以使用JSON檔案來 [預先填入Web範本](#web-template).
      * 當您同時指定PRINT和WEB選項時，會針對每筆記錄同時產生PDF檔案和JSON檔案。

## 使用REST請求叫用批次API

您可以叫用 [批次API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 透過代表性狀態轉移(REST)請求。 它可讓您提供REST端點給其他使用者以存取API，並設定您自己的方法來處理、儲存和自訂互動式通訊。 您可以開發自己的自訂Java servlet，以便在您的AEM執行個體上部署API。

部署Java Servlet之前，請確保您已進行互動式通訊，且對應的資料檔案已準備就緒。 執行以下步驟來建立和部署Java servlet：

1. 登入您的AEM執行個體並建立互動式通訊。 若要使用下列範常式式碼中所述的互動式通訊， [按一下這裡](assets/SimpleMediumIC.zip).
1. [使用Apache Maven建置和部署AEM專案](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 在您的AEM執行個體上。
1. 新增 [AEM Forms使用者端SDK 6.0.12版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 在您的AEM專案的POM檔案的相依性清單中或更新版本。 例如，

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. 開啟Java專案，建立.java檔案，例如CCMBatchServlet.java。 将以下代码添加到该文件：

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. 在上述程式碼中，將範本路徑(setTemplatePath)取代為您的範本路徑，並設定setBatchType API的值：
   * 當您指定PRINT選項時，會產生互動式通訊的PDF輸出。
   * 當您指定WEB選項時，每個記錄都會產生JSON檔案。 您可以使用JSON檔案來 [預先填入Web範本](#web-template).
   * 當您同時指定PRINT和WEB選項時，會針對每筆記錄同時產生PDF檔案和JSON檔案。

1. [使用maven將更新的程式碼部署至您的AEM執行個體](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. 叫用批次API以產生互動式通訊。 批次API列印會根據記錄數量傳回PDF和.json檔案的串流。 您可以使用JSON檔案來 [預先填入Web範本](#web-template). 如果您使用上述程式碼，API會部署在 `http://localhost:4502/bin/batchServlet`. 程式碼會列印並傳回PDF和JSON檔案的串流。

### 預先填入Web範本 {#web-template}

當您設定batchType以轉譯Web Channel時，API會為每個資料記錄產生JSON檔案。 您可以使用以下語法將JSON檔案與對應的Web Channel合併，以產生互動式通訊：

**語法**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**範例**
如果您的JSON檔案位於 `C:\batch\mergedJsonPath.json` 而且您會使用下列互動式通訊範本： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

然後，發佈節點上的以下URL會顯示互動式通訊的Web Channel
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了將資料儲存在檔案系統外，您還能將JSON檔案儲存在CRX存放庫、檔案系統、網頁伺服器中，或透過OSGI預填服務存取資料。 使用各種通訊協定合併資料的語法如下：

* **CRX通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **檔案通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **預填服務通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME是指OSGI預填服務的名稱。 請參閱建立並執行預填服務。

   IDENTIFIER是指OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

* **http通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>預設只會啟用CRX通訊協定。 若要啟用其他支援的通訊協定，請參閱 [使用Configuration Manager設定預填服務](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
