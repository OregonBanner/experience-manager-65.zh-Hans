---
title: 为以AEM Forms为中心的工作流步骤动态选择用户或用户组
seo-title: 为以AEM Forms为中心的工作流步骤动态选择用户或用户组
description: '了解如何在运行时为AEM Forms工作流选择用户或用户组。 '
seo-description: '了解如何在运行时为AEM Forms工作流选择用户或用户组。 '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 997a35b331385738a8d4a3fcab89c950ed4b7d33

---


# 为以AEM Forms为中心的工作流步骤动态选择用户或用户组 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

了解如何在运行时为AEM Forms工作流选择用户或用户组。

在大型组织中，有要求动态选择流程的用户。 例如，根据代理与客户的接近度选择现场代理来为客户服务。 在这种情况下，将动态选择代理。

在OSGi上指定以表单为中心的 [工作流的任务和Adobe Sign步骤](/help/forms/using/aem-forms-workflow.md) ，为动态选择用户提供选项。 可以使用ECMAScript或OSGi捆绑包动态选择“分配任务”步骤的被分派人，或选择“签名文档”步骤的签署人。

## 使用ECMAScript动态选择用户或用户组 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一种脚本语言。 它用于客户端脚本和服务器应用程序。 执行以下步骤以使用ECMAScript动态选择用户或用户组：

1. 打开CRXDE Lite。 URL为 `https://'[server]:[port]'/crx/de/index.jsp`
1. 在以下路径创建扩展名为。ecma的文件。 如果路径（节点结构）不存在，请创建它：

   * (分配任务步骤的路径) `/apps/fd/dashboard/scripts/participantChooser`
   * （签名路径步骤） `/apps/fd/workflow/scripts/adobesign`

1. 将具有动态选择用户的逻辑的ECMAScript添加到。ecma文件。 单击“ **[!UICONTROL 全部保存]**”。

   有关示例脚本，请参 [阅用于动态选择用户或用户组的示例ECMAScript](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group)。

1. 添加脚本的显示名称。 此名称显示在工作流步骤中。 指定名称：

   1. 展开脚本节点，右键单击 **[!UICONTROL jcr:content节点]** ，然后单击 **[!UICONTROL Mixins]**。
   1. 在“编辑 `mix:title` 混音”对话框中添加属性，然后单击“确 **定”**。
   1. 将以下属性添加到脚本的jcr:content节点：

      | 名称 | 类型 | 值 |
      |--- |--- |--- |
      | jcr:title | 字符串 | 指定脚本的名称。 例如，选择最近的字段代理。 此名称显示在分配任务和签名文档步骤中。 |

   1. 单击“ **全部保存**”。 该脚本可在AEM Workflow的组件中进行选择。

      ![脚本](assets/script.png)

### 范例ECMAScript可动态选择用户或用户组 {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

以下示例ECMAScript动态选择“分配”任务步骤的被分派人。 在此脚本中，根据有效负荷的路径选择用户。 在使用此脚本之前，请确保脚本中提到的所有用户都存在于AEM中。 如果AEM中不存在脚本中提到的用户，则相关进程可能会失败。

```
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

以下示例ECMAScript动态选择Adobe Sign步骤的被分派人。 在使用以下脚本之前，请确保脚本中提到的用户信息（电子邮件地址和电话号码）正确无误。 如果脚本中提到的用户信息不正确，则相关过程可能会失败。

>[!NOTE]
>
>在使用ECMAScript for Adobe Sign时，该脚本必须位于crx-repository中/apps/fd/workflow/scripts/adobesign/，并应具有一个名为getAdobeSignRecipients的函数，以返回用户的列表。

```
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## 使用Java界面动态选择用户或用户组 {#use-java-interface-to-dynamically-choose-a-user-or-group}

您可以使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面为Adobe Sign和分配任务步骤动态选择用户或用户组。 您可以创建一个使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面的OSGi捆绑包，并将其部署到AEM Forms服务器。 它使该选项可在AEM Workflow的分配任务和Adobe Sign组件中进行选择。

您需要 [AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) jar和 [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) granite jar文件才能编译下面列出的代码示例。 将这些jar文件作为外部依赖关系添加到OSGi捆绑项目。 您可以使用任何Java IDE创建OSGi捆绑包。 以下过程提供了使用Eclipse创建OSGi包的步骤：

1. 打开Eclipse IDE。 导航到“文 **[!UICONTROL 件]**”>“ **[!UICONTROL 新建项目”]**。
1. 在“选择向导”屏幕上，选择“创 **[!UICONTROL 建项目]**”，然后单击“下 **[!UICONTROL 一步”]**。
1. 在New Maven项目中，保留默认值，然后单击“下 **[!UICONTROL 一步”]**。 选择原型，然后单击“下 **[!UICONTROL 一步”]**。 例如，maven-archetype-quickstart。 指定 **[!UICONTROL 组ID]**、对象ID、 **[!UICONTROL 版本]**，以 ************&#x200B;及项目的包、完成和单击完成。 将创建项目。
1. 打开pom.xml文件进行编辑，并将文件的所有内容替换为以下内容：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. 添加使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java界面的源代码，以动态选择“分配”任务步骤的用户或用户组。 有关示例代码，请参 [阅使用Java界面动态选择用户或用户组的示例](#-sample-scripts-for)。
1. 打开命令提示符，然后导航到包含OSGi捆绑项目的目录。 使用以下命令创建OSGi包：

   `mvn clean install`

1. 将捆绑包上传到AEM Forms服务器。 您可以使用AEM包管理器将包导入AEM Forms服务器。

导入捆绑包后，Adobe Sign和分配任务步骤中可以使用选择Java界面以动态选择用户或用户组的选项。

### 用于动态选择用户或用户组的示例Java代码 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

以下示例代码动态选择Adobe Sign步骤的被分派人。 在OSGi捆绑中使用代码。 在使用下面列出的代码之前，请确保代码中提到的用户信息（电子邮件地址和电话号码）正确无误。 如果代码中提到的用户信息不正确，则相关过程可能会失败。

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

