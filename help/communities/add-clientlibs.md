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
source-git-commit: 2b1cc29fbfdb80aff6b6fc5c6c4fc9093d12e418
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---


# 添加客户端库 {#add-clientlibs}

## 添加ClientLibraryFolder(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

创建一个名 `clientlibs`为ClientLibraryFolder，其中将包含用于呈现站点页面的JS和CSS。

赋予 `categories`此客户端库的属性值是用于从内容页面直接包含此clientlib或将其嵌入到其他clientlib的标识符。

1. 使用 **CRXDE Lite**，展开 `/etc/designs`

1. 右键单击并 `an-scf-sandbox` 选择 `Create Node`

   * 名称 : `clientlibs`
   * 类型 : `cq:ClientLibraryFolder`

1. Click **OK**

![chlimage_1-220](assets/chlimage_1-220.png)

在新节 **点的** “属性”选 `clientlibs` 项卡中，输入 **类别属性** :

* 名称： **类别**
* 类型： **字符串**
* 值： **apps.an-scf-sandbox**
* Click **Add**
* 单击“ **全部保存”**

注意： 用“apps”预先呈现类别价值。 是用于将“拥有的应用程序”标识为位于/apps文件夹（而非/libs）中的约定。  重要： 添加占 `js.tx`位符t **`css.txt`** 和文件。 （没有它们，它不是正式的cq:ClientLibraryFolder。）

1. 右键单击 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 选择 **创建文件……**
1. Enter **Name:** `css.txt`
1. 选择 **创建文件……**
1. Enter **Name:** `js.txt`
1. 单击“ **全部保存”**

![chlimage_1-221](assets/chlimage_1-221.png)

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

### 嵌入SCF客户端库 {#embed-scf-clientlibs}

在节 **点的** “属性” `clientlibs` 选项卡中，输入多值“字符串”属 **性嵌入**。 这为SCF组 [件嵌入了必要的客户端库(clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf)。 在本教程中，将添加社区组件所需的许多客户端库。

**请注意** ，这可能是生产站点所需的方法，也可能不是，因为每个页面下载的客户端库的方便性与大小／速度之间存在着一定的关系。

如果仅在一个页面上使用一个功能，则可以直接在页面上包含该功能的完整clientlib，例如，

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在这种情况下，将它们全部包括在内，因此更基本的SCF客户端是作者的客户端：

* 名称 : **`embed`**
* 类型 : **`String`**
* 单击 **`Multi`**
* 值: **`cq.social.scf`**

   * 它将弹出一个对话框，在每个条目后 **`+`** 单击以添加以下clientlib类别:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Click **OK**

* 单击“ **全部保存”**

![chlimage_1-222](assets/chlimage_1-222.png)

这是现在 `/etc/designs/an-scf-sandbox/clientlibs` 在存储库中的显示方式：

![chlimage_1-223](assets/chlimage_1-223.png)

### 在PlayPage模板中包含客户端库 {#include-clientlibs-in-playpage-template}

如果页面 `apps.an-scf-sandbox` 中不包含ClientLibraryFolder类别，则SCF组件将不能正常工作，也无法设置样式，因为必需的Javascript和样式将不可用。

例如，如果不包括clientlib，则SCF注释组件将显示为未设置样式：

![chlimage_1-224](assets/chlimage_1-224.png)

在包含apps.an-scf-sandbox clientlibs后，SCF注释组件将显示样式：

![chlimage_1-225](assets/chlimage_1-225.png)

include语句属于脚 `head` 本的一 `html` 节。 默认包 **`foundation head.jsp`** 括可以叠加的脚本： **`headlibs.jsp`**.

**复制headlibs.jsp并包含clientlibs:**

1. 使用 **CRXDE Lite**，选择 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右键单击并选择 **复制** （或从工具栏中选择复制）
1. 选择 **`/apps/an-scf-sandbox/components/playpage`**
1. 右键单击并选择粘 **贴** （或从工具栏中选择粘贴）
1. 多次单 **`headlibs.jsp`** 击以打开它
1. 在文件末尾附加以下行
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 单击“ **全部保存”**

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

![chlimage_1-226](assets/chlimage_1-226.png)

### 到目前为止，保存您的作品 {#saving-your-work-so-far}

此时，存在极简的沙箱，可能值得保存为包，这样，在播放时，如果存储库损坏并想要开始，您可以关闭服务器，重命名或删除文件夹crx-quickstart/，打开服务器，上传并安装此保存的包，无需重复这些最基本的步骤。

此包存在于为 [那些迫不及待地跳入并开始正在播放](/help/communities/create-sample-page.md) 的用户创建示例页面教程中……

要创建包，请执行以下操作：

* 从CRXDE Lite中，单击“包” [图标](https://localhost:4502/crx/packmgr/)
* 单击“ **创建包”**

   * 包名称： an-scf-sandbox-minimal-pkg
   * 版本： 0.1
   * 组: `leave as default`
   * Click **OK**

* Click **Edit**

   * 选择 **过滤器** 选项卡

      * 单击“ **添加过滤器”**
      * 根路径： 浏览至 `/apps/an-scf-sandbox`
      * Click **Done**
      * 单击“ **添加过滤器”**
      * 根路径： 浏览至 `/etc/designs/an-scf-sandbox`
      * Click **Done**
      * 单击“ **添加过滤器”**
      * 根路径： 浏览至 `/content/an-scf-sandbox**`
      * Click **Done**
   * Click **Save**


* 单击“ **生成”**

现在，您可以选 **择** “下载”将其保存到磁盘并在其他位置 **上传包** ，还可以选择“更多”>“复制 **** ”，以将沙箱推送到localhost发布实例以扩展沙箱领域。