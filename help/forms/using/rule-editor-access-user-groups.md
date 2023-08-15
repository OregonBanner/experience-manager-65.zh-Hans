---
title: 向选定的用户组授予对规则编辑器的访问权限
seo-title: Grant rule editor access to select user groups
description: 向选定用户组授予对规则编辑器的受限访问权限。
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 20%

---

# 向选定的用户组授予对规则编辑器的访问权限{#grant-rule-editor-access-to-select-user-groups}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

您可能拥有具有不同技能的不同类型的用户，能够使用自适应Forms。 虽然专家用户可能拥有处理脚本和复杂规则的正确知识，但可能有基本级用户需要仅处理自适应表单的布局和基本属性。

AEM Forms允许您根据用户的角色或职能限制用户对规则编辑器的访问权限。 在自适应Forms配置服务设置中，您可以指定 [用户组](/help/sites-administering/security.md) 可以查看和访问规则编辑器。

## 指定可以访问规则编辑器的用户组 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理员身份登录到AEM Forms。
1. 在创作实例中，单击 ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![锤子](assets/hammer.png) >操作> Web控制台。 Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到并单击 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]**. **[!UICONTROL 自适应表单和交互式通信Web渠道配置]** 出现对话框。 不更改任何值并单击 **保存**.

   它会在CRX存储库中创建文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config 。

1. 以管理员身份登录到CRXDE。 打开文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如，RuleEditorsUserGroup），然后单击 **全部保存**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问，请指定逗号分隔值的列表：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，当不属于指定用户组（此处为RuleEditorsUserGroup）的用户点击字段时，编辑规则图标( ![edit-rules1](assets/edit-rules1.png))在组件工具栏中不可用：

   ![componentstolbarwithre](assets/componentstoolbarwithre.png)

   对具有规则编辑器访问权限的用户可见的组件工具栏

   ![componentstolbarwithoutre](assets/componentstoolbarwithoutre.png)

   对没有规则编辑器访问权限的用户可见的组件工具栏

   有关将用户添加到组的说明，请参阅 [用户管理和安全性](/help/sites-administering/security.md).
