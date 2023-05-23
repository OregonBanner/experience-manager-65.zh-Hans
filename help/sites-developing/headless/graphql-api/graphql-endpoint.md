---
title: 在 AEM 中管理 GraphQL 端点
description: 瞭解如何在Adobe Experience Manager中管理GraphQL端點，以進行Headless內容傳送。
exl-id: a59a5e50-0787-4c1c-a83d-bb3eac1479a8
source-git-commit: a8616b3b30ac04ea24c4a869cabd47518af1a35f
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 97%

---

# 在 AEM 中管理 GraphQL 端点 {#graphql-aem-endpoint}

端点是 AEM 用于访问 GraphQL 的路径。您（或您的应用程序）可以使用此路径来：

* 访问 GraphQL 架构，
* 发送 GraphQL 查询，
* 接收（对您 GraphQL 查询的）响应。

AEM 中有两种类型的端点：

* 全局
   * 可供所有站点使用。
   * 此端点可以使用所有站点配置的所有内容片段模型（在[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中定义）。
   * 如果有任何应该在站点配置中共享的内容片段模型，则这些内容应该在全局站点配置下创建。
* Sites 配置：
   * 对应于站点配置，如[配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)中的定义。
   * 特定于指定站点/项目。
   * Sites 配置特定的端点将来自特定站点配置与来自全局站点配置的内容片段模型结合使用。

>[!CAUTION]
>
>内容片段编辑器可以允许一个站点配置的内容片段引用另一个站点配置（通过策略）的内容片段。
>
>在这种情况下，所有内容将可使用站点配置特定的端点检索。
>
>内容作者应控制这种情境；例如，在考虑将共享内容片段模型放在全局站点配置下时，它会很有用。

AEM 全局端点的 GraphQL 的存储库路径为：

`/content/cq:graphql/global/endpoint`

对于此项，您的应用程序可以在请求 URL 中使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为 AEM 的 GraphQL 启用端点，您需要：

* [启用 GraphQL 端点](#enabling-graphql-endpoint)
* [发布 GraphQL 端点](#publishing-graphql-endpoint)

## 启用 GraphQL 端点 {#enabling-graphql-endpoint}

要启用 GraphQL 端点，您首先需要具有合适的配置。请参阅[内容片段 – 配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果[未启用内容片段模型](/help/assets/content-fragments/content-fragments-configuration-browser.md)，则&#x200B;**创建**&#x200B;选项将不可用。

要启用对应的端点，请执行以下操作：

1. 导航到&#x200B;**工具**、**资源**，然后选择 **GraphQL**。
1. 选择&#x200B;**创建**。
1. 此时将打开&#x200B;**创建新 GraphQL 端点**&#x200B;对话框。在其中可以指定：
   * **名称**：端点的名称，您可以输入任意文本。
   * **使用的 GraphQL 架构提供自**：使用下拉菜单选择所需的站点/项目。

   >[!NOTE]
   >
   >对话框中显示以下警告：
   >
   >* *如果不对 GraphQL 端点仔细管理，则可能会带来数据安全和性能问题。请确保在创建端点后设置适当的权限。*


1. 选择&#x200B;**创建**&#x200B;来确认。
1. **后续步骤**&#x200B;对话框将提供直接指向安全性控制台的链接，这样您可以确保新创建的端点具有合适的权限。

   >[!CAUTION]
   >
   >端点可供所有人访问。这会带来安全问题，特别是在发布实例上，因为 GraphQL 查询会对服务器施加大量负载。
   >
   >您可在端点上设置适合您的用例的 ACL。

## 发布 GraphQL 端点 {#publishing-graphql-endpoint}

选择新端点和&#x200B;**发布**&#x200B;以使其在所有环境中完全可用。

>[!CAUTION]
>
>端点可供所有人访问。
>
>在发布实例上，这会带来安全问题，因为 GraphQL 查询会对服务器施加大量负载。
>
>您必须在端点上设置适合您的用例的 ACL。
