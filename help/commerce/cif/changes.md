---
title: 对Commerce Integration Framework (CIF)加载项的显着更改
description: 与旧版CIF相比，Commerce Integration Framework (CIF)加载项发生了显着更改。
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# 对Commerce Integration Framework (CIF)加载项的显着更改{#notable-changes}

本文档重点介绍Commerce Integration Framework (CIF)加载项与旧版CIF之间的重要差异，旧版主要称为CIF Classic (Quickstart)和CIF开源。

## 安装和更新

AEM CIF附加组件包将通过AEM包管理器进行安装和更新。

**早期CIF版本**

* CIF Classic：无需安装，CIF是快速入门的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* CIF开源：通过GitHub安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过OSGi控制台进行配置。

**早期CIF版本**

* CIF Classic：通过AEM中的OSGi配置
* CIF开源：通过CIF配置浏览器

## 部署CIF Venia项目

项目可用日期 [GitHub AEM指南 — CIF Venia项目](https://github.com/adobe/aem-cif-guides-venia) 和部署通过AEM包管理器完成。

**早期CIF版本**

* CIF Classic：通过AEM包安装

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，可按需请求产品目录数据。 这些API支持在任何给定日期访问实时数据或暂存数据。 无需复制。

**早期CIF版本**

* CIF Classic：通过完整或增量产品导入，在AEM Author上导入实时和暂存产品数据并将其保留在JCR中。 将实时产品数据复制到AEM Publish。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板动态呈现产品目录体验。 无需复制。

**早期CIF版本**

* CIF Classic：AEM作者使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面将复制到AEM Publish。

>[!NOTE]
>
>有关如何将CIF与AEM托管服务或AEM内部部署结合使用的其他文档，请参阅 [Commerce集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
