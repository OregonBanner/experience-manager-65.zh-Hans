---
title: 使用经理视图管理组织层次结构中的任务
seo-title: Managing tasks in an organizational hierarchy using Manager View
description: 经理和组织负责人如何在AEM Forms工作区的“待办事项”选项卡中访问和处理其直接和间接报告的任务。
seo-description: How managers and organization heads can access and work on the tasks of their direct and indirect reports in the To-do tab in AEM Forms workspace.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 使用经理视图管理组织层次结构中的任务{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

在AEM Forms工作区中，经理现在可以访问其层次结构中分配给任何人的任务（直接或间接报告），并对其执行各种操作。 这些任务可在AEM Forms工作区的“待办事项”选项卡中找到。 直接报告任务支持的操作包括：

**转发** 将任务从直接报告转发给任何用户。

**声明** 声明直接下属的任务。

**报销申请和打开** 声明直接下属的任务，并在经理的待办事项列表中自动将其打开。

**拒绝** 拒绝某个其他用户转发到直接报告的任务。 此选项适用于其他用户转发到直接下属的任务。

AEM Forms限制用户仅访问用户具有访问控制(ACL)的任务。 此类检查可确保用户只能获取用户拥有访问权限的任务。 通过使用第三方Web服务和实施来定义层次结构，组织可以自定义经理和直接报告的定义以满足其需求。

1. 创建DSC。 有关更多信息，请参阅中的“为AEM Forms开发组件”主题 [使用AEM Forms编程](https://www.adobe.com/go/learn_aemforms_programming_63) 指南。
1. 在DSC中，为层次结构管理定义新的SPI，以便在AEM Forms用户中定义直接报告和层次结构。 以下是一个示例Java™代码段。

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

1. 创建一个component.xml文件。 请确保spec-id必须与以下代码片段中所示的相同。 以下是一个代码片段示例，您可以调整其用途。

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
1. 您可能需要刷新浏览器或再次注销/登录用户。

以下屏幕说明了如何访问直接下属的任务和可用的操作。

![cu_manager_view](assets/cu_manager_view.png)

访问直接下属的任务并处理任务
