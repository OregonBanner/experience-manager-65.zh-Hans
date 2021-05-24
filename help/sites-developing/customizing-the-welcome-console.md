---
title: 自定义欢迎控制台（经典UI）
seo-title: 自定义欢迎控制台（经典UI）
description: “欢迎”控制台提供了指向AEM中各种控制台和功能的链接列表
seo-description: “欢迎”控制台提供了指向AEM中各种控制台和功能的链接列表
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 9%

---

# 自定义欢迎控制台（经典UI）{#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本页面介绍经典 UI。
>
>有关标准触屏UI的详细信息，请参阅[自定义控制台](/help/sites-developing/customizing-consoles-touch.md)。

“欢迎”控制台提供了指向AEM中各种控制台和功能的链接列表。

![cq_welcomscreen](assets/cq_welcomescreen.png)

可以配置可见的链接。 这可以为特定用户和/或组定义。 要执行的操作取决于目标类型（与所在控制台的部分相关）：

* [主控制台](#links-in-main-console-left-pane)  — 主控制台中的链接（左窗格）
* [资源、文档和参考、功能](#links-in-sidebar-right-pane)  — 侧栏（右窗格）中的链接

## 主控制台中的链接（左窗格）{#links-in-main-console-left-pane}

这列出了AEM的主要控制台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 配置主控制台链接是否可见{#configuring-whether-main-console-links-are-visible}

节点级别权限决定链接是否可见。 相关节点包括：

* **网站:** `/libs/wcm/core/content/siteadmin`

* **数字资产:** `/libs/wcm/core/content/damadmin`

* **社区：** `/libs/collab/core/content/admin`

* **营销活动:** `/libs/mcm/content/admin`

* **收件箱:** `/libs/cq/workflow/content/inbox`

* **用户:** `/libs/cq/security/content/admin`

* **工具:** `/libs/wcm/core/content/misc`

* **标记:** `/libs/cq/tagging/content/tagadmin`

例如：

* 要限制对&#x200B;**工具**&#x200B;的访问，请删除

   `/libs/wcm/core/content/misc`

有关如何设置所需权限的更多信息，请参阅[安全部分](/help/sites-administering/security.md)。

### 侧栏（右窗格）{#links-in-sidebar-right-pane}中的链接

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

这些链接基于存在&#x200B;*和*&#x200B;对以下路径下节点的读取访问：

`/libs/cq/core/content/welcome`

默认情况下，提供了三个部分（稍微间隔）：

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

#### 配置侧栏链接是否可见{#configuring-whether-sidebar-links-are-visible}

可以通过删除对表示链接的节点的读取访问权限来隐藏特定用户或组的链接。

* 资源 — 删除对以下项的访问权限：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 文档 — 删除对以下项的访问权限：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能 — 删除对以下项的访问：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 要删除指向&#x200B;**Reports**&#x200B;的链接，请删除

   `/libs/cq/core/content/welcome/resources/reports`

* 要删除指向&#x200B;**Packages**&#x200B;的链接，请删除

   `/libs/cq/core/content/welcome/features/packages`

有关如何设置所需权限的更多信息，请参阅[安全部分](/help/sites-administering/security.md)。

### 链路选择机制{#link-selection-mechanism}

在`/libs/cq/core/components/welcome/welcome.jsp`中，使用的是[ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)，它对具有以下属性的节点执行查询：

* `jcr:mixinTypes` 值：  `cq:Console`

>[!NOTE]
>
>执行以下查询以查看现有列表：
>
>* `select * from cq:Console`

>



当用户或组对具有mixin `cq:Console`的节点没有读取权限时，该节点不会通过`ConsoleUtil`搜索进行检索，因此它不会列在控制台中。

### 添加自定义项目{#adding-a-custom-item}

[链接选择机制](#link-selection-mechanism)可用于将您自己的自定义项目添加到链接列表。

通过将`cq:Console` mixin添加到小组件或资源，将自定义项目添加到列表中。 这可通过定义属性来完成：

* `jcr:mixinTypes` 值：  `cq:Console`
