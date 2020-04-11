---
title: 创建新登录屏幕
seo-title: 创建新登录屏幕
description: 如何修改LiveCycle模块的登录页，例如AEM Forms工作区或Forms Manager。
seo-description: 如何修改LiveCycle模块的登录页，例如AEM Forms工作区或Forms Manager。
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 创建新登录屏幕{#creating-a-new-login-screen}

您可以修改使用AEM Forms登录屏幕的所有AEM Forms模块的登录屏幕。 例如，这些修改会影响Forms Manager和AEM Forms工作区的登录屏幕。

## 先决条件 {#prerequisite}

1. 使用“管理员” `/lc/crx/de` 权限登录。
1. 执行以下操作：

   1. 复制分层结构：在 `/libs/livecycle/core/content` 的 `/apps/livecycle/core/content`。 保持相同的（节点／文件夹）属性和访问控制。

   1. 复制内容文件夹：从 `/libs/livecycle/core` 到 `/apps/livecycle/core`。

   1. 删除文件夹的 `/apps/livecycle/core` 内容。

1. 执行以下操作：

   1. 复制分层结构：在 `/libs/livecycle/core/components/login` 的 `/apps/livecycle/core/components/login`。 保持相同的（节点／文件夹）属性和访问控制。

   1. 复制组件文件夹：从 `/libs/livecycle/core` 到 `/apps/livecycle/core`。

   1. 删除文件夹的内容： `/apps/livecycle/core/components/login`.

### 添加新区域设置 {#adding-a-new-locale}

1. 复制文 `i18n` 件夹：

   * 起始日期: `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 例如，删除内部除一 `i18n` 个文件夹之外的所有文件夹 `en`。
1. 在文件夹中 `en`，执行以下操作：

   1. 将文件夹重命名为要支持的区域设置名称。 For example, `ar`.
   1. 将属性 `jcr:language` 值更 `ar`改为(对于文 `ar` 件夹)。
   >[!NOTE]
   >
   >如果区域设置是语言——国家／地区代码组合， `ar-DZ`则将文件夹名称和属性值更改为 `ar-DZ`。

1. 复制 `login.jsp`:

   * 起始日期: `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 为以下代码片段修改 `/apps/livecycle/core/components/login/login.jsp`:

   ***区域设置是语言代码***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***区域设置是语言——国家／地区代码***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***更改默认区域设置***

   ```
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)
   
   To
   
   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
   ```

### 添加新文本或修改现有文本 {#adding-new-text-or-modifying-existing-text}

1. 复制文 `i18n` 件夹：

   * 起始日期: `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 现在，修改要更改其文 `sling:message` 本的节点（在所需区域设置代码文件夹下）的属性值。 转换是通过节点属性值中提 `sling:key` 到的键完成的。
1. 要添加新的键值对，请执行以下操作。 请查看屏幕截图中的示例。

   1. 创建类型的节点，或 `sling:MessageEntry`复制现有节点并重命名所有区域设置文件夹下的节点。
   1. 复制 `login.jsp` :

      * 起始日期: `/libs/livecycle/core/components/login`

      * 到 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以合并新添加的文本。
   ![添加新键值对](assets/capture_new.png)

   ```
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   
   To
   
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 添加新样式或修改现有样式 {#adding-new-style-or-modifying-existing-style}

1. Copy `login` node:

   * 起始日期: `/libs/livecycle/core/content`
   * 到 `/apps/livecycle/core/content`

1. 从节 `login.js` 点删 `jquery-1.8.0.min.js`除文件和 `/apps/livecycle/core/content/login.`
1. 修改CSS文件中的样式。
1. 添加新样式：

   1. 向 `/apps/livecycle/core/content/login/login.css`
   1. 复制 `login.jsp`

      * 起始日期: `/libs/livecycle/core/components/login`

      * 到 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以合并新添加的样式。


1. 例如：

   * 将以下内容添加到 `/apps/livecycle/core/content/login/login.css`。

   ```css
   .newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
   ```

   * 在/apps/livecycle/core/components/login.jsp中修改以下内容。

   ```
   <div class="loginContentArea">
   
   To
   
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>如果删除了(从中复 `/apps/livecycle/core/content/login` 制的)中的 `/libs/livecycle/core/content/login`现有图像，则删除CSS中的相应引用。

### 添加新图像 {#add-new-images}

1. 按照添加新样式或修改现有样式（见上文说明）的步骤操作。
1. 在中添加新图像 `/apps/livecycle/core/content/login`。 要添加图像，请执行以下操作：

   1. 安装WebDAV客户端。
   1. 使用webDAV客 `/apps/livecycle/core/content/login` 户端导航到文件夹。 有关详细信息，请参阅： [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

   1. 添加新图像。

1. 在中添加与中添 `/apps/livecycle/core/content/login/login.css,` 加的新图像对应的新样式 `/apps/livecycle/core/content/login`。
1. 使用中的新样 `login.jsp` 式 `/apps/livecycle/core/components`。
1. 例如：

   * 将以下内容添加到 `/apps/livecycle/core/content/login/login.css`

   ```css
   .newLoginContainerBkg {
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```

   * 在/apps/livecycle/core/components/login.jsp中修改以下内容。

   ```
   <div class="loginContainerBkg">
   
   To
   
   <div class="newLginContainerBkg">
   ```
