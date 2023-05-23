---
title: 建立節點
seo-title: Create Nodes
description: 覆蓋註解系統
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 7%

---

# 建立節點 {#create-nodes}

複製最少需要的檔案數，以自訂版本覆蓋註解系統 `/libs` 到 `/apps` 並在中修改它們 `/apps`.

>[!CAUTION]
>
>絕不會編輯/libs資料夾的內容，因為任何重新安裝或升級都可能會刪除或取代/libs資料夾，而/apps資料夾的內容則保持不變。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) 在author執行個體上，首先在/apps資料夾中建立與/libs資料夾中覆蓋元件的路徑相同的路徑。

要複製的路徑為：

* `/libs/social/commons/components/hbs/comments/comment`

路徑中的部分節點為資料夾，部分為元件。

1. 瀏覽至 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 建立 `/apps/social` （如果尚未存在）
   * 選取 `/apps` 節點
   * **[!UICONTROL 建立>資料夾……]**
      * 输入姓名: `social`
1. 選取 `social` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 資料夾……]**
      * 输入姓名: `commons`
1. 選取 `commons` 節點
   * **[!UICONTROL 建立>資料夾……]**
      * 输入姓名: `components`
1. 選取 `components` 節點
   * **[!UICONTROL 建立>資料夾……]**.
      * 输入姓名: `hbs`
1. 選取 `hbs` 節點
   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件……]**
      * 輸入標籤： `comments`
      * 輸入標題： `Comments`
      * 输入描述: `List of comments without showing avatars`
      * 超级类型: `social/commons/components/comments`
      * 輸入群組： `Communities`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
1. 選取 `comments` 節點

   * **[!UICONTROL 建立]** > **[!UICONTROL 建立元件……]**

      * 輸入標籤： `comment`
      * 輸入標題： `Comment`
      * 输入描述: `A comment instance without avatars`
      * 超级类型: `social/commons/components/comments/comment`
      * 輸入群組： `.hidden`
      * 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 確定]**
   * 選取 **[!UICONTROL 全部儲存]**
1. 刪除預設值 `comments.jsp`
   * 選取節點 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選取 **[!UICONTROL 刪除]**
1. 刪除預設的comment.jsp
   * 選取節點 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選取 **[!UICONTROL 刪除]**
   * 選取 **[!UICONTROL 全部儲存]**

>[!NOTE]
>
>為了保留繼承鏈， `Super Type` (屬性 `sling:resourceSuperType`)，其值會設定為與 `Super Type` 覆蓋的元件數目，在此例中為：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


覆蓋圖本身的 `Type`(屬性 `sling:resourceType`)必須是相對自我參照，以便在/apps中找不到的任何內容會在/libs中尋找。
* 名称: `sling:resourceType`
* 类型: `String`
* 价值: `social/commons/components/hbs/comments`

1. 選取綠色 `[+] Add`
   * 名称: `sling:resourceType`
   * 类型: `String`
   * 价值: `social/commons/components/hbs/comments/comment`
1. 選取綠色 `[+] Add`
   * 選取 **[!UICONTROL 全部儲存]**

![create-nodes](assets/create-nodes.png)
