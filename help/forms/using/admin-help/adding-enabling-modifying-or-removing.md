---
title: 新增、啟用、修改或移除端點
seo-title: Adding, enabling, modifying, or removing endpoints
description: 瞭解如何新增、啟用、修改和移除端點。
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 新增、啟用、修改或移除端點 {#adding-enabling-modifying-or-removing-endpoints}

## 將端點新增至服務 {#add-an-endpoint-to-a-service}

端點只能新增到服務。 端點不能單獨存在；它必須與服務相關聯。

>[!NOTE]
>
>新增端點時，建議您使用唯一的名稱。

1. 在Administration Console中，按一下「服務>應用程式和服務>服務管理」。
1. 在「服務管理」頁面上，按一下要設定的服務。
1. 在「端點」標籤上的清單中，選取要新增的端點型別，然後按一下「新增」。
1. 根據端點型別，設定其他端點設定。

[Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[設定任務管理員端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[遠端端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 按一下「新增」。

## 啟用或停用端點 {#enable-or-disable-an-endpoint}

依預設，新端點會自動啟用。 但如果您已停用端點，則需要啟用它才能運作。

如果您遇到服務問題，請停用相關的端點，以便更妥善地疑難排解問題。 您也可以在定期系統維護或升級服務時停用端點。

1. 在Administration Console中，按一下「服務>應用程式和服務>端點管理」。
1. 在「端點管理」頁面上，選取要啟用或停用端點的核取方塊，然後按一下啟用或停用。

## 修改端點 {#modify-an-endpoint}

>[!NOTE]
>
>您使用管理主控台對端點設定所做的變更，不會反映在應用程式的設計階段復本中。 如果您重新部署應用程式，您使用管理主控台對其端點所做的任何變更都將遺失。

1. 在Administration Console中，按一下「服務>應用程式和服務>端點管理」。
1. 在「端點管理」頁面上，按一下要修改的端點。
1. 在「更新端點」頁面上，修改端點名稱、說明和設定。

   >[!NOTE]
   >
   >請勿在名稱或說明中加入&lt;字元，因為它會截斷工作區中顯示的名稱或說明。

1. 若要儲存變更，請按一下[更新]。

您也可以從「服務管理」頁面選取服務，然後按一下「端點」標籤，來執行此工作。

## 移除端點 {#remove-an-endpoint}

1. 在Administration Console中，按一下「服務>應用程式和服務>端點管理」。
1. 在「端點管理」頁面上，選取要移除之端點的核取方塊，然後按一下移除。 端點不再顯示。
