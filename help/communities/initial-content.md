---
title: 初始沙盒内容
seo-title: 初始沙盒内容
description: 创建内容
seo-description: 创建内容
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 4%

---

# 初始沙盒内容{#initial-sandbox-content}

在本节中，您将创建以下所有页面，这些页面均使用[页面模板](initial-app.md#createthepagetemplate):

* SCF沙盒站点，该站点将重定向到主页的英文版本。

   * SCF沙盒 — 网站英文版本的主页。

   * SCF播放 — 要播放的主页的子项。

尽管本教程不深入[语言副本](../../help/sites-administering/tc-prep.md)，但设计该教程是为了使根页面可以通过HTML标头对用户实施首选语言检测，并重定向到相应的语言主页。 惯例是使用双字母国家/地区代码表示页面的节点名称，例如，“en”表示英语，“fr”表示法语，等等。

## 创建首页{#create-first-pages}

现在有[页面模板](initial-app.md#createthepagetemplate)，我们可以在/content目录中建立网站的根页面。

1. 标准UI当前提供了创建站点的蓝图。 由于本教程将创建一个简单的站点，因此经典UI非常有用。

   要切换到经典UI，请选择全局导航，并将鼠标悬停在“项目”图标的右侧。 选择显示的&#x200B;*切换到经典UI*&#x200B;图标：

   ![经典ui](assets/classic-ui.png)

   切换到经典UI的功能必须由管理员](../../help/sites-administering/enable-classic-ui.md)启用。[

1. 从[经典UI欢迎页面](http://localhost:4502/welcome.html)中，选择&#x200B;**[!UICONTROL 网站]**。

   ![classic-ui-website](assets/classic-ui-website.png)

   或者，直接通过浏览到[/siteadmin.](http://localhost:4502/siteadmin)访问网站的经典UI

1. 在资源管理器窗格中，选择&#x200B;**[!UICONTROL 网站]**，然后在工具栏中选择&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建页面]**。

   在&#x200B;**[!UICONTROL 创建页面]**&#x200B;对话框中，输入以下内容：

   * 标题: `SCF Sandbox Site`
   * 名称: `an-scf-sandbox`
   * 选择&#x200B;**[!UICONTROL SCF沙盒播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. 在资源管理器窗格中，选择之前创建的页面`/Websites/SCF Sandbox Site`，然后单击&#x200B;**[!UICONTROL New]** > **[!UICONTROL New Page]**:

   * 标题: `SCF Sandbox`
   * 名称: `en`
   * 选择&#x200B;**[!UICONTROL SCF沙盒播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

1. 在资源管理器窗格中，选择之前创建的页面`/Websites/SCF Sandbox Site/SCF Sandbox`，然后单击&#x200B;**[!UICONTROL New]** > **[!UICONTROL New Page]**

   * 标题: `SCF Play`
   * 名称: `play`
   * 选择&#x200B;**[!UICONTROL SCF沙盒播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

1. 网站现在以此方式显示在“网站”控制台中。 请注意，在资源管理器窗格中选择的项目的子页面显示在可以管理这些子页面的右侧窗格中。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   这是使用网站工具和模板创建的内容的存储库视图：

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## 添加设计路径{#add-the-design-path}

使用“工具”控制台的设计部分创建` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`时，属性“

* `cq:template="/libs/wcm/core/templates/designpage"`

定义了，该函数提供了使用`currentDesign.getPath()`引用脚本中设计资产的可选功能。 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名称: `cq:designPath`
   * 类型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 单击绿色的`[+] Add`

存储库应如下所示：

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* 单击&#x200B;**[!UICONTROL Save All]**

如果在保存配置时遇到任何问题，请重新登录并再次配置。

>[!NOTE]
>
>`cq:designPath`的使用是可选的，并且与[使用clientlibs](develop-app.md#includeclientlibsintemplate)无关，而Clientlibs实质上是必需的，因为SCF组件使用[clientlibs](client-customize.md#clientlibs-for-scf)管理其JS和CSS。
