---
title: 設定帳戶環境
seo-title: Configuring Your Account Environment
description: AEM提供您設定帳戶及製作環境某些方面的功能
seo-description: AEM provides you with the capability to configure your account and certain aspects of the author environment
uuid: ef31be29-5c18-4dc9-ad51-fb001588b31e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b610e19c-f8d9-4ae2-b056-9fd5cf541261
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 52%

---

# 設定帳戶環境{#configuring-your-account-environment}

AEM 提供了配置帐户和创作环境某些方面的功能。

通过使用[标题](/help/sites-authoring/basic-handling.md#the-header)和关联的[我的首选项](#userpreferences)对话框中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项，您可以修改用户选项。

從存取 [使用者](/help/sites-authoring/user-properties.md#user-settings) 選項來識別。

## 用户设置 {#user-settings}

此 **使用者** 設定對話方塊可讓您存取：

* 模拟为

   * 使用 [模擬為](/help/sites-administering/security.md#impersonating-another-user) 使用者可以代表其他使用者工作的功能。

* 配置文件

   * 提供您便利的連結，讓您連結至 [使用者設定](/help/sites-administering/security.md))

* [我的偏好设置](/help/sites-authoring/user-properties.md#my-preferences)

   * 指定用户特有的各种首选项设置

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 我的偏好设置 {#my-preferences}

**我的首选项**&#x200B;对话框可通过标题中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项进行访问。

每个用户都可以为自己设置特定的属性。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **语言**

   這會定義用於編寫環境UI的語言。 從可用清單中選取所需的語言。

   此設定也用於傳統UI。

* **窗口管理**

   這會定義行為或開啟視窗。 选择：

   * **多視窗** （預設）

      * 頁面將在新視窗中開啟。
   * **单窗口**

      * 頁面將在目前視窗中開啟。


* **显示适用于资产的桌面操作**

   此選項需要AEM案頭應用程式才能使用。

* **注释颜色**

   這會定義製作註解時使用的預設顏色。

   * 按一下顏色區塊以開啟色票選取器來選取顏色。
   * 或者，可在字段中输入所需颜色的十六进制代码。

* **相对日期显示**

   為了改善可讀性，AEM會將過去七天內的日期轉譯為相對日期（例如三天前），而將較舊的日期轉譯為確切日期（例如2017年3月20日）。

   此选项定义系统中日期的显示方式。以下选项可供选择：

   * **始终显示确切日期**：将始终显示确切日期（从不显示相对日期）。
   * **1 天**：对于一天内的日期显示相对日期，其他情况则显示确切日期。

   * **7 天（默认）**：对于七天内的日期显示相对日期，其他情况则显示确切日期。

   * **1 个月**：对于一个月内的日期显示相对日期，其他情况则显示确切日期。

   * **1 年**：对于一年内的日期显示相对日期，其他情况则显示确切日期。

   * **始终显示相对日期**：从不显示确切日期，只显示相对日期。

* **启用快捷键**

   AEM 支持使用许多键盘快捷键，以便更高效地进行创作。

   * [用于编辑页面的键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)

   此選項會啟用鍵盤快速鍵。 預設會啟用這些功能，但如果使用者有特定的協助工具要求，則可以停用這些功能。

* **使用经典版创作体验**

   此選項會啟用 [傳統UI](/help/sites-classic-ui-authoring/home.md)-based頁面製作。 依預設，會使用標準UI。

* **启用资产主页**

   仅当系统管理员为整个组织启用了资产主页体验时，此选项才可用。

* **Stock 配置**

   此選項可讓您指定偏好的Adobe Stock設定，且僅在您的系統管理員已啟用時才能使用 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md).
