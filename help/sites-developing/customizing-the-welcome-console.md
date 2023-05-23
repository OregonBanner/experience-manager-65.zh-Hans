---
title: 自訂歡迎主控台（傳統UI）
seo-title: Customizing the Welcome Console (Classic UI)
description: 「歡迎」主控台提供AEM內各種主控台和功能的連結清單
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 8%

---

# 自訂歡迎主控台（傳統UI）{#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本頁面說明傳統UI。
>
>另請參閱 [自訂主控台](/help/sites-developing/customizing-consoles-touch.md) 標準觸控式UI的詳細資訊。

「歡迎」主控台提供AEM內各種主控台和功能的連結清單。

![cq_welcomescreen](assets/cq_welcomescreen.png)

您可以設定可見的連結。 這可為特定使用者和/或群組定義。 要採取的動作取決於目標型別（這與其所在的主控台區段相關）：

* [主要主控台](#links-in-main-console-left-pane)  — 主主控台中的連結（左窗格）
* [資源、檔案與參考資料、功能](#links-in-sidebar-right-pane)  — 側邊欄（右窗格）中的連結

## 主主控台中的連結（左窗格） {#links-in-main-console-left-pane}

這會列出AEM的主要主控台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 設定主控台連結是否可見 {#configuring-whether-main-console-links-are-visible}

節點層級的許可權會決定是否顯示連結。 有問題的節點為：

* **網站：** `/libs/wcm/core/content/siteadmin`

* **数字资产:** `/libs/wcm/core/content/damadmin`

* **社群：** `/libs/collab/core/content/admin`

* **行銷活動：** `/libs/mcm/content/admin`

* **收件匣：** `/libs/cq/workflow/content/inbox`

* **用户:** `/libs/cq/security/content/admin`

* **工具：** `/libs/wcm/core/content/misc`

* **標籤：** `/libs/cq/tagging/content/tagadmin`

例如：

* 若要限制存取 **工具**，移除的讀取存取權

   `/libs/wcm/core/content/misc`

請參閱 [安全性區段](/help/sites-administering/security.md) 有關如何設定所需許可權的詳細資訊。

### 側邊欄中的連結（右窗格） {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

這些連結的基礎是 *和* 下列路徑下的節點讀取存取權：

`/libs/cq/core/content/welcome`

預設提供三個區段（稍微相隔）：

<table>
 <tbody>
  <tr>
   <td><strong>资源</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Service</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> 工作流</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> 任务管理</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> 复制</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> 报表</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> 出版物</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> 手稿</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>檔案與參考資料</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 文档</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> 开发人员资源</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>功能</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> 包</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> 包共享</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> 聚类</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> 备份</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Web 控制台<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Web 控制台状态转储<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### 設定是否顯示側欄連結 {#configuring-whether-sidebar-links-are-visible}

您可以移除代表連結之節點的讀取存取許可權，以隱藏連結，不讓特定使用者或群組存取。

* 資源 — 移除對下列專案的存取權：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 檔案 — 移除對下列專案的存取權：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能 — 移除對下列專案的存取權：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 若要移除的連結 **報表**，移除的讀取存取權

   `/libs/cq/core/content/welcome/resources/reports`

* 若要移除的連結 **套件**，移除的讀取存取權

   `/libs/cq/core/content/welcome/features/packages`

請參閱 [安全性區段](/help/sites-administering/security.md) 有關如何設定所需許可權的詳細資訊。

### 連結選擇機制 {#link-selection-mechanism}

在 `/libs/cq/core/components/welcome/welcome.jsp` 使用屬於 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)，會在具有屬性的節點上執行查詢：

* `jcr:mixinTypes` 值为: `cq:Console`

>[!NOTE]
>
>執行以下查詢以檢視現有清單：
>
>* `select * from cq:Console`
>


當使用者或群組沒有使用mixin的節點的讀取許可權時 `cq:Console`，不會擷取該節點 `ConsoleUtil` 搜尋，因此不會列在主控台上。

### 新增自訂專案 {#adding-a-custom-item}

此 [連結選擇機制](#link-selection-mechanism) 可將您自己的自訂專案新增至連結清單。

透過新增以下專案將您的自訂專案新增到清單 `cq:Console` mixin至您的widget或資源。 這可透過定義屬性來完成：

* `jcr:mixinTypes` 值为: `cq:Console`
