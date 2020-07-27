---
title: 将Maven用于社区
seo-title: 将Maven用于社区
description: AEM CommunitiesAPI jar和AEM Uber API jar
seo-description: AEM CommunitiesAPI jar和AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f05d7c19e3284c0627e29b9590db4749be100229
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 将Maven用于社区 {#using-maven-for-communities}

## 概述 {#overview}

AEM Communities文档的此部分还包括：

* [使用Apache Maven构建AEM项目](../../help/sites-developing/ht-projects-maven.md)。

现在有两种“优步”工件可取代个别工件：

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## 社区API Jar对象 {#communities-api-jar-artifact}

以下是AEM CommunitiesAPI jar的GAV示例：

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

确保指定的版本与为AEM Communities安装的Communities包版本相对应。 要验证已安装的版本号，请执行以下操作：

1. 以管理权限登录。
1. 浏览至 [包管理器](../../help/sites-administering/package-manager.md)。 例如， [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. 找到包： `cq-socialcommunities-pkg-1.x.xxx`
1. 从包名称中提取版本：
   * AEM 6.3的第一个版本是版本1.11.170。
   * 功能包版本为1.12.xxx。

>[!NOTE]
>
>建议您与最新的Communities版本保持同步。
>
>访问最 [新版本](deploy-communities.md#latest-releases) ，确定最新版本。


## Maven依赖关系示例 {#maven-dependency-example}

必须在Uber API jar之前指定Communities API jar。

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
