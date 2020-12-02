---
title: 触屏UI功能状态
description: 特定于 [!DNL Adobe Experience Manager] 触屏优化UI的发行说明。
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---


# 触屏UI功能状态{#touch-ui-feature-status}

从AEM 6.4开始[经典UI已弃用](../release-notes/deprecated-removed-features.md)。 Adobe不会进一步增强经典UI，并鼓励用户利用触屏优化UI中提供的强大新功能。

从6.0版开始，AEM引入了称为“触屏优化UI”（简称“触屏优化UI”）的新用户界面，该界面与[!DNL Adobe Experience Cloud]和整个Adobe用户界面指南保持一致。 在几乎达到功能对等性的情况下，它已成为AEM中的标准UI，具有传统的、面向桌面的界面，称为“经典UI”。

虽然触屏优化UI中提供的大多数功能尚未完整，并且将在未来版本中添加。

以下列表显示了AEM 6.5中实现的功能的当前状态。

有关升级到AEM 6.5的客户的建议，请参阅[客户的用户界面建议](/help/sites-deploying/ui-recommendations.md)。

>[!NOTE]
>
>本页仅涵盖与经典UI的功能对等性。 未列出触屏优化UI中不存在的添加到触屏优化UI的功能和该UI特有的功能。

>[!NOTE]
>
>本列表力求完整，但并非详尽无遗。

## 图例 {#legend}

* **完成**:该功能在触屏优化UI中完全可用。
* **主要**:该功能在触屏优化UI中大多可用。
* **缺失**:该功能在触屏优化UI中不存在，必须使用经典UI才能执行此操作。
* **已替换**:该功能被替换为新实现，其工作方式不同。
* **删除**:该功能在触屏优化UI中不再存在，将不会被替换。

## 功能状态：站点管理员{#feature-status-sites-admin}

这是经典UI站点管理员(`/siteadmin`)所具有的列表功能，以及触屏优化UI中的状态(`/sites.html`)。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 导航站点层次结构 | 完成 | AEM 6.4引入了[内容树视图](/help/sites-authoring/basic-handling.md#content-tree)。 |
| 启动工作流 | 完成 |  |
| 创建新页面 | 完成 |  |
| 创建新站点 | 完成 |  |
| 创建新启动项 | 完成 |  |
| 创建新Live Copy | 完成 |  |
| 创建文件夹 | 完成 |  |
| 显示发布状态 | 完成 | 从AEM 6.5开始，工作流状态显示在列表视图中。 |
| 搜索 | 完成 |  |
| 复制和粘贴页面(重复) | 完成 |  |
| 移动页面 | 完成 |  |
| 发布页面 | 完成 |  |
| 无复制权限的发布页面 | 完成 |  |
| 稍后发布 | 完成 |  |
| 发布树 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 取消发布页面（不具有复制权限） | 完成 |  |
| 稍后取消发布 | 完成 |  |
| 删除 | 完成 |  |
| 锁定／解锁 | 完成 |  |
| 视图/编辑属性 | 完成 |  |
| 设置页面权限 | 完成 |  |
| 版本历史记录 | 完成 |  |
| 恢复版本 | 完成 |  |
| 恢复树和恢复已删除的页面 | 缺失 | 使用经典UI。 |
| 显示旧版本与当前版本之间的差异 | 完成 |  |
| Live Copy操作（滚出） | 完成 |  |
| 查看语言副本 | 完成 |  |
| 查找和替换 | 缺失 | 使用经典UI。 |
| 通知收件箱(JCR事件) | 缺失 | 使用经典UI。 将替换为不同的实现。 |
| 引用 | 完成 | 显示添加到AEM 6.5的传入页面链接。 |

## 功能状态：页面编辑器{#feature-status-page-editor}

这是经典UI页面编辑器(`/cf#`)所具有的列表功能，以及触屏启用(`/editor.html`)的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 编辑网页 | 完成 |  |
| 编辑移动网页 | 完成 |  |
| 编辑通过设计导入程序导入的内容 | 完成 |  |
| 编辑电子邮件 | 完成 |  |
| 编辑混合移动应用程序 | 完成 |  |
| 编辑Forms | 完成 |  |
| 编辑优惠 | 完成 |  |
| 编辑工作流模型 | 完成 |  |
| 模式：编辑和预览 | 完成 |  |
| 响应式预览 | 完成 |  |
| 模式：编辑设计 | 完成 |  |
| 模式：基架 | 完成 |  |
| 模式：Live Copy状态 | 完成 |  |
| 添加注释 | 完成 |  |
| 编辑属性 | 完成 |  |
| 推广页 | 完成 |  |
| 开始和显示工作流 | 完成 |  |
| 工作流包处理 | 大多数 | 在触屏优化UI中完全可访问。 在经典UI中仍显示多个工作流有效负荷。 |
| 锁定／解锁页面 | 完成 |  |
| 发布页面 | 完成 |  |
| 取消发布页面 | 完成 |  |
| 复制页面 | 已删除 | 使用站点管理员复制页面[。](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page) |
| 移动页面 | 已删除 | 使用站点管理员移动页面[。](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page) |
| 删除页面 | 已删除 | 使用站点管理员删除页面[。](/help/sites-authoring/managing-pages.md#deleting-a-page) |
| 显示引用 | 已删除 | 使用站点管理员查看[详细参考列表](/help/sites-authoring/author-environment-tools.md#references)。 |
| 审查日志 | 已删除 | 使用站点管理员和[打开活动边栏](/help/sites-authoring/author-environment-tools.md#events-timeline)。 |
| 创建版本 | 已删除 | 使用站点管理员[创建新版本](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)。 |
| 恢复版本 | 已删除 | 使用站点管理员恢复版本[。](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version) |
| 切换启动项 | 已删除 | 使用站点管理员在启动项[之间切换。](/help/sites-authoring/launches-promoting.md) |
| 翻译页面 | 已删除 | 使用站点管理员将页面添加到翻译项目[。](/help/sites-administering/tc-manage.md) |
| 时间扭曲（选择日期／时间，浏览站点，视图而定） | 完成 |  |
| 设置权限 | 完成 |  |
| Client Context UI | 已替换 | 将使用[ContextHub](/help/sites-authoring/ch-previewing.md) UI。 |
| 各种媒体类型的内容查找器 | 完成 |  |
| 组件列表 | 完成 |  |
| 复制和粘贴组件 | 完成 |  |
| 剪贴板中的组件列表 | 缺失 |  |
| 撤消／重做 | 完成 |  |
| 将内容拖入组件占位符 | 完成 |  |
| 使用组件自动创建将内容直接拖到parsys占位符中 | 完成 |  |

## 功能状态：文本、表和图像编辑器{#feature-status-text-table-and-image-editors}

这是经典UI文本、表和图像编辑器的功能列表以及触屏优化UI中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 富文本编辑器 | 完成 | 可用于就地、对话和全屏。 |
| 启用／禁用RTE插件 | 完成 | 可以使用[模板编辑器](/help/sites-authoring/templates.md)完成。 |
| 将RTE用于纯文本 | 完成 |  |
| RTE插件：链接和锚点 | 完成 |  |
| RTE插件：字符映射 | 完成 |  |
| RTE插件：复制／粘贴 | 完成 |  |
| RTE插件：从Microsoft Word粘贴 | 完成 |  |
| RTE插件：查找和替换 | 完成 |  |
| RTE插件：文本格式（粗体， ...） | 完成 |  |
| RTE插件：子和上标 | 完成 |  |
| RTE插件：两端对齐 | 完成 |  |
| RTE插件：列表语（项目符号／数字） | 完成 |  |
| RTE插件：段落格式 | 完成 |  |
| RTE插件：文本样式 | 完成 |  |
| RTE插件：源代码编辑器（编辑HTML） | 完成 | 仅在对话框和全屏中可用。 |
| RTE插件：拼写检查器 | 完成 |  |
| RTE插件：表（嵌入式表编辑器） | 完成 |  |
| RTE插件：撤消／重做 | 完成 |  |
| RTE插件：允许联机图像 | 完成 |  |
| 表编辑器 | 完成 | 可用于就地、对话和全屏。 |
| 将图像拖入表单元格 | 完成 | 可用的联机 |
| 图像编辑器 | 完成 | 可用于就地、对话和全屏。 |
| 启用／禁用IPE插件 | 完成 | AEM 6.3在[模板编辑器](/help/sites-authoring/templates.md)中引入了UI。 |
| IPE插件：裁剪 | 完成 |  |
| IPE插件：翻转 | 完成 |  |
| IPE插件：撤消／重做 | 完成 |  |
| IPE插件：图像映射 | 完成 |  |
| IPE插件：旋转 | 完成 |  |
| IPE插件：缩放 | 完成 |  |

## 功能状态：工具{#feature-status-tools}

这是经典UI具有的各种工具的列表，以及触屏优化UI中的状态。

| 功能 | 状态 | 注释 |
|--- |--- |--- |
| 任务管理 | 已替换 | 6.0引入了项目和任务。 |
| 工作流收件箱 | 完成 |  |
| 页面模板配置的工作流(`/etc/workflow/wcm/templates.html`) | 缺失 | 使用经典UI。 |
| 标记管理员UI | 完成 |  |
| MSM/Blueprint Control Center | 完成 |  |
| Blueprint Manager UI | 完成 |  |
| 转出配置UI | 缺失 | 使用经典UI。 |
| 用户、组和权限UI | 基本完成 | 对于高级权限编辑，请使用经典UI。 |
| 清除版本(`/etc/versioning/purge.html`) | 缺失 | 使用经典UI。 |
| 外部链接检查程序 (`/etc/linkchecker.html`) | 缺失 | 使用经典UI。 |
| 批量编辑器(`/etc/importers/bulkeditor.html`) | 缺失 | 使用经典UI。 |
| 上传缩略图以添加或覆盖这些缩略图 | 缺失 | 使用经典UI。 |
