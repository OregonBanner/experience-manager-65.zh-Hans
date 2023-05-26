---
title: 在AEM中选择用户界面
description: 配置在AEM中使用哪个接口。
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# 选择您的UI{#selecting-your-ui}

尽管触屏UI现在是标准UI，并且管理和编辑站点几乎达到了功能对等性，但有时用户可能会希望切换到 [经典UI](/help/sites-classic-ui-authoring/classicui.md). 执行此操作有几个选项。

>[!NOTE]
>
>有关与经典UI的功能对等状态的详细信息，请参阅 [触屏UI对等功能](/help/release-notes/touch-ui-features-status.md) 文档。

您可以在多个位置定义要使用的UI：

* [为实例配置默认UI](#configuring-the-default-ui-for-your-instance)
这将设置在用户登录时显示的默认UI，但用户可能能够覆盖此设置，并为其帐户或当前会话选择其他UI。

* [为您的帐户设置经典UI创作](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
此操作会将UI设置为在编辑页面时用作默认值，但用户可以覆盖此项，并为其帐户或当前会话选择其他UI。

* [切换到当前会话的经典UI](#switching-to-classic-ui-for-the-current-session)
这将切换到当前会话的经典UI。

* 对于 [页面创作系统对UI进行某些覆盖](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>用于切换到经典UI的各种选项不会立即可用，必须专门为您的实例配置这些选项。
>
>参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

>[!NOTE]
>
>从以前版本升级的实例将保留经典UI用于页面创作。
>
>升级后，页面创作不会自动切换到触控式UI，但您可以使用来配置此设置 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM创作UI模式服务** ( `AuthoringUIMode` 服务)。 参见 [编辑器的UI覆盖](#ui-overrides-for-the-editor).

## 为实例配置默认UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以使用配置启动和登录时看到的UI [根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

这可以由用户默认设置或会话设置覆盖。

## 为您的帐户设置经典UI创作 {#setting-classic-ui-authoring-for-your-account}

每个用户都可以访问其 [用户首选项](/help/sites-authoring/user-properties.md#userpreferences) 以定义他/她是否希望使用经典UI进行页面创作（而不是默认UI）。

这可以由会话设置覆盖。

## 切换到当前会话的经典UI {#switching-to-classic-ui-for-the-current-session}

使用触屏优化UI时，桌面用户可能希望还原为经典（仅限桌面）UI。 有多种方法可用于切换到当前会话的经典UI：

* **导航链接**

   >[!CAUTION]
   >
   >用于切换到经典UI的此选项不是立即可用的，必须专门为您的实例配置它。
   >
   >
   >参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

   如果启用此项，则每当您将鼠标悬停在适用的控制台上时，将显示一个图标（监视器的符号），点按/单击此项将在经典UI中打开相应的位置。

   例如，链接来自 **站点** 到 **siteadmin**：

   ![syui-01](assets/syui-01.png)

* **URL**

   可以使用欢迎屏幕的URL访问经典UI，网址为 `welcome.html`. 例如：

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >触屏优化UI可通过以下方式访问： `sites.html`. 例如：
   >
   >
   >`https://localhost:4502/sites.html`

### 编辑页面时切换到经典UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>用于切换到经典UI的此选项不是立即可用的，必须专门为您的实例配置它。
>
>参见 [启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md) 了解更多信息。

如果启用， **打开经典UI** 可从以下位置获取： **页面信息** 对话框：

![syui-02](assets/syui-02.png)

### 编辑器的UI覆盖 {#ui-overrides-for-the-editor}

在页面创作时，系统可能会覆盖用户或系统管理员定义的设置。

* 创作页面时：

   * 使用访问页面时，强制使用经典编辑器 `cf#` 在URL中。 例如：
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 使用时强制使用触屏编辑器 `/editor.html` 在URL中或使用触控设备时。 例如：
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何强制都是临时的，只对浏览器会话有效

   * Cookie集的设置将取决于是否启用了触控( `editor.html`)或经典( `cf#`)时，不会将反向链接计算两次。

* 打开页面时 `siteadmin`，将检查是否存在以下项目：

   * Cookie
   * 用户偏好设置
   * 如果两者都不存在，则默认为在中设置的定义。 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 的 **WCM创作UI模式服务** ( `AuthoringUIMode` 服务)。

>[!NOTE]
>
>如果 [用户已定义了页面创作的首选项](#settingthedefaultauthoringuiforyouraccount)，不会通过更改OSGi属性来覆盖该属性。

>[!CAUTION]
>
>由于使用了Cookie（如上所述），因此不建议执行以下任一操作：
>
>* 手动编辑URL — 非标准URL可能会导致未知情况和功能缺失。
>* 使两个编辑器同时打开 — 例如，在不同窗口中打开。

