---
title: 配置重定向页面
seo-title: Configuring redirect page
description: 填写自适应表单后，用户可能会被重定向到表单作者在创建表单时可以配置的网页。
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# 配置重定向页面{#configuring-redirect-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | 本文 |

表单作者可以为每个表单配置一个页面，表单用户在提交表单后会重定向到该页面。

1. 在编辑模式下，选择一个组件，然后单击 ![字段级](assets/field-level.png) > **自适应表单容器**，然后单击 ![cmppr](assets/cmppr.png).

1. 在侧栏中，单击 **提交**.

1. 在提交部分的感谢页面下提供重定向页面的URL。
1. （可选）在“提交操作”下，对于“提交到REST端点”操作，您可以配置要传递到重定向页面的参数。

![重定向页面配置](assets/thank-you-setting-1.png)

重定向页面配置

表单作者可以使用以下传递到“感谢”页面的参数。 对于所有可用的提交操作， `status` 和 `owner` 参数被传递。 除了这两个参数外，还会为以下提交操作传递一些其他参数：

* **存储内容操作** （已弃用） ： `contentPath` — 存储提交数据的存储库中节点的路径 — 被传递。

* **存储PDF操作** （已弃用） ： `contentPath` — 已提交的数据以及将PDF文件存储在存储库中的节点的路径 — 将被传递。

* **提交到Forms工作流程**：传递从表单工作流返回的输出参数。

* **提交到REST端点**：传递为字段内到参数映射添加的参数。 `status` 和 `owner` 此提交操作中未传递参数。 有关更多信息，请参阅 [配置提交到REST端点提交操作](../../forms/using/configuring-submit-actions.md).
