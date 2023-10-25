---
title: 适用于 Eclipse 的 AEM 开发人员工具
description: 了解Adobe Experience Manager的Eclipse开发人员工具。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---

# 适用于 Eclipse 的 AEM 开发人员工具{#aem-developer-tools-for-eclipse}

![AEM Developer Tools for Eclipse的圆形图像主题。](do-not-localize/chlimage_1-9.png)

## 概述 {#overview}

“AEM开发人员工具”是一个基于 [适用于Apache Sling的Eclipse插件](https://sling.apache.org/documentation/development/ide-tooling.html) 根据Apache许可证2发布。

它提供了几项使AEM开发更轻松的功能：

* 通过Eclipse Server Connector与AEM实例无缝集成。
* 内容和OSGI捆绑包的同步。
* 使用代码热插拔功能调试支持。
* 通过特定项目创建向导简单BootstrapAEM项目。
* 轻松编辑JCR属性。

## 要求 {#requirements}

在使用AEM Developer Tools之前，请执行以下操作：

* 下载并安装 [面向Java™ EE开发人员的Eclipse IDE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM Developer Tools当前支持Eclipse Kepler或更高版本

* 可与AEM版本5.6.1或更高版本一起使用
* 配置eclipse安装，通过编辑您的 `eclipse.ini` 配置文件，如中所述 [Eclipse常见问题解答](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>在macOS上，右键单击 **Eclipse.app**，然后选择 **显示包内容** 查找您的 `eclipse.ini`.

## 如何安装适用于Eclipse的AEM开发人员工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

一旦您满足了 [要求](#requirements) 如上所示，您可以安装插件：

1. 浏览 **AEM Developer Tools** 网站： `https://eclipse.adobe.com/aem/dev-tools/`.

1. 复制 **安装链接**.

   或者，您也可以下载归档文件，而不是使用安装链接。 这样做允许脱机安装，但您会遗漏自动更新通知。

1. 在Eclipse中，打开 **帮助** 菜单。
1. 单击 **安装新软件**.
1. 单击 **添加……**.
1. 在 **名称** 键入AEM Developer Tools。
1. 在 **位置** 复制安装URL
1. 单击 **确定**.
1. 选中两者 **AEM** 和 **Sling** 插件。
1. 单击&#x200B;**下一步**。
1. 单击&#x200B;**下一步**。
1. 接受线协议，然后单击 **完成**.
1. 单击 **是** 重新启动Eclipse。

## 如何导入现有项目 {#how-to-import-existing-projects}

>[!NOTE]
>
>请参阅 [如何在Eclipse中使用从AEM下载的捆绑包](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM视角 {#the-aem-perspective}

AEM Development Tools for Eclipse附带了一个透视，您可以通过该透视图完全控制AEM项目和实例。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模块项目 {#sample-multi-module-project}

“AEM开发人员工具”包含一个示例的多模块项目，可帮助您快速上手Eclipse中的项目设置。 它还可用作几项AEM功能的最佳实践指南。 [了解有关项目原型的更多信息](https://github.com/adobe/aem-project-archetype).

要创建示例项目，请完成以下步骤：

1. 在 **文件** > **新建** > **项目** 菜单，浏览到 **AEM** 部分并选择 **AEM示例多模块项目**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一些时间，因为m2eclipse必须扫描原型目录。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 选择 **com.adobe.granite.archetypes ： sample-project-archetype ： （最高数字）** 在菜单中，然后单击 **下一个**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填写 **名称**， **组ID**，和 **工件ID** 作为示例项目。 您还可以选择设置一些高级属性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 现在，配置Eclipse可以连接的AEM服务器。

   要使用Debugger功能，请确保在调试模式下启动AEM，这可以通过在命令行中添加以下内容来实现：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 单击 **完成**. 将创建项目结构。

   >[!NOTE]
   >
   >在全新安装中（更具体地说：从未下载maven依赖项时），您可能会创建项目，但出现错误。 在此情况下，请按照中所述的过程 [解析无效的项目定义](#resolving-invalid-project-definition).

## 疑难解答 {#troubleshooting}

### 解析无效的项目定义 {#resolving-invalid-project-definition}

要解决无效依赖项和项目定义，请按照以下步骤操作：

1. 选择所有已创建的项目。
1. 右键单击。 在菜单中 **Maven**，选择 **更新项目**.
1. Check **强制更新快照/版本**.
1. 单击&#x200B;**确定**。Eclipse会尝试下载所需的依赖项。

### 在JSP文件中启用标记库自动完成 {#enabling-tag-library-autocompletion-in-jsp-files}

标记库自动完成可开箱即用，前提是将适当的依赖关系添加到项目中。 使用AEM Uber Jar时，存在一个已知问题，该问题不包括所需的tld和TagExtraInfo文件。

要解决此问题，请确保org.apache.sling.scripting.jsp.taglib工件位于AEM Uber Jar之前的类路径中。 对于Maven项目，请将以下依赖项放在pom.xml中的Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

请确保为您的部署AEM添加正确的版本。

## 更多信息 {#more-information}

适用于Eclipse网站的官方Apache Sling IDE工具为您提供有用信息：

* 此 [**适用于Eclipse的Apache Sling IDE工具** 用户指南](https://sling.apache.org/documentation/development/ide-tooling.html)，本文档将指导您了解AEM开发工具支持的整体概念、服务器集成和部署功能。
* 此 [“疑难解答”部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* 此 [已知问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

以下官方 [Eclipse](https://www.eclipse.org/) 文档有助于设置环境：

* [Eclipse快速入门](https://eclipseide.org/getting-started/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/latest/index.jsp)
* [Maven集成(m2eclipse)](https://www.eclipse.org/m2e/)
