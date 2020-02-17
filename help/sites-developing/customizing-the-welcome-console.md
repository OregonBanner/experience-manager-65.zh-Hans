---
title: 自定义欢迎控制台（经典UI）
seo-title: 自定义欢迎控制台（经典UI）
description: 欢迎控制台提供指向AEM中各控制台和功能的链接列表
seo-description: 欢迎控制台提供指向AEM中各控制台和功能的链接列表
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 自定义欢迎控制台（经典UI）{#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本页面介绍经典 UI。
>
>有关 [标准触屏优化UI的详细信息](/help/sites-developing/customizing-consoles-touch.md) ，请参阅自定义控制台。

欢迎控制台提供指向AEM中各种控制台和功能的链接列表。

![cq_welcomscreen](assets/cq_welcomescreen.png)

可以配置可见的链接。 可为特定用户和／或用户组定义。 要执行的操作取决于目标类型（这与所在控制台的部分相关）:

* [主控制台](#links-in-main-console-left-pane) -主控制台中的链接（左窗格）
* [资源、文档和参考、功能](#links-in-sidebar-right-pane) -提要栏（右侧窗格）中的链接

## 主控制台中的链接（左窗格） {#links-in-main-console-left-pane}

这将列出AEM的主要控制台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 配置主控制台链接是否可见 {#configuring-whether-main-console-links-are-visible}

节点级别权限决定链接是否可见。 相关节点包括：

* **网站:** `/libs/wcm/core/content/siteadmin`

* **数字资产:** `/libs/wcm/core/content/damadmin`

* **** 社区： `/libs/collab/core/content/admin`

* **营销活动:** `/libs/mcm/content/admin`

* **收件箱:** `/libs/cq/workflow/content/inbox`

* **用户:** `/libs/cq/security/content/admin`

* **工具:** `/libs/wcm/core/content/misc`

* **标记:** `/libs/cq/tagging/content/tagadmin`

例如：

* 要限制对工具的访 **问**，请从

   `/libs/wcm/core/content/misc`

有关如 [何设置所需权限的详细信息](/help/sites-administering/security.md) ，请参阅安全性部分。

### 提要栏中的链接（右侧窗格） {#links-in-sidebar-right-pane}

![cq_welcomencreensidebar](assets/cq_welcomescreensidebar.png)

这些链接基于对以下路径下 *的节点* ，以及对节点的读取访问：

`/libs/cq/core/content/welcome`

默认情况下，提供三个部分（稍微间隔）:

<table>
 <tbody>
  <tr>
   <td><strong>资源</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 云服务</td>
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
   <td> 报告</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> 发布内容</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> 手稿</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>文档和参考</strong></td>
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

#### 配置侧栏链接是否可见 {#configuring-whether-sidebar-links-are-visible}

通过删除对表示链接的节点的读取访问权限，可以从特定用户或用户组隐藏链接。

* 资源——删除对以下内容的访问权限：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 文档——删除对以下内容的访问权限：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能——删除对以下内容的访问：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 要删除指向“报告”的链 **接**，请从

   `/libs/cq/core/content/welcome/resources/reports`

* 要删除指向“包”的链 **接**，请从

   `/libs/cq/core/content/welcome/features/packages`

有关如 [何设置所需权限的详细信息](/help/sites-administering/security.md) ，请参阅安全性部分。

### 链接选择机制 {#link-selection-mechanism}

使 `/libs/cq/core/components/welcome/welcome.jsp` 用中由 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)组成，它对具有以下属性的节点执行查询：

* `jcr:mixinTypes` 值： `cq:Console`

>[!NOTE]
>
>执行以下查询以查看现有列表：
>
>* `select * from cq:Console`
>



当用户或用户组对包含混合的节点没有读取权限时 `cq:Console`，搜索将不检索该节点，因此该节点不会列在 `ConsoleUtil` 控制台中。

### 添加自定义项 {#adding-a-custom-item}

链 [接选择机制](#link-selection-mechanism) ，可用于将您自己的自定义项目添加到链接列表。

通过将混音添加到构件或资源，将自定 `cq:Console` 义项目添加到列表中。 这是通过定义属性来实现的：

* `jcr:mixinTypes` 值： `cq:Console`

