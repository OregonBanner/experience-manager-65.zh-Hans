---
title: '在电子邮件通知中使用元数据 '
seo-title: '在电子邮件通知中使用元数据 '
description: 使用元数据在表单工作流电子邮件通知中填充信息
seo-description: 使用元数据在表单工作流电子邮件通知中填充信息
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---


# 在电子邮件通知中使用元数据 {#use-metadata-in-an-email-notification}

您可以使用分配任务步骤创建任务并将其分配给用户或用户组。 当任务被分配给用户或用户组时，将向已定义的用户或已定义用户组的每个成员发送电子邮件通知。 典型的 [电子邮件通](../../forms/using/use-custom-email-template-assign-task-step.md) 知包含指定任务的链接和与任务相关的信息。

您可以在电子邮件模板中使用元数据动态填充电子邮件通知中的信息。 例如，在运行时（生成电子邮件通知时）动态选择以下电子邮件通知中的标题、描述、到期日、优先级、工作流和最后日期的值。

![默认电子邮件模板](assets/default_email_template_metadata_new.png)

元数据以键值对的形式存储。 您可以在电子邮件模板中指定密钥，该密钥在运行时（生成电子邮件通知时）替换为值。 例如，在下面的代码示例中，“$ {workitem_title}”是键。 在运行时，它被替换为值“Loan-Request”。

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

## 在电子邮件通知中使用系统生成的元数据 {#using-system-generated-metadata-in-an-email-notification}

一个AEM Forms应用程序提供了多个开箱即用的元数据变量（键值对）。 您可以在电子邮件模板中使用这些变量。 变量的值基于关联的表单应用程序。 下表列表了所有可用的现成元数据变量：

<table>
 <tbody> 
  <tr> 
   <td>关键值</td> 
   <td>描述</td> 
  </tr> 
  <tr> 
   <td>工作项_标题</td> 
   <td>关联的表单应用程序的标题。</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>用于访问相关表单应用程序的URL。</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>关联表单应用程序的说明。</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>为关联的表单应用程序指定的优先级。</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>对关联的表单应用程序执行操作的上一个日期。</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>与表单应用程序关联的工作流的名称。</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>将工作流项目分配给当前被分派人的日期和时间。</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>当前被分派人的名称。</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>作者服务器的URL。 例如，https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>发布服务器的URL。 例如，https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## 在电子邮件通知中使用自定义元数据 {#using-custom-metadata-in-an-email-notification}

您还可以在电子邮件通知中使用自定义元数据。 自定义元数据除了包含系统生成的元数据之外，还包含信息。 例如，从数据库检索到的策略详细信息。 可以使用ECMAScript或OSGi捆绑在crx-repository中添加自定义元数据：

### 使用ECMAScript添加自定义元数据  {#use-ecmascript-to-add-custom-metadata}

[ECMAScript是](https://en.wikipedia.org/wiki/ECMAScript) 一种脚本语言。 它用于客户端脚本和服务器应用程序。 请执行以下步骤以使用ECMAScript为电子邮件模板添加自定义元数据：

1. 使用管理帐户登录CRX DE。 URL为https://&#39;[server]:[port]&#39;/crx/de/index.jsp

1. 导航到/apps/fd/仪表板/scripts/metadataScripts。 创建扩展名为。ecma的文件。 例如，usermetadata.ecma

   如果上述路径不存在，请创建它。

1. 向。ecma文件添加代码，该文件具有在键值对中生成自定义元数据的逻辑。 例如，以下ECMAScript代码为保险单生成自定义元数据：

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

1. 单击“全部保存”。 现在，该脚本可在AEM工作流模型中进行选择。

   ![分配任务——元数据](assets/assigntask-metadata.png)

1. （可选）指定脚本的标题：

   如果不指定标题，则“自定义元数据”字段将显示ECMAScript文件的完整路径。 请执行以下步骤为脚本指定有意义的标题：

   1. 展开脚本节点，右键单击 **[!UICONTROL jcr:content节点]** ，然后单击 **[!UICONTROL Mixins]**。
   1. 在“编辑混音”对话框中键入mix:title，然 **后单击**+。
   1. 添加具有以下值的属性。

      | 名称 | jcr:title |
      |---|---|
      | 类型 | 字符串 |
      | 值 | 指定脚本的标题。 例如，策略持有者的自定义元数据。 指定值显示在分配任务步骤中。 |

### 使用OSGi捆绑和Java界面添加自定义元数据 {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

您可以使用WorkitemUserMetadataService Java界面为电子邮件模板添加自定义元数据。 您可以创建使用WorkitemUserMetadataService Java界面的OSGi捆绑包，并将其部署到AEM Forms服务器。 它使元数据可在分配任务步骤中进行选择。

要创建带有Java界面的OSGi捆绑，请将 [AEM Forms客户端](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) SDK jar和 [granite jar文件](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 添加为OSGi捆绑项目的外部依赖项。 您可以使用任何Java IDE创建OSGi捆绑。 以下过程提供了使用Eclipse创建OSGi捆绑包的步骤：

1. 打开Eclipse IDE。 导航到“文件”>“新建项目”。

1. 在“选择向导”屏幕上，选择“创建项目”，然后单击“下一步”。

1. 在New Maven项目中，保留默认值，然后单击“下一步”。 选择原型并单击“下一步”。 例如，maven-archetype-quickstart。 为项目指定组ID、对象ID、版本和包，然后单击“完成”。 将创建项目。

1. 打开pom.xml文件进行编辑，并将文件的所有内容替换为以下内容：

1. 添加使用WorkitemUserMetadataService Java界面为电子邮件模板添加自定义元数据的源代码。 示例代码如下所示：

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

1. 打开命令提示符并导航到包含OSGi捆绑项目的目录。 使用以下命令创建OSGi包：

   `mvn clean install`

1. 将捆绑包上传到AEM Forms服务器。 您可以使用AEM包管理器将包导入AEM Forms服务器。

导入捆绑包后，您可以在分配任务步骤中选择元数据，并将其用作电子邮件模板。
