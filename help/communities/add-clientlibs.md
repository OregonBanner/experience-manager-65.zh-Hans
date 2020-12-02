---
title: 添加客户端库
seo-title: 添加客户端库
description: 添加ClientLibraryFolder
seo-description: 添加ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---


# 添加Clientlibs {#add-clientlibs}

## 添加ClientLibraryFolder(clientlibs){#add-a-clientlibraryfolder-clientlibs}

创建名为`clientlibs`的ClientLibraryFolder，其中将包含用于呈现站点页面的JS和CSS。

赋予此客户端库的`categories`属性值是用于从内容页面直接包含此clientlib或将其嵌入到其他clientlib的标识符。

1. 使用&#x200B;**CRXDE Lite**&#x200B;展开`/etc/designs`

1. 右键单击`an-scf-sandbox`并选择`Create Node`

   * 名称 : `clientlibs`
   * 类型 : `cq:ClientLibraryFolder`

1. 单击&#x200B;**确定**

![add-client-library](assets/add-client-library.png)

在新`clientlibs`节点的&#x200B;**属性**&#x200B;选项卡中，输入&#x200B;**类别**&#x200B;属性：

* 名称：**类别**
* 类型：**字符串**
* 值：**apps.an scf-sandbox**
* 单击&#x200B;**添加**
* 单击&#x200B;**保存全部**

注意：用“apps”预先呈现类别价值。 是用于将“拥有的应用程序”标识为位于/apps文件夹（而非/libs）中的约定。  重要：添加占位符`js.tx`t和&#x200B;**`css.txt`**&#x200B;文件。 （没有它们，它不是正式的cq:ClientLibraryFolder。）

1. 右键单击&#x200B;**`/etc/designs/an-scf-sandbox/clientlibs`**
1. 选择&#x200B;**创建文件……**
1. 输入&#x200B;**名称：** `css.txt`
1. 选择&#x200B;**创建文件……**
1. 输入&#x200B;**名称：** `js.txt`
1. 单击&#x200B;**保存全部**

![clientlibs-css](assets/clientlibs-css.png)

css.txt和js.txt的第一行标识了从中找到以下一列表文件的基本位置。

尝试将css.txt的内容设置为

```
#base=.
 style.css
```

然后在名为style.css的clientlibs下创建一个文件，并将内容设置为

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF客户端库{#embed-scf-clientlibs}

在`clientlibs`节点的&#x200B;**属性**&#x200B;选项卡中，输入多值字符串属性&#x200B;**embed**。 这为SCF组件](/help/communities/client-customize.md#clientlibs-for-scf)嵌入必需的[客户端库(clientlibs)。 在本教程中，将添加社区组件所需的许多客户端库。

**请注** 意，这可能是生产站点所需的方法，也可能不是，因为每个页面下载的客户端库的方便性与大小／速度之间存在着差异。

如果仅在一个页面上使用一个功能，则可以直接在页面上包含该功能的完整clientlib，例如，

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在这种情况下，将它们全部包括在内，因此更基本的SCF客户端是作者的客户端：

* 名称 : **`embed`**
* 类型 : **`String`**
* 单击 **`Multi`**
* 值: **`cq.social.scf`**

   * 它会弹出一个对话，
单击每个条目后的**`+`**&#x200B;以添加以下clientlib类别:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 单击&#x200B;**确定**

* 单击&#x200B;**保存全部**

![scf-clientlibs](assets/scf-clientlibs.png)

这是`/etc/designs/an-scf-sandbox/clientlibs`现在在存储库中的显示方式：

![scf-clientlibs-视图](assets/scf-clientlibs1.png)

### 在PlayPage模板{#include-clientlibs-in-playpage-template}中包含Clientlibs

如果页面中不包含`apps.an-scf-sandbox` ClientLibraryFolder类别，则SCF组件将无法正常工作，也无法设置样式，因为必需的Javascript和样式将不可用。

例如，如果不包括clientlib，则SCF注释组件将显示为未设置样式：

![clientlibs-comment](assets/clientlibs-comment.png)

在包含apps.an-scf-sandbox clientlibs后，SCF注释组件将显示样式：

![clientlibs-comment-steled](assets/clientlibs-comment1.png)

include语句属于`html`脚本的`head`部分。 默认&#x200B;**`foundation head.jsp`**&#x200B;包含可以覆盖的脚本：**`headlibs.jsp`**。

**复制headlibs.jsp并包含clientlibs:**

1. 使用&#x200B;**CRXDE Lite**，选择&#x200B;**`/libs/foundation/components/page/headlibs.jsp`**

1. 右键单击并选择&#x200B;**复制**（或从工具栏中选择复制）
1. 选择 **`/apps/an-scf-sandbox/components/playpage`**
1. 右键单击并选择&#x200B;**粘贴**（或从工具栏中选择粘贴）
1. 多次-单击&#x200B;**`headlibs.jsp`**&#x200B;以打开它
1. 在文件末尾附加以下行
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 单击&#x200B;**保存全部**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

在浏览器中加载您的网站并查看背景是否不是蓝色阴影。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![社区播放](assets/community-play.png)

### 保存您的工作到{#saving-your-work-so-far}

此时，存在极简的沙箱，可能值得保存为包，这样，在播放时，如果存储库损坏并想要开始，您可以关闭服务器，重命名或删除文件夹crx-quickstart/，打开服务器，上传并安装此保存的包，无需重复这些最基本的步骤。

此包存在于[为迫不及待地跳入和开始播放的用户创建示例页面](/help/communities/create-sample-page.md)教程中……

要创建包，请执行以下操作：

* 从CRXDE Lite单击[包图标](https://localhost:4502/crx/packmgr/)
* 单击&#x200B;**创建包**

   * 包名称：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 组: `leave as default`
   * 单击&#x200B;**确定**

* 单击&#x200B;**编辑**

   * 选择&#x200B;**过滤器**&#x200B;选项卡

      * 单击&#x200B;**添加过滤器**
      * 根路径：浏览至`/apps/an-scf-sandbox`
      * 单击&#x200B;**完成**
      * 单击&#x200B;**添加过滤器**
      * 根路径：浏览至`/etc/designs/an-scf-sandbox`
      * 单击&#x200B;**完成**
      * 单击&#x200B;**添加过滤器**
      * 根路径：浏览至`/content/an-scf-sandbox**`
      * 单击&#x200B;**完成**
   * 单击&#x200B;**保存**


* 单击&#x200B;**Build**

现在，您可以选择&#x200B;**下载**&#x200B;将其保存到磁盘并在其他位置选择&#x200B;**上传包**，还可以选择&#x200B;**更多>复制**，以便将沙箱推送到本地主机发布实例以扩展沙箱领域。