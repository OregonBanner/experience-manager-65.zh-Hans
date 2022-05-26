---
title: 内容片段 — 配置浏览器
description: 了解如何在配置浏览器中启用某些内容片段功能，以便利用AEM功能强大的无头交付功能。
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 8dc8eff86ff25534a578dd227033aa185853d930
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 21%

---

# 内容片段 — 配置浏览器{#content-fragments-configuration-browser}

了解如何在配置浏览器中启用某些内容片段功能，以便利用AEM功能强大的无头交付功能。

## 为您的实例启用内容片段功能 {#enable-content-fragment-functionality-instance}

在使用内容片段之前，您需要使用 **配置浏览器** 启用：

* **内容片段模型**  — 必填
* **GraphQL永久查询**  — 可选

>[!CAUTION]
>
>如果未启用 **内容片段模型**:
>
>* the **创建** 选项将不可用于创建新模型。
>* 你将无法 [选择站点配置以创建相关的端点](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


要启用内容片段功能，您需要：

* 通过配置浏览器启用内容片段功能的使用
* 将配置应用到Assets文件夹

### 在配置浏览器中启用内容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用某些内容片段功能](#creating-a-content-fragment-model) you **必须** 首先，通过 **配置浏览器**:

>[!NOTE]
>
>有关更多详细信息，另请参阅 [配置浏览器：](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>支持与内容片段一起使用的子配置（嵌套在配置中的配置），但不能用于GraphQL查询。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用 **创建** 要打开对话框，您需要：

   1. 指定 **标题**.
   1. 要启用其用法，请选择
      * **内容片段模型**
      * **GraphQL 持久查询**

      ![定义配置](assets/cfm-conf-01.png)


1. 选择 **创建** 以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用到您的Assets文件夹 {#apply-the-configuration-to-your-assets-folder}

配置 **全球** ，则会应用于任何资产文件夹。

要将其他配置（即不包括全局配置）与类似的 Assets 文件夹一起使用，您必须定义连接。这是通过在相应文件夹的“ **文件夹属性** ”的“云服务 **”选项卡中选****** 择相应的配置来完成的。

![应用配置](assets/cfm-conf-02.png)
