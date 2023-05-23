---
title: 適用於AEM 6.5 Sites的Headless開發
description: 瞭解AEM 6.5強大的Headless功能(如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗，並跨管道提供這些體驗。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# 適用於AEM 6.5 Sites的Headless開發 {#headless-development}

瞭解AEM 6.5強大的Headless功能(如內容模型、內容片段和GraphQL API)如何搭配運作，讓您集中管理您的體驗，並跨管道提供這些體驗。

## 概述 {#overview}

Headless實施對於向您的受眾提供體驗變得越來越重要，無論他們身在何處，也不論他們使用哪個管道。

Headless 实施放弃了传统的全栈和混合解决方案中的页面和组件管理，专注于创建渠道中性的、可重用的内容片段，以及它们的跨渠道投放。这是一种现代化的动态开发模式，用于实施 Web 体验。

![AEM 实施模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Headful 和 Headless 的比较 {#headful-headless}

本檔案著重於AEM的完整Headless實作模型。 不过，在 AEM 中，Headful 与 Headless 不一定是一个二选一的选择。Headless功能可用來管理內容並將其傳送至各種端點，同時讓內容作者可以編輯單頁應用程式。 这些都可在 AEM 中实现。

>[!TIP]
>
>有关更多信息，请参阅文档 [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md)。

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是適用於Headless實作模式的彈性工具，提供三種強大的服務：

1. 内容模型
   * 内容模型是内容的结构化表示方式。
   * 這些由AEM內容片段模式編輯器中資訊架構師定義。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 內容片段是內容模型的例項化。
   * 這些是由內容作者使用AEM內容片段編輯器建立。
   * 這些檔案儲存在AEM Assets中，並在資產管理員UI中進行管理。
1. 用于投放的内容 API
   * AEM GraphQL API 支持内容片段投放。
   * AEM Assets REST API 支持内容片段 CRUD 操作。
   * 也可以使用直接內容傳送 [內容片段核心元件的JSON匯出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)

## 使用 AEM Headless 的第一步 {#first-steps}

有許多資源可供您開始使用AEM Headless功能。 這些範本適用於不同的使用案例，但都能提供AEM Headless功能的完整概覽。

| 资源 | 描述 | 类型 | 受众 | 估计用时 |
|---|---|---|---|---|
| [Headless 开发人员历程](/help/journey-headless/developer/overview.md) | **對於AEM和Headless的新使用者** 技術，從這裡開始全面介紹AEM及其headless功能，從headless的理論到您的第一個headless專案。 | 指南 | **刚开始接触 AEM 和 Headless** 的开发人员 | 1 小时 |
| [Headless 快速入门指南](/help/sites-developing/headless/getting-started/introduction.md) | **面向有经验的 AEM 用户**，在需要关键 AEM Headless 功能的简短摘要时，可以查看此快速入门概览。 | 快速入門 | **具有 AEM 经验**&#x200B;的开发人员、管理员 | 20 分钟 |
| [AEM Headless實作教學課程快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans) | **如果您偏好實作方法且熟悉AEM**，本教學課程將直接說明如何建立簡單的Headless專案。 | 教程 | 开发人员 | 2 小时 |
