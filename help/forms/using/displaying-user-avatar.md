---
title: 显示用户头像
seo-title: 显示用户头像
description: 如何自定义AEM Forms工作区以显示登录用户的图像。
seo-description: 如何自定义AEM Forms工作区以显示登录用户的图像。
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 显示用户头像{#displaying-the-user-avatar}

登录用户的头像显示在AEM Forms工作区的右上角。 此外，组织层次结构中直接报表的变量会显示在“管理器视图”中。 您可以配置AEM Forms工作区，从数据库中选取用户图像，如LDAP服务器。

>[!NOTE]
>
>用户图像的支持宽高比为1:1。

1. 使用下一步中所述的详细信息创建DSC。 有关更多信息，请参阅《使用AEM Forms进行编程》指南中的“为AEM表单开发组件”主题。[](https://www.adobe.com/go/learn_aemforms_programming_63)
1. 在DSC中，定义一个新的SPI，该SPI公开getCurrentUserImageUrl和getUserImageUrl方法，以获取AEM Forms用户的图像URL。 以下是Java™代码片段示例：

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. 创建component.xml文件。 请确保规范id为，如以下代码片段中所示。

   以下代码片段是一个示例。 根据您的特定要求对其进行自定义。

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. 通过Workbench部署DSC。 重新启动`ProcessManagementClientSessionService`服务。
1. 您可能需要刷新浏览器或再次注销/登录用户。
