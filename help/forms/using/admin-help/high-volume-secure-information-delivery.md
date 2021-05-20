---
title: 大容量安全信息传送
seo-title: 大容量安全信息传送
description: 文档安全支持将许可证与用户关联，而不是与批量生产环境中的文档关联。
seo-description: 文档安全支持将许可证与用户关联，而不是与批量生产环境中的文档关联。
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: 文档安全
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 大容量安全信息传递{#high-volume-secure-information-delivery}

在大规模生产环境中，例如为电信公司生成安全的每月发票的环境中，创建特定于每个文档的许可证可以成为资源密集型过程。 在这种情况下，文档安全支持将许可证与用户关联，而不是与文档关联。 为用户生成的许可证用于为该用户保护的所有文档。

这种方法的一个优势是文档安全数据库的大小不会随着文档而线性增长，而是随着用户数量而增长。 此外，由于您只需为用户创建一次许可证，因此通过这些策略对文档的后续保护会变得更快。 所有此类文档都支持离线访问、文档过期和撤销等功能。

文档安全还支持抽象策略。 抽象策略是包含所有策略属性（如文档安全设置和使用权限）但不包含主体列表的策略模板。 管理员可以使用应具有文档访问权限的不同承担者从抽象策略创建任意数量的策略。 对抽象策略所做的更改不会影响从抽象策略生成的实际策略。

对于电信公司每月生成发票的情况，您可以创建抽象策略，创建用户，然后为每个用户生成唯一的许可证。 这些许可证稍后将应用于每个用户的文档。

只有通过文档安全Java SDK才支持创建抽象策略。 但是，您可以从文档安全网页的抽象策略管理您创建的策略。 使用此方法创建的策略的行为与从文档安全网页创建的策略相同。

有关更多信息，请参阅[使用AEM表单进行编程](https://www.adobe.com/go/learn_aemforms_programming_63) 。
