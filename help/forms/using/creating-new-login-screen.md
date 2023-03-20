---
title: 创建新的登录屏幕
seo-title: Creating a new login screen
description: 如何修改LiveCycle模块的登录页面，例如AEM Forms工作区或Forms管理器。
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---

# 创建新的登录屏幕{#creating-a-new-login-screen}

您可以修改使用AEM Forms登录屏幕的所有AEM Forms模块的登录屏幕。 例如，修改会影响Forms Manager和AEM Forms工作区的登录屏幕。

## 先决条件 {#prerequisite}

1. 登录 `/lc/crx/de` 具有管理员权限。
1. 执行以下操作：

   1. 复制分层结构：of `/libs/livecycle/core/content` at `/apps/livecycle/core/content`.

      维护相同（节点/文件夹）属性和访问控制。

   1. 复制内容文件夹：

      从: `/libs/livecycle/core`

      到: `/apps/livecycle/core`.

   1. 删除 `/apps/livecycle/core` 文件夹。

1. 执行以下操作：

   1. 复制分层结构：of `/libs/livecycle/core/components/login` at `/apps/livecycle/core/components/login`. 维护相同（节点/文件夹）属性和访问控制。

   1. 复制组件文件夹：从 `/libs/livecycle/core` to `/apps/livecycle/core`.

   1. 删除文件夹的内容： `/apps/livecycle/core/components/login`.

### 添加新区域设置 {#adding-a-new-locale}

1. 复制 `i18n` 文件夹：

   * 从 `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 删除内部的所有文件夹 `i18n` 除了一个，比如 `en`.

1. 在文件夹上 `en`，执行以下操作：

   1. 将文件夹重命名为要支持的区域设置名称。 例如：`ar`。

   1. 更改属性 `jcr:language` 值 `ar`(对于 `ar` 文件夹)。
   >[!NOTE]
   >
   >如果区域设置是语言 — 国家/地区代码组合，例如， `ar-DZ`，然后将文件夹名称和属性值更改为 `ar-DZ`.

1. 复制`login.jsp`：

   * 从 `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 修改以下代码片段 `/apps/livecycle/core/components/login/login.jsp`:

***区域设置是语言代码***

```jsp
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
```

收件人

```jsp
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

```jsp
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
```

收件人

```jsp
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

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 添加新文本或修改现有文本 {#adding-new-text-or-modifying-existing-text}

1. 复制 `i18n` 文件夹：

   * 从 `/libs/livecycle/core/components/login`
   * 到 `/apps/livecycle/core/components/login`

1. 现在，修改资产的值 `sling:message` 要更改其文本的节点（位于所需的区域设置代码文件夹下）的。 翻译是通过 `sling:key` 节点的属性。

1. 要添加新的键值对，请执行以下操作。 请查看屏幕截图中的示例，该示例如下所示。

   1. 创建类型的节点 `sling:MessageEntry`，或复制现有节点并对其重命名，位于所有区域设置文件夹下。
   1. 复制`login.jsp`：

      * 从 `/libs/livecycle/core/components/login`

      * 到 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以合并新添加的文本。

   ![添加新的键值对](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   收件人

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 添加新样式或修改现有样式 {#adding-new-style-or-modifying-existing-style}

1. 复制 `login` 节点：

   * 从 `/libs/livecycle/core/content`
   * 到 `/apps/livecycle/core/content`

1. 删除文件 `login.js` 和 `jquery-1.8.0.min.js`，从节点 `/apps/livecycle/core/content/login.`
1. 修改CSS文件中的样式。
1. 要添加新样式，请执行以下操作：

   1. 将新样式添加到 `/apps/livecycle/core/content/login/login.css`
   1. 复制 `login.jsp`

      * 从 `/libs/livecycle/core/components/login`

      * 到 `/apps/livecycle/core/components/login`
   1. 修改 `/apps/livecycle/core/components/login/login.jsp` 以整合新添加的样式。



例如：

* 将以下内容添加到 `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* 在 `/apps/livecycle/core/components/login.jsp`.


   ```jsp
   <div class="loginContentArea">
   ```

   收件人

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>如果 `/apps/livecycle/core/content/login` (复制自 `/libs/livecycle/core/content/login`)，然后删除CSS中的相应引用。

### 添加新图像 {#add-new-images}

1. 按照添加新样式或修改现有样式的步骤操作（见上文）。
1. 在 `/apps/livecycle/core/content/login`. 要添加图像，请执行以下操作：

   1. 安装WebDAV客户端。
   1. 导航到 `/apps/livecycle/core/content/login` 文件夹，使用webDAV客户端。 有关更多信息，请参阅： [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

   1. 添加新图像。

1. 在中添加新样式 `/apps/livecycle/core/content/login/login.css,` 对应于 `/apps/livecycle/core/content/login`.
1. 在中使用新样式 `login.jsp` at `/apps/livecycle/core/components`.

例如：


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    *在/apps/livecycle/core/components/login.jsp中修改以下内容。

```jsp
<div class="loginContainerBkg">
```

收件人

```jsp
<div class="newLginContainerBkg">
```
