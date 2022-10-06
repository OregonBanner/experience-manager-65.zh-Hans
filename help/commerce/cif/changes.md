---
title: 对商务集成框架(CIF)附加组件的显着更改
description: 与旧的CIF版本相比，商务集成框架(CIF)附加组件发生了显着更改。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 对商务集成框架(CIF)附加组件的显着更改{#notable-changes}

本文档重点介绍了商务集成框架(CIF)附加组件与旧CIF版本(主要称为CIF Classic（快速入门）和CIF开源版本)之间的重要区别。

## 安装和更新

AEM CIF附加组件包已安装并更新，其中包含AEM包管理器。

**早期CIF版本**

* CIF Classic:无需安装，CIF是快速入门的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* CIF开源：通过GitHub进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过OSGi控制台进行配置。

**早期CIF版本**

* CIF Classic:通过AEM中的OSGi配置
* CIF开源：通过CIF配置浏览器

## 部署CIF维尼亚项目

项目可用于 [GitHub AEM指南 — CIF Venia项目](https://github.com/adobe/aem-cif-guides-venia) 和通过AEM包管理器完成的部署。

**早期CIF版本**

* CIF Classic:通过AEM包安装

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，按需请求产品目录数据。 这些API支持在任何给定日期访问实时或暂存数据。 无需复制。

**早期CIF版本**

* CIF Classic:通过完整或增量产品导入，将在AEM创作的JCR中导入和保留实时和暂存产品数据。 实时产品数据会复制到AEM发布。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板即时渲染产品目录体验。 无需复制。

**早期CIF版本**

* CIF Classic:AEM作者使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面会被复制到AEM发布。

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM On-Premise结合使用的其他文档，请参阅 [商务集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
