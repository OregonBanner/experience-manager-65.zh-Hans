---
title: 批量导入和导出资产元数据。
description: 批量导入和导出数字资产的元数据。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2fd9a32396152eaf46e69c3141cbe1b6a69a3891

---


# 批量导入和导出资产元数据 {#import-and-export-asset-metadata-in-bulk}

[!DNL Adobe Experience Manager Assets] 允许您使用CSV文件批量导入资产元数据。 您可以通过导入CSV文件，对最近上传的资产或现有资产进行批量更新。 您还可以通过CSV格式从第三方系统批量摄取资产元数据。

## 导入元数据 {#import-metadata}

元数据导入是异步的，不会影响系统性能。 如果选中了工作流标志，则由于XMP写回活动，多个资产的元数据同步更新可能会占用大量资源。 在精益服务器使用期间计划此类导入，以便不影响其他用户的性能。

>[!NOTE]
>
>要在自定义命名空间上导入元数据，请首先注册命名空间。

1. 导航到用 [!DNL Assets] 户界面，然后单 **[!UICONTROL 击工]** 具栏中的创建。
1. 从菜单中，选择元 **[!UICONTROL 数据]**。
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. 选择包含元数据的 CSV 文件。
1. 指定以下参数：

   | 元数据导入参数 | 描述 |
   |:---|:---|
   | [!UICONTROL 批量大小] | 要为其导入元数据的批处理中的资产数。 默认值为 50。最大值为100。 |
   | [!UICONTROL 字段分隔符] | 默认值 `,` 为（逗号）。 您可以指定任何其他字符。 |
   | [!UICONTROL 多值分隔符] | 元数据值的分隔符。 默认值为 `|`. |
   | [!UICONTROL 启动工作流] | 默认为False。 当设置为 `true` 且默认的启动器设置对DAM元数 [!UICONTROL 据回写工作流(将元数据写入二进制XMP数据] )有效时。 启用启动工作流会减慢系统速度。 |
   | [!UICONTROL 资产路径列名称] | 定义包含资产的CSV文件的列名。 |

1. 点按／单 **[!UICONTROL 击工]** 具栏中的导入。 导入元数据后，通知会发送到您的通知收 [!UICONTROL 件箱] 。 导航到资产属性页，并验证是否为资产正确导入了元数据值。

要在导入元数据时添加日期和时间戳，请 `YYYY-MM-DDThh:mm:ss.fff-00:00` 使用日期和时间格式。 日期和时间以24小时 `T`格 `hh` 式的小时数分隔，以纳秒 `fff` 为单位，以及时 `-00:00` 区偏移。 例如， `2020-03-26T11:26:00.000-07:00` 2020年3月26日太平洋标准时间上午11点26分00秒。

>[!CAUTION]
>
>如果日期格式不匹配， `YYYY-MM-DDThh:mm:ss.fff-00:00`则不设置日期值。 导出的元数据CSV文件的日期格式为 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要导入它，请通过添加由表示的纳秒值将其转换为可接受的格式 `fff`。

## 导出元数据 {#export-metadata}

您可以以CSV格式导出多个资产的元数据。 元数据以异步方式导出，不会影响系统性能。 要导出元数据 [!DNL Experience Manager] ，请遍历资产节点及其子节点的 `jcr:content/metadata` 属性，并在CSV文件中导出元数据属性。

批量导出元数据的几个用例包括：

* 迁移资产时，将元数据导入第三方系统。
* 与更广泛的项目团队共享资产元数据。
* 测试或审核元数据以确保合规性。
* 将元数据外置以实现单独的本地化。

1. 选择包含要导出元数据的资产的资产文件夹。 从工具栏中，选择导 **[!UICONTROL 出元数据]**。

1. 在元数 [!UICONTROL 据导出] 对话框中，指定CSV文件的名称。 要导出子文件夹中资产的元数据，请选择“在子 **[!UICONTROL 文件夹中包含资产”]**。

   ![用于导出文件夹中所有资产的元数据的界面和选](assets/export_metadata_page.png "项用于导出文件夹中所有资产的元数据的界面和选项")

1. 选择所需选项。 提供文件名，并根据需要提供日期。

1. 在要导 **[!UICONTROL 出的属性字段中]** ，指定是要导出全部属性还是要导出特定属性。 如果选择要导出的选择性属性，请添加所需的属性。

1. 在工具栏中，单击“ **[!UICONTROL 导出]**”。 系统会显示一条消息，确认已导出元数据。 关闭消息。

1. 打开导出作业的收件箱通知。选择作业，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. 单击&#x200B;**[!UICONTROL 关闭]**。

   ![用于下载包含批量导出的元数据的CSV文件的对话框](assets/csv_download.png)

   *图： 用于下载包含批量导出的元数据的CSV文件的对话框。*

>[!MORELIKETHIS]
>
>* [在Experience Manager资产中导入和导出元数据](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

