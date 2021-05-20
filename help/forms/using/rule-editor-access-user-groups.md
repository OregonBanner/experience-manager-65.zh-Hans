---
title: 向选定的用户组授予对规则编辑器的访问权限
seo-title: 向选定的用户组授予对规则编辑器的访问权限
description: 为选择用户组授予对规则编辑器的受限访问权限。
seo-description: 为选择用户组授予对规则编辑器的受限访问权限。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: 自适应表单
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 8%

---

# 向选定的用户组授予对规则编辑器的访问权限{#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

您可能拥有不同类型的具有各种技能的用户，这些用户可以与自适应Forms一起使用。 虽然专家用户可能拥有使用脚本和复杂规则的正确知识，但可能有一些基本级别的用户需要仅使用自适应表单的布局和基本属性。

AEM Forms允许您根据用户的角色或功能限制用户对规则编辑器的访问权限。 在自适应Forms配置服务设置中，您可以指定可以查看和访问规则编辑器的[用户组](/help/sites-administering/security.md)。

## 指定可以访问规则编辑器{#specify-user-groups-that-can-access-rule-editor}的用户组

1. 以管理员身份登录AEM Forms。
1. 在创作实例中，单击![ adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具![hammer](assets/hammer.png) >操作> Web控制台。 Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到并单击&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**。 **[!UICONTROL 出现“自适应表单和交互式通信Web渠道]** 配置”对话框。请勿更改任何值，然后单击&#x200B;**Save**。

   它会在CRX-repository中创建一个文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 。

1. 以管理员身份登录到CRXDE。 打开文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config以进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如， RuleEditorsUserGroup），然后单击&#x200B;**Save All**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问权限，请指定逗号分隔值列表：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，当不属于指定用户组的用户（此处为RuleEditorsUserGroup）点按字段时，组件工具栏中的“编辑规则”图标(![edit-rules1](assets/edit-rules1.png))不可供她使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有规则编辑器访问权限的用户可看到的组件工具栏

   ![组件stoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   对没有规则编辑器访问权限的用户可见的组件工具栏

   有关将用户添加到组的说明，请参阅[用户管理和安全](/help/sites-administering/security.md)。
