---
title: 配置帐户环境
description: AEM 提供了用于配置帐户和创作环境的某些方面的功能
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 64%

---

# 配置帐户环境{#configuring-your-account-environment}

AEM 提供了用于配置帐户和创作环境的某些方面的功能。

通过使用[标题](/help/sites-authoring/basic-handling.md#the-header)和关联的[我的首选项](#userpreferences)对话框中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项，您可以修改用户选项。

首先，访问标题中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项。

## 用户设置 {#user-settings}

在&#x200B;**用户**&#x200B;设置对话框中，您可以访问：

* 模拟为

   * 使用 [模拟为](/help/sites-administering/security.md#impersonating-another-user) 用户可代表其他用户工作的功能。

* 配置文件

   * 提供指向您的网站的便捷链接 [用户设置](/help/sites-administering/security.md))

* [我的偏好设置](/help/sites-authoring/user-properties.md#my-preferences)

   * 指定用户特有的各种首选项设置

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 我的偏好设置 {#my-preferences}

**我的首选项**&#x200B;对话框可通过标题中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项进行访问。

每个用户都可以为自己设置某些属性。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **语言**

  此选项定义要用于创作环境 UI 的语言。从可用列表中选择所需语言。

  此配置还用于经典UI。

* **窗口管理**

  此选项定义打开窗口的行为。选择：

   * **多窗口**（默认）

      * 页面会在新窗口中打开。

   * **单窗口**

      * 页面会在当前窗口中打开。

* **显示适用于资产的桌面操作**

  此选项需要使用AEM桌面应用程序。

* **注释颜色**

  此选项定义创建注释时使用的默认颜色。

   * 单击颜色块，以便可以打开样本选择器并选择颜色。
   * 或者，可在字段中输入所需颜色的十六进制代码。

* **相对日期显示**

  为了提高可读性，AEM将过去七天内的日期渲染为相对日期（例如，三天前），将更早的日期渲染为确切日期（例如，2017年3月20日）。

  此选项定义系统中日期的显示方式。以下选项可供选择：

   * **始终显示确切日期**：将始终显示确切日期（从不显示相对日期）。
   * **1 天**：对于一天内的日期显示相对日期，其他情况则显示确切日期。

   * **7 天（默认）**：对于七天内的日期显示相对日期，其他情况则显示确切日期。

   * **1 个月**：对于一个月内的日期显示相对日期，其他情况则显示确切日期。

   * **1 年**：对于一年内的日期显示相对日期，其他情况则显示确切日期。

   * **始终显示相对日期**：从不显示确切日期，只显示相对日期。

* **启用快捷键**

  AEM支持使用多个键盘快捷键，以便更高效地创作。

   * [用于编辑页面的键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)

  此选项可启用键盘快捷键。默认情况下，这些功能处于启用状态，但可以禁用，例如，如果用户有特定的辅助功能要求。

* **使用经典版创作体验**

  此选项启用 [经典UI](/help/sites-classic-ui-authoring/home.md)基于的页面创作。 默认情况下，使用标准UI。

* **启用资产主页**

  仅当系统管理员为整个组织启用了资产主页体验时，此选项才可用。

* **Stock 配置**

  此选项可让您指定首选的Adobe Stock配置，并且仅在系统管理员已启用时才可用 [Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md).
