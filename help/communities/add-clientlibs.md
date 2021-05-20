---
title: 添加Clientlibs
seo-title: 添加Clientlibs
description: 添加ClientLibraryFolder
seo-description: 添加ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 添加Clientlibs {#add-clientlibs}

## 添加ClientLibraryFolder(clientlibs){#add-a-clientlibraryfolder-clientlibs}

创建名为`clientlibs`的ClientLibraryFolder，其中将包含用于呈现网站页面的JS和CSS。

给此客户端库的`categories`属性值是用于从内容页面直接包含此clientlib或将其嵌入到其他clientlib的标识符。

1. 使用&#x200B;**CRXDE Lite**，展开`/etc/designs`

1. 右键单击`an-scf-sandbox`并选择`Create Node`

   * 名称 : `clientlibs`
   * 类型 : `cq:ClientLibraryFolder`

1. 单击&#x200B;**确定**

![add-client-library](assets/add-client-library.png)

在新`clientlibs`节点的&#x200B;**属性**&#x200B;选项卡中，输入&#x200B;**类别**&#x200B;属性：

* 名称：**类别**
* 类型：**字符串**
* 值：**apps.anscf-sandbox**
* 单击&#x200B;**Add**
* 单击&#x200B;**Save All**

注意：使用“apps”为类别值添加前缀。 是将“拥有的应用程序”标识为位于/apps文件夹中，而不是/libs中的约定。  重要信息：添加占位符`js.tx`t和&#x200B;**`css.txt`**&#x200B;文件。 （没有cq:ClientLibraryFolder，它不是正式的。）

1. 右键单击&#x200B;**`/etc/designs/an-scf-sandbox/clientlibs`**
1. 选择&#x200B;**创建文件……**
1. 输入&#x200B;**名称：** `css.txt`
1. 选择&#x200B;**创建文件……**
1. 输入&#x200B;**名称：** `js.txt`
1. 单击&#x200B;**Save All**

![clientlibs-css](assets/clientlibs-css.png)

css.txt和js.txt的第一行用于标识可从中找到以下文件列表的基本位置。

尝试将css.txt的内容设置为

```
#base=.
 style.css
```

然后，在名为style.css的clientlibs下创建文件，并将内容设置为

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF Clientlibs {#embed-scf-clientlibs}

在&#x200B;**Properties**&#x200B;选项卡的`clientlibs`节点中，输入多值String属性&#x200B;**embed**。 这为SCF组件](/help/communities/client-customize.md#clientlibs-for-scf)嵌入了必需的[客户端库(clientlibs)。 在本教程中，添加了社区组件所需的许多clientlib。

**** 请注意，这可能是生产站点所需的方法，也可能不是，因为考虑到了方便性与为每个页面下载的clientlib的大小/速度。

如果在一个页面上仅使用一项功能，则可以直接在页面上包含该功能的完整clientlib，例如

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在本例中，包括所有这些SCF客户端，因此更基本的SCF客户端库是作者的客户端库：

* 名称 : **`embed`**
* 类型 : **`String`**
* 单击 **`Multi`**
* 值: **`cq.social.scf`**

   * 会弹出一个对话框，
单击每个条目后的**`+`**&#x200B;以添加以下clientlib类别：

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 单击&#x200B;**确定**

* 单击&#x200B;**Save All**

![scf-clientlibs](assets/scf-clientlibs.png)

下面显示了`/etc/designs/an-scf-sandbox/clientlibs`在存储库中的显示方式：

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### 在PlayPage模板{#include-clientlibs-in-playpage-template}中包含Clientlib

如果页面上没有`apps.an-scf-sandbox` ClientLibraryFolder类别，则SCF组件将无法正常工作，也无法按照必需的Javascript设置样式，并且样式将不可用。

例如，如果不包含clientlibs，则SCF注释组件将显示为未设置样式：

![clientlibs-comment](assets/clientlibs-comment.png)

在包含apps.an-scf-sandbox clientlibs后，SCF评论组件会显示样式：

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include语句属于`html`脚本的`head`部分。 默认的&#x200B;**`foundation head.jsp`**&#x200B;包含可覆盖的脚本：**`headlibs.jsp`**。

**复制headlibs.jsp并包含clientlibs:**

1. 使用&#x200B;**CRXDE Lite**，选择&#x200B;**`/libs/foundation/components/page/headlibs.jsp`**

1. 右键单击并选择&#x200B;**Copy**（或从工具栏中选择Copy）
1. 选择 **`/apps/an-scf-sandbox/components/playpage`**
1. 右键单击并选择&#x200B;**粘贴**（或从工具栏中选择粘贴）
1. 双击&#x200B;**`headlibs.jsp`**&#x200B;将其打开
1. 在文件末尾附加以下行
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 单击&#x200B;**Save All**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

在浏览器中加载您的网站，并查看背景是否不是蓝色阴影。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![社区游戏](assets/community-play.png)

### 到目前为止正在保存您的工作{#saving-your-work-so-far}

此时，存在一个极简主义的沙箱，可能值得将其另存为包，这样在播放时，如果您的存储库已损坏并且您希望重新开始，您就可以关闭服务器、重命名或删除文件夹crx-quickstart/、打开服务器、上载并安装此保存的包，并且不必重复这些最基本的步骤。

[创建示例页面](/help/communities/create-sample-page.md)教程中存在此包，教程针对的是那些迫不及待地想要跳入并开始播放的用户……

要创建资源包，请执行以下操作：

* 在CRXDE Lite中，单击[包图标](https://localhost:4502/crx/packmgr/)
* 单击&#x200B;**创建包**

   * 包名称：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 组: `leave as default`
   * 单击&#x200B;**确定**

* 单击&#x200B;**编辑**

   * 选择&#x200B;**Filters**&#x200B;选项卡

      * 单击&#x200B;**Add filter**
      * 根路径：浏览`/apps/an-scf-sandbox`
      * 单击&#x200B;**Done**
      * 单击&#x200B;**Add filter**
      * 根路径：浏览`/etc/designs/an-scf-sandbox`
      * 单击&#x200B;**Done**
      * 单击&#x200B;**Add filter**
      * 根路径：浏览`/content/an-scf-sandbox**`
      * 单击&#x200B;**Done**
   * 单击&#x200B;**Save**


* 单击&#x200B;**Build**

现在，您可以选择&#x200B;**Download**&#x200B;将其保存到磁盘，然后选择其他位置的&#x200B;**Upload Package**，还可以选择&#x200B;**More > Replicate**，以将沙盒推送到本地主机发布实例以扩展沙盒的领域。
