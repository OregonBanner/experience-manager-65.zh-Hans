---
title: 大容量安全信息交付
seo-title: 大容量安全信息交付
description: 文档安全性支持将许可证关联到用户，而不是关联到大量生产环境中的文档。
seo-description: 文档安全性支持将许可证关联到用户，而不是关联到大量生产环境中的文档。
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 大容量安全信息交付 {#high-volume-secure-information-delivery}

在大量生产环境（例如为电信公司生成有担保的月度发票的环境）中，创建特定于每个文档的许可证可以成为资源密集型流程。 在这种情况下，文档安全性支持将许可证关联到用户而不是文档。 为用户生成的许可证用于为该用户保护的所有文档。

这种方法的一个优点是，文档安全数据库的大小不会随文档而线性增长，而是随用户数量而增长。 此外，由于您只需要为用户创建许可证一次，因此通过这些策略对文档的后续保护将变得更快。 所有此类文档都支持脱机访问、文档到期和撤销等功能。

文档安全性还支持抽象策略。 摘要策略是包含所有策略属性（如文档安全性设置和使用权限）的策略模板，但不包含主体列表。 管理员可以使用应有权访问文档的不同承担者从抽象策略创建任意数量的策略。 对抽象策略所做的更改不会影响从抽象策略生成的实际策略。

对于电信公司的月度发票生成，您可以创建抽象策略，创建用户，然后为每个用户生成唯一的许可证。 许可证稍后将应用于每个用户的文档。

只有通过文档安全Java SDK才支持创建抽象策略。 但是，您可以从Document Security网页的抽象策略管理您创建的策略。 使用此方法创建的策略的行为与通过文档安全网页创建的策略相同。

有关更 [多信息，请参阅使用AEM表单进行编程](https://www.adobe.com/go/learn_aemforms_programming_63) 。
