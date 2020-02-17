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

---


# 如何使用Eclipse开发AEM项目{#how-to-develop-aem-projects-using-eclipse}

本指南介绍如何使用Eclipse开发基于AEM的项目。

>[!NOTE]
>
>Adobe现在提供 [AEM Development Tools for Eclipse](/help/sites-developing/aem-eclipse.md) ，它可以帮助您使用Eclipse开发AEM解决方案。

## 概述 {#overview}

要开始在Eclipse上进行AEM开发，需要执行以下步骤。

每项操作在本“操作方法”的其余部分中都有更详细的说明。

* 安装Eclipse 4.3(Kepler)
* 基于Maven设置AEM项目
* 在Maven POM中为Eclipse准备JSP支持
* 将Maven项目导入Eclipse

>[!NOTE]
>
>本指南基于Eclipse 4.3(Kepler)和AEM 5.6.1。

## 安装Eclipse {#install-eclipse}

从 [Eclipse下载页下载“Eclipse IDE for Java EE Developers”](https://www.eclipse.org/downloads/)。

按照安装说明安 [装Eclipse](https://wiki.eclipse.org/Eclipse/Installation)。

## 基于Maven设置AEM项目 {#set-up-your-aem-project-based-on-maven}

接下来，使用Maven设置项目，如使用Apache Maven [构建AEM项目中所述](/help/sites-developing/ht-projects-maven.md)。

## 准备Eclipse的JSP支持 {#prepare-jsp-support-for-eclipse}

Eclipse还可以在使用JSP(例如，

* 标签库的自动完成
* 对由&lt;cq:defineObjects />和&lt;sling:defineObjects />定义的对象的Eclipse感知

为了使其正常工作：

1. 按照使用Apache Maven [构建AEM项目](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)[中有关如何使用JSP的说明操作](/help/sites-developing/ht-projects-maven.md)。
1. 在内容模块的POM中的&lt;build />部分添加以下内容。

   Eclipse的Maven支持插件m2e不支持maven-jspc-plugin，此配置告知m2e忽略插件以及清理临时编译结果的相关任务。

   这不是问题：如使用JSP [的方法中所述](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)，此设置中的maven-jspc插件仅用于验证JSP作为构建过程的一部分进行编译。 Eclipse已报告JSP中的任何问题，并且不依赖此Maven插件来报告这些问题。

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

1. 现在，您完全可以使用Eclipse开发AEM项目，包括JSP自动完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果您在 `/libs/foundation/global.jsp` 中包含或其他JSP `/libs`，则需要将其复制到项目中，这样Eclipse就可以解析包含内容。 同时，您需要确保Maven未将其捆绑到您的内容包中。 如何实现此目标，请参阅 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)。

