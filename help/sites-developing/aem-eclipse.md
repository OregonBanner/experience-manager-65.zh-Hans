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
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概述 {#overview}

AEM Developer Tools for Eclipse是一个基于Apache License 2下发布的[Eclipse plugin for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)的Eclipse插件。

它优惠了几个使AEM开发更容易的功能：

* 通过Eclipse Server Connector与AEM实例无缝集成。
* 内容和OSGI包的同步。
* 通过代码热插拔功能支持调试。
* 通过特定项目创建向导简单引导AEM项目。
* 轻松编辑JCR属性。

## 要求{#requirements}

在使用AEM开发人员工具之前，您需要：

* 下载并安装[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。 AEM开发人员工具当前支持EclipseKepler或更新版本

* 可与AEM 5.6.1或更高版本一起使用
* 按照[Eclipse常见问题解答](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)中的说明，通过编辑`eclipse.ini`配置文件，配置Eclipse安装以确保至少拥有1 GB的堆内存。

>[!NOTE]
>
>在macOS上，您需要右键单击&#x200B;**Eclipse.app**，然后选择&#x200B;**显示包内容**&#x200B;以找到您的&#x200B;`eclipse.ini`**。**

## 如何安装AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

满足上述[要求](#requirements)后，可以按如下方式安装插件：

1. 浏览&#x200B;[**AEM**&#x200B;开发人员工具网站](https://eclipse.adobe.com/aem/dev-tools/)。

1. 复制&#x200B;**安装链接**。

   请注意，您也可以下载存档文件，而不是使用安装链接。 这允许脱机安装，但您会以这种方式错过自动更新通知。

1. 在Eclipse中，打开&#x200B;**帮助**&#x200B;菜单。
1. 单击&#x200B;**安装新软件**。
1. 单击&#x200B;**添加……**。
1. 在&#x200B;**名称**&#x200B;中，键入AEM Developer Tools。
1. 在&#x200B;**位置**&#x200B;中，复制安装URL。
1. 单击&#x200B;**确定**。
1. 检查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;插件。
1. 单击&#x200B;**下一步**。
1. 单击&#x200B;**下一步**。
1. 接受这些链接协议，然后单击&#x200B;**完成**。
1. 单击&#x200B;**是**&#x200B;以重新启动Eclipse。

## 如何导入现有项目{#how-to-import-existing-projects}

>[!NOTE]
>
>请参阅[从AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)下载Eclipse中的捆绑包时如何使用它。

## AEM透视{#the-aem-perspective}

AEM Development Tools for Eclipse附带一个透视图，它优惠您对AEM项目和实例的完全控制。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模块项目{#sample-multi-module-project}

AEM Developer Tools for Eclipse附带一个范例、多模块项目，它可以帮助您快速掌握Eclipse中的项目设置，并作为几个AEM功能的最佳实践指南。 [进一步了解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

按照以下步骤创建示例项目：

1. 在&#x200B;**文件** > **新建** > **项目**&#x200B;菜单中，浏览至&#x200B;**AEM**&#x200B;部分并选择&#x200B;**AEM示例多模块项目**。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一段时间，因为m2eclipse需要扫描原型目录。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 选择&#x200B;**com.adobe.granite.archetypes:示例——项目——原型：(highest number)**，然后单击&#x200B;**Next**。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 为示例项目填写&#x200B;**名称**、**组id**&#x200B;和&#x200B;**项目id**。 您还可以选择设置一些高级属性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 然后，您应配置Eclipse将连接到的AEM服务器。

   要使用调试器功能，您需要在调试模式下启动AEM —— 这可以通过向命令行添加以下内容来实现：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 单击&#x200B;**完成**。 将创建项目结构。

   >[!NOTE]
   >
   >在新安装中(更具体地说：当从未下载依赖项时)，您可能会创建出错误的项目。 在这种情况下，请按照[解决无效项目定义](#resolving-invalid-project-definition)中描述的过程操作。

## 疑难解答 {#troubleshooting}

### 解析无效的项目定义{#resolving-invalid-project-definition}

要解析无效的依赖项，项目定义将按如下步骤进行：

1. 选择所有创建的项目。
1. 右键单击。 在菜单&#x200B;**Maven**&#x200B;中，选择&#x200B;**更新项目**。
1. 检查&#x200B;**强制更新快照／发行版**。
1. 单击&#x200B;**确定**。Eclipse会尝试下载所需的依赖项。

### 在JSP文件{#enabling-tag-library-autocompletion-in-jsp-files}中启用标记库自动完成

标签库自动完成功能开箱即用，前提是向项目添加了适当的依赖关系。 使用AEM Uber Jar时有一个已知问题，它不包括所需的tld和TagExtraInfo文件。

要解决此问题，请确保org.apache.sling.scripting.jsp.taglib对象位于AEM Uber Jar之前的类路径中。 对于Maven项目，在pom.xml中将以下依赖项放在Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

确保为AEM的部署添加正确的版本。

## 更多信息{#more-information}

适用于Eclipse网站的Apache Sling IDE官方工具为您提供有用的信息：

* 本文档将指导您了解AEM开发工具支持的总体概念、服务器集成和部署功能，其中&#x200B;[**Apache Sling IDE工具包，用于Eclipse**&#x200B;用户指南](https://sling.apache.org/documentation/development/ide-tooling.html)。
* [疑难解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官方[Eclipse](https://eclipse.org/)文档可以帮助您设置环境:

* [Eclipse快速入门](https://eclipse.org/users/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/luna/index.jsp)
* [Maven Integration(m2eclipse)](https://www.eclipse.org/m2e/)

