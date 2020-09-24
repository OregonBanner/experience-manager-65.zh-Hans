---
title: 授予规则编辑者对选定用户组的访问权限
seo-title: 授予规则编辑者对选定用户组的访问权限
description: 授予对规则编辑器的受限访问权限以选择用户组。
seo-description: 授予对规则编辑器的受限访问权限以选择用户组。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---


# 授予规则编辑者对选定用户组的访问权限{#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

您可能具有不同技能的不同类型的用户与自适应Forms一起工作。 虽然专家用户可能拥有使用脚本和复杂规则的正确知识，但可能有一些基本级用户只需要使用自适应表单的布局和基本属性。

AEM Forms允许您根据用户的角色或功能限制规则编辑器对用户的访问。 在自适应Forms配置服务设置中，可以指 [定可以视图](/help/sites-administering/security.md) 和访问规则编辑器的用户组。

## 指定可访问规则编辑器的用户组 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理员身份登录AEM Forms。
1. 在创作实例中，单击 ![](assets/adobeexperiencemanager.png)adobeexperiencemanagerAdobeExperience Manager> ![工具锤](assets/hammer.png) >操作> Web Console。 Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. 在Web控制台窗口中，找到并单 **击自适应表单配置服务**。 **出现“Adaptive Form Configuration Service** （自适应表单配置服务）”对话框。 请勿更改任何值，然后单击“ **保存**”。

   它在CRX-repository中创建一个文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理员身份登录到CRXDE。 打开文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如，RuleEditorsUserGroup），然后单击“全部 **保存”**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问，请指定逗号分隔的列表值：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，当不属于指定用户组（此处为RuleEditorsUserGroup）的用户点击某个字段时，组件工具栏中的“编辑规则”图标( ![edit-rules1](assets/edit-rules1.png))将不可供其使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有规则编辑器访问权限的用户可见的组件工具栏

   ![组件stoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   组件工具栏（对于没有规则编辑器访问权限的用户可见）

   有关将用户添加到组的说明，请参 [阅用户管理和安全](/help/sites-administering/security.md)。

