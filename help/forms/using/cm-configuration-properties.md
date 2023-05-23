---
title: 通訊管理設定屬性
seo-title: Correspondence Management Configuration Properties
description: 本主題說明如何使用解決方案特定設定來修改Asset Composer。 本主題詳細說明您可以編輯的屬性，以及其說明、預設值和可接受值。
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---

# 通訊管理設定屬性 {#correspondence-management-configuration-properties}

若要設定這些屬性，請在瀏覽器中開啟下列URL： `https://<server>:<port>/<contextPath>/system/console/configMgr` 並選取 **通訊管理設定**.

「通訊管理」有下列設定屬性：

<table>
 <tbody>
  <tr>
   <th><p><strong>属性</strong></p> </th>
   <th><p><strong>描述</strong></p> </th>
   <th><p><strong>默认</strong></p> </th>
   <th><p><strong>可接受的值</strong></p> </th>
  </tr>
  <tr>
   <td><p>缩进</p> </td>
   <td>模組的縮排<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td>數字最小寬度</td>
   <td>使用羅馬數字以外的編號清單時，要套用至專案符號/數字欄位的最小寬度</td>
   <td>8.0mm</td>
   <td>任何數字</td>
  </tr>
  <tr>
   <td><p>羅馬數字最小寬度</p> </td>
   <td><p>使用羅馬數字時，要套用至專案符號/數字欄位的最小寬度</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td>轉譯型別</td>
   <td>建立通訊應用程式用來呈現信件預覽的轉譯型別。 </td>
   <td>HTML轉譯</td>
   <td>HTML轉譯/PDF轉譯</td>
  </tr>
  <tr>
   <td><p>啟用CCRPDF反白顯示</p> </td>
   <td><p>在建立通訊應用程式中啟用反白顯示PDF</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>目標反白顯示型別</p> </td>
   <td><p>建立對應應用程式中的目標反白顯示型別</p> </td>
   <td><p>邊框</p> </td>
   <td><p>邊框/填滿/無</p> </td>
  </tr>
  <tr>
   <td><p>目標反白顯示色彩</p> </td>
   <td><p>建立對應應用程式中的目標反白顯示色彩</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>R；G；B格式的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>內容反白顯示型別</p> </td>
   <td><p>建立對應應用程式中的內容反白顯示型別</p> </td>
   <td><p>填滿</p> </td>
   <td><p>邊框/填滿/無</p> </td>
  </tr>
  <tr>
   <td><p>內容反白顯示色彩</p> </td>
   <td><p>建立對應應用程式中的內容反白顯示色彩</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R；G；B格式的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>欄位反白顯示型別</p> </td>
   <td><p>建立對應應用程式中的欄位反白顯示型別</p> </td>
   <td><p>填滿</p> </td>
   <td><p>邊框/填滿/無</p> </td>
  </tr>
  <tr>
   <td><p>欄位反白顯示色彩</p> </td>
   <td><p>建立對應應用程式中的欄位反白顯示色彩</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>R；G；B格式的任何RGB顏色</p> </td>
  </tr>
  <tr>
   <td><p>應用程式逾時</p> </td>
   <td><p>應用程式逾時（以秒為單位）</p> </td>
   <td><p>1200</p> </td>
   <td><p>任何數字</p> </td>
  </tr>
  <tr>
   <td><p>PDF檔案引數名稱</p> </td>
   <td><p>後處理中PDF檔案的引數名稱</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XML資料引數名稱</p> </td>
   <td><p>後處理中XML檔案（資料）的引數名稱</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>XDP檔案引數名稱</p> </td>
   <td><p>傳送到後處理的XDP檔案的引數名稱</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>重新導向URL引數名稱</p> </td>
   <td><p>從後處理程式傳送之重新導向URL的引數名稱此值可以是任何字串變數名稱</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>PDF提交型別</p> </td>
   <td><p>PDF提交型態(從「建立通訊」應用模組提交時產生的PDF型態)</p> </td>
   <td><p>非互動式</p> </td>
   <td><p>互動/非互動</p> </td>
  </tr>
  <tr>
   <td><p>最佳化資料字典例項</p> </td>
   <td><p>啟用最佳化資料字典執行個體傳輸（包含伺服器和使用者端）</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>自動修正不一致之處 </p> </td>
   <td><p>啟用時，會自動處理信件指派中可能發生的不一致情況</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>使用已設定的資料格式</p> </td>
   <td><p>控制是否使用已設定的資料編輯格式和資料顯示格式</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料顯示格式</p> </td>
   <td><p>指定資料的區域設定特定顯示格式</p> </td>
   <td><p>locale=en_US； dateFormat=dd-MM-yyyy； numberDecimalSeparator=.； numberGroupSeparator=，； numberUseGroupSeparator=truelocale=de_DE； dateFormat=dd-MM-yyyy； numberDecimalSeparator=，； numberGroupSeparator=.； numberUseGroupSeparator=truelocale=fr_FR； dateFormat=dd-MM-yyyy； numberDecimalSeparator=，； numberGroupSeparator= ； numberUseGroupSeparator=truelocale=ja_JP； dateFormat=dd-MM-yyy； numberDecimalSeparator=。； numberGroupSeparator=，； numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>資料編輯格式</p> </td>
   <td><p>編輯資料的格式。 將資料寫入為String或從String剖析資料時，會使用此值</p> </td>
   <td><p>locale=en_US； dateFormat=dd-MM-yyyy； numberDecimalSeparator=.； numberGroupSeparator=，； numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>管理發布時的信件例項</p> </td>
   <td><p>啟用/停用「管理信件」功能（僅適用於發佈伺服器）</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用稽核</p> </td>
   <td><p>啟用/停用稽核功能。 為false時，將會停用所有動作的稽核記錄</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用讀取稽核</p> </td>
   <td><p>啟用/停用資產讀取的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用建立稽核</p> </td>
   <td><p>啟用/停用資產建立的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用更新稽核</p> </td>
   <td><p>啟用/停用資產更新的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用回覆稽核</p> </td>
   <td><p>啟用/停用資產回覆的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用發佈稽核</p> </td>
   <td><p>啟用/停用資產發佈的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用SaveAsDraft稽核</p> </td>
   <td><p>啟用/停用儲存信件草稿的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用提交稽核</p> </td>
   <td><p>啟用/停用信件提交的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用電子郵件稽核</p> </td>
   <td><p>啟用/停用電子郵件信件的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用列印稽核</p> </td>
   <td><p>啟用/停用列印信函的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>啟用自訂傳遞稽核</p> </td>
   <td><p>啟用/停用自訂信件傳送的稽核功能</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>附件檔案引數名稱</p> </td>
   <td><p>傳送至發佈程式的附件檔案的引數名稱</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>任何字串變數名稱</p> </td>
  </tr>
  <tr>
   <td><p>CM使用者根目錄</p> </td>
   <td><p>包含所有Correspondence Management使用者資產的資料夾URL</p> </td>
   <td><p>--</p> </td>
   <td><p>有效的資料夾位置</p> </td>
  </tr>
  <tr>
   <td><p>字母快取大小</p> </td>
   <td><p>指定快取中保留的最大字母數。</p> <p>變更此值將導致清理 <code>in-memory</code> 快取。</p> </td>
   <td><p>100</p> </td>
   <td><p>任何數值</p> </td>
  </tr>
  <tr>
   <td><p>啟用字母快取</p> </td>
   <td><p>啟用/停用字母快取。</p> <p>變更此值將導致清理 <code>in-memory </code> 快取。</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>資料元素排序</p> </td>
   <td><p>根據資料元素在Letter中的順序，保持建立通訊介面中的資料元素順序</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>支援重新載入</p> </td>
   <td><p>啟用/停用伺服器端轉譯字母的重新載入支援。</p> <p>停用此專案將改善字母轉譯效能。</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>暫存資料夾</td>
   <td>暫存資料夾的位置。</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>遠端儲存</td>
   <td>將信件例項儲存在指定的處理作者上。</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>相容性選項</td>
   <td>以逗號分隔的configname：configvalue格式的相容性選項。</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>偵錯目錄 </p> <p> </p> </td>
   <td>用於偵錯的檔案系統資料夾位置。 如果目錄沒有 <code>exists</code>，不會產生任何偵錯傾印。</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
