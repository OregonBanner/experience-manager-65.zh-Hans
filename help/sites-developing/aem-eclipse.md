---
title: 适用于 Eclipse 的 AEM 开发人员工具
seo-title: AEM Developer Tools for Eclipse
description: 适用于 Eclipse 的 AEM 开发人员工具
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 3%

---

# 适用于 Eclipse 的 AEM 开发人员工具{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概述 {#overview}

AEM Developer Tools for Eclipse是一个基于 [适用于Apache Sling的Eclipse插件](https://sling.apache.org/documentation/development/ide-tooling.html) 已根据Apache许可证2发布。

它提供了以下几项功能，可简化AEM开发：

* 通过Eclipse Server Connector与AEM实例无缝集成。
* 内容和OSGI包的同步。
* 具有代码热交换功能的调试支持。
* 通过特定项目创建向导简单引导AEM项目。
* 轻松编辑JCR属性。

## 要求 {#requirements}

在使用AEM开发人员工具之前，您需要：

* 下载并安装 [面向Java EE开发人员的Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). AEM开发人员工具当前支持Eclipse Kepler或更高版本

* 可与AEM版本5.6.1或更高版本一起使用
* 配置Eclipse安装，以通过编辑 `eclipse.ini` 配置文件，如 [Eclipse常见问题解答](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>在macOS上，您需要右键单击 **Eclipse.app** 然后选择 **显示包内容** 以找到 `eclipse.ini`**.**

## 如何安装AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

完成 [要求](#requirements) 在上面，您可以按如下方式安装插件：

1. 浏览 [**AEM** 开发人员工具网站](https://eclipse.adobe.com/aem/dev-tools/).

1. 复制 **安装链接**.

   请注意，或者，您也可以下载存档文件，而不是使用安装链接。 这允许离线安装，但您将无法通过这种方式接收自动更新通知。

1. 在Eclipse中，打开 **帮助** 菜单。
1. 单击 **安装新软件**.
1. 单击 **添加……**.
1. 在 **名称** 键入AEM Developer Tools。
1. 在 **位置** 复制安装URL。
1. 单击 **确定**.
1. 同时检查 **AEM** 和 **Sling** 插件。
1. 单击&#x200B;**下一步**。
1. 单击&#x200B;**下一步**。
1. 接受这些临时协议并单击 **完成**.
1. 单击 **是** 以便重新启动Eclipse。

## 如何导入现有项目 {#how-to-import-existing-projects}

>[!NOTE]
>
>请参阅 [从AEM下载Eclipse包时，如何在包中使用](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM透视 {#the-aem-perspective}

Eclipse的AEM开发工具附带一个透视，可让您完全控制AEM项目和实例。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模块项目 {#sample-multi-module-project}

AEM Developer Tools for Eclipse附带一个示例的多模块项目，该项目可帮助您快速掌握Eclipse中项目设置的速度，并且是一些AEM功能的最佳实践指南。 [进一步了解项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

按照以下步骤创建示例项目：

1. 在 **文件** > **新建** > **项目** 菜单，浏览到 **AEM** 选择 **AEM多模块项目示例**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一些时间，因为m2eclipse需要扫描原型目录。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 选择 **com.adobe.granite.archetypes :sample-project-archetype :（最高数）** ，然后单击 **下一个**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填写 **名称**, **组ID** 和 **项目ID** ，以查看示例项目。 您还可以选择设置一些高级属性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 然后，您应该配置一个AEM服务器，Eclipse将连接到该服务器。

   要使用调试器功能，您需要在调试模式下启动AEM — 例如，通过将以下内容添加到命令行中即可实现：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 单击 **完成**. 随即会创建项目结构。

   >[!NOTE]
   >
   >在全新安装中(更具体地说：从未下载maven依赖项时)，您可能会收到创建的项目并出现错误。 在本例中，请按照 [解决无效项目定义](#resolving-invalid-project-definition).

## 疑难解答 {#troubleshooting}

### 解决无效项目定义 {#resolving-invalid-project-definition}

要解决无效的依赖项，项目定义将按如下步骤进行：

1. 选择所有已创建的项目。
1. 右键单击。 在菜单中 **马文** 选择 **更新项目**.
1. 检查 **强制更新快照/版本**.
1. 单击&#x200B;**确定**。Eclipse会尝试下载所需的依赖项。

### 在JSP文件中启用标记库自动完成 {#enabling-tag-library-autocompletion-in-jsp-files}

标记库自动完成功能开箱即用，因为项目中已添加了适当的依赖关系。 使用AEM Uber Jar时存在一个已知问题，该问题不包括所需的tld和TagExtraInfo文件。

要解决此问题，请确保org.apache.sling.scripting.jsp.taglib对象位于AEM Uber Jar之前的类路径中。 对于Maven项目，请将以下依赖项放在pom.xml中Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

确保为部署AEM添加正确的版本。

## 更多信息 {#more-information}

适用于Eclipse网站的官方Apache Sling IDE工具为您提供了以下有用信息：

* 的 [**适用于Eclipse的Apache Sling IDE工具** 用户指南](https://sling.apache.org/documentation/development/ide-tooling.html)，本文档将指导您完成AEM开发工具支持的总体概念、服务器集成和部署功能。
* 的 [疑难解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* 的 [已知问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

以下官员 [Eclipse](https://eclipse.org/) 文档可帮助设置您的环境：

* [Eclipse快速入门](https://eclipse.org/users/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/luna/index.jsp)
* [Maven集成(m2eclipse)](https://www.eclipse.org/m2e/)
