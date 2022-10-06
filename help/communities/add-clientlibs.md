---
title: 添加Clientlibs
seo-title: Add Clientlibs
description: 添加ClientLibraryFolder
seo-description: Add a ClientLibraryFolder
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
source-wordcount: '682'
ht-degree: 1%

---

# 添加Clientlibs {#add-clientlibs}

## 添加ClientLibraryFolder(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

创建名为的ClientLibraryFolder `clientlibs` 其中将包含用于呈现网站页面的JS和CSS。

的 `categories` 给予此客户端库的属性值是用于从内容页面直接包含此clientlib或将其嵌入到其他clientlib的标识符。

1. 使用 **CRXDE Lite**，展开 `/etc/designs`

1. 右键单击 `an-scf-sandbox` 选择 `Create Node`

   * 名称 : `clientlibs`
   * 类型 : `cq:ClientLibraryFolder`

1. 单击 **确定**

![add-client-library](assets/add-client-library.png)

在 **属性** 选项卡 `clientlibs` 节点，输入 **类别** 属性：

* 名称： **类别**
* 类型： **字符串**
* 值： **apps.an-scf-sandbox**
* 单击 **添加**
* 单击 **全部保存**

注意：使用“apps”为类别值添加前缀。 是将“拥有的应用程序”标识为位于/apps文件夹中，而不是/libs中的约定。  重要信息：添加占位符 `js.tx`t和 **`css.txt`** 文件。 （没有cq:ClientLibraryFolder，它不是正式的。）

1. 右键单击 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 选择 **创建文件……**
1. 输入 **名称：** `css.txt`
1. 选择 **创建文件……**
1. 输入 **名称：** `js.txt`
1. 单击 **全部保存**

![clientlibs-css](assets/clientlibs-css.png)

css.txt和js.txt的第一行标识可从中找到以下文件列表的基本位置。

尝试将css.txt的内容设置为

```
#base=.
 style.css
```

然后，在名为style.css的clientlibs下创建文件，并将内容设置为

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF Clientlib {#embed-scf-clientlibs}

在 **属性** 选项卡 `clientlibs` 节点，输入多值字符串属性 **嵌入**. 这嵌入了必要的 [用于SCF组件的客户端库(clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf). 在本教程中，添加了社区组件所需的许多clientlib。

**注意** 这可能是生产站点使用的所需方法，也可能不是，因为考虑到了方便性与为每个页面下载的clientlib的大小/速度。

如果在一个页面上仅使用一项功能，则可以直接在页面上包含该功能的完整clientlib，例如

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

在本例中，包括所有这些SCF客户端，因此更基本的SCF客户端库是作者的客户端库：

* 名称 : **`embed`**
* 类型 : **`String`**
* 单击 **`Multi`**
* 值: **`cq.social.scf`**

   * 此时将弹出一个对话框，单击 **`+`** 在每个条目之后添加以下clientlib类别：

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 单击 **确定**

* 单击 **全部保存**

![scf-clientlibs](assets/scf-clientlibs.png)

这就是方法 `/etc/designs/an-scf-sandbox/clientlibs` 此时应会显示在存储库中：

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### 在PlayPage模板中包含Clientlib {#include-clientlibs-in-playpage-template}

不包含 `apps.an-scf-sandbox` ClientLibraryFolder类别中，SCF组件将无法正常工作，也不会按照必需的Javascript设置样式，并且样式将不可用。

例如，如果不包含clientlibs，则SCF注释组件将显示为未设置样式：

![clientlibs-comment](assets/clientlibs-comment.png)

在包含apps.an-scf-sandbox clientlibs后，SCF评论组件会显示样式：

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include语句属于 `head` 部分 `html` 脚本。 默认 **`foundation head.jsp`** 包含可以覆盖的脚本： **`headlibs.jsp`**.

**复制headlibs.jsp并包含clientlibs:**

1. 使用 **CRXDE Lite**，选择 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右键单击并选择 **复制** （或从工具栏中选择复制）
1. 选择 **`/apps/an-scf-sandbox/components/playpage`**
1. 右键单击并选择 **粘贴** （或从工具栏中选择粘贴）
1. 双击 **`headlibs.jsp`** 打开
1. 在文件末尾附加以下行
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 单击 **全部保存**

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

### 省下你的工作 {#saving-your-work-so-far}

此时，存在一个极简主义的沙箱，可能值得将其另存为包，这样在播放时，如果您的存储库已损坏并且您希望重新开始，您就可以关闭服务器、重命名或删除文件夹crx-quickstart/、打开服务器、上载并安装此保存的包，并且不必重复这些最基本的步骤。

此包存在于 [创建示例页面](/help/communities/create-sample-page.md) 教那些迫不及待地跳进来开始玩的人……

要创建资源包，请执行以下操作：

* 从CRXDE Lite，单击 [包图标](https://localhost:4502/crx/packmgr/)
* 单击 **创建资源包**

   * 包名称：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 组: `leave as default`
   * 单击 **确定**

* 单击 **编辑**

   * 选择 **过滤器** 选项卡

      * 单击 **添加过滤器**
      * 根路径：浏览 `/apps/an-scf-sandbox`
      * 单击 **完成**
      * 单击 **添加过滤器**
      * 根路径：浏览 `/etc/designs/an-scf-sandbox`
      * 单击 **完成**
      * 单击 **添加过滤器**
      * 根路径：浏览 `/content/an-scf-sandbox**`
      * 单击 **完成**
   * 单击 **保存**


* 单击 **生成**

现在，您可以选择 **下载** 将其保存到磁盘， **上传包** ，以及选择 **更多>复制** 要将沙盒推送到localhost发布实例，以扩展沙盒的领域。
