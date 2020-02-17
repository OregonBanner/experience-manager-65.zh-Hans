---
title: 配置帐户锁定设置
seo-title: 配置帐户锁定设置
description: 在指定数量的连续身份验证失败后，使用“启用帐户锁定”选项锁定用户帐户。
seo-description: 在指定数量的连续身份验证失败后，使用“启用帐户锁定”选项锁定用户帐户。
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置帐户锁定设置 {#configure-account-locking-settings}

添加域时，指定是否启用帐户锁定。 选择“启用帐户锁定”选项后，用户帐户在指定数量的连续身份验证失败后会被锁定。 在指定的时间长度后，用户可以尝试再次验证。 此功能可阻止用户尝试各种凭据组合来访问系统。

使用“域管理”页上的设置指定身份验证失败的最大次数和帐户锁定的时间长度。 这些设置适用于启用帐户锁定的所有域。

1. 在管理控制台中，单击 **[!UICONTROL 设置>用户管理>域管理]**。
1. 在“Maximum Centroupt Authentication Failures（最大连续身份验证失败）”框中，输入用户在锁定其帐户之前尝试登录失败的连续次数。 默认值为 20。
1. 在“Unlock The Account After(Minutes)(帐户解除锁定后（分钟）)”框中，输入用户帐户被锁定的分钟数。 在指定的分钟数后，用户可以尝试再次登录。 默认值为 30。
1. 单击&#x200B;**[!UICONTROL 保存]**。

