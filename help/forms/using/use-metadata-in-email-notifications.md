---
title: '在电子邮件通知中使用元数据 '
seo-title: '在电子邮件通知中使用元数据 '
description: 使用元数据在表单工作流电子邮件通知中填充信息
seo-description: 使用元数据在表单工作流电子邮件通知中填充信息
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
exl-id: 18cfc4be-676d-4f08-afc1-4f11bb48dab6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# 在电子邮件通知{#use-metadata-in-an-email-notification}中使用元数据

您可以使用“分配任务”步骤创建任务并将任务分配给用户或组。 将任务分配给用户或组后，将向定义的用户或定义组的每个成员发送电子邮件通知。 典型的[电子邮件通知](../../forms/using/use-custom-email-template-assign-task-step.md)包含已分配任务的链接以及与任务相关的信息。

您可以在电子邮件模板中使用元数据动态填充电子邮件通知中的信息。 例如，在运行时（生成电子邮件通知时）会动态选择以下电子邮件通知中的标题、描述、到期日期、优先级、工作流和最后日期的值。

![默认电子邮件模板](assets/default_email_template_metadata_new.png)

元数据存储在键值对中。 您可以在电子邮件模板中指定键，并在运行时（在生成电子邮件通知时）将键替换为值。 例如，在以下代码示例中，“$ {workitem_title} ”是一个键。 在运行时，它将被值“Loan-Request”替换。

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

## 在电子邮件通知{#using-system-generated-metadata-in-an-email-notification}中使用系统生成的元数据

AEM Forms应用程序提供了一些开箱即用的元数据变量（键值对）。 您可以在电子邮件模板中使用这些变量。 变量的值基于关联的表单应用程序。 下表列出了所有现成可用的元数据变量：

<table>
 <tbody> 
  <tr> 
   <td>键</td> 
   <td>描述</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>关联的表单应用程序的标题。</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>用于访问关联的表单应用程序的URL。</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>关联表单应用程序的描述。</td> 
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
   <td>将工作流项目分配给当前代理人的日期和时间。</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>当前受让人的名称。</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>作者服务器的URL。 例如， https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>发布服务器的URL。 例如， https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## 在电子邮件通知{#using-custom-metadata-in-an-email-notification}中使用自定义元数据

您还可以在电子邮件通知中使用自定义元数据。 自定义元数据除包含系统生成的元数据之外，还包含其他信息。 例如，从数据库检索的策略详细信息。 您可以使用ECMAScript或OSGi包在crx-repository中添加自定义元数据：

### 使用ECMAScript添加自定义元数据{#use-ecmascript-to-add-custom-metadata}

[](https://en.wikipedia.org/wiki/ECMAScript) ECMAScriptis是一种脚本语言。它用于客户端脚本和服务器应用程序。 执行以下步骤以使用ECMAScript为电子邮件模板添加自定义元数据：

1. 使用管理帐户登录到CRX DE。 URL是https://&#39;[server]:[port]&#39;/crx/de/index.jsp

1. 导航到/apps/fd/dashboard/scripts/metadataScripts。 创建扩展名为.ecma的文件。 例如， usermetadata.ecma

   如果上述路径不存在，请创建该路径。

1. 将代码添加到.ecma文件中，该文件具有在键值对中生成自定义元数据的逻辑。 例如，以下ECMAScript代码为保险单生成自定义元数据：

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

1. 单击“全部保存”。 现在，该脚本可供在AEM工作流模型中进行选择。

   ![赋值任务 — 元数据](assets/assigntask-metadata.png)

1. （可选）指定脚本的标题：

   如果未指定标题，“自定义元数据”字段将显示ECMAScript文件的完整路径。 执行以下步骤为脚本指定有意义的标题：

   1. 展开脚本节点，右键单击&#x200B;**[!UICONTROL jcr:content]**&#x200B;节点，然后单击&#x200B;**[!UICONTROL Mixins]**。
   1. 在“编辑混合”对话框中键入mix:title ，然后单击&#x200B;**+**。
   1. 添加具有以下值的属性。

      | 名称 | jcr:title |
      |---|---|
      | 类型 | 字符串 |
      | 值 | 指定脚本的标题。 例如，策略持有者的自定义元数据。 指定的值显示在分配任务步骤中。 |

### 使用OSGi包和Java接口添加自定义元数据{#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

您可以使用WorkitemUserMetadataService Java界面为电子邮件模板添加自定义元数据。 您可以创建使用WorkitemUserMetadataService Java界面的OSGi包，并将其部署到AEM Forms服务器。 它使元数据可供在分配任务步骤中进行选择。

要使用Java界面创建OSGi包，请将[AEM Forms客户端SDK](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) jar和[granite jar](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/)文件添加为OSGi包项目的外部依赖项。 可以使用任何Java IDE创建OSGi包。 以下过程提供了使用Eclipse创建OSGi包的步骤：

1. 打开Eclipse IDE。 导航到文件>新建项目。

1. 在选择向导屏幕上，选择Maven项目，然后单击下一步。

1. 在New Maven项目中，保留默认值，然后单击“下一步”。 选择原型，然后单击“下一步”。 例如，maven-archetype-quickstart。 为项目指定组ID、对象ID、版本和包，然后单击“完成”。 随即会创建项目。

1. 打开pom.xml文件进行编辑，并将文件的所有内容替换为以下内容：

1. 添加使用WorkitemUserMetadataService Java界面为电子邮件模板添加自定义元数据的源代码。 下面列出了示例代码：

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

1. 打开命令提示符，然后导航到包含OSGi包项目的目录。 使用以下命令创建OSGi包：

   `mvn clean install`

1. 将包上载到AEM Forms服务器。 您可以使用AEM包管理器将包导入AEM Forms服务器。

导入包后，您可以在“分配任务”步骤中选择元数据，并将其用作电子邮件模板。
