---
title: 将任务或表单另存为草稿
seo-title: Saving a task or form as a draft
description: 在AEM Forms应用程序中保存任务或表单的草稿副本的步骤
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 将任务或表单另存为草稿 {#saving-a-task-or-form-as-a-draft}

另存为草稿选项可保存任务或表单的快照以及在相关表单中填写的数据。 您也可以从模板创建草稿。 草稿将保存在移动设备中，并与Adobe Experience Manager Forms服务器同步，以供日后检索。

您可以 [更新表单](/help/forms/using/working-with-form.md)， [对其进行注释](/help/forms/using/add-attachments.md) 照片和涂鸦笔记。 在继续更新表单时，建议将其另存为草稿。 对于您决定稍后提交已填写表单的情况，将其另存为草稿会很有帮助。

要为表单门户上保存的表单启用另存为草稿功能，请参阅 [将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md).
要配置自适应表单的提交，请参阅 [草稿和提交组件](/help/forms/using/draft-submission-component.md). (对于与AEM Forms JEE服务器同步的表单无效。)

要创建草稿，请打开表单并点按 **另存为草稿** ![另存为草稿](assets/save-as-draft.png). 提供草稿的名称并点按 **保存**. 草稿将保存在“草稿”文件夹中，并与服务器同步。 如果应用程序处于离线状态，则该文件夹会保存在Outbox文件夹中。

如果以后更新相应的表单，更改会立即反映出来。 将AEM Forms应用程序与AEM Forms服务器同步时，草稿会上传到AEM Forms服务器。 此外，草稿会从“发件箱”移至“任务”或“草稿”文件夹。 其旁边会显示一个编辑图标。

当您继续处理多个任务和起点并保存它们时，草稿将被保存。 每次将应用程序与AEM Forms服务器同步时，草稿都会保存到服务器上。 它确保您随时可以根据上次保存的日期和时间恢复草稿。 例如，如果您重新安装应用程序或更改移动设备，则可以从服务器下载草稿。

## 删除草稿 {#delete-a-draft}

草稿文件夹列出了所有草稿。 您可以使用“删除草稿”选项从移动设备和服务器永久删除草稿。

删除从任务创建的草稿的选项不可用。 删除从任务创建的草稿时，任务将被放弃。

您可以在脱机模式和联机模式下放弃草稿。 在脱机模式下放弃草稿时，仅当与服务器的连接恢复时，草稿才会从服务器中删除。

执行以下步骤可删除草稿：

1. 在AEM Forms应用程序中，导航到 **Forms。**
1. 选择 **草稿** 从“搜索”旁边的下拉菜单中。
1. 带有编辑图标的表单 ![edit-draft-app](assets/edit-draft-app.png) 表示草稿。 点按草稿旁边的水平省略号。
1. 在点按水平省略号时显示的选项中，点按 **删除草稿**.
