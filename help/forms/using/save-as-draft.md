---
title: 将任务或表单另存为草稿
seo-title: 将任务或表单另存为草稿
description: 在AEM Forms应用程序中保存任务或表单的草稿副本的步骤
seo-description: 在AEM Forms应用程序中保存任务或表单的草稿副本的步骤
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 将任务或表单另存为草稿 {#saving-a-task-or-form-as-a-draft}

另存为草稿选项会保存任务或表单的快照以及在关联表单中填写的数据。 您还可以从模板创建草稿。 草稿保存在移动设备中，并与Adobe Experience Manager Forms服务器同步，以供以后检索。

您可以 [更新表单](/help/forms/using/working-with-form.md)，用照 [片对其添加注释](/help/forms/using/add-attachments.md) ，并可以涂写注释。 在您继续更新表单时，建议将其另存为草稿。 在您决定稍后提交已填写的表单的情况下，将其另存为草稿会很有帮助。

要为保存在表单门户上的表单启用另存为草稿功能，请参 [阅将HTML5表单另存为草稿](/help/forms/using/saving-html5-form-draft.md)。
要配置自适应表单的提交，请参阅草 [稿和提交组件](/help/forms/using/draft-submission-component.md)。 （对于与AEM Forms JEE服务器同步的表单无效。）

要创建草稿，请打开表单，然后点按另 **存为草稿**![另存为草稿](assets/save-as-draft.png)。 提供草稿的名称，然后点按保 **存**。 草稿将保存在“草稿”文件夹中，并与服务器同步。 如果应用程序处于脱机状态，则会将其保存在“发件箱”文件夹中。

如果您随后更新了相应的表单，更改会立即反映出来。 在将AEM Forms应用程序与AEM Forms服务器同步时，草稿将上传到AEM Forms服务器。 此外，草稿将从发件箱移至任务或草稿文件夹。 其旁边将显示一个编辑图标。

当您继续处理多个任务和开始点并保存它们时，草稿将保存。 每次您的应用程序与AEM Forms服务器同步时，草稿都会保存到服务器。 它确保您可以随时根据上次保存的日期和时间恢复草稿。 例如，如果您重新安装应用程序或更改移动设备，则可以从服务器下载草稿。

## 删除草稿 {#delete-a-draft}

草稿文件夹列表所有草稿。 您可以使用“删除草稿”选项从移动设备和服务器中永久删除草稿。

用于删除从任务创建的草稿的选项不可用。 删除从任务创建的草稿时，任务将被放弃。

您可以在脱机和联机模式下放弃草稿。 在脱机模式下放弃草稿时，仅当与服务器的连接恢复时，草稿才会从服务器中删除。

执行以下步骤以删除草稿：

1. 在AEM Forms应用程序中，导航到 **表单。**
1. 从“ **搜索** ”旁边的下拉菜单中选择“草稿”。
1. 带有编辑图标的表 ![单edit-draft-app表示草稿](assets/edit-draft-app.png) 。 点按草稿旁边的水平省略号。
1. 在点按水平省略号时显示的选项中，点按删除草 **稿**。
