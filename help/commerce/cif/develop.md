---
title: Develop AEM Commerce
description: 了解如何使用AEM项目原型生成支持商务的AEM项目。 了解如何构建项目并将其部署到本地开发环境。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 2%

---


# 开发AEM Commerce {#develop}

根据AEM的Commerce Integration Framework(CIF)开发AEM Commerce项目时遵循与其他AEM项目相同的规则和最佳做法。 请首先查看以下内容：

- [AEM 6.5 Developing 用户指南](/help/sites-developing/home.md)
- [AEM Core Concepts](/help/sites-developing/the-basics.md)
- [AEM开发 — 准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)

## Local Development for AEM Commerce {#local}

建议当地发展环境与CIF项目合作。

>[!NOTE]
>
>以下说明可帮助您使用CIF(针对AEM 6.5提供焦点)设置AEM Commerce的本地AEM开发环境。 如果您将AEM用作Cloud Service，请参阅[AEM Commerce as Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/home.html)文档。

AEM Commerce Add-On for AEM 6.5 aka。 CIF Add-On也可用于本地开发，并作为AEM包提供。 它可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载为功能包。

### 所需软件

应在本地安装以下内容：

- 本地AEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更高版本
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
- [节点LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 访问CIF加载项

CIF加载项可从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载，搜索“AEM商务加载项”。

>[!TIP]
>
>确保始终使用最新的CIF Add-On版本。

### 本地设置

使用AEM和CIF附加组件进行本地CIF项目开发，步骤如下：

1. 获取AEM 6.5版本并安装AEM 6.5 Service Pack。 AEM 6.5 Service Pack 7是必需的，但我们建议您安装最后一个可用的Service Pack。

1. 解压缩AEM .jar以创建`crx-quickstart`文件夹，运行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 创建`crx-quickstart/install`文件夹

1. 将从软件分发门户下载的所有CIF加载项复制到`crx-quickstart/install`文件夹中。

>[!TIP]
>
>或者，CIF加载项包也可以通过包管理器安装。

1. 开始AEM快速入门

通过OSGI控制台验证设置： `http://localhost:4502/system/console/osgi-installer`。 列表应包括CIF附加相关捆绑包、内容包和OSGI配置。 确保启动所有捆绑包。

## 项目设置{#project}

有两种方法可使用CIF开始您的AEM商务项目。

### 使用AEM Project Archetype

[AEM项目原型](https://github.com/adobe/aem-project-archetype)是引导预配置项目以开始使用CIF的主要工具。 CIF核心组件和所有所需配置都可以包含在生成的项目中，并且还有一个额外选项。

>[!TIP]
>
>使用[AEM Project Archetype 25或更高版本](https://github.com/adobe/aem-project-archetype/releases)生成项目。

有关如何生成AEM项目，请参阅AEM Project Archetype [使用说明](https://github.com/adobe/aem-project-archetype#usage)。 要将CIF包含到项目中，请使用`includeCommerce`选项。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心组件可以在任何项目中使用，方法是包括提供的`all`包或使用CIF内容包和相关OSGI包的个人。 要手动将CIF核心组件添加到项目，请使用以下依赖关系：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEM Venia Reference Store

开始CIF项目的第二个选项是克隆并使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是示范性参考店面应用程序，用于演示AEM的CIF核心组件的用法。 它旨在作为一组最佳实践示例和开发您自己的功能的潜在起点。

要开始使用Venia Reference Store，只需克隆[Git存储库](https://github.com/adobe/aem-cif-guides-venia)，然后开始根据您的需要自定义项目。

>[!NOTE]
>
>Venia Reference Store项目包含两个用于AEM作为Cloud Service和AEM 6.5的构建用户档案。请查看[项目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以了解它们的使用方式。 对于AEM 6.5，请使用`classic`用户档案。

### 将AEM连接到商务系统

要将项目连接到商务系统AEM，必须使用您的商务系统的GraphQL端点进行配置。

两者中，由[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)或[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)生成的项目都已包含必须调整的[默认配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)。

将`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值替换为项目所使用的商务系统的GraphQL端点。

AEM Commerce Add-On和CIF核心组件通过AEM服务器直接通过浏览器连接到商务GraphQL端点。 默认情况下，客户端CIF核心组件和CIF附加创作工具连接到`/api/graphql`。 如果需要，可以通过CIFCloud Service配置来调整此配置（见下文）。

CIF加载项在`/api/graphql`处提供GraphQL代理servlet。 如果您不打算使用本地AEM Dispatcher，则建议还配置GraphQL代理servlet。

导航到http://localhost:4502/system/console/configMgr并为`Adobe CIF GraphQL Proxy Configuration`服务创建OSGI配置。 使用与上述GraphQL客户端相同的商务系统GraphQL端点。

## 其他资源

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
