---
title: 向选定的用户组授予对规则编辑器的访问权限
seo-title: Grant rule editor access to select user groups
description: 將限制存取權授與規則編輯器以選取使用者群組。
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 6%

---

# 向选定的用户组授予对规则编辑器的访问权限{#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

您可能有不同型別的使用者，且他們的各種技能都適用於Adaptive Forms。 雖然專家使用者可能擁有使用指令碼和複雜規則的正確知識，但可能有基本級使用者需要僅使用最適化表單的版面和基本屬性。

AEM Forms可讓您根據使用者的角色或功能，限制使用者的規則編輯器存取權。 在最適化Forms組態服務設定中，您可以指定 [使用者群組](/help/sites-administering/security.md) 可檢視和存取規則編輯器的屬性。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理員身分登入AEM Forms。
1. 在作者執行個體中，按一下 ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![槌子](assets/hammer.png) >作業> Web主控台。 Web主控台會在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在Web主控台視窗中，找到並按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]**. **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 對話方塊隨即顯示。 不要變更任何值並按一下 **儲存**.

   它會在CRX-repository中建立檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理員身分登入CRXDE。 開啟檔案/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config以進行編輯。
1. 使用下列屬性來指定可存取規則編輯器的群組名稱（例如RuleEditorsUserGroup），然後按一下 **全部儲存**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定以逗號分隔的值清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   現在，當不屬於指定使用者群組（此處為RuleEditorsUserGroup）的使用者點選欄位時，編輯規則圖示( ![edit-rules1](assets/edit-rules1.png))在元件工具列中無法使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取許可權的使用者看得見的元件工具列

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   沒有規則編輯器存取權的使用者看得見的元件工具列

   如需新增使用者至群組的指示，請參閱 [使用者管理與安全性](/help/sites-administering/security.md).
