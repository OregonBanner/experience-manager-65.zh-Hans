---
title: 创建功能全面的网站(JSP)
description: 通过本教程，您可以使用AEM创建一个功能齐全的网站
uuid: ec76ad5e-af6c-43ad-ae57-a4ae4ac7029f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 90bc05c9-e971-4e75-bc07-5e137c6c913e
docset: aem65
exl-id: d7cf843c-c837-4b97-b6c5-0fbd6793bdd4
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '4935'
ht-degree: 2%

---

# 创建功能全面的网站(JSP){#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>本文介绍了如何使用JSP并基于经典UI创建网站。 Adobe建议为您的网站使用最新的AEM技术，如文章中详细介绍 [AEM Sites开发入门](/help/sites-developing/getting-started.md).

通过本教程，您可以使用Adobe Experience Manager (AEM)创建一个功能齐全的网站。 该网站将基于通用网站，主要面向Web开发人员。 所有开发都在创作环境中进行。

本教程介绍如何：

1. 安装AEM。
1. 访问CRXDE Lite（开发环境）。
1. 在CRXDE Lite中设置项目结构。
1. 创建模板、组件和脚本，用作创建内容页面的基础。
1. 创建网站的根页面，然后创建内容页面。
1. 创建以下组件以在页面上使用：

   * 顶部导航
   * 列出子项
   * 徽标
   * 图像
   * 文本图像
   * 搜索

1. 包括各种基础组件。

执行完所有步骤后，页面将如下所示：

![chlimage_1-24](assets/chlimage_1-24.png)

**下载最终结果**

要随附教程而不是执行练习，请下载website-1.0.zip。 此文件是一个AEM内容包，其中包含本教程的结果。 使用 [包管理器](/help/sites-administering/package-manager.md) 以将包安装到创作实例。

**注意：** 安装此包将覆盖您使用本教程创建的创作实例上的任何资源。

网站内容包

[获取文件](assets/website-1_0.zip)

## 安装Adobe Experience Manager {#installing-adobe-experience-manager}

要安装用于开发网站的AEM实例，请按照设置 [具有创作和发布实例的部署环境](/help/sites-deploying/deploy.md#author-and-publish-installs)，或执行 [通用安装](/help/sites-deploying/deploy.md#default-local-install). 通用安装包括下载AEM快速入门JAR文件，将license.properties文件放在与JAR文件相同的目录中，然后双击JAR文件。

安装AEM后，单击“欢迎”页面上的CRXDE Lite链接以访问CRXDE Lite开发环境：

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>使用默认CRXDE Lite本地安装的AEM创作实例的URL为 [https://localhost:4502/crx/de/](https://localhost:4502/crx/de/).

### 在CRXDE Lite中设置项目结构 {#setting-up-the-project-structure-in-crxde-lite}

使用CRXDE Lite在存储库中创建mywebsite应用程序结构：

1. 在CRXDE Lite左侧的树中，右键单击 **`/apps`** 文件夹并单击 **创建** > **创建** **文件夹**. 在 **创建文件夹** 对话框，键入 `mywebsite` 作为文件夹名称，然后单击 **确定**.
1. 右键单击 **`/apps/mywebsite`** 文件夹并单击 **创建** > **创建文件夹**. 在 **创建文件夹** 对话框，键入 `components` 作为文件夹名称，然后单击 **确定**.
1. 右键单击 **`/apps/mywebsite`** 文件夹并单击 **创建** > **创建文件夹**. 在 **创建文件夹** 对话框，键入 `templates` 作为文件夹名称，然后单击 **确定**.

   树中的结构现在应如下所示：

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 单击 **全部保存**.

### 设置设计 {#setting-up-the-design}

在本节中，您将使用Designer工具为应用程序创建设计。 该设计为您的网站提供CSS和图像资源。

>[!NOTE]
>
>单击以下链接下载mywebsite.zip。 存档包含用于您设计的static.css和图像文件。

示例static.css文件和图像

[获取文件](assets/mywebsite.zip)

1. 在AEM欢迎页面上，单击 **工具**. ([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. 在文件夹树中，选择 **设计** 文件夹，然后单击 **新** > **新页面**. 类型 `mywebsite` 作为标题，然后单击 **创建**.

1. 如果mywebsite项目未出现在表中，请刷新树或表。

1. [使用WebDAV](/help/sites-administering/webdav-access.md) 访问https://localhost:4502上的URL，复制示例 `static.css` 文件和 `images` 文件夹从下载的mywebsite.zip文件移至 `/etc/designs/mywebsite` 文件夹。

   ![chlimage_1-28](assets/chlimage_1-28.png)

### 创建Contentpage模板、组件和脚本 {#creating-the-contentpage-template-component-and-script}

在此部分中，您将创建以下内容：

* 用于在示例网站中创建内容页面的内容页面模板
* 将用于呈现内容页面的contentpage组件
* contentpage脚本

#### 创建内容页模板 {#creating-the-contentpage-template}

创建模板以用作网站网页的基础。

模板定义新页面的默认内容。 复杂的网站可能使用多个模板在站点中创建不同类型的页面。 在本练习中，所有页面都基于一个简单的模板。

1. 在CRXDE Lite的文件夹树中，右键单击 `/apps/mywebsite/templates` 并单击 **创建** > **创建模板**.

1. 在创建模板对话框中，键入以下值，然后单击 **下一个**：

   * **标签**：contentpage
   * **标题**：我的网站内容页面模板
   * **描述**：这是我的网站内容页面模板
   * **资源类型：** mywebsite/components/contentpage

   使用Ranking属性的默认值。

   ![chlimage_1-29](assets/chlimage_1-29.png)

   资源类型标识呈现页面的组件。 在本例中，使用contentpage模板创建的所有页面都由 `mywebsite/components/contentpage` 组件。

1. 要指定可以使用此模板的页面的路径，请单击加号按钮并键入 `/content(/.*)?` 在显示的文本框中。 然后，单击 **下一个**.

   ![chlimage_1-30](assets/chlimage_1-30.png)

   允许的路径属性的值为 *正则表达式。* 路径与表达式匹配的页面可以使用模板。 在这种情况下，正则表达式将匹配 **/content** 文件夹和所有子页面。

   当作者在/content下创建页面时， **contentpage** 模板会显示在要使用的可用模板的列表中。

1. 单击 **下一个** 在 **允许的父项** 和 **允许的子项** 面板并单击 **确定**. 在CRXDE Lite中，单击 **全部保存**.

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### 创建Contentpage组件 {#creating-the-contentpage-component}

创建 *组件* 定义内容并渲染使用内容页面模板的页面。 组件的位置必须与contentpage模板的Resource Type属性的值相对应。

1. 在CRXDE Lite中，右键单击 `/apps/mywebsite/components` 并单击 **创建** > **组件**.
1. 在 **创建组件** 对话框中，键入以下属性值：

   * **标签**：contentpage
   * **标题**：我的网站内容页面组件
   * **描述**：这是我的网站内容页面组件

   ![chlimage_1-32](assets/chlimage_1-32.png)

   新组件的位置为 `/apps/mywebsite/components/contentpage`. 此路径对应于内容页模板的资源类型（减去初始值） **`/apps/`** 路径的一部分)。

   此通信会将模板连接到组件，并且对于网站的正确运行至关重要。

1. 单击 **下一个** 直到对话框的允许的子项面板出现，然后单击 **确定**. 在CRXDE Lite中，单击 **全部保存**.

   现在的结构如下所示：

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### 开发Contentpage组件脚本 {#developing-the-contentpage-component-script}

将代码添加到contentpage.jsp脚本以定义页面内容。

1. 在CRXDE Lite中，打开文件 `contentpage.jsp` 在 `/apps/mywebsite/components/contentpage`. 默认情况下，文件包含以下代码：

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. 复制以下代码并将其粘贴到contentpage.jsp中的默认代码之后：

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. 单击 **全部保存** 以保存更改。

### 创建网站页面和内容页面 {#creating-your-website-page-and-content-pages}

在此部分中，您将创建以下所有使用内容页面模板的页面：“我的网站”、“英语”、“产品”、“服务”和“客户”。

1. 在AEM欢迎页面上([https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html))，然后单击网站。

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. 在文件夹树中，选择 **网站** 文件夹，然后单击 **新** > **新页面**.
1. 在 **创建页面** 窗口中，输入以下内容：

   * 标题: `My Website`
   * 名称: `mywebsite`
   * 选择 `My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. 单击&#x200B;**创建**。在文件夹树中，选择 **/Websites/My网站** 页面并单击 **新** > **新页面**.
1. 在“创建页”对话框中，输入以下属性值，然后单击“创建”：

   * 标题：英语
   * 名称：en
   * 选择“我的网站内容”页面模板

1. 在文件夹树中，选择 **/Websites/My网站/英语** 页面并单击 **新**> **新页面**.
1. 在 **创建页面** 对话框，输入以下属性值，然后单击 **创建**：

   * 标题：产品
   * 选择“我的网站内容”页面模板

1. 在文件夹树中，选择 **/Websites/My网站/英语** 页面并单击 **新** > **新页面**.
1. 在 **创建页面** 对话框，输入以下属性值，然后单击 **创建**：

   * 标题：服务
   * 选择“我的网站内容”页面模板

1. 在文件夹树中，选择 **/Websites/My网站/英语** 页面并单击 **新** > **新页面**.
1. 在 **创建页面** 对话框，输入以下属性值，然后单击 **创建**：

   * 标题：客户
   * 选择“我的网站内容”页面模板

   您的结构如下所示：

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. 要将您的页面链接到mywebsite设计，请在CRXDE Lite中选择 `/content/mywebsite/en/jcr:content` 节点。 在“属性”选项卡上，为新属性键入以下值，然后单击“添加”：

   * 名称：cq：designPath
   * 类型：字符串
   * 值： /etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 在新的Web浏览器选项卡或窗口中，打开 [https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html) 要查看产品页面，请执行以下操作：

   ![chlimage_1-38](assets/chlimage_1-38.png)

### 增强Contentpage脚本 {#enhancing-the-contentpage-script}

本节介绍如何使用AEM foundation组件脚本并通过编写您自己的脚本来增强contentpage脚本。

此 **产品** 页面将如下所示：

![chlimage_1](assets/chlimage_1.jpeg)

#### 使用“基础”页脚本 {#using-the-foundation-page-scripts}

在本练习中，您将配置pagecontent组件，使其超类型是AEM Page组件。 由于组件继承其超类型的功能，因此pagecontent会继承页面组件的脚本和属性。

例如，在组件JSP代码中，您可以引用超类型组件提供的脚本，就好像这些脚本包含在组件中一样。

1. 在CRXDE Lite中，将资产添加到 `/apps/mywebsite/components/contentpage` 节点。

   1. 选择 `/apps/mywebsite/components/contentpage` 节点。
   1. 在“属性”选项卡的底部，键入以下属性值，然后单击“添加”：

      * **名称：** sling：resourceSuperType
      * **类型：** 字符串
      * **值：** foundation/components/page

   1. 单击全部保存。

1. 打开 `contentpage.jsp` 文件位于 `/apps/mywebsite/components/contentpage` 和将现有代码替换为以下代码：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 它看起来如下所示：

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   打开页面源以查看head.jsp和body.jsp脚本生成的javascript和HTML元素。 打开页面时，以下脚本片段将Sidekick打开：

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### 使用您自己的脚本 {#using-your-own-scripts}

在此部分中，您将创建多个脚本，每个脚本都会生成页面正文的一部分。 然后，在pagecontent组件中创建body.jsp文件以覆盖AEM Page组件的body.jsp。 在body.jsp文件中，包括生成页面主体不同部分的脚本。

**提示：** 当组件包含的文件与组件的超类型中的文件具有相同名称和相对位置时，调用 *覆盖*.

1. 在CRXDE Lite中，创建文件 `left.jsp` 下 `/apps/mywebsite/components/contentpage`：

   1. 右键单击节点 `/apps/mywebsite/components/contentpage`，然后选择**创建**然后选择 **创建文件**.

   1. 在窗口中，键入 `left.jsp` 作为 **名称** 并单击 **确定**.

1. 编辑文件 `left.jsp` 要删除现有内容并替换为以下代码，请执行以下操作：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中，创建文件 `center.jsp` 下 `/apps/mywebsite/components/contentpage`：

   1. 右键单击节点 `/apps/mywebsite/components/contentpage`，选择 **创建**，则 **创建文件**.

   1. 在对话框中，键入 `center.jsp` 作为 **名称** 并单击 **确定**.

1. 编辑文件 `center.jsp` 要删除现有内容并使用以下代码替换它：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中，创建文件 `right.jsp` 下 `/apps/mywebsite/components/contentpage`：

   1. 右键单击节点 `/apps/mywebsite/components/contentpage`，选择 **创建**，则 **创建文件**.

   1. 在对话框中，键入 `right.jsp` 作为 **名称** 并单击 **确定**.

1. 编辑文件 `right.jsp` 要删除现有内容并替换为以下代码，请执行以下操作：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. 保存更改。
1. 在CRXDE Lite中，创建文件 `body.jsp` 下 `/apps/mywebsite/components/contentpage`：
1. 编辑文件 `body.jsp` 要删除现有内容并替换为以下代码，请执行以下操作：

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 它看起来如下所示：

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 创建顶部导航组件 {#creating-the-top-navigation-component}

在此部分中，您将创建一个组件，该组件显示指向网站所有顶级页面的链接以方便导航。 此组件内容显示在使用内容页面模板创建的所有页面的顶部。

在顶部导航组件(topnav)的第一个版本中，导航项仅为文本链接。 在第二个版本中，您使用图像导航链接实施topnav。

顶部导航将如下所示：

![chlimage_1-39](assets/chlimage_1-39.png)

#### 创建顶部导航组件 {#creating-the-top-navigation-component-1}

1. 在CRXDE Lite中，右键单击 `/apps/mywebsite/components`，选择 **创建**，则 **创建组件**.
1. 在 **创建组件** 窗口中，输入以下内容：

   * **标签**： `topnav`

   * **标题**: `My Top Navigation Component`

   * **描述**: `This is My Top Navigation Component`

1. 单击 **下一个** 直到您到达最后一个单击的窗口 **确定**. 保存更改。

#### 创建带有文本链接的上方导航脚本 {#creating-the-top-navigation-script-with-textual-links}

将渲染脚本添加到topnav以生成指向子页面的文本链接：

1. 在CRXDE Lite中，打开文件 `topnav.jsp` 下 `/apps/mywebsite/components/topnav`.
1. 通过复制并粘贴以下代码来替换存在的代码：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### 在Contentpage组件中包含顶部导航 {#including-top-navigation-in-the-contentpage-component}

要在内容页面组件中包含topnav，请执行以下操作：

1. 在CRXDE Lite中，打开 `body.jsp` 下 `/apps/mywebsite/components/contentpage`和替换：

   ```xml
   <div class="topnav">topnav</div>
   ```

   替换为:

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 顶部导航显示如下：

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### 使用字幕增强页面 {#enhancing-pages-with-subtitles}

页面组件定义属性，这些属性使您能够为页面提供字幕。 添加提供有关页面内容信息的字幕。

1. 在浏览器中，打开 **产品** 页面。
1. 在Sidekick上 **页面** 选项卡，单击 **页面属性**.
1. 在对话框的“基本”选项卡上，展开 **更多标题和描述，** 和 **字幕** 属性，类型 **我们的工作**. 单击&#x200B;**确定**。
1. 重复上述步骤以添加字幕 **关于我们的服务** 到 **服务** 页面。
1. 重复上述步骤以添加字幕 **我们获得的信任** 到 **客户** 页面。

   **提示：** 在CRXDE Lite中，选择/content/mywebsite/en/products/jcr：content节点以查看是否添加了subtitle属性。

#### 使用图像链接增强顶部导航 {#enhance-top-navigation-by-using-image-links}

增强topnav组件的渲染脚本，以便为导航控件使用图像链接而不是超文本。 图像包括链接目标的标题和子标题。

此练习演示 [Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing). 修改topnav.jsp脚本以调用一个脚本，该脚本可动态生成图像以用于页面导航链接。 在本练习中，Sling将解析图像源文件的URL以确定用于渲染图像的脚本。

例如，指向产品页面的图像链接的来源可以是https://localhost:4502/content/mywebsite/en/products.navimage.png。 Sling解析此URL以确定资源类型以及用于呈现资源的脚本：

1. Sling确定要访问的资源的路径 `/content/mwebysite/en/products.png.`
1. Sling将此路径与 `/content/mywebsite/en/products` 节点。
1. Sling确定 `sling:resourceType` 该节点的 `mywebsite/components/contentpage`.

1. Sling查找此组件中与URL选择器最匹配的脚本( `navimage`)和文件扩展名( `png`)。

在本练习中，Sling将这些URL与您创建的/apps/mywebsite/components/contentpage/navimage.png.java脚本进行匹配。

1. 在CRXDE Lite中，打开 `topnav.jsp` 下 `/apps/mywebsite/components/topnav.`找到锚点元素的内容（第14行）：

   ```xml
   <%=child.getTitle() %>
   ```

1. 使用以下代码替换锚点内容：

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. 保存更改。
1. 右键单击 `/apps/mywebsite/components/contentpage` 节点并单击 **创建** > **创建文件**.
1. 在 **创建文件** 窗口，作为 **名称**，类型 `navimage.png.java`.

   .java文件扩展名向Sling指示，应使用Apache Sling脚本Java支持编译脚本和创建servlet。

1. 将以下代码复制到 `navimage.png.java.`该代码扩展AbstractImageServlet类：

   * [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 创建用于存储当前资源属性的ImageContext对象。
   * 资源的父页面从ImageContext对象中提取。 然后获取页面标题和字幕。
   * [ImageHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/ImageHelper.html) 用于从站点设计的navimage_bg.jpg文件、页面标题和页面子标题生成图像。

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 顶部导航现在显示如下：

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### 创建列表子组件 {#creating-the-list-children-component}

创建listchildren组件，该组件可生成包含页面标题、描述和日期（例如，产品页面）的页面链接列表。 这些链接定位当前页面的子页面，或组件对话框中指定的根页面的子页面。

![chlimage_1-41](assets/chlimage_1-41.png)

#### 创建产品页面 {#creating-product-pages}

创建位于“产品”页面下方的两个页面。 对于每个描述两个特定产品的页面，您可以设置标题、描述和日期。

1. 在“Websites”页面的文件夹树中，选择“Websites/My Website/English/Products”项目，然后单击“New”>“New Page”。
1. 在对话框中，输入以下属性值，然后单击创建：

   * 标题：产品1。
   * 名称： product1。
   * 选择“我的网站内容”页面模板

1. 使用以下属性值在Products下创建另一个页面：

   * 标题：产品2
   * 名称： product2
   * 选择“我的网站内容”页面模板

1. 在CRXDE Lite中，设置“产品1”页面的说明和日期：

   1. 选择 `/content/mywebsite/en/products/product1/jcr:content` 节点。
   1. 在 **属性** 选项卡，输入以下值：

      * 名称: `jcr:description`
      * 类型: `String`
      * 价值: `This is a description of the Product 1!.`

   1. 单击 **添加**.
   1. 在 **属性** 选项卡，使用以下值创建另一个属性：

      * 名称：日期
      * 类型：字符串
      * 值：2008年2月14日
      * 单击“添加”。

   1. 单击全部保存。

1. 在CRXDE Lite中，设置“产品2”页面的说明和日期：

   1. 选择/content/mywebsite/en/products/product2/jcr：content节点。
   1. 在 **属性** 选项卡，输入以下值：

      * 名称：jcr：description
      * 类型：字符串
      * 值：这是对产品2的说明！。

   1. 单击 **添加**.
   1. 在同一文本框中，将先前的值替换为以下值：

      * 名称：日期
      * 类型：字符串
      * 值：2012年5月11日
      * 单击“添加”。

   1. 单击全部保存。

#### 创建列表子组件 {#creating-the-list-children-component-1}

要创建listchildren组件，请执行以下操作：

1. 在CRXDE Lite中，右键单击 `/apps/mywebsite/components`，选择 **创建**，则 **创建组件**.
1. 在对话框中，输入以下属性值，然后单击“下一步”：

   * 标签：listchildren。
   * 标题：我的列表子组件。
   * 描述：这是我的列表子组件。

1. 继续单击“下一步”，直到显示“允许的子项”面板，然后单击“确定”。

#### 创建列表子脚本 {#creating-the-list-children-script}

开发listchildren组件的脚本。

1. 在CRXDE Lite中，打开文件 `listchildren.jsp` 下 `/apps/mywebsite/components/listchildren`.
1. 将默认代码替换为以下代码：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a new Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. 保存更改。

#### 创建列表子项对话框 {#creating-the-list-children-dialog}

创建用于配置listchildren组件属性的对话框。

1. 在listchildren组件下创建对话框节点：

   1. 在CRXDE Lite中，右键单击 `/apps/mywebsite/components/listchildren`节点并单击 **创建** > **“创建”对话框**.

   1. 在对话框中，输入以下属性值，然后单击“确定”

      * **标签**： `dialog`

      * **标题**： `Edit Component` 并单击 **确定**.

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   具有以下属性：

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. 选择 `/apps/mywebsite/components/listchildren/dialog/items/items/tab1` 节点。
1. 在“属性”选项卡中，更改 **标题** 属性至 `List Children`

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. 选择tab1节点并单击创建>创建节点，输入以下属性值，然后单击确定：

   * 名称：项目
   * 类型：cq：WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. 使用以下属性值在items节点下创建一个节点：

   * 名称： listroot
   * 类型：cq：Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. 为listroot节点添加属性以将其配置为文本字段。 下表中的每一行都表示一个属性。 完成后，单击全部保存。

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | 字段标签 | 字符串 | 列表根的路径 |
   | name | 字符串 | 。/listroot |
   | xtype | 字符串 | textfield |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### 在Contentpage组件中包含列表子项 {#including-list-children-in-the-contentpage-component}

要在内容页面组件中包含listchildren组件，请执行以下操作：

1. 在CRXDE Lite中，打开文件 `left.jsp` 下 `/apps/mywebsite/components/contentpage` 并找到以下代码（第4行）：

   ```xml
   <div>newslist</div>
   ```

1. 将该代码替换为以下代码：

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. 保存更改。

#### 查看页面中的列表子项 {#viewing-list-children-in-a-page}

要查看此组件的完整操作，您可以查看“产品”页面：

* 未定义父页面（“列表根的路径”）时。
* 定义父页面（“列表根的路径”）时。

1. 在浏览器中，重新加载产品页面。 listchildren组件如下所示：

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. 作为列表根的路径，输入： `/content/mywebsite/en`. 单击确定。现在，页面上的listchildren组件如下所示：

   ![chlimage_1-45](assets/chlimage_1-45.png)

### 创建徽标组件 {#creating-the-logo-component}

创建一个显示公司徽标的组件，并提供指向网站主页的链接。 该组件包含一个设计模式对话框，以便在站点设计(/etc/designs/mywebsite)中存储属性值：

* 属性值适用于添加到使用该设计的页面的所有组件实例。
* 可以使用使用该设计的页面上的任何组件实例来配置属性。

设计模式对话框包含用于设置图像和链接路径的属性。 徽标组件将放置在网站中所有页面的左上角。

它将如下所示：

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager提供功能更全面的徽标组件( `/libs/foundation/components/logo`)。

#### 创建徽标组件节点 {#creating-the-logo-component-node}

要创建徽标组件，请执行以下步骤：

1. 在CRXDE Lite中，右键单击/apps/mywebsite/components，然后选择 **创建**，则 **创建组件**.
1. 在创建组件对话框中，输入以下属性值，然后单击下一步：

   * 标签: `logo`.
   * 标题: `My Logo Component`.
   * 描述: `This is My Logo Component`.

1. 单击下一步，直到到达对话框的最后一个面板，然后单击 **确定**.

#### 创建徽标脚本 {#creating-the-logo-script}

本节介绍如何创建脚本以显示带有主页链接的徽标图像。

1. 在CRXDE Lite中，打开文件 `logo.jsp` 下 `/apps/mywebsite/components/logo`.
1. 以下代码创建指向网站主页的链接，并添加对徽标图像的引用。 将代码复制到 `logo.jsp`：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. 保存更改。

#### 创建徽标设计对话框 {#creating-the-logo-design-dialog}

创建用于在“设计”模式下配置徽标组件的对话框。 必须命名设计模式对话框节点 `design_dialog`.

1. 在徽标组件下创建对话框节点：

   1. 右键单击 `/apps/mywebsite/components/logo` 节点并单击 **创建** > **“创建”对话框**.

   1. 键入以下属性值，然后单击“确定”：

      * **标签：** `design_dialog`

      * **标题:** `Logo (Design)`

1. 右键单击design_dialog分支中的tab1节点，然后单击“删除”。 单击全部保存。
1. 在 `design_dialog/items/items`节点，创建一个名为的新节点 `img` 类型 `cq:Widget`. 添加以下属性，然后单击“全部保存”：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | fileNameParameter | 字符串 | 。/imageName |
   | fileReferenceParameter | 字符串 | 。/imageReference |
   | name | 字符串 | 。/图像 |
   | 标题 | 字符串 | 图像 |
   | xtype | 字符串 | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### 创建徽标渲染脚本 {#creating-the-logo-render-script}

创建脚本以检索徽标图像并将其写入页面。

1. 右键单击徽标组件节点，然后单击创建>创建文件，以创建名为img.java的脚本文件GET。
1. 打开文件，将以下代码复制到文件中，然后单击“全部保存”：

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* don't create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### 将徽标组件添加到Contentpage组件 {#adding-the-logo-component-to-the-contentpage-component}

1. 在CRXDE Lite中，打开 `left.jsp` 下 `/apps/mywebsite/components/contentpage file` 并找到以下代码行：

   ```xml
   <div>logo</div>
   ```

1. 将该代码替换为以下代码行：

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 徽标如下所示，尽管目前它只显示基础链接：

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### 在页面中设置徽标图像 {#setting-the-logo-image-in-a-page}

本节介绍如何使用“设计模式”对话框将图像设置为徽标。

1. 在浏览器中打开“产品”页面后，单击Sidekick底部的“设计”按钮以进入设计模式。

   ![右方表示的“设计”按钮。](do-not-localize/chlimage_1-1.png)

1. 在“设计徽标”栏中，单击“编辑”以使用此对话框编辑徽标组件的设置。
1. 在对话框中，单击“图像”选项卡的面板，浏览从mywebsite.zip文件中提取的logo.png图像，然后单击“确定”。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 单击Sidekick标题栏上的三角形以返回“编辑”模式。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. 在CRXDE Lite中，转到以下节点以查看存储的属性值：

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### 包含痕迹导航组件 {#including-the-breadcrumb-component}

在此部分中，您将包含痕迹导航（跟踪）组件，该组件是基础组件之一。

1. 在CRXDE Lite中，浏览至 `/apps/mywebsite/components/contentpage`，打开文件 `center.jsp` 和替换：

   ```java
   <div>trail</div>
   ```

   替换为:

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. 保存更改。
1. 在浏览器中，重新加载 **产品1** 页面。 trail组件如下所示：

   ![chlimage_1-50](assets/chlimage_1-50.png)

### 包括标题组件 {#including-the-title-component}

在本节中，您将包含标题组件，它是基础组件之一。

1. 在CRXDE Lite中，浏览至 `/apps/mywebsite/components/contentpage`，打开文件 `center.jsp` 和替换：

   ```xml
   <div>title</div>
   ```

   替换为:

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. 保存更改。
1. 在浏览器中，重新加载产品页面。 标题组件如下所示：

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **注释**：您可以在编辑模式下设置其他标题和类型/大小。

### 包括段落系统组件 {#including-the-paragraph-system-component}

段落系统(parsys)是网站的重要组成部分，因为它管理着一系列段落。 它允许作者将段落组件添加到页面并提供结构。

将parsys组件（基础组件之一）添加到contentpage组件。

1. 在CRXDE Lite中，浏览至 `/apps/mywebsite/components/contentpage`，打开文件 `center.jsp` 并找到以下代码行：

   ```xml
   <div>parsys</div>
   ```

1. 将该代码行替换为以下代码，然后保存更改：

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. 在浏览器中，刷新产品页面。 它现在具有parsys组件，如下所示：

   ![chlimage_1-52](assets/chlimage_1-52.png)

### 创建图像组件 {#creating-the-image-component}

创建一个在段落系统中显示图像的组件。 为了节省时间，图像组件将创建为徽标组件的副本，并且进行了一些属性更改。

>[!NOTE]
>
>Adobe Experience Manager提供功能更全面的图像组件( `/libs/foundation/components/image`)。

#### 创建图像组件 {#creating-the-image-component-1}

1. 右键单击 `/apps/mywebsite/components/logo` 节点，然后单击复制。
1. 右键单击 `/apps/mywebsite/components` 节点，然后单击粘贴。
1. 右键单击 `Copy of logo` 节点，单击“重命名”，删除现有文本并键入 `image`.

1. 选择 `image` 组件节点，并更改以下属性值：

   * `jcr:title:` 我的图像组件。
   * `jcr:description`：这是我的图像组件。

1. 将资产添加到 `image` 节点具有以下属性值：

   * 名称： componentGroup
   * 类型：字符串
   * 值： MyWeb站点

1. 在 `image` 节点，重命名 `design_dialog` 节点至 `dialog`.

1. 重命名 `logo.jsp` 到 `image.jsp.`

1. 打开img.javaGET并将包更改为 `apps.mywebsite.components.image`.

![chlimage_1-53](assets/chlimage_1-53.png)

#### 创建图像脚本 {#creating-the-image-script}

本节介绍如何创建图像脚本。

1. 打开 `/apps/mywebsite/components/image/` `image.jsp`
1. 使用以下代码替换现有代码，然后保存更改：

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. 保存更改。

#### 创建图像cq：editConfig节点 {#creating-the-image-cq-editconfig-node}

此 `cq:editConfig` 节点类型允许您在编辑组件的属性时配置组件的某些行为。

在此部分中，您可以使用cq：editConfig节点将资产从Content Finder拖到图像组件中。

1. 在CRXDE Lite中的/apps/mywebsite/components/image节点下，创建一个新节点，如下所示：

   * 名称：cq：editConfig。
   * 类型：cq：EditConfig。

1. 在节点cq：editConfig下，创建一个新节点，如下所示：

   * 名称：cq：dropTargets。
   * 类型：cq：DropTargetConfig。

1. 在节点cq：dropTargets下，创建一个新节点，如下所示：

   * 名称：图像。
   * 类型： nt：unstructured。

1. 在CRXDE中，按如下方式设置属性：

| 名称 | 类型 | 价值 |
|---|---|---|
| 接受 | 字符串 | image/(gif | jpeg | png) |
| 组 | 字符串 | 媒体 |
| propertyName | 字符串 | 。/imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### 添加图标 {#adding-the-icon}

在此部分中，您可以添加图标，以使其在Sidekick中列出时显示在图像组件旁边：

1. 在CRXDE Lite中，右键单击文件 `/libs/foundation/components/image/icon.png` 并选择 **收到。**
1. 右键单击节点 `/apps/mywebsite/components/image` 并单击 **粘贴**，然后单击 **全部保存**.

#### 使用图像组件 {#using-the-image-component}

在此部分中，您将看到 **产品** 页面并将图像组件添加到段落系统。

1. 在浏览器中，重新加载 **产品** 页面。
1. 在Sidekick中，单击 **设计模式** 图标。
1. 单击“编辑”按钮可编辑段落的“设计”对话框。
1. 在对话框中，列表 **允许的组件** 显示；导航到 **我的网站**，选择 **我的图像组件** 并单击 **好的。**
1. 返回到 **编辑模式。**
1. 双击parsys框架(打开 **将组件或资产拖动到此处**)。 此 **插入新组件** 和 **Sidekick** 选择器如下所示：

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### 包括工具栏组件 {#including-the-toolbar-component}

在此部分中，您将包含工具栏组件，它是基础组件之一。

在编辑模式和设计模式中，您有多个选项。

1. 在CRXDE Lite中，导航到 `/apps/mywebsite/components/contentpage`，打开 `body.jsp` 文件并找到以下代码：

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. 使用以下代码替换该代码，然后保存更改。

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. 在“AEM Websites”页面的文件夹树中，选择“Websites/My Website/English”，然后单击“New”>“New Page”。 指定以下属性值，然后单击“创建”：

   * 标题：工具栏
   * 选择“我的网站内容”页面模板

1. 在页面列表中，右键单击“工具栏”页面，然后单击“属性”。 选择“在导航中隐藏”，然后单击“确定”。

   “在导航中隐藏”选项可防止页面显示在导航组件中，例如topnav和listchildren。

1. 在工具栏下，创建以下页面：

   * 联系人
   * 反馈
   * 登录
   * 搜索

1. 在浏览器中，重新加载产品页面。 它看起来如下所示：

   ![chlimage_1-55](assets/chlimage_1-55.png)

### 创建搜索组件 {#creating-the-search-component}

在此部分中，您将创建组件以搜索网站上的内容。 此搜索组件可以放置在任何页面的段落系统中（例如，在专门的搜索结果页面上）。

您的搜索输入框将如下所示 **英语** 页面：

![chlimage_1-56](assets/chlimage_1-56.png)

#### 创建搜索组件 {#creating-the-search-component-1}

1. 在CRXDE Lite中，右键单击 `/apps/mywebsite/components`，选择 **创建**，则 **创建组件**.
1. 使用对话框配置组件：

   1. 在第一个面板中，指定以下属性值：

      * 标签：搜索
      * 标题：我的搜索组件
      * 描述：这是我的搜索组件
      * 组：我的网站

   1. 单击“下一步”，然后再次单击“下一步”。
   1. 在“允许的父项”面板上，单击+按钮并键入 `*/parsys`.
   1. 单击“下一步”，然后单击“确定”。

1. 单击全部保存。
1. 复制以下节点并将其粘贴到apps/mywebsite/components/search节点：

   * `/libs/foundation/components/search/dialog`
   * `` `/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. 单击全部保存。

#### 创建搜索脚本 {#creating-the-search-script}

本节介绍如何创建搜索脚本：

1. 打开 `/apps/mywebsite/components/search/search.jsp` 文件。
1. 将以下代码复制到 `search.jsp`：

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. 保存更改。

#### 在Contentpage组件中包含搜索框 {#including-a-search-box-in-the-contentpage-component}

要在内容页面的左侧部分包含搜索输入框，请按以下步骤操作：

1. 在CRXDE Lite中，打开文件 `left.jsp` 下 `/apps/mywebsite/components/contentpage` 并找到以下代码（第2行）：

   ```xml
   %><div class="left">
   ```

1. 插入以下代码 **早于** 该行：

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. 找到以下代码行：

   ```xml
   <div>search</div>
   ```

1. 使用以下代码替换该代码，然后保存更改。

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. 在浏览器中，重新加载产品页面。 搜索组件如下所示：

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### 在搜索页面中包含搜索组件 {#including-the-search-component-in-the-search-page}

在此部分中，您将搜索组件添加到段落系统。

1. 在浏览器中，打开“搜索”页面。
1. 在Sidekick中，单击设计模式图标。
1. 在“设计”分块中（在“搜索”标题下），单击“编辑”。
1. 在对话框中，向下滚动到  **我的网站** 组，选择 **我的搜索组件** 并单击 **确定**.
1. 在Sidekick时，单击三角形以返回编辑模式。
1. 将我的搜索组件从Sidekick拖动到parsys框中。 它看起来如下所示：

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 导航到您的产品页面。 在输入框中搜索客户，然后按Enter。 您将被重定向到“搜索”页面。 切换到预览模式：输出的格式与以下类似：

   ![chlimage_1-59](assets/chlimage_1-59.png)

### 包含Iparsys组件 {#including-the-iparsys-component}

在此部分中，您将包含继承段落系统(iparsys)组件，该组件是基础组件之一。 利用此组件，可在父页面上创建段落结构，并让子页面继承段落。

对于此组件，您可以在编辑模式和设计模式下设置多个参数。

1. 在CRXDE Lite中，导航到 `/apps/mywebsite/components/contentpage`，打开文件 `right.jsp` 和替换：

   ```java
   <div>iparsys</div>
   ```

   替换为:

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. 保存更改。
1. 在浏览器中，重新加载** Products**页面。 整个页面如下所示：

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
