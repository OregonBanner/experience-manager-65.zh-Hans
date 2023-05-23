---
title: 在電子郵件通知中使用中繼資料
seo-title: Use metadata in an email notification
description: 使用中繼資料在表單工作流程電子郵件通知中填入資訊
seo-description: Use metadata to populate information in a forms workflow email notification
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
exl-id: 18cfc4be-676d-4f08-afc1-4f11bb48dab6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# 在電子郵件通知中使用中繼資料 {#use-metadata-in-an-email-notification}

您可以使用「指派任務」步驟來建立任務並指派給使用者或群組。 當任務指派給使用者或群組時，會傳送電子郵件通知給已定義的使用者或已定義群組的每個成員。 典型 [電子郵件通知](../../forms/using/use-custom-email-template-assign-task-step.md) 包含已指派任務的連結及與任務相關的資訊。

您可以在電子郵件範本中使用中繼資料，以動態方式填入電子郵件通知中的資訊。 例如，下列電子郵件通知中的標題、說明、到期日、優先順序、工作流程和上次日期的值會在執行階段動態選取（產生電子郵件通知時）。

![預設電子郵件範本](assets/default_email_template_metadata_new.png)

中繼資料會儲存在索引鍵值配對中。 您可以在電子郵件範本中指定金鑰，而金鑰會在執行階段以值取代（產生電子郵件通知時）。 例如，在以下程式碼範例中，「$ {workitem_title}」是索引鍵。 在執行階段會以「Loan-Request」值取代。

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Please do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## 在電子郵件通知中使用系統產生的中繼資料 {#using-system-generated-metadata-in-an-email-notification}

AEM Forms應用程式提供數個立即可用的中繼資料變數（機碼值組）。 您可以在電子郵件範本中使用這些變數。 變數的值是根據關聯的表單應用程式。 下表列出所有立即可用的中繼資料變數：

<table>
 <tbody> 
  <tr> 
   <td>键</td> 
   <td>描述</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>相關表單應用程式的標題。</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>存取相關表單應用程式的URL。</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>相關表單應用程式的說明。</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>為關聯表單應用程式指定的優先順序。</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>對相關表單應用程式採取行動的最後日期。</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>與表單應用程式關聯的工作流程名稱。</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>將工作流程專案指派給目前受指派人的日期和時間。</td> 
  </tr> 
  <tr> 
   <td>workitem_assigner</td> 
   <td>目前被指定者的姓名。</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>作者伺服器的URL。 例如， https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>發佈伺服器的URL。 例如， https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## 在電子郵件通知中使用自訂中繼資料 {#using-custom-metadata-in-an-email-notification}

您也可以在電子郵件通知中使用自訂中繼資料。 自訂中繼資料除了包含系統產生的中繼資料外，也包含其他資訊。 例如，從資料庫擷取的原則詳細資訊。 您可以使用ECMAScript或OSGi套件組合在crx-repository中新增自訂中繼資料：

### 使用ECMAScript新增自訂中繼資料  {#use-ecmascript-to-add-custom-metadata}

[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) 是指令碼語言。 它用於使用者端指令碼和伺服器應用程式。 執行以下步驟，使用ECMAScript為電子郵件範本新增自訂中繼資料：

1. 使用管理帳戶登入CRX DE。 URL為https://&#39;[伺服器]：[連線埠]&#39;/crx/de/index.jsp

1. 導覽至/apps/fd/dashboard/scripts/metadataScripts。 建立副檔名為.ecma的檔案。 例如，usermetadata.ecma

   如果上述路徑不存在，請建立它。

1. 將程式碼新增至.ecma檔案，該檔案具有在索引鍵值配對中產生自訂中繼資料的邏輯。 例如，下列ECMAScript程式碼會為保單產生自訂中繼資料：

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. 按一下「儲存全部」。 現在，指令碼可在AEM工作流程模型中選擇。

   ![assigntask-metadata](assets/assigntask-metadata.png)

1. （選用）指定指令碼的標題：

   如果您未指定標題，自訂中繼資料欄位會顯示ECMAScript檔案的完整路徑。 執行以下步驟，為指令碼指定有意義的標題：

   1. 展開指令碼節點，用滑鼠右鍵按一下 **[!UICONTROL jcr：content]** 節點，然後按一下 **[!UICONTROL Mixin]**.
   1. 在「編輯Mixin」對話方塊中輸入mix：title並按一下 **+**.
   1. 新增具有以下值的屬性。

      | 名称 | jcr:title |
      |---|---|
      | 类型 | 字符串 |
      | 价值 | 指定指令碼的標題。 例如，原則持有者的自訂中繼資料。 指定的值會顯示在指派工作步驟中。 |

### 使用OSGi套件組合和Java介面來新增自訂中繼資料 {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

您可以使用WorkitemUserMetadataService Java介面為電子郵件範本新增自訂中繼資料。 您可以建立使用WorkitemUserMetadataService Java介面的OSGi套件組合，並將其部署至AEM Forms伺服器。 它使中繼資料可用於指派任務步驟中的選擇。

若要使用Java介面建立OSGi套件組合，請新增 [AEM Forms使用者端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) jar和 [granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 檔案做為OSGi套件專案的外部相依性。 您可以使用任何Java IDE來建立OSGi套件。 下列程式提供使用Eclipse建立OSGi套件的步驟：

1. 開啟Eclipse IDE。 導覽至「檔案>新增專案」。

1. 在「選取精靈」畫面上，選取「Maven專案」，然後按一下「下一步」。

1. 在新Maven專案中，保留預設值，然後按下一步。 選取一個原型，然後按下一步。 例如，maven-archetype-quickstart。 指定專案的群組ID、成品ID、版本和封裝，然後按一下完成。 專案已建立。

1. 開啟pom.xml檔案進行編輯，並將檔案的所有內容取代為下列內容：

1. 新增使用WorkitemUserMetadataService Java介面為電子郵件範本新增自訂中繼資料的原始程式碼。 程式碼範例如下：

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. 開啟命令提示字元並瀏覽至包含OSGi套件專案的目錄。 使用以下命令來建立OSGi套件：

   `mvn clean install`

1. 將套件組合上傳至AEM Forms伺服器。 您可以使用AEM封裝管理員將套件組合匯入至AEM Forms伺服器。

匯入束後，您可以在「指派任務」步驟中選取中繼資料，並將其用於電子郵件範本。
