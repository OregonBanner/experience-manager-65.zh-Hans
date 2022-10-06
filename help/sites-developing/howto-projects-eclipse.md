---
title: 如何使用Eclipse开发AEM项目
seo-title: How to Develop AEM Projects Using Eclipse
description: 本指南介绍如何使用Eclipse来开发基于AEM的项目
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 如何使用Eclipse开发AEM项目{#how-to-develop-aem-projects-using-eclipse}

本指南介绍如何使用Eclipse来开发基于AEM的项目。

>[!NOTE]
>
>Adobe现在提供 [AEM Development Tools for Eclipse](/help/sites-developing/aem-eclipse.md) 它可帮助您使用Eclipse开发AEM解决方案。

## 概述 {#overview}

要开始在Eclipse上开发AEM，需要执行以下步骤。

在本操作说明的其余部分中，将更详细地介绍每个操作说明。

* 安装Eclipse 4.3(Kepler)
* 基于Maven设置AEM项目
* 在Maven POM中为Eclipse准备JSP支持
* 将Maven项目导入Eclipse

>[!NOTE]
>
>本指南基于Eclipse 4.3(Kepler)和AEM 5.6.1。

## 安装Eclipse {#install-eclipse}

从 [Eclipse下载页面](https://www.eclipse.org/downloads/).

在 [安装说明](https://wiki.eclipse.org/Eclipse/Installation).

## 基于Maven设置AEM项目 {#set-up-your-aem-project-based-on-maven}

接下来，使用Maven设置项目，如 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

## 准备对Eclipse的JSP支持 {#prepare-jsp-support-for-eclipse}

Eclipse还可以在使用JSP(例如，

* 自动完成标记库
* 对由定义的对象的日蚀感知 &lt;cq:defineobjects /> 和 &lt;sling:defineobjects />

要使其起作用，请执行以下操作：

1. 按照 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).
1. 在 &lt;build /> 部分。

   Eclipse的Maven支持插件m2e不支持mven-jspc-plugin，此配置告诉m2e忽略插件以及清理临时编译结果的相关任务。

   这不是问题：如 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)，此设置中的maven-jspc-plugin仅用于验证JSP是否在生成过程中编译。 Eclipse已报告JSP中的任何问题，并且不依赖此Maven插件来执行此操作。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### 将Maven项目导入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，选择“文件”>“导入……”
1. 在“导入”对话框中，选择“Maven”>“现有Maven项目”，然后单击“下一步”。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 输入项目顶级文件夹的路径，然后单击“全选”和“完成”。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 现在，您完全可以使用Eclipse来开发AEM项目，包括JSP自动完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果包含 `/libs/foundation/global.jsp` 或 `/libs`，则您需要将该代码复制到项目，以便Eclipse能够解析包含。 同时，您需要确保Maven未将其捆绑到您的内容包中。 如何实现此操作，请参见 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).
