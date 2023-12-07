---
title: Adobe分类
description: 了解如何使用“Adobe分类”将分类数据导出到Adobe Analytics。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Adobe分类{#adobe-classifications}

Adobe分类将分类数据导出到 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 按照预定方式。 导出器是 **com.adobe.cq.scheduled.exporter.Exporter**.

要配置此功能，请执行以下操作：

1. 使用 **导航**，选择 **工具**， **Cloud Service**，则 **旧版Cloud Service**.
1. 滚动到 **Adobe Analytics** 并选择 **显示配置**.
1. 单击 **[+]** Adobe Analytics配置旁边的链接。

1. 在 **创建框架** 对话框：

   * 指定&#x200B;**标题**。
   * （可选）您可以指定 **名称**，适用于在存储库中存储框架详细信息的节点。
   * 选择 **Adobe Analytics分类**

   然后单击 **创建**.

   ![“创建框架”对话框](assets/aa-25.png)

1. 此 **分类设置** 将打开对话框以进行编辑。

   ![“分类设置”对话框](assets/aa-classifications-settings.png)

   这些属性包括：

   | **字段** | **描述** |
   |---|---|
   | 启用 | 选择 **是** 以启用“Adobe分类”设置。 |
   | 发生冲突时覆盖 | 选择 **是** 覆盖所有数据冲突。 默认情况下，设置为 **否**. |
   | 删除已处理的项目 | 如果设置为 **是**，会在导出后删除已处理的节点。 默认为 **假**. |
   | 导出作业描述 | 输入Adobe分类作业的说明。 |
   | 通知电子邮件 | 输入Adobe分类通知的电子邮件地址。 |
   | 报表包 | 输入要为其运行导入作业的报表包。 |
   | 数据集 | 输入要为其运行导入作业的数据集关系ID。 |
   | 转换程序 | 从下拉菜单中，选择转换器实施。 |
   | 数据源 | 导航到数据容器的路径。 |
   | 导出时间表 | 选择导出计划。 默认每30分钟处理一次。 |

1. 单击 **确定** 以保存您的设置。

## 修改页面大小 {#modifying-page-size}

以页面形式处理记录。 默认情况下，“Adobe分类”会创建页面大小为1000的页面。

根据Adobe分类中的定义，页面最大大小可以是25000的，并且可以从Felix控制台进行修改。 在导出期间，“Adobe分类”会锁定源节点，以防止同时进行修改。 导出后、出错时或会话关闭时，节点会解锁。

要更改页面大小，请执行以下操作：

1. 导航到OSGI控制台，网址为 **https://&lt;host>：&lt;port>/system/console/configMgr** 并选择 **AdobeAEM分类导出程序**.

   ![aa-26](assets/aa-26.png)

1. 更新 **导出页面大小** 根据需要，然后单击 **保存**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>“Adobe分类”以前称为“SAINT导出器”。

导出器可以使用转换器将导出数据转换为特定格式。 对于“Adobe分类”，为子接口 `SAINTTransformer<String[]>` 提供了实施转换器接口的方法。 此接口用于将数据类型限制为 `String[]` SAINTAPI使用该标记来查找要选择的此类服务。

在默认实现SAINTDefaultTransformer中，导出程序源的子资源被视为记录，属性名称作为键，属性值作为值。 此 **键** 列自动添加为第一列 — 其值将是节点名称。 命名空间属性(包含 `:`)将被忽略。

*节点结构：*

* id分类 `nt:unstructured`

   * 1 `nt:unstructured`

      * 产品=我的产品名称（字符串）
      * 价格= 120.90（字符串）
      * 大小= M（字符串）
      * 颜色=黑色（字符串）
      * Color^Code = 101（字符串）

**SAINT标题和记录：**

| **键** | **产品** | **价格** | **大小** | **颜色** | **颜色^代码** |
|---|---|---|---|---|---|
| 1 | 我的产品名称 | 120.90 | M | black | 101 |

这些属性包括：

<table>
 <tbody>
  <tr>
   <td><strong>属性路径</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>转换程序</td>
   <td>SAINTTransformer实现的类名</td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td>通知电子邮件地址。</td>
  </tr>
  <tr>
   <td>报告包</td>
   <td>要为其运行导入作业的报表包ID。 </td>
  </tr>
  <tr>
   <td>数据集</td>
   <td>要为其运行导入作业的数据集关系ID。 </td>
  </tr>
  <tr>
   <td>说明</td>
   <td>作业描述。 <br /> </td>
  </tr>
  <tr>
   <td>覆盖</td>
   <td>用于覆盖数据冲突的标志。 默认为 <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>checkdivision</td>
   <td>用于检查报表包兼容性的标记。 默认为 <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>用于在导出后删除已处理节点的标志。 默认为 <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## 自动导出Adobe分类 {#automating-adobe-classifications-export}

您可以创建自己的工作流，以便任何新的导入都会启动该工作流，以在中创建适当且结构正确的数据 **/var/export/** 以便将其导出到“Adobe分类”。
