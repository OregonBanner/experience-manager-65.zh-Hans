---
title: 社群網站要點
seo-title: Community Site Essentials
description: 匯出和刪除社群網站以及建立自訂網站範本
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# 社群網站要點 {#community-site-essentials}

## 自訂網站範本 {#custom-site-template}

可為社群網站的每個語言副本個別指定自訂網站範本。

若要這麼做：

* 建立自訂範本。
* 覆蓋預設的網站範本路徑。
* 新增自訂範本至覆蓋路徑。
* 透過新增以下專案來指定自訂範本： `page-template` 屬性至 `configuration` 節點。

**預設範本**：

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**覆蓋路徑中的自訂範本**：

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**屬性**： page-template

**型別**：字串

**值**： `template-name` （無副檔名）

**設定節點**：

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>覆蓋路徑中的所有節點只需要屬於型別 `Folder`.

>[!CAUTION]
>
>如果自訂範本獲得名稱 *sitepage.hbs*，則會自訂所有社群網站。

### 自訂網站範本範例 {#custom-site-template-example}

例如， `vertical-sitepage.hbs` 是網站範本，可讓功能表連結垂直放置於頁面左下方，而非橫幅的水準下方。

[取得檔案](assets/vertical-sitepage.hbs)
將自訂網站範本放置在覆蓋資料夾中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

透過新增來識別自訂範本 `page-template` 屬性至設定節點：

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

請確定 **全部儲存** 並將自訂程式碼復寫至所有AEM例項（從主控台發佈社群網站內容時，未包含自訂程式碼）。

復寫自訂程式碼的建議作法是 [建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package) 並將其部署在所有執行個體上。

## 匯出社群網站 {#exporting-a-community-site}

社群網站建立後，即可將網站匯出為儲存在封裝管理程式中的AEM套件，並可供下載和上傳。

這可從以下網址取得： [社群網站主控台](sites-console.md#exporting-the-site).

請注意，UGC和自訂程式碼不會包含在社群網站套件中。

若要匯出UGC，請使用 [AEM Communities UGC移轉工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)，這是GitHub上提供的開放原始碼移轉工具。

## 刪除社群網站 {#deleting-a-community-site}

自AEM Communities 6.3 Service Pack 1起，將游標暫留在的社群網站上時，會出現「刪除網站」圖示。 **[!UICONTROL Communities]** > **[!UICONTROL 網站]** 主控台。 在開發期間，如果想要刪除社群網站並重新開始，您可以使用此功能。 刪除社群網站時，會移除與該網站相關聯的下列專案：

* [UGC](#user-generated-content)
* [用户组](#community-user-groups)
* [資料庫記錄](#database-records)

### 社群唯一網站ID {#community-unique-site-id}

若要使用CRXDE識別與社群網站相關聯的不重複網站ID：

* 導覽至網站的語言根目錄，例如 `/content/sites/*<site name>*/en/rep:policy`.

* 尋找 `allow<#>` 具有的節點 `rep:principalName` 在此格式中 `rep:principalName = *community-enable-nrh9h-members*`.

* 網站ID是的第三個元件 `rep:principalName`

   例如，如果 `rep:principalName = community-enable-nrh9h-members`

   * **網站名稱** = *啟用*
   * **網站ID** = *nrh9h*
   * **唯一網站ID** = *enable-nrh9h*

### 用户生成的内容 {#user-generated-content}

從Github取得communities-srp-tools專案：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

這包含一個servlet，可從任何SRP刪除所有UGC。

所有UGC都可移除，或針對特定網站進行，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

這只會移除使用者產生的內容（在發佈時輸入），而不會移除編寫的內容（在作者時輸入）。 因此， [陰影節點](srp.md#shadownodes) 則不受影響。

### 社群使用者群組 {#community-user-groups}

在所有作者和發佈執行個體上，從 [安全性主控台](../../help/sites-administering/security.md)，找到並移除 [使用者群組](users.md) 即：

* 前置詞為 `community`
* 後面接著 [唯一網站id](#community-unique-site-id)

例如：`community-engage-x0e11-members`。
