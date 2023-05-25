---
title: 更新内容片段以进行优化的 GraphQL 筛选
description: 了解如何在 Adobe Experience Manager 中更新内容片段以进行优化的 GraphQL 筛选，从而进行 Headless 内容投放。
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 42%

---


# 更新内容片段以进行优化的 GraphQL 筛选 {#updating-content-fragments-for-optimized-graphql-filtering}

要优化GraphQL筛选器的性能，请运行过程以更新内容片段。

>[!NOTE]
>
>更新内容片段后，您可以遵循以下推荐： [优化GraphQL查询](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## 前提条件 {#prerequisites}

确保您至少具有6.5.17.0版本的AEM。

## 更新内容片段 {#updating-content-fragments}

要运行该过程，请执行以下步骤：

1. [配置OSGi设置](/help/sites-deploying/configuring-osgi.md) 对于 **内容片段迁移作业配置**：

   ![OSGi内容片段迁移作业配置](assets/cfm-graphql-update-01.png "OSGi内容片段迁移作业配置")

1. 在对话框中，按以下方式设置这两个参数：

   * **ContentFragmentMigration：Enabled** ： `1`
   * **ContentFragmentMigration：强制** ： `1`

1. **保存** 规范 — 更新过程启动。

1. 等待该过程完成。 当属性为 `cfGlobalVersion` 显示于 `/content/dam` 并且将设置为 `1`.

1. 返回到OSGi配置以取消激活该过程。

   在的对话框中 **内容片段迁移作业配置** 按以下方式设置这两个参数：

   * **ContentFragmentMigration：Enabled** ： `0`
   * **ContentFragmentMigration：强制** ： `0`

## 限制 {#limitations}

请注意以下限制：

* 只能在完全更新所有内容片段（由 JCR 节点 `/content/dam` 的 `cfGlobalVersion` 属性指示）后，才能优化 GraphQL 筛选器的性能

* 如果在运行更新过程后从包导入了内容片段（使用 `crx/de`），则直到再次执行更新过程后，才会在 GraphQL 查询结果中再次考虑这些内容片段。