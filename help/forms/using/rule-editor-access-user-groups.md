---
title: 授予规则编辑器对选定用户组的访问权限
seo-title: 授予规则编辑器对选定用户组的访问权限
description: 授予对规则编辑器的受限访问权限以选择用户组。
seo-description: 授予对规则编辑器的受限访问权限以选择用户组。
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 授予规则编辑器对选定用户组的访问权限{#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

您可能具有不同技能的不同类型的用户使用自适应表单。 虽然专家用户可能拥有使用脚本和复杂规则的正确知识，但可能有一些基本级用户只需要使用自适应表单的布局和基本属性。

AEM Forms允许您根据用户的角色或功能将规则编辑器访问权限限制为用户。 在“自适应表单配置服务”设置中，可指定可查 [看和访问规则编辑](/help/sites-administering/security.md) 器的用户组。

## 指定可以访问规则编辑器的用户组 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理员身份登录到AEM Forms。
1. 在创作实例中，单击 ![](assets/adobeexperiencemanager.png)adobeexperiencemanagerAdobe Experience Manager >工具锤 ![子](assets/hammer.png) >操作> Web Console。 Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. 在“Web控制台”窗口中，找到并单击“自适 **应表单配置服务”**。 **随后将显示“自适应表单配置服务** ”对话框。 请勿更改任何值，然后单击“保 **存”**。

   它在CRX-repository中创建一个文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config。

1. 以管理员身份登录到CRXDE。 打开文件/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如，RuleEditorsUserGroup），然后单击“全 **部保存”**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问权限，请指定逗号分隔值列表：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，如果用户不是指定用户组的一部分（此处为RuleEditorsUserGroup），则在组件工具栏中对其点击字段时，“编辑规则”图标( ![edit-rules1](assets/edit-rules1.png))不可用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有规则编辑器访问权限的用户可见的组件工具栏

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   组件工具栏（对于没有规则编辑器访问权限的用户可见）

   有关将用户添加到用户组的说明，请参 [阅用户管理和安全](/help/sites-administering/security.md)。

