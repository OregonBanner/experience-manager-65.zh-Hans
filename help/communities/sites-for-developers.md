---
title: 社区站点要点
seo-title: Community Site Essentials
description: 导出和删除社区站点并创建自定义站点模板
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# 社区站点要点 {#community-site-essentials}

## 自定义站点模板 {#custom-site-template}

可以为社区站点的每个语言副本单独指定自定义站点模板。

为此，请执行以下操作：

* 创建自定义模板。
* 覆盖默认站点模板路径。
* 将自定义模板添加到叠加路径。
* 通过添加 `page-template` 属性到 `configuration` 节点。

**默认模板**：

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**覆盖路径中的自定义模板**：

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**属性**： page-template

**类型**：字符串

**值**： `template-name` （无扩展名）

**配置节点**：

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>覆盖路径中的所有节点只需要属于类型 `Folder`.

>[!CAUTION]
>
>如果为自定义模板指定名称 *sitepage.hbs*，则会自定义所有社区站点。

### 自定义站点模板示例 {#custom-site-template-example}

例如， `vertical-sitepage.hbs` 是一个网站模板，它可以在页面左侧垂直放置菜单链接，而不是在横幅下方水平放置。

[获取文件](assets/vertical-sitepage.hbs)
将自定义站点模板放置在覆盖文件夹中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通过添加 `page-template` 属性到配置节点：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

请确保 **全部保存** 并将自定义代码复制到所有AEM实例（从控制台发布社区站点内容时不包括自定义代码）。

复制自定义代码的推荐做法是 [创建资源包](../../help/sites-administering/package-manager.md#creating-a-new-package) 并在所有实例上部署它。

## 导出社区站点 {#exporting-a-community-site}

创建社区站点后，可以将站点导出为存储在包管理器中并可供下载和上传的AEM包。

这可以从以下位置获得： [社区站点控制台](sites-console.md#exporting-the-site).

请注意，UGC和自定义代码未包含在社区站点包中。

要导出UGC，请使用 [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)，它是GitHub上提供的一项开源迁移工具。

## 删除社区站点 {#deleting-a-community-site}

自AEM Communities 6.3 Service Pack 1起，将鼠标悬停在中的社区站点上时，将显示“删除站点”图标。 **[!UICONTROL Communities]** > **[!UICONTROL 站点]** 控制台。 在开发期间，如果想要删除社区站点并重新开始，您可以使用此功能。 删除社区站点时，将删除与该站点关联的以下项目：

* [UGC](#user-generated-content)
* [用户组](#community-user-groups)
* [数据库记录](#database-records)

### 社区唯一站点ID {#community-unique-site-id}

要使用CRXDE识别与社区站点关联的唯一站点ID，请执行以下操作：

* 导航到站点的语言根，例如 `/content/sites/*<site name>*/en/rep:policy`.

* 查找 `allow<#>` 具有的节点 `rep:principalName` 在此格式中 `rep:principalName = *community-enable-nrh9h-members*`.

* 站点ID是的第三个组件 `rep:principalName`

   例如，如果 `rep:principalName = community-enable-nrh9h-members`

   * **站点名称** = *启用*
   * **站点ID** = *nrh9h*
   * **唯一站点ID** = *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

从Github获取communities-srp-tools项目：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

这包含一个servlet，用于从任何SRP中删除所有UGC。

可以删除所有UGC或针对特定站点的UGC，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

这只会删除用户生成的内容（在发布时输入），而不会删除创作内容（在作者时输入）。 因此， [影子节点](srp.md#shadownodes) 不会受到影响。

### 社区用户组 {#community-user-groups}

在所有创作和发布实例上，从 [安全控制台](../../help/sites-administering/security.md)，找到并删除 [用户组](users.md) 即：

* 前缀 `community`
* 后接 [唯一站点id](#community-unique-site-id)

例如：`community-engage-x0e11-members`。
