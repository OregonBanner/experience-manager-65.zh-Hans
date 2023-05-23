---
title: 新增和設定使用者
seo-title: Adding and configuring users
description: 管理控制檯中的「使用者管理」設定可讓您建立或刪除使用者，以及設定其他使用者設定。
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# 新增和設定使用者 {#adding-and-configuring-users}

使用者和群組資訊會儲存在協力廠商儲存系統中，例如LDAP目錄。 「使用者管理」不會寫入協力廠商儲存系統。 相反地，「使用者管理」會將使用者和群組資訊與其自己的資料庫同步

## 建立使用者 {#create-a-user}

建立使用者時，您可以將使用者新增至群組並指派角色給使用者。

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**，然後按一下 **[!UICONTROL 新使用者]**..
1. 下 **[!UICONTROL 一般設定]**，視需要提供資訊，然後按一下 **[!UICONTROL 下一個]**. 如需設定的詳細資訊，請參閱 [使用者設定](adding-configuring-users.md#user-settings).
1. （可選）若要將使用者新增至群組，請按一下 **[!UICONTROL 尋找群組]**，然後執行下列工作：

   * 在 **[!UICONTROL 尋找]** 方塊中，輸入全部或部分群組名稱。
   * 選取要搜尋的網域、選取要顯示的專案數，然後按一下 **[!UICONTROL 尋找]**.
   * （選擇性）若要檢視群組詳細資訊，請選取群組名稱，然後按一下 **[!UICONTROL 確定]** 以返回搜尋結果頁面。
   * 選取群組的核取方塊並按一下 **[!UICONTROL 確定]**.
   * 单击&#x200B;**[!UICONTROL 下一步]**。

1. （可選）若要指派角色給使用者，請按一下 **[!UICONTROL 尋找角色]**，選取要指派的角色核取方塊，然後按一下 **[!UICONTROL 確定]**.
1. 按一下 **[!UICONTROL 完成]**.

   >[!NOTE]
   >
   >如果您發現使用者的任何登入問題，請參閱 [JEE版AEM Forms使用者無法登入OSGi端的AEM Forms](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## 用户设置 {#user-settings}

在建立或編輯使用者時，請指定下列設定。

**正式名稱：** （必要）使用者的唯一識別碼。 網域中的每個使用者和群組都必須有唯一的規範名稱。 選取「系統產生」核取方塊，讓「使用者管理」指派唯一值，或清除核取方塊並指定「標準名稱」的自訂值。

避免在正式名稱中使用底線字元(_)，例如， `sample_user`. 當您根據使用者的正式名稱搜尋使用者時，不會傳回包含底線字元的使用者。

**名字：** （必要）使用者的名字

**姓氏：** （必要）使用者姓氏

**一般名稱：** 使用者的完整名稱或顯示名稱。 例如，如果名字= Gloria，姓氏= Rios，則一般名稱= Gloria Rios。

**電子郵件：** 使用者的電子郵件地址

**電話：** 使用者電話號碼

**說明：** 選擇性說明。 請根據貴組織的需求使用此欄位。

**地址：** 使用者的郵寄地址

**組織：** 使用者所屬的組織

**電子郵件別名：** 使用者的電子郵件別名。 以逗號分隔電子郵件別名。

**網域：** 使用者所屬的網域

**地區設定：** 使用者的ISO地區設定

**商務行事曆索引鍵：** 可讓您根據此設定的值，將商業行事曆對應至使用者。 商務行事曆定義商務和非商務日。 AEM表單可在計算事件（例如提醒、截止日期和呈報）的未來日期和時間時，使用商業行事曆。 指派商務行事曆金鑰給使用者的方式取決於您是使用企業、本機或混合網域。 (請參閱 [新增網域](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

如果您使用本機或混合式網域，有關使用者的資訊只會儲存在「使用者管理」資料庫中。 對於這些使用者，請將商務行事曆索引鍵設定為字串。 然後將商務行事曆索引鍵（字串）對應至表單工作流程中的商務行事曆。

如果您使用企業網域，有關使用者的資訊會儲存在協力廠商儲存系統中，例如LDAP目錄。 「使用者管理」會將目錄中的使用者資訊與「使用者管理」資料庫同步。 此功能可讓您將商務行事曆索引鍵對應到LDAP目錄中的欄位。 例如，假設目錄中的每個使用者記錄都包含國家/地區欄位，而您想要根據使用者所在的國家/地區來指派業務行事曆。 在此情況下，您可以指定國家/地區欄位名稱作為商務行事曆索引鍵設定的值。 然後，您可以將商務行事曆索引鍵（為LDAP目錄中的國家/地區欄位定義的值）對應至表單工作流程中的商務行事曆。

如需商務行事曆的其他資訊，包括如何將商務行事曆索引鍵對應至商務行事曆，請參閱 [設定商務行事曆](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

將名稱限制在53個字元以下。 較短的名稱有助於防止在管理控制檯的「程式管理」頁面中顯示商務行事曆索引鍵時發生問題。

**使用者ID：** （必要）使用者用來登入的使用者ID。 使用者ID不區分大小寫，而且在整個網域中必須是唯一的。

在企業網域中，使用非DN屬性作為使用者ID，因為使用者的DN如果移至組織的其他部分，可能會變更。 此設定視目錄伺服器而定。 值為 `objectGUID` 對於Active Directory 2003， `nsuniqueID` 適用於Sun™ One和 `guid` 適用於eDirectory。

確保使用者ID是唯一的。 請勿使用已指派給已刪除使用者的密碼。

AEM forms無法區分擁有相同使用者ID和密碼但屬於不同網域的使用者帳戶。 為避免此問題，請勿在多個網域上建立具有相同使用者ID的帳戶。

使用SQL Server作為資料庫時，您無法建立超過255個字元的使用者ID。

使用MySQL時，使用者ID可以包含擴充字元。 不過，比較兩個字串（例如abcde和abcde）時，會將其視為相同。 例如，同步時，如果資料庫中新增了新使用者，則會進行比較以檢查資料庫中是否存在具有相同使用者ID的使用者。 若為使用者 *abcde* 當新使用者存在資料庫中時 *abcde* 新增，比較無法區分這兩個名稱。 假設使用者存在於資料庫中，而新使用者會被忽略且不會新增。

請避免建立以數字元號(#)開頭的使用者名稱。 執行任務搜尋不會傳回這些使用者名稱的結果。 (請參閱 [使用任務](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**密碼和確認密碼：** 使用者用來登入的密碼。 至少必須有8個字元。 屬於混合網域的使用者不需要密碼。

## 檢視關於使用者的詳細資訊 {#view-details-about-a-user}

1. 在管理控制檯中，按一下「設定>使用者管理>使用者和群組」。
1. 指定資訊以縮小搜尋範圍，並在「輸入」清單中選取「使用者」，然後按一下「尋找」。 搜尋結果會列在頁面底部。 您可以按一下任何欄標題來排序清單。
1. 按一下使用者的名稱以顯示相關的詳細資訊。 「編輯使用者」頁面會顯示下列有關使用者的詳細資訊：

   * 一般識別資訊，例如，名稱、電子郵件、地址、網域和組織
   * 指派給使用者的角色
   * 使用者所屬的群組

## 變更本機使用者的密碼 {#change-the-password-for-a-local-user}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 指定資訊以縮小特定使用者的搜尋範圍，然後按一下 **[!UICONTROL 尋找]**. 搜尋結果會列在頁面底部。 您可以按一下任何欄標題來排序清單。
1. 按一下使用者名稱，然後按一下 **[!UICONTROL 變更密碼]**.
1. 輸入並確認新密碼，然後按一下 **[!UICONTROL 確定]**. 密碼必須至少為八個字元。

## 編輯使用者的屬性 {#edit-a-user-s-properties}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 若要尋找要編輯的使用者，請執行下列工作：

   * 在 **[!UICONTROL 尋找]** 方塊中，輸入您的搜尋條件。
   * 在 **[!UICONTROL 使用]** 清單，選取 **[!UICONTROL 名稱]**， **[!UICONTROL 電子郵件]**，或 **[!UICONTROL 使用者ID]**.
   * 在 **[!UICONTROL 在清單中]**，選取 **[!UICONTROL 使用者]**.
   * 選取網域、選取要顯示的專案數，然後按一下 **[!UICONTROL 尋找]**.

1. 按一下要編輯的使用者。
1. 若使用者屬於本機或混合式網域，請在 **[!UICONTROL 詳細資訊]** 標籤，編輯 **[!UICONTROL 一般設定]** 和 **[!UICONTROL 登入設定]**，然後按一下 **[!UICONTROL 儲存]**. 如需設定的詳細資訊，請參閱 [使用者設定](adding-configuring-users.md#user-settings). 您無法編輯屬於企業網域的使用者的一般和登入設定。
1. 若要編輯使用者的群組設定，請按一下 **[!UICONTROL 群組成員資格]** 標籤並執行下列工作：

   * 按一下 **[!UICONTROL 尋找群組]** 並完成搜尋資訊。
   * 若要將使用者新增至新群組，請選取群組的核取方塊，然後按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 儲存]**.

   >[!NOTE]
   >
   >無法將本機使用者新增至目錄群組。 不過，目錄使用者可以新增至本機群組。

   * 若要從群組移除使用者，請選取群組的核取方塊，然後按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 儲存]**.


1. 若要編輯使用者的角色，請按一下 **[!UICONTROL 角色指派]** 標籤並執行下列工作：

   * 若要顯示角色清單，請按一下 **[!UICONTROL 尋找角色]**.
   * 若要新增角色，請選取該角色的核取方塊，然後按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 儲存]**.
   * 若要移除角色，請選取該角色的核取方塊，然後按一下 **[!UICONTROL 取消指派]**，然後按一下 **[!UICONTROL 儲存]**.

## 刪除使用者 {#delete-a-user}

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>使用者和群組]**.
1. 若要尋找要刪除的使用者，請執行下列工作：

   * 在 **[!UICONTROL 尋找]** 方塊中，輸入您的搜尋條件。
   * 在 **[!UICONTROL 使用]** 清單，選取 **[!UICONTROL 名稱]**， **[!UICONTROL 電子郵件]**，或 **[!UICONTROL 使用者ID]**.
   * 在 **[!UICONTROL 在清單中]**，選取 **[!UICONTROL 使用者]**.
   * 選取網域、選取要顯示的專案數，然後按一下 **[!UICONTROL 尋找]**.

1. 選取使用者的核取方塊，按一下 **[!UICONTROL 刪除]**，然後按一下 **[!UICONTROL 確定]**.

>[!NOTE]
>
>JEE上的AEM Forms也可讓在OSGi上執行的AEM Forms附加元件的使用者辨識為AEM使用者。 在JEE上的AEM Forms與在OSGi上執行的AEM Forms附加元件之間需要單一登入的情況(例如，HTML工作區)需要此專案。 上述刪除操作只會從JEE上的AEM Forms中移除使用者。 系統不會從OSGi環境上執行的AEM Forms附加元件中刪除使用者。 但是在刪除使用者後所做的任何登入嘗試(登入嘗試AEM Forms附加元件JEE伺服器或AEM Forms附加元件OSGi環境)都遭到拒絕。

## 建立自訂登入錯誤處理常式 {#create-custom-login-error-handler}

如果使用者沒有必要的AEM表單和CQ許可權，嘗試登入以下內嵌在CQ中的應用程式，使用者將被重新導向到包含錯誤追蹤的預設CQ 404頁面：

* 通訊管理解決方案
* AEM Forms工作區

   ***注意&#x200B;**：AEM Forms版本已棄用Flex Workspace。*

* 表單管理員
* 程式報告

CQ提供覆寫預設404處理常式jsp的機制。

如需有關如何自訂錯誤處理頁面的詳細資訊，請參閱 [自訂錯誤處理常式顯示的頁面](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) (位於Adobe Experience Manager檔案中)。
