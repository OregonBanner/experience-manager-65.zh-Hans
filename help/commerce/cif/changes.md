---
title: 对Commerce integration framework(CIF)加载项的重要更改
description: 与旧版CIF相比，Commerce integration framework(CIF)加载项发生了显着更改。
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# 对Commerce integration framework(CIF)加载项的显着更改{#notable-changes}

本文档重点介绍Commerce integration framework(CIF)加载项与旧CIF版本(主要称为CIF Classic (Quickstart)和CIF Open-source)之间的重要差异。

## 安装和更新

AEM CIF附加组件包通过AEM包管理器进行安装和更新。

**早期CIF版本**

* CIF Classic：无需安装，CIF是快速入门的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* CIF开放源代码：通过GitHub进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过OSGi控制台进行配置。

**早期CIF版本**

* CIF Classic：通过AEM中的OSGi配置
* CIF开放源代码：通过CIF配置浏览器

## 部署CIF Venia项目

项目可用日期 [GitHub AEM Guides - CIF Venia项目](https://github.com/adobe/aem-cif-guides-venia) 和部署可通过AEM包管理器完成。

**早期CIF版本**

* CIF Classic：通过AEM包安装

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，可按需请求产品目录数据。 这些API支持在任何给定日期访问实时数据或暂存数据。 无需复制。

**早期CIF版本**

* CIF Classic：通过完全或增量产品导入，在AEM Author上导入实时和暂存产品数据并将这些数据保留在JCR中。 将实时产品数据复制到AEM Publish。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板动态呈现产品目录体验。 无需复制。

**早期CIF版本**

* CIF Classic：AEM Author使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面将复制到AEM Publish。

>[!NOTE]
>
>有关如何将CIF与AEM托管服务或AEM内部部署一起使用的其他文档，请参阅 [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
