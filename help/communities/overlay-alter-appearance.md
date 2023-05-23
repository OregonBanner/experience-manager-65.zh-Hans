---
title: 變更外觀
seo-title: Alter the Appearance
description: 修改指令碼
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# 變更外觀 {#alter-the-appearance}

## 修改指令碼 {#modify-the-script}

comment.hbs指令碼負責為每個評論建立整體HTML。

不顯示每個張貼的評論旁的頭像：

1. 複製 `comment.hbs`從 `libs`至 `apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選取 **[!UICONTROL 複製]**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 選取 **[!UICONTROL 貼上]**

1. 開啟覆蓋的 `comment.hbs`

   * 連按兩下節點 `comment.hbs` 在 `/apps/social/commons/components/hbs/comments/comment folder`

1. 尋找下列行，然後刪除或註解它們：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

請刪除線段或將其周圍加上 `<!--` 和 `-->` 以取消註解。 此外，字元「xxx」也會新增為顯示頭像位置的視覺指標。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 復寫覆蓋 {#replicate-the-overlay}

使用復寫工具將覆蓋的註解元件推送至發佈例項。

>[!NOTE]
>
>更強大的復寫形式是在封裝管理員中建立封裝，並且 [啟用](/help/sites-administering/package-manager.md#replicating-packages) it. 套件可以匯出和封存。

在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 復寫]** 並按一下 **[!UICONTROL 啟動樹狀結構]**.

開始路徑請輸入 `/apps/social/commons` 並選取 **[!UICONTROL 啟動]**.

![verify-content-template](assets/verify-content-template.png)

### 檢視結果 {#view-results}

如果您以管理員身分(例如https://localhost:4503/crx/de )登入發佈執行個體（例如，以管理員/管理員身分），您可以驗證覆蓋的元件是否存在。

如果您登出後重新登入， `aaron.mcdonald@mailinator.com/password` 和重新整理頁面，您會發現貼出的評論不再以頭像顯示，而是顯示簡單的「xxx」。

![create-template-component](assets/create-template-component.png)
