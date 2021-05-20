---
title: 触屏 UI 功能状态
description: 特定于 [!DNL Adobe Experience Manager] 触屏UI的发行说明。
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# 触屏 UI 功能状态 {#touch-ui-feature-status}

从AEM 6.4开始[经典UI已弃用](../release-notes/deprecated-removed-features.md)。 Adobe不会进一步增强经典UI，同时鼓励用户利用触屏UI中提供的强大新功能。

从版本6.0开始， AEM引入了称为“触屏优化UI”（简称“触屏优化UI”）的新用户界面，该用户界面与[!DNL Adobe Experience Cloud]和整个Adobe用户界面指南保持一致。 在几乎实现了功能对等性的情况下，它已成为AEM中的标准UI，该界面采用了以桌面为导向的旧版界面，称为“经典UI”。

虽然触屏优化UI中存在大多数功能，但仍有一些功能尚未完整，且将在未来版本中添加。

以下列表显示了在AEM 6.5中实施的功能的当前状态。

有关升级到AEM 6.5的客户的建议，请参阅[客户的用户界面推荐](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>本页仅介绍与经典UI的功能对等性。 在触屏优化UI中添加的、唯一的、经典UI中不存在的功能未列出。

>[!NOTE]
>
>此列表力求完成，但并不详尽。

## 图例 {#legend}

* **完成**:该功能在触屏UI中完全可用。
* **主要**:该功能在触屏UI中大多可用。
* **缺少**:触屏优化UI中不存在该功能，必须使用经典UI才能执行此操作。
* **已替换**:该功能已被替换为新实施（其工作方式不同）。
* **已删除**:触屏优化UI中不再存在该功能，也不会被替换。

## 功能状态：站点管理员{#feature-status-sites-admin}

这是经典UI站点管理员(`/siteadmin`)具有的功能列表以及触屏UI(`/sites.html`)中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 导航网站层次结构 | 完成 | AEM 6.4引入了[内容树视图](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 启动工作流 | 完成 |  |
| 创建新页面 | 完成 |  |
| 创建新站点 | 完成 |  |
| 创建新启动项 | 完成 |  |
| 创建新Live Copy | 完成 |  |
| 创建文件夹 | 完成 |  |
| 显示发布状态 | 完成 | 从AEM 6.5开始，工作流状态显示在列表视图中。 |
| 搜索 | 完成 |  |
| 复制并粘贴页面（复制） | 完成 |  |
| 移动页面 | 完成 |  |
| 发布页面 | 完成 |  |
| 没有复制权限的发布页面 | 完成 |  |
| 稍后发布 | 完成 |  |
| 发布树 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 取消发布页面（不具有复制权限） | 完成 |  |
| 稍后取消发布 | 完成 |  |
| 删除 | 完成 |  |
| 锁定/解锁 | 完成 |  |
| 查看/编辑属性 | 完成 |  |
| 在页面上设置权限 | 完成 |  |
| 版本历史记录 | 完成 |  |
| 还原版本 | 完成 |  |
| 恢复树并恢复已删除的页面 | 缺少 | 使用经典UI。 |
| 显示旧版本与当前版本之间的差异 | 完成 |  |
| Live Copy操作（转出） | 完成 |  |
| 请参阅语言副本 | 完成 |  |
| 查找和替换 | 缺少 | 使用经典UI。 |
| 通知收件箱（JCR事件） | 缺少 | 使用经典UI。 将替换为不同的实施。 |
| 引用 | 完成 | 显示添加到AEM 6.5的传入页面链接。 |

## 功能状态：页面编辑器{#feature-status-page-editor}

这是经典UI页面编辑器(`/cf#`)具有的功能列表以及触屏优化(`/editor.html`)中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 编辑网页 | 完成 |  |
| 编辑移动网页 | 完成 |  |
| 编辑通过设计导入程序导入的内容 | 完成 |  |
| 编辑电子邮件 | 完成 |  |
| 编辑混合移动设备应用程序 | 完成 |  |
| 编辑Forms | 完成 |  |
| 编辑选件 | 完成 |  |
| 编辑工作流模型 | 完成 |  |
| 模式：编辑和预览 | 完成 |  |
| 响应式预览 | 完成 |  |
| 模式：编辑设计 | 完成 |  |
| 模式：基架 | 完成 |  |
| 模式：Live Copy状态 | 完成 |  |
| 添加注释 | 完成 |  |
| 编辑属性 | 完成 |  |
| 转出页面 | 完成 |  |
| 启动和显示工作流 | 完成 |  |
| 工作流包处理 | 大部分 | 在触屏UI中完全可访问。 经典UI中仍显示多个工作流有效负载。 |
| 锁定/解锁页面 | 完成 |  |
| 发布页面 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 复制页面 | 已删除 | 使用站点管理[复制页面](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)。 |
| 移动页面 | 已删除 | 使用站点管理[移动页面](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)。 |
| 删除页面 | 已删除 | 使用站点管理[删除页面](/help/sites-authoring/managing-pages.md#deleting-a-page)。 |
| 显示引用 | 已删除 | 使用站点管理员查看[详细引用列表](/help/sites-authoring/author-environment-tools.md#references)。 |
| 审查日志 | 已删除 | 使用站点管理和[打开活动边栏](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 创建版本 | 已删除 | 使用站点管理[创建新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)。 |
| 恢复版本 | 已删除 | 使用站点管理[恢复版本](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)。 |
| 切换启动项 | 已删除 | 使用站点管理员在启动项](/help/sites-authoring/launches-promoting.md)之间切换[。 |
| 翻译页面 | 已删除 | 使用站点管理[将页面添加到翻译项目](/help/sites-administering/tc-manage.md)。 |
| 时间扭曲（选择日期/时间，然后按照所查看的内容浏览网站） | 完成 |  |
| 设置权限 | 完成 |  |
| Client Context UI | 已更换 | 今后使用[ContextHub](/help/sites-authoring/ch-previewing.md) UI。 |
| 适用于各种媒体类型的内容查找器 | 完成 |  |
| 组件列表 | 完成 |  |
| 复制并粘贴组件 | 完成 |  |
| 剪贴板中的组件列表 | 缺少 |  |
| 撤消/重做 | 完成 |  |
| 将内容拖动到组件占位符 | 完成 |  |
| 通过组件自动创建，将内容直接拖到Parsys占位符中 | 完成 |  |

## 功能状态：文本、表和图像编辑器{#feature-status-text-table-and-image-editors}

这是经典UI文本、表和图像编辑器具有的功能列表以及触屏UI中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 富文本编辑器 | 完成 | 可用的就地、对话框和全屏。 |
| 启用/禁用RTE插件 | 完成 | 可以使用[模板编辑器](/help/sites-authoring/templates.md)完成。 |
| 对纯文本使用RTE | 完成 |  |
| RTE插件：链接和锚点 | 完成 |  |
| RTE插件：字符映射 | 完成 |  |
| RTE插件：复制/粘贴 | 完成 |  |
| RTE插件：从Microsoft Word粘贴 | 完成 |  |
| RTE插件：查找和替换 | 完成 |  |
| RTE插件：文本格式（粗体、...） | 完成 |  |
| RTE插件：子和上标 | 完成 |  |
| RTE插件：正文 | 完成 |  |
| RTE插件：列表（项目符号/数字） | 完成 |  |
| RTE插件：段落格式 | 完成 |  |
| RTE插件：文本样式 | 完成 |  |
| RTE插件：源代码编辑器（编辑HTML） | 完成 | 仅在对话框和全屏中可用。 |
| RTE插件：拼写检查程序 | 完成 |  |
| RTE插件：表（嵌入式表编辑器） | 完成 |  |
| RTE插件：撤消/重做 | 完成 |  |
| RTE插件：允许内嵌图像 | 完成 |  |
| 表编辑器 | 完成 | 可用的就地、对话框和全屏。 |
| 将图像拖入表格单元格 | 完成 | 可用内联 |
| 图像编辑器 | 完成 | 可用的就地、对话框和全屏。 |
| 启用/禁用IPE插件 | 完成 | AEM 6.3在[模板编辑器](/help/sites-authoring/templates.md)中引入了UI。 |
| IPE插件：裁切 | 完成 |  |
| IPE插件：翻转 | 完成 |  |
| IPE插件：撤消/重做 | 完成 |  |
| IPE插件：图像映射 | 完成 |  |
| IPE插件：旋转 | 完成 |  |
| IPE插件：缩放 | 完成 |  |

## 功能状态：工具{#feature-status-tools}

这是经典UI具有的各种工具列表以及触屏UI中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 任务管理 | 已更换 | 6.0引入了项目和任务。 |
| 工作流收件箱 | 完成 |  |
| 页面模板配置工作流(`/etc/workflow/wcm/templates.html`) | 缺少 | 使用经典UI。 |
| 标记管理员UI | 完成 |  |
| MSM/Blueprint控制中心 | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 转出配置UI | 缺少 | 使用经典UI。 |
| 用户、组和权限UI | 基本完成 | 要进行高级权限编辑，请使用经典UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 缺少 | 使用经典UI。 |
| 外部链接检查程序 (`/etc/linkchecker.html`) | 缺少 | 使用经典UI。 |
| 批量编辑器(`/etc/importers/bulkeditor.html`) | 缺少 | 使用经典UI。 |
| 上传缩略图以添加或覆盖这些缩略图 | 缺少 | 使用经典UI。 |
