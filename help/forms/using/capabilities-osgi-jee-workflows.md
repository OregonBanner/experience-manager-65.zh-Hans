---
title: 表單中心AEM工作流程在OSGi和AEM Forms JEE工作流程上的動作和功能
description: 表單中心AEM工作流程在OSGi和AEM Forms JEE工作流程上的動作和功能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---

# 表單中心AEM工作流程在OSGi和AEM Forms JEE工作流程上的動作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件匣和HTML工作區 {#aem-inbox-and-html-workspace}

您可以使用AEM收件匣在OSGi上執行和監視以Forms為中心的AEM工作流程。 而HTML Workspace可讓您執行及監視AEM Forms JEE Workflow。 下表可協助您瞭解OSGi上Forms中心AEM工作流程的AEM收件匣以及AEM Forms JEE工作流程的HTML Workspace中可用的各種重要動作。

<table>
 <tbody>
  <tr>
   <td>操作</td>
   <td>AEM 收件箱</td>
   <td>HTML工作區</td>
  </tr>
  <tr>
   <td>啟動程式、任務或表單應用程式<br /> </td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交任務</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>將任務指派給群組</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交至多個路由</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>追蹤任務歷史記錄和任務摘要</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>電子郵件通知</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>重新指派任務</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>適用性表單的欄位層級附件</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>行事曆檢視</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>任務層級註解</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>佇列（共用的個人佇列、來自佇列的索賠工作）</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>休假通知</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
    <tr>
   <td>自訂UI元素</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>將任務指派給多個使用者</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM Forms JEE工作流程上的表單中心AEM工作流程 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM Forms JEE Workflow (JEE流程管理的AEM Forms)以表單為中心的AEM Workflow有一組不同的功能。 下表可協助您瞭解OSGi和JEE工作流程的AEM Forms表單中心AEM工作流程中的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上的表單中心AEM工作流程<br /> </td>
   <td>AEM Forms JEE工作流程</td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>與其他AEM解決方案的整合</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>自訂電子郵件範本</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>定義任務優先順序</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>任務在到期日後逾時</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流程中的回圈</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>動態選擇被指定者 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>使用自訂中繼資料</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>電子簽章(Adobe Sign)</td>
   <td>支援 <sup>[1]</sup></td>
   <td>支援 <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>管理任務和表單應用程式</td>
   <td>支援 <sup>[2]</sup><br /> </td>
   <td>支援 <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>文档服务</td>
   <td>支援 <sup>[3]</sup></td>
   <td>支援 <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>將已完成的任務演算為最適化表單或PDF檔案</td>
   <td>支持</td>
   <td>支持 [4]</td>
  </tr>
  <tr>
   <td>與Correspondence Management整合</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>閘道，不等待 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>儲存資料的變數 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>OR和AND拆分</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>使用者頭像</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在工作流程結束時傳送電子郵件</td>
   <td>支援 <sup>[7]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>從工作流程呼叫Web服務</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>工作流暂存</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>唯讀調適型表單</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>隱藏預設儲存按鈕</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>精細地控制工作流程詳細資訊區段</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>輪詢/排程服務</td>
   <td>立即可用</td>
   <td>需要自訂實施</td>
  </tr>
  <tr>
   <td>最適化Forms應用程式</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>汇编程序服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>PDF產生器服務</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>表单服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>输出服务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>檔案保證</td>
   <td>支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>執行指令碼</td>
   <td>支援ECMAScript</td>
   <td>支援Java程式碼片段</td>
  </tr>
  <tr>
   <td>組合器</td>
   <td>支持</td>
   <td>支持</td>
  </tr>  
  <tr>
   <td>HTML5 Forms、互動式PDF forms、表單集</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>程式報告</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>起點類別</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>大量任務核准 </td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用自訂名稱儲存草稿</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用現有程式資料起始程式<br /> </td>
   <td>不支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>將起點儲存為草稿</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>管理員檢視</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>搜索模板</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>與協力廠商應用程式整合</td>
   <td>不支援 <sup>[6]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流程應用程式或起點的任務層級附件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>提醒電子郵件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在任務逾時時變更標題</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>關於任務委派和任務宣告的電子郵件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>委託於不相交群組之間</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>XSLT轉換</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>動態任務優先順序</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>動態標題</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
    <tr>
   <td>動態說明</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用以表單為中心的AEM工作流程，以簽署已填妥的最適化表單。 OSGi上的表單中心AEM工作流程支援表單簽名以外的功能。 此 [表單內簽署](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 不支援體驗。

1. 您需要存取AEM收件匣，才能在AEM Forms OSGi和HTML Workspace上執行及監控以表單為中心的工作流程，以執行及監控AEM Forms JEE工作流程。
1. 原生AEM Forms檔案服務適用於OSGi上的表單中心AEM工作流程和JEE上的AEM Forms工作流程。 AEM Workflow在OSGi和AEM Forms JEE （程式管理）工作流程中，使用原生檔案服務進行以表單為中心的AEM工作流程。
1. AEM Forms JEE工作流程只能轉譯最適化表單。 不支援將最適化表單轉譯為PDF檔案。
1. AEM forms JEE Workflow沒有適用於Adobe Sign的獨立步驟。 您需要啟用Adobe Sign的最適化表單以用於AEM Forms JEE Workflow。 如需詳細資訊，請參閱 [Adobe Sign檔案](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. 您可以使用 [啟動表單資料模型服務](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 叫用Web服務並從協力廠商應用程式發佈或擷取資料的步驟。
1. 您可以使用 [傳送電子郵件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 步驟以傳送電子郵件。

## AEM收件匣和AEM Forms應用程式功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流程有兩個顯著的方法，就是 [AEM收件匣](../../forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 但AEM收件匣和AEM Forms應用程式的功能有所不同。 AEM收件匣僅適用於 [以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md) 而AEM Forms應用程式可搭配以Forms為中心的工作流程及程式管理運作。

下表列出AEM收件匣和AEM Forms應用程式的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>AEM 收件箱</strong></p> </td>
   <td><p><strong>AEM Forms 应用程序</strong></p> </td>
  </tr>
  <tr>
   <td><p>啟動表單應用程式</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>提交任務</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>委派任務</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>追蹤任務歷史記錄和任務摘要</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>新增工作層級附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>檢視工作層次附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>新增欄位層級附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>顯示行事曆檢視</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>新增註解</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
 </tbody>
</table>
