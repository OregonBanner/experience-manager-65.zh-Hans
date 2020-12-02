---
title: 配置重定向页
seo-title: 配置重定向页
description: 填写自适应表单后，可以将用户重定向到表单作者在创建表单时可以配置的网页。
seo-description: 填写自适应表单后，可以将用户重定向到表单作者在创建表单时可以配置的网页。
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# 配置重定向页面{#configuring-redirect-page}

表单作者可以为每个表单配置一个页面，在提交表单后，表单用户将被重定向到该页面。

1. 在编辑模式下，选择一个组件，单击![字段级别](assets/field-level.png) > **自适应表单容器**，然后单击![cmppr](assets/cmppr.png)。

1. 在提要栏中，单击&#x200B;**提交**。

1. 在“提交”部分的“感谢页面”下提供重定向页面的URL。
1. （可选）在“提交操作”下，对于“提交到REST端点”操作，您可以配置要传递到重定向页面的参数。

![重定向页面配置](assets/thank-you-setting-1.png)

重定向页面配置

表单作者可以使用传递到感谢页面的以下参数。 对于所有可用的提交操作，将传递`status`和`owner`参数。 除了这两个参数之外，还会为以下提交操作传递一些附加参数：

* **存储内容操作** （已弃用）: `contentPath`—存储提交数据的存储库中节点的路径——将被传递。

* **存储PDF操作** （已弃用）: `contentPath`-传递提交的数据和指向存储库中存储PDF文件的节点的路径。

* **提交到Forms工作流**:将传递从表单工作流返回的输出参数。

* **提交到REST端点**:将传递为字段内映射添加的参数到参数映射。`status` 和参 `owner` 数未在此提交操作中传递。有关详细信息，请参阅[配置提交到REST端点提交操作](../../forms/using/configuring-submit-actions.md)。

