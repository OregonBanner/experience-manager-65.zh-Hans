---
title: 基本處理
description: 使用AEM製作環境時基本處理的概觀。 它使用站点控制台作为基础。
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 6%

---

# 基本处理{#basic-handling}

>[!NOTE]
>
>* 此頁面旨在概述使用AEM製作環境時的基本處理方式。 它使用&#x200B;**站点**&#x200B;控制台作为基础。
>
>* 部分功能並非在所有主控台中提供，且/或某些主控台提供其他功能。 有關個別主控台及其相關功能的特定資訊，將在其他頁面上詳細說明。
>* 用户在整个 AEM 环境中都可以使用各种键盘快捷键，尤其是在[使用控制台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md)和[编辑页面](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)时。
>


## 歡迎畫面 {#the-welcome-screen}

傳統UI提供一系列主控台，使用眾所周知的機制來導覽和起始動作，包括按一下、連按兩下和 [內容功能表](#context-menus).

登入後，歡迎畫面會隨即顯示，其中會提供控制檯和服務連結清單：

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 控制台 {#consoles}

主要主控台包括：

<table>
 <tbody>
  <tr>
   <td><strong>控制台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td><strong>歡迎</strong></td>
   <td>提供對AEM主要功能的概觀和直接存取（透過連結）。</td>
  </tr>
  <tr>
   <td><strong>数字资产</strong><br /> </td>
   <td>這些主控台可讓您匯入和 <a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理數位資產</a> 例如影像、影片、檔案和音訊檔案。 然後這些資產便可由同一AEM執行個體上執行的任何網站使用。 </td>
  </tr>
  <tr>
   <td><strong>启动项</strong></td>
   <td>這可協助您管理您的 <a href="/help/sites-classic-ui-authoring/classic-launches.md">啟動</a>；這些功能可讓您為日後發行的一或多個已啟動網頁開發內容。<br /> <i>注意：在觸控式UI中，Sites主控台與「參考」邊欄提供許多相同的功能。</i> <i>必要時，可以從「工具」主控台使用此主控台；請選取作業，然後選取啟動。</i></td>
  </tr>
  <tr>
   <td><strong>收件箱 </strong></td>
   <td>在許多情況下，許多人都參與工作流程的子任務，而且每個人都必須先完成自己的步驟，才能將工作移交給下一個人。 收件匣可讓您檢視與這類工作相關的通知。 另請參閱 <a href="/help/sites-administering/workflows.md">使用工作流程</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>标记</strong></td>
   <td>「標籤」主控台可讓您管理標籤。 標籤是簡短名稱或片語，可用來分類和註釋內容片段，使其更容易找到並組織。 如需詳細資訊，請參閱 <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理標籤</a>.</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td>此 <a href="/help/sites-administering/tools-consoles.md">工具主控台</a> 提供對許多專用工具和控制檯的存取，協助您管理網站、數位資產和內容存放庫的其他方面。</td>
  </tr>
  <tr>
   <td><strong>用户</strong></td>
   <td>這些主控台可讓您管理使用者和群組的存取許可權。 如需完整詳細資訊，請參閱 <a href="/help/sites-administering/security.md">使用者管理與安全性</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>网站</strong></td>
   <td>Sites/Websites主控台可讓您 <a href="/help/sites-classic-ui-authoring/classic-page-author.md">建立、檢視及管理網站</a> 在您的AEM執行個體上執行。 透過這些主控台，您可以建立、複製、移動和刪除網站頁面、啟動工作流程，以及啟用（發佈）頁面。 您也可以開啟頁面進行編輯。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流</strong></td>
   <td>工作流程是定義的一系列步驟，用於說明完成某些任務的流程。 在許多情況下，許多人都參與一項任務，每個人必須先完成自己的步驟，才能將工作移交給下一個人。 「工作流程」主控台可讓您建立工作流程模型並管理執行中的工作流程例項。 另請參閱 <a href="/help/sites-administering/workflows.md">使用工作流程</a>.<br /> </td>
  </tr>
 </tbody>
</table>

此 **網站** console提供兩個窗格，供您導覽及管理頁面：

* 左窗格

   這會顯示您網站的樹狀結構以及這些網站中的頁面。

   它也會顯示其他方面或AEM的相關資訊，包括專案、藍圖和資產。

* 右窗格

   這會顯示頁面（在左窗格中選取的位置），且可用於執行動作。

從這裡，您可以 [管理您的頁面](/help/sites-authoring/managing-pages.md) 使用工具列、快顯功能表或開啟頁面以進一步操作。

>[!NOTE]
>
>所有主控台的基本處理方式都相同。 本節內容主要放在 **網站** 主控台，因為它是編寫時使用的主要主控台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 访问帮助 {#accessing-help}

在各種主控台（例如網站）上， **說明** 按鈕可用，這會開啟Package Share或檔案網站。

![chlimage_1-10](assets/chlimage_1-10a.png)

編輯頁面時 [sidekick也有存取說明的按鈕](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## 使用網站控制檯導覽 {#navigating-with-the-websites-console}

此 **網站** console會以樹狀結構列出您的內容頁面（左側窗格）。 為方便瀏覽，可視需要展開樹狀結構的區段(+)或收合區段(-)：

* 按一下頁面名稱（在左窗格中）將：

   * 在右窗格中列出子頁面
   * 同時展開左側窗格中的結構。

      基於效能原因，此動作取決於子節點數目。 在標準安裝中，此擴充方法適用於 `30` 或較少的子節點。

* 在頁面名稱（左窗格）上按兩下也會展開樹狀結構，不過同時開啟頁面時，這種效果並不明顯。

>[!NOTE]
>
>此預設值( `30`)可在您的應用程式特定的siteadmin widget設定中，依每個主控台進行變更：
>
>在網站管理員節點上：
>
>設定屬性的值：
>`treeAutoExpandMax`
>开启:
>`/apps/wcm/core/content/siteadmin`
>
>或是全域佈景主題：
>設定下列專案的值：
>`TREE_AUTOEXPAND_MAX`
>中的:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>另請參閱 [CQ Widget API中的SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin) 以取得更多詳細資料。

## 網站主控台上的頁面資訊 {#page-information-on-the-websites-console}

的右窗格 **網站** console提供清單檢視，內含頁面的相關資訊：

![page-info](assets/page-info.png)

以下是可供使用的欄位；這些欄位的子集會顯示為預設值：

<table>
 <tbody>
  <tr>
   <td><strong>列</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>缩略图</td>
   <td>顯示頁面的縮圖。</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>顯示在頁面上的標題</td>
  </tr>
  <tr>
   <td>名称</td>
   <td>AEM參考頁面的名稱</td>
  </tr>
  <tr>
   <td>发布时间</td>
   <td>指出頁面是否已發佈，並提供發佈日期和時間。</td>
  </tr>
  <tr>
   <td>修改时间</td>
   <td>指出頁面是否已修改，並提供修改日期和時間。 若要儲存任何修改，您必須啟動頁面。</td>
  </tr>
  <tr>
   <td>Scene7發佈</td>
   <td>指出頁面是否已發佈至Scene7。<br /> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td>指示頁面的目前狀態，例如頁面是否為工作流程或即時副本的一部分，或頁面目前是否已鎖定。</td>
  </tr>
  <tr>
   <td>展示次数</td>
   <td>以點選數顯示頁面上的活動。</td>
  </tr>
  <tr>
   <td>模板</td>
   <td>指出頁面所依據的範本。</td>
  </tr>
  <tr>
   <td>在工作流中</td>
   <td>指示頁面何時在工作流程中。</td>
  </tr>
  <tr>
   <td>锁定者</td>
   <td>顯示頁面何時已鎖定，以及已鎖定的使用者帳戶。</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>指示頁面何時為即時副本的一部分。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>若要選取可見欄，請將滑鼠停留在欄標題上。 隨即顯示下拉式功能表，您可在此處使用 **欄** 選項。

中頁面旁的顏色 **已發佈** 和 **修改時間** 欄指示發佈狀態：

| **列** | **颜色** | **描述** |
|---|---|---|
| 发布时间 | 绿色 | 發佈成功。 內容已發佈。 |
| 发布时间 | 黄色 | 正在等候發佈。 系統尚未收到發佈確認。 |
| 发布时间 | 红色 | 发布失败. 未與發佈執行個體建立連線。 這也表示內容已停用。 |
| 发布时间 | *blank* | 此頁面從未發佈。 |
| 修改时间 | 蓝色 | 自上次發佈後，頁面已修改。 |
| 修改时间 | *blank* | 此頁面從未修改過，或自上次發佈以來從未修改過。 |

## 內容功能表 {#context-menus}

Classic UI使用眾所周知的機制來導覽和起始動作，包括按一下和連按兩下。 視目前情況而定，也可以使用一系列前後關聯選單（通常以滑鼠右鍵開啟）：

![chlimage_1-11](assets/chlimage_1-11a.png)
