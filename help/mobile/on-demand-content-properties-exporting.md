---
title: 使用內容屬性匯出內容
seo-title: Using Content Properties to Export Content
description: 以下頁面顯示應用程式屬性和節點。
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# 使用內容屬性匯出內容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

應用程式表示為 *cq：Pages* 在AEM中。

它們共用在任何網站中找到的相同通用屬性 *cq：Page* 除了下面顯示的其他表示支援屬性的整合專案外。

## 应用程序属性 {#app-properties}

下表顯示 **應用程式屬性和節點**.

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>字串：路徑</td>
   <td><p>已設定的Mobile On-DemandCloud Service的路徑。 用於AEM Mobile以進行Mobile On-Demand動作（API叫用）</p> <p>作者選擇應用程式建立關聯的Mobile On-DemandCloud Service時，可透過「管理連線」圖磚設定此關聯。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字串：路徑</td>
   <td><p>應用程式的匯出設定路徑。 匯出設定是包含2個子ContentSync匯出設定範本的資料夾；</p> <p><i>dps-article</i>：用於匯出文章內容的ContentSync匯出設定</p> <p><i>dps-HTMLResources</i>：ContentSync匯出設定可匯出應用程式/文章共用資源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字符串</td>
   <td><p>此應用程式連結/繫結至Mobile On-Demand專案的ID/URI。</p> <p>作者從相關Mobile On-DemandCloud Service的可用專案清單中選擇專案時，可透過「管理連線」表徵圖設定此關聯。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>字符串</td>
   <td>應用程式標題。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>字符串</td>
   <td>内容类型.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日期</td>
   <td>共用資源上次從AEM上傳至AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String：userid</td>
   <td>執行上次從AEM將共用資源請求上傳至AEM Mobile的使用者ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字串：路徑</td>
   <td>儀表板設定的路徑。 路徑可視需要重新導向至自訂控制面板設定。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串：路徑</td>
   <td><p>為或延伸的cq：Component的路徑 <i>mobileapps/core/components/instance。</i></p> <p>這會提供應用程式目錄中的顯示和轉譯功能。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用 ***內容屬性*** 以建立內容。 請參閱下列資源，以建立和匯出文章和共用資源：

* [內容屬性](/help/mobile/content-properties.md)
* [建立文章匯出設定](/help/mobile/creating-article-export-configuration.md)
* [建立共用資源匯出設定](/help/mobile/creating-shared-resources-export-configuration.md)
