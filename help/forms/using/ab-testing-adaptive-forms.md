---
title: 建立和管理最適化表單的A/B測試
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms與Adobe Target整合，可針對最適化表單執行A/B測試，以增強客戶體驗並提高轉換率。
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 294d12e7d1b5293f165a164ff1fcc624f7b2b648
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 2%

---

# 建立和管理最適化表單的A/B測試{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE 已終止]{type=negative tooltip="此功能現已終止服務"}

<div class="preview"> 適用性表單的A/B測試功能已終止服務，不再受支援。 </div>

## 概述 {#overview-br}

如果表單提供的體驗不吸引人，您的客戶可能會捨棄表單。 雖然讓客戶感到沮喪，但也可以提高貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率既關鍵又具有挑戰性。 Adobe Experience Manager Forms掌握此問題的關鍵。

AEM Forms與Adobe Target (一種Adobe Marketing Cloud解決方案)整合，以跨多個數位頻道提供個人化且吸引人的客戶體驗。 Target的一項重要功能是A/B測試，可讓您快速設定同時的A/B測試、向目標使用者呈現相關內容，以及識別可促進更高轉換率的體驗。

透過AEM Forms，您可以即時設定和執行最適化表單的A/B測試。 此外，還提供現成且可自訂的報告功能，以視覺化方式呈現表單體驗的即時效能，並找出能提高使用者參與度和轉換率的體驗。

## 在AEM Forms中設定和整合Target {#set-up-and-integrate-target-in-aem-forms}

開始建立和分析適用性表單的A/B測試之前，您需要設定Target伺服器並將其整合到AEM Forms中。

### 設定目標 {#set-up-target}

若要將AEM與Target整合，請確保您擁有有效的Adobe Target帳戶。 註冊Adobe Target時，您會收到使用者端代碼。 您需要使用者端代碼、與Target帳戶關聯的電子郵件和密碼，才能將AEM與Target連線。

使用者端代碼會識別Adobe Target客戶帳戶，並在呼叫Adobe Target伺服器時作為URL中的子網域。 繼續之前，請先登入 [https://experience.adobe.com/](https://experience.adobe.com/) 如果您有存取權，請檢視 [!DNL Adobe Target] 中的選項 [!UICONTROL 快速存取] 區段。

### 在AEM Forms中整合Target {#integrate-target-in-aem-forms}

執行以下步驟，將執行中的Target伺服器與AEM Forms整合：

1. 在AEM伺服器上，前往https://&lt;*主機名稱*>：&lt;*連線埠*>/libs/cq/core/content/tools/cloudservices.html.

1. 在 **Adobe Target** 區段，按一下 **顯示設定** 然後 **+** 圖示以新增設定。
如果您是第一次設定Target，請按一下 **立即設定。**

1. 在建立組態對話方塊中，指定 **標題** 並可選擇使用 **名稱** 用於設定。

1. 单击&#x200B;**创建**。「編輯元件」對話方塊開啟。
1. 指定您的Target帳戶詳細資料，例如使用者端代碼、電子郵件和密碼。
1. 選取 **Rest** 從「API型別」下拉式清單。

1. 单击&#x200B;**连接到 Adobe Target** 可初始化与 Target 的连接。如果连接成功，则将显示消息连接成功。单击消息上的&#x200B;**确定**，然后单击对话框上的&#x200B;**确定**。已設定Target帳戶。

1. 建立Target架構，如所述 [新增框架](/help/sites-administering/target.md).

1. 前往https://&lt;*主機名稱*>：&lt;*連線埠*>/system/console/configMgr。

1. 按一下 **AEM Forms Target設定**.
1. 選取 **目標框架**.
1. 在 **目標URL** 欄位中，指定要執行A/B測試的所有URL。 例如， https://&lt;*主機名稱*>：&lt;*連線埠*>/ (適用於OSGi上的AEM Forms伺服器)或https://&lt;*主機名稱*>：&lt;*連線埠*>/lc/適用於JEE上的AEM Forms伺服器。
假設您想要設定發佈執行個體的Target URL，且您的客戶可使用主機名稱或IP位址進行存取，則您需要將兩者設定為目標URL — 使用主機名稱和IP位址。 如果您只設定其中一個URL，則不會針對來自其他URL的客戶執行A/B測試。 按一下 **+** 以指定多個URL。

1. 单击“**保存**”。

您的Target伺服器已與AEM Forms整合。 如果您擁有使用Adobe Target的完整授權，現在可以啟用A/B測試。

如果您擁有使用Adobe Target的完整授權，請在將Target與AEM Forms整合後，使用下列引數啟動伺服器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM執行個體在JBoss上執行，則從立即可用服務啟動，在 `jboss\bin\standalone.conf.bat` 檔案，請在以下專案新增 — Dabtesting.enabled=true引數：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss伺服器之外，您還可以在任何應用程式伺服器的伺服器啟動指令碼中新增 — Dabtesting.enabled=true jvm引數。 現在您可以建立和執行最適化表單的A/B測試。

>[!NOTE]
>
>如果您稍後更新已設定的Target URL，請確定您更新任何正在執行的A/B測試，以便它們指向目前的URL。 如需有關更新A/B測試的資訊，請參閱 [更新A/B測試](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).

## 在AEM中建立對象 {#create-audiences-within-aem}

AEM可讓您建立對象，並將其用於A/B測試。 您在AEM中建立的對象可在AEM Forms中使用。 執行以下步驟，在AEM中建立對象：

1. 在製作執行個體中，點選 **Adobe Experience Manager** > **個人化** > **受眾**.

1. 在「對象」頁面中，點選 **建立對象>建立目標對象**.
1. 在「Adobe Target設定」對話方塊中，選取Target設定，然後按一下 **確定**.
1. 在「建立新對象」頁面中，建立規則。 規則可讓您分類對象。 例如，您想要根據作業系統來分類對象。 您的對象A來自Windows，而對象B來自Linux。

   1. 若要根據Windows分類對象，請在規則#1中選取 **作業系統** 屬性型別。 從「時間」下拉式清單中選取 **Windows。**

   1. 若要根據Linux分類對象，請在規則#2中，選取 **作業系統** 屬性型別。 從 **時間** 下拉式清單，選取 **Linux**，然後按一下 **下一個**.

1. 指定已建立對象的名稱，然後按一下 **儲存**.

當您設定表單的A/B測試時，可以選取對象，如下所示。

## 建立A/B測試 {#create-a-b-test}

執行以下步驟，為最適化表單建立A/B測試。

1. 前往 **Forms與檔案** 在https://&lt;*主機名稱*>：&lt;*連線埠*>/aem/forms.html/content/dam/formsanddocuments.

1. 導覽至包含最適化表單的資料夾。
1. 按一下 **選取** 工具列並選取最適化表單。
1. 按一下 **更多** 在工具列中並選取 **設定A/B測試**. 隨即開啟設定A/B測試頁面。

[ ](assets/ab-test-configure-1.png)

1. 指定 **活動名稱** （A/B測試）。

1. 從「對象」下拉式清單中，選取您要為其提供不同表單體驗的對象。 例如， **使用Chrome的訪客**. 對象清單是從已設定的Target伺服器填入。

1. 在 **體驗散佈** 體驗A和B的欄位中，以百分比形式指定分佈，以決定體驗在總對象中的分佈。 例如，如果您分別指定體驗A和B 40、60，則體驗A會提供給40%的對象，而剩下的60%則會看到體驗B。
1. 按一下 **設定**. 會出現一個對話方塊，確認建立A/B測試。
1. 按一下 **編輯體驗B** 以於編輯模式中開啟最適化表單。 修改表單以建立與預設體驗A不同的體驗。體驗B中允許的可能變數為以下變更：

   * CSS或樣式
   * 不同面板或相同面板中的欄位順序
   * 面板布局
   * 面板標題
   * 欄位的說明、標籤和說明文字
   * 不影響或中斷提交流程的指令碼
   * 驗證（使用者端和伺服器端）
   * 體驗B的主題。（您可以為體驗B選擇替代主題）

1. 前往Forms和檔案UI，選取最適化表單，然後按一下 **更多**，並選取 **開始A/B測試**.

您的A/B測試目前正在執行，系統會根據指定的分佈，隨機提供體驗給指定的對象。

## 更新A/B測試 {#update-a-b-test}

您可以更新執行中A/B測試的對象和體驗分佈。 若要這麼做：

1. 在Forms和檔案UI中，導覽至包含執行A/B測試的最適化表單的資料夾。
1. 選取最適化表單。
1. 按一下 **更多** 然後選取 **編輯A/B測試**. 更新A/B測試頁面隨即開啟。

1. 視需要更新對象和體驗分佈。
1. 单击&#x200B;**更新**。

## 檢視和分析A/B測試報告 {#view-and-analyze-a-b-test-report}

在允許A/B測試在所需期間執行後，您可以產生報告並檢查哪個體驗產生了更好的轉換。 您可以宣告表現較好的體驗為獲勝者，或選擇執行其他A/B測試。 要執行此操作，請執行下列步驟：

1. 選取最適化表單，按一下 **更多**，然後按一下 **A/B測試報告**. 報表隨即顯示。

[ ](assets/ab-test-report-3.png)

1. 分析報表，檢視是否有足夠的資料點將其中一個表現較佳的體驗宣告為獲勝者。 您可以選擇繼續使用相同的A/B測試以獲得更多時間，或宣告獲勝者並結束A/B測試。
1. 若要宣告獲勝者並結束A/B測試，請按一下 **結束A/B測試** 報告儀表板上的按鈕。 對話方塊會提示您宣告兩個體驗之一為獲勝者。 選擇獲勝者並確認結束A/B測試。
或者，您可以先按一下 **宣告獲勝者** 按鈕來代表個別體驗。 它會提示您確認獲勝者。 按一下 **是** 以結束A/B測試。

如果您選擇體驗A作為獲勝者，A/B測試將會結束，並且往後，只有體驗A會提供給所有對象。
