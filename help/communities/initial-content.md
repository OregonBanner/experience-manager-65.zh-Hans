---
title: 初始沙箱内容
seo-title: 初始沙箱内容
description: 创建内容
seo-description: 创建内容
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 4%

---


# 初始沙箱内容{#initial-sandbox-content}

在本节中，您将创建以下全部使用[页面模板](initial-app.md#createthepagetemplate)的页面：

* SCF沙箱站点，它将重定向到主页的英文版本。

   * SCF沙箱——站点英语版本的主页。

   * SCF播放——要播放的主页的子项。

虽然本教程不深入[语言副本](../../help/sites-administering/tc-prep.md)，但设计根页面时，根页面可以通过HTML头实现对用户首选语言的检测，并重定向到该语言的相应主页。 惯例是将两个字母的国家／地区代码用于页面的节点名称，例如，“en”表示英语，“fr”表示法语，依此类推。

## 创建首页{#create-first-pages}

现在有[页面模板](initial-app.md#createthepagetemplate)，我们可以在/content目录中建立网站的根页面。

1. 标准UI目前提供创建站点的蓝图。 由于本教程是创建一个简单的站点，因此经典UI很有用。

   要切换到经典UI，请选择全局导航并将鼠标悬停在“项目”图标的右侧。 选择显示的&#x200B;*切换到经典UI*&#x200B;图标：

   ![经典ui](assets/classic-ui.png)

   切换到经典UI的功能必须由管理员[启用。](../../help/sites-administering/enable-classic-ui.md)

1. 从[经典UI欢迎页面](http://localhost:4502/welcome.html)中，选择&#x200B;**[!UICONTROL 网站]**。

   ![经典-ui-website](assets/classic-ui-website.png)

   或者，也可以通过浏览至[/siteadmin直接访问网站的经典UI。](http://localhost:4502/siteadmin)

1. 在资源管理器窗格中，选择&#x200B;**[!UICONTROL 网站]**，然后在工具栏中选择&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建页面]**。

   在&#x200B;**[!UICONTROL 创建页面]**&#x200B;对话框中，输入以下内容：

   * 标题: `SCF Sandbox Site`
   * 名称: `an-scf-sandbox`
   * 选择&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

   ![经典-ui-create-page](assets/classic-ui-create-page.png)

1. 在资源管理器窗格中，选择刚刚创建的页面`/Websites/SCF Sandbox Site`，然后单击&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建页面]**:

   * 标题: `SCF Sandbox`
   * 名称: `en`
   * 选择&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

1. 在资源管理器窗格中，选择刚刚创建的页面`/Websites/SCF Sandbox Site/SCF Sandbox`，然后单击&#x200B;**[!UICONTROL 新建]** > **[!UICONTROL 新建页面]**

   * 标题: `SCF Play`
   * 名称: `play`
   * 选择&#x200B;**[!UICONTROL SCF沙箱播放模板]**
   * 单击&#x200B;**[!UICONTROL 创建]**

1. 网站现在通过此方式显示在“网站”控制台中。 请注意，资源管理器窗格中选定项目的子页面会显示在可以管理这些页面的右侧窗格中。

   ![经典-ui-website-page](assets/classic-ui-website-page.png)

   这是使用网站工具和模板创建内容的存储库视图:

   ![classic-ui-repository-视图](assets/classic-ui-repository-view.png)

## 添加设计路径{#add-the-design-path}

使用“工具”控制台的“设计”部分创建` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)`时，属性“

* `cq:template="/libs/wcm/core/templates/designpage"`

定义，它提供在脚本中使用`currentDesign.getPath()`引用设计资源的可选功能。 例如

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名称: `cq:designPath`
   * 类型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 单击绿色`[+] Add`

存储库应当如下：

![经典-ui-repository-path](assets/classic-ui-repository-path.png)

* 单击&#x200B;**[!UICONTROL 保存全部]**

如果保存配置时出现任何问题，请重新登录并重新配置。

>[!NOTE]
>
>使用`cq:designPath`是可选的，与使用clientlibs](develop-app.md#includeclientlibsintemplate)无关，这是SCF组件使用[clientlibs](client-customize.md#clientlibs-for-scf)管理其JS和CSS时必需的。[
