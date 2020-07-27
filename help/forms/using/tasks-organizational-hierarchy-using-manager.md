---
title: 使用Manager任务管理组织层次结构中的视图
seo-title: 使用Manager任务管理组织层次结构中的视图
description: 管理者和组织负责人如何在AEM Forms工作区的“待办事项”选项卡中访问和处理其直接和间接报告的任务。
seo-description: 管理者和组织负责人如何在AEM Forms工作区的“待办事项”选项卡中访问和处理其直接和间接报告的任务。
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# 使用Manager任务管理组织层次结构中的视图{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

在AEM Forms工作区中，管理者现在可以访问分配给其层次结构中任何人的任务（直接或间接报告），并对其执行各种操作。 任务位于AEM Forms工作区的待办事项选项卡中。 对一任务直接报表支持的操作包括：

**转发** 将任务从直接报告转发给任何用户。

**索赔** 任务直接报告。

**Claim &amp; Open** Claim是直接报表的任务，并在经理的待办列表中自动打开它。

**拒绝** 拒绝由其他用户转发到直接报告的任务。 此选项适用于其他用户转发到直接报告的任务。

AEM Forms将用户仅限于用户具有访问控制(ACL)的任务。 这样的检查可确保用户只能获取用户具有访问权限的任务。 使用第三方Web服务和实施来定义层次结构，组织可以自定义管理者的定义和直接报告，以满足其需求。

1. 创建DSC。 有关详细信息，请参阅《使用AEM Forms进行编程》指南中的“为AEM Forms [开发组件](https://www.adobe.com/go/learn_aemforms_programming_63) ”主题。
1. 在DSC中，为层次管理定义新的SPI，以在AEM Forms用户中定义直接报表和层次。 以下是示例Java™代码片段。

   ```java
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. 创建component.xml文件。 请确保规范ID必须与下面的代码片断中所示相同。 以下是可重用的示例代码片段。

   ```xml
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. 通过Workbench部署DSC。 重新启动 `ProcessManagementTeamTasksService` 服务。
1. 您可能必须刷新浏览器或再次注销／登录用户。

以下屏幕说明了如何访问一任务直接报告和可用的操作。

![cu_manager_视图](assets/cu_manager_view.png)

访问任务的直接报告并采取相应行动任务
