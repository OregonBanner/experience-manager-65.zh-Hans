---
title: AEM Developer Tools for Eclipse
seo-title: AEM Developer Tools for Eclipse
description: 'null'
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概述 {#overview}

AEM Developer Tools for Eclipse是一个Eclipse插件，它基于Apache License 2下发布的 [Eclipse插件for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) 。

它提供了几个使AEM开发更轻松的功能：

* 通过Eclipse Server Connector与AEM实例无缝集成。
* 内容和OSGI包的同步。
* 具有代码热交换功能的调试支持。
* 通过特定项目创建向导简单引导AEM项目。
* 轻松编辑JCR属性。

## 要求 {#requirements}

在使用AEM开发人员工具之前，您需要：

* 下载并安 [装适用于Java EE开发人员的Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。 AEM开发人员工具当前支持Eclipse Kepler或更高版本

* 可与AEM 5.6.1版或更高版本一起使用
* 配置Eclipse安装，以确保通过编辑配置文件(如 `eclipse.ini` Eclipse常见问题中所述)至少拥有1GB [堆内存](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)。

>[!NOTE]
>
>在macOS上，您需要右键单击 **Eclipse.app** ，然后选择“显 **示包内容** ”以查找您的 `eclipse.ini`**。**

## 如何安装Eclipse的AEM Developer Tools {#how-to-install-the-aem-developer-tools-for-eclipse}

满足上述要求后 [](#requirements) ，您可以按如下方式安装插件：

1. 浏览 [**AEM **Developer Tools网站](https://eclipse.adobe.com/aem/dev-tools/)。

1. 复制安 **装链接**。

   请注意，您也可以下载存档，而不是使用安装链接。 这允许脱机安装，但这样会错过自动更新通知。

1. 在Eclipse中，打开“帮 **助** ”菜单。
1. 单击“ **安装新软件”**。
1. **单击**&#x200B;添加…….
1. 在名 **称中** ，键入AEM Developer Tools。
1. 在 **位置** ，复制安装URL。
1. Click **Ok**.
1. 检查 **AEM** 和 **Sling** 插件。
1. 单击&#x200B;**下一步**。
1. 单击&#x200B;**下一步**。
1. 接受这些链接协议，然后单击“ **完成**”。
1. 单击 **是** ，以重新启动Eclipse。

## 如何导入现有项目 {#how-to-import-existing-projects}

>[!NOTE]
>
>请参 [阅从AEM下载Eclipse中的捆绑包时如何使用](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)。

## AEM透视 {#the-aem-perspective}

适用于Eclipse的AEM开发工具随“透视图”一起提供，使您能够完全控制AEM项目和实例。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模块项目 {#sample-multi-module-project}

适用于Eclipse的AEM开发人员工具附带一个多模块项目示例，它可以帮助您快速掌握Eclipse中的项目设置，并作为多个AEM功能的最佳实践指南。 [进一步了解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

按照以下步骤创建示例项目：

1. 在“文 **件** >新建 **>项目** ”菜单中，浏览至“AEM示例”和“ ************ AEM模块多项目项目”部分的AEM和SELECT Section。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一段时间，因为m2eclipse需要扫描原型目录。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 选 **择com.adobe.granite.archetypes:示例——项目——原型：（最大数）** ，然后单击“下 **一步”**。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 为示例项 **目填写名**、 **组ID** 和 **对象ID** 。 您还可以选择设置一些高级属性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 然后，您应配置Eclipse将连接到的AEM服务器。

   要使用调试器功能，您需要在调试模式下启动AEM —— 这可以通过向命令行添加以下内容来实现：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 单击“ **完成**”。 将创建项目结构。

   >[!NOTE]
   >
   >在全新安装中(更具体地说：当从未下载过依赖项时)，您可能会创建出包含错误的项目。 在这种情况下，请按照解决无效项目定义中 [所述的过程操作](#resolving-invalid-project-definition)。

## 疑难解答 {#troubleshooting}

### 解析无效的项目定义 {#resolving-invalid-project-definition}

要解析无效的依赖关系和项目定义，请按如下步骤继续：

1. 选择所有创建的项目。
1. 右键单击。 在菜单中， **选择** “更 **新项目”**。
1. 选中 **强制更新快照／版本**。
1. 单击&#x200B;**确定**。Eclipse会尝试下载所需的依赖关系。

### 在JSP文件中启用标记库自动完成 {#enabling-tag-library-autocompletion-in-jsp-files}

标记库自动完成功能开箱即用，因为项目中添加了适当的依赖关系。 使用AEM Uber Jar时有一个已知问题，该问题不包括所需的tld和TagExtraInfo文件。

要解决该问题，请确保org.apache.sling.scripting.jsp.taglib对象位于AEM Uber Jar之前的类路径中。 对于Maven项目，将以下依赖关系放在pom.xml中的Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

确保为AEM部署添加正确版本。

## More information {#more-information}

适用于Eclipse网站的Apache Sling IDE正式工具集为您提供了有用的信息：

* 本文 [**档是Eclipse **User Guide的Apache Sling IDE工具集](https://sling.apache.org/documentation/development/ide-tooling.html)，它将指导您了解AEM Development Tools支持的整体概念、服务器集成和部署功能。
* 疑难 [解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* “已 [知问题”列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官方 [Eclipse](https://eclipse.org/) 文档可以帮助您设置环境：

* [Eclipse快速入门](https://eclipse.org/users/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/luna/index.jsp)
* [Maven集成(m2eclipse)](https://www.eclipse.org/m2e/)

