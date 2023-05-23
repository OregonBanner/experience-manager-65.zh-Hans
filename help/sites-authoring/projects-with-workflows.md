---
title: 使用项目工作流
seo-title: Working with Project Workflows
description: 各種專案工作流程都可立即使用。
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 15%

---


# 使用项目工作流 {#working-with-project-workflows}

現成可用的專案工作流程包括下列專案：

* **项目审批工作流** – 此工作流允许您将内容分配给用户进行审查和批准。
* **请求启动项** – 此工作流用于请求启动项。
* **请求登陆页面** – 此工作流用于请求登陆页面。
* **请求电子邮件** – 此工作流用于请求电子邮件。
* **產品拍照和產品拍照（商務）**  — 將資產與產品對應
* **DAM建立和翻譯副本及DAM建立語言副本**  — 為資產和資料夾建立翻譯的二進位檔案、中繼資料和標籤。

根據您選取的專案範本，您有特定的工作流程可用：

|  | **简单项目** | **媒体项目** | **產品拍照專案** | **翻译项目** |
|---|:-:|:-:|:-:|:-:|
| 請求復本 |  | x |  |  |
| 產品拍照 |  | x | x |  |
| 產品拍照（商務） |  |  | x |  |
| 專案核准 | x |  |  |  |
| 请求启动项 | x |  |  |  |
| 请求登陆页面 | x |  |  |  |
| 请求电子邮件 | x |  |  |  |
| DAM 创建语言副本&amp;ast; |  |  |  | x |
| DAM 创建和翻译语言副本&amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast;这些工作流不会从项目中的&#x200B;**工作流**&#x200B;拼贴启动。另請參閱 [建立資產的語言副本。](/help/sites-administering/tc-manage.md)

無論您選擇哪個工作流程，開始和完成工作流程的步驟都相同。 只有步驟會變更。

您直接在「專案」中啟動工作流程（「DAM建立語言副本」或「DAM建立和翻譯語言副本」除外）。 專案中任何未完成任務的資訊會列在 **任務** 圖磚。 使用者圖示旁會顯示需要完成之工作的通知。

如需在AEM中使用工作流程的詳細資訊，請參閱下列檔案：

* [参与工作流](/help/sites-authoring/workflows-participating.md)
* [将工作流应用于页面](/help/sites-authoring/workflows-applying.md)
* [配置工作流](/help/sites-administering/workflows.md)

此部分介绍了可用于项目的工作流。

## 請求複製工作流程 {#request-copy-workflow}

此工作流程可讓您向使用者請求手稿，然後核准它。 若要啟動請求複製工作流程：

1. 在媒體專案中，點選或按一下右上角的向下>形箭號 **工作流程** 並選取 **開始工作流程**.
1. 在工作流程精靈中選取 **請求復本** 並按一下 **下一個**.
1. 輸入手稿標題和您請求的簡短摘要。 如果適用，請輸入目標字數、作業優先順序和到期日。

   ![請求複製工作流程](assets/project-request-copy-workflow.png)

1. 按一下 **提交**.

工作流程隨即開始。 任務會顯示在 **任務** 卡片。

## 產品拍照工作流程 {#product-photo-shoot-workflow}

此 **產品拍照** 檔案中詳細說明了工作流程（商務和非商務） [創意專案](/help/sites-authoring/managing-product-information.md)

## 專案核准工作流程 {#project-approval-workflow}

在 **專案核准** 工作流程，您可以將內容指派給使用者、檢閱，然後核准內容。

1. 在簡單專案中，點選或按一下右上角的向下>形箭號 **工作流程** 並選取 **開始工作流程**.
1. 在工作流程精靈中選取 **專案核准工作流程** 並按一下 **下一個**.
1. 輸入標題並選取指派對象。 如果適用，請輸入說明、內容路徑、工作優先順序和到期日。

   ![專案核准工作流程](assets/project-approval-workflow.png)

1. 按一下 **提交**.

工作流程隨即開始。 任務會顯示在 **任務** 卡片。

## 請求啟動工作流程 {#request-launch-workflow}

此工作流程可讓您請求啟動。

1. 在簡單專案中，點選或按一下右上角的向下>形箭號 **工作流程** 並選取 **開始工作流程**.
1. 在工作流程精靈中選取 **請求啟動工作流程** 並按一下 **下一個**.
1. 輸入啟動項的標題並提供啟動項來源路徑。 您也可以新增說明和上線日期（如適用）。 選取繼承來源頁面即時資料或排除子頁面（取決於您希望啟動項的行為）。

   ![請求啟動工作流程](assets/project-request-launch-workflow.png)

1. 按一下 **提交**.

工作流程隨即開始。 工作流程會顯示在 **工作流程** 清單。

## 請求登入頁面工作流程 {#request-landing-page-workflow}

此工作流程可讓您請求登入頁面。

1. 在簡單專案中，點選或按一下右上角的向下>形箭號 **工作流程** 並選取 **開始工作流程**.
1. 在工作流程精靈中選取 **請求登陸頁面** 並按一下 **下一個**.
1. 輸入登入頁面的標題和父路徑。 如果適用，請輸入上線日期或選擇登陸頁面的檔案。

   ![請求登入頁面工作流程](assets/project-request-landing-page-workflow.png)

1. 按一下 **提交**.

工作流程隨即開始。 任務會顯示在 **任務** 卡片。

## 請求電子郵件工作流程 {#request-email-workflow}

此工作流程可讓您請求電子郵件。 此工作流程與出現在「 」中的 **電子郵件** 圖磚。

1. 在簡單專案中，點選或按一下右上角的向下>形箭號 **工作流程** 並選取 **開始工作流程**.
1. 在工作流程精靈中選取 **要求電子郵件** 並按一下 **下一個**.
1. 輸入電子郵件標題，以及行銷活動和範本路徑。 此外，您還可以提供名稱、說明和上線日期。

   ![請求電子郵件工作流程](assets/project-request-email-workflow.png)

1. 按一下 **提交**.

工作流程隨即開始。 任務會顯示在 **任務** 卡片。

## 为资产创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

此 **建立語言副本** 和 **建立和翻譯語言副本** 檔案中詳細說明了工作流程 [建立資產的語言副本。](/help/assets/translation-projects.md)
