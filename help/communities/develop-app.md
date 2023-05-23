---
title: 開發沙箱應用程式
seo-title: Develop Sandbox Application
description: 使用基礎指令碼開發應用程式
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 4%

---

# 開發沙箱應用程式  {#develop-sandbox-application}

在本節中，範本已設定在 [初始應用](initial-app.md) 區段，以及中建立的初始頁面 [初始內容](initial-content.md) 區段，您可使用基礎指令碼開發應用程式，包括啟用使用Communities元件編寫的功能。 在本節結束時，網站將可正常運作。

## 使用Foundation頁面命令檔 {#using-foundation-page-scripts}

預設指令碼是在新增轉譯播放頁面範本的元件時建立的，經過修改後會包含基礎頁面的head.jsp和本機body.jsp。

### 超級資源型別 {#super-resource-type}

第一個步驟是將資源超級型別屬性新增至 `/apps/an-scf-sandbox/components/playpage` 節點，以便繼承超級型別的指令碼和屬性。

使用 CRXDE Lite:

1. 選取節點 `/apps/an-scf-sandbox/components/playpage`.
1. 在屬性標籤中，輸入具有下列值的新屬性：

   名称: `sling:resourceSuperType`

   类型: `String`

   价值: `foundation/components/page`

1. 按一下綠色 **[!UICONTROL +新增]** 按鈕。
1. 按一下 **[!UICONTROL 全部儲存]**.

   ![page-script](assets/page-script.png)

### Head和body指令碼 {#head-and-body-scripts}

1. 在 **CRXDE Lite** 瀏覽器窗格，瀏覽至 `/apps/an-scf-sandbox/components/playpage` 並連按兩下檔案 `playpage.jsp` 以在「編輯」窗格中開啟它。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. 請注意open/close指令碼標籤，將「 // TODO ...」取代為 &lt;html>.

   具有超級型別 `foundation/components/page`，任何未定義在相同資料夾中的指令碼都會解析為中的指令碼 `/apps/foundation/components/page` 資料夾（如果有的話），否則會傳至中的指令碼 `/libs/foundation/components/page` 資料夾。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. 基礎指令碼 `head.jsp` 不需要重疊，但是基礎指令碼 `body.jsp` 空白。

   若要設定編寫，請覆蓋 `body.jsp` 使用本機指令碼，並在內文中加入段落系統(parsys)：

   1. 导航到 `/apps/an-scf-sandbox/components`。
   1. 選取 `playpage` 節點。
   1. 按一下右鍵並選取 `Create > Create File...`

      * 名稱： **body.jsp**
   1. 按一下 **[!UICONTROL 全部儲存]**.

   開啟 `/apps/an-scf-sandbox/components/playpage/body.jsp` 並貼入下列文字：

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. 按一下 **[!UICONTROL 全部儲存]**.

**在瀏覽器中以編輯模式檢視頁面：**

* 标准 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

您不應該只看到標題 **社群播放**，以及用於編輯頁面內容的UI。

當兩側面板均切換為開啟，且視窗寬度足以顯示側邊內容和頁面內容時，會看到「資產/元件」側面板。

![view-page](assets/view-page.png)

* 经典 UI: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

以下是播放頁面在傳統UI中的顯示方式，包括搭配內容尋找器(cf)：

![play-page-view](assets/play-page-view.png)

## Communities元件 {#communities-components}

若要啟用Communities元件以進行編寫，請依照下列指示開始進行：

* [存取Communities元件](basics.md#accessing-communities-components)

就此Sandbox而言，請從以下內容開始 **Communities** 元件（勾選方塊以啟用）：

* 评论
* 论坛
* 评分
* 审核
* 审核摘要（显示）
* 投票

此外，請選擇 **[!UICONTROL 一般]** 元件，例如

* 图像
* 表
* 文本
* 标题 (Foundation)

>[!NOTE]
>
>為頁面段落啟用的元件會儲存於存放庫中，作為 `components` 的屬性
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` 節點。

## 登录页面 {#landing-page}

在多語言環境中，根頁面會包含指令碼，此指令碼會剖析使用者端的請求，以判斷偏好的語言。

在這個簡單的範例中，已將根頁面以靜態方式設定為重新導向至英文頁面，而英文頁面可能會在日後發展為具有播放頁面連結的主要登陸頁面。

將瀏覽器URL變更為根頁面： `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 選取「頁面資訊」圖示
* 選取 **[!UICONTROL 開啟屬性]**
* 在進階標籤上

   * 對於重新導向專案，瀏覽至 **[!UICONTROL 網站]** > **[!UICONTROL SCF沙箱網站]** > **[!UICONTROL SCF沙箱]**
   * 按一下 **[!UICONTROL 確定]**

* 按一下 **[!UICONTROL 確定]**

發佈網站後，在發佈執行個體上瀏覽至根頁面時，會重新導向至英文頁面。

播放communities SCF元件之前的最後一步是新增使用者端程式庫資料夾(clientlibs) .... [新增Clienlibs](add-clientlibs.md)
