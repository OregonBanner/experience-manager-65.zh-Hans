---
title: 自定义 HTTP 标头
description: 了解如何在Adobe Experience Manager Commerce中配置自定义HTTP标头。
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 5%

---

# 自定义 HTTP 标头 {#custom-http-headers}

## 概述 {#overview}

为了更好地控制其后端，作者可以配置将发送到商业引擎的自定义HTTP标头，以及CIF已发送的标头。 常见用例包括多商店设置，您可以在其中使用HTTP标头控制商务后端的响应。

>[!NOTE]
>
>开发人员始终可以使用GraphQL客户端配置来配置自定义HTTP标头。
>

## 配置 {#configuration}

要配置自定义HTTP标头，必须首先定义它们。 必须首先通过将自定义HTTP标头添加到来定义它们 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 使用OSGi配置的服务配置。

您可以在项目的“Cloud Service配置”页中配置HTTP标头的值：

1. 转到“工具” — >“Cloud Services” — >“CIF配置”中的“Cloud Service配置”页面
1. 打开现有配置或创建新配置
1. 转到“高级”选项卡，然后找到“自定义HTTP标头”多字段。 您可以选择之前定义的题头并为它们分配值。

使用上述Cloud Service配置的组件将在每个GraphQL请求中发送这些HTTP标头。

## 限制 {#restrictions}

虽然该服务允许定义任何标头名称，包括标准标头名称，但它们将无法用于配置。 换句话说，您无法使用此功能覆盖标准HTTP标头。 可以找到受限制的标头名称列表 [此处](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers). 除了这些标头之外，还有两个标头无法使用：

* &quot;Store&quot; - CIF用于识别Adobe Commerce商店
* &quot;Preview-Version&quot; — 由CIF用于检索暂存产品
