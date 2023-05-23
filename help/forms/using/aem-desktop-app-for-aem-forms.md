---
title: 適用於AEM Forms的AEM案頭應用程式
seo-title: AEM desktop app for AEM Forms
description: 適用於AEM Forms的AEM案頭應用程式
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 適用於AEM Forms的AEM案頭應用程式 {#aem-desktop-app-for-aem-forms}

AEM案頭應用程式可讓您將Adobe Experience Manager (AEM) Assets存放庫和AEM Forms二進位檔案對應到您系統上的網路目錄。 您可以在檔案總管中檢視同步的資產和二進位檔案，並視需要使用各種應用程式來編輯檔案。 除了檢視檔案之外，您也可以建立、上傳和刪除二進位檔案。 您也可以直接從軟體開啟、編輯和儲存檔案。 例如，您可以從Designer直接開啟和編輯XDP檔案。 您對本機資產所做的變更，會反映在AEM Assets存放庫和AEM Forms UI中。

您可以從AEM執行個體下載應用程式。 如需下載應用程式的詳細資訊，請參閱 [AEM案頭應用程式發行說明](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEM案頭應用程式支援的AEM Forms資產 {#aem-forms-assets-supported-in-aem-desktop-app}

您可以使用應用程式來同步下列型別的AEM Forms二進位檔案：表單範本(.xdp)、PDF表單(.pdf)、檔案(.pdf)、影像、XML結構描述(.xsd)、樣式表(.xfs)。 應用程式會將所有其他檔案（不支援的檔案）列為0位元組檔案。 將不支援的檔案列為0位元組檔案，可確保使用者知道AEM Forms伺服器上存在其他可用的資產。

>[!NOTE]
>
>檔案名稱只能包含英數字元、連字型大小或底線。

## 為AEM案頭應用程式啟用AEM Forms {#enable-aem-forms-for-aem-desktop-app}

AEM案頭應用程式在Microsoft Windows上使用WebDAV通訊協定，在Mac OS X上使用SMB1連線至AEM Forms伺服器。 開箱即用的AEM Forms伺服器不會將二進位檔案和其他資產與WebDAV或SMB使用者端同步。 執行以下步驟，為AEM案頭應用程式啟用AEM Forms：

1. 以管理員身分登入AEM Forms。
1. 在作者執行個體中，按一下 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager >工具]** ![槌子](assets/hammer.png) **[!UICONTROL >部署>作業> Web主控台]**. Web主控台會在新視窗中開啟。
1. 在Web主控台視窗中，找到並開啟 **[!UICONTROL FormsManager AddOn設定]** 選項。
1. 在FormsManager AddOn設定對話方塊中，取消選取 **[!UICONTROL 非同步同步資源]** 核取方塊，然後按一下 **[!UICONTROL 儲存]**.
1. 重新啟動AEM Forms伺服器。 重新啟動後，AEM Forms伺服器會啟用，以接受內容並與AEM案頭應用程式共用。
1. 開啟應用程式並連線至AEM Forms伺服器。

   成功連線時，應用程式會填入 `content/dam` 和 `content/dam/formsanddocuments` 資料夾。 除了將檔案從上方資料夾移至本機資料夾（反之亦然）外，您也可以使用應用程式在自動填入的資料夾之間移動內容。
