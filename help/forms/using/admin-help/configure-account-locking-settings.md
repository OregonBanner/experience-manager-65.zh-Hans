---
title: 設定帳戶鎖定設定
seo-title: Configure account-locking settings
description: 使用[啟用帳戶鎖定]選項，在指定的連續驗證失敗次數之後鎖定使用者帳戶。
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# 設定帳戶鎖定設定 {#configure-account-locking-settings}

新增網域時，請指定是否啟用帳戶鎖定。 選取[啟用帳戶鎖定]選項時，使用者帳戶會在指定的連續驗證失敗次數後鎖定。 在指定的時間長度後，使用者可以嘗試再次驗證。 此功能可防止使用者嘗試各種認證組合來存取系統。

使用「網域管理」頁面上的設定來指定驗證失敗的最大數目和帳戶鎖定的時間長度。 這些設定會套用至所有已啟用帳戶鎖定的網域。

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>網域管理]**.
1. 在「連續驗證失敗數上限」方塊中，輸入使用者在鎖定其帳戶之前，可嘗試登入不成功的連續次數。 默认值为 20。
1. 在「解除鎖定帳戶之後（分鐘）」方塊中，輸入使用者帳戶被鎖定的分鐘數。 在指定的分鐘數後，使用者可以嘗試再次登入。 默认值为 30。
1. 单击“**[!UICONTROL 保存]**”。
