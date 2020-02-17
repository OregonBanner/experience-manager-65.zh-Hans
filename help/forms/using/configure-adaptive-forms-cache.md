---
title: 配置自适应表单缓存
seo-title: 配置自适应表单缓存
description: '自适应表单高速缓存专门设计用于自适应表单和文档。 它高速缓存自适应表单和自适应文档，以减少在客户端上呈现自适应表单或文档所需的时间。 '
seo-description: '自适应表单高速缓存专门设计用于自适应表单和文档。 它高速缓存自适应表单和自适应文档，以减少在客户端上呈现自适应表单或文档所需的时间。 '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 配置自适应表单缓存{#configure-adaptive-forms-cache}

缓存是缩短数据访问时间、减少延迟和提高输入／输出(I/O)速度的机制。 自适应表单缓存仅存储自适应表单的HTML内容和JSON结构，而不保存任何预填数据。 它有助于缩短在客户端上渲染自适应表单或文档所需的时间。 它专为自适应表单而设计，并且还支持自适应文档。

>[!NOTE]
>
>使用自适应表单缓存时，请使用AEM Dispatcher缓存自适应表单或文档的客户端库（CSS和JavaScript）。

>[!NOTE]
>
>在开发自定义组件时，在用于开发的服务器上，保持自适应表单缓存被禁用。

## 配置缓存 {#configure-the-cache}

请执行以下步骤以配置自适应表单缓存：

1. 转到位于https://[server]:[port]/system/console/configMgr的AEM web控制台配置管理器。
1. 单击“ **自适应表单和交互式通信Web通道配置** ”以编辑其配置值。
1. 在编辑配置值对话框中，在自适应表单数字字段中指定AEM Forms服务器实例可以缓存的最大表 **单或文档数** 。 默认值为 100。

   >[!NOTE]
   >
   >要禁用缓存，请将“自适应表单数”字段中的值设置为 **0**。 当您禁用或更改缓存配置时，将重置缓存并从缓存中删除所有表单和文档。

   ![自适应表单HTML缓存的配置对话框](assets/cache-configuration-edit.png)

1. Click **Save** to save the configuration.

