---
title: 配置翻译集成框架
seo-title: Configuring the Translation Integration Framework
description: 瞭解如何設定翻譯整合架構。
seo-description: Learn how to configure the Translation Integration Framework.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: 6dea3a23c70fdb5f07bdf724547e799776002c61
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 47%

---

# 配置翻译集成框架{#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成，以编排 AEM 内容的译文。

* 连接到您的翻译服务提供商。
* 创建翻译集成框架配置。
* 将云配置与您的页面关联。

有关 AEM 中内容翻译功能的概述，请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)。

## 连接到翻译服务提供商 {#connecting-to-a-translation-service-provider}

创建用于将 AEM 连接到您的翻译服务提供商的云配置。默认情况下，AEM 具有连接到 Microsoft Translator 的功能。以下翻譯廠商為翻譯專案提供新API的實作。 深入瞭解整合的連結：

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)（Adobe Exchange 首选合作伙伴）
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://www.smartling.com/software/integrations/adobe-experience-manager/)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (AEM中預先安裝了Microsoft Translator)

>[!NOTE]
>
>若要尋找人工翻譯和機器翻譯提供者的最新清單，請檢視以下頁面：
>
>
>* [AEM人工翻譯](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM機器翻譯](https://www.adobe.com/go/aem-machine-translation-connectors)
>


安装连接器软件包后，即可为连接器创建云配置。一般需要提供凭据，以便向翻译服务进行身份验证。有关为 Microsoft Translator 连接器添加云配置的信息，请参阅[与 Microsoft Translator 集成](/help/sites-administering/tc-msconf.md)。

如果需要，可为同一个连接器创建多个云配置。例如，为您在同一供应商的每个帐户或项目都创建一个配置。

配置连接后，即可创建使用它的翻译集成框架配置。

## 创建翻译集成配置 {#creating-a-translation-integration-configuration}

创建翻译集成框架配置以指定如何翻译您的内容。该配置包括以下信息：

* 要使用哪个翻译服务提供商。
* 要执行人工翻译还是机器翻译.
* 是否翻译与页面或资产关联的其他内容，如标记.

创建框架配置后，请将云配置与要根据该配置翻译的页面关联。开始翻译过程后，将根据关联的框架配置执行翻译工作流。

当网站的不同部分有不同的翻译要求时，请相应地创建多个框架配置。例如，多語言網站包含英文、西班牙文和日文版本。 站点所有者使用两个不同的翻译服务提供商生成西班牙语和日语译文。因此，配置了两个框架配置。每个配置使用一个不同的翻译服务提供商。

配置翻译集成框架后，可[将它与使用它的页面关联](/help/sites-administering/tc-prep.md)。

**注意：** 如需AEM內容翻譯功能的概觀，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md).

架構的單一設定可控制如何翻譯頁面內容、社群內容和資產。
![chlimage_1-386](assets/translation-config-65.jpg)

### 站点配置属性 {#sites-configuration-properties}

Sites屬性可控制執行頁面內容翻譯的方式。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>選取框架為網站內容執行的翻譯方法：</p>
    <ul>
     <li>機器翻譯：翻譯提供者會使用機器翻譯即時執行翻譯。</li>
     <li>人工翻譯：內容會傳送給翻譯提供者，以供譯者翻譯。 </li>
     <li>不翻譯：不傳送內容以供翻譯。 这是为了跳过某些不翻译但可用最新内容更新的内容分支。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>選取要執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，提供者會出現在清單中。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（僅限機器翻譯）說明您要翻譯之內容的類別。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>選取以翻譯與頁面相關聯的標籤。</td>
  </tr>
  <tr>
   <td>翻译页面资产</td>
   <td><p>選取如何翻譯從檔案系統新增至元件或從Assets參照的資產：</p>
    <ul>
     <li>不翻譯：不翻譯頁面資產。</li>
     <li>使用網站翻譯工作流程：根據網站標籤上的設定屬性處理資產。</li>
     <li>使用資產翻譯工作流程：根據資產標籤上屬性的設定處理資產。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>選取此選項可在建立翻譯專案後自動執行翻譯工作。 选择此选项时，无法复查翻译作业和划定其范围。</td>
  </tr>
 </tbody>
</table>

### Communities設定屬性 {#communities-configuration-properties}

Communities屬性可控制如何執行使用者產生的內容翻譯。 翻譯使用者產生的內容一律使用機器翻譯。 如需詳細資訊，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).

| 属性 | 描述 |
|---|---|
| 翻译提供商 | 選取要執行翻譯的翻譯提供者。 為其建立雲端設定的提供者會出現在清單中。 |
| 内容类别 | 說明您要翻譯之內容的類別。 在翻译内容时，类别可能会影响术语和措辞的选择。 |
| 選擇要用作全域共用存放區的地區設定 | （選擇性）選取儲存UGC的語言環境，所有語言副本的貼文都會出現在同一個全域對話中。 依照慣例，選擇 [基本語言](/help/communities/sites-console.md#translation) 適用於網站。 選擇「無通用存放區」會停用全域翻譯。 預設會停用全域翻譯。 |

### 资产配置属性 {#assets-configuration-properties}

资产属性控制如何配置资产。有关翻译资产的更多信息，请参阅[创建资产的语言副本](/help/assets/translation-projects.md)。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>翻译工作流</td>
   <td><p>選取框架為資產執行的翻譯型別：</p>
    <ul>
     <li>機器翻譯：翻譯提供者會使用機器翻譯立即執行翻譯。</li>
     <li>人工翻譯：內容會自動傳送給翻譯提供者，以供手動翻譯。 </li>
     <li>不翻譯：不會傳送資產以供翻譯。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>翻译提供商</td>
   <td>選取要執行翻譯的翻譯提供者。 安裝提供者的對應聯結器後，提供者會出現在清單中。</td>
  </tr>
  <tr>
   <td>内容类别</td>
   <td>（僅限機器翻譯）說明您要翻譯之內容的類別。 在翻译内容时，类别可能会影响术语和措辞的选择。</td>
  </tr>
  <tr>
   <td>翻译资产</td>
   <td>選取以在翻譯專案中包含資產。 </td>
  </tr>
  <tr>
   <td>翻译元数据</td>
   <td>選取以翻譯資產中繼資料。</td>
  </tr>
  <tr>
   <td>翻译标记</td>
   <td>選取以翻譯與資產相關聯的標籤。</td>
  </tr>
  <tr>
   <td>自动执行翻译</td>
   <td>選取此選項可在建立翻譯專案後自動執行翻譯工作。 选择此选项时，无法复查翻译作业或划定其范围。</td>
  </tr>
 </tbody>
</table>

1. 在側邊欄中，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「翻譯整合」區域中，是否已建立任何設定會決定顯示哪個連結：

   * 如果尚未建立任何設定，請按一下或點選「立即設定」。
   * 如果設定已存在，請按一下或點選「 Show Configurations 」，然後按一下或點選「 Available Configurations 」旁邊顯示的+連結。

1. 輸入設定的名稱，然後按一下或點選「建立」。
1. 在「網站」、「社群」和「資產」標籤上設定屬性，然後按一下或點選「確定」。

## 配置页面以供翻译 {#configuring-pages-for-translation}

要配置如何将您的源页面翻译为其他语言，请将这些页面与以下云配置关联：

* 用于将 AEM 连接到您的翻译服务提供商的云配置。
* 用于配置翻译细节的翻译集成框架。

请注意，翻译集成框架云配置标识要用于连接到服务提供商的云配置。将源页面与框架云配置关联时，该页面必须与该框架云配置使用的服务提供商云配置关联。

将页面与云配置关联时，该页面的后代页面继承这种关联。例如，如果您將/content/geometrixx/en/products頁面與翻譯整合框架建立關聯，產品頁面及其下方的所有頁面都會根據該框架進行翻譯。

必要时，可在后代页面上取代该关联。例如，網站的內容主要是關於服裝。 但某个分支的页面介绍公司情况。網站的根頁面與指定使用「服飾」類別進行機器翻譯的翻譯整合架構相關聯。 說明公司的分支使用框架，該框架會使用「一般」類別執行機器翻譯。

此外，適用於任何社群 [SCF元件](/help/communities/scf.md) 在頁面上，使用者產生的內容(UGC)將包含使用者翻譯內容的能力。 如需詳細資訊，請參閱 [翻譯使用者產生的內容](/help/communities/translate-ugc.md).

### 将页面与翻译提供商关联 {#associating-a-page-with-a-translation-provider}

将页面与您用于翻译该页面和后代页面的翻译提供商关联。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Services」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯提供者，然後按一下或點選「完成」。

### 将页面与翻译集成框架关联 {#associating-pages-with-a-translation-integration-framework}

将页面与定义您要如何为该页面和后代页面执行翻译的翻译集成框架关联。

1. 在網站主控台中，選取要設定的頁面，然後按一下或點選「檢視屬性」。
1. 按一下或點選「編輯」，然後按一下或點選「Cloud Services」標籤。
1. 按一下或點選「新增設定>翻譯整合」。
1. 選取要使用的翻譯整合架構，然後按一下或點選「完成」。
