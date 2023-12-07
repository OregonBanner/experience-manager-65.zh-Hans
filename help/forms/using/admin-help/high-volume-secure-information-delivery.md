---
title: 大批量安全信息交付
description: Document Security支持将许可证关联到用户，而不是关联到批量生产环境中的文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 大批量安全信息交付 {#high-volume-secure-information-delivery}

在批量生产环境中（例如为电信公司生成每月安全发票的环境中），创建特定于每个文档的许可证可能会成为一个资源密集型过程。 在这种情况下，Document Security支持将许可证与用户关联，而不是与文档关联。 为用户生成的许可证用于为该用户保护的所有文档。

此方法的一个优点是，document security数据库的大小不会与文档线性增长，而是与用户数量呈线性增长。 此外，由于您只需为用户创建一次许可证，因此通过这些策略对文档的后续保护会变得更快。 所有此类文档都支持脱机访问、文档过期和吊销等功能。

Document Security还支持抽象策略。 抽象策略是包含所有策略属性（如Document Security设置和使用权限）但不包含承担者列表的策略模板。 管理员可以根据抽象策略创建任意数量的策略，这些策略由不同承担者来访问。 对抽象策略所做的更改不会影响从抽象策略生成的实际策略。

如果电信公司需要每月生成发票，则您需要创建抽象策略，创建用户，然后为每个用户生成唯一的许可证。 许可证稍后应用于每个用户的文档。

仅通过Document Security Java SDK支持创建抽象策略。 但是，您可以管理从document security网页的抽象策略创建的策略。 使用此方法创建的策略的行为与从Document Security网页创建的策略相同。

请参阅 [使用AEM表单编程](https://www.adobe.com/go/learn_aemforms_programming_63) 以了解更多信息。
