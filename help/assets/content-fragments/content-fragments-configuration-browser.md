---
title: 内容片段 – 配置浏览器
description: 了解如何在配置浏览器中启用某些内容片段功能，以使用Adobe Experience Manager强大的Headless投放功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 2810e34f642f4643fa4dc24b31a57a68e9194e39
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 45%

---

# 内容片段 – 配置浏览器{#content-fragments-configuration-browser}

了解如何在配置浏览器中启用某些内容片段功能，以使用Adobe Experience Manager (AEM)强大的Headless投放功能。

## 为您的实例启用内容片段功能 {#enable-content-fragment-functionality-instance}

在使用内容片段之前，请使用 **配置浏览器** 要启用以下功能，请执行以下操作：

* **内容片段模型** – 强制
* **GraphQL 持久查询** – 可选

>[!CAUTION]
>
>如果未启用&#x200B;**内容片段模型**：
>
>* 此 **创建** 选项将不可用于创建模型。
>* 您不能 [选择Sites配置以创建相关端点](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

要启用内容片段功能，您需要进行以下操作：

* 通过配置浏览器启用内容片段功能
* 将配置应用到 Assets 文件夹

### 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用特定内容片段功能](#creating-a-content-fragment-model)，您 **必须** 首先通过 **配置浏览器**：

>[!NOTE]
>
>有关更多信息，请参阅 [配置浏览器：](/help/sites-administering/configurations.md#using-configuration-browser).

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**“创建”**&#x200B;来打开对话框，您需要：

   1. 指定&#x200B;**标题**。
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cfm-conf-01.png)

1. 选择&#x200B;**“创建”**&#x200B;以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到 Assets 文件夹 {#apply-the-configuration-to-your-assets-folder}

当配置 **全局** 启用内容片段功能，然后应用于任何资产文件夹。

要将其他配置（即不包括全局配置）与类似的Assets文件夹一起使用，您必须定义连接。 这是通过在适当文件夹的&#x200B;**文件夹属性**&#x200B;的 **Cloud Services** 选项卡中选择适当的&#x200B;**配置**&#x200B;来完成的。

![应用配置](assets/cfm-conf-02.png)
