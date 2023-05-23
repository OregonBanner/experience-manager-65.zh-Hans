---
title: 設定憑證式驗證
seo-title: Configuring certificate-based authentication
description: 將憑證授權單位(CA)憑證匯入信任存放區，並建立憑證式驗證的憑證對應。
seo-description: Import a Certificate Authority (CA) certificate into the Trust Store and create a certificate mapping for certificate-based authentication.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 設定憑證式驗證 {#configuring-certificate-based-authentication}

「使用者管理」通常使用使用者名稱和密碼來執行驗證。 「使用者管理」也支援憑證式驗證，您可以透過Acrobat來驗證使用者，或以程式設計方式驗證使用者。 如需以程式設計方式驗證使用者的詳細資訊，請參閱 [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63).

若要使用憑證式驗證，請將您信任的憑證授權單位(CA)憑證匯入信任存放區，然後建立憑證對應。

## 匯入CA憑證 {#import-the-ca-certificate}

匯入憑證時，請選取「信任憑證驗證」和「信任身分」選項，以及您所需的任何其他選項。 如需有關匯入憑證的詳細資訊，請參閱 [管理憑證](/help/forms/using/admin-help/certificates.md#managing-certificates).

## 設定憑證對應 {#configuring-certificate-mapping}

若要為使用者啟用憑證式驗證，請建立憑證對應。 A *憑證對應* 定義憑證屬性與網域中使用者屬性之間的對應。 您可以將多個憑證對應至相同網域。

當您測試憑證時，「使用者管理」會上傳憑證檢查，以確保它符合下列要求：

* 憑證有效。
* 您指定的簽發者可以驗證憑證。
* 憑證包含對應所需的屬性。
* 您指定的對應只會將憑證對應到AEM表單資料庫中的一個使用者。 系統會檢查目前和過時（已刪除）的使用者，以確定他們是否符合對應條件。 因此，如果有多位使用者（包括過時的使用者）考量到屬性值，憑證測試就會失敗。

>[!NOTE]
>
>您無法編輯現有的憑證對應。

**新增憑證對應**

1. 在管理控制檯中，按一下「設定>使用者管理>設定>憑證對應」。
1. 按一下「新增憑證對應」，然後在「核發者」清單中，選取在「信任存放區管理」中設定的憑證別名。
1. 將憑證的其中一個屬性對應到使用者的屬性。 例如，您可以將憑證的一般名稱對應到使用者的登入ID。

   如果憑證中屬性的內容與「使用者管理」資料庫中使用者屬性的內容不同，您可以使用Java規則運算式(regex)來比對這兩個屬性。 例如，如果憑證的一般名稱是類似以下的名稱 *Alex Pink （驗證）* 和 *Alex Pink （簽署）* 而「使用者管理」資料庫中的一般名稱是 *亞歷克斯·平克*，您會使用規則運算式來擷取憑證屬性的必要部分(在此範例中， *亞歷克斯·平克*.) 您指定的規則運算式必須符合Java規則運算式規格。

   您可以在「自訂順序」方塊中指定群組的順序，以轉換運算式。 自訂順序會與 `java.util.regex.Matcher.replaceAll()` 方法。 看到的行為將對應至該方法的行為，且必須相應地指定輸入字串（自訂順序）。

   若要測試規則運算式，請在「測試引數」方塊中輸入值，然後按一下「測試」。

   您可以在規則運算式中使用下列字元：

   * 。（任何字元）
   * &amp;ast； （0次或更多次）
   * () （以方括弧指定群組）
   * \ （用來將規則運算式字元逸出為一般字元）
   * $n （用於指稱第n個群組）

   規則運算式的範例：

   * 將「Alex Pink」從「Alex Pink （驗證）」中擷取

      **規則運算式：** (.&amp;ast；) \（驗證\）

   * 將「Alex Pink」從「Alex (Authentication) Pink」中擷取

      **規則運算式：** (.&amp;ast；)\（驗證\） (.&amp;ast；)

   * 將「Pink Alex」從「Alex (Authentication) Pink」中擷取

      **規則運算式：** (.&amp;ast；)\（驗證\） (.&amp;ast；)

      自訂順序： $2 $1 （傳回第二個群組，串連至第一個群組，以空白字元擷取）

   * 若要從「smtp：apink@sampleorg.com」擷取「apink@sampleorg.com」

      **規則運算式：** smtp：(.&amp;ast；)
   如需使用規則運算式的詳細資訊，請參閱 [關於規則運算式的Java教學課程](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. 在「針對網域」清單中，選取使用者的網域。
1. 若要測試此設定，請按一下[瀏覽]上傳範例使用者憑證，按一下[測試憑證]，如果設定正確，請按一下[確定]。

**編輯現有的憑證對應**

1. 在Administration Console中，按一下「設定>使用者管理>設定」。
1. 按一下「憑證對應」。
1. 選取要編輯和編輯其設定的憑證對應。 您可以更新規則運算式和自訂順序。
1. 若要測試變更，請按一下[瀏覽]上傳範例憑證、按一下[測試憑證]，然後按一下[確定]。

**刪除憑證對應**

1. 在管理控制檯中，按一下「設定>使用者管理>設定>憑證對應」。
1. 選取要刪除的憑證對應核取方塊，按一下刪除，然後按一下確定。
