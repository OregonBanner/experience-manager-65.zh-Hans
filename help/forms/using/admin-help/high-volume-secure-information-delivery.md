---
title: 大容量安全信息投放
seo-title: 大容量安全信息投放
description: 文档安全性支持将许可证关联到用户，而不是关联到大规模生产环境中的文档。
seo-description: 文档安全性支持将许可证关联到用户，而不是关联到大规模生产环境中的文档。
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# 大容量安全信息投放{#high-volume-secure-information-delivery}

在大量生产环境(例如为电信公司生成有担保的月度发票的)中，创建特定于每个文档的许可证可以成为资源密集型流程。 在这种情况下，文档安全支持将许可证关联到用户，而不是文档。 为用户生成的许可证将用于为该用户提供保护的所有文档。

这种方法的一个优点是文档安全数据库的大小不会随文档而线性增长，而是随用户数的增长而线性增长。 此外，由于您只需要为用户创建一次许可证，因此通过这些策略对文档的后续保护变得更快。 所有此类文档均支持离线访问、文档过期和撤销等功能。

文档安全性还支持抽象策略。 抽象策略是包含所有策略属性(如文档安全设置和使用权限)的策略模板，但不包含主体列表。 管理员可以使用应有权访问文档的不同承担者从抽象策略创建任意数量的策略。 对抽象策略所做的更改不会影响从抽象策略生成的实际策略。

如果电信公司每月为其生成发票，您可以创建抽象策略，创建用户，然后为每个用户生成唯一许可证。 许可证稍后将应用于每个用户的文档。

只有通过文档安全Java SDK支持创建抽象策略。 但是，您可以从文档安全网页管理从抽象策略创建的策略。 使用此方法创建的策略的行为与通过文档安全网页创建的策略相同。

有关详细信息，请参阅[使用AEM表单进行编程](https://www.adobe.com/go/learn_aemforms_programming_63)。
