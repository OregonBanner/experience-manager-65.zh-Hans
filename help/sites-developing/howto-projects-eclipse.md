---
title: 如何使用Eclipse开发AEM项目
seo-title: 如何使用Eclipse开发AEM项目
description: 本指南介绍如何使用Eclipse开发基于AEM的项目
seo-description: 本指南介绍如何使用Eclipse开发基于AEM的项目
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 如何使用Eclipse开发AEM项目{#how-to-develop-aem-projects-using-eclipse}

本指南介绍如何使用Eclipse开发基于AEM的项目。

>[!NOTE]
>
>Adobe现在提供[AEM Development Tools for Eclipse](/help/sites-developing/aem-eclipse.md)，它可以帮助您使用Eclipse开发AEM解决方案。

## 概述 {#overview}

要开始使用AEM on Eclipse开发，需要以下步骤。

每项操作在本“操作方法”的其余部分中都有更详细的说明。

* 安装Eclipse 4.3(Kepler)
* 根据Maven设置AEM项目
* 在Maven POM中准备对Eclipse的JSP支持
* 将Maven项目导入Eclipse

>[!NOTE]
>
>本指南基于Eclipse 4.3(Kepler)和AEM 5.6.1。

## 安装Eclipse {#install-eclipse}

从[Eclipse下载页面](https://www.eclipse.org/downloads/)下载“Eclipse IDE for Java EE开发人员”。

按照[安装说明](https://wiki.eclipse.org/Eclipse/Installation)安装Eclipse。

## 根据Maven {#set-up-your-aem-project-based-on-maven}设置AEM项目

接下来，使用Maven设置项目，如[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目中所述。

## 准备对Eclipse {#prepare-jsp-support-for-eclipse}的JSP支持

Eclipse还可以提供与JSP结合的支持，例如

* 标签库的自动完成
* 对由&lt;cq:defineObjects />和&lt;sling:defineObjects />定义的对象的Eclipse感知

为了使其正常工作：

1. 按照[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目中的[如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中的说明操作。
1. 在内容模块的POM中的&lt;build />部分添加以下内容。

   Eclipse的Maven支持插件m2e不支持maven-jspc插件，此配置告知m2e忽略插件以及清理临时编译结果的相关任务。

   这不是问题：如[如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中所述，此设置中的maven-jspc-plugin仅用于验证JSP作为构建过程的一部分进行编译。 Eclipse已报告JSP中的任何问题，并且不依赖此Maven插件才能这样做。

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

1. 现在，您已准备好使用Eclipse开发AEM项目，包括JSP自动完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果您在`/libs`中包含`/libs/foundation/global.jsp`或其他JSP，您需要将其复制到您的项目，这样Eclipse就能解析包含。 同时，您需要确保Maven未将其捆绑到您的内容包中。 如何实现这一点，请参见[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目。

