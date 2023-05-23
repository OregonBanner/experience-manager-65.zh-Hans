---
title: 防止CSRF攻擊
seo-title: Preventing CSRF attacks
description: 瞭解如何防止跨網站請求偽造(CSRF)攻擊，並保護使用者資料不被破壞。
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 防止CSRF攻擊 {#preventing-csrf-attacks}

## CSRF攻擊的運作方式 {#how-csrf-attacks-work}

跨網站請求偽造(CSRF)是一種網站漏洞，其中使用有效使用者的瀏覽器來傳送惡意請求，可能會透過iFrame。 由於瀏覽器會根據網域傳送Cookie，因此如果使用者目前登入應用程式，可能會危及使用者的資料。

例如，假設您登入瀏覽器中的管理主控台。 您會收到包含連結的電子郵件訊息。 按一下連結，即可在瀏覽器中開啟新標籤。 您開啟的頁面包含隱藏的iFrame，會使用已驗證的AEM表單工作階段的Cookie向表單伺服器提出惡意請求。 由於「使用者管理」會收到有效的Cookie，因此會傳遞請求。

## CSRF相關辭彙 {#csrf-related-terms}

**推薦者：** 要求來源頁面的位址。 例如，site1.com上的網頁包含site2.com的連結。 按一下連結即可將要求張貼至site2.com。 此請求的參照網址為site1.com ，因為請求是從來源為site1.com的頁面發出的。

**加入允許清單的URI：** URI會識別表單伺服器上正在要求的資源，例如/adminui或/contentspace。 某些資源可能會允許請求從外部網站進入應用程式。 這些資源會視為已加入允許清單的URI。 表單伺服器絕不會從允許清單中的URI執行反向連結檢查。

**Null查閱者：** 當您開啟新的瀏覽器視窗或Tab鍵，然後輸入地址並按Enter鍵時，引用為空。 此請求是全新請求，並非源自上層網頁；因此，此請求沒有反向連結。 表單伺服器可從下列位置接收Null參照：

* 在Acrobat的SOAP或REST端點上提出的請求
* 在AEM Forms SOAP或REST端點上提出HTTP請求的任何案頭使用者端
* 當開啟新的瀏覽器視窗並輸入任何AEM forms web應用程式登入頁面的URL時

在SOAP和REST端點上允許Null參照。 在所有URI登入頁面（例如/adminui和/contentspace）及其對應的對應資源上也允許null參照。 例如， /contentspace的對應servlet是/contentspace/faces/jsp/login.jsp，這應該是null參照例外狀況。 只有在啟用Web應用程式的GET篩選時，才需要此例外。 您的應用程式可以指定是否允許null反向連結。 請參閱以下主題中的「防範跨網站請求偽造攻擊」： [強化AEM表單及安全性](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**允許的反向連結例外狀況：** Allowed Referer Exception是允許的反向連結清單的子清單，其中會封鎖要求。 允許的「參考例外」專屬於Web應用程式。 如果「允許的反向連結」的子集不允許呼叫特定的Web應用程式，您可以透過「允許的反向連結例外」將反向連結加入封鎖清單。 在web.xml檔案中為您的應用程式指定允許的Referer例外。 (請參閱說明和Tutorials頁面上的AEM表單強化和安全性中的「防止跨網站請求偽造攻擊」。)

## 允許的反向連結如何運作 {#how-allowed-referers-work}

AEM forms提供參照篩選功能，可協助防止CSRF攻擊。 以下為參照篩選的運作方式：

1. 表單伺服器會檢查用於叫用的HTTP方法：

   * 如果是POST，表單伺服器會執行反向連結標題檢查。
   * 如果是GET，則表單伺服器會略過參考者檢查，除非CSRF_CHECK_GETS設定為true （在這種情況下，它會執行參考者標頭檢查）。 CSRF_CHECK_GETS是在應用程式的web.xml檔案中指定的。 (請參閱以下主題中的「保護免受跨網站請求偽造攻擊」： [強化與安全性指南](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. 表單伺服器會檢查請求的URI是否已加入允許清單：

   * 如果URI已加入允許清單，則伺服器會傳遞要求。
   * 如果請求的URI未列入允許清單，則伺服器會擷取請求的參照器。

1. 如果請求中有反向連結，伺服器會檢查其是否允許為反向連結。 如果允許，伺服器會檢查參照者例外狀況：

   * 若為例外狀況，則要求會被封鎖。
   * 如果不是例外，則會傳遞要求。

1. 如果請求中沒有反向連結，則伺服器會檢查是否允許null反向連結。

   * 如果允許空值參照，則會傳遞請求。
   * 如果不允許null參照器，則伺服器會檢查請求的URI是否是null參照器的例外，並據此處理請求。

## 設定允許的查閱者 {#configure-allowed-referers}

當您執行Configuration Manager時，預設主機和IP位址或表單伺服器會新增到允許的反向連結清單中。 您可以在管理控制檯中編輯此清單。

1. 在管理控制檯中，按一下「設定>使用者管理>設定>設定允許的反向連結URL」。「允許的反向連結」清單會顯示在頁面底部。
1. 若要新增允許的反向連結：

   * 在「允許的反向連結」方塊中輸入主機名稱或IP位址。 若要一次新增多個允許的查閱者，請在新行中輸入每個主機名稱或IP位址。
   * 在「HTTP連線埠」和「HTTPS連線埠」方塊中，指定允許使用HTTP、HTTPS或兩者的連線埠。 如果您將這些方塊留空，則會使用預設連線埠（HTTP為連線埠80，HTTPS為連線埠443）。 如果您輸入 `0` （零）在方塊中，會啟用該伺服器上的所有連線埠。 您也可以輸入特定的連線埠號碼，以僅啟用該連線埠。
   * 按一下「新增」。

1. 若要從[允許的反向連結]清單中移除專案，請從清單中選取專案，然後按一下[刪除]。

   如果「允許的參照者清單」是空的，則CSRF功能會停止運作且系統變得不安全。

1. 變更「允許的反向連結」清單後，重新啟動AEM表單伺服器。
