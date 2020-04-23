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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# 初始沙箱内容 {#initial-sandbox-content}

在此部分中，您将创建以下全部使用页面模板 [的页面](initial-app.md#createthepagetemplate):

* SCF沙箱站点，它将重定向到英文版的主页。

   * SCF沙箱——站点的英文版主页。

      * SCF播放——要在其中播放的主页的子级。

虽然本教程不深入 [研究语言副本](../../help/sites-administering/tc-prep.md)，但设计它是为了使根页面能够通过HTML标题实现对用户首选语言的检测，并重定向到相应的语言主页。 惯例是将双字母国家／地区代码用于页面的节点名称，例如，“en”表示英语，“fr”表示法语，等等。

## 创建首页 {#create-first-pages}

现在有一个页 [面模板](initial-app.md#createthepagetemplate)，我们可以在/content目录中建立网站的根页面。

1. 标准UI目前提供了创建站点的蓝图。 由于本教程创建的是一个简单的站点，因此经典UI很有用。

   要切换到经典UI，请选择全局导航并将鼠标悬停在“项目”图标的右侧。 选择显 *示的切换到经典UI* 图标：

   ![chlimage_1-36](assets/chlimage_1-36.png)

   必须由管理员启用切换到经 [典UI的功能](../../help/sites-administering/enable-classic-ui.md)。

1. 从经典UI [欢迎页面中](http://localhost:4502/welcome.html)，选择 **[!UICONTROL 网站]**。

   ![chlimage_1-37](assets/chlimage_1-37.png)

   或者，也可以通过浏览到 [/siteadmin直接访问网站的经典UI。](http://localhost:4502/siteadmin)

1. 在资源管理器窗格中，选 **[!UICONTROL 择网站]** ，然后在工具栏中选择“新建 **[!UICONTROL ”]** >“ **[!UICONTROL 新建页面”]**。

   在“创 **[!UICONTROL 建页面]** ”对话框中，输入以下内容：

   * 标题: `SCF Sandbox Site`
   * 名称: `an-scf-sandbox`
   * 选择 **[!UICONTROL SCF沙箱播放模板]**
   * Click **[!UICONTROL Create]**
   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 在资源管理器窗格中，选择刚刚创建的页面， `/Websites/SCF Sandbox Site`然后单击“新 **[!UICONTROL 建]** >新 **[!UICONTROL 建页面]**”:

   * 标题: `SCF Sandbox`
   * 名称: `en`
   * 选择 **SCF沙箱播放模板&#x200B;**
   * Click **Create **

1. 在资源管理器窗格中，选择刚刚创建的页面，然 `/Websites/SCF Sandbox Site/SCF Sandbox`后单击“新 **[!UICONTROL 建]** >新 **[!UICONTROL 建页面”]**

   * 标题: `SCF Play`
   * 名称: `play`
   * 选择 **[!UICONTROL SCF沙箱播放模板]**
   * Click **[!UICONTROL Create]**

1. 网站控制台中现在会显示此网站。 请注意，资源管理器窗格中选定项目的子页面将显示在可以管理这些页面的右侧窗格中。

   ![chlimage_1-39](assets/chlimage_1-39.png)

   这是使用网站工具和模板创建内容的存储库视图:

   ![chlimage_1-40](assets/chlimage_1-40.png)

## 添加设计路径 {#add-the-design-path}

当使 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` 用“工具”控制台的设计部分创建时，属性“

* `cq:template="/libs/wcm/core/templates/designpage"`

定义，该功能提供了在脚本中使用引用设计资源的可选功能 `currentDesign.getPath()`例如

* &lt;% String favIcon = currentDesign.getPath()+ &quot;/favicon.ico&quot;;%>


   * 名称: `cq:designPath`
   * 类型: `String`
   * 值: `/etc/designs/an-scf-sandbox`

* 单击绿色 `[+] Add`

存储库应当如下：

![chlimage_1-41](assets/chlimage_1-41.png)

* 单击“ **[!UICONTROL 全部保存”]**

[ 难以省钱？ 重新登录！ ]

>[!NOTE]
>
>cq:designPath的使用是可选的，与clientlibs的使用无关 [，这是SCF组件使用clientlibs管理其JS和CSS时必需的，](develop-app.md#includeclientlibsintemplate)因为Clientlibs [](client-customize.md#clientlibs-for-scf) 是必需的。


