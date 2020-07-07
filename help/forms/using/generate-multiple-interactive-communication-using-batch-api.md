---
title: 使用Batch API生成多个交互式通信
description: 使用Batch API生成多个交互式通信
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---


# 使用Batch API生成多个交互式通信 {#use-batch-api-to-generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 模板是无任何数据的交互式通信。 批处理API将数据与模板相结合以生成交互式通信。 API在大规模制作交互式通信中非常有用。 例如，电话单、多个客户的信用卡对帐单。

批处理API接受JSON格式和表单数据模型中的记录（数据）。 生成的交互式通信数等于配置的表单数据模型中输入JSON文件中指定的记录。 您可以使用API生成打印和Web输出。 “打印”选项会生成PDF文档，而“WEB”选项会为每个单独的记录生成JSON格式的数据。

## 使用Batch API {#using-the-batch-api}

您可以将Batch API与监视文件夹结合使用，也可以作为独立的Rest API。 为生成的交互式通信配置模板、输出类型（HTML、PRINT或Both）、区域设置、预填服务和名称，以使用批处理API。

您将记录与交互式通信模板相结合以生成交互式通信。 批处理API可以直接从JSON文件或通过表单数据模型访问的外部数据源读取记录（交互式通信模板的数据）。 您可以将每个记录保存在单独的JSON文件中，或创建JSON数组以将所有记录保存在单个文件中。

**JSON文件中的单个记录**

```JSON
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON文件中的多个记录**

```JSON
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

### 将Batch API用于监视文件夹 {#using-the-batch-api-watched-folders}

为了方便地体验API,AEM Forms提供已配置为使用批处理API的监视文件夹服务。 您可以通过AEM FormsUI访问服务以生成多个交互式通信。 您还可以根据需要创建自定义服务。 您可以使用下面列出的方法将Batch API用于监视文件夹：

* 以JSON文件格式指定输入数据（记录）以生成交互式通信
* 使用保存在外部数据源中并通过表单数据模型访问的输入数据（记录）产生交互式通信

#### 指定JSON文件格式的输入数据记录以生成交互式通信 {#specify-input-data-in-JSON-file-format}

您将记录与交互式通信模板相结合以生成交互式通信。 您可以为每个记录单独创建一个JSON文件，也可以创建一个JSON数组，将所有记录保存在一个文件中：

要从JSON文件中保存的记录创建交互式通信，请执行以下操作：

1. 创建“ [监视”文](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 件夹并将其配置为使用Batch API:
   1. 登录到AEM Forms作者实例。
   1. 导航到 **[!UICONTROL 工具]** >表 **[!UICONTROL 单]** > **[!UICONTROL 配置监]**&#x200B;视文件夹。 点按 **[!UICONTROL 新建]**。
   1. 指定文 **[!UICONTROL 件夹]** 的名 **[!UICONTROL 称和]** 物理路径。 For example, `c:\batchprocessing`.
   1. 在“进程 **[!UICONTROL 文件]** ：使用”字 **[!UICONTROL 段中选择“服务]** ”选项。
   1. 在“服 **[!UICONTROL 务名称”字段中选择com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchService]** Impl **[!UICONTROL 服务]** 。
   1. 指定输 **[!UICONTROL 出文件模式]**。 例如，%F/模式 [指定](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) “监视文件夹”可在“监视文件夹\输入”文件夹的子文件夹中查找输入文件。
1. 配置高级参数：
   1. 打开“高 **[!UICONTROL 级]** ”选项卡并添加以下自定义属性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | templatePath | 字符串 | 指定要使用的交互式通信模板的路径。 例如，/content/dam/formsanddocuments/testsample/mediamic。 它是强制属性。 |
      | recordPath | 字符串 | recordPath字段的值有助于设置交互通信的名称。 可以将记录字段的路径设置为recordPath字段的值。 例如，如果指定/employee/Id,id字段的值将变为相应交互通信的名称。 默认值是随机随 [机UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |
      | usePrefillService | 布尔型 | 将该值设置为False。 您可以使用usePrefillService参数使用从为相应的交互式通信配置的预填服务获取的数据预填交互式通信。 当usePrefillService设置为true时，输入JSON数据（对于每个记录）将被视为FDM参数。 默认值为false。 |
      | batchType | 字符串 | 将值设置为PRINT、WEB或WEB_AND_PRINT。 默认值为WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定输出交互式通信的区域设置。 现成的服务不使用区域设置选项，但您可以创建自定义服务以生成本地化的交互式通信。 默认值为en_US |

   1. 点按 **[!UICONTROL 创建]** 已创建监视的文件夹。
1. 使用监视的文件夹生成交互式通信：
   1. 打开监视文件夹。 导航到输入文件夹。
   1. 在输入文件夹中创建一个文件夹，然后将JSON文件放在新创建的文件夹中。
   1. 等待“监视文件夹”处理文件。 处理开始时，包含该文件的输入文件和子文件夹将移至暂存文件夹。
   1. 打开输出文件夹以视图输出：
      * 在“监视文件夹配置”中指定“打印”选项时，将生成交互式通信的PDF输出。
      * 在“监视文件夹配置”中指定WEB选项时，将生成每个记录的JSON文件。 您可以使用JSON文 [件预填Web模板](#web-template)。
      * 指定“打印”和“网络”选项时，将生成PDF文档和每个记录的JSON文件。

#### 使用保存在外部数据源中并通过表单数据模型访问的输入数据来产生交互式通信 {#use-fdm-as-data-source}

您将保存在外部数据源中的数据（记录）与交互式通信模板相结合，以生成交互式通信。 创建交互式通信时，可通过表单数据模型(FDM)将其连接到外部数据源以访问数据。 您可以配置“监视文件夹”批处理服务，以从外部数据源使用相同的表单数据模型获取数据。 要根 [据保存在外部数据源中的记录创建交互式通信，请执行以下操作](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. 配置模板的表单数据模型：
   1. 打开与交互式通信模板关联的表单数据模型。
   1. 选择顶级模型对象，然后点按编辑属性。
   1. 从“编辑属性”窗格下的“读取服务”字段选择提取或获取服务。
   1. 点按读取服务参数的铅笔图标，将参数绑定到请求属性并指定绑定值。 它将服务参数绑定到指定的绑定属性或文本值，该值作为参数传递给服务以从数据源获取与指定值关联的详细信息。

      <br>
        在此示例中，id参数使用用户用户档案的id属性值并将其作为参数传递给读取服务。 它将从员工数据模型对象中读取并返回指定id的关联属性值。 因此，如果您在表单的id字段中指定00250，则读取服务将读取具有00250员工id的员工的详细信息。
        <br>

      ![配置请求属性](assets/request-attribute.png)

   1. 保存属性和表单数据模型。
1. 为请求属性配置值：
   1. 在文件系统上创建。json文件并打开它进行编辑。
   1. 创建JSON数组并指定从表单数据模型获取数据的主属性。 例如，以下JSON请求FDM发送id为27126或27127的记录数据：

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

   1. 保存并关闭文件。

1. 创建“ [监视”文](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 件夹并将其配置为使用Batch API服务：
   1. 登录到AEM Forms作者实例。
   1. 导航到 **[!UICONTROL 工具]** >表 **[!UICONTROL 单]** > **[!UICONTROL 配置监]**&#x200B;视文件夹。 点按 **[!UICONTROL 新建]**。
   1. 指定文 **[!UICONTROL 件夹]** 的名 **[!UICONTROL 称和]** 物理路径。 For example, `c:\batchprocessing`.
   1. 在“进程 **[!UICONTROL 文件]** ：使用”字 **[!UICONTROL 段中选择“服务]** ”选项。
   1. 在“服 **[!UICONTROL 务名称”字段中选择com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchService]** Impl **[!UICONTROL 服务]** 。
   1. 指定输 **[!UICONTROL 出文件模式]**。 例如，%F/模式 [指定](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) “监视文件夹”可在“监视文件夹\输入”文件夹的子文件夹中查找输入文件。
1. 配置高级参数：
   1. 打开“高 **[!UICONTROL 级]** ”选项卡并添加以下自定义属性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | templatePath | 字符串 | 指定要使用的交互式通信模板的路径。 例如，/content/dam/formsanddocuments/testsample/mediamic。 它是强制属性。 |
      | recordPath | 字符串 | recordPath字段的值有助于设置交互通信的名称。 可以将记录字段的路径设置为recordPath字段的值。 例如，如果指定/employee/Id,id字段的值将变为相应交互通信的名称。 默认值是随机随 [机UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |  |
      | usePrefillService | 布尔型 | 将该值设置为True。 默认值为false。  当该值设置为true时，Batch API将从配置的表单数据模型读取数据并将其填充到交互式通信中。 当usePrefillService设置为true时，输入JSON数据（对于每个记录）将被视为FDM参数。 |
      | batchType | 字符串 | 将值设置为PRINT、WEB或WEB_AND_PRINT。 默认值为WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定输出交互式通信的区域设置。 现成的服务不使用区域设置选项，但您可以创建自定义服务以生成本地化的交互式通信。 默认值为en_US。 |

   1. 点按 **[!UICONTROL 创建]** 已创建监视的文件夹。
1. 使用监视的文件夹生成交互式通信：
   1. 打开监视文件夹。 导航到输入文件夹。
   1. 在输入文件夹中创建文件夹。 将在步骤2中创建的JSON文件放在新创建的文件夹中。
   1. 等待“监视文件夹”处理文件。 处理开始时，包含该文件的输入文件和子文件夹将移至暂存文件夹。
   1. 打开输出文件夹以视图输出：
      * 在“监视文件夹配置”中指定“打印”选项时，将生成交互式通信的PDF输出。
      * 在“监视文件夹配置”中指定WEB选项时，将生成每个记录的JSON文件。 您可以使用JSON文 [件预填Web模板](#web-template)。
      * 指定“打印”和“网络”选项时，将生成PDF文档和每个记录的JSON文件。

## 使用REST请求调用批处理API

您可以通 [过代表性状态传](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 输(REST)请求调用批处理API。 它允许您向其他用户提供一个REST端点，以访问API并配置您自己的方法来处理、存储和自定义交互式通信。 您可以开发自己的自定义Java servlet以在AEM实例上部署API。

在部署Java servlet之前，请确保具有交互式通信并准备好相应的数据文件。 请执行以下步骤以创建和部署Java servlet:

1. 登录到AEM实例并创建交互式通信。 要使用下面给出的示例代码中提到的交互式通信，请单 [击此处](assets/SimpleMediumIC.zip)。
1. [在AEM实例上使用Apache Maven构建和部署](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) AEM项目。
1. 在 [AEM项目的POM文件的依赖项列表中](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) 添加AEM Forms客户端SDK版本6.0.12或更高版本。 例如，

   ```XML
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. 打开Java项目，创建。java文件，例如CCMBatchServlet.java。 将以下代码添加到文件：

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

1. 在上面的代码中，将模板路径(setTemplatePath)替换为模板的路径并设置setBatchType API的值：
   * 当您为交互式通信指定“打印”选项时，将生成PDF输出。
   * 指定WEB选项时，将生成每个记录的JSON文件。 您可以使用JSON文 [件预填Web模板](#web-template)。
   * 指定“打印”和“网络”选项时，将生成PDF文档和每个记录的JSON文件。

1. [使用maven将更新的代码部署到AEM实例](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven)。
1. 调用批处理API以生成交互式通信。 批处理API会根据记录数返回PDF和。json文件流。 您可以使用JSON文 [件预填Web模板](#web-template)。 如果您使用上述代码，则在部署API `http://localhost:4502/bin/batchServlet`。 该代码打印并返回PDF和JSON文件流。

### 预填Web模板 {#web-template}

将batchType设置为呈现Web渠道时，API会为每个数据记录生成一个JSON文件。 您可以使用以下语法将JSON文件与相应的Web渠道合并，以生成交互式通信：

**语法**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**示例**，如果您的JSON文件位于， `C:\batch\mergedJsonPath.json` 并且您使用以下交互式通信模板： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

然后，发布节点上的以下URL将显示交互式通信的Web渠道
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了在文件系统上保存数据外，您还可以将JSON文件存储在CRX-repository、文件系统、Web服务器中，或者可以通过OSGI预填服务访问数据。 使用各种协议合并数据的语法有：

* **CRX协议**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **文件协议**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **预填服务协议**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME指OSGI预填服务的名称。 请参阅创建并运行预填服务。

   标识符指OSGI预填服务获取预填数据所需的任何元数据。 登录用户的标识符是可以使用的元数据示例。

* **HTTP协议**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>默认情况下，仅启用CRX协议。 要启用其他受支持的协议，请参 [阅使用Configuration Manager配置预填服务](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)。
