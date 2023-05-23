---
title: 將HTML5表單儲存為草稿
seo-title: Saving an HTML5 form as a draft
description: 將HTML5表單儲存為草稿，並在稍後階段繼續填寫表單。
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# 將HTML5表單儲存為草稿 {#saving-an-html-form-as-a-draft}

您可以將HTML5表單儲存為草稿，並在稍後階段繼續填寫表單。 Forms入口網站可讓任何使用者儲存和還原HTML5表單。 若要啟用「另存為草稿」功能，請將下列設定新增至設定檔節點：

## 允許另存為草稿功能的自訂設定檔 {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms可立即提供 **另存為草稿** 設定檔。 您可以使用另存為草稿設定檔來轉譯表單，以啟用HTML5表單的草稿功能。 您可以在下列位置為表單指定HTML轉譯器設定檔： [Forms Manager](/help/forms/using/introduction-managing-forms.md).

若要為您現有的「 」啟用「另存為草稿」功能 [自訂設定檔](/help/forms/using/custom-profile.md)，新增下列屬性至您的自訂設定檔節點：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>啟用另存為草稿功能</p> <p>此設定檔的。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>允許上傳附件</p> <p>使用此設定檔。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿儲存和清單 {#drafts-storage-and-listing}

為表單啟用「另存為草稿」功能後；儲存表單時，它會列在 [草稿與提交元件](/help/forms/using/draft-submission-component.md). 您可以從「草稿和提交」元件中擷取並開始填寫已儲存的表單。

若要為「草稿和提交」元件啟用表單清單，請將下列屬性新增至設定檔節點：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字符串</td>
   <td>true</td>
   <td>若要啟用草稿和表單以列於<br /> 提交後Forms Portal草稿和提交元件</td>
  </tr>
 </tbody>
</table>

依預設，AEM Forms會將與表單草稿和提交相關聯的使用者資料儲存在發佈執行個體上的/content/forms/fp節點中。 您可以新增自訂儲存提供者，詳情請參閱 [草稿和提交元件的自訂儲存](/help/forms/using/adding-custom-storage-provider-forms.md).
