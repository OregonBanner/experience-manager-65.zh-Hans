---
title: 設定目錄
seo-title: Configuring directories
description: 瞭解如何新增、編輯和刪除目錄以及設定使用者管理以使用虛擬清單檢視。
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 0%

---

# 設定目錄 {#configuring-directories}

針對您設定的每個企業網域，指定驗證提供者查詢使用者資訊的目錄。 您可以為一個網域設定多個目錄。

## 新增目錄或自訂SPI {#adding-directories-or-custom-spis}

針對您設定的每個企業網域，指定驗證提供者查詢使用者資訊的目錄。 您可以將目錄新增至現有的企業網域或您正在新增的新企業網域。 您可以為一個網域設定多個目錄。 您也可以設定網域以使用自訂服務提供者介面(SPI)進行同步。

### 新增目錄 {#add-a-directory}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增企業網域」或選取現有的企業網域。
1. 按一下「新增目錄」。
1. 在「設定檔名稱」方塊中，輸入名稱以區分此目錄，然後按一下「下一步」。
1. 設定目錄伺服器設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 若要確認可以連線到LDAP伺服器，請按一下[測試]。 如果測試失敗，請檢閱應用程式伺服器記錄檔中的例外狀況，以判斷失敗的根本原因。 按一下關閉，然後按下一步。
1. 選取「使用者設定」並視需要設定設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 若要確認基本DN和其他已設定的屬性是否收集正確的使用者批次，請按一下「測試」。 LDAP會嘗試使用提供的設定（例如基本DN、搜尋篩選器和所有屬性）來擷取前200筆記錄。

   如果傳回使用者，結果會顯示根據屬性集指派給每個欄位的值。 如果測試因伺服器名稱不存在、授權資訊不正確或屬性不正確而失敗，則會出現下列錯誤訊息：「指定的搜尋條件未傳回任何結果」。 若要判斷失敗的根本原因，請檢閱應用程式伺服器記錄檔中的例外狀況。 按一下關閉，然後按下一步。

1. 選取「群組設定」，並視需要設定設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 若要確認基本DN和其他已設定的屬性是否收集正確的群組批次，請按一下[測試]。 如果傳回群組，結果會顯示根據屬性集指派給每個欄位的值。 单击关闭。

### 新增自訂SPI {#add-a-custom-spi}

如需建立自訂SPI的相關資訊，請參閱以下的「為AEM表單開發SPI」： [使用AEM表單程式設計](https://www.adobe.com/go/learn_aemforms_programming_63). 若要使新部署的自訂SPI可與網域相關聯，請重新啟動伺服器。

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增企業網域」或選取現有的企業網域。
1. 按一下「新增目錄」。
1. 在「設定檔名稱」方塊中輸入名稱，選取「自訂SPI提供者」，然後按一下「下一步」。
1. 從清單中選取自訂使用者提供者，然後按一下「下一步」。
1. 從清單中選取自訂群組提供者，然後按一下[完成]。

## 編輯目錄 {#edit-a-directory}

您可以編輯先前設定之目錄的詳細資訊。

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中適當的網域，然後在出現的頁面上，從清單中選取適當的目錄。
1. 視需要設定目錄、使用者和群組設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 单击确定。

## 刪除目錄 {#delete-a-directory}

當您在刪除目錄後同步化網域時，該目錄中的所有使用者和群組在資料庫中都會標示為過時。 它們不會從管理控制檯的任何搜尋中傳回。

>[!NOTE]
>
>企業網域至少需要一個驗證提供者和目錄提供者。

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中適當的網域。
1. 選取適當目錄的核取方塊，然後按一下「刪除」。
1. 在出現的確認頁面上按一下「確定」，然後再次按一下「確定」。

## 目錄設定 {#directory-settings}

將目錄新增至網域時，請指定下列目錄設定。

**伺服器：** （必要）目錄伺服器的完整網域名稱(FQDN)。 例如，在adobe.com網路上名為x的電腦，FQDN是x.adobe.com。 可以使用IP位址取代FQDN伺服器名稱。

**連線埠：** （必要）目錄伺服器使用的連線埠。 通常為389，如果安全通訊端層(SSL)通訊協定用於透過網路傳送驗證資訊，則為636。

**SSL：** （必要）指定在透過網路傳送資料時，目錄伺服器是否使用SSL。 預設值為「否」。 設定為Yes時，應用程式伺服器的Java™執行階段環境(JRE)必須信任對應的LDAP伺服器憑證。

**繫結** （必要）指定存取目錄的方式。

**匿名：** 不需要使用者名稱或密碼。 匿名使用者可能只能擷取有限數量的資料。 此選項可能對初始測試很有用。

**使用者：** 需要驗證。 在「名稱」方塊中，指定可存取目錄的使用者記錄名稱。 最好輸入使用者帳戶的完整辨別名稱(DN)，例如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」方塊中，指定相關的密碼。 當您選取「使用者」作為「繫結」選項時，需要這些設定。

**名稱：** 未啟用匿名存取時，可用來連線至LDAP資料庫的名稱。 對於Active Directory 2003，請指定 `[domain name]\[userid]`. 對於Sun™ One、eDirectory或IBM Tivoli Directory Server，請指定使用者的完整名稱，例如uid=lcuser，ou=it，o=company.com。

**密碼：** 在未啟用匿名存取時，與您指定連線至LDAP資料庫的名稱對應的密碼。

**頁面填入：** 選取後，會使用對應的預設LDAP值填入「使用者」和「群組」設定頁面上的屬性。

**擷取基本DN：** 擷取基本DN並在下拉式清單中顯示它們。 當您有多個基本DN且需要選取值時，此設定很有用。

**啟用轉介：** 當您的組織使用以階層式結構組織的多個Active Directory網域，而且您只為父系網域指定了目錄設定時，此設定適用。 在此情況下，當您選取此選項時，「使用者管理」可以從子網域存取使用者和群組詳細資訊。

>[!NOTE]
>
>按一下[測試]以確認可以連線到LDAP伺服器。 若要判斷任何失敗的根本原因，請檢閱應用程式伺服器記錄檔中的例外狀況。

### 用户设置 {#user-settings}

**唯一識別碼：** （必要）用於識別使用者的唯一且常數屬性。 使用非DN屬性作為唯一識別碼，因為使用者的DN可能會隨著他們移至組織的其他部分而變更。 此設定視目錄伺服器而定。 該值是Active Directory 2003的objectGUID、Sun™ One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>請確定您輸入的屬性在組織中必定是唯一的。 輸入不正確的值可能會導致嚴重的系統問題。

**基本DN：** 設定為從LDAP階層同步化使用者和群組的起點。 最好在階層的最低層級指定基本DN，該階層包含需要同步處理服務的所有使用者和群組。

如果您在「目錄」設定中選取了「啟用參照」選項，請將「基本DN」選項設定為 *dc* DN的一部分。 若要讓反向連結運作，搜尋範圍必須包含父網域和子網域。

>[!NOTE]
>
>請勿在此設定中包含使用者的DN。 若要同步特定使用者，請使用「搜尋篩選器」設定。

雖然Base DN是Administration Console中的必要設定，但某些目錄伺服器(例如IBM Domino Enterprise Server)可能需要空的BaseDN。 若要指定空的基本DN，請匯出config.xml檔案、編輯config.xml檔案中的設定，然後重新匯入它。 (請參閱 [匯入和匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜尋篩選器：** （必要）用來尋找與使用者相關聯之記錄的搜尋篩選器。 您可以執行一個層級搜尋或子層級搜尋。 （請參閱搜尋篩選器語法或RFC 2254。） 如需Microsoft AD架構的其他資訊，請參閱Active Directory架構。

**說明：** 使用者說明的結構描述屬性

**全名：** （必要）使用者完整名稱的結構描述屬性

**登入ID：** （必要）使用者登入ID的結構描述屬性

**姓氏：** （必要）使用者姓氏的結構描述屬性

**名字：** （必要）使用者名字的結構描述屬性

**首字母：** 使用者縮寫的結構描述屬性

**商務行事曆：** 可讓您根據此設定的值（商務行事曆索引鍵），將商務行事曆對應至使用者。 商務行事曆定義商務和非商務日。 AEM表單可在計算事件（例如提醒、截止日期和呈報）的未來日期和時間時，使用商業行事曆。 指派商務行事曆金鑰給使用者的方式取決於您是使用企業網域、本機網域或混合網域。 （請參閱設定商務行事曆）。

如果您使用企業網域，可以將「商務行事曆」設定對應到LDAP目錄中的欄位。 例如，如果目錄中的每個使用者記錄包含 *國家/地區* 欄位，而您想要根據使用者所在的國家/地區指派商務行事曆，請指定 *國家/地區* 欄位名稱作為「商業行事曆」設定的值。 然後，您可以對應業務行事曆索引鍵(為以下專案定義的值： *國家/地區* LDAP目錄中的欄位)至表單工作流程中的商務行事曆。

在表單工作流程頁面中顯示商務行事曆索引鍵名稱的空間量有限。 將商務行事曆索引鍵名稱限製為少於53個字元，以避免在這些頁面上截斷它。

**修改時間戳記：** 若要啟用差異目錄同步處理，請設定此值，以修改時間戳記。 （請參閱啟用差異目錄同步處理。）

**組織：** 使用者所屬組織名稱的結構描述屬性。

**主要電子郵件：** 使用者主要電子郵件地址的結構描述屬性。

**次要電子郵件：** 使用者次要電子郵件地址的結構描述屬性。

**電話：** 使用者電話號碼的結構描述屬性。

**郵寄地址：** 使用者郵寄地址的結構描述屬性。

**地區設定：** 包含ISO地區設定資訊的結構描述屬性。 值是兩個字母的語言代碼，或是語言和國家/地區代碼。

**時區：** 包含使用者所在時區的結構描述屬性。 值是字串，例如「城市/國家」。

**啟用虛擬清單檢視(VLV)控制：** LDAP控制項，可讓AEM表單從目錄伺服器以批次擷取資料。 如果您使用Sun One作為LDAP目錄，而且該目錄包含許多使用者，則啟用VLV會建立「使用者管理」在搜尋使用者時可以使用的索引。 當使用只能同步有限數量資料的正常使用者帳戶時，此功能會很有用。 您也可以為群組啟用VLV。 如果您選取「啟用虛擬清單檢視(VLV)控制項」，請在「排序欄位」方塊中指定名稱。

>[!NOTE]
>
>若要啟用VLV，請設定Sun One。 另請參閱 [設定使用者管理以使用虛擬清單檢視(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序欄位：** 如果您選取「啟用虛擬清單檢視(VLV)控制」，請指定用來排序索引的屬性名稱。 此屬性名稱（例如uid）是您在目錄伺服器上建立VLV索引時指定的名稱。

### 群組設定 {#group-settings}

**唯一識別碼：** （必要）用於識別群組的唯一和常數屬性。 使用非DN屬性作為唯一識別碼。 此設定視目錄伺服器而定。 值是Active Directory 2003的objectGUID、Sun One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>請確定您輸入的屬性在組織中必定是唯一的。 輸入不正確的值可能會導致嚴重的系統問題。

**基本DN：** （必要）目錄的基本辨別名稱。

雖然Base DN是Administration Console中的必要設定，但某些目錄伺服器(例如IBM Domino Enterprise Server)需要空的BaseDN。 若要指定空的基本DN，請匯出config.xml檔案、編輯config.xml檔案中的設定，然後重新匯入它。 (請參閱 [匯入和匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜尋篩選器：** （必要）用來尋找與群組相關聯之記錄的搜尋篩選器。 您可以執行一個層級搜尋或子層級搜尋。

**說明：** 群組說明的結構描述屬性

**全名：** （必要）群組完整名稱的結構描述屬性

**成員DN：** （必要）群組內成員辨別名稱的結構描述屬性

**成員唯一識別碼：** 屬於所選群組之成員的使用者或群組的唯一識別碼。 此值取決於目錄伺服器。 該值是AD2003的objectSID、Sun One的nsuniqueID和eDirectory的guid。

如果以非DN屬性指定「成員DN」，「使用者管理」會使用「成員唯一識別碼」來查詢LDAP，以收集與唯一識別碼值對應的使用者DN。

如果DN被指定為唯一識別碼，您就不需要設定「成員唯一識別碼」。

**組織：** 群組所屬組織名稱的結構描述屬性

**主要電子郵件：** 群組主要電子郵件地址的結構描述屬性

**次要電子郵件：** 群組的次要電子郵件地址的結構描述屬性

**修改時間戳記：** 若要啟用差異目錄同步處理，請設定此值，以修改時間戳記。 （請參閱啟用差異目錄同步處理。）

**啟用虛擬清單檢視(VLV)控制：** LDAP控制項，可讓AEM表單從目錄伺服器以批次擷取資料。 如果您使用Sun One作為LDAP目錄，而且該目錄包含許多群組，則啟用VLV會建立「使用者管理」在搜尋群組時可以使用的索引。 當使用只能同步有限數量資料的正常使用者帳戶時，此功能會很有用。 您也可以為使用者啟用VLV。 如果您選取「啟用虛擬清單檢視(VLV)控制項」，請指定「排序欄位名稱」。

>[!NOTE]
>
>若要啟用VLV，請設定Sun One。 另請參閱 [設定使用者管理以使用虛擬清單檢視(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序欄位名稱：** 如果您選取「啟用虛擬清單檢視(VLV)控制」，請指定用來排序索引的屬性名稱。 此屬性名稱是您在目錄伺服器上建立VLV索引時所指定的名稱。

>[!NOTE]
>
>按一下「測試」 ，確認是根據基本DN和搜尋條件收集使用者和群組設定。

如果傳回使用者和群組，結果會顯示根據屬性集指派給每個欄位的值。

>[!NOTE]
>
>「使用者管理」不支援網域內的重複使用者ID；只會同步處理一個具有使用者ID的使用者。

## 設定使用者管理以使用虛擬清單檢視(VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

目錄同步是User Management的重要需求。 使用者和群組會從企業目錄同步至AEM Forms資料庫，以指派角色和許可權。 使用者人數依需求從100到100000+不等，因此有效同步資料是一項工程挑戰。

LDAP通訊協定提供使用要求控制項，以分頁方式查詢大型資料集的機制。 使用Microsoft Active Directory時，LDAP到AEM表單資料庫同步處理會使用PagedResultsControl來擷取特定大小批次的資料。 Sun ONE Directory Server不支援此控制項。 若要針對Sun ONE Directory Server完成分頁查詢，請使用「虛擬清單檢視」(VLV)控制項。 此控制項包含目錄伺服器端設定和使用者端實作。

>[!NOTE]
>
>本節說明如何將VLV控制項用於Sun ONE Directory Server。 不過，您可以將此控制項用於支援VLV控制項的任何目錄伺服器。

1. 設定目錄時，請在「使用者設定」頁面和「群組設定」頁面上選取「啟用虛擬清單檢視(VLV)控制」。 當您選取核取方塊時，您也必須在「排序欄位」方塊中指定排序名稱。 預設值為uid。 (請參閱 [新增目錄或自訂SPI](configuring-directories.md#adding-directories-or-custom-spis) 或 [編輯目錄](configuring-directories.md#edit-a-directory).)
1. 使用Sun ONE管理主控台或命令列指令碼來建立使用者和群組的LDAP VLV專案。 如果您使用命令列指令碼，則可以使用範例使用者和群組LDIF檔案。 (請參閱 [為VLV設定Sun ONE Directory Server](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. 停止伺服器並建立必要的索引。 (請參閱 [建立VLV的目錄伺服器索引](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### 為VLV設定Sun ONE Directory Server {#configuring-the-sun-one-directory-server-for-vlv}

建立VLV需要一組包含 `vlvSearch` 和 `vlvIndex` 物件類別。 vlvSearch專案包含搜尋基礎與 `vlvFilter` attribute，指定包含您要排序之屬性的物件類別。 此 `vlvIndex` 物件類別包含 `vlvSort` 屬性，指定要排序的一或多個屬性，以及排序這些屬性的順序。 (減號(-)表示反字母順序)。 搭配AEM表單使用VLV時，使用者和群組需要個別的專案。

>[!NOTE]
>
>可以使用Sun ONE圖形化使用者介面(GUI)或命令列指令碼來建立Object專案。 如需使用GUI建立Object專案的指示，請參閱Sun ONE檔案。

以下是使用者的VLV專案指令碼LDIF範例：

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**使用指令碼建立物件專案**

1. 範例指令碼有一個名為的LDAP專案 `lcuser`. 此專案用於AEM表單中使用者同步的VLV相關設定。 請相應地修改以下屬性：

   **專案名稱：** 此範例中的專案名稱是 `lcuser`. 若 `lcuser` ，則必須在範例指令碼的所有區域中加以變更。

   **vlvBase：** 在「使用者設定」頁面上指定的基本DN。

   **vlvFilter：** 「使用者設定」頁面上指定的「搜尋篩選」。

   **vlvSort：** 「使用者設定」頁面的「VLV設定」區段中指定的「排序欄位」。 VLV控制項需要您指定排序控制項。 此欄位會用作已建立vlv索引的排序引數。

   **aci：** 範例指令碼中指定的存取控制可授予任何已驗證身分的使用者存取VLV索引的權利，以進行讀取、搜尋和比較作業。 管理員可以限制繫結使用者的存取權，此繫結使用者是在「使用者管理」使用者介面中指定的「目錄伺服器設定」頁面中設定的。 如果未提供許可權，使用者搜尋無法使用VLV，且LDAP伺服器擲回許可權例外狀況。

   >[!NOTE]
   >
   >根據慣例，vlvIndex專案名稱也會設為 `lcuser`，但您可以為其指定其他名稱。 在vlvindex工具中使用相同的名稱。 (請參閱 [建立VLV的目錄伺服器索引&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. 使用 `ldapmodify` Sun ONE Server隨附的工具，分別使用群組的基本DN、搜尋篩選器和排序欄位，為群組建立類似的專案：

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例如，輸入下列文字：

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### 建立VLV的目錄伺服器索引 {#create-the-directory-server-index-for-vlv}

設定目錄設定並為使用者和群組建立LDAP VLV專案之後，請停止伺服器並建立所需的索引。

1. 建立物件專案之後，停止Sun ONE Server。
1. 使用vlvindex工具，輸入下列文字以產生索引：

   *目錄伺服器執行處理* `\vlvindex.bat -n userRoot -T lcuser`

   會產生下列輸出：

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex工具存在於目錄伺服器執行處理目錄中。 如果Sun ONE Server有兩個執行server1和server2的執行個體，則vlvindex工具位於 *Sun ONE伺服器目錄*\server1目錄。 引數的值 `-T` 是 `cn` 先前在範例LDIF中建立之vlvindex專案的屬性。 在此案例中，它是 `lcuser`.

1. 如果群組也啟用了VLV，請為群組建立對應的索引。 執行下列命令以確認是否建立索引：

   *sun one server目錄* `\shared\bin>ldapsearch -h`*主機名稱* `-p`*連線埠號碼* `-s base -b "" objectclass=*`

   會產生輸出，例如下列範例資料：

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
