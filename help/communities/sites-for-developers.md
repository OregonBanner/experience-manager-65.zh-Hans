---
title: Community Site Essentials
seo-title: Community Site Essentials
description: 导出和删除社区站点以及创建自定义站点模板
seo-description: 导出和删除社区站点以及创建自定义站点模板
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: 89156f94f2d0494d44d4f0b99abfba4fafbc66d3

---


# Community Site Essentials {#community-site-essentials}

## 自定义站点模板 {#custom-site-template}

可以为社区站点的每个语言副本单独指定自定义站点模板。

为此，请执行以下操作：

* 创建自定义模板。
* 叠加默认站点模板路径。
* 将自定义模板添加到叠加路径。
* 通过向节点添加属性来指 `page-template` 定自定义模 `configuration` 板。

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
>如果为自定义模板指定名称 *sitepage.hbs*，则将自定义所有社区站点。


### 自定义站点模板示例 {#custom-site-template-example}

例如，站点模 `vertical-sitepage.hbs` 板导致菜单链接在页面左侧垂直放置，而不是在横幅下方水平放置。

[获取文](assets/vertical-sitepage.hbs)件将自定义站点模板放在叠加文件夹中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通过向配置节点添加属 `page-template` 性来标识自定义模板：

`/content/sites/sample/en/configuration`

![chlimage_1-80](assets/chlimage_1-80.png)

请务必保 **存全部** ，并将自定义代码复制到所有AEM实例（从控制台发布社区站点内容时不包括自定义代码）。

复制自定义代码的建议做法是创 [建一个包](../../help/sites-administering/package-manager.md#creating-a-new-package) ，并将其部署到所有实例。

## 导出社区站点 {#exporting-a-community-site}

创建社区站点后，可以将站点导出为存储在包管理器中并可供下载和上传的AEM包。

可从“社区站点”控 [制台中执行此操作](sites-console.md#exporting-the-site)。

请注意，UGC和自定义代码不包含在社区站点包中。

要导出UGC，请使用 [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)，这是GitHub上提供的一个开放源代码迁移工具。

## 删除社区站点 {#deleting-a-community-site}

自AEM Communities 6.3 Service Pack 1起，“删除站点”图标显示在“社区” **[!UICONTROL >“站点”控制台中]** 的社区站 **** 点上。 在开发过程中，如果需要删除社区站点和开始，您可以使用此功能。 删除社区站点时，会删除与该站点关联的以下项目：

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

   * **站点名称** = *enable*
   * **站点ID** = *nrh9h*
   * **唯一站点ID** = *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

从Github获取communities-srp-tools项目：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

它包含一个servlet，用于从任何SRP中删除所有UGC。

所有UGC都可能被删除，或者特定站点的UGC都会被删除，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

这只会删除用户生成的内容（在发布时输入）和未创作的内容（在创作时输入）。 因此， [阴影节点](srp.md#shadownodes) 不受影响。

### 社区用户组 {#community-user-groups}

在所有作者实例和发布实例上，从安 [全控制台](../../help/sites-administering/security.md)，找到并删 [除以下用户组](users.md) :

* 前缀为 `community`
* 后跟唯 [一站点ID](#community-unique-site-id)

For example, `community-engage-x0e11-members`.

### Enablement Assets {#enablement-assets}

从主控制台中：

* Select **[!UICONTROL Assets]**.
* 进入 **[!UICONTROL 选择]** 模式。
* 选择以唯一站点Id命名 [的文件夹](#community-unique-site-id)。
* 选 **[!UICONTROL 择删除]** (可能需要从更 **[!UICONTROL 多……]**)。

### 数据库记录 {#database-records}

没有用于选择性地删除特定支持社区站点的数据库条目的工具。

删除所有社区站点后，请使用MySQL Workbench放置enablementdb和scormenginedb。
