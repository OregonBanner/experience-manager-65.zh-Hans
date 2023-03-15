---
title: 选择您的 UI
seo-title: Selecting your UI
description: 配置您在 AEM 中工作时将使用的界面
seo-description: Configure which interface you will use to work in AEM
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 83%

---

# 选择您的 UI{#selecting-your-ui}

尽管触屏优化 UI 现在是标准 UI，并且在管理和编辑站点方面几乎实现了功能对等性，但有时用户还是希望切换到[经典 UI](/help/sites-classic-ui-authoring/classicui.md)。可使用几个选项进行切换。

>[!NOTE]
>
>有关与经典 UI 的功能对等性状态的详细信息，请参阅[触屏优化 UI 功能对等性](/help/release-notes/touch-ui-features-status.md)文档。

您可以在多个位置定义要使用的 UI：

* [配置实例的默认 UI](#configuring-the-default-ui-for-your-instance) 此操作将设置用户登录时显示的默认 UI，但是，用户可以覆盖此设置，为其帐户或当前会话选择其他 UI。

* [为您的帐户设置经典 UI 创作](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account) 此操作将设置编辑页面时使用的默认 UI，但是，用户可以覆盖此设置，为其帐户或当前会话选择其他 UI。

* [将当前会话切换为经典 UI](#switching-to-classic-ui-for-the-current-session) 此操作会将当前会话切换为经典 UI。

* 对于[页面创作，系统会重写某些与 UI 有关的设置](#ui-overrides-for-the-editor)。

>[!CAUTION]
>
>切换到经典 UI 的各种选项无法立即开箱即用，必须对您的实例进行专门配置。
>
>参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

>[!NOTE]
>
>对于从以前版本升级而来的实例，页面创作将继续使用经典 UI。
>
>升级后，页面创作不会自动切换到触控式UI，但您可以使用来配置此设置 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM创作UI模式服务** ( `AuthoringUIMode` 服务)。 请参阅[编辑器的 UI 重写](#ui-overrides-for-the-editor)。

## 配置实例的默认 UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以通过使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)配置启动和登录时显示的 UI。

该设置可能会被用户默认设置或会话设置所重写。

## 为您的帐户设置经典 UI 创作 {#setting-classic-ui-authoring-for-your-account}

每个用户都可以访问[用户首选项](/help/sites-authoring/user-properties.md#userpreferences)来定义自己是否希望使用经典 UI 进行页面创作（而不是默认 UI）。

该设置可能会被会话设置所重写。

## 将当前会话切换为经典 UI {#switching-to-classic-ui-for-the-current-session}

使用触屏优化 UI 时，桌面用户可能想要还原到经典（仅限桌面）UI。将当前会话切换到经典 UI 的方法有多种。

* **导航链接**

   >[!CAUTION]
   >
   >用于切换到经典 UI 的该选项无法立即开箱即用，必须对您的实例进行专门配置。
   >
   >
   >参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

   如果启用该选项，那么每当您将鼠标悬停在适用的控制台上时，都会显示一个图标（一个显示器符号），点按/单击它将在经典 UI 中打开相应的位置。

   例如，从&#x200B;**站点**&#x200B;到&#x200B;**站点管理员**&#x200B;的链接：

   ![syui-01](assets/syui-01.png)

* **URL**

   可以使用欢迎屏幕的URL访问经典UI，网址为 `welcome.html`.例如：

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >触屏优化 UI 可以通过 `sites.html` 访问。例如：
   >
   >
   >`https://localhost:4502/sites.html`

### 编辑页面时切换为经典 UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>用于切换到经典 UI 的该选项无法立即开箱即用，必须对您的实例进行专门配置。
>
>参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

如果已启用，**打开经典 UI** 将可从&#x200B;**页面信息**&#x200B;对话框中访问：

![syui-02](assets/syui-02.png)

### 编辑器的 UI 重写 {#ui-overrides-for-the-editor}

创作页面时，系统可能会重写用户或系统管理员定义的设置。

* 创作页面时：

   * 使用访问页面时，强制使用经典编辑器 `cf#` 在URL中。 例如：
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 使用时强制使用触屏编辑器 `/editor.html` 在URL中或使用触控设备时。 例如：
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何强制操作都是临时的，而且仅对浏览器会话有效

   * Cookie集的设置将取决于是否启用了触控( `editor.html`)或经典( `cf#`)时，不会将反向链接计算两次。

* 在通过 `siteadmin` 打开页面时，将检查以下各项是否存在：

   * Cookie
   * 用户首选项
   * 如果两者都不存在，则将默认使用 [WCM 创作 UI 模式服务](/help/sites-deploying/configuring-osgi.md)（**服务**）的 `AuthoringUIMode`OSGi 配置中设置的定义。

>[!NOTE]
>
>如果[用户已经为页面创作定义了首选项](#settingthedefaultauthoringuiforyouraccount)，那么更改 OSGi 属性不会覆盖该设置。

>[!CAUTION]
>
>由于使用 Cookie，如之前所述，建议不要执行以下操作：
>
>* 手动编辑 URL - 非标准 URL 可能会导致未知情况和功能缺失。
>* 同时打开两种模式的编辑器 - 例如，在不同的窗口中打开。

