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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 添加Clientlibs{#add-clientlibs}

## 添加ClientLibraryFolder(clientlibs) {#add-a-clientlibraryfolder-clientlibs}

创建一个名为的ClientLibraryFolder, `clientlibs`其中将包含用于呈现站点页面的JS和CSS。

赋予 `categories`此客户端库的属性值是用于从内容页面直接包含此clientlib或将其嵌入到其他clientlib的标识符。

1. 使用 **CRXDE Lite**，展开 `/etc/designs`

1. 右键单击 `an-scf-sandbox` 并选择 `Create Node`

   * 名称 : `clientlibs`
   * 类型 : `cq:ClientLibraryFolder`

1. click **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

在新节 **点的** “属性”选 `clientlibs` 项卡中，输入**`categories`**属性：

* 名称：类 **别**
* 类型：字 **符串**
* 值：apps. **an-scf-sandbox**
* click **Add**
* 单击“ **全部保存”**

注意：使用“apps”为类别值预设。 是将“拥有的应用程序”标识为位于/apps文件夹（而非/libs）中的约定。  重要：添加占 `js.tx`位符t和**`css.tx`**t文件。 （没有cq:ClientLibraryFolder，它不是正式的cq:ClientLibraryFolder。）

1. 右键单击 **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 选择 **创建文件……**
1. **输入**&#x200B;名称： `css.txt`
1. 选择 **创建文件……**
1. **输入**&#x200B;名称： `js.txt`
1. 单击“ **全部保存”**

![chlimage_1-48](assets/chlimage_1-48.png)

css.txt和js.txt的第一行标识了从中找到以下文件列表的基本位置。

尝试将css.txt的内容设置为

```
#base=.
 style.css
```

然后，在clientlibs下创建一个名为style.css的文件，并将内容设置为

`body {`

`background-color: #b0c4de;`

`}`

### 嵌入SCF Clientlib {#embed-scf-clientlibs}

在节 **点的** “属性”选 `clientlibs` 项卡中，输入多值“字符串”属 **性embed**。 这为SCF组件 [嵌入了必需的客户端库(clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf)。 在本教程中，添加了“社区”组件所需的许多客户端库。

**请注意** ，这可能是生产站点所使用的方法，也可能不是所需的方法，因为每页下载的clientlib的方便性与大小／速度有所不同。

如果仅在一个页面上使用一个功能，则可以直接在页面上包含该功能的完整clientlib，例如&lt;% ui:includeClientLib类别=cq.social.hbs.forum&quot; %>

在这种情况下，包括所有的SCF客户端，因此更基本的SCF客户端是作者的客户端：

* 名称 : **`embed`**
* 类型 : **`String`**
* 单击 **`Multi`**
* 值： **`cq.social.scf`***&lt;enter>将在每个条目后弹出一个对话框单击**[+] *,*以添加以下clientlib类别：*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * click **OK**

* 单击“ **全部保存”**

![chlimage_1-49](assets/chlimage_1-49.png)

这是现在应 `/etc/designs/an-scf-sandbox/clientlibs` 该如何显示在存储库中的方式：

![chlimage_1-50](assets/chlimage_1-50.png)

### 在PlayPage模板中包含Clientlibs {#include-clientlibs-in-playpage-template}

如果页面 `apps.an-scf-sandbox` 中不包括ClientLibraryFolder类别，则SCF组件将无法正常工作，也无法设置样式，因为必需的Javascript和样式将不可用。

例如，在不包括clientlibs的情况下，SCF注释组件显示为未设置样式：

![chlimage_1-51](assets/chlimage_1-51.png)

包括apps.an-scf-sandbox clientlibs后，SCF注释组件将显示样式：

![chlimage_1-52](assets/chlimage_1-52.png)

包含语句属于 <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 部分 <html> 脚本. 默认包 **`foundation head.jsp`** 括可覆盖的脚本： **`headlibs.jsp`**.

**复制headlibs.jsp并包含clientlibs:**

1. 使用 **CRXDE Lite**，选择 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右键单击并选择**复制**（或从工具栏中选择复制）
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. 右键单击并选择**粘贴**（或从工具栏中选择粘贴）
1. 双击 **`headlibs.jsp`** 以打开它
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

在浏览器中加载您的网站，并查看背景是否不是蓝色阴影。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![chlimage_1-53](assets/chlimage_1-53.png)

### 到目前为止，保存您的作品 {#saving-your-work-so-far}

此时，存在极简的沙箱，可能值得保存为包，这样，在播放时，如果您的存储库损坏并且希望重新开始，您可以关闭服务器，重命名或删除文件夹crx-quickstart/，打开服务器，上传并安装此保存的包，无需重复这些最基本的步骤。

此包位于“创 [建示例页面](/help/communities/create-sample-page.md) ”教程中，面向迫不及待地跳入并开始播放的用户……

要创建包，请执行以下操作：

* 从CRXDE lite中，单击“包” [图标](https://localhost:4502/crx/packmgr/)
* 单击“ **创建包”**

   * 包名称：an-scf-sandbox-minimal-pkg
   * 版本：0.1
   * 组：&lt;leave as default>
   * click **OK**

* click **Edit**

   * 选择**过滤器**选项卡

      * 单击“ **添加过滤器”**
      * 根路径：&lt;浏览至** /apps/an-scf-sandbox**>
      * click **Done**
      * 单击“ **添加过滤器”**
      * 根路径：&lt;浏览到 **/etc/designs/an-scf-sandbox**>
      * click **Done**
      * 单击“ **添加过滤器”**
      * 根路径：&lt;浏览到 **/content/an-scf-sandbox**>
      * click **Done**
   * click **Save**


* 单击“构 **建”**

现在，您可以选 **择** Download（下载）将其保存到磁盘并将其上载到其他位置的Package **（上载包），还可以选择More（更多）> Replicate****** （复制），以将沙箱推送到本地主机发布实例以扩展沙箱领域。