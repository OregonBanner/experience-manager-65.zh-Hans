---
title: Adobe分类
seo-title: Adobe分类
description: 了解Adobe分类。
seo-description: 了解Adobe分类。
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: 4456b5366387c27810c407d6ac9e6c17fc290269
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 5%

---


# Adobe分类{#adobe-classifications}

Adobe分类按计划将分类数据导出到[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。 导出器是&#x200B;**com.adobe.cq.scheduled.exporter.Exporter**&#x200B;的实现。

要配置此项，请执行以下操作：

1. 使用&#x200B;**导航**，选择&#x200B;**工具**、**Cloud Services**，然后选择&#x200B;**传统Cloud Services**。
1. 滚动到&#x200B;**Adobe Analytics**&#x200B;并选择&#x200B;**显示配置**。
1. 单击您的Adobe Analytics配置旁的&#x200B;**[+]**&#x200B;链接。

1. 在&#x200B;**创建框架**&#x200B;对话框中：

   * 指定&#x200B;**标题**。
   * 或者，您也可以为存储库中存储框架详细信息的节点指定&#x200B;**名称**。
   * 选择&#x200B;**Adobe Analytics分类**

   然后单击&#x200B;**创建**。

   ![“创建框架”对话框](assets/aa-25.png)

1. 将打开&#x200B;**分类设置**&#x200B;对话框进行编辑。

   ![“分类设置”对话框](assets/aa-classifications-settings.png)

   属性包括：

   | **字段** | **描述** |
   |---|---|
   | 启用 | 选择&#x200B;**是**&#x200B;以启用Adobe分类设置。 |
   | 发生冲突时覆盖 | 选择&#x200B;**是**&#x200B;以覆盖任何数据冲突。 默认情况下，此值设置为&#x200B;**否**。 |
   | 删除已处理的项目 | 如果设置为&#x200B;**Yes**，则在导出处理的节点后将其删除。 默认值为&#x200B;**False**。 |
   | 导出作业描述 | 输入Adobe分类作业的说明。 |
   | 通知电子邮件 | 输入Adobe分类通知的电子邮件地址。 |
   | 报表包 | 输入要为其运行导入作业的报表包。 |
   | 数据集 | 输入要运行其导入作业的数据集关系ID。 |
   | 转换程序 | 从下拉菜单中，选择变压器实现。 |
   | 数据源 | 导航到数据容器的路径。 |
   | 导出时间表 | 选择导出计划。 默认为每30分钟一次。 |

1. 单击&#x200B;**确定**&#x200B;以保存设置。

## 修改页面大小{#modifying-page-size}

记录在页面中处理。 默认情况下，Adobe分类创建页面大小为1000的页面。

页面在Adobe分类中的每个定义最大可为25000，并可从Felix控制台进行修改。 在导出过程中，Adobe分类会锁定源节点以防止并发修改。 导出后、出错时或会话关闭时，节点将解锁。

要更改页面大小：

1. 导航到位于&#x200B;**https://&lt;host>的OSGI控制台：&lt;port>/system/console/configMgr**，然后选择&#x200B;**AdobeAEM分类导出器**。

   ![aa-26](assets/aa-26.png)

1. 根据需要更新&#x200B;**导出页面大小**，然后单击&#x200B;**保存**。

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe分类以前称为SAINT导出器。

导出器可以使用转换器将导出数据转换为特定格式。 对于Adobe分类，已提供实现变压器接口的子接口`SAINTTransformer<String[]>`。 此接口用于将SAINTAPI使用的数据类型限制为`String[]`，并具有一个标记接口来查找此类服务以供选择。

在默认实现SAINTDefaultTransformer中，导出器源的子资源被视为属性名称作为键和属性值作为值的记录。 **键**&#x200B;列自动添加为第一列——其值将是节点名称。 将忽略命名空间属性（包含`:`）。

*节点结构：*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name（字符串）
      * 价格= 120.90（字符串）
      * 大小= M（字符串）
      * 颜色=黑色（字符串）
      * Color^Code = 101（字符串）

**SAINT标题和记录：**

| **键** | **产品** | **价格** | **大小** | **颜色** | **颜色代码** |
|---|---|---|---|---|---|
| 1 | 我的产品名称 | 120.90 | M | black | 101 |

属性包括：

<table>
 <tbody>
  <tr>
   <td><strong>属性路径</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>变压器</td>
   <td>SAINTransferm实现的类名</td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td>通知电子邮件地址。</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>要运行其导入作业的报表包ID。 </td>
  </tr>
  <tr>
   <td>数据集</td>
   <td>要运行其导入作业的数据集关系ID。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>作业描述。<br /> </td>
  </tr>
  <tr>
   <td>覆盖</td>
   <td>覆盖数据冲突的标志。 默认值为<strong>false</strong>。</td>
  </tr>
  <tr>
   <td>检查分支</td>
   <td>用于检查报表包的兼容性的标记。 默认值为<strong>true</strong>。</td>
  </tr>
  <tr>
   <td>已删除</td>
   <td>在导出后删除已处理节点的标记。 默认值为<strong>false</strong>。</td>
  </tr>
 </tbody>
</table>

## 自动Adobe分类导出{#automating-adobe-classifications-export}

您可以创建自己的工作流，以便任何新导入都启动工作流以在&#x200B;**/var/export/**&#x200B;中创建适当且结构正确的Adobe，以便将其导出到“数据分类”。
