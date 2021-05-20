---
title: 社区站点要点
seo-title: 社区站点要点
description: 导出和删除社区站点以及创建自定义站点模板
seo-description: 导出和删除社区站点以及创建自定义站点模板
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 社区站点要点{#community-site-essentials}

## 自定义网站模板{#custom-site-template}

可以单独地为社区站点的每个语言副本指定自定义站点模板。

为此，请执行以下操作：

* 创建自定义模板。
* 覆盖默认网站模板路径。
* 将自定义模板添加到叠加路径。
* 通过向`configuration`节点添加`page-template`属性来指定自定义模板。

**默认模板**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**叠加路径中的自定义模板**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**属性**:页面模板

**类型**:字符串

**值**: `template-name` （无扩展）

**配置节点**:

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>叠加路径中的所有节点只需为`Folder`类型。

>[!CAUTION]
>
>如果为自定义模板指定名称&#x200B;*sitepage.hbs*，则将自定义所有社区站点。

### 自定义网站模板示例{#custom-site-template-example}

例如，`vertical-sitepage.hbs`是一个网站模板，它会导致菜单链接垂直放置在页面左侧，而不是横幅的下方。

[获取](assets/vertical-sitepage.hbs)
文件将自定义网站模板放置到叠加文件夹中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通过向配置节点添加`page-template`属性来识别自定义模板：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

确保&#x200B;**保存所有**&#x200B;并将自定义代码复制到所有AEM实例（从控制台发布社区站点内容时，不包含自定义代码）。

复制自定义代码的建议做法是： [创建包](../../help/sites-administering/package-manager.md#creating-a-new-package)并在所有实例上部署该包。

## 导出社区站点{#exporting-a-community-site}

创建社区站点后，可以将该站点导出为存储在包管理器中的AEM包，以供下载和上载。

可从[Communities Sites控制台](sites-console.md#exporting-the-site)中执行此操作。

请注意，社区站点包中未包含UGC和自定义代码。

要导出UGC，请使用[AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)（GitHub上提供的开源迁移工具）。

## 删除社区站点{#deleting-a-community-site}

从AEM Communities 6.3 Service Pack 1开始，在将鼠标悬停在&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**&#x200B;控制台中的社区站点上方时，会显示“删除站点”图标。 在开发过程中，如果需要删除社区站点并重新开始，则可以使用此功能。 删除社区网站时，会删除与该网站关联的以下项目：

* [UGC](#user-generated-content)
* [用户组](#community-user-groups)
* [资产](#enablement-assets)
* [数据库记录](#database-records)

### 社区唯一网站ID {#community-unique-site-id}

要使用CRXDE标识与社区站点关联的唯一网站ID，请执行以下操作：

* 导航到站点的语言根目录，如`/content/sites/*<site name>*/en/rep:policy`。

* 以此格式`rep:principalName = *community-enable-nrh9h-members*`查找`allow<#>`节点，其中`rep:principalName`为节点。

* 网站ID是`rep:principalName`的第3个组件

   例如，如果`rep:principalName = community-enable-nrh9h-members`

   * **站点名称**  =  *enable*
   * **网站ID**  =  *nrh9h*
   * **唯一网站ID**  =  *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

从Github获取communities-srp-tools项目：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

此URL包含一个Servlet，用于从任何SRP中删除所有UGC。

可以删除所有UGC，或者为特定站点删除所有UGC，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

这仅会删除用户生成的内容（在发布时输入）和未创作的内容（在创作时输入）。 因此，[阴影节点](srp.md#shadownodes)不会受到影响。

### 社区用户组{#community-user-groups}

在所有创作和发布实例上，从[安全控制台](../../help/sites-administering/security.md)中，找到并删除以下用户组[](users.md):

* 前缀为`community`
* 后跟[唯一站点id](#community-unique-site-id)

例如，`community-engage-x0e11-members`。

### 启用资产{#enablement-assets}

从主控制台中：

* 选择&#x200B;**[!UICONTROL 资产]**。
* 进入&#x200B;**[!UICONTROL 选择]**&#x200B;模式。
* 选择使用[唯一站点Id](#community-unique-site-id)命名的文件夹。
* 选择&#x200B;**[!UICONTROL Delete]**（可能需要从&#x200B;**[!UICONTROL 更多……中选择）]**)。

### 数据库记录{#database-records}

没有用于选择性地删除某个特定启用社区站点的数据库条目的工具。

删除所有社区站点后，使用MySQL Workbench删除enablementdb和scormenginedb。
