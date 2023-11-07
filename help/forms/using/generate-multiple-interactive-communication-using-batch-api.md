---
title: 使用批处理API生成多个交互式通信
description: 使用批处理API生成多个交互式通信
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 1%

---

# 使用批处理API生成多个交互式通信 {#use-batch-api-to-generate-multiple-ic}

您可以使用批处理API从模板生成多个交互式通信。 模板是一种没有任何数据的交互式通信。 批处理API将数据与模板结合起来以生成交互式通信。 该API在交互式通信的大量生产中非常有用。 例如，电话帐单、多个客户的信用卡对帐单。

批处理API接受JSON格式和表单数据模型中的记录（数据）。 生成的交互式通信数量等于在配置的表单数据模型中的输入JSON文件中指定的记录。 您可以使用API生成打印和Web输出。 PRINT选项会生成一个PDF文档，而WEB选项会为每个单独的记录生成JSON格式的数据。

## 使用批处理API {#using-the-batch-api}

您可以将批处理API与Watched文件夹结合使用，或作为独立的Rest API使用。 为使用批处理API生成的交互式通信配置模板、输出类型(HTML、打印或两者)、区域设置、预填充服务和名称。

将记录与交互式通信模板结合以生成交互式通信。 批处理API可以直接从JSON文件或通过表单数据模型访问的外部数据源读取记录（交互式通信模板的数据）。 您可以将每个记录保存在单独的JSON文件中，也可以创建JSON数组以将所有记录保存在单个文件中。

**JSON文件中的单个记录**

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

**JSON文件中的多个记录**

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

### 将批处理API与Watched文件夹一起使用 {#using-the-batch-api-watched-folders}

为了更便于体验API，AEM Forms现成提供了配置为使用批处理API的Watched文件夹服务。 您可以通过AEM Forms UI访问该服务，以生成多个交互式通信。 您还可以根据要求创建自定义服务。 您可以使用下列方法将批处理API与Watched文件夹一起使用：

* 指定采用JSON文件格式的输入数据（记录）以生成交互式通信
* 使用保存在外部数据源中并通过表单数据模型访问的输入数据（记录）产生交互式通信

#### 指定JSON文件格式的输入数据记录以生成交互式通信 {#specify-input-data-in-JSON-file-format}

将记录与交互式通信模板结合以生成交互式通信。 您可以为每个记录创建单独的JSON文件，或创建一个JSON数组以将所有记录保留在单个文件中：

要根据保存在JSON文件中的记录创建交互式通信，请执行以下操作：

1. 创建 [观察文件夹](/help/forms/using/creating-configure-watched-folder.md) 并将其配置为使用批处理API：
   1. 登录到AEM Forms创作实例。
   1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置Watched文件夹]**. 点按 **[!UICONTROL 新建]**.
   1. 指定 **[!UICONTROL 名称]** 和物理 **[!UICONTROL 路径]** 文件夹的。 例如：`c:\batchprocessing`。
   1. 选择 **[!UICONTROL 服务]** 中的选项 **[!UICONTROL 处理文件，使用]** 字段。
   1. 选择 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 中的服务 **[!UICONTROL 服务名称]** 字段。
   1. 指定 **[!UICONTROL 输出文件模式]**. 例如，%F/ [模式](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定Watched文件夹可以在Watched文件夹\input文件夹的子文件夹中找到输入文件。
1. 配置高级参数：
   1. 打开 **[!UICONTROL 高级]** 选项卡并添加以下自定义属性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | templatepath | 字符串 | 指定要使用的交互式通信模板的路径。 例如，/content/dam/formsanddocuments/testsample/mediumic。 它是必需属性。 |
      | recordpath | 字符串 | recordPath字段的值有助于设置交互式通信的名称。 您可以将记录字段的路径设置为recordPath字段的值。 例如，如果指定/employee/Id，则id字段的值将成为相应交互式通信的name。 默认值为随机 [随机UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | 布尔值 | 将值设置为False。 可以使用usePrefillService参数预填充交互式通信，该数据是从为相应的交互式通信配置的预填充服务中获取的数据的。 当usePrefillService设置为true时，输入JSON数据（每个记录）将被视为FDM参数。 默认值为false。 |
      | batchtype | 字符串 | 将值设置为PRINT、WEB或WEB_AND_PRINT。 缺省值为WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定输出交互式通信的区域设置。 现成服务不使用区域设置选项，但您可以创建自定义服务来生成本地化的交互式通信。 默认值为en_US |

   1. 点按 **[!UICONTROL 创建]** 已创建观察文件夹。
1. 使用watched文件夹生成交互式通信：
   1. 打开Watched文件夹 导航到输入文件夹。
   1. 在输入文件夹中创建文件夹，并将JSON文件放在新创建的文件夹中。
   1. 等待Watched文件夹处理文件。 处理开始时，输入文件和包含该文件的子文件夹将移至暂存文件夹。
   1. 打开输出文件夹以查看输出：
      * 在Watched文件夹配置中指定PRINT选项时，将生成交互式通信的PDF输出。
      * 在监视文件夹配置中指定WEB选项时，将为每个记录生成一个JSON文件。 您可以使用JSON文件来 [预填充Web模板](#web-template).
      * 当您同时指定PRINT和WEB选项时，将生成PDF文档以及每个记录的JSON文件。

#### 使用保存在外部数据源中并通过表单数据模型访问的输入数据产生交互式通信 {#use-fdm-as-data-source}

将保存在外部数据源中的数据（记录）与交互式通信模板组合在一起，生成交互式通信。 创建交互式通信时，可通过表单数据模型(FDM)将其连接到外部数据源以访问数据。 您可以将Watched Folders批处理服务配置为使用相同的表单数据模型从外部数据源提取数据。 至 [使用保存在外部数据源中的记录创建交互式通信](/help/forms/using/work-with-form-data-model.md)：

1. 配置模板的表单数据模型：
   1. 打开与交互式通信模板关联的表单数据模型。
   1. 选择您的顶级模型对象，然后点按编辑属性。
   1. 从编辑属性窗格下的读取服务字段中选择获取或获取服务。
   1. 点击读取服务参数的铅笔图标以将参数绑定到请求属性并指定绑定值。 它将服务参数绑定到指定的绑定属性或文本值，该属性或文本值作为参数传递给服务，以从数据源获取与指定值关联的详细信息。

      <br>
        在此示例中，id参数接受用户配置文件的id属性的值，并将其作为参数传递给读取服务。 它将从指定ID的员工数据模型对象中读取并返回关联属性的值。 因此，如果您在表单的id字段中指定00250，则读取服务将读取具有员工id的员工00250详细信息。
        <br>

      ![配置请求属性](assets/request-attribute.png)

   1. 保存属性和表单数据模型。
1. 配置请求属性的值：
   1. 在文件系统上创建一个.json文件并打开它进行编辑。
   1. 创建JSON数组并指定从表单数据模型提取数据的主要属性。 例如，以下JSON请求FDM发送id为27126或27127的记录的数据：

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

   1. 保存并关闭该文件。

1. 创建 [观察文件夹](/help/forms/using/creating-configure-watched-folder.md) 并将其配置为使用批处理API服务：
   1. 登录到AEM Forms创作实例。
   1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置Watched文件夹]**. 点按 **[!UICONTROL 新建]**.
   1. 指定 **[!UICONTROL 名称]** 和物理 **[!UICONTROL 路径]** 文件夹的。 例如：`c:\batchprocessing`。
   1. 选择 **[!UICONTROL 服务]** 中的选项 **[!UICONTROL 处理文件，使用]** 字段。
   1. 选择 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 中的服务 **[!UICONTROL 服务名称]** 字段。
   1. 指定 **[!UICONTROL 输出文件模式]**. 例如，%F/ [模式](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定Watched文件夹可以在Watched文件夹\input文件夹的子文件夹中找到输入文件。
1. 配置高级参数：
   1. 打开 **[!UICONTROL 高级]** 选项卡并添加以下自定义属性：

      | 属性 | 类型 | 描述 |
      |--- |--- |--- |
      | templatepath | 字符串 | 指定要使用的交互式通信模板的路径。 例如，/content/dam/formsanddocuments/testsample/mediumic。 它是必需属性。 |
      | recordpath | 字符串 | recordPath字段的值有助于设置交互式通信的名称。 您可以将记录字段的路径设置为recordPath字段的值。 例如，如果指定/employee/Id，则id字段的值将成为相应交互式通信的name。 默认值为随机 [随机UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | 布尔值 | 将该值设置为True。 默认值为false。  当该值设置为true时，批处理API会从配置的表单数据模型中读取数据，并将其填充到交互式通信中。 当usePrefillService设置为true时，输入JSON数据（每个记录）将被视为FDM参数。 |
      | batchtype | 字符串 | 将值设置为PRINT、WEB或WEB_AND_PRINT。 缺省值为WEB_AND_PRINT。 |
      | 区域设置 | 字符串 | 指定输出交互式通信的区域设置。 现成服务不使用区域设置选项，但您可以创建自定义服务来生成本地化的交互式通信。 缺省值为en_US。 |

   1. 点按 **[!UICONTROL 创建]** 已创建观察文件夹。
1. 使用watched文件夹生成交互式通信：
   1. 打开Watched文件夹 导航到输入文件夹。
   1. 在输入文件夹中创建文件夹。 将在步骤2中创建的JSON文件放入新创建的文件夹中。
   1. 等待Watched文件夹处理文件。 处理开始时，输入文件和包含该文件的子文件夹将移至暂存文件夹。
   1. 打开输出文件夹以查看输出：
      * 在Watched文件夹配置中指定PRINT选项时，将生成交互式通信的PDF输出。
      * 在监视文件夹配置中指定WEB选项时，将为每个记录生成一个JSON文件。 您可以使用JSON文件来 [预填充Web模板](#web-template).
      * 当您同时指定PRINT和WEB选项时，将生成PDF文档以及每个记录的JSON文件。

## 使用REST请求调用批处理API

您可以调用 [批处理API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 通过代表性状态传输(REST)请求。 通过它，您可以向其他用户提供REST端点来访问API，并配置您自己的方法来处理、存储和自定义交互式通信。 您可以开发自己的自定义Java servlet来在AEM实例上部署API。

在部署Java Servlet之前，请确保您具有交互式通信并且相应的数据文件已准备就绪。 执行以下步骤创建和部署Java servlet：

1. 登录AEM实例并创建交互式通信。 要使用下面给出的示例代码中所述的交互式通信， [单击此处](assets/SimpleMediumIC.zip).
1. [使用Apache Maven构建和部署AEM项目](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 在您的AEM实例上。
1. 添加 [AEM Forms客户端SDK版本6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) AEM项目的POM文件的依赖关系列表中或更高版本。 例如，

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. 打开Java项目，创建一个.java文件，例如CCMBatchServlet.java。 将以下代码添加到该文件：

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

1. 在上述代码中，将模板路径(setTemplatePath)替换为模板的路径，并设置setBatchType API的值：
   * 指定PRINT选项时，将生成交互式通信的PDF输出。
   * 当您指定WEB选项时，将为每个记录生成一个JSON文件。 您可以使用JSON文件来 [预填充Web模板](#web-template).
   * 当您同时指定PRINT和WEB选项时，将生成PDF文档以及每个记录的JSON文件。

1. [使用maven将更新的代码部署到AEM实例](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. 调用批处理API以生成交互式通信。 批处理API打印根据记录数返回PDF流和.json文件。 您可以使用JSON文件来 [预填充Web模板](#web-template). 如果您使用上述代码，则API部署在 `http://localhost:4502/bin/batchServlet`. 该代码会打印并返回PDF流和JSON文件。

### 预填充Web模板 {#web-template}

当您设置batchType以渲染Web渠道时，API会为每个数据记录生成一个JSON文件。 您可以使用以下语法将JSON文件与相应的Web渠道合并以生成交互式通信：

**语法**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**示例**
如果您的JSON文件位于 `C:\batch\mergedJsonPath.json` 并使用以下交互式通信模板： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

然后，发布节点上的以下URL显示了交互式通信的Web渠道
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了将数据保存在文件系统上，还可将JSON文件存储在CRX存储库、文件系统、Web服务器中，或通过OSGI预填充服务访问数据。 使用各种协议合并数据的语法如下：

* **CRX协议**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **文件协议**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **预填充服务协议**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

  SERVICE_NAME是指OSGI预填充服务的名称。 请参阅创建并运行预填充服务。

  标识符是指OSGI预填充服务获取预填充数据所需的任何元数据。 登录用户的标识符是可以使用的元数据的示例。

* **HTTP协议**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>默认情况下仅启用CRX协议。 要启用其他支持的协议，请参见 [使用配置管理器配置预填充服务](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
