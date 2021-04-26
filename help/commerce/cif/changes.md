---
title: Commerce Integration Framework(CIF)加载项的显着更改
description: 与旧版CIF相比，Commerce Integration Framework(CIF)加载项发生了显着变化。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 对Commerce Integration Framework(CIF)add-on{#notable-changes}的显着更改

本文档强调了商务集成框架(CIF)附加组件与旧CIF版本(主要称为CIF Classic（快速入门）和CIF开放源码)之间的重要区别。

## 安装和更新

AEM CIF加载项包将通过AEM包管理器安装和更新。

**先前的CIF版本**

* CIF经典：无需安装，CIF是快速启动的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* CIF开放源：通过GitHub进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

通过OSGi控制台配置终结点。

**先前的CIF版本**

* CIF经典：通过AEM中的OSGi配置
* CIF开放源：通过CIF配置浏览器

## CIF维尼亚项目的部署

[GitHub AEM指南中提供的项目 — CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)，并通过包AEM manager完成部署

**先前的CIF版本**

* CIF经典：通过AEM包安装

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，按需获取产品目录数据。 这些API支持在任何给定日期访问实时或分阶段数据。 无需复制。

**先前的CIF版本**

* CIF经典：通过完全或增量产品导入，实时和分阶段产品数据会在AEM作者的JCR中导入并保留。 将实时产品数据复制到AEM发布。

## 利用AEM渲染实现产品目录体验

AEM使用已分配给产品和类别的AEM目录模板，即时呈现产品目录体验。 无需复制。

**先前的CIF版本**

* CIF经典：AEM作者使用目录蓝图工具为每个类别/产品创建一个AEM页面。 这些页面将被复制到AEM发布。

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM On-premise一起使用的其他文档，请参阅[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
