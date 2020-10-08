---
title: 社区站点基础
seo-title: 社区站点基础
description: 导出和删除社区站点以及创建自定义站点模板
seo-description: 导出和删除社区站点以及创建自定义站点模板
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# 社区站点基础 {#community-site-essentials}

## 自定义站点模板 {#custom-site-template}

可以为社区站点的每个语言副本单独指定自定义站点模板。

为此，请执行以下操作：

* 创建自定义模板。
* 叠加默认站点模板路径。
* 将自定义模板添加到叠加路径。
* 通过向节点添加属性来 `page-template` 指定自定义 `configuration` 模板。

**默认模板**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**叠加路径中的自定义模板**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**属性**:page-template

**类型**:字符串

**值**: `template-name` （无扩展）

**配置节点**:

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>叠加路径中的所有节点只需为类型 `Folder`。

>[!CAUTION]
>
>如果为自定义模板指定了名 *称sitepage.hbs*，则将自定义所有社区站点。

### 自定义站点模板示例 {#custom-site-template-example}

例如，站点 `vertical-sitepage.hbs` 模板会导致菜单链接垂直放置在页面左侧而不是横幅下方。

[获取文](assets/vertical-sitepage.hbs)件将自定义站点模板放在叠加文件夹中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通过向配置节点添加属 `page-template` 性来标识自定义模板：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

请务必保 **存全部** ，并将自定义代码复制到所有AEM实例（从控制台发布社区站点内容时不包括自定义代码）。

复制自定义代码的建议做法是 [创建包并在](../../help/sites-administering/package-manager.md#creating-a-new-package) 所有实例上部署它。

## 导出社区站点 {#exporting-a-community-site}

创建社区站点后，可以将站点导出为存储在包管理器中的AEM包，并可供下载和上传。

可从“社区站点” [控制台访问](sites-console.md#exporting-the-site)。

请注意，UGC和自定义代码不包括在社区站点包中。

要导出UGC，请使用 [AEM CommunitiesUGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)（GitHub上提供的一个开放源代码迁移工具）。

## 删除社区站点 {#deleting-a-community-site}

从AEM Communities6.3 Service Pack 1开始，“社区”>“站点”控制台中将鼠标悬停在社区站点上方时，将显示“删 **[!UICONTROL 除站点]** ” **[!UICONTROL 图标]** 。 在开发过程中，如果需要删除社区站点和开始，则可以使用此功能。 删除社区站点时，会删除与该站点关联的以下项目：

* [UGC](#user-generated-content)
* [用户组](#community-user-groups)
* [资产](#enablement-assets)
* [数据库记录](#database-records)

### 社区唯一站点ID {#community-unique-site-id}

要标识与社区站点关联的唯一站点ID，请使用CRXDE:

* 导航到站点的语言根目录，如 `/content/sites/*<site name>*/en/rep:policy`。

* 查找 `allow<#>` 具有此格 `rep:principalName` 式的节点 `rep:principalName = *community-enable-nrh9h-members*`。

* 站点ID是 `rep:principalName`

   例如，如果 `rep:principalName = community-enable-nrh9h-members`

   * **站点名称** =启 *用*
   * **站点ID** = *nrh9h*
   * **唯一站点ID** = *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

从Github获取communities-srp-tools项目：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

它包含一个servlet，用于从任何SRP中删除所有UGC。

可以删除所有UGC或针对特定站点，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

这只会删除用户生成的内容（在发布时输入）和未创作的内容（在创作时输入）。 因此， [阴影节点](srp.md#shadownodes) 不受影响。

### 社区用户组 {#community-user-groups}

在所有作者和发布实例上，从 [安全控制台](../../help/sites-administering/security.md)，找到并 [删除以下用](users.md) 户组：

* 前缀为 `community`
* 后跟唯 [一站点ID](#community-unique-site-id)

For example, `community-engage-x0e11-members`.

### Enablement Assets {#enablement-assets}

从主控制台：

* Select **[!UICONTROL Assets]**.
* 进入 **[!UICONTROL 选择]** 模式。
* 选择使用唯一站点ID [命名的文件夹](#community-unique-site-id)。
* 选 **[!UICONTROL 择]** “删除”(可能需要从更 **[!UICONTROL 多……]**)。

### 数据库记录 {#database-records}

没有用于选择性地删除特定启用社区站点的数据库条目的工具。

删除所有社区站点后，使用MySQL Workbench删除enablementdb和scormenginedb。
