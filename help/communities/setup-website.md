---
title: 设置网站结构
description: 了解如何设置网站结构，包括要创建的文件夹。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 设置网站结构 {#setup-website-structure}

要设置您的网站，请按照下面的说明说明在下列位置创建文件夹：

* `/apps/an-scf-sandbox`

  这是自定义应用程序和模板所在的位置。

* `/etc/designs/an-scf-sandbox`

  这是可下载设计元素所在的位置。

* `/content/an-scf-sandbox`

  这是可下载网页所在的位置。

本教程中的代码依赖于应用程序、设计和内容相同的主文件夹名称。 如果您为网站选择其他名称，请始终替换 `an-scf-sandbox` 你选择的名字。

>[!NOTE]
>
>关于名称：
>
>* 在CRXDE中看到的名称是节点名称，它们构成了可寻址内容的路径。
>* 节点名称可以包含空格，但在URI中使用时，该空格必须编码为“%20”或“+”。
>* 节点名称可以包含连字符和下划线，但是当节点名称在Java™文件中作为包名称引用时，必须对它们进行编码。 连字符和下划线均使用下划线进行转义，后跟其Unicode值：
>
* 连字符变为“_002d”
* 下划线变为“_005f”

## 设置应用程序目录(/apps) {#setup-the-application-directory-apps}

存储库中的/apps目录包含用于实施从/content目录提供的页面的行为和呈现的代码。

/apps目录受到保护，不能与/content和/etc/designs目录一样公开访问。

1. 创建 `/apps/an-scf-sandbox` 文件夹。

   使用 **[!UICONTROL CRXDE Lite]**，在资源管理器窗格中

   1. 选择 `/apps` 文件夹。
   1. 右键单击 **[!UICONTROL 创建]**...或将 **[!UICONTROL 创建……]** 菜单。
   1. 选择 **[!UICONTROL 创建文件夹……]**.
   1. 在 **[!UICONTROL 创建文件夹]** 对话框，输入 `an-scf-sandbox`.
   1. 单击&#x200B;**[!UICONTROL 确定]**。

1. 创建 **[!UICONTROL 组件]** 子文件夹。

   1. 选择 `/apps/an-scf-sandbox` 文件夹。
   1. 单击 **[!UICONTROL “创建”>“创建文件夹”]**.
   1. 在 **[!UICONTROL 创建文件夹]** 对话框，输入 **[!UICONTROL 组件]**.
   1. 单击&#x200B;**[!UICONTROL 确定]**。

1. 创建 **[!UICONTROL 模板]** 子文件夹。

   1. 选择 `/apps/an-scf-sandbox` 文件夹。
   1. 单击 **[!UICONTROL “创建”>“创建文件夹”]**.
   1. 在 **[!UICONTROL 创建文件夹]** 对话框，输入 **[!UICONTROL 模板]**.
   1. 单击&#x200B;**[!UICONTROL 确定]**。
   1. 重新选择 `/apps/an-scf-sandbox`.
   1. 选择 **[!UICONTROL 全部保存]**.

   与任何编辑过程一样，您应经常保存。 如果在输入数据时遇到问题，可能是因为登录已超时，也可能是因为必须保存以前的编辑。

1. CRXDE Lite浏览器窗格中的结构现在应如下所示：

   ![crxde-template](assets/crxde-template.png)

## 设置设计目录(/etc/designs) {#setup-the-design-directory-etc-designs}

/etc/designs目录包含要与页面内容一起下载的图像、脚本和样式表。

1. 要在经典UI中使用设计器工具，请浏览 [https://&lt;server>：&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   注：如果使用CRXDE Lite创建类型为的节点 `cq:Page`，则不会将页面的访问控制和复制设置为默认设置。

1. 在资源管理器窗格中，选择 **[!UICONTROL 设计]** 文件夹，然后单击 **[!UICONTROL 新建]** > **[!UICONTROL 新建页面]**.

   输入：

   * 标题： **[!UICONTROL SCF沙盒]**
   * 名称： **[!UICONTROL an-scf-sandbox]**
   * 选择 **[!UICONTROL 设计页面模板]**

   单击&#x200B;**[!UICONTROL 创建]**。

   ![design-template](assets/design-template.png)

1. 如果未显示“SCF沙盒”文件夹，请刷新资源管理器窗格。

1. 返回CRXDE Lite(http:// localhost：4502/crx/de)并展开/etc/designs以查看名为“an-scf-sandbox”的节点。

   在CRXDE的右下窗格中，您可以查看“属性”选项卡、“访问控制”选项卡和“复制”选项卡，以查看使用“设计页模板”定义的内容。

   ![crxde-configure-template](assets/crxde-configure-template.png)

## 设置内容目录(/content) {#setup-the-content-directory-content}

存储库中的/content目录是网站内容所在的位置。 /content下的路径包含浏览器请求的URL的路径。

*之后* 该 [页面模板](initial-app.md#createthepagetemplate) 创建作为初始应用程序的一部分，可以根据模板创建初始页面内容.... [**⇒**](initial-app.md)
