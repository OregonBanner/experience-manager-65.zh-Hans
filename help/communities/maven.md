---
title: 将Maven用于社区
seo-title: 将Maven用于社区
description: AEM Communities API jar和AEM Uber API jar
seo-description: AEM Communities API jar和AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# 将Maven用于社区 {#using-maven-for-communities}

## 概述 {#overview}

AEM Communities文档的此部分除了以下功能之外：

* [使用Apache Maven构建AEM项目](../../help/sites-developing/ht-projects-maven.md)。

现在有两件“优步”文物可替代个别文物：

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API Jar对象 {#communities-api-jar-artifact}

以下是AEM Communities API jar的GAV示例：

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
1. 浏览至包 [管理器](../../help/sites-administering/package-manager.md)。 例如， [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. 找到 *cq-socialcommunities-pkg-1.x.xxx包*
1. 从包名称中提取版本：
   * AEM 6.3的第一个版本是版本1.11.170。
   * 功能包将为版本1.12.xxx。

>[!NOTE]
>
>建议使用最新的Communities版本保持最新。
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
