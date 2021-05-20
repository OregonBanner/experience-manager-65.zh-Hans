---
title: 配置帐户锁定设置
seo-title: 配置帐户锁定设置
description: 使用“启用帐户锁定”选项可在指定数量的连续身份验证失败后锁定用户帐户。
seo-description: 使用“启用帐户锁定”选项可在指定数量的连续身份验证失败后锁定用户帐户。
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%

---

# 配置帐户锁定设置{#configure-account-locking-settings}

添加域时，请指定是否启用帐户锁定。 选中启用帐户锁定选项后，在指定数量的连续身份验证失败后，用户帐户将被锁定。 在指定的时长后，用户可以尝试再次进行身份验证。 此功能可阻止用户尝试各种凭据组合来访问系统。

使用“域管理”页上的设置，指定身份验证失败的最大次数和帐户被锁定的时长。 这些设置适用于已启用帐户锁定的所有域。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>用户管理>域管理]**。
1. 在“最大连续身份验证失败次数”框中，输入用户在帐户被锁定之前尝试登录失败的连续次数。 默认值为 20。
1. 在“在以后解锁帐户（分钟）”框中，输入用户帐户被锁定的分钟数。 在指定的分钟数后，用户可以尝试再次登录。 默认值为 30。
1. 单击&#x200B;**[!UICONTROL 保存]**。
