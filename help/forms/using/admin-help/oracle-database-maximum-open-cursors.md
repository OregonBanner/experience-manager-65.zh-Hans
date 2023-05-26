---
title: oracle数据库最大打开游标阈值
seo-title: Oracle database maximum open cursors threshold
description: 了解如何在Oracle中为打开游标配置最大值。
seo-description: Learn about configuring a maximum value for open cursors in Oracle.
uuid: c1d20997-f853-4772-b1c6-8cea73221d0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d3565776-1b7d-498c-9840-b17f80170d9b
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# oracle数据库最大打开游标阈值 {#oracle-database-maximum-open-cursors-threshold}

要为Oracle中的打开游标配置最大值，可能必须将此值调整为适合您的应用程序的数字。 显然，在中等负载下，打开的平均游标数为2700。 建议开始设置上限为3000。 有关详细信息，请访问 [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
