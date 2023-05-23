---
title: 管理受邀和本機使用者帳戶
seo-title: Managing invited and local user accounts
description: 使用Document Security，您可以搜尋、檢視、編輯、鎖定、解鎖和刪除受邀和本機使用者帳戶。
seo-description: Using document security, you can search for, view, edit, lock, unlock, and delete invited and local user accounts.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# 管理受邀和本機使用者帳戶 {#managing-invited-and-local-user-accounts}

使用「受邀的使用者和本機使用者」頁面來管理您的受邀使用者和本機使用者。 只有在符合下列要求時，才會顯示此頁面：

* 您是已指派Document Security管理受邀和本機使用者角色和管理控制檯使用者角色的管理員。 (請參閱 [建立和設定角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* 已啟用受邀使用者註冊。 (請參閱 [設定受邀使用者註冊](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

「受邀和本機使用者」頁面包含兩個標籤，可用來搜尋、檢視、編輯、鎖定、解除鎖定和刪除受邀和本機使用者帳戶。

您也可以手動將註冊電子郵件傳送給受邀的使用者。 例如，如果電子郵件授權的註冊期結束，且使用者無法使用URL進行註冊，則您可能想要這麼做。 在這種情況下，您可以向受邀使用者重新傳送註冊電子郵件。 當受邀使用者註冊並啟動帳戶時，該使用者會成為本機使用者。

>[!NOTE]
>
>受邀使用者也可以直接透過檔案安全性參考的LDAP目錄新增，或者在使用者或管理員建立或編輯原則時邀請新使用者，因此啟動註冊邀請電子郵件時。 如果您在「受邀使用者註冊」頁面上啟用「啟用受邀使用者註冊」選項，使用者可以將新的受邀使用者新增到原則中。

## 新增受邀使用者 {#add-an-invited-user}

您可以一次新增一個或多個受邀使用者帳戶到Document Security。 若要新增受邀使用者帳戶，您需要該使用者的電子郵件地址。 當您新增使用者時，Document Security會傳送一封註冊電子郵件，邀請使用者註冊。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」，然後按一下「邀請新使用者」。
1. 輸入您要邀請之使用者的電子郵件地址。 在一行中輸入多個地址，以逗號分隔。

   您在啟用受邀使用者註冊時所建立的訊息會傳送給使用者。 (請參閱 [設定受邀使用者註冊](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. 单击确定。

## 檢視本機使用者的相關資訊 {#view-information-about-a-local-user}

您可以檢視本機使用者的相關資訊，包括名稱、電子郵件地址、組織、註冊狀態和網域。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」，然後按一下「邀請新使用者」。
1. 按一下「本機使用者」標籤，然後在「管理本機使用者」頁面上，按一下您要檢視之使用者的電子郵件地址。

   會顯示使用者詳細資訊，您可以重設使用者的密碼並停用帳戶。

## 傳送電子郵件給未註冊的外部使用者 {#send-an-email-to-an-unregistered-external-user}

當您新增受邀使用者時，Document Security會自動傳送註冊電子郵件請求給使用者。 您也可以手動產生註冊電子郵件，以傳送給尚未註冊的受邀使用者。 例如，如果受邀使用者的註冊電子郵件過期，您可能會想要執行此動作，以傳送新的邀請。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」。
1. 在使用者清單中，選取要傳送註冊電子郵件給每個使用者的核取方塊，然後按一下「重新傳送邀請電子郵件」。
1. 檢閱選取的使用者清單，然後按一下「確定」。

## 重設本機使用者密碼 {#reset-a-local-user-password}

您可以為已註冊Document Security但忘記密碼的已啟動受邀使用者重設密碼。 當您重設密碼時，會產生一封電子郵件，其中包含使用者的新臨時密碼。

當您啟用受邀使用者註冊程式時，您會建立電子郵件訊息，並傳送給使用者，提示他們重設密碼。 (請參閱 [設定受邀使用者註冊](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」 ，然後按一下「本機使用者」索引標籤。
1. 在使用者清單中，選取適當的使用者。
1. 在「管理本機使用者」頁面上，按一下「重設密碼」，然後按一下「確定」。 包含新密碼的重設密碼電子郵件會傳送給使用者。

## 啟用或停用使用者帳戶 {#enable-or-disable-a-user-account}

您可以停用本機使用者帳戶，暫時限制使用者登入Document Security。 當您停用帳戶時，使用者無法使用受原則保護的檔案，或建立或套用原則。

您可以啟用目前停用的本機使用者帳戶。 您無法啟用列示為已註冊的受邀使用者帳戶。 註冊狀態表示受邀使用者已註冊，但尚未使用啟用電子郵件中的連結啟用帳戶。

**限制使用者帳戶**

1. 在Administration Console中，按一下「服務> Document Security >受邀和本機使用者」 ，然後按一下「本機使用者」索引標籤。
1. 在使用者清單中，選取適當的使用者。
1. 在「本機使用者詳細資訊」頁面上，按一下「帳戶停用」。

**復原使用者帳戶**

1. 按一下「已邀請」和「本機使用者」，然後按一下「本機使用者」標籤。
1. 在使用者清單中，選取適當的使用者。
1. 在「本機使用者詳細資訊」頁面上，按一下「帳戶啟用」。

## 移除受邀使用者帳戶 {#remove-an-invited-user-account}

您可以從Document Security刪除受邀使用者帳戶。 例如，當使用者變更其個人電子郵件帳戶資訊時，您可能會想要刪除帳戶。

如果您刪除使用者帳戶，只有您或其他管理員可以透過在「受邀使用者」頁面上選取「新增受邀使用者」選項來恢復帳戶。 使用者無法將已刪除的使用者帳戶新增至原則，而且無法透過此方法啟動任何邀請程式。

>[!NOTE]
>
>透過AEM Forms使用者管理介面刪除的受邀使用者必須先透過下列程式再次刪除，才能重新啟用。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」 ，然後按一下「受邀使用者」索引標籤。
1. 選取一或多個使用者旁的核取方塊，按一下刪除，然後按一下確定。

## 搜尋受邀的使用者帳戶 {#search-for-an-invited-user-account}

您可以使用電子郵件地址來搜尋受邀的使用者帳戶。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」。
1. 在「尋找電子郵件」方塊中，輸入使用者的電子郵件地址，然後按一下「尋找」。

## 搜尋本機使用者帳戶 {#search-for-a-local-user-account}

您可以使用使用者的電子郵件地址或名稱和網域來搜尋本機使用者。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」 ，然後按一下「本機使用者」索引標籤。
1. 在「尋找」方塊中輸入搜尋條件，選取「名稱」或「電子郵件」，然後按一下「尋找」。

## 移除本機使用者帳戶 {#remove-a-local-user-account}

您可以從Document Security中刪除本機使用者帳戶。 例如，當使用者變更其個人電子郵件帳戶資訊時，您可能會想要刪除帳戶。

1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」 ，然後按一下「本機使用者」索引標籤。
1. 選取一或多個使用者旁的核取方塊，按一下刪除，然後按一下確定。

## 排序使用者清單 {#sort-the-user-list}

您可以依欄標題排序使用者清單，以更輕鬆地找到使用者。 欄標題旁邊的三角形圖示表示目前使用哪一欄來排序：

* 向上指的三角形表示遞增順序。
* 向下指的三角形表示遞減順序。

   1. 在管理控制檯中，按一下「服務> Document Security >受邀和本機使用者」。
   1. 若要排序受邀使用者，請按一下受邀使用者索引標籤，然後按一下適當的欄標題。
   1. 若要排序本機使用者，請按一下[本機使用者]索引標籤，然後按一下適當的欄標題。
