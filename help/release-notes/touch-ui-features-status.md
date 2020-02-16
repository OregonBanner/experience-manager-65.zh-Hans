---
title: 触控UI功能状态
description: 特定于Adobe Experience Manager触屏优化UI的发行说明。
uuid: ceb081cc-7c33-4408-8032-3ac83d461268
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: f736581d-e6ea-4ec8-bfc7-16b9aa592097
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# 触控UI功能状态{#touch-ui-feature-status}

>[!CAUTION]
>
>[经典UI自AEM 6](../release-notes/deprecated-removed-features.md) .4起已弃用。Adobe不打算对经典UI进行进一步的增强，并鼓励用户利用触屏优化UI中提供的强大新功能。

从6.0版开始，AEM引入了称为“触屏优化UI”（也称为“触屏优化UI”）的新用户界面，该界面符合Adobe Marketing Cloud和Adobe整体用户界面准则。 在几乎达到功能对等性的情况下，这已成为AEM中的标准UI，该UI具有传统的、面向桌面的界面，称为“经典UI”。

虽然触屏优化UI中提供了大多数功能，但仍有一些功能尚未完整，并且将在将来的发行版中添加。

以下列表显示了在AEM 6.5中实现的功能的当前状态。

有关升级到AEM 6.5的客户的建议，请参阅客户 [的用户界面建议](/help/sites-deploying/ui-recommendations.md) ，了解详细信息。

>[!NOTE]
>
>请注意，本页仅包含经典UI的功能对等性。
>
>未列出经典UI中不存在的触屏优化UI所添加和特有的功能。

>[!NOTE]
>
>此列表力求完整，但不应视为详尽无遗。

## 图例 {#legend}

* **完成**:该功能在触屏优化UI中完全可用
* **主要**:该功能在触屏优化UI中大多可用。
* **缺失**:该功能在触屏优化UI中不存在，必须使用经典UI才能执行此操作。
* **已替换**:该功能被替换为新实现，其工作方式不同。
* **删除**:该功能在触屏优化UI中不再存在，将不会被替换。

## 功能状态：站点管理员 {#feature-status-sites-admin}

这是经典UI站点管理员( `/siteadmin`)拥有的功能和触屏优化UI()中的状态的列 `/sites.html`表。

<table>
 <tbody>
  <tr>
   <td><strong>功能<br /> </strong></td>
   <td><strong>状态<br /> </strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td>导航站点层次结构</td>
   <td>完成<br /> </td>
   <td>AEM 6.4引入了内容 <a href="/help/sites-authoring/basic-handling.md#content-tree">树视图</a>。</td>
  </tr>
  <tr>
   <td>启动工作流</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>创建新页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>创建新站点</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>创建新启动项</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>创建新Live Copy <br /> </td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>创建文件夹</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>显示发布状态</td>
   <td>完成</td>
   <td>从AEM 6.5开始，工作流状态显示在列表视图中</td>
  </tr>
  <tr>
   <td>搜索</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>复制／粘贴页面（复制）</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>移动页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>发布页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>无复制权限的发布页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>稍后发布</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>发布树</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>取消发布页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>取消发布页面（不具有复制权限）</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>稍后取消发布</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>锁定／解锁</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>查看／编辑属性</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>设置页面权限</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>版本历史</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>恢复版本</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>恢复树和恢复已删除的页面</td>
   <td>缺失</td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>显示旧版本与当前版本之间的差异<br /> </td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Live copy操作（滚出）</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>查看语言副本</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>查找并替换</td>
   <td>Missing<br /> </td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>通知收件箱（JCR事件）</td>
   <td>缺失</td>
   <td>使用经典UI。 将替换为不同的实现。</td>
  </tr>
  <tr>
   <td>引用</td>
   <td>完成</td>
   <td>显示添加到AEM 6.5的传入页面链接。<br /> </td>
  </tr>
 </tbody>
</table>

## 功能状态：页面编辑器 {#feature-status-page-editor}

这是经典UI页面编辑器( `/cf#`)所具有的功能和触屏启用( `/editor.html`)中的状态列表。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>状态</strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td>编辑网页</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑移动网页<br /> </td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑通过设计导入程序导入的内容<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑电子邮件</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑混合移动应用程序</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑表单</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑选件</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑工作流模型<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>代码：编辑和预览</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>响应式预览<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>模式：编辑设计</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>模式：基架</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>模式：Live copy状态<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>添加注释</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>编辑属性<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>转出页面</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>开始和显示工作流</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流包处理</td>
   <td>大多数</td>
   <td>在触屏优化UI中完全可访问。 在经典UI中仍显示多个工作流有效负荷。<br /> </td>
  </tr>
  <tr>
   <td>锁定／解锁页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>发布页面 <br /> </td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>取消发布页面</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>复制页面</td>
   <td>已删除<br /> </td>
   <td>使用站点管理员复 <a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">制页面</a>。<br /> </td>
  </tr>
  <tr>
   <td>移动页面</td>
   <td>已删除</td>
   <td>使用站点管理 <a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">员移动页面</a>。<br /> </td>
  </tr>
  <tr>
   <td>删除页面</td>
   <td>已删除</td>
   <td>使用站点管理员 <a href="/help/sites-authoring/managing-pages.md#deleting-a-page">删除页面</a>。<br /> </td>
  </tr>
  <tr>
   <td>显示引用</td>
   <td>已删除</td>
   <td>使用站点管理 <a href="/help/sites-authoring/author-environment-tools.md#references">员查看详细的参考列表</a>。<br /> </td>
  </tr>
  <tr>
   <td>审查日志</td>
   <td>已删除</td>
   <td>使用站点管理员并 <a href="/help/sites-authoring/author-environment-tools.md#events-timeline">打开活动边栏</a>。<br /> </td>
  </tr>
  <tr>
   <td>创建版本</td>
   <td>已删除</td>
   <td>使用站点管理 <a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">员创建新版本</a>。<br /> </td>
  </tr>
  <tr>
   <td>恢复版本</td>
   <td>已删除</td>
   <td>使用站点管理员恢 <a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">复版本</a>。</td>
  </tr>
  <tr>
   <td>切换启动项</td>
   <td>已删除</td>
   <td>使用站点管理员在 <a href="/help/sites-authoring/launches-promoting.md">启动项之间切换</a>。<br /> </td>
  </tr>
  <tr>
   <td>翻译页面</td>
   <td>已删除</td>
   <td>使用站点管理员 <a href="/help/sites-administering/tc-manage.md">向翻译项目添加页面</a>。<br /> </td>
  </tr>
  <tr>
   <td>时间扭曲（选择日期／时间，浏览站点，然后查看）<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>设置权限</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>Client Context UI<br /> </td>
   <td>已更换</td>
   <td>以后 <a href="/help/sites-authoring/ch-previewing.md">使用ContextHub</a> UI。</td>
  </tr>
  <tr>
   <td>适用于各种媒体类型的内容查找器<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>组件列表</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>复制和粘贴组件<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>剪贴板中的组件列表</td>
   <td>缺失</td>
   <td> </td>
  </tr>
  <tr>
   <td>撤消／重做</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>将内容拖放到组件占位符中</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>使用组件自动创建将内容直接拖放到parsys占位符中<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 功能状态：文本、表和图像编辑器 {#feature-status-text-table-and-image-editors}

这是经典UI文本、表和图像编辑器具有的功能以及触屏优化UI中的状态列表。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>状态 </strong></td>
   <td><strong>注释<br /> </strong></td>
  </tr>
  <tr>
   <td>富文本编辑器</td>
   <td>完成</td>
   <td>可用于就地、对话框和全屏。</td>
  </tr>
  <tr>
   <td>启用／禁用RTE插件</td>
   <td>完成<br /> </td>
   <td>可以使用模板编辑 <a href="/help/sites-authoring/templates.md">器完成</a>。</td>
  </tr>
  <tr>
   <td>将RTE用于纯文本</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：链接和锚点</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：字符映射</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：复制／粘贴</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：从Microsoft word粘贴<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：查找和替换</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：文本格式（粗体， ...）</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：子标和上标</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：两端对齐</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：列表（项目符号／编号）</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：段落格式</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：文本样式</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：源代码编辑器（编辑HTML）<br /> </td>
   <td>完成<br /> </td>
   <td>仅在对话框和全屏中可用。<br /> </td>
  </tr>
  <tr>
   <td>RTE插件：拼写检查器</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：表（嵌入式表编辑器）</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：撤消／重做<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTE插件：允许内嵌图像</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>表编辑器</td>
   <td>完成</td>
   <td>可用于就地、对话框和全屏。<br /> </td>
  </tr>
  <tr>
   <td>将图像拖放到表单元格中<br /> </td>
   <td>完成</td>
   <td>可用的联机</td>
  </tr>
  <tr>
   <td>图像编辑器<br /> </td>
   <td>完成</td>
   <td>可用于就地、对话框和全屏。<br /> </td>
  </tr>
  <tr>
   <td>启用／禁用IPE插件</td>
   <td>完成</td>
   <td>AEM 6.3在模板编辑器中引入 <a href="/help/sites-authoring/templates.md">了UI</a>。</td>
  </tr>
  <tr>
   <td>IPE插件：裁剪</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE插件：翻转</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE插件：撤消／重做</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE插件：图像映射</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE插件：旋转</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPE插件：缩放</td>
   <td>完成<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 功能状态：工具 {#feature-status-tools}

这是经典UI具有的各种工具以及触屏优化UI中的状态列表。

<table>
 <tbody>
  <tr>
   <td><strong>功能<br /> </strong></td>
   <td><strong>状态<br /> </strong></td>
   <td><strong>注释</strong></td>
  </tr>
  <tr>
   <td>任务管理</td>
   <td>已更换</td>
   <td>6.0引入了项 <a href="/help/sites-authoring/projects.md">目和任务</a>。<br /> </td>
  </tr>
  <tr>
   <td>工作流收件箱<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>页面模板配置工作流(<code>/etc/workflow/wcm/templates.html</code>)</td>
   <td>Missing<br /> </td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>标记管理员UI<br /> </td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>MSM/Blueprint控制中心</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>Blueprint Manager UI</td>
   <td>完成</td>
   <td> </td>
  </tr>
  <tr>
   <td>推出配置UI</td>
   <td>缺失</td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>用户、组和权限UI<br /> </td>
   <td>基本完成<br /> </td>
   <td>对于高级权限编辑，请使用经典UI。<br /> </td>
  </tr>
  <tr>
   <td>清除版本(<code>/etc/versioning/purge.html</code>)</td>
   <td>缺失</td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>外部链接检查程序 (<code>/etc/linkchecker.html</code>)</td>
   <td>缺失</td>
   <td>使用经典UI。<br /> </td>
  </tr>
  <tr>
   <td>批量编辑器(<code>/etc/importers/bulkeditor.html</code>)</td>
   <td>Missing<br /> </td>
   <td>使用经典UI。</td>
  </tr>
  <tr>
   <td>上传缩略图以添加或覆盖这些缩略图<br /> </td>
   <td>缺失</td>
   <td>使用经典UI。</td>
  </tr>
 </tbody>
</table>

