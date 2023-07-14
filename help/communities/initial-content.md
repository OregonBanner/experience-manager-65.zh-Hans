---
title: 初始沙盒内容
description: 创建内容
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 2%

---

# 初始沙盒内容 {#initial-sandbox-content}

在此部分中，您将创建以下页面，这些页面都使用 [页面模板](initial-app.md#createthepagetemplate)：

* SCF沙盒站点，重定向到主页的英语版本。

   * SCF沙盒 — 站点的英文版本的主页。

   * SCF播放 — 要播放的主页的子页面。

尽管本教程并未深入探讨 [语言副本](../../help/sites-administering/tc-prep.md)，因此根页面可以通过HTML标题为用户实施首选语言检测，并重定向到该语言的相应主页。 惯例是将两个字母的国家/地区代码用于页面的节点名称，例如，“en”表示英语，“fr”表示法语。

## 创建第一页 {#create-first-pages}

现在，有一个 [页面模板](initial-app.md#createthepagetemplate)中，您可以在/content目录中建立网站的根页面。

1. 标准UI当前提供用于创建站点的蓝图。 由于本教程创建的是简单的站点，因此经典UI非常有用。

   要切换到经典UI，请选择全局导航，并将鼠标悬停在项目图标的右侧。 选择 *切换到经典UI* 图标，将显示：

   ![经典ui](assets/classic-ui.png)

   切换到经典UI的功能必须 [由管理员启用](../../help/sites-administering/enable-classic-ui.md).

1. 从 [经典UI欢迎页面](http://localhost:4502/welcome.html)，选择 **[!UICONTROL 网站]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   或者，通过浏览以直接访问网站的经典UI [/siteadmin.](http://localhost:4502/siteadmin)

1. 在资源管理器窗格中，选择 **[!UICONTROL 网站]** 然后在工具栏中选择 **[!UICONTROL 新]** > **[!UICONTROL 新页面]**.

   在 **[!UICONTROL 创建页面]** 对话框，请输入以下内容：

   * 标题: `SCF Sandbox Site`
   * 名称: `an-scf-sandbox`
   * 选择 **[!UICONTROL SCF沙盒播放模板]**
   * 单击 **[!UICONTROL 创建]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 在资源管理器窗格中，选择您创建的页面， `/Websites/SCF Sandbox Site`，然后单击 **[!UICONTROL 新]** > **[!UICONTROL 新页面]**：

   * 标题: `SCF Sandbox`
   * 名称: `en`
   * 选择 **[!UICONTROL SCF沙盒播放模板]**
   * 单击 **[!UICONTROL 创建]**

1. 在资源管理器窗格中，选择您创建的页面， `/Websites/SCF Sandbox Site/SCF Sandbox`，然后单击 **[!UICONTROL 新]** > **[!UICONTROL 新页面]**

   * 标题: `SCF Play`
   * 名称: `play`
   * 选择 **[!UICONTROL SCF沙盒播放模板]**
   * 单击 **[!UICONTROL 创建]**

1. 这就是网站现在在“网站”控制台中的显示方式。 请注意，在资源管理器窗格中选择的项目的子页面将显示在可以对其进行管理的右侧窗格中。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   这是使用网站工具和模板创建的内容的存储库视图：

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 添加设计路径 {#add-the-design-path}

时间 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 创建时使用“工具”控制台的“设计”部分，即属性“

* `cq:template="/libs/wcm/core/templates/designpage"`

定义了，这提供了在脚本中使用引用设计资源的可选功能 `currentDesign.getPath()`. 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名称: `cq:designPath`
   * 类型: `String`
   * 价值: `/etc/designs/an-scf-sandbox`

* 单击绿色 `[+] Add`

存储库应如下所示：

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 单击 **[!UICONTROL 全部保存]**

如果保存配置时出现任何问题，请重新登录并再次配置。

>[!NOTE]
>
>使用 `cq:designPath` 是可选的，并且与 [clientlibs的使用](develop-app.md#includeclientlibsintemplate)，这些参数是SCF组件使用 [clientlibs](client-customize.md#clientlibs-for-scf) 以管理其JS和CSS。
