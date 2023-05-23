---
title: 初始设置
seo-title: Initial Setup
description: 設定社群
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# 初始设置 {#initial-setup}

## 啟動作者和發佈執行個體 {#start-author-and-publish-instances}

為了開發和示範之目的，必須執行一個作者和一個發佈例項。

若要這麼做，請遵循基本AEM [快速入門](../../help/sites-deploying/deploy.md#getting-started) 指示，結果為：

* 創作環境： [localhost：4502](http://localhost:4502/)
* 發佈環境於 [localhost：4503](http://localhost:4503/)

若為AEM Communities，

* 製作環境適用於：

   * 網站、範本和元件的開發。
   * 管理和設定工作。

* 發佈環境適用於：

   * 發佈和仲裁內容的社群體驗。
   * 建立社群群組、成員和成員群組。

>[!NOTE]
>
>若不熟悉AEM，請檢視以下說明檔案： [基本處理](../../help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).

## 安裝最新Communities版本 {#install-latest-communities-release}

本教學課程會建立 [參與社群網站](overview.md#engagement-community) 且是以AEM Communities 6.2 Feature Pack 1.10版為基礎。

若要確保已安裝最新的Feature Pack，請造訪：

* [最新版本](deploy-communities.md#latest-releases)

## 配置 Analytics {#configure-analytics}

時間 [已為社群網站設定Adobe Analytics](analytics.md)，提供社群活動的相關資訊，可改善社群成員的體驗，並為網站管理員提供意見回饋。

可選擇與Adobe Analytics整合。

## 設定通知的電子郵件 {#configure-email-for-notifications}

通知功能，預設可用於所有使用建立的網站 `Communities Sites` console提供通知的電子郵件通道。

若要為網站正確設定電子郵件，這是必要的。

另請參閱 [設定電子郵件](email.md).

## 啟用通道服務 {#enable-the-tunnel-service}

在製作環境中建立社群網站時，通道服務可讓您將角色指派給在發佈環境中註冊的受信任社群成員。 通道服務也允許從存取社群成員 [成員和群組主控台](members.md) 在作者環境中。

慣例適用於在發佈環境中建立的成員與成員群組： *not* 在作者環境中重新建立。 如需詳細資訊，請參閱 [管理使用者和使用者群組](users.md).

如需啟用通道服務的簡單指示，請參閱： **作者** 例項，請參閱 [通道服務](deploy-communities.md#tunnel-service-on-author).

## 社群管理員角色 {#community-administrator-role}

「社群管理員」群組的成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）和稽核內容。

### 创建用户 {#create-user}

建立使用者： *作者*，已指派社群管理員角色的使用者：

* 在作者執行個體上

   * 例如， [http://localhost:4502/](http://localhost:4503/)

* 以管理員許可權登入

   * 例如，使用者名稱&#39;admin&#39; /密碼&#39;admin&#39;

* 從主控台，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.
* 從 **編輯** 功能表，選取 **[!UICONTROL 新增使用者]**

* 在 `Create New User` 對話方塊輸入：

   * **[!UICONTROL ID]**：天狼星
   * **[!UICONTROL 電子郵件地址]**： sirius.nilson@mailinator.com
   * **[!UICONTROL 密碼]**：密碼
   * **[!UICONTROL 確認密碼(&amp;A)；]**：密碼
   * **[!UICONTROL 名字]**：天狼星
   * **[!UICONTROL 姓氏]**： Nilson

### 將Sirius指派給社群管理員群組 {#assign-sirius-to-community-administrators-group}

向下捲動至 `Add User to Groups`：

* 輸入&#39;C&#39;進行搜尋

   * 选择 `Community Administrators`
   * 选择 `Community Enablement Managers`

* 选择&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 啟用社交登入 {#enable-social-login}

使用Facebook和Twitter社交登入的示範版本之前，您必須

1. 安裝修正套件或 [最新feature pack](deploy-communities.md#latestfeaturepack) (2017年3月Facebook API變更內容)。
1. [啟用OAuth提供者](social-login.md#adobe-granite-oauth-authentication-handler) 在發佈環境中。

對於生產伺服器，必須建立提供社交登入所需的雲端服務。

另請參閱 [使用Facebook和Twitter進行社交登入](social-login.md).

## 建立教學課程標籤 {#create-tutorial-tags}

使用「 」的標籤名稱空間建立要用於engage教學課程的標籤 `Tutorial`.

使用 [標籤主控台](../../help/sites-administering/tags.md#tagging-console) 若要建立下列標籤：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然後依照指示執行下列動作：

1. [設定標籤許可權](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [發佈標籤](../../help/sites-administering/tags.md#publishing-tags).

為AEM Communities快速入門Tutorials建立的標籤範例套件

[获取文件](assets/tutorial_tags-v63.zip)

## UGC常用存放區的MongoDB {#mongodb-for-ugc-common-store}

建議設定（但選用） [MSRP](msrp.md) (MongoDB)作為 [公用存放區](working-with-srp.md) 以體驗從發佈和/或作者環境仲裁所有UGC的彈性。

如需指示，請造訪 [如何設定MongoDB以進行示範](demo-mongo.md).

根據預設，安裝作者和發佈AEM例項時，使用者產生的內容(UGC)會儲存在 [JCR Tar儲存](../../help/sites-deploying/platform.md) ，存取方式： [JSRP](jsrp.md). JSRP不是通用存放區，這表示UGC只會顯示在輸入它的執行個體上。 通常UGC會輸入在發佈執行個體上，且不會顯示在製作環境中，導致需要使用發佈執行個體的所有稽核任務。
